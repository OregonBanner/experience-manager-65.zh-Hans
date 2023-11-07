---
title: 使用Translator管理词典
description: AEM提供了一个控制台，用于管理组件UI中使用的文本的各种翻译
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2320'
ht-degree: 1%

---

# 使用Translator管理词典{#using-translator-to-manage-dictionaries}

AEM提供了一个控制台，用于管理组件UI中使用的文本的各种翻译。 此控制台位于

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

使用翻译工具管理英语字符串及其翻译。 词典在存储库中创建，例如/apps/myproject/i18n。

您管理的翻译工具及词典用于以不同语言呈现组件UI。 如果要翻译页面或用户生成的内容，请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md) 和 [用户生成的内容的翻译](/help/communities/translate-ugc.md).

>[!CAUTION]
>
>仅编辑为项目创建并位于下的词典 `/apps`.
>
>此工具中还提供了AEM系统词典。 请勿更改AEM系统词典，因为这会导致AEM UI出现问题。 此外，升级时可能会丢失更改。 AEM系统词典位于 `/libs`.

>[!NOTE]
>
>虽然Translator工具具有经典的UI界面，但它用于翻译短语，而不管这些短语位于哪个界面上。

翻译人员列出了AEM中使用的文本，以及各种语言翻译：

![chlimage_1-205](assets/chlimage_1-205.png)

您可以搜索、筛选和编辑英语和已翻译文本。 您还可以将词典导出为XLIFF格式进行翻译，然后将翻译导入回词典中。

也可以从此控制台将i18n词典添加到翻译项目。 您可以创建一个项目或将其添加到现有项目中。

1. 单击 **翻译字典**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 根据需要选择创建或添加选项。 这将打开一个对话框。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 填写必填字段，然后单击“确定”。 ![chlimage_1-208](assets/chlimage_1-208.png)

1. 您现在可以单击 **确定** 或者参阅目标词典。

   >[!NOTE]
   >
   >有关翻译项目的更多信息，请阅读 [管理翻译项目](/help/sites-administering/tc-manage.md).

## 创建词典 {#creating-a-dictionary}

创建词典以管理本地化的UI字符串。 创建词典后，您可以使用翻译工具对其进行管理。

1. 使用CRXDE Lite，添加根节点( `sling:Folder`)作为保存语言定义的结构：

   ` /apps/<projectName>/i18n`

   例如，`/apps/myProject/i18n`

