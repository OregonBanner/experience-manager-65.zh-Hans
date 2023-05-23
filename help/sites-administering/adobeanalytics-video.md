---
title: 为 Adobe Analytics 配置视频跟踪
seo-title: Configuring Video Tracking for Adobe Analytics
description: 瞭解如何設定SiteCatalyst的視訊追蹤。
seo-description: Learn about configuring video tracking for SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
exl-id: 5d51f898-b6d1-40ac-bdbf-127cda1dc777
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 2%

---

# 为 Adobe Analytics 配置视频跟踪{#configuring-video-tracking-for-adobe-analytics}

有數種方法可用來追蹤視訊事件，其中2種是舊版Adobe Analytics的舊版選項。 這些舊版選項為：舊版里程碑和舊版秒數。

>[!NOTE]
>
>在繼續之前，請確定您擁有 **可播放的視訊** 已在AEM中上傳。
>
>為確保您的影片在頁面上播放，請參閱 **[本教學課程](/help/sites-authoring/default-components-foundation.md#video)** 以取得如何在AEM中轉碼視訊檔案的相關資訊。

使用以下程式，透過每個方法設定視訊追蹤的架構。

>[!NOTE]
>
>若為新實作，建議您 **不使用** 舊版視訊追蹤選項。 請使用 **里程碑** 方法取代。

## 常見步驟 {#common-steps}

1. 透過拖曳設定網頁 **視訊元件** 從sidekick新增可播放專案 **視訊作為資產** 用於元件

1. [建立Adobe Analytics設定和框架](/help/sites-administering/adobeanalytics.md).

   * 後面章節的範例使用名稱 **my-sc-configuration** 設定和 **videofw** 用於框架。

1. 在「架構」頁面上，選取RSID並將使用方式設定為「全部」。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 從Sidekick的「一般」元件類別中，將「視訊」元件拖曳至框架上。
1. 選取追蹤方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非舊版里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊版里程碑](/help/sites-administering/adobeanalytics.md)
   * [舊版秒數](/help/sites-administering/adobeanalytics.md)

1. 當您選取追蹤方法時，CQ變數的清單會隨之變更。 使用下列章節，瞭解如何進一步設定元件，並透過Adobe Analytics屬性對應CQ變數。

## 里程碑 {#milestones}

Milestones方法可追蹤有關視訊的最多資訊、高度自訂且易於設定。

若要使用「里程碑」方法，請指定以時間為基礎的軌跡位移來定義里程碑。 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。 元件會為您定義的每個里程碑建立CQ變數，以便您對應至Adobe Analytics屬性。 這些CQ變數的名稱會使用以下格式：

```shell
eventdata.events.milestoneXX
```

XX字尾是定義里程碑的軌跡位移。 例如，指定4、8、16、20和28秒的軌跡位移會產生下列CQ變數：

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

下表說明為Milestones方法提供的預設CQ變數：

<table>
 <tbody>
  <tr>
   <th>CQ變數</th>
   <th>Adobe Analytics屬性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>對應至此的變數將包含 <strong>使用者易記</strong> 名稱(<strong>標題</strong>)，若已在DAM中設定；若未設定，則影片的 <strong>檔案名稱</strong> 將改為傳送。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 僅與eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 僅與eventdata.events.a.media.view一起傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次超過區段里程碑時傳送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次觸發里程碑時都會傳送，使用者觀看指定區段所花費的秒數也會與此事件一併傳送。 例如eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化視訊檢視時傳送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>視訊完成播放時傳送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>當指定的里程碑通過時傳送，X代表里程碑觸發時的秒數。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>在每個里程碑時傳送；在Adobe Analytics呼叫中顯示為pev3，通常以「視訊」傳送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>完全符合eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含已檢視區段的資訊，例如2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以設定視訊的 **使用者易記** 透過在DAM中開啟影片以進行編輯，並設定來「命名」 **標題** 將中繼資料欄位命名為所需的名稱。

1. 選取「里程碑」作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤位移清單（以秒為單位）。 例如，下列值會定義里程碑在視訊開始後的4、8、16、20和28秒：

   ```xml
   4,8,16,20,24
   ```

   位移值必須是大於0的整數。 默认值为 `10,25,50,75`。

1. 若要將CQ變數對應至Adobe Analytics屬性，請從ContentFinder拖曳元件上CQ變數旁的Adobe Analytics屬性。

   如需最佳化對應的詳細資訊，請參閱 [在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 指南。

1. [新增框架](/help/sites-administering/adobeanalytics.md) 至頁面。
1. 若要在中測試設定 **預覽模式**，播放影片以觸發Adobe Analytics呼叫。

以下的Adobe Analytics追蹤資料範例適用於使用4、8、16、20和24的追蹤位移，以及CQ變數的下列對應的里程碑追蹤：

<table>
 <tbody>
  <tr>
   <th>CQ 变量</th>
   <th>Adobe Analytics屬性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1， prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

在此範例中，視訊元件在架構頁面上會如下所示：

![video1](assets/video1.png)

>[!NOTE]
>
>若要檢視對Adobe Analytics發出的呼叫，請使用適當的工具，例如DigitalPulse Debugger或Fiddler。

使用DigitalPulse Debugger檢視使用所提供範例呼叫Adobe Analytics時，呼叫看起來應該像這樣：

![chlimage_1-128](assets/chlimage_1-128.png)

*這是&#x200B;**第一次呼叫**對Adobe Analytics的變更，包含下列值：*

* *eventdata.a.media.name的prop1和eVar1，*
* *props2-4，以及包含contentType （影片）和區段(1)的eVar2和eVar3:O:1-4)*
* *已對應至eventdata.events.a.media.view的事件3。*

![chlimage_1-129](assets/chlimage_1-129.png)

