---
title: 自定义网站控制台（经典UI）
seo-title: 自定义网站控制台（经典UI）
description: 可以扩展“网站管理”控制台以显示自定义列
seo-description: 可以扩展“网站管理”控制台以显示自定义列
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---

# 自定义网站控制台（经典UI）{#customizing-the-websites-console-classic-ui}

## 将自定义列添加到网站（站点管理）控制台{#adding-a-custom-column-to-the-websites-siteadmin-console}

可以扩展“网站管理”控制台以显示自定义列。 控制台基于JSON对象构建，该对象可通过创建实施`ListInfoProvider`接口的OSGI服务来扩展。 此类服务会修改发送到客户端以构建控制台的JSON对象。

此分步教程介绍如何通过实施`ListInfoProvider`界面在“网站管理”控制台中显示新列。 它包括以下步骤：

1. [创建OSGi服](#creating-the-osgi-service) 务并将包含该服务的包部署到AEM服务器。
1. （可选）[通过发出JSON调用来测试新服务](#testing-the-new-service)，以请求用于构建控制台的JSON对象。
1. [通过扩展存](#displaying-the-new-column) 储库中控制台的节点结构来显示新列。

>[!NOTE]
>
>本教程还可用于扩展以下管理控制台：
>
>* 数字资产控制台
>* 社区控制台

>



### 创建OSGI服务{#creating-the-osgi-service}

`ListInfoProvider`接口定义了两种方法：

* `updateListGlobalInfo`，要更新列表的全局属性，
* `updateListItemInfo`，以更新单个列表项。

两种方法的参数包括：

* `request`，关联的Sling HTTP请求对象，
* `info`，要更新的JSON对象（分别为全局列表或当前列表项）
* `resource`, Sling资源。

以下实施示例：

* 为每个项目添加&#x200B;*星形*&#x200B;属性，如果页面名称以&#x200B;*e*&#x200B;开头，则该属性为`true`，否则为`false`。

* 添加&#x200B;*stiredCount*&#x200B;属性，该属性是列表的全局属性，包含有星号列表项的数量。

要创建OSGI服务，请执行以下操作：

1. 在CRXDE Lite中，[创建包](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
1. 添加下面的示例代码。
1. 构建包。

新服务已启动且正在运行。

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* 您的实施应根据提供的请求和/或资源，决定是否应将信息添加到JSON对象。
>* 如果您的`ListInfoProvider`实施定义了响应对象中已存在的属性，则其值将被您提供的值覆盖。

>
>  
您可以使用[服务排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING)来管理多个`ListInfoProvider`实施的执行顺序。

### 测试新服务{#testing-the-new-service}

当您打开网站管理控制台并浏览您的网站时，浏览器将发出ajax调用，以获取用于构建控制台的JSON对象。 例如，当您浏览`/content/geometrixx`文件夹时，会向AEM服务器发送以下请求以构建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要确保在部署包含新服务的包后，新服务正在运行：

1. 将您的浏览器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 响应应按如下方式显示新属性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 显示新列{#displaying-the-new-column}

最后一步是调整网站管理控制台的节点结构，以通过覆盖`/libs/wcm/core/content/siteadmin`来显示所有Geometrixx页面的新属性。 请按如下方式继续：

1. 在CRXDE Lite中，使用`sling:Folder`类型的节点创建节点结构`/apps/wcm/core/content`以反映结构`/libs/wcm/core/content`。

1. 复制节点`/libs/wcm/core/content/siteadmin`并将其粘贴到`/apps/wcm/core/content`下方。

1. 将节点`/apps/wcm/core/content/siteadmin/grid/assets`复制到`/apps/wcm/core/content/siteadmin/grid/geometrixx`并更改其属性：

   * 删除&#x200B;**pageText**

   * 将&#x200B;**pathRegex**&#x200B;设置为`/content/geometrixx(/.*)?`
这将使所有geometrixx网站的网格配置处于活动状态。

   * 将&#x200B;**storeProxySuffix**&#x200B;设置为`.pages.json`

   * 编辑&#x200B;**storeReaderFields**&#x200B;多值属性并添加`starred`值。

   * 要激活MSM功能，请将以下MSM参数添加到多字符串属性&#x200B;**storeReaderFields**&#x200B;中：

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`下添加`starred`节点（类型为&#x200B;**nt:unstructured**），其属性如下：

   * **dataIndex**: `starred` 字符串类型

   * **标题**: `Starred` 字符串类型

   * **xtype**: `gridcolumn` 字符串类型

1. （可选）删除您不希望在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`中显示的列

1. `/siteadmin` 是默认指向的虚路 `/libs/wcm/core/content/siteadmin`径。要将此内容重定向到`/apps/wcm/core/content/siteadmin`上的siteadmin版本，请定义属性`sling:vanityOrder`的值大于`/libs/wcm/core/content/siteadmin`上定义的值。 默认值为300，因此任何更高的值都适合。

1. 转到网站管理控制台，然后导航到Geometrixx站点：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx)。

1. 提供了名为&#x200B;**Stared**&#x200B;的新列，该列显示如下自定义信息：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多个网格配置与&#x200B;**pathRegex**&#x200B;属性定义的请求路径匹配，则将使用第一个网格配置，而不是最具体的网格配置，这意味着配置的顺序很重要。

### 示例包{#sample-package}

本教程的结果可在包共享上的[自定义网站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin)包中找到。
