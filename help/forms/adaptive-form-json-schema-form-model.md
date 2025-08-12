---
title: 如何为自适应表单设计JSON架构？
description: 了解如何为自适应表单创建JSON架构，并根据该架构创建自适应表单以生成架构投诉数据。
feature: Adaptive Forms, Foundation Components
role: User, Developer
level: Beginner, Intermediate
exl-id: 8eeb9c5e-6866-4bfe-b922-1f028728ef0d
source-git-commit: bf35f847f6f00d21915dfedb10cf38ea74344988
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 6%

---

# 为自适应表单设计 JSON 架构 {#creating-adaptive-forms-using-json-schema}


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| 核心组件 | [单击此处](/help/forms/adaptive-form-core-components-json-schema-form-model.md) |
| 基础 | 本文 |

>[!NOTE]
>
> Adobe建议为[创建新的自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)或[将自适应Forms添加到AEM Sites页面](/help/forms/creating-adaptive-form-core-components.md)使用现代的、可扩展的数据捕获[核心组件](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/adaptive-form-json-schema-form-model.html) |
| AEM as a Cloud Service | 本文 |


## 先决条件 {#prerequisites}

使用JSON架构作为自适应表单的表单模型创作时，需要基本了解JSON架构。 建议在阅读本文之前通读以下内容。

