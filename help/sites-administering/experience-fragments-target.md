---
title: 将体验片段导出到Adobe Target
seo-title: 将体验片段导出到Adobe Target
description: 将体验片段导出到Adobe Target
seo-description: 将体验片段导出到Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
translation-type: tm+mt
source-git-commit: 6723b12bebba2f239c0886e5f378f1dc70e5e247

---


# 将体验片段导出到Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>本页中的某些功能需要应用AEM 6.5.3.0。
>
>6.5.3.0
>
>* **现在可以选择** “Externalizer域”。
>
>
6.5.2.0:
>
>* 体验片段可导出到以下任一位置：
   >   * 默认工作区。
   >   * 在云配置中指定的命名工作区。
>* 必须使用 [Adobe I/O将AEM与Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。
>
>
AEM 6.5.0.0和6.5.1.0:
>
>* AEM体验片段将导出到Adobe Target的默认工作区。
>* AEM必须根据与Adobe target集成下的说明与Adobe [Target集成](/help/sites-administering/target.md)。


您可以将 [在Adobe Experience Manager](/help/sites-authoring/experience-fragments.md)(AEM)中创建的Experience Fragments导出到Adobe Target(Target)。 然后，可在Target活动中将其用作选件，以大规模测试和个性化体验。

有三种格式选项可用于将体验片段导出到Adobe Target:

* HTML（默认）:支持Web和混合内容交付
* JSON:支持无外设内容交付
* HTML 和 JSON

AEM Experience Fragments可以导出到Adobe Target中的默认工作区，或导出到Adobe Target的用户定义工作区。 这是通过Adobe I/O完成的，对于Adobe I/O,AEM必须 [使用Adobe I/O与Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。

>[!NOTE]
>
>Adobe Target本身不存在Adobe target工作区。 在Adobe IMS（标识管理系统）中定义和管理这些组件，然后选择它们以在使用Adobe I/O集成的解决方案中使用。

>[!NOTE]
>
>Adobe Target工作区仅可用于允许组织（组）的成员创建和管理此组织的选件和活动；而不授予其他用户访问权限。 例如，全球关注的国家特定组织。

>[!NOTE]
>
>有关详细信息，另请参阅：
>
>* [Adobe Target开发](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心组件——体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>



## 前提条件 {#prerequisites}

>[!CAUTION]
>
>本页中的某些功能需要应用AEM 6.5.3.0。

需要执行各种操作：

1. 您必须 [使用Adobe I/O将AEM与Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。
2. 体验片段从AEM作者实例中导出，因此您需要在作者实例上配置 [AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) ，以确保将体验片段内的任何引用外置以用于Web交付。

   >[!NOTE]
   >
   >对于默认未涵盖的链接重写，可使 [用体验片段链接重写提供程序](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 。 通过这种方式，可以为实例开发自定义规则。

## 添加云配置 {#add-the-cloud-configuration}

在导出片段之前，您需要将 **Adobe Target的云配置****** 添加到片段或文件夹。 这还允许您：

* 指定用于导出的格式选项
* 选择目标工作区作为目标
* 选择外部化器域以重写体验片段中的引用（可选）

在所需文件夹和／或片段的 **页面属性** ，可以选择所需的选项；将根据需要继承规范。

1. 导航到“体 **验片段** ”控制台。

1. 打开 **相应文件夹** 或片段的页面属性。

   >[!NOTE]
   >
   >如果将云配置添加到Experience Fragment父文件夹，则此配置将由所有子文件夹继承。
   >
   >
   >如果将云配置添加到体验片段本身，则所有变量都会继承该配置。

1. 选择“ **云服务** ”选项卡。

1. 在“ **云服务配置**”下，从下 **拉列表中选择Adobe Target** 。

1. 
   >[!NOTE]
   >
   >可以自定义体验片段选件的JSON格式。 为此，请定义客户体验片段组件，然后在组件Sling Model中注释如何导出其属性。
   >
   >请参阅核心组件：
   >
   >[核心组件——体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   在 **Adobe Target下** ，选择：

   * 相应的配置
   * 所需的格式选项
   * adobe target工作区
   * if required - externalizer域
   >[!CAUTION]
   >
   >externalizer域是可选的。 当您希望导出的内容指向特定的发布域时，将配置AEM *externalizer* 。 有关详细信息，请 [参阅配置AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)。

   例如，对于文件夹：

   ![文件夹——云服](assets/xf-target-integration-01.png "务文件夹——云服务")

1. **保存并关闭**.

## 将体验片段导出到Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>对于媒体资产（如图像），只有引用会导出到Target。 资产本身将保留在AEM资产中，并从AEM发布实例中传送。
>
>因此，需要先发布包含所有相关资产的体验片段，然后再导出到Target。

要将体验片段从AEM导出到Target（在指定云配置后），请执行以下操作：

1. 导航到体验片段控制台。
1. 选择要导出到目标的体验片段。

   >[!NOTE]
   >
   >它必须是体验片段Web变量。

1. 点按／单 **击导出至Adobe Target**。

   >[!NOTE]
   >
   >如果体验片段已导出，请在Adobe Target中 **选择更新**。

1. 根据需要点按／单 **击导出** ，不发 **布或** 发布。

   >[!NOTE]
   >
   >选择 **发布** ，将立即发布体验片段并将其发送到Target。

1. 点按／单击确 **认对话框** 中的确定。

   您的体验片段现在应位于Target中。

   >[!NOTE]
   >
   >[导出的各种详细信息](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) ，可在控制台和属 **性的列表视图** 中查看 **这些**。

   >[!NOTE]
   >
   >在Adobe Target中查看体验片段时，看到的上次修改日期是片段在 ** AEM中上次修改的日期，而不是片段上次导出到Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用“页面信息”菜单中的类似命令从页面编辑器 [执行导出](/help/sites-authoring/author-environment-tools.md#page-information) 。

## 在Adobe target中使用您的体验片段 {#using-your-experience-fragments-in-adobe-target}

执行上述任务后，体验片段会显示在Target的“选件”页面上。 请查看特定Target文 [档](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) ，了解您可以在其中实现什么。

>[!NOTE]
>
>在Adobe Target中查看体验片段时，看到的上次修改日期是片段在 ** AEM中上次修改的日期，而不是片段上次导出到Adobe Target的日期。

## 删除已导出到Adobe target的体验片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

如果删除已导出到Target的体验片段，则该片段已在Target中的选件中使用，则可能会导致问题。 删除片段会使选件在AEM传送片段内容时无法使用。

要避免此类情况，请执行以下操作：

* 如果活动中当前未使用体验片段，则AEM允许用户删除片段，但不显示警告消息。
* 如果Target中的活动当前正在使用体验片段，则会显示一条错误消息，警告AEM用户删除片段对活动可能产生的后果。

   AEM中的错误消息不会禁止用户（强制）删除体验片段。 如果体验片段被删除：

   * 包含AEM体验片段的Target选件可能显示不期望的行为

      * 随着体验片段HTML被推送到Target，选件可能仍会呈现
      * 如果引用的资产也在AEM中被删除，则体验片段中的任何引用可能无法正常工作。
   * 当然，由于体验片段在AEM中已不存在，因此无法对体验片段进行任何进一步修改。