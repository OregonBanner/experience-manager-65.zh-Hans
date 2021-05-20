---
title: HTML5表单的表单桥API
seo-title: HTML5表单的表单桥API
description: 外部应用程序使用FormBridge API连接到XFA移动设备表单。 API在父窗口中调度FormBridgeInitialized事件。
seo-description: 外部应用程序使用FormBridge API连接到XFA移动设备表单。 API在父窗口中调度FormBridgeInitialized事件。
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---

# HTML5表单的表单桥API {#form-bridge-apis-for-html-forms}

您可以使用表单桥API在基于XFA的HTML5表单与应用程序之间打开通信渠道。 表单桥API提供了一个&#x200B;**connect** API以创建连接。

**connect** API接受将处理程序作为参数。 在基于XFA的HTML5表单与表单桥之间成功创建连接后，将调用句柄。

您可以使用以下示例代码创建连接。

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>确保在包含formRuntime.jsp文件之前创建连接。

## 可用的表单桥API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回脚本库的版本号

* **输入**:无
* **输出**:脚本库的版本号
* **错误**:无

**isConnected()检** 查表单状态是否已初始化

* **输入**:无
* **输出**: **** 如果XFA表单状态已初始化，则为true

* **错误**:无

**connect(handler， context)** 与FormBridge建立连接，并在建立连接并初始化表单状态后执行函数

* **输入**:

   * **处理程序**:连接表单桥后要执行的函数
   * **上下文**:将Handler函数的上下文(this)设 ** 置到的对象。

* **输出**:无
* **错误**:无

**getDataXML(options)** 以XML格式返回当前表单数据

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理程序函数。此函数传递的对象包含&#x200B;*data*&#x200B;属性中的XML。
      * **上下文**:已设置successfunction的上下文(this) ** 的对象
      * **validationChecker**:用于调用以检查从服务器收到的验证错误的函数。验证函数传递一个错误字符串数组。
      * **formState**:必须返回数据XML的XFA表单的JSON状态。如果未指定，则返回当前呈现表单的数据XML。

* **输出：** 无
* **错误：** 无

**registerConfig(configName， config)** 使用FormBridge注册用户/门户特定配置。这些配置会覆盖默认配置。 配置部分中指定了支持的配置。

* **输入:**

   * **configName:** 要覆盖的配置的名称

      * **widgetConfig:** 允许用户使用自定义小组件覆盖表单中的默认小组件。配置将被覆盖，如下所示：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 允许用户覆盖仅渲染第一页的默认行为。配置将被覆盖，如下所示：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true>, shrinkPageDisabled: &lt;true> })。*

      * **LoggingConfig:** 允许用户覆盖日志记录级别、禁用类别的日志记录，或者显示日志控制台还是发送到服务器。配置可以覆盖如下：

      ```javascript
      formBridge.registerConfig{
        "LoggerConfig" : {
      {
      "on":`<true *| *false>`,
      "category":`<array of categories>`,
      "level":`<level of categories>`, "
      type":`<"console"/"server"/"both">`
      }
        }
      ```

      * **SubmitServiceProxyConfig:** 允许用户注册提交和记录代理服务。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** 配置的值



* **输出：** 包含dataproperty中配置原始值的对 ** 象。

* **错误：** 无

**hideFields(fieldArray)** 隐藏其Som表达式在fieldArray中提供的字段。将指定字段的存在属性设置为不可见

* **输入:**

   * **fieldArray:** 要隐藏的字段的Som表达式数组

* **输出：** 无
* **错误：** 无

**showFields(fieldArray)** 显示其Som表达式在fieldArray中提供的字段。将提供字段的存在属性设置为可见

* **输入:**

   * **fieldArray:** 要显示的字段的Som表达式数组

* **输出：** 无
* **错误：** 无

**hideSubmitButtons()** 隐藏表单中的所有提交按钮

* **输入**:无
* **输出**:无
* **错误**:如果未初始化表单状态，则引发异常

**getFormState()** 返回表示表单状态的JSON

* **输入：** 无
* **输出：** 包含JSON的对象，该JSON表示dataproperty中的当前表单 ** 状态。

* **错误：** 无

**restoreFormState(options)** 从选项对象中提供的JSON状态还原表单状态。操作完成后，将应用状态并调用成功或错误处理程序

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理程序函数
      * **上下文**:已设置成功函数的上下文(this) ** 的对象
      * **formState**:表单的JSON状态。表单将恢复为JSON状态。

* **输出：** 无
* **错误：** 无

**setFocus(som)** 集中在Som表达式中指定的字段

* **输入：** 要设置焦点的字段的某个表达式
* **输出：** 无
* **错误：** 在Som表达式不正确时引发异常

**setFieldValue(som， value)** 为给定Som表达式设置字段值

* **输入:**

   * **som:** 包含字段的Som表达式的数组。用于设置字段值的部分表达式。
   * **值：** 包含与somarray中提供的Som表达式对应的值的数 ****&#x200B;组。如果值的数据类型与fieldType不同，则不会修改该值。

* **输出：** 无
* **错误：** 在Som表达式不正确时引发异常

**getFieldValue(som)** 返回给定Som表达式的字段值

* **输入：** 包含值必须检索的字段的一些表达式的数组
* **输出：** 在dataproperty中包含结果为Array的 **** 对象。

* **错误：** 无

### getFieldValue()API {#example-of-nbsp-getfieldvalue-api}的示例

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som， property)** 检索在Som表达式中指定的字段的给定属性的值列表

* **输入:**

   * **som:** 包含字段的Som表达式的数组
   * **属性**:其值为必需属性的名称

* **输出：** 在dataproperty中将结果作为Array包含的 ** 对象

* **错误：** 无

**setFieldProperties(som， property， values)** 为Som表达式中指定的所有字段设置给定属性的值

* **输入:**

   * **som:** 包含值必须设置的字段的Som表达式的数组
   * **属性**:必须设置其值的属性
   * **值：** 包含在Som表达式中指定字段的给定属性值的数组

* **输出：** 无
* **错误：** 无

## 表单桥API {#sample-usage-of-form-bridge-api}的使用示例

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
