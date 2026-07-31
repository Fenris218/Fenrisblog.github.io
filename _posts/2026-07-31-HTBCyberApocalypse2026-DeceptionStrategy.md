---
title: HTBCyberApocalypse2026-DeceptionStrategy
date: 2026-07-31 09:05:58 +0700
categories: [CTF, Forensic, Windows, HTBCyberApocalypse2026]
tags: [forensic, malware, dllhijacking, rc4, wireshark, procmon, mitreattck]
media_subpath: /assets/img/2026-07-31-HTBCyberApocalypse2026_DeceptionStrategy/
toc: true
comments: false
---

## Mô tả : 
A trusted harbor-latch mechanism is behaving erratically, processing routine transit writs with a strange, stuttering cadence. Under the cover of this mechanical distraction, an unseen hand bypassed the inner witness-marks and completely drained an Eastreach private credit-cache. Sift through the compromised latch's residual ash-logs and custody chains to track the phantom access before the stolen coin vanishes into the undercity.
3 Files đính kèm :![IMG-20260731074918408.png](IMG-20260731074918408.png)



## Câu hỏi : 
### 1. What is the name of the process that originated the malicious behavior?
-> Discord 
### 2. What is the Unix epoch timestamp when the malicious module was loaded?
DLL malicious là d3d11.dll (sigcheck virustotal) 

![IMG-20260731080714642.png](IMG-20260731080714642.png)

Tìm trong procmon thấy PID 7664 load lúc 21:28:11 (UTC+7)=> đổi sang UTC => Epoch time
![IMG-20260731080917201.png](IMG-20260731080917201.png)
-> 1782570491
### 3. Which exported function of the malicious module was invoked later?
Use CFF explorer.exe
![IMG-20260731080956118.png](IMG-20260731080956118.png)
-> D3D11CreateDevice
### 4. What 16-byte registry value does the malware use to derive its RC4 key (00aa11bb...)?
Find in the procmon file after thời gian malicious module được load, nó lập tức truy vấn một registry value dài 16 byte
![IMG-20260731082346497.png](IMG-20260731082346497.png)

-> 1aa3a658ce2c4a4258983eba1853f08c

### 5. What is the name of the mutex created by the malware?
Unpack UPX rồi Rev malicious DLL, tìm chỗ gọi CreateMutexW
![IMG-20260731082813953.png](IMG-20260731082813953.png)
-> Local\DiscordRuntimeCache

### 6. What is the MITRE ATT&CK technique ID for the collection method?What is the MITRE ATT&CK technique ID for the collection method?
Virustotal
![IMG-20260731082907306.png](IMG-20260731082907306.png)
-> T1115

### 7. What is the IP address of the C2 server?
Filter wireshark ngay sau khoảng thời gian DLL malicious được load (14:28:11 UTC) thì ta thấy máy thực thi (IP: 192.168.239.131) giao tiếp với IP 203.49.53.184 qua HTTP với các nội dung bị mã hóa
![IMG-20260731084231109.png](IMG-20260731084231109.png)

-> 203.49.53.184

### 8. What is the crypto wallet seed phrase stolen by the malware?
payload exfiltration bằng RC4 với key `1aa3a658ce2c4a4258983eba1853f08c`  đã tìm được ở trên — nhưng **key phải dùng theo thứ tự byte đảo ngược (reversed)** so với thứ tự đọc được từ registry mới khớp (`8cf05318ba3e9858424a2cce58a6a31a`), sau đó decrypt RC4 với lần lượt các gói giao tiếp với C2
```
from hashlib import sha256

from Crypto.Cipher import ARC4  

key = bytes.fromhex("8cf05318ba3e9858424a2cce58a6a31a") 

cipher = ARC4.new(key)  

payloads = {

1: "a86a7e43122a5921b8cb98ce94df3030816c28ac861c214db9ed001510867b1c33d2d7eeaab63c2043fb4d5e4ea7db0ca6bb9d927967266b9e45724d0b0f72773f547b373920619d755db05dca5b4f57e43c6313a02b7fc89f52f298892dede5136213c16161ba70c294916fd68551470603490246be5dec564ed43a8d3bd5dca3712e3e7f3f084a75eea13c98e8cb4a0adb8b876a031e8552c8bc554886155c40ae2046d8430fd04680866aa2ae3e3756b8953e5bccebd3a391d4d7fa3d83ad23463c73695b10740c2d041684528d534a0dad6d76beca3cbcbd341ed2f263bae0b3ecb40a8aa208b28a8287ecd58e640e0a56e08d12b0fe123c26f9a096b6edb2011fbeeb3f2164f6cf91cc4ea158b0cfc1104a2d09c6d2a4ecc9c518a7157d98bd072878f9e01b9396b457d660e7388823cd690c2bf0b5eb37dd26439f8701f395511fc68fd8e43e1ee4317e31b7c59d73fa42616f4bea339f7b406669251a07ac68bd140bfc2d0a0a8ae1fd8284df4205f77cba49773945ae0a9895c5b2207496a51e245a2042a634be3d964efbf18a86b13ceee803744ad36430e97441df49ad3057a2d3b476826e776845062558ef550dd276489a6addb371a0ab911dc79b1c84abfdd1bed65ef73a81a3add651c0de6e8007c580f7bfa5b2d6e121d4e96de8e3f9a29105003f01c6270283e40c69a9",

2: "b46a3a52086f3833a2da90ce968c6f30916d25a69c01621bb9e40f1852c570533dd084bab0b66c2f4df65c5300b0d411eee8d5867a626865985d3b48451d6424704963216b2c77d27213a247cb1a491be435274ef4107bc4825cb7b79e61e0e30d2309da747fff67cfdb8776dd801d5b0d46521947b218b95249df3a8c26c1d1aa6522696425010e8cf4ef2b9df3cf0f0bdecefd2b0d159f4fcea71b4ed40e4740a07379ce4e06c34c82c970b9e7297851b3d4335198bbdda2c5d6daf829dae825412b2007091b6f1d2d360cc34f814b0f14af7b24ab8521bdf822fcdabc2ee8dbace7e05880a00af39d8a81a9c582644a4840e79d13e4bf5a212ff1bad5f7ecb00132a8e9282c64fec3c5c547ed50abc7dc040f2809ddd2a6e7d68c18b8176494ab4e3270f9e3528997e651d763be23832581655062c5afe927c72b00d1cf06ef95470cc08ad1f739f8b763672bb191b173ec15627d4ff7248832043268261a15ab7fe90e06ec68075e9ae5e58cc1d85f11f738ed4f772c41fa1bd09991df694d9aa50266413d49e27bba279a59fba58480b039a2e30f355cd27135bb744cde45ff3a58a2c7b344d169646a520f610ae55918d36b03f34c",

3: "89702a470975566fa1df868583c4696497662ced911a2f42a7e2121716da740126f0c5c283b4750e4dff78114cabc60cb7c9b19d503410438d551f470f2b2324245b653a463b72967212ec02a371",

4: "866831405a291038f6cb9ec594ce7f64c27028af9d1b6219b9f70a115e976b4f379495fbb0a1792f0cf8584549acd058fee980937c262c6b99593355004a6236225876297c69709a7e18a256a371",

}
for i, hexdata in payloads.items():

    cipher = ARC4.new(key)      # tạo mới cho từng payload

    plaintext = cipher.decrypt(bytes.fromhex(hexdata))

    print(plaintext.decode("utf-8", errors="replace"))

```

![IMG-20260731085724817.png](IMG-20260731085724817.png)
-> glow fix connect talon title risk barrel marine truth disease garbage cheese
