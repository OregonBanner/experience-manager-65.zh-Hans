---
title: 建立自訂Cloud Service
seo-title: Creating a Custom Cloud Service
description: 預設Cloud Services集可使用自訂Cloud Service型別擴展
seo-description: The default set of Cloud Services can be extended with custom Cloud Service types
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 14%

---

# 建立自訂Cloud Service{#creating-a-custom-cloud-service}

預設Cloud Services集可使用自訂Cloud Service型別擴展。 這可讓您以結構化的方式將自訂標籤插入頁面中。 這主要是用於第三方分析提供者，例如Google Analytics、圖表節拍等。 Cloud Services會從父頁面繼承至子頁面，且能夠在任何層級中斷繼承。

>[!NOTE]
>
>此建立新Cloud Service的逐步指南是使用Google Analytics的範例。 並非所有情況都適用於您的使用案例。

1. 在CRXDE Lite中，建立新節點，位於 `/apps`：

   * **名称**: `acs`
   * **类型**: `nt:folder`

1. 在下建立新節點 `/apps/acs`：

   * **名称**: `analytics`
   * **类型**: `sling:Folder`

1. 在下建立2個新節點 `/apps/acs/analytics`：

   * **名稱**：元件
   * **类型**: `sling:Folder`

   和

   * **名稱**：範本
   * **类型**: `sling:Folder`


1. 按一下右鍵 `/apps/acs/analytics/components`. 選取 **建立……** 後面接著 **建立元件……** 開啟的對話方塊可讓您指定：

   * **標籤**： `googleanalyticspage`
   * **标题**: `Google Analytics Page`
   * **超级类型**: `cq/cloudserviceconfigs/components/configpage`
   * **群組**： `.hidden`

1. 按一下 **下一個** 兩次，並指定：

   * **允许的父项:** `acs/analytics/templates/googleanalytics`

   按一下 **下一個** 兩次，然後按一下 **確定**.

1. 將屬性新增至 `googleanalyticspage`：

   * **名称:** `cq:defaultView`
   * **值:** `html`

1. 建立名為的新檔案 `content.jsp` 在 `/apps/acs/analytics/components/googleanalyticspage`，包含下列內容：

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. 在下建立新節點 `/apps/acs/analytics/components/googleanalyticspage/`：

   * **名称**: `dialog`
   * **类型**: `cq:Dialog`
   * **属性**:

      * **名称**: `title`
      * **类型**: `String`
      * **值**: `Google Analytics Config`
      * **名称**: `xtype`
      * **类型**: `String`
      * **值**: `dialog`

1. 在下建立新節點 `/apps/acs/analytics/components/googleanalyticspage/dialog`：

   * **名称**: `items`
   * **类型**: `cq:Widget`
   * **属性**:

      * **名称**: `xtype`
      * **类型**: `String`
      * **值**: `tabpanel`

1. 在下建立新節點 `/apps/acs/analytics/components/googleanalyticspage/dialog/items`：

   * **名称**: `items`
   * **类型**: `cq:WidgetCollection`

1. 在下建立新節點 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`：

   * **名稱**：tab1
   * **类型**: `cq:Panel`
   * **属性**:

      * **名称**: `title`
      * **类型**: `String`
      * **值**: `Config`

1. 在下建立新節點 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`：

   * **名稱**：專案
   * **类型**: `nt:unstructured`
   * **属性**:

      * **名称**: `fieldLabel`
      * **型別**：字串
      * **值**：帳戶ID

      * **名称**: `fieldDescription`
      * **类型**: `String`
      * **值**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名称**: `name`
      * **类型**: `String`
      * **值**: `./accountID`
      * **名称**: `validateOnBlur`
      * **类型**: `String`
      * **值**: `true`
      * **名称**: `xtype`
      * **类型**: `String`
      * **值**: `textfield`

1. 複製 `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` 至 `/apps/acs/analytics/components/googleanalyticspage/body.jsp` 和變更 `libs` 至 `apps` 第34行並將第79行的指令碼參考設為完整路徑。
1. 在下建立新範本 `/apps/acs/analytics/templates/`：

   * 替換為 **資源型別** = `acs/analytics/components/googleanalyticspage`
   * 替換為 **標籤** = `googleanalytics`
   * 替換為 **標題**= `Google Analytics Configuration`
   * 替換為 **allowedpath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * 替換為 **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * 替換為 **sling：resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` （在範本節點上，而不是jcr：content節點）
   * 替換為 **cq：designPath** = `/etc/designs/cloudservices/googleanalytics` （在jcr：content上）

1. 建立新元件： `/apps/acs/analytics/components/googleanalytics`.

   將下列內容新增至 `googleanalytics.jsp`：

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   這應根據設定屬性輸出自訂標籤。

1. 導覽至 `http://localhost:4502/miscadmin#/etc/cloudservices` 和建立新頁面：

   * **标题**: `Google Analytics`
   * **名称**: `googleanalytics`

   返回CRXDE Lite中，並在 `/etc/cloudservices/googleanalytics`，將下列屬性新增至 `jcr:content`：

   * **名称**: `componentReference`
   * **类型**: `String`
   * **值**: `acs/analytics/components/googleanalytics`


1. 導覽至新建立的「服務」頁面( `http://localhost:4502/etc/cloudservices/googleanalytics.html`)並按一下 **+** 若要建立新設定：

   * **父配置**: `/etc/cloudservices/googleanalytics`
   * **标题:**  `My First GA Config`

   選擇 **Google Analytics設定** 並按一下 **建立**.

1. 輸入 **帳戶ID**，例如 `AA-11111111-1`. 单击&#x200B;**确定**。
1. 導覽至頁面，並在頁面屬性下新增新建立的設定。 **Cloud Services** 標籤。
1. 頁面中將會新增自訂標籤。
