---
title: AEM Forms应用程序疑难解答
seo-title: AEM Forms应用程序疑难解答
description: 了解AEM Forms应用程序的常见问题以及如何对它们进行疑难解答。
seo-description: 了解AEM Forms应用程序的常见问题以及如何对它们进行疑难解答。
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Forms应用程序疑难解答 {#troubleshoot-aem-forms-app}

本文介绍在构建AEM Forms应用程序时可能显示的错误消息以及解决这些错误消息的步骤。

本文中的部分包括：

* [iOS用户的附件丢失](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [由工作区用户提交的HTML5表单草稿在门户上不可见](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [HTML5表单（未缓存）无法在AEM Forms应用程序中加载](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms在Windows上不同步](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [不支持的Gradle版本](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Gradle和Android Gradle插件兼容性问题](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## iOS用户的附件丢失 {#attachment-loss-for-ios-users}

针对iOS的AEM Forms应用程序配置为与OSGi上的AEM Forms同步，仅支持字段级附件。 所有附件必须具有唯一的名称。 如果多个附件的名称相同，则只保留一个附件，而所有其他具有相同名称的附件将丢失。 执行以下步骤以防止iOS设备上的用户发生数据丢失：

1. 在连接的服务器上，导航到 **Adobe Experience Manager >工具>操作> Web Console**。
1. 查找并单击“自 **适应表单配置服务”**。
1. 在“自适应表单配置服务”对话框中，启用“ **使文件名唯一”**。

   如果 **禁用了“使文件名唯一** ”设置，则用户尝试提交具有多个附件的自适应表单时会丢失数据。

1. 单击&#x200B;**保存**。

## 由工作区用户提交的HTML5表单草稿在门户上不可见 {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

对于在AEM Forms应用程序中启用了“另存为草稿 **** HTML渲染配置文件”的HTML5表单，工作区用户不会看到保存的草稿。 要查看由门户上的工作区用户提交的HTML5表单的已保存草稿，请执行以下步骤：

1. 打开CRXDE并使用管理员凭据登录。

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. 在CRXDE的根路径中，在“访问控制”下的“访问控制列表”中，单击 **+**。
1. 在“添 **加新条目** ”对话框中，单击“主体”(Principal)字段中的组搜索按钮。
1. 在“选择主体”(Select Principal)对话框的“名称”(Name)字段中，键入并 `PERM_WORKSPACE_USER` 单击“搜 **索”(Search**)。
1. 在“选 `PERM_WORKSPACE_USER` 择主体”(Select Principal)对话框中选择组，然后单击“确 **定”(OK**)。
1. 在“添加新条目”对话框的“主 `PERM_WORKSPACE_USER` 体”(Principal)字段中，选择组。

   为用 `jcr:read` 户组启用权限。

1. 单击&#x200B;**确定**。

## HTML5表单（未缓存）无法在AEM Forms应用程序中加载 {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

当AEM Forms应用程序连接到旧版AEM Forms服务器时，未缓存的HTML5表单无法加载到AEM Forms应用程序中。

请执行以下步骤以解决此问题：

1. 在创作实例中，导航到 **Adobe Experience Manager >工具>配置Workspace App Offline Service >立即配置**。
1. 在“工 **作区应用程序脱机服务** ”页中，单击“ **手动资源缓存”**。

   URL:https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. 在“手 **动资源缓存** ”选项卡中，单击 **** +按钮以添加CRX路径。
1. 在添加 **新资源字段中** ，键入：/etc.clientlibs/fd/xfaforms/I18N/en_US.js，然后单击“ **添加**”。
1. 单击&#x200B;**保存**。

## AEM Forms在Windows上不同步 {#aem-forms-do-not-sync-on-windows}

在Windows上的AEM Forms应用程序中，如果表单的路径或其任何资源包含的字符大于或等于256个字符，则表单不会与连接的服务器同步。

修改表单的路径及其资源，将字符数减少到少于256个字符。

## 不支持的Gradle版本 {#unsupported-version-of-gradle}

**** 错误消息：项目使用的Gradle版本不受支持。

在Android studio中构建AEM Forms应用程序时，将显示错误消息。 此问题是由于系统上支持的Gradle版本不受支持而导致的。

**** 分辨率：单 **击“修复Gradle包装器”并重新导入项目** ，以解决此问题。

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Gradle和Android Gradle插件兼容性问题 {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** 错误消息：Android Gradle插件和Gradle的版本不兼容。

当您从Android studio用户界面的“构 **建”菜单中选择** “构建APK **** ”选项时，将显示错误消息。

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**** 分辨率：打 **开Gradle Scripts** > **gradle-wrapper.properties文件并编辑** distributionUrl **** 属性。

例如，Android studio控制台建议将Gradle版本降级为3.5。编辑gradle-wrapper. **properties文**&#x200B;件的&#x200B;**distributionUrl中的版本** 。

再次 **选择“构** 建 **”>“构建APK** ”以解决错误并生成。apk文件。

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

