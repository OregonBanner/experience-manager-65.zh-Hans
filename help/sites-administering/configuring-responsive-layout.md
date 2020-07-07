---
title: 配置布局容器和布局模式
seo-title: 配置布局容器和布局模式
description: 了解如何配置布局容器和布局模式。
seo-description: 了解如何配置布局容器和布局模式。
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---


# 配置布局容器和布局模式{#configuring-layout-container-and-layout-mode}

[响应式布局](/help/sites-authoring/responsive-layout.md) 是实现响应式Web [设计的一种机制](https://en.wikipedia.org/wiki/Responsive_web_design)。 这允许用户创建具有根据用户使用的设备而定的布局和尺寸的网页。

>[!NOTE]
>
>这可以与使用自 [适应Web设计](/help/sites-developing/mobile-web.md) （主要针对经典UI）的移动Web机制进行比较。

AEM 使用一组机制为页面实现响应式布局：

* [**布局容器&#x200B;**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)组件

   此组件提供了一种网格段落系统，让您可以在响应式网格内添加和放置组件。它可用作页面的默认parsys和／或在组件浏览器中为作者提供。

   * 默认的 **布局容器** 组件定义在：

      /libs/wcm/foundation/components/responledvegrid

   * 您可以定义布局容器:

      * 作为用户可以添加到页面的组件。
      * 作为页面的默认parsys。
      * 两者.

         您可以将布局容器作为页面的标准，同时允许用户在其中添加更多布局容器; 例如，实现列控件。

* **[布局模](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**式将布局容器放置到页面上后，您就可以使用布局&#x200B;**模式**，在响应式网格内放置内容。

* [**模拟器&#x200B;**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)模拟器让您能够创建并编辑响应式网站，这些网站可以根据设备/窗口大小，通过交互方式调整组件大小来重新安排布局。随后，用户可以使用模拟器查看内容的呈现方式。

>[!CAUTION]
>
>Although the **Layout Container** component is available in the classic UI, its full functionality is only available in the touch-enabled UI.

通过这些响应式网格机制，您可以：

* 使用断点（指示设备分组）根据设备布局定义不同的内容行为。
* 根据设备组隐藏组件（定义将在哪个断点隐藏组件）。
* 使用水平对齐网格功能（将组件放入网格中，根据需要调整大小，定义它们何时应该折叠/重排成并排或上下放置的形式）。
* 实现列控件。

>[!NOTE]
>
>在开箱即用的安装中，已为We.Retail参考站点配 [置响应式布局](/help/sites-developing/we-retail.md)。 您仍必须 [激活其他页面的布局容器](#enable-the-layout-container-component-for-page) 组件。

## 配置响应式模拟器 {#configuring-the-responsive-emulator}

此任务允许您在站点上查看响 **应式** “模拟器”。

### 注册页面组件以进行模拟 {#register-your-page-components-for-emulation}

要使模拟器能够支持您的页面，您必须注册您的页面组件。 请参 [阅注册页面组件以进行模拟](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定设备组 {#specify-the-device-groups}

要指定在模拟器的设备列表中显示的设备组，请参 [阅指定设备组](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 将站点链接到指定的设备组 {#link-your-site-to-the-specified-device-groups}

要包含模拟器，您需要将站点链接到设备组。 请参 [阅添加设备列表](/help/sites-developing/responsive.md#adding-the-devices-list) （适用于经典和触屏优化UI）。

## 激活站点的布局模式 {#activate-layout-mode-for-your-site}

这些过程用于在您的站 **点上启** 用布局模式。

### 配置断点 {#configure-the-breakpoints}

[断点](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用于响应式设计。
* 可以定义：

   * 在页面模板中，设置将从中复制到使用该模板创建的任何页面。
   * 在页面节点上，设置将从中继承到任何子页面。

* 定义标题和宽度：

   * 标题描述了通用设备分组，如果需要，具有方向； 例如，手机、平板电脑、平板电脑横向。
   * 宽度定义该通用设备分组的最大宽度（以像素为单位）。 例如，如果断点电话的宽度为768，则它是电话设备所使用的布局的最大宽度。

* 当您使用模拟器时，页面编辑器顶部的标记将可见。
* 继承自父节点层次结构，可以随意覆盖。
* 有一个默认（现成）断点，它涵盖上次配置的断点之上的所 *有断点* 。

它们可以使用CRXDE Lite或XML进行定义。

>[!NOTE]
>
>如果要设置新项目：
>
>* 您需要向模板添加断点。
>
>
如果要迁移现有项目（包含现有内容），您需要：
>
>* 为模板添加断点
>* 向现有页面添加相同的断点
>
>  
继承正在运行中，您可以将继承限制在内容的根页面。

#### 使用CRXDE Lite配置断点 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或等效产品），导航到以下任一位置：

   * 您的模板定义。
   * 页 `jcr:content` 面的节点。

1. 在 `jcr:content` 创建节点下：

   * 名称: `cq:responsive`
   * 类型: `nt:unstructured`

1. 在此下创建节点：

   * 名称: `breakpoints`
   * 类型: `nt:unstructured`

1. 在断点节点下，您可以创建任意数量的断点。 每个定义都是具有以下属性的单个节点：

   * 名称: `<descriptive name>`
   * 类型: `nt:unstructured`
   * 标题: `String` * `<descriptive title seen in Emulator>`*
   * 宽度: `Decimal` * `<value of breakpoint>`*

#### 使用XML配置断点 {#configuring-breakpoints-using-xml}

断点位于相应 `<jcr:content>` 模板(或 `.context.html` 内容)文件夹下的部分中。

示例定义：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 添加响应式信息提供者 {#add-a-responsive-information-provider}

>[!NOTE]
>
>仅当页面组件不基于基础页面组件时，才需要此设置。

将以下节 `cq:infoProviders` 点结构复制到父页面组件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 为页面启用组件大小调整 {#enable-component-resizing-for-the-page}

这些过程是必需的，因此您可以在布局模式下调整 **组件** 大小。

### 将布局容器设置为主Parsys {#set-layout-container-as-main-parsys}

要将页面的主parsys设置为布局容器，您需要将parsys定义为：

`wcm/foundation/components/responsivegrid`

在以下任一位置：

* 页面组件
* 页面模板（供将来使用）

以下两个示例说明了定义：

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### 包含响应式CSS {#include-the-responsive-css}

#### 使用更少的CSS实现断点 {#css-for-breakpoints-using-less}

AEM使用LESS生成必需CSS的部分，这些项目需要包含在您的项目中。

您还需要创建一个客 [户端库](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) ，以提供其他配置和函数调用。 以下LESS提取是您需要添加到项目中的最低值示例：

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

基本网格定义可在以下位置找到：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 样式注意事项 {#styling-considerations}

响应式容器中保留的组件将根据响应式网格大小调整大小（连同其各自的HTML DOM元素）。 因此，在这些情况下，建议避免（或更新）固定宽度（包含）DOM元素的定义。

例如：

* 之前:

   * `width=100px`

* 之后:

   * `max-width=100px`

#### 调整大小和自适应图像符合性 {#resizing-and-adaptive-image-compliance}

在网格中调整组件大小时，将触发以下监听器（视情况而定）:

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

要正确调整响应式网格中包含的自适应图像内容的大小和更新其内容，您需要将一个集 `afterEdit` 合添加 `REFRESH_PAGE` 到每个包含 `EditConfig` 的组件的文件中。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

自适应图像机制通过控制根据窗口的当前大小选择正确图像的脚本使用。 在DOM准备就绪后或在收到专用事件时激活。 当前，必须刷新页面才能正确反映用户操作的结果。

>[!CAUTION]
>
>必须将自定义样式表客户端库作为标题的一部分加载，才能在创作和发布时正常工作。

## 为页面启用布局容器组件 {#enable-the-layout-container-component-for-page}

这些任务允许作者将布局容器组 **件的实例** 拖动到页面上。

### 启用布局容器组件进行页面编辑 {#enable-the-layout-container-component-for-page-editing}

要允许作者向内容页面添加响应式网格，您需要为页面启用布局容器组件。 您可以使用以下任一方式执行此操作：

* **创作环境**

   使用 [设计模式](/help/sites-authoring/default-components-designmode.md) ，为页面 **激活图** 层容器组件。

* **组件定义**

   在定 `allowedComponent` 义组件时使用或静态包含。

### 配置布局容器的网格 {#configure-the-grid-of-the-layout-container}

您可以配置布局容器的每个特定实例的可用列数：

1. **创作环境**

   您可以配置每个特定布局容器实例的可用列数。

   为此，请使用 [设计模式](/help/sites-authoring/default-components-designmode.md)，然后打开所需容器的设计对话框。 您可以在此处指定有多少列可用于定位和调整大小。 默认为 12。

1. **XML**

   响应式网格的定义在中指定：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定义以下参数：

   * 可用列数：

      * `columns="{String}8"`
   * 可添加到当前组件的组件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


