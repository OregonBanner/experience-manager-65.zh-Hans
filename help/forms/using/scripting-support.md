---
title: HTML5表单的脚本支持
seo-title: HTML5表单的脚本支持
description: HTML5 Forms支持的JavaScript、FormCalc属性和其他方法。
seo-description: HTML5 Forms支持的JavaScript、FormCalc属性和其他方法。
uuid: 697d5ec4-c818-41e4-b813-883c01b7ff3a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4ef78c8c-783f-4aac-a499-692cd4acef75
feature: 移动设备表单
exl-id: bcb5afc5-2190-4269-aba2-63842db9df3f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3911'
ht-degree: 6%

---

# 对HTML5表单{#scripting-support-for-html-forms}的脚本支持

HTML5表单中支持的JavaScript、FormCalc属性和方法如下所示：

## $event {#event}

<table>
 <tbody>
  <tr>
   <th>属性 </th>
   <th>描述<br /> </th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>prevText</code></td>
   <td>指定字段内容，然后字段根据用户的操作进行更改。 此值与撤消功能类似，可以回调。</td>
   <td><p>不适用于下拉框和列表框。 <code>PrevText </code>无法在以下情况下正常工作：</p>
    <ul>
     <li>在iPad的“数字”字段中键入一些特殊字符键(例如$、(、)、&amp;、@等)，以及 </li>
     <li>对于“日期”字段（通过日历输入日期时）。<br /> </li>
    </ul> <p>不支持通过脚本设置值。</p> </td>
  </tr>
  <tr>
   <td><code>target</code></td>
   <td>指定事件在其上执行操作的对象。</td>
   <td>不支持通过脚本设置值。<br /> </td>
  </tr>
  <tr>
   <td><code>newtext</code></td>
   <td>指定字段在响应用户操作而发生更改后的内容。</td>
   <td><p><code>newText</code>属性在以下情况下无法正常工作：</p>
    <ul>
     <li>论文本的选替</li>
     <li>删除、复制和粘贴文本时。</li>
     <li>在数字字段<br />中键入一些特殊字符键(例如$、(、)、&amp;、@等) </li>
     <li>使用shift+字母数字组合。 </li>
     <li>使用日期/时间字段时。</li>
    </ul>
    <div>
      不支持通过脚本设置值。
    </div> </td>
  </tr>
  <tr>
   <td>更改</td>
   <td>指定用户在执行操作后立即键入或粘贴到字段中的值。 </td>
   <td><p>对于以下情况，更改属性无法正常工作：</p>
    <ul>
     <li>论文本的选替</li>
     <li>删除、复制和粘贴文本时。</li>
     <li>在数字字段<br />中键入一些特殊字符键(例如$、(、)、&amp;、@等) </li>
     <li>使用shift+字母数字组合。 </li>
     <li>使用日期/时间字段时。</li>
    </ul> <p>不支持通过脚本设置值。</p> </td>
  </tr>
  <tr>
   <td>关键</td>
   <td>确定用户是否按箭头键进行选择。 此属性仅适用于列表框和下拉列表。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>修饰符</td>
   <td>确定在执行特定事件时是否按住修饰符键(例如，Microsoft® Windows®上的Ctrl)。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### $host {#host}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td><code>apptype</code></td>
   <td>返回主机的应用程序类型。 仅适用于客户端应用程序。</td>
   <td>返回<code>HTML 5</code>。</td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>返回当前应用程序的名称。</td>
   <td>返回浏览器名称及其版本。 例如，在Chrome浏览器中，返回的值为 <code>Chrome &lt;version&gt;.</code></td>
  </tr>
  <tr>
   <td><code>numPages</code></td>
   <td>返回文档中的页数。</td>
   <td>HTML5表单的分页策略与PDF forms分页策略不相同。 因此，numPages API在这两种情况下都可以返回不同的值。</td>
  </tr>
  <tr>
   <td><code>platform</code></td>
   <td>返回表示运行脚本的计算机平台的字符串。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>title</code></td>
   <td>指定文档的标题。 它仅适用于客户端应用程序。</td>
   <td>它会以表单形式返回HTML文档的标题，而不是像PDF forms一样返回表单元数据标题。</td>
  </tr>
  <tr>
   <td><code>version</code></td>
   <td>返回表示当前应用程序版本号的字符串。</td>
   <td>它会返回表单的版本。</td>
  </tr>
  <tr>
   <td><code>calculationsEnabled</code></td>
   <td>指定是否执行计算脚本。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>validationsEnabled</code></td>
   <td>指定是否执行验证脚本。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>pageUp</code></td>
   <td>转到上一页。</td>
   <td>HTML5表单与PDF表单的分页策略不同，因此HTML5表单的上一页与PDF表单的上一页不同。</td>
  </tr>
  <tr>
   <td><code>pageDown</code></td>
   <td>移动到表单的下一页。 在运行时使用pageDown方法。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>setFocus</code></td>
   <td>将键盘焦点设置到指定的字段。 该字段被指定为对象，或由该字段的SOM表达式指定。 它仅适用于客户端应用程序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>resetdata</code></td>
   <td>将文档中的字段重置为其默认值。</td>
   <td>清除表单中包含合并数据的所有数据，而不是将其恢复为默认值。</td>
  </tr>
  <tr>
   <td><code>messageBox</code></td>
   <td>在屏幕上显示一个对话框。 它仅适用于客户端应用程序</td>
   <td>类型为“是/否”的消息框将转换为“确定/取消”。 不支持包含三个按钮的消息框。</td>
  </tr>
  <tr>
   <td>currentPage</td>
   <td><p>在运行时设置文档的当前活动页面。</p> <p>页面值以0为基础，因此文档的第一页返回值0。</p> <p>当layout:ready在客户端上执行时，当前页面属性可用。 但是，当layout:ready在服务器上执行时，它不可用，因为直到表单布局执行后才会执行属性。</p> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 字段 {#field}

<table>
 <tbody>
  <tr>
   <th><strong><span>属性</span></strong></th>
   <th><strong><span>描述<br /> </span></strong></th>
   <th><strong><span>例外</span></strong></th>
  </tr>
  <tr>
   <td><code>presence</code></td>
   <td>控制关联对象在不同处理阶段的参与率。 如果对象是容器，则容器的内容将继承此控件所适用的任何限制。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>access</code></td>
   <td>控制用户对内容的访问。</td>
   <td>不适用于排除组。 此外，HTML5表单对非交互式和受保护对象也给予相同的处理。<br /> </td>
  </tr>
  <tr>
   <td><code>name</code></td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>HTML5表单不允许设置对象的name属性。 它是HTML5表单的只读属性。</td>
  </tr>
  <tr>
   <td><code>value</code></td>
   <td>包含单个数据内容单位的内容元素。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>rawValue</code></td>
   <td>指定此字段的未格式化值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>formattedValue</code></td>
   <td>指定此字段的格式化值。</td>
   <td>不支持通过脚本设置<code>formattedValue</code>。</td>
  </tr>
  <tr>
   <td><code>editValue</code></td>
   <td>指定此字段的编辑值。</td>
   <td>不支持设置<code>editValue </code>到脚本。</td>
  </tr>
  <tr>
   <td><code>formatMessage</code></td>
   <td>指定此字段的格式验证消息字符串。</td>
   <td>不支持设置<code>formatMessage </code>到脚本。</td>
  </tr>
  <tr>
   <td><code>fillcolor</code></td>
   <td>指定此字段的背景颜色值。 您需要将border.fill.presence属性设置为单独可见。</td>
   <td>它无法正确返回字段的默认颜色。</td>
  </tr>
  <tr>
   <td><code>border</code></td>
   <td>边框对象描述对象周围的边框。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>ui</code></td>
   <td>用户界面对象封装了表单对象的用户界面描述。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>mandatory</code></td>
   <td>为字段指定nullTest值。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>borderColor</code></td>
   <td>指定此字段的边框颜色值。 您需要将border.edge.presence属性设置为单独可见。</td>
   <td>无法正确返回字段的默认边框颜色。</td>
  </tr>
  <tr>
   <td><code>length</code></td>
   <td>列表中的项目数。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>addItem</code></td>
   <td>将新项目添加到当前字段。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>clearItem</code></td>
   <td>从字段中删除所有项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>boundItem</code></td>
   <td>获取下拉列表或列表框的特定显示项的绑定值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execCalculate</code></td>
   <td>执行字段的计算脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execValidate</code></td>
   <td>执行字段的验证脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>execEvent</code></td>
   <td>执行对象的事件脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getItemState</code></td>
   <td>返回指定项的选择状态</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItemState</code></td>
   <td>设置指定项目的选择状态。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getDisplayItem</code></td>
   <td>检索指定项目索引的项目显示文本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>getSaveItem</code></td>
   <td>检索指定项目索引的数据值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>deleteItem</code></td>
   <td>删除指定索引处的项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td><code>setItems</code></td>
   <td>设置当前字段中的指定项目。 它会替换预先存在的项目。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>caption</td>
   <td>标题对象描述与表单设计对象关联的描述性标签。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供数据的验证。 验证对象可在表单生命周期中多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>parentSubform</td>
   <td>指定此字段的父子表单（页面）。</td>
   <td>始终返回父子表单，而不是返回第一个非范围划分的父子表单。<br /> </td>
  </tr>
  <tr>
   <td>selectedIndex</td>
   <td>第一个选定项的索引。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 表单 {#form}

| **属性** | **描述** | **例外** |
|---|---|---|
| formNodes | 返回绑定到指定数据对象的所有表单模型对象的列表。 |  |

## InstanceManager {#instancemanager}

| 属性 | 描述 |
|---|---|
| `name` | 用于在脚本表达式中标识此元素的标识符。 |
| `occur` | 描述对其封闭容器允许的实例数的限制。 |
| `min` | 指定可实例化的最小实例数。 |
| `max` | 指定可实例化的最大实例数。 |
| `count` | 指定实例化的当前实例数。 |
| `setInstances` | 从此节点添加或删除指定的子表单或子表单集。 |
| `addInstance` | 向此节点添加子表单或子表单集的新实例。 |
| `removeInstance` | 从此节点中删除子表单或子表单集。 |
| `moveInstance` | 将表单模型对象的子对象移动到表单模型内的其他指定位置。 对象的相应数据模型信息也在数据模型内被重新定位。 |
| `insertInstance` | 向此节点插入子表单或子表单集的新实例。 |

## 列表 {#list}

| 属性 | 描述 |
|---|---|
| `length` | 列表中的元素数。 |
| `item` | 集合中从零开始的索引。 |
| `append` | 将节点附加到节点列表的末尾。 |
| `remove` | 从节点列表中删除节点。 |
| `insert` | 在节点列表中的特定节点之前插入节点。 |

## 节点 {#node}

| 属性 | 描述 | 例外 |
|---|---|---|
| createNode | 根据有效的类名称创建新节点。 | 无 |
| `isContainer` | 指定此对象是否为容器对象。 | 无 |
| `isNull` | 指示当前数据值是否为空值。 | 无 |
| `resolveNode` | 从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定对象的值。 | 无 |
| `resolveNodes` | 从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定对象的值。 | 无 |
| oneOfChild | 根据有效的类名称创建新节点。 | 无 |
| getElement | 返回指定的子对象。 | 无 |
| getAttribute | 获取指定的属性值。 | 无 |
| setAttribute | 设置指定属性的值。 | 无 |

## 模型 {#model}

| 属性 | 描述 | 例外 |
|---|---|---|
| NA | NA | NA |

## 子表单 {#subform}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>instanceIndex</td>
   <td>指定对象相对于其他实例化实例的索引。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execEvent</td>
   <td>执行对象的事件脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>getInvalidObjects</td>
   <td>返回子表单（包括）中包含的未通过验证测试的节点列表。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述对象周围的边框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此字段的边框颜色值。 您需要将border.edge.presence属性设置为单独可见。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供数据的验证。 验证对象可在表单生命周期中多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>name</td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>访问</td>
   <td>控制用户对容器对象（如子表单）内容的访问。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execValidate</td>
   <td>根据子表单或子表单集相对于同一表单对象的其他实例的位置计算其索引。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>instanceManager</td>
   <td>instanceManager对象管理表单模型对象的实例创建、删除和移动。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

### 提交 {#submit}

| 属性 | 描述 |
|---|---|
| 目标 | 数据提交到的URL。 此属性的遗漏意味着XFA处理应用程序使用产品特定技术（如访问配置对象中的产品特定信息）来获取URI。 |

## 树 {#tree}

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>描述</th>
   <th>例外</th>
  </tr>
  <tr>
   <td>节点</td>
   <td>返回当前对象的所有子对象的列表。</td>
   <td>
    <ul>
     <li>xfa.nodes、desc不支持</li>
     <li>针对PDF和HTML报告的节点数不同。 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定此节点的名称。</td>
   <td>HTML中不允许使用脚本设置名称。</td>
  </tr>
  <tr>
   <td>parent</td>
   <td>获取此节点的父项。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>索引</td>
   <td>返回此节点在其相似名称、范围内、相似子关系节点集合中的位置。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>somExpression</td>
   <td>获取此节点的SOM表达式。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNode</td>
   <td>从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定对象的值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>resolveNodes</td>
   <td>从当前XML表单对象模型对象开始计算指定的SOM表达式，并返回在SOM表达式中指定对象的值。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 子格式集 {#subformset}

| 属性 | 描述 | 例外 |
|---|---|---|
| instanceManager | instanceManager对象管理表单模型对象的实例创建、移除和移动。 | 无 |

## content {#content}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指示当前数据值是否为null值。 |  |

## dataValue {#datavalue}

| **属性** | **描述** | **例外** |
|---|---|---|
| isNull | 指示当前数据值是否为null值。 |  |

## 边缘 {#edge}

<table>
 <tbody>
  <tr>
   <td><strong>属性 </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述阵列对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 填充 {#fill}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性定义填充的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 线性 {#linear}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性描述表单上线性渐变填充的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 折线图 {#line}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边缘对象描述边框或矩形的弧、线或一侧。<br /> </td>
   <td>不支持颜色、帽子等属性。<br /> </td>
  </tr>
 </tbody>
</table>

## 图案 {#pattern}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述阵列对象的唯一颜色。 </td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 径向 {#radial}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>颜色属性描述径向对象的唯一颜色</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 拼点 {#stipple}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述拼合对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 绘制 {#draw}

<table>
 <tbody>
  <tr>
   <td>属性</td>
   <td>描述</td>
   <td>例外</td>
  </tr>
  <tr>
   <td>ui</td>
   <td>ui对象封装了表单对象的用户界面描述。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>字幕</td>
   <td>标题对象描述与表单设计对象关联的描述性标签。</td>
   <td> </td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定可用于在脚本表达式中指定此对象或事件的标识符。</td>
   <td>不支持在运行时设置值</td>
  </tr>
  <tr>
   <td>选定</td>
   <td>值对象封装了单个数据内容单位。<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 角 {#corner}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>颜色</td>
   <td>color属性描述角对象的唯一颜色。</td>
   <td>
    <ul>
     <li>无法检索默认值。 </li>
     <li>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改不会反映在UI中。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## checkButton {#checkbutton}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述checkButton对象周围的边框。 </td>
   <td>这些更改将反映在模型中，可用于编写脚本，但不会与HTML元素同步。 因此，这些更改未反映在UI中。<br /> </td>
  </tr>
 </tbody>
</table>

## choiceList {#choicelist}

<table>
 <tbody>
  <tr>
   <td><strong>属性<br /> </strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述choiceList对象周围的边框。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## dateTimeEdit {#datetimeedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述dateTimeEdit对象周围的边框。 |  |

## 图像 {#image}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>contentType</td>
   <td>指定引用文档中的内容类型，以MIME类型表示。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>name<br /> </td>
   <td>用于在脚本表达式中标识此元素的标识符。</td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## imageEdit {#imageedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述imageEdit对象周围的边框。 |  |

## numericEdit {#numericedit}

| **属性** | **描述** | **例外** |
|---|---|---|
| 边框 | 边框对象描述对象周围的边框。 | 无 |

## 对象 {#object}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>className</td>
   <td>确定此对象的类的名称。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 矩形 {#rectangle}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边缘对象描述边框或矩形的弧、线或一侧。<br /> </td>
   <td>不支持颜色、大写等属性。</td>
  </tr>
 </tbody>
</table>

## textEdit {#textedit}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>边框</td>
   <td>边框对象描述对象周围的边框。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## exclGroup {#exclgroup}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>布局</td>
   <td>指定要由此对象使用的布局策略。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>边框</td>
   <td>指定此字段周围的边框。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>mandatory</td>
   <td>为字段指定nullTest值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderColor</td>
   <td>指定此字段的边框颜色值。必须先定义边框，然后才能通过脚本更改颜色。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>borderWidth</td>
   <td>指定此字段的边框宽度。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>h</td>
   <td>布局的高度测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>瞬态</td>
   <td>指定处理应用程序是否必须在表单提交或保存操作中保存排除组的值。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>w</td>
   <td>指定布局宽度的测量。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>x</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的x坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>y</td>
   <td>使用定位布局放置时，指定容器锚点相对于父容器左上角的y坐标。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>字幕</td>
   <td>标题对象描述与表单设计对象关联的描述性标签。<br /> </td>
   <td>无</td>
  </tr>
  <tr>
   <td>验证</td>
   <td>验证对象控制表单上用户提供数据的验证。 验证对象可在表单生命周期中多次激活。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>dataNode</td>
   <td>获取在合并后表单节点绑定到的数据节点。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>存在</td>
   <td>指定对象的可见性。</td>
   <td> </td>
  </tr>
  <tr>
   <td>访问</td>
   <td>控制用户对容器对象（如子表单）内容的访问。</td>
   <td>对于排除组中的单个项目，始终会返回打开状态。 </td>
  </tr>
  <tr>
   <td>name</td>
   <td>指定可用于在脚本表达式中指定此对象或事件的标识符。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>成员</td>
   <td>指定排除组的成员。 </td>
   <td>无</td>
  </tr>
  <tr>
   <td>selectedMember</td>
   <td>返回排除组的选定成员。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>execCalculate</td>
   <td>对指定对象的计算事件和任何子对象执行任何脚本。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>计算</td>
   <td>计算对象控制字段值的计算。<br /> </td>
   <td>无</td>
  </tr>
 </tbody>
</table>

## 弧 {#arc}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边缘对象描述边框或矩形的弧、线或一侧。<br /> </td>
   <td>不支持颜色、大写等属性。 </td>
  </tr>
 </tbody>
</table>

## 边框 {#border}

<table>
 <tbody>
  <tr>
   <td><strong>属性<strong></strong></strong></td>
   <td><strong>描述<strong></strong></strong></td>
   <td><strong>例外<strong></strong></strong></td>
  </tr>
  <tr>
   <td>边缘</td>
   <td>边缘对象描述边框或矩形的弧、线或一侧。<br /> </td>
   <td>不支持颜色、大写等属性。 </td>
  </tr>
 </tbody>
</table>

## $布局 {#layout}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>例外</strong></td>
  </tr>
  <tr>
   <td>h</td>
   <td>确定给定表单设计对象的高度。<br /> </td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持高度(h)属性。 </li>
     <li>不支持参数“XFA-Form对象发生在的第一个内容区域的偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>w</td>
   <td>确定给定表单设计对象的宽度。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持宽度(w)属性。 </li>
     <li>不支持参数“XFA-Form对象发生在的第一个内容区域的偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>x</td>
   <td>确定给定表单设计对象相对于其父对象的x坐标。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持x坐标(x)属性。 </li>
     <li>不支持参数“XFA-Form对象发生在的第一个内容区域的偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>y</td>
   <td>确定给定表单设计对象相对于其父对象的y坐标。</td>
   <td>
    <ul>
     <li>页面区域和内容区域不支持y坐标(y)属性。 </li>
     <li>不支持参数“XFA-Form对象发生在的第一个内容区域的偏移”。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>pagecount</td>
   <td>确定当前表单的页数。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法会为PDF和HTML表单返回不同的值。</li>
     <li>通过隐藏对象来减少页面计数时，abspagecount方法会返回错误值。<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>页面内容</td>
   <td>从表单的指定页面中检索表单设计对象的类型。</td>
   <td>无</td>
  </tr>
  <tr>
   <td>absPageCount</td>
   <td>确定当前表单的页面计数。</td>
   <td>
    <ul>
     <li>layout.pageCount()方法会为PDF和HTML表单返回不同的值。</li>
     <li>通过隐藏对象来减少页面计数时，abspagecount方法会返回错误值。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 项目 {#items}

| **属性** | **描述** | **例外** |
|---|---|---|
| 存在 | 指定对象的可见性。 | 无 |

## FormCalc {#formcalc}

FormCalc是一种特定于XFA的语言，用于创建以电子表单为中心的逻辑和计算根。 FormCalculation提供了一组功能强大的构建函数。

### FormCalc支持的函数{#formcalc-supported-functions}

### 表单计算表达式支持{#formcalc-expression-support}

<table>
 <tbody>
  <tr>
   <td><strong>类别 </strong></td>
   <td><strong>描述 </strong></td>
   <td><strong>示例 </strong></td>
  </tr>
  <tr>
   <td>简单表达式</td>
   <td>加、减、乘、除和圆括号</td>
   <td>(a+b)*3</td>
  </tr>
  <tr>
   <td>变量声明</td>
   <td>定义变量</td>
   <td>var a<br /> var a=3<br /> a=3</td>
  </tr>
  <tr>
   <td>逻辑表达式</td>
   <td>
    <ul>
     <li>逻辑（和/或）</li>
     <li>比较（大/小/等）</li>
    </ul> </td>
   <td>A或1<br /> 1 &lt;&gt; 2<br /> A NE B<br /> A或1<br /> 1 &lt;&gt; 2<br /> A NE B</td>
  </tr>
  <tr>
   <td>如果表达式</td>
   <td><br type="_moz" /> </td>
   <td>如果(a&gt;b)，则为2 endif</td>
  </tr>
  <tr>
   <td>while</td>
   <td><br type="_moz" /> </td>
   <td>而(ilt 5)do i = i + 1 endwile</td>
  </tr>
  <tr>
   <td>对象</td>
   <td><br type="_moz" /> </td>
   <td>对于i = 100，向下到1 <br />, do s = s + i结束</td>
  </tr>
  <tr>
   <td>每个</td>
   <td><br type="_moz" /> </td>
   <td>对于(1、2、3)<br />中的每个i， s = s + i结尾</td>
  </tr>
  <tr>
   <td>函数声明</td>
   <td>在FormCalc中定义自定义函数</td>
   <td>func foo(n)do var f = nendfunc</td>
  </tr>
 </tbody>
</table>

### Acrobat API支持{#acrobat-api-support}

1. **算术函数**

   1. Abs()
   1. Avg()
   1. Ceil()
   1. 计数()
   1. Floor()
   1. 最大()
   1. 最小()
   1. Mod()
   1. Round()
   1. 总计()

1. **科学功能**

   1. Acos()
   1. Asin()
   1. Atan()
   1. Atan2()
   1. Cos()
   1. Sin()
   1. 谭()
   1. Exp()
   1. 日志()
   1. Pow()
   1. Sqrt()
   1. Deg2Rad()
   1. Rad2Deg()
   1. Pi()

1. **财务职能**

   1. 四月()
   1. Cterm()
   1. Fv()
   1. Ipmt()
   1. Npv()
   1. Pmt()
   1. Ppmt()
   1. Pv()
   1. Rate()
   1. 术语()

1. **逻辑函数**

   1. Choose()
   1. If()
   1. Oneof()
   1. Within()

1. **字符串函数**

   1. 于()
   1. Concat()
   1. 左()
   1. Len()
   1. Lower()
   1. Ltrim()
   1. 替换()
   1. 右()
   1. Rtrim()
   1. 空间()
   1. Stuff()
   1. Substr()
   1. Upper()
   1. WordNum()

1. **日期和时间**

   1. 日期()
   1. num2date()
   1. DateFmt()

<table>
 <tbody>
  <tr>
   <td><strong>API</strong></td>
   <td><strong>描述</strong></td>
   <td><strong>象差</strong></td>
  </tr>
  <tr>
   <td>console.println()</td>
   <td>此Acrobat API会将输出转储到JavaScript控制台。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.alert()</td>
   <td>此Acrobat API通过JavaScript弹出窗口发出警报消息。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.beep()</td>
   <td>使系统播放声音。</td>
   <td>不执行任何操作。</td>
  </tr>
  <tr>
   <td>app.execDialog()</td>
   <td>向用户显示一个模式对话框。 必须先由用户关闭模态对话框，然后才能直接再次使用主机应用程序。</td>
   <td>未执行任何操作。<br /> </td>
  </tr>
  <tr>
   <td>app.launchURL()</td>
   <td>在浏览器窗口中启动URL。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setInterval()</td>
   <td>指定JavaScript脚本和时间段。 每经过一段时间，都会执行该脚本。 此方法的返回值必须保留在JavaScript变量中。 否则，间隔对象将被垃圾收集，这将导致时钟停止。 要终止定期执行，请将返回的间隔对象传递到clearInterval。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.setTimeOut()</td>
   <td>指定JavaScript脚本和时间段。 该脚本仅在经过该时段后执行一次。此方法的返回值必须保留在JavaScript变量中。 否则，超时对象将被垃圾收集，这将导致时钟停止。 要取消超时事件，请将返回的超时对象传递给clearTimeOut。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.clearInterval()</td>
   <td>取消由setInterval方法最初设置的先前注册的间隔。</td>
   <td>在HTML5表单中，API无法正确运行。</td>
  </tr>
  <tr>
   <td>app.clearTimeOut()</td>
   <td>取消之前注册的超时间隔。 此类间隔最初由setTimeOut设置。</td>
   <td>在HTML5表单中，API无法正确运行。<br /> </td>
  </tr>
  <tr>
   <td>app.eval()</td>
   <td>运行给定脚本。</td>
   <td> </td>
  </tr>
  <tr>
   <td>app.activeDocs</td>
   <td>包含每个活动文档的Doc对象的数组。 如果没有处于活动状态的文档，则activeDocs不返回任何内容；即，它的行为与核心JavaScript中的d = new Array(0)的行为相同。</td>
   <td>为HTMl5表单返回空数组。</td>
  </tr>
  <tr>
   <td>app.calculate</td>
   <td>如果为true（默认值），则可以执行计算。 如果为false，则不允许计算。</td>
   <td>对于HTMl5 Forms，始终为true。</td>
  </tr>
  <tr>
   <td>app.constants</td>
   <td>用于保存各种常数值的包装器对象。 当前，此属性返回具有单个属性align的对象。</td>
   <td>HTML5表单返回空对齐对象。</td>
  </tr>
  <tr>
   <td>app.focusRect</td>
   <td>打开和关闭焦点矩形。 焦点矩形是按钮、复选框、单选按钮和签名周围的淡淡虚线，用于指示表单字段具有键盘焦点。 值为true会打开焦点矩形。</td>
   <td>对于HTML5表单，始终为true。</td>
  </tr>
  <tr>
   <td>app.formsVersion</td>
   <td>查看器的版本号构成软件。 如果要在脚本中保持向后兼容性，请检查此属性以确定较新版本软件中的对象、属性或方法是否可用。</td>
   <td>始终为11.001。</td>
  </tr>
  <tr>
   <td>app.language</td>
   <td>运行的Acrobat查看器的语言。</td>
   <td>对于HTMl5表单，始终为“简体中文”。</td>
  </tr>
 </tbody>
</table>

## 支持的XFA事件{#supported-xfa-events}

支持以下客户端XFA事件：

* 初始化
* 验证
* 计算
* 单击
* 输入
* 退出
* 更改
* ValidationState

>[!NOTE]
>
>HTML5表单在客户端（浏览器）上呈现。 建议使用客户端&#x200B;**validate**&#x200B;和&#x200B;**calculate**&#x200B;脚本，而不是服务器端脚本。
