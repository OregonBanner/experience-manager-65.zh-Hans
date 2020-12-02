---
title: 管理翻译项目
seo-title: 管理翻译项目
description: 了解如何在AEM中管理翻译项目。
seo-description: 了解如何在AEM中管理翻译项目。
uuid: f6f79b5b-dc08-4dde-b464-719345d233a6
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c8672774-6911-497d-837b-1e5953c4226a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 1%

---


# 管理翻译项目{#managing-translation-projects}

准备翻译内容后，您需要通过创建缺失的语言副本来完成语言结构，并创建翻译项目。

翻译项目使您能够管理AEM内容的翻译。 翻译项目是AEM [project](/help/sites-authoring/projects.md)的类型，它包含要翻译为其他语言的资源。 这些资源是使用语言主控创建的[语言副本](/help/sites-administering/tc-prep.md)的页面和资产。

将资源添加到翻译项目时，会为其创建一个翻译作业。 作业提供命令和状态信息，用于管理在资源上执行的人工翻译和机器翻译工作流。

>[!NOTE]
>
>一个翻译项目可以包含多个翻译作业。

翻译项目是长期的项目，由语言和翻译方法／提供者定义，以符合全球化的组织治理。 它们应在初始翻译期间或手动启动一次，并在整个内容和翻译更新活动中保持有效。

翻译项目和作业是使用翻译准备工作流创建的。 这些工作流有三个选项，分别用于初始翻译(Create&amp;Translate)和更新(Update Translation):

