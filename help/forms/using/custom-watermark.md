---
title: 字母PDF预览中的自定义水印
seo-title: 字母PDF预览中的自定义水印
description: 了解如何在字母PDF预览中创建自定义水印。
seo-description: 了解如何在字母PDF预览中创建自定义水印。
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# 字母PDF预览{#custom-watermark-in-letter-pdf-preview}中的自定义水印

## 概述 {#overview}

在“创建通信”UI中，代理用户将通信预览为最终形状，在最终形状下发送给后期处理，例如用于电子邮件或打印。

为防止未授权使用此预览，组织可以在PDF上加上水印。 默认水印为“预览”，它显示在PDF中。

要在预览PDF中启用水印，请在https://&#39;[服务器]:[端口]&#39;/system/console/configMgr的&#x200B;**[!UICONTROL 对应管理配置]**&#x200B;中选择&#x200B;**[!UICONTROL 在预览期间应用水印]**&#x200B;选项。

![default-watermark](assets/default-watermark.png)

您可以使用以下步骤自定义水印的文本和外观：

## 在“创建对应UI {#customizewatermark-}”中自定义PDF预览中的水印

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为&#x200B;**[!UICONTROL previewwatermark]**&#x200B;的文件夹，其路径／结构与libs文件夹中的previewwatermark文件夹类似：

   1. 右键单击以下路径中的&#x200B;**previewwatermark**&#x200B;文件夹，然后选择&#x200B;**叠加节点**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 确保“叠加节点”对话框具有以下值：

      **路径：** /libs/fd/cm/configFiles/previewwatermark

      **叠加位置** :/apps/

      **匹配节点类型：已选** 中

      >[!NOTE]
      >
      >请勿在/libs分支中进行更改。 您所做的任何更改都可能会丢失，因为只要您：
      >
      >    
      >    
      >    * 在实例上升级
      >    * 应用热修复
      >    * 安装功能包


   1. 单击&#x200B;**确定**，然后单击&#x200B;**保存全部**。 在指定路径中创建&#x200B;**[!UICONTROL previewwatermark]**&#x200B;文件夹。



1. 将ddx文件从“/libs/fd/cm/configFiles/previewwatermark”文件夹复制并粘贴到“/apps/fd/cm/configFiles/previewwatermark”文件夹，然后单击&#x200B;**[!UICONTROL 保存全部]**。
1. 在/apps/fd/cm/configFiles/previewwatermark/下的ddx文件中进行所需的更改。

   ```xml
   <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
    <PDF result="output.pdf">
     <PDF source="input.pdf"/>
           <Watermark opacity="15%" rotation="45">
            <StyledText>
                     <p font-family="Georgia" font-size="70pt" color="black" font-weight="bold">
                         PREVIEW
                    </p>
            </StyledText>
           </Watermark>
    </PDF>
   </DDX>
   ```

   有关自定义水印外观、文本和对齐方式的信息，请参阅[Assembler Service和DDX Reference](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf)文档中的添加和删除水印和背景。

   >[!NOTE]
   >
   >在ddx文件中，对结果和源的引用应保持不更改为output.pdf和input.pdf。 不应更改文件ddx的名称。

1. 单击&#x200B;**保存全部**。

