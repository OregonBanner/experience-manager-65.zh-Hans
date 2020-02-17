---
title: 交互通信概述
seo-title: 交互通信概述
description: 本文包括概述、示例用例、创建工作流以及交互式通信和字母之间的区别。
seo-description: 交互通信关键功能、示例用例、创建工作流程以及交互通信和通信管理之间的差异
uuid: a06b4ac7-ca20-4d6d-b2b7-87b21e2f5cf9
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: 67b03098-c58d-4a57-90e0-e4ddd78e5d99
translation-type: tm+mt
source-git-commit: dc7804c9985bf9a14bfad40f546e393b39615dab

---


# 交互通信概述 {#interactive-communications-overview}

本文包括概述、示例用例、创建工作流以及交互式通信和字母之间的区别。

![](do-not-localize/correspondence-management.png)

Interactive Communications集中化和管理安全、个性化和交互式通信的创建、汇编和交付，如业务通信、文档、声明、利益声明、营销邮件、帐单和欢迎工具包。

## 关键功能 {#key-capabilities}

以下是Interactive Communications的主要功能：

* 与表单数据模型的即装即用集成，可轻松简化对后端数据库和其他CRM系统（如MS® Dynamics）的访问
* 用于打印和Web渠道的集成创作界面，能够从打印渠道自动生成Web渠道
* 以易于理解的可视格式在印刷品和Web中展示信息的图表
* 文档片段支持规则编辑器和表单数据模型
* 代理用户界面显示交互式通信的打印和Web预览
* 拖放组件可快速构建印刷和Web渠道

## 示例用例 {#sample-use-case}

信用 [卡客户示例用例的欢迎工具包](/help/forms/using/finance-reference-site-walkthrough.md#credit-card-application-walkthrough) (Welcome kit for a credit card customer)展示了交互式通信的功能。

## Interactive Communication creation  {#interactive-communication-creation}

![interactive_communication-01](assets/interactive_communication-01.jpg)

### 工作流 {#workflow}

要创建交互式通信，请准备好 [交互式通信的构](#buildingblocks) 建块，然后完成以下步骤：

1. 选择创建 [交互式通信](/help/forms/using/create-interactive-communication.md)。

1. 指定表 [单数据模型](/help/forms/using/data-integration.md)、预填服务以及 [打印和Web渠道模板](/help/forms/using/web-channel-print-channel.md)。 您可以选择从打印渠道生成Web渠道。

1. 使用拖 [放界面](/help/forms/using/introduction-interactive-communication-authoring.md)，根据需要添加文档片段、图像、组件以打印和Web通道。
1. 为插入的组件配置属性，如：

   1. [图像](/help/forms/using/create-interactive-communication.md#step2)
   1. [表](/help/forms/using/create-interactive-communication.md#tables) （包括布局片段）
   1. [图表](/help/forms/using/chart-component-interactive-communications.md)
   1. [文档片段](/help/forms/using/create-interactive-communication.md#document-fragment-properties)

1. 预览打印和Web渠道，并根据需要编辑交互式通信。
1. 代理使用代理UI准备交 [互式通信](/help/forms/using/prepare-send-interactive-communication.md) ，以将其发送到收件人／帖子进程。

### 构建基块 {#buildingblocks}

以下是创建交互式通信所需的构件块：

* [表单数据模型](/help/forms/using/data-integration.md)
* [印刷和Web渠道模板](/help/forms/using/web-channel-print-channel.md)
* [文档片段](/help/forms/using/document-fragments.md)
* 图像
* [Web渠道](/help/forms/using/themes.md) 的主题

## 交互通信与通信管理 {#interactive-communications-vs-correspondence-management}

交互通信是创建客户通信的默认和推荐方法。 要继续使用在AEM 6.3 Forms和AEM 6.2 Forms中创建的字母，您需要安 [装兼容包](/help/forms/using/compatibility-package.md)。 以下是交互通信功能与字母功能的比较。

<table>
 <tbody>
  <tr>
   <td><strong>功能</strong></td>
   <td><strong>交互式通信</strong></td>
   <td><strong>书信</strong></td>
  </tr>
  <tr>
   <td>输出</td>
   <td>印刷和Web</td>
   <td>打印</td>
  </tr>
  <tr>
   <td>架构</td>
   <td>表单数据模型 </td>
   <td>数据字典 </td>
  </tr>
  <tr>
   <td>本地化</td>
   <td>表单数据模型中不支持</td>
   <td>数据字典中支持</td>
  </tr>
  <tr>
   <td>规则编辑器</td>
   <td>
    <ul>
     <li>文本和条件支持规则编辑器，用于创建内联条件</li>
     <li>交互式通信编辑器支持在Web通道组件上应用规则</li>
    </ul> </td>
   <td>没有用于创建条件表达式的UI</td>
  </tr>
  <tr>
   <td>创作</td>
   <td>用于构建打印和Web通道的拖放界面</td>
   <td>无拖放机构 </td>
  </tr>
  <tr>
   <td>图表</td>
   <td>印刷和Web渠道中支持的图表</td>
   <td>不受支持</td>
  </tr>
  <tr>
   <td>主题</td>
   <td>使用主题来设计Web渠道的样式</td>
   <td>不支持主题</td>
  </tr>
  <tr>
   <td>审核和版本控制</td>
   <td>不受支持</td>
   <td>受支持</td>
  </tr>
  <tr>
   <td>草稿和管理实例</td>
   <td>不受支持</td>
   <td>受支持</td>
  </tr>
  <tr>
   <td>批处理</td>
   <td>受支持 </td>
   <td>受支持</td>
  </tr>
  <tr>
   <td>代理签名</td>
   <td>不受支持</td>
   <td>受支持</td>
  </tr>
  <tr>
   <td>远程功能</td>
   <td>不受支持</td>
   <td>受支持</td>
  </tr>
 </tbody>
</table>

