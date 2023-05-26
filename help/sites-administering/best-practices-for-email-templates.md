---
title: 电子邮件模板的最佳实践
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

# 电子邮件模板的最佳实践 {#best-practices-for-email-templates}

>[!CAUTION]
>
>已弃用AEM电子邮件组件。 由于电子邮件将内容和样式结合在了一起，因此由AEM提供的现成可用电子邮件组件对于客户的重用受到限制，因为需要将自定义样式实施到项目所需的任何组件中。
>
>可以在项目级别实施电子邮件组件，已弃用的AEM电子邮件组件说明了如何实现这一点。 但是，这些已弃用的组件不应在项目中使用。

本文档介绍了一些有关电子邮件设计的最佳实践，这些实践最终形成了完善的电子邮件营销活动模板。

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
>您应确保它位于 `master` 页面
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>为Adobe Campaign创建邮件模板时，必须包含资产 **acMapping** 具有值 **mapRecipient** 在 **jcr：content** 节点，否则您将无法在中选择Adobe Campaign模板 **页面属性** AEM （字段已禁用）。

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
   <td><p>可按设计更改进行配置 <i>cq：doctype</i> 中的属性<i>“/etc/designs/default/jcr：content/campaign_newsletterpage”</i></p> <p>默认值为“XHTML”：</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>可更改为“HTML_5”：</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>指定字符定义以确保正确呈现特殊字符。</p> <p>将CHARSET声明（例如iso-8859-15、UTF-8）添加到 &lt;head&gt;</p> </td>
   <td><p>设置为UTF-8。</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>使用对所有结构进行编码 &lt;table&gt;元素。 对于更复杂的布局，应嵌套表以构建复杂的结构。</p> <p>即使没有css，电子邮件也应看起来良好。</p> </td>
   <td><p>在整个模板中使用表来结构化内容。 当前最多使用四个嵌套表（1个基表+最大值）。 3个嵌套级别)</p> <p>&lt;div&gt; 标记仅用于创作模式，以确保正确编辑组件。</p> </td>
  </tr>
  <tr>
   <td>使用元素属性（如单元格内边距、有效值和宽度）来设置表格尺寸。 这将强制使用盒模型结构。</td>
   <td><p>所有表都包含必要的属性，例如 <i>边框</i>， <i>单元格填充</i>， <i>单元格间距</i> 和 <i>宽度</i>.</p> <p>要协调表内的元素位置，所有表单元格都具有属性 <i>valign=”top”</i> 被设置了。</p> </td>
  </tr>
  <tr>
   <td><p>尽可能考虑移动便利性。 使用媒体查询来增加小屏幕上的文本大小，为链接提供缩略图大小的点击区域。</p> <p>如果设计允许，则使电子邮件具有响应性。</p> </td>
   <td>就CSS样式用于说明演示设计而言，媒体查询用于提供对移动设备友好的版本。</td>
  </tr>
  <tr>
   <td>内联CSS比将所有CSS放在开头要好。</td>
   <td><p>为了更好地演示底层HTML结构并便于自定义新闻稿结构，仅内联了一些CSS定义。</p> <p>已将基本样式和模板变体提取到 &lt;head&gt; 页面的。 在新闻稿最终提交时，这些CSS定义应内联到HTML中。 已计划建立一个自动内联机制，但目前不可用。</p> </td>
  </tr>
  <tr>
   <td>保持CSS简单。 避免使用复合样式声明、简写代码、CSS布局属性、复杂选择器和伪元素。</td>
   <td>就CSS样式用于说明演示设计而言，CSS建议得到遵循。</td>
  </tr>
  <tr>
   <td>电子邮件的最大宽度应为600-800像素。 这将使它们在许多客户端提供的预览窗格大小范围内性能更好。</td>
   <td>此 <i>宽度</i> 在演示设计中，内容表的限制为600像素。</td>
  </tr>
 </tbody>
</table>

### 图像 {#images}

/libs/mcm/campaign/components/image

| **最佳实践** | **实施** |
|---|---|
| 添加 *alt* 图像的属性 | 此 *alt* 属性已定义为图像组件的必需属性。 |
| 使用 *jpg* 而不是 *png* 图像格式 | 图像将始终由图像组件用作JPG。 |
| 使用 `<img>` 元素，而不是表格中的背景图像。 | 模板中不使用背景图像数据。 |
| 在图片上添加attribute style=&quot;display block&quot;。 允许在Gmail上良好显示。 | 所有图像默认包含 *style=&quot;display block&quot;* 属性。 |

### 文本和链接 {#text-and-links}

/libs/mcm/campaign/components/heading， /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>最佳实践</strong></td>
   <td><strong>实施</strong></td>
  </tr>
  <tr>
   <td>在CSS (font-family)中使用html而不是样式</td>
   <td>富文本编辑器（例如，在文本文本组件中）现在支持选择字体系列和字体大小并将其应用于所选文本。 它们将渲染为标记。</td>
  </tr>
  <tr>
   <td>使用基本的跨平台字体，例如 <i>佐治亚州贝尔达纳市，阿里亚尔</i> 和 <i>Times New Roman</i>.</td>
   <td><p>取决于新闻稿的设计。</p> <p>对于演示设计，使用了“Helvetica”字体，但将回退到通用无衬线字体（如果不存在）。</p> </td>
  </tr>
 </tbody>
</table>

### 通用 {#generic}

| **最佳实践** | **实施** |
|---|---|
| 使用W3C验证器更正HTML代码。 确保所有打开的标记均已正确关闭。 | 代码已验证。 对于XHTML过渡Doctype，仅缺少 `<html>` 缺少元素。 |
| 不必担心JavaScript或Flash — 这些技术基本上不受电子邮件客户端的支持。 | 新闻稿模板中既不使用JavaScript，也不使用Flash。 |
| 添加纯文本版本以进行多部分发送。 | 在页面属性中构建了一个新构件，以便轻松地从页面内容中提取纯文本版本。 这可用作最终纯文本版本的起点。 |

## Campaign新闻稿模板和示例 {#campaign-newsletter-templates-and-examples}

AEM提供了一些现成的模板和组件，可供您创建Campaign新闻稿。 您可以使用这些模板和组件创建自定义新闻稿。

### 模板 {#templates}

为了提供坚实的基础，并拓宽内容流的各种可能性，提供了三种稍微不同的模板类型。 您可以轻松地使用这些功能构建自定义新闻稿。

所有客户都拥有 **标头**， a **页脚** 和 **正文** 部分。 在正文部分的下方，每个模板的不同之处在于 **列设计** （1、2或3列）。

![](assets/chlimage_1-69.png)

### 组件 {#components}

当前有 [七个可在营销活动模板中使用的组件](/help/sites-authoring/adobe-campaign-components.md). 这些组件都基于Adobe标记语言 **HTL**.

| **组件名称** | **组件路径** |
|---|---|
| 标题 | /libs/mcm/campaign/components/heading |
| 图像 | /libs/mcm/campaign/components/image |
| 文本与个性化 | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| 链接 | /libs/mcm/campaign/components/reference |
| Dynamic Media Classic(以前称为Scene7)图像模板 | /libs/mcm/campaign/s7image |
| 目标引用 | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>这些组件针对邮件内容进行了优化；也就是说，它们遵循本文档中概述的最佳实践。 使用其他现成组件通常违反这些规则。

以下详细介绍了这些组件： [Adobe Campaign组件](/help/sites-authoring/adobe-campaign-components.md).
