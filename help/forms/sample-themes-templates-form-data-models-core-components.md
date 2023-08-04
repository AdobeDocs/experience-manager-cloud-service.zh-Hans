---
title: 核心组件中的示例主题、模板和表单数据模型
description: AEM Forms核心组件提供自适应表单主题、模板和表单数据模型示例
solution: Experience Manager Forms
topic: Administration
role: Admin, User
hide: true
hidefromtoc: true
level: Intermediate
source-git-commit: 2b290be134be05bc15891082e8b54efef62076d0
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 3%

---


# 核心组件中的示例主题、模板和表单数据模型 {#sample-themes-templates-and-data-models}

[!DNL AEM Forms] 核心组件提供现成的示例主题、模板和表单数据模型，以快速创建通用的自适应表单。 这些内容还有助于作者学习的可扩展性、适应性和响应性 [AEM Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 在无缝连接数据库的同时快速创建简单的表单和复杂的表单。

参考内容包中包含的示例主题、模板和表单数据模型包括：

| 模板 | 主题 | 表单数据模型 |
---------|----------|---------
| 基本 | 画布 | Microsoft® Dynamics 365 |
| 空白 | WKND | Salesforce |
| 联系我们 | 画架 |  |
| 联系人详细信息更新 |   |   |
| 同意书 | |  |
| 记录服务请求 |  |  |
| 提供反馈 |  |  |
| 福利登记 |  |   |
| 雇员福利汇总 |   |   |
| 申请帐户对帐单 |   |   |
| 安全检查表 |   |   |
| 质量控制检查 |   |   |
| 购买请求 |  |  |

## 示例主题 {#Sample-Themes}

参考示例主题可帮助作者定义和自定义表单的样式，甚至具有CSS基础知识的作者也可以根据需要自定义主题。

**如何获取这些主题？**
* 要了解这些主题，请执行以下操作 **Formsas a Cloud Service** 环境， [启用自适应Forms核心组件](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html) 并使用 [前端管道](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) 以部署这些主题。
* 将这些主题放在 **AEM 6.5 Forms** 环境， [启用自适应Forms核心组件](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components.html) 并使用 [包管理器](https://experienceleague.corp.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-or-customize-themes-for-adaptive-forms-core-components) 以部署这些主题。

此 **开箱即用** [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 主题描述如下：

![OOTB主题](assets/OOTB-themes.png)

### 画布 {#Canvas}

画布主题是表单的默认主题，强调使用基本颜色、透明度和平面图标。 在下面的屏幕截图中，您可以看到画布主题的外观。

![画布主题](assets/Safety-Inspection-Theme-Canvas.png)

### WKND {#WKND}

WKND主题体现了生动、富于想象力且引人入胜的设计，在您的表单上展示时尚的外观。 主题基于 [WKND站点](https://wknd.site/us/en.html) 这是一个旅游和冒险网站 [Adobe Experience Manager核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html).

![WKND主题](assets/Safety-Inspection-Form-Theme.png)


### 画架 {#Easel}

框架主题有助于创建吸引人且易于设置的表单外观，并且经过自定义以简化并方便用户使用。 画架主题是基于一个概念，即艺术家在创作画作时，使用便携式展位支撑画布。

![画框主题](assets/Safety-Inspection-Theme-Easel.png)

## 示例模板 {#Sample-templates}

模板定义了要在表单中复制的初始表单结构、内容和操作，或者使用与表单类似的模板结构，例如同意表单、福利注册表单等。

**如何获取这些模板？**
您可以通过部署 [基于AEM Archetype 43或更高版本的项目](https://github.com/adobe/aem-project-archetype) 敬您的 **AEM Formsas a Cloud Service** 或 **AEM 6.5** Forms环境。

此 **开箱即用** [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 模板说明如下：

![引用模板](assets/reference-templates-core-components.png)

### 基本 {#Basic}

基本模板可帮助您快速创建注册体验表单。 您还可以使用它来预览的功能 [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction). 它提供了用于逐节呈现数据的向导布局。

![基本模板](assets/Basic-template-desktop-view.png)

### 空白 {#Blank}

使用空白画布模板从头开始创建自适应表单结构、内容和规则。 空白模板中未预先纳入任何表单元件。

![空白模板](assets/Blank-temp-desktop-view.png)

### 联系我们 {#Contact-Us}

联系我们的表单模板用于创建表单，以促进网站访客与表单管理员之间的通信。 用户可以通过表单提交查询、反馈或支持请求。

![联系我们模板](assets/Contact-us-desktop-view.png)

### 联系人详细信息更新 {#Contact-Details-Update}

联系人详细信息更新模板可帮助作者创建用于客户地址和联系人详细信息更新的表单。 该表单还可帮助客户更新与订阅或权益相关的个人信息，以确保无缝通信以及不间断地访问服务或权益。

![Contact-details-update](assets/Contact-details-update.png)

### 同意书 {#Consent-Form}

同意书模板用于创建一个表格，用于从参与特定活动、研究、医疗程序或可能涉及其个人信息或权利的任何情况的参与者处获取法律文档。 该表格确保透明度，保护参与者的权利，并明确理解个人所同意的内容。

![同意书](assets/Consent-form-desktop-view.png)

### 记录服务请求 {#Log-Service-Request}

Log service request template可帮助创建向服务提供程序请求特定于日志的记录服务的表单。 该表单可用作创建票证的正式请求，用于记录事件、活动或数据以监控或跟踪状态。

![记录服务请求模板](assets/Log-service-request-desktop-view.png)


### 提供反馈 {#Give-Feedback}

提供反馈表单模板有助于构建一个表单，以向另一个人员或团队提供建设性的反馈。 该表单有助于确保反馈清晰、具体和可操作，并促进开放式沟通和改进。

![提供反馈模板](assets/Give-feedback-desktop-view.png)


### 福利登记 {#Benefits-Enrollment}

福利登记表单模板用于创建一个表单，以从员工那里收集有关其首选福利和保险选项的基本信息。 它通常伴随年度福利登记期。

![福利登记模板](assets/Benefits-enrollment-form-template.png)


### 员工福利汇总 {#Employee-Benefits-Summary}

员工福利汇总表单模板用于创建表单，以收集有关个人福利的基本详细信息。 它有助于快速准确地评估覆盖范围，为高效的协助和支持提供全面的概述。
![员工福利汇总](assets/Employee-benefits-summary.png)


### 帐户对帐单请求 {#Request-for-Account-Statement}

Request for account statement模板有助于创建表单，以启动获取准确且最新的客户对帐单的过程。 报表提供财务交易、活动的详细记录或使用此表格的客户的其他相关信息。

![Request-for-account-statement](assets/Request-for-account-statment.png)

### 安全检查 {#Safety-Inspection}

安全检查表单模板有助于创建表单以输入安全工作环境的详细信息。 通过使用此表格进行定期检查，可以识别潜在危险。 该表格涵盖多个方面，例如紧急出口、消防安全、电气安全、危险材料、个人防护设备、工作站人机工程学，以保障员工、访客和客户的安全和福祉。

![安全检查表](assets/Safety-inspection-form.png)

### 质量控制检验 {#Quality-Control-Inspection}

质量控制检查表单模板用于创建表单，以评估和记录产品或项目的视觉外观、尺寸、功能、文档、测试结果以及总体质量。 它有助于识别缺陷、不符合项以及确保符合质量标准所必需的纠正措施。

![质量控制检验](assets/Quality-Control-Inspection.png)


### 购买请求 {#Purchase-Request}

采购申请表模板有助于建立表单，以启动采购流程，并允许员工正式请求购买其工作所需的货物或服务。 该表单可捕获基本详细信息，如物料说明、数量、首选供应商（如果适用）、预算分配、采购理由、交货信息和所需批准。

![purchase-request-form](assets/Purchase-request-form.png)

## 引用表单数据模型 {#reference-models}

创建 [自适应表单](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#adaptive-forms-core-components) 基于 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction#adaptive-forms-core-components)，您可以将表单与数据库Microsoft®Dynamics 365和Salesforce服务器连接以启用业务工作流。 例如：

* 在Microsoft®Dynamics 365和Salesforce中写入自适应表单提交的数据。
* 通过表单数据模型中定义的自定义实体在Microsoft®Dynamics 365和Salesforce中写入数据，反之亦然。
* 查询Microsoft®Dynamics 365和Salesforce服务器以获取数据并预填充自适应Forms。
* 从Microsoft®Dynamics 365和Salesforce服务器读取数据。

您可以通过安装 [参考内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* Microsoft® Dynamics 365
* Salesforce

有关使用这些模型的信息，请参阅 [配置Microsoft®Dynamics 365和Salesforce云服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html#configure-dynamics-cloud-service)
