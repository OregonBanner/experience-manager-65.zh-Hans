---
title: 支持自适应表单本地化的新语言环境
seo-title: 支持自适应表单本地化的新语言环境
description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认情况下，支持的语言环境为英语、法语、德语和日语。
seo-description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认情况下，支持的语言环境为英语、法语、德语和日语。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 1a4bfc91cf91b4b56cc4efa99f60575ac1a9a549
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# 支持自适应表单本地化的新语言环境{#supporting-new-locales-for-adaptive-forms-localization}

## 关于区域设置词典 {#about-locale-dictionaries}

自适应表单的本地化依赖于两种类型的区域设置词典：

**表单特定词典** 包含自适应表单中使用的字符串。 例如，标签、字段名称、错误消息、帮助说明等。 它作为一组XLIFF文件管理，适用于每个区域设置，您可以在访问 `https://<host>:<port>/libs/cq/i18n/translator.html`。

**全局字典** AEM客户端库中有两个全局字典，管理为JSON对象。 这些词典包含默认错误消息、月名、货币符号、日期和时间模式等。 您可以在CRXDe Lite中找到这些字典，地址为/libs/fd/xfaforms/clientlibs/I18N。 这些位置为每个区域设置包含单独的文件夹。 由于全局字典通常不经常更新，因此为每个区域设置保留单独的JavaScript文件使浏览器能够在同一服务器上访问不同的自适应表单时缓存它们并减少网络带宽使用。

### 自适应表单的本地化如何工作 {#how-localization-of-adaptive-form-works}

有两种方法可标识自适应表单的区域设置。 呈现自适应表单时，它通过以下方式标识所请求的区域设置：

* 查看自适应 `[local]` 表单URL中的选择器。 The format of the URL is `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. 使用选 `[local]` 择器可缓存自适应表单。

* 按指定顺序查看以下参数：

   * 请求参 `afAcceptLang`数要覆盖用户的浏览器区域设置，您可以通过 
`afAcceptLang` 请求参数以强制使用区域设置。 例如，以下URL将强制在日语区域设置中呈现表单：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 为用户设置的浏览器区域设置，使用标题在请求中指 `Accept-Language` 定。

   * AEM中指定用户的语言设置。

   * 默认情况下，浏览器区域设置处于启用状态。 要更改浏览器区域设置，
      * 打开配置管理器。 URL为 `http://[server]:[port]/system/console/configMgr`
      * 找到并打开自 **[!UICONTROL 适应表单和交互式通信Web渠道配置]** 。
      * 更改“使用浏览器 **[!UICONTROL 区域设置]** ”选项的 **[!UICONTROL 状态并保]** 存配置。

识别区域设置后，自适应表单会选取特定于表单的词典。 如果找不到所请求区域设置的特定于表单的词典，则它将该词典用于创作自适应表单的语言。

如果没有区域设置信息，则以表单的原始语言提供自适应表单。 原始语言是开发自适应表单时使用的语言。

如果所请求区域设置的客户端库不存在，则它检查客户端库是否存在区域设置中的语言代码。 例如，如果请求的区域设 `en_ZA` 置为（南非英语），并且不存在 `en_ZA` 客户端库，自适应表单将使用客户端库( `en` 英语)语言（如果存在）。 但是，如果这些表单都不存在，自适应表单将字典用于区 `en` 域设置。

## 添加对不支持的区域设置的本地化支持 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支持本地化适应表单内容，语言版本有英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、巴西葡萄牙语(pt-BR)、中文(zh-CN)、中国台湾(zh-TW)和韩语(ko-KR)。

要在自适应表单运行时添加对新区域设置的支持，请执行以下操作：

1. [向GuideLocalizationService服务添加区域设置](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [为区域设置添加XFA客户端库](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [为区域设置添加自适应表单客户端库](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [为词典添加区域设置支持](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新启动服务器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 向指南本地化服务添加区域设置 {#add-a-locale-to-the-guide-localization-service-br}

1. 转到 `https://'[server]:[port]'/system/console/configMgr`.
1. 单击以编辑指 **南本地化服务** 组件。
1. 将要添加的区域设置添加到支持的区域设置列表。

![指南本地化服务](assets/configservice.png)

### 为区域设置添加XFA客户端库 {#add-xfa-client-library-for-a-locale-br}

创建带有类别的 `cq:ClientLibraryFolder` 类 `etc/<folderHierarchy>`型节点， `xfaforms.I18N.<locale>`并将以下文件添加到客户端库：

* **I18N.js** , `xfalib.locale.Strings` 定义 `<locale>` 中的定义 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.txt** ，包含以下内容：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 为区域设置添加自适应表单客户端库 {#add-adaptive-form-client-library-for-a-locale-br}

创建以下类型 `cq:ClientLibraryFolder` 的节 `etc/<folderHierarchy>`点，其类别 `guides.I18N.<locale>` 为和依赖项 `xfaforms.3rdparty`为 `xfaforms.I18N.<locale>` 和 `guide.common`。&quot;

将以下文件添加到客户端库：

* **i18n.js定义** ，具有“ `guidelib.i18n`calendarSymbols”、、、、 `datePatterns`、 `timePatterns`、按XFA规范的模式(在地区设置XFA规范中 `dateTimeSymbols``numberPatterns``numberSymbols``currencySymbols``typefaces``<locale>`[](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf))、XFA规范中描述的模式。 您还可以在中了解如何为其他支持的语言环境定义该 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`语言。
* **LogMessages.js** 定 `guidelib.i18n.strings` 义 `guidelib.i18n.LogMessages` 和(如 `<locale>` 中定义) `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。
* **js.txt** ，包含以下内容：

```text
i18n.js
LogMessages.js
```

### 为词典添加区域设置支持 {#add-locale-support-for-the-dictionary-br}

仅当您添加的内容 `<locale>` 不在以下范围之 `en`中时， `de`才执行此步 `es`骤：添加、 `fr`、、、 `it`、、 `pt-br`、、 `zh-cn``zh-tw``ja``ko-kr`、、、、

1. 在下 `nt:unstructured` 创建 `languages` 一个节 `etc`点（如果尚不存在）。

1. 向节点添加多值字 `languages` 符串属性（如果尚不存在）。
1. 添加默 `<locale>` 认的区 `de`域设置 `es`、 `fr`、 `it`、、 `pt-br`、 `zh-cn``zh-tw``ja``ko-kr`（如果尚不存在）。

1. 添加 `<locale>` 到属性的 `languages` 值中 `/etc/languages`。

将 `<locale>` 出现在 `https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### Restart the server {#restart-the-server}

重新启动AEM服务器，使添加的区域设置生效。

## 添加西班牙语支持的示例库 {#sample-libraries-for-adding-support-for-spanish}

用于添加对西班牙语支持的示例客户端库

[获取文件](assets/sample.zip)
