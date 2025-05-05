---
title: 在AEM Forms中使用表单数据模型(FDM)的流程是什么？
description: 添加数据模型对象、服务、创建数据模型对象和子属性、配置服务、使用OData服务的导航属性。
feature: Adaptive Forms, Form Data Model
role: Admin, User
level: Beginner, Intermediate
exl-id: c17c0443-d4dc-41f8-9315-6cc49e6c471f
source-git-commit: 7b31a2ea016567979288c7a8e55ed5bf8dfc181d
workflow-type: tm+mt
source-wordcount: '4146'
ht-degree: 0%

---

# 使用表单数据模型(FDM) {#work-with-form-data-model}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/work-with-form-data-model.html) |
| AEM as a Cloud Service | 本文 |


![数据集成](do-not-localize/data-integeration.png)

表单数据模型(FDM)编辑器提供了直观的用户界面和用于编辑和配置表单数据模型(FDM)的工具。 使用该编辑器，您可以在表单数据模型(FDM)中添加和配置来自关联数据源的数据模型对象、属性和服务。 此外，它还允许您在不使用数据源的情况下创建数据模型对象和属性，并在以后将它们与各自的数据模型对象和属性绑定。 您还可以生成和编辑数据模型对象属性的示例数据，在预览时可用于预填充自适应Forms <!--and interactive communications-->。 您可以测试在表单数据模型(FDM)中配置的数据模型对象和服务，以确保其与数据源正确集成。

如果您是初次使用Forms数据集成，并且尚未配置数据源或创建表单数据模型(FDM)，请参阅以下主题：

* [[!DNL Experience Manager Forms]数据集成](data-integration.md)
* [配置数据源](configure-data-sources.md)
* [创建表单数据模型(FDM)](create-form-data-models.md)

有关您可以使用表单数据模型编辑器执行的各种任务和配置的详细信息，请参阅。

>[!NOTE]
>
>您必须是&#x200B;**fdm-author**&#x200B;和&#x200B;**forms-user**&#x200B;组的成员才能创建和使用表单数据模型(FDM)。 请与您的[!DNL Experience Manager]管理员联系以成为组的成员。

## 添加数据模型对象和服务 {#add-data-model-objects-and-services}

如果您使用数据源创建了表单数据模型(FDM)，则可以使用表单数据模型编辑器来添加数据模型对象和服务，配置其属性，在数据模型对象之间构建关联，以及测试表单数据模型(FDM)和服务。

可在表单数据模型(FDM)中添加来自可用数据源的数据模型对象和服务。 当添加的数据模型对象显示在“模型”选项卡中时，添加的服务显示在“服务”选项卡中。

要添加数据模型对象和服务，请执行以下操作：