1. [创建新项目](#creating-translation-projects-using-the-references-panel)
1. [添加到现有项目](#adding-pages-to-a-translation-project)
1. [仅限内容结构](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>选项3与翻译作业／项目无关。 它允许您将语言主控的内容和结构更改复制到（未翻译）语言副本。 您可以使用它保持语言主语同步，即使不进行翻译。

## 执行初始翻译并更新现有翻译{#performing-initial-translations-and-updating-existing-translations}

AEM会检测是为内容的初始翻译创建翻译项目，还是更新已翻译的语言副本。 为页面创建翻译项目并指明要翻译的语言副本时，AEM会检测目标语言副本中是否已存在源页面：

* **语言副本不包含页面：AEM将** 此情况视为初始翻译。页面会立即复制到语言副本中并包含在项目中。 将翻译的页面导入AEM后，AEM会直接将其复制到语言副本。
* **语言副本已包含页面：AEM** 将此情况视为更新的翻译。此时会创建启动项，并将页面副本添加到启动项中，并包含在项目中。 启动项允许您在将更新的翻译提交到语言副本之前查看其：

   * 将已翻译的页面导入AEM后，将在启动项中覆盖该页面。
   * 仅当提升启动项时，译文页面才会覆盖语言副本。

例如，为/content/geometrixx/cn主控语言的法语翻译创建/content/geometrixx/fr语言根目录。 法文副本中没有其他页面。

* 将为/content/geometrixx/cn/products页面和所有子页面创建翻译项目，目标是法语语言副本。 由于语言副本不包括/content/geometrixx/fr/products页面，AEM会立即将/content/geometrixx/cn/products页面和所有子页面复制到法语语言副本。 这些副本也包含在翻译项目中。
* 将为/content/geometrixx/en页面和所有子页面创建翻译项目，目标为法语语言副本。 由于语言副本包括与/content/geometrixx/en页（语言根）对应的页面，AEM将复制/content/geometrixx/en页面和所有子页面，并将其添加到启动项。 这些副本也包含在翻译项目中。

## 使用“引用”面板{#creating-translation-projects-using-the-references-panel}创建翻译项目

创建翻译项目，以便执行和管理用于翻译您语言资源的工作流主控。 在创建项目时，您以要翻译的语言主控以及要执行翻译的语言副本指定页面：

* 与所选页面关联的翻译集成框架的云配置决定了翻译项目的许多属性，如要使用的翻译工作流。
* 将为所选的每个语言副本创建一个项目。
* 此时会创建选定页面和关联资产的副本并将其添加到每个项目。 这些副本稍后将发送给翻译提供商进行翻译。

您可以指定选定页面的子页面也被选定。 在这种情况下，子页面的副本也会添加到每个项目中，以便进行翻译。 当任何子页面与不同的翻译集成框架配置关联时，AEM会创建其他项目。

您还可以[手动创建翻译项目](#creating-a-translation-project-using-the-projects-console)。

**初始翻译和更新翻译**

“引用”面板指示您是更新现有语言副本还是创建语言副本的第一个版本。 当选定页面存在语言副本时，将显示“更新语言副本”选项卡，用于提供对项目相关命令的访问。

![chlimage_1-239](assets/chlimage_1-239.png)

翻译后，您可以在覆盖语言副本之前，[查看翻译](#reviewing-and-promoting-updated-content)。 当所选页面不存在语言副本时，将显示“创建并翻译”选项卡，提供对项目相关命令的访问。

![chlimage_1-240](assets/chlimage_1-240.png)

### 为新语言副本{#create-translation-projects-for-a-new-language-copy}创建翻译项目

1. 使用站点控制台选择要添加到翻译项目的页面。

   例如，要翻译Geometrixx演示站点的英文页面，请选择Geometrixx演示站点>英文。

1. 在工具栏中，单击或点按引用。

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. 选择“语言副本”，然后选择要翻译源页面的语言副本。
1. 单击或点按创建和翻译，然后配置翻译作业：

   * 使用语言下拉列表选择要翻译的语言副本。 根据需要选择其他语言。 列表中显示的语言与您创建的[语言根](/help/sites-administering/tc-prep.md#creating-a-language-root)对应。
   * 要翻译您选择的页面和所有子页面，请选择选择所有子页面。 要仅翻译您选择的选定页面，请清除该选项。
   * 对于“项目”，选择“创建新翻译项目”。
   * 键入项目的名称。

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. 单击或点按创建。

### 为现有语言副本{#create-translation-projects-for-an-existing-language-copy}创建翻译项目

1. 使用站点控制台选择要添加到翻译项目的页面。

   例如，要翻译Geometrixx演示站点的英文页面，请选择Geometrixx演示站点>英文。

1. 在工具栏中，单击或点按引用。

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. 选择“语言副本”，然后选择要翻译源页面的语言副本。
1. 单击或点按更新语言副本，然后配置转换作业：

   * 要翻译您选择的页面和所有子页面，请选择选择所有子页面。 要仅翻译您选择的选定页面，请清除该选项。
   * 对于“项目”，选择“创建新翻译项目”。
   * 键入项目的名称。

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. 单击或点按开始。

## 将页面添加到翻译项目{#adding-pages-to-a-translation-project}

创建翻译项目后，可以使用“资源”窗格向项目添加页面。 添加页面对于将来自同一项目中不同分支的页面包含在内非常有用。

将页面添加到翻译项目时，这些页面将包含在新的翻译作业中。 您还可以[向现有作业](#adding-pages-assets-to-a-translation-job)添加页面。

与创建新项目时一样，在添加页面时，页面的副本会在必要时添加到启动项，以避免覆盖现有语言副本。 （请参阅[为现有语言副本创建翻译项目](#performing-initial-translations-and-updating-existing-translations)。）

1. 使用站点控制台选择要添加到翻译项目的页面。

   例如，要翻译Geometrixx演示站点的英文页面，请选择Geometrixx演示站点>英文。

1. 在工具栏中，单击或点按引用。

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. 选择“语言副本”，然后选择要翻译源页面的语言副本。

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. 单击或点按更新语言副本，然后配置属性：

   * 要翻译您选择的页面和所有子页面，请选择选择所有子页面。 要仅翻译您选择的选定页面，请清除该选项。
   * 对于“项目”，选择“添加到现有翻译项目”。
   * 选择项目。

   >[!NOTE]
   >
   >在翻译项目中设置的目标语言应与语言副本的路径匹配，如引用面板中所示。

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. 单击或点按开始。

## 将页面／资产添加到转换作业{#adding-pages-assets-to-a-translation-job}

您可以向翻译项目的翻译作业中添加页面、资产、标记或i18n词典。 要添加页面或资产，请执行以下操作：

1. 在翻译项目的“翻译作业”拼贴的底部，单击或点按省略号。

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. 单击或点按添加和页面／资产。

   ![chlimage_1-248](assets/chlimage_1-247.png)

1. 选择要添加的分支的最上方的项目，然后单击或点按复选标记图标。 您可以进行多选。

   ![chlimage_1-248](assets/chlimage_1-248.png)

1. 或者，您也可以选择搜索图标，轻松查找要添加到翻译作业的页面或资产。

   ![chlimage_1-249](assets/chlimage_1-249.png)

您的页面和／或资产会添加到您的翻译作业。

## 将i18n词典添加到翻译作业{#adding-i-n-dictionaries-to-a-translation-job}

您可以向翻译项目的翻译作业中添加页面、资产、标记或i18n词典。 要添加i18n词典，请执行以下操作：

1. 在翻译项目的“翻译作业”拼贴的底部，单击或点按省略号。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 单击或点按添加和I18N词典。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 选择要添加的词典，然后单击或点按添加按钮。

   ![chlimage_1-252](assets/chlimage_1-252.png)

你的字典现在在翻译工作。

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>有关i18n字典的详细信息，请阅读[使用转换器管理字典](/help/sites-developing/i18n-translator.md)。

## 将标记添加到翻译作业{#adding-tags-to-a-translation-job}

您可以向翻译项目的翻译作业中添加页面、资产、标记或i18n词典。 添加标记：

1. 在翻译项目的“翻译作业”拼贴的底部，单击或点按省略号。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 单击或点按添加，然后单击标记。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择要添加的标记，然后单击或点按复选标记图标。 您可以进行多选。

   ![chlimage_1-256](assets/chlimage_1-256.png)

您的标记现已添加到翻译作业中。

![chlimage_1-257](assets/chlimage_1-257.png)

## 查看翻译项目详细信息{#seeing-translation-project-details}

翻译摘要拼贴包含为翻译项目配置的属性。 除了通用[项目信息](/help/sites-authoring/projects.md#project-info)之外，“转换”选项卡还包含转换特定属性：

* 源语言：正在翻译的页面的语言。
* 目标语：翻译页面时所用的语言。
* 翻译方法：翻译工作流。 支持人文翻译或机器翻译。
* 翻译提供商：执行翻译的翻译服务提供商。
* 内容类别:（机器翻译）用于翻译的内容类别。
* 云配置：用于项目的转换服务连接器的云配置。

当使用页面的“资源”窗格创建项目时，将根据源页面的属性自动配置这些属性。

![chlimage_1-258](assets/chlimage_1-258.png)

## 监视翻译作业的状态{#monitoring-the-status-of-a-translation-job}

翻译项目的翻译作业拼贴提供了翻译作业的状态以及作业中的页面和资产数量。

![chlimage_1-259](assets/chlimage_1-259.png)

下表描述了作业或作业中的项目可以具有的每种状态：

| 状态 | 描述 |
|---|---|
| 个草稿 | 转换作业尚未启动。 创建翻译作业时，其状态为“草稿”。 |
| 已提交 | 翻译作业中的文件在成功发送到翻译服务时具有此状态。 在发出请求范围命令或开始命令后，可能会出现此状态。 |
| 已请求设定范围 | 对于“人文翻译”工作流，作业中的文件已提交给翻译供应商进行范围界定。 发出“请求范围”命令后将显示此状态。 |
| 已完成范围的设定 | 供应商已确定翻译作业的范围。 |
| 承诺翻译 | 项目所有者已接受该范围。 此状态表示翻译供应商应开始翻译作业中的文件。 |
| 正在翻译 | 对于作业，该作业中一个或多个文件的翻译尚未完成。 对于作业中的某个项目，正在翻译该项目。 |
| 已翻译 | 对于作业，该作业中所有文件的翻译已完成。 对于作业中的某个项目，该项目将进行翻译。 |
| 准备审阅 | 作业中的项目已翻译，文件已导入AEM。 |
| 完成 | 项目所有者已表示翻译合同已完成。 |
| 取消 | 指示翻译供应商应停止处理翻译作业。 |
| 错误更新 | 在AEM和翻译服务之间传输文件时出错。 |
| 未知状态 | 出现未知错误。 |

要查看作业中每个文件的状态，请单击或点按拼贴底部的省略号。

## 设置转换作业的到期日期{#setting-the-due-date-of-translation-jobs}

指定翻译供应商需要返回翻译文件的日期。 您可以为项目或特定作业设置截止日期：

* **项目：** 项目中的转换作业继承到期日期。
* **作业：** 您为作业设置的到期日将覆盖为项目设置的到期日。

仅当您所使用的翻译供应商支持此功能时，才能正确设置到期日期。

以下过程设置项目的到期日。

1. 单击或点按“翻译摘要”拼贴底部的省略号。

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. 在“基本”选项卡上，使用“到期日期”属性的日期选取器选择到期日。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. 单击或点按完成。

以下过程设置翻译作业的到期日期。

1. 在转换作业拼贴中，单击或点按命令菜单，然后单击或点按到期日。

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. 在对话框中，单击或点按日历图标，然后选择要用作截止日期的日期和时间，然后单击保存。

   ![chlimage_1-263](assets/chlimage_1-263.png)

## 范围转换作业{#scoping-a-translation-job}

对翻译作业进行范围设置，以从您的翻译服务提供商获得翻译成本的估计。 当您对作业进行范围设置时，源文件将提交给翻译供应商，该供应商将文本与其存储的翻译池（翻译记忆库）进行比较。 通常，范围是需要翻译的词数。

要获取有关范围界定结果的更多信息，请与翻译供应商联系。

>[!NOTE]
>
>范围确定是可选的。 您可以开始翻译作业，而不进行范围界定。

当您对转换作业进行作用域时，该作业的状态为`Scope Requested`。 当转换供应商返回范围时，状态将更改为`Scope Completed`。 完成作业范围时，可以使用“显示范围”命令查看作业范围结果。

仅当您使用的翻译供应商支持此功能时，范围确定才能正确工作。

1. 在“项目”控制台中，打开您的翻译项目。
1. 在转换作业拼贴中，单击或点按命令菜单，然后单击或点按请求范围。

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. 当作业状态更改为SCOPE_COMPLETED时，在转换作业拼贴上单击或点按命令菜单，然后单击或点按显示范围。

## 启动转换作业{#starting-a-translation-job}

开始将源页面翻译为目标语的翻译作业。 将根据“翻译摘要”拼贴的属性值执行翻译。

开始翻译作业后，“翻译作业”拼贴会显示“正在进行翻译”状态。

![chlimage_1-265](assets/chlimage_1-265.png)

1. 在“项目”控制台中，打开翻译项目。
1. 在转换作业拼贴中，单击或点按命令菜单，然后单击或点按开始。

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. 在确认翻译开始的操作对话框中，单击或点按关闭。

## 取消转换作业{#canceling-a-translation-job}

取消翻译作业以停止翻译过程并阻止翻译供应商执行任何其他翻译。 当作业的状态为`Committed For Translation`或`Translation In Progress`时，可以取消作业。

1. 在“项目”控制台中，打开翻译项目。
1. 在转换作业拼贴中，单击或点按命令菜单，然后单击或点按取消。
1. 在确认取消翻译的操作对话框中，单击或点按确定。

## 接受／拒绝工作流{#accept-reject-workflow}

当内容在翻译后返回且处于“准备审阅”状态时，您可以进入翻译作业并接受／拒绝内容。

![chlimage_1-267](assets/chlimage_1-267.png)

如果选择“拒绝翻译”，则可以选择添加评论。

![chlimage_1-268](assets/chlimage_1-268.png)

拒绝内容会将其发送回翻译供应商，他将能够在该供应商处看到评论。

## 查看和提升更新的内容{#reviewing-and-promoting-updated-content}

为现有语言副本翻译内容时，请查看翻译，根据需要进行更改，然后提升翻译以将其移至语言副本。 当翻译作业显示“准备审阅”状态时，您可以审阅已翻译的文件。

![chlimage_1-269](assets/chlimage_1-269.png)

1. 以语言主控选择页面，单击或点按引用，然后单击或点按语言副本。
1. 单击或点按要查看的语言副本。

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. 单击或点按启动项以显示与启动项相关的命令。

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. 要打开要查看和编辑内容的页面的启动项副本，请单击打开页面。
1. 查看内容并进行必要更改后，要提升启动项副本，请单击提升。
1. 在提升启动项页面上，指定要提升的页面，然后单击或点按提升。

## 比较语言副本{#comparing-language-copies}

要将语言副本与语言主控比较，请执行以下操作：

1. 在&#x200B;**站点**&#x200B;控制台中，导航到要比较的语言副本。
1. 打开&#x200B;**[引用](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板。
1. 在&#x200B;**副本**&#x200B;标题下，选择&#x200B;**语言副本。**
1. 选择您的特定语言副本，然后单击**与主控的**比较，或**与先前的**比较（如果适用）。

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. 此时将并列打开两个页面（启动页面和源页面）。

   有关使用此功能的完整信息，请参阅[页面差异](/help/sites-authoring/page-diff.md)。

## 正在完成和存档转换作业{#completing-and-archiving-translation-jobs}

在您查看了供应商提供的已翻译文件后完成翻译作业。 对于人文翻译工作流，完成翻译会向供应商表明翻译合同已履行，并且他们应将翻译保存到其翻译记忆库。

完成作业后，该作业将显示“完成”状态。

![chlimage_1-272](assets/chlimage_1-272.png)

在翻译作业完成后存档该作业，您不再需要查看作业状态详细信息。 存档作业时，将从项目中删除翻译作业拼贴。

## 创建语言副本的结构{#creating-the-structure-of-a-language-copy}

填充您的语言副本，使其包含您正在翻译的主控语言的内容。 在填充语言副本之前，必须先创建语言副本的语言根[。](/help/sites-administering/tc-prep.md#creating-a-language-root)

1. 使用“站点”控制台选择您用作源的主控语言的语言根。 例如，要翻译Geometrixx演示站点的英语页面，请选择“内容”>“Geometrixx演示站点”>“英语”。
1. 在工具栏中，单击或点按引用。

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. 选择“语言副本”，然后选择要填充的语言副本。

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. 单击或点按更新语言副本以显示翻译工具，并配置属性：

   * 选择“选择所有子页面”选项。
   * 对于“项目”，选择“仅创建结构”。

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. 单击或点按开始。

## 使用项目控制台{#creating-a-translation-project-using-the-projects-console}创建翻译项目

如果您希望使用“项目”控制台，可以手动创建翻译项目。

在手动创建翻译项目时，除了[基本属性](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project)之外，还必须提供以下与翻译相关的属性的值：

* **名称：** 项目名称。
* **源语言：** 源内容的语言。
* **目标语** 言：内容翻译到的语言。
* **翻译方法：** 选择“人工翻译”以指示要手动执行翻译。

1. 在项目控制台的工具栏中，单击或点按创建。
1. 选择翻译项目模板，然后单击或点按下一步。
1. 输入基本属性的值。
1. 单击或点按高级，并提供与翻译相关的属性的值。
1. 单击或点按创建。在确认框中，单击或点按完成以返回到项目控制台，或单击或点按打开项目以打开和开始管理项目。

## 导出转换作业{#exporting-a-translation-job}

您可以下载翻译作业的内容，例如，通过连接器发送到未与AEM集成的翻译提供商，或查看内容。

1. 从翻译作业拼贴的下拉菜单中，单击或点按导出。
1. 在“导出”对话框中，单击或点按“下载导出的文件”，如有必要，请使用Web浏览器对话框保存文件。
1. 在“导出”对话框中，单击或点按关闭。

## 导入转换作业{#importing-a-translation-job}

您可以将已翻译的内容导入AEM，例如，当翻译提供商将翻译内容发送给您时，因为这些内容未通过连接器与AEM集成。

1. 从翻译作业拼贴的下拉菜单中，单击或点按导入。
1. 使用Web浏览器的对话框选择要导入的文件。
1. 在“导入”对话框中，单击或点按关闭。

