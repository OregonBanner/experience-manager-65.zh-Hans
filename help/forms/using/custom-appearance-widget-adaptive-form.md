---
title: 为自适应表单域创建自定义外观
seo-title: 为自适应表单域创建自定义外观
description: 在自适应Forms中自定义现成组件的外观。
seo-description: 在自适应Forms中自定义现成组件的外观。
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 0%

---


# 为自适应表单字段创建自定义外观{#create-custom-appearances-for-adaptive-form-fields}

## 简介 {#introduction}

自适应表单利用[外观框架](/help/forms/using/introduction-widgets.md)帮助您为自适应表单字段创建自定义外观并提供不同的用户体验。 例如，将单选按钮和复选框替换为切换按钮或使用自定义jQuery插件限制用户在电话号码或电子邮件ID等字段中的输入。

此文档介绍如何使用jQuery插件为自适应表单字段创建这些替代体验。 此外，它还展示了一个示例，用于为数字字段组件创建自定义外观以显示为数字步进器或滑块。

我们首先来看一下本文使用的关键术语和概念。

**外** 观指自适应表单字段各个元素的样式、外观和组织。它通常包括标签、提供输入的交互区域、帮助图标以及字段的简短和长篇描述。 本文讨论的外观定制适用于字段输入区域的外观。

**jQuery** plugin提供基于jQuery构件框架的标准机制，以实现替代外观。

**ClientLib** 由复杂的JavaScript和CSS代码驱动的AEM客户端处理中的客户端库系统。有关详细信息，请参阅使用客户端库。

**原型** A Maven项目模板工具包，定义为Maven项目的原始图案或模型。有关详细信息，请参阅原型简介。

**用户** 控制指构件中包含字段值的主元素，外观框架用于将自定义构件UI与自适应表单模型绑定。

## 创建自定义外观的步骤{#steps-to-create-a-custom-appearance}

创建自定义外观的步骤高度如下：

1. **创建项目**:创建一个Maven项目，它生成要部署到AEM的内容包。
1. **扩展现有构件类**:扩展现有构件类并覆盖所需的类。
1. **创建客户端库**:创建 `clientLib: af.customwidget` 库并添加所需的JavaScript和CSS文件。

1. **构建和安装项目**:构建Maven项目并在AEM上安装生成的内容包。
1. **更新自适应表单**:更新自适应表单字段属性以使用自定义外观。

### 创建项目{#create-a-project}

主原型是创建自定义外观的起点。 要使用的原型的详细信息如下：

* **存储库**:https://repo.adobe.com/nexus/content/groups/public/
* **工件Id**:自定外观原型
* **组ID**:com.adobe.aemforms
* **版本**:1.0.4

执行以下命令以基于原型创建本地项目：

`mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

该命令从存储库下载Maven插件和原型信息，并根据以下信息生成项目：

* **groupId**:生成的Maven项目使用的组ID
* **artifactId**:生成的Maven项目使用的对象ID。
* **版本**:生成的Maven项目的版本。
* **包**:用于文件结构的包。
* **artifactName**:生成的AEM包的对象名称。
* **packageGroup**:生成的AEM包的包组。
* **widgetName**:用于引用的外观名称。

生成的项目具有以下结构：

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 扩展现有构件类{#extend-an-existing-widget-class}

创建项目模板后，根据需要进行以下更改：

1. 将第三方插件依赖关系包含到项目。

   1. 将第三方或自定义jQuery插件放在`jqueryplugin/javascript`文件夹中，并将相关CSS文件放在`jqueryplugin/css`文件夹中。 有关详细信息，请参阅`jqueryplugin/javascript and jqueryplugin/css`文件夹下的JS和CSS文件。

   1. 修改`js.txt`和`css.txt`文件，以包含jQuery插件的任何其他JavaScript和CSS文件。

1. 将第三方插件与框架集成，实现自定义外观框架与jQuery插件之间的交互。 只有在您扩展或覆盖以下功能后，新构件才能正常工作。

<table>
 <tbody>
  <tr>
   <td><strong>函数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>渲染函数返回构件的默认HTML元素的jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，<code>&lt;a&gt;</code>、<code>&lt;input&gt;</code>和<code>&lt;li&gt;</code>。 返回的元素将用作<code>$userControl</code>。 如果<code>$userControl</code>指定上述约束，则<code>AbstractWidget</code>类的函数将按预期工作，否则某些常用API（焦点，单击）需要更改。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此示例显示 <code>blur</code> 它是HTML事件, <code>XFA_EXIT_EVENT</code> 是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>返回一个地图，其中提供有关在选项更改时要执行的操作的详细信息。 键是提供给构件的选项，值是检测到选项发生更改时调用的函数。 该构件为所有常用选项（<code>value</code>和<code>displayValue</code>除外）提供处理程序。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>只要jQuery构件的值保存在XFA模型中(例如文本字段的退出事件),jQuery构件框架就会加载该函数。 实施应返回在构件中保存的值。 该处理函数提供了选项的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>默认情况下，在XFA中进入事件时，将显示字段的<code>rawValue</code>。 调用此函数向用户显示<code>rawValue</code>。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>默认情况下，在退出事件的XFA中，显示字段的<code>formattedValue</code>。 调用此函数向用户显示<code>formattedValue</code>。 </td>
  </tr>
 </tbody>
</table>

1. 根据需要更新`integration/javascript`文件夹中的JavaScript文件。

   * 将文本`__widgetName__`替换为实际的构件名称。
   * 从合适的现成构件类扩展构件。 在大多数情况下，它是与要替换的现有构件相对应的构件类。 父类名称用于多个位置，因此建议搜索文件中字符串`xfaWidget.textField`的所有实例，并将它们替换为使用的实际父类。
   * 扩展`render`方法以提供替代UI。 它是调用jQuery插件以更新UI或交互行为的位置。 `render`方法应返回用户控制元素。

   * 扩展`getOptionsMap`方法以覆盖因构件更改而受影响的任何选项设置。 该函数返回一个映射，该映射为在选项更改时要执行的操作提供详细信息。 键是提供给构件的选项，值是检测到选项发生更改时调用的函数。
   * `getEventMap`方法将构件触发的事件与自适应表单模型所需的事件进行映射。 默认值映射默认构件的标准HTML事件，如果触发了替代事件，则需要更新。
   * `showDisplayValue`和`showValue`应用显示和编辑图片子句，可以被覆盖以具有替代行为。

   * 当`commit`发生事件时，自适应表单框架将调用`getCommitValue`方法。 通常，它是退出事件，但下拉菜单、单选按钮和复选框元素在更改时出现的情况除外)。 有关详细信息，请参阅[自适应Forms表达式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 模板文件为各种方法提供示例实现。 删除不要扩展的方法。

### 创建客户端库{#create-a-client-library}

由Maven原型生成的示例项目会自动创建所需的客户端库，并将它们打包到具有类别`af.customwidgets`的客户端库中。 `af.customwidgets`中可用的JavaScript和CSS文件在运行时自动包含。

### 构建和安装{#build-and-install}

要构建项目，请在shell上执行以下命令，以生成需要安装在AEM服务器上的CRX包。

`mvn clean install`

>[!NOTE]
>
>主项目引用POM文件中的远程存储库。 这仅供参考，根据Maven标准，存储库信息会在`settings.xml`文件中捕获。

### 更新自适应表单{#update-the-adaptive-form}

要将自定义外观应用于自适应表单字段，请执行以下操作：

1. 在编辑模式下打开自适应表单。
1. 为要应用自定义外观的字段打开&#x200B;**属性**&#x200B;对话框。
1. 在&#x200B;**样式**&#x200B;选项卡中，更新`CSS class`属性以添加`widget_<widgetName>`格式的外观名称。 例如：**widget_numericstepper**

## 示例：创建自定义外观   {#sample-create-a-custom-appearance-nbsp}

现在，让我们看一个示例，为数字字段创建自定义外观以显示为数字步进器或滑块。 执行以下步骤：

1. 执行以下命令以创建基于Maven原型的本地项目：

   `mvn archetype:generate -DarchetypeRepository=https://repo.adobe.com/nexus/content/groups/public/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它提示您为以下参数指定值。
   *此示例中使用的值以粗体突出显示*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 导航到`customWidgets`（为`artifactID`属性指定的值）目录并执行以下命令以生成Eclipse项目：

   `mvn eclipse:eclipse`

1. 打开Eclipse工具并执行以下操作以导入Eclipse项目：

   1. 选择&#x200B;**[!UICONTROL “文件”>“导入”>“现有项目到Workspace]**”。

   1. 浏览并选择执行`archetype:generate`命令的文件夹。

   1. 单击&#x200B;**[!UICONTROL 完成]**。

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. 选择要用于自定义外观的构件。 此示例使用以下数字步进构件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse项目中，查看`plugin.js`文件中的插件代码，确保它符合外观要求。 在此示例中，外观满足以下要求：

   * 数字步进器应从`- $.xfaWidget.numericInput`扩展。
   * 构件的`set value`方法在焦点位于字段后设置值。 这是自适应表单构件的必需要求。
   * 需要重写`render`方法以调用`bootstrapNumber`方法。

   * 除了插件的主源代码之外，该插件没有其他依赖关系。
   * 该范例不对步进器执行任何样式，因此不需要任何其他CSS。
   * `$userControl`对象应可用于`render`方法。 它是使用插件代码克隆的`text`类型的字段。

   * 禁用字段时，应禁用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按钮。

1. 将`bootstrap-number-input.js`（jQuery插件）的内容替换为`numericStepper-plugin.js`文件的内容。
1. 在`numericStepper-widget.js`文件中，添加以下代码以覆盖渲染方法以调用插件并返回`$userControl`对象：

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 在`numericStepper-widget.js`文件中，重写`getOptionsMap`属性以覆盖访问选项，并在禁用模式下隐藏+和——按钮。

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 保存更改，导览至包含`pom.xml`文件的文件夹，然后执行以下Maven命令来构建项目：

   `mvn clean install`

1. 使用AEM Package Manager安装包。

1. 在要应用自定义外观的编辑模式下打开自适应表单，并执行以下操作：

   1. 右键单击要应用外观的字段，然后单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开编辑组件对话框。

   1. 在样式选项卡中，更新&#x200B;**[!UICONTROL CSS类]**&#x200B;属性以添加`widget_numericStepper`。

您刚刚创建的新外观现可供使用。
