---
title: 设置您的营销活动
seo-title: 设置您的营销活动
description: 要设置新营销活动，需要创建品牌以保存您的营销活动，然后创建营销活动以保存体验，最后为新营销活动定义属性。
seo-description: 要设置新营销活动，需要创建品牌以保存您的营销活动，然后创建营销活动以保存体验，最后为新营销活动定义属性。
uuid: 244a150e-7b5e-4eff-bd15-e3b04be6a3e9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 19ad4751-1d5d-49de-b76b-3501b3e98e62
docset: aem65
translation-type: tm+mt
source-git-commit: dc1985c25c797f7b994f30195d0586f867f9b3ee

---


# 设置您的营销活动{#setting-up-your-campaign}

设置新营销活动包括以下（一般）步骤：

1. [创建品牌](#creating-a-new-brand)以保存您的营销活动。
1. 如果需要，您可以[为新品牌定义属性](#defining-the-properties-for-your-new-brand)。
1. [创建营销活动](#creating-a-new-campaign)以保存体验（例如 Teaser 页面或新闻稿）。
1. 如果需要，您可以[为新营销活动定义属性](#defining-the-properties-for-your-new-campaign)。

然后，根据要创建的体验类型，您需要[创建体验](#creating-a-new-experience)。体验的细节和体验创建之后的操作取决于您要创建的体验类型：

* 如果创建 Teaser：

   1. [创建 Teaser 体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience)。
   1. [向 Teaser 中添加内容](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser)。
   1. [为 Teaser 创建触点](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser)（将 Teaser 添加到内容页面）。

* 如果创建新闻稿：

   1. [创建新闻稿体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience)。
   1. [向新闻稿中添加内容](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)。
   1. [对新闻稿进行个性化设置](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)。
   1. [创建引人注目的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。
   1. 向订阅者或潜在客户[发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)。

* 如果创建 Adobe Target（以前称为 Test&amp;Target）选件：

   1. [创建 Adobe Target 选件体验](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience)。
   1. [与 Adobe Target 集成](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)。

>[!NOTE]
>
>请参阅[分段](/help/sites-administering/campaign-segmentation.md)，以了解有关定义区段的详细说明。

## 创建新品牌 {#creating-a-new-brand}

要创建新的品牌：

1. 打开 **MCM**，然后在左边窗格选择&#x200B;**营销活动**。

1. 选择&#x200B;**新建...**&#x200B;以输入&#x200B;**标题**&#x200B;和&#x200B;**名称**&#x200B;和要用于新品牌的模板：

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 单击&#x200B;**创建**。您的新品牌将在 MCM 中显示（带有默认图标）。

### 为您的新品牌定义属性 {#defining-the-properties-for-your-new-brand}

1. 从左边窗格中选择&#x200B;**营销活动**，然后在右边窗格中选择您的新品牌图标并单击&#x200B;**属性...**

   您可以输入&#x200B;**标题**、**说明**，以及要用作图标的图像。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

### 创建新营销活动 {#creating-a-new-campaign}

创建新的营销活动：

1. 从&#x200B;**营销活动**&#x200B;中，选择左边窗格中您的新品牌，或者双击右边窗格中的图标。

   将会显示概述（如果是新品牌，则概述为空）。

1. 单击&#x200B;**新建...**，然后指定&#x200B;**标题**、**名称**&#x200B;和要用作您的新营销活动的模板。

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. 单击&#x200B;**创建**。您的新营销活动将显示在 MCM 中。

### 定义新营销活动的属性 {#defining-the-properties-for-your-new-campaign}

配置以下可控制行为的营销活动属性：

* **优先级：**&#x200B;该营销活动相对于其他营销活动的优先级。当多个营销活动同时开启时，优先级最高的营销活动将控制访客体验。
* **“开始时间”和“结束时间”：**&#x200B;这两个属性可控制营销活动对访客体验的控制时间段。“开始时间”属性控制营销活动开始控制体验的时间。“结束时间”属性控制营销活动停止控制体验的时间。
* **图像：**&#x200B;在 AEM 中表示营销活动的图像。
* **云服务：**&#x200B;与营销活动集成的云服务配置。（请参阅[与 Adobe Marketing Cloud 集成](/help/sites-administering/marketing-cloud.md)。）

* **Adobe Target：**&#x200B;这些属性用于配置与 Adobe Target 集成的营销活动。（请参阅[与 Adobe Target 集成](/help/sites-administering/target.md)。）

1. 从&#x200B;**营销活动**&#x200B;中，选择您的品牌。在右侧窗格中，选择您的营销活动，然后单击&#x200B;**属性**。

   您可以输入各种属性，包括“**标题**”、“**说明**”和所需的任何“**云服务**”。

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

### 创建新体验 {#creating-a-new-experience}

创建新体验的步骤取决于体验类型：

* [创建 Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [创建新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [创建 Adobe Target 选件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>和之前的版本一样，仍然可以在&#x200B;**网站**&#x200B;控制台中将创建体验并作为页面（并且在之前版本中创建的所有此类页面都仍然完全受支持）。
>
>现在建议使用 MCM 来创建体验。

### 配置新体验 {#configuring-your-new-experience}

既然您已为体验创建了基本梗概，则还需要根据相应体验类型继续执行以下操作：

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers):

   * [将 Teaser 页面连接到访客区段。](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [为 Teaser 创建触点](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser)（将 Teaser 添加到内容页面）。

* [新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)：

   * [向新闻稿中添加内容](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)。
   * [对新闻稿进行个性化设置](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)。
   * 向订阅者或潜在客户[发送新闻稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters)。
   * [创建引人注目的新闻稿登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage)。

* [Adobe Target 选件](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers)：

   * [与 Adobe Target 集成](/help/sites-administering/target.md)。

### 添加新触点 {#adding-a-new-touchpoint}

如果您已有体验，则可以从 MCM 的日历视图直接添加触点：

1. 为营销活动选择日历视图。

1. 单击&#x200B;**添加触点...**&#x200B;打开对话框。指定您要添加的体验：

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 单击&#x200B;**确定**&#x200B;进行保存。

## 使用潜在客户 {#working-with-leads}

>[!NOTE]
>
>Adobe 不打算进一步增强此功能（管理潜在客户）。
>Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

在 AEM MCM 中，您可以组织和添加潜在客户，方法是手动输入，或导入逗号分隔的列表（例如邮寄列表）。生成潜在客户的其他方法包括 Newsletter 注册或社区注册（经配置后，它们可触发生成潜在客户的工作流）。

潜在客户通常会进行分类，并被放入列表中，以使您之后可以对整个列表执行操作（例如，向特定列表发出自定义电子邮件）。

在信息面板中，您可通过单击左侧窗格的&#x200B;**潜在客户**&#x200B;来访问所有潜在客户。还可从&#x200B;**列表**&#x200B;窗格中访问潜在客户。

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>要添加或修改用户的头像，请打开 Clickstream Cloud (Ctrl+Alt+c)，加载个人资料，并单击&#x200B;**编辑**。

### 创建新潜在客户 {#creating-new-leads}

创建新潜在客户后，请务必[激活潜在客户](#activating-or-deactivating-leads)，以便跟踪其发布实例活动并对其体验进行个性化设置。

手动创建新潜在客户：

1. 在 AEM 中，导航到 MCM。在功能板中，单击&#x200B;**潜在客户**。
1. 单击&#x200B;**新建**。**新建**&#x200B;窗口将打开。

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. 根据需要，在字段中输入信息。单击&#x200B;**地址**&#x200B;选项卡。

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. 根据需要，输入地址信息。单击&#x200B;**保存**&#x200B;保存该潜在客户。如果需要添加更多潜在客户，则单击&#x200B;**保存并新建**。

   潜在客户窗格中将显示新潜在客户。在单击该条目后，输入的所有信息将显示在右侧窗格中。在创建潜在客户后，可以将其添加到列表中。

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### 激活或取消激活潜在客户 {#activating-or-deactivating-leads}

激活潜在客户可帮助您跟踪其发布实例活动，使您可以个性化设置其体验。如果不想再跟踪其活动，可取消激活。

激活或取消激活潜在客户：

1. 在 AEM 中，导航到 MCM，并单击&#x200B;**潜在客户**。

1. 选择要激活或取消激活的潜在客户，并单击&#x200B;**激活**&#x200B;或&#x200B;**取消激活**。

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   与 AEM 页面一样，发布状态显示在&#x200B;**已发布**&#x200B;列。

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### 导入新潜在客户 {#importing-new-leads}

在导入新潜在客户时，可以向现有列表自动添加它们，也可以创建包含这些潜在客户的新列表。

要从逗号分隔的列表导入潜在客户，请执行以下操作：

1. 在 AEM 中，导航到 MCM，并单击&#x200B;**潜在客户**。

   >[!NOTE]
   >
   >或者，可通过执行以下操作之一导入潜在客户：
   >
   >
   >
   >    * 在信息面板中，单击&#x200B;**列表**&#x200B;窗格中的&#x200B;**导入潜在客户**
      >
      >    
   * 单击&#x200B;**列表**，然后在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**导入潜在客户**。


1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**导入****潜在客户**。

1. 输入“采样数据”中所述的信息。可以导入以下字段：email,familyName,givenName,gender,aboutMe,city,country,phoneNumber,postalCode,region,streetAddress

   >[!NOTE]
   >
   >CSV 列表中的第一行为预定义标签，必须严格按以下示例写入：
   >
   >
   >`email,givenName,familyName` -例如，如 `givenname`果编写为，系统将无法识别它。

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. 单击&#x200B;**下一步**。您可以在此处预览这些潜在客户，以确保其准确无误。

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. 单击&#x200B;**下一步**。选择希望这些潜在客户所属的列表。如果不希望其属于列表，请删除该字段中的信息。默认情况下，AEM 会创建一个包含日期和时间的列表名称。单击&#x200B;**导入**。

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   潜在客户窗格中将显示新潜在客户。在单击该条目后，输入的所有信息将显示在右侧窗格中。在创建潜在客户后，可以将其添加到列表中。

### 将潜在客户添加到列表 {#adding-leads-to-lists}

向预先存在的列表中添加潜在客户：

1. 在 MCM 中，单击&#x200B;**潜在客户**&#x200B;以查看所有可用的潜在客户。

1. 选择要添加到列表中的潜在客户，方法是选中相应潜在客户旁的复选框。可以添加的潜在客户数量没有限制。

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**添加到列表...**。**添加到列表**&#x200B;窗口将打开。

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. 选择要向其添加潜在客户的列表，并单击&#x200B;**确定**。这些潜在客户将添加到相应列表中。

### 查看潜在客户信息 {#viewing-lead-information}

要查看潜在客户信息，请在 MCM 中，单击相应潜在客户旁的复选框，右侧窗格将打开，其中显示该潜在客户的所有信息，包括列表从属关系。

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### 修改现有潜在客户 {#modifying-existing-leads}

修改现有潜在客户信息：

1. 在 MCM 中，单击&#x200B;**潜在客户**。在潜在客户列表中，选中要编辑的潜在客户旁的复选框。该潜在客户的所有信息将显示在右侧窗格中。

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >一次只能编辑一个潜在客户。如果需要修改同一列表中的多个潜在客户，可修改该列表。

1. 单击&#x200B;**编辑**。**编辑潜在客户**&#x200B;窗口将打开。

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. 根据需要进行编辑，并单击&#x200B;**保存**&#x200B;以保存更改。

   >[!NOTE]
   >
   >要更改潜在客户头像，请转到用户个人资料。可以在 Clickstream Cloud 中加载个人资料，方法是按 CTRL+ALT+c，单击&#x200B;**加载**，然后选择个人资料。

### 删除现有潜在客户 {#deleting-existing-leads}

要在 MCM 中删除现有潜在客户，请选中该潜在客户旁的复选框，并单击&#x200B;**删除**。该潜在客户即会从该潜在客户列表和所有相关列表中删除。

>[!NOTE]
>
>在删除之前，AEM 会确认您是否要删除现有潜在客户。在删除后，无法检索它。

## 使用列表 {#working-with-lists}

>[!NOTE]
>
>Adobe 不打算进一步增强此功能（管理列表）。
>Adobe 的建议是[利用 Adobe Campaign 以及将其与 AEM 集成](/help/sites-administering/campaign.md)。

使用列表可将您的潜在客户组织到组中。借助列表，可以将营销活动定向到所选客户组，例如，可以向特定列表发送目标新闻稿。在 MCM 中，列表会显示在功能板中，也可以通过单击&#x200B;**列表**&#x200B;显示。这两种方法都可提供列表名称和成员数量。

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

如果单击&#x200B;**列表**，则还可查看该列表是否为另一个列表的成员，并可看到说明。

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### 创建新列表 {#creating-new-lists}

创建新列表（组）：

1. 在 MCM 信息面板中，单击&#x200B;**新建列表...**，或者在&#x200B;**列表**&#x200B;中，单击&#x200B;**新建**...。“创建列表”窗口将打开。

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. 输入名称（必填），并根据需要输入说明，然后单击&#x200B;**保存**。该列表将显示在&#x200B;**列表**&#x200B;窗格中。

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### 修改现有列表 {#modifying-existing-lists}

修改现有列表：

1. 在 MCM 中，单击&#x200B;**列表**。

1. 在列表中，选中要编辑的列表旁的复选框，并单击&#x200B;**编辑**。**编辑列表**&#x200B;窗口将打开。

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >一次只能编辑一个列表。

1. 根据需要进行编辑，并单击&#x200B;**保存**&#x200B;以保存更改。

### 删除现有列表 {#deleting-existing-lists}

要删除现有列表，请在 MCM 中，选中该列表旁的复选框，并单击&#x200B;**删除**。该列表即已删除。从属于该列表的潜在客户不会被删除，仅删除与该列表的从属关系。

>[!NOTE]
>
>在删除之前，AEM 会确认您是否要删除现有列表。在删除后，无法检索它。

### 合并列表 {#merging-lists}

您可以将现有列表与另一个列表合并。在执行此操作时，要合并的列表将变成另一个列表的成员。它仍将作为单独的实体存在，不能被删除。

如果您在两个不同的位置召开同一会议，并且希望将它们合并到所有会议的与会者列表中，则可以合并列表。

要合并现有列表，请执行以下操作：

1. 在 MCM 中，单击&#x200B;**列表**。

1. 选择要与另一个列表合并的列表，方法是选中该列表旁的复选框。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**合并列表**。

   >[!NOTE]
   >
   >一次只能合并一个列表。

1. 在&#x200B;**合并列表**&#x200B;窗口中，选择要与之合并的列表，并单击&#x200B;**确定**。

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   合并的列表应增加一个成员。要查看列表是否已合并，请选择合并的列表，并在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**显示潜在客户**。

1. 重复该步骤，直至合并完所需的所有列表。

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>从成员资格中删除合并的列表与从列表中删除潜在客户一样。打开&#x200B;**列表**&#x200B;选项卡，选择包含合并列表的列表，并通过单击该列表旁的红色圆圈来删除成员资格。

### 查看列表中的潜在客户 {#viewing-leads-in-lists}

您随时可以通过浏览或搜索成员来查看属于特定列表的潜在客户。

查看属于特定列表的潜在客户：

1. 在 MCM 中，单击&#x200B;**列表**。

1. 选中要查看其成员的列表旁的复选框。

1. 在&#x200B;**工具**&#x200B;菜单中，选择&#x200B;**显示潜在客户**。AEM 会显示属于该列表成员的潜在客户。您可以浏览列表或搜索成员。

   >[!NOTE]
   >
   >此外，还可以从列表中删除潜在客户，方法是选择它们，然后单击&#x200B;**删除成员资格**。

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. 单击&#x200B;**关闭**&#x200B;返回 MCM。
