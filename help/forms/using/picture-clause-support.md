---
title: HTML5表单的Picture子句支持
seo-title: Picture clause support for HTML5 forms
description: HTML5表单支持XFA Picture子句，用于显示日期、文本和数字符号的值以及格式化的值。
seo-description: HTML5 forms supports XFA Picture clause for display value and formatted value for date, text, and numeric symbols.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# HTML5表单的Picture子句支持 {#picture-clause-support-for-html-forms}

HTML5表单支持XFA Picture子句，用于显示日期、文本和数字符号的值以及格式化的值。 支持以下Picture子句表达式：

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支持Edit Picture子句。 此外，不支持DateTime和Time Picture子句符号。

## 支持的日期字段符号 {#supported-date-field-symbols}

Date Picture子句支持的表达式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture子句符号}

>[!NOTE]
>
>picture子句的默认模式为{MMM D， YYYY}模式。 如果未应用任何阵列，则使用缺省阵列。

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th>解释</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月的1或2位数(1-31)日</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月补零两位数(01-31)的天数。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>一年中的1或2位数(1-12)月份。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>月份中填充零的两位数(01-12)。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>当前区域设置的缩写月份名称<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>当前区域设置的完整月份名称<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>当前区域设置的缩写工作日名称<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>当前区域设置的完整工作日名称<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>2位数年份，其中00 = 2000,29 = 2029,30 = 1930,99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位数年份<br /> </td>
  </tr>
 </tbody>
</table>

## Numeric Picture子句 {#numeric-picture-clause}

HTML5表单支持数字图片符号。 但是，PDF forms和HTMLForms之间的支持存在差异。

In **PDF forms**，数字的格式与Picture子句中的符号数无关

In **HTMLForms**，仅当数字的位数小于Picture子句中的符号数时，才会对数字进行格式化。

**示例**：考虑一个Picture子句： num{zzz，zzz，zz9}。

数字 **10000** 格式为 **10,000** 在HTML和PDF forms中。

数字1000000PDF forms格式为1,000,000。 但是，在HTMLForms中，数字保持为1000000格式。

中支持的Numeric Picture子句表达式 **HTMLForms** 为：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture子句符号}

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th><strong>解释</strong></th>
   <th>输入解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>输出格式</strong>：一位数字。 或者，如果输入数据为空或相应位置有空格，则为零位数。<br /> </td>
   <td>一位数</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>输出格式</strong>：一位数字。 或者，如果输入数据为空，则为空格，或者为相应位置中的零位数。<br /> </td>
   <td>一位数或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>输出格式</strong>：一位数字。 或者，如果输入数据为空、有空格或对应位置中的零位数，则无意义。<br /> </td>
   <td>一位数或无</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>输出格式</strong>：由指数符号(E)组成的浮点数的指数部分。 后跟一个可选的加号或减号。 后跟指数值。<br /> </td>
   <td>与输出格式设置相同</td>
  </tr>
  <tr>
   <td>Cr或cr<br /> </td>
   <td>如果数字为负，则为贷方符号(CR)。 否则什么也没有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>输出格式：数字为负数时为负号。 其他空间。<br /> </td>
   <td>如果数字为负数，则使用负号。 如果数字为正数，则使用加号</td>
  </tr>
  <tr>
   <td>V</td>
   <td>常用区域设置的十进制基数。 允许在输入解析时隐含十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>常用区域设置的十进制基数。 允许在输入解析和输出格式设置时隐含十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>常用区域设置的十进制基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>， (U+FF0C)</td>
   <td>主要区域设置的分组分隔符</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>当前区域设置的货币符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>常用区域设置的百分比符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>数字为负数时用左括号。 其他空间。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>数字为负数时用右括号。 其他空间。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>制表符</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## 文本图片子句 {#text-picture-clause}

HTML5表单支持以下Text Picture子句表达式：

* text{text Picture子句符号}

| **符号** | **解释** |
|---|---|
| A | 单个字母字符。 |
| X | 单个字符。 |
| O | 单个字母数字字符。 |
| 0（零） | 单个字母数字字符。 |
| 9 | 一位数字。 |
