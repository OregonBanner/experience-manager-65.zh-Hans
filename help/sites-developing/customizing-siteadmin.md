---
title: 自定义网站控制台（经典UI）
seo-title: Customizing the Websites Console (Classic UI)
description: 可以扩展网站管理控制台以显示自定义列
seo-description: The Websites Administration console can be extended to display custom columns
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
source-wordcount: '781'
ht-degree: 0%

---

# 自定义网站控制台（经典UI）{#customizing-the-websites-console-classic-ui}

## 将自定义列添加到网站(siteadmin)控制台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

可以扩展网站管理控制台以显示自定义列。 控制台基于可通过创建用于实现的OSGI服务来扩展的JSON对象而构建 `ListInfoProvider` 界面。 此类服务会修改发送到客户端的JSON对象，以构建控制台。

此分步教程介绍了如何通过实施 `ListInfoProvider` 界面。 它包含以下步骤：

1. [创建OSGI服务](#creating-the-osgi-service) 并将包含它的包部署到AEM服务器。
1. （可选） [测试新服务](#testing-the-new-service) 通过发出JSON调用来请求用于构建控制台的JSON对象。
1. [显示新列](#displaying-the-new-column) 通过在存储库中扩展控制台的节点结构。

>[!NOTE]
>
>本教程还可用于扩展以下管理控制台：
>
>* 数字资产控制台
>* 社区控制台
>


### 创建OSGI服务 {#creating-the-osgi-service}

此 `ListInfoProvider` 接口定义了两种方法：

* `updateListGlobalInfo`，更新列表的全局属性，
* `updateListItemInfo`，以更新单个列表项。

这两种方法的参数为：

* `request`，关联的Sling HTTP请求对象，
* `info`，要更新的JSON对象，它分别是全局列表或当前列表项，
* `resource`，Sling资源。

以下实施示例：

* 添加 *星形* 每个项目的属性，即 `true` 如果页面名称以 *e*、和 `false` 否则。

* 添加 *starredCount* 属性，该属性对列表是全局属性，包含星形列表项的数量。

要创建OSGI服务，请执行以下操作：

1. 在CRXDE Lite， [创建捆绑包](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 在下方添加示例代码。
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
>* 您的实施应根据提供的请求和/或资源决定是否应将该信息添加到JSON对象。
>* 如果您的 `ListInfoProvider` 实施定义了响应对象中已存在的属性，其值将由您提供的值覆盖。
>
>  您可以使用 [服务排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 管理多个执行顺序 `ListInfoProvider` 实施。

### 测试新服务 {#testing-the-new-service}

当您打开网站管理控制台并浏览您的站点时，浏览器将发出ajax调用以获取用于构建控制台的JSON对象。 例如，当您浏览到 `/content/geometrixx` 文件夹，则会向AEM服务器发送以下请求以构建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要确保新服务在部署包含它的捆绑包后正在运行，请执行以下操作：

1. 将浏览器指向以下URL：
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 响应应按如下方式显示新属性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 显示新列 {#displaying-the-new-column}

最后一步是调整网站管理控制台的节点结构，通过叠加来显示所有Geometrixx页面的新属性 `/libs/wcm/core/content/siteadmin`. 按照以下步骤操作：

1. 在CRXDE Lite中，创建节点结构 `/apps/wcm/core/content` 具有类型的节点 `sling:Folder` 以反映结构 `/libs/wcm/core/content`.

1. 复制节点 `/libs/wcm/core/content/siteadmin` 并粘贴到下方 `/apps/wcm/core/content`.

1. 复制节点 `/apps/wcm/core/content/siteadmin/grid/assets` 到 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 并更改其属性：

   * 移除 **pageText**

   * 设置 **pathRegex** 到 `/content/geometrixx(/.*)?`
这将使所有geometrixx网站的网格配置处于活动状态。

   * 设置 **storeproxysuffix** 到 `.pages.json`

   * 编辑 **storeReaderFields** 多值物业并加上 `starred` 值。

   * 要激活MSM功能，请将以下MSM参数添加到多字符串属性中 **storeReaderFields**：

      * **msm：isSource**
      * **msm：isInBlueprint**
      * **msm：isLiveCopy**

1. 添加 `starred` 节点（属于类型） **nt：unstructured**)下 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 具有以下属性：

   * **dataIndex**： `starred` 字符串类型

   * **标头**： `Starred` 字符串类型

   * **xtype**： `gridcolumn` 字符串类型

1. （可选）删除您不想显示的列 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是一个虚名路径，默认指向 `/libs/wcm/core/content/siteadmin`.
要将此重定向到您在上的siteadmin版本，请执行以下操作 `/apps/wcm/core/content/siteadmin` 定义属性 `sling:vanityOrder` ，其值将高于在上定义的 `/libs/wcm/core/content/siteadmin`. 默认值为300，因此任何更高的值都适用。

1. 转到网站管理控制台并导航到Geometrixx站点：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 新列名为 **星形** 可用，按如下方式显示自定义信息：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多个网格配置与由定义的请求路径匹配 **pathRegex** 属性，将使用第一个属性，而不是最具体的属性，这意味着配置的顺序很重要。

### 示例包 {#sample-package}

本教程的结果可在 [自定义网站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 包共享。
