---
title: Windows Search
date: 2026-09-07 08:34:00 +0700
categories: [Forensic, Windows, DFIR, ESEDatabase]
tags: [forensic, windows, esedatabase, searchindexer, propertystore]
media_subpath: /assets/img/2026-09-07-Windows_Search/
toc: true
comments: false
---
# Windows.edb

`C:\\ProgramData\\Microsoft\\Search\\Data\\Applications\\Windows\\Windows.edb`

Windows Search Indexer is a service that records information about files and data types in select directories and enables users to search for these files using the Start Menu and Windows Explorer.

`The important thing about Windows.edb is that it caches parts of PDF and TXT files, etc., for Windows Search.`

### Structure

Windows.edb contains several tables, three of which provide the most value to investigators:

#### **SystemIndex_Gthr**

This table contains metadata of every file and folder indexed by Search Indexer. Stroz Friedberg identified the following columns as those typically most useful to an investigator:

| **ScopeID** | An integer that can be used to determine the record’s parent folder. This ID is also referenced in the Scope column in the SystemIndex_GthrPth table. |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DocumentID** | An integer assigned to every file and folder. Assignment of this ID occurs sequentially as files are created. This ID is also referenced in the WorkID column in the SystemIndex_PropertyStore table. |
| **SDID** | A [Security Descriptor ID](https://learn.microsoft.com/en-us/windows/win32/secauthz/security-descriptor-definition-language) that contains information about file ownership and access control. |
| **LastModified** | Last modified timestamp of the record, stored in Windows File Time format.                                                                            |
| **FileName** | Name of the file or folder.                                                                                                                           |

#### **SystemIndex_GthrPth**

This table contains parent folders of the files indexed in the SystemIndex_Gthr table:

| **Scope** | An integer assigned to every folder. This can be correlated with ScopeID from SystemIndex_Gthr. |
|-------|-------------------------------------------------------------------------------------------------|
| **Parent** | The Scope of the record’s parent folder. This can be correlated with ScopeID from SystemIndex_Gthr. |
| **Name** | The name of the folder.                                                                         |

#### **SystemIndex_PropertyStore**

This table contains additional attributes about the indexed files and folders, including the following columns of interest:

| **WorkID** | An integer assigned to the record. Maps to DocumentID in SystemIndex_Gthr table. |
|--------|----------------------------------------------------------------------------------|
| **System_Search_GatherTime** | The time at which the record was indexed in the database, stored in Windows File Time format. |
| **System_Size** | The size of the file in bytes.                                                   |
| **System_ModifiedTime** | The $FN last modified time of the record, stored in Windows File Time format.    |
| **System_CreatedTime** | The $FN creation time of the record, stored in Windows File Time format.         |
| **System_FileOwner** | User who created the file, stored as username.                                   |
| **System_ItemPathDisplay** | Full path of the record.                                                         |
| **System_ItemType** | File type of the record based on the extension of the file. If a file does not have an extension, the value will be a single period ("."). |
| **System_FileAttributes** | [Windows file attributes](https://learn.microsoft.com/en-us/windows/win32/fileio/file-attribute-constants). |
| **System_Search_AutoSummary** | Partial contents of the file. Stroz Friedberg was unable to determine a consistent rule for how many bytes were recorded in this property in Windows 10. See further sections for more information on AutoSummary. |

The screenshot below illustrates a sample from the Windows 10 SystemIndex_PropertyStore table when viewed with [ESEDatabaseView](https://www.nirsoft.net/utils/ese_database_view.html). The highlighted record shows an example of a text file where partial content was indexed by the service.

![image.png](image.png)

However, when using ESEDatabaseView to read System_Search_AutoSummary, it will fail to read utf-16-le. Therefore, it's better to just use ESEDatabaseView. to find the WorkID and then dump the indexed file/folder in SystemIndex_PropertyStore using the script below.

```javascript
from dissect.esedb import EseDB

with open(r"D:\BKISC\Deleted\Windows.edb", "rb") as f:
    db = EseDB(f)
    table = db.table("SystemIndex_PropertyStore")
    
    # Tìm WorkID 2872 và print tất cả giá trị có data
    print("\n=== WorkID 2872 ===")
    for record in table.records():
        try:
            if record.get("WorkID") == 2872:
                for col in table.columns:
                    try:
                        val = record.get(col.name)
                        if val:
                            if isinstance(val, bytes):
                                decoded = val.decode("utf-16-le", errors="replace")
                                print(f"{col.name}: {decoded}")
                            else:
                                print(f"{col.name}: {val}")
                    except:
                        pass
        except:
            pass
```
