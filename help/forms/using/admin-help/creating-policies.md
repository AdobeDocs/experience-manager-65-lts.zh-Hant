---
title: 建立和管理原則
description: 原則是一組機密性設定，以及可存取套用該原則之檔案的使用者。 您可以使用AEM表單建立和管理各種型別的原則。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e8faf76e-5287-4b0c-b440-f348443287f3
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '4725'
ht-degree: 0%

---

# 建立和管理原則 {#creating-and-managing-policies}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

*原則*&#x200B;定義了一組機密性設定，以及可以存取套用原則之檔案的使用者。 *原則集*&#x200B;用於將具有共同業務目的的一組原則分組。 然後，這些原則集將可供系統中的部分使用者使用。 如需有關原則的詳細資訊，請參閱[原則及受原則保護的檔案](/help/forms/using/admin-help/document-security.md#policies-and-policy-protected-documents)。

## 原則型別 {#types-of-policies}

Document Security提供下列型別的原則。

**個人原則**

使用者可以透過適合特定情況的設定，建立、編輯、複製、刪除和套用他們自己的原則。 只有建立原則的人和管理員可以存取該個人原則。 個人原則會顯示在「原則」頁面的「我的原則」標籤上。

如果管理員啟用此權能，受邀使用者也可以建立、編輯、複製和刪除個人原則。

**共用原則**

管理員和原則組專員會根據貴組織針對不同型別檔案和使用者識別的機密性要求，建立共用原則。 共用原則包含於原則集中，並且可供特定原則集的所有授權使用者（檔案發佈者、原則集協調者和檔案收件者）使用。 管理員和原則組專員可以啟用和停用共用原則。 共用原則會顯示在「原則」頁面的「原則集」標籤上的原則集中。

當您第一次安裝Document Security時，它包含一個共用原則，名為&#x200B;*限制到所有主體*。 將此原則套用至檔案時，任何能登入Document Security的使用者都可以存取該檔案。 此原則位於名為&#x200B;*全域原則集*&#x200B;的原則集中。 預設不會啟用此原則。 如果符合貴組織的需求，則可將其啟用。

**Microsoft® Outlook自動產生的原則**

