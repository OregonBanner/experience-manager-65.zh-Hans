---
title: 自定义创建通信UI
seo-title: 自定义创建通信UI
description: 了解如何自定义创建通信UI。
seo-description: 了解如何自定义创建通信UI。
uuid: 9dee9b6f-4129-4560-9bf8-db48110b76f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 13a93111-c08c-4457-b69a-a6f6eb6da330
docset: aem65
feature: 通信管理
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 0%

---

# 自定义创建通信UI{#customize-create-correspondence-ui}

## 概述 {#overview}

通信管理允许您重新品牌化其解决方案模板，以提升品牌价值并遵守贵组织的品牌标准。 重新品牌化用户界面包括更改组织徽标，该徽标显示在“创建通信”UI的左上角。

您可以使用贵组织的徽标更改“创建通信”UI中的徽标。

![创建通信UI中的自定义图标](assets/0_1_introscreenshot.png)

创建通信UI中的自定义图标

### 更改创建通信UI {#changing-the-logo-in-the-create-correspondence-ui}中的徽标

要设置您选择的徽标图像，请执行以下操作：

1. 在CRX](#creatingfolderstructure)中创建相应的[文件夹结构。
1. [在您在CRX中创](#uploadlogo) 建的文件夹中上传新的徽标文件。

1. [在CRX上](#createcss) 设置CSSon以引用新徽标。
1. 清除浏览器历史记录，然后[刷新创建通信UI](#refreshccrui)。

## 创建所需的文件夹结构 {#creatingfolderstructure}

创建文件夹结构（如下所述），用于托管自定义徽标图像和样式表。 根文件夹/apps的新文件夹结构与/libs文件夹的结构类似。

对于任何自定义设置，请在/apps分支中创建一个并行文件夹结构，如下所述。

/apps分支（文件夹结构）：

* 确保文件在系统更新时是安全的。 如果是升级、功能包或热修复程序，则会更新/libs分支，如果您在/libs分支中托管更改，则会覆盖这些更改。
* 帮助您不打扰当前系统/分支，如果您使用默认位置存储自定义文件，则可能会出错解决该问题。
* 在AEM搜索资源时，可帮助您的资源获得更高的优先级。 AEM配置为先搜索/apps分支，然后搜索/libs分支以查找资源。 此机制表示系统使用您的叠加（以及在此处定义的自定义设置）。

请按照以下步骤在/apps分支中创建所需的文件夹结构：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为`css`的文件夹，其路径/结构与css文件夹类似（位于ccrui文件夹中）。

   创建css文件夹的步骤：

   1. 右键单击以下路径中的&#x200B;**css**&#x200B;文件夹，然后选择&#x200B;**覆盖节点**:`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![覆盖节点](assets/1_overlaynode_css.png)

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

      ![覆盖节点路径](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >请勿在/libs分支中进行更改。 您所做的任何更改都可能会丢失，因为当您执行以下操作时，此分支将容易发生更改：
      >
      >    
      >    
      >    * 在实例上升级
      >    * 应用热修复程序
      >    * 安装功能包


   1. 单击&#x200B;**确定**。在指定的路径中创建css文件夹。



1. 在apps文件夹中，创建一个名为`imgs`的文件夹，其路径/结构与imgs文件夹（位于ccrui文件夹中）类似。

   1. 右键单击以下路径中的&#x200B;**imgs**&#x200B;文件夹，然后选择&#x200B;**覆盖节点**:`/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

   1. 单击&#x200B;**确定**。

      >[!NOTE]
      >
      >您还可以在/apps文件夹中手动创建文件夹结构。

1. 单击&#x200B;**Save All**&#x200B;以在服务器上保存更改。

## 将新徽标上传到CRX {#uploadlogo}

将您的自定义徽标文件上传到CRX。 标准HTML规则控制徽标的呈现。 支持的图像文件格式取决于您用来访问AEM Forms的浏览器。 所有浏览器都支持JPEG、GIF和PNG。 有关更多信息，请参阅特定于浏览器的有关支持的图像格式的文档。

* 徽标图像的默认尺寸为48 px * 48 px。 确保图像与此大小相似或大于48 px * 48 px。
* 如果徽标图像的高度大于50像素，则“创建通信”用户界面会将图像向下缩放到最大高度50像素，因为这是标题的高度。 缩小图像时，“创建通信”用户界面会保持图像的宽高比。
* 如果图像较小，则“创建通信”用户界面不会放大图像，因此请确保您使用的徽标图像高度至少为48像素，并且宽度足够清晰。

请按照以下步骤将自定义徽标文件上传到CRX:

1. 转到 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，请以管理员身份登录。
1. 在CRXDE中，右键单击以下路径中的&#x200B;**imgs**&#x200B;文件夹，然后选择&#x200B;**创建>创建文件**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![在imgs文件夹中创建新节点](assets/2_contentexplorernewnode.png)

1. 在“创建文件”对话框中，输入CustomLogo.png文件的名称（或您的徽标文件的名称）。

   ![CustomLogo.png作为新节点](assets/3_contentexplorernewnode_customlogo.png)

1. 单击&#x200B;**Save All**。

   在您创建的新文件（此处为CustomLogo.png）下，将显示jcr:content属性。

1. 在文件夹结构中单击jcr:content。

   将显示jcr:content的属性。

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. 双击&#x200B;**jcr:data**&#x200B;属性。

   此时会出现“编辑jcr:data”对话框。

   现在，单击newlogo.png文件夹，双击jcr:content（dim选项）并设置类型nt:resource。 如果不存在，请创建名为jcr:content的属性。

1. 在“编辑jcr:data”对话框中，单击&#x200B;**浏览**&#x200B;并选择要用作徽标的图像文件（此处为CustomLogo.png）。

   支持的图像文件格式取决于您用来访问AEM Forms的浏览器。 所有浏览器都支持JPEG、GIF和PNG。 有关更多信息，请参阅特定于浏览器的有关支持的图像格式的文档。

   ![示例自定义徽标文件](assets/geometrixx-outdoors.png)

   示例：CustomLogo.png用作自定义徽标

1. 单击&#x200B;**Save All**。

## 创建CSS以将徽标与UI集成 {#createcss}

自定义徽标图像要求在内容上下文中加载其他样式表。

使用以下步骤设置样式表以呈现徽标：

1. 转到 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，请以管理员身份登录。
1. 在以下位置创建名为customcss.css的文件（不能使用其他文件名）：

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   创建customcss.css文件的步骤：

   1. 右键单击&#x200B;**css**&#x200B;文件夹，然后选择&#x200B;**创建>创建文件**。
   1. 在“新建文件”对话框中，将CSS的名称指定为`customcss.css`（不能使用其他文件名），然后单击&#x200B;**确定**。
   1. 将以下代码添加到新创建的css文件。 在代码的content:url中，指定您已上传到CRXDE中的imgs文件夹的图像名称。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 单击&#x200B;**Save All**。

## 刷新创建通信UI以查看自定义徽标 {#refreshccrui}

清除浏览器缓存，然后在浏览器中打开创建通信UI实例。 您应会看到自定义徽标。

![使用自定义徽标创建通信用户界面](assets/0_1_introscreenshot-1.png)

创建通信UI中的自定义图标
