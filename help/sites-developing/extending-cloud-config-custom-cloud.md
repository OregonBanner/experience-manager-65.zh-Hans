---
title: 创建自定义Cloud Service
seo-title: 创建自定义Cloud Service
description: 默认Cloud Services集可以使用自定义Cloud Service类型进行扩展
seo-description: 默认Cloud Services集可以使用自定义Cloud Service类型进行扩展
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 12%

---


# 创建自定义Cloud Service{#creating-a-custom-cloud-service}

默认的Cloud Services集可以用自定义Cloud Service类型进行扩展。 这允许您以结构化方式将自定义标记注入页面。 这将主要用于第三方分析提供商，例如Google Analytics、Chartbeat等。 Cloud Services从父页面继承到子页面，能够在任何级别中中断继承。

>[!NOTE]
>
>此创建新Cloud Service的分步指南是使用Google Analytics的示例。 所有内容可能不适用于您的使用案例。

1. 在CRXDE Lite中，在`/apps`下创建新节点：

   * **名称**: `acs`
   * **类型**: `nt:folder`

1. 在`/apps/acs`下创建新节点：

   * **名称**: `analytics`
   * **类型**: `sling:Folder`

1. 在`/apps/acs/analytics`下新建2个节点：

   * **名称**:组件
   * **类型**: `sling:Folder`

   和

   * **名称**:模板
   * **类型**: `sling:Folder`


1. 右键单击`/apps/acs/analytics/components`。 选择&#x200B;**创建……**&#x200B;后跟&#x200B;**创建组件……**&#x200B;打开的对话框允许您指定：

   * **标签**: `googleanalyticspage`
   * **标题**: `Google Analytics Page`
   * **超级类型**: `cq/cloudserviceconfigs/components/configpage`
   * **组**: `.hidden`

1. 单击&#x200B;**下一步**&#x200B;两次，然后指定：

   * **允许的父项:** `acs/analytics/templates/googleanalytics`

   单击&#x200B;**Next**&#x200B;两次，然后单击&#x200B;**OK**。

1. 将属性添加到`googleanalyticspage`:

   * **名称:** `cq:defaultView`
   * **值：** `html`

1. 在`/apps/acs/analytics/components/googleanalyticspage`下新建一个名为`content.jsp`的文件，其中包含以下内容：

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

1. 在`/apps/acs/analytics/components/googleanalyticspage/`下创建新节点：

   * **名称**: `dialog`
   * **类型**: `cq:Dialog`
   * **属性**:

      * **名称**: `title`
      * **类型**: `String`
      * **值**:  `Google Analytics Config`
      * **名称**: `xtype`
      * **类型**: `String`
      * **值**:  `dialog`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog`下创建新节点：

   * **名称**: `items`
   * **类型**: `cq:Widget`
   * **属性**:

      * **名称**: `xtype`
      * **类型**: `String`
      * **值**:  `tabpanel`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items`下创建新节点：

   * **名称**: `items`
   * **类型**: `cq:WidgetCollection`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`下创建新节点：

   * **名称**:tab1
   * **类型**: `cq:Panel`
   * **属性**:

      * **名称**: `title`
      * **类型**: `String`
      * **值**:  `Config`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`下创建新节点：

   * **名称**:项目
   * **类型**: `nt:unstructured`
   * **属性**:

      * **名称**: `fieldLabel`
      * **类型**:字符串
      * **值**:帐户ID

      * **名称**: `fieldDescription`
      * **类型**: `String`
      * **值**:  `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名称**: `name`
      * **类型**: `String`
      * **值**:  `./accountID`
      * **名称**: `validateOnBlur`
      * **类型**: `String`
      * **值**:  `true`
      * **名称**: `xtype`
      * **类型**: `String`
      * **值**:  `textfield`

1. 将`/libs/cq/cloudserviceconfigs/components/configpage/body.jsp`复制到`/apps/acs/analytics/components/googleanalyticspage/body.jsp`，将第34行的`libs`更改为`apps`，并使第79行的脚本引用成为完全限定的路径。
1. 在`/apps/acs/analytics/templates/`下创建新模板：

   * 具有&#x200B;**资源类型** = `acs/analytics/components/googleanalyticspage`
   * 具有&#x200B;**标签** = `googleanalytics`
   * 具有&#x200B;**Title**= `Google Analytics Configuration`
   * with **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * with **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * 与&#x200B;**sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage`（在模板节点上，而不是jcr:content节点上）
   * 具有&#x200B;**cq:designPath** = `/etc/designs/cloudservices/googleanalytics`（在jcr:content上）

1. 创建新组件：`/apps/acs/analytics/components/googleanalytics`。

   将以下内容添加到`googleanalytics.jsp`:

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

   这应根据配置属性输出自定义标记。

1. 导航到`http://localhost:4502/miscadmin#/etc/cloudservices`并创建新页面：

   * **标题**: `Google Analytics`
   * **名称**: `googleanalytics`

   返回CRXDE Lite，在`/etc/cloudservices/googleanalytics`下，将以下属性添加到`jcr:content`:

   * **名称**: `componentReference`
   * **类型**: `String`
   * **值**:  `acs/analytics/components/googleanalytics`


1. 导航到新创建的服务页面(`http://localhost:4502/etc/cloudservices/googleanalytics.html`)并单击&#x200B;**+**&#x200B;以创建新配置：

   * **父配置**: `/etc/cloudservices/googleanalytics`
   * **标题:**  `My First GA Config`

   选择&#x200B;**Google Analytics配置**&#x200B;并单击&#x200B;**创建**。

1. 输入&#x200B;**帐户ID**，例如`AA-11111111-1`。 单击&#x200B;**确定**。
1. 导航到页面，并在&#x200B;**Cloud Services**&#x200B;选项卡下的页面属性中添加新创建的配置。
1. 页面中将添加自定义标记。

