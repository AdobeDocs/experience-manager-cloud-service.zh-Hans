---
Title: How to Integrate Marketo Engage with AEM Forms?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 4%

---


# 将Marketo Engage与AEM Forms集成

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

将AEM Forms与[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)集成后，用户可以利用Marketo Engage的功能，从捕获的数据创建业务逻辑并自动化工作流，包括智能营销活动和电子邮件自动化。 配置的表单可以将捕获的数据发送到Marketo Engage进行处理。

## 将Marketo Engage与表单集成的优势

下面是将AEM表单与Adobe Marketo Engage连接的一些优势：

* **简化的集成**：将表单与Marketo Engage连接后，无需创建单独的表单数据模型。 集成过程简单明了，并且对用户友好。
* **自动数据捕获**：它有助于自动捕获表单提交并将其存储在Marketo中，从而消除手动数据输入并减少错误。

* **潜在客户管理**：通过将表单提交直接集成到营销数据库中，可以更好地跟踪和培养潜在客户，从而简化潜在客户管理流程。

* **促销活动效果提高**：它使用表单数据来分析和优化营销活动，从而提高整体效果和投资回报率(ROI)。

* **Analytics和报表**：它有助于在Marketo中获取对强大分析和报表工具(如Munchkin)的访问权限，以衡量表单和营销活动的有效性。

* **跟进自动化**：它有助于自动化跟进电子邮件和表单提交触发的工作流，确保与潜在客户及时沟通。

## 与其他表单解决方案相比，使用AEM Forms的主要优势

下表概述了选择AEM Forms而不是其他替代表单解决方案的几个原因：

| **功能** | **AEM Forms** | **其他表单解决方案** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **自定义项** | 允许添加特定的自定义函数、调整表单操作和修改字段行为以增强表单交互和复杂工作流 | 不支持自定义 |
| **规则编辑器** | 支持用于添加逻辑和条件的内置规则编辑器。 | 不支持规则编辑器 |
| **布局选项** | 支持多个布局选项 | 布局选项有限 |
| **预填充服务** | 提供预填充服务以自动填充表单数据。 | 无可用的预填充服务 |
| **嵌入站点** | 可以使用iFrame嵌入站点 | 无法使用iFrame嵌入站点 |
| **轻松与站点集成** | 无需额外学习；AEM Forms使用与站点相同的技能 | 可能需要额外学习 |
| **数据提交** | 可以将数据提交到各种平台，并提供多个连接器，例如连接到SharePoint、连接到OneDrive、连接到Salesforce等。 | 可以将数据提交到有限的连接器，例如提交到Salesforce |

## 将Marketo Engage与表单集成的注意事项

将Marketo Engage与AEM Forms集成时的一些注意事项：

* AEM仅支持各种Marketo数据库中的People(Leads)数据库。
* Marketo允许创建[10个自定义对象](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)作为用户定义的对象，以存储Leads中标准字段以外的专用数据，从而支持独特的业务需求。
* 仅当自定义对象与Lead数据库关联时，AEM才能访问这些对象

## 将Marketo Engage与表单集成的先决条件

以下是将Marketo Engage连接到AEM Forms的先决条件：

* 有效的Adobe Marketo Engage许可证
* 用于[检索客户端ID和客户端密钥](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)以创建云配置的Marketo Engage的工作实例。

## 创建云服务配置以将AEM Forms (自适应Forms)与Marketo Engage连接

![工作流](/help/forms/assets/workflow-marketo-1.png)

云配置可将您的Experience Manager实例连接到Adobe Marketo Engage实例。 执行以下步骤以创建Marketo Engage云配置：

1. 转到&#x200B;**工具** > **Cloud Service** > **Marketo Engage**。

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

1. 打开文件夹以托管配置，然后单击&#x200B;**创建**。 出现&#x200B;**创建Marketo Engage配置**&#x200B;窗口。

   >[!NOTE]
   >
   > 您还可以[为云服务配置](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations)配置文件夹。

1. 指定要连接到服务的配置和凭据的&#x200B;**标题**。 您可以从Adobe Marketo Engage仪表板检索身份验证凭据：
   * **客户端ID**&#x200B;和&#x200B;**客户端密钥**&#x200B;在&#x200B;**管理员** > **集成** > **启动点**&#x200B;中可用，方法是选择自定义服务并单击&#x200B;**查看详细信息**。
   * **标识URL**&#x200B;在&#x200B;**管理员** > **集成** > **Web服务**&#x200B;中可用，作为&#x200B;**REST API**&#x200B;部分中的&#x200B;**标识**。

1. 单击&#x200B;**连接**。  连接成功后，将显示`Authentication Successful`消息。
1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以保存云配置设置。

![Marketo Engage云配置](/help/forms/assets/marketo-engage-cloud-configuration.png)

现在，您可以使用创建的云服务配置将Marketo Engage数据源连接到自适应表单。

## 下一步

您已创建云服务配置以将Adobe Marketo Engage与AEM Forms集成。 现在，您可以集成：
* [带Marketo Engage的新自适应表单](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [带Marketo Engage的现有自适应表单](/help/forms/use-marketo-engage-data-source-in-form.md)

## 相关文章

{{af-submit-action}}

## 另请参阅

{{marketo-engage-see-also}}



