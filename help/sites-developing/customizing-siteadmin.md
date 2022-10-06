---
title: 自定义网站控制台（经典UI）
seo-title: Customizing the Websites Console (Classic UI)
description: 可以扩展“网站管理”控制台以显示自定义列
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

## 将自定义列添加到网站（站点管理）控制台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

可以扩展“网站管理”控制台以显示自定义列。 控制台基于JSON对象构建，可通过创建实施的OSGI服务来扩展该对象 `ListInfoProvider` 界面。 此类服务会修改发送到客户端以构建控制台的JSON对象。

此分步教程介绍如何通过实施 `ListInfoProvider` 界面。 它包括以下步骤：

1. [创建OSGI服务](#creating-the-osgi-service) 并将包含该包的包部署到AEM服务器。
1. （可选） [测试新服务](#testing-the-new-service) 通过发出JSON调用来请求用于构建控制台的JSON对象。
1. [显示新列](#displaying-the-new-column) 扩展存储库中控制台的节点结构。

>[!NOTE]
>
>本教程还可用于扩展以下管理控制台：
>
>* 数字资产控制台
>* 社区控制台
>


### 创建OSGI服务 {#creating-the-osgi-service}

的 `ListInfoProvider` 界面定义了两种方法：

* `updateListGlobalInfo`，要更新列表的全局属性，
* `updateListItemInfo`，以更新单个列表项。

两种方法的参数包括：

* `request`，关联的Sling HTTP请求对象，
* `info`，要更新的JSON对象（分别为全局列表或当前列表项）
* `resource`, Sling资源。

以下实施示例：

* 添加 *星星* 属性， `true` 如果页面名称以 *e*&#x200B;和 `false` 否则。

* 添加 *stardesCount* 属性，该属性对于列表是全局的，并包含有星号的列表项数。

要创建OSGI服务，请执行以下操作：

1. 在CRXDE Lite中， [创建包](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
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
>* 如果 `ListInfoProvider` 实施定义了响应对象中已存在的属性，其值将被您提供的值覆盖。
>
>  您可以使用 [服务排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 管理多个 `ListInfoProvider` 实施。

### 测试新服务 {#testing-the-new-service}

当您打开网站管理控制台并浏览您的网站时，浏览器将发出ajax调用，以获取用于构建控制台的JSON对象。 例如，当您浏览 `/content/geometrixx` 文件夹，则会将以下请求发送到AEM服务器以构建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要确保在部署包含新服务的包后，新服务正在运行：

1. 将您的浏览器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 响应应按如下方式显示新属性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 显示新列 {#displaying-the-new-column}

最后一步是调整“网站管理”控制台的节点结构，以通过叠加来显示所有Geometrixx页面的新属性 `/libs/wcm/core/content/siteadmin`. 请按如下方式继续：

1. 在CRXDE Lite中，创建节点结构 `/apps/wcm/core/content` 节点类型 `sling:Folder` 以反映结构 `/libs/wcm/core/content`.

1. 复制节点 `/libs/wcm/core/content/siteadmin` 并粘贴到下面 `/apps/wcm/core/content`.

1. 复制节点 `/apps/wcm/core/content/siteadmin/grid/assets` to `/apps/wcm/core/content/siteadmin/grid/geometrixx` 并更改其属性：

   * 删除 **pageText**

   * 已设置 **pathRegex** to `/content/geometrixx(/.*)?`
这将使所有geometrixx网站的网格配置处于活动状态。

   * 已设置 **storeProxySuffix** to `.pages.json`

   * 编辑 **storeReaderFields** 多值属性并添加 `starred` 值。

   * 要激活MSM功能，请将以下MSM参数添加到多字符串属性 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 添加 `starred` 节点（类型） **nt：非结构化**&#x200B;下面) `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 具有以下属性：

   * **dataIndex**: `starred` 字符串类型

   * **标题**: `Starred` 字符串类型

   * **xtype**: `gridcolumn` 字符串类型

1. （可选）拖放您不希望在 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虚路径，默认情况下，该路径指向 `/libs/wcm/core/content/siteadmin`.
要将此重定向到您的siteadmin版本，请在 `/apps/wcm/core/content/siteadmin` 定义属性 `sling:vanityOrder` 的值大于 `/libs/wcm/core/content/siteadmin`. 默认值为300，因此任何更高的值都适合。

1. 转到网站管理控制台，然后导航到Geometrixx站点：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 名为的新列 **星号** 可用，按如下方式显示自定义信息：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多个网格配置与 **pathRegex** 属性中，将使用第一个属性，而不是最具体的属性，这意味着配置的顺序很重要。

### 示例包 {#sample-package}

本教程的结果可在 [自定义网站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 包共享。
