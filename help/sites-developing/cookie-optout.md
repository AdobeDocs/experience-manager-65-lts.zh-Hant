---
title: 設定Cookie使用方式
description: AEM提供的服務可讓您設定和控制Cookie在網頁中的使用方式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 219555d8-26e1-4047-b885-ec34084154c1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 設定Cookie使用方式{#configuring-cookie-usage}

AEM提供的服務可讓您設定和控制Cookie在網頁中的使用方式：

* 可設定的伺服器端服務會維護可用的Cookie清單。
* JavaScript API可讓您的JavaScript程式碼驗證是否可使用Cookie。

使用此功能可確保您的頁面符合使用者對Cookie使用方式的同意。

## 設定允許的Cookie {#configuring-allowed-cookies}

設定Adobe Granite選擇退出服務，指定在網頁上使用Cookie的方式。 下表說明您可以設定的特性。

若要設定服務，您可以使用[網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)或[新增OSGi設定到存放庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)。 下表說明任一方法所需的特性。 對於OSGi設定，服務PID為`com.adobe.granite.optout`。

| 屬性名稱（Web主控台） | OSGi屬性名稱 | 描述 |
|---|---|---|
| 選擇退出Cookie | optout.cookies | Cookie的名稱，當顯示在使用者的裝置上時，表示使用者尚未同意使用Cookie。 |
| 選擇退出HTTP標題 | optout.headers | 表示使用者尚未同意使用Cookie的HTTP標頭名稱（如果存在）。 |
| 白名單Cookie | optout.whitelist.cookies | 對網站運作而言不可或缺的Cookie清單，且可在未經使用者同意的情況下使用。 |

## 驗證Cookie使用方式 {#validating-cookie-usage}

使用使用者端JavaScript來呼叫Adobe Granite選擇退出服務，確認您可使用Cookie。 使用Granite.OptOutUtil JavaScript物件來執行下列任何工作：

* 取得Cookie名稱清單，該清單指出使用者不同意將Cookie用於追蹤目的。
* 取得可用的Cookie清單。
* 判斷網頁瀏覽器是否包含Cookie，指出使用者不同意使用Cookie進行追蹤。
* 決定是否可使用特定Cookie。

granite.utils [使用者端資料庫資料夾](/help/sites-developing/clientlibs.md#referencing-client-side-libraries)提供Granite.OptOutUtil物件。 將下列程式碼新增至您的頁面標題JSP，加入JavaScript程式庫的連結：

`<ui:includeClientLib categories="granite.utils" />`

例如，下列JavaScript函式會先決定是否允許使用COOKIE_NAME Cookie，再寫入至其中：

```
function writeCookie(value){
   if (!Granite.OptOutUtil.maySetCookie("COOKIE_NAME"))
      return;
   if (value) {
      value = encodeURIComponent(value);
      document.cookie = "COOKIE_NAME=" + value;
   }
}
```

## Granite.OptOutUtil JavaScript物件 {#the-granite-optoututil-javascript-object}

Granite.OptOutUtil可讓您判斷是否允許使用Cookie。

### getCookieNames()函式 {#getcookienames-function}

Cookie的名稱，當出現時，表示使用者未同意使用Cookie。

**引數**

無。

**傳回**

Cookie名稱陣列。

#### getWhitelistCookieNames()函式 {#getwhitelistcookienames-function}

不論使用者同意為何，都可使用的Cookie名稱。

**引數**

無。

**傳回**

Cookie名稱陣列。

#### isOptedOut()函式 {#isoptedout-function}

判斷使用者的瀏覽器是否包含未表示同意使用Cookie的任何Cookie。

**引數**

無。

**傳回**

如果找到表示不同意的Cookie，則布林值為`true`；如果沒有Cookie表示不同意，則值為`false`。

### maySetCookie(cookieName)函式 {#maysetcookie-cookiename-function}

決定特定Cookie是否可用於使用者的瀏覽器。 此函式等同於使用`isOptedOut`函式來判斷指定的Cookie是否包含在`getWhitelistCookieNames`函式傳回的清單中。

**引數**

* cookieName：字串。 Cookie的名稱。

**傳回**

如果可以使用`cookieName`，則布林值為`true`；如果無法使用`cookieName`，則值為`false`。
