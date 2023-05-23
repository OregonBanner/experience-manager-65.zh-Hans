---
title: 创建辅助内容（WCAG 2.0 符合性）
seo-title: Creating Accessible Content (WCAG 2.0 Conformance)
description: WCAG 2.0 包含一系列非技术层面的准则及成功标准，旨在确保残障人士能够访问并使用 Web 内容。
seo-description: WCAG 2.0 consists of a set of technology independent guidelines and success criteria to help make web content accessible to, and usable by, persons with disabilities.
page-status-flag: de-activated
uuid: c2c0cac0-2a9f-478d-8261-e8cc894aae34
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 378bc33d-ab6c-4651-9688-102c961561fc
exl-id: 01c69aa9-2623-42dc-9e2d-62bc5e01cf0e
source-git-commit: ce6d24e53a27b64a5d0a9db2e4b6672bd77cf9ec
workflow-type: tm+mt
source-wordcount: '9153'
ht-degree: 37%

---

# 创建辅助内容（WCAG 2.0 符合性）{#creating-accessible-content-wcag-conformance}

>[!CAUTION]
>
>由於Classic UI在AEM 6.4中已過時，此頁面上的內容尚未針對WCAG 2.1更新。
>
>如需與AEM和WCAG 2.1相關的詳細資訊，請參閱下列頁面：
>
>* [AEM與網頁協助工具准則](/help/managing/web-accessibility.md)
>* [WCAG 2.1 快速指南](/help/managing/qg-wcag.md)
>* [创建无障碍内容（WCAG 2.1 合规性）](/help/sites-authoring/creating-accessible-content.md)


WCAG 2.0 包含一系列非技术层面的准则及成功标准，旨在确保残障人士能够访问并使用 Web 内容。

>[!NOTE]
>
>另请参阅：
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [配置富文本编辑器以创建辅助内容](/help/sites-administering/rte-accessible-content.md)
>


這些指南根據三個一致性等級進行分級：A級（最低）、AA級和AAA級（最高）。 簡言之，層級的定義如下：

* **级别 A：**&#x200B;您的站点满足基本的、最低级别的无障碍性。要达到此级别，需满足所有级别 A 成功标准。
* **AA級：** 這是您努力追求的理想無障礙環境支援等級，其中您的網站可達到更高的無障礙環境支援等級，因此大部分使用者都可使用大部分的技術。 为达到此级别，所有 A 级和 AA 级成功标准均已满足。
* **AAA 级：**&#x200B;您的网站达到了高水平的可访问性。 要达到此级别，需满足所有级别 A、级别 AA 和级别 AAA 成功标准。

在创建站点时，您应该大体上确定希望自己的站点符合哪个等级。

