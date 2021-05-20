---
title: 在OSGi环境中强化和保护AEM表单
seo-title: 在OSGi环境中强化和保护AEM表单
description: 了解在OSGi服务器上保护AEM Forms的建议和最佳实践。
seo-description: 了解在OSGi服务器上保护AEM Forms的建议和最佳实践。
uuid: abca7e7c-38c3-44f5-8d8a-4615cfce26c6
topic-tags: Security
discoiquuid: b1bd04bf-0d6d-4e6b-8c7c-eafd1a24b5fe
role: Administrator
exl-id: 5da3cc59-4243-4098-b1e0-438304fcd0c5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1463'
ht-degree: 0%

---

# 在OSGi环境{#hardening-and-securing-aem-forms-on-osgi-environment}上强化和保护AEM表单

了解在OSGi服务器上保护AEM Forms的建议和最佳实践。

保护服务器环境对组织至关重要。 本文介绍了有关保护运行AEM Forms的服务器的建议和最佳实践。 这不是适用于您的操作系统的全面的主机强化文档。 相反，本文介绍了为增强已部署应用程序的安全性而应实施的各种安全强化设置。 但是，为了确保应用程序服务器保持安全，除了本文中提供的建议外，您还应实施安全监控、检测和响应过程。 该文档还包含保护PII（个人身份信息）的最佳实践和准则。

本文面向负责规划应用程序或基础架构开发和部署的AEM Forms的顾问、安全专家、系统架构师和IT专业人员。 这些角色包括以下常见角色：

* IT和运营的工程师必须在自己或客户的组织中部署安全的Web应用程序和服务器。
* 负责为组织中的客户规划建筑工作的架构师和规划师。
* IT安全专家，他们专注于在组织内的平台之间提供安全性。
* 需要客户和合作伙伴详细资源的Adobe和合作伙伴的顾问。

下图显示了典型AEM Forms部署中使用的组件和协议，包括相应的防火墙拓扑：

![典型架构](assets/typical-architecture.png)

AEM Forms是高度可自定义的，并且可以在许多不同的环境中工作。 某些建议可能不适用于您的组织。

## 安全传输层{#secure-transport-layer}

传输层安全漏洞是任何面向互联网或面向内联网的应用程序服务器的首要威胁之一。 本节介绍如何针对这些漏洞强化网络上的主机。 它解决了网络分段、传输控制协议/互联网协议(TCP/IP)堆栈强化以及防火墙用于主机保护的问题。

### 限制开放端点{#limit-open-endpoints}

组织可以具有外部防火墙以限制最终用户和AEM Forms发布场之间的访问。 组织还可以具有内部防火墙，以限制发布场与组织元素内的其他元素（例如，创作实例、处理实例、数据库）之间的访问。 允许防火墙允许最终用户和组织元素内访问有限数量的AEM Forms URL:

#### 配置外部防火墙{#configure-external-firewall}

您可以配置外部防火墙以允许特定AEM Forms URL访问Internet。 填写或提交自适应表单、HTML5、通信管理信件或登录AEM Forms服务器时，需要访问以下URL:

<table> 
 <tbody>
  <tr>
   <td>组件</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>自适应表单</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>HTML5 表单</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>通信管理 </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Forms Portal </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> AEM Forms 应用程序</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### 配置内部防火墙{#configure-internal-firewall}

您可以配置内部防火墙，以允许某些AEM Forms组件（例如，创作实例、处理实例、数据库）与发布场和拓扑图中提到的其他内部组件通信：

<table> 
 <tbody>
  <tr>
   <td>主机<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>发布场（发布节点）</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>处理服务器</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Forms Workflow附加服务器(JEE服务器上的AEM Forms)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### 设置存储库权限和访问控制列表(ACL){#setup-repository-permissions-and-access-control-lists-acls}

默认情况下，发布节点上可用的资产可供每个人访问。 所有资产均启用只读访问权限。 需要启用匿名访问。 如果您计划限制表单视图并仅向经过身份验证的用户提交访问权限，则使用通用组将仅允许经过身份验证的用户对发布节点上可用的资产具有只读访问权限。 以下位置/目录包含需要强化的表单资产（对于已验证的用户具有只读访问权限）：

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## 安全地处理表单数据{#securely-handle-forms-data}

AEM Forms将数据存储到预定义位置和临时文件夹。 您应该保护数据以防止未经授权的使用。

### 设置临时文件夹{#setup-periodic-cleanup-of-temporary-folder}的定期清理

