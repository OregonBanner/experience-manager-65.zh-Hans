---
title: 使用具有客户端设备像素比的智能成像
description: 了解如何在Adobe Experience Manager as a Cloud Service中结合使用客户端设备像素比率和智能成像，以及Dynamic Media。
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 关于使用客户端设备像素比(DPR)进行智能成像 {#client-side-dpr}

当前的智能成像解决方案使用用户代理字符串来确定正在使用的设备类型（台式机、平板电脑、移动设备等）。

设备检测功能（基于用户代理字符串的DPR）通常不准确，尤其是对于Apple设备。 此外，无论何时启动新设备，都必须对其进行验证。

客户端DPR可为您提供100%的准确值，并且适用于任何设备(无论是Apple还是启动的任何其他新设备)。

## 使用客户端DPR代码

**服务器端渲染的应用程序**

1. 加载服务工作程序初始化(`srvinit.js`)，方法是在HTML页面的标头部分包含以下脚本：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe建议您加载此脚本 _之前_ 任何其他脚本，以便服务工作人员立即开始初始化。

1. 在HTML页面正文部分的顶部包含以下DPR图像标记代码：

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   必须包含此DPR图像标记代码 _之前_ 您的HTML页面中的所有静态图像。

**客户端渲染的应用程序**

1. 在HTML页面的标题部分包含以下DPR脚本：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   您可以将两个DPR脚本合并为一个脚本，以避免多个网络请求。

   Adobe建议您加载这些脚本 _之前_ “HTML”页面中的任何其他脚本。
Adobe还建议您在差异HTML标记下Bootstrap应用程序，而不是正文元素。 原因是 `dprImageInjection.js` 动态插入位于HTML页面主体部分顶部的图像标记。

## JavaScript文件下载 {#client-side-dpr-script}

下载中的以下JavaScript文件仅作为示例引用提供给您。 如果您打算在HTML页面中使用这些文件，请确保编辑每个文件的代码以符合您自己的要求。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript文件下载](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [智能图像处理](/help/assets/imaging-faq.md)

