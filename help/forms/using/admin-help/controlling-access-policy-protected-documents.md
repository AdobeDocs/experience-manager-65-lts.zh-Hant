---
title: 控制對受原則保護檔案的存取權
description: 瞭解如何檢視、管理及控制受原則保護檔案的存取權。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 553c0a95-26e9-4d2c-b53d-846861c6a1d7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# 控制對受原則保護檔案的存取權 {#controlling-access-to-policy-protected-documents}

您可以控制收件者使用受原則保護檔案的方式，無論受原則保護檔案的分佈範圍有多廣。

您可以使用「檔案」頁面執行下列工作：

* 搜尋並檢視受原則保護檔案的詳細資訊。 您可以檢視有關檔名稱、發行者名稱、原則名稱和套用原則的日期的資訊。 如果刪除了保護檔案的原則，您也可以在原則名稱下看到已刪除的原則ID。 使用者可以檢視和管理他們自己的受原則保護的檔案。 管理員可以檢視和管理所有受原則保護的檔案。
* 變更套用至檔案的原則詳細資訊。 使用者可以編輯他們自己的原則，管理員可以編輯共用和個人原則，原則集協調員可以在他們擁有許可權的原則集中編輯共用原則。 您可以直接從「檔案詳細資訊」頁面存取與檔案關聯的原則。
* 撤銷並恢復受原則保護檔案的存取權。 管理員可以撤銷並恢復任何檔案的存取權。 原則組協調員（有權管理檔案的人）可以從其原則組撤銷和恢復對使用共用原則的受原則保護檔案的存取權。 如果使用者已建立保護檔案的原則，或該原則是允許此功能的共用原則，則使用者可以撤銷對其受原則保護檔案的存取權。
* 切換套用至檔案的原則。 將原則套用至檔案的使用者，可以在建立原則或共用原則啟用此功能時切換原則。 原則組專員可以從其原則組切換原則。 管理員可以切換套用至任何檔案的原則。

當檔案受原則保護，而您撤銷存取許可權或切換套用的原則時，變更將生效，如下所示：

* 如果檔案線上上，除非使用者開啟檔案，否則會立即套用變更。 在這種情況下，使用者必須關閉檔案才能使變更生效。
* 如果收件者離線使用檔案（例如在筆記型電腦上），則變更會在下次收件者透過開啟任何受原則保護的檔案與Document Security同步時生效。

## 檢視檔案的相關資訊 {#view-information-about-a-document}

對於「檔案」頁面上列出的每個檔案，您可以看到檔名稱、發行者名稱、原則名稱以及檔案受保護日期。 如果保護檔案的原則已刪除，則原則ID會列在「原則名稱」下。

您也可以在「檔案詳細資訊」頁面上檢視有關特定檔案的更多詳細資訊（如下所述）：

>[!NOTE]
>
>使用[檔案詳細資訊]頁面上的[原則名稱]連結，存取在Microsoft Outlook中為附加至電子郵件訊息之檔案的收件者自動產生的原則。 這些原則不會出現在原則頁面上。

**檔名稱：**&#x200B;選取檔案的名稱。

**檔案識別碼：**&#x200B;當原則套用至檔案時，Document Security會指派的唯一識別碼。 document security會使用此編號來追蹤檔案。

**檔案狀態：**&#x200B;檔案的狀態（例如，使用中或撤銷）。

**發佈者：**&#x200B;附加原則至檔案的使用者名稱。

**原則名稱：**&#x200B;用來保護檔案的原則名稱。 您可以按一下名稱以開啟原則。 使用此連結來存取Acrobat為Outlook中附加至電子郵件訊息之檔案的收件者產生的原則。 這些原則不會顯示在「原則」頁面上。

**原則型別：**&#x200B;套用至檔案的原則型別。

**發佈日期：**&#x200B;將原則套用至檔案的日期。

**相關反複專案：**&#x200B;如果檔案有相關反複專案，此專案也會出現在清單中。 按一下連結可檢視檔案的相關版序清單。

使用者可以檢視有關受保護檔案的資訊。 管理員可檢視任何使用者已受原則保護之檔案的相關資訊。 原則組專員可檢視受原則保護之檔案的相關資訊，而不受其原則組的保護。

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。 「檔案詳細資訊」頁面隨即開啟，顯示有關檔案的詳細資訊。 此頁面也提供撤銷檔案存取權、切換原則以及檢視與此檔案相關之事件的選項。

