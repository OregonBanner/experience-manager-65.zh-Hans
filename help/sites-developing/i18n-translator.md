---
title: 使用翻译器管理词典
seo-title: 使用翻译器管理词典
description: AEM提供一个控制台，用于管理组件UI中使用的文本的各种翻译
seo-description: AEM提供一个控制台，用于管理组件UI中使用的文本的各种翻译
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用翻译器管理词典{#using-translator-to-manage-dictionaries}

AEM提供一个控制台，用于管理组件UI中使用的文本的各种翻译。 此控制台位于

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

使用翻译工具管理英语字符串及其翻译。 字典在存储库中创建，例如/apps/myproject/i18n。

请注意，翻译工具和您管理的词典用于以不同语言显示组件UI。 如果要翻译页面或用户生成的内容，请参阅 [翻译多语言站点的内容](/help/sites-administering/translation.md)[和翻译用户生成的内容](/help/communities/translate-ugc.md)。

>[!CAUTION]
>
>仅编辑为项目创建并位于下面的词典 `/apps`。
>
>AEM系统词典也在此工具中可用。 请勿更改AEM系统词典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统词典位于下 `/libs`方。

>[!NOTE]
>
>尽管“翻译器”工具有经典UI界面，但它用于翻译短语，而不管在哪个界面中找到这些短语。

翻译器将AEM中使用的文本与各种语言翻译并列：

![chlimage_1-205](assets/chlimage_1-205.png)

您可以搜索、过滤和编辑英语文本和译文。 您还可以将词典导出为XLIFF格式进行翻译，然后将翻译导回词典。

还可以从此控制台将i18n词典添加到翻译项目。 您可以创建新项目或添加到现有项目。

1. 单击“ **翻译词典**”。

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 根据需要选择创建或添加选项。 此时将打开一个对话框。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 根据需要填写字段，然后单击“确定”。 ![chlimage_1-208](assets/chlimage_1-208.png)

1. 您现在可以单击“ **确定** ”或查看Target词典。

   >[!NOTE]
   >
   >有关翻译项目的更多信息，请阅读管 [理翻译项目](/help/sites-administering/tc-manage.md)。

## 创建词典 {#creating-a-dictionary}

创建用于管理本地化的UI字符串的词典。 创建词典后，可以使用翻译工具管理该词典。

1. 使用CRXDE Lite，为新词典添加根节点( `sling:Folder`)作为包含语言定义的结构：

   ` /apps/<projectName>/i18n`

   For example, `/apps/myProject/i18n`

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
   >这是Sling i18n模块 [的结构](https://sling.apache.org/site/internationalization-support.html)。

1. 重新加载翻译器和词典路径(例如，) `/apps/myProject/i18n`将在工具栏的下拉选择器中可用。 选择此选项可开始添加字符串及其翻译。

   >[!NOTE]
   >
   >翻译器将仅保存路径下实际存在的语言的翻译(例如， `/apps/myProject/i18n`)。
   >
   >确保这些语言与网格中显示的语言相对应。

## 管理词典字符串 {#managing-dictionary-strings}

使用翻译工具管理词典中的字符串。 您可以添加、修改和删除英语字符串，并提供译文字符串。

>[!CAUTION]
>
>仅编辑为项目创建并位于下面的词典 `/apps`。
>
>请勿更改AEM系统词典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统词典位于下 `/libs`方。

### 添加、更改和删除字符串 {#adding-changing-and-removing-strings}

将英文字符串添加到组件已国际化的词典。 只添加国际化字符串，这样您就不会通过翻译未使用的字符串来浪费资源。

您添加到词典的字符串必须与在代码中指定的字符串完全匹配。 如果代码中使用的默认英语字符串与词典中的英语字符串不匹配，则在需要时，译文的字符串不会显示在UI中。 字符串区分大小写。

**提供翻译提示**

使用字典字符串的Comment属性向翻译者提供信息以阐明字符串的含义。 通常，UI会帮助用户确定含糊词的含义。 但是，翻译器在UI的上下文中看不到该字符串。 翻译提示可消除歧义。 例如，注释有助于翻译者理解英语单词“请求”是用作名词而不是动词。

翻译提示还可区分相同且含义不同的字符串。 例如，单词“搜索”可以是名词或动词，它要求词典中有两个带有两个不同翻译提示的“搜索”条目。 请求字符串的代码还包括翻译提示，以便在UI中使用正确的字符串。

**包括索引变量**

将变量包含在本地化字符串中，以便在句子中构建上下文含义。 例如，登录Web应用程序后，主页显示消息“欢迎返回管理员”。 收件箱中有2条邮件。” 页面上下文决定用户名和消息数。

要在本地化字符串中包含变量，请将括号内的索引放在get方法第一个参数中变量的位置。 使用本地化提示描述这些值。 翻译者必须理解变量的含义，因为不同的语言使用不同的句子结构。

请注意， [请求已翻译字符串的代码](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) ，会根据上下文为索引变量提供值。

例如，当用户登录到网站时，下面的字符串会显示在词典中：

`Welcome back {0}. You have {1} messages.`

以下评论描述了变量：

`{0} = the user name, {1} = the number of items in the user's inbox`

**修改字符串**

在代码中更改或删除英文字符串时，更改或删除这些字符串。 当您更改字符串时，原始字符串会被保留，并会生成反映该更改的新字符串。 在删除字符串之前，请确保没有代码使用它。

请按照以下过程添加字符串。

1. 在“词典”下拉菜单中，选择要向其添加字符串的词典。 在下拉菜单中，词典由其在存储库中的路径表示。
1. 在“字符串和翻译”表上方，单击“添加”。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 在“添加字符串”对话框的“字符串”框中，键入英文字符串。 在“注释”框中，根据需要键入翻译者的翻译提示。
1. 单击“确定”。
1. 单击保存。

   ![chlimage_1-210](assets/chlimage_1-210.png)

请按照以下过程更改词典中的字符串。

1. 在“词典”下拉菜单中，选择包含要更改的字符串的词典。
1. 双击要更改的字符串。
1. 在“编辑字符串”对话框中，选择“修改字符串”或“注释（创建副本）”。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 修改字符串或注释，然后单击“确定”。
1. 单击保存。

   ![chlimage_1-212](assets/chlimage_1-212.png)

请按照以下过程从词典中删除字符串。

1. 在“词典”下拉菜单中，选择要从中删除字符串的词典。
1. 单击删除。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 单击保存。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 搜索字符串 {#searching-for-strings}

“翻译器”工具底部的搜索栏提供了字符串选择选项：

* **** 按文本过滤：与英文字符串、注释或翻译匹配的模式。 表中只显示与图案的全部或部分匹配的项目。
* **** 更改：“任意”、“已修改”、“新建”、“已删除”:显示已更改且未保存的项目。

   * 任意：显示已修改、添加或删除的项目。
   * 修改时间：显示已更改的项目。
   * 新：显示添加的项目。
   * 已删除：显示要删除的项目。
   * 多项选择：显示具有所有选定属性的项目。

* **评论**:显示具有翻译员注释的项目。
* **** 缺少翻译：显示至少一种语言没有翻译的项目。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 在搜索栏中，选择筛选选项。
1. 要使用选项进行筛选，请单击筛选。
1. 要删除过滤器并查看词典中的所有项目，请单击“清除”。

### 编辑译文字符串 {#editing-translated-strings}

在将英文字符串添加到词典后，可以添加该字符串的翻译。 您还可以 [导出词典](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) ，以便让第三方翻译该词典。

1. 选择 [您的项目特定词典](#creating-a-dictionary) ，因为该词典指定了包含翻译的存储库中的路径。 例如，选择 **词典** :

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >仅编辑为项目创建并位于下面的词典 `/apps`。
   >
   >AEM系统词典也在此工具中可用。 请勿更改AEM系统词典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统词典位于下 `/libs`方。

1. 要编辑某个字符串的译文，您可以：

   * 双击所需字符串的相应语言以编辑该文本：
   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 双击所需字符串的 **字符串** 或注释字段以打开 **Edit string** （编辑字符串）对话框，根据需要编辑翻译，然后单击 ******** OKAdrobe关闭对话框：
   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 单击 **工具栏中的** “保存”以提交更改。

   >[!NOTE]
   >
   >单击“重 **置并刷新** ”(而非“保 **存”**)可还原对先前文本所做的任何更改。

## 使用第三方翻译人员 {#using-third-party-translators}

为了支持使用第三方翻译服务，翻译工具允许您导出和导入词典。

### 导出词典 {#exporting-a-dictionary}

将词典导出到XLIFF文件，以便第三方服务能够翻译词典字符串。

* 导出词典并包含某种语言的英语和译文术语。
* 导出部分或全部英文字符串。

导出XLIFF文件并包含语言时，存储库中词典的节点结构必须包含该语言。 如果未包含该语言，则会出错。 例如，要导出法语XLIFF文件，词典文件夹必须包含名为的 `mix:language` 子节点 `fr`。 (请参 [阅创建词典](/help/sites-developing/i18n-translator.md#creating-a-dictionary)。)

请按照以下过程导出特定语言的XLIFF文件。

1. 打开翻译工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用“词典”下拉菜单选择要导出的词典。
1. 单击“导出”>“ *Export Full* XX Xliff选项”，其中 *XX* 是双字母语言代码，如DE或FR。

   XLIFF文件在新选项卡或窗口中打开。

1. 使用Web浏览器命令将页面另存为文件，如“文件”>“将页面另存为”。

请按照以下过程导出全部或部分英文字符串。

1. 打开翻译工具。 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用“词典”下拉菜单选择要导出的词典。
1. 如果要导出字符串的子集，请选择词典中要导出的项目。 如果不选择任何项目，则导出所有项目。
1. 单击“导出”>“将选定内容导出为Xliff”（仅限字符串）。
1. 在出现的对话框中，复制文本并将其粘贴到文本文件中。

### 导入词典 {#importing-a-dictionary}

将XLIFF文件导入词典以填充词典。 当词典包括英文字符串的翻译且XLIFF文件包含同一字符串的不同翻译时，将替换该词典翻译。

1. 打开翻译工具 `http://<host>:<port>/libs/cq/i18n/translator.html`
1. 单击“导入”>“XLIFF翻译”。
1. 选择要导入的文件，然后单击“确定”。

## 管理受支持的语言 {#managing-supported-lanuages}

添加或删除翻译工具支持并向网页用户提供的语言。

### 更改字典表中列出的语言 {#changing-languages-listed-in-the-dictionary-table}

“翻译器”工具在词典表中包含以下语言：

* de —— 德语
* fr —— 法语
* it —— 意大利语
* es —— 西班牙语
* ja —— 日语
* pt-br —— 巴西葡萄牙语
* zh-cn —— 简体中文
* zh-tw —— 繁体中文（有限支持）
* ko-kr —— 朝鲜语

请按照以下过程添加或删除语言。

1. 使用CRXDE Lite创建新节点：

   `/etc/languages`

1. 在此节点上，创建一个属性：

   * **名称**: `languages`
   * **类型**: `Multi-String`
   * **值**:您希望显示的语言列表。 例如：

      * fr
      * es
   >[!NOTE]
   >
   >语言代码必须为小写。

1. 单击 **“在CRXDE** Lite中保存全部”，然后重新加载转换器。 网格将更新以显示定义的语言。

   >[!NOTE]
   >
   >译文器将仅保存字典中实际存 [在的语言的译文](#creating-a-dictionary) (即，在字典路径下 `/apps/myProject/i18n`)。
   >
   >确保这些语言与网格中显示的语言相对应。

### 为作者提供语言 {#making-languages-available-to-authors}

在为AEM实例中新的语言定义词典后，您需要使其可供作者选择(例如，在“首选项”中使 **用**):

1. 要更改“安全”控制台的“首选项”中 **可用的****语言列表** :

   1. 在应用程序代码中为以下对象创建叠加：

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. 要从“网站”控制台 **的** “首选项”中提供 **该语言** ，您需要在应用程序中进行以下更改：

   1. 在下面为结构创建叠加：

      `/libs/cq/security/content/tools/userProperties`

   1. 在叠加中，更新以下语言列表：

      `items/common/items /lang/options`

1. 保存所有内容并重新加载相应的控制台。

### 更改语言名称和默认国家／地区 {#changing-language-names-and-default-countries}

各国都使用同一种语言，例如美国，英国和澳大利亚都使用英语。 这由表示语言和国家（如，和）的代码 `en_US`表 `en_GB` 示 `en_AU`。

显示标记时（例如，在语言副本对话框中）使用默认国家／地区，它们用于解析语言代码的国家／地区。

>[!NOTE]
>
>对于由上述翻译器管理的本地化，只有确切的语言才有效。 如果语言首选项下拉框使 `en_uk`用，则存储库中必 `en_uk` 须有词典。

要更改默认定义：

1. 语言列表存储在：

   `/libs/wcm/core/resources/languages`

   通过将其复制到以下位置来覆盖它：

   `/apps/wcm/core/resources/languages`

   然后在那里更改或扩展列表。 语言 `defaultCountry` 节点上的属性(例如，) `ja`必须包含完整代码，如 `ja_jp`，该代码将定义 `jp` 为语言的默认国家／地区 `ja`。

1. 更新 **CQ WCM语言管理器**。

   * **语言列表**:

      存储库中语言列表的路径。 将其设置为用于叠加的位置：

      ```
             /apps/wcm/core/resources/languages
      ```
   您可以使用OSGi web控制台执行此操作：

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 出版词典 {#publishing-dictionaries}

将您的词典并入AEM应用程序的发布管理流程中。 例如，将词典包含在应用程序的内容包中以部署到发布实例。 此策略具有以下优点：

* 词典可用于其发布环境中的组件。
* 组件UI字符串的更改与更新的翻译一起部署。

同样，词典字符串测试应作为正常软件开发生命周期的一部分执行。

>[!NOTE]
>
>不应将常规发布功能或复制用于字典。 相反，应以与代码和配置相同的方式对待词典。 这包括使用源控件跟踪更改，以及使用内容包将更改应用于创作和发布。

>[!NOTE]
>
>使用Dispatcher时，您需要使缓存的页 [面失效](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) ，以便在呈现的组件字符串中包含新的字典字符串。

