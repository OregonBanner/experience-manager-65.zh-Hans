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

---


# 管理对工作流的访问{#managing-access-to-workflows}

根据用户帐户配置ACL以允许（或禁用）启动和参与工作流。

## 工作流所需的用户权限 {#required-user-permissions-for-workflows}

在以下情况下，可以对工作流采取行动：

* 您正在使用帐 `admin` 户
* 帐户已分配给默认组 `workflow-users`:

   * 此用户组拥有用户执行工作流操作所需的所有权限。
   * 当帐户在此组中时，它仅有权访问其启动的工作流。

* 帐户已分配给默认组 `workflow-administrators`:

   * 此用户组拥有特权用户监视和管理工作流所需的所有权限。
   * 帐户在此组中时，它有权访问所有工作流。

>[!NOTE]
>
>这些是最低要求。 您的帐户还必须是已分配的参加者或已分配组的成员才能执行特定步骤。

## 配置对工作流的访问 {#configuring-access-to-workflows}

工作流模型会继承一个默认访问控制列表(ACL)，用于控制用户如何与工作流交互。 要自定义工作流的用户访问权限，请在包含工作流模型节点的文件夹的存储库中修改访问控制列表(ACL):

* [将特定工作流模型的ACL应用到/var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [在/var/workflow/models中创建子文件夹，并将ACL应用于](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>有关使用CRXDE lite配置ACL的信息，请参 [阅访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management)。

### 将特定工作流模型的ACL应用到/var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

如果工作流模型存储在其中， `/var/workflow/models` 则您可以在文件夹中指定一个特定的ACL（仅与该工作流相关）:

1. 在Web浏览器中打开CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，选择工作流模型文件夹的节点：

   `/var/workflow/models`

1. 单击“访 **问控制** ”选项卡。
1. 在“本 **地访问控制策略** (**访问控制列表**)”表中，单击加号图标以添 **加条目**。
1. 在“添 **加新条目** ”对话框中，添加具有以下属性的新ACE:

   * **主要**: `content-authors`
   * **类型**: `Deny`
   * **权限**: `jcr:read`
   * **rep:glob**:对特定工作流的引用
   ![wf-108](assets/wf-108.png)

   “访 **问控制列表** ”(Access Control List `content-authors` )表现在包括对工作流 `prototype-wfm-01` 模型的限制。

   ![wf-109](assets/wf-109.png)

1. 单击“ **全部保存**”。

   该 `prototype-wfm-01` 工作流不再对组成员可 `content-authors` 用。

### 在/var/workflow/models中创建子文件夹，并将ACL应用于 {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

开 [发团队可以在](/help/sites-developing/workflows-models.md#creating-a-new-workflow)

`/var/workflow/models`

与存储在

`/var/workflow/models/dam/`

然后，您可以向文件夹本身添加ACL。

1. 在Web浏览器中打开CRXDE Lite(例如， [http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在节点树中，选择工作流模型文件夹中单个文件夹的节点；例如：

   `/var/workflow/models/prototypes`

1. 单击“访 **问控制** ”选项卡。
1. 在“适 **用的访问控制策略** ”(Applicable Access Control Policy **)表格中，单击加号图标** 以添加条目。
1. 在“本 **地访问控制策略** (**访问控制列表**)”表中，单击加号图标以添 **加条目**。
1. 在“添 **加新条目** ”对话框中，添加具有以下属性的新ACE:

   * **主要**: `content-authors`
   * **类型**: `Deny`
   * **权限**: `jcr:read`
   >[!NOTE]
   >
   >与将特 [定工作流模型的ACL应用到/var/workflow/models一样](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) ，您可以包含rep:glob以限制对特定工作流的访问。

   ![wf-110](assets/wf-110.png)

   “访 **问控制列表** ”(Access Control List `content-authors` )表现在包括对文件夹 `prototypes` 的限制。

   ![wf-111](assets/wf-111.png)

1. 单击“ **全部保存**”。

   文件夹中的模 `prototypes` 型不再对组成员可 `content-authors` 用。

