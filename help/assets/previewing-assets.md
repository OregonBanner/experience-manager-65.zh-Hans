---
title: 预览资源
description: 了解如何通过应用图像预设和查看器预设在Dynamic Media中预览资源，例如视频和图像。
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# 使用软件界面预览资源 {#previewing-assets}

您可以使用“预览”来查看客户在其Web浏览器中查看已上传的数字资产时的外观。 分配给资产的默认嵌入式跨设备查看器用于预览。

查看器是各种设置的集合，或者 *预设*，如查看器显示大小、缩放行为、颜色方案、边框和字体。 这些预设决定用户在其计算机屏幕和移动设备上查看富媒体资产的方式。

除了为视频、旋转集和图像集使用专用的预览功能外，您还可以使用您创建的查看器预设来预览资源。 或者，使用图像预设来预览图像的演绎版。

* [应用图像预设](/help/assets/image-presets.md)
* [应用查看器预设](/help/assets/viewer-presets.md)

>[!NOTE]
>
>当您位于Adobe Experience Manager的网页（站点）上时，无法在中预览资源 **编辑** 模式。 单击以转到预览模式 **[!UICONTROL 预览]** 在页面的右上角。

要在用户界面中启用或禁用查看器预设，请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md).

**要使用软件界面预览资产，请执行以下操作：**

1. 从 **[!UICONTROL Adobe Experience Manager]**，位于 **[!UICONTROL 导航]** 页面，选择 **[!UICONTROL 资产]**，则 **[!UICONTROL 文件]** 以访问资产。
1. 在页面的右上角附近，从 **[!UICONTROL 视图]** 下拉列表，选择 **[!UICONTROL 列表视图]**.
1. （可选）使用 **[!UICONTROL 类型]** 列按要预览的类型对资源进行排序。
1. 在 **[!UICONTROL 标题]** 列中，单击要预览的资源的标题名称（不是缩略图图像）。
1. 根据所单击的资源类型，执行以下任一操作：


   <table>
    <tbody>
      <tr>
      <td><strong>您单击的资源类型</strong><br /> </td>
      <td><strong>能否预览特定演绎版中的资源？</strong></td>
      <td><strong>是否能够在查看器中预览资源？</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在维查看器中预览3D资产</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择维查看器。</li>
      <li>选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。</li>
      <li>选择 <strong>全屏</strong> 使显示设备上的查看器最大化。</li>
      </ul>
      <p><strong>浏览3D场景</strong></p>
      <ul>
      <li><p><strong>转动3D摄像头</strong>  — 使视图围绕3D场景和对象旋转。</p> 鼠标：左键单击+拖动 </p> 触摸屏：按下+拖动</p></li>
      <li><p><strong>平移相机</strong>  — 向左、向右、向上和向下平移视图。</p> 鼠标：右键单击+拖动 </p> 触摸屏：双指按下+拖动</p></li>
      <li><p><strong>缩放相机</strong>  — 缩放相机，以便能够进出3D场景中的区域。</p> 鼠标：滚轮 </p> 触摸屏：手指捏合</p></li>
      <li><p><strong>重新居中相机</strong>  — 使视图围绕3D场景和对象旋转。</p> 鼠标：双击 </p> 触摸屏：双击</li></ul></td>
      </tr>
      <tr>
      <td><p>图像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>节目 </strong>从列表中，选择要预览的特定格式副本。</li>
      </ul> <p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 用于分别增大或减小所选图像的缩放的图标。 选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动图像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒体</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>节目 </strong>从列表中，选择要预览的特定格式副本。</li>
      </ul> <p>选择要预览的高分辨率视频演绎版可能会导致视频看起来被截断。 出现此问题是因为演绎版预览会在用于预览的嵌入式查看器的上下文中显示客户将看到的全部内容的确切分辨率。</p> <p>在资源级别预览自适应视频集时，演绎版将分组到一个播放体验中。 也就是说，根据查看设备和连接速度，自适应视频经过适当的调整以适合查看和使用最佳分辨率回放。<br /> </p> <p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>图像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 图标，以便您分别增大或减小所选图像的缩放。 选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动图像以平移。</p> </td>
      </tr>
      <tr>
      <td>旋转集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 用于分别增大或减小所选图像的缩放的图标。 选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动图像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒体集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 用于分别增大或减小所选图像的缩放的图标。 选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动图像以平移。</p> </td>
      </tr>
      <tr>
      <td>传送集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定查看器中预览资源</strong>
      <ul>
      <li>在页面的左上角附近，单击图标，此时将显示下拉列表。 选择要应用于资源的查看器。</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360视频<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
      <ul>
      <li>在页面的左上角附近，选择图标，此时将显示下拉列表。 选择 <strong>节目</strong>，然后选择要预览的节目。</li>
      </ul> <p><strong>在特定查看器中预览资源</strong></p>
      <ul>
      <li>在页面的左上角附近，选择图标，此时将显示下拉列表。 选择 <strong>查看器</strong>，然后选择要应用于资源的查看器。</li>
      </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 用于分别增大或减小所选图像的缩放的图标。 选择 <strong>重置</strong> 如果要将图像恢复为原始缩放，请执行以下操作。<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动图像以平移。</p> </td>
      </tr>
    </tbody>
    </table>

## 使用键盘预览资源 {#keyboard-navigation-asset-preview}

1. 在Assets用户界面中，导航到包含要预览的资源的文件夹。

1. 在文件夹中，按 `<Tab>` 使用键盘上的键或箭头键选择资产。

1. 按 `<Enter>` 以便您可以在预览模式下打开选定的资源。

1. 执行以下任一操作：

   * 要放大，请按 `<Tab>` 要将焦点移动到放大(+)图标，然后按 `<Enter>` 一次或多次，以增量方式放大。
   * 要缩小，请按 `<Tab>` 要将焦点移动到缩小(-)图标，然后按 `<Enter>` 一次或多次，逐步缩小。
   * 要移动视图 *已缩放* 水平或垂直资源时，按各自的箭头键。
   * 按 `<Shift>` + `<Tab>` 以便您可以重置视图并将焦点放回资源。
