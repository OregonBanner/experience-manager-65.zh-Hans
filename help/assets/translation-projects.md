---
title: 创建翻译项目
description: 了解如何在 [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Admin
feature: Translation
exl-id: 8990feca-cfda-4974-915e-27aa9d8f2ee1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 17%

---

# 创建翻译项目 {#creating-translation-projects}

要创建语言副本，请触发以下语言副本工作流之一： [!DNL Experience Manager] 用户界面。

* **创建和翻译**:在此工作流中，要翻译的资产将会复制到您要翻译的语言的语言根目录中。 此外，根据您选择的选项，将在“项目”控制台中为资产创建一个翻译项目。 根据设置，可以手动启动翻译项目，也可以在翻译项目创建后立即自动运行翻译项目。

* **更新语言副本**:运行此工作流以翻译其他资产组，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹。

>[!PREREQUISITES]
>
>* 创建翻译项目的用户是组的成员 `projects-administrators`.
>* 翻译服务提供程序支持二进制文件的翻译。


## 创建和翻译工作流 {#create-and-translate-workflow}

您可以使用创建和翻译工作流首次为特定语言生成语言副本。 工作流提供了以下选项：

* 只创建结构.
* 创建新翻译项目.
* 添加到现有翻译项目.

### 只创建结构 {#create-structure-only}

使用“ **[!UICONTROL 仅创建结构]** ”选项可在目标语言根目录中创建目标文件夹层次结构，以匹配源语言根目录中源文件夹的层次结构。 在这种情况下，源资产会复制到目标文件夹。 但是，不会生成翻译项目。

1. 在 [!DNL Assets] 界面中，选择要在目标语言根目录中创建结构的源文件夹。

1. 打开 **[!UICONTROL 引用]** 窗格，单击 **[!UICONTROL 语言副本]** 在 **[!UICONTROL 副本]**.

   ![语言副本](assets/translation-language-copies.png)

1. 单击 **[!UICONTROL 创建和翻译]**. 从 **[!UICONTROL 目标语言]** 列表中，选择要为其创建文件夹结构的语言。

1. 从&#x200B;**[!UICONTROL 项目]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 仅创建结构]**。

1. 单击&#x200B;**[!UICONTROL 创建]**。目标语言的新结构列在 **[!UICONTROL 语言副本]**.

   ![语言副本](assets/lang-copy2.png)

1. 单击列表中的结构，然后单击 **[!UICONTROL 在资产中显示]** 导航到目标语言中的文件夹结构。

   ![资产显示](assets/reveal-in-assets.png)

### 创建新翻译项目 {#create-a-new-translation-project}

如果您使用此选项，则要翻译的资产将会复制到您要翻译的语言的语言根目录中。 根据您选择的选项，将在“项目”控制台中为资产创建一个翻译项目。 翻译项目可以手动启动，也可以在翻译项目创建后立即自动运行，具体取决于设置。

1. 在 [!DNL Assets] 用户界面中，选择要为其创建语言副本的源文件夹。
1. 打开 **[!UICONTROL 引用]** 窗格，单击 **[!UICONTROL 语言副本]** 在 **[!UICONTROL 副本]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. 单击 **[!UICONTROL 创建和翻译]** 在底部。

1. 从&#x200B;**[!UICONTROL 目标语言]**&#x200B;列表中，选择要为其创建文件夹结构的语言。

1. 从 **[!UICONTROL 项目]** 列表，选择 **[!UICONTROL 创建新的翻译项目]**.

1. 在&#x200B;**[!UICONTROL 项目标题]**&#x200B;字段中，输入项目标题。

1. 单击&#x200B;**[!UICONTROL 创建]**。[!DNL Assets] 将从源文件夹复制到目标文件夹，以了解您在步骤4中选择的区域设置。

   ![语言副本](assets/lang-copy2.png)

1. 要导航到文件夹，请选择语言副本，然后单击 **[!UICONTROL 在资产中显示]**.

   ![资产显示](assets/reveal-in-assets.png)

1. 导航到项目控制台。 翻译文件夹将会复制到项目控制台。

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. 打开文件夹以查看翻译项目。

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. 单击项目以打开详细信息页面。

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. 要查看翻译作业的状态，请单击 **[!UICONTROL 翻译作业]** 拼贴。

   ![chlimage_1-73](assets/chlimage_1-73.png)

   有关作业状态的更多详细信息，请参阅 [监控翻译作业的状态](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 导航到 [!DNL Assets] 用户界面，并打开 [!UICONTROL 属性] 页面查看已翻译的元数据。

   ![在资产属性页面中查看已翻译的元数据](assets/translated-metadata-asset-properties.png)

   *图：资产属性页面中的已翻译元数据。*

   >[!NOTE]
   >
   >此功能适用于资产和文件夹。 选择资产而不是文件夹后，会复制直至语言根目录的整个文件夹层次结构，以为资产创建语言副本。

### 添加到现有翻译项目 {#add-to-existing-translation-project}

如果您使用此选项，则翻译工作流会为运行之前的翻译工作流后添加到源文件夹的资产运行。 只有新添加的资产才会复制到包含先前翻译过的资产的目标文件夹。 在这种情况下，不会创建新的翻译项目。

1. 在 [!DNL Assets] 在用户界面中，导航到包含未翻译资产的源文件夹。
1. 选择要翻译的资产，然后打开&#x200B;**[!UICONTROL “引用”窗格]**。**[!UICONTROL 语言副本]**&#x200B;部分显示当前可用的翻译副本数。
1. 单击 **[!UICONTROL 语言副本]** 在 **[!UICONTROL 副本]**. 此时将显示可用翻译副本列表。
1. 单击 **[!UICONTROL 创建和翻译]** 在底部。

1. 从&#x200B;**[!UICONTROL 目标语言]**&#x200B;列表中，选择要为其创建文件夹结构的语言。

1. 从“项 **[!UICONTROL 目]** ”列表中，选择 **[!UICONTROL 添加到现有翻译项目]** ，以在文件夹上运行翻译工作流。

   >[!NOTE]
   >
   >如果您选择 **[!UICONTROL 添加到现有翻译项目]** 选项，则仅当项目设置与预先存在的项目的设置完全匹配时，翻译项目才会添加到预先存在的项目。 否则，将创建新项目。

1. 从 **[!UICONTROL 现有翻译项目]** 列表中，选择一个项目以添加要翻译的资产。

1. 单击&#x200B;**[!UICONTROL 创建]**。要翻译的资产将添加到目标文件夹。更新的文件夹列在&#x200B;**[!UICONTROL 语言副本]**&#x200B;部分下。

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. 导航到项目控制台，然后打开您添加到的现有翻译项目。
1. 单击翻译项目查看项目详细信息页面。

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. 单击位于 **翻译作业** 拼贴，以在翻译工作流中查看资产。 翻译作业列表还会显示资产元数据和标记条目。这些条目指示资产的元数据和标记也会被翻译。

   >[!NOTE]
   >
   >如果删除标记或元数据的条目，则不会翻译任何资产的标记或元数据。

   >[!NOTE]
   >
   >如果您添加到翻译作业的资产包含子资产，请选择子资产并将其删除，以便翻译继续，而不会出现任何问题。

1. 要开始翻译资产，请单击 **[!UICONTROL 翻译作业]** 拼贴并选择 **[!UICONTROL 开始]** 列表。

   ![chlimage_1-81](assets/chlimage_1-81.png)

   消息会通知翻译作业的开始。

1. 要查看翻译作业的状态，请单击 **[!UICONTROL 翻译作业]** 拼贴。

   ![chlimage_1-83](assets/chlimage_1-83.png)

   有关更多详细信息，请参阅 [监控翻译作业的状态](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 翻译完成后，状态将变为“准备审阅”。 导航到 [!DNL Assets] ，并打开每个已翻译资产的“属性”页面以查看已翻译的元数据。

## 更新语言副本 {#update-language-copies}

运行此工作流以翻译任何其他资产集，并将其包含在特定区域设置的语言副本中。 在这种情况下，已翻译的资产会添加到已包含先前已翻译资产的目标文件夹。 根据选项的选择，将创建翻译项目或为新资产更新现有翻译项目。 更新语言副本工作流包含以下选项：

* 创建新翻译项目
* 添加到现有翻译项目

### 创建新翻译项目 {#create-a-new-translation-project-1}

如果您使用此选项，则会为要更新语言副本的资产集创建翻译项目。

1. 从 [!DNL Assets] UI中，选择您添加资产的源文件夹。
1. 打开 **[!UICONTROL 引用]** 窗格，然后单击 **[!UICONTROL 语言副本]** 在 **[!UICONTROL 副本]** 以显示语言副本列表。
1. 选中&#x200B;**[!UICONTROL 语言副本]**&#x200B;前面的复选框，然后选择相应区域设置的目标文件夹。

   ![选择语言副本](assets/lang-copy1.png)

1. 单击 **[!UICONTROL 更新语言副本]** 在底部。

1. 从 **[!UICONTROL 项目]** 列表，选择 **[!UICONTROL 创建新的翻译项目]**.

1. 在&#x200B;**[!UICONTROL 项目标题]**&#x200B;字段中，输入项目标题。

1. 单击 **[!UICONTROL 开始]**.
1. 导航到项目控制台。 翻译文件夹将会复制到项目控制台。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 打开文件夹以查看翻译项目。

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. 单击项目以打开详细信息页面。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 要开始翻译资产，请单击 **[!UICONTROL 翻译作业]** 拼贴并选择 **[!UICONTROL 开始]** 列表。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   消息会通知翻译作业的开始。

1. 要查看翻译作业的状态，请单击 **[!UICONTROL 翻译作业]** 拼贴。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   有关作业状态的更多详细信息，请参阅 [监控翻译作业的状态](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. 导航到 [!DNL Assets] ，并打开每个已翻译资产的“属性”页面以查看已翻译的元数据。

### 添加到现有翻译项目 {#add-to-existing-translation-project-1}

如果您使用此选项，则会将资产集添加到现有翻译项目，以更新所选区域设置的语言副本。

1. 从 [!DNL Assets] UI中，选择您添加资产文件夹的源文件夹。
1. 打开 **[!UICONTROL 引用窗格]**，然后单击 **[!UICONTROL 语言副本]** 在 **[!UICONTROL 副本]** 以显示语言副本列表。

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. 选中&#x200B;**[!UICONTROL 语言副本]**&#x200B;前面的复选框，这将选择所有语言副本。除与您要翻译的区域设置对应的语言副本外，取消选择其他副本。

   ![选择语言副本](assets/lang-copy1.png)

1. 单击 **[!UICONTROL 更新语言副本]** 在底部。

1. 从 **[!UICONTROL 项目]** 列表，选择 **[!UICONTROL 添加到现有翻译项目]**.

1. 从 **[!UICONTROL 现有翻译项目]** 列表中，选择一个项目以添加要翻译的资产。

1. 单击 **[!UICONTROL 开始]**.
1. 参见第9-14步 [添加到现有翻译项目](translation-projects.md#add-to-existing-translation-project) 完成其余的程序。

## 创建临时语言副本 {#creating-temporary-language-copies}

当您运行翻译工作流以使用原始资产的编辑版本更新语言副本时，现有语言副本将保留，直到您批准已翻译的资产为止。 [!DNL Adobe Experience Manager Assets] 将新翻译的资产存储在临时位置，并在您明确批准资产后更新现有语言副本。 如果您拒绝资产，语言副本将保持不变。

1. 单击下的源根文件夹 **[!UICONTROL 语言副本]** 您已为其创建语言副本，然后单击 **[!UICONTROL 在资产中显示]** 要在中打开文件夹，请执行以下操作 [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. 从 [!DNL Assets] 界面中，选择已翻译的资产并单击 **[!UICONTROL 编辑]** ，以在编辑模式下打开资产。
1. 编辑资产，然后保存更改。
1. 执行 [添加到现有翻译项目](#add-to-existing-translation-project) 更新语言副本的过程。
1. 单击位于 **[!UICONTROL 翻译作业]** 拼贴。 从 **[!UICONTROL 翻译作业]** 页面上，您可以清楚地查看存储资产翻译版本的临时位置。

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. 选中旁边的复选框 **[!UICONTROL 标题]**.
1. 在工具栏中，单击 **[!UICONTROL 接受翻译]** ![接受翻译](assets/do-not-localize/thumb-up.png) 然后单击 **[!UICONTROL 接受]** 对话框中，使用已编辑资产的已翻译版本覆盖目标文件夹中已翻译资产。

   >[!NOTE]
   >
   >要启用翻译工作流以更新目标资产，请接受资产和元数据。

   单击 **[!UICONTROL 拒绝翻译]** ![拒绝翻译](assets/do-not-localize/thumb-down.png) 以在目标区域设置根目录中保留资产的最初翻译版本，并拒绝编辑的版本。

1. 要查看已翻译的元数据，请导航到 [!DNL Assets] 控制台，然后打开 [!UICONTROL 属性] 页。

## 提示和限制 {#tips-limitations}

* 如果您为复杂的资产启动翻译工作流，例如PDF和 [!DNL Adobe InDesign] 文件、其子资产或演绎版（如果有）均不会提交以进行翻译。
* 如果您使用机器翻译，则不会翻译资产二进制文件。
