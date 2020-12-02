---
title: 对AEM Forms应用程序进行疑难解答
seo-title: 对AEM Forms应用程序进行疑难解答
description: 了解AEM Forms应用程序的常见问题以及如何解决这些问题。
seo-description: 了解AEM Forms应用程序的常见问题以及如何解决这些问题。
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---


# 对AEM Forms应用程序{#troubleshoot-aem-forms-app}进行疑难解答

本文介绍构建AEM Forms应用程序时可能显示的错误消息以及解决这些错误的步骤。

本文的章节包括：

* [iOS用户的附件丢失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [工作区用户提交的HTML5表单草稿在门户上不可见](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表单（未缓存）无法在AEM Forms应用程序中加载](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms在Windows上不同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支持的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle插件兼容性问题](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用户的附件丢失{#attachment-loss-for-ios-users}

AEM Forms的iOS应用程序配置为在OSGi上与AEM Forms同步，仅支持字段级附件。 所有附件必须具有唯一的名称。 如果多个附件的名称相同，则仅保留一个附件，而所有其他名称相同的附件将丢失。 请执行以下步骤以防止iOS设备上的用户发生数据丢失：

1. 在连接的服务器上，导航到&#x200B;**Adobe Experience Manager>工具>操作> Web Console**。
1. 查找并单击&#x200B;**自适应表单配置服务**。
1. 在自适应表单配置服务对话框中，启用&#x200B;**使文件名唯一**。

   如果&#x200B;**使文件名唯一**&#x200B;设置处于禁用状态，则如果用户尝试提交具有多个附件的自适应表单，则会丢失数据。

1. 单击&#x200B;**保存**。

## 工作区用户提交的HTML5表单草稿在门户{#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}上不可见

对于在具有&#x200B;**另存为草稿** HTML渲染用户档案的AEM Forms应用程序中启用的HTML5表单，工作区用户不会看到保存的草稿。 要视图门户上由工作区用户提交的已保存的HTML5表单草稿，请执行以下步骤：

1. 打开CRXDE并使用管理员凭据登录。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路径中，在访问控制列表下的访问控制下，单击&#x200B;**+**。
1. 在&#x200B;**添加新条目**&#x200B;对话框中，单击“主体”字段中的组搜索按钮。
1. 在“选择主体”对话框的“名称”字段中，键入`PERM_WORKSPACE_USER`并单击“搜索”**。**
1. 在“选择主体”对话框中选择`PERM_WORKSPACE_USER`组，然后单击&#x200B;**确定**。
1. 在“添加新条目”对话框中，在“主体”字段中选择`PERM_WORKSPACE_USER`组。

   为用户组启用`jcr:read`权限。

1. 单击&#x200B;**确定**。

## HTML5表单（未缓存）无法在AEM Forms应用程序{#html-forms-not-cached-fail-to-load-in-aem-forms-app}中加载

当AEM Forms应用程序连接到旧版AEM Forms服务器时，未缓存的HTML5表单无法在AEM Forms应用程序中加载。

请执行以下步骤以解决问题：

1. 在创作实例中，导航到&#x200B;**Adobe Experience Manager>工具>配置Workspace应用程序脱机服务>立即配置**。
1. 在&#x200B;**工作区App Offline Service**&#x200B;页中，单击&#x200B;**手动资源缓存**。

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在&#x200B;**手动资源缓存**&#x200B;选项卡中，单击&#x200B;**+**&#x200B;按钮以添加CRX路径。
1. 在&#x200B;**添加新资源**&#x200B;字段中，键入：/etc.clientlibs/fd/xfaforms/I18N/en_US.js，然后单击&#x200B;**添加**。
1. 单击&#x200B;**保存**。

## AEM Forms在Windows上不同步{#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms应用程序中，如果表单的路径或其任何资源包含大于或等于256个字符，则表单将不与连接的服务器同步。

修改表单的路径及其资源，将字符数减少到少于256个字符。

## 不支持的Gradle {#unsupported-version-of-gradle}版本

**错误消息：** 项目使用的Gradle版本不受支持。

在Android Studio中构建AEM Forms应用程序时，将显示错误消息。 由于系统上支持的Gradle版本不受支持，因此出现问题。

**解决方** 法： **单击“修复Gradle包装器”并重新导** 入项目以解决此问题。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle插件兼容性问题{#gradle-and-android-gradle-plug-in-compatibility-issues}

**错误消** 息：Android Gradle插件和Gradle的版本不兼容。

从Android Studio用户界面的&#x200B;**Build**&#x200B;菜单中选择&#x200B;**Build APK**&#x200B;选项时，将显示错误消息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**分辨率：** 打 **开Gradle Scripts** >  **gradle-wrapper.properties文件并** 编辑distributionUrl **** 属性。

例如，Android Studio控制台建议将Gradle版本降级为3.5。在&#x200B;**gradle-wrapper.properties**&#x200B;文件的&#x200B;**distributionUrl**&#x200B;中编辑该版本。

再次选择&#x200B;**Build** > **Build APK**&#x200B;以解决错误并生成。apk文件。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

