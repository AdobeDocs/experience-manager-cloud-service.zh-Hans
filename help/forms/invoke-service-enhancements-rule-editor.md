---
title: 对基于核心组件的表单的Invoke service VRE有哪些增强？
description: 对规则编辑器的Invoke服务的增强
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
keywords: 在VRE中调用服务增强功能，使用调用服务填充下拉选项，使用调用服务输出设置可重复面板，使用调用服务输出设置面板，使用调用服务的输出参数验证其他字段。
source-git-commit: f77e0cd03a63200cb86fada780f2fecff5fadf94
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 2%

---


# 在基于核心组件的表单的可视规则编辑器中使用调用服务

<span class="preview">这是一项预发布功能，可通过我们的[预发布渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features)访问。</span>

自适应表单中的可视化规则编辑器支持&#x200B;**调用服务**&#x200B;功能，该功能允许您从为您的实例配置的表单数据模型(FDM)列表中选择服务。 您可以将表单字段直接映射到服务的输入参数。 要将表单字段映射到输出参数，请使用指定表单数据模型服务的事件有效负荷选项。 此外，可视规则编辑器允许您基于其输出响应为&#x200B;**调用服务**&#x200B;操作创建成功和失败处理程序的规则。 成功处理程序管理&#x200B;**调用服务**&#x200B;操作的成功执行，而失败处理程序处理发生的任何错误。

### 在表单的规则编辑器中使用“调用服务”的优势

在自适应表单的规则编辑器中使用“调用服务”操作的优点很少：

* **简化的集成**：可视规则编辑器简化了将外部服务或API集成到自适应Forms中的过程。 通过使用&#x200B;**调用服务**，您可以轻松地将表单连接到各种数据源和服务，而无需复杂的编码，从而使表单集成更高效。

* **动态响应处理**：您可以根据&#x200B;**调用服务**&#x200B;的输出响应来管理成功和错误响应，从而允许表单动态地响应不同的场景。 它确保表单能够恰当地处理各种情况，提高灵活性和控制能力。

* **增强的用户交互**：在规则编辑器中使用&#x200B;**调用服务**&#x200B;可在表单中启用实时验证，从而提供更好的用户体验。 它还可确保数据在服务器端得到准确验证，从而减少错误并提高表单可靠性。

## 为成功和失败响应调用服务处理程序

>[!NOTE]
>
> 您只能对基于核心组件的表单使用&#x200B;**调用服务**&#x200B;成功和失败处理程序。 基于基础组件的Forms不支持&#x200B;**调用服务**&#x200B;成功和失败处理程序。

可视规则编辑器允许您基于其输出响应为&#x200B;**调用服务**&#x200B;操作创建成功和失败处理程序的规则。 下图描述了自适应表单的可视化规则编辑器中的&#x200B;**调用服务**：

![调用服务处理程序](/help/forms/assets/invoke-service-rule-editor.png)

要添加成功或失败处理程序，请分别单击&#x200B;**[!UICONTROL 添加成功处理程序]**&#x200B;或&#x200B;**[!UICONTROL 添加失败处理程序]**。

单击&#x200B;**[!UICONTROL 添加成功处理程序]**&#x200B;后，将显示&#x200B;**[!UICONTROL 调用服务成功处理程序]**&#x200B;规则编辑器，允许您指定规则或逻辑来管理操作成功时的&#x200B;**调用服务**&#x200B;输出响应。 即使不定义条件，您也可以指定规则；但是，您可以通过单击&#x200B;**[!UICONTROL 添加条件]**&#x200B;选项为成功处理程序添加条件。

![调用服务成功处理程序](/help/forms/assets/invoke-service-success-handler.png)

您可以添加多个规则以处理&#x200B;**调用服务**&#x200B;操作的成功响应：

![多个成功处理程序](/help/forms/assets/invoke-service-multiple-success-handlers.png){width=50%， height=50%}

同样，您可以添加规则以在操作不成功时处理&#x200B;**调用服务**&#x200B;输出响应。 下图显示了&#x200B;**[!UICONTROL 调用服务失败处理程序]**&#x200B;规则编辑器：

![调用服务失败处理程序](/help/forms/assets/invoke-service-failue-handler.png)

