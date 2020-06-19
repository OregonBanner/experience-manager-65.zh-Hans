---
title: 信件和互动通信的后处理
seo-title: 信函的后处理
description: 通过信件管理中的邮件后处理功能，您可以创建AEM和Forms邮件后处理流程，如打印和电子邮件，并将它们与信件集成。
seo-description: 通过信件管理中的邮件后处理功能，您可以创建AEM和Forms邮件后处理流程，如打印和电子邮件，并将它们与信件集成。
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---


# 信件和互动通信的后处理{#post-processing-of-letters-and-interactive-communications}

## 后处理 {#post-processing}

代理可以关联和执行信件和交互通信的后处理工作流。 可以在“信函”模板的“属性”视图中选择要执行的后处理。 您可以设置邮件发送、打印、传真或存档您的最终信件的帖子流程。

![后处理](assets/ppoverview.png)

要将帖子流程与信件或交互式通信关联起来，您首先需要设置帖子流程。 提交的信件可以执行两种工作流:

1. **表单工作流：** 这些是JEE流程管理工作流的AEM Forms。 有关设置表单工 [作流的说明](#formsworkflow)。

1. **AEM Workflow:** AEM工作流还可用作已提交信件的后处理。 有关设置AEM Workflow [的说明](../../forms/using/aem-forms-workflow.md)。

## 表单工作流 {#formsworkflow}

1. 在AEM中，使用以下URL打开服务器的Adobe Experience ManagerWeb控制台配置： `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![配置管理器](assets/2configmanager-1.png)

1. 在此页上，找到AEM Forms客户端SDK配置，然后单击以展开它。
1. 在服务器URL中，输入JEE服务器上AEM Forms的名称、登录详细信息，然后单击“保 **存”**。

   ![输入LiveCycle服务器的名称](assets/1cofigmanager.png)

1. 指定用户名和密码。
1. 确保将sun.util.calendar添加到反序列化防火墙配置。

   转到反序列化防火墙配置，在“允许列出的包前缀类”下添加sun.util.calendar。

1. 现在，您的服务器已映射，并且JEEAEM Forms中的帖子进程在创建字母时可在AEM用户界面中使用。

   ![创建包含列出的帖子流程的信件屏幕](assets/0configmanager.png)

1. 要验证进程／服务，请复制进程的名称，然后返回“Adobe Experience ManagerWeb控制台配置”页>“AEM Forms客户端SDK配置”，并将该进程添加为新服务。

   例如，如果字母的“属性”页中的下拉框将进程的名称显示为Forms Workflow -> ValidCCPostProcess/SaveXML，则添加一个服务名称 `ValidCCPostProcess/SaveXML`。

1. 要使用JEE工作流上的AEM Forms进行后处理，请设置必要的参数和输出。 参数的默认值如下所示。

   转到“Adobe Experience ManagerWeb控制台配置”页>“ **[!UICONTROL 对应管理配置]** ”并设置以下参数：

   1. **inPDFDoc(PDF文档参数):** 作为输入的PDF文档。 此输入包含呈现的字母作为输入。 所指示的参数名称是可配置的。 可以从配置中的“对应管理”配置配置这些配置。
   1. **inXMLDoc（XML数据参数）:** 作为输入的XML文档。 此输入包含用户以XML形式输入的数据。
   1. **inXDPDoc(XDP文档参数):** 作为输入的XML文档。 此输入包含基础布局(XDP)。
   1. **inAttachmentDocs(Attachment文档参数):** 列表输入参数。 此输入包含作为输入的所有附件。
   1. **redirectURL（重定向URL输出）:** 指示要重定向到的url的输出类型。

   您的表单工作流必须具有PDF文档参数或XML数据参数作为输入，其名称与“对应管理配置”中 **[!UICONTROL 指定的名称相同]**。 这是流程在“后期流程”下拉列表中列出的必需条件。

## 发布实例的设置 {#settings-on-the-publish-instance}

1. 登录 `https://localhost:publishport/aem/forms`到
1. 导航到 **[!UICONTROL 字母]** ，以视图发布实例中可用的已发布字母。
1. 配置AEM DS设置。 请参 [阅配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。

>[!NOTE]
>
>在使用表单或AEM工作流时，在从发布服务器提交任何内容之前，必须配置DS设置服务。 否则，表格提交将失败。

## 字母实例检索 {#letter-instances-retrieval}

通过使用LetterInstanceService中定义的以下API，可以进一步处理保存的字母实例，如检索字母实例和删除字母实例。

<table>
 <tbody>
  <tr>
   <td><strong>服务器端API</strong></td>
   <td><strong>操作名称</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><p>公共LetterInstanceVO</p> <p>getLetterInstance(String letterInstanceId)</p> <p>抛出ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>提取指定的字母实例 </td>
  </tr>
  <tr>
   <td>公共void deleteLetterInstance(String letterInstanceId)引发ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>删除了指定的字母实例 </td>
  </tr>
  <tr>
   <td>列表getAllLetterInstances(查询)抛出ICCException; </td>
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

## 将过帐流程与信函关联 {#associating-a-post-process-with-a-letter}

在CCR用户界面中，完成以下步骤以将后处理与字母关联：

1. 将鼠标悬停在字母上并点按 **视图属性**。
1. 选择&#x200B;**编辑**。
1. 在“基本属性”中，使用“后处理”下拉框，选择要与信函关联的后处理。 下拉列表中列出了AEM和与表单相关的后处理。
1. 点按&#x200B;**保存**。
1. 在使用“后期处理”配置信函后，发布信函，（可选）在发布实例上指定AEM DS设置服务中的处理URL。 这可确保在处理实例上运行后处理。

## 重新加载草稿字母实例  {#reloaddraft}

可以使用以下url在用户界面中重新加载草稿字母实例：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID: 已提交信函实例的唯一ID。

有关保存草稿信函的详细信息，请参 [阅保存草稿和提交信函实例](../../forms/using/create-correspondence.md#savingdrafts)。
