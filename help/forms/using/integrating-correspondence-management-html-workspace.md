---
title: 在AEM Forms工作区中集成第三方应用程序
seo-title: 在AEM Forms工作区中集成第三方应用程序
description: 在AEM Forms工作区中集成第三方应用程序，如通信管理。
seo-description: 如何在AEM Forms工作区中集成第三方应用程序（如通信管理）。
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 在AEM Forms工作区中集成第三方应用程序{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作区支持管理表单和文档的任务分配和完成活动。 这些表单和文档可以是XDP、PDF、HTML或Flex格式呈现的XDP表单、Flex®表单或参考线（已弃用）。

这些功能得到进一步增强。 AEM Forms现在支持与支持类似于AEM Forms工作区的功能的第三方应用程序的协作。 此功能的一个常见部分是分配工作流和任务的后续批准。 AEM Forms为AEM Forms企业用户提供单一的统一体验，以便通过AEM Forms工作区处理受支持应用程序的所有此类任务分配或批准。

例如，让我们将Correponsement Management视为与AEM Forms工作区集成的示例候选。 通信管理有“信函”的概念，可以呈现并允许操作。

## 创建对应管理资产 {#create-correspondence-management-assets}

开始，方法是创建在AEM Forms工作区中呈现的示例对应管理模板。 有关详细信息，请参 [阅创建字母模板](../../forms/using/create-letter.md)。

访问位于其URL的“对应管理”模板，验证“对应管理”模板是否可以成功呈现。 URL的模式与 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

其中 `encodedLetterId` 是URL编码的字母Id。 在Workbench中为工作区任务定义渲染进程时，指定相同的字母Id。

## 创建任务以在AEM Workspace中渲染和提交字母 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

在执行这些步骤之前，请确保您是以下用户组的成员：

* cm-agent-users
* 工作区用户

有关详细信息，请参 [阅添加和配置用户](/help/forms/using/admin-help/adding-configuring-users.md)。

使用以下步骤创建任务以在AEM Workspace中渲染和提交字母：

1. 启动工作台。 以管理员身份登录到localhost。
1. 单击“文件”>“新建”>“应用程序”。 在“应用程序名称”字段中，输入， `CMDemoSample` 然后单击“完成”。
1. 选择 `CMDemoSample/1.0` 并右键单击 `NewProcess`。 在名称字段中，输入，然 `CMRenderer` 后单击完成。
1. 拖动开始点活动选取器并对其进行配置：

   1. 在演示文稿数据中，选择“使用CRX资产”。

      ![useacrxasset](assets/useacrxasset.png)

   1. 浏览资产。 在“选择表单资产”对话框中，“字母”选项卡列表服务器上的所有字母。

      ![字母选项卡](assets/letter_tab_new.png)

   1. 选择相应的字母，然后单击“ **确定”**。

1. 单击“管理操作用户档案”。 此时将显示“管理操作用户档案”对话框。 确保正确选择了渲染进程和提交进程。
1. 要使用数据XML文件打开该字母，请在“准备数据进程”中浏览并选择相应的数据文件。
1. 单击“确定”。
1. 为“开始点输出”和“任务附件”定义变量。 定义的变量将包含开始点输出和任务附件数据。
1. （可选）要在工作流中添加其他用户，请拖动活动选取器，对其进行配置，然后将其分配给用户。 编写自定义包装器（示例如下）或下载并安装DSC（示例如下）以扩展“Letter”模板、“开始点输出”和“任务附件”。

   示例自定义包装器如下：

   ```java
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

   [获取文件](assets/dscsample.zip)下载DSC:上面附加的DSCSample.zip文件中提供示例DSC。 下载并解压缩DSCSample.zip文件。 在使用DSC服务之前，您需要配置它。 有关信息，请参 [阅配置DSC服务](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)。

   在“定义活动”对话框中，选择相应的活动，如getLetterInstanceInfo，然后单击“确 **定”**。

1. 部署应用程序。 如果出现提示登记并保存资产。
1. 登录到位于https://&#39;[server]:[port]&#39;/lc/content/ws的AEM Forms工作区。
1. 打开您添加的任务,CMRender。 出现“Correponsement Management（通信管理）”信函。

   ![cminworkspace](assets/cminworkspace.png)

1. 填写所需数据并提交信件。 窗口将关闭。 在此过程中，任务将分配给在步骤9中的工作流中指定的用户。

   >[!NOTE]
   >
   >在填写字母中的所有必需变量之前，“提交”按钮不会启用。