以下部分介绍 [WCAG 2.0 准则](https://www.w3.org/TR/WCAG20/#guidelines)以及[符合](https://www.w3.org/TR/UNDERSTANDING-WCAG20/conformance.html) A 级和 AA 级的相关成功标准。

>[!NOTE]
>
>由於某些型別的內容無法滿足所有AAA級成功標準，因此不建議將此符合程度作為一般原則來要求。

>[!NOTE]
>
>本檔案使用下列內容：
>
>* [WCAG 2.0 准则](https://www.w3.org/TR/WCAG20/#guidelines)的简称。
>* 中使用的編號 [WCAG 2.0指引](https://www.w3.org/TR/WCAG20/#guidelines) 以協助與WCAG網站進行交叉參照。
>


## 准则 1：可感知 {#principle-perceivable}

[准则 1：可感知 – 信息和用户界面组件必须以可感知的方式呈现给用户。](https://www.w3.org/TR/WCAG20/#perceivable)

### 替换文本 (1.1) {#text-alternatives}

[指南 1.1 文本替代：为任何非文本内容提供替换文本，以便可以将其更改为人们需要的其他形式，例如大字体、盲文、语音、符号或更简单的语言。](https://www.w3.org/TR/WCAG20/#text-equiv)

### 非文字內容(1.1.1) {#non-text-content}

* 成功标准 1.1.1
* A 级
* 非文本内容：呈现给用户的所有非文本内容都具有相同用途的替换文本，以下所列情况除外。

#### 用途 – 非文本内容 (1.1.1) {#purpose-non-text-content}

網頁上的資訊可以用許多不同的非文字格式提供，例如圖片、影片、動畫、圖表和圖形。失明或嚴重視力障礙的人無法看到非文字內容，但他們可以透過熒幕閱讀器閱讀文字內容，或透過盲文顯示裝置以觸覺形式呈現文字內容。 因此，透過以圖形格式提供文字替代內容，看不到圖形內容的人可以存取內容所提供的對等版本資訊。

另一個實用的優點是，替代文字功能可讓搜尋引擎技術為非文字內容編制索引。

#### 如何達到標準 — 非文字內容(1.1.1) {#how-to-meet-non-text-content}

对于静态图形，基本的要求是为图形提供对等的替换文本。此方法的完成位置 **替代文字** 欄位：

>[!NOTE]
>
>一些现成的组件（如&#x200B;**轮播**&#x200B;和&#x200B;**幻灯片**&#x200B;放映）不提供向图像添加替代文本描述的方法。為您的AEM執行個體實作這些元件的版本時，您的開發團隊應設定這些元件以支援 `alt` 屬性。 这样做可确保作者可以将其添加到该内容中（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

此 **替代文字** 欄位位於 **進階** 的影像屬性標籤 **影像** 元件對話方塊：

![傳統UI中影像元件的「編輯」對話方塊；顯示「替代文字」欄位。](assets/chlimage_1-17a.png)

AEM新增 **替代文字** 預設為影像。 對於傳統UI，建立預設屬性的方式有兩種不同的情況，但預設值可能不足以作為替代值，並且可能必須在中編輯 **進階** 影像屬性索引標籤：

* 文件:

影像會從使用者的硬碟上傳。 如果您將影像元件新增至頁面，然後從硬碟或其他來源選擇影像，預設值為 **替代文字** 是 `file`. 此值必須在 **進階** 影像屬性索引標籤。 同樣地，此值不會顯示在 **替代文字** 欄位，但是當值變更時，新值會顯示在「 」欄位中。

* 资产:

從數位資產存放庫新增影像。 如果您將影像從數位資產存放庫拖曳至網頁，則 **標題** 和 **替代文字** 該影像的值取自該影像的中繼資料。

>[!NOTE]
>
>在上述兩種情況下，預設值 **替代文字** 值在中不可見 **進階影像屬性** 標籤。 若要變更預設值，只需在 **替代文字** 欄位。

>[!NOTE]
>
>如果您的影像純粹是裝飾性的(請參閱 [建立良好的替代文字](#creating-good-text-alternatives))，則可在 **替代文字** 使用空格鍵的欄位。 這樣做會建立一個空白 `alt` 屬性，提示熒幕閱讀程式忽略影像。

#### 创建有效的替换文本 {#creating-good-text-alternatives}

非文字內容有多種形式，因此替代文字的值取決於圖形在網頁中所扮演的角色。 一些一般經驗法則包含下列內容：

* 替代文字應簡明扼要，但清楚擷取非文字內容所提供的基本資訊。
* 應避免過長的說明（超過100個字元）。 如果替代文字需要更多細節：

   * 在替换文本中提供简短的描述
   * 同时，在同一页面的其他位置或在一个单独的网页中提供更加详尽的描述文本。然后，为该图像创建一个链接，或者在图像旁边放置一个文本链接，以便链接到该单独的描述。

* 替换文本不应复制同一页面邻近位置以文本形式提供的内容。请切记，许多图像的作用是解释说明页面文本中已涵盖的要点，因此详尽的替换文本可能已经存在。
* 如果非文字內容是另一個頁面或檔案的連結，且沒有其他文字構成相同連結的一部分，則影像的替代文字必須指出連結的目的地。 它不能描述图像。
* 如果非文字內容包含在按鈕元素中，並且沒有文字構成相同按鈕的一部分，則影像的替代文字必須指示按鈕的功能，而不是說明影像。
* 您可以為影像指定空白(null)的替代文字，但前提是影像沒有替代文字。 例如，它是純粹的裝飾性圖形。 或者，如果頁面文字中已存在對等文字。

此 [W3C草稿：提供實用替代文字的HTML5技術](https://html.spec.whatwg.org/multipage/images.html#alt) 提供更多詳細資訊，以及針對不同型別影像提供適當替代文字的範例。

以下特定类型的非文本内容可能需要替换文本：

* 說明像片：

這些是人物、物件或地點的影像。 請思考像片在頁面中的角色；適當的對等文字可能是 *像片 [物件]*，但可能取決於周圍的文字。

* 圖示：

傳達特定資訊的小圖形符號（圖形）。 必須在頁面和網站上一致地使用它們。 頁面上或網站上的所有圖示例項都應使用相同的簡短替代文字，除非這樣做會造成相鄰文字不必要的重複。

* 圖表與圖形：

這些通常代表數值資料。 因此，提供替代文字的一個選項可能是包含圖表或圖形中顯示的主要趨勢的簡短摘要。 如有需要，也可在文字中使用 **說明** 中的欄位 **進階** 影像屬性索引標籤。 此外，还可以在页面或站点的其他位置以表形式提供源数据。

![圖表範例。 以下為提供替代方案的最佳方法。](assets/chlimage_1-2a.jpeg)

若要提供此範例圖表的替代方法，請新增簡明的 `alt` 文字置入影像本身，然後以全文字替代文字跟隨影像。

```xml
<p><img src="figure1.gif" alt="Figure 1" ></p>
<p> Figure 1. Distribution of Articles by Journal Category.
Pie chart: Language=68%, Education=14% and Science=18%.</p>
```

>[!NOTE]
>
>上述程式碼片段僅用於說明順序。 使用 **影像** 元件，而非 `img src` 上面使用的參考。

在AEM中，您可以使用 **替代文字** 和 **說明** 影像設定對話方塊中的欄位 — 如所示 [如何達到標準 — 非文字內容(1.1.1)](#how-to-meet-non-text-content).

* 地圖、圖表、流程圖：

用於提供空間資料的圖形(例如。 要支持描述对象或进程之间的关系)，请确保以文本格式提供关键消息。对于映射，提供等效完整文本可能不太现实，但如果提供映射来作为帮助相关人员找到特定位置的一种方法，则映射图像的替换文本可以简短地指示为 *X 映射*，然后在页面其他位置的文本中或者通过&#x200B;**图像**&#x200B;组件&#x200B;**高级**&#x200B;选项卡中的&#x200B;**描述**&#x200B;字段提供该特定位置的说明。

* 驗證碼：

驗證碼是 *完全自動化的公用圖靈測試，區分電腦和人類*. 這是用於網頁的安全性檢查，可區分人類與惡意軟體，但可能會導致存取障礙。 這些影像需要使用者描述他們所看到的內容，以便通過安全性測試。 为这些图像提供替代文本是不可能的，因此必须思考出非图形的替代解决方案。

W3C提供幾個建議，例如： 这些方法中的每一种都有其自身的优点和缺点。

    *邏輯謎題
    *使用聲音輸出而非影像
    *限制使用帳戶和垃圾郵件篩選器。

* 背景影像：

這些影像是使用階層式樣式表(CSS)而不是HTML來達成。 無法指定替代文字值。 因此，背景影像不應提供重要的文字資訊，即便提供，頁面文字中也必須提供此資訊。

不過，當影像無法顯示時，請務必顯示替代背景。

>[!NOTE]
>
>背景和前景文字之間應該要有適當等級的對比。 以下將對此對比進行更詳細的討論 [對比（最小） (1.4.3)](#contrast-minimum).

#### 更多資訊 — 非文字內容(1.1.1) {#more-information-non-text-content}

* [了解成功标准 1.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/text-equiv-all.html)
* [如何达到成功标准 1.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#text-alternatives)
* [W3C：提供實用替代文字的HTML5技術](https://html.spec.whatwg.org/multipage/images.html#alt)
* [驗證碼的W3C說明和替代方案](https://www.w3.org/TR/turingtest/)

### 基于时间的媒体 (1.2) {#time-based-media}

[准則1.2以時間為基礎的媒體：提供以時間為基礎的媒體替代方案。](https://www.w3.org/TR/WCAG20/#text-equiv)

此資訊會處理以下網路內容： *基於時間*. 這涵蓋使用者可播放的內容（例如視訊、音訊和動畫內容），並且可以是預先錄製或即時資料流。

### 純音訊和純視訊（預先錄製）(1.2.1) {#audio-only-and-video-only-pre-recorded}

* 成功标准 1.2.1
* A 级
* 纯音频和纯视频（预先录制）：对于预先录制的纯音频媒体和预先录制的纯视频媒体，均存在以下情况，除非音频或视频就是文本的替代媒体 ，且明确进行了如下标记：

   * 僅限預先錄製的音訊：提供時間型媒體的替代方案，為預先錄製的僅限音訊內容提供同等資訊。
   * 僅限預先錄製的視訊：提供時間型媒體的替代方案或音軌，為預先錄製的僅限視訊內容提供同等資訊。

#### 用途 — 純音訊和純視訊（預先錄製）(1.2.1) {#purpose-audio-only-and-video-only-pre-recorded}

以下用户可能会遇到音频和视频的无障碍问题：

* 沒有音軌或音軌不足以通知視訊或動畫中發生的事情時，患有視覺障礙的人；
* 有聽力障礙或耳聾且聽不到音軌的人；
* 可以聽到音軌但不瞭解說話內容的人（例如，因為這是他們不瞭解的語言）。

使用不支援以特定媒體格式(例如AdobeFlash)播放內容的瀏覽器或裝置的人也可能無法播放視訊或音訊。

以不同格式提供此資訊，例如文字（或沒有音訊的視訊）可讓無法存取原始內容的人存取這些資訊。

#### 如何達到標準 — 純音訊和純視訊（預先錄製）(1.2.1) {#how-to-meet-audio-only-and-video-only-pre-recorded}

* 如果内容是预先录制的不含视频的音频（如播客）：

   * 提供緊接在內容之前或之後的音訊內容文字記錄連結。

   成績單應該是一個HTML頁面，其中包含所有口語和重要的非口語內容的對等文字。 它應該也會指出說話者、設定描述、聲音表達，以及其他重要音訊的描述。

* 如果內容為動畫或預先錄製的無音訊視訊：

   * 提供緊接在內容之前或之後的連結，以提供視訊所提供資訊的同等文字說明
   * 或是常用的音訊格式（例如MP3）中的對等音訊描述。

>[!NOTE]
>
>如果音訊或視訊內容是作為網頁上其他格式內容的替代品而提供，則不需要遵循上述要求。 例如，如果影片說明文字指示的清單，則此影片不需要替代文字，因為文字指示已經充當影片的替代文字。

在AEM網頁中插入多媒體(尤其是Flash內容)類似於插入影像。 不過，由於多媒體內容遠不止是靜態影像，因此有各種不同的設定和選項可用來控制多媒體的播放方式。

>[!NOTE]
>
>如果将多媒体与信息性内容结合使用，则也必须创建替代内容的链接。例如，要加入文本记录，应创建一个用于显示记录的 HTML 页面，然后在音频内容旁边或下方添加一个链接。

#### 更多信息 - 纯音频和纯视频（预先录制）(1.2.1) {#more-information-audio-only-and-video-only-pre-recorded}

* [了解成功标准 1.2.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-av-only-alt.html)
* [如何达到成功标准 1.2.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)

### 字幕（預先錄製）(1.2.2) {#captions-pre-recorded}

* 成功标准 1.2.2
* A 级
* 字幕（预先录制）：为同步媒体中所有预先录制的音频内容提供了字幕，除非该媒体是文本的替代媒体，且明确进行了相应标记。

#### 用途 — 字幕（預先錄製）(1.2.2) {#purpose-captions-pre-recorded}

耳聾或聽力缺佳的人無法或非常難以存取音訊內容。 註解是口語和非口語音訊的對等文字，會在視訊期間的適當時間顯示在畫面上。 它們可讓無法聽到音訊的人瞭解正在發生的事情。

>[!NOTE]
>
>在視訊或動畫的相同頁面上提供適當的文字或非文字等同專案（直接提供等同資訊）時，不需要註解。

#### 如何達到標準 — 字幕（預先錄製）(1.2.2) {#how-to-meet-captions-pre-recorded}

字幕有以下两种形式：

* 开放式：字幕在视频播放过程中始终可见
* 隐藏式：字幕可以由用户打开或关闭 

儘可能使用隱藏式字幕。 它讓使用者可以選擇是否檢視字幕。

對於隱藏式字幕，請建立並提供適當格式的同步字幕檔案，例如 [SMIL](https://www.w3.org/AudioVideo/)，以及視訊檔案。

請參閱中的教學課程 [更多資訊 — 字幕（預先錄製）(1.2.2)](#more-information-captions-pre-recorded). 請務必提供註解，讓使用者知道有字幕可觀看影片。

如果您必須使用開啟的註解，請將文字內嵌到視訊曲目中。 此方法是使用視訊編輯應用程式來達成，該應用程式允許將標題覆蓋在視訊上。

#### 更多資訊 — 字幕（預先錄製）(1.2.2) {#more-information-captions-pre-recorded}

* [了解成功标准 1.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-captions.html)：
* [如何达到成功标准 1.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#time-based-media)
* [W3C：同步的多媒体](https://www.w3.org/AudioVideo/)
* [字幕、记录和音频描述 - WebAIM 文章](https://webaim.org/techniques/captions/)

### 音訊描述或替代媒體（預先錄製） (1.2.3) {#audio-description-or-media-alternative-pre-recorded}

* 成功标准 1.2.3
* A 级
* 音訊描述或替代媒體（預先錄製）：為同步媒體提供以時間為基礎的媒體替代或預先錄製的視訊內容的音訊描述，除非媒體是文字的替代媒體，且明確標示為文字。

#### 用途 — 音訊說明或替代媒體（預先錄製） (1.2.3) {#purpose-audio-description-or-media-alternative-pre-recorded}

如果影片或動畫中的資訊僅以視覺效果顯示，失明或視障人士就會遇到協助工具障礙。或者，如果音軌提供的資訊不足，無法透過視覺效果瞭解正在發生的事情。

#### 如何達到標準 — 音訊說明或替代媒體（預先錄製） (1.2.3) {#how-to-meet-audio-description-or-media-alternative-pre-recorded}

有兩種方法可達成此成功標準。 兩者皆可接受：

1. 為視訊內容加入其他音訊說明。 您可以透過下列三種方式之一完成此方法：

   * 在現有對話方塊中暫停期間，提供未出現在現有音訊曲目中的場景變更相關資訊；
   * 提供一段附加的可选新音轨，其中不仅包含原始音轨，而且还包含有关场景变换的额外音频信息。

      * 使用者可以在現有音軌之間切換(這項 *不會* 包含音訊說明)和新的音軌(哪些 *會* 包含音訊說明)。
      * 此方法可防止對不需要額外說明的使用者造成中斷。
   * 建立視訊內容的第二個版本，以允許擴充的音訊說明。 這樣做可藉由在適當的點暫時暫停音訊和視訊，減少在現有對話方塊之間的間隙中提供詳細音訊說明的困難。 因此，在動作再次開始之前，可以輸入更長的音訊說明。 如同上一個範例，最好將此作為選用的額外音訊曲目提供，以防止對不需要額外說明的使用者造成干擾。


1. 提供視訊或動畫的音訊和視覺元素的文字稿，它是適當的對等文字。 在適當的情況下，應包括說話者的指示、語調的描述、語音表情。 根据文本长度的不同，既可以将记录放置在视频或动画所在的页面上，也可以将其放置在单独的页面上；如果选择后者，则需要在视频或动画旁边提供记录的链接。

至于如何创建带有音频描述的视频，具体细节不在本指南的范围之内。创建视频和音频描述非常耗时，但是 Adobe 的其他产品可以帮助您完成这些任务。如果在 Adobe Flash Professional 中创建内容，则还应当创建一个脚本来提示用户下载合适的插件，并通过 `<noscript>` 元素提供替换文本。

#### 更多信息 - 音频描述或替代媒体（预先录制）(1.2.3) {#more-information-audio-description-or-media-alternative-pre-recorded}

* [了解成功标准 1.2.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc.html)：
* [如何达到成功标准 1.2.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc)
* [Adobe Encore CS5](https://helpx.adobe.com/premiere-pro/using/whats-new.html)

### 字幕（实时）(1.2.4)  {#captions-live}

* 成功标准 1.2.4
* AA 级
* 註解（即時）：為同步媒體中的所有即時音訊內容提供註解。

#### 用途 — 字幕（即時） (1.2.4) {#purpose-captions-live}

该成功标准与[字幕（预先录制）](#captions-pre-recorded)的标准完全相同，因为其用途在于解决耳聋或听力欠佳的用户遇到的无障碍问题，两者的不同之处在于该成功标准需要处理网络直播等实时演示。

#### 如何达到标准 – 字幕（实时）(1.2.4) {#how-to-meet-captions-live}

遵循下列專案所提供的指引： [字幕（預先錄製）](#captions-pre-recorded) 以上。然而，由於媒體的即時性質，必須儘快建立註解布建，並對正在發生的情況做出回應。 因此，应当考虑使用实时字幕工具或语音转文本工具。

与此相关的详细说明不在本指南的范围之内，但是以下资源提供了有用的信息：

* [WebAIM：实时字幕](https://webaim.org/techniques/captions/realtime)
* [AccessIT （華盛頓大學）：能否使用語音辨識自動產生註解？](https://www.washington.edu/doit/programs/accessit?1209)

#### 更多信息 – 字幕（实时）(1.2.4) {#more-information-captions-live}

* [了解成功标准 1.2.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-real-time-captions.html)
* [如何达到成功标准 1.2.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-real-time-captions)

### 音訊說明（預先錄製） (1.2.5)  {#audio-description-pre-recorded}

* 成功标准 1.2.5
* AA 级
* 音频描述（预先录制）：为同步媒体中的所有预先录制的视频内容提供了音频描述。

#### 用途 — 音訊說明（預先錄製） (1.2.5) {#purpose-audio-description-pre-recorded}

此成功標準與 [音訊說明或替代媒體（預先錄製）](#audio-description-or-media-alternative-pre-recorded)但作者必須提供更詳細的音訊說明才能符合AA級標準。

#### 如何達到標準 — 音訊說明（預先錄製） (1.2.5) {#how-to-meet-audio-description-pre-recorded}

遵循下列專案所提供的指引： [音訊說明或替代媒體（預先錄製）](#audio-description-or-media-alternative-pre-recorded).

#### 更多資訊 — 音訊說明（預先錄製） (1.2.5) {#more-information-audio-description-pre-recorded}

* [了解成功标准 1.2.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/media-equiv-audio-desc-only.html)
* [如何达到成功标准 1.2.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-media-equiv-audio-desc-only)

### 可調整(1.3) {#adaptable}

[指引1.3改寫：建立可以不同方式呈現的內容（例如更簡單的版面），而不會遺失資訊或結構。](https://www.w3.org/TR/WCAG20/#content-structure-separation)

本指引涵蓋支援以下人員所需的需求：

* 可能無法存取作者在中提供的資訊 *標準* 二維多欄彩色網頁版面

* 可能使用純音訊或替代視覺顯示，例如大型文字或高對比。

### 信息和关系 (1.3.1)  {#info-and-relationships}

* 成功标准 1.3.1
* A 级
* 資訊和關係：透過表示法傳遞的資訊、結構和關係可以程式化方式確定，或可在文字中使用。

#### 用途 — 資訊和關係(1.3.1) {#purpose-info-and-relationships}

殘障人士使用的許多輔助技術都仰賴結構性資訊來有效顯示或輸出內容。 此結構資訊可採用頁面標題、表格列與欄標題，以及清單型別的形式。 例如，熒幕助讀程式可讓使用者在標題之間導覽頁面。 但是，當頁面內容似乎只有透過視覺樣式而非基礎HTML的結構時，則沒有可用於輔助技術的結構資訊，限制其支援更輕鬆瀏覽的能力。

此成功標準旨在確保透過HTML提供此類結構性資訊，以便瀏覽器和輔助技術可存取並利用這些資訊。

#### 如何达到标准 – 信息和关系 (1.3.1) {#how-to-meet-info-and-relationships}

AEM 允许轻松地使用相应的 HTML 元素构建网页。在RTE （文字元件）中開啟頁面內容，並使用 **格式** 功能表以指定適當的結構元素（例如段落和標題）。

下圖顯示已設定為段落文字樣式的文字；使用的原始程式碼檢視顯示它有正確的開啟和關閉 &lt;p> 和 &lt;/p> 標籤之間。

![在來源編輯模式（傳統UI）中顯示的Paragraph元素範例。](assets/chlimage_1-18a.png)

請確定您的網頁已透過以下步驟獲得適當的結構：

* **使用標題：**

只要您已啟用RTE的協助工具功能(請參閱 [AEM與協助工具](/help/sites-administering/rte-accessible-content.md))，則AEM提供三個層級的頁面標題。 您可以使用这些标题标识内容的章节和子章节。标题 1 是最高级别的标题，标题 3 是最低级别的标题。系统管理员可以配置系统以允许使用更多标题级别。

下圖示範不同標題型別的範例。

![下拉式選擇器（傳統UI）中顯示的標題H1到H3。](assets/chlimage_1-19a.png)

* **強調的文字**：

使用或元素來指示強調。 切勿在段落中使用标题突出显示文本。

    *反白標示您要強調的文字；
    *按一下「**屬性**」面板中顯示的**B**圖示(&amp;lt；strong&amp;gt；)或**I**圖示(&amp;lt；em&amp;gt；)(確保已選取HTML)。

>[!NOTE]
>
>标准 AEM 安装中的 RTE（富文本编辑器）设置为：
>
>* &lt;b> 的 &lt;strong>
* &lt;i> 的 &lt;em>
  >
兩者雖然效果相同，但和較為可取，因為兩者在語義上正確。 開發團隊可以在開發專案執行個體時將RTE設定為使用和(而非和)。

* **使用列表**：可以使用 HTML 指定三种不同类型的列表：

   * 此 `<ul>` 元素用於 *未排序* 清單（專案符號）清單。 单个列表项使用 `<li>` 元素进行标识。


   在RTE中，使用 **專案符號清單** 圖示。

   * `<ol>` 元素用于表示&#x200B;*编号*&#x200B;列表。单个列表项使用 `<li>` 元素进行标识。


   在 RTE 中，使用&#x200B;**编号列表**&#x200B;图标。

如果您想要將現有內容變更為特定清單型別，請反白適當的文字並選取適當的清單型別。 如前一個顯示段落文字輸入方式的範例所示，適當的清單元素會自動新增至您的HTML，但您可以在來源編輯檢視中檢視此清單。

>[!NOTE]
此 `<dl>` RTE不支援元素。

* **使用表格**：

資料表格必須使用HTML表格元素來識別：

    *一個&#39;&lt;table>&#39;元素
    * a `&lt;tr>&#39;表格中每一列的元素
    * a `&lt;th>&#39;每個列和欄標題的元素
    * a `&lt;td>&#39;每個資料儲存格的元素

>[!NOTE]
表格應透過 **表格** 元件。 雖然可以在文字元件中建立表格，但不建議這麼做。

此外，辅助表会使用以下元素和属性：

    * &#39;&lt;caption>&#39;元素用於為表格提供可見的標題。 字幕預設會顯示在表格上方的中央，但可以使用CSS適當地放置字幕。 描述采用编程方式与表相关联，因此这是一种提供内容简介的有用方法。
    * &#39;&lt;h3 class=&quot;summary&quot;>&#39;元素透過提供視力正常使用者可看到的內容的摘要，協助失明使用者更輕鬆地瞭解表格中顯示的資訊。 当使用了复杂或非常规的表布局时，这种方法尤其有用（该属性不会显示在浏览器中，只会由辅助型技术读取）。
    *的&#39;scope&#39;屬性&lt;th>&#39;元素用於指示儲存格是代表特定列的標題，還是代表特定欄的標題。 在复杂的表中，即数据单元格可能与一个或多个标题相关联的情况下，类似的方法是使用标题和 id 属性。

>[!NOTE]
默认情况下，这些元素和属性不直接可用，但系统管理员可以在&#x200B;**表属性**&#x200B;对话框中添加对这些值的支持（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

新增 **表格**，您可以設定 **表格屬性** 使用對話方塊。

    *適當的**標題**。
    *理想情況下，請移除**Width**、**Height**、**Border**、**Cell邊框間距**、**Cell間距**的任何預設值。 因为这些属性可以在全局样式表中设置。

![表格屬性對話方塊。](assets/chlimage_1-20a.png)

然後，您可以使用 **儲存格屬性** 若要選擇儲存格是資料儲存格或標題儲存格，以及如果是標題儲存格，則要與列或欄相關，或兩者都相關，請執行下列動作：

![呼叫屬性對話方塊；將一列（通常是第一列）設定為標頭列。](assets/chlimage_1-21a.png)

* **複雜資料表：**

有時候，如果有具有兩個或多個標題層級的複雜表格，則基本表格屬性可能不足以提供所有必要的結構資訊。 對於這些型別的複雜表格，必須在標題與其相關儲存格之間使用 **頁首** 和 **id** 屬性。 例如，在下表中，标题和 ID 是相匹配的，以便为辅助型技术用户建立程序化关联。

>[!NOTE]
ID屬性無法在現成可用的安裝中使用。 可透過設定HTML規則和RTE中的序列化程式來啟用。

>[!NOTE]
表格應透過 **表格** 元件。 雖然可以在文字元件中建立表格，但不建議這麼做。

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

若要在AEM中達到此目的，您必須使用來源編輯模式直接新增標籤。

>[!NOTE]
在標準安裝中，此功能無法立即使用。 它需要設定RTE；HTML規則和序列化程式。

#### 更多信息 – 信息和关系 (1.3.1) {#more-information-info-and-relationships}

* [了解成功标准 1.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-programmatic.html)
* [如何达到成功标准 1.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-programmatic)

### 感官特性 (1.3.3)  {#sensory-characteristics}

* 成功标准 1.3.3
* A 级
* 感官特性：提供理解和操作內容的指示，並不只依賴元件的感官特性，例如形狀、大小、視覺位置、方向或聲音。

#### 用途 — 感官特性(1.3.3) {#purpose-sensory-characteristics}

设计者往往关注可视设计特征，如颜色、形状、文本样式，或者内容在展示信息时所在的绝对或相对位置。在傳達資訊方面，這些可能是強大的設計技巧，但盲人或視障人士可能無法存取需要視覺識別屬性（例如位置、顏色或形狀）的資訊。

同樣地，如果音訊內容沒有反映在任何替代文字中，需要區分不同聲音（例如，男性或女性講話的內容）的資訊會讓有聽覺障礙的人遇到協助工具障礙。

>[!NOTE]
有關替代顏色的需求，請參閱 [使用顏色](#use-of-color).

#### 如何達到標準 — 感官特性(1.3.3) {#how-to-meet-sensory-characteristics}

請確定任何依賴頁面內容視覺特性的資訊也會以替代格式呈現。

* 不要依賴視覺位置來提供資訊。 例如，如果希望用户通过页面右侧的菜单访问更多信息，那么请不要只提及&#x200B;*右侧的菜单*；而是要为该菜单命名（例如，通过标题进行命名），然后以文本方式提及该名称。
* 切勿将文本样式（例如，粗体或斜体文本）作为传递信息的唯一方式。

>[!NOTE]
如果在非視覺內容中理解描述性辭彙的含義，則可以使用描述性詞語。 例如，使用 *以上* 和 *以下* 通常是可接受的，因為它們分別表示特定內容專案之前和之後的內容。 朗讀內容時仍然有意義。

#### 更多信息 - 感官特性 (1.3.3) {#more-information-sensory-characteristics}

* [了解成功标准 1.3.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/content-structure-separation-understanding.html)
* [如何达到成功标准 1.3.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-understanding)

### 可區分(1.4) {#distinguishable}

[准則1.4可區分：讓使用者更容易檢視和聆聽內容，包括將前景與背景分開。](https://www.w3.org/TR/WCAG20/#visual-audio-contrast)

### 使用色彩(1.4.1)  {#use-of-color}

* 成功标准 1.4.1
* A 级
* 使用色彩：色彩不是傳達資訊、指示動作、提示回應或區分視覺元素的唯一視覺方式。

>[!NOTE]
此成功標準特別針對色彩感知。 其他形式的認知包含在 [可調整(1.3)](#adaptable)；包括程式化存取顏色和其他視覺化簡報編碼。

#### 用途 — 使用顏色(1.4.1) {#purpose-use-of-color}

颜色能够有效地增强网页的美感，而且还有助于传递信息。但是，由于各种视觉障碍（从失明到色盲）的限制，部分用户无法辨认某些颜色。此問題使得色彩編碼成為提供資訊的不可靠方式。

例如，有紅 — 綠色覺缺陷的人無法區分綠色陰影和紅色陰影。 这些用户可能会将这两种颜色看成第三种颜色（如棕色），在这种情况下，他们就无法辨认红色、绿色和棕色。

此外，如果用户使用仅支持文本的浏览器、单色显示设备或查看黑白打印的页面，他们也无法感知到颜色。

#### 如何达到标准 – 使用颜色 (1.4.1) {#how-to-meet-use-of-color}

无论在何处使用颜色传递信息，都应确保无需看到颜色即可获取相应的信息。

例如，确保通过颜色传递的信息也明确地提供在文本中。下圖顯示色彩和文字如何表示座位的效能可用性：

<table>
 <tbody>
  <tr>
   <td><p><strong>效能</strong></p> </td>
   <td><p><strong>可用性</strong></p> </td>
  </tr>
  <tr>
   <td><p>星期二3月16日<sup>th</sup></p> </td>
   <td><p>可用名額</p> </td>
  </tr>
  <tr>
   <td><p>星期三3月17日<sup>th</p> </td>
   <td><p>可用名額</p> </td>
  </tr>
  <tr>
   <td><p>星期四3月18日<sup>th</sup></p> </td>
   <td><p>已售出</p> </td>
  </tr>
 </tbody>
</table>

如果颜色用作提供信息的线索，则还应该提供其他可视线索，如更改样式（例如，粗体、斜体）或者字体。 这样可以帮助弱视或色盲的用户识别信息。但是，不能完全依赖这种方法，因为这对于根本无法看到页面的用户而言并无助益。

#### 更多信息 – 使用颜色 (1.4.1) {#more-information-use-of-color}

* [了解成功标准 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [如何达到成功标准 1.4.1](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)
* [滿足3:1對比率的指引，包含「網頁安全」色彩清單](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/working-examples/G183/link-contrast.html)

### 对比度（最小）(1.4.3) {#contrast-minimum}

* 成功标准 1.4.3
* AA 级
* 對比（最小）：文字的視覺化呈現和影像的對比率至少為4.5:1，以下除外：

   * 大型文字：大型文字與大型文字影像的對比率至少為3:1。
   * 附属内容：文本或文本的图像是未激活的用户界面组件的一部分，只是纯粹的装饰，对任何人都不可见，或者只是包含其他重要可视内容的图片的一部分，对于此类文本或文本的图像，没有对比度要求。
   * 商标标志：文本是徽标或品牌名称的一部分，对于此类文本，没有最低对比度要求。

#### 用途 – 对比度（最小）(1.4.3) {#purpose-contrast-minimum}

有某些視覺障礙的人可能無法分辨某些低對比的顏色配對。 如果出现以下任一情况，此类用户便可能遇到无障碍问题：

* 文本与其背景颜色之间的对比度极低。
* 文字（例如連結文字和非連結文字）的色彩編碼對於辨別資訊非常重要。

>[!NOTE]
純粹用於裝飾目的的文字會從此成功標準中排除。

#### 如何達到標準 — 對比（最小） (1.4.3) {#how-to-meet-contrast-minimum}

請確定文字與其背景的對比度已足夠。 對比率視相關文字的大小和樣式而定：

* 对于大小小于 18 点（或粗体为小于 14 点）的文本，文本中的文字/图像与背景之间的对比度至少应为 4.5:1。
* 對於大小至少為18點（或粗體為14點）的文字，對比率應至少為3:1。
* 如果陣列化背景，則任何文字周圍的背景都應著色，以保持4.5:1或3:1的比例。

要检查对比度，可使用颜色对比度工具，例如 [Paciello Group Color Contrast Analyzer](https://www.paciellogroup.com/resources/contrast-analyser.html) 或 [WebAIM Color Contrast Checker](https://webaim.org/resources/contrastchecker/)。這些工具可讓您檢查顏色配對，並報告任何對比問題。

或者，如果您不太在意頁面外觀的指定，則可以選擇不指定背景和前景文字顏色。 在这种情况下，无需检查对比度，因为用户的浏览器会确定文本和背景的颜色。

如果無法滿足建議的對比等級，請提供替代對等版本頁面的連結（沒有色彩對比問題）。 或者，讓使用者根據自己的需求調整頁面色彩配置的對比。

#### 更多信息 - 对比度（最小）(1.4.3) {#more-information-contrast-minimum}

* [了解成功标准 1.4.3](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-contrast.html)
* [如何达到成功标准 1.4.3](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-contrast)

### 文本的图像 (1.4.5) {#images-of-text}

* 成功标准 1.4.5
* AA 级
* 文本的图像：如果使用的技术可以达到可视呈现效果，使用文本来传递信息而不使用文本的图像，以下情况除外：

   * 可自訂：可視地根據使用者的需求自訂文字影像；
   * 基本：文字的特定呈現方式對於傳遞的資訊至關重要。

>[!NOTE]
標誌型別（屬於標誌或品牌名稱的文字）被認為是必要的。

#### 用途 — 文字影像(1.4.5) {#purpose-images-of-text}

当需要文本的某种特定样式时，通常会使用文本的图像；例如，商标标志或从其他来源生成的文本（如纸质文档的扫描件）。 然而，與以HTML呈現並使用CSS設定樣式的文字相比，文字的影像在變更大小或外觀方面缺乏彈性，而這對於視覺障礙或閱讀困難的人可能是必要的。

#### 如何達到標準 — 文字影像(1.4.5) {#how-to-meet-images-of-text}

如果必须使用文本的图像，应使用 CSS 将文本的图像替换为 HTML 形式的对等文本，这样就可以对文本进行自定义。如需範例，請參閱 [C30：使用CSS以文字的影像取代文字，並提供使用者介面控制項以進行切換](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C30).

#### 更多信息 - 文本的图像 (1.4.5) {#more-information-images-of-text}

* [了解成功标准 1.4.5](https://www.w3.org/TR/UNDERSTANDING-WCAG20/visual-audio-contrast-text-presentation.html)
* [如何达到成功标准 1.4.5](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-visual-audio-contrast-text-presentation)

## 准則2：可操作 {#principle-operable}

[准则 2：可操作 – 用户界面组件和导航必须可以操作。](https://www.w3.org/TR/WCAG20/#operable)

### 暂停、停止、隐藏 (2.2.2)  {#pause-stop-hide}

* 成功标准 2.2.2
* A 级
* 暂停、停止、隐藏：对于移动、闪烁、滚动或自动更新的信息，符合以下情况：

   * 移动、闪烁、滚动：对于任何 (a) 自动启动，(b) 持续时间超过 5 秒钟，并 (c) 与其他内容并行呈现的移动、闪烁或滚动信息，提供了一个机制来允许用户执行暂停、停止或隐藏操作，除非移动、闪烁或滚动是某种行为的必需部分；
   * 自動更新：對於(a)自動開始且(b)與其他內容同時顯示的任何自動更新資訊，使用者有一種機制可以暫停、停止或隱藏該資訊，或是控制更新的頻率，除非自動更新是重要活動的一部分。

注意要点：

1. 有關閃爍或閃爍內容的需求，請參閱 [切勿設計會導致癲癇發作的內容(2.3)](#seizures).
1. 由於任何不符合此成功標準的內容都會干擾使用者使用整個頁面的能力，網頁上的所有內容（無論是否用於滿足其他成功標準）都必須符合此成功標準。 请参阅[符合性要求 5：不干涉](https://www.w3.org/TR/WCAG20/#cc5)。
1. 軟體定期更新或串流至使用者代理程式的內容，不必保留或呈現暫停起始與繼續簡報之間產生或接收的資訊，因為這在技術上可能行不通，且在許多情況下這麼做可能會誤導使用者。
1. 如果所有使用者在該階段中無法進行互動，而且如果未指出進度，可能會讓使用者感到困惑或認為內容已凍結或中斷，則作為預先載入階段的一部分或類似情況發生的動畫可視為必要。

#### 用途 — 暫停、停止、隱藏(2.2.2) {#purpose-pause-stop-hide}

某些使用者可能會發現移動的內容會分散注意力，且難以專注於頁面的其他部分。 此外，如果用户无法跟上移动的文本，他们可能就很难阅读此类内容。

#### 如何达到标准 - 暂停、停止、隐藏 (2.2.2) {#how-to-meet-pause-stop-hide}

如果创建的网页包含移动、闪光或闪烁的内容，则可以采纳以下一项或多项建议，具体视内容的性质而定。

* 提供暫停捲動內容的方法，讓使用者有足夠的時間閱讀。 例如，新聞捲軸或自動更新的文字。
* 确保闪烁的内容会在 5 秒钟后停止闪烁。
* 使用适当的技术来显示可由浏览器禁用的闪烁内容。例如，Graphics Interchange Format (GIF) 或 Animated Portable Network Graphics (APNG) 文件。
* 在網頁上提供表單控制項，讓使用者可停用頁面上的所有閃爍內容。
* 如果以上任何一項均不可行，請提供包含所有內容但不需閃爍的頁面的連結。

#### 更多信息 – 暂停、停止、隐藏 (2.2.2) {#more-information-pause-stop-hide}

* [了解成功标准 2.2.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/time-limits-pause.html)
* [如何达到成功标准 2.2.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-time-limits-pause)

### 癲癇發作(2.3) {#seizures}

[指引2.3癲癇發作：請勿設計會導致癲癇發作的內容。](https://www.w3.org/TR/WCAG20/#seizure)

### 闪光三次或低于阈值 (2.3.1) {#three-flashes-or-below-threshold}

* 成功标准 2.3.1
* A 级
* 闪光三次或低于阈值：网页不包含在任何一秒内闪光超过 3 次，或闪光低于一般闪光和红色闪光阈值的内容。

>[!NOTE]
由于任何未达到此成功标准的内容会干涉用户使用整个页面的能力，因此网页上的所有内容（无论是否用来达到其他成功标准）必须达到此成功标准。请参阅[符合性要求 5：不干涉](https://www.w3.org/TR/WCAG20/#cc5)。

#### 用途 – 闪光三次或低于阈值 (2.3.1) {#purpose-three-flashes-or-below-threshold}

在某些情況下，閃爍的內容可能會導致光敏性癲癇發作。 此成功標準可讓這類使用者存取及體驗所有內容，而不需擔心內容閃爍問題。

#### 如何達到標準 — 三個Flash或低於臨界值(2.3.1) {#how-to-meet-three-flashes-or-below-threshold}

请采取措施确保应用以下技术：

* 确保组件在任何一秒内的闪光次数均不超过三次；
* 如果无法满足上述条件，则应在屏幕上以像素为单位将闪光的内容显示在&#x200B;*小块安全区域*&#x200B;内。这块区域的面积通过一个复杂的公式来计算（详见 [G176：尽量缩小闪光区域的面积](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/G176)），因此，仅当需要闪光内容时，才应使用这种技术。

#### 更多信息 – 闪光三次或低于阈值 (2.3.1) {#more-information-three-flashes-or-below-threshold}

* [了解成功标准 2.3.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/seizure-does-not-violate.html)
* [如何达到成功标准 2.3.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#seizure)

### 页面带有标题 (2.4.2)  {#page-titled}

* 成功标准 2.4.2
* A 级
* 頁面標題：網頁的標題會說明主題或用途。

#### 用途 — 頁面有標題(2.4.2) {#purpose-page-titled}

此成功標準可協助每個人（無論是否有任何特定問題）快速識別網頁內容，而不需完整閱讀頁面。 在瀏覽器索引標籤中開啟數個網頁時，此設計很有用，因為頁面標題會顯示在索引標籤中，因此可以快速找到。

#### 如何達到標準 — 頁面有標題(2.4.2) {#how-to-meet-page-titled}

在 AEM 中创建新 HTML 页面时，可以指定页面标题。請確定標題已充分說明頁面內容，讓訪客可快速識別內容是否符合其需求。

您也可以在編輯頁面時編輯頁面標題，存取方式為 **Sidekick** - **頁面** 標籤 —  **頁面屬性……**

#### 更多信息 – 页面带有标题 (2.4.2) {#more-information-page-titled}

* [了解成功标准 2.4.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-title.html)
* [如何达到成功标准 2.4.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-title)

### 链接目的（在上下文中）(2.4.4)  {#link-purpose-in-context}

* 成功标准 2.4.4
* A 级
* 連結目的（在內容中）：每個連結的目的都可以單獨從連結文字中決定，或是從連結文字連同其程式決定的連結內容一起決定。 例外情況是連結的用途對於一般使用者模稜兩可。

#### 用途 — 連結用途（在內容中） (2.4.4) {#purpose-link-purpose-in-context}

對於所有使用者而言，無論是否有損毀，透過適當的連結文字清楚指出連結的方向是至關重要的。 此設計可協助使用者決定他們是否實際想要追蹤連結。 對於視力正常的使用者，有意義的連結文字在頁面上有多個連結時非常有用（尤其是頁面含有大量文字時），因為有意義的連結文字可更清楚指示目標頁面的功能。 雖然輔助型技術（可在單一頁面上產生所有連結的清單）的使用者可以更輕鬆地脫離上下文理解連結文字。

#### 如何达到标准 – 链接目的（在上下文中）(2.4.4) {#how-to-meet-link-purpose-in-context}

首先，确保链接文本清晰地描述了链接目的。

* 错误示例：

   * 文本内容：有关 2010 年秋季晚间课程的详细信息，请单击此处。
   * 原因分析：没有清晰明确地指明链接目标位置。

* 正确示例：

   * 文本内容：2010 年秋季晚间课程 - 详细信息。
   * 原因：稍微調整文字和連結元素的位置，可以改善連結文字：

链接用词在各个页面中应保持一致，尤其是导航栏的链接。例如，如果特定页面的链接在某个页面中被命名为&#x200B;**出版物**，则在其他页面中也应使用该文本，以确保一致性。

不過，在撰寫時，圍繞標題的使用有一些問題：

* 標題屬性中包含的文字僅供滑鼠使用者作為工具提示快顯視窗使用，且無法使用鍵盤進行存取。
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
以上代碼片段僅供說明之用，建議您使用 **影像** 元件。

雖然提供不需要額外內容即可識別連結目的的連結文字是明智之舉，但您不一定會認識到這一點。 与上下文无关的链接可用于以下情况，其 HTML 示例详见：[如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs)。

* 当链接文本是由紧密相关的链接组成的列表的一部分时，以及当链接周围的列表项提供了足够的上下文时。
* 当可以通过&#x200B;*之前*（而非之后）的段落文本清晰识别链接目的时。
* 當連結包含在資料表格中，且因此可從相關標題中清楚識別目的時。
* 其中連結清單包含在標題集中，而標題本身會提供適當的內容。
* 其中連結清單包含在巢狀連結中，且巢狀連結上方的父清單專案會提供適當的內容。

有时，一个页面上会有多个链接（其中每个链接都提供了复杂而又必要的链接方向详情），此时可以为该网页提供一个替代版本，使其显示完全相同的内容，只是其中的链接文本较为简洁。

或者，也可以使用指令碼，以便在連結本身中提供最少量的文字。但是，在啟動位於頁面頂端的適當控制項時，連結文字會 *已展開* 以取得更詳細的資訊。類似的方法是使用CSS *隱藏* 視力正常使用者的完整連結，但仍會以全熒幕閱讀器使用者的形式輸出。這不屬於本檔案的範圍，但如需如何達成此目標的詳細資訊，請參閱 [更多資訊 — 連結目的（在內容中） (2.4.4)](#more-information-link-purpose-in-context) 區段。

#### 更多信息 – 链接目的（在上下文中）(2.4.4) {#more-information-link-purpose-in-context}

* [了解成功标准 2.4.4](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-refs.html)
* [如何达到成功标准 2.4.4](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs)
* [C7：使用CSS隱藏連結文字的一部分](https://www.w3.org/TR/2008/NOTE-WCAG20-TECHS-20081211/C7)

## 准则 3：可理解 {#principle-understandable}

[原則3：可理解 — 使用者介面的資訊和操作必須是可理解的。](https://www.w3.org/TR/WCAG20/#understandable)

### 讓文字內容可讀可懂(3.1) {#make-text-content-readable-and-understandable}

[Guidelinate 3.1可讀取：讓文字內容可讀取且可理解。](https://www.w3.org/TR/WCAG20/#meaning)

### 頁面語言(3.1.1) {#language-of-page}

* 成功标准 3.1.1
* A 级
* 頁面語言：每個網頁的預設人類語言都可依程式決定。

#### 用途 — 頁面語言(3.1.1) {#purpose-language-of-page}

此成功標準旨在確保文字和其他語言內容正確呈現。 對於熒幕助讀程式使用者，這可確保內容的發音正確，而視覺瀏覽器更有可能正確顯示特定字元集。

#### 如何達到標準 — 頁面語言(3.1.1) {#how-to-meet-language-of-page}

要达到此成功标准，可以使用页面顶部 `<html>` 元素中的 `lang` 属性来识别网页的默认语言。例如：

* 如果页面采用英式英语编写，则 `<html>` 元素应该写成：

`<html lang = "en-gb">`

* 然而，要呈現成美式英文的頁面應採用以下標準：

`<html lang = "en-us">`

在 AEM 中，创建页面时会设置页面的默认语言，但是也可以在编辑页面时更改该语言，通过 **Sidekick** - **页面**&#x200B;选项卡 - **页面属性...** - **高级**&#x200B;选项卡可访问该设置。

#### 更多信息 – 页面语言 (3.1.1) {#more-information-language-of-page}

* [了解成功标准 3.1.1](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-doc-lang-id.html)
* [如何达到成功标准 3.1.1](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-doc-lang-id)
* 這些程式碼以ISO 639-1為基礎。 如需每種語言的更詳盡程式碼清單，請參閱 [W3 Schools網站](https://www.w3schools.com/tags/ref_language_codes.asp).

### 區域性語言(3.1.2)  {#language-of-parts}

* 成功标准 3.1.2
* AA 级
* 部分語言：內容中每個段落或片語的人類語言，可以程式化方式決定，但適當的名稱、技術術語、不定式語言的字詞，以及成為緊鄰文字白話一部分的字詞或片語除外。

#### 用途 — 區域性語言(3.1.2) {#purpose-language-of-parts}

此成功標準的用途與成功標準類似 [頁面語言](#language-of-page)，但適用於單一頁面上包含多種語言內容的網頁（例如，由於引號或不常見的外來字）。

套用此成功標準的頁面允許：

* 用於插入重音字元的盲文轉換軟體。
* 熒幕助讀程式可正確朗讀未使用預設語言的單字。
* Google Translate等翻譯工具可正確將內容從一種語言翻譯成另一種語言。

#### 如何達到標準 — 零件語言(3.1.2) {#how-to-meet-language-of-parts}

`lang` 属性可用于标识内容语言的更改。例如，引用的德语（ISO 639-1 代码“de”）可以采用以下方式表示：

```xml
<blockquote cite = "John F. Kennedy" lang = "de">
     <p>Ich bin ein Berliner</p>
 </blockquote>
```

>[!NOTE]
現成可用的執行個體不支援區塊引號。 可開發自訂元件以支援該功能。

同样，如果通过以下方式使用 `span` 元素，则浏览器可以准确地呈现不常见的外来词或短语：

```xml
<p>The only French phrase I know is <span lang = "fr">je ne sais quoi</span>.</p>
```

>[!NOTE]
如果包含使用不同语言的人名或城市，或者使用默认语言中常用的外来词或短语（如英语中的 *schadenfreude*），则不必遵循此成功标准。

要添加包含相应语言的 span 元素，可以在 RTE 的源代码编辑模式下手动编辑 HTML 标记，以将其写成如上显示的方式。或者，也可以由系统管理员将 `lang` 属性添加到 RTE 中（请参阅[添加对其他 HTML 元素和属性的支持](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes)）。

#### 更多信息 – 局部语言 (3.1.2) {#more-information-language-of-parts}

* [了解成功标准 3.1.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/meaning-other-lang-id.html)
* [如何达到成功标准 3.1.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-meaning-other-lang-id)

### 協助使用者避免和更正錯誤(3.3) {#help-users-avoid-and-correct-mistakes}

[准则 3.3 辅助输入：帮助用户避免和更正错误。](https://www.w3.org/TR/WCAG20/#minimize-error)

### 标签或说明 (3.3.2) {#labels-or-instructions}

* 成功标准 3.3.2
* A 级
* 標籤或指示：內容需要使用者輸入時，會提供標籤或指示。

#### 用途 — 標籤或指示(3.3.2) {#purpose-labels-or-instructions}

提供指示以幫助人們完成表單是介面可用性良好做法的基本部分。 對於有視覺或認知障礙的人，如果無法瞭解表單的版面以及在特定表單欄位中要提供的資料型別，這個選項會很有幫助。

在AEM中，新增表單元件時會新增預設標籤，例如 **文字欄位**，移至頁面。 此默认标题取决于组件类型。您也可以在该字段编辑对话框的&#x200B;**标题与文本**&#x200B;选项卡中添加自己的标题。应务必确保标签能够帮助用户理解与每个表单组件相关的数据。

![標題和文字索引標籤（編輯對話方塊）；已新增標題「說明」。](assets/chlimage_1-22a.png)

此 **標題** 欄位必須用於欄位元素，因為它提供可用於輔助技術的標籤。 僅在該欄位旁的文字中寫入標籤是不夠的。

對於某些表單元件，您也可以使用 **隱藏標題** 核取方塊。以這種方式隱藏的標籤仍適用於輔助技術，但不會顯示在熒幕上。 雖然這在某些情況下可能是不錯的方法，但最好儘可能加入視覺標籤。有些使用者可能會檢視畫面的一小部分（一次檢視一個欄位），並需要標籤才能正確識別欄位。

#### 图像按钮 {#image-buttons}

使用了图像按钮（如&#x200B;**图像按钮**&#x200B;组件）后，编辑对话框&#x200B;**标题与文本**&#x200B;选项卡中的&#x200B;**标题**&#x200B;字段实际上会为图像提供替换文本，而不是提供标签。因此，在以下示例中，包含文本 `Submit` 的图像，其替代文本就是 `Submit`，该文本是使用编辑对话框中的&#x200B;**标题**&#x200B;字段添加的。

![在「標題」欄位中設定替代文字的影像按鈕（「編輯」對話方塊）。](assets/chlimage_1-23a.png)

#### 表单字段组 {#groups-of-form-fields}

如果有一組相關控制項，例如 **選項群組**，群組和個別控制項可能需要標題。 在 AEM 中添加一组单选按钮时，**标题**&#x200B;字段会提供此组标题，而单个标题会在创建单选按钮（**项目**）时指定。

![新增專案至選項群組。 群組標題為「聯絡方式」 — 定義於「標題」欄位。](assets/chlimage_1-24a.png)

但是，组标题和单选按钮本身之间并没有编程关联。範本編輯器必須將標題包裝在必要欄中 `fieldset` 和 `legend` 標籤來建立此關聯，而這只能透過編輯頁面原始碼來完成。 或者，系統管理員可以新增對這些元素的支援，以使它們出現在 **欄位屬性** 對話方塊(請參閱 [新增對其他HTML元素和屬性的支援](/help/sites-administering/rte-accessible-content.md#add-support-for-more-html-elements-and-attributes))。

#### 有关 Forms 的其他考虑事项 {#additional-considerations-for-forms}

如果必须按照特定的格式输入数据，应在标签文本中予以清楚说明。例如，如果必须以 `DD-MM-YYYY` 格式输入日期，应在标签中特别指明这一点。這表示當熒幕助讀程式的使用者遇到該欄位時，會自動公告標籤，以及關於格式的其他資訊。

如果必须输入表单字段，请在标签中使用“必填”一词来说明。AEM 会为必填字段添加一个星号，但是最好在标签本身中也包含 `required` 一词（在编辑对话框的&#x200B;**标题**&#x200B;字段中）。

![在「標題」欄位中為熒幕助讀程式使用者新增其他資訊（必填字）。](assets/chlimage_1-25a.png)

標籤的位置也很重要，因為這有助於他們找到適當的欄位。 當使用者面對複雜表單時，這尤其重要。 請遵循下列慣例：

* 核取方塊或選項按鈕：

標籤會直接放置於欄位右側。

* 所有其他表單元件（例如，文字方塊、下拉式方塊）：

標籤會放在緊靠欄位上方或左側的位置。

在功能有限的簡單表單中，適當地標示 `Submit` 按鈕可作為相鄰欄位的標籤(例如 `Search`)。 在尋找標籤文字的空間可能困難的情況下，這個用法很有用。

#### 更多資訊 — 標籤或指示(3.3.2) {#more-information-labels-or-instructions}

* [了解成功标准 3.3.2](https://www.w3.org/TR/UNDERSTANDING-WCAG20/minimize-error-cues.html)
* [如何达到成功标准 3.3.2](https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-minimize-error-cues)
