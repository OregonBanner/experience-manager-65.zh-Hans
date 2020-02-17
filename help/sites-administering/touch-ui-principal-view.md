---
title: 权限管理的主视图
seo-title: 权限管理的主视图
description: 了解有助于权限管理的新触屏UI界面。
seo-description: 了解有助于权限管理的新触屏UI界面。
uuid: 16c5889a-60dd-4b66-bbc4-74fbdb5fc32f
contentOwner: sarchiz
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: db8665fa-353f-45c2-8e37-169d5c1df873
docset: aem65
translation-type: tm+mt
source-git-commit: a156e09e77951041dce017f2f78069bc050b6bdb

---


# 权限管理的主视图{#principal-view-for-permissions-management}

## 概述 {#overview}

AEM 6.5引入了用户和用户组的权限管理。 主要功能与经典UI保持相同，但更易用、更高效。

## 使用方法 {#how-to-use}

### 访问UI {#accessing-the-ui}

基于新UI的权限管理可通过“安全性”下的“权限”卡访问，如下所示：

![](assets/screen_shot_2019-03-17at63333pm.png)

新视图使得在所有已明确授予权限的路径中查看给定主体的整套权限和限制变得更容易。 这样，您就无需转到

用于管理高级权限和限制的CRXDE。 它已在同一视图中合并。 视图默认为“每个人”组。

![](assets/unu-1.png)

有一个过滤器，允许用户选择查看“用户”( **Users**)、“组”( **Groups**)或“全部”(All)的主体类型， **并**&#x200B;搜索任何主体&#x200B;**。**

![](assets/image2019-3-20_23-52-51.png)

### 查看主体的权限 {#viewing-permissions-for-a-principal}

左侧的框架允许用户向下滚动以查找任何主体，或根据选定的筛选器搜索组或用户，如下所示：

![](assets/doi-1.png)

单击该名称后，右侧将显示已分配的权限。 权限窗格显示特定路径上的访问控制条目列表以及配置的限制。

![](assets/trei-1.png)

### 为主体添加新的访问控制条目 {#adding-new-access-control-entry-for-a-principal}

通过单击“添加ACE”按钮，可以通过添加新的“访问控制条目”来添加新权限。

![](assets/patru.png)

这会显示下面显示的窗口，下一步是选择需要配置权限的路径。

![](assets/cinci-1.png)

在此，我们选择一个路径，以便为 **dam用户配置权限**:

![](assets/sase-1.png)

选择路径后，工作流将返回此屏幕，用户随后可以从可用的命名空间（如或）中选择一个或多个权限， `jcr`如 `rep` 下 `crx`所示。

可以通过使用文本字段进行搜索，然后从列表中选择来添加权限。

>[!NOTE]
>
>有关权限和说明的完整列表，请参阅 [此页](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

![](assets/image2019-3-21_0-5-47.png) ![](assets/image2019-3-21_0-6-53.png)

选择权限列表后，用户可以选择权限类型：拒绝或允许，如下所示。

![](assets/screen_shot_2019-03-17at63938pm.png) ![](assets/screen_shot_2019-03-17at63947pm.png)

### 使用限制 {#using-restrictions}

除了给定路径上的权限列表和权限类型之外，此屏幕还允许为细粒度访问控制添加限制，如下所示：

![](assets/image2019-3-21_1-4-14.png)

>[!NOTE]
>
>有关每项限制的含义的更多信息，请查阅 [本页](/help/sites-administering/user-group-ac-admin.md#restrictions)。

通过选择限制类型、输入值并点击 **+图标，可以添加如下限制** 。 ![](assets/sapte-1.png) ![](assets/opt-1.png)

新的ACE将反映在访问控制列表中，如下所示。 请注意， `jcr:write` 这是包括上面添加的权 `jcr:removeNode` 限的聚合权限，但下面并未显示该权限所涵盖的权限 `jcr:write`。

### 编辑ACE {#editing-aces}

通过选择一个主体并选择要编辑的ACE，可以编辑访问控制条目。

例如，在此处，我们可以通过单击右 **侧的铅笔图标** ，编辑dam用户的以下条目：

![](assets/image2019-3-21_0-35-39.png)

在显示编辑屏幕时，会预先选择已配置的ACE，单击它们旁边的叉号图标即可删除这些ACE，或者可以为给定路径添加新权限，如下所示。

![](assets/noua-1.png)

在此，我们将为给定 `addChildNodes` 路径 **上的DAM用户添加权限** 。

![](assets/image2019-3-21_0-45-35.png)

单击右上方的“保存 **** ”按钮可保存更改，更改将反映在**dam-users **的新权限中，如下所示：

![](assets/zece-1.png)

### 删除ACE {#deleting-aces}

可以删除访问控制条目以删除授予特定路径上的主体的所有权限。 ACE旁边的X图标可用于删除它，如下所示：

![](assets/image2019-3-21_0-53-19.png) ![](assets/unspe.png)

### 经典UI权限组合 {#classic-ui-privilege-combinations}

请注意，新权限UI显式地使用基本权限集而不是预定义的组合，这些组合没有真正反映已授予的确切底层权限。

它导致了对具体配置内容的混淆。 下表列出了从经典UI到构成这些权限的实际权限之间的映射：

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

