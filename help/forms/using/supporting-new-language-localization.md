---
title: 支持自适应表单本地化的新区域设置
seo-title: 支持自适应表单本地化的新区域设置
description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认情况下，支持的区域设置为英语、法语、德语和日语。
seo-description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认情况下，支持的区域设置为英语、法语、德语和日语。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 支持自适应表单本地化的新区域设置{#supporting-new-locales-for-adaptive-forms-localization}

## 关于区域设置词典 {#about-locale-dictionaries}

自适应表单的本地化依赖于两种类型的区域设置词典：

**表单特定词典** 包含自适应表单中使用的字符串。 例如，标签、字段名称、错误消息、帮助说明等。 它作为一组XLIFF文件管理，每个区域设置都可以访问它 `https://<host>:<port>/libs/cq/i18n/translator.html`。

**全局字典** AEM客户端库中有两个全局字典，管理为JSON对象。 这些词典包含默认错误消息、月名、货币符号、日期和时间模式等。 您可以在CRXDe Lite中找到这些字典，网址为/libs/fd/xfaforms/clientlibs/I18N。 这些位置为每个区域设置包含单独的文件夹。 由于全局字典通常不会频繁更新，因此保留每个区域设置的单独JavaScript文件使浏览器能够在访问同一服务器上的不同自适应表单时缓存它们并减少网络带宽使用。

### 自适应表单的本地化如何工作 {#how-localization-of-adaptive-form-works}

在渲染自适应表单时，它会通过按指定顺序查看以下参数来标识所请求的区域设置：

* 请求参 `afAcceptLang`数要覆盖用户的浏览器区域设置，可以传递请 `afAcceptLang` 求参数以强制使用区域设置。 例如，以下URL将强制在日语区域设置中呈现表单：
   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* 为用户设置的浏览器区域设置，使用标题在请求中指 `Accept-Language` 定。

* 在AEM中指定的用户的语言设置。

识别区域设置后，自适应表单会选取特定于表单的词典。 如果找不到所请求区域设置的表单特定词典，则使用英语(en)词典。

如果所请求区域设置的客户端库不存在，则它检查客户端库是否存在区域设置中的语言代码。 例如，如果请求的区域设置为 `en_ZA` （南非英语），并且不存在的客户端库，则自适应表单将使用客户端库（英语） `en_ZA``en` （如果存在）。 但是，如果这些表单都不存在，自适应表单将使用词典进行区 `en` 域设置。

## 添加对不支持的区域设置的本地化支持 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支持以下语言本地化自适应表单内容：英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语——巴西语(pt-BR)、中文(zh-CN)、中文——台湾语(zh-TW)和韩语(ko-KR)语言环境。

要在自适应表单运行时添加对新区域设置的支持，请执行以下操作：

1. [将区域设置添加到GuideLocalizationService服务](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [为区域设置添加XFA客户端库](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [为区域设置添加自适应表单客户端库](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [为词典添加区域设置支持](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新启动服务器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 向指南本地化服务添加区域设置 {#add-a-locale-to-the-guide-localization-service-br}

1. 转到 `https://'[server]:[port]'/system/console/configMgr`.
1. 单击以编辑“指 **南本地化服务** ”组件。
1. 将要添加的区域设置添加到支持的区域设置列表中。

![指南本地化服务](assets/configservice.png)

### 为区域设置添加XFA客户端库 {#add-xfa-client-library-for-a-locale-br}

创建一个类型为“ `cq:ClientLibraryFolder` 类别 `etc/<folderHierarchy>`”的节点，并 `xfaforms.I18N.<locale>`将以下文件添加到客户端库：

* **I18N.js** , `xfalib.locale.Strings` 定义 `<locale>` 中的定义 `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.txt** ，包含以下内容：

```
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 为区域设置添加自适应表单客户端库 {#add-adaptive-form-client-library-for-a-locale-br}

创建类型为以下的节 `cq:ClientLibraryFolder` 点，其 `etc/<folderHierarchy>`中类别为，依赖关系为 `guides.I18N.<locale>` 和， `xfaforms.3rdparty`且 `xfaforms.I18N.<locale>` 为 `guide.common`。&quot;

将以下文件添加到客户端库：

* **i18n.js** ，定义了具有“日历符号”、 `guidelib.i18n`、 `datePatterns`、 `timePatterns`、按XFA规范的模式的模式，在XSet SpecificationLocale中，以XFA规范中描述的XFA规范， `dateTimeSymbols``numberPatterns``numberSymbols``currencySymbols``typefaces``<locale>`[](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)以XFA规范的形式。 您还可以查看在中为其他支持的区域设置定义它的方式 `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`。
* **LogMessages.js** 定义 `guidelib.i18n.strings` 和 `guidelib.i18n.LogMessages` , `<locale>` 如中定义 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`。
* **js.txt** ，包含以下内容：

```
i18n.js
LogMessages.js
```

### 为词典添加区域设置支持 {#add-locale-support-for-the-dictionary-br}

仅当添加不在 `<locale>` 、、、、、、、 `en`、添加中 `de`、添加中时，才 `es`执行此步 `fr``it``pt-br``zh-cn``zh-tw``ja``ko-kr`骤。

1. 在下 `nt:unstructured` 创建一 `languages` 个节 `etc`点（如果尚不存在）。

1. 向节点添加多值字符串属 `languages` 性（如果尚不存在）。
1. 添加默 `<locale>` 认区域设 `de`置值、 `es`区域设置值、区域设置值、区域设 `fr`置值、区域设 `it``pt-br``zh-cn``zh-tw``ja``ko-kr`置值、区域设置值、区域设置值、区域设置值、区域设置值。

1. 添加 `<locale>` 到的属性 `languages` 的值 `/etc/languages`。

此时 `<locale>` 将显示在 `https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### Restart the server {#restart-the-server}

重新启动AEM服务器，使添加的区域设置生效。

## 用于添加对西班牙语支持的示例库 {#sample-libraries-for-adding-support-for-spanish}

用于添加西班牙语支持的示例客户端库

[获取文件](assets/sample.zip)
