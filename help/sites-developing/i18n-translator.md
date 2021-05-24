---
title: 使用翻译器管理字典
seo-title: 使用翻译器管理字典
description: AEM提供了一个控制台，用于管理组件UI中使用的各种文本的翻译
seo-description: AEM提供了一个控制台，用于管理组件UI中使用的各种文本的翻译
uuid: 4eea3110-e958-473e-8d22-c84fa435edbd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: adf3364c-11f1-45c6-b41d-2c7d48b626f9
exl-id: a8d50c09-72d0-406e-874e-50a985227a56
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# 使用翻译器管理字典{#using-translator-to-manage-dictionaries}

AEM提供了一个控制台，用于管理组件UI中使用的各种文本的翻译。 此控制台在

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

使用翻译工具管理英文字符串及其翻译。 字典在存储库中创建，例如/apps/myproject/i18n。

请注意，翻译工具和您管理的字典用于以不同语言显示组件UI。 如果要翻译页面或用户生成的内容，请参阅[多语言站点的翻译内容](/help/sites-administering/translation.md)和[用户生成内容的翻译](/help/communities/translate-ugc.md)。

>[!CAUTION]
>
>仅编辑为项目创建并位于`/apps`下的字典。
>
>AEM系统字典在此工具中也可用。 请勿更改AEM系统字典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统字典位于`/libs`下。

>[!NOTE]
>
>尽管翻译工具具有经典UI界面，但它用于翻译短语，而不管在哪个界面中找到这些短语。

翻译人员将AEM中使用的各种语言翻译文本列在一起：

![chlimage_1-205](assets/chlimage_1-205.png)

您可以搜索、过滤和编辑英文文本和翻译文本。 您还可以将字典导出为XLIFF格式进行翻译，然后将翻译导回字典。

也可以从此控制台将i18n词典添加到翻译项目。 您可以创建新项目或添加到现有项目。

1. 单击&#x200B;**翻译字典**。

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. 根据需要选择创建或添加选项。 将打开一个对话框。

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. 根据需要填写字段，然后单击“确定”。 ![chlimage_1-208](assets/chlimage_1-208.png)

1. 您现在可以单击&#x200B;**OK**&#x200B;或查看Target词典。

   >[!NOTE]
   >
   >有关翻译项目的更多信息，请阅读[管理翻译项目](/help/sites-administering/tc-manage.md)。

## 创建字典{#creating-a-dictionary}

创建用于管理本地化的UI字符串的字典。 创建字典后，可以使用翻译工具管理该字典。

