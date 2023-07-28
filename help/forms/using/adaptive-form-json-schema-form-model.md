---
title: 如何使用JSON架构创建自适应Forms？
description: 了解如何使用JSON架构作为表单模型创建自适应表单。 您可以使用现有JSON架构创建自适应表单。 深入了解JSON模式示例，在JSON模式定义中预配置字段，限制自适应表单组件的可接受值，并了解不受支持的结构。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 5%

---

# 使用JSON架构创建自适应表单 {#creating-adaptive-forms-using-json-schema}

<span class="preview"> Adobe建议使用现代化的、可扩展的数据捕获 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 对象 [创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 这些组件在创建自适应Forms方面实现了重大进步，确保了令人印象深刻的用户体验。 本文介绍了使用基础组件创作自适应Forms的旧方法。 </span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html) |
| AEM 6.5 | 本文 |


## 前提条件 {#prerequisites}

使用JSON架构作为自适应表单的表单模型创作时，需要基本了解JSON架构。 建议在阅读本文之前通读以下内容。

* [创建自适应表单](creating-adaptive-form.md)
* [JSON架构](https://json-schema.org/)

## 使用JSON架构作为表单模型  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] 支持使用现有JSON架构作为表单模型来创建自适应表单。 此JSON架构表示组织中的后端系统生成或使用数据的结构。 您使用的JSON架构应符合 [v4规范](https://json-schema.org/draft-04/schema).

使用JSON架构的主要功能包括：

* 在自适应表单的创作模式下，JSON的结构在“内容查找器”选项卡中显示为树。 您可以将元素从JSON层次结构拖放到自适应表单中。
* 您可以使用与关联架构兼容的JSON预填充表单。
* 在提交时，用户输入的数据将作为JSON提交，该JSON与关联的架构保持一致。

JSON架构包含简单和复杂的元素类型。 元素具有向元素添加规则的属性。 将这些元素和属性拖动到自适应表单上时，会自动映射到相应的自适应表单组件。

JSON元素与自适应表单组件的映射如下所示：

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
     <li>enumNames中列出的值将显示在拖放框中。</li>
     <li>枚举中列出的值用于计算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>带格式约束的字符串属性。 例如，电子邮件和日期。</p> <p>语法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>当类型为字符串且格式为电子邮件时，将映射电子邮件组件。</li>
     <li>当类型为字符串且格式为hostname时，将映射带验证的文本框组件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 文本字段<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>数字属性<br /> </td>
   <td>子类型设置为float的数字字段<br /> </td>
  </tr>
  <tr>
   <td>integer属性<br /> </td>
   <td>子类型设置为整数的数字字段<br /> </td>
  </tr>
  <tr>
   <td>布尔属性<br /> </td>
   <td>开关<br /> </td>
  </tr>
  <tr>
   <td>对象属性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>数组属性</td>
   <td>可重复面板，最小值和最大值分别等于minItems和maxItems。 仅支持同质数组。 因此项约束必须是对象，而不是数组。<br /> </td>
  </tr>
 </tbody>
</table>

### 通用架构属性 {#common-schema-properties}

自适应表单使用JSON架构中可用的信息来映射每个生成的字段。 特别是：

* 此 `title` 属性用作自适应表单组件的标签。
* 此 `description` 属性设置为自适应表单组件的完整描述。
* 此 `default` 属性用作自适应表单字段的初始值。
* 此 `maxLength` 属性设置为 `maxlength` 文本字段组件的属性。
* 此 `minimum`， `maximum`， `exclusiveMinimum`、和 `exclusiveMaximum` 属性用于数值框组件。
* 要支持的范围，请执行以下操作 `DatePicker component` 其他JSON架构属性 `minDate` 和 `maxDate` 提供……
* 此 `minItems` 和 `maxItems` 属性用于限制可从面板组件添加或删除的项目/字段数。
* 此 `readOnly` 属性设置 `readonly` 自适应表单组件的属性。
* 此 `required` 属性将自适应表单字段标记为必填字段，而在面板（其中类型为对象）中，最终提交的JSON数据具有的字段具有对应于该对象的空值。
* 此 `pattern` 属性设置为自适应表单中的验证模式（正则表达式）。
* JSON架构文件的扩展名必须保留为.schema.json。 例如， &lt;filename>.schema.json。

## 示例JSON架构 {#sample-json-schema}

以下是JSON架构的示例。

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

### 可重用架构定义 {#reusable-schema-definitions}

定义键用于标识可重用架构。 可重用架构定义用于创建片段。 它类似于识别XSD中的复杂类型。 下面给出了具有定义的示例JSON架构：

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

上例定义了一个客户记录，其中每个客户都有一个送货地址和账单地址。 两个地址的结构相同（地址具有街道地址、城市和州/省），因此最好不要重复这些地址。 它还使得添加和删除字段对于任何未来的更改都非常容易。

## 在JSON架构定义中预配置字段 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem：afProperties** 属性，用于预配置要映射到自定义自适应表单组件的JSON架构字段。 下面列出了一个示例：

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

JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，并使用自适应表单脚本模型API。 您可以预配置表单对象，以 [计算表达式](adaptive-form-expressions.md) 在表单事件中。

使用aem：afproperties属性为自适应表单组件预配置自适应表单表达式或脚本。 例如，当触发初始化事件时，以下代码设置telephone字段的值并将值打印到日志：

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

您应该是 [表单 — 超级用户组](forms-groups-privileges-tasks.md) 为表单对象配置脚本或表达式。 下表列出了自适应表单组件支持的所有脚本事件。

<table>
 <tbody>
  <tr>
   <th><strong></strong>组件\事件</th>
   <th>初始化 <br /> </th>
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
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数值字段</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>数值步进器</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>单选按钮</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>电话</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>开关</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>按钮</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>复选框</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>下拉面板</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>图像选择</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>数据输入字段</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>日期选取器</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>电子邮件</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>文件附件</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>图像</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>面板</td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="“是”勾选图标" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

在JSON中使用事件的一些示例包括：在初始化事件上隐藏字段，以及在值提交事件上配置另一个字段的值。 有关为脚本事件创建表达式的详细信息，请参见 [自适应表单表达式](adaptive-form-expressions.md).

以下是前面提到的示例的JSON代码示例。

### 在初始化事件中隐藏字段 {#hiding-a-field-on-initialize-event}

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

#### 在值提交事件上配置另一个字段的值 {#configure-value-of-another-field-on-value-commit-event}

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

您可以向JSON架构元素添加以下限制，以限制自适应表单组件可以接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 架构属性</strong></p> </td>
   <td><p><strong>数据类型</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>组件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定数值和日期的上限。 默认情况下，包含最大值。</p> </td>
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
   <td><p>指定数值和日期的下限。 默认情况下，将包含最小值。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>布尔值</p> </td>
   <td><p>如果为true，则表单的组件中指定的数值或日期必须小于为maximum属性指定的数值或日期。</p> <p>如果为false，则表单的组件中指定的数值或日期必须小于或等于为maximum属性指定的数值或日期。</p> </td>
   <td>
    <ul>
     <li>数值框</li>
     <li>数值步进器</li>
     <li>日期选取器</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>布尔值</p> </td>
   <td><p>如果为true，则表单的组件中指定的数值或日期必须大于为最小属性指定的数值或日期。</p> <p>如果为false，则表单的组件中指定的数值或日期必须大于或等于为minimum属性指定的数值或日期。</p> </td>
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
   <td><p>指定组件中允许的最小字符数。 最小长度必须等于或大于零。</p> </td>
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
   <td><p>指定字符的顺序。 如果字符符合指定的模式，则组件接受这些字符。</p> <p>pattern属性映射到相应自适应表单组件的验证模式。</p> </td>
   <td>
    <ul>
     <li>映射到XSD架构的所有自适应表单组件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>字符串</td>
   <td>指定数组中的最大项数。 最大项数必须等于或大于零。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>字符串</td>
   <td>指定数组中的最小项数。 最小项数必须等于或大于零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>



## 启用符合架构的数据 {#enablig-schema-compliant-data}

要启用自适应表单以在表单提交时生成与架构兼容的数据，请执行以下步骤：

1. 转到Experience ManagerWeb控制台，网址为 `https://server:host/system/console/configMgr`.
1. 定位 **[!UICONTROL 自适应表单和互动通信Web渠道配置]**.
1. 点按以在编辑模式下打开配置。
1. 选择 **[!UICONTROL 生成符合架构的数据]** 复选框。
1. 保存设置。

![自适应表单和交互式通信Web渠道配置](/help/forms/using/assets/af-ic-web-channel-configuration.png)

## 不受支持的结构  {#non-supported-constructs}

自适应表单不支持以下JSON架构结构：

* 空类型
* 合并类型，例如any和
* OneOf、AnyOf、All和NOT
* 仅支持同质数组。 因此，项约束必须是对象，而不是数组。

## 常见问题 {#frequently-asked-questions}

**为什么我无法为可重复的子表单（minOccours或maxOccurs值大于1）拖动子表单的单个元素（从任何复杂类型生成的结构）？**

在可重复的子表单中，必须使用完整的子表单。 如果只需要选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个长且复杂的结构。 如何查找特定元素？**

您有两个选项：

* 滚动浏览树结构
* 使用搜索框查找元素

**JSON架构文件的扩展名应该是什么？**

JSON架构文件的扩展名必须是.schema.json。 例如， &lt;filename>.schema.json。
