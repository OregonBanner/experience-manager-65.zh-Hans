---
title: AEM Headless 翻译快速入门
description: 了解如何组织您的 Headless 内容以及 AEM 的翻译工具的工作原理。
exl-id: 764f78a7-1d3d-4406-85b1-b80dffae2350
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 90%

---

# AEM Headless 翻译快速入门 {#getting-started}

了解如何组织您的 Headless 内容以及 AEM 的翻译工具的工作原理。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 翻译历程的上一个文档[了解 AEM 中的 Headless 内容和翻译方法](learn-about.md)中，您学习了 Headless CMS 的含义的基本理论，现在应：

* 了解 Headless 内容交付的基本概念。
* 熟悉 AEM 支持 Headless 和翻译的方式。

本文基于这些基础知识之上，以便您了解 AEM 如何存储和管理 Headless 内容以及您如何使用 AEM 的翻译工具来翻译该内容。

## 目标 {#objective}

本文档可帮助您了解如何开始在 AEM 中翻译 Headless 内容。阅读本文档后，您应：

* 了解内容结构对翻译的重要性。
* 了解 AEM 如何存储 Headless 内容。
* 熟悉 AEM 的翻译工具。

## 要求和先决条件 {#requirements-prerequisites}

在开始翻译 Headless AEM 内容之前，需要满足许多要求。

### 知识 {#knowledge}

* 在 CMS 中翻译内容的经验
* 在使用大型 CMS 的基本功能方面的经验
* 具有 AEM 基本操作的应用知识
* 了解您正在使用的翻译服务
* 基本理解正在翻译的内容

>[!TIP]
>
>如果您不能熟练使用 AEM 等大型 CMS，请考虑先查看[基本操作](/help/sites-authoring/basic-handling.md)文档，然后再继续。“基本操作”文档不是历程的一部分，因此，请在完成后返回此页面。

### 工具 {#tools}

* 用于测试翻译内容的沙盒访问
* 用于连接到您的首选翻译服务的凭据
* 成为 AEM 中的 `projects-administrators` 组的成员

## 结构是关键所在 {#content-structure}

AEM 的内容（无论是 Headless 还是传统网页）都由其结构推动。AEM 对内容结构的要求很少，但在项目规划中仔细考虑您的内容层次结构会让翻译变得更轻松。

>[!TIP]
>
>在 Headless 项目的一开始就规划翻译。尽早与项目经理和内容架构师密切合作。
>
>国际化项目经理可能需为一个单独的角色，其职责是定义应翻译的内容、不应翻译的内容以及哪些已翻译内容可由区域或本地内容制作者修改。

## AEM 存储 Headless 内容的方式 {#headless-content-in-aem}

对于翻译专家来说，深入了解 AEM 管理 Headless 内容的方式并不重要。但是，在您以后使用 AEM 的翻译工具时，熟悉基本概念和术语会很有帮助。最重要的是，您需要了解自己的内容及其结构以有效翻译该内容。

### 内容模型 {#content-models}

为了跨渠道、地区和语言一致地交付 Headless 内容，内容必须是高度结构化的。AEM 使用内容模型来实施此结构。将内容模型视为一种用于创建 Headless 内容的模板或模式。由于每个项目都有自己的需求，因此，每个项目均定义了自己的内容片段模型。AEM 对此类模型没有固定的要求或结构。

内容架构师会在项目的早期阶段定义此结构。作为翻译专家，您应该与内容架构师密切合作以理解和编排内容。

>[!NOTE]
>
>内容架构师负责定义内容模型。翻译专家只需熟悉以下步骤中概述的结构。

由于内容模型定义了内容的结构，因此，您需要知道必须翻译模型的哪些字段。通常，您与内容架构师一起定义此内容。要浏览内容模型的字段，请执行以下步骤。

1. 导航到 **工具** -> **资产** -> **内容片段模型**.
1. 内容片段模型通常存储在文件夹结构中。点按或单击项目的文件夹。
1. 这将列出模型。点按或单击模型可查看详细信息。
   ![内容片段模型](assets/content-fragment-models.png)
1. **内容片段模型编辑器**&#x200B;将打开。
   1. 左列包含模型的字段。我们对此列感兴趣。
   1. 右列包含可添加到模型中的字段。我们可以忽略此列。
      ![内容片段模型编辑器](assets/content-fragment-model-editor.png)
