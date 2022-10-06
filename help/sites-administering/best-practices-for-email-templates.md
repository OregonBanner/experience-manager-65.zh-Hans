---
title: 电子邮件模板最佳实践
seo-title: Best Practices for Email Templates
description: 查找有关在AEM中创建电子邮件模板的最佳实践。
seo-description: Find best practices on creating email templates in AEM.
uuid: 07417a63-7ca6-484c-b55d-57b319428329
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
discoiquuid: 2418777e-4eb2-4d82-aa9e-8d1b0bf740f3
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# 电子邮件模板最佳实践 {#best-practices-for-email-templates}

>[!CAUTION]
>
>AEM电子邮件组件已弃用。 由于电子邮件的性质（将内容和样式合并在一起），AEM提供的现成电子邮件组件对客户的重复使用有限，因为需要在项目所需的任何组件中实施自定义样式。
>
>电子邮件组件可以在项目级别实施，已弃用的AEM电子邮件组件说明了如何实现这一点。 但是，不应在项目中使用这些已弃用的组件。

本文档介绍有关电子邮件设计的一些最佳实践，这些最佳实践可生成一个完善的电子邮件促销活动模板。

AEM中提供的演示营销活动遵循所有这些最佳实践。 介绍了每个最佳实践在演示营销活动中如何实施最佳实践。

创建您自己的新闻稿时，请使用这些最佳实践。

>[!NOTE]
>
>所有营销活动内容均应在 `master` 类型页面 `cq/personalization/components/ambitpage`.
>
>例如，如果计划的营销活动结构类似于
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>您应确保它位于 `master` 页面
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>为Adobe Campaign创建邮件模板时，必须包含属性 **acMapping** 值 **mapRecipient** 在 **jcr:content** 的节点，或者您将无法在 **页面属性** （字段被禁用）。

## 模板/页面组件 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td><p>指定文档类型以确保一致的渲染。</p> <p>在开头添加DOCTYPE(HTML或XHTML)</p> </td>
   <td><p>可通过设计更改 <i>cq:doctype</i> 属性<i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>默认值为“XHTML”：</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可更改为“HTML5”：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字符定义，以确保正确呈现特殊字符。</p> <p>将CHARSET声明（例如iso-8859-15、UTF-8）添加到 &lt;head&gt;</p> </td>
   <td><p>设置为UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用对所有结构进行编码 &lt;table&gt;元素。 对于更复杂的布局，应嵌套表格以构建复杂的结构。</p> <p>即使没有css，电子邮件也应会显示正常。</p> </td>
   <td><p>在整个模板中都使用表来构建内容。 当前最多使用四个嵌套表（1个基表+最大）。 3个嵌套级别)</p> <p>&lt;div&gt; 标记仅在创作模式下使用，以确保正确编辑组件。</p> </td>
  </tr>
  <tr>
   <td>使用元素属性（如单元格内边距、有效值和宽度）设置表尺寸。 这会强制使用框模型结构。</td>
   <td><p>所有表都包含必需的属性，如 <i>边框</i>, <i>cellpadding</i>, <i>单元格间距</i> 和 <i>宽度</i>.</p> <p>要协调表内的元素定位，所有表单元格都具有属性 <i>valign="top"</i> 设置。</p> </td>
  </tr>
  <tr>
   <td><p>考虑移动友好性（如果可能）。 使用媒体查询可增加小屏幕上的文本大小，为链接提供缩览图大小的点击区域。</p> <p>在设计允许的情况下，发送电子邮件作为响应式。</p> </td>
   <td>就CSS样式用于说明演示设计而言，媒体查询用于提供移动设备友好版本。</td>
  </tr>
  <tr>
   <td>内联CSS比将所有CSS放在开头更好。</td>
   <td><p>为了更好地演示基础HTML结构并简化自定义新闻稿结构的可能性，仅插入了一些CSS定义。</p> <p>基本样式和模板变量已提取到 &lt;head&gt; 页面的“隐藏主体”。 在最终提交新闻稿时，这些CSS定义应嵌入到HTML中。 已计划自动启用机制，但目前尚不可用。</p> </td>
  </tr>
  <tr>
   <td>保持CSS简单。 避免使用复合样式声明、简写代码、CSS布局属性、复杂的选择器和伪元素。</td>
   <td>就CSS样式用于说明演示设计而言，正在遵循CSS推荐。</td>
  </tr>
  <tr>
   <td>电子邮件的最大宽度应为600-800像素。 这样，它们就可以在许多客户端提供的预览窗格大小内更好地运行。</td>
   <td>的 <i>宽度</i> 在演示设计中，内容表的像素限制为600像素。</td>
  </tr>
 </tbody>
