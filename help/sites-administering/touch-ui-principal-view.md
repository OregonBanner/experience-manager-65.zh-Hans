---
title: 权限管理的主体视图
description: 了解新的触屏UI界面，该界面有助于进行权限管理。
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: fd8bb7d3d9040e0a7a6b2f65751445f41aeab73e
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---


# 权限管理的主体视图{#principal-view-for-permissions-management}

## 概述 {#overview}

AEM 6.5引入了用户和组的权限管理。 主要功能与经典UI相同，但更加用户友好且高效。

## 使用方法 {#how-to-use}

### 访问UI {#accessing-the-ui}

通过安全性下的权限卡访问新的基于UI的权限管理，如下所示：

![权限管理UI](assets/screen_shot_2019-03-17at63333pm.png)

通过新视图，可以更轻松地查看明确授予权限的所有路径上给定主体的整套权限和限制。 这样便无需转至

CRXDE用于管理高级权限和限制。 该报表已合并到同一视图中。 该视图默认为“everyone”组。

![“每个人”组的视图](assets/unu-1.png)

有一个过滤器允许用户选择要查看的承担者类型 **用户**， **组**，或 **全部**&#x200B;并搜索任意主体&#x200B;**.**

![搜索承担者类型](assets/image2019-3-20_23-52-51.png)

### 查看承担者的权限 {#viewing-permissions-for-a-principal}

左侧的框架允许用户向下滚动以查找任何承担者或根据所选筛选器搜索组或用户，如下所示：

![查看主体的权限](assets/doi-1.png)

单击名称会在右侧显示分配的权限。 权限窗格显示特定路径上的访问控制条目列表以及配置的限制。

![查看ACL列表](assets/trei-1.png)

### 为主体添加新的访问控制条目 {#adding-new-access-control-entry-for-a-principal}

可以通过添加访问控制条目来添加新权限。 只需单击Add ACE按钮。

![为主体添加新ACL](assets/patru.png)

此时将显示以下窗口，下一步是选择必须配置权限的路径。

![配置权限路径](assets/cinci-1.png)

此处，选择一个路径，您可以在其中配置权限 **dam-users**：

![dam-users的配置示例](assets/sase-1.png)

选择路径后，工作流将返回此屏幕，用户随后可以从可用命名空间中选择一个或多个权限(例如 `jcr`， `rep` 或 `crx`)，如下所示。

可以通过使用文本字段进行搜索，然后从列表中选择来添加权限。

>[!NOTE]
>
>有关权限和说明的完整列表，请参阅 [此页面](/help/sites-administering/user-group-ac-admin.md#access-right-management).

![给定路径的搜索权限。](assets/image2019-3-21_0-5-47.png) ![为“dam-users”添加新条目，如在垂直列中选择的路径所示。](assets/image2019-3-21_0-6-53.png)

选择权限列表后，用户可以选择权限类型：拒绝或允许，如下所示。

![选择权限](assets/screen_shot_2019-03-17at63938pm.png) ![选择权限](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制 {#using-restrictions}

除了给定路径上的权限和权限类型列表之外，此屏幕还允许您为细粒度访问控制添加限制，如下所示：

![添加限制](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>有关每个限制的含义的更多信息，请参阅 [Jackrabbit Oak文档](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html).

通过选择限制类型、输入值并单击 **+** 图标。

![添加限制类型](assets/sapte-1.png) ![添加限制类型](assets/opt-1.png)

新的ACE会反映在“访问控制列表”中，如下所示。 请注意 `jcr:write` 是聚合权限，包括 `jcr:removeNode` ，但下文未显示其在 `jcr:write`.

### 编辑ACE {#editing-aces}

通过选择承担者并选择要编辑的ACE，可以编辑访问控制条目。

例如，您可以在此处编辑以下条目 **dam-users** 单击右侧的铅笔图标：

![添加限制](assets/image2019-3-21_0-35-39.png)

此时将显示编辑屏幕，其中已预先选择配置的ACE，单击它们旁边的交叉图标可以删除这些ACE，也可以为给定路径添加新权限，如下所示。

![编辑条目](assets/noua-1.png)

此处 `addChildNodes` 已添加权限 **dam-users** 在给定路径上。

![添加权限](assets/image2019-3-21_0-45-35.png)

单击 **保存** 按钮，并且更改会反映在的新权限中 **dam-users** 如下所示：

![保存更改](assets/zece-1.png)

### 删除ACE {#deleting-aces}

可以删除访问控制条目，以删除授予特定路径上的承担者的所有权限。 可以使用ACE旁边的X图标将其删除，如下所示：

![删除ACE](assets/image2019-3-21_0-53-19.png) ![删除ACE](assets/unspe.png)

### 经典UI权限组合 {#classic-ui-privilege-combinations}

新权限UI明确使用基本权限集，而不是预定义的组合，这些组合不能真正反映所授予的确切基础权限。

这会导致混淆，不知到底在配置什么内容。 下表列出了从经典UI到组成权限组合的实际权限之间的映射：

<table>
 <tbody>
  <tr>
   <th>经典UI权限组合</th>
   <th>权限UI权限</th>
  </tr>
  <tr>
   <td>读取</td>
   <td><code>jcr:read</code></td>
  </tr>
  <tr>
   <td>修改</td>
   <td><p><code>jcr:modifyProperties</code></p> <p><code>jcr:lockManagement</code></p> <p><code>jcr:versionManagement</code></p> </td>
  </tr>
  <tr>
   <td>创建</td>
   <td><p><code>jcr:addChildNodes</code></p> <p><code>jcr:nodeTypeManagement</code></p> </td>
  </tr>
  <tr>
   <td>删除</td>
   <td><p><code>jcr:removeNode</code></p> <p><code>jcr:removeChildNodes</code></p> </td>
  </tr>
  <tr>
   <td>读取 ACL</td>
   <td><code>jcr:readAccessControl</code></td>
  </tr>
  <tr>
   <td>编辑 ACL</td>
   <td><code>jcr:modifyAccessControl</code></td>
  </tr>
  <tr>
   <td>复制</td>
   <td><code>crx:replicate</code></td>
  </tr>
 </tbody>
</table>
