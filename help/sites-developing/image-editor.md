---
title: 图像编辑器
seo-title: 图像编辑器
description: 图像编辑器是AEM的一个核心部分，组件可以利用它来方便内容作者处理图像。
seo-description: 图像编辑器是AEM的一个核心部分，组件可以利用它来方便内容作者处理图像。
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 图像编辑器{#image-editor}

图像编辑器是AEM的一个核心部分，组件可以利用它来方便内容作者处理图像。

>[!CAUTION]
>
>要使用本文所述的图像编辑器功能， [必须安装功能包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) 24267。

## 图像映射的相对单位 {#relative-units-for-image-map}

图像编辑器将图像映射区域保留为绝对和相对单位。 当作为数据属性提供在响应式图像组件中用于在客户端动态调整图像映射（相对于图像大小）的时候，相对单位是有用的。

### imageMap属性 {#imagemap-property}

图像编辑器将图像映射坐标作为属 `imageMap` 性保留到JCR。 其格式如下。

属性存储如下映射区域：

`[area1][area2][...]`

区域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

示例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支持SVG图像 {#support-for-svg-images}

图像编辑器支持可缩放矢量图形(SVG)。

* 支持从DAM拖放SVG资源以及从本地文件系统上传SVG文件。

## 按MIME类型启用插件 {#enabling-plugins-by-mime-type}

在某些情况下，创作操作必须限于某些MIME类型，因为服务器端处理中不支持。 例如，可能不允许编辑SVG图像。

通过在单个插件的配置节点上设置属性，可以按MIME类 `supportedMimeTypes` 型选择性地启用图像编辑器中的插件。

### 示例 {#example}

例如，假设仅允许对GIF、JPEG、PNG、WEBP和TIFF图像进行裁切。

然 `supportedMimeTypes` 后，必须将该属性设置为图像组件节点上插件的配置节点上允许的MIME `cq:editConfig` 类型的字符串。

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

