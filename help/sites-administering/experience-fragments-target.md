---
title: 将体验片段导出到 Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: 将体验片段导出到 Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 079b7b1e386ac2d02026ee2d8db411e517168b00
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 2%

---

# 将体验片段导出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>本页面上的某些功能需要应用AEM 6.5.3.0（或更高版本）。
>
>6.5.3.0:
>
>* **外部器域** 现在可以选择。
   >  **注意：** 外部器域仅与发送到Target的体验片段的内容相关，而与元数据（如查看选件内容）无关。
>
>6.5.2.0:
>
>* 体验片段可导出到以下任一位置：
   >
   >   * 默认工作区。
   >   * 在云配置中指定的命名工作区。
   >   * **注意：** 要导出到特定工作区，需要使用Adobe Target Premium。
>
>* AEM必须 [与Adobe Target集成(使用Adobe I/O)](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0和6.5.1.0:
>
>* AEM体验片段会导出到Adobe Target的默认工作区中。
>* AEM必须按照 [与Adobe Target集成](/help/sites-administering/target.md).


您可以导出 [体验片段](/help/sites-authoring/experience-fragments.md)，在Adobe Experience Manager(AEM)中创建，到Adobe Target(Target)。 然后，即可在Target活动中将这些体验用作选件，以便测试和个性化大量体验。

有三种格式选项可用于将体验片段导出到Adobe Target:

* HTML（默认）：支持Web和混合内容交付
* JSON:支持无头内容交付
* HTML 和 JSON

AEM体验片段可导出到Adobe Target中的默认工作区，或导出到Adobe Target的用户定义的工作区。 这是通过Adobe I/O完成的，AEM必须为 [与Adobe Target集成(使用Adobe I/O)](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Adobe Target工作区本身不存在于Adobe Target中。 这些配置文件在Adobe IMS(Identity Management系统)中进行定义和管理，然后选择它们以在使用Adobe I/O集成的解决方案中使用。

>[!NOTE]
>
>Adobe Target工作区可用于仅允许组织（组）成员为该组织创建和管理选件和活动；而不授予其他用户访问权限。 例如，全球关注的具体国家组织。

>[!NOTE]
>
>有关详细信息，另请参阅：
>
>* [Adobe Target开发](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心组件 — 体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)
>


## 前提条件 {#prerequisites}

>[!CAUTION]
>
>本页面上的某些功能需要应用AEM 6.5.3.0。

需要执行各种操作：

1. 你必须 [使用Adobe I/O将AEM与Adobe Target集成](/help/sites-administering/integration-target-ims.md).
2. 体验片段是从AEM创作实例导出的，因此您需要 [配置AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) ，以确保体验片段中的任何引用外部化以用于Web交付。

   >[!NOTE]
   >
   >对于默认未涵盖的链接重写， [体验片段链接重写程序提供程序](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 中。 借助此功能，可以为您的实例开发自定义规则。

## 添加云配置 {#add-the-cloud-configuration}

在导出片段之前，您需要添加 **云配置** 表示 **Adobe Target** 到片段或文件夹。 这还允许您：

* 指定要用于导出的格式选项
* 选择Target工作区作为目标
* 选择外部器域以重写体验片段中的引用（可选）

在 **页面属性** 所需文件夹和/或片段的内容；将根据需要继承规范。

1. 导航到 **体验片段** 控制台。

1. 打开 **页面属性** 文件夹或片段。

   >[!NOTE]
   >
   >如果将云配置添加到体验片段父文件夹，则该配置将由所有子文件夹继承。
   >
   >
   >如果将云配置添加到体验片段本身，则该配置将由所有变量继承。

1. 选择 **Cloud Services** 选项卡。

1. 在 **Cloud Service配置**，选择 **Adobe Target** 从下拉列表中。

   >[!NOTE]
   >
   >可以自定义体验片段选件的JSON格式。 要执行此操作，请定义客户体验片段组件，然后在组件Sling模型中注释如何导出其属性。
   >
   >请参阅核心组件：
   >
   >[核心组件 — 体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   在 **Adobe Target** 选择：

   * 相应的配置
   * 所需的格式选项
   * Adobe Target工作区
   * 如果需要 — externalizer域

   >[!CAUTION]
   >
   >外部器域是可选的。
   >
   > 当您希望导出的内容指向特定的 *发布* 域。 有关更多详细信息，请参阅 [配置AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   > 另请注意，外部器域仅与发送到Target的体验片段的内容相关，而与元数据（如查看选件内容）无关。

   例如，对于文件夹：

   ![文件夹 — Cloud Services](assets/xf-target-integration-01.png "文件夹 — Cloud Services")

1. **保存并关闭**.

## 将体验片段导出到Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>对于媒体资产（如图像），只会将引用导出到Target。 资产本身将保留在AEM Assets中，并从AEM发布实例交付。
>
>因此，需要先发布体验片段（包含所有相关资产），然后再导出到Target。

要将体验片段从AEM导出到Target（在指定云配置后），请执行以下操作：

1. 导航到体验片段控制台。
1. 选择要导出到target的体验片段。

   >[!NOTE]
   >
   >它必须是体验片段Web变量。

1. 点按/单击 **导出到Adobe Target**.

   >[!NOTE]
   >
   >如果体验片段已导出，请选择 **在Adobe Target中更新**.

1. 点按/单击 **不发布即导出** 或 **发布** 。

   >[!NOTE]
   >
   >选择 **发布** 将立即发布体验片段并将其发送到Target。

1. 点按/单击 **确定** 在确认对话框中。

   您的体验片段现在应该位于Target中。

   >[!NOTE]
   >
   >[各种详细信息](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 的 **列表视图** 和 **属性**.

   >[!NOTE]
   >
   >在Adobe Target中查看体验片段时， *上次修改时间* 所看到的日期是片段在AEM中的上次修改日期，而不是片段上次导出到Adobe Target的日期。

>[!NOTE]
>
>或者，您也可以使用 [页面信息](/help/sites-authoring/author-environment-tools.md#page-information) 菜单。

## 在Adobe Target中使用您的体验片段 {#using-your-experience-fragments-in-adobe-target}

执行上述任务后，体验片段会显示在Target的“选件”页面上。 请看 [特定Target文档](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 了解您在那里能取得的成就。

>[!NOTE]
>
>在Adobe Target中查看体验片段时， *上次修改时间* 所看到的日期是片段在AEM中的上次修改日期，而不是片段上次导出到Adobe Target的日期。

## 删除已导出到Adobe Target的体验片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

如果删除已导出到Target的体验片段，则该片段已在Target的选件中使用，则该体验片段可能会导致问题。 删除片段会导致选件在AEM交付片段内容时不可用。

为避免出现这种情况：

* 如果活动中当前未使用体验片段，则AEM允许用户删除片段，而不显示警告消息。
* 如果Target中的活动当前正在使用体验片段，则会显示一条错误消息，警告AEM用户删除片段对活动可能产生的影响。

   AEM中的错误消息不禁止用户（强制）删除体验片段。 如果删除了体验片段：

   * 包含AEM体验片段的Target选件可能显示不希望的行为

      * 由于体验片段HTML已推送到Target，因此选件很可能仍会呈现
      * 如果还在AEM中删除了引用的资产，则体验片段中的任何引用可能无法正常工作。
   * 当然，对体验片段进行任何进一步的修改都是不可能的，因为体验片段不再存在于AEM中。