*這是&#x200B;**第三個呼叫**製作至Adobe Analytics：*

* *prop1和eVar1包含a.media.name；*
* *event1，因為已檢視區段*
* *event2已傳送並播放時間= 4*
* *event11已傳送，因為已達到eventdata.events.milestone8*
* *prop2至4未傳送（因為未觸發eventdata.events.a.media.view）*

## 非舊版里程碑 {#non-legacy-milestones}

除了使用軌道長度的百分比來定義里程碑以外，「非舊式里程碑」方法類似於「里程碑」方法。 共性如下：

* 當視訊播放超過里程碑時，頁面會呼叫Adobe Analytics以追蹤事件。
* 此 [CQ變數的靜態集合](#cqvars) 為與Adobe Analytics屬性對應而定義。
* 元件會為您定義的每個里程碑建立CQ變數，以便您對應至Adobe Analytics屬性。

這些CQ變數的名稱會使用以下格式：

XX字尾是定義里程碑的軌道長度的百分比。 例如，指定10、25、50和75的百分比會產生以下CQ變數：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 選取「非舊版里程碑」作為追蹤方法後，在「追蹤位移」方塊中，輸入以逗號分隔的追蹤長度百分比清單。 例如，下列預設值會定義里程碑為軌跡長度的10%、25%、50%和75%：

   ```xml
   10,25,50,75
   ```

   位移值必須是大於0的整數。

1. 若要將CQ變數對應至Adobe Analytics屬性，請從ContentFinder拖曳元件上CQ變數旁的Adobe Analytics屬性。

   如需最佳化對應的詳細資訊，請參閱 [在Adobe Analytics中測量視訊](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html) 指南。

1. [新增框架](/help/sites-administering/adobeanalytics.md) 至頁面。
1. 若要在中測試設定 **預覽模式**，播放影片以觸發Adobe Analytics呼叫。

## 舊版里程碑 {#legacy-milestones}

此方法類似於Milestones方法，差異在於中指定的里程碑 *追蹤位移* 欄位是視訊中的百分比，而不是設定點。

>[!NOTE]
>
>「追蹤位移」欄位僅接受逗號分隔的清單，其中包含1到100之間的整數。

1. 設定「軌跡位移」。

   * e.g.10,50,75,100

   此外，傳送至Adobe Analytics的資訊可自訂性較低；只有3個變數可用於對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>對應至此的變數將包含 <strong>使用者易記</strong> 名稱(<strong>標題</strong>)；如果未設定「標題」，則影片的 <strong>檔案名稱</strong> 將改為傳送。 只傳送一次，在播放視訊開始時傳送。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以設定視訊的 **使用者易記** 透過在DAM中開啟影片以進行編輯，並設定來「命名」 **標題** 將中繼資料欄位命名為所需的名稱。 您還需要儲存完成時所做的變更。

1. 將這些變數對應至prop 1至3

   此 **其他相關資訊** 在呼叫中將串連傳送至 **一** 變數已命名 **pev3**.

   **呼叫範例** 使用DigitalPulse Debugger檢視時，使用所提供範例前往Adobe Analytics的畫面應如下所示：

   ![lmilestones1](assets/lmilestones1.png)

   *此&#x200B;**pev3**呼叫中傳送的變數包含下列資訊：*

   * *名稱*  — 視訊檔案的名稱(*film.avi*)

   * *長度*  — 視訊檔案的長度，以秒為單位(*100*)

   * *播放器名稱*  — 用來播放視訊檔案的視訊播放器(*HTML5影片*)

   * *總播放秒數*  — 影片播放的總秒數(*25*)

   * *開始時間戳記*  — 識別視訊播放開始時間的時間戳記(*1331035567*)

   * *播放工作階段*  — 播放工作階段的詳細資料。 此欄位會指出使用者與視訊的互動方式。 這可能包括他們開始播放視訊的位置、他們是否使用視訊滑桿來推進視訊，以及他們停止播放視訊的位置(*L10E24S58L58 — 視訊停止於秒。 區段L10的25個，然後略過至秒。 48*)

## 舊版秒數 {#legacy-seconds}

使用**legacy seconds**方法時，Adobe Analytics呼叫會每隔N秒觸發一次，其中N會在「追蹤位移」欄位中指定。

1. 將「軌跡位移」設定為任何秒數，

   * 例如6
   >[!NOTE]
   >
   >「追蹤位移」欄位僅接受大於0的整數

   傳送至Adobe Analytics的資訊較不易自訂。 只有3個變數可用於對應：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>對應至此的變數將包含 <strong>使用者易記</strong> 名稱(<strong>標題</strong>)；如果未設定「標題」，則影片的 <strong>檔案名稱</strong> 將改為傳送。 只傳送一次，在播放視訊開始時傳送。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>對應至此的變數將包含檔案名稱。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>對應至此的變數將包含檔案在伺服器上的路徑。 只傳送一次，在播放視訊開始時傳送。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以設定視訊的 **使用者易記** 透過在DAM中開啟影片以進行編輯，並設定來「命名」 **標題** 將中繼資料欄位命名為所需的名稱。 您還需要儲存完成時所做的變更。

1. 將這些變數對應至prop1、prop2和prop3

   此 **其他相關資訊** 在呼叫中，將會以串連方式傳送至 **一** 變數已命名 **pev3**.

   使用DigitalPulse Debugger檢視使用所提供範例呼叫Adobe Analytics時，呼叫看起來應該像這樣：

   ![lseconds](assets/lseconds.png)

   *此呼叫類似於上述舊版里程碑呼叫。 請參閱pev3的相關資訊&#x200B;**[提供於此](/help/sites-administering/adobeanalytics.md)**.*

**本教學課程中使用的參考：**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html)
