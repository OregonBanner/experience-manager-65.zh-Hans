---
title: 基架
seo-title: 基架
description: 有时，您可能需要创建大量结构相同但内容不同的页面。使用基架，您可以创建一个表单（即基架），其中包含的字段反映您要用于页面的结构，然后使用此表单轻松创建基于此结构的页面。
seo-description: 有时，您可能需要创建大量结构相同但内容不同的页面。使用基架，您可以创建一个表单（即基架），其中包含的字段反映您要用于页面的结构，然后使用此表单轻松创建基于此结构的页面。
uuid: 5904abc0-b256-4da4-a7d7-3c17ea299648
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: a63e5732-b1a3-4639-9838-652af401e788
docset: aem65
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# 基架{#scaffolding}

有时，您可能需要创建大量结构相同但内容不同的页面。通过标准的 AEM 界面，您将需要创建每个页面，将相应的组件拖曳到页面上并逐个地对它们进行填充。

使用基架，您可以创建一个表单（即基架），其中包含的字段反映您要用于页面的结构，然后使用此表单轻松创建基于此结构的页面。

>[!NOTE]
>
>基架（在经典 UI 中）[使用 MSM 继承](#scaffolding-with-msm-inheritance)。

## 基架的工作原理 {#how-scaffolding-works}

Scaffolds are stored in the **Tools** console of the site admin.

* 打开&#x200B;**工具**&#x200B;控制台，然后单击&#x200B;**默认页面基架**。
* 在“默认页面基架”下，单击 **geometrixx**。
* 在 **geometrixx** 下，您将找到一个名为&#x200B;**新闻**&#x200B;的“基架页面”**。双击可打开此页面。

![howscaffold_work](assets/howscaffolds_work.png)

The scaffold consists of a form with a field for each piece of content that will make up the page to be created and four important parameters which are accessed through the **Page Properties** of the scaffold page.

![pageprops](assets/pageprops.png)

基架页面属性有：

* **标题文本**：这是此基架页面自己的名称。在本示例中，它的名称为“新闻”。
* **说明**：显示在基架页面的标题下方。
* **目标模板**：这是此基架在创建新页面时要使用的模板。在本示例中使用的是 *Geometrrixx 内容页面*&#x200B;模板。
* **目标路径**：这是此基架要在其下创建新页面的父页面的路径。In this example the path is */content/geometrixx/en/news*.

基架的主体是表单。当用户希望使用基架创建页面时，他需要填充表单并单击底部的“创建&#x200B;**”。In the **News** example above the form has the following fields:

* **标题**：这是要创建页面的名称。每个基架都具有此字段。
* **文本**：此字段对应生成页面上的文本组件。
* **图像**:此字段对应于生成页面上的图像组件。
* **图像/高级**：**标题**：图像的标题。
* **图像/高级**：**替代文本**：图像的替代文本。
* **图像／高级**:说 **明**:图像的描述。
* **图像/高级**：**尺寸**：图像的尺寸。
* **标记/关键字**：要分配给此页面的元数据。每个基架都具有此字段。

### 创建基架 {#creating-a-scaffold}

To create a new scaffold go to the **Tools** console, then **Default Page Scaffolding** and create a new page. A single page template type will be available, the *Scaffolding Template.*

Go to the **Page Properties** of the new page and set the *Title Text*, *Description*, *Target Template* and *Target Path*, as described above.

接下来，您必须定义此 scaffold 将创建的页面的结构。To do this go into **[design mode](/help/sites-authoring/page-authoring.md#sidekick)**on the scaffold page. 随即显示一个链接，允许您在&#x200B;**对话框编辑器**中编辑 scaffold。

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

使用对话框编辑器，您可以指定每次使用此基架创建新页面时将创建的属性。

基架对话框定义的工作方式与组件类似（请参阅[组件](/help/sites-developing/components.md)）。但还是存在一些重要差异：

* 组件对话框定义呈现为普通对话框（例如，对话框编辑器的中间窗格所示），而基架对话框定义虽然在对话框编辑器中显示为普通对话框，但在基架页面上却呈现为基架表单（如上面的&#x200B;**新闻**&#x200B;基架所示）。
* 组件对话框仅为定义单个特定组件的内容所需的那些值提供字段。基架对话框必须为要创建页面的每个段落中的每个属性提供字段。
* 就组件对话框而言，用于呈现指定内容的组件是隐式的，因此在创建段落时会自动填充段落的 `sling:resourceType` 属性。对于基架，定义给定段落的内容和分配组件的所有信息必须由对话框自身提供。在基架对话框中，必须通过在页面创建时使用“隐藏&#x200B;**”字段提交此信息来提供此信息。

研究对话框编辑器中的示例&#x200B;**新闻**&#x200B;基架对话框可帮助了解此过程的运行方式。进入基架页面的设计模式并单击对话框编辑器链接。

Now, click on the dialog field **Dialog > Tab Panel > Text > Text**, like this:

![textedit](assets/textedit.png)

此字段的属性列表将显示在对话框编辑器的右侧，如下所示：

![list_of_properties](assets/list_of_properties.png)

注意此字段的 name 属性。它具有值

`./jcr:content/par/text/text`

这是当基架用于创建页面时，将向其写入此字段内容的属性的名称。此属性以相对路径表示，从表示要创建页面的节点开始。它指定 text 属性，此属性位于 text 节点之下，此节点位于 par 节点之下，而 par 节点自身又是页面节点下 jcr:content 节点的子项。

它定义要输入到此字段的文本的内容存储的位置。然而，我们还需要为此内容再指定两个特性。

* 存储在此处的字符串必须解释为&#x200B;*富文本*，以及
* 哪个组件应该用于在生成页面上呈现此内容。

请注意，在普通的组件对话框中，您不必指定此信息，因为它是隐式的，对话框已绑定到特定的组件。

要指定这两类信息，可使用隐藏字段。Click on the first hidden field **Dialog > Tab Panel > Text > Hidden**, like this:

![隐藏](assets/hidden.png)

此隐藏字段的属性如下所示：

![hidden_list_props](assets/hidden_list_props.png)

此隐藏字段的 name 属性为

`./jcr:content/par/text/textIsRich`

This is a boolean property used to interpret the text string stored at `./jcr:content/par/text/text`.

因为我们知道文本应解释为富文本，所以我们将此字段的 `value` 属性指定为 `true`。

>[!CAUTION]
>
>The dialog editor allows the user to change the values of *existing* properties in the dialog definition. 要添加新属性，用户必须使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)。例如，在使用对话框编辑器将新的隐藏字段添加到对话框定义时，它没有 *value* 属性（即名为“value”的属性）。如果涉及的隐藏字段需要设置默认的 *value* 属性，则必须使用其中一个 CRX 工具手动添加此属性。通过对话框编辑器本身无法添加该值。然而，此属性一旦存在，即可使用对话框编辑器编辑其值。

可通过单击查看第二个隐藏字段，如下所示：

![hidden2](assets/hidden2.png)

此隐藏字段的属性如下所示：

![hidden_list_props2](assets/hidden_list_props2.png)

此隐藏字段的 name 属性为

`./jcr:content/par/text/sling:resourceType`

并且为此属性指定的固定值为

`foundation/components/textimage`

它指定要用于呈现此段落文本内容的组件是&#x200B;*文本图像*&#x200B;组件。Using with the `isRichText` boolean specified in the other hidden field, the component can render the actual text string stored at `./jcr:content/par/text/text` in the desired way.

### 使用 MSM 继承的基架 {#scaffolding-with-msm-inheritance}

在经典 UI 中，基架与 MSM 继承完全集成（如果适用）。

当您以&#x200B;**基架**&#x200B;模式打开页面（使用 Sidekick 底部的图标）时，任何使用了继承的组件都将带有以下指示标记：

* 锁符号（对于大多数组件；例如文本和标题）
* 包含文本&#x200B;**单击以取消继承**&#x200B;的蒙版（对于图像组件）

这两种指示标记都表示该组件无法编辑 - 除非取消继承。

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>这与[编辑页面内容时继承的组件](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui)类似。

单击锁符号或图像图标可以中断继承：

* 锁符号将变为打开的挂锁。
* 解锁后，您便可以编辑内容。

![chlimage_1-1](assets/chlimage_1-1.jpeg)

解锁后，您可以通过单击已解锁的挂锁符号来恢复继承 - 此操作将会丢失您所做的任何编辑。

>[!NOTE]
>
>If the inheritance is canceled at the page level (from the Livecopy tab of Page Properties) then all components will be editable in **Scaffolding** mode (they will be shown in unlocked state).
