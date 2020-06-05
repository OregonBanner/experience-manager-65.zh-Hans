---
title: OSGi组和权限上的AEM Forms
seo-title: OSGi组和权限上的AEM Forms
description: 将用户分配到组以在OSGi上管理AEM Forms
seo-description: 将用户分配到组以在OSGi上管理AEM Forms
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: dbb99875cc6f3c8810670ffe923756f7c13d4ace
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# OSGi组和权限上的AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

您可以 [在AEM中](/help/sites-administering/user-group-ac-admin.md#group-administration) 创建组 [，并将策](/help/sites-administering/user-group-ac-admin.md#user-administration) 略和用户分配到这些组。 这些策略控制属于组的用户的权限。

安装AEM [Forms Add-on包后](../../forms/using/installing-configuring-aem-forms-osgi.md)，本文中提到的组（如forms-user和forms-power-user）将自动可用于分配。 下表列表了用户根据组分配可对OSGi上的AEM Forms执行的任务:

<table>
 <tbody>
  <tr>
   <td>组</td> 
   <td>任务</td> 
  </tr>
  <tr>
   <td>表单用户 <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应表单</li> 
     <li>创建、预览和发布交互式通信和文档片段</li> 
     <li>将资产上传到AEM实例</li> 
     <li>创建主题</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>表单——用户</td> 
   <td>
    <ul> 
     <li>创建、预览、发布和提交自适应表单</li> 
     <li>创建、预览和发布交互式通信和文档片段</li> 
     <li>使用代码编辑器为自适应表单创建脚本</li> 
     <li>上传包括脚本在内的资源</li> 
     <li>创建主题</li> 
     <li>导入包含XDP的包</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>审查提交</li> 
     <li>批准或拒绝提交</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>创建和预览自适应表单或交互式通信模板</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>创建和修改表单数据模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>使用代理UI访问通信管理信函或交互通信</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>工作流编辑器</p> </td> 
   <td>
    <ul> 
     <li>创建收件箱应用程序</li> 
     <li>创建工作流模型</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>工作流用户</td> 
   <td>
    <ul> 
     <li>使用AEM收件箱应用程序<br /><strong>注意： </strong>您必须具有cm-agent-users和workflow-users组分配，才能在AEM收件箱中访问Interactive Communications Agent UI。</li> 
     <li>管理工作流实例</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>配置 PDF 生成器</li> 
     <li>配置监视文件夹</li> 
     <li>管理工作流程应用程序</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. 具有表单用户组权限的用户无法为自适应表单编写脚本。
1. 具有模板作者组权限的用户无法为模板编写脚本。

