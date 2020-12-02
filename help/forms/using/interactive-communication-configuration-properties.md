---
title: 交互通信配置属性
seo-title: 交互通信配置属性
description: 编辑交互通信的默认配置属性
seo-description: 编辑交互通信的默认配置属性
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---


# 交互通信配置属性{#interactive-communications-configuration-properties}

交互通信包括在安装[AEM Forms加载项](../../forms/using/installing-configuring-aem-forms-osgi.md)软件包后自动配置的属性。 交互通信作者可以使用&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页编辑这些默认配置属性。

使用以下URL打开&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页：

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

配置属性包括：

* [文档片段配置](#document-fragments-configuration)
* [创建对应配置](#create-correspondence-configuration)
* [自适应表单与交互式通信Web渠道配置](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [自适应表单与交互通信Web渠道主题配置](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## 文档片段配置{#document-fragments-configuration}

点按&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页上的&#x200B;**文档片段配置**&#x200B;以视图文档片段的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>数据显示格式</td> 
   <td>创建用于打印和Web渠道的交互式通信时，可用的字段、变量和表单数据模型元素的区域设置特定显示格式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US、de_DE、fr_FR和ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>缩进</td> 
   <td>应用于列表文档片段中文本的单个缩进单位的宽度。</td> 
   <td>12.7毫米</td> 
   <td>数字</td> 
  </tr> 
  <tr> 
   <td>罗马数字最小宽度</td> 
   <td>在列表文档片段中使用罗马数字时，应用于项目符号或数字字段的最小宽度。 </td> 
   <td>12.7毫米</td> 
   <td>数字</td> 
  </tr> 
  <tr> 
   <td>最小宽度数</td> 
   <td>在列表文档片段中使用编号列表（除罗马数字之外）时，要应用于项目符号或编号字段的最小宽度。</td> 
   <td>8毫米</td> 
   <td>数字</td> 
  </tr> 
 </tbody> 
</table>

## 创建对应配置{#create-correspondence-configuration}

点按&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页上的&#x200B;**创建对应配置**&#x200B;以视图代理UI的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>显示要编辑的已解析内容</td> 
   <td>选中此复选框可在代理UI上编辑文本模块时显示已解析的内容（实际值而非占位符）。</td> 
   <td>未选择</td> 
   <td>不适用</td> 
  </tr> 
  <tr> 
   <td>在预览期间应用水印</td> 
   <td>选中此复选框可将水印应用于“在预览模式下打印交互通信的渠道”。</td> 
   <td>未选择</td> 
   <td>不适用</td> 
  </tr> 
  <tr> 
   <td>在PDF中启用字体嵌入</td> 
   <td><p>选中此复选框可在PDF文档中启用嵌入字体。 选择此选项后，您可以使用代理UI在生成或预览PDF文档后嵌入新字体。 使用交互通信的打印渠道生成和预览PDF文档。</p> <p>如果用于生成PDF的计算机上有字体，而访问PDF的客户端计算机上没有字体，则在PDF文档中嵌入字体很有用。</p> <p>有关嵌入字体的详细信息，请参阅<a href="../../forms/using/customize-text-editor.md" target="_blank">自定义文本编辑器</a>。</p> </td> 
   <td>未选择</td> 
   <td>不适用</td> 
  </tr> 
 </tbody> 
</table>

## 自适应表单和交互式通信Web渠道配置{#adaptive-form-and-interactive-communication-web-channel-configuration}

点按&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页上的&#x200B;**自适应表单和交互式通信Web渠道配置**，以视图自适应Forms和交互式通信Web渠道的配置属性。 下表描述了与交互通信相关的属性：

| 属性 | 描述 | 默认 | 可接受值 |
|---|---|---|---|
| 显示占位符 | 选中此复选框可显示自适应表单和交互式通信中包含的字段的占位符。 | 已选定 | 不适用 |
| 最大缓存条目数 | 设置可使用缓存检索的最大自适应表单和交互式通信数。 | 100 | 数字 |
| 使文件名唯一 | 选中此复选框可为自适应Forms和交互式通信中作为附件包含的文件提供唯一名称。 | 未选择 | 不适用 |

## 自适应表单和交互式通信Web渠道主题配置{#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

点按&#x200B;**Adobe Experience ManagerWeb控制台配置**&#x200B;页上的&#x200B;**自适应表单和交互式通信Web渠道主题配置**，以视图自适应Forms和交互式通信Web渠道主题的配置属性。

<table>
 <tbody> 
  <tr> 
   <td>属性</td> 
   <td>描述</td> 
   <td>默认</td> 
   <td>可接受值</td> 
  </tr> 
  <tr> 
   <td>字体列表名</td> 
   <td>列表在创建自适应Forms和交互通信时可用的字体。</td> 
   <td><p>格鲁吉亚</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>影响</p> <p>Palatino Linotype</p> </td> 
   <td>所有有效的Adobe服务器字体</td> 
  </tr> 
 </tbody> 
</table>