1. 点按或单击模型的某个字段。AEM 会标记该字段，其详细信息会显示在右列中。
   ![内容片段模型编辑器详细信息](assets/content-fragment-model-editor-detail.png)

记下字段 **属性名称** 用于所有必须翻译的字段。 在历程的后期，您将需要此信息。 这些 **属性名称**&#x200B;需要来通知AEM必须翻译内容的哪些字段。

>[!TIP]
>
>通常，内容架构师为翻译专家提供 **属性名称**&#x200B;是翻译所需的所有字段的。 在历程的后期需要这些字段名称。 前面的步骤是为了便于翻译专家理解而提供的。

### 内容片段 {#content-fragments}

内容作者使用内容模型来创建实际的 Headless 内容。内容作者选择作为其内容基础的模型，然后创建内容片段。内容片段是模型的实例，表示要以 Headless 方式交付的实际内容。

如果内容模型是内容的模式，内容片段则为基于这些模式的实际内容。内容片段表示必须翻译的内容。

在数字资源管理 (DAM) 中，内容片段在 AEM 中作为资源进行管理。这一点很重要，因为它们都位于路径 `/content/dam` 下。

## 建议的内容结构 {#recommended-structure}

按照之前的建议，与您的内容架构师协作，确定适合您项目的内容结构。但是，以下是经验证的、简单且直观的结构，此结构非常有效。

在 `/content/dam` 下定义项目的基本文件夹。

```text
/content/dam/<your-project>
```

用于创作内容的语言称为语言根。在我们的示例中，语言根为英语，并且应位于此路径的下方。

```text
/content/dam/<your-project>/en
```

应将所有可能需要本地化的项目内容置于语言根下。

```text
/content/dam/<your-project>/en/<your-project-content>
```

应将翻译创建为语言根旁边的同级文件夹，其文件夹名称代表该语言的 ISO-2 语言代码。例如，德语将具有以下路径。

```text
/content/dam/<your-project>/de
```

>[!NOTE]
>
>内容架构师通常负责创建这些语言文件夹。如果未创建这些语言文件夹，AEM 以后将无法创建翻译作业。

最终结构可能如下所示。

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

您应记下内容的特定路径，因为稍后需要使用此路径来配置翻译。

>[!NOTE]
>
>一般来说，内容架构师负责定义内容结构，但可以与翻译专家合作。
>
>为了完整起见，这里进行了详细说明。

## AEM 翻译工具 {#translation-tools}

现在，您已了解什么是内容片段以及内容结构的重要性，我们可以来看看如何翻译此内容。AEM 中的翻译工具非常强大，这些工具从高层次上更易于理解。

* **翻译连接器** – 此连接器旨在将 AEM 与您使用的翻译服务联系起来。
* **翻译规则** – 规则定义了特定路径下的应翻译的内容。
* **翻译项目** – 翻译项目收集应作为单个翻译工作处理的内容并跟踪翻译进度，与连接器连接以传输要翻译的内容并重新从翻译服务接收此内容。

您通常只为实例和每个Headless项目的规则设置一次连接器。 之后，您可以使用翻译项目来翻译内容并不断更新其翻译。

## 后续内容 {#what-is-next}

现在，您已完成 Headless 翻译历程的这一部分，您应：

* 了解内容结构对翻译的重要性。
* 了解 AEM 如何存储 Headless 内容。
* 熟悉 AEM 的翻译工具。

在此知识的基础上继续您的AEM Headless翻译历程，接下来查看文档 [配置翻译集成](configure-connector.md) 您将在其中学习如何将AEM连接到翻译服务。|

## 其他资源 {#additional-resources}

我们建议您查看文档[配置翻译连接器](configure-connector.md)来继续 Headless 翻译历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续 Headless 历程所必需的。

* [AEM 基本操作](/help/sites-authoring/basic-handling.md) – 了解 AEM UI 的基础知识，以便能够舒适地导航和执行基本任务，例如查找内容。
* [标识要翻译的内容](/help/sites-administering/tc-rules.md) – 了解翻译规则如何标识需要翻译的内容。
* [配置翻译集成框架](/help/sites-administering/tc-tic.md) – 了解如何配置翻译集成框架以与第三方翻译服务集成。
* [管理翻译项目](/help/sites-administering/tc-manage.md) – 了解如何在 AEM 中创建和管理机器翻译项目和人工翻译项目。
* [AEM as a Headless CMS 简介](/help/sites-developing/headless/introduction.md)
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
* [AEM 中的 Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans)
