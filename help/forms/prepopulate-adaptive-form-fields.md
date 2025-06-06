---
title: 如何预填自适应表单字段？
description: 使用现有数据预填自适应表单的字段，用户可通过使用其社交个人资料登录在表单中预填基本信息。
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 1%

---

# 预填自适应表单字段{#prefill-adaptive-form-fields}

>[!NOTE]
>
> Adobe建议为[创建新的自适应Forms](/help/forms/creating-adaptive-form-core-components.md)或[将自适应Forms添加到AEM Sites页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)使用现代的、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)。 这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应Forms的旧方法。

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

## 简介 {#introduction}

您可以使用现有数据预填自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 要在自适应表单中预填充数据，请按照预填充自适应Forms数据结构所遵循的格式，将用户数据作为预填充XML/JSON提供。

## 预填充数据的结构 {#the-prefill-structure}

自适应表单可以包含绑定字段和未绑定字段的组合。 绑定字段是从“内容查找器”选项卡拖动的字段，在字段编辑对话框中包含非空的`bindRef`属性值。 未绑定的字段直接从Sidekick的组件浏览器中拖动，并且具有空的`bindRef`值。

您可以预填自适应表单的绑定和未绑定字段。 预填充数据包含afBoundData和afUnBoundData部分，用于预填充自适应表单的绑定和未绑定字段。 `afBoundData`部分包含绑定字段和面板的预填充数据。 此数据必须与关联的表单模型架构兼容：

