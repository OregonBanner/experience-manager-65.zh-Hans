---
title: 身份管理
seo-title: 身份管理
description: 了解AEM中的身份管理。
seo-description: 了解AEM中的身份管理。
uuid: d9b83cd7-c47a-41a5-baa4-bbf385d13bfd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 994a5751-7267-4a61-9bc7-01440a256c65
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# 身份管理{#identity-management}

只有在您提供登录功能时，才能识别网站的各个访客。 您可能希望提供登录功能的原因有多种：

* [AEM](/help/communities/overview.md)Communities站点访问者需要登录才能向社区发布内容。
* [已关闭的用户组](/help/sites-administering/cug.md)

   您可能需要将访问您的网站（或网站的各个部分）的权限限制为特定访客。

* [个性化](/help/sites-administering/personalization.md) -允许访客配置访问网站的某些方面。

登录（和注销）功能由帐户提供， [该帐户具有 **Profile **](#profiles-and-user-accounts)，其中包含有关注册访客（用户）的其他信息。 注册和授权的实际过程可能不同：

* 从网站自助注册

   可 [以配置社区站点](/help/communities/sites-console.md) ，以允许访客使用其Facebook或Twitter帐户自行注册或登录。

* 从网站申请注册

   对于已关闭的用户组，您可能允许访客请求注册，但通过工作流强制授权。

* 从创作环境中注册每个帐户

   如果您拥有少量配置文件（无论如何都需要授权），您可以决定直接注册每个配置文件。

为了允许访客注册，可以使用一系列组件和表单来收集所需的标识信息，然后再收集其他（通常是可选的）配置文件信息。 注册后，还应当能够查看和更新自己提交的详细信息。

可以配置或开发其他功能：

* 配置所需的任何反向复制。
* 通过开发表单和工作流，允许用户删除其配置文件。

>[!NOTE]
>
>配置文件中指定的信息还可用于通过“区段”和“营销活动”为用户提供 [目标](/help/sites-administering/campaign-segmentation.md)[内容](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。

## 注册表单 {#registration-forms}

表 [单](/help/sites-authoring/default-components.md#form-component) ，可用于收集注册信息，然后生成新帐户和配置文件。

例如，用户可以使用Geometrixx页面请求新的配置文件`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![注册表](assets/registerform.png)

提交请求后，将打开配置文件页面，用户可在其中提供个人详细信息。

![概要分析页](assets/profilepage.png)

新帐户也会显示在“用户”控 [制台中](/help/sites-administering/security.md)。

## 登录 {#login}

登录组件可用于收集登录信息，然后激活登录过程。

这为访客提供了“用户名”和“密码 **”的标准字段** ，并提供了“登录 ******** ”按钮，以在输入凭据时激活登录过程。

例如，用户可以使用Geometrixx工具栏上的“登录”选项登录或创建新帐户，该工具栏使用页面： ****

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![登录](assets/login.png)

## 注销 {#logging-out}

由于存在登录机制，因此也需要注销机制。 此选项在Geometrixx中 **作为“注销** ”选项可用。

## 查看和更新配置文件 {#viewing-and-updating-a-profile}

根据您的注册表单，访客的个人资料中可能包含注册信息。 他们应该能够在以后的阶段查看和／或更新它。 这可以用类似的表单完成；例如，在Geometrixx中：

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

要查看您的个人资料的详细信息，请单击任 **何页面右上角的** “我的个人资料”;例如，帐户 `admin` :
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

您可以使用Client Context(在创作环境中， [并具有足够的权限](/help/sites-administering/client-context.md) )查看另一个配置文件：

1. 打开页面；例如，Geometrixx页面：

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. 单 **击右上角的** “我的配置文件”。 您将看到您经常帐户的档案；例如，管理员。
1. 按 **Control-alt-C** 打开Client Context。
1. 在Client Context的左上角，单击“加载配 **置文件”按钮** 。

   ![](do-not-localize/loadprofile.png)

1. 从对话框窗口的下拉列表中选择另一个配置文件；例如，艾莉森 **·帕克**。
1. 单击&#x200B;**确定**。
1. 再次单击“我的 **配置文件”**。 此时将更新表单，其中包含Alison的详细信息。

   ![profilesion](assets/profilealison.png)

1. 您现在可以使用“编 **辑配置文件** ”或“ **更改密码** ”来更新详细信息。

## 将字段添加到配置文件定义 {#adding-fields-to-the-profile-definition}

您可以向配置文件定义中添加字段。 例如，向Geometrixx配置文件添加“收藏夹颜色”字段：

1. 从“网站”控制台中，导航到Geometrixx Outdoors站点>英语>用户>我的配置文件。
1. 双击“我的配置 **文件** ”页面以打开它进行编辑。
1. 在Sidekick的 **组件** ，展开表 **单部分** 。
1. 将“下 **拉列表** ”从Sidekick拖到表单中，就在“关于我” **字段的下方** 。
1. 双击下拉列 **表组件** ，打开配置对话框并输入：

   * **元素名称** - `favoriteColor`
   * **标题** - `Favorite Color`
   * **项目** -将多种颜色添加为项目
   单击&#x200B;**确定**&#x200B;进行保存。

1. 关闭页面并返回到“网站”控 **制台** ，然后激活“我的配置文件”页面。

   下次查看配置文件时，您可以选择喜爱的颜色：

   ![parkefavcolor](assets/aparkerfavcolour.png)

   该字段将保存在相关用户帐 **户的** “配置文件”部分下：

   ![arkerxdelite](assets/aparkercrxdelite.png)

## 个人资料状态 {#profile-states}

有许多用例需要了解用户（或者更确切地说，是其配置文件）是否处于特 *定状态* 。

这包括在用户配置文件中定义适当的属性，其方式如下：

* 对用户可见且可访问
* 为每个属性定义两个状态
* 允许在定义的两种状态之间切换

这是通过以下方式完成的：

* [状态提供者](#state-providers)

   管理特定属性的两种状态以及两种属性之间的过渡。

* [工作流](#workflows)

   管理与状态相关的操作。

可以定义多个状态；例如，在Geometrixx中，这些包括：

* 在新闻稿或评论线程上订阅（或取消订阅）通知
* 向朋友添加和删除连接

### 状态提供者 {#state-providers}

状态提供程序管理相关属性的当前状态以及两个可能状态之间的过渡。

状态提供者作为组件实施，因此可以为项目自定义。 在Geometrixx中，这些包括：

* 取消订阅/订阅论坛主题
* 添加/删除好友

### 工作流 {#workflows}

状态提供者管理配置文件属性及其状态。

需要一个工作流来实施与状态相关的操作。 例如，订阅通知时，该工作流将处理实际的订阅操作；从通知中取消订阅时，该工作流将处理从订阅列表中删除用户的操作。

## 配置文件和用户帐户 {#profiles-and-user-accounts}

配置文件作为用户帐户的一部分存储在内容[存储库中](/help/sites-administering/user-group-ac-admin.md)。

配置文件位于以下位置 `/home/users/geometrixx`:

![chlimage_1-138](assets/chlimage_1-138.png)

在标准安装（创作或发布）中，每个人都有权读取所有用户的整个配置文件信息。 每个人都是一个“*自动包含所有现有用户和用户组的内置用户组”。 不能编辑成员列表*”。

这些访问权限由以下通配符ACL定义：

/home everyone allojcr:read rep:glob = */profile*

这允许：

* 论坛、评论或博客文章，以显示相应配置文件中的信息（如图标或全名）
* geometrixx配置文件页面的链接

如果此类访问不适合您的安装，您可以更改这些默认设置。

这可以使用“访问控制” **[选项卡完](/help/sites-administering/user-group-ac-admin.md#access-right-management)**成：

![aclmanager](assets/aclmanager.png)

## 个人资料组件 {#profile-components}

还提供一系列配置文件组件，用于定义站点的配置文件要求。

### 检查密码字段 {#checked-password-field}

此组件为您提供了两个字段。分别用于：

* 输入密码
* 确认密码已正确输入。

使用默认设置时组件将显示为：

![dc_profiles_checkedpassword](assets/dc_profiles_checkedpassword.png)

### 个人资料头像照片 {#profile-avatar-photo}

此组件为用户提供了选择和上传头像照片文件的途径。

![dc_profiles_avatarphoto](assets/dc_profiles_avatarphoto.png)

### 个人资料详细姓名 {#profile-detailed-name}

此组件允许用户输入详细的名称。

![dc_profiles_detailedname](assets/dc_profiles_detailedname.png)

### 个人资料性别 {#profile-gender}

此组件允许用户输入其性别。

![dc_profiles_geder](assets/dc_profiles_gender.png)

