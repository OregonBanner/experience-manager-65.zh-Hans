---
title: HTML5表单支持图片子句
seo-title: HTML5表单支持图片子句
description: HTML5表单支持XFA Picture子句用于显示值，以及日期、文本和数字符号的格式化值。
seo-description: HTML5表单支持XFA Picture子句用于显示值，以及日期、文本和数字符号的格式化值。
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: 移动设备表单
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---

# HTML5表单{#picture-clause-support-for-html-forms}的图片子句支持

HTML5表单支持XFA Picture子句用于显示值，以及日期、文本和数字符号的格式化值。 支持以下Picture子句表达式：

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobiles Forms不支持编辑图片子句。 此外，不支持DateTime和Time Picture子句符号。

## 支持的日期字段符号{#supported-date-field-symbols}

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
   <td>每月的零填充两位数(01-31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>1 — 或2位数(1-12)的月份。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>每年的零填充两位数(01-12)。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>当前区域设置的缩写月份名称<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>当前区域设置的完整月名<br /> </td>
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
   <td>2位年份，其中00 = 2000,29 = 2029,30 = 1930,99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位数年份<br /> </td>
  </tr>
 </tbody>
</table>

## 数字图片子句{#numeric-picture-clause}

HTML5表单支持数字图片符号。 但是，PDF forms和HTML Forms在支持方面存在差异。

在&#x200B;**PDF forms**&#x200B;中，不管Picture子句中符号的数量如何，都会格式化数字

在&#x200B;**HTML Forms**&#x200B;中，仅当数字的位数小于Picture子句中符号数时，才会设置数字的格式。

**示例**:请考虑一个图片条款：num{zzz，zzz，zz9}。

数字&#x200B;**10000**&#x200B;在HTML和PDF forms中均格式为&#x200B;**10,000**。

编号1000000的格式为1,000,000PDF forms。 但是，在HTML Forms中，数字的格式仍为1000000。

**HTML Forms**&#x200B;中支持的数值图片子句表达式为：

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
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空或对应位置有空格，则为零位。<br /> </td>
   <td>一位数</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空，则在相应位置输入空格或零位。<br /> </td>
   <td>单位数或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空、空格或相应位置的零位，则不使用任何内容。<br /> </td>
   <td>一位数或零</td>
  </tr>
  <tr>
   <td>错误</td>
   <td><strong>输出格式</strong>:由指数符号(E)组成的浮点数的指数部分。后跟可选的加号或减号。 后跟指数值。<br /> </td>
   <td>与输出格式相同</td>
  </tr>
  <tr>
   <td>CR或cr<br /> </td>
   <td>如果数字为负，则计数符号(CR)。 否则就没有。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>输出格式：如果数字为负数，则显示减号。 其他空格。<br /> </td>
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
   <td>.</td>
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

## 文本图片子句{#text-picture-clause}

HTML5表单支持以下文本图片子句表达式：

* text{text picture子句符号}

| **符号** | **解释** |
|---|---|
| A | 单个字母字符。 |
| X | 单个字符。 |
| O | 单个字母数字字符。 |
| 0（零） | 单个字母数字字符。 |
| 9 | 一位数。 |
