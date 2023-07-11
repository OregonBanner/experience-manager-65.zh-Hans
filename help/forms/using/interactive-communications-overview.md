---
title: 交互式通信概述
seo-title: Interactive Communications Overview
description: 本文包括概述、示例用例、创建工作流以及交互式通信与信件之间的区别。
seo-description: Interactive Communication key capabilities, sample use cases, creation workflow, and differences between Interactive Communication and Correspondence Management
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
topic-tags: interactive-communications, introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
exl-id: 6cfbeec0-0be3-48b2-a4bb-fd19c69c92c7
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 7%

---


# 交互式通信概述 {#interactive-communications-overview}

本文包括概述、示例用例、创建工作流以及交互式通信与信件之间的区别。

![hero-image](do-not-localize/correspondence-management.png)

交互式通信可以集中管理安全、个性化的交互式信函的创建、编排和交付，例如业务信函、文档、对帐单、福利通知、营销邮件、账单和欢迎资料包。

## 主要功能 {#key-capabilities}

以下是交互式通信的主要功能：

- 与表单数据模型的现成集成，使对后端数据库和其他CRM系统(如MS® Dynamics)的访问变得轻松而简化
- 打印和Web渠道的集成创作界面，能够自动从打印渠道生成Web渠道
- 以易于理解的可视格式在打印和Web中展示信息的图表
- 文档片段支持规则编辑器和表单数据模型
- 代理用户界面显示交互式通信的打印和Web预览
- 拖放组件以快速构建打印和Web渠道

## 交互式通信创建 {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### 工作流 {#workflow}

要创建交互式通信，请 [构建基块](#buildingblocks) 准备交互式通信，然后完成以下步骤：

1. 选择以 [创建交互式通信](/help/forms/using/create-interactive-communication.md).

1. 指定 [表单数据模型](/help/forms/using/data-integration.md)，预填充服务，以及 [打印和Web渠道模板](/help/forms/using/web-channel-print-channel.md). 您可以选择从打印渠道生成Web渠道。

1. 使用 [拖放界面](/help/forms/using/introduction-interactive-communication-authoring.md)，根据需要添加要打印的文档片段、图像、组件以及交互式通信的Web渠道。
1. 为插入的组件配置属性，如下所示：

   1. [图像](/help/forms/using/create-interactive-communication.md#step2)
   1. [表](/help/forms/using/create-interactive-communication.md#tables) （包括布局片段）
   1. [图表](/help/forms/using/chart-component-interactive-communications.md)
   1. [文档片段](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 预览打印和Web渠道，并根据需要编辑交互式通信。
1. 代理使用代理UI来 [准备交互式通信](/help/forms/using/prepare-send-interactive-communication.md) ，以发送给收件人/后处理。

### 构建基块 {#buildingblocks}

以下是创建交互式通信所需的构建块：

- [表单数据模型](/help/forms/using/data-integration.md)
- [打印和Web渠道模板](/help/forms/using/web-channel-print-channel.md)
- [文档片段](/help/forms/using/document-fragments.md)
- 图像
- [主题](/help/forms/using/themes.md) 对于Web渠道

## 交互式通信与通信管理 {#interactive-communications-vs-correspondence-management}

交互式通信是创建客户通信的默认和推荐方法。 要继续使用在AEM 6.3 Forms和AEM 6.2 Forms中创建的字母，您需要 [安装兼容包](/help/forms/using/compatibility-package.md). 以下是交互式通信功能和信件功能的比较。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>交互式通信</strong></td>
   <td><strong>书信</strong></td>
  </tr>
  <tr>
   <td>输出</td>
   <td>打印和Web</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>Schema</td>
   <td>表单数据模型 </td>
   <td>数据字典 </td>
  </tr>
  <tr>
   <td>本地化</td>
   <td>表单数据模型不支持</td>
   <td>在数据字典中受支持</td>
  </tr>
  <tr>
   <td>规则编辑器</td>
   <td>
    <ul>
     <li>用于创建内联条件的文本和条件支持规则编辑器</li>
     <li>交互式通信编辑器支持在Web渠道的组件中应用规则</li>
    </ul> </td>
   <td>没有用于创建条件表达式的UI</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>用于构建打印和Web渠道的拖放界面</td>
   <td>无拖放机制 </td>
  </tr>
  <tr>
   <td>图表</td>
   <td>打印和Web渠道中支持的图表</td>
   <td>不受支持</td>
  </tr>
  <tr>
   <td>主题</td>
   <td>使用主题为Web渠道设置样式</td>
   <td>不支持主题</td>
  </tr>
   <tr>
   <td>草稿</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>提交内容</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
  <tr>
   <td>审核</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
   <tr>
   <td>版本控制</td>
   <td>不支持</td>
   <td>支持</td>
  </tr>
   <td>批处理</td>
   <td>支持 </td>
   <td>支持</td>
  </tr>
  <tr>
   <td>代理签名</td>
   <td>不受支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <td>远程功能</td>
   <td>不受支持</td>
   <td>支持</td>
  </tr>
 </tbody>
</table>