1. 使用CRXDE Lite，将新词典的根节点(`sling:Folder`)添加为包含语言定义的结构：

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
   >这是[Sling i18n模块](https://sling.apache.org/site/internationalization-support.html)中的结构。

1. 重新加载翻译器和字典路径(例如，`/apps/myProject/i18n`)将在工具栏的下拉选择器中可用。 选择此选项可开始添加字符串及其翻译。

   >[!NOTE]
   >
   >翻译器将仅保存路径下实际存在的语言的翻译(例如，`/apps/myProject/i18n`)。
   >
   >确保这些语言与网格中显示的语言相对应。

## 管理字典字符串{#managing-dictionary-strings}

使用翻译工具管理字典中的字符串。 您可以添加、修改和删除英语字符串，还可以提供翻译后的字符串。

>[!CAUTION]
>
>仅编辑为项目创建并位于`/apps`下的字典。
>
>请勿更改AEM系统字典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统字典位于`/libs`下。

### 添加、更改和删除字符串{#adding-changing-and-removing-strings}

将英语字符串添加到组件已国际化的词典中。 仅添加国际化的字符串，以便您不会通过翻译未使用的字符串来浪费资源。

您添加到词典的字符串必须与代码中指定的字符串完全匹配。 如果代码中使用的默认英语字符串与词典中的英语字符串不匹配，则翻译后的字符串不会在需要时显示在UI中。 字符串区分大小写。

**提供翻译提示**

使用词典字符串的Comment属性向翻译人员提供信息以阐明字符串的含义。 通常，UI会帮助用户确定模糊词语的含义。 但是，翻译人员在UI的上下文中看不到字符串。 翻译提示可消除歧义。 例如，注释有助于翻译人员了解英语单词“请求”是用作名词，而不是动词。

翻译提示还会区分相同且含义不同的字符串。 例如，词Search可以是名词或动词，需要在词典中输入两个“Search”项，并提供两个不同的翻译提示。 请求字符串的代码还包含翻译提示，以便在UI中使用正确的字符串。

**包括索引变量**

在本地化字符串中包含变量，以将上下文含义构建到句子中。 例如，登录Web应用程序后，主页显示消息“欢迎返回管理员”。 收件箱中有2条邮件。” 页面上下文确定用户名和消息数量。

要将变量包含在本地化字符串中，请将方括号内的索引放置在get方法第一个参数中变量的位置。 使用本地化提示描述这些值。 翻译人员必须理解变量的含义，因为不同的语言使用不同的句子结构。

请注意，请求翻译字符串](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences)的代码会根据上下文为索引变量提供值。[

例如，当用户登录到网站时，将显示以下字符串，并将其包含在词典中：

`Welcome back {0}. You have {1} messages.`

以下注释介绍了变量：

`{0} = the user name, {1} = the number of items in the user's inbox`

**修改字符串**

更改或删除在代码中更改或删除的英文字符串。 更改字符串时，将保留原始字符串，并创建一个新字符串来反映该更改。 在删除字符串之前，请确保没有代码使用该字符串。

请按照以下过程添加字符串。

1. 在“字典”下拉菜单中，选择要将字符串添加到的字典。 在下拉菜单中，词典由其在存储库中的路径表示。
1. 在“字符串和翻译”表上方，单击“添加”。

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. 在“添加字符串”对话框的“字符串”框中，键入英文字符串。 在注释框中，根据需要为翻译人员键入翻译提示。
1. 单击确定。
1. 单击保存。

   ![chlimage_1-210](assets/chlimage_1-210.png)

请按照以下过程更改词典中的字符串。

1. 在词典下拉菜单中，选择包含要更改的字符串的词典。
1. 双击要更改的字符串。
1. 在编辑字符串对话框中，选择修改字符串或注释（创建副本）。

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. 修改字符串或注释，然后单击“确定”。
1. 单击保存。

   ![chlimage_1-212](assets/chlimage_1-212.png)

请按照以下过程从字典中删除字符串。

1. 在字典下拉菜单中，选择要从中删除字符串的字典。
1. 单击删除。

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. 单击保存。

   ![chlimage_1-214](assets/chlimage_1-214.png)

### 搜索字符串{#searching-for-strings}

“翻译器”工具底部的搜索栏提供字符串选择选项：

* **按文本过滤：** 与英语字符串、评论或翻译匹配的模式。表中仅显示与模式全部或部分匹配的项目。
* **更改：任意、已修改、新建、已删除：** 显示已更改且未保存的项目。

   * 任意：显示已修改、添加或删除的项目。
   * 已修改：显示已更改的项目。
   * 新：显示已添加的项目。
   * 已删除：显示要删除的项目。
   * 多个选择：显示具有所有选定属性的项目。

* **评论**:显示有注释的翻译员项目。
* **缺少翻译：** 显示至少一种语言没有翻译的项目。

![chlimage_1-215](assets/chlimage_1-215.png)

1. 在搜索栏中，选择筛选选项。
1. 要使用选项进行过滤，请单击“过滤”。
1. 要删除过滤器并查看字典中的所有项目，请单击“清除”。

### 编辑已翻译的字符串{#editing-translated-strings}

在将英语字符串添加到词典后，可以添加该字符串的翻译。 您还可以[导出字典](/help/sites-developing/i18n-translator.md#exporting-a-dictionary)，以便第三方翻译该字典。

1. 选择[您的项目特定词典](#creating-a-dictionary)，因为该词典指定了包含翻译的存储库中的路径。 例如，选择&#x200B;**字典**&#x200B;作为：

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >仅编辑为项目创建并位于`/apps`下的字典。
   >
   >AEM系统字典在此工具中也可用。 请勿更改AEM系统字典，因为这可能会导致AEM UI出现问题。 此外，升级时更改可能会丢失。 AEM系统字典位于`/libs`下。

1. 要编辑其中一个字符串的翻译文本，您可以执行以下任一操作：

   * 双击所需字符串的相应语言以编辑该单个文本：

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * 双击&#x200B;**String**&#x200B;或&#x200B;**Comment**&#x200B;字段，打开所需字符串以打开&#x200B;**编辑字符串**&#x200B;对话框，根据需要编辑翻译，然后单击&#x200B;**OK**&#x200B;以关闭对话框：

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 单击工具栏中的&#x200B;**Save**&#x200B;以提交更改。

   >[!NOTE]
   >
   >单击&#x200B;**重置并刷新**（而不是&#x200B;**保存**）会还原对先前文本所做的任何更改。

## 使用第三方翻译器{#using-third-party-translators}

为了支持使用第三方翻译服务，翻译工具允许您导出和导入字典。

### 导出字典{#exporting-a-dictionary}

将字典导出到XLIFF文件，以便第三方服务可以翻译该字典字符串。

* 导出字典，并包含语言的英语和译文。
* 导出部分或全部英文字符串。

导出XLIFF文件并包含语言时，存储库中词典的节点结构必须包含该语言。 如果不包含语言，则会发生错误。 例如，要导出法语XLIFF文件，词典文件夹必须包含名为`fr`的`mix:language`子节点。 （请参阅[创建字典](/help/sites-developing/i18n-translator.md#creating-a-dictionary)。）

请按照以下过程导出特定语言的XLIFF文件。

1. 打开翻译工具`http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用“字典”下拉菜单选择要导出的字典。
1. 单击导出>导出完整&#x200B;*XX* Xliff选项，其中&#x200B;*XX*&#x200B;是双字母语言代码，如DE或FR。

   XLIFF文件将在新选项卡或窗口中打开。

1. 使用Web浏览器命令将页面另存为文件系统上的文件，如“文件”>“页面另存为”。

请按照以下过程导出全部或部分仅英文字符串。

1. 打开翻译工具。`http://<host>:<port>/libs/cq/i18n/translator.html`
1. 使用“字典”下拉菜单选择要导出的字典。
1. 如果要导出字符串的子集，请选择词典中要导出的项目。 选择“无”项目将导出所有项目。
1. 单击导出>将选定内容导出为Xliff（仅限字符串）。
1. 在出现的对话框中，复制文本并将其粘贴到文本文件中。

### 导入字典{#importing-a-dictionary}

将XLIFF文件导入字典以填充该字典。 当词典包含英语字符串的翻译，而XLIFF文件包含同一字符串的不同翻译时，将替换词典翻译。

1. 打开翻译工具`http://<host>:<port>/libs/cq/i18n/translator.html`
1. 单击导入> XLIFF翻译。
1. 选择要导入的文件，然后单击“确定”。

## 管理支持的语言{#managing-supported-lanuages}

添加或删除翻译工具支持的语言以及提供给网页用户的语言。

### 更改词典表{#changing-languages-listed-in-the-dictionary-table}中列出的语言

“翻译器”工具在词典表中包含以下语言：

* de — 德语
* fr — 法语
* it — 意大利语
* es — 西班牙语
* ja — 日语
* pt-br — 巴西葡萄牙语
* zh-cn — 简体中文
* zh-tw — 繁体中文（有限支持）
* ko-kr — 朝鲜语

请按照以下过程添加或删除语言。

1. 使用CRXDE Lite创建新节点：

   `/etc/languages`

1. 在此节点上，创建一个属性：

   * **名称**: `languages`
   * **类型**: `Multi-String`
   * **值**:要显示的语言列表。例如：

      * fr
      * es

   >[!NOTE]
   >
   >语言代码必须为小写。

1. 在CRXDE Lite中单击&#x200B;**全部保存**&#x200B;并重新加载转换器。 将更新网格以显示定义的语言。

   >[!NOTE]
   >
   >翻译器将只保存字典](#creating-a-dictionary)中实际存在[的语言的翻译（即，字典路径下`/apps/myProject/i18n`）。
   >
   >确保这些语言与网格中显示的语言相对应。

### 为作者提供语言{#making-languages-available-to-authors}

在为AEM实例新的语言定义字典后，您需要使其可供作者选择（例如，在&#x200B;**Preferences**&#x200B;中使用）：

1. 要更改&#x200B;**Security**&#x200B;控制台的&#x200B;**Preferences**&#x200B;中可用语言的列表，请执行以下操作：

   1. 在应用程序代码中为以下对象创建一个叠加：

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. 要使语言从&#x200B;**网站**&#x200B;控制台在&#x200B;**首选项**&#x200B;中可用，您需要在应用程序中进行以下更改：

   1. 在下面为结构创建叠加：

      `/libs/cq/security/content/tools/userProperties`

   1. 在叠加内，更新下面的语言列表：

      `items/common/items /lang/options`

1. 保存所有内容并重新加载相应的控制台。

### 更改语言名称和默认国家/地区{#changing-language-names-and-default-countries}

各国都使用同一种语言，例如美国、英国和澳大利亚都使用英语。 这由指示语言和国家/地区的代码表示，如`en_US`、`en_GB`和`en_AU`。

显示标记时，会使用默认国家/地区（例如，在语言副本对话框中），它们用于解析语言代码的国家/地区。

>[!NOTE]
>
>对于由上述翻译器管理的本地化，只有确切的语言才有效。 如果语言首选项下拉列表使用`en_uk`，则存储库中必须有`en_uk`字典。

要更改默认定义，请执行以下操作：

1. 语言列表存储在以下位置：

   `/libs/wcm/core/resources/languages`

   通过将其复制到以下位置来叠加它：

   `/apps/wcm/core/resources/languages`

   然后在此处更改或扩展列表。 语言节点上的属性`defaultCountry`(例如，`ja`)必须包含完整代码，如`ja_jp`，该代码会将`jp`定义为语言`ja`的默认国家/地区。

1. 更新&#x200B;**CQ WCM语言管理器**。

   * **语言列表**:

      存储库中语言列表的路径。 将此值设置为用于叠加的位置：

      ```
             /apps/wcm/core/resources/languages
      ```
   您可以使用OSGi Web控制台执行此操作：

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## 发布字典{#publishing-dictionaries}

将您的字典纳入AEM应用程序的版本管理流程中。 例如，在应用程序的内容包中包含字典，以部署到发布实例。 此策略具有以下好处：

* 词典可用于其发布环境中的组件。
* 对组件UI字符串所做的更改会与更新的转换一起部署。

同样，字典字符串的测试应作为正常软件开发生命周期的一部分执行。

>[!NOTE]
>
>常规发布功能或复制功能不应用于字典。 相反，词典的处理方式应与代码和配置相同。 这包括使用源代码管理跟踪更改，以及使用内容包将更改应用到创作和发布。

>[!NOTE]
>
>使用Dispatcher时，您需要[使缓存的页面](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html)失效，以在呈现的组件字符串中包含新的词典字符串。
