---
title: 为Adobe Analytics配置视频跟踪
seo-title: 为Adobe Analytics配置视频跟踪
description: 了解如何为SiteCatalyst配置视频跟踪。
seo-description: 了解如何为SiteCatalyst配置视频跟踪。
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7

---


# 为Adobe Analytics配置视频跟踪{#configuring-video-tracking-for-adobe-analytics}

可以使用多种方法跟踪视频事件，其中2种是旧版Adobe Analytics的旧版选项。 以下是旧版选项：旧式里程碑和旧式秒数。

>[!NOTE]
>
>在继续之前，请确保** **在AEM中上传了** **可播放视频。

>要确保您的视频在页面上播放，请参 **[阅本教程](/help/sites-authoring/default-components-foundation.md#video)**，了解如何在AEM中转码视频文件。

请按照以下过程使用每个方法为视频跟踪设置框架。

>[!NOTE]
>
>对于新实施，建议不要 **使用** “旧版”视频跟踪选项。 请改用 **Milestones** 方法。

## 常见步骤 {#common-steps}

1. 通过从Sidekick中拖动视频组 **件** ，并将可播放视频添加为组件的资 **产来设置网页**

1. [创建Adobe Analytics配置和框架](/help/sites-administering/adobeanalytics.md)。

   * 以下各节中的示例使用名 **称my-sc-configuration** （用于配置）和 **videof** （用于框架）。

1. 在框架页面上，选择一个RSID并将用法设置为全部。 ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. 从Sidekick中的常规组件类别，将视频组件拖动到框架上。
1. 选择跟踪方法：

   * [里程碑](/help/sites-administering/adobeanalytics.md)
   * [非传统里程碑](/help/sites-administering/adobeanalytics.md)
   * [旧版里程碑](/help/sites-administering/adobeanalytics.md)
   * [旧版秒数](/help/sites-administering/adobeanalytics.md)

1. 当您选择跟踪方法时，CQ变量列表会相应地更改。 有关如何进一步配置组件以及将CQ变量与Adobe Analytics属性映射的信息，请参阅下面几节。

## Milestones {#milestones}

Milestones方法可跟踪有关视频的大多数信息，并且可高度自定义，且易于配置。

要使用Milestones方法，请指定基于时间的跟踪偏移以定义里程碑。 当视频播放通过里程碑时，该页面将调用Adobe Analytics来跟踪该事件。 对于您定义的每个里程碑，该组件会创建一个CQ变量，您可以将其映射到Adobe Analytics属性。 这些CQ变量的名称使用以下格式：

```shell
eventdata.events.milestoneXX
```

XX后缀是定义里程碑的轨道偏移。 例如，指定4、8、16、20和28秒的轨道偏移可生成以下CQ变量：

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

下表描述了为Milestones方法提供的默认CQ变量：

<table>
 <tbody>
  <tr>
   <th>CQ变量</th>
   <th>Adobe Analytics属性</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>如果在DAM中设置，则映射 <strong>到该变量的变量将包含视频的</strong> (<strong>标题</strong>)用户友好名称；如果未设置此值，则将发送视 <strong>频的文</strong> 件名。 在播放视频开始时，仅发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此变量的变量将包含文件的名称。 仅与eventdata.events.a.media.view一起发送 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到该路径的变量将包含文件在服务器上的路径。 仅与eventdata.events.a.media.view一起发送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>每次通过区段里程碑时发送 </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>每次触发里程碑时发送，用户观看给定区段所花费的秒数也会随此事件一起发送。 例如eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>在初始化视频视图时发送</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>视频播放完成时发送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>当给定里程碑通过时，X表示里程碑触发的秒数<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>发送到每个里程碑；在Adobe Analytics调用中显示为pev3，通常以“视频”的形式发送<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>完全匹配eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>包含有关已查看区段的信息，例如2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以通过打开视频以 **在DAM中进行编辑** ，并将“标题 **** ”元数据字段设置为所需名称来设置视频的用户友好名称。

1. 在选择里程碑作为跟踪方法后，在“跟踪偏移”框中，以秒为单位输入以逗号分隔的跟踪偏移列表。 例如，以下值定义视频开始后4、8、16、20和28秒的里程碑：

   ```xml
   4,8,16,20,24
   ```

   偏移值必须是大于0的整数。 默认值为 `10,25,50,75`.

1. 要将CQ变量映射到Adobe Analytics属性，请将Adobe Analytics属性从ContentFinder拖动到组件上CQ变量旁。

   有关优化映射的信息，请参阅Adobe Analytics [中的测量视频](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html) 。

1. [将框架添加](/help/sites-administering/adobeanalytics.md) 到页面。
1. 要在“预览”模式 **中测试设置**，请播放视频以获取要触发的Adobe Analytics调用。

Adobe Analytics跟踪数据示例随后适用于使用4、8、16、20和24的跟踪偏移量以及CQ变量的以下映射进行的里程碑跟踪：

<table>
 <tbody>
  <tr>
   <th>CQ 变量</th>
   <th>Adobe Analytics属性</th>
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
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

在此示例中，视频组件在框架页面上显示如下：

![video1](assets/video1.png)

>[!NOTE]
>
>要查看对Adobe Analytics的调用，请使用适当的工具，如DigitalPulse Debugger或Fiddler。

使用提供的示例调用Adobe Analytics时，在使用DigitalPulse Debugger查看时，应如下所示：

![chlimage_1-128](assets/chlimage_1-128.png)

*这是对Adobe **Analytics进行的第一次调用**，其中包含以下值：*

* *prop1和eVar1 for eventdata.a.media.name,*
* *props2-4，以及eVar2和eVar3，它们包含contentType（视频）和segment(1:O:1-4)*
* *event3，它被映射到eventdata.events.a.media.view。*

![chlimage_1-129](assets/chlimage_1-129.png)

*这是Adobe **Analytics的第三次**（电话）:*

* *prop1和eVar1包含a.media.name;*
* *event1，因为已查看区段*
* *播放时间时发送的event2 = 4*
* *event11已发送，因为已到达eventdata.events.milestone8*
* *prop2至4不会发送（因为eventdata.events.a.media.view未触发）*

## 非传统里程碑 {#non-legacy-milestones}

除里程碑是使用跟踪长度的百分比定义的以外，“非旧版里程碑”方法与“里程碑”方法类似。 共性如下：

* 当视频播放通过里程碑时，该页面将调用Adobe Analytics来跟踪该事件。
* 为 [与Adobe Analytics属性进行映射而定义的CQ变量的静态集](#cqvars) 。
* 对于您定义的每个里程碑，该组件会创建一个CQ变量，您可以将其映射到Adobe Analytics属性。

这些CQ变量的名称使用以下格式：

XX后缀是定义里程碑的轨道长度百分比。 例如，指定10、25、50和75的百分比可生成以下CQ变量：

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. 在选择“非旧版里程碑”作为跟踪方法后，在“跟踪偏移”框中输入以逗号分隔的跟踪长度百分比列表。 例如，以下默认值定义的里程碑占跟踪长度的10%、25%、50%和75%:

   ```xml
   10,25,50,75
   ```

   偏移值必须是大于0的整数。

1. 要将CQ变量映射到Adobe Analytics属性，请将Adobe Analytics属性从ContentFinder拖动到组件上CQ变量旁。

   有关优化映射的信息，请参阅Adobe Analytics [中的测量视频](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html) 。

1. [将框架添加](/help/sites-administering/adobeanalytics.md) 到页面。
1. 要在“预览”模式 **中测试设置**，请播放视频以获取要触发的Adobe Analytics调用。

## 旧版里程碑 {#legacy-milestones}

此方法与Milestones方法类似，其区别在于在“跟踪偏移”字段中指定的里程碑是百分比 ** ，而不是视频中的设置点。

>[!NOTE]
>
>“跟踪偏移”字段只接受一个以逗号分隔的列表，其中包含1到100之间的整数。

1. 设置“轨道偏移”。

   * 例如10,50,75,100
   此外，发送到Adobe Analytics的信息也不太可自定义；只有3个变量可用于映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>如果在DAM中设置，则映射 <strong>到该变量的变量将包含视频的</strong> (<strong>标题</strong>)用户友好名称；如果未设置标题，则将发送视 <strong>频的文件名</strong> 。 在播放视频开始时，仅发送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此变量的变量将包含文件的名称。 在播放视频开始时，仅发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到该变量的变量将包含文件在服务器上的路径。 在播放视频开始时，仅发送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以通过打开视频以 **在DAM中进行编辑** ，并将“标题 **** ”元数据字段设置为所需名称来设置视频的用户友好名称。 您还需要保存完成后所做的更改。

1. 将这些变量映射到prop 1到3

   调用 **中的其余相关信息** ，将连接到一个名为pev3的 **变量** 中 ****。

   **使用提供的示例** ，对Adobe Analytics的示例调用在使用DigitalPulse Debugger查看时应当如下：

   ![lmilestones1](assets/lmilestones1.png)

   *在调&#x200B;**用中发送的**pev3变量包含以下信息：*

   * *名称* -视频文件的名称(*film.avi*)

   * *长度* -视频文件的长度，以秒为单位(*100*)

   * *播放器名称* -用于播放视频文件的视频播放器(*HTML5视频*)

   * *已播放的总秒数* -已播放视频的总秒数(*25*)

   * *开始时间戳* -标识视频播放何时开始的时间戳(*1331035567*)

   * *播放会话* -播放会话的详细信息。 此字段指示用户与视频的交互方式。 这可能包括一些数据，例如他们开始播放视频的位置、他们是否使用视频滑块来推进视频，以及他们停止播放视频的位置(*L10E24S58L58 —— 视频在一秒内停止。 第L10节的25个，然后跳到秒。 48*)

## 旧版秒数 {#legacy-seconds}

使用**传统秒**方法时，Adobe Analytics调用每隔N秒被触发一次，其中N在“跟踪偏移”字段中指定。

1. 将“轨道偏移”设置为任意秒数，

   * 例如6
   >[!NOTE]
   >
   >“跟踪偏移”字段只接受大于0的整数

   发送到Adobe Analytics的信息不太可自定义。 只有3个变量可用于映射：

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>如果在DAM中设置，则映射 <strong>到该变量的变量将包含视频的</strong> (<strong>标题</strong>)用户友好名称；如果未设置标题，则将发送视 <strong>频的文件名</strong> 。 在播放视频开始时，仅发送一次。<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>映射到此变量的变量将包含文件的名称。 在播放视频开始时，仅发送一次。</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>映射到该变量的变量将包含文件在服务器上的路径。 在播放视频开始时，仅发送一次。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可以通过打开视频以 **在DAM中进行编辑** ，并将“标题 **** ”元数据字段设置为所需名称来设置视频的用户友好名称。 您还需要保存完成后所做的更改。

1. 将这些变量映射到prop1、prop2和prop3

   调 **用中的其余相关信息** ，将被关联到名为pev3 **的******&#x200B;一个变量中。

   使用提供的示例调用Adobe Analytics时，在使用DigitalPulse Debugger查看时，应如下所示：

   ![lseconds](assets/lseconds.png)

   *此调用与上述旧版里程碑调用类似。 请参见此处提供的有关pev3 **[的信息](/help/sites-administering/adobeanalytics.md)**。*

**本教程中使用的参考：**

[0] [https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/video_overview.html)
