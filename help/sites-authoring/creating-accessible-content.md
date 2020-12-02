---
title: 为Adobe Experience Manager创建辅助内容（WCAG 2.1符合性）
description: 使用AEM帮助使残障人士能够访问和使用Web内容
translation-type: tm+mt
source-git-commit: df992fc0204519509c4662a7d4315939af2fc92c
workflow-type: tm+mt
source-wordcount: '13956'
ht-degree: 99%

---


# 创建无障碍内容（WCAG 2.1 合规性）{#creating-accessible-content-wcag-conformance}

[Web 内容无障碍准则 (WCAG) 2.1](https://www.w3.org/TR/WCAG/) 由[万维网联盟工作组](https://www.w3.org/Consortium/activities#Accessibility_Guidelines_Working_Group)制定，它包含一系列独立于技术的准则和成功标准，旨在确保残障人士能够访问并使用 Web 内容。

作为对该准则的介绍，联盟提供了一系列条款和支持文档：

* [WCAG 2.1 的新增内容](https://www.w3.org/TR/WCAG/#new-features-in-wcag-2-1)
* [如何满足 WCAG 2.1](https://www.w3.org/WAI/WCAG21/quickref/)
* [了解 WCAG 2.1](https://www.w3.org/WAI/WCAG21/Understanding/)
* [用于 WCAG 2.1 的技术](https://www.w3.org/WAI/WCAG21/Techniques/)
* [WCAG 文档](https://www.w3.org/WAI/standards-guidelines/wcag/docs/)

此外，请参阅：
* [WCAG 2.1 快速指南](/help/managing/qg-wcag.md)。
* [Adobe 解决方案的“无障碍合规性”报告](https://www.adobe.com/accessibility/compliance.html)。
* [配置富文本编辑器以生成辅助内容](/help/sites-administering/rte-accessible-content.md)

准则依据三个合规性级别进行分级：A 级（最低）、AA 级以及 AAA 级（最高）。以下是各个级别的简要定义：

* **级别 A：**&#x200B;您的站点满足基本的、最低级别的无障碍性。要达到此级别，需满足所有级别 A 成功标准。
* **级别 AA：**&#x200B;这是要努力实现的理想无障碍级别，在此级别，站点满足基本级别的无障碍性，因此多数情况下大部分人都可以使用大部分技术访问站点。要达到此级别，需满足所有级别 A 和级别 AA 成功标准。
* **级别 AAA：**&#x200B;您的站点在无障碍方面达到了非常高的级别。要达到此级别，需满足所有级别 A、级别 AA 和级别 AAA 成功标准。

在创建站点时，您应该大体上确定希望自己的站点符合哪个等级。

以下部分介绍 [WCAG 2.1 准则的各个层面](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)以及[符合](https://www.w3.org/TR/WCAG/#conformance-to-wcag-2-1) A 级和 AA 级的相关成功标准。

>[!NOTE]
>
>在此文档中，我们将使用：
>
>* [WCAG 2.1 准则的简称](https://www.w3.org/TR/WCAG/#wcag-2-layers-of-guidance)。
>* [WCAG 2.1 准则中使用的编号](https://www.w3.org/TR/WCAG/#numbering-in-wcag-2-1)，以便与 WCAG 网站进行交叉引用。


## 准则 1：可感知 {#principle-perceivable}

[准则 1：可感知 - 信息和用户界面组件必须以可感知的方式呈现给用户。](https://www.w3.org/TR/WCAG/#perceivable)

### 替换文本 (1.1) {#text-alternatives}

[准则 1.1 替换文本：为所有非文本内容提供替换文本，以便使其可更改为人们需要的其他形式，如大印刷字体、盲文、语音、符号或更简单的语言。](https://www.w3.org/TR/WCAG/#text-alternatives)

### 非文本内容 (1.1.1)  {#non-text-content}

* 成功标准 1.1.1
* A 级
* 非文本内容：呈现给用户的所有非文本内容都具有相同用途的替换文本，以下所列情况除外。

#### 用途 - 非文本内容 (1.1.1) {#purpose-non-text-content}

网页上的信息可以通过多种不同的非文本格式提供，例如图片、视频、动画、图表和图形。失明或患有严重视觉障碍的用户无法看到非文本内容，但是他们可以通过屏幕阅读器的朗读访问文本内容，也可以通过盲文显示设备以触觉形式获取内容。因此，通过为图形格式的内容提供替换文本，无法看到图形内容的用户便可以获取与该内容中提供的信息相对等的文本内容。

另外的一个实用好处是，替换文本使非文本内容能够通过搜索引擎技术建立索引。

#### 如何达到标准 - 非文本内容 (1.1.1)  {#how-to-meet-non-text-content}

对于静态图形，基本的要求是为图形提供对等的替换文本。这可以在&#x200B;**替换文本**&#x200B;字段中完成，例如，请参阅核心组件&#x200B;**[图像](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/image.html)**。

>[!NOTE]
>
>某些开箱即用的核心组件（例如&#x200B;**[轮播](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/carousel.html)**）没有提供用于向单个图像添加替换文本描述的&#x200B;**替换文本**&#x200B;字段，尽管存在适用于整个组件的&#x200B;**标签**&#x200B;字段（**[辅助功能](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/carousel.html#accessibility-tab)**&#x200B;选项卡）。
>
>为AEM实例实施这些版本时，开发团队需要配置这些组件以支持`alt`属性，以便作者可以将其添加到内容中（请参阅[添加对其他HTML元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

默认情况下，AEM 要求填写&#x200B;**替换文本**&#x200B;字段。如果图像是纯粹的装饰并且不需要替换文本，则可以选中&#x200B;**图像具有装饰性**&#x200B;选项。

#### 创建有效的替换文本 {#creating-good-text-alternatives}

非文本内容的形式多种多样，因此替换文本的值取决于图形在网页中所起的作用。以下是一些需要遵循的一般经验法则：

* 替换文本应当既简洁明了，又能清晰地表达非文本内容所提供的基本信息。
* 应当避免使用冗长的描述（超过 100 个字符）。如果替换文本需要表达更多的详细信息，则可以通过以下方法来实现：
   * 在替换文本中提供简短的描述
   * 同时，在同一页面的其他位置或在一个单独的网页中提供更加详尽的描述文本。然后，为该图像创建一个链接，或者在图像附近放置一个文本链接，以便链接到该单独的描述。
* 替换文本不应复制同一页面邻近位置以文本形式提供的内容。请切记，许多图像的作用是解释说明页面文本中已涵盖的要点，因此详尽的替换文本可能已经存在。
* 如果非文本内容是指向另一页面或文档的链接，而且该链接没有任何其他的文本形式部分，则图像的替换文本必须指明链接的目标位置，而不是对图像进行描述。
* 如果按钮元素中包含非文本内容，而且该按钮没有任何文本形式部分，则图像的替换文本必须指明按钮的功能，而不是对图像进行描述。
* 图像的替换文本指定为空 (null) 是完全可以接受的，但是这仅限于图像不需要替换文本的情况（例如，图像仅起装饰作用），或者页面文本中已存在对等的文本。

<!--
The [W3C draft: HTML5 Techniques for providing useful text alternatives](https://dev.w3.org/html5/alt-techniques/) has more details and examples of appropriate alternative text provision for images of different types.
-->

以下特定类型的非文本内容可能需要替换文本：

* 说明性照片：指人物、对象或地点的图像。重要的是要考虑照片在页面中的作用，通常建议描述图像内容，因为辅助型技术可以读出元素类型（例如，`graphic` 或 `image`）；可以在替换文本描述中使用 `screenshot` 或 `illustration` 来提高清晰度，但这取决于上下文。一致性是一个重要因素，在做出某项决策时，该决策应该是面向整个创作团队的，并且应被应用于整个用户体验中。
* 图标：指传递特定信息的小图形符号（图形）。页面和站点上使用的图标必须保持一致。图标在页面或站点上出现的所有实例都应使用相同的简短替代文本，除非这样做会与相邻的文本产生不必要的重复情况。
* 图表和图形：通常用于表示数值数据。因此，替代文本的选择之一就是简要地总结图表或图形中表现出来的主要趋势。如有必要，还可以在&#x200B;**高级**&#x200B;图像属性选项卡中的&#x200B;**描述**&#x200B;字段中以文本形式提供更加详尽的描述。此外，还可以在页面或站点的其他位置以表形式提供源数据。
* 映射、示意图、流程图：对于提供空间数据的图形（例如，支持描述对象之间的关系或者某个流程），请确保以文本格式提供关键消息，并且此文本信息位于每个关联的数据点附近。对于映射，提供等效完整文本可能不太现实，但如果提供映射来作为帮助相关人员找到特定位置的一种方法，则映射图像的替代文本可以简短地指示为“X 映射”**，然后在页面其他位置的文本中或者通过&#x200B;**图像**&#x200B;组件&#x200B;**高级**&#x200B;选项卡中的&#x200B;**描述**&#x200B;字段提供该特定位置的说明。
* CAPTCHA：CAPTCHA 是 *Completely Automated Public Turing test to tell Computers and Humans Apart*（全自动区分计算机和人类的图灵测试）的缩写。这是一项在网页中用于区分人类和恶意软件的安全检查，但同时也会妨碍网页的无障碍性。用户要想通过安全测试，必须按照要求描述自己所看到的这些图像。为这些图像提供替代文本显然是不可能的，因此需要思考出非图形的替代解决方案。W3C 提供了许多建议，例如：这些方法各有优缺点。
   * 逻辑谜题
   * 使用声音输出替代图像
   * 限制使用帐户和垃圾邮件筛选器。
* 背景图像：背景图像是使用层叠样式表 (CSS) 而不是 HTML 实现的。这就意味着无法指定替代文本值。因此，背景图像不应提供重要的文本信息 - 即便提供，这些信息必须也要在页面的文本中有所提及。尽管如此，当图像无法显示时，也应务必显示替代背景。

>[!NOTE]
>
>背景与前景文本之间应该有适当的对比度等级；这在[对比度（最小）(1.4.3)](#contrast-minimum) 中有更加详细的讨论。

#### 更多信息 - 非文本内容 (1.1.1)  {#more-information-non-text-content}

* [了解成功标准 1.1.1](https://www.w3.org/WAI/WCAG21/Understanding/non-text-content.html)
* [如何达到成功标准 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/#non-text-content)
* [CAPTCHA 的 W3C 解释和替代方法](https://www.w3.org/TR/turingtest/)

<!--
* [W3C: HTML5 Techniques for providing useful text alternatives (draft)](https://dev.w3.org/html5/alt-techniques/)
-->

### 基于时间的媒体 (1.2)  {#time-based-media}

[准则 1.2 基于时间的媒体：为基于时间的媒体提供替代内容。](https://www.w3.org/TR/WCAG/#time-based-media)

此准则涉及“基于时间”**&#x200B;的 Web 内容。这包括用户可以播放的内容（例如，视频、音频和动画内容），这些内容可以是预先录制的，也可以是实时流传输的。

### 纯音频和纯视频（预先录制）(1.2.1) {#audio-only-and-video-only-prerecorded}

* 成功标准 1.2.1
* A 级
* 纯音频和纯视频（预先录制）：对于预先录制的纯音频媒体和预先录制的纯视频媒体，均存在以下情况，除非音频或视频就是文本的替代媒体 ，且明确进行了如下标记：
   * 预先录制的纯音频：对于预先录制的纯音频内容，提供了基于时间的媒体的替代内容，以呈现对等信息。
   * 预先录制的纯视频：对于预先录制的纯视频内容，要么提供了基于时间的媒体的替代内容，要么提供了音轨，以呈现对等信息。

#### 用途 - 纯音频和纯视频（预先录制）(1.2.1) {#purpose-audio-only-and-video-only-prerecorded}

以下用户可能会遇到音频和视频的无障碍问题：

* 患有视觉障碍的用户在没有音轨，或者音轨提供的信息不足以告知他们视频或动画中正在播放的内容时；
* 因患有听觉障碍或耳聋而无法听到音轨的用户；
* 可以听到音轨但无法理解所讲内容的用户（例如，因为语言不通而无法理解）。

如果用户使用的浏览器或设备不支持播放特定媒体格式（如 Adobe Flash）的内容，则这些用户可能也无法访问相关视频或音频。

如果以不同的格式提供这些信息，如使用文本（或者对于无音频的视频，使用音频），则无法访问原始内容的用户便可以访问这些信息。

#### 如何达到标准 - 纯音频和纯视频（预先录制）(1.2.1) {#how-to-meet-audio-only-and-video-only-prerecorded}

* 如果内容是预先录制的不含视频的音频（如播客）：
   * 在紧靠内容之前或之后的位置提供一个链接，指向音频内容的文本记录。这份记录应采用 HTML 页面的形式，其中包含所有讲话内容以及重要的非讲话内容的对等文本，还指出讲话者并描述讲话背景、声音表情及其他任何重要的音频。
* 如果内容是不含音频的动画或预先录制的不含音频的视频：
   * 在紧靠内容之前或之后的位置提供一个链接，指向与视频提供的信息对等的文本描述。
   * 或者，指向以常用的音频格式（如 MP3）呈现的对等音频描述。

>[!NOTE]
>
>如果音频或视频内容是作为同一网页上已经存在的其他格式内容的替换内容提供的，则可能不需要其他替换文本。
>
>准则《[了解 WCAG 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)》提供了进一步的信息。

在 AEM 网页中插入多媒体的方式与插入图像类似。但是，多媒体内容与静态图像相比还是更为复杂，而且在控制多媒体的播放方式时有各种不同的设置和选项。

>[!NOTE]
>
>如果将多媒体与信息性内容结合使用，则也必须创建替代内容的链接。例如，要加入文本记录，应创建一个用于显示记录的 HTML 页面，然后在音频内容旁边或下方添加一个链接。

#### 更多信息 - 纯音频和纯视频（预先录制）(1.2.1) {#more-information-audio-only-and-video-only-prerecorded}

* [了解成功标准 1.2.1](https://www.w3.org/WAI/WCAG21/Understanding/audio-only-and-video-only-prerecorded.html)
* [如何达到成功标准 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/#audio-only-and-video-only-prerecorded)

### 字幕（预先录制）(1.2.2) {#captions-prerecorded}

* 成功标准 1.2.2
* A 级
* 字幕（预先录制）：为同步媒体中所有预先录制的音频内容提供了字幕，除非该媒体是文本的替代媒体，且明确进行了相应标记。

#### 用途 - 字幕（预先录制）(1.2.2) {#purpose-captions-prerecorded}

耳聋或听力欠佳的用户无法或很难获取音频内容。字幕是讲话和非讲话音频的对等文本，在视频播放过程中会在相应的时间显示在屏幕上。这让无法听到音频的用户可以了解正在播放的内容。

#### 如何达到标准 - 字幕（预先录制）(1.2.2) {#how-to-meet-captions-prerecorded}

字幕有以下两种形式：

* 开放式：字幕在视频播放过程中始终可见
* 隐藏式：字幕可以由用户打开或关闭 

尽量使用隐藏式字幕，因为这样用户可以选择是否观看字幕。

对于隐藏式字幕，需要以适当的格式（如 [SMIL](https://www.w3.org/AudioVideo/)）为对应的视频文件创建并提供同步字幕文件（与此相关的详细操作说明不在本指南的范围之内，但是我们在[更多信息 - 字幕（预先录制）(1.2.2)](#more-information-captions-prerecorded) 中提供了一些教程的链接。确保提供注释或在视频播放器中启用字幕功能，以便让用户知道视频有字幕可看。

如果必须使用开放式字幕，应将文本嵌入到视频轨道中。可以使用能够将字幕覆盖到视频上的视频编辑应用程序来完成嵌入。

#### 更多信息 - 字幕（预先录制）(1.2.2) {#more-information-captions-prerecorded}

* [了解成功标准 1.2.2](https://www.w3.org/WAI/WCAG21/Understanding/captions-prerecorded.html)
* [如何达到成功标准 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/#captions-prerecorded)

<!--
* [W3C: Synchronized Multimedia](https://www.w3.org/AudioVideo/)
* [Captions, Transcripts, and Audio Descriptions - by WebAIM](https://webaim.org/techniques/captions/)
-->

### 音频描述或替代媒体（预先录制）(1.2.3) {#audio-description-or-media-alternative-prerecorded}

* 成功标准 1.2.3
* A 级
* 音频描述或替代媒体（预先录制）：对于同步的媒体，为预先录制的视频内容提供了基于时间的媒体的替代内容或音频描述，除非该媒体是文本的替代媒体，且明确进行了相应标记。

#### 用途 - 音频描述或替代媒体（预先录制）(1.2.3) {#purpose-audio-description-or-media-alternative-prerecorded}

如果视频或动画中的信息仅以可视形式呈现，或者音轨提供的信息不足以让用户了解视频或动画中正在播放的内容，则失明或患有视觉障碍的用户将会遇到无障碍问题。

#### 如何达到标准 - 音频描述或替代媒体（预先录制）(1.2.3) {#how-to-meet-audio-description-or-media-alternative-prerecorded}

可以通过以下两种方式来达到该成功标准。任何一种方式都是可以接受的：

1. 为视频内容提供附加的音频描述。可以采用以下三种方式中的任何一种来实现：
   * 在现有对话暂停期间，提供有关场景变换的信息，该信息不作为现有音轨内容的一部分；
   * 提供一段附加的可选新音轨，其中不仅包含原始音轨，而且还包含有关场景变换的额外音频信息。
      * 这允许用户在现有音轨（*不含*&#x200B;音频描述）和新音轨（*含有*&#x200B;音频描述）之间进行切换。
      * 这可以避免妨碍到不需要附加描述的用户。
   * 为视频内容创建第二个版本，以便提供延长的音频描述。这样，通过在合适的时间点暂停音频和视频，便可降低在现有对话的间隙提供详细音频描述的难度。最终，在重新开始播放视频之前，便可以提供一个更长的音频描述。与上一种方式中所提到的一样，为了避免妨碍到不需要附加描述的用户，最好将此类音频描述作为可选的额外音轨来提供。
1. 为视频或动画中的音频和视觉元素提供适当的对等文本记录。这应当包括，在适当情况下，指出讲话者，以及描述讲话背景、视觉上呈现的任何事件或信息和语音表述内容。根据文本长度的不同，既可以将记录放置在视频或动画所在的页面上，也可以将其放置在单独的页面上；如果选择后者，则需要在视频或动画旁边提供记录的链接。

至于如何创建带有音频描述的视频，具体细节不在本指南的范围之内。创建视频和音频描述非常耗时，但是 Adobe 的其他产品可以帮助您完成这些任务。

#### 更多信息 - 音频描述或替代媒体（预先录制）(1.2.3) {#more-information-audio-description-or-media-alternative-prerecorded}

* [了解成功标准 1.2.3](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-or-media-alternative-prerecorded.html)
* [如何达到成功标准 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-or-media-alternative-prerecorded)

<!--
* [Adobe Encore](https://www.adobe.com/products/encore.html) - a DVD authoring software tool
-->

### 字幕（实时）(1.2.4)  {#captions-live}

* 成功标准 1.2.4
* AA 级
* 字幕（实时）：为同步媒体中的所有实时音频内容提供了字幕 。

#### 用途 - 字幕（实时）(1.2.4)  {#purpose-captions-live}

该成功标准与[字幕（预先录制）](#captions-prerecorded)的标准完全相同，因为其用途在于解决耳聋或听力欠佳的用户遇到的辅助功能问题，两者的不同之处在于该成功标准需要处理网络直播等实时演示。

#### 如何达到标准 - 字幕（实时）(1.2.4) {#how-to-meet-captions-live}

遵循上面[字幕（预先录制）](#captions-prerecorded)所提供的指南。但鉴于媒体的实时性质，必须尽可能以最快的速度提供字幕，并对正在发生的情况做出回应。因此，应当考虑使用实时字幕工具或语音转文本工具。

与此相关的详细说明不在本指南的范围之内，但是以下资源提供了有用的信息：

* [WebAIM：实时字幕](https://www.webaim.org/techniques/captions/realtime.php)

* [AccessComputing 项目（华盛顿大学）：能否利用语音识别技术自动生成字幕？](https://www.washington.edu/accesscomputing/can-captions-be-generated-automatically-using-speech-recognition)

#### 更多信息 - 字幕（实时）(1.2.4) {#more-information-captions-live}

* [了解成功标准 1.2.4](https://www.w3.org/WAI/WCAG21/Understanding/captions-live.html)
* [如何达到成功标准 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/#captions-live)

### 音频描述（预先录制）(1.2.5)  {#audio-description-prerecorded}

* 成功标准 1.2.5
* AA 级
* 音频描述（预先录制）：为同步媒体中的所有预先录制的视频内容提供了音频描述 。

#### 用途 - 音频描述（预先录制）(1.2.5) {#purpose-audio-description-prerecorded}

此成功标准与[音频描述或替代媒体（预先录制）](#audio-description-or-media-alternative-prerecorded)的标准几乎完全相同，唯一不同之处在于，作者必须提供更加详细的音频描述才能符合 AA 级标准。

#### 如何达到标准 - 音频描述（预先录制）(1.2.5) {#how-to-meet-audio-description-prerecorded}

遵循[音频描述或替代媒体（预先录制）](#audio-description-or-media-alternative-prerecorded)所提供的指南。

#### 更多信息 - 音频描述（预先录制）(1.2.5) {#more-information-audio-description-prerecorded}

* [了解成功标准 1.2.5](https://www.w3.org/WAI/WCAG21/Understanding/audio-description-prerecorded.html)
* [如何达到成功标准 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/#audio-description-prerecorded)

### 适应性 (1.3)  {#adaptable}

[准则 1.3 适应性：创建可用不同方式呈现的内容（例如更简单的布局），而不会丢失信息或结构。](https://www.w3.org/TR/WCAG/#adaptable)

该准则包含为支持以下用户而必须满足的要求：

* 可能无法访问作者使用相应内容的默认呈现方式呈现的信息（例如，多列布局或大量使用颜色和/或图像的页面）的用户。

* 可能要使用纯音频内容或可视替代显示方式（如大文本或高对比度）的用户。

### 信息和关系 (1.3.1)  {#info-and-relationships}

* 成功标准 1.3.1
* A 级
* 信息和关系：通过呈现传递的信息、结构和关系，可以采用编程方式进行确定或在文本中提供。

#### 用途 - 信息和关系 (1.3.1)  {#purpose-info-and-relationships}

残障人士使用的许多辅助型技术都依赖结构性信息才能有效地显示或“理解”**&#x200B;内容。此类结构性信息有多种形式，如页面标题、表行标题和列标题以及列表类型。举例来说，屏幕阅读器可以让用户从页面的一个标题导航到另一个标题。但是，如果页面内容仅仅在可视样式而非基本 HTML 中具有结构，则辅助型技术便无法获取结构性信息，从而限制它们辅助用户轻松浏览的能力。

该成功标准旨在确保此类结构性信息通过 HTML 或其他代码技术以编程的方式提供，这样浏览器和辅助型技术便可以访问并利用这些信息。

#### 如何达到标准 - 信息和关系 (1.3.1) {#how-to-meet-info-and-relationships}

AEM 允许轻松地使用相应的 HTML 元素构建语义上有意义的 Web 内容。可在 RTE（一种文本组件）中打开页面内容，然后使用&#x200B;**段落格式**&#x200B;菜单（段落符号）指定相应的结构元素（例如，段落、标题等）。

在适用的情况下，您可以使用以下元素来确保网页具有相应的结构：

* **标题：**&#x200B;只要您启用了 RTE 辅助功能，AEM 就会提供 3 个级别的页面标题。您可以使用这些标题标识内容的章节和子章节。标题 1 是最高级别的标题，标题 3 是最低级别的标题。系统管理员可以配置系统以允许使用更多标题级别。

* **列表**：可以使用 HTML 指定三种不同类型的列表：
   * `<ul>` 元素用于表示&#x200B;*无序*（项目符号）列表。单个列表项使用 `<li>` 元素进行标识。在 RTE 中，使用&#x200B;**项目符号列表**&#x200B;图标。
   * `<ol>` 元素用于表示&#x200B;*编号*&#x200B;列表。单个列表项使用 `<li>` 元素进行标识。
在 RTE 中，使用**编号列表**&#x200B;图标。

   如果您希望将现有内容更改为特定列表类型，可以突出显示相应的文本，然后选择相应的列表类型。正如上述示例中显示的段落文本输入方式一样，相应的列表元素会自动添加到 HTML。

   在全屏模式下，单个“项目符号列 **表”和** “编 **号列表** ”图标可见。 当不处于全屏模式时，这两个选项在单个列表图标的后 **面可** 用。

* **表**：数据表必须使用 HTML 表元素进行标识：
   * 一个 `<table>` 元素
   * 每个表行均使用 `<tr>` 元素进行标识
   * 每个行标题和列标题均使用 `<th>` 元素进行标识
   * 每个数据单元格均使用 `<td>` 元素进行标识

   此外，辅助表会使用以下元素和属性：

   * `<caption>` 元素用于为表提供可视描述。默认情况下，描述显示在表上方居中的位置，但是可以使用 CSS 相应地调整位置。描述采用编程方式与表相关联，因此这是一种提供内容简介的有用方法。
   * `<summary>` 元素通过总结视力正常的用户可以看到的内容，帮助失明的用户更加轻松地了解表中提供的信息。当使用了复杂或非常规的表布局时，这种方法尤其有用（该属性不会显示在浏览器中，只会由辅助型技术读取）。
   * `<th>` 元素的 `scope` 属性用于指示某个单元格表示特定行的标题，还是特定列的标题。在复杂的表中，即数据单元格可能与一个或多个标题相关联的情况下，类似的方法是使用标题和 id 属性。

   >[!NOTE]
   >
   >默认情况下，这些元素和属性不直接可用，但系统管理员可以在&#x200B;**表属性**&#x200B;对话框中添加对这些值的支持（请参阅[添加对其他HTML元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

   要打开您可以在其中选择&#x200B;**表属性**&#x200B;选项卡的&#x200B;**表**&#x200B;对话框，请执行以下操作：

   * 定义相应的&#x200B;**描述**。
   * 理想情况下，请删除 **Width**、 **Height**、Border **、** Border Border Sell PaddingSpacing **、****** Cell Spacing的默认值。 因为这些属性可以在全局样式表中设置。

   然后，您可以使用&#x200B;**单元格属性**&#x200B;来选择单元格是数据单元格还是标题单元格：

* **强调**：使用 `<strong>` 或 `<em>` 元素指示要强调的内容。切勿在段落中使用标题突出显示文本。
   * 突出显示要强调的文本；
   * 单击&#x200B;**属性**&#x200B;面板中显示的 **B** 图标（表示 `<strong>`）或 **I** 图标（表示 `<em>`）（确保已选择 HTML）。

      >[!NOTE]
      >
      >标准 AEM 安装中的 RTE（富文本编辑器）设置为：
      >
      >* `<b>`对象`<strong>`
      >* `<i>`对象`<em>`

      >
      >尽管两种形式效果相同，但是最好使用 `<strong>` 和 `<em>`，因为从语义上来讲，它们才是正确的 HTML 标记。开发团队在开发项目实例时，可以将 RTE 配置为使用 `<strong>` 和 `<em>`（而非 `<b>` 和 `<i>`）。


* **复杂数据表**：在某些情况下，一些复杂表拥有两级或更多级标题，此时，基本的表属性可能不足以提供所有必需的结构性信息。对于此类复杂表，需要使用&#x200B;**标题**&#x200B;和 **id** 属性在标题和与之相关的单元格之间建立关系。

   >[!NOTE]
   >
   >现成的安装中没有 id 属性。可以通过在 RTE 中配置 HTML 规则和序列化器来启用该属性。

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

   要在 AEM 中实现此操作，必须使用源代码编辑模式直接添加标记。

   >[!NOTE]
   >
   >该功能并非在标准安装中直接可用。它需要配置 RTE、HTML 规则和序列化器。

#### 更多信息 - 信息和关系 (1.3.1) {#more-information-info-and-relationships}

* [了解成功标准 1.3.1](https://www.w3.org/WAI/WCAG21/Understanding/info-and-relationships.html)
* [如何达到成功标准 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/#info-and-relationships)

### 有意义的顺序 (1.3.2)  {#meaningful-sequence}

* 成功标准 1.3.2
* A 级
* 有意义的顺序：当内容的呈现顺序会影响内容含义时，可以通过编程方式确定正确的阅读顺序。

#### 用途 - 有意义的顺序 (1.3.2) {#purpose-meaningful-sequence}

此成功标准旨在使用户代理既能够提供内容的替代呈现方式，同时还能保留理解内容含义所需的阅读顺序。能够以编程方式确定至少一个有意义的内容呈现顺序，这一点很重要。当辅助技术以错误的顺序阅读内容，或者在应用替代样式表或其他格式更改时，不符合此成功标准的内容可能会使用户感到困惑或是不知所措。

#### 如何达到标准 - 有意义的顺序 (1.3.2) {#how-to-meet-meaningful-sequence}

遵循[如何达到成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence) 中的准则。

#### 更多信息 - 有意义的顺序 (1.3.2) {#more-information-meaningful-sequence}

* [了解成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/Understanding/meaningful-sequence.html)
* [如何达到成功标准 1.3.2](https://www.w3.org/WAI/WCAG21/quickref/#meaningful-sequence)

### 感官特性 (1.3.3)  {#sensory-characteristics}

* 成功标准 1.3.3
* A 级
* 感官特性：为了解和使用内容而提供的说明不完全依赖于组件的感官特性，如形状、大小、可视位置、方向或声音。

#### 用途 - 感官特性 (1.3.3)  {#purpose-sensory-characteristics}

设计者往往关注可视设计特征，如颜色、形状、文本样式，或者内容在展示信息时所在的绝对或相对位置。在传达信息方面，这些可能是非常强大的设计技术（可以改善具有认知无障碍需求的视力正常用户的整体无障碍体验），但是失明或患有视觉障碍的用户可能无法访问需要视觉识别属性（例如位置、颜色或形状）的信息。

同样，如果用户在获取信息时必须辨认不同的声音（例如，男性或女性讲话的内容），而且音频内容没有反映在任何替换文本中，则患有听觉障碍的用户就会遇到无障碍问题。

>[!NOTE]
>
>有关颜色替代内容的要求，请参阅[使用颜色](#use-of-color)。

#### 如何达到标准 - 感官特性 (1.3.3)  {#how-to-meet-sensory-characteristics}

确保那些依赖页面内容的可视特性传递的任何信息都同时以替代格式呈现。

* 切勿依赖可视位置来提供信息。例如，如果希望用户通过页面右侧的菜单访问更多信息，那么请不要只提及&#x200B;*右侧的菜单*；而是要为该菜单命名（例如，通过标题进行命名），然后以文本方式提及该名称。
* 切勿将文本样式（例如，粗体或斜体文本）作为传递信息的唯一方式。

>[!NOTE]
>
>如果用户在非可视上下文中可以理解使用的描述性词语的含义，则可以使用描述性词语。例如，使用&#x200B;*上面*&#x200B;和&#x200B;*下面*&#x200B;通常是可以接受的，因为它们分别表示特定内容项之前和之后的内容；在朗读内容时，这也是可以接受的。

#### 更多信息 - 感官特性 (1.3.3)  {#more-information-sensory-characteristics}

* [了解成功标准 1.3.3](https://www.w3.org/WAI/WCAG21/Understanding/sensory-characteristics.html)
* [如何达到成功标准 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/#sensory-characteristics)

### 可辨别性 (1.4)  {#distinguishable}

[准则 1.4 可辨别性：使用户更容易看到和听到内容，包括将前景与背景分离开。](https://www.w3.org/TR/WCAG/#distinguishable)

### 使用颜色 (1.4.1)   {#use-of-color}

* 成功标准 1.4.1
* A 级
* 使用颜色：颜色不用作传递信息、指示动作、提示响应或区分可视元素的唯一可视方式。

>[!NOTE]
>
>此成功标准专门针对颜色感知。[适应性 (1.3)](#adaptable) 中涵盖其他形式的感知；包括以编程方式访问颜色和其他可视呈现编码。

#### 用途 - 使用颜色 (1.4.1)  {#purpose-use-of-color}

颜色能够立竿见影地增强网页的美感，而且还有助于传递信息。但是，由于各种视觉障碍（从失明到色盲）的限制，部分用户无法辨认某些颜色。这就使颜色编码无法可靠地提供信息。

例如，一些患有红绿色盲症的用户无法辨认绿色和红色阴影。这些用户可能会将这两种颜色看成第三种颜色（如棕色），在这种情况下，他们就无法辨认红色、绿色和棕色。

此外，如果用户使用仅支持文本的浏览器、单色显示设备或查看黑白打印的页面，他们也无法感知到颜色。

还需要考虑的一个事项是界面元素（例如，选项卡、切换按钮等）的“选定”**&#x200B;状态，这些状态需要以颜色和视觉呈现方式以外的其他某种方式传递。对于这些元素，在创建不依赖特定感官的全包容用户体验时，额外使用图案、形状和编程信息将很有帮助。

#### 如何达到标准 - 使用颜色 (1.4.1) {#how-to-meet-use-of-color}

无论在何处使用颜色传递信息，都应确保无需看到颜色即可获取相应的信息。

例如，确保通过颜色传递的信息也明确地提供在文本中。

如果使用颜色作为提供信息的提示，则应提供其他可视提示，如更改样式（如粗体、斜体）或字体。这有助于视力不佳或具有色觉辨认障碍的人识别信息。但是，不能完全依赖这种方法，因为这对于根本无法看到页面的用户而言并无助益。因此，提供隐藏文本或使用编程解决方案（例如 [Web 标准的无障碍的富因特网应用程序 (ARIA) 套件](https://www.w3.org/WAI/standards-guidelines/aria/)）将此信息传递给失明用户将（有时）非常有用。

#### 更多信息 - 使用颜色 (1.4.1) {#more-information-use-of-color}

* [了解成功标准 1.4.1](https://www.w3.org/WAI/WCAG21/Understanding/use-of-color.html)
* [如何达到成功标准 1.4.1](https://www.w3.org/WAI/WCAG21/quickref/#use-of-color)

### 音频控制 (1.4.2)  {#audio-control}

* 成功标准 1.4.2
* A 级
* 音频控制：如果网页上的任何音频自动播放超过 3 秒，则要么有一种机制可用来暂停或停止音频播放，要么有一种独立于整体系统音量控制的机制可用来调控音频音量。

#### 用途 - 音频控制 (1.4.2) {#purpose-audio-control}

如果同时还有其他音频正在播放，则使用屏幕阅读软件的用户可能会难以听清语音输出。尤其是当屏幕阅读器的语音输出是基于软件的（现今大多数都是如此），并且是通过与系统声音相同的音量控制来调控时，这种困难就会加剧。此外，一些患有认知障碍和神经系统障碍的用户可能对声音敏感。这些用户认为无法更改音频内容的音量将会造成很大干扰。

因此，用户能够关闭背景声音是非常重要的。

>[!NOTE]
>
>控制音量包括能够将音量减小到零。

#### 如何达到标准 - 音频控制 (1.4.2) {#how-to-meet-audio-control}

遵循[如何达到成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control) 中的准则。

#### 更多信息 - 音频控制 (1.4.2) {#more-information-audio-control}

* [了解成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/Understanding/audio-control.html)
* [如何达到成功标准 1.4.2](https://www.w3.org/WAI/WCAG21/quickref/#audio-control)

### 对比度（最小）(1.4.3) {#contrast-minimum}

* 成功标准 1.4.3
* AA 级
* 对比度（最小）：文本的可视呈现以及文本的图像至少要有 4.5:1 的对比度，以下内容除外：
   * 大文本：大号文本及其图像至少要有 3:1 的对比度。
   * 附属内容：文本或文本的图像是未激活的用户界面组件的一部分，只是[纯粹的装饰](https://www.w3.org/TR/WCAG/#dfn-pure-decoration)，对任何人都不可见，或者只是包含其他重要可视内容的图片的一部分，对于此类文本或文本的图像，没有对比度要求。
   * 商标标志：文本是徽标或品牌名称的一部分，对于此类文本，没有最低对比度要求。

   >[!NOTE]
   >
   >请参阅[了解非文本对比度](https://www.w3.org/WAI/WCAG21/Understanding/non-text-contrast.html)获取更多详细信息，从而帮助确保内容作者了解有关非文本元素（包括图标、界面元素等）的其他要求。

#### 用途 - 对比度（最小）(1.4.3) {#purpose-contrast-minimum}

患有某种视觉障碍的用户可能无法辨认某些对比度低的颜色对。如果出现以下任一情况，此类用户便可能遇到无障碍问题：

* 文本与其背景颜色之间的对比度极低。
* 文本的颜色编码（例如链接文本和非链接文本）在辨认信息时起到重要作用。

>[!NOTE]
>
>此成功标准不适用于仅起装饰作用的文本。

#### 如何达到标准 - 对比度（最小）(1.4.3)  {#how-to-meet-contrast-minimum}

确保文本与其背景之间有明显的对比度。对比度取决于相关文本的大小和样式：

* 对于大小小于 18 点（或粗体为小于 14 点）的文本，文本中的文字/图像与背景之间的对比度至少应为 4.5:1。
* 对于大小至少为 18 点（或粗体至少为 14 点）的文本，对比度至少应为 3:1。
* 如果背景带有图案，则应将任何文本周围的背景变浅，以便将对比度维持在 4.5:1 或 3:1。

>[!NOTE]
>
>请记住，字体在呈现同等 PT/PX/EM 大小的方式上可能有所不同。
>
>在为 Web 内容选择适当的字体和大小时，建议在可读性和可用性方面做出良好的判断。

>[!NOTE]
>
>以下网站可以帮助您转换到其他单位：
>
>* [Px 到 Em 计算器 - Omni](https://www.omnicalculator.com/conversion/px-to-em)
>* [字体大小转换：pixel-point-em-rem-percent](https://websemantics.uk/tools/font-size-conversion-pixel-point-em-rem-percent/)
>* [PMtoEM.com：让 PX 到 EM 的转换变得简单](http://pxtoem.com)


要检查对比度，可使用颜色对比度工具，例如 [Paciello Group Color Contrast Analyser](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM Color Contrast Checker](https://www.webaim.org/resources/contrastchecker/)。这些工具可以用来检查颜色对，并报告任何对比度问题。

或者，如果您不太在意页面外观的指定，则可以选择不指定背景和前景文本颜色。在这种情况下，无需检查对比度，因为用户的浏览器将确定文本和背景的颜色。

如果页面无法达到建议的对比度级别，则将需要提供一个链接以指向该页面的对等替代版本（不存在颜色对比度问题），或者允许用户根据自己的要求调整页面颜色方案的对比度。

#### 更多信息 - 对比度（最小）(1.4.3)  {#more-information-contrast-minimum}

* [了解成功标准 1.4.3](https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html)
* [如何达到成功标准 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/#contrast-minimum)

### 调整文本大小 (1.4.4)  {#resize-text}

* 成功标准 1.4.4
* A 级
* 调整文本大小：除了文本的字幕和图像之外，在不使用辅助技术的情况下，文本大小最多可放大 200%，且不会丢失内容或功能。

#### 用途 - 调整文本大小 (1.4.4) {#purpose-resize-text}

此成功标准旨在确保成功缩放视觉呈现的文本，包括基于文本的控件（已显示出来供用户查看的文本字符，[与仍以 ASCII 等数据格式表示的文本字符]），以便具有轻微视觉障碍的用户可以直接阅读相关内容，而无需使用屏幕放大镜等辅助技术。网页上的所有内容都能缩放，这一点或许能够让用户受益，但文本是最关键的。

#### 如何达到标准 - 调整文本大小 (1.4.4) {#how-to-meet-resize-text}

除了遵循[如何达到成功标准 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text) 下的准则外，您还可以鼓励内容作者在其页面设计和字体大小（例如，响应式 Web 设计）中使用不固定、灵活的宽度和高度，以便读者可以调整文本大小。

#### 更多信息 - 调整文本大小 (1.4.4) {#more-information-resize-text}

* [了解成功标准 1.4.4](https://www.w3.org/WAI/WCAG21/Understanding/resize-text.html)
* [如何达到成功标准 1.4.4](https://www.w3.org/WAI/WCAG21/quickref/#resize-text)

### 文本的图像 (1.4.5) {#images-of-text}

* 成功标准 1.4.5
* AA 级
* 文本的图像：如果使用的技术可以达到可视呈现效果，使用文本来传递信息而不使用文本的图像，以下情况除外：
   * 可自定义：文本的图像可根据用户的要求以可视方式进行自定义；
   * 必需：文本的特定呈现方式对要传递的信息而言是必需的。

>[!NOTE]
>
>商标标志（属于徽标或品牌名称一部分的文本）被认为是必需的。

#### 用途 - 文本的图像 (1.4.5)  {#purpose-images-of-text}

当需要文本的某种特定样式时，通常会使用文本的图像；例如，商标标志或从其他来源生成的文本（如纸质文档的扫描件）。但是，与以 HTML 呈现的文本和使用 CSS 设置格式的文本相比，文本的图像无法灵活地改变大小或外观，而这些改变可能正是患有视觉障碍或有阅读障碍的用户所必需的。

#### 如何达到标准 - 文本的图像 (1.4.5)  {#how-to-meet-images-of-text}

如果必须使用文本的图像，应使用 CSS 将文本的图像替换为 HTML 形式的对等文本，这样就可以对文本进行自定义。有关如何实现这一操作的示例，请参阅 [C30：使用 CSS 将文本替换为文本的图像并提供用于切换的用户界面控件](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30)。

#### 更多信息 - 文本的图像 (1.4.5)  {#more-information-images-of-text}

* [了解成功标准 1.4.5](https://www.w3.org/WAI/WCAG21/Understanding/images-of-text.html)
* [如何达到成功标准 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/#images-of-text)

## 准则 2：可操作  {#principle-operable}

[准则 2：可操作 - 用户界面组件和导航必须可以操作。](https://www.w3.org/TR/WCAG/#operable)

### 无障碍键盘 (2.1) {#keyboard-accessible}

[准则 2.1 无障碍键盘：仅用键盘即可实现所有功能。](https://www.w3.org/TR/WCAG/#keyboard-accessible)

此准则涉及的是，确保用户可以使用键盘访问所有功能。

### 键盘 (2.1.1)  {#keyboard}

* 成功标准 2.1.1
* A 级
* 键盘：内容的所有功能均可通过键盘接口操作，且不需要任何击键时间限制，除非底层功能需要依赖于用户的输入行为路径而非单纯依赖于用户最后输入的内容。

#### 用途 - 键盘 (2.1.1) {#purpose-keyboard}

此成功标准旨在确保在可能的情况下，通过键盘或键盘接口（以便使用替代键盘）来操作内容。对于视觉障碍人士（无法使用鼠标等需要手眼协作的设备的人），以及必须使用替代键盘或充当键盘模拟器的输入设备的人士而言，如果内容是可以通过键盘或替代键盘操作的，那么他们就能够操作这些内容。键盘模拟器包括语音输入软件、通过呼吸来操作的软件、屏幕键盘、扫描软件以及各种辅助技术和备用键盘。此外，视力欠佳的人也可能难以跟踪指针，如果可以通过键盘控制指针，他们会发现使用软件会容易得多（或者这是他们能够使用软件的唯一方法）。

#### 如何达到标准 - 键盘 (2.1.1) {#how-to-meet-keyboard}

遵循[如何达到成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard) 中的准则。

#### 更多信息 - 键盘 (2.1.1) {#more-information-keyboard}

* [了解成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何达到成功标准 2.1.1](https://www.w3.org/WAI/WCAG21/quickref/#keyboard)

### 无键盘陷入 (2.1.2)  {#no-keyboard-trap}

* 成功标准 2.1.2
* A 级
* 无键盘陷阱：如果可以使用键盘接口将键盘焦点移动到页面的某个组件，则焦点应同样可以通过键盘接口的方式从该组件上移开；如果除了通过未修改的箭头、Tab 键或其他标准退出方法外，上述移开功能还需通过其他手段实现，则应告知用户将焦点移开的方法。

#### 用途 - 无键盘陷阱 (2.1.2) {#purpose-no-keyboard-trap}

此成功标准旨在确保内容不会&#x200B;*陷入*&#x200B;网页内容子部分中的键盘焦点内。当一个页面综合采用了多种格式以及使用插件或嵌入式应用程序渲染页面时，经常会出现这种问题。

有时，网页的功能会将焦点限制在内容的子部分（例如，模态对话框）。在这种情况下，您应该为用户提供一种方法，使其能够退出该内容的子部分（例如，按 ESC 键关闭模态对话框，或者使用“关闭”按钮关闭模态对话框）。

#### 如何达到标准 - 无键盘陷阱 (2.1.2) {#how-to-meet-no-keyboard-trap}

遵循[如何达到成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap) 中的准则。

#### 更多信息 - 无键盘陷阱 (2.1.2) {#more-information-no-keyboard-trap}

* [了解成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/Understanding/no-keyboard-trap.html)
* [如何达到成功标准 2.1.2](https://www.w3.org/WAI/WCAG21/quickref/#no-keyboard-trap)

### 充足的时间 (2.2) {#enough-time}

[准则 2.2 充足的时间：为用户提供充足的时间来阅读和使用内容。](https://www.w3.org/TR/WCAG/#enough-time)

此准则涉及的是，确保用户有充足的时间来阅读内容并执行操作。

### 计时可调 (2.2.1)  {#timing-adjustable}

* 成功标准 2.2.1
* A 级
* 键盘：为用户提供充足的时间来阅读和使用内容。

#### 用途 - 计时可调 (2.2.1) {#purpose-timing-adjustable}

此成功标准旨在确保残障用户有尽可能充足的时间与 Web 内容交互。失明、视力欠佳、行动不便以及认知困难等残障人士，可能需要更多时间来阅读内容或执行在线填表等操作。如果 Web 功能是计时的，则某些用户难以在限制时间内完成所需的操作。这可能会导致他们无法访问相关服务。设计不限时功能将有助于残障人士成功完成这些操作。提供相应选项，让用户可以选择禁用时间限制、自定义时间限制长度或在达到时间限制前请求更多时间，这有助于那些需要超过预期时间的用户成功完成任务。这些选项应按照对用户最有帮助的顺序列出。禁用时间限制是最优选项，其次是自定义时间限制长度，再次是在达到时间限制之前请求更多时间。

#### 如何达到标准 - 计时可调 (2.2.1) {#how-to-meet-timing-adjustable}

遵循[如何达到成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable) 中的准则。

#### 更多信息 - 计时可调 (2.2.1) {#more-information-timing-adjustable}

* [了解成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/Understanding/timing-adjustable.html)
* [如何达到成功标准 2.2.1](https://www.w3.org/WAI/WCAG21/quickref/#timing-adjustable)

### 暂停、停止、隐藏 (2.2.2)  {#pause-stop-hide}

* 成功标准 2.2.2
* A 级
* 暂停、停止、隐藏：对于移动、闪烁、滚动或自动更新的信息，符合以下情况：
   * 移动、闪烁、滚动：对于任何 (a) 自动启动，(b) 持续时间超过 5 秒钟，并 (c) 与其他内容并行呈现的移动、闪烁或滚动信息，提供了一个机制来允许用户执行暂停、停止或隐藏操作，除非移动、闪烁或滚动是某种行为的必需部分；
   * 自动更新：对于任何 (a) 自动启动，并 (b) 与其他内容并行呈现的自动更新信息，提供了一个机制来允许用户执行暂停、停止或隐藏操作，或者控制更新的频率，除非自动更新是某种行为的必需部分。

注意要点：

1. 有关闪烁或闪光内容的要求，请参阅切勿设计会导致癫痫发作的内容 (2.3)。
1. 由于任何未达到此成功标准的内容会干涉用户使用整个页面的能力，因此网页上的所有内容（无论是否用来达到其他成功标准）必须达到此成功标准。请参阅[符合性要求 5：不干涉](https://www.w3.org/TR/WCAG20/#cc5)。
1. 通过软件定期更新或以流式传输至用户代理的内容，不需要保留或呈现在启动暂停和恢复呈现期间生成或收到的信息，因为这可能没有技术可行性，而且在许多情况下可能会误导这样做。
1. 对于在预加载阶段或类似情况下出现的动画，如果所有用户在该阶段都无法进行交互，并且如果不指示进度可能会让用户感到困惑，或导致他们认为内容冻结或中断，则可以将此类动画视为必需内容。

#### 用途 - 暂停、停止、隐藏 (2.2.2)  {#purpose-pause-stop-hide}

某些用户可能会认为移动的内容会让人分心，甚至让人觉得难受，而且难以将注意力集中在页面的其他部分。此外，如果用户无法跟上移动的文本，他们可能就很难阅读此类内容。

#### 如何达到标准 - 暂停、停止、隐藏 (2.2.2)  {#how-to-meet-pause-stop-hide}

如果创建的网页包含移动、闪光或闪烁的内容，则可以采纳以下一项或多项建议，具体视内容的性质而定。

* 提供一种可使滚动的内容暂停的方法，以便让用户有充足的时间进行阅读。例如，新闻滚动条、自动更新的文本以及自动推进的图像轮播。
* 确保闪烁的内容会在 5 秒钟后停止闪烁。
* 使用适当的技术来显示可由浏览器禁用的移动或闪烁内容。例如，Graphics Interchange Format (GIF) 或 Animated Portable Network Graphics (APNG) 文件。
* 在网页上提供一个表单控件，让用户能够禁用页面上的所有移动或闪烁内容。
* 如果以上建议均不可行，则可以提供一个链接，以指向包含所有内容但不含任何移动或闪烁内容的页面。

#### 更多信息 - 暂停、停止、隐藏 (2.2.2) {#more-information-pause-stop-hide}

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

#### 用途 - 闪光三次或低于阈值 (2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情况下，闪光的内容会导致光敏性癫痫发作。此成功标准旨在让此类用户能够访问和体验所有内容，而无需担心闪光的内容。

#### 如何达到标准 - 闪光三次或低于阈值 (2.3.1)  {#how-to-meet-three-flashes-or-below-threshold}

应采取措施确保应用以下技术：

* 确保组件在任何一秒内的闪光次数均不超过三次；
* 如果无法满足上述条件，则应在屏幕上以像素为单位将闪光的内容显示在&#x200B;*小块安全区域*&#x200B;内。这块区域的面积通过一个复杂的公式来计算（详见 [G176：尽量缩小闪光区域的面积](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)），因此，仅当闪光的内容&#x200B;*绝对*&#x200B;有必要时，才应使用这种技术。

#### 更多信息 - 闪光三次或低于阈值 (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [了解成功标准 2.3.1](https://www.w3.org/WAI/WCAG21/Understanding/three-flashes-or-below-threshold.html)
* [如何达到成功标准 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/#three-flashes-or-below-threshold)

### 可导航 (2.4) {#navigable}

[准则 2.4 可导航：提供帮助用户导航、查找内容并确定其位置的方法。](https://www.w3.org/TR/WCAG/#navigable)

此准则涉及的是，确保内容便于用户导航且简洁明了。

### 绕过块 (2.4.1)  {#bypass-blocks}

* 成功标准 2.4.1
* A 级
* 绕过块：提供一种机制，绕过多个网页上重复出现的内容块。

#### 用途 - 绕过块 (2.4.1) {#purpose-bypass-blocks}

此成功标准旨在让按顺序浏览内容的人更直接地访问网页的主要内容。网页和应用程序通常包含也会在其他页面或屏幕上显示的内容。重复出现的内容块示例包括但不限于：导航链接、标题图形、菜单和广告画面。就本规定而言，单个字词、短语或单个链接等较小的重复内容不被视为重复块。

#### 如何达到标准 - 绕过块 (2.4.1) {#how-to-meet-bypass-blocks}

遵循[如何达到成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks) 中的准则。

#### 更多信息 - 绕过块 (2.4.1) {#more-information-bypass-blocks}

* [了解成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/Understanding/bypass-blocks.html)
* [如何达到成功标准 2.4.1](https://www.w3.org/WAI/WCAG21/quickref/#bypass-blocks)

### 页面带有标题 (2.4.2)  {#page-titled}

* 成功标准 2.4.2
* A 级
* 页面带有标题：网页带有标题，以描述主题或用途。

#### 用途 - 页面带有标题 (2.4.2)  {#purpose-page-titled}

此成功标准旨在帮助每个人（无论是否患有任何特定障碍缺陷）无需阅读整个页面即可快速识别网页内容。当在不同的浏览器选项卡中打开了多个网页时，这种方法格外有用，因为页面标题会显示在选项卡中，从而可以快速定位。

#### 如何达到标准 - 页面带有标题 (2.4.2)  {#how-to-meet-page-titled}

在 AEM 中创建新 HTML 页面时，可以指定页面标题。应确保标题能够充分描述页面内容和用途，尤其是任何独特方面，以便访客能够快速识别该页面的内容是否与自己的需求切实相关。

您也可以在编辑页面时编辑页面标题，通过&#x200B;**页面信息** - **属性**&#x200B;可访问该设置。

#### 更多信息 - 页面带有标题 (2.4.2) {#more-information-page-titled}

* [了解成功标准 2.4.2](https://www.w3.org/WAI/WCAG21/Understanding/page-titled.html)
* [如何达到成功标准 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/#page-titled)

### 焦点顺序 (2.4.3)  {#focus-order}

* 成功标准 2.4.3
* A 级
* 焦点顺序：如果网页可以按顺序依次导航并且导航顺序会影响含义或操作，则可聚焦组件应该按照不改变含义和可操作性的顺序接收焦点。

#### 用途 - 焦点顺序 (2.4.3) {#purpose-focus-order}

此成功标准旨在确保用户按顺序导航内容时，他们接收到信息的顺序与内容含义一致，并且这种按顺序导航的操作可通过键盘实现。此成功标准可让用户形成与内容一致的心智模型，从而减少混淆。内容中可能存在不同的反映逻辑关系的顺序。例如，在由多个字段和/或步骤组成的在线表单中移动组件反映了内容中的逻辑关系。

#### 如何达到标准 - 焦点顺序 (2.4.3) {#how-to-meet-focus-order}

遵循[如何达到成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order) 中的准则。

#### 更多信息 - 焦点顺序 (2.4.3) {#more-information-focus-order}

* [了解成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/Understanding/focus-order.html)
* [如何达到成功标准 2.4.3](https://www.w3.org/WAI/WCAG21/quickref/#focus-order)

### 链接目的（在上下文中）(2.4.4)  {#link-purpose-in-context}

* 成功标准 2.4.4
* A 级
* 链接目的（在上下文中）：每个链接的目的可以通过单独的链接文本确定，也可以通过链接文本与其以编程方式确定的链接上下文一起确定，除非链接的目的对一般用户而言模糊不清。

#### 用途 - 链接目的（在上下文中）(2.4.4)  {#purpose-link-purpose-in-context}

对于所有用户（无论是否患有某方面的缺陷）而言，通过适当的链接文本清晰地指明链接方向至关重要。这有助于用户决定自己是否切实希望追踪某个链接。对于视力正常的用户而言，当页面上有多个链接时，有意义的链接文本极其有用（尤其当页面包含大量文本时），因为有意义的链接文本能够更加清晰地说明目标页面的功能。使用一些辅助型技术的用户可以在单个页面上生成所有链接的列表，如果链接文本是唯一的且可以提供有用信息，则用户可以轻松地脱离上下文理解链接文本。但是，如果链接无法提供足够的信息来准确描述链接目标位置，则患有认知障碍的视力正常用户可能会感到困惑。

#### 如何达到标准 - 链接目的（在上下文中）(2.4.4) {#how-to-meet-link-purpose-in-context}

首先，确保链接文本清晰地描述了链接目的。

* 错误示例：
   * 文本内容：有关 2010 年秋季晚间课程的详细信息，请单击此处。
   * 原因分析：没有清晰明确地指明链接目标位置。
* 正确示例：
   * 文本内容：2010 年秋季晚间课程 - 详细信息。
   * 原因分析：通过稍微调整链接元素的文本和位置，可以改进链接文本。

链接用词在各个页面中应保持一致，尤其是导航栏的链接。例如，如果特定页面的链接在某个页面中被命名为&#x200B;**出版物**，则在其他页面中也应使用该文本，以确保一致性。

编写文本时，在使用标题属性确保页面上呈现的类似链接提供有关目标位置的唯一信息方面还存在一些问题（例如，“阅读更多”通常是指一系列的不同目标位置）：

* 通常情况下，只有使用鼠标的用户才可以在工具提示弹出框中看到标题属性中包含的文本，而使用键盘或移动设备的用户始终无法看到该文本。
* 屏幕阅读器可以朗读标题属性，但是这项功能可能默认未启用；因此用户可能意识不到标题属性的存在。
* 标题文本的外观很难更改，这就意味着一些用户可能很难或无法阅读该文本。

因此，尽管标题属性可用于为链接提供额外的上下文，但是应务必注意其限制，而且不要将其用作相应链接文本的替代内容。

如果链接是由图像构成的，则应确保该图像的替代文本描述了链接的目标位置。例如，如果将一个书架的图像设置为某人出版物的链接，则替代文本应该写成&#x200B;**张三的出版物**，而不是&#x200B;**书架**。

或者，如果链接锚包含的文本不仅描述了链接的目的，而且还说明了图像元素（这样文本就会显示在图像旁边），则可将图像的 alt 属性设置为空：

```xml
<a href="publications.html">
<img src = "bookshelf.jpg" alt = "" />
John Smith’s publications
</a>
```

>[!NOTE]
>
>以上代码片段仅用于说明目的，建议使用&#x200B;**图像**&#x200B;组件。

虽然提供无需附加上下文即可标识链接目的的链接文本是一种可取的方法，但该方法并不认为始终可行。与上下文无关的链接可用于以下情况，其 HTML 示例详见：[如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)。

* 当链接文本是由紧密相关的链接组成的列表的一部分时，以及当链接周围的列表项提供了足够的上下文时。
* 当可以通过&#x200B;*之前*（而非之后）的段落文本清晰识别链接目的时。
* 当链接包含于数据表内，从而可以通过关联的标题清晰识别链接目的时。
* 当链接列表包含于一系列标题内且标题本身提供了合适的上下文时。
* 当链接列表包含于嵌套的链接内且嵌套链接上面的父列表项提供了合适的上下文时。

在某些情况下，一个页面上会有多个链接（其中每个链接都提供了复杂而又必要的链接方向详情），此时可以为该网页提供一个替代版本，使其显示完全相同的内容，只是其中的链接文本较为简洁。

或者，也可以使用脚本，这样就能够最大限度地减少链接本身中提供的文本；但是，在将位于页面顶部的相应控件激活后，链接文本就会&#x200B;*扩展*&#x200B;成更多的详细信息。类似的方法还有使用 CSS 为视力正常的用户&#x200B;*隐藏*&#x200B;完整的链接，但是仍然将完整的链接呈现给屏幕阅读器用户。与此相关的说明不在本文档的范围之内，但是可以在[更多信息 - 链接目的（在上下文中）(2.4.4)](#more-information-link-purpose-in-context) 部分获取有关如何实现此操作的更多信息。

#### 更多信息 - 链接目的（在上下文中）(2.4.4) {#more-information-link-purpose-in-context}

* [了解成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/Understanding/link-purpose-in-context.html)
* [如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/#link-purpose-in-context)

<!--
* [C7: Using CSS to hide a portion of the link text](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)
-->

### 多种方式 (2.4.5)  {#multiple-ways}

* 成功标准 2.4.5
* AA 级
* 多种方式：除了按照流程或步骤正常来到网页之外，还有其他方法可用于在一组网页中来到所需网页。

#### 用途 - 多种方式 (2.4.5) {#purpose-multiple-ways}

此成功标准旨在让用户能够以最符合其需求的方式找到内容。用户可能会发现一种技术比另一种技术更易于使用或理解。

即便是小型网站，也应为用户提供一些不同的定位方式。对于只有三、四个页面的网站，如果所有页面均链接自主页，则只需在主页上提供所有页面的链接、以及在各自页面上提供前往主页的链接即可，而主页上的链接也可用作站点地图。

#### 如何达到标准 - 多种方式 (2.4.5) {#how-to-meet-multiple-ways}

遵循[如何达到成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways) 中的准则。

#### 更多信息 - 多种方式 (2.4.5) {#more-information-multiple-ways}

* [了解成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/Understanding/multiple-ways.html)
* [如何达到成功标准 2.4.5](https://www.w3.org/WAI/WCAG21/quickref/#multiple-ways)

### 标题和标签 (2.4.6)  {#headings-and-labels}

* 成功标准 2.4.6
* AA 级
* 标题和标签：标题和标签用于描述主题或用途。

#### 用途 - 标题和标签 (2.4.6) {#purpose-headings-and-labels}

此成功标准旨在帮助用户了解网页中包含哪些信息以及这些信息的组织方式。当标题清晰且具有描述性时，用户可以更轻松地找到所寻找的信息，并且可以更轻松地了解内容不同部分之间的关系。描述性标签可帮助用户识别内容中的特定组件。

#### 如何达到标准 - 标题和标签 (2.4.6) {#how-to-meet-headings-and-labels}

遵循[如何达到成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels) 中的准则。

#### 更多信息 - 标题和标签 (2.4.6) {#more-information-headings-and-labels}

* [了解成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/Understanding/headings-and-labels.html)
* [如何达到成功标准 2.4.6](https://www.w3.org/WAI/WCAG21/quickref/#headings-and-labels)

### 焦点可见 (2.4.7)  {#focus-visible}

* 成功标准 2.4.7
* AA 级
* 焦点可见：任何键盘可操作的用户界面都具有这样一种操作模式 - 键盘焦点指示器是可见的。

#### 用途 - 焦点可见 (2.4.7) {#purpose-focus-visible}

此成功标准旨在帮助用户了解当前的键盘焦点在哪个元素。

用户必须能够知道在多个元素中，哪一个元素是当前的键盘焦点所在。如果屏幕上只有一个键盘可操作控件，则应该可以达到成功标准，因为这样的视觉设计只会呈现一个键盘可操作项目。

成功标准中说的“操作模式”，则是考虑到了部分平台可能无法始终显示焦点指示器的情况。在大多数情况下只有一种操作模式，因此，此成功标准可适用。

#### 如何达到标准 - 焦点可见 (2.4.7) {#how-to-meet-focus-visible}

遵循[如何达到成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible) 中的准则。

#### 更多信息 - 焦点可见 (2.4.7) {#more-information-focus-visible}

* [了解成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/Understanding/focus-visible.html)
* [如何达到成功标准 2.4.7](https://www.w3.org/WAI/WCAG21/quickref/#focus-visible)

## 准则 3：可理解 {#principle-understandable}

[准则 3：可理解 - 信息和用户界面操作必须可以理解。](https://www.w3.org/TR/WCAG/#understandable)

### 使文本内容可读且可理解 (3.1)  {#make-text-content-readable-and-understandable}

[准则 3.1 可读：使文本内容可读且可理解。](https://www.w3.org/TR/WCAG/#readable)

### 页面语言 (3.1.1)  {#language-of-page}

* 成功标准 3.1.1
* A 级
* 页面语言：每个网页的默认人类语言都可以采用编程方式来确定。

#### 用途 - 页面语言 (3.1.1)  {#purpose-language-of-page}

此成功标准旨在确保能够正确呈现文本和其他语言内容。对于屏幕阅读器用户而言，这意味着确保内容发音正确；而对于可视浏览器用户而言，这则更可能意味着确保正确显示某些字符集。

#### 如何达到标准 - 页面语言 (3.1.1)  {#how-to-meet-language-of-page}

要达到此成功标准，可以使用页面顶部 `<html>` 元素中的 `lang` 属性来识别网页的默认语言。例如：

* 如果页面采用英语编写，则 `<html>` 元素应该写成：
   `<html lang = “en”>`

* 而要以西班牙语呈现的页面应该采用以下标准：
   `<html lang = “es”>`

在 AEM 中，页面的默认语言是在创建页面时设置的，但是也可以在编辑[页面属性](/help/sites-authoring/editing-page-properties.md)时进行更改。

>[!NOTE]
>
>AEM 针对根语言的变体做了进一步的微调，例如，美式英语 - en-us、英式英语 - en-gb 和加拿大英语 - en-ca。这种详细级别对辅助型技术来说通常是多余的，尽管它可以用于标识页面内容中的区域变化。

#### 更多信息 - 页面语言 (3.1.1) {#more-information-language-of-page}

* [了解成功标准 3.1.1](https://www.w3.org/WAI/WCAG21/Understanding/language-of-page.html)
* [如何达到成功标准 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/#language-of-page)
* 代码基于 ISO 639-1。[W3 Schools 站点](https://www.w3schools.com/tags/ref_language_codes.asp)提供了各种语言的更广泛代码列表。

### 局部语言 (3.1.2)   {#language-of-parts}

* 成功标准 3.1.2
* AA 级
* 局部语言：内容中每个段落或短语的人类语言可以采用编程方式来确定，但专有名词、术语、不确定语言的词语，以及周围文本的本地语言中包含的词语或短语除外。

#### 用途 - 局部语言 (3.1.2)  {#purpose-language-of-parts}

此成功标准的用途与[页面语言](#language-of-page)的成功标准类似，不同之处在于此成功标准适用于在单个页面包含多语言内容的网页（例如，因为引用其他语言或者使用不常见的外来词而包含其他语言）。

应用此成功标准的页面允许：

* 盲文转换软件插入重音字符。
* 屏幕阅读器朗读那些具有特殊字符或未使用在页面级别标识的默认语言的单词。
* Google Translate 等翻译工具准确地将内容从一种语言翻译成另外一种语言。

#### 如何达到标准 - 局部语言 (3.1.2)  {#how-to-meet-language-of-parts}

`lang` 属性可用于标识内容语言的更改。例如，引用的德语（ISO 639-1 代码“de”）可以采用以下方式表示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
>
>现成的实例不支持 blockquote。可以开发支持该功能的自定义组件。

同样，如果通过以下方式使用 `span` 元素，则浏览器可以准确地呈现不常见的外来词或短语：

```xml
<p>The only French phrase I know is <span lang = “fr”>je ne sais quoi</code>.</p>
```

>[!NOTE]
>
>如果包含使用不同语言的人名或城市，或者使用默认语言中常用的外来词或短语（如英语中的 *schadenfreude*），则不必遵循此成功标准。

要添加包含相应语言的 span 元素，可以在 RTE 的源代码编辑模式下手动编辑 HTML 标记，以将其写成如上显示的方式。或者，系统管理员可以在RTE中包含`lang`属性（请参阅[添加对其他HTML元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

#### 更多信息 - 局部语言 (3.1.2) {#more-information-language-of-parts}

* [了解成功标准 3.1.2](https://www.w3.org/WAI/WCAG21/Understanding/language-of-parts.html)
* [如何达到成功标准 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/#language-of-parts)

### 可预测 (3.2) {#predictable}

[准则 3.2 可预测：使网页以可预见的方式显示和操作。](https://www.w3.org/TR/WCAG/#predictable)

此准则涉及的是，确保网页的外观与操作保持一致。

### 聚焦 (3.2.1)  {#on-focus}

* 成功标准 3.2.1
* A 级
* 聚焦：当任何用户界面组件收到焦点时，它不会发起对上下文的更改。

#### 用途 - 聚焦 (3.2.1) {#purpose-on-focus}

此成功标准旨在确保访客在以自己的方式浏览文档时，功能是可预测的。任何能够在收到焦点时触发事件的组件，均不得更改上下文。组件收到焦点时更改上下文的示例，包括但不限于：

* 组件收到焦点时自动提交表单；
* 组件收到焦点时启动新窗口；
* 组件收到焦点时，焦点转移到另一个组件；

焦点可以通过键盘（例如，通过 Tab 键前往控件）或鼠标（例如，单击文本字段）移到控件。将鼠标移到控件上方不会移动焦点，除非脚本会实施此行为。请注意，对于某些类型的控件，单击控件也可能会激活该控件（例如按钮），这反过来又会发起对上下文的更改。

#### 如何达到标准 - 聚焦 (3.2.1) {#how-to-meet-on-focus}

遵循[如何达到成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus) 中的准则。

#### 更多信息 - 聚焦 (3.2.1) {#more-information-on-focus}

* [了解成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/Understanding/on-focus.html)
* [如何达到成功标准 3.2.1](https://www.w3.org/WAI/WCAG21/quickref/#on-focus)

### 输入 (3.2.2)  {#on-input}

* 成功标准 3.2.2
* A 级
* 输入：更改任何用户界面组件的设置，不会自动导致上下文更改，除非在使用组件之前，已告知用户该行为。

#### 用途 - 输入 (3.2.2) {#purpose-on-input}

此成功标准旨在确保输入数据或选择表单控件这样的操作具有可预见的效果。更改任何用户界面组件的设置，就会更改该控件的某些方面，当用户不再与界面交互时，这些方面的更改会一直存在。因此，选中复选框、在文本字段中输入文本，或更改列表控件中的选定项会更改其设置，但激活链接或按钮则不会更改其设置。上下文更改可能会给那些不容易感知更改或容易被更改分散注意力的用户造成困惑。只有当明确告知为响应用户操作而会发生上下文更改时，此类更改才是恰当的。

#### 如何达到标准 - 输入 (3.2.2) {#how-to-meet-on-input}

遵循[如何达到成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input) 中的准则。

#### 更多信息 - 输入 (3.2.2) {#more-information-on-input}

* [了解成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/Understanding/on-input.html)
* [如何达到成功标准 3.2.2](https://www.w3.org/WAI/WCAG21/quickref/#on-input)

### 一致的导航 (3.2.3)  {#consistent-navigation}

* 成功标准 3.2.3
* AA 级
* 一致的导航：在一组网页内的多个网页上重复应用的导航机制，这些网页每次均以相同的相对顺序重复出现，除非用户自发更改浏览顺序。

#### 用途 - 一致的导航 (3.2.3) {#purpose-consistent-navigation}

此成功标准旨在鼓励使用一致的呈现和布局，当用户与一组网页内的重复内容进行交互，并且需要多次找到特定信息或功能时，这种一致的呈现和布局会很有帮助。视力欠佳的人使用屏幕放大功能每次显示屏幕的一小部分时，通常会使用视觉提示和页面边界来快速找到重复内容。对于使用空间记忆或设计中的视觉提示来找到重复内容的视觉用户而言，按相同顺序呈现重复内容也非常重要。

请务必注意，本节中使用了“相同顺序”这种说法，这并不意味着不能使用子导航菜单，或者不能使用二级导航块或页面结构。相反，此成功标准旨在帮助与网页中重复内容进行交互的用户预测其寻找内容的位置，并在再次遇到时更快地找到这些内容。

用户可以通过使用自适应用户代理或通过设置首选项来发起顺序更改，以对他们最有用的方式呈现信息。

#### 如何达到标准 - 一致的导航 (3.2.3) {#how-to-meet-consistent-navigation}

遵循[如何达到成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation) 中的准则。

#### 更多信息 - 一致的导航 (3.2.3) {#more-information-consistent-navigation}

* [了解成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/Understanding/consistent-navigation.html)
* [如何达到成功标准 3.2.3](https://www.w3.org/WAI/WCAG21/quickref/#consistent-navigation)

### 一致的标识 (3.2.4)  {#consistent-identification}

* 成功标准 3.2.4
* A 级
* 一致的标识：一组网页内具有相同功能的组件，均采用一致的方式进行标识。

#### 用途 - 一致的标识 (3.2.4) {#purpose-consistent-identification}

此成功标准旨在确保采用一致的方式标识一组网页内重复出现的功能组件。使用屏幕阅读器的用户在操作网站时所使用的一种策略是，依赖他们对可能出现在不同网页上的功能的熟悉程度，且这种依赖程度很深。如果相同的功能在不同网页上具有不同的标签（或者更通俗地讲，具有不同的访问名称），则网站的使用难度会显著增加。这也可能会令人困惑，并增加认知困难人士的认知负担。因此，一致的标签将有所帮助。

此一致性要求的适用范围也包括替代文本。如果图标或其他非文本项目具有相同的功能，则其相应的替代文本也应保持一致。

如果某个网页上有两个组件的功能与一组网页内另一个页面上的组件功能相同，则所有这 3 个组件都必须保持一致。因此，同一页面上的那两个组件将保持一致。

尽管在单个网页内始终保持一致是理想的最佳做法，但准则 3.2.4 仅解决一组网页内的一致性问题（该组网页内的多个页面上包含重复出现的某些内容）。

#### 如何达到标准 - 一致的标识 (3.2.4) {#how-to-meet-consistent-identification}

遵循[如何达到成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification) 中的准则。

#### 更多信息 - 一致的标识 (3.2.4) {#more-information-consistent-identification}

* [了解成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/Understanding/consistent-identification.html)
* [如何达到成功标准 3.2.4](https://www.w3.org/WAI/WCAG21/quickref/#consistent-identification)

### 辅助输入 (3.3) {#input-assistance}

[准则 3.3 辅助输入：帮助用户避免和更正错误。](https://www.w3.org/TR/WCAG/#input-assistance)

### 错误标识 (3.3.1)  {#error-identification}

* 成功标准 3.3.1
* A 级
* 错误标识：如果自动检测到输入错误，则会识别出错的项目，并以文本形式向用户描述该错误。

#### 用途 - 错误标识 (3.3.1) {#purpose-error-identification}

此成功标准旨在确保用户知道发生了错误，并可确定错误的具体内容。错误消息应尽可能具体和明确。表单提交失败时，重新显示表单并指示错误字段并不足以让某些用户感知发生了错误。例如，屏幕阅读器用户在遇到某个指示器之前，不会知道内容中存在错误。他们可能会在遇到错误指示器之前就完全放弃表单，认为页面根本无法正常工作。根据 WCAG 中的定义，[输入错误](https://www.w3.org/TR/WCAG/#dfn-input-error)是用户提供的不可接受的信息。这包括：

网页要求提供但用户忽略了的信息，或者用户虽已提供但不是要求的数据格式或允许的值。例如：

* 用户未能在省/自治区/直辖市、地区等字段输入正确的缩写；
* 用户输入的不是有效的省/自治区/直辖市缩写；
* 用户输入的邮政编码不存在；
* 用户输入的出生日期在未来 2 年之后；
* 用户在只接受数字的电话号码字段中输入字母字符或括号；
* 用户输入的竞价低于上一个竞价或最低竞价增幅。

#### 如何达到标准 - 错误标识 (3.3.1) {#how-to-meet-error-identification}

遵循[如何达到成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification) 中的准则。

#### 更多信息 - 错误标识 (3.3.1) {#more-information-error-identification}

* [了解成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/Understanding/error-identification.html)
* [如何达到成功标准 3.3.1](https://www.w3.org/WAI/WCAG21/quickref/#error-identification)

### 标签或说明 (3.3.2) {#labels-or-instructions}

* 成功标准 3.3.2
* A 级
* 标签或说明：当内容需要用户输入时，提供标签或说明。

#### 用途 - 标签或说明 (3.3.2)  {#purpose-labels-or-instructions}

在提升界面易用性的最佳实践中，一种基本的做法是提供说明来帮助用户完成表单。这种做法对于患有视觉障碍或认知障碍的用户而言特别有用，否则这类用户可能难以理解表单的布局以及要在特定的表单字段中提供的数据种类。

##### 表单

在 AEM WKND 演示项目中，当向页面添加表单组件（如&#x200B;**文本字段**）时，会添加默认标签。此默认标题视组件类型而定，您也可以在该字段编辑对话框的&#x200B;**标题与文本**&#x200B;选项卡中添加自己的标题。应务必确保标签能够帮助用户理解与每个表单组件相关的数据。

此&#x200B;**标题**&#x200B;字段必须用于字段元素，因为该字段提供了适用于辅助型技术的标签。只在字段旁边用文本编写一个标签是不够的。

对于某些形式的组件而言，还可以使用&#x200B;**隐藏标题**&#x200B;复选框来隐藏显示的标签。通过这种方式隐藏的标签仍可用于辅助型技术，但不会显示在屏幕上。尽管在某些情况下这不失为一种好方法，但是通常最好尽可能保留可视的标签，因为有些用户可能只查看屏幕上很小的一部分（每次一个字段），并且需要借助标签来准确地识别字段。

###### 图像按钮 {#image-buttons}

使用了图像按钮（如 WKND 项目的&#x200B;**图像按钮**&#x200B;组件）后，编辑对话框&#x200B;**标题与文本**&#x200B;选项卡中的&#x200B;**标题**&#x200B;字段实际上会为图像提供替换文本，而不是提供标签。因此，在以下示例中，包含文本 `Submit` 的图像，其替代文本就是 `Submit`，该文本是使用编辑对话框中的&#x200B;**标题**&#x200B;字段添加的。

###### 表单字段组 {#groups-of-form-fields}

在 WKND 项目中，如果存在一组相关控件（如&#x200B;**单选按钮组**），则可能需要该组以及单个控件的标题。在 AEM 中添加一组单选按钮时，**标题**&#x200B;字段会提供此组标题，而单个标题会在创建单选按钮（**项目**）时指定。

但是，组标题和单选按钮本身之间并没有编程关联。模板编辑器需要将标题包装在必需的 `fieldset` 和 `legend` 标记中，以便创建此关联，而且该操作只能通过编辑页面源代码来完成。或者，系统管理员也可以添加对这些元素的支持，以使它们显示在&#x200B;**字段属性**&#x200B;对话框中（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

###### 有关表单的其他考虑事项 {#additional-considerations-for-forms}

如果必须按照特定的格式输入数据，应在标签文本中予以清楚说明。例如，如果必须以 `DD-MM-YYYY` 格式输入日期，应在标签中特别指明这一点。这意味着当屏幕阅读器用户遇到此类字段时，阅读器会自动将标签以及与格式相关的其他信息一并读出。

如果必须输入表单字段，请在标签中使用“必填”一词来说明。AEM 会为必填字段添加一个星号，但是最好在标签本身中也包含 `required` 一词（在编辑对话框的&#x200B;**标题**&#x200B;字段中）。

标签的位置也非常重要，因为它有助于用户找到对应的字段。当用户面对复杂的表单时，这显得尤为重要。应遵循以下约定：

* 复选框或单选按钮：
标签放在紧靠字段右侧的位置。
* 所有其他表单组件（例如，文本框和组合框）：
标签放在紧靠字段上方或左侧的位置。

在功能非常有限的简单表单中，可以相应地标记 `Submit` 按钮，以将其用作相邻字段的标签（如 `Search`）。当很难找到用于提供标签文本的空间时，这种方法非常有用。

#### 更多信息 - 标签或说明 (3.3.2)  {#more-information-labels-or-instructions}

* [了解成功标准 3.3.2](https://www.w3.org/WAI/WCAG21/Understanding/labels-or-instructions.html)
* [如何达到成功标准 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/#labels-or-instructions)

### 错误建议 (3.3.3)  {#error-suggestion}

* 成功标准 3.3.3
* AA 级
* 键盘：如果自动检测到输入错误并且知道有关更正的建议，则向用户提供建议，除非这会危及内容的安全性或用途。

#### 用途 - 错误建议 (3.3.3) {#purpose-error-suggestion}

此成功标准旨在确保用户在可能的情况下接收合理建议以便更正输入错误。在 WCAG 中，[输入错误](https://www.w3.org/TR/WCAG/#dfn-input-error)的定义是指系统“不接受的用户提供的信息”。系统不接受的信息示例包括：要求提供但用户忽略了的信息，以及用户虽已提供但不是要求的数据格式或允许的值。

成功标准 3.3.1 会提供错误通知。然而，认知困难的人士可能很难理解如何更正错误。患有视觉障碍的人士可能无法明白到底应该如何更正错误。如果表单提交失败，用户或许会放弃表单，因为他们可能不确定如何更正错误，即使他们知道已经发生错误。

内容作者可以提供错误描述，或者用户代理可以根据特定于技术的、通过编程方式确定的信息来提供错误描述。

#### 如何达到标准 - 错误建议 (3.3.3) {#how-to-meet-error-suggestion}

遵循[如何达到成功标准 3.3.3](https://www.w3.org/WAI/WCAG21/quickref/#error-suggestion) 中的准则。

#### 更多信息 - 错误建议 (3.3.3) {#more-information-error-suggestion}

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

#### 用途 - 错误预防（法律、金融、数据）(3.3.4) {#purpose-error-prevention-legal-financial-data}

此成功标准旨在帮助残障用户在执行无法撤销的操作时，避免因错误而造成严重后果。例如，购买不可退款的机票，或者提交订单在经纪帐户中购买股票，这些都是可能产生严重后果的金融交易。如果用户弄错航空旅行日期，他/她最终可能会拿到一张无法改签的日期错误的机票。如果用户在要购买的股票数量上出错，他/她最终可能会购买超出预期数量的股票。这两种错误涉及的交易都是立即发生且事后无法更改，并且可能代价高昂。同样，如果用户无意中修改或删除了存储在数据库中并且以后需要访问的数据（如旅行服务网站中自己的全部旅行档案），这也可能是一个无法挽救的错误。当涉及修改或删除“用户可控”数据时，此项标准的目的是防止大量丢失数据，例如删除一份文件或记录，而不是要求在每次保存命令时进行确认，也不是指对文档、记录或其他数据进行简单的创建或编辑。

残障用户可能更容易出错。患有阅读障碍的人可能会颠倒数字和字母，而患有运动障碍的人则可能会意外按错按键。提供撤销操作这一功能，让用户能够纠正可能导致严重后果的错误。提供复核和更正信息这一功能，让用户在采取可能会造成严重后果的行动之前，有机会及时发现错误。

用户可控数据是指用户可查看的数据，用户可以通过有意的操作来改变和/或删除这些数据。用户控制此类数据的示例可能包括：更新用户帐户的电话号码和地址，或者从网站删除过去发票的记录。它不是指用户无法直接查看或与之交互的数据，例如互联网日志记录和搜索引擎监测数据。

#### 如何达到标准 - 错误预防（法律、金融、数据）(3.3.4) {#how-to-meet-error-prevention-legal-financial-data}

遵循[如何达到成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data) 中的准则。

#### 更多信息 - 错误预防（法律、金融、数据）(3.3.4) {#more-information-error-prevention-legal-financial-data}

* [了解成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/Understanding/error-prevention-legal-financial-data.html)
* [如何达到成功标准 3.3.4](https://www.w3.org/WAI/WCAG21/quickref/#error-prevention-legal-financial-data)

## 原则 4：强健 {#principle-robust}

[原则 4：强健 - 内容必须足够强健，以供包括辅助技术在内的各种用户代理进行解读。](https://www.w3.org/TR/WCAG/#robust)

### 兼容 (4.1) {#compatible}

[准则 4.1 兼容：最大限度地兼容当前和未来用户代理，包括辅助技术。](https://www.w3.org/TR/WCAG/#compatible)

最大限度地兼容当前和未来用户代理，包括辅助技术。

### 解析 (4.1.1)  {#parsing}

* 成功标准 4.1.1
* A 级
* 解析：在使用标记语言实施的内容中，元素具有完整的开始和结束标签，元素根据其规范进行嵌套，元素不包含重复属性，所有 ID 都是唯一的，除非规范允许。

#### 用途 - 解析 (4.1.1) {#purpose-parsing}

此成功标准旨在确保用户代理（包括辅助技术）能够准确地解读和分析内容。如果内容无法解析为数据结构，则不同的用户代理可能会以不同的方式呈现内容，或者完全无法解析内容。一些用户代理会使用“修复技术”来呈现编码欠佳的内容。

由于修复技术因用户代理而异，因此作者不能假设内容将被准确地解析为数据结构，或者内容将被包括辅助技术在内的专业用户代理正确呈现，除非内容是根据该技术的正式语法所定义的规则创建的。在标记语言中，元素和属性语法中的错误以及未提供正确嵌套的开始/结束标签，会导致使用户代理无法可靠地解析内容的错误。因此，成功标准要求内容只能使用正式语法的规则来解析。

#### 如何达到标准 - 解析 (4.1.1) {#how-to-meet-parsing}

遵循[如何达到成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing) 中的准则。

#### 更多信息 - 解析 (4.1.1) {#more-information-parsing}

* [了解成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/Understanding/parsing.html)
* [如何达到成功标准 4.1.1](https://www.w3.org/WAI/WCAG21/quickref/#parsing)

### 名称、角色、值 (4.1.2)  {#name-role-value}

* 成功标准 4.1.2
* A 级
* 名称、角色、值：对于所有用户界面组件(包括但不限于：表单元素、链接以及由脚本生成的组件)，其名称和角色可以通过编程方式来确定；可由用户设置的状态、属性和值可以通过编程方式来设置；而且用户代理（包括辅助技术）可以收到这些项目的更改通知。

#### 用途 - 名称、角色、值 (4.1.2) {#purpose-ame-role-value}

此成功标准旨在确保辅助技术 (AT) 能够收集关于内容中用户界面控件状态的信息，激活（或设置）并跟踪内容中用户界面控件的状态。

当使用来自无障碍访问技术的标准控件时，此过程非常简单。如果根据规范使用用户界面元素，则符合此规定的条件。（请参阅下面的成功标准 4.1.2 示例）

但是，如果创建了自定义控件，或者界面元素被（使用代码或脚本）编程为具有不同于常规的角色和/或功能，则需要采取其他措施以确保控件可向辅助技术提供重要信息并允许辅助技术控制这些重要信息。

用户界面控件的一个特别重要的状态是它是否具有焦点。控件的焦点状态可以通过编程方式确定，并且会向用户代理和辅助技术发送关于焦点状态的变更通知。用户界面控件状态的其他示例包括：复选框或单选按钮是否已被选中，或者可折叠的树或列表节点是否已展开或折叠。

#### 如何达到标准 - 名称、角色、值 (4.1.2) {#how-to-meet-ame-role-value}

遵循[如何达到成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value) 中的准则。

#### 更多信息 - 名称、角色、值 (4.1.2) {#more-information-ame-role-value}

* [了解成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/Understanding/name-role-value.html)
* [如何达到成功标准 4.1.2](https://www.w3.org/WAI/WCAG21/quickref/#name-role-value)
