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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# 自定义网站控制台（经典UI）{#customizing-the-websites-console-classic-ui}

## 将自定义列添加到网站(siteadmin)控制台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

“网站管理”控制台可以扩展为显示自定义列。 该控制台基于JSON对象构建，可通过创建实现该界面的OSGI服务来扩展该 `ListInfoProvider` 对象。 此类服务将修改发送到客户端的JSON对象以构建控制台。

此分步教程介绍如何通过实现界面在网站管理控制台中显示新 `ListInfoProvider` 列。 它包括以下步骤：

1. [创建OSGI服务](#creating-the-osgi-service) ，并将包含该服务的捆绑包部署到AEM服务器。
1. （可选） [通过发出JSON](#testing-the-new-service) 调用来请求用于构建控制台的JSON对象，来测试新服务。
1. [通过扩展存储库中](#displaying-the-new-column) 控制台的节点结构来显示新列。

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
* `updateListItemInfo`，更新单个列表项。

这两种方法的参数有：

* `request`，关联的Sling HTTP请求对象，
* `info`，要更新的JSON对象，它分别是全局列表或当前列表项，
* `resource`,Sling资源。

以下实施示例：

* 为每个 *项* 添加带星号的属性，即 `true` 页面名称开始带有 *e*，否则 `false` 。

* 添加一 *个星号* Count属性，该属性对于列表是全局的，并包含星号列表项的数量。

要创建OSGI服务，请执行以下操作：

1. 在CRXDE Lite中， [创建捆绑](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
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
>* 如果 `ListInfoProvider` 实现定义了响应对象中已存在的属性，则其值将被您提供的属性覆盖。

>
>  
您可以使用 [服务排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) ，管理多个实施的执行 `ListInfoProvider` 顺序。

### 测试新服务 {#testing-the-new-service}

打开网站管理控制台并浏览您的站点时，浏览器将发出ajax调用，以获取用于构建控制台的JSON对象。 例如，当您浏览到文件夹 `/content/geometrixx` 时，以下请求将发送到AEM服务器以构建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

确保在部署包含新服务的包后，新服务正在运行：

1. 将您的浏览器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 响应应按如下方式显示新属性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 显示新列 {#displaying-the-new-column}

最后一步是通过覆盖使网站管理控制台的节点结构适应以显示所有Geometrixx页面的新属性 `/libs/wcm/core/content/siteadmin`。 按如下方式继续：

1. 在CRXDE Lite中，使用类型的节点创 `/apps/wcm/core/content` 建节点结构以 `sling:Folder` 反映该结构 `/libs/wcm/core/content`。

1. 复制节点 `/libs/wcm/core/content/siteadmin` 并将其粘贴到下 `/apps/wcm/core/content`面。

1. 将节点复 `/apps/wcm/core/content/siteadmin/grid/assets` 制到 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 并更改其属性：

   * 删除页 **面文本**

   * 将 **pathRegex** 设置为 `/content/geometrixx(/.*)?`此操作将使所有geometrixx网站的网格配置处于活动状态。

   * 将 **storeProxySuffix设置为** `.pages.json`

   * 编辑 **storeReaderFields** multivalued属性并添加 `starred` 值。

   * 要激活MSM功能，请向多字符串属性storeReaderFields添加以下MSM **参数**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 使用以下 `starred` 属性添加一个 **节点(nt**:unstructured `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` )类型：

   * **dataIndex**: `starred` 字符串类型

   * **header**: `Starred` 字符串类型

   * **xtype**: `gridcolumn` 字符串类型

1. （可选）将不希望显示的列拖放到 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虚路径，默认情况下指 `/libs/wcm/core/content/siteadmin`向
要将其重定向到您的siteadmin版本，请 `/apps/wcm/core/content/siteadmin` 在定义属 `sling:vanityOrder` 性时将其值定义为高于上定义的值 `/libs/wcm/core/content/siteadmin`。 默认值为300，因此任何较高的值都适合。

1. 转到“网站管理”控制台并导航到Geometrixx站点：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx)。

1. 新列名为Starded **** ，可用，按如下方式显示自定义信息：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多个网格配置与pathRegex属性所定 **义的请求路径** 匹配，则将使用第一个网格配置，而不是最具体的网格配置，这意味着配置的顺序很重要。

### 示例包 {#sample-package}

在包共享上自定义网站管理控 [制台包中，可以查看本教程](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 的结果。
