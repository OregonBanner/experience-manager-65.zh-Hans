---
title: HTML5表单的Form Bridge API
seo-title: HTML5表单的Form Bridge API
description: 外部应用程序使用FormBridge API连接到XFA移动表单。 API在父窗口上调度一个FormBridgeInitialized事件。
seo-description: 外部应用程序使用FormBridge API连接到XFA移动表单。 API在父窗口上调度一个FormBridgeInitialized事件。
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# HTML5表单的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API在基于XFA的HTML5表单和应用程序之间打开通信渠道。 表单桥API提供&#x200B;**connect** API以创建连接。

**connect** API接受处理函数作为参数。 在基于XFA的HTML5表单与表单桥接器之间建立成功连接后，将调用句柄。

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
>请确保在包含formRuntime.jsp文件之前创建连接。

## 可用的表单桥接器API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回脚本库的版本号

* **输入**:无
* **输出**:脚本库的版本号
* **错误**:无

**isConnected()检** 查表单状态是否已初始化

* **输入**:无
* **输出**: **如** 果XFA表单状态已初始化，则为true

* **错误**:无

**connect(handler, context)** 与FormBridge建立连接，并在建立连接并初始化表单状态后执行该函数

* **输入**:

   * **处理函数**:连接Form Bridge后要执行的函数
   * **上下文**:将handlerfunction的上下文(this)设 ** 置到的对象。

* **输出**:无
* **错误**:无

**getDataXML（选项）** 以XML格式返回当前表单数据

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理函数。此函数传递的对象包含&#x200B;*data*&#x200B;属性中的XML。
      * **上下文**:将successfunction的上下文(this)设置 ** 到的对象
      * **validationChecker**:用于调用以检查从服务器收到的验证错误的函数。验证函数传递了一组错误字符串。
      * **formState**:必须返回数据XML的XFA表单的JSON状态。如果未指定，则返回当前呈现的表单的数据XML。

* **输出：** 无
* **错误：** 无

**registerConfig(configName, config)在FormBridge** 中注册用户／门户特定配置。这些配置将覆盖默认配置。 配置部分中指定了支持的配置。

* **输入:**

   * **configName:** 要覆盖的配置的名称

      * **widgetConfig:** 允许用户使用自定义构件覆盖表单中的默认构件。配置将被重写，如下所示：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 允许用户覆盖仅呈现第一页的默认行为。配置将被重写，如下所示：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true>,shrinkPageDisabled: &lt;true> })。*

      * **LoggingConfig:** 允许用户覆盖日志记录级别、禁用类别日志记录，或者显示日志控制台还是发送到服务器。配置可以重写，如下所示：

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

      * **SubmitServiceProxyConfig：允** 许用户注册提交和记录器代理服务。

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** 配置值



* **输出：** 包含dataproperty中配置的原始值的 ** 对象。

* **错误：** 无

**hideFields(fieldArray)隐** 藏其Som表达式在fieldArray中提供的字段。将指定字段的存在属性设置为不可见

* **输入:**

   * **fieldArray:** 要隐藏的字段的某些表达式的数组

* **输出：** 无
* **错误：** 无

**showFields(fieldArray)** 显示其Som表达式在fieldArray中提供的字段。将提供字段的存在属性设置为可见

* **输入:**

   * **fieldArray:** 要显示的字段的Som表达式的数组

* **输出：** 无
* **错误：** 无

**hideSubmitButtons()隐** 藏表单中的所有提交按钮

* **输入**:无
* **输出**:无
* **错误**:表单状态未初始化时引发异常

**getFormState()返** 回表示表单状态的JSON

* **输入：** 无
* **输出：** 包含JSON的对象，该JSON在dataproperty中表示当前表单 ** 状态。

* **错误：** 无

**restoreFormState（选项）** 从选项对象中提供的JSON状态恢复表单状态。操作完成后，将应用状态并调用成功或错误处理程序

* **输入:**

   * **选项：包** 含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理函数
      * **上下文**:将successfunction的上下文(this)设置 ** 到的对象
      * **formState**:表单的JSON状态。表单将恢复为JSON状态。

* **输出：** 无
* **错误：** 无

**setFocus(som)集** 对在Som表达式中指定的字段进行聚焦

* **输入：** 要设置焦点的字段的某些表达式
* **输出：** 无
* **错误：** 在Som表达式不正确时引发异常

**setFieldValue(som, value)** 设置给定Som表达式的字段值

* **输入:**

   * **som：包** 含字段的某些表达式的数组。设置字段值的表达式。
   * **value：包含** 与somarray中提供的Som表达式对应的值的 ****&#x200B;数组。如果值的数据类型与fieldType不同，则不修改该值。

* **输出：** 无
* **错误：** 在Som表达式不正确时引发异常

**getFieldValue(som)** 返回给定Som表达式的字段值

* **Input：包** 含值必须检索的字段的Som表达式的数组
* **输出：** 在dataproperty中将结果作为Array包含 **** 的对象。

* **错误：** 无

### getFieldValue()API {#example-of-nbsp-getfieldvalue-api}示例

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

**getFieldProperties(som, property)检** 索Som表达式中指定字段的给定属性的值列表

* **输入:**

   * **som：包** 含字段的Som表达式的数组
   * **属性**:其值为必需属性的名称

* **输出：** 数据属性中包含结果为Array的 ** 对象

* **错误：** 无

**setFieldProperties(som, property, values)** 为Som表达式中指定的所有字段设置给定属性的值

* **输入:**

   * **som:** 包含必须设置值的字段的Som表达式的数组
   * **属性**:必须设置其值的属性
   * **value：包** 含Som表达式中指定字段的给定属性的值的数组

* **输出：** 无
* **错误：** 无

## Form Bridge API {#sample-usage-of-form-bridge-api}的示例使用

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
