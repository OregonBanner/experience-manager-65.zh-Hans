---
title: 配置和配置浏览器
description: 了解AEM配置以及它们如何管理AEM中的工作区设置。
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 6%

---

# 配置和配置浏览器 {#configuration-browser}

AEM配置用于管理AEM中的设置，并用作工作区。

## 什么是配置？ {#what-is-a-configuration}

可以从两个不同的观点考虑配置。

* [管理员](#configurations-administrator) 使用配置作为AEM中的工作区来定义和管理设置组。
* [开发人员](#configurations-developer) 使用实现配置的底层配置机制来在AEM中保留和查找设置。

简而言之：从管理员的角度来看，配置是您创建工作区以管理AEM中的设置的方式，而开发人员应该了解AEM如何在存储库中使用和管理这些配置。

从您的角度来看，配置在AEM中有两个主要用途：

* 配置可为某些用户组启用某些功能。
* 配置定义这些功能的访问权限。

## 管理员配置 {#configurations-administrator}

AEM管理员和作者可以将配置视为工作区。 通过实施这些功能的访问权限，这些工作区可用于收集设置组及其关联内容以进行组织。

可为AEM中的许多不同功能创建配置。

* [云配置](/help/sites-administering/configurations.md)
* [上下文中心区段](/help/sites-administering/segmentation.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可编辑模板](/help/sites-authoring/templates.md)

### 示例 {#administrator-example}

例如，管理员可以为可编辑模板创建两个配置。

* WKND常规
* WKND — 杂志

随后，管理员可以使用WKND-General配置创建常规页面模板，然后使用WKND-Magazine下特定于杂志的模板。

然后，管理员可以将WKND-General与WKND网站的所有内容相关联。 但是，WKND-Magazine配置只会与杂志站点相关联。

通过执行此操作：

* 当内容作者为杂志创建页面时，作者可以从常规模板(WKND-General)或杂志模板(WKND-Magazine)中进行选择。
* 当内容作者为网站的非杂志其他部分创建页面时，作者只能从常规模板(WKND-General)中进行选择。

类似设置不仅适用于可编辑模板，也适用于云配置、ContextHub区段和内容片段模型。

### 使用配置浏览器 {#using-configuration-browser}

通过配置浏览器，管理员可以轻松地创建、管理和配置对AEM中配置的访问权限。

>[!NOTE]
>
>仅当您的用户具有 `admin` 权限。 还需要管理员权限才能为配置分配访问权限或修改配置。

#### 创建配置 {#creating-a-configuration}

使用配置浏览器，可以在AEM中轻松创建配置。

1. 登录AEMas a Cloud Service，从主菜单选择 **工具** -> **常规** -> **配置浏览器**.
1. 点按或单击&#x200B;**创建**。
1. 提供配置的&#x200B;**标题**&#x200B;和&#x200B;**名称**。

   ![创建配置](assets/configuration-create.png)

   * **标题**&#x200B;应为描述性的。
   * **名称**&#x200B;会成为存储库中的节点名称。
      * 它会根据标题自动生成，并根据 [AEM 命名约定](/help/sites-developing/naming-conventions.md)进行调整。
      * 如有必要可以调整。
1. 检查要允许的配置类型。
   * [云配置](/help/sites-administering/configurations.md)
   * [上下文中心区段](/help/sites-administering/segmentation.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可编辑模板](/help/sites-authoring/templates.md)
1. 点按或单击&#x200B;**创建**。

>[!TIP]
>
>配置可以嵌套。

#### 编辑配置及其访问权限 {#access-rights}

如果您将配置视为工作区，则可以对这些配置设置访问权限，以强制执行谁可以访问这些工作区，谁不能访问这些工作区。

1. 登录AEMas a Cloud Service，从主菜单选择 **工具** -> **常规** -> **配置浏览器**.
1. 选择要修改的配置，然后点按或单击 **属性** 工具栏中。
1. 选择要添加到配置的任何其他功能。

   >[!NOTE]
   >
   >创建配置后，无法取消选择功能。

1. 使用 **有效权限** 按钮以查看角色列表以及当前向配置授予哪些权限。
   ![有效权限窗口](assets/configuration-effective-permissions.png)
1. 要分配新权限，请在 **选择用户或组** 中的字段 **添加新权限** 部分。
   * 此  **选择用户或组** 字段提供基于现有用户和角色的自动完成功能。
1. 从自动完成结果中选择相应的用户或角色。
   * 您可以选择多个用户或角色。
1. 选中所选用户或角色应具有的访问选项，然后单击 **添加**.
   ![向配置添加访问权限](assets/configuration-edit.png)
1. 重复这些步骤，以便您可以选择用户或角色，并根据需要分配其他访问权限。
1. 选择 **保存并关闭** 等你完事了。

## 作为开发人员的配置 {#configurations-developer}

作为开发人员，了解AEMas a Cloud Service如何处理配置以及它如何处理配置解析非常重要。

### 配置和内容分离 {#separation-of-config-and-content}

尽管 [管理员和用户可能会将配置视为工作区](#configurations-administrator) 要管理不同的设置和内容，请务必了解配置和内容由AEM在存储库中单独存储和管理。

* `/content` 是所有内容的家园。
* `/conf` 是所有配置的主页。

内容通过引用其关联的配置 `cq:conf` 属性。 AEM根据内容及其上下文执行查找 `cq:conf` 属性以查找相应的配置。

### 示例 {#developer-example}

对于此示例，假设您有一些应用程序代码对DAM设置感兴趣。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有配置查找的起点是下的内容资源 `/content`. 这可以是页面、页面内的组件、资产或DAM文件夹。 这是您正在为其查找适用于此上下文的正确配置的实际内容。

现在，使用 `Conf` 对象中，您可以检索您感兴趣的特定配置项目。 在这种情况下，它是 `dam/imageserver`，这是与关联的设置的集合。 `imageserver`. 此 `getItem` 调用返回 `ValueMap`. 然后，您阅读 `bgkcolor` 字符串属性，并在属性（或整个配置项）不存在的情况下提供默认值“FFFFFF”。

现在，我们来看看相应的JCR内容：

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

在此示例中，您可以在此处假定具有WKND特定的DAM文件夹以及相应的配置。 从该文件夹开始 `/content/dam/wknd`，您可以看到有一个名为的字符串属性 `cq:conf` 引用应用于子树的配置。 属性设置在 `jcr:content` 资源文件夹或页面的URL值。 这些 `conf` 链接是明确的，因此只需查看CRXDE中的内容即可轻松跟踪链接。

跳入 `/conf`，您可以按照引用操作，查看其中的 `/conf/wknd` 节点。 这是配置。 它的查找对应用程序代码是透明的。 此示例代码从未有过专用引用，它隐藏在 `Conf` 对象。 要应用哪种配置，可通过JCR内容进行控制。

您可以看到配置包含一个名为的固定名称 `settings` 包含实际项的节点，包括 `dam/imageserver` 你在这个案子中需要的。 此类项目可视为“设置文档”，并由 `cq:Page` 包括 `jcr:content` 保存实际内容。

最后，您可以查看属性 `bgkcolor` 该示例代码需要。 此 `ValueMap` 你从这里回来 `getItem` 基于页面的 `jcr:content` 节点。

### 配置分辨率 {#configuration-resolution}

上述基本示例显示了单个配置。 但在许多情况下，您需要使用不同的配置，例如默认的全局配置、每个品牌的不同配置，以及子项目的特定配置。

为了支持这一点，AEM中的配置查找具有按照以下优先顺序排列的继承和回退机制：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 引用的特定配置 `cq:conf` 在中的某个位置 `/content`
   * 层次结构是任意的，可以像网站结构一样设计，知道这一点不是应用程序代码的业务
   * 可由具有配置权限的用户在运行时更改
1. `/conf/<siteconfig>/<parentconfig>`
   * 遍历父项以获取回退配置
   * 可由具有配置权限的用户在运行时更改
1. `/conf/<siteconfig>`
   * 遍历父项以获取回退配置
   * 可由具有配置权限的用户在运行时更改
1. `/conf/global`
   * 系统全局设置
   * 安装的全局默认值
   * 由设置 `admin` 角色
   * 可由具有配置权限的用户在运行时更改
1. `/apps`
   * 应用程序默认值
   * 通过应用程序部署修复了
   * 运行时只读
1. `/libs`
   * AEM产品默认值
   * 仅可按Adobe更改，不允许项目访问
   * 通过应用程序部署修复了
   * 运行时只读

### 使用配置 {#using-configurations}

AEM中的配置基于Sling上下文感知配置。 Sling捆绑包提供了可用于获取上下文感知配置的服务API。 上下文感知配置是与内容资源或资源树相关的配置 [如上一个示例中所述。](#developer-example)

有关上下文感知配置、示例及其使用方式的更多详细信息， [请参阅Sling文档。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台 {#confmgr-web-console}

出于调试和测试目的，我们提供了 **ConfMgr** Web控制台位于 `https://<host>:<port>/system/console/conf`，可显示给定路径/项目的配置。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **内容路径**
* **项目**
* **用户**

要查看已解析哪些配置并接收解析这些配置的示例代码，请选择 **解决**.

### 上下文感知配置Web控制台 {#context-aware-web-console}

出于调试和测试目的，我们提供了 **上下文感知配置** Web控制台位于 `https://<host>:<port>/system/console/slingcaconfig`，用于查询存储库中的上下文感知配置并查看其属性。

![上下文感知配置Web控制台](assets/configuration-context-aware-console.png)

只需提供：

* **内容路径**
* **配置名称**

要检索所选配置的关联上下文路径和属性，请选择 **解决**.
