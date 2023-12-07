---
title: 图像编辑器
description: 图像编辑器是AEM的核心部分，组件可以使用该编辑器来促进内容作者处理图像。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 9%

---

# 图像编辑器{#image-editor}

图像编辑器是AEM的核心部分，组件可以使用该编辑器来促进内容作者处理图像。

>[!CAUTION]
>
>要使用本文中介绍的图像编辑器的功能， [功能包24267](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 必须安装。

## 图像映射的相对单位 {#relative-units-for-image-map}

图像编辑器将图像映射区域作为绝对和相对单位保留。 当提供相对单位作为数据属性用于动态调整响应图像组件中客户端上的图像映射（相对于图像大小）的大小时，相对单位很有用。

### imageMap属性 {#imagemap-property}

图像映射坐标作为 `imageMap` 属性。 它具有以下格式。

该属性按如下方式存储映射区域：

`[area1][area2][...]`

区域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

示例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支持SVG图像 {#support-for-svg-images}

图像编辑器支持可缩放矢量图形(SVG)。

* 从 DAM 拖放上传 SVG 资源以及从本地文件系统上传 SVG 文件均受支持。

## 按MIME类型启用插件 {#enabling-plugins-by-mime-type}

在某些情况下，由于服务器端处理缺乏支持，必须限制某些MIME类型的创作操作。 例如，可能不允许编辑SVG图像。

MIME类型可以通过设置 `supportedMimeTypes` 属性。

### 示例 {#example}

例如，假设仅允许对GIF、JPEG、PNG、WEBP和TIFF图像使用裁切功能。

此 `supportedMimeTypes` 然后，必须在上的插件的配置节点上将属性设置为允许的MIME类型的字符串。 `cq:editConfig` 图像组件的节点。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
