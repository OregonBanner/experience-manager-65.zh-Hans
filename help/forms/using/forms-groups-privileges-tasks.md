---
title: OSGi组和权限上的AEM Forms
seo-title: OSGi组和权限上的AEM Forms
description: 将用户分配到组以管理OSGi上的AEM Forms
seo-description: 将用户分配到组以管理OSGi上的AEM Forms
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# OSGi组和权限上的AEM Forms{#aem-forms-on-osgi-groups-and-privileges}

您可以 [在AEM中](/help/sites-administering/user-group-ac-admin.md#group-administration) ，创建用 [户组](/help/sites-administering/user-group-ac-admin.md#user-administration) ，并将策略和用户分配到用户组。 这些策略控制属于组的用户的权限。

安装 [AEM Forms Add-on包后](../../forms/using/installing-configuring-aem-forms-osgi.md)，本文中提及的组（如forms-user和forms-power-user）将自动可用于分配。 下表列表了用户可以根据组分配对OSGi上的AEM Forms执行的任务:

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
   <td>表单提交审阅者</td> 
   <td>
    <ul> 
     <li>审查提交内容</li> 
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
   <td>模板——用户</td> 
   <td>
    <ul> 
     <li>创建和预览自适应表单或交互式通信模板</li> 
     <li>使用代码编辑器为自适应表单或交互式通信模板创建脚本</li> 
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
     <li>使用AEM收件箱应用程序<br /><strong>注意：要 </strong>访问AEM收件箱中的Interactive Communications Agent UI，您必须具有cm-agent用户和工作流用户组分配。</li> 
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