您还可以添加多个规则来处理来自&#x200B;**调用服务**&#x200B;操作的不成功响应。

**在服务器**&#x200B;上启用错误验证}功能允许作者在设计要在服务器上运行的自适应表单时添加验证。

## 在规则编辑器中使用调用服务的先决条件

在规则编辑器中使用&#x200B;**调用服务**&#x200B;之前，必须满足以下先决条件：

* 确保已配置数据源。 有关配置数据源的说明，[单击此处](/help/forms/configure-data-sources.md)。
* 使用配置的数据源创建表单数据模型。 有关创建表单数据模型的指导，[单击此处](/help/forms/create-form-data-models.md)。
* 确保为您的环境启用了核心组件。 有关如何为您的环境启用核心组件的详细说明，请[单击此处](/help/forms/enable-adaptive-forms-core-components.md)。

## 通过不同的用例探索调用服务

可视规则编辑器的&#x200B;**调用服务**&#x200B;允许您执行若干有用的操作。 您可以使用此插件填充下拉选项、设置可重复或简单的面板以及验证表单字段，所有这些操作都基于&#x200B;**调用服务**&#x200B;的输出响应。 因此，可增强表单的灵活性和交互性。

下表描述了一些可使用&#x200B;**调用服务**&#x200B;的情况：

