---
title: '如何将数据库连接到 [!DNL AEM Forms] as a Cloud Service? '
seo-title: AEM Forms Data Integration
description: 您可以从中检索数据并将数据保存到RESTful Web服务、基于SOAP的Web服务和OData服务 [!DNL AEM Forms] as a Cloud Service。 该服务提供了专用工具，用于检索、测试、验证数据并将数据发送到各种类型的数据源。
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 将数据源连接到 Cloud Service {#aem-forms-data-integration}

![数据集成](do-not-localize/data-integeration.png)

企业基础架构包括不同的后端系统或数据源，如数据库、 Web服务、REST服务、OData服务和CRM解决方案。 他们共同开发了一个信息系统，该系统为企业应用程序提供数据，以执行日常业务。 另一方面，应用程序会捕获数据，并将其发回以更新数据源。

[!DNL AEM Forms] 自适应Forms和交互式通信等应用程序需要与数据源集成，以便在呈现表单和创建交互式通信时获取客户数据。 有时，会根据自适应Forms中的用户输入从数据源获取数据。 此外，可以回写提交的自适应表单数据，以更新各个数据源。

虽然分布式模块化系统有其自身的优势，但挑战在于集成和创建跨数据源的数据关联。 数据集成是功能高效的企业基础架构的关键，该基础架构具有与业务数据交换应用程序相连的不同数据源。

## 数据集成概述 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 数据集成允许配置不同数据源并将其与 [!DNL AEM Forms]. 它提供了直观的用户界面，以创建跨连接数据源的业务实体和服务的统一数据表示模式。 统一表示形式称为表单数据模型，它是JSON模式的扩展。 表单数据模型中的实体称为数据模型对象。 表单数据模型允许您：

* 从连接的数据源访问数据模型对象、属性和服务。
* 创建自定义数据模型对象和属性
* 在数据源内和数据源之间构建数据模型对象之间的关联。
* 调用数据模型对象服务，以查询数据源或从数据源写入数据。

创建表单数据模型后，您可以在各种自适应表单和交互式通信工作流中使用该模型，例如：

* 基于表单数据模型创建自适应Forms和交互式通信
* 预填充自适应Forms和来自已配置数据源的交互式通信
* 使用自适应表单规则调用数据源服务/操作
* 将提交的自适应表单数据写入数据源

## 数据集成入门 {#get-started-with-data-integration}

实施数据集成的第一步是识别和配置数据源，这些数据源存储您要在自适应Forms和交互式通信用例中利用的信息。 接下来，您需要创建一个表单数据模型，该模型使用来自一个或多个数据源的数据模型对象、属性和服务。 您可以基于表单数据模型创建自适应Forms和交互式通信，其中交互式通信中的自适应表单字段或占位符绑定到相应的数据源属性。

[!DNL AEM Forms] 还允许您创建与数据源无关的表单数据模型，并稍后将表单数据模型中的数据模型对象和属性与数据源关联或绑定。 它消除了您在处理表单数据模型时对数据源的任何依赖。

请查看以下内容，以开始、了解和实施数据集成。

* [配置数据源](configure-data-sources.md)
* [创建表单数据模型](create-form-data-models.md)
* [使用表单数据模型](work-with-form-data-model.md)
* [使用表单数据模型](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支持关系数据库。
