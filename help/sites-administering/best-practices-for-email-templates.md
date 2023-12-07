---
title: 电子邮件模板的最佳实践
description: 查找有关在AEM中创建电子邮件模板的最佳实践。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
docset: aem65
exl-id: 6666eddc-dc17-4bd4-9d55-e6522f40a680
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# 电子邮件模板的最佳实践 {#best-practices-for-email-templates}

>[!CAUTION]
>
>本文适用于已弃用的基于Foundation组件的AEM电子邮件组件。
>
>我们鼓励用户使用现代的 [核心组件电子邮件组件。](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

本文档介绍了一些有关电子邮件设计的最佳实践，这些实践最终形成了开发良好的电子邮件营销活动模板。

AEM中提供的演示活动遵循所有这些最佳实践。 对于每种最佳实践，都介绍了如何在演示活动中实施最佳实践。

创建您自己的新闻稿时，请遵循这些最佳实践。

>[!NOTE]
>
>所有营销活动内容都应在 `master` 类型页面 `cq/personalization/components/ambitpage`.
>
>例如，如果您的计划促销活动结构类似于
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>确保它位于 `master` 页面
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>在为Adobe Campaign创建邮件模板时，必须包含资产 **acMapping** 值为 **mapRecipient** 在 **jcr：content** 节点的链接。 如果没有该模板，则无法在中选择Adobe Campaign模板 **页面属性** Experience Manager（字段已禁用）。

## 模板/页面组件 {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td><p>指定文档类型，以确保一致的呈现。</p> <p>在开头添加DOCTYPE(HTML或XHTML)</p> </td>
   <td><p>可按设计更改进行配置 <i>cq：doctype</i> 中的属性<i>“/etc/designs/default/jcr：content/campaign_newsletterpage”</i></p> <p>默认值为“XHTML”：</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可更改为“HTML_5”：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字符定义，以确保正确呈现特殊字符。</p> <p>将CHARSET声明（例如，iso-8859-15、UTF-8）添加到 &lt;head&gt;</p> </td>
   <td><p>设置为UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用对所有结构进行编码 &lt;table&gt;元素。 对于更复杂的布局，应嵌套表以构建复杂的结构。</p> <p>即使没有CSS，电子邮件也应看起来不错。</p> </td>
   <td><p>在整个模板中使用表来结构化内容。 当前最多使用四个嵌套表（1个基表+最大值）。 3个嵌套级别)</p> <p>&lt;div&gt; 标记仅用于创作模式，以确保正确编辑组件。</p> </td>
  </tr>
  <tr>
   <td>使用元素属性（如单元格内边距、有效值和宽度）来设置表格尺寸。 此方法强制使用盒模型结构。</td>
   <td><p>所有表都包含必需属性，如 <i>边框</i>， <i>单元格填充</i>， <i>单元格间距</i>、和 <i>宽度</i>.</p> <p>要协调表内的元素位置，所有表单元格都具有属性 <i>valign="top"</i> 被设置了。</p> </td>
  </tr>
  <tr>
   <td><p>尽可能考虑使用方便移动设备。 使用媒体查询可增加小屏幕上的文本大小，为链接提供缩略图大小的点击区域。</p> <p>如果设计允许，则使电子邮件具有响应性。</p> </td>
   <td>就CSS样式用于说明演示设计而言，媒体查询用于提供对移动设备友好的版本。</td>
  </tr>
  <tr>
   <td>内联CSS比将所有CSS放在开头要好。</td>
   <td><p>为了更好地演示底层HTML结构并便于自定义新闻稿结构，仅内联了一些CSS定义。</p> <p>基本样式和模板变体已提取到中的样式块 &lt;head&gt; 页面的。 在新闻稿最终提交时，这些CSS定义将内联到HTML中。 已计划使用自动内联机制，但目前不可用。</p> </td>
  </tr>
  <tr>
   <td>保持CSS简单。 避免使用复合样式声明、简写代码、CSS布局属性、复杂选择器和伪元素。</td>
   <td>就用于说明演示设计的CSS样式而言，遵循CSS建议。</td>
  </tr>
  <tr>
   <td>电子邮件的最大宽度应为600-800像素。 这种大小调整使它们在许多客户端提供的预览窗格大小范围内表现得更好。</td>
   <td>此 <i>宽度</i> 在演示设计中，内容表的像素限制为600像素。</td>
  </tr>
 </tbody>
</table>

### 图像 {#images}

/libs/mcm/campaign/components/image

| **最佳实践** | **实现** |
|---|---|
| 添加 *alt* 图像的属性 | 此 *alt* 属性已定义为图像组件的必需属性。 |
| 使用 *jpg* 而不是 *png* 图像格式 | 图像始终由图像组件用作JPG。 |
| 使用 `<img>` 元素而不是表格中的背景图像。 | 模板中不使用背景图像数据。 |
| 在图片上添加attribute style=&quot;display block&quot;。 这样一来，它们就能在Gmail上正常显示。 | 所有图像默认包含 *style=&quot;display block&quot;* 属性。 |

### 文本和链接 {#text-and-links}

/libs/mcm/campaign/components/heading， /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td>在CSS(font-family)中使用html而不是样式</td>
   <td>RtfEditor（例如，在文本组件中）现在支持选择字体系列和字体大小并将其应用到所选文本。 它们呈现为标记。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字体，例如 <i>Arial®， Verdana，佐治亚州</i>、和 <i>Times New Roman®</i>.</td>
   <td><p>取决于新闻稿的设计。</p> <p>对于演示设计，使用“Helvetica®”字体，但它会回退到通用无衬线字体（如果不存在）。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳实践** | **实现** |
|---|---|
| 使用W3C验证器更正HTML代码。 确保所有打开的标记均已正确关闭。 | 代码已验证。 仅对于XHTML过渡Doctype，缺少的xmlns属性 `<html>` 缺少元素。 |
| 避免使用JavaScript或Flash — 电子邮件客户端通常不支持这些技术。 | 新闻稿模板中未使用JavaScript或Flash。 |
| 为多部分发送添加纯文本版本。 | 在页面属性中内置了一个新构件，以便轻松地从页面内容中提取纯文本版本。 您可以将其用作最终纯文本版本的起点。 |

## 营销活动新闻稿模板和示例 {#campaign-newsletter-templates-and-examples}

AEM提供了多个现成的模板和组件供您创建Campaign新闻稿。 您可以使用这些模板和组件创建自定义新闻稿。

### 模板 {#templates}

为了提供坚实的基础并拓宽内容流可能性，提供了三种略有不同的现成模板类型。 您可以轻松使用这三种类型来构建自定义新闻稿。

所有客户都有 **标题**， a **页脚**，和 **正文** 部分。 在正文部分的下方，每个模板均不同 **列设计** （一、二或三列）。

![可能的新闻稿的变体](assets/chlimage_1-69.png)

### 组件 {#components}

当前有 [可在营销活动模板中使用的七个组件](/help/sites-authoring/adobe-campaign-components.md). 这些组件都基于Adobe标记语言 **HTL**.

| **组件名称** | **组件路径** |
|---|---|
| 标题 | /libs/mcm/campaign/components/heading |
| 图像 | /libs/mcm/campaign/components/image |
| 文本个性化(&amp;P) | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 链接 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(以前称为Scene7)图像模板 | /libs/mcm/campaign/s7image |
| 目标引用 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>这些组件针对邮件内容进行了优化；也就是说，它们遵循了本文档中概述的最佳实践。 使用其他现成的组件通常违反这些规则。

有关这些组件的详细说明，请参阅 [Adobe Campaign组件](/help/sites-authoring/adobe-campaign-components.md).
