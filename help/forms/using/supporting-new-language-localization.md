---
title: 支持自适应表单本地化的新区域设置
seo-title: 支持自适应表单本地化的新区域设置
description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认支持的区域设置为英语、法语、德语和日语。
seo-description: AEM Forms允许您为本地化自适应表单添加新区域设置。 默认支持的区域设置为英语、法语、德语和日语。
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
feature: 自适应表单
role: Admin
exl-id: 2ed4d99e-0e90-4b21-ac17-aa6707a3ba7d
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 支持自适应表单本地化的新区域设置{#supporting-new-locales-for-adaptive-forms-localization}

## 关于区域设置字典 {#about-locale-dictionaries}

自适应表单的本地化依赖于两种类型的区域设置字典：

**表单特定词典** 包含自适应表单中使用的字符串。例如，标签、字段名称、错误消息、帮助描述等。 它作为每个区域设置的一组XLIFF文件进行管理，您可以在`https://<host>:<port>/libs/cq/i18n/translator.html`访问它。

**全局** 字典在AEM客户端库中有两个全局字典，管理为JSON对象。这些字典包含默认错误消息、月名、货币符号、日期和时间模式等。 您可以在CRXDe Lite的/libs/fd/xfaforms/clientlibs/I18N中找到这些字典。 这些位置包含每个区域设置的单独文件夹。 由于全局字典通常不经常更新，因此为每个区域设置保留单独的JavaScript文件使浏览器能够在访问同一服务器上的不同自适应表单时缓存它们并减少网络带宽使用。

### 自适应表单的本地化工作原理 {#how-localization-of-adaptive-form-works}

有两种方法可识别自适应表单的区域设置。 呈现自适应表单后，它会通过标识所请求的区域设置：

* 查看自适应表单URL中的`[local]`选择器。 URL的格式为`http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`。 使用`[local]`选择器可缓存自适应表单。

* 按指定顺序查看以下参数：

   * 请求参数`afAcceptLang`
要覆盖用户的浏览器区域设置，您可以通过 
`afAcceptLang` 请求参数强制设置区域。例如，以下URL将强制在日语区域设置中渲染表单：
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * 为用户设置的浏览器区域设置，在请求中使用`Accept-Language`标头指定。

   * 在AEM中指定的用户的语言设置。

   * 默认情况下，浏览器区域设置处于启用状态。 要更改浏览器区域设置，请
      * 打开配置管理器。 URL为`http://[server]:[port]/system/console/configMgr`
      * 找到并打开&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道]**&#x200B;配置。
      * 更改&#x200B;**[!UICONTROL 使用浏览器区域设置]**&#x200B;选项和&#x200B;**[!UICONTROL 保存]**&#x200B;配置的状态。

识别区域设置后，自适应表单会选取特定于表单的词典。 如果找不到所请求区域设置的特定于表单的词典，则该词典会使用该词典来编写自适应表单的语言。

如果不存在区域设置信息，则使用表单的原始语言提交自适应表单。 原始语言是开发自适应表单时使用的语言。

如果所请求区域设置的客户端库不存在，则它会检查客户端库是否存在区域设置中存在的语言代码。 例如，如果请求的区域设置为`en_ZA`（南非英语），并且`en_ZA`的客户端库不存在，则自适应表单将使用客户端库（如果存在）来表示`en`（英语）语言。 但是，如果其中不存在，则自适应表单会使用字典进行`en`区域设置。

## 为不支持的区域设置添加本地化支持 {#add-localization-support-for-non-supported-locales}

AEM Forms目前支持以英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中国 — 台湾语(zh-TW)和韩语(ko-KR)区域设置本地化自适应表单内容。

要在自适应表单运行时添加对新区域设置的支持，请执行以下操作：

1. [向GuideLocalizationService服务添加区域设置](../../forms/using/supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [为区域设置添加XFA客户端库](../../forms/using/supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [为区域设置添加自适应表单客户端库](../../forms/using/supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [为词典添加区域设置支持](../../forms/using/supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [重新启动服务器](../../forms/using/supporting-new-language-localization.md#p-restart-the-server-p)

### 向指南本地化服务中添加区域设置 {#add-a-locale-to-the-guide-localization-service-br}

1. 转到 `https://'[server]:[port]'/system/console/configMgr`.
1. 单击以编辑&#x200B;**Guide Localization Service**&#x200B;组件。
1. 将要添加的区域设置添加到支持区域设置列表。

![指南本地化服务](assets/configservice.png)

### 为区域设置添加XFA客户端库 {#add-xfa-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`下创建类型为`cq:ClientLibraryFolder`的节点（具有类别`xfaforms.I18N.<locale>`），并将以下文件添加到客户端库：

* **I18N.js** 定义 `xfalib.locale.Strings` 的 `<locale>` 内容（如中定义） `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`。

* **js.** txt包含以下内容：

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### 为区域设置添加自适应表单客户端库 {#add-adaptive-form-client-library-for-a-locale-br}

在`etc/<folderHierarchy>`下创建类型为`cq:ClientLibraryFolder`的节点，类别为`guides.I18N.<locale>`，依赖项为`xfaforms.3rdparty`、`xfaforms.I18N.<locale>`和`guide.common`。 &quot;

将以下文件添加到客户端库：

* **i18n.** jsdefining `guidelib.i18n`，具有“calendarSymbols”、 `datePatterns`、 `timePatterns`、 `dateTimeSymbols`、 `numberPatterns`、 `numberSymbols` `currencySymbols`、 `typefaces` 的模式(如 `<locale>` 区域设置集规范 [](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf)中所述的XFA规范)。您还可以在`/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`中查看如何为其他支持的区域设置定义该区域设置。
* **LogMessages.** js `guidelib.i18n.strings` 定 `guidelib.i18n.LogMessages` 义和 `<locale>` (在中定 `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`义)。
* **js.** txt包含以下内容：

```text
i18n.js
LogMessages.js
```

### 为词典添加区域设置支持 {#add-locale-support-for-the-dictionary-br}

仅当您添加的`<locale>`不在`en`、`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`之间时，才执行此步骤。

1. 在`etc`下创建`nt:unstructured`节点`languages`（如果尚未创建）。

1. 将多值字符串属性`languages`添加到节点（如果不存在）。
1. 添加`<locale>`默认区域设置值`de`、`es`、`fr`、`it`、`pt-br`、`zh-cn`、`zh-tw`、`ja`、`ko-kr`（如果尚不存在）。

1. 将`<locale>`添加到`/etc/languages`的`languages`属性的值中。

`<locale>`将显示在`https://'[server]:[port]'/libs/cq/i18n/translator.html`。

### 重新启动服务器 {#restart-the-server}

重新启动AEM服务器，使添加的区域设置生效。

## 添加对西班牙语支持的示例库 {#sample-libraries-for-adding-support-for-spanish}

用于添加对西班牙语支持的示例客户端库

[获取文件](assets/sample.zip)