## 檢視檔案的相關版序 {#view-related-iterations-for-a-document}

如果啟用了追蹤相關版序，您可以追蹤不同使用者已儲存的檔案版本。 只有某些應用程式支援此功能，例如PTC Pro/ENGINEER Wildfire。

當多位使用者共同作業並儲存同一份檔案的不同版本時，此功能相當實用。 document security可以追蹤各種版序；因此，您可以輕鬆檢視不同版本的檔案資訊。

如果啟用此功能，您可以從「檔案」頁面檢視檔案的相關版序。

1. 檢視檔案的檔案詳細資訊頁面。 （請參閱[檢視檔案](controlling-access-policy-protected-documents.md#view-information-about-a-document)的相關資訊。）
1. 按一下「檢視相關版序」。 只有在啟用特徵時，才能使用選項。 相關版序清單隨即顯示。 對於每個版序，您可以檢視下列資訊：

   * **反複專案：**&#x200B;檔案名稱。 檔案名稱可能與原始檔案名稱不同，其結尾會附加一個版本號碼。
   * **發行者：**&#x200B;原始檔案的發行者。
   * **建立者：**&#x200B;儲存反複專案的使用者。
   * **建立日期：**&#x200B;儲存反複專案的日期和時間。
   * **原則：**&#x200B;保護反複專案的原則。 不同的反複專案可能受不同的原則保護。

1. 若要顯示該版序的「檔案詳細資訊」頁面，請按一下版序的檔案名稱。

## 撤銷和恢復對檔案的存取權 {#revoking-and-reinstating-access-to-documents}

您可以撤銷並恢復受原則保護檔案的存取權：

**使用者：**&#x200B;可以撤銷或恢復使用個人原則或共用原則保護之檔案的存取權，這些原則為套用原則的使用者啟用撤銷功能。 無法撤銷檔案存取權或切換原則的使用者需要連絡管理員。

**管理員：**&#x200B;可以撤銷或恢復任何受原則保護檔案的存取許可權，包括受個人或共用原則保護的檔案。 如果管理員撤銷對受共用原則保護的檔案的存取權，則只有管理員可以恢復該檔案的存取許可權。

**原則組協調員：**&#x200B;可以撤銷或恢復原則組所保護之檔案的存取許可權。

當您撤銷或恢復檔案存取許可權時，變更會在下列時間生效：

* 如果檔案線上上並已關閉，則下次收件者透過開啟受原則保護的檔案與Document Security同步時，變更會生效。
* 如果檔案線上上且已開啟，則變更會在收件者關閉檔案時生效。
* 如果檔案是離線的（亦即，在沒有網際網路連線的情況下使用，例如在筆記型電腦上），則變更會在下次收件者與Document Security同步時生效。

**撤銷受原則保護檔案的存取權**

1. 在Document Security頁面上，按一下「檔案」。
1. 選取適當檔案旁的核取方塊，然後按一下撤銷。 您可以一次撤銷多個檔案的存取權。
1. 選取要在檔案撤銷後向嘗試開啟檔案的使用者顯示的訊息：

   * **一般訊息：**&#x200B;指出作者已撤銷檔案
   * **檔案已終止：**&#x200B;表示作者已終止檔案
   * **已修訂的檔案**：表示作者已修訂檔案

1. （選擇性）如果有較新版本的檔案可用，請輸入URL並按一下測試以驗證URL。
1. 按一下「確定」，然後再次按一下「確定」以返回「檔案」頁面。

**復原檔案存取許可權**

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下取消撤銷，然後按一下確定。

## 切換套用至檔案的原則 {#switch-a-policy-that-is-applied-to-a-document}

使用者、原則組專員和管理員可以切換套用到受原則保護檔案的原則（您一次只能套用一個原則到檔案）。 如果使用者已建立原則，或該原則是已啟用此功能之共用原則，則使用者可以切換套用至其受原則保護檔案的原則。 否則，管理員或原則集協調員必須切換原則。 管理員可以為任何使用者的受原則保護檔案切換原則。 原則組專員可以從其原則組切換原則。

當您切換原則時，新原則的強制如下：

* 如果檔案線上上並已關閉，則下次收件者透過線上上開啟任何受原則保護的檔案與Document Security同步時，變更會生效。
* 如果檔案線上上且已開啟，則變更會在使用者關閉檔案時生效。
* 如果檔案離線（在使用中而沒有使用中的網際網路或網路連線，例如在筆記型電腦上），則下次使用者透過線上上開啟受原則保護的檔案與Document Security同步時，將會套用變更。

>[!NOTE]
>
>若要允許匿名存取目前沒有此存取權的受原則保護檔案，請移除使用者端應用程式中的現有原則，然後套用允許匿名存取的原則。 如果您切換原則，使用者仍然必須登入才能存取檔案。

1. 在Document Security頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下「切換原則」。 最多會顯示100個原則的清單。
1. 如果未顯示您想要的原則，請從[尋找]清單中選取[原則名稱]或[原則ID]，輸入名稱或ID，然後按一下[尋找]。
1. 按一下清單中的新原則。
1. 按一下「切換原則」，然後按一下「確定」返回「檔案」頁面。

## 搜尋檔案 {#search-for-a-document}

您可以使用清單中可用的日期範圍條件與搜尋條件的組合，在「檔案」頁面上搜尋檔案。 這些條件包括檔名稱、原則名稱或所有檔案。

其他搜尋選項僅供管理員使用：

**檔案識別碼：** Document Security在套用原則時指派給檔案的唯一識別碼。

**檔名稱：**&#x200B;檔名稱。

**發行者名稱：**&#x200B;附加原則至檔案的使用者名稱。 您可以從所有網域或指定的網域中選取使用者。

**原則識別碼：**&#x200B;附加至檔案的原則識別碼。

**原則名稱：**&#x200B;附加至檔案的原則名稱。

**所有檔案：**&#x200B;所有受系統管理員和使用者保護的檔案。 使用「所有檔案」選項進行搜尋可能會傳回一長串檔案。

1. 在Document Security頁面上，按一下「檔案」。
1. 在「尋找」清單中，選取所需的搜尋條件。

   您可以將條件指定為檔案ID、檔名稱、發行者名稱、原則ID、原則名稱或所有檔案。

   如果您指定發行者名稱，請按一下[通訊錄]圖示，並指定您要搜尋使用者的網域，然後按一下[確定]返回[檔案]搜尋頁面。

1. （選用）在日期清單中，選取日期範圍選項。 如果您選取「自訂日期」 ，請在出現的方塊中以yyyy/mm/dd格式輸入日期，或使用日期選擇器指定日期範圍：

   * 按一下行事曆以開啟日期選擇器。
   * 使用箭頭來尋找年份和月份。
   * 按一下行事曆上當月某日。
   * 按一下「確定」以關閉「日期選擇器」。

1. 按一下「尋找」。

## 排序檔案清單 {#sort-the-document-list}

您可以依欄標題排序檔案清單。 欄標題旁邊的三角形圖示表示目前使用哪一欄來排序。 向上三角形表示遞增順序，而向下三角形表示遞減順序。

1. 在Document Security頁面上，按一下「檔案」。
1. 按一下適當的欄標題。
1. 若要變更排序順序，請再次按一下欄。

## 新增封面頁至受原則保護的檔案 {#add-cover-page-to-policy-protected-documents}

如果存在大多數非Adobe PDF檢視器，當您開啟受Document Security保護的檔案時，第一頁會顯示為空白頁面，或者應用程式會在不開啟檔案的情況下中止。

您可以使用「頁面0 （包裝函式檔案）」支援，讓非Adobe PDF檢視器開啟受保護的檔案並在檔案中顯示封面頁。

>[!NOTE]
>
>在Adobe Reader/Acrobat或Mobile Reader中檢視此類檔案（包含頁面0）時，受保護檔案會依預設開啟。

**若要將封面頁新增至受原則保護的檔案**

在Workbench中使用下列處理：

**保護
具有封面頁的檔案：**&#x200B;使用指定的原則保護PDF檔案的安全，並將封面頁新增至檔案

**擷取受保護的檔案：**&#x200B;從含有封面頁的PDF檔案擷取受原則保護的PDF檔案

使用下列Document Security API：

**protectDocumentWithCoverPage：**&#x200B;使用指定的原則保護指定PDF的安全，並傳回包含封面頁和受保護檔案作為附件的檔案
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument：**&#x200B;擷取封面檔案中所含受保護檔案的附件。 可以使用protectDocumentWithCoverPage方法建立具有封面頁的檔案
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
