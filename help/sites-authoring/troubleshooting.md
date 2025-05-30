---
title: 疑難排解AEM中的製作問題
description: 使用AEM時可能會遇到的一些問題。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 1e735d57-834a-4251-9b92-ccc6d4712f2a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 疑難排解製作時的AEM{#troubleshooting-aem-when-authoring}

下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。

>[!NOTE]
>
>如果發生問題，也值得檢查您執行個體（發行版本和Service Pack）的[已知問題](/help/release-notes/release-notes.md)清單。

>[!NOTE]
>
>擁有管理員許可權且想要疑難排解AEM問題的使用者，可以使用[疑難排解AEM （適用於管理員）](/help/sites-administering/troubleshoot.md)中所述的疑難排解方法。 如果您沒有足夠的許可權，請聯絡您的系統管理員，瞭解如何疑難排解AEM。

## 發佈網站上仍顯示舊的頁面版本 {#old-page-version-still-on-published-site}

* **問題**：

   * 您已經變更頁面，並將頁面復寫至發佈網站，但發佈網站上仍顯示&#x200B;*舊*&#x200B;版本的頁面。

* **原因**：

   * 這可能有多種原因，通常是快取(本機瀏覽器或Dispatcher)，但有時復寫佇列可能會發生問題。

* **解決方案**：

   * 這裡有多種可能性：
   * 確認已正確復寫頁面。 檢查頁面狀態，並視需要檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，然後再次存取您的頁面。
   * 將`?`新增至頁面URL的結尾。 例如：

      * `http://localhost:4502/sites.html/content?`
      * 這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果復寫佇列發生問題，請聯絡您的系統管理員。

## 元件動作在工具列上不可見 {#component-actions-not-visible-on-toolbar}

* **問題**：

   * 在作者環境中編輯內容頁面時，看不到所有適用的元件動作。

* **原因**：

   * 在極少數情況下，先前的動作可能會影響工具列。

* **解決方案**：

   * 重新整理頁面。
