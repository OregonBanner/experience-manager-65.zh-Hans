---
title: 基于XDP的自适应表单中的XFA支持
seo-title: 基于XDP的自适应表单中的XFA支持
description: 列表支持自适应表单中的XFA事件、属性、脚本和验证。
seo-description: 列表支持自适应表单中的XFA事件、属性、脚本和验证。
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 5%

---


# 基于XDP的自适应表单中的XFA支持{#xfa-support-in-xdp-based-adaptive-forms}

## 简介 {#introduction}

自适应表单支持在XDP文件中定义的各种XFA事件、属性、脚本和验证，包括：

* 执行在XDP文件中的事件上定义的脚本。
* 捕获XDP文件中字段的默认值和行为属性。
* 执行XDP文件中定义的验证脚本。

当基于XDP文件创建自适应表单时，将在表单创作UI中自动填充属性、事件和验证。 但是，表单作者可以覆盖其中的一些元素，以创建替代体验。

本文列表支持自适应表单中接受的XFA事件、属性和验证，并说明如何在自适应表单中覆盖它们。

## 自适应表单{#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}中支持的XFA元素及其映射

### 字段 {#fields}

使用XDP文件创建自适应表单时，可以将XFA字段拖放到自适应表单上。 下表列表了XFA字段如何映射到自适应表单字段。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA字段或容器</strong></p> </td>
   <td><p><strong>相应的自适应表单组件</strong></p> </td>
  </tr>
  <tr>
   <td><p>按钮 </p> </td>
   <td><p>按钮</p> </td>
  </tr>
  <tr>
   <td><p>复选框 </p> </td>
   <td><p>复选框</p> </td>
  </tr>
  <tr>
   <td><p>列表框 </p> </td>
   <td><p>下拉列表</p> </td>
  </tr>
  <tr>
   <td><p>日期／时间字段 </p> </td>
   <td><p>日期选取器</p> </td>
  </tr>
  <tr>
   <td><p>签名涂写</p> </td>
   <td><p>潦草签名</p> </td>
  </tr>
  <tr>
   <td><p>数字字段 </p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>十进制字段</p> </td>
   <td><p>数值框</p> </td>
  </tr>
  <tr>
   <td><p>文本字段 </p> </td>
   <td><p>文本框</p> </td>
  </tr>
  <tr>
   <td><p>密码字段 </p> </td>
   <td><p>密码框</p> </td>
  </tr>
  <tr>
   <td><p>图像</p> </td>
   <td><p>图像</p> </td>
  </tr>
  <tr>
   <td><p>文本</p> </td>
   <td><p>文本</p> </td>
  </tr>
  <tr>
   <td><p>子表单 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>区域（组）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子表单集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 属性 {#properties}

下表捕获了在XDP文件中定义的各种XFA脚本在自适应表单中的行为。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA组件属性</strong></p> </td>
   <td><p><strong>自适应表单中的相应行为</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>以自适应形式映射到“绑定引用”(bindRef)属性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>映射到自适应表单中的可见属性。 您可以使用“可见性”表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>访问 </p> </td>
   <td><p>映射到自适应表单中的启用属性。 您可以使用访问表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：角色 </p> </td>
   <td><p>映射到自适应表单中的角色属性。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：speatPriority </p> </td>
   <td><p>以自适应形式映射到speakPriority属性。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：speakText</p> </td>
   <td><p>映射到自适应表单中的自定义辅助功能文本。</p> </td>
  </tr>
  <tr>
   <td><p>辅助功能：工具提示 </p> </td>
   <td><p>映射到自适应表单中的简短描述属性。</p> </td>
  </tr>
  <tr>
   <td><p>题注<em>（所有字段类型）</em></p> </td>
   <td><p>映射到自适应表单中的“标题”属性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em>（所有字段类型）</em></p> </td>
   <td><p>以自适应形式映射到显示模式。</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em>（所有字段类型）</em></p> </td>
   <td><p>映射到自适应表单中的值属性。</p> </td>
  </tr>
  <tr>
   <td><p>项<em>(列表框，复选框)</em></p> </td>
   <td><p>映射到自适应表单中的选项属性。 您可以使用“选项”表达式覆盖它。</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em>（文本字段）</em></p> </td>
   <td><p>映射到自适应表单中允许的最大字符数属性。</p> </td>
  </tr>
  <tr>
   <td><p>multiline<em>（文本字段）</em></p> </td>
   <td><p>映射到自适应表单中的允许多行属性。</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em>（数字字段，小数字字段）</em></p> </td>
   <td><p>映射到自适应表单中的Frac digits属性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em>（数字字段，小数字字段）</em></p> </td>
   <td><p>映射到自适应表单中的潜在客户数字属性。</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em>(列表框)</em></p> </td>
   <td><p>映射到自适应表单中的允许多个选择属性。</p> </td>
  </tr>
 </tbody>
</table>

### 脚本 {#scripts}

下表捕获了在XDP文件中定义的各种XFA脚本在自适应表单中的行为。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA脚本事件</strong></p> </td>
   <td><p><strong>自适应表单中的相应行为</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>计算</p> </td>
   <td><p>以自适应形式映射到“计算表达式”。</p> </td>
  </tr>
  <tr>
   <td><p>验证 </p> </td>
   <td><p>以自适应形式映射到验证表达式。</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>单击（按钮字段）</p> </td>
   <td><p>映射到按钮的“单击”表达式。</p> </td>
  </tr>
  <tr>
   <td><p>支持服务器端脚本</p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>支持Web服务</p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。</p> </td>
  </tr>
  <tr>
   <td><p>更改（涂抹字段、单选按钮、复选框）</p> </td>
   <td><p>此脚本在运行时执行，不能以自适应形式覆盖。</p> </td>
  </tr>
 </tbody>
</table>

### 验证{#validations}

下表捕获了XFA验证如何映射到自适应表单中的验证。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA验证</strong></p> </td>
   <td><p><strong>自适应表单中的相应验证</strong></p> </td>
  </tr>
  <tr>
   <td><p>验证模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>验证模式消息(formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>必需(nullTest)</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>空消息(nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>验证脚本(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>验证脚本消息(scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您不能覆盖绑定到XFA复选框的自适应表单单选按钮和复选框组的必需属性。

