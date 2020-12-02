---
title: “教程：规划交互式通信”
seo-title: 规划您的交互式通信
description: 规划交互式通信的剖析
seo-description: 规划交互式通信的剖析
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 3%

---


# 教程：规划交互式通信{#tutorial-plan-the-interactive-communication}

规划交互式通信的剖析

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是[创建您的第一个交互式通信](/help/forms/using/create-your-first-interactive-communication.md)系列中的一个步骤。 建议按照时间顺序按照系列来了解、执行和演示完整的教程用例。

规划交互式通信的第一步是最终确定交互式通信的内容。 法律、财务、支持或营销等部门的主题专家可以帮助您最终确定内容。 内容完成后，您必须对其进行分析，以确定创建交互式通信所需的各种资产类型。

## 规划注意事项{#planning-considerations}

交互式通信包括以下元素：

* **静** 态文本主要包括交互式通信的一般部分，这些部分在性质上是通用的，并包含在与所有客户的通信中。例如，页眉、页脚、问候或免责声明。
* **从后端系统（表单数据模型）来源** 的数据是客户特定的，并与交互式通信动态合并。例如，策略编号或地址可以使用表单数据模型来源。
* **用于打** 印和Web版本的交互式通信的布局或模板。
* **交** 互式通信中显示各种文本段落的顺序。
* **正在自定义通信的前线员工(代理** UI)在发送通信前输入的数据。例如，付款到期日。

* **根据** 预定义条件填充的条件数据。例如，生成交互式通信的日期。
* **存储在存储库中的图像**，如徽标和签名图像。企业徽标等图像将出现在大多数或所有交互式通信中。
* **简化交** 互式通信中复杂数据表示所需的图表和表

## 交互通信剖析{#anatomy-of-the-interactive-communication}

完成用于创建交互式通信的内容和元素后，您可以创建交互式通信的剖析。 解剖结构必须包含[规划注意事项](/help/forms/using/planning-interactive-communications.md#planning-considerations)部分中列出的详细信息。 根据我们的使用案例，以下是电信运营商向其客户发送的月度账单的剖析示例。

解剖结构包括具有以下输入模式的数据：

* 静态文本
* 表单数据模型
* 代理 UI
* 条件数据
* 图像

在每个部分中，粗体文本表示静态文本。 数据库包括customer、bills和calls表。 表单数据模型可以从这些表中的任何一个接收数据。 有关详细信息，请参阅[创建表单数据模型](/help/forms/using/create-form-data-model0.md)。

下表说明了交互式通信剖析中每个字段的数据源：

<table>
 <tbody>
  <tr>
   <td>区域</td>
   <td>静态文本</td>
   <td>FDM </td>
   <td>代理 UI</td>
   <td>图像</td>
  </tr>
  <tr>
   <td>帐单详细信息</td>
   <td><p>发票编号</p> <p>帐单日期</p> <p>帐单期间</p> <p>您的计划</p> </td>
   <td><p><strong>您的计划</strong>字段的值</p> <p>表——客户</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>发票编号</li>
     <li>帐单日期</li>
     <li>帐单期间</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>客户详细信息</td>
   <td><p>供应地</p> <p>状态代码</p> <p>移动号码</p> <p>备用联系人号码</p> <p>关系编号</p> <p>连接数</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>名称</li>
     <li>地址</li>
     <li>移动号码</li>
     <li>备用联系人号码</li>
     <li>关系编号</li>
    </ul> <p>表——客户</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>供应地</li>
     <li>状态代码</li>
     <li>连接数</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>帐单汇总</td>
   <td><p>上一余额</p> <p>付款</p> <p>调整</p> <p>当前帐单期间的费用</p> <p>到期金额</p> <p>到期日期</p> </td>
   <td><p><strong>当前帐单期间</strong>字段的值</p> <p>表——清单</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>上一余额</li>
     <li>付款</li>
     <li>调整</li>
     <li>到期金额</li>
     <li>到期日期</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>费用汇总</td>
   <td><p>通话费</p> <p>电话会议费用</p> <p>短信费用 </p> <p>移动Internet费用</p> <p>国家漫游费用</p> <p>国际漫游费用</p> <p>增值服务费</p> <p>总费用</p> <p>应付总额</p> <p>“增值服务费用”字段上的条件</p> </td>
   <td><p>以下字段的值：</p>
    <ul>
     <li>通话费</li>
     <li>电话会议费用</li>
     <li>短信费用 </li>
     <li>移动Internet费用</li>
     <li>国家漫游费用</li>
     <li>国际漫游费用</li>
     <li>增值服务费</li>
     <li>总费用（“未计费用”计算字段）</li>
     <li>应付总额（“未付”计算字段）</li>
    </ul> <p>表——清单</p> </td>
   <td>无字段</td>
   <td>—</td>
  </tr>
  <tr>
   <td>明细调用——传出</td>
   <td><p>列名称：</p>
    <ul>
     <li>日期</li>
     <li>时间</li>
     <li>数字</li>
     <li>持续时间</li>
     <li>费用</li>
    </ul> </td>
   <td><p>所有值</p> <p>表——调用</p> </td>
   <td>无字段</td>
   <td>—</td>
  </tr>
  <tr>
   <td>立即付款</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>增值服务</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

