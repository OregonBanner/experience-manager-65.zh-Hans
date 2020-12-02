---
title: HTML5表单的图片子句支持
seo-title: HTML5表单的图片子句支持
description: HTML5表单支持XFA Picture子句（用于显示值）和格式化日期、文本和数字符号的值。
seo-description: HTML5表单支持XFA Picture子句（用于显示值）和格式化日期、文本和数字符号的值。
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---


# 支持HTML5表单的Picture子句{#picture-clause-support-for-html-forms}

HTML5表单支持XFA Picture子句（用于显示值）和格式化日期、文本和数字符号的值。 支持以下Picture子句表达式:

* 类别(locale){picture-clause} |类别(locale){picture-clause} |类别(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>目前，Mobile Forms不支持编辑图片子句。 此外，不支持DateTime和Time Picture子句符号。

## 支持的日期字段符号{#supported-date-field-symbols}

支持日期图片子句表达式:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause symbols}

>[!NOTE]
>
>图片子句的默认模式为{MMM D,YYYY}模式。 如果未应用任何图案，则使用默认图案。

<table>
 <tbody>
  <tr>
   <th><strong>符号</strong></th>
   <th>解释</th>
  </tr>
  <tr>
   <td>D</td>
   <td>每月1位或2位(1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>每月的零位填充两位数(01-31)。<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>年度的1-或2位(1-12)月。<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>一年中的零填充两位数(01-12)月。<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>当前区域设置的缩写月份名称<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>当前区域设置的整月名称<br /> </td>
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
   <td>2位数年份，其中00 = 2000, 29 = 2029, 30 = 1930, 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>4位数年份<br /> </td>
  </tr>
 </tbody>
</table>

## 数字图片子句{#numeric-picture-clause}

HTML5表单支持数字图片符号。 但是，PDF forms和HTMLForms在支持方面存在差异。

在&#x200B;**PDF forms**&#x200B;中，不管Picture子句中符号的数量如何，都格式化数字

在&#x200B;**HTMLForms**&#x200B;中，仅当数字的数字小于Picture子句中符号数时，才格式化数字。

**示例**:请考虑Picture子句：num{zzz,zzz,zz9}。

数字&#x200B;**10000**&#x200B;在HTML和PDF forms中均格式化为&#x200B;**10,000**。

数字1000000的格式设置为1,000,000PDF forms。 但是，在HTMLForms中，数字仍未格式化为1000000。

**HTMLForms**&#x200B;中Numeric Picture子句支持的表达式为：

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
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空或相应位置有空格，则为零位。<br /> </td>
   <td>单位数</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空，或者空格，或者对应位置的零位。<br /> </td>
   <td>单位数或空格</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>输出格式</strong>:一个数字。或者，如果输入数据为空、空格或相应位置的零位，则无用处。<br /> </td>
   <td>一位数或无</td>
  </tr>
  <tr>
   <td>错误</td>
   <td><strong>输出格式</strong>:由指数符号(E)组成的浮点数的指数部分。后跟可选的加号或减号。 后跟指数值。<br /> </td>
   <td>与输出格式相同</td>
  </tr>
  <tr>
   <td>CR或CR<br /> </td>
   <td>如果数字为负，则表示信用符号(CR)。 没别的。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S或s<br /> </td>
   <td>输出格式：如果数字为负数，则为减号。 其他空格。<br /> </td>
   <td>如果数字为负，则减号。 数字为正时加号</td>
  </tr>
  <tr>
   <td>V</td>
   <td>当前区域设置的十进制数。 允许在输入解析时隐含小数基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>当前区域设置的十进制数。 允许在输入解析和输出格式设置时隐含小数基数。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>。</td>
   <td>当前区域设置的十进制数。</td>
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
   <td>((U+FF08)</td>
   <td>如果数字为负，则使用左括号。 其他空间。</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>)(U+FF09)</td>
   <td>如果数字为负，则右括号。 其他空间。</td>
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

HTML5表单支持以下文本图片子句表达式:

* text{text Picture子句符号}

| **符号** | **解释** |
|---|---|
| A | 单字母字符。 |
| X | 单个字符。 |
| O | 单个字母数字字符。 |
| 0（零） | 单个字母数字字符。 |
| 9 | 一位数。 |
