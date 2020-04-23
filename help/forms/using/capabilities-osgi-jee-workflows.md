---
title: 以表单为中心的AEM工作流在OSGi和AEM Forms JEE工作流中的操作和功能
seo-title: 以表单为中心的AEM工作流在OSGi和AEM Forms JEE工作流中的操作和功能
description: 'null'
seo-description: 'null'
uuid: 8af9527d-fa5e-4fcb-88e1-49571528fca6
contentOwner: khsingh
topic-tags: publish
discoiquuid: 89bcc76d-122f-4a3f-b857-16e5376e1624
docset: aem65
translation-type: tm+mt
source-git-commit: 182043b43e9fdb2e7e6de982bceb87b43f36a3ba

---


# 以表单为中心的AEM工作流在OSGi和AEM Forms JEE工作流中的操作和功能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM收件箱和HTML Workspace {#aem-inbox-and-html-workspace}

您可以使用AEM收件箱在OSGi上运行和监视以表单为中心的AEM工作流。 而HTML Workspace允许您运行和监视AEM Forms JEE工作流。 下表可帮助您了解OSGi上以表单为中心的AEM工作流的AEM收件箱中以及AEM Forms JEE工作流的HTML Workspace中的各种重要操作。

<table>
 <tbody>
  <tr>
   <td>操作</td>
   <td>AEM 收件箱</td>
   <td>HTML工作区</td>
  </tr>
  <tr>
   <td>启动进程、任务或表单应用程序<br /> </td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交任务</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>将任务分配给组</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>提交到多条路由</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>跟踪任务历史记录和任务摘要</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>电子邮件通知</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>重新分配任务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>自适应表单的字段级附件</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>日历视图</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>任务级别注释</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>队列(共享的个人队列，来自队列的声明任务)</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>离职通知</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
    <tr>
   <td>自定义UI元素</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>将任务分配给多个用户</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>

## OSGi和AEM Forms JEE工作流上以表单为中心的AEM工作流 {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi和AEM Forms JEE工作流（JEE流程管理上的AEM Forms）上以表单为中心的AEM工作流具有不同的功能集。 下表可帮助您了解以表单为中心的AEM工作流中有关OSGi的重要功能，以及JEE工作流中的AEM Forms的重要功能：

<table>
 <tbody>
  <tr>
   <td>功能</td>
   <td>OSGi上以表单为中心的AEM工作流<br /> </td>
   <td>AEM Forms JEE工作流</td>
  </tr>
  <tr>
   <td>自适应表单</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与其他AEM解决方案集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>（已弃用）涂抹签名</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>自定义电子邮件模板</td>
   <td>支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>定义任务优先级</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>到期日后超时任务</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流内的循环</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态选择被分派人 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>使用自定义元数据</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>电子签名(Adobe Sign)</td>
   <td>Supported <sup>[1]</sup></td>
   <td>Supported <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>管理任务和表单应用程序</td>
   <td>Supported <sup>[2]</sup><br /> </td>
   <td>Supported <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>文档服务</td>
   <td>Supported <sup>[3]</sup></td>
   <td>Supported <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>将已完成的任务渲染为自适应表单或PDF文档</td>
   <td>支持</td>
   <td>支持 [4]</td>
  </tr>
  <tr>
   <td>与通信管理集成</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>重置按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>工作流阶段</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>只读自适应表单</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>隐藏默认保存按钮</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>对工作流详细信息部分的精细控制</td>
   <td>支持</td>
   <td>不支持</td>
  </tr>
  <tr>
   <td>HTML5表单，交互式PDF表单，表单集<br /> </td>
   <td>不支持<br /> </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>进程报告</td>
   <td>不支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>数字签名</td>
   <td>支持<br /> </td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>起点类别</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>批量任务批准 </td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>用自定义名称保存草稿</td>
   <td>不支持 </td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>使用现有流程数据启动流程<br /> </td>
   <td>不支持</td>
   <td>支持 </td>
  </tr>
  <tr>
   <td>将起点另存为草稿</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>用户头像</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>经理视图</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>搜索模板</td>
   <td>不支持</td>
   <td>支持<br /> </td>
  </tr>
  <tr>
   <td>与第三方应用程序集成</td>
   <td>Not Supported <sup>[6]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>工作流应用程序或起点的任务级附件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>提醒电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>更改任务超时时的标题</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>关于任务委托和任务索赔的电子邮件</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在工作流结束时发送电子邮件</td>
   <td>Supported <sup>[7]</sup></td>
   <td>支持</td>
  </tr>
  <tr>
   <td>在不相交的组之间委派</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>从工作流调用Web服务</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>XSLT变换</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>网关，无等待 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>用于存储数据的变量 </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>或，并拆分</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>动态任务优先级</td>
   <td>不支持</td>
   <td>不支持</td>
  </tr>
 </tbody>
</table>

1. 您可以在OSGi上使用以表单为中心的AEM工作流来签署已填写的自适应表单。 OSGi上以表单为中心的AEM工作流支持表单签名。 不 [支持表单签名](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) 。

1. 您需要访问AEM收件箱才能运行和监视AEM Forms OSGi上以表单为中心的工作流，以及运行和监视AEM Forms JEE工作流的HTML Workspace。
1. 本机AEM Forms文档服务适用于OSGi上的以表单为中心的AEM工作流和JEE工作流上的AEM Forms。 AEM Workflow使用本机文档服务在OSGi和AEM Forms JEE（流程管理）工作流上以表单为中心的AEM工作流。
1. AEM Forms JEE工作流只能渲染自适应表单。 它不支持将自适应表单渲染为PDF文档。
1. AEM表单JEE工作流没有Adobe Sign的单独步骤。 您需要为AEM表单JEE工作流启用Adobe Sign的自适应表单。 有关详细信息，请参 [阅Adobe Sign文档](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)。
1. 您可以使用“调 [用表单数据模型服务](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) ”步骤调用Web服务服务并从第三方应用程序发布或检索数据。
1. 您可以使用“发送电 [子邮件](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) ”步骤发送电子邮件。

## AEM收件箱与AEM Forms应用程序功能之间的区别 {#differences-between-aem-inbox-and-aem-forms-app-features}

启动以表单为中心的工作流程的两种主要方法是使用 [AEM收件箱](../../forms/using/manage-applications-inbox.md) 和AEM Forms应用程序。 但是，AEM收件箱和AEM Forms应用程序的功能不同。 AEM收件箱仅适用于以 [表单为中心的工作流](../../forms/using/aem-forms-workflow.md) ，而AEM Forms应用程序适用于以表单为中心的工作流以及流程管理。

下表列表了AEM收件箱和AEM Forms应用程序的功能：

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>AEM 收件箱</strong></p> </td>
   <td><p><strong>AEM Forms 应用程序</strong></p> </td>
  </tr>
  <tr>
   <td><p>启动表单应用程序</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>提交任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>委派任务</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>跟踪任务历史记录和任务摘要</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加任务级附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>查看任务级别附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>添加字段级附件</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
  <tr>
   <td><p>显示日历视图</p> </td>
   <td><p>支持</p> </td>
   <td><p>不支持</p> </td>
  </tr>
  <tr>
   <td><p>添加注释</p> </td>
   <td><p>支持</p> </td>
   <td><p>支持</p> </td>
  </tr>
 </tbody>
</table>

