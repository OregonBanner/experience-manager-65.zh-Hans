---
title: 使用XML模式创建自适应表单
seo-title: 使用XML模式创建自适应表单
description: 自适应表单可以使用XML模式作为表单模型，从而使您能够利用现有的XSD模板创建自适应表单。 可以将模式元素从XSD拖放到自适应表单上。
seo-description: 自适应表单可以使用XML模式作为表单模型，从而使您能够利用现有的XSD模板创建自适应表单。 可以将模式元素从XSD拖放到自适应表单上。
uuid: 84c35728-1b6c-4286-854b-51c03bfd0eac
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d6c12b3-3a70-48e9-a83b-974360a8b0b6
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 5%

---


# 使用XML模式{#creating-adaptive-forms-using-xml-schema}创建自适应表单

## 前提条件 {#prerequisites}

使用XML模式作为表单模型创作自适应表单需要对XML模式有基本的了解。 此外，还建议在本文之前阅读以下内容。

* [创建自适应表单](../../forms/using/creating-adaptive-form.md)
* [XML 架构](https://www.w3.org/TR/xmlschema-2/)

## 使用XML模式作为表单模型{#using-an-xml-schema-as-form-model}

AEM Forms支持使用现有的XML模式作为表单模型创建自适应表单。 此XML模式表示组织中的后端系统生成或使用数据的结构。

使用XML模式的主要功能有：

* 在自适应表单的创作模式下，XSD的结构在“内容查找器”选项卡中显示为树。 您可以将元素从XSD层次结构拖放到自适应表单。
* 您可以使用符合相关模式的XML预填充表单。
* 提交时，用户输入的数据将作为符合相关模式的XML提交。

XML模式由简单和复杂的元素类型组成。 元素具有向元素添加规则的属性。 当这些元素和属性被拖动到自适应表单上时，它们会自动映射到相应的自适应表单组件。

XML元素与自适应表单组件的映射如下所示：

<table>
 <tbody>
  <tr>
   <th><strong>XML元素或属性 </strong></th>
   <th><strong>自适应表单组件</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>文本框</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>复选框</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>所有类型的数值</li>
    </ul> </td>
   <td>数值框</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>日期选取器</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>下拉列表</td>
  </tr>
  <tr>
   <td>任何复杂类型元素</td>
   <td>面板</td>
  </tr>
 </tbody>
</table>

## 示例XML模式{#sample-xml-schema}

下面是一个XML模式的示例。

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>确保XML模式只有一个根元素。 不支持具有多个根元素的XML模式。

## 使用XML模式{#adding-special-properties-to-fields-using-xml-schema}向字段添加特殊属性

您可以向XML模式元素添加以下属性，以向相关自适应表单的字段添加特殊属性。

<table>
 <tbody>
  <tr>
   <th><strong>模式属性</strong></th>
   <th><strong>以自适应形式使用</strong></th>
   <th><strong>支持 </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>将字段标记为必填<br /> </td>
   <td>属性</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>添加默认值</td>
   <td>元素和属性</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>指定最小发生次数</p> <p>(对于可重复的子表单（复杂类型）</p> </td>
   <td>元素（复杂类型）</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>指定最大值</p> <p>(对于可重复的子表单（复杂类型）</p> </td>
   <td>元素（复杂类型）</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>将模式元素拖动到自适应表单时，将通过以下方式生成默认标题：
>
>* 大写元素名称的第一个字符
>* 在大小写混合边界处插入空白。

>
>
例如，如果添加`userFirstName`模式元素，则自适应表单中生成的描述为`User First Name`。

## 限制自适应表单组件{#limit-acceptable-values-for-an-adaptive-form-component}的可接受值

可以向XML模式元素添加以下限制以限制自适应表单组件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 模式属性</strong></p> </td>
   <td><p><strong>数据类型</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>组件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大数字数。 指定的位数必须大于零。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定数值和日期的上界。 默认情况下，包含最大值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器<br /> </li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定数值和日期的下限。 默认情况下，会包括最小值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布尔型</p> </td>
   <td><p>如果为true，则表单组件中指定的数字值或日期必须小于为maximum属性指定的数字值或日期。</p> <p>如果为false，则表单组件中指定的数字值或日期必须小于或等于为maximum属性指定的数字值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布尔型</p> </td>
   <td><p>如果为true，则表单组件中指定的数字值或日期必须大于为最小属性指定的数字值或日期。</p> <p>如果为false，则表单组件中指定的数字值或日期必须大于或等于为最小属性指定的数字值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最少字符数。 最小长度必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大字符数。 最大长度必须大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的字符数。 长度必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定组件中允许的最大小数位数。 fractionDigits必须等于或大于零。</p> </td>
   <td>
    <ul>
     <li> 数据类型为浮点或小数的数字框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定字符的顺序。 如果字符符合指定的模式，则组件接受这些字符。</p> <p>模式属性映射到相应自适应表单组件的验证模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD模式的所有自适应表单组件 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 常见问题 {#frequently-asked-questions}

**如何知道树中的哪个元素与哪个XML元素关联？**

在内容查找器中多次单击某个元素时，将显示一个字段名称和一个名为`bindRef`的属性。 此属性将树元素映射到模式中的元素或属性。

![XML模式元素的二进制字段](assets/dblclick.png)

bindRef</code>字段显示树元素与模式中元素或属性之间的关联。

>[!NOTE]
>
>属性的`bindRef`值中有一个`@`符号，以区分它们与元素。 例如，`/config/projectDetails/@duration`。

**为什么我无法拖动子表单的单个元素（从任何复杂类型生成的结构）以用于可重复的子表单（minOccours或maxOccurs值大于1）?**

在可重复的子表单中，必须使用完整的子表单。 如果只想选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个很长的复杂结构。如何找到特定元素？**

您有两种选择：

* 滚动浏览树结构
* 使用“搜索”框查找元素

**什么是bindRef?**

`bindRef`是自适应表单组件与模式元素或属性之间的连接。 它指定`XPath`，从此组件或字段捕获的值在输出XML中可用。 从预填充（预填充）XML预填充字段值时，也使用`bindRef`。