在为文件附件、验证或预览组件配置表单时，相应数据会存储在位于/tmp/fd/的发布节点中。 数据会定期清除。 您可以修改默认数据清除作业，使其更加积极。 要修改计划清除数据的作业，请打开AEM Web Console，打开AEM Forms临时存储清理任务，并修改Cron表达式。

在上述情况下，数据仅会保存给经过身份验证的用户。 此外，还使用访问控制列表(ACL)保护数据。 因此，修改数据清除是保护信息的额外步骤。

### 通过表单门户提交操作{#secure-data-saved-by-forms-portal-submit-action}保存的数据安全

默认情况下，自适应表单的表单门户提交操作会将数据保存到发布节点的本地存储库中。 数据保存在/content/forms/fp中。 **不建议在发布实例上存储数据。**

您可以将存储服务配置为通过线路发送到处理群集，而无需在发布节点上本地保存任何内容。 处理群集位于专用防火墙后的安全区域中，并且数据保持安全。

使用AEM DS设置服务的处理服务器的凭据将数据从发布节点发布到处理服务器。 建议使用对处理服务器存储库具有读写访问权限的受限非管理用户的凭据。 有关更多信息，请参阅[为草稿和提交配置存储服务](/help/forms/using/configuring-draft-submission-storage.md)。

### 由表单数据模型(FDM){#secure-data-handled-by-form-data-model-fdm}处理的安全数据

使用具有最低所需权限的用户帐户来配置表单数据模型(FDM)的数据源。 使用管理帐户可以为未经授权的用户提供对元数据和架构实体的公开访问。\
数据集成还提供了授权FDM服务请求的方法。 您可以插入执行前和执行后授权机制来验证请求。 在预填表单、提交表单以及通过规则调用服务时，会生成服务请求。

**预处理授权：** 您可以在执行请求之前，使用预处理授权来验证请求的真实性。您可以使用输入、服务和请求详细信息来允许或停止执行请求。 如果停止执行，则可返回数据集成异常OPERATION_ACCESS_DENIED。 您还可以在发送客户端请求以执行之前对其进行修改。 例如，更改输入并添加其他信息。

**后处理授权：** 在将结果返回给请求者之前，您可以使用后处理授权来验证和控制结果。您还可以过滤、修剪和插入附加数据到结果。

### 限制用户访问{#limit-user-access}

创作、发布和处理实例需要一组不同的用户角色。 请勿使用管理员凭据运行任何实例。

**在发布实例上：**

* 只有表单用户组的用户才能预览、创建草稿和提交表单。
* 只有cm-user-agent组的用户才能预览通信管理信件。
* 禁用所有非必需的匿名访问。

**在创作实例上：**

* 有一组不同的预定义群组，这些群组拥有每个角色的特定权限。 将用户分配到群组。

   * 表单用户组的用户：

      * 可以创建、填写、发布和提交表单。
      * 无法创建基于XDP的自适应表单。
      * 没有编写自适应表单脚本的权限。
      * 无法导入XDP或包含XDP的任何包
   * 表单 — 高级用户组的用户创建、填写、发布和提交所有类型的表单，编写自适应表单的脚本，导入包含XDP的包。
   * 模板作者用户和模板高级用户可以预览和创建模板。
   * fdm-authors的用户可以创建和修改表单数据模型。
   * cm-user-agent组的用户可以创建、预览和发布通信管理信件。
   * 工作流编辑器组的用户可以创建收件箱应用程序和工作流模型。


**在处理作者时：**

* 对于远程保存和提交用例，请创建具有读取、创建和修改crx-repository内容/form/fp路径的权限的用户。
* 将用户添加到工作流用户组，以允许用户使用AEM收件箱应用程序。

## AEM Forms环境{#secure-intranet-elements-of-an-aem-forms-environment}的安全内联网元素

通常，处理群集和Forms Workflow附加组件(JEE上的AEM Forms)在防火墙后运行。 所以，这些是安全的。 您仍可以执行一些步骤来强化这些环境：

### 安全处理群集{#secure-processing-cluster}

处理群集在创作模式下运行，但不会将其用于开发活动。 不允许将普通用户包含在处理群集的内容作者和表单用户组中。

### 使用AEM最佳实践保护AEM Forms环境{#use-aem-best-practices-to-secure-an-aem-forms-environment}

本文档提供了特定于AEM Forms环境的说明。 您应确保基础AEM安装在部署时是安全的。 有关详细说明，请参阅[AEM安全检查列表](/help/sites-administering/security-checklist.md)文档。
