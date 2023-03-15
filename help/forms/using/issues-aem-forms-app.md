---
title: AEM Forms应用程序疑难解答
seo-title: Troubleshoot AEM Forms app
description: 了解AEM Forms应用程序的常见问题以及如何对其进行故障排除。
seo-description: Learn about common issues with AEM Forms app and how to troubleshoot them.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# AEM Forms应用程序疑难解答 {#troubleshoot-aem-forms-app}

本文介绍了构建AEM Forms应用程序时可能显示的错误消息以及解决这些消息的步骤。

本文中的部分包括：

* [iOS用户的附件丢失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Workspace用户提交的HTML5表单草稿在门户上不可见](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [无法在AEM Forms应用程序中加载HTML5表单（未缓存）](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms无法在Windows上同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不受支持的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle插件兼容性问题](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用户的附件丢失 {#attachment-loss-for-ios-users}

iOS的AEM Forms应用程序配置为在OSGi上与AEM Forms同步，该应用程序仅支持字段级附件。 所有附件必须具有唯一的名称。 如果多个附件具有相同的名称，则仅保留一个附件，而具有相同名称的所有其他附件都将丢失。 执行以下步骤，防止iOS设备上的用户遇到数据丢失问题：

1. 在连接的服务器上，导航到 **Adobe Experience Manager >工具>操作> Web控制台**.
1. 查找并单击 **[!UICONTROL 自适应表单和交互式通信Web渠道配置]**.
1. 在 [!UICONTROL 自适应表单和交互式通信Web渠道配置] 对话框，启用 **使文件名唯一**.

   如果 **使文件名唯一** 设置已禁用，如果用户尝试提交具有多个附件的自适应表单，则会遇到数据丢失。

1. 单击“**保存**”。

## Workspace用户提交的HTML5表单草稿在门户上不可见 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

适用于AEM Forms应用程序中启用的HTML5表单，具有 **另存为草稿** HTML渲染配置文件，工作区用户看不到保存的草稿。 要查看由工作区用户在门户上提交的HTML5表单的已保存草稿，请执行以下步骤：

1. 打开CRXDE并使用管理员凭据登录。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路径中，在访问控制下的访问控制列表中，单击 **+**.
1. 在 **添加新条目** 对话框中，单击“承担者”字段中的组搜索按钮。
1. 在“选择承担者”对话框的“名称”字段中，键入 `PERM_WORKSPACE_USER` 并单击 **搜索**.
1. 选择 `PERM_WORKSPACE_USER` 组，然后单击 **确定**.
1. 在“添加新条目”对话框中， `PERM_WORKSPACE_USER` 在“承担者”字段中选择“组”。

   启用 `jcr:read` 用户组的权限。

1. 单击&#x200B;**确定**。

## 无法在AEM Forms应用程序中加载HTML5表单（未缓存） {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

当AEM Forms应用程序连接到较低版本的AEM Forms服务器时，未缓存的HTML5表单无法在AEM Forms应用程序中加载。

执行以下步骤来解决问题：

1. 在创作实例中，导航到 **Adobe Experience Manager >工具>配置Workspace App离线服务>立即配置**.
1. In **Workspace应用程序离线服务** 页面，单击 **手动资源缓存**.

   URL： https://&lt;server>：&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在 **手动资源缓存** 选项卡，单击 **+** 按钮以添加CRX路径。
1. 在 **添加新资源** 字段，键入： /etc.clientlibs/fd/xfaforms/I18N/en_US.js ，然后单击 **添加**.
1. 单击“**保存**”。

## AEM Forms无法在Windows上同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms应用程序中，如果表单路径或其任何资源包含大于或等于256个字符，则表单不会与连接的服务器同步。

修改表单的路径及其资源，将字符数减少到256个字符以下。

## 不受支持的Gradle版本 {#unsupported-version-of-gradle}

**错误消息：** 该项目正在使用不受支持的Gradle版本。

在Android Studio中构建AEM Forms应用程序时显示错误消息。 出现此问题的原因是，系统上支持的Gradle版本不受支持。

**分辨率：** 单击 **修复Gradle包装并重新导入项目** 以解决问题。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle插件兼容性问题 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**错误消息：** Android Gradle插件和Gradle的版本不兼容。

选择时显示错误消息 **构建APK** 选项来自 **生成** Android Studio用户界面上的菜单。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**分辨率：** 打开 **Gradle脚本** > **gradle-wrapper.properties** 文件并编辑 **distributionUrl** 属性。

例如，Android Studio控制台建议将Gradle版本降级为3.5。在中编辑版本 **distributionUrl**&#x200B;之&#x200B;**gradle-wrapper.properties** 文件。

选择 **生成** > **构建APK** 再次尝试解决该错误并生成.apk文件。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
