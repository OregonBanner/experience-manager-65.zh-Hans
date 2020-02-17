---
title: 体验片段
seo-title: 体验片段
description: 了解自定义体验片段。
seo-description: 了解自定义体验片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b

---


# 体验片段{#experience-fragments}

## 基本信息 {#the-basics}

[体验片段](/help/sites-authoring/experience-fragments.md)是由一个或多个组件构成的组件组，包括可在页面内引用的内容和布局。

体验片段主数据和／或变体使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

因为没有，它 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 会还原为

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 纯 HTML 呈现版本 {#the-plain-html-rendition}

使用URL `.plain.` 中的选择器，您可以访问纯HTML再现。

这可从浏览器访问，但其主要用途是允许其他应用程序（例如，第三方Web应用程序、自定义移动实施）仅使用URL直接访问体验片段的内容。

纯HTML再现将协议、主机和上下文路径添加到以下路径：

* 类型： `src`、 `href`或 `action`

* 或结束于： `-src`或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>链接始终引用发布实例。 这些链接旨在由第三方使用，因此始终从发布实例调用链接，而不是从作者调用。

![xf-14](assets/xf-14.png)

纯再现选择器使用变压器而不是其他脚本；Sling Rewriter [是变压器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) ，它是一个Sling Rewriter。 此配置位于

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 社交变量 {#social-variations}

社交变体可以发布到社交媒体（文本和图像）上。 在AEM中，这些社交变体可以包含组件；例如，文本组件、图像组件。

社交帖子的图像和文本可以从任何深度级别（在构建块或布局容器中）的任何图像资源类型或文本资源类型中获取。

社交变量还允许构建基块，并在进行社交操作（在发布环境中）时考虑它们。

要将正确的文本和图像发布到社交媒体网络，如果您正在开发自己的自定义组件，则需要遵守一些惯例。

对于此，必须使用以下属性：

* 用于提取图像

   * `fileReference`
   * `fileName`

* 用于提取文本

   * `text`

不会考虑不使用本公约的组件。

## 体验片段模板 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***只有***[可编辑的模板](/help/sites-developing/page-templates-editable.md) ，才支持体验片段。

为体验片段开发新模板时，您可以按照可编辑模板的标准 [做法操作](/help/sites-developing/page-templates-editable.md)。

要创建由创建体验片段向导检测到的体 **验片段模板** ，您必须遵循以下规则集之一：

1. 两者:

   1. 模板的资源类型（初始节点）必须继承自：
      `cq/experience-fragments/components/xfpage`

   1. 并且模板的名称必须以下列内容开头：
      `experience-fragments`
这允许用户在/content/experience-fragments中创建体验片段，因为此文件夹的属性包含名称以开头的所 `cq:allowedTemplates` 有模板 `experience-fragment`。 客户可以更新此属性，以包含他们自己的命名方案或模板位置。

1. [可以在](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) “体验片段”控制台中配置允许的模板。
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 体验片段组件 {#components-for-experience-fragments}

[开发与](/help/sites-developing/components.md) Experience Fragments一起使用的组件遵循标准实践。

唯一的附加配置是确保模板上允 [许使用组件，这是通过内容策略实现的](/help/sites-developing/page-templates-editable.md#content-policies)。

## The Experience Fragment Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以创建体验片段。 体验片段：

* 由一组组件和一个布局组成，
* 可以独立于AEM页面存在。

此类组的一个使用案例是将内容嵌入第三方接触点（如Adobe Target）。

### 默认链接重写 {#default-link-rewriting}

使用“ [导出到目标](/help/sites-administering/experience-fragments-target.md) ”功能，您可以：

* 创建体验片段，
* 添加组件，
* 然后以HTML格式或JSON格式将其导出为Adobe Target选件。

可以在AEM的 [创作实例上启用此功能](/help/sites-administering/experience-fragments-target.md#Prerequisites)。 它需要有效的Adobe Target配置以及Link Externalizer的配置。

Link Externalizer用于确定创建Target选件的HTML版本时所需的正确URL，该版本随后将发送到Adobe Target。 这是必需的，因为Adobe Target要求可以公开访问Target HTML选件内的所有链接；这意味着链接引用的任何资源以及体验片段本身都必须在发布后才能使用它们。

默认情况下，当您构建Target HTML选件时，会向AEM中的自定义Sling选择器发送请求。 此选择器称为 `.nocloudconfigs.html`。 正如其名称所暗示的，它创建了体验片段的纯HTML渲染，但不包括云配置（这将是多余的信息）。

在生成HTML页面后，Sling Rewriter管道将修改输出：

1. 元 `html`素将 `head`替换 `body` 、和元 `div` 素。 将删 `meta`除、 `noscript` 和元素(它们是原始元素的子元 `title` 素，当它们被元素替换时，不考虑 `head``div` 这些元素)。

   这样做是为了确保HTML Target选件可以包含在目标活动中。

1. AEM会修改HTML中存在的任何内部链接，以便它们指向已发布的资源。

   要确定要修改的链接，AEM会按照此模式对HTML元素的属性进行修改：

   1. `src` 属性
   1. `href` 属性
   1. `*-src` 属性（如data-src、custom-src等）
   1. `*-href` 属性( `data-href`如 `custom-href`、 `img-href`等)
   >[!NOTE]
   >
   >在大多数情况下，HTML中的内部链接是相对链接，但有时自定义组件在HTML中提供完整URL。 默认情况下，AEM会忽略这些完全正规的URL，并且不做任何修改。

   这些属性中的链接通过AEM Link Externalizer运行， `publishLink()` 以便重新创建URL，就像它在已发布的实例上一样，也就像公开提供的一样。

使用现成实施时，上述过程应足以从体验片段生成目标选件，然后将其导出到Adobe Target。 但是，有些使用案例在此过程中没有说明；包括：

* Sling Mapping仅在发布实例上可用
* 调度程序重定向

对于这些用例，AEM提供链接重写器提供者界面。

### 链接重写器提供者界面 {#link-rewriter-provider-interface}

>[!NOTE]
>
>此接口在 [AEM 6.5 SP1(6.5.1.0)中引入](/help/release-notes/sp-release-notes.md)。

对于更复杂的情况，AEM提供了链 [接重写程序](#default-link-rewriting)（默认）提供者界面。 这是一个 `ConsumerType` 接口，您可以作为服务在捆绑包中实现。 它会绕过AEM在从体验片段呈现的HTML选件的内部链接上执行的修改。 此界面允许您自定义重写内部HTML链接的过程，以符合您的业务需求。

将此接口作为服务实现的用例包括：

* 发布实例上启用了Sling映射，但创作实例上未启用
* 调度程序或类似技术用于在内部重定向URL
* 资源 `sling:alias mechanisms` 已经到位

>[!NOTE]
>
>此界面仅处理生成的目标选件中的内部HTML链接。

链接重写器提供者界 `ExperienceFragmentLinkRewriterProvider`面()如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用链接重写器提供者界面 {#how-to-use-the-link-rewriter-provider-interface}

要使用该接口，您首先需要创建一个包，其中包含实现链接重写器提供者接口的新服务组件。

此服务将用于插入Experience Fragment Export to Target重写，以便能够访问各种链接。

For example, `ComponentService`:

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

您需要向系统表明，当对某个体验片段变体发出“导出到目标”调用时，它是否需要重写链接。 通过实现以下方法来实现：

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

* 链接 `src`

* `href` 仅限

* 对于特定体验片段：
   `/content/experience-fragment/master`

通过“导出到目标”系统的任何其他体验片段将被忽略，并且不受本服务中实施的更改的影响。

#### rewriteLink {#rewritelink}

对于受重写过程影响的体验片段变体，它随后将继续让服务处理链接重写。 每当在内部HTML中遇到链接时，都会调用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作为输入，该方法接收以下参数：

* `link`
当 `String` 前正在处理的链接的表示形式。 这通常是指向创作实例上的资源的相对URL。

* `tag`
当前正在处理的HTML元素的名称。

* `attribute`
确切的属性名称。

例如，如果“导出到目标”系统当前正在处理此元素，则可以定义 `CSSInclude` 为：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

调用方法时 `rewriteLink()` 使用以下参数：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

创建服务时，您可以根据给定的输入做出决策，然后相应地重写链接。

例如，我们要删除URL的 `/etc.clientlibs` 一部分并添加相应的外部域。 为了简单起见，我们将考虑我们有权访问您的服务的资源解析程序，如 `rewriteLinkExample2`:

>[!NOTE]
>
>有关如何通过服务用户获取资源解析程序的详细信息，请参阅AEM [中的服务用户](/help/sites-administering/security-service-users.md)。

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
>如果上述方法返 `null`回，则“导出到目标”系统将保留该链接，该链接是指向某个资源的相对链接。

#### 优先级- getPriority {#priorities-getpriority}

需要多种服务来满足不同种类的体验片段，甚至拥有通用服务来处理所有体验片段的外部化和映射，这种情况并不少见。 在这些情况下，可能会与要使用的服务发生冲突，因此AEM提供了为不同服务定义优先 **级** 的可能性。 使用以下方法指定优先级：

* `getPriority()`

此方法允许使用多个服务，其中对于同 `shouldRewrite()` 一体验片段，该方法返回true。 从其方法返回最高数量的服 `getPriority()`务是处理体验片段变量的服务。

例如，您可以有一个处理所 `GenericLinkRewriterProvider` 有体验片段的基本映射以及所有体验片段变 `shouldRewrite()` 量的 `true` 方法返回时。 对于多个特定的体验片段，您可能需要特殊处理，因此在这种情况下，您可以提供一个方法仅对某些 `SpecificLinkRewriterProvider` 体验片 `shouldRewrite()` 段变量返回true的方法。 要确保选择 `SpecificLinkRewriterProvider` 处理这些体验片段变量，它在方法中返回的数 `getPriority()` 字必须高于 `GenericLinkRewriterProvider.`
