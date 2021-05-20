---
title: 信件PDF预览中的自定义水印
seo-title: 信件PDF预览中的自定义水印
description: 了解如何在信件PDF预览中创建自定义水印。
seo-description: 了解如何在信件PDF预览中创建自定义水印。
uuid: 5adfede3-9b38-4a12-bf14-6d80cfb0a05a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: adc7ec13-0675-4071-9c4c-e238202d9d85
docset: aem65
feature: 通信管理
exl-id: 7d90fade-1ca4-41d8-bbf9-45490465784a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# 信件PDF预览中的自定义水印{#custom-watermark-in-letter-pdf-preview}

## 概述 {#overview}

在“创建通信”UI中，代理用户以最终形式预览通信，在最终形式中，通信被发送到后处理，如用于电子邮件或打印。

为防止未经授权使用此数据，组织可以对预览PDF强制施加水印。 默认水印为“PREVIEW”，该水印在PDF中显示。

要在预览PDF中启用水印，请在https://&#39;[服务器]:[端口]`/system/console/configMgr的&#x200B;**[!UICONTROL 通信管理配置]**&#x200B;中选择&#x200B;**[!UICONTROL 应用水印]**&#x200B;预览期间选项。

![默认水印](assets/default-watermark.png)

您可以使用以下步骤来自定义水印的文本和外观：

## 在创建通信UI {#customizewatermark-}的PDF预览中自定义水印

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为&#x200B;**[!UICONTROL previewwatermark]**&#x200B;的文件夹，其路径/结构与libs文件夹中的previewwatermark文件夹类似：

   1. 右键单击以下路径中的&#x200B;**previewwatermark**&#x200B;文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/configFiles/previewwatermark`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/configFiles/previewwatermark

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

      >[!NOTE]
      >
      >请勿在/libs分支中进行更改。 您所做的任何更改都可能会丢失，因为当您执行以下操作时，此分支将容易发生更改：
      >
      >    
      >    
      >    * 在实例上升级
      >    * 应用热修复程序
      >    * 安装功能包


   1. 单击&#x200B;**确定**，然后单击&#x200B;**保存全部**。 在指定的路径中创建&#x200B;**[!UICONTROL previewwatermark]**&#x200B;文件夹。



1. 将dx文件从“/libs/fd/cm/configFiles/previewwatermark”文件夹复制并粘贴到“/apps/fd/cm/configFiles/previewwatermark”文件夹，然后单击&#x200B;**[!UICONTROL 保存所有]**。
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

   有关自定义水印外观、文本和对齐方式的信息，请参阅[汇编程序服务和DDX参考](https://help.adobe.com/en_US/livecycle/11.0/ddxRef.pdf)文档中的添加和删除水印和背景。

   >[!NOTE]
   >
   >在ddx文件中，对结果和源的引用应保持不更改为output.pdf和input.pdf。 文件ddx的名称也不应更改。

1. 单击&#x200B;**Save All**。
