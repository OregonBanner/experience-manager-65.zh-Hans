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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

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
>* 体验片段可以导出到以下任一位置：
   >
   >   
   * 默认工作区。
   >   * 在云配置中指定的命名工作区。
>* AEM必须 [与使用Adobe I/O的Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。

>
>
AEM 6.5.0.0和6.5.1.0:
>
>* AEM体验片段将导出到默认的Adobe Target工作区。
>* AEM必须根据与Adobe Target集成下的说明与 [Adobe Target集成](/help/sites-administering/target.md)。


您可以将 [在Adobe Experience Manager](/help/sites-authoring/experience-fragments.md)(AEM)中创建的体验片段导出到Adobe Target(目标)。 然后，它们可用作目标活动的优惠，以大规模测试和个性化体验。

有三种格式选项可用于将体验片段导出到Adobe Target:

* HTML（默认）: 支持Web和混合内容投放
* JSON: 支持无头内容投放
* HTML 和 JSON

AEM体验片段可以导出到默认的Adobe Target工作区，或导出到用户定义的Adobe Target工作区。 这是通过Adobe I/O完成的，对于它，AEM必须 [与使用Adobe I/O的Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。

>[!NOTE]
>
>Adobe Target工作区本身不存在。 它们在Adobe IMS(Identity Management系统)中进行定义和管理，然后选择用于使用Adobe I/O集成的各种解决方案。

>[!NOTE]
>
>Adobe Target工作区可用于仅允许组织（组）成员创建和管理此组织的优惠和活动; 而不授予其他用户访问权限。 例如，全球关注的特定国家组织。

>[!NOTE]
>
>有关更多信息，另请参阅：
>
>* [Adobe Target开发](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心组件——体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

>



## 前提条件 {#prerequisites}

>[!CAUTION]
>
>本页中的某些功能需要应用AEM 6.5.3.0。

需要执行各种操作：

1. 您必须使用 [Adobe I/O将AEM与Adobe Target集成](/help/sites-administering/integration-ims-adobe-io.md)。
2. 体验片段从AEM作者实例中导出，因此您需 [要在作者实例上配置AEM Link](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) Externalizer，以确保将体验片段中的任何引用外部化以进行Web投放。

   >[!NOTE]
   >
   >对于默认未涵盖的链接重写，可 [使用体验片段链接重写程序](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 。 通过此，可以为实例开发自定义规则。

## 添加云配置 {#add-the-cloud-configuration}

在导出片段之前，您需要添加 **云配置****以将其** Adobe Target到片段或文件夹。 这还允许您：

* 指定用于导出的格式选项
* 选择目标工作区作为目标
* 选择externalizer域以重写体验片段中的引用（可选）

在所需文件夹和/ **或片段的** “页面属性”中可选择所需选项； 将根据需要继承规范。

1. Navigate to the **Experience Fragments** console.

1. 打开 **相应文件夹** 或片段的页面属性。

   >[!NOTE]
   >
   >如果将云配置添加到体验片段父文件夹，则所有子级都会继承该配置。
   >
   >
   >如果将云配置添加到体验片段本身，则所有变量都会继承该配置。

1. 选择“ **Cloud Service** ”选项卡。

1. 在 **Cloud Service配**&#x200B;置下，从 **下拉** 列表中，选择Adobe Target。

1. 
   >[!NOTE]
   >
   >可以自定义体验片段优惠的JSON格式。 为此，请定义客户体验片段组件，然后在组件Sling Model中注释如何导出其属性。
   >
   >请参阅核心组件：
   >
   >[核心组件——体验片段](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/experience-fragment.html)

   在 **Adobe Target** 下选择：

   * 适当的配置
   * 所需的格式选项
   * Adobe Target工作区
   * if required - externalizer域

   >[!CAUTION]
   >
   >外部化器域是可选的。 当您希望导出的内容指向特定发布域时，将配置AEM *外部* 器。 有关详细信息，请 [参阅配置AEM Link Externalizer](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)。

   例如，对于文件夹：

   ![文件夹——云服](assets/xf-target-integration-01.png "务文件夹-Cloud Service")

1. **保存并关闭**.

## 将体验片段导出到Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>对于媒体资产（如图像），只会导出引用到目标。 资产本身仍存储在AEM Assets中，并通过AEM发布实例传送。
>
>因此，需要先发布包含所有相关资产的体验片段，然后再导出到目标。

要将体验片段从AEM导出到目标（在指定云配置后）:

1. 导航到体验片段控制台。
1. 选择要导出到目标的体验片段。

   >[!NOTE]
   >
   >它必须是体验片段Web变体。

1. 点按／单击 **导出至Adobe Target**。

   >[!NOTE]
   >
   >如果体验片段已导出，请选择 **Adobe Target更新**。

1. 根据需要点按/ **单击导出** ，而 **不进行发** 布或“发布”。

   >[!NOTE]
   >
   >选 **择发布** ，将立即发布体验片段并将其发送到目标。

1. 点按／单 **击确** 认对话框中的确定。

   您的体验片段现在应处于目标。

   >[!NOTE]
   >
   >[在控制台](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 和属性的列表视图中 **，可以看到** 导出的 **各种详细**&#x200B;信息。

   >[!NOTE]
   >
   >在Adobe Target中查看体验片段时，所 *看到的上* 次修改日期是片段在AEM中上次修改的日期，而不是片段上次导出到Adobe Target的日期。

>[!NOTE]
>
>或者，也可以使用“页面信息”菜单中的类似命令从页面编辑器 [执行导出](/help/sites-authoring/author-environment-tools.md#page-information) 。

## 在Adobe Target中使用您的体验片段 {#using-your-experience-fragments-in-adobe-target}

执行上述任务后，体验片段显示在优惠页面的目标中。 请查看特定的 [目标文档](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) ，了解您可以实现哪些目标。

>[!NOTE]
>
>在Adobe Target中查看体验片段时，所 *看到的上* 次修改日期是片段在AEM中上次修改的日期，而不是片段上次导出到Adobe Target的日期。

## 删除已导出到Adobe Target的体验片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

如果删除已导出到目标的体验片段在目标的优惠中已使用，则可能会导致问题。 删除片段会导致优惠在AEM传送片段内容时不可用。

要避免此类情况：

* 如果活动中当前未使用体验片段，则AEM允许用户删除片段，而不显示警告消息。
* 如果目标中的活动当前正在使用体验片段，则会显示一条错误消息，警告AEM用户删除片段对活动可能造成的后果。

   AEM中的错误消息不禁止用户（强制）删除体验片段。 如果体验片段被删除：

   * AEM体验片段的目标优惠可能显示不期望的行为

      * 优惠可能仍会呈现，因为体验片段HTML已推送到目标
      * 如果引用的资产也在AEM中被删除，则体验片段中的任何引用都可能无法正常工作。
   * 当然，由于体验片段在AEM中已不存在，因此无法对体验片段进行任何进一步修改。