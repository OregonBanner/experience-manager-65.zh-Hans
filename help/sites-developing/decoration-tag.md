---
title: 修饰标记
description: 呈现网页中的组件后，可以生成一个 HTML 元素，以将呈现的组件封装在其中。对于开发人员而言，AEM 可提供清晰而简单的逻辑来控制用于封装所包含组件的修饰标记。
exl-id: d049ebf1-7fa6-4d2c-86f9-b18e107092ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 10%

---

# 修饰标记{#decoration-tag}

呈现网页中的组件后，可以生成一个 HTML 元素，以将呈现的组件封装在其中。这主要用于两个目的：

* 仅当组件与HTML元素封装时，才能编辑组件。
* 封装元素用于应用提供以下内容的HTML类：

   * 布局信息
   * 样式信息

对于开发人员而言，AEM 可提供清晰而简单的逻辑来控制用于封装所包含组件的修饰标记。装饰标签的呈现方式和呈现方式是由两个因素的组合来定义的，本页将深入讨论这两个因素：

* 组件本身可以使用一组属性配置其装饰标记。
* 包含组件（HTL、JSP、调度程序等）的脚本可以使用包含参数来定义装饰标记的方面。

## 推荐 {#recommendations}

以下是有关何时包含包装器元素的一些一般建议，有助于避免遇到意外问题：

* WCMMode（编辑或预览模式）、实例（创作或发布）或环境（暂存或生产）中包装器元素的存在不应有差异，因此页面的CSS和JavaScripts在所有情况下的工作方式均相同。
* 应将包装器元素添加到所有可编辑的组件中，以便页面编辑器能够正确初始化和更新这些组件。
* 对于不可编辑的组件，如果包装元素不提供特定功能，则可以避免该包装元素，因此所得的标记不会不必要的臃肿。

## 组件控件{#component-controls}

以下属性和节点可应用于组件以控制其装饰标记的行为：

* **`cq:noDecoration {boolean}`:** 此属性可添加到组件，如果值为true，则强制AEM不在该组件上生成任何包装器元素。

* **`cq:htmlTag`节点：** 此节点可添加到组件下，并可以具有以下属性：

   * **`cq:tagName {String}`:** 这可用于指定用于封装组件的自定义HTML标记，而不是默认DIV元素。
   * **`class {String}`:** 这可用于指定要添加到包装器的css类名称。
   * 其他属性名称将作为HTML属性添加，其中的字符串值与提供的字符串值相同。

## 脚本控件{#script-controls}

但是，包装器行为确实不同，具体取决于是使用[HTL](/help/sites-developing/decoration-tag.md#htl)还是[JSP](/help/sites-developing/decoration-tag.md#jsp)来包含元素。

### HTL {#htl}

通常，HTL中的包装器行为可概括如下：

* 默认情况下（仅执行`data-sly-resource="foo"`时）不呈现包装器DIV。
* 所有wcm模式（在创作和发布时均禁用、预览、编辑）的呈现方式均相同。

也可以完全控制包装器的行为。

* HTL脚本可完全控制包装器标记的生成行为。
* 组件属性（如`cq:noDecoration`和`cq:tagName`）也可以定义包装器标记。

可以完全控制HTL脚本中包装器标记的行为及其关联逻辑。

有关在HTL中进行开发的更多信息，请参阅[HTL文档](https://docs.adobe.com/content/help/zh-Hans/experience-manager-htl/using/overview.html)。

#### 决策树{#decision-tree}

此决策树将总结用于确定包装器标记行为的逻辑。

![chlimage_1-75](assets/chlimage_1-75a.png)

#### 用例{#use-cases}

以下三个用例提供了如何处理包装器标记的示例，并说明了控制包装器标记的所需行为是多么简单。

以下所有示例都假定具有以下内容结构和组件：

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 用例1:包含用于代码重用的组件{#use-case-include-a-component-for-code-reuse}

最典型的用例是，由于代码重用的原因，组件包含其他组件时。 在这种情况下，不希望包含的组件通过其自己的工具栏和对话框进行编辑，因此不需要包装器，并且将忽略该组件的`cq:htmlTag`。 这可以视为默认行为。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

在`/content/test.html`上生成输出：

**`Hello World!`**

例如，组件包括用于显示图像的核心图像组件，在这种情况下通常使用合成资源，该合成资源包括通过将表示组件将具有的所有属性的映射对象传递到数据 — 资源来包含虚拟子组件。

#### 用例2:包含可编辑的组件{#use-case-include-an-editable-component}

另一个常见用例是容器组件包含可编辑的子组件（如布局容器）时。 在这种情况下，每个包含的子项都必须需要一个包装器才能正常工作（除非使用`cq:noDecoration`属性明确禁用）。

由于包含的组件在本例中是独立组件，因此它需要包装器元素才能使编辑器正常工作，并定义其布局和样式以应用。 要触发此行为，请使用`decoration=true`选项。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

在`/content/test.html`上生成输出：

**`<article class="component-two">Hello World!</article>`**

#### 用例3:自定义行为{#use-case-custom-behavior}

可能存在任意数量的复杂情况，HTL可以明确提供以下内容，从而轻松实现这些复杂情况：

* **`decorationTagName='ELEMENT_NAME'`** 定义包装器的元素名称。
* **`cssClassName='CLASS_NAME'`** 定义要在其上设置的CSS类名称。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

结果输出`/content/test.html`:

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

当包含使用`cq:includ`e或`sling:include`的组件时，AEM中的默认行为是使用DIV来封装元素。 但是，可以通过两种方式自定义此包装：

* 明确告知AEM不要使用`cq:noDecoration`来封装组件。
* 使用自定义HTML标记，使用`cq:htmlTag`/ `cq:tagName`或`decorationTagName`封装组件。

### 决策树{#decision-tree-1}

以下决策树说明了`cq:noDecoration`、`cq:htmlTag`、`cq:tagName`和`decorationTagName`如何影响包装器行为。

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