使用Acrobat，您可以將原則套用至您在Microsoft® Outlook中作為電子郵件附件傳送的檔案。 在Outlook中，您可以使用現有原則來保護檔案。 或者，您可以使用Acrobat透過預設機密性設定產生並套用至附加至電子郵件訊息之檔案的自動產生原則。 (請參閱&#x200B;*[Acrobat說明](https://help.adobe.com/en_US/acrobat/pro/using/index.html)*。)

>[!NOTE]
>
>若要讓原則可在Outlook中使用，您必須在Acrobat中將原則設定為我的最愛。 所有其他原則（包括您是發佈者的原則）不會顯示在Outlook中。

## 誰可以建立和管理原則與原則集 {#who-can-create-and-manage-policies-and-policy-sets}

您與原則和原則集互動的方式取決於您在組織內的角色：

**使用者：**&#x200B;使用者可以建立、編輯和刪除其個人原則。 如果管理員啟用此權能，受邀使用者也可以建立個人原則。

**原則組協調員：**&#x200B;原則組協調員可以在他們被指定為協調員的原則組內建立和管理共用原則。 原則集協調員通常是組織中的專家，可以最好地編寫特定原則集中的原則。

**管理員：**&#x200B;管理員可以編輯任何使用者的個人原則。 他們可以建立共用原則。 他們也可以建立、編輯和刪除原則集，以及指定原則集協調員。

如需各種Document Security角色的詳細資訊，請參閱[關於Document Security使用者](/help/forms/using/admin-help/document-security.md#about-document-security-users)。

## 建立和編輯原則 {#creating-and-editing-policies}

使用者可以建立或編輯個人原則，以供自己使用。 管理員和原則組專員可以為您的組織建立或編輯共用原則。

### 編輯原則的注意事項 {#considerations-for-editing-policies}

編輯原則時，變更會影響原則目前保護的檔案，以及之後原則保護的檔案。 例如，如果您從套用至檔案的原則中移除收件者，則收件者無法再開啟檔案。

檔案的狀態會決定變更何時生效：

* 如果檔案線上上，除非使用者開啟檔案，否則會立即套用變更。 在這種情況下，使用者必須關閉檔案才能使變更生效。
* 如果收件者離線使用檔案（例如在筆記型電腦上），則變更會在下次收件者將檔案上線時生效。 然後，它會透過開啟任何受原則保護的檔案來與Document Security同步。

>[!NOTE]
>
>Acrobat為Microsoft中附加至電子郵件訊息之檔案的收件者自動產生的原則，不會出現在原則清單中®Outlook。 您只能透過開啟關聯檔案的檔案詳細資訊頁面來檢視這些原則。

編輯原則時，會套用以下限制：

* 只有當管理員啟用此權能時，受邀使用者才能編輯原則。 如果您無法編輯原則，將無法使用「編輯」選項。
* 原則組專員只有在擁有正確許可權時，才能編輯原則組內的原則。 超級使用者或原則集管理員會在Document Security管理員介面中設定這些許可權。
* 如果原則設定了浮水印，且管理員在原則建立後將其刪除，則當您編輯並儲存原則時，此浮水印將不再套用至檔案。 只要不編輯原則，刪除的水印僅會保留在現有的原則中。 如果您編輯原則，則必須選取另一個浮水印，以取代刪除的浮水印。
* 您無法透過編輯套用的原則來授與檔案的匿名存取權。 如果您編輯原則，使用者仍然必須登入才能存取檔案。 若要對此檔案套用匿名存取，請先移除使用者端應用程式中的原則，然後套用另一個允許匿名存取的原則。
* Acrobat為Microsoft Outlook中附加至電子郵件訊息之檔案的收件者自動產生的原則，不會出現在原則清單中。 若要存取此原則，請在[檔案]頁面上尋找檔案，開啟[檔案詳細資訊]頁面，然後按一下檔案詳細資訊清單中的原則名稱。

**建立或編輯原則**

1. 在Document Security頁面上，按一下原則並按一下以下其中一個標籤：

   * 若要建立或編輯個人原則，請按一下[我的原則]索引標籤。
   * 若要建立或編輯共用原則，如果您有許可權，請按一下[原則集]索引標籤，然後按一下適當的原則集名稱，再按一下[原則]索引標籤。

1. 按一下「新增」或從清單中選取您要編輯的原則。
1. 在「名稱」方塊中，輸入可唯一識別原則的名稱。 在「說明」方塊中，說明此原則的用途以及何時使用。 如果原則在原則集內，則所有指定使用者的名稱和描述都會出現在原則清單中。 個人原則僅適用於使用者和管理員。

   下列字元無法用於名稱或說明：

   * 小於符號(&lt;)
   * 大於符號(>)
   * &amp;符號(&amp;)
   * 單引號(&#39;)
   * 雙引號(&quot;)
   * 反斜線(\)
   * 正斜線(/)

   如果您在名稱或說明中使用了下列字元，這些字元會轉換為空格：

   * 歸位（ASCII字元13）
   * 換行（ASCII字元10）。

   >[!NOTE]
   >
   >您可以建立包含延伸字元的原則名稱；但是，在兩個字串之間進行比較時，重音和非重音字元（例如「e」和「é」）會被視為相同。 當有人建立原則時，會進行比較以檢查是否有同名原則存在。 比較無法區分相同名稱，重音字元除外。 假設原則已新增至資料庫，但未新增新原則。

1. 將使用者和群組新增到原則中，並設定適當的許可權。 （請參閱[使用者與群組](creating-policies.md#users-and-groups)。）
1. 在一般設定下，選取適當的選項。 （請參閱[一般設定](creating-policies.md#general-settings)。）
1. （選擇性）如果適用，請選取外部授權提供者並指定其屬性。 如果您不想使用外部授權提供者，請按一下「移除預設提供者」。

   外部授權提供者用來設定原則內的屬性，選取時，外部授權提供者會使用此資訊來評估原則。 可用的屬性是由管理員和安裝軟體的人員所設定。

1. 在進階設定下，選取適當的選項。 （請參閱[進階設定](creating-policies.md#advanced-settings)。）
1. 在「不可變更的進階設定」下，選取適當的選項。 （請參閱[不可變更的進階設定](creating-policies.md#unchangeable-advanced-settings)。）
1. 按一下「儲存」。 原則會出現在原則清單中。 新原則旁邊會顯示一個紅色圓圈圖示，表示它仍為停用狀態。

   若要讓使用者可以使用原則，請啟用它。 （請參閱[啟用或停用共用原則](creating-policies.md#enable-or-disable-shared-policies)。）

### 使用者和群組 {#users-and-groups}

在「使用者和群組」區域中，您可以指定有權存取受原則保護檔案的使用者。 對於您指定的每個使用者或群組，您也可以設定檔案使用許可權。

>[!NOTE]
>
>檔案發佈者是使用原則保護檔案的使用者。 原則中預設會包含此使用者，且具有完整存取許可權，包括撤銷和原則切換功能。 但是，管理員可以變更檔案發佈者對共用原則的存取權。 例如，管理員可以限制檔案發行者撤銷檔案存取或切換原則。

**新增使用者或群組：**&#x200B;若要新增使用者或使用者群組，請按一下[新增使用者或群組]，然後按一下[進階搜尋]，以便您可以尋找使用者或群組。 使用者包括您組織的內部使用者，以及已註冊Document Security的受邀使用者。 選取此選項時，會顯示「新增使用者或群組」頁面：

* 在「尋找」方塊中，輸入使用者或群組名稱或電子郵件地址。
* 在「使用」清單中，選取「名稱」或「電子郵件」。
* 在型別清單中，選取使用者或群組。
* 從「範圍」清單中選取您要搜尋的領域，然後按一下「尋找」。
* 傳回結果時，選取要新增的使用者或群組，然後按一下「新增」。

>[!NOTE]
>
>如果您輸入正確的受邀使用者名稱或電子郵件地址，但未傳回任何結果，表示使用者可能尚未註冊，或帳戶可能遭刪除。 您可以嘗試將使用者新增為受邀使用者型別，或聯絡您的管理員。

**邀請新使用者：**&#x200B;若要新增受邀使用者，請按一下[邀請新使用者]，在出現的方塊中輸入使用者的電子郵件地址，然後按一下[邀請]。 只有在管理員啟用此選項時，它才可用。 將新的受邀使用者新增至原則時，如果尚未邀請使用者註冊，Document Security會傳送註冊邀請電子郵件。 使用者必須使用電子郵件中的連結來建立帳戶，然後他們必須啟用帳戶。

註冊之後，受邀使用者可以使用他們有權使用的受原則保護檔案。 根據管理員所啟用的權能，外部使用者可能有權將原則套用至檔案、建立、編輯和刪除原則，以及將其他外部使用者新增至原則。

**新增匿名使用者：**&#x200B;若要允許匿名使用者存取，請按一下[新增匿名使用者]。 只有在管理員為Document Security啟用匿名使用者存取權時，此選項才可用。 （請參閱設定Document Security伺服器）。 此選項會授予每個人存取受此原則保護之檔案的許可權，無論他們是否具有Document Security帳戶。 如果選取此選項，則無法將其他型別的使用者新增到原則中。

>[!NOTE]
>
>若要允許匿名存取目前沒有的受原則保護檔案，請移除現有原則，然後套用允許匿名存取的原則。 如果您切換或變更現有原則，使用者仍必須登入才能存取檔案。

#### 指定使用者和群組的檔案許可權 {#specify-the-document-permissions-for-users-and-groups}

您可以一次為一個使用者或群組指定檔案許可權，也可以從清單中選取多個使用者和群組，並使用欄標題區域中的選項變更其許可權。

依預設，所有受原則保護的檔案都具有允許使用者線上上時開啟檔案的許可權。

「許可權和選項」索引標籤會顯示在Document Security中。

這些檔案許可權可在許可權索引標籤上取得。 您可以將這些許可權套用至PDF、PTC Pro/E和Microsoft Office檔案。

**列印：**&#x200B;允許使用者列印受此原則保護的檔案。 對於Office和Pro/E檔案，您可以選取「列印」核取方塊以允許列印，或清除該核取方塊以防止列印。 如果您選取「顯示PDF的自訂許可權」核取方塊，您可選取下列選項：

**不允許：**&#x200B;不允許使用者列印PDF。

**允許：**&#x200B;使用者可以列印PDF。

**低解析度。 僅限：**&#x200B;使用者可以低解析度列印PDF。

**修改：**&#x200B;允許使用者修改受此原則保護的檔案。 對於Office和Pro/E檔案，您可以選取「修改」核取方塊以允許修改，或清除該核取方塊以防止修改。 如果您選取「顯示PDF的自訂許可權」核取方塊，您可選取下列選項：

**不允許：**&#x200B;不允許使用者修改PDF。

**任何：**&#x200B;使用者可以修改PDF。

**共同作業：**&#x200B;允許使用者使用Adobe Acrobat中的[共同作業]選項與他人共同作業。 即使原則中未明確指定複製許可權，此許可權仍可讓使用者複製表單資料。

**變更頁面：**&#x200B;使用者可以在PDF中新增及移除頁面，以及編輯內容。

**填寫並簽署：**&#x200B;允許使用者在PDF上填寫表單欄位並簽署。

**複製：**&#x200B;允許使用者從受此原則保護的檔案複製文字。

**熒幕Reader：**&#x200B;如果您選取「顯示PDF的自訂許可權」核取方塊，則會顯示此許可權。 選取此選項時，Adobe Acrobat有權將臨時標籤新增至PDF，以提升其透過熒幕助讀程式的可讀性。

這些檔案許可權可在「選項」標籤上取得。 您可以將這些許可權套用至PDF、PTC Pro/E和Microsoft Office檔案：

**離線：**&#x200B;允許使用者離線檢視受此原則保護的檔案。

**許可權有效性：**&#x200B;選取許可權一律有效或設定檔案許可權有效期。 如果您選取有效期間，請按一下日曆圖示以選取日期，並使用箭頭指定24小時格式的時間。

對於共用原則，管理員可以為檔案發佈者（將原則套用至檔案的使用者）停用下列許可權：

**撤銷：**&#x200B;允許檔案發行者撤銷檔案存取許可權。

**切換：**&#x200B;允許檔案發行者切換原則許可權。

### 一般設定 {#general-settings}

「一般設定」區域包含下列設定：

**有效期間：**&#x200B;受原則保護檔案可供授權收件者存取的時間期間。 您可以從下列有效期間選項中選擇：

**檔案在：**&#x200B;之後將無效。檔案從安全保護開始可存取指定的天數。

**檔案在此日期之後將無效：**&#x200B;檔案從套用原則至檔案的日期到指定的結束日期都有效。

**有效起始日期：**&#x200B;檔案在您指定的日期內有效。 您可以使用行事曆透過按一下行事曆圖示來選取日期（如果適用）。

**檔案一律有效：**&#x200B;檔案有效期未過期。

>[!NOTE]
>
>有效日期是根據Document Security系統的時區，而不是根據您本機電腦的時區。

**稽核：**&#x200B;啟用或停用與受原則保護檔案關聯之事件的稽核。 例如，Document Security可以記錄事件，例如嘗試開啟檔案。 稽核的事件會顯示在「事件」頁面上的清單中。 如果您未選取此選項，Document Security將不會記錄與原則相關聯檔案的事件。

>[!NOTE]
>
>管理員也必須在[稽核與隱私權設定]組態頁面上啟用伺服器稽核，稽核功能才能運作。

**延伸使用追蹤：**&#x200B;啟用或停用延伸使用追蹤。 Document Security支援追蹤與在PDF檔案上執行的各種操作相關聯的使用者事件。 可使用Java指令碼存取Document Security物件。 按一下按鈕、播放多媒體檔案或儲存檔案是從受原則保護的PDF引發的一些事件範例。 使用Document Security物件時，您也可以擷取使用者資訊。 可以從全域層級或原則層級的Document Security伺服器啟用事件追蹤。

**自動離線租期：**&#x200B;收件者可以離線使用受原則保護檔案的最大天數（沒有使用中的網際網路或網路連線）。 當租期到期時，收件者必須再次同步化檔案才能繼續使用。

### 外部授權服務提供者 {#external-authorization-providers}

如果您已設定任何外部驗證服務提供者，請加以選取。 列出可用的提供者。

### 驗證設定 {#authentication-settings}

您可以覆寫您在伺服器上設定的驗證設定，並指定與此原則相關的驗證選項。 選取[Override Global Authentication Settings]，然後選取與此原則相關的驗證選項。 下列驗證選項可供使用：

**允許使用者名稱密碼驗證：**&#x200B;如果要讓使用者端應用程式在連線到伺服器時使用使用者名稱/密碼驗證，請選取此選項。

**允許Kerberos驗證：**&#x200B;如果您想要讓使用者端應用程式在連線到伺服器時使用Kerberos驗證，請選取此選項。

**允許使用者端憑證驗證：**&#x200B;如果您想要讓使用者端應用程式在連線到伺服器時使用憑證驗證，請選取此選項。

**允許延伸驗證**&#x200B;選取以啟用延伸驗證。 選取此選項可讓使用者端應用程式使用延伸驗證。 延伸驗證可提供自訂驗證程式，以及在Document Security伺服器上設定的不同驗證選項

如果您正在覆寫全域驗證設定，您可以選擇與此原則相關的驗證選項。 例如，如果您已在伺服器上啟用三個驗證選項（使用者名稱和密碼、使用者端憑證和延伸驗證），則可以覆寫該全域設定，並只選取此原則的延伸驗證。 確定伺服器上已設定您在此選取的驗證選項。 在此範例中，您無法選取Kerberos作為驗證選項，因為它並未在伺服器上設定。

>[!NOTE]
>
>Apple Mac OS X搭配Adobe Acrobat 11.0.6版及更新版本均支援延伸驗證。

### 進階設定 {#advanced-settings}

進階設定區域包含下列設定：

**動態浮水印：**&#x200B;選取要在檔案頁面上動態顯示的浮水印（例如，當收件者列印檔案時）。 動態浮水印可唯一識別檔案，因此有助於確保檔案的機密性，並防止侵犯版權。 例如，管理員可以設定動態浮水印，顯示目前日期、使用者名稱或正在使用檔案的人員的識別碼。 或者，用來保護檔案的原則名稱。 如果設定浮水印，也可以顯示自訂文字或圖形元素。 管理員可設定浮水印選項，管理員和使用者可將這些選項套用至原則。

（請參閱[設定動態浮水印](/help/forms/using/admin-help/configuring-client-server-options.md#configure-dynamic-watermarks)。）

如果您正在編輯原則，而管理員刪除了您先前為此原則選取的已設定浮水印，則「編輯原則」頁面上會顯示附註。 在此情況下，如果您要儲存已編輯的檔案，如果要讓新的浮水印出現在檔案上，請選取新的浮水印。

>[!NOTE]
>
>對於提供匿名使用者存取權的原則，即使您選取此型別的浮水印，匿名使用者的使用者名稱和識別碼也不會顯示為浮水印。

**僅針對PDF使用認證的Acrobat外掛程式：**&#x200B;選取原則時，此選項會指定Acrobat 8.0和更新版本在開啟受原則保護的檔案時，必須以認證模式執行。 當Acrobat以認證模式執行時，不會載入任何協力廠商的外掛程式。

如果您擔心檔案收件者寫入的外掛程式可能會繞過Acrobat 8.0和更新版本中的任何檔案保護，請選取此選項。 如果您的檔案收件者必須使用Acrobat中的協力廠商外掛程式才能與檔案互動，請勿選取此選項。

此選項只在Acrobat 8.0或更新版本中啟用認證模式；管理員必須停用Acrobat 7.0的存取權。

（請參閱[設定Document Security伺服器](/help/forms/using/admin-help/configuring-client-server-options.md#configure-the-document-security-server)。）

此選項不適用於Adobe Reader。

**拒絕存取的錯誤訊息：**&#x200B;任何嘗試在未經許可的情況下開啟受原則保護檔案的人都會看到此訊息。 此訊息會顯示在Acrobat中。 無法顯示此訊息的使用者端會顯示預設訊息，指出存取被拒絕。

### 不可變更的進階設定 {#unchangeable-advanced-settings}

「不可變更的進階設定」區域包含下列設定。 在儲存原則之後，您無法變更這些設定。

**加密演演算法和金鑰長度：**&#x200B;用來保護您的檔案。 您可以從下列選項中選擇：

* AES 128位元
* AES 256位元。 只有Acrobat 9.0和更新版本支援此選項。 若要對PDF檔案使用AES 256加密，請取得並安裝Java Cryptography Extension (JCE) Unlimited Strength管轄原則檔案。 這些檔案會取代[JAVE_HOME]/lib/security資料夾中的local_policy.jar和US_export_policy.jar檔案。 例如，如果您使用Sun JDK 1.6，請將下載的檔案複製到[dep root]/Java/jdk1.6.0_26/lib/security資料夾。 您可以從[Java SE下載](https://java.sun.com/javase/downloads/index.jsp)下載這些檔案。
* 無加密。 Acrobat 9.0和更新版本目前支援此選項。 如果選取此選項，則會停用「檔案限制」選項。 如果您想要使用Document Security進行檔案稽核或版本控制，但不想加密檔案，此選項可能很有用。

**檔案限制：**&#x200B;選取要加密的PDF檔案元件。 其他使用者端應用程式會加密整個檔案，但不會加密連結或內嵌的檔案。 您可以從下列選項中選擇：

* 整個檔案，包括其附件和中繼資料。 *中繼資料*&#x200B;是有關檔案及其內容的資訊，您可以透過檔案[內容]對話方塊或Acrobat [進階]功能表檢視。 在Acrobat中，您可以將不同型別的檔案（例如文字、音訊和視訊檔案）附加至PDF檔案。
* 檔案及其附件，但不包括中繼資料。
* 僅限檔案附件。 您可將附件加密為PDF檔案，而不需加密檔案內容。

## 啟用或停用共用原則 {#enable-or-disable-shared-policies}

若要讓共用原則可用，管理員或原則集協調員必須啟用它。 您可以啟用新原則或先前停用的原則。 您停用的共用原則仍會被強制用於受該原則保護的檔案。

停用的原則旁邊會顯示紅色的X。

>[!NOTE]
>
>管理員無法停用個人原則，使用者也無法啟用和停用自己的原則。

1. 在Document Security頁面上，按一下「原則」，然後按一下「原則集」標籤。
1. 按一下適當的原則集名稱，然後按一下「原則」標籤。
1. 選取適當原則旁的核取方塊，按一下[啟用]或[停用]，然後按一下[確定]。

## 檢視原則的相關資訊 {#view-information-about-a-policy}

使用「我的原則」標籤，您可以搜尋個人原則。

管理員建立的原則集會列在「原則」頁面的「原則集」標籤上。 它們包含有關原則集的資訊，包括其名稱、建立和修改日期以及說明。 按一下原則集名稱，即可檢視其詳細資訊。 有權管理原則的原則集協調員可以在特定原則集中建立共用原則。

當您建立或編輯原則時，會顯示一個頁面，您可以在其中設定要包含在原則中的原則名稱、許可權等級、機密性設定和收件者。

管理員可以為原則設定以下機密性設定：

* 一般檔案機密性選項，例如檔案有效期間和離線租期
* 已授權的使用者，以及其中每個使用者的檔案限制和許可權
* 進階檔案機密性選項，包括動態浮水印和檔案加密

使用者可以檢視他們建立的原則，以及他們有權存取的任何共用原則。 管理員可以檢視Document Security中的所有共用和個人原則。

您可以檢視出現在清單中之原則的詳細資訊，包括原則中包含的使用者或群組，以及為這些使用者指定的機密性設定。

>[!NOTE]
>
>Acrobat為Microsoft Outlook中附加至電子郵件訊息之檔案的收件者自動產生的原則，不會出現在原則清單中。 您只能透過開啟關聯檔案的檔案詳細資訊頁面來檢視這些原則。

1. 在Document Security頁面上，按一下「原則」，然後按一下「我的原則」標籤。
1. 填寫搜尋資訊，以便搜尋個人原則。
1. 從清單中選取適當的原則。
1. 您可以在「原則詳細資訊」頁面檢視原則的詳細資訊、編輯原則或檢視與原則相關的事件。

## 搜尋原則 {#search-for-policies}

管理員可以搜尋共用原則以及其他使用者建立的個人原則。

1. 若要搜尋共用原則，請按一下[原則]，然後按一下[原則集]標籤。 按一下清單中的原則集，然後按一下「原則」標籤。

   若要搜尋個人原則，請在Document Security頁面上按一下「原則」，然後按一下「我的原則」標籤。

1. 在「尋找」清單中，選取下列其中一個選項：

   **原則識別碼：**&#x200B;當使用者建立原則時所產生的原則識別碼。 輸入正確的原則ID。

   **原則名稱：**&#x200B;原則的名稱。 您可以搜尋部分或全部原則名稱。

1. 在文字方塊中，輸入對應的值。 例如，如果您選取了「原則名稱」，請輸入您要搜尋的原則名稱。
1. 在「顯示」清單中，選取要顯示的結果數目，然後按一下「尋找」。 隨即顯示搜尋結果。
1. （選擇性）若要檢視原則詳細資訊，請按一下原則。

## 複製原則 {#copy-a-policy}

您可以複製現有原則，並使用新的名稱和說明來儲存它。 複製原則是使用現有設定來建立原則的有效方式。

只有當管理員啟用此功能時，外部使用者才能複製原則。 如果您無法建立原則，將無法使用「複製」選項。

1. 在Document Security頁面上，按一下「原則」，然後按一下「我的原則」標籤。
1. 從清單中選取適當的原則。
1. 在[原則詳細資訊]頁面上，按一下[複製]。
1. 在「新原則名稱」方塊中，輸入新原則名稱。 選擇性地輸入新的「摘要」。

   下列字元無法用於名稱或說明：

   * 小於符號(&lt;)
   * 大於符號(>)
   * &amp;符號(&amp;)
   * 單引號(&#39;)
   * 雙引號(&quot;)
   * 反斜線(\)
   * 正斜線(/)

   如果您在名稱或說明中使用了下列字元，這些字元會轉換為空格：

   * 歸位（ASCII字元13）
   * 換行（ASCII字元10）。

   >[!NOTE]
   >
   >您可以建立包含延伸字元的原則名稱；但是，在兩個字串之間進行比較時，重音和非重音字元（例如「e」和「é」）會被視為相同。 當有人建立原則時，會進行比較以檢查是否有同名原則存在。 比較無法區分相同名稱，重音字元除外。 假設原則已新增至資料庫，但未新增新原則。

1. 按一下「確定」。

## 刪除原則 {#delete-a-policy}

您可以刪除您建立的原則。 管理員可以刪除任何使用者建立的原則。 原則組專員可以刪除其原則組中的原則。 您刪除的原則仍會被強制用於受該原則保護的檔案。 您可以一次刪除多個原則。

只有當管理員啟用此功能時，受邀的使用者才能刪除原則。 如果您無法刪除原則，則無法使用刪除選項。

1. 在Document Security頁面上，按一下「原則」。
1. 按一下「我的原則」標籤。
1. 若要刪除共用原則，請按一下[原則集]索引標籤，然後按一下適當的原則集名稱。
1. 選取適當原則旁的核取方塊，按一下[刪除]，然後按一下[確定]。

>[!NOTE]
>
>使用使用者端應用程式從檔案中移除原則。 (請參閱Acrobat說明或適當的Acrobat Reader DC擴充功能說明)。

## 排序原則清單 {#sort-the-policy-list}

您可以依欄標題排序原則清單，更輕鬆地尋找原則。 欄標題旁的三角形圖示表示目前用來排序的欄。 向上三角形表示遞增順序，而向下三角形表示遞減順序。

1. 在Document Security頁面上，按一下「原則」，然後按一下「原則集」標籤。
1. 選取原則集，然後按一下「原則」標籤。
1. 按一下適當的欄標題。
1. 若要變更排序順序，請再次按一下欄。
