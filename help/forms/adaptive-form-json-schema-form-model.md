---
title: 为自适应表单设计 JSON 架构
description: 瞭解如何使用JSON結構描述作為表單模型來建立最適化Forms。 您可以使用現有的JSON結構描述來建立最適化Forms。 深入瞭解JSON結構描述範例、在JSON結構描述定義中預先設定欄位、限制最適化表單元件的可接受值，以及瞭解不支援的建構。
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 8eeb9c5e-6866-4bfe-b922-1f028728ef0d
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 4%

---

# 为自适应表单设计 JSON 架构 {#creating-adaptive-forms-using-json-schema}

## 前提条件 {#prerequisites}

使用JSON結構描述作為表單模型來製作調適型表單需要基本瞭解JSON結構描述。 建議您先閱讀下列內容，再閱讀本文。

* [建立最適化表單](creating-adaptive-form.md)
* [JSON結構描述](https://json-schema.org/)

## 使用JSON結構描述作為表單模型  {#using-a-json-schema-as-form-model}

Adobe Experience Manager表單支援使用現有JSON結構描述作為表單模型來建立調適型表單。 此JSON結構描述代表組織中後端系統產生或使用資料的結構。 您使用的JSON結構描述應符合 [v4規格](https://json-schema.org/draft-04/schema).

使用JSON結構描述的主要功能包括：

* 在最適化表單的製作模式下，JSON的結構會在「內容尋找器」標籤中顯示為樹狀結構。 您可以從JSON階層拖曳元素，並將其新增至最適化表單。
* 您可以使用與相關結構描述相容的JSON預先填入表單。
* 在提交時，使用者輸入的資料會以JSON形式提交，且符合相關聯的結構描述。

JSON結構描述包含簡單和複雜的元素型別。 元素具有將規則新增至元素的屬性。 將這些元素和屬性拖曳至最適化表單時，會自動對應至對應的最適化表單元件。

JSON元素與最適化表單元件的對應如下：

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
   <th><strong>JSON元素、屬性或屬性</strong></th>
   <th><strong>最適化表單元件</strong></th>
  </tr>
  <tr>
   <td><p>具有enum和enumNames限制的字串屬性。</p> <p>語法，</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>下拉式元件：</p>
    <ul>
     <li>enumNames中列出的值會顯示在拖放方塊中。</li>
     <li>列舉中列出的值會用於計算。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>具有格式限制的字串屬性。 例如，電子郵件和日期。</p> <p>語法，</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>當型別為字串且格式為電子郵件時，會對映電子郵件元件。</li>
     <li>當型別為字串且格式為主機名稱時，會對應具有驗證的Textbox元件。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> 文字欄位<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>數字屬性<br /> </td>
   <td>子型別設定為浮點數的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>integer屬性<br /> </td>
   <td>子型別設定為整數的數值欄位<br /> </td>
  </tr>
  <tr>
   <td>布林值屬性<br /> </td>
   <td>开关<br /> </td>
  </tr>
  <tr>
   <td>物件屬性<br /> </td>
   <td>面板<br /> </td>
  </tr>
  <tr>
   <td>陣列屬性</td>
   <td>可重複面板，最小值和最大值分別等於minItems和maxItems。 僅支援同質陣列。 因此，專案限制必須是物件，而不是陣列。<br /> </td>
  </tr>
 </tbody>
</table>

### 通用結構描述屬性 {#common-schema-properties}

最適化表單會使用JSON結構描述中可用的資訊來對應每個產生的欄位。 尤其是：

* 此 `title` 屬性可作為最適化表單元件的標籤。
* 此 `description` 屬性已設定為最適化表單元件的詳細說明。
* 此 `default` 屬性會作為最適化表單欄位的初始值。
* 此 `maxLength` 屬性已設為 `maxlength` 文字欄位元件的屬性。
* 此 `minimum`， `maximum`， `exclusiveMinimum`、和 `exclusiveMaximum` 屬性用於Numeric box元件。
* 若要支援範圍 `DatePicker component` 其他JSON結構描述屬性 `minDate` 和 `maxDate` 提供……
* 此 `minItems` 和 `maxItems` 屬性可用來限制可從面板元件新增或移除的專案/欄位數量。
* 此 `readOnly` 屬性會設定 `readonly` 最適化表單元件的屬性。
* 此 `required` 屬性會將「調適型表單」欄位標籤為必填欄位，而在面板（其中type為object型別）中，最終提交的JSON資料中會有欄位具有對應於該物件的空白值。
* 此 `pattern` 屬性已設定為最適化表單中的驗證模式（規則運算式）。
* JSON結構描述檔案的副檔名必須保留為.schema.json。 例如， &lt;filename>.schema.json.

## 範例JSON結構描述 {#sample-json-schema}

以下是JSON結構描述的範例。

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

### 可重複使用的結構描述定義 {#reusable-schema-definitions}

定義索引鍵可用來識別可重複使用的結構描述。 可重複使用的結構描述定義用於建立片段。 <!-- It is similar to identifying complex types in XSD.--> 具有定義的JSON結構描述範例如下：

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

上述範例會定義客戶記錄，其中每個客戶都有送貨和帳單地址。 兩個地址的結構相同（地址有街道地址、城市和州/省），因此最好不要複製地址。 此外，日後變更時也能輕鬆新增和刪除欄位。

## JSON結構描述定義中的預先設定欄位 {#pre-configuring-fields-in-json-schema-definition}

您可以使用 **aem：afProperties** 屬性來預先設定JSON結構描述欄位，以對應至自訂最適化表單元件。 範例如下：

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

<!--- ## Configure scripts or expressions for form objects  {#configure-scripts-or-expressions-for-form-objects}

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

## 限制最適化表單元件的可接受值 {#limit-acceptable-values-for-an-adaptive-form-component}

您可以將下列限制新增至JSON結構描述元素，以限制最適化表單元件可接受的值：

<table>
 <tbody>
  <tr>
   <td><p><strong> 結構描述屬性</strong></p> </td>
   <td><p><strong>数据类型</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
   <td><p><strong>组件</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定數值和日期的上限。 依預設，會包含最大值。</p> </td>
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
   <td><p>指定數值和日期的下限。 依預設，會包含最小值。</p> </td>
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
   <td><p>如果為true，則表單元件中指定的數值或日期必須小於為最大屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須小於或等於為最大屬性指定的數值或日期。</p> </td>
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
   <td><p>如果為true，則表單元件中指定的數值或日期必須大於為最小屬性指定的數值或日期。</p> <p>如果為false，則表單元件中指定的數值或日期必須大於或等於為最小屬性指定的數值或日期。</p> </td>
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
   <td><p>指定元件中允許的最小字元數。 最小長度必須等於或大於零。</p> </td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>字符串</td>
   <td>指定元件中允許的最大字元數。 最大長度必須等於或大於零。</td>
   <td>
    <ul>
     <li>文本框</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>字符串</p> </td>
   <td><p>指定字元順序。 如果字元符合指定的模式，元件會接受字元。</p> <p>pattern屬性對應至對應的最適化表單元件的驗證模式。</p> </td>
   <td>
    <ul>
     <li>對應至XSD結構描述的所有Adaptive Forms元件 </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>字符串</td>
   <td>指定陣列中專案的最大數量。 最大專案數必須等於或大於零。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>字符串</td>
   <td>指定陣列中專案的最小數量。 最小專案數必須等於或大於零。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 不支援的結構  {#non-supported-constructs}

最適化Forms不支援下列JSON結構描述：

* 空值型別
* 聯合型別，例如any和
* OneOf、AnyOf、AllOf和NOT
* 僅支援同質陣列。 因此，專案限制必須是物件，而不是陣列。

## 常见问题 {#frequently-asked-questions}

**為什麼我無法為可重複的子表單（minOccours或maxOccurs值大於1）拖曳子表單的個別元素（由任何複雜型別產生的結構）？**

在可重複的子表單中，您必須使用完整的子表單。 如果您只想使用選擇性欄位，請使用整個結構並刪除不需要的結構。

**我在內容尋找器中有個長而複雜的結構。 如何找到特定元素？**

您有兩個選項：

* 捲動瀏覽樹狀結構
* 使用搜尋方塊來尋找元素

**JSON結構描述檔案的副檔名應該為何？**

JSON結構描述檔案的副檔名必須是.schema.json。 例如， &lt;filename>.schema.json.