* [创建自适应表单](creating-adaptive-form.md)
* [JSON架构](https://json-schema.org/)

## 使用JSON架构作为表单模型  {#using-a-json-schema-as-form-model}

Adobe Experience Manager表单支持使用现有JSON架构作为表单模型来创建自适应表单。 此JSON架构表示组织中的后端系统生成或使用数据的结构。 您使用的JSON架构应符合[v4规范](https://json-schema.org/draft-04/schema)。

使用JSON架构的主要功能包括：

* 在自适应表单的创作模式下，JSON的结构在内容查找器选项卡中显示为树。 您可以将元素从JSON层次结构拖放到自适应表单中。
* 您可以使用与关联架构兼容的JSON预填充表单。
* 在提交时，用户输入的数据将作为JSON提交，该JSON与关联的架构保持一致。
* 您还可以根据[2012-20 version](https://json-schema.org/draft/2020-12/release-notes)的规范基于JSON架构创建表单。

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
   <td>子类型设置为float<br />的数值字段 </td>
  </tr>
  <tr>
   <td>整数属性<br /> </td>
   <td>子类型设置为integer<br />的数字字段 </td>
  </tr>
  <tr>
   <td>布尔属性<br /> </td>
   <td>交换机<br /> </td>
  </tr>
  <tr>
   <td>对象属性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>数组属性</td>
   <td>可重复面板，最小值和最大值分别等于minItems和maxItems。 仅支持同质数组。 因此，项约束必须是对象，而不是数组。<br /> </td>
  </tr>
 </tbody>
</table>

### 通用架构属性 {#common-schema-properties}

自适应表单使用JSON架构中可用的信息来映射每个生成的字段。 特别是：

* `title`属性用作自适应表单组件的标签。
* `description`属性设置为自适应表单组件的完整描述。
* `default`属性用作自适应表单字段的初始值。
* `maxLength`属性设置为文本字段组件的`maxlength`属性。
* `minimum`、`maximum`、`exclusiveMinimum`和`exclusiveMaximum`属性用于数值框组件。
* 为了支持`DatePicker component`范围，提供了其他JSON架构属性`minDate`和`maxDate`。
* `minItems`和`maxItems`属性用于限制可从面板组件添加或删除的项/字段数。
* `readOnly`属性设置自适应表单组件的`readonly`属性。
* `required`属性将自适应表单字段标记为必填字段，而在面板（其中类型为对象）中，最终提交的JSON数据具有的字段具有对应于该对象的空值。
* 在自适应表单中，`pattern`属性设置为验证模式（正则表达式）。
* JSON架构文件的扩展名必须保留为.schema.json。 例如，&lt;文件名>.schema.json。

## 示例JSON架构 {#sample-json-schema}

>[!BEGINTABS]

>[!TAB JSON架构v4]

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


>[!TAB JSON架构2012-20]


```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/employee.schema.json",
  "$defs": {
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
          "$ref": "#/$defs/personalDetails"
        },
        "projectDetails": {
          "$ref": "#/$defs/projectDetails"
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
          "$ref": "#/$defs/GeneralDetails"
        },
        "Family": {
          "$ref": "#/$defs/Family"
        },
        "Income": {
          "$ref": "#/$defs/Income"
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
            "$ref": "#/$defs/projects"
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
            "$ref": "#/$defs/projectsAdditional"
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
      }
  }
  }
```

>[!ENDTABS]

从JSON架构V4到版本2020-12规范的主要更改包括：

* ID声明为`$id`
* 定义声明为`$defs`

### 可重用架构定义 {#reusable-schema-definitions}

定义键用于标识可重用架构。 可重用架构定义用于创建片段。 <!-- It is similar to identifying complex types in XSD.-->下面给出了具有定义的示例JSON架构：

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

您可以使用&#x200B;**aem:afProperties**&#x200B;属性预配置JSON架构字段以映射到自定义自适应表单组件。 下面列出了一个示例：

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

<!--
## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. You can pre-configure form objects to [evaluate an expression](adaptive-form-expressions.md) on a form event.

Use the aem:afproperties property to preconfigure Adaptive Form expressions or scripts for Adaptive Form components. For example, when the initialize event is triggered, the below code sets value of telephone field and prints a value to the log :

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

You should be a member of the [forms-power-user group](forms-groups-privileges-tasks.md) to configure scripts or expressions for form object. The below table lists all the script events supported for an Adaptive Form component.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Component \ Event</th>
   <th>initialize <br /> </th>
   <td>Calculate</td>
   <td>Visibility</td>
   <td>Validate</td>
   <td>Enabled</td>
   <td>Value Commit</td>
   <td>Click </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Text Field</td>
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
   <td>Numeric Field</td>
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
   <td>Numeric Stepper</td>
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
   <td>Radio Button</td>
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
   <td>Telephone</td>
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
   <td>Switch</td>
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
   <td>Button</td>
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
   <td>Check Box</td>
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
   <td>Drop-down</td>
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
   <td>Image Choice</td>
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
   <td>Date Input Field</td>
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
   <td>Date Picker</td>
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
   <td>Email</td>
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
   <td>File Attachment</td>
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
   <td>Image</td>
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
   <td>Panel</td>
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

Some examples of using events in a JSON are hiding a field on initialize event and configure value of another field on value commit event. For detailed information about creating expressions for the script events, see [Adaptive Form Expressions](adaptive-form-expressions.md).

Here is the sample JSON code for previously mentioned examples.

### Hiding a field on initialize event {#hiding-a-field-on-initialize-event}

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

#### Configure value of another field on value commit event {#configure-value-of-another-field-on-value-commit-event}

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

-->

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
     <li>映射到XSD架构的所有自适应Forms组件 </li>
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

要启用所有基于JSON架构的自适应Forms在提交表单时生成与架构兼容的数据，请执行以下步骤：

1. 转到位于`https://server:host/system/console/configMgr`的Experience Manager Web控制台。
1. 找到&#x200B;**[!UICONTROL 自适应表单和交互通信Web渠道配置]**。
1. 选择以在编辑模式下打开配置。
1. 选中&#x200B;**[!UICONTROL 生成符合架构的数据]**&#x200B;复选框。
1. 保存设置。

![自适应表单和交互式通信Web渠道配置](/help/forms/assets/af-ic-web-channel-configuration.png)


## 不受支持的结构  {#non-supported-constructs}

自适应Forms不支持以下JSON架构结构：

* 空类型
* 合并类型，例如any和
* OneOf、AnyOf、All和NOT
* 仅支持同质数组。 因此，项约束必须是对象，而不是数组。
* $ref中的URI引用

## 常见问题解答 {#frequently-asked-questions}

**为什么我无法为可重复的子表单（minOccours或maxOccurs值大于1）拖动子表单的单个元素（从任何复杂类型生成的结构）？**

在可重复的子表单中，必须使用完整的子表单。 如果只需要选择字段，请使用整个结构并删除不需要的字段。

**我在内容查找器中有一个长且复杂的结构。 如何查找特定元素？**

您有两个选项：

* 滚动浏览树结构
* 使用搜索框查找元素

**JSON架构文件的扩展名应该是什么？**

JSON架构文件的扩展名必须是.schema.json。 例如，&lt;文件名>.schema.json。

## 另请参阅 {#see-also}

{{see-also}}

<!--

>[!MORELIKETHIS]
>
>* [Design XML Schema for an Adaptive Form](/help/forms/adaptive-form-xml-schema-form-model.md)

-->
