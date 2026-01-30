---
title: VSL2026-Accidental
date: 2026-01-25 08:13:00 +0700
categories: [CTF, Forensic, VSL2026]
tags: [forensic, memorydump] # TAG names should always be lowercase
media_subpath: /assets/img/2026-01-25-VSL2026_Accidental/
toc: true
comments: false
---
# Accidental

- Công cụ : FTK Imager, SQLite, virustotal
- Thông tin đề:

![image.png](image.png)

Đề cho ta một file challenge.E01, tiến hành mở bằng FTK. Dựa vào mô tả đề chúng ta biết được người dùng đã tải về và thực thi chương trình theo hướng dẫn, dẫn đến các tài liệu bị mã hóa, từ đó ta export ActivitiesCache.db để xem lịch sử hoạt động của người dùng

![image 1.png](image%201.png)

![image 2.png](image%202.png)

theo lịch sử thì người dùng đã thực thi file setup.exe Local\Temp có vẻ đáng ngờ, tiến hành export và kiểm tra bằng virustotal

![image 3.png](image%203.png)

virustotal báo đây là 1 trojan , khả năng cao chính là thứ đã mã hóa dữ liệu người dùng

![image 4.png](image%204.png)

kiểm tra hành động của file thì thấy nó có hành vi ofuscated files ⇒ chính là mã độc cần tìm, tiếp theo ta mở bằng IDA và dùng MCP để phân tích 

![image 5.png](image%205.png)

đây là pseudocode mã hóa của chương trình 

```bash
encryptFile(const char *filename) {
    HCRYPTKEY hKey = NULL;
    DWORD fileSize, encrypted_size;
    BYTE *buffer = NULL;
    HANDLE hInputFile, hOutputFile;
    
    // 1. Kiểm tra file đã mã hóa
    if (IsFileAlreadyEncrypted(filename))
        return FAIL;
    
    // 2. Chuẩn bị tên output file
    strcpy(outputName, filename);
    lastDot = strrchr(outputName, '.');
    if (lastDot)
        *lastDot = 0;
    strcat(outputName, ".vsl");  // Thêm extension
    
    // 3. Mở file input
    hInputFile = CreateFileA(filename,
        GENERIC_READ,
        FILE_SHARE_READ,
        NULL,
        OPEN_EXISTING,
        FILE_ATTRIBUTE_NORMAL | FILE_FLAG_SEQUENTIAL_SCAN,
        NULL);
    
    if (hInputFile == INVALID_HANDLE_VALUE)
        return FAIL;
    
    // 4. Lấy kích thước file
    fileSize = GetFileSize(hInputFile, NULL);
    DWORD chunkSize = min(fileSize, 0x80000);  // 512KB
    
    // 5. Lấy file timestamps
    GetFileTime(hInputFile, &creationTime, &lastAccessTime, &lastWriteTime);
    
    // 6. Chuẩn bị marker header
    BYTE marker[0x44];  // 68 bytes
    memcpy(marker, "CRYPT_V1", 8);
    *(DWORD*)(marker + 8) = fileSize;
    *(DWORD*)(marker + 12) = (fileSize > 0x80000) ? 2 : 1;
    *(FILETIME*)(marker + 16) = lastWriteTime;
    memcpy(marker + 24, lastDot, 32);  // Original extension
    
    // 7. Duplicate AES key
    CryptDuplicateKey(g_hAESKey, 0, 0, &hKey);
    
    // 8. Set cipher mode CBC (mode=2)
    DWORD mode = 2;
    CryptSetKeyParam(hKey, KP_MODE, (BYTE*)&mode, 0);
    
    // 9. Allocate buffer
    DWORD bufferSize = (chunkSize + 15) & 0xFFFFFFF0 + 32;
    buffer = HeapAlloc(GetProcessHeap(), 0, bufferSize);
    
    // 10. Mở file output
    hOutputFile = CreateFileA(outputName,
        GENERIC_WRITE,
        0,
        NULL,
        CREATE_ALWAYS,
        FILE_ATTRIBUTE_NORMAL | FILE_FLAG_SEQUENTIAL_SCAN,
        NULL);
    
    // 11. Mã hóa dữ liệu
    ReadFile(hInputFile, buffer, chunkSize, &bytesRead, NULL);
    
    DWORD encryptedSize = bytesRead;
    CryptEncrypt(hKey, NULL, TRUE, 0, buffer, &encryptedSize, bufferSize);
    
    // 12. Tính checksum
    DWORD checksum = CalculateChecksum(&marker, sizeof(marker));
    
    // 13. Ghi file output
    WriteFile(hOutputFile, &marker, 0x44, &bytesWritten, NULL);
    WriteFile(hOutputFile, buffer, encryptedSize, &bytesWritten, NULL);
    
    // 14. Nếu file lớn, mã hóa phần còn lại
    if (fileSize > 0x80000) {
        for (i = fileSize - chunkSize; i > 0; i -= bytesRead) {
            DWORD chunkToRead = min(i, 0x40000);
            ReadFile(hInputFile, buffer, chunkToRead, &bytesRead, NULL);
            WriteFile(hOutputFile, buffer, bytesRead, &bytesWritten, NULL);
        }
    }
    
    // 15. Cleanup
    CryptDestroyKey(hKey);
    CloseHandle(hInputFile);
    CloseHandle(hOutputFile);
    RtlSecureZeroMemory(buffer, bufferSize);
    HeapFree(GetProcessHeap(), 0, buffer);
    
    // 16. Xóa file gốc an toàn
    SecureDeleteFile(filename);
    
    return SUCCESS;

```

