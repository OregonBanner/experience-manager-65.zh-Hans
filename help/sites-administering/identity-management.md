---
title: Identity Management
seo-title: Identity Management
description: 了解AEM中的身份管理。
seo-description: Learn about identity management in AEM.
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
exl-id: acb5b235-523e-4c01-9bd2-0cc2049f88e2
source-git-commit: 1036127ae508ec76c868db5fb67709c104c51123
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 2%

---


# Identity Management{#identity-management}

只有在您提供网站访问者登录功能后，才能识别这些访问者。 您可能希望提供登录功能的原因有多种：

* [AEM Communities](/help/communities/overview.md)站点访客需要登录才能将内容发布到社区。
* [封闭用户组](/help/sites-administering/cug.md)

  您可能需要限制特定访客访问您的网站（或部分网站）。

* [个性化](/help/sites-administering/personalization.md) 允许访客配置访问网站方式的某些方面。

登录（和注销）功能由 [具有的帐户 **个人资料**](#profiles-and-user-accounts)，其中包含有关已注册访客（用户）的其他信息。 注册和授权的实际流程可能有所不同：

* 从网站自助注册

  A [社区站点](/help/communities/sites-console.md) 可以配置为允许访客使用其Facebook或Twitter帐户自助注册或登录。

* 网站注册申请

  对于封闭用户组，您可能允许访客请求注册，但通过工作流强制执行授权。

* 从创作环境注册每个帐户

  如果您的配置文件数量较少（无论如何都需要授权），则可以决定直接注册每个配置文件。

要允许访客注册，可使用一系列组件和表单来收集所需的标识信息，然后收集其他（通常是可选的）配置文件信息。 在注册后，他们还可以查看和更新已提交的详细信息。

可以配置或开发其他功能：

* 配置所需的任何反向复制。
* 允许用户通过结合工作流开发表单来删除其用户档案。

>[!NOTE]
>
>配置文件中指定的信息也可用于通过以下方式向用户提供目标内容 [区段](/help/sites-administering/campaign-segmentation.md) 和 [营销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## 注册Forms {#registration-forms}

A [表单](/help/sites-authoring/default-components.md#form-component) 可用于收集注册信息，然后生成新的帐户和配置文件。

例如，用户可以使用“Geometrixx”页面请求新的配置文件
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![示例注册表](assets/registerform.png)

提交请求后，将打开用户档案页面，用户可在其中提供个人详细信息。

![示例配置文件页面](assets/profilepage.png)

新帐户也显示在 [用户控制台](/help/sites-administering/security.md).

## 登录 {#login}

登录组件可用于收集登录信息，然后激活登录过程。

这向访客提供了以下标准字段 **用户名** 和 **密码**，带有 **登录** 按钮以在输入凭据时激活登录过程。

例如，用户可以登录，也可以使用 **登录** Geometrixx工具栏上的选项（使用页面）：

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登录页面示例](assets/login.png)

## 注销 {#logging-out}

由于存在登录机制，因此还需要注销机制。 这可用作 **注销** Geometrixx选项。

## 查看和更新用户档案 {#viewing-and-updating-a-profile}

根据您的注册表，访客可能在他们的个人资料中注册了信息。 他们应该能够在以后的阶段查看和/或更新此内容。 这可以用类似的形式完成；例如，Geometrixx：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

要查看个人资料的详细信息，请单击 **我的个人资料** 任意页面的右上角；例如，使用 `admin` 帐户：
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用查看其他配置文件 [客户端上下文](/help/sites-administering/client-context.md) （在创作环境中，并且有足够的权限）：

1. 打开一个页面；例如，Geometrixx页面：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 单击 **我的个人资料** 在右上角。 您将看到当前帐户的用户档案；例如，管理员。
1. 按 **control-alt-C** 以打开客户端上下文。
1. 在客户端上下文的左上角，单击 **加载配置文件** 按钮。

   ![“加载配置文件”图标](do-not-localize/loadprofile.png)

1. 从对话框窗口的下拉列表中选择另一个配置文件；例如， **艾莉森·帕克**.
1. 单击&#x200B;**确定**。
1. 再次单击 **我的个人资料**. 将使用Alison的详细信息更新表单。

   ![Alison的示例配置文件](assets/profilealison.png)

1. 您现在可以使用 **编辑个人资料** 或 **更改密码** 以更新详细信息。

## 将字段添加到用户档案定义 {#adding-fields-to-the-profile-definition}

您可以将字段添加到用户档案定义。 例如，要将“最喜爱的颜色”字段添加到Geometrixx配置文件，请执行以下操作：

1. 从网站控制台导航到Geometrixx Outdoors站点>英语>用户>我的个人资料。
1. 双击 **我的个人资料** 页面，以打开它进行编辑。
1. 在 **组件** 按Tab键展开 **表单** 部分。
1. 拖动 **下拉列表** 从副手到外形，就在下方 **关于我** 字段。
1. 双击 **下拉列表** 组件打开配置对话框并输入：

   * **元素名称** - `favoriteColor`
   * **标题** - `Favorite Color`
   * **项目**  — 添加多种颜色作为项目

   单击 **确定** 以保存。

1. 关闭页面并返回 **网站** 控制台并激活“我的配置文件”页面。

   下次查看配置文件时，您可以选择最喜爱的颜色：

   ![Alison Parker最喜爱的颜色示例字段](assets/aparkerfavcolour.png)

   该字段将保存在 **个人资料** 相关用户帐户的部分：

   ![Alison Parker在CRXDE中的数据](assets/aparkercrxdelite.png)

## 配置文件状态 {#profile-states}

在许多用例中，需要知道用户（或其配置文件）是否位于 *特定状态* 还是不行。

这涉及在用户配置文件中定义适当的属性，其方式如下：

* 对用户可见和可访问
* 为每个属性定义两种状态
* 允许在定义的两个状态之间切换

此操作可通过以下方式完成：

* [状态提供程序](#state-providers)

  管理特定属性的两种状态以及这两种状态之间的过渡。

* [工作流](#workflows)

  用于管理与状态相关的操作。

可以定义多个状态；例如，在Geometrixx中，这些状态包括：

* 订阅（或取消订阅）新闻稿或评论会话上的通知
* 添加和删除与朋友的连接

### 状态提供程序 {#state-providers}

状态提供程序管理相关资产的当前状态，以及两个可能状态之间的过渡。

状态提供程序作为组件实施，因此可以根据您的项目进行自定义。 在Geometrixx中，这些功能包括：

* 取消订阅/订阅论坛主题
* 添加/删除朋友

### 工作流 {#workflows}

状态提供程序管理配置文件属性及其状态。

实施与状态相关的操作需要工作流。 例如，在订阅通知时，工作流将处理实际的订阅操作；在从通知取消订阅时，工作流将处理从订阅列表中删除用户的操作。

## 配置文件和用户帐户 {#profiles-and-user-accounts}

配置文件作为的一部分，存储在内容存储库中[用户帐户](/help/sites-administering/user-group-ac-admin.md).

配置文件位于 `/home/users/geometrixx`：

![在CRXDE中看到的配置文件](assets/chlimage_1-138.png)

在标准安装（创作或发布）中，每个人都具有对所有用户整个配置文件信息的读取权限。 每个人都是“*内置组自动包含所有现有用户和组。 无法编辑成员列表*“。

这些访问权限由以下通配符ACL定义：

/home每个用户都允许jcr：read rep：glob = &#42;/profile&#42;

这允许：

* 论坛、评论或博客帖子以显示相应配置文件中的信息（如图标或全名）
* geometrixx配置文件页面的链接

如果此类访问不适用于您的安装，则可以更改这些默认设置。

这可以使用以下代码来完成 **[访问控制](/help/sites-administering/user-group-ac-admin.md#access-right-management)** 选项卡：

![在CRXDE中管理ACL](assets/aclmanager.png)

## 配置文件组件 {#profile-components}

一系列配置文件组件也可用于定义您站点的配置文件要求。

### 检查密码字段 {#checked-password-field}

此组件为您提供以下两个字段：

* 输入密码
* 检查以确认密码输入正确。

在默认设置下，组件将按如下方式显示：

![检查密码对话框](assets/dc_profiles_checkedpassword.png)

### 个人资料头像照片 {#profile-avatar-photo}

此组件为用户提供了一种选择和上传头像照片文件的机制。

![头像选择器](assets/dc_profiles_avatarphoto.png)

### 个人资料详细姓名 {#profile-detailed-name}

此组件允许用户输入详细名称。

![详细名称对话框](assets/dc_profiles_detailedname.png)

### 个人资料性别 {#profile-gender}

此组件允许用户输入其性别。

![性别选择器](assets/dc_profiles_gender.png)
