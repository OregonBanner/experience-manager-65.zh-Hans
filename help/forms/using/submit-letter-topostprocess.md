---
title: 信件和交互通信的后期处理
seo-title: 信函的后处理
description: 通过“信函后期处理”功能，您可以创建AEM和表单后期流程（如打印和电子邮件），并将它们与您的信件集成。
seo-description: 通过“信函后期处理”功能，您可以创建AEM和表单后期流程（如打印和电子邮件），并将它们与您的信件集成。
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# 信件和交互通信的后期处理{#post-processing-of-letters-and-interactive-communications}

## 后处理 {#post-processing}

代理可以关联和执行信件和交互式通信的后处理工作流。 可以在“信函”模板的“属性”视图中选择要执行的后期进程。 您可以设置发布流程，以通过电子邮件、打印、传真或存档您的最终信件。

![后处理](assets/ppoverview.png)

要将帖子流程与信件或交互式通信相关联，您首先需要设置帖子流程。 可以对提交的信函执行两种类型的工作流：

1. **** 表单工作流：这些是JEE流程管理工作流中的AEM Forms。 有关设置表单工作 [流的说明](../../forms/using/submit-letter-topostprocess.md#main-pars-header-3)。

1. **** AEM Workflow:AEM工作流还可用作已提交信函的发布流程。 有关设置 [AEM Workflow的说明](../../forms/using/aem-forms-workflow.md)。

## 表单工作流 {#formsworkflow}

1. 在AEM中，使用以下URL打开服务器的Adobe Experience Manager Web Console配置： `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![配置管理器](assets/2configmanager-1.png)

1. 在此页上，找到AEM Forms客户端SDK配置，然后单击以展开它。
1. 在服务器URL中，输入JEE服务器上AEM Forms的名称、登录详细信息，然后单击“保 **存”**。

   ![输入LiveCycle服务器的名称](assets/1cofigmanager.png)

1. 指定用户名和密码。
1. 确保将sun.util.calendar添加到反序列化防火墙配置。

   转到反序列化防火墙配置，并在包前缀的白名单类下添加sun.util.calendar。

1. 现在，您的服务器已映射，并且JEE上的AEM Forms中的发布进程在创建字母时可在AEM用户界面中使用。

   ![创建包含列出的帖子进程的信件屏幕](assets/0configmanager.png)

1. 要验证进程／服务的身份，请复制进程的名称，然后返回Adobe Experience Manager Web Console“配置”页面> AEM Forms客户端SDK配置，并将该进程添加为新服务。

   例如，如果字母的“属性”页面的下拉框将进程名称显示为Forms Workflow -> ValidCCPostProcess/SaveXML，则添加服务名称为 `ValidCCPostProcess/SaveXML`。

1. 要在JEE工作流中使用AEM Forms进行后期处理，请设置必要的参数和输出。 参数的默认值如下所示。

   转到Adobe Experience Manager Web Console的“配置”页>“ **[!UICONTROL 对应管理配置]** ”，并设置以下参数：

   1. **** inPDFoc（PDF文档参数）:作为输入的PDF文档。 此输入包含已渲染的字母作为输入。 所指示的参数名称是可配置的。 可以从配置中的“对应管理”配置配置这些组件。
   1. **** inXMLDoc（XML数据参数）:作为输入的XML文档。 此输入包含用户以XML形式输入的数据。
   1. **** inXDPDoc（XDP文档参数）:作为输入的XML文档。 此输入包含基础布局(XDP)。
   1. **** inAttachmentDocs（Attachment Documents参数）:列表输入参数。 此输入包含作为输入的所有附件。
   1. **** redirectURL（重定向URL输出）:指示要重定向到的URL的输出类型。
   您的表单工作流必须具有PDF文档参数或XML数据参数作为输入，并且输入的名称与“对应管理配置”中 **[!UICONTROL 指定的名称相同]**。 这是进程在“后期进程”下拉列表中列出的必需条件。

## 发布实例的设置 {#settings-on-the-publish-instance}

1. 登录 `https://localhost:publishport/aem/forms`到
1. 导航到 **[!UICONTROL 字母]** ，以查看发布实例上可用的已发布字母。
1. 配置AEM DS设置。 请参 [阅配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。

>[!NOTE]
>
>在使用表单或AEM工作流时，在从发布服务器提交任何内容之前，必须配置DS设置服务。 否则，提交表单将失败。

## Letter实例检索 {#letter-instances-retrieval}

通过使用LetterInstanceService中定义的以下API，可以进一步处理保存的字母实例，如检索字母实例和删除字母实例。

<table>
 <tbody>
  <tr>
   <td><strong>服务器端API</strong></td>
   <td><strong>操作名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><p>Public LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>引发ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>提取指定的字母实例 </td>
  </tr>
  <tr>
   <td>公共void deleteLetterInstance(String letterInstanceId)引发ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>删除了指定的字母实例 </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)throws ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>此API根据输入查询参数获取字母实例。 要获取所有字母实例，查询参数可以作为null传递。<br /> </td>
  </tr>
  <tr>
   <td>公共Boolean letterInstanceExists(String letterInstanceName)引发ICCException; </td>
   <td>letterInstanceExists </td>
   <td>检查给定名称是否存在LetterInstance </td>
  </tr>
 </tbody>
</table>

## 将帖子流程与信函关联 {#associating-a-post-process-with-a-letter}

在CCR用户界面中，完成以下步骤以将后处理与字母关联：

1. 将鼠标悬停在字母上，然后点按 **查看属性**。
1. 选择&#x200B;**编辑**。
1. 在“基本属性”中，使用“后处理”下拉框，选择要与信函关联的后处理。 下拉列表中列出了AEM和与表单相关的帖子进程。
1. 点按&#x200B;**保存**。
1. 在使用“发布流程”配置信函后，发布信函，（可选）在发布实例上指定AEM DS设置服务中的处理URL。 这可确保在处理实例上运行后处理。

## 重新加载草稿字母实例 {#reloaddraft}

可以使用以下url在用户界面中重新加载草稿字母实例：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID:已提交字母实例的唯一ID。

有关保存草稿字母的详细信息，请参 [阅保存草稿和提交字母实例](../../forms/using/create-correspondence.md#savingdrafts)。