![image.png](09a43a38-c685-4ea6-913b-a837c1966539.png)

Để decrypt được thì chúng ta cần trích xuất các thông tin sau từ file image

```
 "ComputerName": "DESKTOP-8DLHUJ4",
    "UserName":     "employee",
    "UserSID":      "S-1-5-21-2194485576-443945188-1043422397-1001",
    "VolumeSerial": "E9F59FE0",  # Giá trị từ $Boot sector
    "MachineGUID":  "dca5645e-d0dc-4f10-ac03-59fe070380cd",
    "PersistPath":  r"C:\Users\employee\AppData\Local\Temp\WindowsSecurityService.exe"
```

dưới đây là script decode từ chat GPT =))

```bash
import hashlib
from Crypto.Cipher import AES
import struct
import os

# ============================================================
# CẤU HÌNH CHÍNH XÁC (Đã điền đầy đủ)
# ============================================================
info = {
    "ComputerName": "DESKTOP-8DLHUJ4",
    "UserName":     "employee",
    "UserSID":      "S-1-5-21-2194485576-443945188-1043422397-1001",
    "VolumeSerial": "E9F59FE0",  # Giá trị từ $Boot sector
    "MachineGUID":  "dca5645e-d0dc-4f10-ac03-59fe070380cd",
    "PersistPath":  r"C:\Users\employee\AppData\Local\Temp\WindowsSecurityService.exe"
}

# ============================================================
# LOGIC GIẢI MÃ
# ============================================================
def get_decryption_key(info):
    # Tạo chuỗi nguồn đúng định dạng của malware
    # Format: CompName|User|SID|VolSerial|GUID|MalwarePath
    raw_str = f"{info['ComputerName']}|{info['UserName']}|{info['UserSID']}|{info['VolumeSerial']}|{info['MachineGUID']}|{info['PersistPath']}"
    
    print(f"[+] Key String: {raw_str}")
    
    # Băm SHA-256
    sha256_hash = hashlib.sha256(raw_str.encode('ascii')).digest()
    
    # AES Key là 16 byte đầu tiên
    aes_key = sha256_hash[:16]
    print(f"[+] AES Key:    {aes_key.hex().upper()}")
    return aes_key

def decrypt_file(filepath):
    # Khóa giải mã
    key = get_decryption_key(info)
    
    if not os.path.exists(filepath):
        print(f"[-] Không tìm thấy file: {filepath}")
        return

    try:
        with open(filepath, "rb") as f:
            # 1. Đọc Header (68 bytes)
            header = f.read(68)
            
            # Kiểm tra Marker 'CRYPT_V1'
            if b"CRYPT_V1" not in header:
                print("[-] Lỗi: File không có Header CRYPT_V1 hợp lệ.")
                return

            # 2. Parse thông tin kích thước từ Header
            # Offset 16 (4 bytes): Kích thước file gốc
            original_size = struct.unpack('<I', header[16:20])[0]
            # Offset 20 (4 bytes): Kích thước phần bị mã hóa
            encrypted_len = struct.unpack('<I', header[20:24])[0]

            print(f"[*] Đang giải mã: {filepath}")
            print(f"    - Kích thước gốc: {original_size} bytes")
            print(f"    - Phần mã hóa:    {encrypted_len} bytes")

            # 3. Đọc dữ liệu
            encrypted_data = f.read(encrypted_len) # Phần đầu bị mã hóa
            plaintext_tail = f.read()              # Phần đuôi không bị mã hóa

        # 4. Giải mã AES-128 ECB
        cipher = AES.new(key, AES.MODE_ECB)
        decrypted_chunk = cipher.decrypt(encrypted_data)

        # 5. Ghép lại thành file hoàn chỉnh
        # Ghép phần đã giải mã + phần đuôi
        restored_data = decrypted_chunk + plaintext_tail
        
        # Cắt bỏ padding thừa (nếu có) để về đúng kích thước gốc
        final_data = restored_data[:original_size]

        # 6. Lưu file kết quả
        output_path = filepath.replace(".vsl", "")
        # Xử lý trường hợp tên file trùng lặp
        if os.path.exists(output_path):
             output_path += ".restored"
             
        with open(output_path, "wb") as f_out:
            f_out.write(final_data)
            
        print(f"[+] THÀNH CÔNG! File đã được khôi phục tại:\n    -> {output_path}")

    except Exception as e:
        print(f"[-] Có lỗi xảy ra: {e}")

# ============================================================
# CHẠY
# ============================================================
if __name__ == "__main__":
    # Thay đổi tên file dưới đây thành tên file flag của bạn
    # Ví dụ: flag.txt.vsl, TaiLieu.docx.vsl
    TARGET_FILE = "ProjectFinal.vsl" 
    
    decrypt_file(TARGET_FILE)
```

Tiến hành decrypt file mã hóa trong Document của người dùng 

![image 6.png](image%206.png)

check header của file ProjectFinal.restored thấy nó là file Zip cho nên mình đổi tên file lại và unzip

![image 7.png](image%207.png)

![image 8.png](image%208.png)

![image 9.png](image%209.png)