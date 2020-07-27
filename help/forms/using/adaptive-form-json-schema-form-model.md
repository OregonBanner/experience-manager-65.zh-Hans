---
title: 使用JSON模式创建自适应表单
seo-title: 使用JSON模式创建自适应表单
description: 自适应表单可以使用JSON模式作为表单模型，从而允许您利用现有JSON模式创建自适应表单。
seo-description: 自适应表单可以使用JSON模式作为表单模型，从而允许您利用现有JSON模式创建自适应表单。
uuid: bdeaeae8-65a3-4c46-b27d-fe68481e31f1
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 375ba8fc-3152-4564-aec5-fcff2a95cf4c
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 5%

---


# 使用JSON模式创建自适应表单{#creating-adaptive-forms-using-json-schema}

## 前提条件 {#prerequisites}

使用JSON模式作为表单模型创作自适应表单需要基本了解JSON模式。 建议在本文之前阅读以下内容。

* [创建自适应表单](../../forms/using/creating-adaptive-form.md)
* [JSON模式](https://json-schema.org/)

## 将JSON模式用作表单模型  {#using-a-json-schema-as-form-model}

AEM Forms支持使用现有JSON模式作为表单模型创建自适应表单。 此JSON模式表示组织中的后端系统生成或使用数据的结构。 您使用的JSON模式应符合 [v4规范](https://json-schema.org/draft-04/schema)。

使用JSON模式的主要功能有：

* 在自适应表单的创作模式下，JSON的结构会在内容查找器选项卡中显示为树。 您可以将元素从JSON层次结构拖放到自适应表单。
* 您可以使用符合关联模式的JSON预填表单。
* 提交时，用户输入的数据将作为符合相关模式的JSON提交。

JSON模式由简单和复杂的元素类型组成。 元素具有向元素添加规则的属性。 当这些元素和属性被拖动到自适应表单上时，它们会自动映射到相应的自适应表单组件。

JSON元素与自适应表单组件的映射如下：

```json
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>JSON元素、属性或属性</strong></th>
   <th><strong>自适应表单组件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames约束的字符串属性。</p> <p>语法，</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉组件：</p>
    <ul>
     <li>enumNames中列出的值显示在下拉框中。</li>
     <li>枚举中列出的值用于计算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>具有格式约束的字符串属性。 例如，电子邮件和日期。</p> <p>语法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>当类型为字符串且格式为电子邮件时，将映射电子邮件组件。</li>
     <li>类型为字符串且格式为hostname时，将映射具有验证的文本框组件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>{</p> <p>“类型”: "string",</p> <p>}</p> </td>
   <td><br /> <br /> 文本字段<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>数字属性<br /> </td>
   <td>子类型设置为浮点的数字字段<br /> </td>
  </tr>
  <tr>
   <td>integer属性<br /> </td>
   <td>子类型设置为整数的数字字段<br /> </td>
  </tr>
  <tr>
   <td>布尔属性<br /> </td>
   <td>切换<br /> </td>
  </tr>
  <tr>
   <td>object property<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>数组属性</td>
   <td>最小和最大分别等于minItems和maxItems的可重复面板。 仅支持同质阵列。 因此，项目约束必须是对象而不是数组。<br /> </td>
  </tr>
 </tbody>
</table>

### 常见模式属性 {#common-schema-properties}

自适应表单使用JSON模式中的可用信息映射每个生成的字段。 特别是：

* 标题属性用作自适应表单组件的标签。
* description属性设置为自适应表单组件的长描述。
* 默认属性用作自适应表单字段的初始值。
* maxLength属性设置为文本字段组件的maxlength属性。
* “数字”框组件使用minimum、maximum、exclusiveMinimum和exclusiveMaximum属性。
* 为了支持DatePicker组件的范围，还提供了其他JSON模式属性minDate和maxDate。
* minItems和maxItems属性用于限制可从面板组件添加或删除的项目／字段数。
* readOnly属性设置自适应表单组件的只读属性。
* 必需属性将自适应表单字段标记为必需字段，而在面板（其中类型为对象）的情况下，最终提交的JSON数据的字段具有与该对象对应的空值。
* 模式属性以自适应形式设置为验证模式(常规表达式)。
* JSON模式文件的扩展名必须保留为。模式.json。 例如，&lt;filename>.模式.json。

## 示例JSON模式 {#sample-json-schema}

以下是JSON模式的示例。

```json
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### 可重用模式定义 {#reusable-schema-definitions}

定义密钥用于识别可重用模式。 可重用的模式定义用于创建片段。 它类似于在XSD中识别复杂类型。 下面给出了具有定义的示例JSON模式:

```json
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

上例定义了客户记录，其中每个客户同时具有发运地址和开单地址。 两个地址的结构相同——地址有街道地址、城市地址和州地址——因此最好不要重复地址。 它还使添加和删除字段变得很容易，以便将来进行任何更改。

## JSON模式定义中的预配置字段 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem:afProperties属性** ，预配置JSON模式字段以映射到自定义自适应表单组件。 下面列出了一个示例：

```json
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## 为表单对象配置脚本或表达式  {#configure-scripts-or-expressions-for-form-objects}

JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，并使用自适应表单脚本模型API。 您可以预配置表单对象，以 [评估表单表达式](../../forms/using/adaptive-form-expressions.md) ()事件。

使用aem:afproperties属性为自适应表单组件预配置自适应表单表达式或脚本。 例如，当触发初始化事件时，下面的代码设置电话字段的值并将值打印到日志：

```json
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

您应是表单功能用户 [组的成员](/help/forms/using/forms-groups-privileges-tasks.md) ，以配置表单对象的脚本或表达式。 下表列表了自适应表单组件支持的所有脚本事件。

<table>
 <tbody>
  <tr>
   <th><strong></strong>组件\事件</th>
   <th>initialize <br /> </th>
   <td>计算</td>
   <td>可见性</td>
   <td>验证</td>
   <td>启用</td>
   <td>值提交</td>
   <td>单击 </td>
   <td>选项</td>
  </tr>
  <tr>
   <td>文本字段</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数字字段</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数值步进器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>电话</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>切换</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>按钮</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>下拉列表</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>图像选择</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>数据输入字段</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>图像</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>面板</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

在JSON中使用事件的一些示例是，在初始化事件时隐藏字段，在值提交事件时配置其他字段的值。 有关为脚本表达式创建事件的详细信息，请参阅自 [适应表单表达式](../../forms/using/adaptive-form-expressions.md)。

以下是上述示例的示例JSON代码。

### 在初始化事件时隐藏字段 {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### 在值提交事件中配置其他字段的值 {#configure-value-of-another-field-on-value-commit-event}

```json
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## 限制自适应表单组件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以向JSON模式元素添加以下限制以限制自适应表单组件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 模式属性</strong></p> </td>
   <td><p><strong>数据类型</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>组件</strong></p> </td>
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
   <td><code>maxLength</code></td>
   <td>字符串</td>
   <td>指定组件中允许的最大字符数。 最大长度必须等于或大于零。</td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定字符的顺序。 如果字符符合指定的模式，则组件接受字符。</p> <p>模式属性映射到相应自适应表单组件的验证模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD模式的所有自适应表单组件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxItems</td>
   <td>字符串</td>
   <td>指定数组中最大项数。 最大项目必须等于或大于零。</td>
   <td> </td>
  </tr>
  <tr>
   <td>minItems</td>
   <td>字符串</td>
   <td>指定数组中最小项数。 最小项目必须等于或大于零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 不支持的构造  {#non-supported-constructs}

自适应表单不支持以下JSON模式构造：

* Null类型
* 合并类型（如任何）和
* OneOf、AnyOf、AllOf和NOT
* 仅支持同质阵列。 因此，项目约束必须是对象而不是数组。

## 常见问题 {#frequently-asked-questions}

**为什么我无法拖动子表单的单个元素（从任何复杂类型生成的结构）以用于可重复的子表单（minOccours或maxOccurs值大于1）?**

在可重复的子表单中，必须使用完整的子表单。 如果只想选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个很长的复杂结构。 如何找到特定元素？**

您有两种选择：

* 滚动浏览树结构
* 使用“搜索”框查找元素

**JSON模式文件的扩展名是什么？**

JSON模式文件的扩展名必须为。模式.json。 例如，&lt;filename>.模式.json。
