---
title: 在自适应表单中使用Adobe Sign
seo-title: 在自适应表单中使用Adobe Sign
description: 为自适应表单启用电子签名(Adobe Sign)工作流，以自动执行签名工作流，简化单个和多签名流程，以及通过移动设备对表单进行电子签名。
seo-description: 为自适应表单启用电子签名(Adobe Sign)工作流，以自动执行签名工作流，简化单个和多签名流程，以及通过移动设备对表单进行电子签名。
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: 自适应Forms,Adobe Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 0%

---

# 在自适应表单{#using-adobe-sign-in-an-adaptive-form}中使用[!DNL Adobe Sign]

[!DNL Adobe Sign] 为自适应表单启用电子签名工作流。电子签名可改进工作流程，以处理法律、销售、工资、人力资源管理等领域的文档。

在典型的[!DNL Adobe Sign]和自适应表单场景中，用户填充自适应表单以申请服务。 例如，抵押贷款和信用卡申请要求所有借款人和共同申请人签名。 要为类似情景启用电子签名工作流，您可以将[!DNL Adobe Sign]与AEM [!DNL Forms]集成。 还有一些示例，您可以使用[!DNL Adobe Sign]执行以下操作：

* 通过完全自动化的建议书、报价和合同流程，与任何设备达成交易。
* 更快地完成人力资源流程，并为员工提供数字体验。
* 缩短合同周期并更快地载入您的供应商。
* 创建可自动处理常见流程的数字工作流。

