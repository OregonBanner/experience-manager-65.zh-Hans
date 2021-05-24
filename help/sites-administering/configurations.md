---
title: 配置和配置浏览器
description: 了解AEM配置以及它们如何在AEM中管理工作区设置。
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# 配置和配置浏览器{#configuration-browser}

AEM配置用于管理AEM中的设置并用作工作区。

## 什么是配置？{#what-is-a-configuration}

配置可以从两个不同的角度来考虑。

* [管理](#configurations-administrator) 员使用配置作为AEM中的工作区来定义和管理设置组。
* [开发](#configurations-developer) 人员使用底层配置机制来实施配置，以便在AEM中保留和查找设置。

总之：从管理员的角度来看，配置是您如何创建工作区以管理AEM中的设置，而开发人员应该了解AEM如何在存储库中使用和管理这些配置。

无论从何种角度来看，配置在AEM中都有两个主要用途：

* 配置可为特定用户组启用某些功能。
* 配置定义这些功能的访问权限。

## 管理员{#configurations-administrator}的配置

AEM管理员和作者可以将配置视为工作区。 这些工作区可用于通过实施这些功能的访问权限，为组织目的收集设置组及其关联内容。

可以在AEM中为许多不同的功能创建配置。

* [云配置](/help/sites-administering/configurations.md)
* [ContextHub区段](/help/sites-administering/segmentation.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可编辑的模板](/help/sites-authoring/templates.md)

### 示例 {#administrator-example}

例如，管理员可以为可编辑模板创建两个配置。

* WKND-General
* WKND-Magazine

然后，管理员可以使用WKND-General配置创建常规页面模板，然后使用WKND-Magazine下的特定于该杂志的模板。

然后，管理员可以将WKND常规与WKND站点的所有内容关联。 但是，WKND-Magazine配置将仅与杂志网站关联。

通过执行以下操作：

* 当内容作者为杂志创建新页面时，作者可以从常规模板(WKND-General)或杂志模板(WKND-Magazine)中进行选择。
* 当内容作者为网站的其他部分（而非杂志）创建新页面时，作者只能从常规模板(WKND-General)中进行选择。

不仅对可编辑的模板，对于云配置、ContextHub区段和内容片段模型也可进行类似设置。

### 使用配置浏览器{#using-configuration-browser}

通过配置浏览器，管理员可以轻松地在AEM中创建、管理和配置配置配置的访问权限。

>[!NOTE]
>
>仅当用户具有`admin`权限时，才可以使用配置浏览器创建配置。 `admin` 此外，还需要权限才能为配置分配访问权限或以其他方式修改配置。

#### 创建配置{#creating-a-configuration}

在AEM中使用配置浏览器创建新配置非常简单。

1. 作为Cloud Service登录AEM，并从主菜单中选择&#x200B;**工具** -> **常规** -> **配置浏览器**。
1. 点按或单击&#x200B;**创建**。
1. 为您的配置提供&#x200B;**标题**&#x200B;和&#x200B;**名称**。

   ![创建配置](assets/configuration-create.png)

   * **Title**&#x200B;应该是描述性的。
   * **Name**&#x200B;将成为存储库中的节点名称。
      * 它将根据标题自动生成，并根据[AEM命名约定进行调整。](/help/sites-developing/naming-conventions.md)
      * 如有必要，可进行调整。
1. 检查您希望允许的配置类型。
   * [云配置](/help/sites-administering/configurations.md)
   * [ContextHub区段](/help/sites-administering/segmentation.md)
   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可编辑的模板](/help/sites-authoring/templates.md)
1. 点按或单击&#x200B;**创建**。

>[!TIP]
>
>可以嵌套配置。

#### 编辑配置及其访问权限{#access-rights}

如果将配置视为工作区，则可以对这些配置设置访问权限，以强制哪些人可以访问这些工作区，哪些人可能不访问这些工作区。

1. 作为Cloud Service登录AEM，并从主菜单中选择&#x200B;**工具** -> **常规** -> **配置浏览器**。
1. 选择要修改的配置，然后点按或单击工具栏中的&#x200B;**属性**。
1. 选择要添加到配置的任何其他功能
   >[!NOTE]
   >
   >创建配置后，无法取消选择某个特征。
1. 使用&#x200B;**有效权限**按钮可查看角色矩阵以及当前授予配置的权限。
   ![有效权限窗口](assets/configuration-effective-permissions.png)
1. 要分配新权限，请在&#x200B;**添加新权限**&#x200B;部分的&#x200B;**选择用户或组**&#x200B;字段中输入用户或组名称。
   * **选择用户或组**&#x200B;字段根据现有用户和角色提供自动完成功能。
1. 从自动完成结果中选择相应的用户或角色。
   * 您可以选择多个用户或角色。
1. 检查选定用户或角色应具有的访问选项，然后单击&#x200B;**Add**。
   ![向配置添加访问权限](assets/configuration-edit.png)
1. 重复这些步骤以选择用户或角色，并根据需要分配其他访问权限。
1. 完成后，点按或单击&#x200B;**保存并关闭**。

## 开发人员{#configurations-developer}的配置

作为开发人员，了解AEM as a Cloud Service如何与配置一起工作以及如何处理配置解析非常重要。

### 配置与内容的分离{#separation-of-config-and-content}

尽管[管理员和用户可能将配置视为工作场所](#configurations-administrator)来管理不同的设置和内容，但务必要了解，配置和内容由AEM在存储库中单独存储和管理。

* `/content` 是所有内容的主页。
* `/conf` 是所有配置的主页。

内容通过`cq:conf`属性引用其关联的配置。 AEM根据内容及其上下文`cq:conf`属性执行查找，以查找相应的配置。

### 示例 {#developer-example}

在本例中，假设您有一些对DAM设置感兴趣的应用程序代码。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有配置查找的起点都是内容资源，通常位于`/content`下。 这可以是页面、页面内的组件、资产或DAM文件夹。 这是我们要查找的实际内容，其中提供了适用于此上下文的正确配置。

现在，在`Conf`对象的手中，我们可以检索我们感兴趣的特定配置项。 在本例中为`dam/imageserver`，它是与`imageserver`相关的设置集合。 `getItem`调用返回`ValueMap`。 然后，我们读取`bgkcolor`字符串属性，并在属性（或整个配置项）不存在时提供默认值“FFFFF”。

现在，让我们查看相应的JCR内容：

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

在此示例中，我们假定此处有一个WKND特定的DAM文件夹和相应的配置。 从该文件夹`/content/dam/wknd`开始，我们将看到一个名为`cq:conf`的字符串属性，该属性引用应用于子树的配置。 资产文件夹或页面的`jcr:content`中通常会设置该属性。 这些`conf`链接是明确的，因此只需查看CRXDE中的内容，便可轻松跟踪它们。

在`/conf`内跳转，我们会按照引用操作，看到有一个`/conf/wknd`节点。 这是一个配置。 请注意，其查找对应用程序代码完全透明。 示例代码从未具有对它的专用引用，它隐藏在`Conf`对象的后面。 应用的配置通过JCR内容完全控制。

我们看到该配置包含一个名为`settings`的固定节点，该节点包含实际项目，包括我们在本例中需要的`dam/imageserver`。 此类项目可以被视为“设置文档”，通常由`cq:Page`表示，其中包含实际内容的`jcr:content`。

最后，我们看到示例代码所需的属性`bgkcolor`。 我们从`getItem`返回的`ValueMap`基于页面的`jcr:content`节点。

### 配置分辨率{#configuration-resolution}

上述基本示例显示了单个配置。 但是，在很多情况下，您希望具有不同的配置，例如默认全局配置、每个品牌的不同配置，以及子项目的特定配置。

要支持此功能，AEM中的配置查找将按照以下首选项顺序包含继承和回退机制：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 从`/content`中某处的`cq:conf`引用的特定配置
   * 层次结构是任意的，并且可以像您的站点结构一样进行设计，要了解这一点，并非应用程序代码的业务
   * 具有配置权限的用户在运行时可更改
1. `/conf/<siteconfig>/<parentconfig>`
   * 遍历备用配置的父项
   * 具有配置权限的用户在运行时可更改
1. `/conf/<siteconfig>`
   * 遍历备用配置的父项
   * 具有配置权限的用户在运行时可更改
1. `/conf/global`
   * 系统全局设置
   * 通常是安装的全局默认值
   * 由`admin`角色设置
   * 具有配置权限的用户在运行时可更改
1. `/apps`
   * 应用程序默认值
   * 已通过应用程序部署修复
   * 运行时为只读
1. `/libs`
   * AEM产品默认值
   * 仅可按Adobe更改，不允许项目访问
   * 已通过应用程序部署修复
   * 运行时为只读

### 使用配置{#using-configurations}

AEM中的配置基于Sling上下文感知配置。 Sling包提供了一个服务API，可用于获取上下文感知配置。 上下文感知配置是与内容资源或资源树相关的配置，如上一个示例中所述。](#developer-example)[

有关上下文感知配置、示例以及如何使用这些配置的更多详细信息，请[参阅Sling文档。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台{#confmgr-web-console}

出于调试和测试目的，在`https://<host>:<port>/system/console/conf`处有一个&#x200B;**ConfMgr** Web控制台，该控制台可显示给定路径/项目的配置。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **内容路径**
* **项目**
* **用户**

单击&#x200B;**Resolve**&#x200B;查看已解析的配置，并接收将解析这些配置的示例代码。

### 上下文感知配置Web控制台{#context-aware-web-console}

出于调试和测试目的，在`https://<host>:<port>/system/console/slingcaconfig`处有一个&#x200B;**上下文感知配置** Web控制台，该控制台允许查询存储库中的上下文感知配置并查看其属性。

![上下文感知配置Web控制台](assets/configuration-context-aware-console.png)

只需提供：

* **内容路径**
* **配置名称**

单击&#x200B;**Resolve**&#x200B;以检索选定配置的关联上下文路径和属性。
