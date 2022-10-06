---
title: 对HTML5表单的图片子句支持
seo-title: Picture clause support for HTML5 forms
description: HTML5表单支持XFA Picture子句用于显示值，以及日期、文本和数字符号的格式化值。
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

# 对HTML5表单的图片子句支持 {#picture-clause-support-for-html-forms}

HTML5表单支持XFA Picture子句用于显示值，以及日期、文本和数字符号的格式化值。 支持以下Picture子句表达式：

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支持编辑图片子句。 此外，不支持DateTime和Time Picture子句符号。

## 支持的日期字段符号 {#supported-date-field-symbols}

支持的Date Picture子句表达式：

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause符号}

>[!NOTE]
>
>图片子句的默认模式为{MMM D， YYYY}模式。 如果未应用模式，则使用默认模式。

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th>解释</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月的1位或2位(1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月的零位(01-31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1 — 或2位(1-12)的月份。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>一年中的零位(01-12)。<br /> </td>
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

## 数值图片子句 {#numeric-picture-clause}

HTML5表单支持数字图片符号。 但是，PDF forms和HTMLForms在支持方面存在差异。

在 **PDF forms**，则不管Picture子句中符号的数量如何，都会设置数字的格式

在 **HTMLForms**，则仅当数字的位数小于Picture子句中符号数时，才会设置数字的格式。

**示例**:请考虑一个图片条款：num{zzz，zzz，zz9}。

数字 **10000** 格式为 **一万** HTML和PDF forms。

编号1000000的格式为1,000,000PDF forms。 但是，在HTMLForms中，数字仍未格式化为1000000。

支持中数值图片子句的表达式 **HTMLForms** 为：

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th><strong>解释</strong></th>
   <th>输入解析</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>输出格式</strong>:一个数字。 或者，如果输入数据为空或对应位置有空格，则为零位。<br /> </td>
   <td>一位数</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>输出格式</strong>:一个数字。 或者，如果输入数据为空，则在相应位置输入空格或零位。<br /> </td>
   <td>单位数或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>输出格式</strong>:一个数字。 或者，如果输入数据为空、空格或相应位置的零位，则不会有任何用处。<br /> </td>
   <td>一位数或零</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>输出格式</strong>:由指数符号(E)组成的浮点数的指数部分。 后跟可选的加号或减号。 后跟指数值。<br /> </td>
   <td>与输出格式相同</td>
  </tr>
  <tr>
   <td>CR或CR<br /> </td>
   <td>如果数字为负，则计数符号(CR)。 否则就没有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>输出格式：如果数字为负数，则显示减号。 其他空间。<br /> </td>
   <td>如果数字为负数，则减号。 数字为正数时加号</td>
  </tr>
  <tr>
   <td>V</td>
   <td>当前区域设置的小数基数。 允许在输入解析时隐含小数基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>当前区域设置的小数基数。 允许在输入解析和输出格式时隐含小数基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>当前区域设置的小数基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>,(U+FF0C)</td>
   <td>当前区域设置的分组分隔符</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$(U+FF04)</td>
   <td>当前区域设置的货币符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>%(U+FF05)</td>
   <td>当前区域设置的百分比符号。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>(U+FF08)</td>
   <td>如果数字为负数，则使用左括号。 其他空间。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>如果数字为负数，则右括号。 其他空间。</td>
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

HTML5表单支持以下文本图片子句表达式：

* text{text picture子句符号}

| **符号** | **解释** |
|---|---|
| A | 单个字母字符。 |
| X | 单个字符。 |
| O | 单个字母数字字符。 |
| 0（零） | 单个字母数字字符。 |
| 9 | 一位数。 |
