---
title: 為Adobe Experience Manager建立無障礙內容（符合WCAG 2.1）
description: 使用AEM協助讓身心障礙人士存取及使用網路內容
exl-id: 2145d761-f51d-482b-a0e7-ef7500c4872f
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '13818'
ht-degree: 69%

---

# 创建无障碍内容（WCAG 2.1 合规性） {#creating-accessible-content-wcag-conformance}

此 [網頁內容可及性指引(WCAG) 2.1](https://www.w3.org/TR/WCAG/)，起草者： [全球資訊網協會工作組](https://www.w3.org/groups/#Accessibility_Guidelines_Working_Group)，包含一系列技術獨立指引和成功標準，以協助身心障礙人士存取及使用網路內容。

作为对该准则的介绍，联盟提供了一系列条款和支持文档：

* [WCAG 2.1 的新增内容](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [如何满足 WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [了解 WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [用于 WCAG 2.1 的技术](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG 文档](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，请参阅：
* 此 [WCAG 2.1快速指南](/help/managing/qg-wcag.md).
* [Adobe 解决方案的“无障碍合规性”报告](https://www.adobe.com/accessibility/compliance.html)
* [配置富文本编辑器以创建辅助内容](/help/sites-administering/rte-accessible-content.md)

该指南根据三个一致性级别进行分级：A 级（最低）、AA 级和 AAA 级（最高）。簡言之，層級的定義如下：

* **级别 A：**&#x200B;您的站点满足基本的、最低级别的无障碍性。要达到此级别，需满足所有级别 A 成功标准。
* **级别 AA：**&#x200B;这是要努力实现的理想无障碍级别，在此级别，站点满足基本级别的无障碍性，因此多数情况下大部分人都可以使用大部分技术访问站点。为达到此级别，所有 A 级和 AA 级成功标准均已满足。
* **AAA 级：**&#x200B;您的网站达到了高水平的可访问性。 为达到此级别，所有 A 级、AA 级和 AAA 级成功标准均已满足。

在创建站点时，您应该大体上确定希望自己的站点符合哪个等级。

以下部分介绍 [WCAG 2.1 准则的各个层面](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)以及[符合](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A 级和 AA 级的相关成功标准。

>[!NOTE]
>
>在本文件中，使用了以下内容：
>
>* [WCAG 2.1 准则的简称](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)。
>* [WCAG 2.1 准则中使用的编号](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1)，以便与 WCAG 网站进行交叉引用。


## 准则 1：可感知 {#principle-perceivable}

[准则 1：可感知 – 信息和用户界面组件必须以可感知的方式呈现给用户。](https://www.w3.org/TR/WCAG/#perceivable)

### 替换文本 (1.1) {#text-alternatives}

[指南 1.1 文本替代：为任何非文本内容提供替换文本，以便可以将其更改为人们需要的其他形式，例如大字体、盲文、语音、符号或更简单的语言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文字內容(1.1.1) {#non-text-content}

* 成功标准 1.1.1
* A 级
* 非文本内容：呈现给用户的所有非文本内容都具有相同用途的替换文本，以下所列情况除外。

#### 用途 – 非文本内容 (1.1.1) {#purpose-non-text-content}

网页上的信息可以多种不同的非文本格式提供，例如图片、视频、动画、图表和图形。盲人或有严重视力障碍的人无法看到非文本内容。但是，他们可以通过屏幕阅读器读取文本内容或通过盲文显示设备以触觉形式呈现文本内容来访问相关内容。因此，透過以圖形格式提供文字替代內容，看不到圖形內容的人可以存取內容所提供的對等版本資訊。

另一個實用的優點是，替代文字功能可讓搜尋引擎技術為非文字內容編制索引。

#### 如何達到標準 — 非文字內容(1.1.1) {#how-to-meet-non-text-content}

对于静态图形，基本的要求是为图形提供对等的替换文本。這可以在以下位置完成： **替代文字** 欄位。例如，請參閱核心元件 **[影像](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/image.html)**.

>[!NOTE]
>
>某些开箱即用的核心组件（例如&#x200B;**[轮播](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html)**）没有提供用于向单个图像添加替换文本描述的&#x200B;**替换文本**&#x200B;字段，尽管存在适用于整个组件的&#x200B;**标签**&#x200B;字段（**[辅助功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/carousel.html#accessibility-tab)**&#x200B;选项卡）。
>
>因此，在为 AEM 实例实施这些版本时，开发团队必须将此类组件配置为支持 `alt` 属性，以便作者可以将其添加到内容中（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

默认情况下，AEM 要求填写&#x200B;**替换文本**&#x200B;字段。如果图像是纯粹的装饰并且不需要替换文本，则可以选中&#x200B;**图像具有装饰性**&#x200B;选项。

#### 创建有效的替换文本 {#creating-good-text-alternatives}

非文字內容有多種形式，因此替代文字的值取決於圖形在網頁中所扮演的角色。 一些要遵循的一般經驗法則包括：

* 替代文字應簡明扼要，但清楚擷取非文字內容所提供的基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更多細節：
   * 在替换文本中提供简短的描述
   * 同时，在同一页面的其他位置或在一个单独的网页中提供更加详尽的描述文本。然后，为该图像创建一个链接，或者在图像旁边放置一个文本链接，以便链接到该单独的描述。
* 替换文本不应复制同一页面邻近位置以文本形式提供的内容。請記住，許多影像都是頁面文字中已涵蓋點的插圖，因此可能會存在詳細的替代文字。
* 如果非文字內容是另一個頁面或檔案的連結，且沒有其他文字構成相同連結的一部分，則影像的替代文字必須指出連結的目的地。 它不能描述图像。
* 如果非文字內容包含在按鈕元素中，並且沒有文字構成相同按鈕的一部分，則影像的替代文字必須指示按鈕的功能。 它不能描述图像。
* 为图像提供空 (null) 替代文本是完全可以接受的，但前提是该图像不需要替代文本。例如，它是一个纯粹的装饰图形，或者页面文本中存在等效文本时。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

以下特定类型的非文本内容可能需要替换文本：

* 说明性照片：指人物、对象或地点的图像。請務必思考像片在頁面中的角色，並描述影像內容，因為輔助技術會朗讀元素型別(例如 `graphic` 或 `image`)；這可以提高使用的清晰度 `screenshot` 或 `illustration` 替代文字說明，但這取決於上下文。 一致性是一个重要因素，在做出某项决策时，该决策应该是面向整个创作团队的，并且应被应用于整个用户体验中。
* 图标：指传递特定信息的小图形符号（图形）。页面和站点上使用的图标必须保持一致。图标在页面或站点上出现的所有实例都应使用相同的简短替换文本，除非这样做会与相邻的文本产生不必要的重复情况。
* 图表和图形：通常用于表示数值数据。因此，替代文本的选择之一就是简要地总结图表或图形中表现出来的主要趋势。如有必要，还可以在&#x200B;**高级**&#x200B;图像属性选项卡中的&#x200B;**描述**&#x200B;字段中以文本形式提供更加详尽的描述。此外，还可以在页面或站点的其他位置以表形式提供源数据。
* 映射、示意图、流程图：对于提供空间数据的图形（例如，支持描述对象之间的关系或者某个流程），请确保以文本格式提供关键消息，并且此文本信息位于每个关联的数据点附近。对于映射，提供等效完整文本可能不太现实，但如果提供映射来作为帮助相关人员找到特定位置的一种方法，则映射图像的替换文本可以简短地指示为 *X 映射*，然后在页面其他位置的文本中或者通过&#x200B;**图像**&#x200B;组件&#x200B;**高级**&#x200B;选项卡中的&#x200B;**描述**&#x200B;字段提供该特定位置的说明。
* 驗證碼：驗證碼是 *完全自動化的公用圖靈測試，區分電腦和人類*.這是用於網頁的安全性檢查，可區分人類與惡意軟體，但可能會導致存取障礙。 這些影像需要使用者描述他們所看到的內容，以便通過安全性測試。 为这些图像提供替代文本是不可能的，因此必须思考出非图形的替代解决方案。W3C提供一些建議，例如：
   * 邏輯謎題
   * 使用聲音輸出而非影像
   * 限制使用帐户和垃圾邮件过滤器。
* 背景图像：背景图像是使用层叠样式表 (CSS) 而不是 HTML 实现的。这就意味着无法指定替换文本值。因此，背景图像不应提供重要的文本信息 - 即便提供，这些信息必须也要在页面的文本中有所提及。尽管如此，当图像无法显示时，也应务必显示替代背景。

>[!NOTE]
>
>背景和前景文字之間應該要有適當等級的對比，詳情請參閱 [對比（最小） (1.4.3)](#contrast-minimum).

#### 更多資訊 — 非文字內容(1.1.1) {#more-information-non-text-content}

* [了解成功标准 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何达到成功标准 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [驗證碼的W3C說明和替代方案](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 基于时间的媒体 (1.2) {#time-based-media}

[准則1.2以時間為基礎的媒體：提供以時間為基礎的媒體替代方案。](https://www.w3.org/TR/WCAG/#time-based-media)

此准则涉及“基于时间”**&#x200B;的 Web 内容。这包括用户可以播放的内容（例如，视频、音频和动画内容），这些内容可以是预先录制的，也可以是实时流传输的。

### 纯音频和纯视频（预先录制）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功标准 1.2.1
* A 级
* 纯音频和纯视频（预先录制）：对于预先录制的纯音频媒体和预先录制的纯视频媒体，均存在以下情况，除非音频或视频就是文本的替代媒体 ，且明确进行了如下标记：
   * 僅限預先錄製的音訊：提供時間型媒體的替代方案，為預先錄製的僅限音訊內容提供同等資訊。
   * 僅限預先錄製的視訊：是以時間為基礎的媒體替代方案，或是提供音軌，為僅限預先錄製的視訊內容提供同等資訊。

#### 用途 – 纯音频和纯视频（预先录制）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

以下用户可能会遇到音频和视频的无障碍问题：

* 沒有音軌或音軌不足以通知視訊或動畫中發生的事情時，患有視覺障礙的人；
* 有聽力障礙或耳聾且聽不到音軌的人；
* 可以聽到音軌但不瞭解說話內容的人（例如，因為這是他們不瞭解的語言）。

使用不支援以特定媒體格式(例如AdobeFlash)播放內容的瀏覽器或裝置的人也可能無法播放視訊或音訊。

以不同格式提供此資訊，例如文字（或沒有音訊的視訊）可讓無法存取原始內容的人存取這些資訊。

#### 如何达到标准 – 纯音频和纯视频（预先录制）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果内容是预先录制的不含视频的音频（如播客）：
   * 提供緊接在內容之前或之後的音訊內容文字記錄連結。成績單應該是一個HTML頁面，其中包含所有口語和重要的非口語內容的對等文字，以及說話者的指示、對語境的描述、語音表達，以及對任何其他重要音訊的描述。
* 如果内容是不含音频的动画或预先录制的不含音频的视频：
   * 提供緊接在內容之前或之後的連結，以提供視訊所提供資訊的同等文字說明
   * 或是常用的音訊格式（例如MP3）中的對等音訊描述。

>[!NOTE]
>
>如果音频或视频内容是作为同一网页上存在的其他格式内容的替换内容提供的，则可能不需要其他替换文本。
>
>准则《[了解 WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)》提供了进一步的信息。

在 AEM 网页中插入多媒体的方式与插入图像类似。然而，由於多媒體內容遠不止是靜態影像，因此有各種不同的設定和選項來控制多媒體播放的方式。

>[!NOTE]
>
>如果将多媒体与信息性内容结合使用，则也必须创建替代内容的链接。例如，要加入文本记录，应创建一个用于显示记录的 HTML 页面，然后在音频内容旁边或下方添加一个链接。

#### 更多信息 – 纯音频和纯视频（预先录制）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [了解成功标准 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何达到成功标准 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 字幕（预先录制）(1.2.2) {#captions-prerecorded}

* 成功标准 1.2.2
* A 级
* 字幕（预先录制）：为同步媒体中所有预先录制的音频内容提供了字幕，除非该媒体是文本的替代媒体，且明确进行了相应标记。

#### 用途 – 字幕（预先录制）(1.2.2) {#purpose-captions-prerecorded}

耳聋或听力欠佳的用户无法或很难获取音频内容。字幕是讲话和非讲话音频的对等文本，在视频播放过程中会在相应的时间显示在屏幕上。这让无法听到音频的用户可以了解正在播放的内容。

#### 如何达到标准 – 字幕（预先录制）(1.2.2) {#how-to-meet-captions-prerecorded}

字幕有以下两种形式：

* 开放式：字幕在视频播放过程中始终可见
* 隐藏式：字幕可以由用户打开或关闭 

尽量使用隐藏字幕，因为这样用户可以选择是否观看字幕。

對於隱藏式字幕，請建立並提供適當格式的同步字幕檔案(例如 [SMIL](https://www.w3.org/AudioVideo/))以及影片檔案(如何執行此動作的詳細資訊不在本指南的涵蓋範圍內，但我們已提供下列部分教學課程的連結： [更多資訊 — 字幕（預先錄製）(1.2.2)](#more-information-captions-prerecorded))。 确保提供注释或在视频播放器中启用字幕功能，以便让用户知道视频有字幕可看。

如果您必須使用開啟的註解，請將文字內嵌到視訊曲目中。 這可以使用視訊編輯應用程式來完成，該應用程式允許將標題覆蓋在視訊上。

#### 更多信息 – 字幕（预先录制）(1.2.2) {#more-information-captions-prerecorded}

* [了解成功标准 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何达到成功标准 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音频描述或替代媒体（预先录制）(1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功标准 1.2.3
* A 级
* 音訊描述或替代媒體（預先錄製）：為同步媒體提供以時間為基礎的媒體替代或預先錄製的視訊內容的音訊描述，除非媒體是文字的替代媒體，且明確標示為文字。

#### 用途 – 音频描述或替代媒体（预先录制）(1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果视频或动画中的信息仅以可视形式呈现，或者音轨提供的信息不足以让用户了解视频或动画中正在播放的内容，则失明或患有视觉障碍的用户将会遇到无障碍问题。

#### 如何达到标准 – 音频描述或替代媒体（预先录制）(1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

有兩種方法可達成此成功標準。 兩者皆可接受：

1. 為視訊內容加入其他音訊說明。 這可透過下列三種方式之一達成：
   * 在現有對話方塊中暫停期間，提供未出現在現有音訊曲目中的場景變更相關資訊；
   * 提供一段附加的可选新音轨，其中不仅包含原始音轨，而且还包含有关场景变换的额外音频信息。
      * 使用者可以在現有音軌之間切換(這項 *不會* 包含音訊說明)和新的音軌(哪些 *會* 包含音訊說明)。
      * 這可防止對不需要額外說明的使用者造成中斷。
   * 建立視訊內容的第二個版本，以允許擴充的音訊說明。 這可藉由在適當的點暫時暫停音訊和視訊，減少在現有對話方塊之間的間隙中提供詳細音訊說明的困難。 因此，在動作再次開始之前，可以輸入更長的音訊說明。 如同上一個範例，最好將此作為選用的額外音訊曲目提供，以防止對不需要額外說明的使用者造成干擾。
1. 提供視訊或動畫的音訊和視覺元素的文字稿，它是適當的對等文字。 这应当包括，在适当情况下，指出讲话者，以及描述讲话背景、视觉上呈现的任何事件或信息和语音表述内容。根据文本长度的不同，既可以将记录放置在视频或动画所在的页面上，也可以将其放置在单独的页面上；如果选择后者，则需要在视频或动画旁边提供记录的链接。

至于如何创建带有音频描述的视频，具体细节不在本指南的范围之内。创建视频和音频描述非常耗时，但是 Adobe 的其他产品可以帮助您完成这些任务。

#### 更多信息 – 音频描述或替代媒体（预先录制）(1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [了解成功标准 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何达到成功标准 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 字幕（实时）(1.2.4)  {#captions-live}

* 成功标准 1.2.4
* AA 级
* 註解（即時）：為同步媒體中的所有即時音訊內容提供註解。

#### 用途 — 字幕（即時） (1.2.4) {#purpose-captions-live}

该成功标准与[字幕（预先录制）](#captions-prerecorded)的标准完全相同，因为其用途在于解决耳聋或听力欠佳的用户遇到的辅助功能问题，两者的不同之处在于该成功标准需要处理网络直播等实时演示。

#### 如何达到标准 – 字幕（实时）(1.2.4) {#how-to-meet-captions-live}

遵循上面[字幕（预先录制）](#captions-prerecorded)所提供的指南。但鉴于媒体的实时性质，必须尽可能以最快的速度提供字幕，并对正在发生的情况做出回应。因此，应当考虑使用实时字幕工具或语音转文本工具。

与此相关的详细说明不在本指南的范围之内，但是以下资源提供了有用的信息：

* [WebAIM：实时字幕](https://webaim.org/techniques/captions/realtime)

* [AccessComputing 项目（华盛顿大学）：能否利用语音识别技术自动生成字幕？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 更多信息 – 字幕（实时）(1.2.4) {#more-information-captions-live}

* [了解成功标准 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何达到成功标准 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音频描述（预先录制）(1.2.5)  {#audio-description-prerecorded}

* 成功标准 1.2.5
* AA 级
* 音频描述（预先录制）：为同步媒体中的所有预先录制的视频内容提供了音频描述。

#### 用途 – 音频描述（预先录制）(1.2.5) {#purpose-audio-description-prerecorded}

此成功标准与[音频描述或替代媒体（预先录制）](#audio-description-or-media-alternative-prerecorded)的标准几乎完全相同，唯一不同之处在于，作者必须提供更加详细的音频描述才能符合 AA 级标准。

#### 如何达到标准 – 音频描述（预先录制）(1.2.5) {#how-to-meet-audio-description-prerecorded}

遵循[音频描述或替代媒体（预先录制）](#audio-description-or-media-alternative-prerecorded)所提供的指南。

#### 更多信息 – 音频描述（预先录制）(1.2.5) {#more-information-audio-description-prerecorded}

* [了解成功标准 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何达到成功标准 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 可調整(1.3) {#adaptable}

[指引1.3改寫：建立可以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG/#adaptable)

本指引涵蓋支援以下人員所需的需求：

* 可能无法访问作者使用相应内容的默认呈现方式呈现的信息（例如，多列布局或大量使用颜色和/或图像的页面）的用户。

* 可能要使用纯音频内容或可视替代显示方式（如大文本或高对比度）的用户。

### 信息和关系 (1.3.1)  {#info-and-relationships}

* 成功标准 1.3.1
* A 级
* 資訊和關係：透過表示法傳遞的資訊、結構和關係可以程式化方式確定，或可在文字中使用。

#### 用途 — 資訊和關係(1.3.1) {#purpose-info-and-relationships}

殘障人士使用的許多輔助技術都仰賴結構資訊來有效顯示或 *瞭解* 內容。 此結構資訊可採用頁面標題、表格列與欄標題，以及清單型別的形式。 例如，熒幕助讀程式可讓使用者在標題之間導覽頁面。 但是，當頁面內容似乎只有透過視覺樣式而非基礎HTML的結構時，則沒有可用於輔助技術的結構資訊，限制其支援更輕鬆瀏覽的能力。

该成功标准旨在确保此类结构性信息通过 HTML 或其他代码技术以编程的方式提供，这样浏览器和辅助型技术便可以访问并利用这些信息。

#### 如何达到标准 – 信息和关系 (1.3.1) {#how-to-meet-info-and-relationships}

AEM 允许轻松地使用相应的 HTML 元素构建语义上有意义的 Web 内容。在RTE （文字元件）中開啟頁面內容，並使用 **引數格式** 選單（段落符號）以指定適當的結構元素（例如，段落和標題）。

在适用的情况下，您可以使用以下元素来确保网页具有相应的结构：

* **标题：**&#x200B;只要您启用了 RTE 辅助功能，AEM 就会提供三个级别的页面标题。您可以使用这些标题标识内容的章节和子章节。标题 1 是最高级别的标题，标题 3 是最低级别的标题。系统管理员可以配置系统以允许使用更多标题级别。

* **列表**：可以使用 HTML 指定三种不同类型的列表：
   * `<ul>` 元素用于表示&#x200B;*无序*（项目符号）列表。单个列表项使用 `<li>` 元素进行标识。
在 RTE 中，使用**项目符号列表**&#x200B;图标。
   * `<ol>` 元素用于表示&#x200B;*编号*&#x200B;列表。单个列表项使用 `<li>` 元素进行标识。
在 RTE 中，使用**编号列表**&#x200B;图标。

   如果您想要將現有內容變更為特定清單型別，請反白適當的文字並選取適當的清單型別。 如同先前顯示如何輸入段落文字的範例一樣，適當的清單元素會自動新增至您的HTML。

   在全屏模式下，单个&#x200B;**项目符号列表**&#x200B;和&#x200B;**编号列表**&#x200B;图标可见。 当不处于全屏模式时，这两个选项在单个&#x200B;**列表**&#x200B;图标的后面可用。

* **表**：数据表必须使用 HTML 表元素进行标识：
   * 一个 `<table>` 元素
   * 每个表行均使用 `<tr>` 元素进行标识
   * 每个行标题和列标题均使用 `<th>` 元素进行标识
   * 每个数据单元格均使用 `<td>` 元素进行标识

   此外，可存取的表格會使用下列元素和屬性：

   * `<caption>` 元素用于为表提供可视描述。默认情况下，描述显示在表上方居中的位置，但是可以使用 CSS 相应地调整位置。描述采用编程方式与表相关联，因此这是一种提供内容简介的有用方法。
   * `<summary>` 元素通过总结视力正常的用户可以看到的内容，帮助失明的用户更加轻松地了解表中提供的信息。這在使用了複雜或非常規表格佈局的情況下很有用（此屬性不會顯示在瀏覽器中，只會由輔助技術讀取）。
   * `<th>` 元素的 `scope` 属性用于指示某个单元格表示特定行的标题，还是特定列的标题。在复杂的表中，即数据单元格可能与一个或多个标题相关联的情况下，类似的方法是使用标题和 id 属性。

   >[!NOTE]
   >
   >依預設，這些元素和屬性不直接可用，但系統管理員可以在以下位置新增對這些值的支援： **表格屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes).

   若要開啟 **表格** 對話方塊，您可在其中選取 **表格屬性** 標籤：

   * 定義適當的 **註解**.
   * 理想情况下，请删除 **Width**、 **Height**、Border **、** Border Border Sell PaddingSpacing **、****** Cell Spacing的默认值。 因为这些属性可以在全局样式表中设置。

   然後，您可以使用 **儲存格屬性** 若要選擇儲存格是資料或標題儲存格：

* **强调**：使用 `<strong>` 或 `<em>` 元素指示要强调的内容。切勿在段落中使用标题突出显示文本。
   * 突出显示要强调的文本；
   * 按一下 **B** 圖示(for `<strong>`)或 **I** 圖示(for `<em>`)內顯示 **屬性** 面板(請確定已選取HTML)。

      >[!NOTE]
      >
      >标准 AEM 安装中的 RTE（富文本编辑器）设置为：
      >
      >* `<b>`对象`<strong>`
      >* `<i>`对象`<em>`

      >
      >尽管两种形式效果相同，但是最好使用 `<strong>` 和 `<em>`，因为从语义上来讲，它们才是正确的 HTML 标记。开发团队在开发项目实例时，可以将 RTE 配置为使用 `<strong>` 和 `<em>`（而非 `<b>` 和 `<i>`）。

* **複雜資料表**：有時候，如果有具有兩個或多個標題層級的複雜表格，則基本表格屬性可能不足以提供所有必要的結構資訊。 對於這些型別的複雜表格，必須在標題與其相關儲存格之間使用 **頁首** 和 **id** 屬性。

   >[!NOTE]
   >
   >ID屬性無法在現成可用的安裝中使用。 可透過設定HTML規則和RTE中的序列化程式來啟用。

   例如，在下表中，标题和 ID 是相匹配的，以便为辅助型技术用户建立程序化关联。

   ```xml
     <table>
       <tr>
         <th rowspan="2" id="h">Homework</th>
         <th colspan="3" id="e">Exams</th>
         <th colspan="3" id="p">Projects</th>
       </tr>
       <tr>
         <th id="e1" headers="e">1</th>
         <th id="e2" headers="e">2</th>
         <th id="ef" headers="e">Final</th>
         <th id="p1" headers="p">1</th>
         <th id="p2" headers="p">2</th>
         <th id="pf" headers="p">Final</th>
       </tr>
       <tr>
         <td headers="h">15%</td>
         <td headers="e e1">15%</td>
         <td headers="e e2">15%</td>
         <td headers="e ef">20%</td>
         <td headers="p p1">10%</td>
         <td headers="p p2">10%</td>
         <td headers="p pf">15%</td>
       </tr>
     </table>
   ```

   要在 AEM 中实现此操作，使用源代码编辑模式直接添加标记。

   >[!NOTE]
   >
   >在標準安裝中，此功能無法立即使用。 它需要設定RTE、HTML規則和序列化程式。

#### 更多信息 – 信息和关系 (1.3.1) {#more-information-info-and-relationships}

* [了解成功标准 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何达到成功标准 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意义的顺序 (1.3.2)  {#meaningful-sequence}

* 成功标准 1.3.2
* A 级
* 有意义的顺序：当内容的呈现顺序会影响内容含义时，可以通过编程方式确定正确的阅读顺序。

#### 用途 – 有意义的顺序 (1.3.2) {#purpose-meaningful-sequence}

此成功标准旨在使用户代理既能够提供内容的替代呈现方式，同时还能保留理解内容含义所需的阅读顺序。能够以编程方式确定至少一个有意义的内容呈现顺序，这一点很重要。当辅助技术以错误的顺序阅读内容，或者在应用替代样式表或其他格式更改时，不符合此成功标准的内容可能会使用户感到困惑或是不知所措。

#### 如何达到标准 – 有意义的顺序 (1.3.2) {#how-to-meet-meaningful-sequence}

遵循[如何达到成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence) 中的准则。

#### 更多信息 – 有意义的顺序 (1.3.2) {#more-information-meaningful-sequence}

* [了解成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何达到成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特性 (1.3.3)  {#sensory-characteristics}

* 成功标准 1.3.3
* A 级
* 感官特性：提供理解和操作內容的指示，並不只依賴元件的感官特性，例如形狀、大小、視覺位置、方向或聲音。

#### 用途 — 感官特性(1.3.3) {#purpose-sensory-characteristics}

设计者往往关注可视设计特征，如颜色、形状、文本样式，或者内容在展示信息时所在的绝对或相对位置。在传达信息方面，这些可能是强大的设计技术（可以改善具有认知无障碍需求的视力正常用户的整体无障碍体验），但是失明或患有视觉障碍的用户可能无法访问需要视觉识别属性（例如位置、颜色或形状）的信息。

同樣地，如果音訊內容沒有反映在任何替代文字中，需要區分不同聲音（例如，男性或女性講話的內容）的資訊會讓有聽覺障礙的人遇到協助工具障礙。

>[!NOTE]
>
>有關替代顏色的需求，請參閱 [使用顏色](#use-of-color).

#### 如何達到標準 — 感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

請確定任何依賴頁面內容視覺特性的資訊也會以替代格式呈現。

* 不要依賴視覺位置來提供資訊。 例如，如果希望用户通过页面右侧的菜单访问更多信息，那么请不要只提及&#x200B;*右侧的菜单*；而是要为该菜单命名（例如，通过标题进行命名），然后以文本方式提及该名称。
* 切勿将文本样式（例如，粗体或斜体文本）作为传递信息的唯一方式。

>[!NOTE]
>
>若在非視覺內容中理解描述性辭彙的意義，則可使用描述性辭彙。 例如，使用 *以上* 和 *以下* 通常可以接受，因為它們分別表示特定內容專案之前和之後的內容；當朗讀內容時，這仍然有意義。

#### 更多信息 - 感官特性 (1.3.3) {#more-information-sensory-characteristics}

* [了解成功标准 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何达到成功标准 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分：讓使用者更容易檢視和聆聽內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG/#distinguishable)

### 使用色彩(1.4.1)  {#use-of-color}

* 成功标准 1.4.1
* A 级
* 使用色彩：色彩不是傳達資訊、指示動作、提示回應或區分視覺元素的唯一視覺方式。

>[!NOTE]
>
>此成功標準特別針對色彩感知。 其他形式的認知包含在 [可調整(1.3)](#adaptable)；包括程式化存取顏色和其他視覺化簡報編碼。

#### 用途 — 使用顏色(1.4.1) {#purpose-use-of-color}

颜色能够有效地增强网页的美感，而且还有助于传递信息。但是，由于各种视觉障碍（从失明到色盲）的限制，部分用户无法辨认某些颜色。这就使颜色编码无法可靠地提供信息。

例如，有紅 — 綠色覺缺陷的人將無法區分綠色陰影和紅色陰影。 这些用户可能会将这两种颜色看成第三种颜色（如棕色），在这种情况下，他们就无法辨认红色、绿色和棕色。

此外，如果用户使用仅支持文本的浏览器、单色显示设备或查看黑白打印的页面，他们也无法感知到颜色。

進一步考量是 *已選取* 介面元素的狀態（例如，標籤、切換按鈕等），除了使用顏色和視覺呈現方式外，必須以其他某種方式傳遞。 对于这些元素，在创建不依赖特定感官的全包容用户体验时，额外使用图案、形状和编程信息将很有帮助。

#### 如何达到标准 – 使用颜色 (1.4.1) {#how-to-meet-use-of-color}

无论在何处使用颜色传递信息，都应确保无需看到颜色即可获取相应的信息。

例如，确保通过颜色传递的信息也明确地提供在文本中。

如果颜色用作提供信息的线索，则还应该提供其他可视线索，如更改样式（例如，粗体、斜体）或者字体。 这样可以帮助弱视或色盲的用户识别信息。但是，不能完全依赖这种方法，因为这对于根本无法看到页面的用户而言并无助益。因此，提供隐藏文本或使用编程解决方案（例如 [Web 标准的无障碍的富因特网应用程序 (ARIA) 套件](https://www.w3.org/WAI/standards-guidelines/aria/)）将此信息传递给失明用户将（有时）非常有用。

#### 更多信息 – 使用颜色 (1.4.1) {#more-information-use-of-color}

* [了解成功标准 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何达到成功标准 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音频控制 (1.4.2)  {#audio-control}

* 成功标准 1.4.2
* A 级
* 音频控制：如果网页上的任何音频自动播放超过 3 秒，则要么有一种机制可用来暂停或停止音频播放，要么有一种独立于整体系统音量控制的机制可用来调控音频音量。

#### 用途 – 音频控制 (1.4.2) {#purpose-audio-control}

如果同时还有其他音频正在播放，则使用屏幕阅读软件的用户可能会难以听清语音输出。尤其是当屏幕阅读器的语音输出是基于软件的（现今大多数都是如此），并且是通过与系统声音相同的音量控制来调控时，这种困难就会加剧。此外，一些患有认知障碍和神经系统障碍的用户可能对声音敏感。这些用户认为无法更改音频内容的音量将会造成干扰。

因此，用户能够关闭背景声音是非常重要的。

>[!NOTE]
>
>控制音量包括能够将音量减小到零。

#### 如何达到标准 – 音频控制 (1.4.2) {#how-to-meet-audio-control}

遵循[如何达到成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control) 中的准则。

#### 更多信息 – 音频控制 (1.4.2) {#more-information-audio-control}

* [了解成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何达到成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 对比度（最小）(1.4.3) {#contrast-minimum}

* 成功标准 1.4.3
* AA 级
* 對比（最小）：文字的視覺化呈現和影像的對比率至少為4.5:1，以下除外：
   * 大型文字：大型文字與大型文字影像的對比率至少為3:1。
   * 附屬專案：文字或文字影像屬於非使用中使用者介面元件的一部分， [純裝飾](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，對任何人都不可見，或是包含其他重要視覺內容的圖片的一部分，則不需要對比。
   * 商标标志：文本是徽标或品牌名称的一部分，对于此类文本，没有最低对比度要求。

   >[!NOTE]
   >
   >请参阅[了解非文本对比度](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)获取更多详细信息，从而帮助确保内容作者了解有关非文本元素（包括图标、界面元素等）的其他要求。

#### 用途 – 对比度（最小）(1.4.3) {#purpose-contrast-minimum}

有某些視覺障礙的人可能無法分辨某些低對比的顏色配對。 如果出现以下任一情况，此类用户便可能遇到无障碍问题：

* 文本与其背景颜色之间的对比度极低。
* 文字（例如連結文字和非連結文字）的色彩編碼對於辨別資訊非常重要。

>[!NOTE]
>
>純粹用於裝飾目的的文字會從此成功標準中排除。

#### 如何達到標準 — 對比（最小） (1.4.3) {#how-to-meet-contrast-minimum}

請確定文字與其背景的對比度已足夠。 對比率視相關文字的大小和樣式而定：

* 对于大小小于 18 点（或粗体为小于 14 点）的文本，文本中的文字/图像与背景之间的对比度至少应为 4.5:1。
* 對於大小至少為18點（或粗體為14點）的文字，對比率應至少為3:1。
* 如果陣列化背景，則任何文字周圍的背景都應著色，以保持4.5:1或3:1的比例。

>[!NOTE]
>
>請記住，字型在呈現等同的PT/PX/EM大小的方式上可能有所不同。
>
>為網頁內容選擇適當的字型與大小時，請在可讀性與可用性方面做出良好的判斷與錯誤。

>[!NOTE]
>
>以下网站可以帮助您转换到其他单位：
>
>* [Px到Em電腦 — Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* 請參閱「Font size conversion： pixel-point-em-rem-percent」，網址為 `https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/`
>* 請參閱PMtoEM.com：PX到EM的轉換非常簡單，請前往 `http://pxtoem.com/`


要检查对比度，可使用颜色对比度工具，例如 [Paciello Group Color Contrast Analyzer](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM Color Contrast Checker](https://webaim.org/resources/contrastchecker/)。這些工具可讓您檢查顏色配對，並報告任何對比問題。

或者，如果您不太在意頁面外觀的指定，則可以選擇不指定背景和前景文字顏色。 在这种情况下，无需检查对比度，因为用户的浏览器会确定文本和背景的颜色。

如果無法滿足建議的對比等級，請提供替代對等版本頁面的連結（沒有色彩對比問題）。 或者，讓使用者根據自己的需求調整頁面色彩配置的對比。

#### 更多信息 - 对比度（最小）(1.4.3) {#more-information-contrast-minimum}

* [了解成功标准 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何达到成功标准 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 调整文本大小 (1.4.4)  {#resize-text}

* 成功标准 1.4.4
* A 级
* 调整文本大小：除了文本的字幕和图像之外，在不使用辅助技术的情况下，文本大小最多可放大 200%，且不会丢失内容或功能。

#### 用途 – 调整文本大小 (1.4.4) {#purpose-resize-text}

此成功标准旨在确保成功缩放视觉呈现的文本，包括基于文本的控件（已显示出来供用户查看的文本字符，[与仍以 ASCII 等数据格式表示的文本字符]），以便具有轻微视觉障碍的用户可以直接阅读相关内容，而无需使用屏幕放大镜等辅助技术。网页上的所有内容都能缩放，这一点或许能够让用户受益，但文本是最关键的。

#### 如何达到标准 – 调整文本大小 (1.4.4) {#how-to-meet-resize-text}

除了遵循以下指南之外 [如何達到成功標準1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 您可以鼓勵內容作者在其頁面設計和字型大小（例如Responsive Web Design）中使用不固定、彈性的寬度和高度，讓讀者能夠調整文字大小。

#### 更多信息 – 调整文本大小 (1.4.4) {#more-information-resize-text}

* [了解成功标准 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何达到成功标准 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文本的图像 (1.4.5) {#images-of-text}

* 成功标准 1.4.5
* AA 级
* 文本的图像：如果使用的技术可以达到可视呈现效果，使用文本来传递信息而不使用文本的图像，以下情况除外：
   * 可自訂：可視地根據使用者的需求自訂文字影像；
   * 基本：文字的特定呈現方式對於傳遞的資訊至關重要。

>[!NOTE]
>
>標誌型別（屬於標誌或品牌名稱的文字）被認為是必要的。

#### 用途 — 文字影像(1.4.5) {#purpose-images-of-text}

当需要文本的某种特定样式时，通常会使用文本的图像；例如，商标标志或从其他来源生成的文本（如纸质文档的扫描件）。 然而，與以HTML呈現並使用CSS設定樣式的文字相比，文字的影像在變更大小或外觀方面缺乏彈性，而這對於視覺障礙或閱讀困難的人可能是必要的。

#### 如何達到標準 — 文字影像(1.4.5) {#how-to-meet-images-of-text}

如果必须使用文本的图像，应使用 CSS 将文本的图像替换为 HTML 形式的对等文本，这样就可以对文本进行自定义。如需範例，請參閱 [C30：使用CSS以文字的影像取代文字，並提供使用者介面控制項以進行切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### 更多信息 - 文本的图像 (1.4.5) {#more-information-images-of-text}

* [了解成功标准 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何达到成功标准 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 准則2：可操作 {#principle-operable}

[准则 2：可操作 – 用户界面组件和导航必须可以操作。](https://www.w3.org/TR/WCAG/#operable)

### 无障碍键盘 (2.1) {#keyboard-accessible}

[准则 2.1 无障碍键盘：仅用键盘即可实现所有功能。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

此准则涉及的是，确保用户可以使用键盘访问所有功能。

### 键盘 (2.1.1)  {#keyboard}

* 成功标准 2.1.1
* A 级
* 键盘：内容的所有功能均可通过键盘接口操作，且不需要任何击键时间限制，除非底层功能需要依赖于用户的输入行为路径而非单纯依赖于用户最后输入的内容。

#### 用途 – 键盘 (2.1.1) {#purpose-keyboard}

此成功标准旨在确保在可能的情况下，通过键盘或键盘接口（以便使用替代键盘）来操作内容。对于视觉障碍人士（无法使用鼠标等需要手眼协作的设备的人），以及必须使用替代键盘或充当键盘模拟器的输入设备的人士而言，如果内容是可以通过键盘或替代键盘操作的，那么他们就能够操作这些内容。键盘模拟器包括语音输入软件、通过呼吸来操作的软件、屏幕键盘、扫描软件以及各种辅助技术和备用键盘。此外，视力欠佳的人也可能难以跟踪指针，如果可以通过键盘控制指针，他们会发现使用软件会容易得多（或者这是他们能够使用软件的唯一方法）。

#### 如何达到标准 – 键盘 (2.1.1) {#how-to-meet-keyboard}

遵循[如何达到成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard) 中的准则。

#### 更多信息 – 键盘 (2.1.1) {#more-information-keyboard}

* [了解成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何达到成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 无键盘陷阱 (2.1.2)  {#no-keyboard-trap}

* 成功标准 2.1.2
* A 级
* 无键盘陷阱：如果可以使用键盘接口将键盘焦点移动到页面的某个组件，则焦点应同样可以通过键盘接口的方式从该组件上移开；如果除了通过未修改的箭头、Tab 键或其他标准退出方法外，上述移开功能还需通过其他手段实现，则应告知用户将焦点移开的方法。

#### 用途 – 无键盘陷阱 (2.1.2) {#purpose-no-keyboard-trap}

此成功标准旨在确保内容不会&#x200B;*陷入*&#x200B;网页内容子部分中的键盘焦点内。当一个页面综合采用了多种格式以及使用插件或嵌入式应用程序渲染页面时，经常会出现这种问题。

有时，网页的功能会将焦点限制在内容的子部分（例如，模态对话框）。在这种情况下，您应该为用户提供一种方法，使其能够退出该内容的子部分（例如，按 ESC 键关闭模态对话框，或者使用“关闭”按钮关闭模态对话框）。

#### 如何达到标准 – 无键盘陷阱 (2.1.2) {#how-to-meet-no-keyboard-trap}

遵循[如何达到成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap) 中的准则。

#### 更多信息 – 无键盘陷阱 (2.1.2) {#more-information-no-keyboard-trap}

* [了解成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何达到成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 充足的时间 (2.2) {#enough-time}

[准则 2.2 充足的时间：为用户提供充足的时间来阅读和使用内容。](https://www.w3.org/TR/WCAG/#enough-time)

此准则涉及的是，确保用户有充足的时间来阅读内容并执行操作。

### 计时可调 (2.2.1)  {#timing-adjustable}

* 成功标准 2.2.1
* A 级
* 键盘：为用户提供充足的时间来阅读和使用内容。

#### 用途 – 计时可调 (2.2.1) {#purpose-timing-adjustable}

此成功标准旨在确保残障用户有尽可能充足的时间与 Web 内容交互。失明、视力欠佳、行动不便以及认知困难等残障人士，可能需要更多时间来阅读内容或执行在线填表等操作。如果 Web 功能是计时的，则某些用户难以在限制时间内完成所需的操作。这可能会导致他们无法访问相关服务。设计不限时功能将有助于残障人士成功完成这些操作。提供停用時間限制、自訂時間限制長度或在時間限制發生前要求更多時間的選項，有助於需要超過預期時間的使用者成功完成工作。 这些选项应按照对用户最有帮助的顺序列出。禁用时间限制是最优选项，其次是自定义时间限制长度，再次是在达到时间限制之前请求更多时间。

#### 如何达到标准 – 计时可调 (2.2.1) {#how-to-meet-timing-adjustable}

遵循[如何达到成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable) 中的准则。

#### 更多信息 – 计时可调 (2.2.1) {#more-information-timing-adjustable}

* [了解成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何达到成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暂停、停止、隐藏 (2.2.2)  {#pause-stop-hide}

* 成功标准 2.2.2
* A 级
* 暂停、停止、隐藏：对于移动、闪烁、滚动或自动更新的信息，符合以下情况：
   * 移动、闪烁、滚动：对于任何 (a) 自动启动，(b) 持续时间超过 5 秒钟，并 (c) 与其他内容并行呈现的移动、闪烁或滚动信息，提供了一个机制来允许用户执行暂停、停止或隐藏操作，除非移动、闪烁或滚动是某种行为的必需部分；
   * 自動更新：對於(a)自動開始且(b)與其他內容同時顯示的任何自動更新資訊，使用者有一種機制可以暫停、停止或隱藏該資訊，或是控制更新的頻率，除非自動更新是重要活動的一部分。

注意要点：

1. 有关闪烁或闪光内容的要求，请参阅切勿设计会导致癫痫发作的内容 (2.3)。
1. 由於任何不符合此成功標準的內容都會干擾使用者使用整個頁面的能力，網頁上的所有內容（無論是否用於滿足其他成功標準）都必須符合此成功標準。 请参阅[符合性要求 5：不干涉](https://www.w3.org/TR/WCAG20/#cc5)。
1. 軟體定期更新或串流至使用者代理程式的內容，不必保留或呈現暫停起始與繼續簡報之間產生或接收的資訊，因為這在技術上可能行不通，且在許多情況下這麼做可能會誤導使用者。
1. 如果所有使用者在該階段中無法進行互動，而且如果未指出進度，可能會讓使用者感到困惑或認為內容已凍結或中斷，則作為預先載入階段的一部分或類似情況發生的動畫可視為必要。

#### 用途 — 暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些用户可能会认为移动的内容会让人分心，甚至让人觉得难受，而且难以将注意力集中在页面的其他部分。此外，如果用户无法跟上移动的文本，他们可能就很难阅读此类内容。

#### 如何达到标准 - 暂停、停止、隐藏 (2.2.2) {#how-to-meet-pause-stop-hide}

如果创建的网页包含移动、闪光或闪烁的内容，则可以采纳以下一项或多项建议，具体视内容的性质而定。

* 提供一种可使滚动的内容暂停的方法，以便让用户有充足的时间进行阅读。例如，新闻滚动条、自动更新的文本以及自动推进的图像轮播。
* 确保闪烁的内容会在 5 秒钟后停止闪烁。
* 使用适当的技术来显示可由浏览器禁用的移动或闪烁内容。例如，Graphics Interchange Format (GIF) 或 Animated Portable Network Graphics (APNG) 文件。
* 在网页上提供一个表单控件，让用户能够禁用页面上的所有移动或闪烁内容。
* 如果以上建议均不可行，则可以提供一个链接，以指向包含所有内容但不含任何移动或闪烁内容的页面。

#### 更多信息 – 暂停、停止、隐藏 (2.2.2) {#more-information-pause-stop-hide}

* [了解成功标准 2.2.2](https://www.w3.org/WAI/WCAG21/Understanding/pause-stop-hide.html)
* [如何达到成功标准 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/#pause-stop-hide)

### 癫痫发作和生理反应 (2.3) {#seizures-and-physcial-reactions}

[准则 2.3 癫痫发作：切勿设计会导致癫痫发作或生理反应的内容。](https://www.w3.org/TR/WCAG/#seizures-and-physical-reactions)

### 闪光三次或低于阈值 (2.3.1) {#three-flashes-or-below-threshold}

* 成功标准 2.3.1
* A 级
* 闪光三次或低于阈值：网页不包含在任何一秒内闪光超过 3 次，或闪光低于一般闪光和红色闪光阈值的内容。

>[!NOTE]
>
>由于任何未达到此成功标准的内容会干涉用户使用整个页面的能力，因此网页上的所有内容（无论是否用来达到其他成功标准）必须达到此成功标准。请参阅[符合性要求 5：不干涉](https://www.w3.org/TR/WCAG/#cc5)。

#### 用途 – 闪光三次或低于阈值 (2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能會導致光敏性癲癇發作。 此成功標準可讓這類使用者存取及體驗所有內容，而不需擔心內容閃爍問題。

#### 如何達到標準 — 三個Flash或低於臨界值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

请采取措施确保应用以下技术：

* 确保组件在任何一秒内的闪光次数均不超过三次；
* 如果无法满足上述条件，则应在屏幕上以像素为单位将闪光的内容显示在&#x200B;*小块安全区域*&#x200B;内。此區域是使用複雜的公式來計算，涵蓋在 [G176：讓閃爍區域保持足夠小](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)，所以只有在需要*閃爍的內容時，才應使用此技巧。

#### 更多信息 – 闪光三次或低于阈值 (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [了解成功标准 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何达到成功标准 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可导航 (2.4) {#navigable}

[准则 2.4 可导航：提供帮助用户导航、查找内容并确定其位置的方法。](https://www.w3.org/TR/WCAG/#navigable)

此准则涉及的是，确保内容便于用户导航且简洁明了。

### 绕过块 (2.4.1)  {#bypass-blocks}

* 成功标准 2.4.1
* A 级
* 绕过块：提供一种机制，绕过多个网页上重复出现的内容块。

#### 用途 – 绕过块 (2.4.1) {#purpose-bypass-blocks}

此成功标准旨在让按顺序浏览内容的人更直接地访问网页的主要内容。网页和应用程序通常包含也会在其他页面或屏幕上显示的内容。重复出现的内容块示例包括但不限于：导航链接、标题图形、菜单和广告画面。就本规定而言，单个字词、短语或单个链接等较小的重复内容不被视为重复块。

#### 如何达到标准 – 绕过块 (2.4.1) {#how-to-meet-bypass-blocks}

遵循[如何达到成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks) 中的准则。

#### 更多信息 – 绕过块 (2.4.1) {#more-information-bypass-blocks}

* [了解成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何达到成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 页面带有标题 (2.4.2)  {#page-titled}

* 成功标准 2.4.2
* A 级
* 頁面標題：網頁的標題會說明主題或用途。

#### 用途 — 頁面有標題(2.4.2) {#purpose-page-titled}

此成功標準可協助每個人（無論是否有任何特定問題）快速識別網頁內容，而不需完整閱讀頁面。 当在不同的浏览器选项卡中打开了多个网页时，这种方法十分有用，因为页面标题会显示在选项卡中，从而可以快速定位。

#### 如何達到標準 — 頁面有標題(2.4.2) {#how-to-meet-page-titled}

在 AEM 中创建新 HTML 页面时，可以指定页面标题。应确保标题能够充分描述页面内容和用途，尤其是任何独特方面，以便访客能够快速识别该页面的内容是否与自己的需求相关。

您也可以在编辑页面时编辑页面标题，通过&#x200B;**页面信息** – **属性**&#x200B;可访问该设置。

#### 更多信息 – 页面带有标题 (2.4.2) {#more-information-page-titled}

* [了解成功标准 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何达到成功标准 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦点顺序 (2.4.3)  {#focus-order}

* 成功标准 2.4.3
* A 级
* 焦点顺序：如果网页可以按顺序依次导航并且导航顺序会影响含义或操作，则可聚焦组件应该按照不改变含义和可操作性的顺序接收焦点。

#### 用途 – 焦点顺序 (2.4.3) {#purpose-focus-order}

此成功标准旨在确保用户按顺序导航内容时，他们接收到信息的顺序与内容含义一致，并且这种按顺序导航的操作可通过键盘实现。此成功标准可让用户形成与内容一致的心智模型，从而减少混淆。内容中可能存在不同的反映逻辑关系的顺序。例如，在由多个字段和/或步骤组成的在线表单中移动组件反映了内容中的逻辑关系。

#### 如何达到标准 – 焦点顺序 (2.4.3) {#how-to-meet-focus-order}

遵循[如何达到成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order) 中的准则。

#### 更多信息 – 焦点顺序 (2.4.3) {#more-information-focus-order}

* [了解成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何达到成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 链接目的（在上下文中）(2.4.4)  {#link-purpose-in-context}

* 成功标准 2.4.4
* A 级
* 連結目的（在內容中）：每個連結的目的都可以單獨從連結文字中決定，或是從連結文字連同其程式決定的連結內容一起決定，除非連結的目的對於一般使用者來說模稜兩可。

#### 用途 — 連結用途（在內容中） (2.4.4) {#purpose-link-purpose-in-context}

對於所有使用者而言，無論是否有損毀，透過適當的連結文字清楚指出連結的方向是至關重要的。 这有助于用户决定自己是否切实希望追踪某个链接。對於視力正常的使用者，有意義的連結文字在頁面上有多個連結時非常有用（尤其是頁面含有大量文字時），因為有意義的連結文字可更清楚指示目標頁面的功能。 使用一些辅助型技术的用户可以在单个页面上生成所有链接的列表，如果链接文本是唯一的且可以提供有用信息，则用户可以轻松地脱离上下文理解链接文本。但是，如果链接无法提供足够的信息来准确描述链接目标位置，则患有认知障碍的视力正常用户可能会感到困惑。

#### 如何达到标准 – 链接目的（在上下文中）(2.4.4) {#how-to-meet-link-purpose-in-context}

首先，确保链接文本清晰地描述了链接目的。

* 错误示例：
   * 文本内容：有关 2010 年秋季晚间课程的详细信息，请单击此处。
   * 原因分析：没有清晰明确地指明链接目标位置。
* 正确示例：
   * 文本内容：2010 年秋季晚间课程 - 详细信息。
   * 原因：稍微調整文字和連結元素的位置，可以改善連結文字：

链接用词在各个页面中应保持一致，尤其是导航栏的链接。例如，如果特定页面的链接在某个页面中被命名为&#x200B;**出版物**，则在其他页面中也应使用该文本，以确保一致性。

编写文本时，在使用标题属性确保页面上呈现的类似链接提供有关目标位置的唯一信息方面还存在一些问题（例如，“阅读更多”通常是指一系列的不同目标位置）：

* 標題屬性中包含的文字僅供滑鼠使用者作為工具提示快顯視窗使用，且無法透過鍵盤或行動使用者一致地存取。
* 熒幕助讀程式可以讀取標題屬性，但此功能可能預設為未啟用；因此使用者可能不知道存在標題屬性。
* 變更標題文字的外觀很困難，這表示有些人可能難以或無法閱讀。

因此，雖然title屬性可用於為連結提供額外內容，請注意其限制，且請勿將其用作適當連結文字的替代方式。

如果链接是由图像构成的，则应确保该图像的替换文本描述了链接的目标位置。例如，如果将一个书架的图像设置为某人出版物的链接，则替换文本应该写成&#x200B;**张三的出版物**，而不是&#x200B;**书架**。

或者，如果連結錨點包含描述連結用途以及影像元素的文字（因此文字會出現在影像旁邊），請對影像使用空的alt屬性：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith's publications
</a>
```

>[!NOTE]
>
>以上代碼片段僅供說明之用，建議您使用 **影像** 元件。

雖然提供不需要額外內容即可識別連結目的的連結文字是明智之舉，但您不一定會認識到這一點。 与上下文无关的链接可用于以下情况，其 HTML 示例详见：[如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)。

* 連結文字是緊密相關連結清單的一部分，而且當連結周圍的清單專案提供足夠的內容時。
* 連結的目的可清楚識別，可於 *先前* （不是下列）段落文字。
* 連結包含在資料表中，因此可從相關標題中清楚識別用途。
* 連結清單包含在一組標題中，標題本身會提供適當的上下文。
* 巢狀連結內含連結清單，而巢狀連結上方的父清單專案會提供適當的內容。

有时，一个页面上会有多个链接（其中每个链接都提供了复杂而又必要的链接方向详情），此时可以为该网页提供一个替代版本，使其显示完全相同的内容，只是其中的链接文本较为简洁。

或者，使用指令碼，以便在連結本身中提供最少量的文字。 啟動位於頁面頂端的適當控制項時，連結文字會 *已展開* 以取得更詳細的資訊。 類似的方法是使用CSS *隱藏* 視力正常使用者的完整連結，但仍會以全熒幕閱讀器使用者的形式輸出。 這不屬於本檔案的範圍，但如需如何達成此目標的詳細資訊，請參閱 [更多資訊 — 連結目的（在內容中） (2.4.4)](#more-information-link-purpose-in-context) 區段。

#### 更多信息 – 链接目的（在上下文中）(2.4.4) {#more-information-link-purpose-in-context}

* [了解成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多种方式 (2.4.5)  {#multiple-ways}

* 成功标准 2.4.5
* AA 级
* 多种方式：除了按照流程或步骤正常来到网页之外，还有其他方法可用于在一组网页中来到所需网页。

#### 用途 – 多种方式 (2.4.5) {#purpose-multiple-ways}

此成功标准旨在让用户能够以最符合其需求的方式找到内容。用户可能会发现一种技术比另一种技术更易于使用或理解。

即便是小型网站，也应为用户提供一些不同的定位方式。对于只有三、四个页面的网站，如果所有页面均链接自主页，则只需在主页上提供所有页面的链接、以及在各自页面上提供前往主页的链接即可，而主页上的链接也可用作站点地图。

#### 如何达到标准 – 多种方式 (2.4.5) {#how-to-meet-multiple-ways}

遵循[如何达到成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways) 中的准则。

#### 更多信息 – 多种方式 (2.4.5) {#more-information-multiple-ways}

* [了解成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何达到成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 标题和标签 (2.4.6)  {#headings-and-labels}

* 成功标准 2.4.6
* AA 级
* 标题和标签：标题和标签用于描述主题或用途。

#### 用途 – 标题和标签 (2.4.6) {#purpose-headings-and-labels}

此成功标准旨在帮助用户了解网页中包含哪些信息以及这些信息的组织方式。当标题清晰且具有描述性时，用户可以更轻松地找到所寻找的信息，并且可以更轻松地了解内容不同部分之间的关系。描述性标签可帮助用户识别内容中的特定组件。

#### 如何达到标准 – 标题和标签 (2.4.6) {#how-to-meet-headings-and-labels}

遵循[如何达到成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels) 中的准则。

#### 更多信息 – 标题和标签 (2.4.6) {#more-information-headings-and-labels}

* [了解成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何达到成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦点可见 (2.4.7)  {#focus-visible}

* 成功标准 2.4.7
* AA 级
* 焦点可见：任何键盘可操作的用户界面都具有这样一种操作模式 - 键盘焦点指示器是可见的。

#### 用途 – 焦点可见 (2.4.7) {#purpose-focus-visible}

此成功标准旨在帮助用户了解当前的键盘焦点在哪个元素。

用户必须能够知道在多个元素中，哪一个元素是当前的键盘焦点所在。如果屏幕上只有一个键盘可操作控件，则应该可以达到成功标准，因为这样的视觉设计只会呈现一个键盘可操作项目。

成功标准中说的“操作模式”，则是考虑到了部分平台可能无法始终显示焦点指示器的情况。通常只有一種作業模式，因此此成功標準適用。

#### 如何达到标准 – 焦点可见 (2.4.7) {#how-to-meet-focus-visible}

遵循[如何达到成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible) 中的准则。

#### 更多信息 – 焦点可见 (2.4.7) {#more-information-focus-visible}

* [了解成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何达到成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 准则 3：可理解 {#principle-understandable}

[原則3：可理解 — 使用者介面的資訊和操作必須是可理解的。](https://www.w3.org/TR/WCAG/#understandable)

### 讓文字內容可讀可懂(3.1) {#make-text-content-readable-and-understandable}

[Guidelinate 3.1可讀取：讓文字內容可讀取且可理解。](https://www.w3.org/TR/WCAG/#readable)

### 頁面語言(3.1.1) {#language-of-page}

* 成功标准 3.1.1
* A 级
* 頁面語言：每個網頁的預設人類語言都可依程式決定。

#### 用途 — 頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準旨在確保文字和其他語言內容正確呈現。 對於熒幕助讀程式使用者，這可確保內容的發音正確，而視覺瀏覽器更有可能正確顯示特定字元集。

#### 如何達到標準 — 頁面語言(3.1.1) {#how-to-meet-language-of-page}

要达到此成功标准，可以使用页面顶部 `<html>` 元素中的 `lang` 属性来识别网页的默认语言。例如：

* 如果页面采用英语编写，则 `<html>` 元素应该写成：
   `<html lang = "en">`

* 而要以西班牙语呈现的页面应该采用以下标准：
   `<html lang = "es">`

在 AEM 中，页面的默认语言是在创建页面时设置的，但是也可以在编辑[页面属性](/help/sites-authoring/editing-page-properties.md)时进行更改。

>[!NOTE]
>
>AEM 针对根语言的变体做了进一步的微调，例如，美式英语 - en-us、英式英语 - en-gb 和加拿大英语 - en-ca。这种详细级别对辅助型技术来说通常是多余的，尽管它可以用于标识页面内容中的区域变化。

#### 更多信息 – 页面语言 (3.1.1) {#more-information-language-of-page}

* [了解成功标准 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何达到成功标准 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 這些程式碼以ISO 639-1為基礎。 如需每種語言的更詳盡程式碼清單，請參閱 [W3 Schools網站](https://www.w3schools.com/tags/ref_language_codes.asp).

### 區域性語言(3.1.2)  {#language-of-parts}

* 成功标准 3.1.2
* AA 级
* 部分語言：可程式化地決定內容中每個段落或片語的人類語言。 唯一例外的情況是專有名稱、技術術語、不定語言的單詞，以及成為緊鄰文字白話一部分的單字或短語。

#### 用途 — 區域性語言(3.1.2) {#purpose-language-of-parts}

此成功標準的用途與成功標準類似 [頁面語言](#language-of-page)，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引號或不常見的外來字）。

套用此成功標準的頁面允許：

* 用於插入重音字元的盲文轉換軟體。
* 屏幕阅读器朗读那些具有特殊字符或未使用在页面级别标识的默认语言的单词。
* Google Translate等翻譯工具可正確將內容從一種語言翻譯成另一種語言。

#### 如何達到標準 — 零件語言(3.1.2) {#how-to-meet-language-of-parts}

`lang` 属性可用于标识内容语言的更改。例如，引用的德语（ISO 639-1 代码“de”）可以采用以下方式表示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>現成可用的執行個體不支援區塊引號。 可開發自訂元件以支援該功能。

同样，如果通过以下方式使用 `span` 元素，则浏览器可以准确地呈现不常见的外来词或短语：

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>納入不同語言的人名或城市時，不必遵循此成功標準。或者，使用預設語言中常用的外來字詞或短語時，例如 *幸災樂禍* 英文版。

要添加包含相应语言的 span 元素，可以在 RTE 的源代码编辑模式下手动编辑 HTML 标记，以将其写成如上显示的方式。或者，也可以由系统管理员将 `lang` 属性添加到 RTE 中（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

#### 更多信息 – 局部语言 (3.1.2) {#more-information-language-of-parts}

* [了解成功标准 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何达到成功标准 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可预测 (3.2) {#predictable}

[准则 3.2 可预测：使网页以可预见的方式显示和操作。](https://www.w3.org/TR/WCAG/#predictable)

此准则涉及的是，确保网页的外观与操作保持一致。

### 聚焦 (3.2.1)  {#on-focus}

* 成功标准 3.2.1
* A 级
* 聚焦：当任何用户界面组件收到焦点时，它不会发起对上下文的更改。

#### 用途 – 聚焦 (3.2.1) {#purpose-on-focus}

此成功标准旨在确保访客在以自己的方式浏览文档时，功能是可预测的。任何能够在收到焦点时触发事件的组件，均不得更改上下文。组件收到焦点时更改上下文的示例，包括但不限于：

* 组件收到焦点时自动提交表单；
* 组件收到焦点时启动新窗口；
* 组件收到焦点时，焦点转移到另一个组件；

焦點可以透過鍵盤（例如，按Tab鍵移至控制項）或滑鼠（例如，按一下文字欄位）移至控制項。 将鼠标移到控件上方不会移动焦点，除非脚本会实施此行为。對於某些型別的控制項，按一下控制項也可以啟動控制項（例如按鈕），這反過來又可以在前後關聯中啟動變更。

#### 如何达到标准 – 聚焦 (3.2.1) {#how-to-meet-on-focus}

遵循[如何达到成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus) 中的准则。

#### 更多信息 – 聚焦 (3.2.1) {#more-information-on-focus}

* [了解成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何达到成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 输入 (3.2.2)  {#on-input}

* 成功标准 3.2.2
* A 级
* 输入：更改任何用户界面组件的设置，不会自动导致上下文更改，除非在使用组件之前，已告知用户该行为。

#### 用途 – 输入 (3.2.2) {#purpose-on-input}

此成功标准旨在确保输入数据或选择表单控件这样的操作具有可预见的效果。更改任何用户界面组件的设置，就会更改该控件的某些方面，当用户不再与界面交互时，这些方面的更改会一直存在。因此，选中复选框、在文本字段中输入文本，或更改列表控件中的选定项会更改其设置，但激活链接或按钮则不会更改其设置。上下文更改可能会给那些不容易感知更改或容易被更改分散注意力的用户造成困惑。只有当明确告知为响应用户操作而会发生上下文更改时，此类更改才是恰当的。

#### 如何达到标准 – 输入 (3.2.2) {#how-to-meet-on-input}

遵循[如何达到成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input) 中的准则。

#### 更多信息 – 输入 (3.2.2) {#more-information-on-input}

* [了解成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何达到成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致的导航 (3.2.3)  {#consistent-navigation}

* 成功标准 3.2.3
* AA 级
* 一致的导航：在一组网页内的多个网页上重复应用的导航机制，这些网页每次均以相同的相对顺序重复出现，除非用户自发更改浏览顺序。

#### 用途 – 一致的导航 (3.2.3) {#purpose-consistent-navigation}

此成功標準旨在鼓勵使用者使用一致的呈現和版面配置，以便與一組網頁內的重複內容互動，且必須找到特定資訊或功能超過一次。 视力欠佳的人使用屏幕放大功能每次显示屏幕的一小部分时，通常会使用视觉提示和页面边界来快速找到重复内容。对于使用空间记忆或设计中的视觉提示来找到重复内容的视觉用户而言，按相同顺序呈现重复内容也非常重要。

请务必注意，本节中使用了“相同顺序”这种说法，这并不意味着不能使用子导航菜单，或者不能使用二级导航块或页面结构。反之，此成功標準旨在協助使用者與整個網頁的重複內容互動，以便預測其所尋找內容的位置。 而且，當他們再次遇到時可以更快速地找到它。

用户可以通过使用自适应用户代理或通过设置首选项来发起顺序更改，以对他们最有用的方式呈现信息。

#### 如何达到标准 – 一致的导航 (3.2.3) {#how-to-meet-consistent-navigation}

遵循[如何达到成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation) 中的准则。

#### 更多信息 – 一致的导航 (3.2.3) {#more-information-consistent-navigation}

* [了解成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何达到成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致的标识 (3.2.4)  {#consistent-identification}

* 成功标准 3.2.4
* A 级
* 一致的标识：一组网页内具有相同功能的组件，均采用一致的方式进行标识。

#### 用途 – 一致的标识 (3.2.4) {#purpose-consistent-identification}

此成功标准旨在确保采用一致的方式标识一组网页内重复出现的功能组件。使用屏幕阅读器的用户在操作网站时所使用的一种策略是，依赖他们对可能出现在不同网页上的功能的熟悉程度，且这种依赖程度很深。如果相同的功能在不同网页上具有不同的标签（或者更通俗地讲，具有不同的访问名称），则网站的使用难度会显著增加。这也可能会令人困惑，并增加认知困难人士的认知负担。因此，一致的标签会有所帮助。

此一致性要求的适用范围也包括替换文本。如果图标或其他非文本项目具有相同的功能，则其相应的替换文本也应保持一致。

如果某个网页上有两个组件的功能与一组网页内另一个页面上的组件功能相同，则所有这 3 个组件都必须保持一致。因此，同一页面上的那两个组件将保持一致。

尽管在单个网页内始终保持一致是理想的最佳做法，但准则 3.2.4 仅解决一组网页内的一致性问题（该组网页内的多个页面上包含重复出现的某些内容）。

#### 如何达到标准 – 一致的标识 (3.2.4) {#how-to-meet-consistent-identification}

遵循[如何达到成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification) 中的准则。

#### 更多信息 – 一致的标识 (3.2.4) {#more-information-consistent-identification}

* [了解成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何达到成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 辅助输入 (3.3) {#input-assistance}

[准则 3.3 辅助输入：帮助用户避免和更正错误。](https://www.w3.org/TR/WCAG/#input-assistance)

### 错误标识 (3.3.1)  {#error-identification}

* 成功标准 3.3.1
* A 级
* 错误标识：如果自动检测到输入错误，则会识别出错的项目，并以文本形式向用户描述该错误。

#### 用途 – 错误标识 (3.3.1) {#purpose-error-identification}

此成功标准旨在确保用户知道发生了错误，并可确定错误的具体内容。错误消息应尽可能具体和明确。如果表單提交失敗，重新顯示表單並指示錯誤的欄位，不足以讓某些使用者察覺已發生錯誤。 例如，屏幕阅读器用户在遇到某个指示器之前，不会知道内容中存在错误。他们可能会在遇到错误指示器之前就完全放弃表单，认为页面根本无法正常工作。根据 WCAG 中的定义，[输入错误](https://www.w3.org/TR/WCAG/#dfn-input-error)是用户提供的不可接受的信息。這包含下列專案。

網頁需要但使用者省略的資訊，或使用者提供但超出所需資料格式或允許值的資訊。
例如：

* 使用者無法在州、省或地區欄位中輸入適當的縮寫；
* 用户输入的不是有效的省/自治区/直辖市缩写；
* 使用者輸入的郵遞區號不存在；
* 用户输入的出生日期在未来 2 年之后；
* 用户在只接受数字的电话号码字段中输入字母字符或括号；
* 用户输入的竞价低于上一个竞价或最低竞价增幅。

#### 如何达到标准 – 错误标识 (3.3.1) {#how-to-meet-error-identification}

遵循[如何达到成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification) 中的准则。

#### 更多信息 – 错误标识 (3.3.1) {#more-information-error-identification}

* [了解成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何达到成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 标签或说明 (3.3.2) {#labels-or-instructions}

* 成功标准 3.3.2
* A 级
* 標籤或指示：內容需要使用者輸入時，會提供標籤或指示。

#### 用途 — 標籤或指示(3.3.2) {#purpose-labels-or-instructions}

提供指示以幫助人們完成表單是介面可用性良好做法的基本部分。 这种做法对于患有视觉障碍或认知障碍的用户而言十分有用，否则这类用户可能难以理解表单的布局以及要在特定的表单字段中提供的数据种类。

##### Forms

在 AEM WKND 演示项目中，当向页面添加表单组件（如&#x200B;**文本字段**）时，会添加默认标签。此默认标题取决于组件类型。您也可以在该字段编辑对话框的&#x200B;**标题与文本**&#x200B;选项卡中添加自己的标题。应务必确保标签能够帮助用户理解与每个表单组件相关的数据。

此 **標題** 欄位必須用於欄位元素，因為它提供可用於輔助技術的標籤。 僅在該欄位旁的文字中寫入標籤是不夠的。

对于某些表单组件，还可以使用&#x200B;**隐藏标题**&#x200B;复选框以可视方式隐藏标签。以这种方式隐藏的标签仍然可用于辅助技术，但不会显示在屏幕上。雖然這在某些情況下可能是不錯的方法，但最好儘可能加入視覺標籤，因為有些使用者可能會看到畫面的一小部分（一次看一個欄位），並需要標籤才能正確識別欄位。

###### 图像按钮 {#image-buttons}

使用影像按鈕的位置(例如， **影像按鈕** 元件)、WKND專案的 **標題** 中的欄位 **標題和文字** 「編輯」對話方塊的tab實際上會提供影像的替代文字，而不是標籤。 因此，在以下示例中，包含文本 `Submit` 的图像，其替换文本就是 `Submit`，该文本是使用编辑对话框中的&#x200B;**标题**&#x200B;字段添加的。

###### 表单字段组 {#groups-of-form-fields}

在 WKND 项目中，如果存在一组相关控件（如&#x200B;**单选按钮组**），则可能需要该组以及单个控件的标题。在 AEM 中添加一组单选按钮时，**标题**&#x200B;字段会提供此组标题，而单个标题会在创建单选按钮（**项目**）时指定。

但是，组标题和单选按钮本身之间并没有编程关联。範本編輯器必須將標題包裝在必要欄中 `fieldset` 和 `legend` 標籤來建立此關聯，而這只能透過編輯頁面原始碼來完成。 或者，系統管理員可以新增對這些元素的支援，以使它們出現在 **欄位屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

###### 有关 Forms 的其他考虑事项 {#additional-considerations-for-forms}

如果必须按照特定的格式输入数据，应在标签文本中予以清楚说明。例如，如果必须以 `DD-MM-YYYY` 格式输入日期，应在标签中特别指明这一点。這表示當熒幕助讀程式的使用者遇到該欄位時，會自動公告標籤，以及關於格式的其他資訊。

如果必须输入表单字段，请在标签中使用“必填”一词来说明。AEM 会为必填字段添加一个星号，但是最好在标签本身中也包含 `required` 一词（在编辑对话框的&#x200B;**标题**&#x200B;字段中）。

標籤的位置也很重要，因為這有助於他們找到適當的欄位。 當使用者面對複雜表單時，這尤其重要。 請遵循下列慣例：

* 复选框或单选按钮：
标签放在紧靠字段右侧的位置。
* 所有其他表单组件（例如，文本框和组合框）：
标签放在紧靠字段上方或左侧的位置。

在功能有限的簡單表單中，適當地標示 `Submit` 按鈕可作為相鄰欄位的標籤(例如 `Search`)。 在尋找標籤文字的空間可能困難的情況下，這個用法很有用。

#### 更多資訊 — 標籤或指示(3.3.2) {#more-information-labels-or-instructions}

* [了解成功标准 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何达到成功标准 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 错误建议 (3.3.3)  {#error-suggestion}

* 成功标准 3.3.3
* AA 级
* 键盘：如果自动检测到输入错误并且知道有关更正的建议，则向用户提供建议，除非这会危及内容的安全性或用途。

#### 用途 – 错误建议 (3.3.3) {#purpose-error-suggestion}

此成功标准旨在确保用户在可能的情况下接收合理建议以便更正输入错误。在 WCAG 中，[输入错误](https://www.w3.org/TR/WCAG/#dfn-input-error)的定义是指系统“不接受的用户提供的信息”。系统不接受的信息示例包括：要求提供但用户忽略了的信息，以及用户虽已提供但不是要求的数据格式或允许的值。

成功标准 3.3.1 会提供错误通知。然而，认知困难的人士可能很难理解如何更正错误。患有视觉障碍的人士可能无法明白到底应该如何更正错误。如果表单提交失败，用户或许会放弃表单，因为他们可能不确定如何更正错误，即使他们知道已经发生错误。

内容作者可以提供错误描述，或者用户代理可以根据特定于技术的、通过编程方式确定的信息来提供错误描述。

#### 如何达到标准 – 错误建议 (3.3.3) {#how-to-meet-error-suggestion}

遵循[如何达到成功标准 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion) 中的准则。

#### 更多信息 – 错误建议 (3.3.3) {#more-information-error-suggestion}

* [了解成功标准 3.3.3](https://www.w3.org/WAI/WCAG21/Understanding/error-suggestion.html)
* [如何达到成功标准 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion)

### 错误预防（法律、金融、数据）(3.3.4)  {#error-prevention-legal-financial-data}

* 成功标准 3.3.4
* AA 级
* 错误预防（法律、金融、数据）：对于用户操作将产生法律承诺或财务交易的网页，会修改或删除数据存储系统中用户可控数据的网页，或者会交用户测试响应的网页，以下至少有一项为真：

   * 可撤销
提交的信息是可以撤销的。
   * 已检查
检查用户输入的数据是否有输入错误，并为用户提供一次更正错误的机会。
   * 已确认
提供一种机制，用于在最终提交之前复核、确认和更正信息。

#### 用途 – 错误预防（法律、金融、数据）(3.3.4) {#purpose-error-prevention-legal-financial-data}

此成功标准旨在帮助残障用户在执行无法撤销的操作时，避免因错误而造成严重后果。例如，购买不可退款的机票，或者提交订单在经纪帐户中购买股票，这些都是可能产生严重后果的金融交易。如果用户弄错航空旅行日期，他们最终可能会拿到一张无法改签的日期错误的机票。如果用户在要购买的股票数量上出错，他们最终可能会购买超出预期数量的股票。這兩種代價高昂的錯誤都會涉及立即發生且事後無法變更的交易。 同樣地，如果使用者無意中修改或刪除了儲存在資料庫中但之後必須存取的資料（例如旅行服務網站中自己的整個旅行設定檔），也可能是無法復原的錯誤。 当涉及修改或删除“用户可控”数据时，此项标准的目的是防止大量丢失数据，例如删除一份文件或记录，而不是要求在每次保存命令时进行确认，也不是指对文档、记录或其他数据进行简单的创建或编辑。

残障用户可能更容易出错。患有阅读障碍的人可能会颠倒数字和字母，而患有运动障碍的人则可能会意外按错按键。提供撤销操作这一功能，让用户能够纠正可能导致严重后果的错误。提供复核和更正信息这一功能，让用户在采取可能会造成严重后果的行动之前，有机会及时发现错误。

用户可控数据是指用户可查看的数据，用户可以通过有意的操作来改变和/或删除这些数据。用户控制此类数据的示例可能包括：更新用户帐户的电话号码和地址，或者从网站删除过去发票的记录。它不是指用户无法直接查看或与之交互的数据，例如互联网日志记录和搜索引擎监测数据。

#### 如何达到标准 – 错误预防（法律、金融、数据）(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

遵循[如何达到成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data) 中的准则。

#### 更多信息 – 错误预防（法律、金融、数据）(3.3.4) {#more-information-error-prevention-legal-financial-data}

* [了解成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何达到成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 准则 4：强健 {#principle-robust}

[准则 4：强健 – 内容必须足够强健，以供包括辅助技术在内的各种用户代理进行解读。](https://www.w3.org/TR/WCAG/#robust)

### 可兼容 (4.1) {#compatible}

[准则 4.1 兼容：最大限度地兼容当前和未来用户代理，包括辅助技术。](https://www.w3.org/TR/WCAG/#compatible)

最大限度地兼容当前和未来用户代理，包括辅助技术。

### 解析 (4.1.1)  {#parsing}

* 成功标准 4.1.1
* A 级
* 解析：在使用标记语言实施的内容中，元素具有完整的开始和结束标签，元素根据其规范进行嵌套，元素不包含重复属性，所有 ID 都是唯一的，除非规范允许。

#### 用途 – 解析 (4.1.1) {#purpose-parsing}

此成功标准旨在确保用户代理（包括辅助技术）能够准确地解读和分析内容。如果内容无法解析为数据结构，则不同的用户代理可能会以不同的方式呈现内容，或者无法解析内容。一些用户代理会使用“修复技术”来呈现编码欠佳的内容。

由於修復技術因使用者代理而異，作者無法假設內容已正確剖析為資料結構，或內容將由專業使用者代理（包括輔助技術）正確呈現，除非內容是根據該技術的正式文法中定義的規則所建立。 在标记语言中，元素和属性语法中的错误以及未提供正确嵌套的开始/结束标签，会导致使用户代理无法可靠地解析内容的错误。因此，成功标准要求内容只能使用正式语法的规则来解析。

#### 如何达到标准 – 解析 (4.1.1) {#how-to-meet-parsing}

遵循[如何达到成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing) 中的准则。

#### 更多信息 – 解析 (4.1.1) {#more-information-parsing}

* [了解成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何达到成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名称、角色、值 (4.1.2)  {#name-role-value}

* 成功标准 4.1.2
* A 级
* 名称、角色、值：对于所有用户界面组件(包括但不限于：表单元素、链接以及由脚本生成的组件)，其名称和角色可以通过编程方式来确定；可由用户设置的状态、属性和值可以通过编程方式来设置；而且用户代理（包括辅助技术）可以收到这些项目的更改通知。

#### 用途 – 名称、角色、值 (4.1.2) {#purpose-ame-role-value}

此成功标准旨在确保辅助技术 (AT) 能够收集关于内容中用户界面控件状态的信息，激活（或设置）并跟踪内容中用户界面控件的状态。

当使用来自无障碍访问技术的标准控件时，此过程非常简单。如果根据规范使用用户界面元素，则符合此规定的条件。（请参阅下面的成功标准 4.1.2 示例）

但是，如果建立了自訂控制項，或介面元素被設定為（以程式碼或指令碼）具有不同於平常的角色和/或功能，則必須採取其他措施，以確保控制項為輔助技術提供重要資訊，並允許輔助技術控制這些資訊。

用户界面控件的一个重要的状态是它是否具有焦点。控件的焦点状态可以通过编程方式确定，并且会向用户代理和辅助技术发送关于焦点状态的变更通知。使用者介面控制項狀態的其他範例包括是否已選取核取方塊或選項按鈕。或是展開或收合可收合的樹狀結構或清單節點。

#### 如何达到标准 – 名称、角色、值 (4.1.2) {#how-to-meet-ame-role-value}

遵循[如何达到成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value) 中的准则。

#### 更多信息 – 名称、角色、值 (4.1.2) {#more-information-ame-role-value}

* [了解成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何达到成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
