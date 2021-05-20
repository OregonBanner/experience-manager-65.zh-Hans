---
title: 在AEM Forms工作区中集成第三方应用程序
seo-title: 在AEM Forms工作区中集成第三方应用程序
description: 在AEM Forms工作区中集成第三方应用程序，如通信管理。
seo-description: 如何在AEM Forms工作区中集成诸如通信管理之类的第三方应用程序。
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# 在AEM Forms工作区中集成第三方应用程序{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作区支持对表单和文档的任务分配和完成活动进行管理。 这些表单和文档可以是XDP Forms、Flex®表单或已以XDP、PDF、HTML或Flex格式呈现的指南（已弃用）。

这些功能得到进一步增强。 AEM Forms现在支持与第三方应用程序协作，这些应用程序支持类似于AEM Forms工作区的功能。 此功能的常见部分是任务分配和后续批准工作流。 AEM Forms为AEM Forms企业用户提供了单一的统一体验，以便通过AEM Forms工作区可以处理受支持应用程序的所有此类任务分配或批准。

例如，让我们将通信管理视为与AEM Forms工作区集成的示例候选项。 通信管理具有“信件”的概念，可以呈现并允许执行操作。

## 创建通信管理资产{#create-correspondence-management-assets}

首先，创建在AEM Forms工作区中呈现的示例通信管理模板。 有关更多详细信息，请参阅[创建信件模板](../../forms/using/create-letter.md)。

在通信管理模板的URL中访问该模板，以验证通信管理模板是否可以成功呈现。 URL的模式与`https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`类似

其中，`encodedLetterId`是URL编码的字母Id。 在Workbench中为工作区任务定义渲染进程时，指定相同的字母ID。

## 创建任务以在AEM Workspace {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}中呈现和提交信件

在执行这些步骤之前，请确保您是以下组的成员：

* cm-agent-users
* 工作区用户

有关更多信息，请参阅[添加和配置用户](/help/forms/using/admin-help/adding-configuring-users.md)。

请按照以下步骤创建任务，以在AEM Workspace中渲染和提交信件：

1. 启动Workbench。 以管理员身份登录到localhost。
1. 单击“文件”>“新建”>“应用程序”。 在“应用程序名称”字段中，输入`CMDemoSample`，然后单击“完成”。
1. 选择`CMDemoSample/1.0`并右键单击`NewProcess`。 在名称字段中，输入`CMRenderer`，然后单击“完成”。
1. 拖动“起始点”活动选取器并对其进行配置：

   1. 在演示数据中，选择使用CRX资产。

      ![useacrxasset](assets/useacrxasset.png)

   1. 浏览资产。 在“选择表单资产”对话框中，“信件”选项卡列出了服务器上的所有信件。

      ![信件选项卡](assets/letter_tab_new.png)

   1. 选择相应的信件并单击&#x200B;**确定**。

1. 单击管理操作配置文件。 此时将显示“管理操作配置文件”对话框。 确保已正确选择渲染进程和提交进程。
1. 要使用数据XML文件打开信件，请浏览并选择准备数据进程中的相应数据文件。
1. 单击确定。
1. 为起始点输出和任务附件定义变量。 定义的变量将包含起始点输出和任务附件数据。
1. （可选）要在工作流中添加其他用户，请拖动活动选取器，对其进行配置，然后将其分配给用户。 编写自定义包装器（下面给出示例）或下载并安装DSC（下面给出）以扩展信件模板、起始点输出和任务附件。

   下面列出了自定义包装器示例：

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [获取](assets/dscsample.zip)
文件下载DSC:上面附加的DSCSample.zip文件中提供了示例DSC。下载并解压缩DSCSample.zip文件。 在使用DSC服务之前，您需要对其进行配置。 有关信息，请参阅[配置DSC服务](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)。

   在“定义活动”对话框中，选择相应的活动，如getLetterInstanceInfo ，然后单击&#x200B;**确定**。

1. 部署应用程序。 如果系统提示签入并保存资产。
1. 登录到位于https://&#39;[server]的AEM Forms工作区：[port]&#39;/lc/content/ws。
1. 打开您添加的任务，CMRenderer。 出现“Correspondence Management（通信管理）”信件。

   ![cminworkspace](assets/cminworkspace.png)

1. 填写所需数据并提交信件。 窗口关闭。 在此过程中，任务会被分配给步骤9中工作流中指定的用户。

   >[!NOTE]
   >
   >填写信件中的所有必需变量后，才会启用“提交”按钮。
