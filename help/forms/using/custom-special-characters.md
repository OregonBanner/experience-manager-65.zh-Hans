---
title: 通信管理中的自定义特殊字符
seo-title: 通信管理中的自定义特殊字符
description: 了解如何在“对应管理”中添加自定义特殊字符。
seo-description: 了解如何在“对应管理”中添加自定义特殊字符。
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 通信管理中的自定义特殊字符{#custom-special-characters-in-correspondence-management}

## 概述 {#overview}

Correponsement Management内置了默认支持210个特殊字符，您可以轻松插入这些字符。

例如，可以插入以下特殊字符：

* 货币符号，如€、¥和英镑
* 诸如∑、√、gratab和^等数学符号
* 标点符号‟为和”

可以在字母中插入特殊字符：

* 在文本编 [辑器中](/help/forms/using/document-fragments.md#createtext)
* 在可编 [辑的内联模块中，通信](../../forms/using/create-correspondence.md#managecontent)

![特殊字符线模块](assets/specialcharactersinlinemodule.png)

管理员可以通过自定义添加对更多／自定义特殊字符的支持。 本文提供了有关如何添加对其他自定义特殊字符的支持的说明。

## 在“对应管理”中添加或修改对自定义特殊字符的支持 {#creatingfolderstructure}

使用以下步骤添加对自定义特殊字符的支持：

1. 转到并 `https://'[server]:[port]'/[ContextPath]/crx/de` 以管理员身份登录。
1. 在apps文件夹中，创建一个名为 **[!UICONTROL specialcharacters的文件夹]** ，其路径／结构与specialcharacters文件夹（位于libs下的textEditorConfig文件夹中）类似：

   1. 右键单击以下路 **径中的** “特定字符”文件夹，然后选择“ **叠加节点”**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 确保“叠加节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

      >[!NOTE]
      >
      >请勿在/libs分支中进行更改。 您所做的任何更改都可能会丢失，因为只要您：
      >
      >
      >
      >    * 在实例上升级
      >    * 应用热修复
      >    * 安装功能包


   1. 单击“ **确定** ”，然后单击“ **全部保存”**。 将在指定路径中创建指定字符文件夹。

      创建叠加后，验证节点结构标签。 使用叠加在/apps中创建的每个节点应具有与该节点在/libs中定义的相同类和属性。 如果/apps位置下的节点结构中缺少任何属性或标记，请将其标记与/libs中的相应节点同步。



1. 确保textEditorConfig **[!UICONTROL 节点具有]** 以下属性和值：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | cmConfigurationType | 字符串 | cmTextEditorConfiguration |
   | cssPath | 字符串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 右键单击以下路 **[!UICONTROL 径中的特定字符]** ，然后选择“ **创建”>“子节点”** ，然后单击“全 **部保存”**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 刷新“文本编辑器”\“创建对应UI”页。 您添加的节点是UI中特殊字符列表中的最后一个节点。
1. 单击“ **全部保存**”。
1. 根据需要在特殊字符中进行更改：

<table>
 <tbody>
  <tr>
   <td><strong>收件人...</strong></td>
   <td><strong>完成以下步骤</strong></td>
  </tr>
  <tr>
   <td>添加自定义特殊字符</td>
   <td>
    <ol>
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加子节点（含必需属性）。</li>
     <li>单击“全部保存”</li>
     <li>刷新文本编辑器\创建对应UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新现有特殊字符的属性</td>
   <td>
    <ol>
     <li>叠加要更新的节点（如上所述）并验证标记和类。</li>
     <li>更改任何值，如caption、value、endValue和multipleCaption。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建对应UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏特殊字符</td>
   <td>
    <ol>
     <li>覆盖“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下要隐藏的节点</li>
     <li>将sling:hideResource(Boolean)属性添加到要隐藏的节点（在应用程序下）。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建对应UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏多个特殊字符</td>
   <td>
    <ol>
     <li>将属性“sling:hideChildren（String或String[]）”添加到“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”。 </li>
     <li>将节点名称（要隐藏的特殊字符）添加为“sling:hideChildren”属性的值。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建对应UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>对特殊字符排序</td>
   <td>
    <ol>
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加子节点（含必需属性）。 </li>
     <li>将“sling:orderBefore(String)”属性添加到新创建的子节点。 </li>
     <li>添加节点名称作为值，新添加的特殊字符将显示在该值之前。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建对应UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

