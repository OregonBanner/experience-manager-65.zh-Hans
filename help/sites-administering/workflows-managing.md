---
title: 管理对工作流的访问
seo-title: 管理对工作流的访问
description: 了解如何管理对工作流的访问。
seo-description: 了解如何管理对工作流的访问。
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---


# 管理对工作流的访问{#managing-access-to-workflows}

根据用户帐户配置ACL以允许（或禁用）启动和参与工作流。

## 工作流{#required-user-permissions-for-workflows}所需的用户权限

在下列情况下，可对工作流采取行动：

* 您正在使用`admin`帐户
* 帐户已分配给默认组`workflow-users`:

   * 此组包含用户执行工作流操作所需的所有权限。
   * 当帐户在此组中时，它仅有权访问已启动的工作流。

* 帐户已分配给默认组`workflow-administrators`:

   * 此组拥有特权用户监视和管理工作流所需的所有权限。
   * 帐户在此组中时，它有权访问所有工作流。

>[!NOTE]
>
>这些是最低要求。 您的帐户还必须是已分配的参加者或已分配组的成员，才能执行特定步骤。

## 配置对工作流{#configuring-access-to-workflows}的访问

工作流模型继承默认的访问控制列表(ACL)，用于控制用户如何与工作流交互。 要自定义工作流的用户访问权限，请修改包含工作流模型节点的文件夹的存储库中的访问控制列表(ACL):

* [将特定工作流模型的ACL应用于/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中创建子文件夹，并将ACL应用于](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有关使用CRXDE Lite配置ACL的信息，请参见[访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 将特定工作流模型的ACL应用于/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型存储在`/var/workflow/models`中，则可以在文件夹中指定仅与该工作流相关的特定ACL:

1. 在Web浏览器中打开CRXDE Lite(例如，[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，选择工作流模型文件夹的节点：

   `/var/workflow/models`

1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 在&#x200B;**本地访问控制策略**(**访问控制列表**)表中，单击加号图标到&#x200B;**添加条目**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，添加具有以下属性的新ACE:

   * **主要**:  `content-authors`
   * **类型**: `Deny`
   * **特权**:  `jcr:read`
   * **rep:glob**:对特定工作流的引用

   ![wf-108](assets/wf-108.png)

   **访问控制列表**&#x200B;表现在包括对`prototype-wfm-01`工作流模型的`content-authors`的限制。

   ![wf-109](assets/wf-109.png)

1. 单击&#x200B;**保存全部**。

   `prototype-wfm-01`工作流不再对`content-authors`组的成员可用。

### 在/var/workflow/models中创建子文件夹，并将ACL应用于该{#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

您的[开发团队可以在](/help/sites-developing/workflows-models.md#creating-a-new-workflow)的子文件夹中创建工作流

`/var/workflow/models`

与存储在

`/var/workflow/models/dam/`

然后，您可以向文件夹本身添加ACL。

1. 在Web浏览器中打开CRXDE Lite(例如，[http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，选择工作流模型文件夹中单个文件夹的节点；例如：

   `/var/workflow/models/prototypes`

1. 单击&#x200B;**访问控制**&#x200B;选项卡。
1. 在&#x200B;**适用的访问控制策略**&#x200B;表中，单击加号图标以添加&#x200B;**条目。**
1. 在&#x200B;**本地访问控制策略**(**访问控制列表**)表中，单击加号图标到&#x200B;**添加条目**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，添加具有以下属性的新ACE:

   * **主要**:  `content-authors`
   * **类型**: `Deny`
   * **特权**:  `jcr:read`

   >[!NOTE]
   >
   >与[将特定工作流模型的ACL应用到/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)一样，您可以包含一个rep:glob以限制对特定工作流的访问。

   ![wf-110](assets/wf-110.png)

   **访问控制列表**&#x200B;表现在包括对`prototypes`文件夹`content-authors`的限制。

   ![wf-111](assets/wf-111.png)

1. 单击&#x200B;**保存全部**。

   `prototypes`文件夹中的模型不再对`content-authors`组的成员可用。

