---
title: 管理代理签名图像
seo-title: 管理代理签名图像
description: 在创建了信件模板后，您可以使用它管理数据、内容和附件，在AEM Forms中创建通信。
seo-description: 在创建了信件模板后，您可以使用它管理数据、内容和附件，在AEM Forms中创建通信。
uuid: 48b2697e-6065-4e23-9aa8-333e7b11ede1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: a81cdd53-f0fb-4ac5-b2ec-c19aeee7186e
docset: aem65
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# 管理代理签名映像{#manage-agent-signature-images}

## 概述 {#overview}

在Corresponce Management中，您可以使用图像以字母形式呈现代理签名。 在设置代理签名图像后，在创建信函时，您可以将信件中的代理签名图像作为发送方代理的签名呈现。

agentSignatureImage DDE是表示代理的签名图像的计算DDE。 此计算DDE的表达式使用由表达式管理器构建块公开的新自定义函数。 此自定义函数将agentID和agentFolder作为输入参数，并基于这些参数获取图像内容。 SystemContext系统数据字典为Correspondence Management中的字母提供了对当前系统上下文中的信息的访问权限。 系统上下文包括有关当前登录用户和活动配置参数的信息。

您可以在cmuserroot文件夹下添加图像。 在[对应管理配置属性](/help/forms/using/cm-configuration-properties.md)中，使用“CM用户根”属性，可以更改从中获取代理签名图像的文件夹。

agentFolder DDE的值来自Corresponce Management配置属性的CMUserRoot配置参数。 默认情况下，此配置参数指向CRX存储库中的/content/cmUserRoot。 可以在“配置属性”中更改CMUserRoot配置的值。
您还可以覆盖默认自定义函数以定义您自己获取用户签名图像的逻辑。

## 添加代理签名映像{#adding-agent-signature-image}

1. 确保代理签名图像的名称与用户的AEM用户名相同。 （图像文件名不需要扩展名。）
1. 在CRX中，在内容文件夹中创建一个名为`cmUserRoot`的文件夹。

   1. 转到 `https://'[server]:[port]'/crx/de`. 如有必要，请以管理员身份登录。

   1. 右键单击&#x200B;**content**&#x200B;文件夹，然后选择&#x200B;**创建** > **创建文件夹**。

      ![创建文件夹](assets/1_createnode_cmuserroot.png)

   1. 在“创建文件夹”对话框中，输入文件夹名称`cmUserRoot`。 单击&#x200B;**保存全部**。

      >[!NOTE]
      >
      >cmUserRoot是AEM查找代理签名图像的默认位置。 但是，您可以通过编辑[Corresponce Management配置属性](/help/forms/using/cm-configuration-properties.md)中的CM User Root属性来更改它。

1. 在内容资源管理器中，导航到cmUserRoot文件夹并在其中添加代理签名图像。

   1. 转到 `https://'[server]:[port]'/crx/explorer/index.jsp`. 如有必要，以管理员身份登录。
   1. 单击&#x200B;**内容资源管理器**。 内容浏览器将在新窗口中打开。
   1. 在内容资源管理器中，导航到cmUserRoot文件夹并选择它。 右键单击&#x200B;**cmUserRoot**&#x200B;文件夹，然后选择&#x200B;**新建节点**。

      ![cmUserRoot中的新节点](assets/2_cmuserroot_newnode.png)

      在新节点的行中进行以下条目，然后单击绿色复选标记。

      **名称：** JohnDoe（或您的代理签名文件的名称）

      **类型：** nt:file

      在`cmUserRoot`文件夹下，将创建一个名为`JohnDoe`的新文件夹（或您在上一步中指定的名称）。

   1. 单击您创建的新文件夹（此处为`JohnDoe`）。 “内容资源管理器”会将文件夹的内容显示为灰显。

   1. 多次 — 单击&#x200B;**jcr:content**&#x200B;属性，将其类型设置为&#x200B;**nt:resource**，然后单击绿色复选标记以保存条目。

      如果该属性不存在，请首先创建名为jcr:content的属性。

      ![jcr:content属性](assets/3_jcrcontentntresource.png)

      jcr:content的子属性中有jcr:data，它是灰显的。 多次单击jcr:data。 该属性将变为可编辑，条目中将显示“选择文件”按钮。 单击&#x200B;**选择文件**，然后选择要用作徽标的图像文件。 图像文件不需要扩展名。

      ![JCR数据](assets/5_jcrdata.png)
   单击&#x200B;**保存全部**。

1. 确保您在字母中使用的XDP\layout在左下角有一个图像字段（或您要呈现签名的布局中的其他适当位置），以呈现签名图像。
1. 创建通信时，在“数据”选项卡中，使用以下步骤为签名图像选择一个图像字段：

   1. 从右侧窗格的“链接类型”弹出菜单中选择“系统”。

   1. 从SystemContext DD的“列表元素”面板中的“代理签名图像DDE”中选择代理。

   1. 保存信。

1. 呈现字母后，您会看到您根据布局在图像字段中的字母预览中签名。

   ![信中的代理签名图像](assets/letterwithsignature.png)

