---
title: 体验片段
seo-title: 体验片段
description: 了解如何自定义体验片段。
seo-description: 了解如何自定义体验片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 2%

---


# 体验片段{#experience-fragments}

## 基本信息 {#the-basics}

[体验片段](/help/sites-authoring/experience-fragments.md)是由一个或多个组件构成的组件组，包括可在页面内引用的内容和布局。

体验片段主控和／或变体使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

由于没有`/libs/cq/experience-fragments/components/xfpage/xfpage.html`，它会还原为

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## 纯 HTML 呈现版本 {#the-plain-html-rendition}

使用URL中的`.plain.`选择器，可以访问纯HTML再现。

可以从浏览器访问，但其主要用途是允许其他应用程序（例如，第三方Web应用程序、自定义移动实施）仅使用URL直接访问体验片段的内容。

纯HTML再现将协议、主机和上下文路径添加到以下路径：

* 类型：`src`、`href`或`action`

* 或结束于：`-src`或`-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>链接始终引用发布实例。 这些链接旨在由第三方使用，因此始终从发布实例调用链接，而不是从作者调用。

![xf-12](assets/xf-14.png)

纯格式副本选择器使用变压器，而不是附加脚本；使用[Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)作为变压器。 此配置位于

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 社交变量{#social-variations}

社交变体可以发布到社交媒体（文本和图像）。 在AEM中，这些社交变体可以包含组件；例如，文本组件、图像组件。

社交帖子的图像和文本可以从任何深度级别(在构建块或布局容器中)的任何图像资源类型或文本资源类型中获取。

社交变化还允许构建基块，并在进行社交操作(在发布环境)时考虑它们。

要将正确的文本和图像发布到社交媒体网络，如果您正在开发自己的自定义组件，则需要遵守一些惯例。

对于此，必须使用以下属性：

* 用于提取图像

   * `fileReference`
   * `fileName`

* 用于提取文本

   * `text`

不采用本公约的构成部分不予考虑。

## 体验片段模板{#templates-for-experience-fragments}

>[!CAUTION]
>
>***体*** [验片](/help/sites-developing/page-templates-editable.md) 段支持可在线模板。

为体验片段开发新模板时，您可以按照[可编辑模板](/help/sites-developing/page-templates-editable.md)的标准做法操作。

要创建由&#x200B;**创建体验片段**&#x200B;向导检测到的体验片段模板，您必须遵循以下规则集之一：

1. 两者:

   1. 模板的资源类型（初始节点）必须继承自：
      `cq/experience-fragments/components/xfpage`

   1. 模板的名称必须以下列内容开头：
      `experience-fragments`
这允许用户在/content/experience-fragments中创建体验片段， 
`cq:allowedTemplates` 此文件夹的属性包括名称以开头的所有模板 `experience-fragment`。客户可以更新此属性，以包含自己的命名方案或模板位置。

1. [允许](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 的模板可在体验片段控制台中配置。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 体验片段的组件{#components-for-experience-fragments}

[开发](/help/sites-developing/components.md) 组件以与Experience Fragments一起使用／与Experience Fragments一起使用遵循标准惯例。

唯一的额外配置是确保模板上允许[组件，这是通过内容策略](/help/sites-developing/page-templates-editable.md#content-policies)实现的。

## 体验片段链接重写程序提供程序- HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以创建体验片段。 体验片段：

* 由一组组件和一个布局组成，
* 可以独立于AEM页面存在。

此类组的一个使用案例是将内容嵌入第三方接触点，如Adobe Target。

### 默认链路重写{#default-link-rewriting}

使用[导出到目标](/help/sites-administering/experience-fragments-target.md)功能，您可以：

* 创建体验片段，
* 添加组件，
* 然后以HTML格式或JSON格式将其导出为Adobe Target优惠。

在AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites)的作者实例上可以启用[此功能。 它需要有效的Adobe Target配置和链接外部器的配置。

链接外部化器用于确定创建目标优惠的HTML版本时需要的正确URL，该版本随后将发送到Adobe Target。 这是必要的，因为Adobe Target要求目标HTML优惠内的所有链接都可以公开访问；这意味着必须先发布链接引用的任何资源以及体验片段本身，然后才能使用这些资源。

默认情况下，当您构建目标HTML优惠时，请求将发送到AEM的自定义Sling选择器。 此选择器称为`.nocloudconfigs.html`。 正如其名称所暗示的，它会创建体验片段的纯HTML渲染，但不包括云配置（这将是多余的信息）。

生成HTML页面后，Sling Rewriter管道会修改输出：

1. `html`、`head`和`body`元素被替换为`div`元素。 将删除`meta`、`noscript`和`title`元素（它们是原始`head`元素的子元素，当它们被`div`元素替换时，不考虑这些元素）。

   这样做是为了确保HTML目标优惠可以包含在目标活动中。

1. AEM将修改HTML中存在的所有内部链接，以便它们指向已发布的资源。

   要确定要修改的链接，AEM对HTML元素的属性遵循以下模式：

   1. `src` 属性
   1. `href` 属性
   1. `*-src` 属性（如data-src、custom-src等）
   1. `*-href` 属性( `data-href`如 `custom-href`、 `img-href`等)

   >[!NOTE]
   >
   >在大多数情况下，HTML中的内部链接是相对链接，但有时自定义组件在HTML中提供完整URL。 默认情况下，AEM会忽略这些成熟的URL，并且不进行任何修改。

   这些属性中的链接通过AEM Link Externalizer `publishLink()`运行，以便重新创建URL，就像它在已发布的实例上一样，公开可用。

在使用现成的实施时，上述过程应足以从体验片段生成目标优惠，然后将其导出到Adobe Target。 但是，有些使用案例在此过程中没有说明；包括：

* Sling Mapping仅适用于发布实例
* 调度程序重定向

对于这些用例，AEM提供链接重写器提供程序界面。

### 链路重写器提供程序接口{#link-rewriter-provider-interface}

>[!NOTE]
>
>此接口在[AEM 6.5 SP1(6.5.1.0)](/help/release-notes/sp-release-notes.md)中引入。

对于更复杂的情况，AEM会优惠链路重写器提供程序接口（未由[default](#default-link-rewriting)覆盖）。 这是一个`ConsumerType`接口，作为服务，您可以在包中实现它。 它绕过AEM在从体验片段呈现的HTML优惠的内部链接上执行的修改。 此界面允许您自定义重写内部HTML链接的过程，以符合您的业务需求。

将此接口作为服务实现的用例包括：

* 发布实例上启用Sling映射，但作者实例上不启用
* 调度程序或类似技术用于在内部重定向URL
* 资源`sling:alias mechanisms`已到位

>[!NOTE]
>
>此界面仅处理生成的目标优惠中的内部HTML链接。

链接重写器提供程序接口(`ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用链路重写器提供程序接口{#how-to-use-the-link-rewriter-provider-interface}

要使用该接口，您首先需要创建一个包，其中包含实现链接重写器提供程序接口的新服务组件。

此服务将用于插入体验片段导出以进行目标重写，以便能够访问各种链接。

例如，`ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

为了使服务正常工作，现在有三种方法需要在服务中实现：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您需要向系统指示，当对某个体验片段变体发出“导出到目标”调用时，系统是否需要重写链接。 通过实现以下方法实现：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法作为参数接收“导出到目标”系统当前正在重写的体验片段变量。

在上面的示例中，我们要重写：

* `src`中的链接

* `href` 仅限

* 对于特定体验片段：
   `/content/experience-fragment/master`

通过导出到目标系统的任何其他体验片段将被忽略，不受此服务中实施的更改的影响。

#### rewriteLink {#rewritelink}

对于受重写过程影响的体验片段变体，它随后将继续让服务处理链接重写。 每当在内部HTML中遇到链接时，都会调用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作为输入，该方法接收参数：

* `link`不为目标组件考虑  
`String` 当前正在处理的链接的表示形式。这通常是指向创作实例上的资源的相对URL。

* `tag`
当前正在处理的HTML元素的名称。

* `attribute`
确切的属性名称。

例如，如果“导出到目标”系统当前正在处理此元素，则可以将`CSSInclude`定义为：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

调用`rewriteLink()`方法时使用以下参数：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

创建服务时，您可以根据给定的输入做出决策，然后相应地重写链接。

对于我们的示例，我们要删除URL的`/etc.clientlibs`部分并添加相应的外部域。 为了简单起见，我们将考虑我们有权访问您的服务的资源解析程序，如`rewriteLinkExample2`中所示：

>[!NOTE]
>
>有关如何通过服务用户获取资源解析程序的详细信息，请参见AEM](/help/sites-administering/security-service-users.md)中的[服务用户。

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法返回`null`，则“导出到目标”系统将保留该链接，该链接是指向资源的相对链接。

#### 优先级- getPriority {#priorities-getpriority}

需要多种服务来满足不同类型的体验片段，甚至拥有通用服务来处理所有体验片段的外部化和映射，这种情况并不少见。 在这些情况下，可能会发生与要使用的服务相关的冲突，因此AEM提供为不同服务定义&#x200B;**优先级**&#x200B;的可能性。 使用以下方法指定优先级：

* `getPriority()`

此方法允许使用`shouldRewrite()`方法为同一体验片段返回true的多个服务。 从其`getPriority()`方法返回最大数的服务是处理体验片段变量的服务。

例如，您可以有一个`GenericLinkRewriterProvider`，它处理所有体验片段的基本映射，以及当`shouldRewrite()`方法返回所有体验片段变量的`true`时。 对于多个特定的体验片段，您可能需要特殊处理，因此在这种情况下，您可以提供`SpecificLinkRewriterProvider`，其中`shouldRewrite()`方法仅对某些体验片段变量返回true。 要确保选择`SpecificLinkRewriterProvider`来处理这些体验片段变量，它必须在其`getPriority()`方法中返回一个比`GenericLinkRewriterProvider.`高的数字
