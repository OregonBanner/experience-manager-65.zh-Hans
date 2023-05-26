---
title: 配置布局容器和布局模式
seo-title: Configuring Layout Container and Layout Mode
description: 了解如何配置布局容器和布局模式。
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 3%

---

# 配置布局容器和布局模式{#configuring-layout-container-and-layout-mode}

[响应式布局](/help/sites-authoring/responsive-layout.md) 是一种实现机制 [响应式网页设计](https://en.wikipedia.org/wiki/Responsive_web_design). 这允许用户创建网页，这些网页的布局和维度取决于其用户使用的设备。

>[!NOTE]
>
>这可以与 [移动Web](/help/sites-developing/mobile-web.md) 机制，使用自适应Web设计（主要用于经典UI）。

AEM 使用一组机制为页面实现响应式布局：

* [**布局容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;组件

   此组件提供了一个网格段落系统，允许您在响应式网格内添加和放置组件。 它可以用作页面的默认parsys和/或在组件浏览器中提供给作者。

   * 默认 **布局容器** 组件定义于：

      /libs/wcm/foundation/components/responsivegrid

   * 您可以定义布局容器：

      * 作为用户可以添加到页面的组件。
      * 作为页面的默认parsys。
      * 两者。

         您可以将布局容器作为页面的标准，同时允许用户在此中添加更多布局容器；例如，实现列控件。

* **[布局模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
将布局容器放置到页面上后，您可以使用 
**版面** 模式，用于将内容定位在响应式网格中。

* [**模拟器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
这允许您创建和编辑响应式网站，这些网站可通过以交互方式调整组件大小，根据设备/窗口大小重新排列布局。 然后，用户可以使用模拟器查看内容的呈现方式。

>[!CAUTION]
>
>尽管 **布局容器** 组件在经典UI中可用，其完整功能仅在触屏UI中可用。

借助这些响应式网格机制，您可以：

* 使用断点（指示设备分组）根据设备布局定义不同的内容行为。
* 根据设备组隐藏组件（定义组件将在哪个断点上隐藏）。
* 使用水平对齐网格功能（将组件放入网格中，根据需要调整大小，定义它们何时应折叠/重排成并排或上下对齐）。
* 实现列控件。

>[!NOTE]
>
>在开箱即用的安装中，已为 [We.Retail引用站点](/help/sites-developing/we-retail.md). 你还是必须的 [激活布局容器组件](#enable-the-layout-container-component-for-page) 用于其他页面。

## 配置响应式模拟器 {#configuring-the-responsive-emulator}

此任务允许您查看响应式 **模拟器** 在您的网站上。

### 注册页面组件以进行模拟 {#register-your-page-components-for-emulation}

要使模拟器支持您的页面，您必须注册页面组件。 参见 [注册用于模拟的页面组件](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### 指定设备组 {#specify-the-device-groups}

要指定显示在模拟器的“设备”列表中的设备组，请参阅 [指定设备组](/help/sites-developing/responsive.md#specifying-the-device-groups).

### 将您的站点链接到指定的设备组 {#link-your-site-to-the-specified-device-groups}

要包含模拟器，请将您的站点链接到设备组。 参见 [添加设备列表](/help/sites-developing/responsive.md#adding-the-devices-list) （适用于经典UI和触屏优化UI）。

## 激活网站的布局模式 {#activate-layout-mode-for-your-site}

这些过程用于启用 **版面** 模式。

### 配置断点 {#configure-the-breakpoints}

[断点](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 在响应式设计中使用。
* 可以定义：

   * 在页面模板上，设置会从中复制到使用该模板创建的任何页面。
   * 在页面节点上，任何子页面都会从中继承设置。

* 定义标题和宽度：

   * 标题描述通用设备分组，必要时提供方向；例如，手机、平板电脑、表格横向。
   * 宽度定义了该通用设备分组的最大宽度（以像素为单位）。 例如，如果断点电话的宽度为768，则表示它是用于电话设备的最大布局宽度。

* 使用模拟器时，在页面编辑器顶部显示为标记。
* 继承自父节点层次结构，可以随意覆盖。
* 有一个默认（开箱即用）断点，它涵盖了最后一个断点以上所有断点 *已配置* 断点。

它们可以使用CRXDE Lite或XML进行定义。

>[!NOTE]
>
>如果您要设置新项目：
>
>* 向模板添加断点。
>
>如果要迁移现有项目（包含现有内容），您必须：
>
>* 向模板添加断点
>* 将相同的断点添加到现有页面
>
>  由于继承正在进行，您可以将其限制为内容的根页面。

#### 使用CRXDE Lite配置断点 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或等效项），导航到：

   * 您的模板定义。
   * 此 `jcr:content` 节点。

1. 下 `jcr:content` 创建节点：

   * 名称: `cq:responsive`
   * 类型: `nt:unstructured`

1. 在此下创建节点：

   * 名称: `breakpoints`
   * 类型: `nt:unstructured`

1. 在断点节点下，可以创建任意数量的断点。 每个定义都是一个具有以下属性的节点：

   * 名称: `<descriptive name>`
   * 类型: `nt:unstructured`
   * 标题: `String` * `<descriptive title seen in Emulator>`*
   * 宽度: `Decimal` * `<value of breakpoint>`*

#### 使用XML配置断点 {#configuring-breakpoints-using-xml}

断点位于 `<jcr:content>` 部分 `.context.html` 在相应的模板（或内容）文件夹下。

示例定义：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 添加响应信息提供程序 {#add-a-responsive-information-provider}

>[!NOTE]
>
>仅当页面组件不是基于基础页面组件时，才需要此项。

复制以下内容 `cq:infoProviders` 将节点结构放入父页面组件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 为页面启用组件调整大小 {#enable-component-resizing-for-the-page}

这些过程是必需的，这样您便可以在 **版面** 模式。

### 将布局容器设置为主Parsys {#set-layout-container-as-main-parsys}

要将页面的main parsys设置为布局容器，请将parsys定义为：

`wcm/foundation/components/responsivegrid`

在：

* 页面组件
* 页面模板（供将来使用）

以下两个示例说明了定义：

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP：**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### 包含响应式CSS {#include-the-responsive-css}

#### 使用LESS的断点的CSS {#css-for-breakpoints-using-less}

AEM使用LESS来生成必要CSS的各个部分，这些项目需要包含这些部分。

您还必须创建 [客户端库](https://experienceleague.adobe.com/docs/) 以提供额外的配置和函数调用。 以下LESS提取是必须添加到项目的最小值示例：

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

可在以下位置找到基本网格定义：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 样式设置注意事项 {#styling-considerations}

根据响应式网格大小调整保持在响应式容器内的组件(连同它们各自的HTMLDOM元素)的大小。 因此，在这些情况下，建议避免（或更新）固定宽度（包含）DOM元素的定义。

例如：

* 之前:

   * `width=100px`

* 之后:

   * `max-width=100px`

#### 调整大小和自适应图像符合性 {#resizing-and-adaptive-image-compliance}

在网格内对组件大小的任何调整都将相应地触发以下监听器：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

要正确调整响应式网格中包含的自适应图像的大小并更新其内容，您需要添加 `afterEdit` 设置为 `REFRESH_PAGE` 侦听器进入 `EditConfig` 每个包含的组件的文件。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

该自适应图像机制可通过控制为窗口的当前大小选择正确图像的脚本来提供。 它在DOM准备就绪或收到专用事件时激活。 当前必须刷新页面才能正确反映用户操作的结果。

>[!CAUTION]
>
>自定义样式表clientlibs必须作为标头的一部分加载，它们才能在创作和发布中正常工作。

## 为页面启用布局容器组件 {#enable-the-layout-container-component-for-page}

这些任务允许作者拖动 **布局容器** 组件放到页面上。

### 启用布局容器组件以进行页面编辑 {#enable-the-layout-container-component-for-page-editing}

要允许作者进一步向内容页面添加响应式网格，您需要为页面启用布局容器组件。 您可以使用以下任一方式执行此操作：

* **创作环境**

   使用 [设计模式](/help/sites-authoring/default-components-designmode.md) 以激活 **图层容器** 页面组件。

* **组件定义**

   使用 `allowedComponent` 或定义组件时的静态include。

### 配置布局容器的网格 {#configure-the-grid-of-the-layout-container}

您可以配置可用于布局容器每个特定实例的列数：

1. **创作环境**

   您可以配置可用于布局容器每个特定实例的列数。

   要执行此操作，请使用 [设计模式](/help/sites-authoring/default-components-designmode.md)，然后打开所需容器的“设计”对话框。 您可以在此指定有多少列可用于定位和大小调整。 默认值为12。

1. **XML**

   响应式网格的定义指定于：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定义以下参数：

   * 可用列数：

      * `columns="{String}8"`
   * 可添加到当前组件的组件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
