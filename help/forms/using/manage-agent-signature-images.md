---
title: 管理代理签名图像
description: 创建信件模板后，可通过管理数据、内容和附件，在AEM Forms中使用该模板创建信件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: f044ed75-bb72-4be1-aef6-2fb3b2a2697b
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# 管理代理签名图像{#manage-agent-signature-images}

## 概述 {#overview}

在通信管理中，您可以使用图像来呈现信件中的代理签名。 设置代理签名图像后，在创建信件时，可以将信件中的代理签名图像渲染为发件人代理的签名。

agentSignatureImage DDE是一个计算的DDE，表示代理的签名图像。 此计算DDE的表达式使用表达式管理器构建块公开的新自定义函数。 此自定义函数将agentID和agentFolder作为输入参数，并根据这些参数获取图像内容。 SystemContext系统数据字典允许“通信管理”中的信件访问当前系统上下文中的信息。 系统上下文包括有关当前登录的用户和活动配置参数的信息。

您可以在cmuserroot文件夹下添加图像。 在 [通信管理配置属性](/help/forms/using/cm-configuration-properties.md)，使用CM用户根属性，您可以更改从中获取代理签名图像的文件夹。

agentFolder DDE的值从Correspondence Management配置属性的CMUserRoot配置参数中获取。 默认情况下，此配置参数指向CRX存储库中的/content/cmUserRoot。 您可以在配置属性中更改CMUserRoot配置的值。
您还可以覆盖默认自定义函数，以定义您自己的用于获取用户签名图像的逻辑。

## 添加代理签名图像 {#adding-agent-signature-image}

1. 确保代理签名映像的名称与用户的AEM用户名相同。 （图像文件名不需要扩展名。）
1. 在CRX中，创建一个名为的文件夹 `cmUserRoot` 在内容文件夹中。

   1. 转到 `https://'[server]:[port]'/crx/de`. 如有必要，请以管理员身份登录。

   1. 右键单击 **内容** 文件夹并选择 **创建** > **创建文件夹**.

      ![创建文件夹](assets/1_createnode_cmuserroot.png)

   1. 在创建文件夹对话框中，输入文件夹的名称 `cmUserRoot`. 单击&#x200B;**全部保存**。

      >[!NOTE]
      >
      >cmUserRoot是AEM查找代理签名映像的默认位置。 但是，您可以通过编辑中的CM User Root属性来更改它 [通信管理配置属性](/help/forms/using/cm-configuration-properties.md).

1. 在内容资源管理器中，导航到cmUserRoot文件夹并在其中添加代理签名图像。

   1. 转到 `https://'[server]:[port]'/crx/explorer/index.jsp`. 如有必要，以管理员身份登录。
   1. 单击 **内容资源管理器**. 内容资源管理器将在新窗口中打开。
   1. 在内容资源管理器中，导航到cmUserRoot文件夹并将其选定。 右键单击 **cmUserRoot** 文件夹并选择 **新建节点**.

      ![cmUserRoot中的新节点](assets/2_cmuserroot_newnode.png)

      在新节点的行中生成以下条目，然后单击绿色复选标记。

      **名称：** JohnDoe（或代理签名文件的名称）

      **类型：** nt：file

      在 `cmUserRoot` 文件夹，一个名为的新文件夹 `JohnDoe` （或您在上一步中提供的名称）将创建。

   1. 单击已创建的新文件夹（此处） `JohnDoe`)。 内容资源管理器将文件夹的内容显示为灰色。

   1. 双击 **jcr：content** 属性，将其类型设置为 **nt：resource**，然后单击绿色复选标记以保存条目。

      如果属性不存在，请先创建一个名为jcr：content的属性。

      ![jcr：content属性](assets/3_jcrcontentntresource.png)

      jcr：content的子属性中包括jcr：data，它呈灰显状态。 双击jcr：data。 该属性将变为可编辑，并且条目中会显示“选择文件”按钮。 单击 **选择文件** 并选择要用作徽标的图像文件。 图像文件无需扩展名。

      ![JCR数据](assets/5_jcrdata.png)

   单击&#x200B;**全部保存**。

1. 确保您在信件中使用的XDP\layout在左下方（或您要呈现签名的布局中的其他适当位置）有一个图像字段来呈现签名图像。
1. 创建通信时，在“数据”选项卡中，使用以下步骤为签名图像选择一个图像字段：

   1. 从右窗格的“链接类型”弹出菜单中选择“系统”。

   1. 从SystemContext DD的“数据元素”面板的列表中选择agentSignatureImage DDE。

   1. 保存书信。

1. 呈现信件时，您可以在信件预览中看到您根据布局在图像字段中签名。

   ![信件中的代理签名图像](assets/letterwithsignature.png)
