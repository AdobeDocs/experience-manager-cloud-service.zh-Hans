---
title: AEM 6.5 Forms与AEM云服务之间的更改内容
description: 您是Experience Manager Forms用户并且希望升级到Adobe Experience Manager Formsas a Cloud Service吗？ 了解在升级或迁移到Cloud Service之前最显着的更改。
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 5%

---

# 对现有Adobe Experience Manager Forms用户的显着更改  {#notable-changes-for-existing-AEM-Forms-users}

与Adobe Experience Manager FormsOn-Premise和Adobe Experience Manager Forms FormsOn-Premise相比， as a Cloud Service对现有功能做出了一些显着更改 [!DNL Adobe-Managed Service] 环境。 主要区别如下：

* 该服务提供本地和云原生开发环境。 您可以使用 [本地开发环境](setup-local-development-environment.md) 在将这些资产部署到云环境之前，要开发和测试您的自定义代码、组件、模板、主题、自适应Forms和其他资产，请执行以下操作： 它有助于加快开发过程。
* [!DNL AEM] 因为Cloud Service随附了内置CDN。 其主要目的是通过从浏览器附近的边缘 CDN 节点提供可缓存的内容来减少延迟。它经过全面的管理和配置，可提供最佳的 AEM 应用程序性能。
* 云原生环境没有Web控制台（配置管理器）。 您可以使用 [[!DNL AEM Forms] as a Cloud ServiceSDK生成配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) 和CI/CD管线到 [部署配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) 到Cloud Service实例。

* 本地化的自适应Forms的URL约定现在支持在URL中指定区域设置。 新的URL约定允许在调度程序或CDN上缓存本地化的表单。 在Cloud Service环境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 请求自适应表单的本地化版本，而不是 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建议使用Dispatcher或CDN缓存。 这有助于提高预填充表单的渲染速度。
* 预填充服务将数据与客户端上的自适应表单合并。 它有助于缩短预填自适应表单所需的时间。 您始终可以配置以在Adobe Experience Manager FormsServer上运行合并操作。
* 默认情况下，电子邮件仅支持HTTP和HTTP协议。 [联系支持团队](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 启用用于发送电子邮件的端口，并为环境启用SMTP协议。
* Adobe Experience Manager Forms as a Cloud Service为您的AEM项目提供了许多新功能和可能性。 但是，Adobe Experience Manager Maven项目需要进行一些更改才能与AEM Cloud Service兼容。 在高级别上，AEM要求将内容和代码分离为离散的子包，以便遵循可变内容和不可变内容之间的拆分。 使用 [Repository Modernizer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 用于通过将内容和代码分离为离散包来重构现有项目包的工具，以与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* 使用特定于环境的配置来获取秘密OSGi配置值，例如密码、专用API密钥或任何其他值。 出于安全原因，这些量度无法存储在Git中。 [使用特定于密钥环境的配置，在所有Adobe Experience Manager as a Cloud Service环境（包括暂存和生产环境）中存储密钥的值](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

有关Adobe Experience Manager as a Cloud Service中更改的完整列表，请参阅 [新增功能与不同功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## 关键增强功能 {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

以下功能和增强功能仅在 [!DNL AEM Forms] as a Cloud Service:

**增强的可视化规则编辑器**
该服务提供强化的 [可视化规则编辑器](rule-editor.md#visual-rule-editor). 该服务向可视化规则编辑器添加了以下功能，以帮助您编写功能强大的规则：

* [新提交事件](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`和 `Error`

* [新数据类型 `scope`](rule-editor.md#custom-functions). 您可以使用 `scope` 自定义函数中用于传递表单整个范围的数据类型。

* 使用功能 [@this在自定义函数中指定JSDoc](rule-editor.md#custom-functions). 它允许在活动组件中使用@this来调用自定义函数。

* 能够为基于属性的规则添加条件。

**核心组件**
的 [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 是一套用于AEM的标准化Web内容管理(WCM)组件，可加快开发时间并降低维护成本。 [!DNL AEM Forms] as a Cloud Service支持 **[!UICONTROL AEM Forms容器]** 核心组件。 您可以使用组件将自适应表单嵌入到AEM Sites页面。

**AEM for Formsas a Cloud Service**
[AEM原型](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) 帮助您开始开发 [!DNL AEM Forms] as a Cloud Service。 您可以使用Archetype版本27或更高版本创建与 [!DNL AEM Forms] as a Cloud Service环境。 原型还包含一些示例主题和模板，可帮助您快速入门。

**表单和Sign之间的信息流安全且得到改进**
[自适应Forms和Adobe Sign集成](working-with-adobe-sign.md) Cloud Service提供同时提交数据和签名活动。 它使表单提交独立于签名状态，为更快地提交铺平了道路。 此外，该服务不会在Cloud Service实例上保存任何数据，从而使签名过程变得超级安全。

**最佳实践分析器和迁移工具**
Best Practices Analyzer对您当前的AEM实施进行评估。 在之前运行该工具 [迁移到Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md). 它评估了从现有Adobe Experience Manager(AEM)部署到AEMas a Cloud Service的准备情况。

该服务还提供 [改进的迁移体验](migrate-to-forms-as-a-cloud-service.md) 帮助您轻松从 [!DNL AEM 6.4 Forms] 和 [!DNL AEM 6.5 Forms] to [!DNL AEM Forms] as a Cloud Service。

**更快的表单呈现和更快的服务器端验证**
该服务使用CDN和Dispatcher缓存，为Adaptive Forms提供更快的演绎版和服务器端验证。

**改进了验证码**
您现在可以 [验证验证验证码](captcha-adaptive-forms.md) 在自适应表单提交时或在业务逻辑中。 您还可以添加条件以在用户操作上验证CAPTCHA，并根据规则在自适应表单中显示或隐藏CAPTCHA组件。

CAPTCHA组件与Google reCAPTCHA提供了现成集成。 您还可以根据需要为组件配置更多验证码服务。

**记录文档的多个主控页面**
现在，您可以为记录文档的每个页面使用不同的主控页面，并通过分页选项控制自适应表单面板在记录文档上的放置。

**向无标题表添加列**
您可以向没有标题的表中添加和删除列。 隐藏的标题会添加到此类表中，以帮助您添加和删除列。 这些标题在创作过程中可见，但在已发布的表单中仍处于隐藏状态。 没有标题的表大多位于使用Automated forms conversion服务创建的自适应Forms中。

**改进了提交操作**
您可以使用 [发送电子邮件](configuring-submit-actions.md#send-email#send-email) 提交操作以作为附件发送记录文档(DoR)PDF。

**为工作流分组电子邮件**
您可以选择 [发送通知电子邮件](aem-forms-workflow-step-reference.md#assign-task-step) 将任务步骤分配给单个人员或组。

**增强的调用表单数据模型步骤**
现在，您可以在调用表单数据模型步骤中为输入服务参数的相对有效负荷选项指定文件夹路径。 它可帮助您将指定文件夹中存在的文件映射到服务参数，而无需指定确切的文件名。

**提高了翻译文件的可读性**
在Formsas a Cloud Service上，自适应表单的字段和面板的读取顺序以及相应翻译文件（.XLIFF文件）的消息键具有相似的结构。 它有助于提高手动翻译速度。

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