[!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 支持：

* 单用户和多用户签名工作流
* 顺序和同时的签名工作流
* 表单内和表单外的签名体验
* 以匿名或已登录用户的身份对表单进行签名
* 动态签名流程(与AEM [!DNL Forms]工作流集成)
* 通过知识库、电话和社交用户档案进行身份验证

了解将Adobe Sign与自适应表单结合使用的[最佳实践](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)，以创建更好的签名体验。

## 前提条件 {#prerequisites}

在自适应表单中使用[!DNL Adobe Sign]之前：

* 确保将AEM [!DNL Forms]云服务配置为使用[!DNL Adobe Sign]。 有关详细信息，请参阅[将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)。
* 请准备好签名者列表。 您至少需要每个签名者的电子邮件地址。

## 为自适应表单{#configure-adobe-sign-for-an-adaptive-form}配置[!DNL Adobe Sign]

执行以下步骤来配置自适应表单的[!DNL Adobe Sign]:

1. [编辑自适应表单属性以用于Adobe符号](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [将Adobe Sign字段添加到自适应表单](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [为自适应表单启用Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [为自适应表单选择Adobe SignCloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [将Adobe Sign签名者添加到自适应表单](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [为自适应表单选择提交操作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![签名者详细信息](assets/signer_details_new.png)

### 编辑[!DNL Adobe Sign]的自适应表单属性 {#enableadobesign}

为现有或新的自适应表单配置[!DNL Adobe Sign]的自适应表单属性。

[为Adobe创建自适应表单](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 描述了创建基本自适应表单的步骤。请参阅[创建自适应表单](../../forms/using/creating-adaptive-form.md) ，以了解创建自适应表单时可用的其他选项。

#### 为[!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}创建自适应表单

执行以下步骤以创建启用符号的自适应表单：

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 自适应表单]**。 此时会显示模板列表。 选择模板，然后点按&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL Basic]**&#x200B;选项卡中：

   1. 为自适应表单指定&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 标题]**。

   1. 选择在使用AEM [!DNL Forms]配置[!DNL Adobe Sign]时创建的[配置容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。

      >[!NOTE]
      >
      >**[!UICONTROL Adobe SignCloud Service]**&#x200B;下拉列表显示在您在此字段中选择的配置容器中配置的云服务。 选择&#x200B;**[!UICONTROL 启用Adobe Sign]**&#x200B;选项时，自适应表单属性的&#x200B;**[!UICONTROL Adobe SignCloud Service]**&#x200B;下拉列表可在&#x200B;**[!UICONTROL 电子签名]**&#x200B;部分中找到。

1. 在&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡中，选择以下选项之一：

   * 选择&#x200B;**[!UICONTROL 关联表单模板作为记录文档模板]**&#x200B;选项，然后选择记录文档模板。 如果您使用基于表单模板的自适应表单，则发送进行签名的文档将仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   * 选择&#x200B;**[!UICONTROL 生成记录文档]**&#x200B;选项。 如果使用启用了“记录文档”选项的自适应表单，则发送以供签名的文档将显示自适应表单的所有字段。

1. 点按&#x200B;**[!UICONTROL 创建。]** 将创建启用符号的自适应表单，该表单可用于添加 [!DNL Adobe Sign] 字段。

#### 编辑[!DNL Adobe Sign]的自适应表单 {#editafsign}

执行以下步骤以在现有自适应表单中使用[!DNL Adobe Sign]:

1. 导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应表单，然后点按&#x200B;**[!UICONTROL 属性]**。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡中，选择使用AEM [!DNL Forms]配置[!DNL Adobe Sign]时创建的[配置容器](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)。
1. 在&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡中，选择以下选项之一：

   * 选择&#x200B;**[!UICONTROL 关联表单模板作为记录文档模板]**&#x200B;选项，然后选择记录文档模板。 如果您使用基于表单模板的自适应表单，则发送进行签名的文档将仅显示基于关联表单模板的字段。 它不会显示自适应表单的所有字段。

   * 选择&#x200B;**[!UICONTROL 生成记录文档]**&#x200B;选项。 如果使用启用了“记录文档”选项的自适应表单，则发送以供签名的文档将显示自适应表单的所有字段。

1. 点按&#x200B;**[!UICONTROL 保存并关闭]**。 已为[!DNL Adobe Sign]启用自适应表单。

### 将Adobe Sign字段添加到自适应表单 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 具有可放置在自适应表单上的各种字段。这些字段接受各种类型的数据（如签名、缩写、公司或标题），并帮助在签名期间收集额外信息以及签名。 您可以使用[!DNL Adobe Sign]块组件将[!DNL Adobe Sign]字段放置在自适应表单中的不同位置。

执行以下步骤，向自适应表单添加字段并自定义与这些字段相关的各种选项：

1. 将&#x200B;**[!UICONTROL Adobe Sign块]**&#x200B;组件从组件浏览器拖放到自适应表单。 [!DNL Adobe Sign]块组件具有所有受支持的[!DNL Adobe Sign]字段。 默认情况下，它会向自适应表单中添加&#x200B;**签名**&#x200B;字段。

   ![符号块](assets/sign_block_new.png)

   默认情况下， [!DNL Adobe Sign]块在已发布的自适应表单中不可见。 它仅在签名文档中可见。 您可以从[!DNL Adobe Sign]块组件的属性中更改[!DNL Adobe Sign]块的可见性。

   >[!NOTE]
   >
   >    * 在自适应表单中使用[!DNL Adobe Sign]块并非强制要求。 [!DNL Adobe Sign]如果不使用[!DNL Adobe Sign]块并为签名者添加字段，则默认签名字段将显示在签名文档的底部。
   >    * 仅对自动生成记录文档的自适应表单使用[!DNL Adobe Sign]块。 如果使用自定义XDP生成记录文档或基于表单模板的自适应表单，则不支持[!DNL Adobe Sign]块。


1. 选择&#x200B;**[!UICONTROL Adobe Sign块]**&#x200B;组件，然后点按&#x200B;**编辑** ![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.选** 择和添加 [!DNL Adobe Sign] 字段。**B.将** 块展 [!DNL Adobe Sign] 开为全屏视图

1. 点按&#x200B;**[!UICONTROL Adobe Sign]字段** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png)图标。 它显示用于选择和添加[!DNL Adobe Sign]字段的选项。

   展开&#x200B;**[!UICONTROL 类型]**&#x200B;下拉字段以选择[!DNL Adobe Sign]字段，然后点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标，以将所选字段添加到[!DNL Adobe Sign]块。 **[!UICONTROL Type]**&#x200B;下拉字段包括“签名”、“签名者信息”和“数据”字段类型。 [!DNL Adobe Sign] 与AEM支持 [!DNL Forms] 字段的集成(仅  在“类型”下拉框中列出)。有关[!DNL Adobe Sign]字段的详细信息，请参阅[Adobe Sign文档](https://helpx.adobe.com/sign/help/field-types.html)。

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   必须为字段提供唯一的名称。 您还可以选择必需选项来将字段标记为必填。 除了&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 必需]**&#x200B;选项外，某些[!DNL Adobe Sign]字段还有更多选项。 例如，蒙版和多行。 此外，无论字段位于相同还是不同的[!DNL Adobe Sign]块中，都为每个[!DNL Adobe Sign]字段指定唯一的名称。

   如果从下拉列表中选择&#x200B;**[!UICONTROL 数字签名]**，则可以将数字签名应用到自适应表单：

   * 在线使用云签名使用由信任服务提供商托管的[数字ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)进行签名。
   * 通过使用智能卡、USB令牌或基于文件的数字ID下载包含Adobe Acrobat或Reader的文档，从本地进行。

### 为自适应表单启用[!DNL Adobe Sign] {#enableadobsignforanadaptiveform}

开箱即用地，未为自适应表单启用[!DNL Adobe Sign]。 请执行以下步骤以启用它：

1. 在内容浏览器中，点按&#x200B;**[!UICONTROL 表单容器]**，然后点按&#x200B;**[!UICONTROL 配置]** ![配置](assets/configure.png)图标。 它会打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开&#x200B;**[!UICONTROL 电子签名]**&#x200B;折叠面板，然后选择&#x200B;**[!UICONTROL 启用Adobe Sign]**&#x200B;选项。 它为自适应表单启用[!DNL Adobe Sign]。

### 选择[!DNL Adobe Sign]Cloud Service和签名顺序 {#selectadobesigncloudserviceforanadaptiveform}

您可以为AEM [!DNL Forms]的实例配置多个[!DNL Adobe Sign]服务。 建议为每个功能（人力资源、财务等）单独提供一组服务。 它使跟踪和报告已签名文档变得更轻松。 例如，银行有多个部门。 您可以为每个部门单独配置以更好地跟踪文档。

文档还可以有多个签名者。 例如，信用卡申请可以有多个申请人。 银行在开始处理申请之前需要所有申请人的签名。 对于多签名者方案，您可以选择按顺序或同时顺序对文档进行签名。

执行以下步骤以选择云服务和签名顺序：

![云服务](assets/cloud-service.png)

1. 在内容浏览器中，点按&#x200B;**[!UICONTROL 表单容器]**，然后点按&#x200B;**[!UICONTROL 配置]** ![配置](assets/configure.png)图标。 它会打开属性浏览器并显示自适应表单容器属性。
1. 在属性浏览器中，展开&#x200B;**[!UICONTROL 电子签名]**&#x200B;折叠面板，然后选择&#x200B;**[!UICONTROL 启用Adobe Sign]**&#x200B;选项。 它为自适应表单启用[!DNL Adobe Sign]。
1. 从已配置的[!DNL Adobe Sign]Cloud Services列表中选择云服务。

   如果&#x200B;**[!UICONTROL Adobe SignCloud Service]**&#x200B;列表为空，请按照[使用AEM Forms配置Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md)一文配置服务。

   此下拉列表列出了工具> **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;的`global`文件夹中存在的云服务。 此外，该下拉列表还列出了在创建自适应表单时，您在&#x200B;**[!UICONTROL 配置容器]**&#x200B;字段中选择的文件夹中存在的云服务。

1. 从&#x200B;**[!UICONTROL 签名者可以签名]**&#x200B;对话框中选择签名顺序。 [!DNL Adobe Sign] 歌手可以按顺序 **[!UICONTROL 对自适应表单进行]** (依次为另一个签名者，或 **[!UICONTROL 同时]** )签名。

   按顺序，一个签名者每次接收用于签名的表单。 签名者完成对文档的签名后，表单会发送给下一位签名者，依此类推。

   同时，多个签名者一次可以签署一个表单。

1. [将签名者添加到自](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 适应格式，然后点 ![按完成aem_6_3_forms_](assets/aem_6_3_forms_save.png) save图标以保存更改。


### 将签名者添加到自适应表单 {#addsignerstoanadaptiveform}

自适应表单只能有一个或多个签名者。 添加签名者时，您还可以为签名者配置身份验证详细信息。 您还可以选择表单填充者和歌手是否是同一个人。 执行以下步骤以添加和提供有关签名者的各种详细信息：

1. 在内容浏览器中，点按&#x200B;**[!UICONTROL 表单容器]**，然后点按&#x200B;**[!UICONTROL 配置]** ![配置](assets/configure.png)图标。 它会打开具有自适应表单容器属性的属性浏览器。
1. 在属性浏览器中，展开&#x200B;**[!UICONTROL 电子签名]**&#x200B;折叠面板，然后选择&#x200B;**[!UICONTROL 启用Adobe Sign]**&#x200B;选项。 它为自适应表单启用[!DNL Adobe Sign]。
1. 点按&#x200B;**[!UICONTROL 签名者配置]**&#x200B;下的&#x200B;**[!UICONTROL 添加签名者]**。 它会向自适应表单中添加签名者。 您可以向自适应表单中添加多个[!DNL Adobe Sign]签名者。
   ![电话详细信息](assets/phone-details.png)

1. 单击&#x200B;**编辑** ![aem_6_3_edit](assets/aem_6_3_edit.png)图标以指定有关签名者的以下信息：

   * **[!UICONTROL 标题]:** 指定一个标题以唯一标识签名者。

   * **[!UICONTROL 签名者与填写表单的人员是否为同一人？]:** 如果表 **单填写者和第一个签名者是同一个人，请选择是**。如果将选项设置为&#x200B;**No，**，则不要在自适应表单中使用签名步骤组件。 如果表单包含签名步骤组件，则字段会自动设置为“是”。

   * **[!UICONTROL 签名者电子邮件地址]:** 指定签名者的电子邮件地址。签名者将收到指定电子邮件地址上的待签名文档/表单。 您可以选择使用在表单字段中提供的电子邮件地址、登录用户的AEM用户配置文件中，或手动输入电子邮件地址。 这是强制性步骤。 确保第一个签名者或唯一签名者（如果是单个签名者）的电子邮件地址与用于配置AEM云服务的[!DNL Adobe Sign]帐户不相同。

   * **[!UICONTROL 签名者身份验证方法]:** 指定在打开表单进行签名之前对用户进行身份验证的方法。您可以在电话、知识库和基于社交身份的身份验证之间进行选择。
   >[!NOTE]
   >
   >    * 默认情况下，基于社交身份的身份验证提供了使用Facebook、Google和LinkedIn进行身份验证的选项。 您可以联系[!DNL Adobe Sign]支持以启用其他社交身份验证提供程序。


   * **[!DNL Adobe Sign]要填写或签名的字段：** 为签 [!DNL Adobe Sign] 名者选择字段。自适应表单可以有多个[!DNL Adobe Sign]字段。 您可以选择为签名者启用特定字段。 字段显示所有可用的[!DNL Adobe Sign]块。 选择块时，该块的所有字段都将被选中。 您可以使用X图标取消选择字段。

   ![signer-details](assets/signer-details.png)

   上图有两个[!DNL Adobe Sign]块示例：个人信息和办公室详细信息

   点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标。 添加并配置签名者。

### 为自适应表单选择提交操作 {#selectsubmitactionforanadaptiveform}

在将[!DNL Adobe Sign]字段添加到自适应表单后，从表单容器中启用[!DNL Adobe Sign]，选择[!DNL Adobe Sign]Cloud Service，然后添加[!DNL Adobe Sign]签名者，为自适应表单选择适当的提交操作。 有关自适应表单提交操作的详细信息，请参阅[配置提交操作](../../forms/using/configuring-submit-actions.md)。

此外，只有在所有签名者签署表单后，才会提交启用[!DNL Adobe Sign]的自适应表单。 您可以在表单门户的“待签名”部分找到部分签名的表单。 [!DNL Adobe Sign] 配置服务会在常规 [!DNL Adobe Sign] 间隔处 [保持轮](../../forms/using/adobe-sign-integration-adaptive-forms.md) 询服务器，以验证签名的状态。如果所有签名者都完成了对表单的签名，则会启动提交操作服务并提交表单。 如果您使用自定义提交操作，并且表单使用[!DNL Adobe Sign]，请更新您的自定义提交操作以使用提交操作服务。

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

您的表单签名体验已准备就绪。 您可以预览表单以验证签名体验。 在已发布的表单上，当签名者收到通过电子邮件进行签名的表单时，将显示[!DNL Adobe Sign]块字段。 此体验也称为表单外签名体验。 您还可以为第一个签名者配置表单内签名体验，有关详细步骤，请参阅[创建表单内签名体验](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)。

## 为自适应表单{#configure-cloud-signatures-for-an-adaptive-form}配置云签名

基于云的数字签名或远程签名是新一代的数字签名，可跨桌面、移动设备和Web使用，并满足签名者身份验证的最高级别合规性和保证。 您可以使用基于云的数字签名对自适应表单进行签名。

在[编辑Adobe符](../../forms/using/working-with-adobe-sign.md#enableadobesign)的自适应表单属性后，执行以下步骤以将云签名字段添加到自适应表单：

1. 将&#x200B;**[!UICONTROL Adobe Sign块]**&#x200B;组件从组件浏览器拖放到自适应表单。 [!UICONTROL Adobe Sign块]组件具有所有受支持的[!DNL Adobe Sign]字段。 默认情况下，它会向自适应表单中添加&#x200B;**[!UICONTROL 签名]**&#x200B;字段。

   ![符号块](assets/sign-block-new.png)

1. 选择&#x200B;**[!UICONTROL Adobe Sign块]**&#x200B;组件，然后点按&#x200B;**编辑** ![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 它显示用于添加字段和设置字段外观格式的选项。

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.选** 择和添加 [!DNL Adobe Sign] 字段。**B.将** 块展 [!DNL Adobe Sign] 开为全屏视图

1. 点按&#x200B;**[!UICONTROL Adobe Sign字段]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png)图标。 它显示用于选择和添加[!DNL Adobe Sign]字段的选项。

   展开&#x200B;**[!UICONTROL 类型]**&#x200B;下拉字段以选择&#x200B;**[!UICONTROL 数字签名]**，然后点按&#x200B;**完成**&#x200B;图标以将选定字段添加到[!DNL Adobe Sign]块。

   ![数字签名](assets/digital_signatures_new.png)

   必须为字段提供唯一的名称。

   使用以下方法将数字签名应用于自适应表单：

   * 云签名：使用由信任服务提供商托管的[数字ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)进行签名。
   * Adobe Acrobat或Reader:使用Adobe Acrobat或Reader下载并打开文档，以使用智能卡、USB令牌或基于文件的数字ID进行签名。

   将云签名字段添加到自适应表单后，请执行以下步骤以完成配置过程：

   * [为自适应表单启用Adobe Sign](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [为自适应表单选择Adobe SignCloud Service](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [将Adobe Sign签名者添加到自适应表单](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [为自适应表单选择提交操作](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 创建表单内签名体验{#create-in-form-signing-experience}

用户在填写表单时，还可以对自适应表单进行签名。 此体验也称为表单内签名体验。 表单内签名体验仅适用于多个签名者环境中的第一个歌手。 执行以下步骤为自适应表单创建表单内签名体验：

1. [添加并配置签名步骤组件](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. [添加摘要步骤组件](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)。

![表单内签名体验](assets/in_form_signing_experience_new.png)

### 添加并配置签名步骤组件{#add-and-configure-the-signature-step-component}

使用“签名步骤”组件提供一个用于以电子方式对填写的表单进行签名的区域。 呈现包含签名步骤组件的部分时，会显示填写表单的可签名PDF版本。 签名步骤组件占用表单的全宽。 建议在包含签名步骤组件的部分上不要包含任何其他组件。

执行以下步骤以配置签名步骤组件：

1. 将&#x200B;**[!UICONTROL 签名步骤]**&#x200B;组件从组件浏览器拖放到表单中。
1. 选择新添加的签名步骤组件，然后点按配置&#x200B;**![配置](assets/configure.png)图标。**&#x200B;它会打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **[!UICONTROL 名称]**:指定组件的名称。

   * **[!UICONTROL 标题]:** 指定组件的唯一标题。
   * **[!UICONTROL 模板消息]:** 指定加载签名PDF时要显示的消息。[!DNL Adobe Sign] 服务需要一些时间来准备和加载签名PDF。
   * **[!UICONTROL 签名服务]:** 选择 **[!DNL Adobe Sign]** 选项。

   * **[!UICONTROL 使用旧版电子签名组件]**:如果您在 [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md)、AEM应用程序中使用相 [!DNL Forms] 应的自适应表单，或者底层自适应表单具有旧版电子签名组件，请选择 **使用旧版电子签名** 组件。

   * **[!UICONTROL 配置]**:选择配置([!DNL Adobe Sign] Cloud Service)。只有启用了&#x200B;**使用旧版E-sign组件**&#x200B;选项时，下拉框才可用。

   * **[!UICONTROL CSS类]**:为组件指定CSS类。

   点按完成![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)图标以保存更改。

   ![签名步骤](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * 将&#x200B;**[!UICONTROL 签名步骤]**&#x200B;组件拖放到表单时，**[!UICONTROL 签名者和填写表单的人是否相同？]** 选项自动设置为 **是**。需要保持表单正常工作。
      >
      > 
   * 使用“签名步骤”组件后的“摘要步骤”组件可获得最佳体验。 在签名步骤组件中完成表单签名后，摘要步骤会自动并立即提交表单。 如果不使用摘要步骤，则只有在使用[Adobe Sign配置服务](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)设置的间隔后，才会触发自动提交。
      > 以下是一些最佳实践：
   > * 包含签名步骤的自适应表单面板始终位于自适应表单的最后一个或第二个最后一个面板中。 仅当最后一个面板包含摘要步骤时，它才能是最后一个面板。
   > * 包含“签名”或“摘要”步骤组件的面板不能包含任何其他组件。
   > * 包含签名步骤的自适应表单不能具有提交按钮。
   > * 包含签名步骤的自适应表单的提交通过后台服务或摘要步骤进行处理。 如果有一个已配置的签名者也在填写表单，则使用“摘要”步骤处理自适应表单提交的好处是它会立即评估签名者是否已签署表单并调用提交操作。 后台服务需要更长时间来评估所有已配置的签名者是否已签署表单，并延迟提交自适应表单。
   > * 设计表单，以禁止用户从包含“签名”或“摘要”步骤的面板导航回来。



### 配置感谢页面或摘要步骤组件{#configure-the-thank-you-page-or-summary-step-component}

**摘要步骤**&#x200B;组件自动提交表单，在自定义的“摘要”页面中填充信息，并显示已提交表单的摘要。 它还会获取返回图中的所需信息。 摘要步骤组件具有可用于表单的全宽。 建议在包含摘要步骤组件的部分上不要包含任何其他组件。

现在，表单中的签名体验已准备就绪。 您可以预览表单以验证签名体验。

## 常见问题 {#frequently-asked-questions}

**问：** 您可以在另一个自适应表单中嵌入一个自适应表单。嵌入式自适应表单是否启用[!DNL Adobe Sign]?
**答案：** 否，AEM不 [!DNL Forms] 支持使用嵌入已启用自适应表单以 [!DNL Adobe Sign] 进行签名的自适应表单

**问：** 当我使用高级模板创建自适应表单并将其打开进行编辑时，会出现一则错误消息“电子签名或签名者配置不正确”。中。 如何解决错误消息？
**答案：** 使用高级模板创建的自适应表单配置为使用 [!DNL Adobe Sign]。要解决该错误，请创建并选择[!DNL Adobe Sign]云配置，并为自适应表单配置[!DNL Adobe Sign]签名者。

**问：** 能否在自 [!DNL Adobe Sign] 适应表单的静态文本组件中使用文本标记？**答案：** 是的，您可以在文本组件中使用文本标记，以向 [!DNL Adobe Sign] 记录文 [档](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) （仅限自动生成的记录文档选项）启用的自适应表单添加字段。要了解创建文本标记的过程和规则，请参阅[Adobe Sign文档](https://helpx.adobe.com/sign/using/text-tag.html)。 另请注意，自适应表单对文本标记的支持有限。 您可以使用文本标记仅创建那些[Adobe Sign块](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)支持的字段。

**问：** AEM提 [!DNL Forms] 供了 [!UICONTROL Adobe Sign] 块和签名步骤组件。能否在自适应表单中同时使用这些功能？
**答案：** 您可以在表单中同时使用这两个组件。以下是使用这些组件的一些建议：

**Adobe Sign块：** 您可以使用Adobe Sign [!UICONTROL 块] 在自适应表 [!UICONTROL 单的任] 意位置添加Adobe签名字段。它还有助于为签名者分配特定字段。 默认情况下，预览或发布自适应表单时[!UICONTROL Adobe Sign]块不可见。 这些块仅在签名文档中启用。 在签名文档中，只启用分配给签名者的字段。 [!UICONTROL Adobe] 签名块可用于第一个和后续签名者。

**签名步骤组件：** 您可以使用签名步骤组件创建表单内签名体验。它仅允许第一个签名者在填写表单时进行签名。 呈现包含签名步骤组件的部分时，会显示表单的可签名PDF版本。 它通常是表单的最后一个或倒数第二个部分，后跟摘要组件。

## 故障诊断 {#troubleshoot}

### [!DNL Adobe Sign] 协议失败  {#adobe-sign-agreement-failures}

****
问题：在 [!DNL Adobe Sign] 为自适应表单配置服务时，服务无法为基础 [!DNL Adobe Sign] 自适应表单创建协议。

**分辨率**

* 检查自适应表单中使用的Adobe Sign云服务[配置。](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* 确保用于配置[!DNL Adobe Sign]云服务的[!DNL Adobe Sign]服务器上的API应用程序具有所需的权限。
* 如果您使用多个[!DNL Adobe Sign]云服务，请将所有服务的&#x200B;**[!UICONTROL oAuth URL]**&#x200B;指向同一个&#x200B;**[!UICONTROL Adobe Sign Shard]**。

* 使用单独的电子邮件地址来配置[!DNL Adobe Sign]帐户，并为第一个签名者和单个签名者配置。 第一个签名者或唯一签名者（如果是单个签名者）的电子邮件地址不能与用于配置AEM云服务的[!DNL Adobe Sign]帐户相同。

### 为启用[!DNL Adobe Sign]的自适应表单配置的AEM [!DNL Forms]工作流不启动{#adobe-sign-aem-form-workflow-failures}

****
问题：为自 [!DNL Adobe Sign] 适应表单配置后，使用“调用工作流”选项配 [!DNL Forms] 置的工作流不会启动。

**分辨率**

* 当您使用[!DNL Adobe Sign]而不执行“签名”步骤或表单需要多个人的签名时，AEM [!DNL Forms]服务器会等待调度程序确认所有人都已签名表单。 只有在所有人员完成签名后，计划程序才会提交自适应表单，并且只有在成功提交自适应表单后，工作流才会启动。 您可以缩短[调度程序](adobe-sign-integration-adaptive-forms.md)的时间间隔，以快速检查表单签名的状态并加快表单提交。


## 相关文章{#related-articles}

* [将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [将Adobe Sign与自适应表单结合使用的最佳实践](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
