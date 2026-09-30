---
title: 使用JBoss EAP 8 (Linux)的AEM Forms 6.5 LTS上指令碼執行失敗
description: 在Linux環境中設定JBoss EAP 8.0時，執行Shell指令碼或啟動檔案時可能會遇到某些錯誤
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 4dfaa625-47fa-4681-9e2f-a3bbdca95276
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 1%
---
# 使用JBoss EAP 8 (Linux)的AEM Forms 6.5 LTS上指令碼執行失敗

## 問題

在&#x200B;**Linux**&#x200B;環境中設定&#x200B;**JBoss EAP 8.0 (AEM Forms 6.5.1 LTS)**&#x200B;時，執行Shell指令碼或啟動檔案時可能會遇到下列其中一個錯誤：

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

在&#x200B;**Windows**&#x200B;系統上建立或編輯Shell指令碼或組態檔，且包含&#x200B;**CRLF （歸位+換行）**&#x200B;行結尾時，就會發生這些錯誤。
Linux系統僅支援&#x200B;**LF （換行）**&#x200B;行結尾，而Windows樣式的行結尾會導致指令碼執行失敗。

## 適用於

* **JBoss EAP 8.0**
* **Linux / UNIX作業系統**

## 疑難排解步驟

1. **識別受影響的檔案**

   * 檢閱錯誤輸出以識別導致失敗的`.sh`指令碼或組態檔。

2. **將檔案轉換成Unix格式**

   * 使用`dos2unix`公用程式將Windows樣式的行尾轉換為Unix格式：

     ```bash
     dos2unix <file_name>
     ```

   * 將`<file_name>`取代為擲回錯誤的實際指令碼或設定檔。

3. **如有需要，請重複**

   * 如果多個指令碼受到影響，請針對所有相關的`.sh`檔案（例如安裝程式、LCM或JBoss啟動指令碼）重複轉換。

4. **重新執行指令碼**

   * 轉換後，重新執行指令碼以確認問題已解決。

將檔案轉換成Unix (LF)行結尾後，`/bin/sh^M`和`$'\r': command not found`錯誤已解決，JBoss指令碼在Linux上成功執行。
