---
title: 為JEE上的AEM Forms記錄自訂元件API的交易。
description: 瞭解如何使用TransactionRecorder API來記錄自訂元件的交易。
feature: Transaction Reports
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
hide: true
hidefromtoc: true
exl-id: e2d1b548-ce30-471b-b01c-ce37b737aeb5
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# 為JEE上的AEM Forms記錄自訂元件API的交易 {#record-a-transaction-for-custom-components}

當您在自訂元件中使用可記帳API時，可以為元件啟用交易報告。 若要啟用交易報告，請修改元件的`component.xml`檔案，並在必須啟用交易報告的作業底下新增下列指定的標籤。

**標籤**： `<transaction-operation-type>CONVERT</transaction-operation-type> // Supported values are SUBMIT, CONVERT, RENDER.`

| 舊的作業標籤 | 新操作標籤 |
| ----------- | ----------- |
| `<operation>`<br> `<.... tags`<br>`<...>`<br>`<operation>` | `<operation>`<br> `<.... tags`<br>`<...>`<br>`<transaction-operation-type>CONVERT</transaction-operation-type`<br>`<operation>` |

如果您必須為API （例如批次API）擷取多個交易，其中交易計數會隨輸入計數而改變，請在API層級處理交易計數。

**若要記錄變動的交易計數：**

1. 在程式碼中匯入類別`"com.adobe.idp.dsc.InvocationContextStack"`。 此類別是`adobe-livecycle-client.jar` sdk檔案的一部分。 sdk檔案可在`<AEM_Forms_JEE_Install>\sdk\client-libs\common`取得

   >[!NOTE]
   > 如果您已在使用者端專案中套用檔案，請以新檔案更新上述共用的使用者端檔案。

1. 在必須記錄變動交易的API中：
   1. 新增邏輯，讓您可以將交易計數儲存在某個整數變數中，例如`transaction_count`。
   1. 作業成功時，新增`InvocationContextStack.recordTransactionCount(transaction_count)`。

<!--For example, you can set count for your custom component by importing class `"com.adobe.idp.dsc.InvocationContextStack"` in the code available at `adobe-livecycle-client.jar`  and determine the transaction count basis API input/result and add (In this case we add count is equal to 3):
`InvocationContextStack.recordTransactionCount(<count>).` to 
`InvocationContextStack.recordTransactionCount(3)`.-->

## 相關文章

* [在JEE上啟用和檢視AEM Forms的交易報告](/help/forms/using/transaction-report-overview-jee.md)
* [適用於AEM Forms on JEE的計費API清單](/help/forms/using/transaction-reports-billable-apis-jee.md)
