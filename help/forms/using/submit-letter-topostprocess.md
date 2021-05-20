---
title: 信件和交互式通信的后处理
seo-title: 信件的后处理
description: 通过通信管理中信件的后处理，您可以创建AEM和Forms帖子流程（如打印和电子邮件），并将它们与您的信件集成。
seo-description: 通过通信管理中信件的后处理，您可以创建AEM和Forms帖子流程（如打印和电子邮件），并将它们与您的信件集成。
uuid: 40cb349d-6ba2-4794-9ec6-dcab15c35b8d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9b06c394-8e26-429c-b78f-22afa271aeb3
docset: aem65
feature: 通信管理
exl-id: 91ee4422-99c1-4907-a507-5968c6984f28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# 信件和交互式通信的后处理{#post-processing-of-letters-and-interactive-communications}

## 后处理{#post-processing}

座席可以关联并执行信件和交互通信的后处理工作流。 可以在信件模板的“属性”视图中选择要执行的后处理。 您可以设置帖子流程，以发送电子邮件、打印、传真或存档您的最终信件。

![后处理](assets/ppoverview.png)

要将帖子流程与信件或交互式通信关联，您首先需要设置帖子流程。 对于提交的信件，可以执行两种类型的工作流：

1. **Forms Workflow:** 这些是JEE上的AEM Forms流程管理工作流。设置[Forms Workflow](#formsworkflow)的说明。

1. **AEM工作流：** AEM工作流也可用作已提交信件的帖子流程。有关设置[AEM Workflow](../../forms/using/aem-forms-workflow.md)的说明。

## 表单工作流 {#formsworkflow}

1. 在AEM中，使用以下URL为您的服务器打开Adobe Experience Manager Web控制台配置：`https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![配置管理器](assets/2configmanager-1.png)

1. 在此页面上，找到AEM Forms客户端SDK配置，并单击以将其展开。
1. 在服务器URL中，输入JEE服务器上AEM Forms的名称和登录详细信息，然后单击&#x200B;**Save**。

   ![输入LiveCycle服务器的名称](assets/1cofigmanager.png)

1. 指定用户名和密码。
1. 确保将sun.util.calendar添加到反序列化防火墙配置中。

   转到“反序列化防火墙配置”，列入允许列表并在包前缀的类下，添加sun.util.calendar。

1. 现在，您的服务器已映射，并且在创建信件时，可在AEM用户界面中使用JEE上的AEM Forms中的后处理。

   ![创建列出帖子进程的信件屏幕](assets/0configmanager.png)

1. 要验证进程/服务，请复制进程的名称，然后返回到Adobe Experience Manager Web控制台配置页面> AEM Forms客户端SDK配置，并将该进程作为新服务添加。

   例如，如果信件的“属性”页中的下拉列表将进程名称显示为Forms Workflow-> ValidCCPostProcess/SaveXML，请将服务名称添加为`ValidCCPostProcess/SaveXML`。

1. 要在JEE上使用AEM Forms工作流进行后处理，请设置必要的参数和输出。 参数的默认值如下所示。

   转到Adobe Experience Manager Web控制台配置页面> **[!UICONTROL 通信管理配置]**&#x200B;并设置以下参数：

   1. **在PDFDoc（PDF文档参数）中：** 作为输入的PDF文档。此输入包含呈现的字母作为输入。 指示的参数名称是可配置的。 它们可以通过配置中的通信管理配置进行配置。
   1. **inXMLDoc（XML数据参数）：** 作为输入的XML文档。此输入包含用户以XML形式输入的数据。
   1. **在XDPDoc（XDP文档参数）中：** 作为输入的XML文档。此输入包含基础布局(XDP)。
   1. **inAttachmentDocs(Attachment Documents（Attachment Documents参数）：** 列表输入参数。此输入包含作为输入的所有附件。
   1. **redirectURL（重定向URL输出）：** 一种输出类型，用于指示要重定向到的URL。

   您的表单工作流必须具有PDF文档参数或XML数据参数作为输入，且其名称与&#x200B;**[!UICONTROL 通信管理配置]**&#x200B;中指定的名称相同。 该流程需要在“后处理”下拉列表中列出。

## 发布实例{#settings-on-the-publish-instance}中的设置

1. 登录到`https://localhost:publishport/aem/forms`。
1. 导航到&#x200B;**[!UICONTROL Letters]**&#x200B;以查看发布实例上可用的已发布信件。
1. 配置AEM DS设置。 请参阅[配置AEM DS设置](../../forms/using/configuring-the-processing-server-url-.md)。

>[!NOTE]
>
>使用Forms或AEM工作流时，在从发布服务器提交任何内容之前，必须配置DS设置服务。 否则，《表》报送失败。

## 信件实例检索{#letter-instances-retrieval}

使用LetterInstanceService中定义的以下API，可以进一步处理保存的信件实例，如检索信件实例和删除信件实例。

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
   <td>获取指定的信件实例 </td>
  </tr>
  <tr>
   <td>公共void deleteLetterInstance(String letterInstanceId)引发ICCException; </td>
   <td>deleteLetterInstance </td>
   <td>已删除指定的信件实例 </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query)引发ICCException; </td>
   <td>getAllLetterInstances </td>
   <td>此API根据输入查询参数获取信件实例。 要获取所有信件实例，查询参数可以传递为null。<br /> </td>
  </tr>
  <tr>
   <td>公共布尔值letterInstanceExists(String letterInstanceName)引发ICCException; </td>
   <td>letterInstanceExists </td>
   <td>检查LetterInstance是否按给定名称存在 </td>
  </tr>
 </tbody>
</table>

## 将后处理与信件{#associating-a-post-process-with-a-letter}关联

在CCR用户界面中，完成以下步骤以将帖子处理与信件关联：

1. 将鼠标悬停在信件上，然后点按&#x200B;**查看属性**。
1. 选择&#x200B;**编辑**。
1. 在“基本属性”中，使用“帖子处理”下拉列表，选择要与信件关联的帖子处理。 与AEM和Forms相关的后处理流程都会列在下拉列表中。
1. 点按&#x200B;**保存**。
1. 使用“后处理”配置信件后，发布信件，并（可选）在发布实例上，在AEM DS设置服务中指定处理URL。 这可确保后处理在处理实例上运行。

## 重新加载草稿信件实例  {#reloaddraft}

可以使用以下url在用户界面中重新加载草稿信件实例：

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID:提交的信件实例的唯一ID。

有关保存草稿信件的更多信息，请参阅[保存草稿并提交信件实例](../../forms/using/create-correspondence.md#savingdrafts)。
