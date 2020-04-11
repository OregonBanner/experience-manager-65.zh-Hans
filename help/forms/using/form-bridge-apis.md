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
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# HTML5表单的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API在基于XFA的HTML5表单与应用程序之间打开通信渠道。 Form Bridge API提供了用于 **创建连接** 的连接API。

**connect** API接受处理函数作为参数。 在基于XFA的HTML5表单与表单桥接器之间成功创建连接后，将调用句柄。

可以使用以下示例代码创建连接。

```
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

## 可用的Form Bridge API {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回脚本库的版本号

* **输入**:无
* **输出**:脚本库的版本号
* **错误**:无

**isConnected()检查表单状态是否已初始化** 。

* **输入**:无
* **输出**:如 **** 果XFA表单状态已初始化，则为true

* **错误**:无

**connect(handler, context)** 与FormBridge建立连接，并在建立连接并初始化表单状态后执行该函数

* **输入**:

   * **handler**:连接Form Bridge后要执行的函数
   * **上下文**:将处理函数的上下文(this)设置 *到的对* 象。

* **输出**:无
* **错误**:无

**getDataXML（选项）** 以XML格式返回当前表单数据

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理程序函数。 传递此函数的对象在data属性中包含 *XML* 。
      * **上下文**:成功函数的上下文(this)设置 *到的对* 象
      * **validationChecker**:用于调用以检查从服务器收到的验证错误的函数。 验证函数会传递一个错误字符串数组。
      * **formState**:必须返回其数据XML的XFA表单的JSON状态。 如果未指定，则返回当前呈现的表单的数据XML。

* **输出：** 无
* **错误：** 无

**registerConfig(configName, config)** 在FormBridge中注册用户／门户特定配置。 这些配置将覆盖默认配置。 配置部分中指定了支持的配置。

* **输入:**

   * **configName:** 要覆盖的配置名称

      * **widgetConfig:** 允许用户使用自定义构件覆盖表单中的默认构件。 配置将被覆盖，如下所示：

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** 允许用户覆盖仅呈现第一页的默认行为。 配置将被覆盖，如下所示：

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled:&lt;true| false>, shrinkPageDisabled:&lt;true| false> })。*

      * **LoggingConfig:** 允许用户覆盖记录级别、禁用类别的记录，或者是显示日志控制台还是发送到服务器。 配置可以被覆盖，如下所示：

      ```JavaScript
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

         ```JavaScript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** 配置值



* **输出：** 包含数据属性中配置的原始值 *的对* 象。

* **错误：** 无

**hideFields(fieldArray)** 隐藏其Som表达式在fieldArray中提供的字段。 将指定字段的presence属性设置为不可见

* **输入:**

   * **fieldArray:** 要隐藏的字段的一些表达式的数组

* **输出：** 无
* **错误：** 无

**showFields(fieldArray)** 显示其Som表达式在fieldArray中提供的字段。 将提供的字段的存在属性设置为可见

* **输入:**

   * **fieldArray:** 要显示的字段的Som表达式的数组

* **输出：** 无
* **错误：** 无

**hideSubmitButtons()** 隐藏表单中的所有提交按钮

* **输入**:无
* **输出**:无
* **错误**:未初始化表单状态时引发异常

**getFormState()返回** 表示表单状态的JSON

* **输入：** 无
* **输出：** 包含JSON的对象，JSON表示数据属性中的当前表 *单状* 态。

* **错误：** 无

**restoreFormState（选项）** 从选项对象中提供的JSON状态恢复表单状态。 将应用状态，并在操作完成后调用成功或错误处理程序

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**:错误处理程序函数
      * **成功**:成功处理程序函数
      * **上下文**:将成功函数的上下文(this)设置到的 *对象* 。
      * **formState**:表单的JSON状态。 表单将恢复为JSON状态。

* **输出：** 无
* **错误：** 无

**setFocus(som)** Sets focus to the field in the Som表达式

* **输入：** 要设置焦点的字段的某些表达式
* **输出：** 无
* **错误：** 在Som表达式不正确时引发异常

**setFieldValue(som, value)** 设置给定Som表达式的字段值

* **输入:**

   * **som:** 包含字段的Som表达式的数组。 设置字段值的部分表达式。
   * **value:** 包含与somarray中提供的Som表达式对应的值的 ****&#x200B;数组。 如果值的数据类型与fieldType不同，则不修改该值。

* **输出：** 无
* **错误：** 如果Som表达式不正确，将引发异常

**getFieldValue(som)** 返回给定Som表达式的字段值

* **输入：** 包含必须检索其值的字段的Som表达式的数组
* **输出：** 将结果作为“数组”包含在data属 **性中** 的对象。

* **错误：** 无

### getFieldValue()API示例 {#example-of-nbsp-getfieldvalue-api}

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

**getFieldProperties(som, property)** 检索Som表达式中指定字段的给定属性的值的列表

* **输入:**

   * **som:** 包含Som表达式的字段数组
   * **属性**:其值为必需的属性的名称

* **输出：** 将结果作为数据属性中的Array包 *含的对* 象

* **错误：** 无

**setFieldProperties(som, property, values)** 为Som表达式中指定的所有字段设置给定属性的值

* **输入:**

   * **som:** 包含必须设置其值的字段的某些表达式的数组
   * **属性**:必须设置其值的属性
   * **value:** 包含Som表达式中指定字段的给定属性值的数组

* **输出：** 无
* **错误：** 无

## Form Bridge API的示例使用 {#sample-usage-of-form-bridge-api}

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