</table>

### 图像 {#images}

/libs/mcm/campaign/components/image

| **最佳实践** | **实施** |
|---|---|
| 添加 *alt* 图像属性 | 的 *alt* 属性已定义为图像组件的必需属性。 |
| 使用 *jpg* 而不是 *png* 图像格式 | 图像组件将始终作为JPG提供。 |
| 使用 `<img>` 元素而不是表格中的背景图像。 | 模板中不使用背景图像数据。 |
| 在图片上添加属性style=&quot;display block&quot;。 在Gmail上显示良好。 | 默认情况下，所有图像都包含 *style=&quot;display block&quot;* 属性。 |

### 文本和链接 {#text-and-links}

/libs/mcm/campaign/components/heading， /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td>在CSS（字体系列）中使用html而不是样式</td>
   <td>富文本编辑器（例如，在文本时间组件中）现在支持选择字体系列和字体大小并将其应用于选定的文本。 它们将呈现为标记。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字体，例如 <i>佐治亚韦尔达纳亚里尔</i> 和 <i>《泰晤士报新罗马报》</i>.</td>
   <td><p>取决于新闻稿的设计。</p> <p>在演示设计中，使用了字体“Helvetica”，但将回退到通用的无衬线字体（如果不存在）。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳实践** | **实施** |
|---|---|
| 使用W3C验证器更正HTML代码。 确保已正确关闭所有打开的标记。 | 已验证代码。 对于XHTML过渡Doctype，仅 `<html>` 元素缺失。 |
| 无需费心使用JavaScript或Flash — 这些技术基本上不受电子邮件客户端的支持。 | 新闻稿模板中不使用JavaScript和Flash。 |
| 为多部分发送添加纯文本版本。 | 已在页面属性中构建了一个新小组件，以便轻松地从页面内容中提取纯文本版本。 这可用作最终纯文本版本的起点。 |

## Campaign新闻稿模板和示例 {#campaign-newsletter-templates-and-examples}

AEM随附了多个模板和组件，供您开箱即用来创建营销活动新闻稿。 您可以使用这些模板和组件创建自定义新闻稿。

### 模板 {#templates}

为了提供坚实的基础并扩大各种内容流可能性，开箱即用的模板类型有三种略有不同。 您可以轻松使用这些组件来构建自定义新闻稿。

所有 **标题**, a **页脚** 和 **身体** 中。 在正文部分下方，每个模板在 **列设计** （1列、2列或3列）。

![](assets/chlimage_1-69.png)

### 组件 {#components}

当前 [可在营销活动模板中使用的七个组件](/help/sites-authoring/adobe-campaign-components.md). 这些组件都基于Adobe标记语言 **HTL**.

| **组件名称** | **组件路径** |
|---|---|
| 标题 | /libs/mcm/campaign/components/heading |
| 图像 | /libs/mcm/campaign/components/image |
| 文本与个性化 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 链接 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(以前称为Scene7)图像模板 | /libs/mcm/campaign/s7image |
| 目标参考 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>这些组件针对邮件内容进行了优化；也就是说，他们遵循本文档中概述的最佳实践。 使用其他现成的组件通常会违反这些规则。

这些组件在 [Adobe Campaign组件](/help/sites-authoring/adobe-campaign-components.md).
