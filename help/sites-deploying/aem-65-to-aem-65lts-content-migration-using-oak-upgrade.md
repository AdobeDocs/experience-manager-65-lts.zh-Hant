---
title: 使用Oak將AEM 6.5移轉至AEM 6.5 LTS內容 — 升級
description: 瞭解如何使用Oak升級工具將內容從AEM 6.5移轉至AEM 6.5 LTS
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: a85b54d5a7c3b00f95f439941a390dcfee883187
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# 使用Oak將AEM 6.5移轉至AEM 6.5 LTS內容 — 升級 {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

本檔案說明如何將Adobe Experience Manager從&#x200B;**6.5**&#x200B;升級為&#x200B;**6.5 LTS**，並著重於移轉內容存放庫。 內容包括使用Oak-upgrade工具，以精確和控制方式在存放庫之間傳輸內容。

## 先決條件 {#prerequisites}

開始移轉之前，請確定已符合下列需求：

1. Java相容性：必須安裝並設定AEM 6.5 LTS，才能與Java™ 17一起執行。 設定後，請啟動AEM執行個體，確認所有套件組合皆有效且執行中沒有任何問題
1. 系統資源：確保有足夠的磁碟空間和記憶體可在移轉過程中處理這兩個存放庫
1. Oak-upgrade工具：從`oak-upgrade`官方Maven存放庫[下載](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) jar。 確保版本符合AEM 6.5 LTS中使用的Oak核心版本。 Oak-upgrade工具會在Oracle® Java™ 11或更新版本上執行

## 移轉程式 {#step-by-step-migration-process}

### 停止AEM 6.5和AEM 6.5 LTS {#stopping-aem65-and-aem65lts}

在起始移轉之前，請停止AEM 6.5和AEM 6.5 LTS執行個體。 這麼做可確儲存放庫處於穩定狀態，在移轉期間不會發生額外的寫入。

### 備份AEM 6.5執行個體 {#backing-up-the-aem65-instance}

對您的AEM 6.5執行個體進行完整備份（如果尚未進行）。

### 使用Oak-upgrade工具移轉內容 {#using-the-oak-upgrade-tool-for-content-migration}

Oak-Upgrade工具會透過命令列執行，如下所示：

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

以下是必要的命令和選項：

**金鑰選項**

* `--include-paths`：指定要包含在移轉中的子樹狀結構。 如需命令使用方式的詳細資訊，請參閱此範例：

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`：從移轉中排除特定路徑。 使用此選項時請小心 — 如果路徑存在於目標系統上，則會將其移除。 如需命令使用方式的詳細資訊，請參閱此範例：

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`：依預設，Oak-upgrade只會移轉對二進位檔的參照，將實際檔案留在原始blob/資料存放區。 因此，新的存放庫仍然依賴二進位檔的來源存放區。 若要移轉二進位檔與存放庫內容，請使用`--copy-binaries`引數將所有二進位檔資料複製到新存放區，如下所示：

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### 移轉查核點 {#migratiing-checkpoints}

將舊的SegmentMK存放庫(Oak 1.6以前版本)移轉至新的SegmentMK (Oak版本大於或等於1.6版本)時，查核點也會一併移轉。 此程式避免在新存放庫上首次執行Oak時重新索引。 不過，在下列情況下不會移轉查核點：

1. 已指定自訂包含 — 、排除 — 或合併 — 路徑，或
1. 系統會參考複製二進位檔案。 未指定來源資料存放區，且兩個不同的查核點在相同路徑下包含不同的二進位檔案。

在第二個案例中，Oak-upgrade會傳送下列警告和中斷訊息：

```
Checkpoints are not copied, because no external datastore has been specified. This results in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

解決此問題最簡單的方法是在命令列選項（例如`--src-datastore`或`--src-s3datastore`）中指定來源資料存放區。

也可以忽略警告，但在此情況下，儲存庫在第一次啟動時已完全重新索引。 這可能是一個漫長的過程，尤其是對於大型執行個體而言。 在重新索引程式完成之前，存放庫無法使用。 使用`--skip-checkpoints`選項隱藏警告。

您也可以在啟動AEM之前使用[離線重新索引](/help/sites-deploying/offline-reindexing.md)離線重新索引存放庫，以避免在第一次啟動時完全重新索引。

如需Oak升級工具和進階使用方式的詳細資訊，請參閱[正式檔案](https://jackrabbit.apache.org/oak/docs/migration.html)。
