---
title: 通信管理中的自定义特殊字符
seo-title: 通信管理中的自定义特殊字符
description: 了解如何在通信管理中添加自定义特殊字符。
seo-description: 了解如何在通信管理中添加自定义特殊字符。
uuid: a1890f6d-8e0c-471f-a9bd-861acf1f17e6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9f26565c-a7ba-4e9e-bf77-a95eb8e351f2
docset: aem65
feature: 通信管理
exl-id: 3e978c3e-12f2-4dc6-801d-8ab4c5df6700
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---

# 通信管理中的自定义特殊字符{#custom-special-characters-in-correspondence-management}

## 概述 {#overview}

通信管理内置默认支持210个特殊字符，您可以轻松插入字母。

例如，您可以插入以下特殊字符：

* 货币符号，如€、¥和£
* 数学符号，如∑、√、∂和^
* 标点符号（“和”）

您可以在字母中插入特殊字符：

* 在[文本编辑器](/help/forms/using/document-fragments.md#createtext)中
* 在[可编辑的内联模块中，通信](../../forms/using/create-correspondence.md#managecontent)

![specialcharactersinlinemodule](assets/specialcharactersinlinemodule.png)

管理员可以通过自定义添加对更多/自定义特殊字符的支持。 本文提供了有关如何添加对其他自定义特殊字符的支持的说明。

## 在通信管理中添加或修改对自定义特殊字符的支持 {#creatingfolderstructure}

使用以下步骤添加对自定义特殊字符的支持：

1. 转到`https://'[server]:[port]'/[ContextPath]/crx/de`并以管理员身份登录。
1. 在apps文件夹中，创建一个名为&#x200B;**[!UICONTROL specialcharacters]**&#x200B;的文件夹，其路径/结构与specialcharacters文件夹类似（位于libs下的textEditorConfig文件夹中）：

   1. 右键单击以下路径中的&#x200B;**特殊字符**&#x200B;文件夹，然后选择&#x200B;**覆盖节点**:

      `/libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters`

   1. 确保“覆盖节点”对话框具有以下值：

      **路径：** /libs/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters

      **叠加位置：** /apps/

      **匹配节点类型：** 已选中

      >[!NOTE]
      >
      >请勿在/libs分支中进行更改。 您所做的任何更改都可能会丢失，因为当您执行以下操作时，此分支将容易发生更改：
      >
      >
      >
      >    * 在实例上升级
      >    * 应用热修复程序
      >    * 安装功能包


   1. 单击&#x200B;**确定**，然后单击&#x200B;**保存全部**。 在指定的路径中创建特定字符文件夹。

      创建叠加后，验证节点结构标记。 在/apps中使用叠加创建的每个节点都应具有与/libs中为该节点定义的相同类和属性。 如果/apps位置下的节点结构中缺少任何属性或标记，请将其标记与/libs中的相应节点同步。



1. 确保&#x200B;**[!UICONTROL textEditorConfig]**&#x200B;节点具有以下属性和值：

   | 名称 | 类型 | 值 |
   |---|---|---|
   | cmConfigurationType | 字符串 | cmTextEditorConfiguration |
   | cssPath | 字符串 | /libs/fd/cm/ma/gui/components/admin/createasset/textcontrol/clientlibs/textcontrol |

1. 右键单击以下路径中的&#x200B;**[!UICONTROL 特殊字符]**&#x200B;文件夹，然后选择&#x200B;**创建>子节点**，然后单击&#x200B;**保存全部**:

   /apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters/&lt;YourChildNode>

1. 刷新文本编辑器\创建通信UI页。 您添加的节点是UI中特殊字符列表中的最后一个节点。
1. 单击&#x200B;**Save All**。
1. 根据需要更改特殊字符：

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
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加子节点，并包含必需属性。</li>
     <li>单击Save All</li>
     <li>刷新文本编辑器\创建通信UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>更新现有特殊字符的属性</td>
   <td>
    <ol>
     <li>按照上述说明叠加要更新的节点，并验证标记和类。</li>
     <li>更改任何值，如caption、value、endValue和multipleCaption。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建通信UI以查看更改。</li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏特殊字符</td>
   <td>
    <ol>
     <li>叠加要隐藏在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下的节点</li>
     <li>将sling:hideResource(Boolean)属性添加到要隐藏的节点（在应用程序下）。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建通信UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>隐藏多个特殊字符</td>
   <td>
    <ol>
     <li>将属性“sling:hideChildren（String或String[]）”添加到“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”。 </li>
     <li>添加节点名称（要隐藏的特殊字符）作为“sling:hideChildren”属性的值。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建通信UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td>对特殊字符排序</td>
   <td>
    <ol>
     <li>在“/apps/fd/cm/ma/gui/configuration/textEditorConfig/specialcharacters”下添加子节点，并包含必需属性。 </li>
     <li>将“sling:orderBefore(String)”属性添加到新创建的子节点。 </li>
     <li>将节点名称添加为值，新添加的特殊字符将在该值之前显示。 </li>
     <li>单击“全部保存”。 </li>
     <li>刷新文本编辑器\创建通信UI以查看更改。<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