| **用例** | **描述** |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **使用调用服务的输出填充下拉选项** | 根据从调用服务输出中检索的数据动态填充下拉列表选项。 [单击此处](#use-case-1-populate-dropdown-values-using-the-output-of-invoke-service)查看实施。 |
| **使用调用服务的输出设置可重复的面板** | 使用调用服务输出中的数据配置可重复面板，从而允许使用动态面板。 [单击此处](#use-case-2-set-repeatable-panel-using-output-of-invoke-service)查看实施。 |
| **使用调用服务的输出设置面板** | 使用调用服务输出中的特定值设置面板的内容或可见性。 [单击此处](#use-case-3-set-panel-using-output-of-invoke-service)查看实施。 |
| **使用调用服务的输出参数来验证其他字段** | 使用调用服务中的特定输出参数来验证表单字段。 [单击此处](#use-case-4-use-output-parameter-of-invoke-service-to-validate-other-fields)查看实施。 |

创建一个`Get Information`表单，该表单根据在`Pet ID`文本框中输入的输入检索值。 下面的屏幕截图显示了以下用例中使用的表单：

![获取信息表单](/help/forms/assets/get-information-form.png)

**表单字段**

将以下字段添加到表单：
* **输入Pet ID**： Textbox
* **选择照片URL**：下拉列表
* **标记**：面板
   * 名称：文本框
   * ID：文本框
* **类别**：面板
   * 名称：文本框
* **提交**：“提交”按钮

>[!NOTE]
>
> 在表单字段的&#x200B;**属性**&#x200B;对话框的&#x200B;**绑定引用**&#x200B;字段中，选择![foldersearch_18](assets/folder-search-icon.svg)，然后导航以选择您在表单数据模型(FDM)中添加的二进制属性。

**配置面板**

将面板设置为具有以下约束的重复面板：
* 最小值：1
* 最大值：4

您可以根据自己的需要调整重复面板的值。

**数据源**

在此示例中，[Swagger Petstore](https://petstore.swagger.io/) API用于配置数据源。 已为[getPetById](https://petstore.swagger.io/#/pet/getPetById)服务配置[表单数据模型](/help/forms/create-form-data-models.md)，该服务根据输入的ID检索宠物详细信息。

让我们使用[Swagger Petstore](https://petstore.swagger.io/) API中的[addPet](https://petstore.swagger.io/#/pet/addPet)服务发布以下JSON：

```
{
        "id": 101,
        "category": {
            "id": 1,
            "name": "Labrador"
        },
        "name": "Lisa",
        "photoUrls": [
            "https://example.com/photos/lisa1.jpg",
            "https://example.com/photos/lisa2.jpg"
        ],
        "tags": [
            {
                "id": 1,
                "name": "vaccinated"
            },
            {
                "id": 2,
                "name": "friendly"
            },
            {
                "id": 3,
                "name": "house-trained"
            }
        ],
        "status": "available"
    }
```


规则和逻辑是使用`Pet ID`文本框上的规则编辑器中的&#x200B;**调用服务**&#x200B;操作实现的，用于演示上述用例。

现在，让我们详细探讨每个用例的实施。

### 用例1：使用调用服务的输出填充下拉值

此用例演示了如何根据`Invoke Service`的输出动态填充下拉选项。

#### 实施

要实现此目的，请在`Pet ID`文本框上创建规则以调用`getPetById`服务。 在规则中，将&#x200B;**[!UICONTROL 添加成功处理程序]**&#x200B;中`photo-url`下拉列表的`enum`属性设置为`photoUrls`。

![设置下拉值](/help/forms/assets/set-dropdownoption.png)

#### 输出

在`Pet ID`文本框中输入`101`以根据输入的值动态填充下拉选项。

![结果](/help/forms/assets/output1.png)

### 用例2：使用调用服务的输出设置可重复面板

此用例演示如何根据&#x200B;**调用服务**&#x200B;的输出动态填充可重复面板。

#### 注意事项

* 确保可重复面板的名称与要为其设置面板的&#x200B;**调用服务**&#x200B;的参数匹配。
* 面板针对相应的&#x200B;**调用服务**&#x200B;字段返回的值数重复。

#### 实施

在`Pet ID`文本框上创建规则以调用`getPetById`服务。 在&#x200B;**[!UICONTROL 添加成功处理程序]**&#x200B;中，添加另一个成功处理程序响应。 在规则中将`tags`面板的值设置为`tags`。

![为可重复面板创建规则](/help/forms/assets/create-rule-repeatable-panel.png)

#### 输出

在`Pet ID`文本框中输入`101`以根据输入值动态填充可重复面板。

![输出](/help/forms/assets/output2.png)

### 用例3：使用调用服务的输出设置面板

此用例演示了如何根据&#x200B;**调用服务**&#x200B;的输出动态设置面板的值。

#### 注意事项

* 请确保面板的名称与要为其设置面板的&#x200B;**调用服务**&#x200B;的参数匹配。
* 该面板会针对由相应的Invoke Service字段返回的值数重复执行。

#### 实施

在`Pet ID`文本框上创建规则以调用`getPetById`服务。 在&#x200B;**[!UICONTROL 添加成功处理程序]**&#x200B;中，添加另一个成功处理程序响应。 在规则中将`categoryname`文本框的值设置为`category.name`。

![为可重复面板创建规则](/help/forms/assets/set-panel-values.png)

#### 输出

在`Pet ID`文本框中输入`101`以根据输入值动态填充面板。

![输出](/help/forms/assets/output3.png)

### 用例4：使用调用服务的输出参数验证其他字段

此用例演示如何使用&#x200B;**调用服务**&#x200B;的输出来动态验证其他表单字段。

#### 实施

在`Pet ID`文本框上创建规则以调用`getPetById`服务。 在&#x200B;**[!UICONTROL 添加失败处理程序]**&#x200B;中，添加失败处理程序响应。 如果输入的`Pet ID`不正确，请隐藏&#x200B;**提交**&#x200B;按钮。

![失败处理程序](/help/forms/assets/create-rule-failure-handler.png)

#### 输出

在`Pet ID`文本框中输入`102`，且&#x200B;**提交**&#x200B;按钮已隐藏。

![输出](/help/forms/assets/output4.png)

## 常见问题解答

**问：如果我使用Invoke Service创建了规则，然后升级到核心组件的最新版本，会发生什么情况？**

**A：**&#x200B;升级到最新版本的核心组件时，**调用服务**&#x200B;规则会自动更新到最新的用户界面，因为它向后兼容。

**问：我是否可以添加多个规则来处理调用服务操作的成功或失败响应？**

**A：**&#x200B;是，您可以添加多个规则来处理&#x200B;**调用服务**&#x200B;操作的成功或失败响应。

## 相关文章

* [配置数据源](configure-data-sources.md)
* [创建表单数据模型(FDM)](create-form-data-models.md)
* [使用表单数据模型(FDM)](work-with-form-data-model.md)
* [使用表单数据模型(FDM)](using-form-data-model.md)


## 其他资源

{{see-also-rule-editor}}

