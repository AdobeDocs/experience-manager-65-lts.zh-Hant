---
title: 建立或設定watched資料夾
description: 瞭解如何建立或刪除watched資料夾，或修改現有watched資料夾的內容。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 8f52ec13-80a9-4b28-824f-0f09fb988529
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---

# 建立或設定watched資料夾 {#create-or-configure-a-watched-folder}

管理員可以設定網路資料夾，稱為&#x200B;*watched資料夾*，這樣當使用者將檔案(例如PDF檔案)放入watched資料夾時，就會啟動預先設定的作業並操控檔案。 執行指定的作業後，該作業會將修改的檔案儲存在指定的輸出資料夾中。 如需有關管理watched資料夾的詳細資訊，請參閱[管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)。

您可以使用watched資料夾使用者介面來：

* 建立watched資料夾
* 修改現有watched資料夾的內容
* 刪除watched資料夾

## 建立watched資料夾 {#create-a-watched-folder}

設定watched資料夾之前，請先確定下列事項：

* Watched資料夾是AEM表單的進階功能。 此功能需要AEM Forms附加元件套件才能運作。 確保已安裝並設定適當的AEM Forms附加元件套件。
* 您可以在共用存放區或本機存放區中建立watched資料夾。 確定設定為執行watched資料夾的AEM表單使用者擁有watched資料夾的讀寫許可權。
* 您可以使用服務、工作流程或指令碼，自動執行watched資料夾的作業。 確保對應的服務、工作流程或指令碼已建立並準備執行。 如需有關建立服務、工作流程及指令碼的資訊，請參閱[處理檔案的各種方法](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files)。
* Watched資料夾有各種屬性，請參閱[Watched資料夾屬性](watched-folder-in-aem-forms.md#watchedfolderproperties)。

執行以下步驟來建立watched資料夾：

1. 選取畫面左上角的&#x200B;**Adobe Experience Manager**&#x200B;圖示。
1. 選取&#x200B;**工具** > **Forms** > **設定Watched資料夾。**&#x200B;會顯示已設定的Watched資料夾清單。
1. 選取&#x200B;**新增**。 隨即顯示建立watched資料夾所需的欄位清單：

   * **名稱**：識別watched資料夾。 名稱只能使用英數字元。
   * **路徑**：指定watched資料夾位置。 在叢集環境中，此設定必須指向共用網路資料夾，在叢集的不同節點上執行AEM的每個使用者都可以存取該資料夾。
   * **處理檔案使用**：要啟動的處理程式的型別。 您可以指定工作流程、指令碼或服務。
   * **服務名稱/指令碼路徑/工作流程路徑**：欄位的行為是根據使用&#x200B;**欄位的**&#x200B;處理檔案所指定的值。 您可以指定下列值：

      * 針對「工作流程」，指定要執行的工作流程模型。 例如，/etc/workflow/models/&lt;workflow_name>/jcr：content/model
      * 在指令碼中，指定要執行的指令碼的JCR路徑。 例如， /etc/watchfolder/test/testScript.ecma
      * 針對服務，指定用於找到OSGi服務的篩選器。 此服務已註冊為com.adobe.aemfd.watchfolder.service.api.ContentProcessor Interface的實作。 例如，下列程式碼是使用自訂(foo=bar)屬性的ContentProcessor介面的自訂實作。

   >[!NOTE]
   >
   >如果您已針對&#x200B;**使用**&#x200B;欄位的「處理檔案」選取&#x200B;**服務**，則必須將「服務名稱」(inputProcessorType)欄位的值括在括弧中。 例如(foo=bar)。

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **輸出檔案模式**：指定watched資料夾用來判斷輸出檔案和資料夾之名稱與位置的模式清單(以分號(；)分隔)。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。

1. 選取&#x200B;**進階**。 進階標籤包含更多欄位。 這些欄位大多包含預設值。

   * **承載對應程式篩選器：**&#x200B;當您建立watched資料夾時，它會在被監視的資料夾中建立資料夾結構。 資料夾結構有階段、結果、保留、輸入和失敗資料夾。 資料夾結構可作為工作流程的輸入裝載，並接受來自工作流程的輸出。 也可以列出失敗點（如果有）。 承載的結構與watched資料夾的結構不同。 您可以撰寫自訂指令碼，將watched資料夾的結構對應至裝載。 此類指令碼稱為裝載對應程式篩選器。 提供兩種現成的裝載對應程式實作。 如果您沒有[自訂實作](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter)，請使用其中一個現成的實作：

      * **預設對應程式：**&#x200B;使用預設裝載對應程式，將watched資料夾的輸入和輸出內容保留在裝載中的個別輸入和輸出資料夾中。
      * **簡單檔案型裝載對應程式：**&#x200B;使用簡單檔案型裝載對應程式，將輸入和輸出內容直接保留在裝載資料夾中。 它不會建立任何額外的階層，像是預設的對應程式。

   * **執行模式**：指定工作流程執行所允許的執行模式清單（以逗號分隔）。
   * **在**&#x200B;之後逾時暫存的檔案：指定在已擷取處理之輸入檔案/資料夾被視為逾時並標籤為失敗前，要等候的秒數。 逾時機制只會在這個屬性的值為正數時啟動。
   * **節流時刪除逾時的階段檔案**：如果啟用，則只有在為watched資料夾開啟節流時，才會啟動&#x200B;**在**&#x200B;之後逾時的階段檔案機制。
   * **每隔以下時間掃描輸入資料夾：**&#x200B;指定掃描watched資料夾輸入的時間間隔（秒）。 除非啟用「節流」設定，否則輪詢「間隔」應比處理平均作業的時間長；否則，系統可能會超載。 間隔的值必須大於或等於1。
   * **排除檔案模式**：指定分號(；)分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的檔案和資料夾。 不會掃描任何具有指定模式的檔案或資料夾以進行處理。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **包含檔案模式**：指定以分號(；)分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的資料夾和檔案。 例如，如果「包含檔案模式」是input&amp;amp；ast；，則會擷取符合input&amp;amp；ast；的所有檔案和資料夾。 預設值為&amp;amp；ast；，表示所有檔案和資料夾。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。
   * **等待時間：**&#x200B;指定建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（毫秒）。 例如，如果等待時間為3,600,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 預設值為 0。

     此設定對於確保檔案或資料夾的所有內容都複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，且檔案下載需要10分鐘，請將等待時間設為10&amp;amp；ast；60&amp;amp；ast；1000毫秒。 此間隔可防止watched資料夾掃描未滿十分鐘的檔案。

   * **刪除早於下列時間的結果：**&#x200B;指定刪除早於指定值的檔案和資料夾前的等待時間（天數）。 此設定對於確保結果資料夾不會填滿非常有用。 值為–1天表示絕不刪除結果資料夾。 預設值為 -1。
   * **結果資料夾名稱：**&#x200B;指定要儲存結果的資料夾名稱。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理並儲存在失敗資料夾中。 您可以使用絕對或相對路徑配合下列檔案模式：

      * %F =檔案名稱前置詞
      * %E =副檔名
      * %Y =年（完整）
      * %y =年（最後兩位數）
      * %M =月
      * %D =日期
      * %d =一年中的第幾天
      * %H =小時（24小時時鐘）
      * %h =小時（12小時時鐘）
      * %m =分鐘
      * %s =秒
      * %l =毫秒
      * %R =隨機數字（介於0-9之間）
      * %P =處理程式或工作識別碼
      * 例如，如果是2009年7月17日晚上8點，而您指定C：/Test/WF0/failure/%Y/%M/%D/%H/，則結果資料夾為C：/Test/WF0/failure/2009/07/17/20。
      * 如果路徑不是絕對路徑而是相對路徑，則會在watched資料夾內建立資料夾。 預設值為result/%Y/%M/%D/，這是watched資料夾內的Result資料夾。 如需檔案模式的詳細資訊，請參閱[關於檔案模式](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns)。

   * **失敗資料夾名稱：**&#x200B;指定儲存失敗檔案的資料夾。 此位置永遠是相對於watched資料夾。 您可以使用檔案模式，如「結果資料夾」中所述。
   * **保留資料夾名稱：**&#x200B;指定成功掃描和擷取後儲存檔案的資料夾。 路徑可以是絕對、相對或Null目錄。 您可以使用檔案模式，如「結果資料夾」中所述。 預設值為preserve/%Y/%M/%D/。
   * **批次大小：**&#x200B;指定每次掃描要擷取的檔案或資料夾數目。 它可防止系統過載；一次掃描太多檔案可能會導致當機。 預設值為 2。

     如果掃描間隔很小，執行緒會經常掃描輸入資料夾。 如果檔案經常被拖放到watched資料夾中，則您應該將掃描間隔維持在較小的範圍內。 如果檔案不常捨棄，請使用較大的掃描間隔，讓其他服務可以使用執行緒。

   * **節流開啟：**&#x200B;啟用此選項時，它會限制AEM在任何指定時間處理之watched資料夾工作的數目。 「批次大小」值決定作業的最大數量。 如需詳細資訊，請參閱[節流](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **以類似名稱覆寫現有的檔案**：設定為True時，會覆寫結果資料夾和保留資料夾中的檔案。 設定為False時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為False。
   * **失敗時保留檔案：**&#x200B;設定為True時，如果發生失敗，則會保留輸入檔案。 預設值為true。
   * **包含具有模式的檔案：**&#x200B;指定分號(；)分隔的模式清單，Watched資料夾會使用這些模式來決定要掃描和擷取的資料夾和檔案。 例如，如果輸入「包含檔案模式」，則會擷取符合輸入的所有檔案和資料夾。 如需詳細資訊，請參閱[管理說明](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md)
   * **非同步叫用Watched資料夾：**&#x200B;將叫用型別識別為非同步或同步。 預設值為非同步。 建議將非同步處理用於長效處理作業，而建議將同步處理用於暫時性或短效處理作業。
   * **啟用Watched資料夾：**&#x200B;啟用此選項時，就會啟用Watched資料夾。 預設值為True。

## 修改現有watched資料夾的內容 {#modify-properties-of-an-existing-watched-folder}

除了變更watched資料夾的名稱之外，您還可以修改現有watched資料夾的所有屬性。 執行以下步驟來修改現有watched資料夾的內容：

1. 選取畫面左上角的&#x200B;**Adobe Experience Manager**&#x200B;圖示。
1. 選取&#x200B;**工具** > **Forms** > **設定Watched資料夾。**&#x200B;會顯示已設定的Watched資料夾清單。
1. 在Watched資料夾熒幕的左側，選取watchfolder並選取&#x200B;**編輯。**&#x200B;顯示建立watched資料夾所需的欄位清單。 **基本**&#x200B;索引標籤中列出的欄位是必要的。 進階標籤包含更多欄位。 這些欄位大多包含預設值。 您可以依需求修改這些屬性。
1. 修改屬性之後，請選取&#x200B;**更新**。 修改後的屬性會儲存。
