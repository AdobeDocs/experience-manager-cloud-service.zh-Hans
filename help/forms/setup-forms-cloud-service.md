---
title: 载入AEM Formsas a Cloud Service
description: 了解如何设置和配置 [!DNL AEM Forms] as a Cloud Service环境
source-git-commit: b8366fc19a89582f195778c92278cc1e15b15617
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 17%

---

# 载入 [!DNL AEM Forms] as a Cloud Service {#overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html) |
| AEM as a Cloud Service | 本文 |


## 决定角色 {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> 载入之前 [!DNL AEM Forms] as a Cloud Service的环境，决定角色并为您的项目构建团队。 典型的 [!DNL AEM Forms] 项目团队具有以下角色：

* **用户体验(UX)设计器**：用户体验(UX)设计器定义样式、布局和品牌化 [!DNL AEM Forms] 资产。

* **Forms从业者**：Forms从业者根据UX设计器提供的样式、布局和品牌创建自适应Forms、主题和模板。 该从业人员还创建自适应表单并将其与表单数据模型和AEM Workflow集成。 Forms从业人员通常执行前端相关任务。

* **Forms开发人员**：Forms开发人员开发自定义表单解决方案。  Forms开发人员通常执行后端开发，例如开发自定义组件、AEM工作流、预填充服务等。

* **AEM管理员**：AEM管理员可帮助进行整体配置，例如设置用户、强化环境、配置数据源、配置电子邮件和第三方软件。 AEM管理员还可以帮助进行集成，例如与Adobe Analytics、Adobe Target和Adobe Sign集成。

* **最终用户**：最终用户与发布的表单交互并提交表单，签署提交的表单，通过Web门户跟踪提交的应用程序，并接收个性化通信。

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## 服务入门 {#onboarding}

* [载入](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) 到 [!DNL Adobe Experience Manager] as a Cloud Service。

* （仅适用于沙盒）载入服务后， [创建](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) 和 [运行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 生产和非生产管道。 它可以启用并引入以下最新功能 [!DNL AEM Forms] 对您的环境as a Cloud Service。

您可以使用Formsas a Cloud Service创建自适应表单（数字注册）或生成客户通信。 完成之后 [入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) 到 [!DNL Adobe Experience Manager] as a Cloud Service，执行以下操作之一以启用数字注册或客户通信功能。 您还可以启用以下两项功能：

1. 登录 Cloud Manager，并打开您的 AEM Forms as a Cloud Service 实例。

1. 打开“编辑程序”选项，转到“解决方案和加载项”选项卡，然后选择&#x200B;**[!UICONTROL Forms - 通信]**&#x200B;选项。

   ![通信](assets/communications.png)

   如果您已启用 **[!UICONTROL Forms - 数字登记]**&#x200B;选项，则选择 **[!UICONTROL Forms - 通信加载项]**&#x200B;选项。

   ![加载项](assets/add-on.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。

1. 运行构建管道。成功运行构建管道后，将为您的环境启用通信 API。

>[!NOTE]
>
> 要启用和配置文档操作 API，请将以下规则添加到 [Dispatcher 配置](setup-local-development-environment.md#forms-specific-rules-to-dispatcher)：
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## 配置用户 {#config-users}

完成服务入门培训后，请登录 [!DNL AEM Forms] as a Cloud Service环境，打开“创作”和“发布”实例，并将用户添加到特定于Forms的 [AEM组](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing)，基于其角色。 下表列出了特定于Forms的AEM组（现成可用）以及相应的用户类型。 该表还提供了每种用户类型的AEM实例类型：

| 用户类型（角色） | 用户组 | AEM实例 |
|---|---|---|
| 表单从业者/Forms开发人员 | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | 创作实例 |
| 用户体验(UX)设计器 | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | 创作实例 |
| AEM 管理员 | <ul> <li>[!DNL aem-administrators]，</li> <li>[!DNL fd-administrators] </li> </ul> | 创作和发布实例 |
| 最终用户 | <ul> <li>当用户必须登录才能查看并提交自适应表单时，请将这些用户添加到 [!DNL forms-users] 组。 </li> <li>当访问自适应Forms不需要用户身份验证时，不要向此类用户分配任何组。 </li> </ul> | 创作和发布实例 |

有关特定于Forms的AEM组和相应权限的更多信息，请参阅 [组和权限](forms-groups-privileges-tasks.md).

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## 下一步 {#next-steps}

[设置本地开发环境](setup-local-development-environment.md). 您可以使用本地开发环境创建自适应表单和相关资产（主题、模板、自定义提交操作、预填充服务等），并且 [将PDF forms转换为自适应Forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=zh-Hans) 无需登录到云开发环境。

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit’s product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications etc.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title ‘You now have administrator rights to manage Adobe software and services for your organization’. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#onboarding-users-in-admin-console) via IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=en). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
