---
title: 适用于HTML5表单的Form Bridge API
description: 外部应用程序使用FormBridge API连接到XFA Mobile表单。 API在父窗口中调度FormBridgeInitialized事件。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 适用于HTML5表单的Form Bridge API {#form-bridge-apis-for-html-forms}

您可以使用Form Bridge API打开基于XFA的HTML5表单与您的应用程序之间的通信渠道。 Form Bridge API提供了 **connect** 用于创建连接的API。

此 **connect** API接受处理程序作为参数。 在基于XFA的HTML5表单与表单桥接器之间成功创建连接后，将调用句柄。

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

## 可用的Form Bridge API  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

返回脚本库的版本号

* **输入**：无
* **输出**：脚本库的版本号
* **错误**：无

**isConnected()** 检查表单状态是否已初始化

* **输入**：无
* **输出**： **True** 如果XFA表单状态已初始化

* **错误**：无

**connect(handler， context)** 与FormBridge建立连接，并在建立连接且Form State初始化后执行函数

* **输入**:

   * **处理程序**：连接Form Bridge后执行的函数
   * **上下文**：上下文(this)的目标对象 *处理程序* 函数已设置。

* **输出**：无
* **错误**：无

**getDataXML(options)** 以XML格式返回当前表单数据

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**：错误处理程序函数
      * **success**：成功处理程序函数。 此函数传递一个包含XML的对象 *数据* 属性。
      * **上下文**：上下文(this)的目标对象 *success* 函数已设置
      * **validationChecker**：用于调用以检查从服务器收到的验证错误的函数。 验证函数传递了错误字符串的数组。
      * **formState**：必须为其返回数据XML的XFA表单的JSON状态。 如果未指定，则返回当前渲染表单的数据XML。

* **输出：** 无
* **错误：** 无

**registerConfig(configName， config)** 向FormBridge注册用户/门户特定配置。 这些配置将覆盖默认配置。 支持的配置在配置部分中指定。

* **输入:**

   * **configName：** 要覆盖的配置名称

      * **widgetConfig：** 允许用户使用自定义构件覆盖表单中的默认构件。 将按如下方式覆盖配置：

        *formBridge.registerConfig(&quot;widgetConfig&quot;：{/&amp;ast；configuration&amp;ast；/})*

      * **pagingConfig：** 允许用户覆盖仅呈现第一页的默认行为。 将按如下方式覆盖配置：

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;：{pagingDisabled： &lt;true false=&quot;&quot;>，shrinkPageDisabled： &lt;true false=&quot;&quot;> })。*

      * **Loggingconfig：** 允许用户覆盖日志记录级别，禁用某个类别的日志记录，或者是否显示日志控制台或发送到服务器。 可按如下方式覆盖配置：

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

      * **SubmitServiceProxyConfig：** 允许用户注册提交和记录器代理服务。

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **配置：** 配置的值

* **输出：** 包含配置原始值的对象 *数据* 属性。

* **错误：** 无

**hideFields(fieldArray)** 隐藏fieldArray中提供Som表达式的字段。 将指定字段的presence属性设置为不可见

* **输入:**

   * **字段数组：** 要隐藏的字段的Som表达式数组

* **输出：** 无
* **错误：** 无

**showFields(fieldArray)** 显示其Som表达式在fieldArray中提供的字段。 将所提供字段的presence属性设置为可见

* **输入:**

   * **字段数组：** 要显示的字段的Som表达式数组

* **输出：** 无
* **错误：** 无

**hideSubmitButton()** 隐藏表单中的所有提交按钮

* **输入**：无
* **输出**：无
* **错误**：如果表单状态未初始化，则引发异常

**getFormState()** 返回表示表单状态的JSON

* **输入：** 无
* **输出：** 包含表示当前表单状态的JSON的对象 *数据* 属性。

* **错误：** 无

**restoreFormState(options)** 从选项对象中提供的JSON状态恢复表单状态。 应用状态，并在操作完成后调用成功或错误处理程序

* **输入:**

   * **选项：** 包含以下属性的JavaScript对象：

      * **错误**：错误处理程序函数
      * **success**：成功处理程序函数
      * **上下文**：上下文(this)的目标对象 *success* 函数已设置
      * **formState**：表单的JSON状态。 表单将恢复为JSON状态。

* **输出：** 无
* **错误：** 无

**setFocus (som)** 将焦点设置为Som表达式中指定的字段

* **输入：** 要设置焦点的字段的SOM表达式
* **输出：** 无
* **错误：** 如果Som表达式不正确，则引发异常

**setFieldValue (som， value)** 设置给定Som表达式的字段值

* **输入:**

   * **som：** 包含字段的Som表达式的数组。 用于设置字段值的som表达式。
   * **值：** 数组，其中包含与中提供的Som表达式对应的值 **som**&#x200B;数组。 如果该值的数据类型与fieldType不同，则不会修改该值。

* **输出：** 无
* **错误：** 如果Som表达式不正确，则引发异常

**getFieldValue (som)** 返回给定Som表达式的字段值

* **输入：** 包含必须检索其值的字段的Som表达式的数组
* **输出：** 将结果作为数组包含在中的对象 **数据** 属性。

* **错误：** 无

### getFieldValue() API示例 {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som， property)** 检索Som表达式中指定的字段的给定属性的值列表

* **输入:**

   * **som：** 包含字段的Som表达式的数组
   * **属性**：需要其值的属性的名称

* **输出：** 将结果作为数组包含在中的对象 *数据* 属性

* **错误：** 无

**setFieldProperties（som，属性，值）** 为Som表达式中指定的所有字段设置给定属性的值

* **输入:**

   * **som：** 包含必须设置其值的字段的Som表达式的数组
   * **属性**：必须设置其值的属性
   * **值：** 包含Som表达式中指定的字段的给定属性的值的数组

* **输出：** 无
* **错误：** 无

## Form Bridge API的示例用法 {#sample-usage-of-form-bridge-api}

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
