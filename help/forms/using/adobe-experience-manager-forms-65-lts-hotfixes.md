---
title: Adobe Experience Manager Forms 6.5 LTS Hotfix
description: 提供如何下載和安裝AEM Forms 6.5 LTS的Hotfix的相關資訊。 若為AEM 6.5 （非LTS），請參閱AEM 6.5 Forms Hotfix文章。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
source-git-commit: 989d83cfc56f7a7d4e2aea5a7ac1ca444d505859
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%
---
# Adobe Experience Manager Forms 6.5 LTS Hotfix{#aem-form-hotfix}

本文列出為解決已知問題、改善系統穩定性及增強AEM Forms 6.5 LTS整體效能而實作的重大修正。


本文適用於AEM Forms 6.5 LTS。 若為AEM 6.5 （非LTS）部署，請參閱[Adobe Experience Manager Forms Hotfix](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/release-notes/aem-forms-hotfix)。

>[!NOTE]
>
> 這些Hotfix的設計是累積性的，包含所有先前的修正。 將最新Hotfix套用至某個版本時，不僅可解決最近的問題，還可整合所有先前的錯誤修正和增強功能。

## AEM Forms 6.5 LTS的Hotfix {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>Hotfix下載連結（AEM Software Distribution連結）</strong></td>
    <td><strong>已修正的問題</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2026年9月21日</strong><br>
      <em>適用於：</em> AEM Forms 6.5 LTS Service Pack 2 JEE部署(JBoss、WebLogic、WebSphere)<br>
    </td>
    <td>
    <p><strong>若要安裝此Hotfix，請依序完成下列步驟：</strong></p>
    <p><strong>步驟1：安裝修補程式</strong></p>
    <ul>
    <strong>JBoss：</strong>
    <li>Windows — 適用於JBoss JEE伺服器的Windows上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">Hotfix</a></li>
    <li>Linux- JBoss JEE伺服器Linux上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz">Hotfix</a></li>
    <strong>WebLogic：</strong>
    <li>Windows — 適用於Weblogic JEE伺服器的Windows上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">Hotfix</a></li>
    <li>Linux- Linux上適用於Weblogic JEE伺服器的AEM Forms 6.5 LTS SP2 <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz">Hotfix</a></li>
    <strong>WebSphere：</strong>
    <li>Windows- Websphere JEE伺服器Windows上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">Hotfix</a></li>
    <li>Linux — 適用於Websphere JEE伺服器Linux上AEM Forms 6.5 LTS SP2的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz">Hotfix</a></li>
    </ul>
    <p>使用標準AEM Forms on JEE修補程式安裝程式來安裝修補程式。 <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>步驟2：安裝弱點修正套件組合</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">AEM Forms 6.5 LTS SP2的弱點修正套件</a></li>
    </ul>
    <ol>
    <li>在<code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>開啟OSGi主控台。</li>
    <li>按一下<strong>安裝/更新</strong>。</li>
    <li>選取<strong>開始套件</strong>和<strong>重新整理套件</strong>核取方塊。</li>
    <li>按一下<strong>選擇檔案</strong>，然後上傳下載的套件。</li>
    <li>等候記錄檔結清，且組合顯示為<strong>作用中</strong>。</li>
    </ol>
    <p><strong>步驟3：更新AEM Forms Workbench安裝程式</strong></p>
    <p>您必須更新至最新的AEM Forms Workbench安裝程式。 從<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">AEM Forms Workbench安裝程式</a>下載。</p>
    <p><strong>步驟4：更新使用者端程式庫檔案（開發人員）</strong></p>
    <p>此修補程式包含對SDK使用者端程式庫<code>adobe-livecycle-client.jar</code>的主要更新（請參閱<a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">包含AEM Forms Java程式庫檔案</a>）。 如果您的專案使用此JAR檔案，請在安裝Hotfix之後，更新專案類別路徑中的<code>adobe-livecycle-client.jar</code>。 最新版本可在<code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>取得。</p>
    <p>此Hotfix為累積式，您可以直接套用至AEM Forms 6.5 LTS Service Pack 2或舊版Service Pack，而不需要先安裝Service Pack 2。</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b>在Apache Shiro更新至2.1.0版後，JEE上的AEM Forms無法透過Shiro安全管理員的<code>NoClassDefFoundError</code>啟動。 此Hotfix會還原成功的開機程式。</li>
    <li>JEE上的<b>FORMS-26819</b> AEM Forms失敗，並出現<code>org.owasp.esapi.reference.JavaLogFactory</code>的「找不到類別」錯誤。 此Hotfix會解析缺少的類別。</li>
    <li><b>FORMS-26584、FORMS-26589</b>升級至AEM Forms 6.5 LTS後，TaskManager端點已移除。 此Hotfix會還原TaskManager端點。</li>
    <li><b>FORMS-26569</b>在JEE上，由於安全XML產生器，Configuration Manager MergeEars步驟失敗並出現DOCTYPE宣告錯誤(<code>ALC-LCM-010-200</code>)。 此Hotfix可讓MergeEars步驟完成。</li>
    <li>IBM WebSphere Liberty部署中缺少<b>FORMS-25063</b>應用程式層級記錄。 此Hotfix會還原應用程式層級的記錄。</li>
    <li><b>FORMS-24892</b>在JBoss上，電子郵件失敗並顯示「IMAPProvider不是子型別」。 此Hotfix可還原JBoss上的電子郵件功能。</li>
    <li><b>FORMS-24692</b>在WebSphere Liberty設定檔(WLP)上，電子郵件失敗並顯示「無法將通訊端轉換為TLS」。 此Hotfix會透過WLP上的TLS還原電子郵件。</li>
    <li><b>FORMS-26688</b>已將Gibson程式庫更新至6.0.29665850版。</li>
    <li><b>FORMS-25222</b>反向移植SAML宣告驗證改善。</li>
    <li><b>FORMS-26733， FORMS-26734</b>已將Apache Log4j更新至2.25.5版。</li>
    <li>此Hotfix也包含安全性修正。</li>
    </ul>
    <p><strong>組建：</strong> AEMForms-6.6.0-0008</p>
    </td>
  </tr>
  <tr>
    <td>
      <strong>2025年9月9日</strong><br>
    <td>
    <ul>
    <li>Windows - Windows上的AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Hotfix2</a></li>
    <li>Linux- Linux上適用於AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Hotfix2</a></li>
     <li>macOS- MacOS</a>上AEM Service Pack 6.5 LTS的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">Hotfix2</li>
    <td>
    <ul>
    <li>解決啟用伺服器端驗證(SSV)時提交作業可能失敗的問題，提升表單提交的可靠性如果您遇到任何問題，請聯絡[Adobe Experience Manager Forms支援](https://business.adobe.com/in/support/main.html)
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## 下載並安裝OSGi Hotfix {#download-install-hotfix}

執行以下步驟來下載及安裝Hotfix：

1. 從Software Distribution連結下載[Hotfix](#hotfix-for-adaptive-forms)。
1. 解壓縮Hotfix封存檔案，以便取得Experience Manager套件(.zip)和套件(.jar)檔案。
1. 透過[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上傳及安裝封裝(.zip)。
1. 開啟設定管理員組合`https://server:host/system/console/bundles`，上傳並安裝組合(.jar)。 已安裝Hotfix。
