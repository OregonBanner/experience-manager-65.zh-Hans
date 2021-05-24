---
title: 权限管理的主体视图
seo-title: 权限管理的主体视图
description: 了解可简化权限管理的新触屏UI界面。
seo-description: 了解可简化权限管理的新触屏UI界面。
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
exl-id: 4ce19c95-32cb-4bb8-9d6f-a5bc08a3688d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 1%

---

# 权限管理的主视图{#principal-view-for-permissions-management}

## 概述 {#overview}

AEM 6.5引入了用户和组的权限管理。 主要功能与经典UI相同，但更易于用户使用且效率更高。

## 使用方法 {#how-to-use}

### 访问UI {#accessing-the-ui}

基于UI的新权限管理可通过“安全”下的“权限”卡进行访问，如下所示：

![](assets/screen_shot_2019-03-17at63333pm.png)

通过新视图，可以更轻松地在明确授予权限的所有路径中查看给定主体的整套权限和限制。 这样，您就无需转到

CRXDE可管理高级权限和限制。 已在同一视图中合并。 该视图默认为“每个人”组。

![](assets/unu-1.png)

有一个过滤器允许用户选择主体类型以查看&#x200B;**用户**、**组**&#x200B;或&#x200B;**全部**&#x200B;并搜索任何主体&#x200B;**。**

![](assets/image2019-3-20_23-52-51.png)

### 查看主体{#viewing-permissions-for-a-principal}的权限

左侧的框架允许用户向下滚动以查找任何主体，或根据选定的过滤器搜索组或用户，如下所示：

![](assets/doi-1.png)

单击名称可在右侧显示已分配的权限。 权限窗格显示特定路径上的访问控制条目列表以及配置的限制。

![](assets/trei-1.png)

### 为主体{#adding-new-access-control-entry-for-a-principal}添加新的访问控制条目

通过单击添加ACE按钮添加新的访问控制条目，可添加新权限。

![](assets/patru.png)

此时将显示下面显示的窗口，下一步是选择需要配置权限的路径。

![](assets/cinci-1.png)

在此，我们选择一个路径，用于配置&#x200B;**dam-users**&#x200B;的权限：

![](assets/sase-1.png)

选择路径后，工作流会返回到此屏幕，用户随后可以从可用的命名空间（如`jcr`、`rep`或`crx`）中选择一个或多个权限，如下所示。

可以通过使用文本字段进行搜索，然后从列表中选择来添加权限。

>[!NOTE]
>
>有关权限和描述的完整列表，请参阅[此页面](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

选择权限列表后，用户可以选择权限类型：拒绝或允许，如下所示。

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制{#using-restrictions}

除了给定路径上的权限列表和权限类型之外，此屏幕还允许为细粒度访问控制添加限制，如下所示：

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>有关每个限制含义的更多信息，请参阅[此页面](/help/sites-administering/user-group-ac-admin.md#restrictions)。

可通过选择限制类型、输入值并点击&#x200B;**+**&#x200B;图标，添加如下所示的限制。![](assets/sapte-1.png) ![](assets/opt-1.png)

新ACE将反映在访问控制列表中，如下所示。 请注意，`jcr:write`是包含上面添加的`jcr:removeNode`的聚合权限，但下面未显示为`jcr:write`下所涵盖的权限。

### 编辑ACE {#editing-aces}

可通过选择主体并选择要编辑的ACE来编辑访问控制条目。

例如，在此，我们可以通过单击右侧的铅笔图标，编辑&#x200B;**dam-users**&#x200B;的以下条目：

![](assets/image2019-3-21_0-35-39.png)

在编辑屏幕中显示了预选配置的ACE，单击它们旁边的交叉图标可删除这些ACE，或者可以为给定路径添加新权限，如下所示。

![](assets/noua-1.png)

下面，我们将在给定路径上为&#x200B;**dam-users**&#x200B;添加`addChildNodes`权限。

![](assets/image2019-3-21_0-45-35.png)

单击右上方的&#x200B;**Save**&#x200B;按钮可保存更改，这些更改将反映在**dam用户**的新权限中，如下所示：

![](assets/zece-1.png)

### 删除ACE {#deleting-aces}

可以删除访问控制条目，以删除为特定路径上的主体授予的所有权限。 ACE旁边的X图标可用于删除，如下所示：

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### 经典UI权限组合{#classic-ui-privilege-combinations}

请注意，新权限UI明确使用基本权限集，而不是预定义的组合，这些组合不会真正反映已授予的基本权限。

这会造成对具体配置内容的混淆。 下表列出了从经典UI到构成这些权限的实际权限之间的映射：

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
