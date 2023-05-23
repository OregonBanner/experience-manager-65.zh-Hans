---
title: AEM Forms工作區的疑難排解准則
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: 啟用記錄並在瀏覽器中使用偵錯工具，針對AEM Forms工作區進行疑難排解。
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: d3923e5e693e7426ee57e81e203f31964a23af3a
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---

# AEM Forms工作區的疑難排解准則 {#troubleshooting-guidelines-for-aem-forms-workspace}

本文討論如何透過啟用記錄功能和使用瀏覽器中的偵錯工具來偵錯AEM Forms工作區。 本檔案也會說明您在使用AEM Forms工作區時可能會遇到的一些常見問題及其因應措施。

## 無法安裝AEM Forms工作區套件 {#unable-to-install-aem-forms-workspace-package}

安裝修補程式後，請開啟AEM Forms工作區。 如果您遇到「找不到資源」錯誤，請開啟CRX封裝管理員，然後重新安裝 `adobe-lc-workspace-pkg-<version>.zip` 封裝。

安裝套件時，如果您遇到錯誤 `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`，請執行下列步驟：

1. 登入CRXDE Lite。 預設URL為 `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. 刪除下列節點：

   `/home/groups/P/PERM_WORKSPACE_USER`

1. 前往「封裝管理員」。 預設URL為 `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. 搜尋並安裝 `adobe-lc-workspace-pkg-[version].zip` 封裝。
1. 重新啟動應用程式伺服器。

## AEM Forms工作區記錄 {#aem-forms-workspace-nbsp-logging}

您可以產生不同層級的記錄，以最佳化錯誤疑難排解。 例如，在複雜應用程式中，在元件層級記錄有助於對特定元件進行偵錯和疑難排解。

在AEM Forms工作區中：

* 若要取得特定元件檔案的記錄資訊，請附加 `/log/<ComponentFile>/<LogLevel>` URL中，然後按下 `Enter`. 指定記錄層級上元件檔案的所有記錄資訊都會列印在主控台上。

* 若要取得所有元件檔案的記錄資訊，請附加 `/log/all/trace` URL中，然後按下 `Enter`.

* 記錄格式： `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>依預設，所有元件的記錄層級都設為INFO。

* 只有該瀏覽器工作階段會維護使用者設定的記錄層級。 當使用者重新整理頁面時，所有元件的記錄層級都會設定為其初始值。

### AEM Forms工作區中的元件檔案清單 {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategorymodel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>工作清單模型</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>任務模型</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>任務檢視</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categorymodel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequueModel</p> </td>
   <td><p>uissettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>共用檢視</p> </td>
   <td><p>uissettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>使用者資訊模型</p> </td>
  </tr>
  <tr>
   <td><p>outofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofficeView</p> </td>
   <td><p>起點模型</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>偏好設定檢視</p> </td>
   <td><p>起始點檢視</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>伺服器模型</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>伺服器檢視</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>任務詳細資料檢視</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### AEM Forms工作區中可用的記錄層級 {#log-levels-available-in-nbsp-aem-forms-workspace}

* 致命
* 错误
* 警告
* 信息
* 偵錯
* TRACE
* 关闭

## 瀏覽器的偵錯資訊 {#debugging-information-for-browsers}

指令碼和樣式可以在不同的瀏覽器中偵錯。

* **在IE中進行偵錯**：若要在IE中偵錯AEM Forms工作區，請參閱： [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **在Chrome中偵錯**：若要在Chrome中開啟Debugger，請使用捷徑：Ctrl+Shift+I。如需詳細資訊，請參閱： [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **在Firefox中進行偵錯**：數個附加元件可用於在Firefox中偵錯指令碼和樣式。 例如，Firebug就是這類偵錯公用程式([https://getfirebug.com](https://getfirebug.com))。

## 常见问题解答 {#faqs}

1. PDF表單未在Google Chrome中轉譯或提交。

   1. 安裝Adobe®Reader®外掛程式。
   1. 在Chrome中開啟chrome://plugins ，檢視可用的外掛程式。
   1. 停用ChromePDF檢視器外掛程式，並啟用Adobe Reader外掛程式。

1. Google Chrome中未轉譯SWF表單或指南。

   1. 在Chrome中開啟chrome://plugins ，檢視可用的外掛程式。
   1. 如需AdobeFlash®播放器外掛程式的詳細資訊，請參閱。
   1. 停用AdobeFlash Player外掛程式下的PepperFlash。

1. 我已經自訂AEM Forms工作區，但看不到變更。

   清除瀏覽器的快取，然後存取AEM Forms工作區。

1. 使用者在案頭開啟表單時，需要執行哪些動作才能以HTML呈現表單？

   使用Workbench時，在指派作業步驟中選取預設設定檔的「HTML」選項按鈕。

1. 按一下時附件未顯示。

   若要檢視附件，請在瀏覽器中啟用快顯視窗。

1. 使用者已登入表單應用程式。 如果使用者嘗試登入工作區，則可能無法載入（如果使用者沒有工作區許可權）。

   從其他表單應用程式登出，然後登入工作區。

1. HTML表單，在其設計中使用流程屬性，在AEM Forms工作區中呈現時，在表單內顯示提交按鈕。

   設計表單時，當您使用流程屬性時，它會在表單內新增提交按鈕。 在AEM Forms工作區中呈現為PDF時，一般使用者看不到提交按鈕。 不過，在AEM Forms工作區中以HTML表單形式呈現時，一般使用者可看到「提交」按鈕。 按一下表單內的此「提交」按鈕不會起始任何動作。 按一下AEM Forms工作區底部的「提交」按鈕（在表單外）即可完成工作。