- 对于使用[XFA表单模板](#xfa-based-af)的自适应Forms，请使用与XFA模板的数据架构兼容的预填充XML。
- 对于使用[XML架构](#xml-schema-af)的自适应Forms，请使用与XML架构结构兼容的预填充XML。
- 对于使用[JSON架构](#json-schema-based-adaptive-forms)的自适应Forms，请使用与JSON架构兼容的预填充JSON。
- 对于使用FDM架构的自适应Forms，请使用与FDM架构兼容的预填充JSON。
- 对于具有[无表单模型](#adaptive-form-with-no-form-model)的自适应Forms，没有绑定数据。 每个字段都是未绑定的字段，并使用未绑定的XML预填充。

### 预填充XML结构示例 {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### 预填充JSON结构示例 {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

对于同名的绑定字段或未绑定字段，所有字段中都会填充在XML标记或JSON对象中指定的数据。 例如，表单中的两个字段映射到预填充数据中的名称`textbox`。 在运行时，如果第一个文本框字段包含“A”，则“A”会自动填充到第二个文本框中。 此链接称为自适应表单字段的实时链接。

### 使用XFA表单模板的自适应表单 {#xfa-based-af}

基于XFA的自适应Forms的预填充XML和提交的XML的结构如下：

- **预填充XML结构**：基于XFA的自适应表单的预填充XML必须与XFA表单模板的数据架构兼容。 要预填充未绑定的字段，请将预填充XML结构包装到`/afData/afBoundData`标记中。

- **提交的XML结构**：当不使用预填充XML时，提交的XML包含`afData`包装器标记中绑定和未绑定字段的数据。 如果使用预填充XML，则提交的XML具有与预填充XML相同的结构。 如果预填充XML以`afData`根标记开头，则输出XML也具有相同的格式。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从架构根标记（如`employeeData`）开始，则提交的XML也以`employeeData`标记开始。

Prefill-Submit-Data-ContentPackage.zip

[获取文件](assets/prefill-submit-data-contentpackage.zip)
包含预填充数据和已提交数据的示例

### 基于XML架构的自适应Forms  {#xml-schema-af}

基于XML架构的自适应Forms的预填充XML和提交的XML的结构如下：

- **预填充XML结构**：预填充XML必须符合关联的XML架构。 要预填充未绑定字段，请将预填充XML结构包装到/afData/afBoundData标记中。
- **提交的XML结构**：如果未使用预填充XML，则提交的XML包含`afData`包装器标记中绑定和未绑定字段的数据。 如果使用预填充XML，则提交的XML具有与预填充XML相同的结构。 如果预填充XML以`afData`根标记开头，则输出XML具有相同的格式。 如果预填充XML没有`afData/afBoundData`包装器，而是直接从架构根标记（如`employeeData`）开始，则提交的XML也以`employeeData`标记开始。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

对于模型为XML架构的字段，数据将预填充到`afBoundData`标记中，如下面的示例XML所示。 它可用于使用一个或多个未绑定的文本字段预填自适应表单。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>建议不要在绑定面板(通过从Sidekick或数据源选项卡拖动组件而创建的具有非空`bindRef`的面板)中使用未绑定字段。 它可能会导致这些未绑定字段的数据丢失。 此外，建议整个表单中的字段名称是唯一的，特别是对于未绑定的字段。

#### 不具有afData和afBoundData包装器的示例 {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### 基于JSON架构的自适应Forms {#json-schema-based-adaptive-forms}

对于基于JSON模式的自适应Forms，预填充JSON和提交的JSON的结构描述如下。 有关详细信息，请参阅[使用JSON架构创建自适应Forms](adaptive-form-json-schema-form-model.md)。

- **预填充JSON结构**：预填充JSON必须与关联的JSON架构兼容。 或者，如果您还希望预填充未绑定字段，也可以将其包装到/afData/afBoundData对象中。
- **提交的JSON结构**：如果未使用预填充JSON，则提交的JSON包含afData包装器标记中绑定和未绑定字段的数据。 如果使用预填充JSON，则提交的JSON具有与预填充JSON相同的结构。 如果预填充JSON以afData根对象开头，则输出JSON具有相同的格式。 如果预填充JSON没有afData/afBoundData包装器，而是直接从架构根对象（如用户）开始，则提交的JSON也将从用户对象开始。

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

对于使用JSON架构模型的字段，数据预填充到afBoundData对象中，如下面的示例JSON所示。 它可用于使用一个或多个未绑定的文本字段预填自适应表单。 以下是使用`afData/afBoundData`包装器的数据示例：

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

以下是没有`afData/afBoundData`包装器的示例：

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> 在绑定面板(通过从Sidekick或数据源选项卡拖动组件而创建的具有非空bindRef的面板)中使用未绑定字段，是&#x200B;**不**&#x200B;推荐的，因为它可能会导致未绑定字段的数据丢失。 建议在表单中保留唯一的字段名称，尤其是未绑定的字段。
>

### 无表单模型的自适应表单 {#adaptive-form-with-no-form-model}

对于没有表单模型的自适应Forms，所有字段的数据都在`<afUnboundData> tag`的`<data>`标记下。

此外，请注意以下事项：

为各个字段提交的用户数据的XML标记是使用字段名称生成的。 因此，字段名称必须是唯一的。

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## 配置预填充服务 {#configuring-prefill-service-using-configuration-manager}

使用&#x200B;**默认预填充服务配置**&#x200B;的`alloweddataFileLocations`属性设置数据文件的位置或数据文件位置的正则表达式。

以下JSON文件显示了一个示例：

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

要设置配置的值，请[使用AEM SDK生成OSGi配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=zh-Hans#generating-osgi-configurations-using-the-aem-sdk-quickstart)和[将配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=zh-Hans#deployment-process)部署到您的Cloud Service实例。

>[!NOTE]
>
> - 默认情况下，所有类型的自适应Forms（XSD、XDP、JSON、FDM，且不基于表单模型）都允许通过crx文件预填充。 仅允许对JSON和XML文件使用预填充。
> - crx协议负责预填充的数据安全性，因此默认情况下允许使用。 使用通用正则表达式通过其他协议进行预填充可能会导致漏洞。 在配置中，指定用于保护数据的安全URL配置。

## 可重复面板的奇特案例 {#the-curious-case-of-repeatable-panels}

通常，绑定（表单架构）和未绑定字段是在同一自适应表单中创作的，但如果绑定是可重复的，则以下是一些例外情况：

- 使用XFA表单模板、XSD、JSON架构或FDM架构的自适应Forms不支持未绑定的可重复面板。
- 请勿在绑定可重复面板中使用未绑定字段。

>[!NOTE]
>
> 根据经验，如果绑定字段和未绑定字段在用户填充的数据中相交，请勿将其混合使用。 如果可能，您应该修改架构或XFA表单模板，并为未绑定的字段添加一个条目，这样该字段也会绑定，并且其数据就像提交数据中的其他字段一样可用。

## 支持预填充用户数据的协议 {#supported-protocols-for-prefilling-user-data}

配置了有效的正则表达式后，可通过以下协议使用预填充数据格式的用户数据预填充自适应Forms：

### crx://协议 {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

指定的节点必须具有名为`jcr:data`的属性并保存数据。

### file://协议  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

引用的文件必须位于同一服务器上。

### https://协议 {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### service://协议 {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME是指OSGI预填充服务的名称。 请参阅[创建并运行预填充服务](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service)。
- 标识符是指OSGI预填充服务获取预填充数据所需的任何元数据。 登录用户的标识符是可以使用的元数据的示例。

>[!NOTE]
>
> 不支持传递身份验证参数。

### 在slingRequest中设置数据属性 {#setting-data-attribute-in-slingrequest}

您还可以在`slingRequest`中设置`data`属性，其中`data`属性是包含XML或JSON的字符串，如下面的示例代码所示（示例为XML）：

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

您可以编写包含所有数据的简单XML或JSON字符串，并在slingRequest中进行设置。 可以在任何组件的渲染器JSP中轻松完成此操作，您想要将这些组件包含在可设置slingRequest数据属性的页面中。

例如，您希望为具有特定标题类型的页面使用特定设计。 要实现此目的，您可以编写自己的`header.jsp`，将其包含在页面组件中并设置`data`属性。

另一个很好的示例是用例，您想要在通过Facebook、Twitter或LinkedIn等社交帐户登录时预填充数据。 在这种情况下，您可以在`header.jsp`中包含一个简单的JSP，它从用户帐户中获取数据并设置数据参数。

预填充页面component.zip

[获取文件](assets/prefill-page-component.zip)
页面组件中的prefill.jsp示例

## [!DNL AEM Forms]自定义预填充服务 {#aem-forms-custom-prefill-service}

您可以对这些方案使用自定义预填充服务，在这些方案中，您会不断从预定义的源中读取数据。 预填充服务从定义的数据源中读取数据，并使用预填充数据文件的内容预填充自适应表单的字段。 它还有助于您将预填数据与自适应表单永久关联。

### 创建并运行预填充服务 {#create-and-run-a-prefill-service}

预填充服务是一种OSGi服务，通过OSGi捆绑包进行打包。 您可以创建OSGi捆绑包，将其上传并安装到[!DNL AEM Forms]捆绑包。 开始创建捆绑包之前：

- [下载 [!DNL AEM Forms] 客户端SDK](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html)
- 下载样板包

- 将数据（预填充数据）文件放入crx存储库中。 可以将文件放置在crx-repository的\contents文件夹中的任意位置。

[获取文件](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### 创建预填充服务 {#create-a-prefill-service}

样板包（示例预填充服务包）包含[!DNL AEM Forms]预填充服务的示例实现。 在代码编辑器中打开样板包。 例如，在Eclipse中打开样板项目进行编辑。 在代码编辑器中打开样板包后，请执行以下步骤，以创建该服务。

1. 打开src\main\java\com\adobe\test\Prefill.java文件进行编辑。
1. 在代码中，将值设置为：

   - `nodePath:`指向crx存储库位置的节点路径变量包含数据（预填充）文件的路径。 例如， /content/prefilldata.xml
   - `label:` label参数指定服务的显示名称。 例如，默认预填充服务

1. 保存并关闭`Prefill.java`文件。
1. 将`AEM Forms Client SDK`包添加到样板项目的生成路径。
1. 编译项目并为包创建.jar。

#### 启动并使用预填充服务 {#start-and-use-the-prefill-service}

要启动预填充服务，请将JAR文件上载到[!DNL AEM Forms] Web控制台，然后激活该服务。 现在，该服务开始出现在自适应Forms编辑器中。 要将预填充服务与自适应表单关联，请执行以下操作：

1. 在Forms编辑器中打开自适应表单，然后打开表单容器的“属性”面板。
1. 在属性控制台中，导航到[!DNL AEM Forms]容器>基本>预填充服务。
1. 选择默认预填充服务并单击&#x200B;**[!UICONTROL 保存]**。 服务与表单相关联。

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/cn/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/cn/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->