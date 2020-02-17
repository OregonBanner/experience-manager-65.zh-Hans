---
title: 自定义网站控制台（经典UI）
seo-title: 自定义网站控制台（经典UI）
description: “网站管理”控制台可以扩展为显示自定义列
seo-description: “网站管理”控制台可以扩展为显示自定义列
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
translation-type: tm+mt
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# 自定义网站控制台（经典UI）{#customizing-the-websites-console-classic-ui}

## 将自定义列添加到网站(siteadmin)控制台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

“网站管理”控制台可以扩展为显示自定义列。 该控制台基于JSON对象构建，该对象可以通过创建实现该接口的OSGI服务进行 `ListInfoProvider` 扩展。 此类服务将修改发送到客户端以构建控制台的JSON对象。

此分步教程介绍如何通过实现界面在“网站管理”控制台中显示新 `ListInfoProvider` 列。 它包括以下步骤：

1. [创建OSGI服务](#creating-the-osgi-service) ，并将包含该服务的捆绑包部署到AEM服务器。
1. （可选） [](#testing-the-new-service) 通过发出JSON调用来请求用于构建控制台的JSON对象，来测试新服务。
1. [通过扩展存储库](#displaying-the-new-column) 中控制台的节点结构来显示新列。

>[!NOTE]
>
>本教程还可用于扩展以下管理控制台：
>
>* 数字资产控制台
>* 社区控制台
>



### 创建OSGI服务 {#creating-the-osgi-service}

该接 `ListInfoProvider` 口定义两种方法：

* `updateListGlobalInfo`，更新列表的全局属性，
* `updateListItemInfo`，以更新单个列表项。

两种方法的参数为：

* `request`，关联的Sling HTTP请求对象，
* `info`，要更新的JSON对象，它分别是全局列表或当前列表项，
* `resource`, Sling资源。

以下实施示例：

* 为每个项 *目添加带星号的属性* ，即页面名 `true` 称以e开头，否则，该属 *性将显*&#x200B;示为 `false` e。

* 添加一 *个staredCount属性* ，该属性是列表的全局属性，包含带星号的列表项数。

要创建OSGI服务，请执行以下操作：

1. 在CRXDE Lite中，创 [建一个包](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
1. 添加以下示例代码。
1. 构建捆绑包。

新服务已启动并正在运行。

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
>* 您的实施应根据提供的请求和／或资源决定是否应将信息添加到JSON对象。
>* 如果实 `ListInfoProvider` 现定义了响应对象中已存在的属性，则其值将被您提供的属性覆盖。
   >  您可以使用 [服务等级](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) ，管理多个实施的执行 `ListInfoProvider` 顺序。
>



### 测试新服务 {#testing-the-new-service}

当您打开网站管理控制台并浏览您的站点时，浏览器将发出ajax调用以获取用于构建控制台的JSON对象。 例如，当您浏览到该文件夹时， `/content/geometrixx` 以下请求将发送到AEM服务器以构建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

确保新服务在部署包含该服务的包后正在运行：

1. 将您的浏览器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

1. 响应应按如下方式显示新属性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 显示新列 {#displaying-the-new-column}

最后一步是通过覆盖使“网站管理”控制台的节点结构适应以显示所有Geometrixx页面的新属性 `/libs/wcm/core/content/siteadmin`。 按如下步骤继续：

1. 在CRXDE Lite中，创建节点结构，其类 `/apps/wcm/core/content` 型为节点，以 `sling:Folder` 反映该结构 `/libs/wcm/core/content`。

1. 复制节点 `/libs/wcm/core/content/siteadmin` 并将其粘贴到下方 `/apps/wcm/core/content`。

1. 将节点复制 `/apps/wcm/core/content/siteadmin/grid/assets` 到并 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 更改其属性：

   * 删除页 **面文本**

   * 将 **pathRegex设置**`/content/geometrixx(/.*)?`为此操作将使所有geometrixx网站的网格配置处于活动状态。

   * 将 **storeProxySuffix设置为**`.pages.json`

   * 编辑 **storeReaderFields** multivalued属性并添加 `starred` 值。

   * 要激活MSM功能，请将以下MSM参数添加到多字符串属性 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 添加一 `starred` 个节点(类型 **为nt:unstructured**), `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 其属性如下：

   * **dataIndex**:字 `starred` 符串类型

   * **header**:字 `Starred` 符串类型

   * **xtype**:字 `gridcolumn` 符串类型

1. （可选）将不希望显示在的列拖放到 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虚路径（默认为） `/libs/wcm/core/content/siteadmin`。
要将其重定向到您的siteadmin版本，请 `/apps/wcm/core/content/siteadmin` 在定义属性时 `sling:vanityOrder` 将其值定义为高于上定义的值 `/libs/wcm/core/content/siteadmin`。 默认值为300，因此任何较高的值都适合。

1. 转到“网站管理”控制台，然后导航到Geometrixx站点：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx)。

1. 名为Stardered的新列 **可用** ，按如下所示显示自定义信息：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多个网格配置与 **pathRegex** 属性定义的请求路径匹配，则将使用第一个网格配置，而不是最具体的网格配置，这意味着配置的顺序很重要。

### 示例包 {#sample-package}

本教程的结果可在包共享上的自 [定义网站管理控制台包中找](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 到。