1. 登录[!DNL Experience Manager]创作实例，导航到&#x200B;**[!UICONTROL Forms >数据集成]**，然后打开要向其中添加数据模型对象的表单数据模型(FDM)。
1. 在数据源窗格中，展开数据源以查看可用的数据模型对象和服务。
1. 选择要添加到表单数据模型(FDM)的数据模型对象和服务，然后选择&#x200B;**[!UICONTROL 添加选定项]**。

   ![选定对象](assets/selected-objects.png)

   选定的数据模型对象和服务

   **[!UICONTROL 模型]**&#x200B;选项卡以图形方式显示所有数据模型对象及其添加到表单数据模型(FDM)的属性。 每个数据模型对象在表单数据模型(FDM)中用方框表示。

   ![模型选项卡](assets/model-tab.png)

   **[!UICONTROL 模型]**&#x200B;选项卡显示添加的数据模型对象

   >[!NOTE]
   >
   >您可以按住并拖动数据模型对象框，以便在内容区域中组织它们。 在表单数据模型(FDM)中添加的所有数据模型对象在“数据源”窗格中都显示为灰色。

   **[!UICONTROL 服务]**&#x200B;选项卡列出了已添加的服务。

   ![services-tab](assets/services-tab.png)

   **[!UICONTROL 服务]**&#x200B;选项卡显示数据模型服务

   >[!NOTE]
   >
   >除了数据模型对象和服务之外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 有关详细信息，请参阅[使用OData服务的导航属性](#work-with-navigation-properties-of-odata-services)。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存表单模型对象。

   >[!NOTE]
   >
   >您可以使用自适应表单规则调用在表单数据模型(FDM)的“服务”选项卡中配置的服务。 配置的服务在规则编辑器的“调用服务”操作中可用。有关在自适应表单规则中使用这些服务的详细信息，请参阅[规则编辑器](rule-editor.md)中的“调用服务和设置规则值”。

## 创建数据模型对象和子属性 {#create-data-model-objects-and-child-properties}

### 创建数据模型对象 {#create-data-model-objects}

虽然可以从配置的数据源添加数据模型对象，但也可以创建没有数据源的数据模型对象或实体。 如果您尚未在表单数据模型(FDM)中配置数据源，则此功能尤为有用。

要创建没有数据源的数据模型对象，请执行以下操作：

1. 登录[!DNL Experience Manager]创作实例，导航到&#x200B;**[!UICONTROL Forms >数据集成]**，然后打开要在其中创建数据模型对象或实体的表单数据模型(FDM)。
1. 选择&#x200B;**[!UICONTROL 创建实体]**。
1. 在[!UICONTROL 创建数据模型]对话框中，指定数据模型对象的名称并选择&#x200B;**[!UICONTROL 添加]**。 数据模型对象被添加到表单数据模型(FDM)中。 新添加的数据模型对象未绑定到数据源，并且不具有下图中所示的任何属性。

   ![new-entity](assets/new-entity.png)

接下来，您可以在未绑定数据模型对象中添加子属性。

### 添加子属性 {#child-properties}

表单数据模型编辑器允许您在数据模型对象中创建子属性。 创建的属性未绑定到数据源中的任何属性。 您稍后可以将子属性与包含数据模型对象中的另一个属性绑定。

要创建子属性，请执行以下操作：

1. 在表单数据模型中，选择一个数据模型对象，然后选择&#x200B;**[!UICONTROL 创建子属性]**。
1. 在&#x200B;**[!UICONTROL 创建子属性]**&#x200B;对话框中，在&#x200B;**[!UICONTROL 名称]**&#x200B;和&#x200B;**[!UICONTROL 类型]**&#x200B;字段中分别指定属性的名称和数据类型。 您可以选择为属性指定标题和描述。
1. 如果属性是计算属性，则启用计算属性。 计算属性的值是根据规则或表达式计算的。 有关详细信息，请参阅[编辑属性](#properties)。
1. 如果数据模型对象绑定到数据源，则添加的子属性将自动绑定到具有相同名称和数据类型的父数据模型对象的属性。

   要手动绑定子属性与数据模型对象属性，请选择&#x200B;**[!UICONTROL 绑定引用]**&#x200B;字段旁边的浏览图标。 **[!UICONTROL 选择对象]**&#x200B;对话框列出了父数据模型对象的所有属性。 选择要绑定的属性，然后选择勾号图标。 您只能选择与子属性具有相同数据类型的属性。

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;保存子属性，选择&#x200B;**[!UICONTROL 保存]**&#x200B;保存表单数据模型(FDM)。 现在，子属性已添加到数据模型对象中。

创建数据模型对象和属性后，您可以继续基于表单数据模型(FDM)创建自适应Forms <!--and interactive communications-->。 之后，当您具有可用数据源并配置好数据源时，可以将表单数据模型(FDM)与数据源绑定。 绑定在关联的自适应Forms <!--and interactive communications-->中自动更新。 有关使用表单数据模型(FDM)创建自适应Forms <!--and interactive communications-->的更多信息，请参阅[使用表单数据模型](using-form-data-model.md)。

### 绑定数据模型对象和属性 {#bind-data-model-objects-and-properties}

当要与表单数据模型(FDM)集成的数据源可用时，可将其添加到表单数据模型(FDM)，如[更新数据源](create-form-data-models.md#update)中所述。 然后，执行以下操作以绑定未绑定的数据模型对象和属性：

1. 在表单数据模型中，选择要与数据源绑定的未绑定数据源。
1. 选择&#x200B;**[!UICONTROL 编辑属性]**。
1. 在&#x200B;**[!UICONTROL 编辑属性]**&#x200B;窗格中，选择&#x200B;**[!UICONTROL 绑定]**&#x200B;字段旁边的浏览图标。 它会打开&#x200B;**[!UICONTROL 选择对象]**&#x200B;对话框，其中列出了在表单数据模型(FDM)中添加的数据源。

   ![select-object](assets/select-object.png)

1. 展开数据源树并选择要绑定的数据模型对象，然后选择勾号图标。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存属性，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存表单数据模型。 数据模型对象现在与数据源绑定。 请注意，数据模型对象不再标记为“未绑定”。

   ![绑定模型对象](assets/bound-model-object.png)

## 配置服务 {#configure-services}

要读取和写入数据模型对象的数据，请执行以下操作以配置读取和写入服务：

1. 选中数据模型对象顶部的复选框以将其选中，然后选择&#x200B;**[!UICONTROL 编辑属性]**。

   ![编辑 — 属性](assets/edit-properties.png)

   编辑属性以配置数据模型对象的读写服务

   将打开[!UICONTROL 编辑属性]对话框。

   ![edit-properties-2](assets/edit-properties-2.png)

   “编辑属性”对话框

   >[!NOTE]
   >
   >除了数据模型对象和服务之外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 在将OData服务数据源添加到表单数据模型(FDM)时，表单数据模型(FDM)中会提供一个可用于数据模型对象中所有导航属性的服务。 您可以使用此服务读取相应数据模型对象的导航属性。
   >
   >
   >有关使用该服务的详细信息，请参阅[使用OData服务的导航属性](#work-with-navigation-properties-of-odata-services)。

1. 切换&#x200B;**[!UICONTROL 顶层对象]**&#x200B;以指定数据模型对象是否为顶层模型对象。

   在表单数据模型(FDM)中配置的数据模型对象可用于基于表单数据模型(FDM)的自适应表单内容浏览器中的“数据模型对象”选项卡。 在两个数据模型对象之间添加关联时，与关联的数据模型对象嵌套在&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中的关联数据模型对象下。 如果嵌套数据模型是顶级对象，则它还会单独出现在&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中。 因此，您会看到其中的两个条目，一个位于嵌套层次结构内，另一个位于嵌套层次结构外，这可能会使表单作者感到困惑。 要使关联的数据模型对象仅显示在嵌套层次结构中，请禁用“顶级对象”属性。

1. 为选定的数据模型对象选择读取和写入服务。 将显示服务的参数。

   ![读写服务](assets/read-write-services.png)

   为员工数据源配置的读写服务

1. 为读取服务参数选择![aem_6_3_edit](assets/edit.svg)以将参数绑定到用户配置文件属性、请求属性或文本值[&#128279;](#bindargument)，并指定绑定值。
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存参数，选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存属性，选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存表单数据模型(FDM)。

### 绑定读取服务参数 {#bindargument}

根据绑定值，将读取服务参数绑定到用户配置文件属性、请求属性或文本值。 该值将作为参数传递给服务，以从数据源获取与指定值关联的详细信息。

#### 文本值 {#literal-value}

从&#x200B;**[!UICONTROL 绑定到]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 文本]**，然后在&#x200B;**[!UICONTROL 绑定值]**&#x200B;字段中输入值。 从数据源中检索与值关联的详细信息。 使用此选项可检索与静态值关联的详细信息。

在此示例中，与&#x200B;**4367655678**&#x200B;关联的详细信息作为`mobilenum`参数的值从数据源中检索。 如果传递手机号码参数的值，则关联的详细信息可以包括客户名称、客户地址和城市等属性。

![文本值](assets/fdm_binding_literal_new.png)

#### 用户配置文件属性 {#user-profile-attribute}

从&#x200B;**[!UICONTROL 绑定到]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 用户配置文件属性]**，然后在&#x200B;**[!UICONTROL 绑定值]**&#x200B;字段中输入属性名称。 基于属性名称，从数据源检索登录[!DNL Experience Manager]实例的用户详细信息。

在&#x200B;**[!UICONTROL 绑定值]**&#x200B;字段中指定的属性名称必须包含完整的绑定路径，直到用户的属性名称为止。 打开以下URL以访问CRXDE上的用户详细信息：

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![用户配置文件](assets/binding_crxde_user_profile_new.png)

在此示例中，在`grios`用户的&#x200B;**[!UICONTROL 绑定值]**&#x200B;字段中指定`profile.empid`。

![编辑参数](assets/edit_argument_user_profile_new.png)

`id`参数接受用户配置文件的`empid`属性的值，并将其作为参数传递给读取服务。 它会从与登录用户关联的`empid`的员工数据模型对象中读取并返回关联属性的值。

#### 请求属性 {#request-attribute}

使用请求属性从数据源检索关联的属性。

1. 从&#x200B;**[!UICONTROL 绑定到]**&#x200B;下拉菜单中选择&#x200B;**[!UICONTROL 请求属性]**，然后在&#x200B;**[!UICONTROL 绑定值]**&#x200B;字段中输入属性名称。

1. 为head.jsp创建一个[叠加](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/overlays.html?lang=en#developing)。 要创建叠加，请打开CRX DE并将`https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`文件复制到`https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`

   >[!NOTE]
   >
   > * 如果使用静态模板，请将head.jsp覆盖在：
   >   `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   > * 如果您使用可编辑的模板，请在以下位置叠加aftemplatedpage.jsp：
   >   `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. 为请求属性设置[!DNL paramMap]。 例如，将以下代码加入apps文件夹中的.jsp文件中：

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   例如，使用以下代码从数据源检索petid的值：


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

根据请求中指定的属性名称，从数据源检索详细信息。

例如，在请求中将attribute指定为`petid=100`将检索与数据源中的属性值关联的属性。

## 添加关联 {#add-associations}

通常，数据源中的数据模型对象之间会建立关联。 关联可以是一对一或一对多。 例如，可以有多个与员工关联的家属。 它称为一对多关联，由`1:n`在连接关联的数据模型对象的行上描述。 但是，如果关联为给定员工ID返回唯一的员工姓名，则称为一对一关联。

当您将数据源中的关联数据模型对象添加到表单数据模型(FDM)时，它们的关联将保留并以箭头线连接的方式显示。 您可以在表单数据模型(FDM)中跨不同数据源的数据模型对象之间添加关联。

>[!NOTE]
>
>JDBC数据源中的预定义关联不会保留在表单数据模型(FDM)中。 您必须手动创建它们。

要添加关联，请执行以下操作：

1. 选中数据模型对象顶部的复选框以将其选中，然后选择&#x200B;**[!UICONTROL 添加关联]**。 将打开“添加关联”对话框。

   ![添加关联](assets/add-association.png)

   >[!NOTE]
   >
   >除了数据模型对象和服务之外，OData服务元数据文档还包括定义两个数据模型对象之间的关联的导航属性。 在表单数据模型(FDM)中添加关联时，可以使用这些导航属性。 有关详细信息，请参阅[使用OData服务的导航属性](#work-with-navigation-properties-of-odata-services)。

   将打开[!UICONTROL 添加关联]对话框。

   ![add-association-2](assets/add-association-2.png)

   “添加关联”对话框

1. 在“添加关联”窗格中：

   * 指定关联的标题。
   * 选择关联类型 — **[!UICONTROL 一对一]**&#x200B;或&#x200B;**[!UICONTROL 一对多]**。
   * 选择要关联的数据模型对象。
   * 选择读取服务以从选定的模型对象中读取数据。 此时将显示读取服务参数。 编辑以更改参数（如有必要），并将其绑定到要关联的数据模型对象的属性。

   在以下示例中， Dependents数据模型对象的读取服务的默认参数是`dependentid`。

   ![add-association-example](assets/add-association-example.png)

   依赖项读取服务的默认参数是依赖的

   但是，参数必须是关联数据模型对象（在此示例中为`Employeeid`）之间的公共属性。 因此，`Employeeid`参数必须绑定到Employee数据模型对象的`id`属性，才能从Dependents数据模型对象获取关联的依赖项详细信息。

   ![add-association-example-2](assets/add-association-example-2.png)

   已更新参数和绑定

   选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存参数。

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;保存关联，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;保存表单数据模型(FDM)。
1. 根据需要重复这些步骤以创建更多关联。

>[!NOTE]
>
>所添加的关联将显示在数据模型对象框中，其中包含指定的标题和连接关联的数据模型对象的线。
>
>通过选中关联对应的复选框并选择&#x200B;**[!UICONTROL 编辑关联]**，可以编辑关联。

![已添加关联](assets/added-association.png)

## 编辑属性 {#properties}

您可以编辑数据模型对象的属性、其属性以及在表单数据模型(FDM)中添加的服务。

要编辑属性，请执行以下操作：

1. 选中表单数据模型(FDM)中数据模型对象、属性或服务旁边的复选框。
1. 选择&#x200B;**[!UICONTROL 编辑属性]**。 将打开选定模型对象、属性或服务的&#x200B;**[!UICONTROL 编辑属性]**&#x200B;窗格。

   * **[!UICONTROL 数据模型对象]**：指定读取和写入服务并编辑参数。
   * **[!UICONTROL 属性]**：指定属性的类型、子类型和格式。 您还可以指定selected属性是否为数据模型对象的主键。
   * **[!UICONTROL 服务]**：指定服务的输入模型对象、输出类型和参数。 对于Get服务，您可以指定它是否应返回数组。

     ![edit-properties-service](assets/edit-properties-service.png)

   获取服务的“编辑属性”对话框

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;保存属性，然后选择&#x200B;**[!UICONTROL 保存]**&#x200B;保存表单数据模型(FDM)。

### 创建计算属性 {#computed}

计算属性是根据规则或表达式计算其值的属性。 使用规则，您可以将计算属性的值设置为文本字符串、数字、数学表达式的结果或表单数据模型(FDM)中其他属性的值。

例如，您可以创建一个计算属性&#x200B;**FullName**，其值是现有&#x200B;**FirstName**&#x200B;和&#x200B;**LastName**&#x200B;属性串联的结果。 为此，请执行以下操作：

1. 创建一个名为`FullName`且数据类型为字符串的新属性。
1. 启用&#x200B;**[!UICONTROL Computed]**&#x200B;并选择&#x200B;**[!UICONTROL Done]**&#x200B;以创建该属性。

   ![已计算](assets/computed.png)

   将创建FullName计算属性。 请注意属性旁边的图标以描述计算属性。

   ![计算属性](assets/computed-prop.png)

1. 选择FullName属性并选择&#x200B;**[!UICONTROL 编辑规则]**。 此时将打开一个规则编辑器窗口。
1. 在规则编辑器窗口中，选择&#x200B;**[!UICONTROL 创建]**。 将打开&#x200B;**[!UICONTROL 设置值]**&#x200B;规则窗口。

   从选择选项下拉列表中，选择&#x200B;**[!UICONTROL 数学表达式]**。 其他可用选项为&#x200B;**[!UICONTROL 表单数据模型对象]**&#x200B;和&#x200B;**[!UICONTROL 字符串]**。

1. 在数学表达式中，在第一个和第二个对象中分别选择&#x200B;**[!UICONTROL FirstName]**&#x200B;和&#x200B;**[!UICONTROL LastName]**。 选择&#x200B;**[!UICONTROL 加]**&#x200B;作为运算符。

   选择&#x200B;**[!UICONTROL 完成]**，然后选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以关闭规则编辑器窗口。 该规则与以下内容类似。

   ![规则](assets/rule.png)

1. 在表单数据模型(FDM)上，选择&#x200B;**[!UICONTROL 保存]**。 已配置计算属性。

## 使用OData服务的导航属性 {#work-with-navigation-properties-of-odata-services}

在OData服务中，导航属性用于定义两个数据模型对象之间的关联。 这些属性是在实体类型或复杂类型上定义的。 例如，在从示例[TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/) OData示例服务的元数据文件中进行的以下提取中，人员实体包含三个导航属性 — Friends、BestFriend和Trips。

有关导航属性的详细信息，请参阅[OData文档](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536)。

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

在表单数据模型(FDM)中配置OData服务时，实体容器中的所有导航属性均可通过表单数据模型(FDM)中的服务使用。 在此TripPin OData服务示例中，`Person`实体容器中的三个导航属性可以使用表单数据模型(FDM)中的一个`GET LINK`服务进行读取。

下面重点介绍了表单数据模型(FDM)中的`GET LINK of Person /People`服务，它是TripPin OData服务的`Person`实体中三个导航属性的组合服务。

![nav-prop-service](assets/nav-prop-service.png)

将`GET LINK`服务添加到表单数据模型(FDM)的“服务”选项卡后，可以编辑属性以选择要在服务中使用的输出模型对象和导航属性。 例如，以下示例中的以下`GET LINK of Person /People`服务使用Trip作为输出模型对象，并将导航属性作为Trips。

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>**NavigationPropertyName**&#x200B;参数的&#x200B;**[!UICONTROL 默认值]**&#x200B;字段中可用的值取决于&#x200B;**[!UICONTROL 返回数组的状态？]**&#x200B;切换按钮。 启用后，它将显示收藏集类型的导航属性。

在此示例中，您还可以选择输出模型对象作为Person，选择导航属性参数作为Friends或BestFriend (具体取决于&#x200B;**[!UICONTROL Return数组是？]**&#x200B;已启用或已禁用)。

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

同样，在表单数据模型(FDM)中添加关联时，您可以选择一个`GET LINK`服务并配置其导航属性。 但是，若要能够选择导航属性，请确保&#x200B;**[!UICONTROL 绑定到字段]**&#x200B;设置为&#x200B;**[!UICONTROL 文本]**。

![add-association-nav-prop](assets/add-association-nav-prop.png)

## 生成和编辑示例数据 {#sample}

表单数据模型(FDM)编辑器允许您为表单数据模型(FDM)中的所有数据模型对象属性（包括计算属性）生成示例数据。 它是一组符合为每个属性配置的数据类型的随机值。 您还可以编辑并保存数据，即使重新生成示例数据也会保留这些数据。

执行以下操作可生成和编辑示例数据：

1. 打开表单数据模型(FDM)并选择&#x200B;**[!UICONTROL 编辑示例数据]**。 它在“编辑示例数据”窗口中生成并显示示例数据。

   ![生成示例数据](assets/form_data_model_generate_sample_data_new.png)

1. 在&#x200B;**[!UICONTROL 编辑示例数据]**&#x200B;窗口中，根据需要编辑数据，然后选择&#x200B;**[!UICONTROL 保存]**。

<!--Next, you can use the sample data to prefill and test interactive communications based on the form data model. For more information, see [Use form data model](using-form-data-model.md).-->

## 测试数据模型对象和服务 {#test-data-model-objects-and-services}

您的表单数据模型(FDM)已配置，但在投入使用之前，您可能需要测试配置的数据模型对象和服务是否按预期工作。 要测试数据模型对象和服务，请执行以下操作：

1. 在表单数据模型(FDM)中选择数据模型对象或服务，然后分别选择&#x200B;**[!UICONTROL 测试模型对象]**&#x200B;或&#x200B;**[!UICONTROL 测试服务]**。

   将打开“测试表单数据模型”窗口。

   ![test-data-model](assets/test-data-model.png)

1. 在[!UICONTROL 测试表单数据模型]窗口中，从输入窗格中选择要测试的数据模型对象或服务。

1. 在测试代码中指定一个参数值，然后选择&#x200B;**[!UICONTROL 测试]**。 成功的测试会在“输出”窗格中返回输出。

   ![测试结果](assets/test_results_form_data_model_new.png)

同样，也可以在表单数据模型(FDM)中测试其他数据模型对象和服务。

## 自动验证输入数据 {#automated-validation-of-input-data}

表单数据模型(FDM)在调用DermisBridge API时（根据表单数据模型中提供的验证条件）验证作为输入接收的数据。 验证基于在用于调用API的查询对象中设置的`ValidationOptions`标志。

可以将标志设置为以下任意值：

* **FULL**： FDM基于所有约束执行验证
* **关**：无验证
* **BASIC**： FDM根据“必需”和“可空”约束执行验证

如果没有为`ValidationOptions`标志设置值，则对输入数据执行&#x200B;**BASIC**&#x200B;验证。

以下是将验证标志设置为&#x200B;**FULL**&#x200B;的示例：

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>为输入数据中的属性提供的值必须与为元数据文档中的属性定义的数据类型匹配。\
>如果值与为属性定义的数据类型不匹配，则DermisBridge API显示异常，而不考虑`ValidationOptions`标志的值。 如果将日志级别设置为“调试”，则会将错误记录到&#x200B;**error.log**&#x200B;文件中。

表单数据模型(FDM)根据数据类型约束列表验证输入数据。 输入数据的约束列表可能会因数据源而异。

下表列出了基于数据源的输入数据的约束条件：

<table>
 <tbody> 
  <tr> 
   <td>约束</td> 
   <td>描述</td> 
   <td>输入数据源</td> 
  </tr> 
  <tr> 
   <td>必填</td> 
   <td>如果为true，则参数必须包含在输入数据中。</td> 
   <td>Swagger、WSDL和数据库</td> 
  </tr> 
  <tr> 
   <td>可空</td> 
   <td>如果为true，则可将输入数据中的参数值设置为Null。</td> 
   <td>WSDL、Odata和数据库</td> 
  </tr> 
  <tr> 
   <td>最大值</td> 
   <td>指定数值的上限。 指定为上限的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>最小值</td> 
   <td>指定数字值的下限。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>指定数值的上限。 指定为上限的最大值不得分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>指定数字值的下限。 不得将指定为下限的最小值分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>minlength</td> 
   <td>指定字符串中包含的字符数的下限。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>指定字符串中包含的字符数的上限。 指定为上限的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger、WSDL、Odata和数据库</td> 
  </tr> 
  <tr> 
   <td>模式</td> 
   <td>指定固定字符序列。 仅当字符符合指定的模式时，才能成功验证输入字符串。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>指定数组中的最小项数。 指定为下限的最小值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>指定数组中的最大项数。 指定为上限的最大值也可以分配给输入数据中的参数。</td> 
   <td>Swagger和WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>如果为true，则数组的所有元素在输入数据中必须是唯一的。</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>枚举（字符串）<br /> <br /> </td> 
   <td>将输入数据中的参数值限制为一组固定的字符串值。 它必须是一个数组，其中至少有一个元素，每个元素都是唯一的。</td> 
   <td>Swagger、WSDL和Odata</td> 
  </tr> 
  <tr> 
   <td>枚举（数字）<br /> <br /> </td> 
   <td>将输入数据中的参数值限制为一组固定的数值。 它必须是一个数组，其中至少有一个元素，每个元素都是唯一的。</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

在此示例中，根据Swagger文件中定义的最大值、最小值和所需约束来验证输入数据。 仅当存在订单ID且其值介于1-10之间时，输入数据才符合验证标准。

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that must be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

如果输入数据不符合验证标准，则显示例外。 如果日志级别设置为&#x200B;**Debug**，则会在&#x200B;**error.log**&#x200B;文件中记录错误。 例如，

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## 后续步骤 {#next-steps}

您有一个工作表单数据模型(FDM)，现在可以在自适应Forms <!--and interactive communications-->工作流中使用。 有关详细信息，请参阅[使用表单数据模型(FDM)](using-form-data-model.md)。