1. 在此根下添加所需的语言结构。 例如：

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >这是来自 [Sling i18n模块](https://sling.apache.org/site/internationalization-support.html).

1. 重新加载翻译器和词典路径(例如， `/apps/myProject/i18n`)将显示在工具栏的下拉选择器中。 选择此项以开始添加字符串及其翻译。

   >[!NOTE]
   >
   >翻译人员将仅保存路径下实际存在的语言的翻译(例如， `/apps/myProject/i18n`)。
   >
   >确保这些语言与网格中显示的语言对应。

## 管理字典字符串 {#managing-dictionary-strings}

使用翻译工具管理词典中的字符串。 您可以添加、修改和删除英文字符串，还可以提供翻译后的字符串。

>[!CAUTION]
>
>仅编辑为项目创建并位于下的词典 `/apps`.
>
>请勿更改AEM系统词典，因为这会导致AEM UI出现问题。 此外，升级时可能会丢失更改。 AEM系统词典位于 `/libs`.

### 添加、更改和删除字符串 {#adding-changing-and-removing-strings}

将英语字符串添加到组件已国际化的词典中。 仅添加国际化字符串，以便您不会通过翻译未使用的字符串而浪费资源。

添加到字典的字符串必须与代码中指定的字符串完全匹配。 如果代码中使用的默认英文字符串与词典中的英文字符串不匹配，则在需要时，翻译后的字符串不会出现在UI中。 字符串区分大小写。

**提供翻译提示**

使用词典字符串的Commenet属性向翻译人员提供信息以阐明字符串的含义。 通常，UI会帮助用户确定模糊单词的含义。 但是，翻译人员不会在UI的上下文中看到字符串。 翻译提示可消除歧义。 例如，注释可帮助翻译人员了解英语单词Request用作名词而不是动词。

翻译提示还可以区分相同且具有不同含义的字符串。 例如，Search一词可以是名词或动词，在词典中需要两个“Search”条目，并带有两个不同的翻译提示。 请求字符串的代码还包括翻译提示，以便在UI中使用正确的字符串。

**包括索引变量**

在本地化字符串中包含变量以将上下文含义构建到句子中。 例如，在登录到Web应用程序后，主页显示消息“欢迎返回管理员”。 您的收件箱中有2封邮件。” 页面上下文确定用户名和消息数。

要在本地化的字符串中包含变量，请将带括号的索引放置在get方法第一个参数中的变量位置。 使用本地化提示描述这些值。 翻译人员必须理解变量的含义，因为不同的语言使用不同的句子结构。

请注意 [请求已翻译字符串的代码](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) 根据上下文提供索引变量的值。

例如，当用户登录到网站并包含在词典中时，将显示以下字符串：

`Welcome back {0}. You have {1} messages.`

以下注释描述了变量：

`{0} = the user name, {1} = the number of items in the user's inbox`

**修改字符串**

在代码中更改或删除英文字符串时，更改或删除英文字符串。 更改字符串时，将保留原始字符串并生成一个反映更改的新字符串。 在删除字符串之前，请确保没有代码使用它。

使用以下过程可添加字符串。

1. 在“词典”下拉菜单中，选择要向其添加字符串的词典。 在下拉菜单中，词典在存储库中由其路径表示。
1. 在“字符串和翻译”表的上方，单击“添加”。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 在“添加字符串”对话框的“字符串”框中，键入英文字符串。 在“注释”框中，根据需要键入翻译器的翻译提示。
1. 单击确定。
1. 单击保存。

   ![chlimage_1-210](assets/chlimage_1-210.png)

使用以下过程可更改词典中的字符串。

1. 在“词典”下拉菜单中，选择包含要更改的字符串的词典。
1. 双击要更改的字符串。
1. 在“编辑字符串”对话框中，选择“修改字符串”或“注释”（创建副本）。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 修改字符串或注释，然后单击“确定”。
1. 单击保存。

   ![chlimage_1-212](assets/chlimage_1-212.png)

使用以下过程可从词典中删除字符串。

1. 在“词典”下拉菜单中，选择要从中删除字符串的词典。
1. 单击删除。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 单击保存。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 搜索字符串 {#searching-for-strings}

Translator工具底部的搜索栏提供了字符串选择选项：

* **按文本过滤：** 与英语字符串、注释或翻译匹配的模式。 只有与全部或部分阵列匹配的项才会出现在表中。
* **更改：任何、已修改、新建、已删除：** 显示已更改但未保存的项目。

   * 任意：显示已修改、添加或删除的项目。
   * 已修改：显示已更改的项目。
   * 新增：显示已添加的项目。
   * 已删除：显示要删除的项目。
   * 多项选择：显示具有所有选定属性的项目。

* **具有评论**：显示包含翻译人员注释的项目。
* **缺少翻译：** 显示至少有一种语言没有翻译的项目。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 在搜索栏上，选择筛选选项。
1. 要使用选项进行筛选，请单击“筛选”。
1. 要删除筛选器并查看词典中的所有项目，请单击“清除”。

### 编辑翻译的字符串 {#editing-translated-strings}

将英文字符串添加到词典后，可以添加该字符串的翻译。 您还可以 [导出词典](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) 由第三方翻译。

1. 选择 [您的项目特定词典](#creating-a-dictionary) 因为它指定存储库中保存翻译的路径。 例如，选择 **词典** 作为：

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >仅编辑为项目创建并位于下的词典 `/apps`.
   >
   >此工具中还提供了AEM系统词典。 请勿更改AEM系统词典，因为这会导致AEM UI出现问题。 此外，升级时可能会丢失更改。 AEM系统词典位于 `/libs`.

1. 要编辑其中一个字符串的翻译文本，您可以：

   * 双击所需字符串的相应语言以编辑该单个文本：

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 双击 **字符串** 或 **注释** 字段作为打开 **编辑字符串** 对话框，根据需要编辑翻译，然后单击 **确定** 要关闭对话框，请执行以下操作：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 单击 **保存** 以提交更改。

   >[!NOTE]
   >
   >单击 **重置和刷新** (而不是 **保存**)还原对先前文本的任何更改。

## 使用第三方翻译人员 {#using-third-party-translators}

为了支持使用第三方翻译服务，翻译工具允许您导出和导入词典。

### 导出词典 {#exporting-a-dictionary}

将词典导出到XLIFF文件，以便第三方服务可以翻译词典字符串。

* 导出词典，并包含英语和一种语言的翻译术语。
* 仅导出部分或全部英文字符串。

导出XLIFF文件并包含语言时，存储库中词典的节点结构必须包含该语言。 如果未包含语言，则会发生错误。 例如，要导出法语XLIFF文件，词典文件夹必须包括 `mix:language` 子节点已命名 `fr`. (请参阅 [创建词典](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

使用以下过程可导出特定语言的XLIFF文件。

1. 打开翻译工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用词典下拉菜单选择要导出的词典。
1. 单击“导出”>“完全导出” *XX* Xliff选项，其中 *XX* 是双字母语言代码，如DE或FR。

   XLIFF文件将在新选项卡或窗口中打开。

1. 使用Web浏览器命令将页面另存为文件系统中的文件，如“文件”>“另存为页面”。

使用以下过程可导出全部或部分英文字符串。

1. 打开翻译工具。 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用词典下拉菜单选择要导出的词典。
1. 如果要导出字符串的子集，请在词典中选择要导出的项目。 选择“无项目”将导出所有项目。
1. 单击“导出”>“将所选内容导出为Xliff”（仅限字符串）。
1. 在出现的对话框中，复制文本并将其粘贴到文本文件中。

### 导入词典 {#importing-a-dictionary}

将XLIFF文件导入词典以填充词典。 当词典包含英语字符串的翻译，并且XLIFF文件包含同一字符串的不同翻译时，词典翻译将被替换。

1. 打开翻译工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 单击“导入”>“XLIFF翻译”。
1. 选择要导入的文件，然后单击“确定”。

## 管理支持的语言 {#managing-supported-lanuages}

添加或删除翻译工具支持的语言以及向网页用户提供的语言。

### 更改字典表中列出的语言 {#changing-languages-listed-in-the-dictionary-table}

翻译工具在词典表中包含以下语言：

* de — 德语
* fr — 法语
* it — 意大利语
* es — 西班牙语
* ja — 日语
* pt-br — 巴西葡萄牙语
* zh-cn — 简体中文
* zh-tw — 繁体中文（有限支持）
* ko-kr — 韩语

使用以下过程添加或删除语言。

1. 使用CRXDE Lite创建节点：

   `/etc/languages`

1. 在此节点上，创建一个属性：

   * **名称**：`languages`
   * **类型**：`Multi-String`
   * **值**：要显示的语言列表。 例如：

      * fr
      * es

   >[!NOTE]
   >
   >语言代码必须为小写。

1. 单击 **全部保存** CRXDE Lite并重新加载转换器。 网格将更新以显示定义的语言。

   >[!NOTE]
   >
   >翻译人员将只保存实际语言的翻译 [在字典中呈现](#creating-a-dictionary) (即，在词典路径下，例如 `/apps/myProject/i18n`)。
   >
   >确保这些语言与网格中显示的语言对应。

### 使语言对作者可用 {#making-languages-available-to-authors}

在为AEM实例的新语言定义词典后，您需要使其可供作者选择(例如，用于 **偏好设置**)：

1. 要更改中可用的语言列表，请执行以下操作 **偏好设置** 的 **安全性** 控制台：

   1. 在应用程序代码中创建覆盖以用于：

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. 若要使该语言可用于 **偏好设置** 从 **网站** 控制台。您需要在应用程序中进行以下更改：

   1. 为下面的结构创建叠加：

      `/libs/cq/security/content/tools/userProperties`

   1. 在覆盖内更新下的语言列表：

      `items/common/items /lang/options`

1. 保存所有内容并重新加载相应的控制台。

### 更改语言名称和默认国家/地区 {#changing-language-names-and-default-countries}

不同的国家使用相同的语言，例如，美国、英国和澳大利亚都使用英语。 这由指示语言和国家/地区的代码指示，例如 `en_US`， `en_GB` 和 `en_AU`.

显示标记时使用默认国家/地区（例如，在语言复制对话框中），它们用于解析语言代码的国家/地区。

>[!NOTE]
>
>对于由上述翻译员管理的本地化，只有完全相同的语言才有效。 如果语言首选项下拉列表使用 `en_uk`，必须有 `en_uk` 词典中的词典。

要更改默认定义，请执行以下操作：

1. 语言列表存储在以下位置：

   `/libs/wcm/core/resources/languages`

   复制此项至以下位置，以将其覆盖：

   `/apps/wcm/core/resources/languages`

   然后在那里更改或扩展列表。 属性 `defaultCountry` 在语言节点上(例如， `ja`)必须包含完整代码，例如 `ja_jp`，它们将定义 `jp` 作为语言的默认国家/地区 `ja`.

1. 更新 **CQ WCM语言管理器**.

   * **语言列表**：

     存储库中语言列表的路径。 将其设置为用于叠加的位置：

     ```
            /apps/wcm/core/resources/languages
     ```

   您可以使用OSGi Web控制台执行此操作：

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 发布词典 {#publishing-dictionaries}

将您的字典合并到AEM应用程序的发行管理流程中。 例如，将字典包含在应用程序的内容包中，以部署到发布实例。 此策略具有以下优势：

* 字典可用于其发布环境中的组件。
* 对组件UI字符串所做的更改将随更新的翻译一起部署。

同样，词典字符串的测试应该作为正常软件开发生命周期的一部分来执行。

>[!NOTE]
>
>请勿对字典使用常规发布功能或复制。 相反，应按处理代码和配置的方式处理词典。 这包括使用源代码管理来跟踪更改，以及使用内容包将更改应用于创作和发布。

>[!NOTE]
>
>使用Dispatcher时，您需要 [使缓存的页面失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) 在渲染的组件字符串中包含新词典字符串。
