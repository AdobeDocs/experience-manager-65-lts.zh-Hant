---
title: Acrobat Reader DC擴充功能使用的憑證型別
description: 瞭解Acrobat Reader DC擴充功能所使用的憑證型別。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ca919915-c37b-4793-b5e2-21a464c5dcdf
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 2%

---

# Acrobat Reader DC擴充功能使用的憑證型別 {#certificate-types-used-by-acrobat-reader-dc-extensions}

憑證檢視器提供下列憑證相關資訊：

* 憑證「易記」名稱
* 憑證設定檔
* 有效期限
* Acrobat Reader DC擴充功能使用許可權

## 憑證「易記」名稱 {#certificate-friendly-name}

Acrobat Reader DC擴充功能憑證的「易記」名稱是說明憑證屬性的字串，如下列範例所示：

是2D條碼完整生產V6.1 P8 0002054

字串包含以下元素：

**憑證型別：**&#x200B;說明憑證啟動的AEM表單模組，以及啟動等級，例如「ARE 2D條碼已滿」。 如需可用憑證型別的清單，請參閱憑證設定檔區段表格中的型別欄。

**部署型別：**&#x200B;表示憑證的預期用途，例如生產。 該值可以是「評估」或「生產」。 如需與每個憑證型別相關聯的部署型別清單，請參閱憑證設定檔區段表格中的部署型別欄。

**使用許可權版本：**&#x200B;說明憑證可以使用的使用許可權演演算法版本，例如V6.1。此版本不表示Acrobat或Acrobat Reader DC擴充功能的版本。

**設定檔代碼：**&#x200B;設定檔代碼是完整憑證屬性的簡短描述，例如P8。 如需與每種檔案型別相關聯的設定檔程式碼清單，請參閱「憑證設定檔」區段表格中的設定檔程式碼欄。

**序號：**&#x200B;將序號指派給Adobe發行的每個憑證，例如0002054。 Adobe企業支援或Adobe企業客戶代表可使用此序號，追蹤憑證至特定產品訂單或OEM關係。

## 憑證設定檔 {#certificate-profiles}

下表列出您在分析Acrobat Reader DC擴充功能憑證時可能會遇到的憑證設定檔。

<table>
 <thead>
  <tr>
   <th><p>設定檔代碼</p></th>
   <th><p>類型</p></th>
   <th><p>有效期限</p></th>
   <th><p>部署型別</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP生產</p></td>
   <td><p>最大</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP內部測試</p></td>
   <td><p>2年</p></td>
   <td><p>評估與測試</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC擴充功能，生產</p></td>
   <td><p>最大</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC擴充功能，Adobe內部使用</p></td>
   <td><p>2年</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC擴充功能，合作夥伴整合</p></td>
   <td><p>2年</p></td>
   <td><p>評估與測試</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC擴充功能，評估</p></td>
   <td><p>60 天</p></td>
   <td><p>評估</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms，生產</p></td>
   <td><p>最大</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x，生產</p></td>
   <td><p>最大</p></td>
   <td><p>生產</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms；可供OEM使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms；可供OEM使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>僅限簽章；可供OEM使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>僅限離線註解；OEM可使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>僅提供註解；可供OEM使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完整許可權；可供OEM使用</p></td>
   <td><p>最大</p></td>
   <td><p>生產與評估</p></td>
  </tr>
 </tbody>
</table>

## 有效期限 {#validity-period}

評估憑證會核發給客戶和開發人員，以便他們能夠評估並開發產品的範例應用程式。 這些憑證的有效期介於60到90天之間。 到期日是問題資料之後的第二個月。

合作夥伴整合憑證會核發給Adobe業務合作夥伴，以支援軟體開發、整合、建立原型和示範。 這些憑證的有效期為發行日期起兩年。

Adobe內部使用憑證用於Adobe，以支援軟體開發、整合、建立原型和示範。 這些憑證的有效期為發行日期起兩年。

生產憑證會核發給購買Acrobat Reader DC擴充功能的客戶。 這些憑證在憑證授權單位(CA)所允許的最大期間內有效，在「憑證設定檔」表格中顯示為&#x200B;*Max*。

## Acrobat Reader DC擴充功能使用許可權 {#acrobat-reader-dc-extensions-usage-rights}

當您在Certificate Viewer中檢查Acrobat Reader DC擴充功能憑證時，可以從「詳細資訊」標籤（如果已設定）選取使用許可權專案，以檢視憑證可啟用的Adobe Reader使用許可權詳細清單。 在特定檔案上啟用的使用許可權可以是憑證啟用的使用許可權的子集。

如果在非合作環境中需要線上註解，請聯絡Adobe支援以取得更多資訊。 Mode屬性符合部署型別，且是&#x200B;*生產*&#x200B;或&#x200B;*評估*。

允許的Acrobat Reader DC擴充功能使用許可權包含一或多個特定元素。 這些元素會用於不同的組合，以實現各種授權產品功能。

<table>
 <thead>
  <tr>
   <th><p>使用許可權元素</p></th>
   <th><p>Adobe Reader在檢視啟用許可權的PDF檔案時啟用的功能</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>填寫表單欄位並在本機儲存檔案。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>將表單資料匯入和匯出為FDF、XFDF、XML和XDP檔案。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>新增、變更或刪除PDF表單上的欄位和欄位屬性。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>當資料不在瀏覽器工作階段中執行時，透過電子郵件或離線方式將其提交至伺服器。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>從相同PDF表單中的範本頁面建立頁面。</p></td>
  </tr>
  <tr>
   <td><p>簽署</p></td>
   <td><p>以數位方式簽署和儲存PDF檔案，並清除數位簽章。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>建立和修改檔案註釋，例如註解。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>將註解（例如註釋）儲存在單獨的資料檔案中，並從檔案載入註釋。</p></td>
  </tr>
  <tr>
   <td><p>條碼純文字</p></td>
   <td><p>列印檔案時，檔案內含以未加密形式標示的表單資料，不需要授權伺服器軟體即可解碼。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>從線上檔案檢閱和註解伺服器上傳及下載註解，例如註解。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>連線至PDF表單中定義的Web服務或資料庫。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>修改與PDF檔案關聯的內嵌檔案物件。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC擴充功能使用許可權只能從Adobe以搭配使用的特定組合授權。 無法單獨授權這些功能。 如需使用許可權可用組合的詳細資訊，請聯絡AEM表單客戶代表。
