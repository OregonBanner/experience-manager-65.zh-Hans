---
title: 预览资产
description: 了解如何在Dynamic Media中预览资产
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: a1e4d64a9ac7dc02c5cf2ac6b01994736c45b449
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 21%

---


# 使用软件界面{#previewing-assets}预览资产

您可以使用预览查看您上传的数字资产在客户自己的Web浏览器中查看时的外观。 预览时将使用为资产分配的默认嵌入式跨设备查看器。

查看器是各种设置（或称“预设”，例如查看器的显示大小、缩放行为、颜色方案、边框、字体等）的集合，这些设置决定了用户在其计算机屏幕和移动设备上查看富媒体资产的方式。

除了使用专门的“预览”功能预览视频、旋转集和图像集之外，您还可以通过使用自己创建的查看器预设来预览资产。或者，也可以使用图像预设来预览图像的演绎版。

* [应用图像预设](/help/assets/image-presets.md)
* [应用查看器预设](/help/assets/viewer-presets.md)

>[!NOTE]
>
>当您位于AEM的网页（站点）上时，无法在编辑模式下预览 **资产** 。 您需要通过单击页面右上角的&#x200B;**预览**，转至&#x200B;**预览**&#x200B;模式。

要在用户界面中启用或禁用查看器预设，请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

**使用软件界面预览资产**

1. 从&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;的&#x200B;**[!UICONTROL 导航]**&#x200B;页面，点按&#x200B;**[!UICONTROL 资产]**，然后点按&#x200B;**[!UICONTROL 文件]**&#x200B;以访问资产。
1. 在页面的右上角附近，从&#x200B;**[!UICONTROL 视图]**&#x200B;下拉列表中，点按&#x200B;**[!UICONTROL 列表视图。]**
1. （可选）使用&#x200B;**[!UICONTROL 类型]**&#x200B;列按要预览的类型对资产进行排序。
1. 在&#x200B;**[!UICONTROL 标题]**&#x200B;列下，单击要预览的资产的标题名称（而非缩略图）。
1. 根据您单击的资产类型，执行下列任一操作：


   <table>
    <tbody>
      <tr>
      <td><strong>您单击的资产类型</strong><br /> </td>
      <td><strong>能否在特定再现中预览资产？</strong></td>
      <td><strong>能否在查看器中预览资产？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在维查看器中预览3D资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择维查看器。</li>
      <li>点按<strong>重置</strong>可将图像恢复为原始缩放。</li>
      <li>点按<strong>全屏</strong>以最大化显示设备上的查看器。</li>
      </ul>
      <p><strong>导航3D场景</strong></p>
      <ul>
      <li><p><strong>旋转3D相机</strong> -围绕3D场景和对象绕行视图。</p> 鼠标：左键单击+拖动。 </p> 触摸屏：按+拖动。</p></li>
      <li><p><strong>平移相机</strong> -向左、向右、向上和向下平移视图。</p> 鼠标：右键单击+拖动。 </p> 触摸屏：双指按+拖动。</p></li>
      <li><p><strong>缩放相机</strong> -缩放相机以在3D场景中移入和移出区域。</p> 鼠标：滚轮。 </p> 触摸屏：手指开合。</p></li>
      <li><p><strong>重新进入相机</strong> -围绕3D场景和对象绕行视图。</p> 鼠标：多次单击。 </p> 触摸屏：多次点击。</li></ul></td>
      </tr>
      <tr>
      <td><p>图像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定再现中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>演绎版</strong>，然后选择要预览的特定演绎版。</li>
      </ul> <p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>图标可分别增大或减小所选图像的缩放比例。 单击<strong>重置</strong>可使图像恢复到原始缩放比例。
<br /> 如果您在触摸屏上，请多次点击图像以逐步放大。当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>多媒体</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定再现中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>演绎版</strong>，然后选择要预览的特定演绎版。</li>
      </ul> <p>选择分辨率更高的视频演绎版以进行预览可能会导致视频出现截断。 这是因为演绎版预览会在用于预览的嵌入式查看器的上下文中向您显示客户将看到的确切分辨率。</p> <p>当您在资产级别预览自适应视频集时，演绎版将分组为一个播放体验。 也就是说，自适应视频的大小调整得当，以便在观看设备和连接速度的上下文中使用最佳分辨率进行观看和回放。<br /> </p> <p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>图像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>图标可分别增大或减小所选图像的缩放比例。 单击<strong>重置</strong>可使图像恢复到原始缩放比例。
<br /> 如果您在触摸屏上，请多次点击图像以逐步放大。当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>旋转集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>图标可分别增大或减小所选图像的缩放比例。 单击<strong>重置</strong>可使图像恢复到原始缩放比例。
<br /> 如果您在触摸屏上，请多次点击图像以逐步放大。当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>混合媒体集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 单击列表中的<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>图标可分别增大或减小所选图像的缩放比例。 单击<strong>重置</strong>可使图像恢复到原始缩放比例。
<br /> 如果您在触摸屏上，请多次点击图像以逐步放大。当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>旋转集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定查看器中预览资产</strong>
      <ul>
      <li>在页面的左上角附近，单击该图标以显示下拉列表。 选择要应用于资产的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360视频<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>在特定再现中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，点按图标以显示下拉列表。 选择<strong>演绎版</strong>，然后选择要预览的演绎版。</li>
      </ul> <p><strong>在特定查看器中预览资产</strong></p>
      <ul>
      <li>在页面的左上角附近，点按图标以显示下拉列表。 选择<strong>查看器</strong>，然后选择要应用到资产的查看器。</li>
      </ul> <p>使用<strong>+</strong>和<strong>-</strong>图标可分别增大或减小所选图像的缩放比例。 单击<strong>重置</strong>可使图像恢复到原始缩放比例。
<br /> 如果您在触摸屏上，请多次点击图像以逐步放大。当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
    </tbody>
    </table>

## 使用键盘{#keyboard-navigation-asset-preview}预览资产

1. 在资产用户界面中，导航到包含要预览的资产的文件夹。

1. 在文件夹中，按键盘上的`<Tab>`键或箭头键选择资产。

1. 按`<Enter>`以预览模式打开选定的资产。

1. 执行以下操作之一：

   * 要放大，请按`<Tab>`将焦点移到放大(+)图标，然后按`<Enter>`一次或多次以增量方式放大。

   * 要缩小，请按`<Tab>`将焦点移到缩小(-)图标，然后按`<Enter>`一次或多次以增量方式缩小。

   * 要水平或垂直移动&#x200B;*缩放*&#x200B;资产的视图，请按相应的箭头键。

   * 按`<Shift>` + `<Tab>`重置视图并将焦点放回资产上。
