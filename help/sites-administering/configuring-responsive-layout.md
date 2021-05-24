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
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---

# 配置布局容器和布局模式{#configuring-layout-container-and-layout-mode}

[响应](/help/sites-authoring/responsive-layout.md) 式布局是实现响应式 [Web设计的机制](https://en.wikipedia.org/wiki/Responsive_web_design)。这允许用户创建布局和维度取决于用户所使用设备的网页。

>[!NOTE]
>
>这可以与[移动Web](/help/sites-developing/mobile-web.md)机制进行比较，后者使用自适应Web设计（主要用于经典UI）。

AEM 使用一组机制为页面实现响应式布局：

* [**布局容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;组件

   此组件提供了一种网格段落系统，让您可以在响应式网格内添加和放置组件。它可用作页面的默认Parsys，和/或在组件浏览器中供作者使用。

   * 默认的&#x200B;**布局容器**&#x200B;组件在下面定义：

      /libs/wcm/foundation/components/responsinggrid

   * 您可以定义布局容器：

      * 作为用户可添加到页面的组件。
      * 作为页面的默认Parsys。
      * 两者.

         您可以将布局容器作为页面的标准容器，同时允许用户在其中添加其他布局容器；例如，实现列控件。

* **[布局](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
模式将布局容器放置到页面上后，即可使用 
**** 布局模式，用于在响应式网格内放置内容。

* [**模拟器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
模拟器让您能够创建并编辑响应式网站，这些网站可以根据设备/窗口大小，通过交互方式调整组件大小来重新安排布局。随后，用户可以使用模拟器查看内容的呈现方式。

>[!CAUTION]
>
>尽管&#x200B;**布局容器**&#x200B;组件在经典UI中可用，但其完整功能仅在触屏UI中可用。

通过这些响应式网格机制，您可以：

* 使用断点（表示设备分组）根据设备布局定义不同的内容行为。
* 根据设备组隐藏组件（定义组件将隐藏的断点）。
* 使用水平对齐网格功能（将组件放入网格中，根据需要调整大小，定义它们何时应该折叠/重排成并排或上下放置的形式）。
* 实现列控件。

>[!NOTE]
>
>在开箱即用的安装中，为[We.Retail引用站点](/help/sites-developing/we-retail.md)配置了响应式布局。 对于其他页面，您仍必须[激活布局容器组件](#enable-the-layout-container-component-for-page)。

## 配置响应式模拟器{#configuring-the-responsive-emulator}

此任务允许您在网站上查看响应式&#x200B;**模拟器**。

### 注册页面组件以进行模拟{#register-your-page-components-for-emulation}

要使模拟器能够支持您的页面，您必须注册页面组件。 请参阅[注册用于模拟的页面组件](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定设备组{#specify-the-device-groups}

要指定在模拟器的“设备”列表中显示的设备组，请参阅[指定设备组](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 将您的站点链接到指定的设备组{#link-your-site-to-the-specified-device-groups}

要包含模拟器，您需要将网站链接到设备组。 请参阅[添加设备列表](/help/sites-developing/responsive.md#adding-the-devices-list)（对于经典UI和触屏优化UI）。

## 激活网站{#activate-layout-mode-for-your-site}的布局模式

在您的网站上，可使用这些过程来启用&#x200B;**布局**&#x200B;模式。

### 配置断点{#configure-the-breakpoints}

[断点](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用于响应式设计。
* 可以定义：

   * 在页面模板上，设置将从中复制到使用该模板创建的任何页面。
   * 在页面节点上，任何子页面都将从中继承设置。

* 定义标题和宽度：

   * 标题描述了通用设备分组，如有需要，具有方向；例如，手机、平板电脑、平板电脑。
   * 宽度定义通用设备分组的最大宽度（以像素为单位）。 例如，如果断点手机的宽度为768，则表示该断点手机设备所使用的布局的最大宽度。

* 使用模拟器时，将作为标记显示在页面编辑器的顶部。
* 继承自父节点层次结构，可以随意覆盖。
* 有一个默认（现成）断点，它涵盖高于最后&#x200B;*配置的*&#x200B;断点的所有断点。

它们可以使用CRXDE Lite或XML进行定义。

>[!NOTE]
>
>如果要设置新项目：
>
>* 您需要向模板添加断点。
>
>
如果您正在迁移现有项目（包含现有内容），则需要：
>
>* 向模板添加断点
>* 向现有页面添加相同的断点

>
>  
继承正在运行中，因此您可以将继承限制为内容的根页面。

#### 使用CRXDE Lite{#configuring-breakpoints-using-crxde-lite}配置断点

1. 使用CRXDE Lite（或等效项），导航到以下任一位置：

   * 您的模板定义。
   * 页面的`jcr:content`节点。

1. 在`jcr:content`下创建节点：

   * 名称: `cq:responsive`
   * 类型: `nt:unstructured`

1. 在此下，创建节点：

   * 名称: `breakpoints`
   * 类型: `nt:unstructured`

1. 在断点节点下，您可以创建任意数量的断点。 每个定义都是一个具有以下属性的节点：

   * 名称: `<descriptive name>`
   * 类型: `nt:unstructured`
   * 标题: `String` * `<descriptive title seen in Emulator>`*
   * 宽度: `Decimal` * `<value of breakpoint>`*

#### 使用XML {#configuring-breakpoints-using-xml}配置断点

断点位于`.context.html`的`<jcr:content>`部分中相应的模板（或内容）文件夹下。

示例定义：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 添加响应信息提供程序{#add-a-responsive-information-provider}

>[!NOTE]
>
>仅当页面组件不基于基础页面组件时，才需要执行此操作。

将以下`cq:infoProviders`节点结构复制到父页面组件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 为页面{#enable-component-resizing-for-the-page}启用组件大小调整功能

这些过程是必需的，因此您可以在&#x200B;**布局**&#x200B;模式下调整组件大小。

### 将布局容器设置为主Parsys {#set-layout-container-as-main-parsys}

要将页面的主Parsys设置为布局容器，您需要将Parsys定义为：

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

#### 使用LESS {#css-for-breakpoints-using-less}的断点的CSS

AEM使用LESS生成部分必要的CSS，这些CSS需要包含在您的项目中。

您还需要创建[客户端库](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html)以提供其他配置和函数调用。 以下LESS提取是您需要添加到项目中的最低值示例：

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

#### 样式注意事项{#styling-considerations}

响应式容器中保留的组件将根据响应式网格大小调整大小（连同其各自的HTML DOM元素）。 因此，在这些情况下，建议避免（或更新）固定宽度（包含）的DOM元素的定义。

例如：

* 之前:

   * `width=100px`

* 之后:

   * `max-width=100px`

#### 调整大小和自适应图像符合性{#resizing-and-adaptive-image-compliance}

在网格中调整组件大小的任何操作都将触发以下监听器（根据需要）：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

要正确调整响应式网格中包含的自适应图像的内容大小并更新其内容，您需要将设置为`REFRESH_PAGE`侦听器的`afterEdit`添加到每个包含组件的`EditConfig`文件中。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

自适应图像机制通过脚本提供，该脚本控制针对窗口的当前大小选择正确图像。 在DOM准备就绪后或收到专用事件时，该活动会激活。 当前必须刷新页面才能正确反映用户操作的结果。

>[!CAUTION]
>
>自定义样式表clientlib必须作为标头的一部分加载，才能在创作和发布时正常工作。

## 为页面{#enable-the-layout-container-component-for-page}启用布局容器组件

这些任务允许作者将&#x200B;**布局容器**&#x200B;组件的实例拖动到页面上。

### 启用布局容器组件以进行页面编辑{#enable-the-layout-container-component-for-page-editing}

要允许作者向内容页面添加更多响应式网格，您需要为页面启用布局容器组件。 您可以使用以下任一方式执行此操作：

* **创作环境**

   使用[设计模式](/help/sites-authoring/default-components-designmode.md)激活页面的&#x200B;**层容器**&#x200B;组件。

* **组件定义**

   定义组件时，请使用`allowedComponent`或静态包含。

### 配置布局容器{#configure-the-grid-of-the-layout-container}的网格

您可以配置每个布局容器特定实例可用的列数：

1. **创作环境**

   您可以配置每个布局容器特定实例可用的列数。

   要实现此目的，请使用[设计模式](/help/sites-authoring/default-components-designmode.md)，然后打开所需容器的设计对话框。 在此，您可以指定多少列可用于定位和调整大小。 默认为 12。

1. **XML**

   响应式网格的定义在中指定：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定义以下参数：

   * 可用列数：

      * `columns="{String}8"`
   * 可添加到当前组件的组件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
