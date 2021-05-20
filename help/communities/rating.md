---
title: 使用评级
seo-title: 使用评级
description: 向页面添加评级组件
seo-description: 向页面添加评级组件
uuid: a986970b-1221-4648-9a69-410f4480e0ae
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a0e5491e-66bc-47b0-94a5-45a02bc558da
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 2%

---

# 使用评级{#using-ratings}

`Rating`组件是独立的，或与其他Communities功能结合使用。 此组件允许已登录的社区成员通过对内容进行评级来表达其意见。

## 向页面{#adding-a-rating-to-a-page}添加评级

要在创作模式下将`Rating`组件添加到页面，请找到组件`Communities / Rating`并将其拖动到页面上的位置，如相对于要评级的成员的功能的位置。

有关必要信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](rating-basics.md#essentials-for-client-side)时，将显示`Rating`组件。

![评级](assets/rating.png)

## 配置评级{#configuring-rating}

选择要访问的已放置的`Rating`组件，然后选择`Configure`图标以打开编辑对话框。

![configure-new](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文本和标签]**&#x200B;选项卡下，指定评级的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL 计数名称]**
(*必需*)唯一标识此实 `Rating` 例的简单名称。必须是存储库的有效节点名称。

## 网站访客体验{#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个评级。 会员可随时更改其评级。

### 匿名 {#anonymous}

不支持匿名发布评级。 网站访客必须注册（成为会员）并登录以参与。

## 附加信息 {#additional-information}

有关更多信息，请参阅[Rating Essentials](rating-basics.md)页面，供开发人员使用。
