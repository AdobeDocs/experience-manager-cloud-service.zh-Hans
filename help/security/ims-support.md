---
title: 对 Adobe Experience Manager as a Cloud Service 的 IMS 支持
description: 对 Adobe Experience Manager as a Cloud Service 的 IMS 支持
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 92%

---

# 对 Adobe Experience Manager as a Cloud Service 的 IMS 支持 {#ims-support-for-aem-as-a-cloud-service}

## 简介 {#introduction}

* AEM as a Cloud Service 包括对 AEM 实例和基于身份验证的 Adobe 身份管理系统（简称 IMS）的 Admin console 支持。
* 通过 Admin Console，管理员可以集中管理所有 Experience Cloud 用户。
* 可以将用户和组分配到与 AEM as a Cloud Service 实例相关联的产品配置文件，从而让他们可以登录到该实例。

>[!TIP]
>
>请参阅我们的Experience League课程[为管理员配置对AEM的访问权限](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem)，以了解用户如何使用AdobeIMS对AEM as a Cloud Service进行身份验证，以及如何使用AdobeIMS用户、用户组和产品配置文件来控制对AEM及其特性和功能的访问。 Adobe ID必需。

## 主要亮点 {#key-highlights}

AEM as a Cloud Service 仅为作者、管理员和开发人员用户提供 IMS 身份验证支持。它不为客户站点（如站点访客）的外部最终用户提供支持。

* Admin Console 将客户表示为 IMS 组织，将环境中的作者实例和发布实例表示为产品上下文实例。这将允许系统和产品管理员管理对实例的访问。
* Admin Console 中的产品配置文件将决定用户可以访问哪些实例。
* 客户将能够使用自己的符合 SAML 2 规范的身份提供程序（简称 IDP）进行单点登录。
* 仅支持客户单点登录的 Enterprise ID 或 Federated ID，不支持个人 Adobe ID。

## 架构 {#architecture}

IMS 身份验证在 AEM 和 Adobe IMS 端点之间使用 OAuth 协议进行工作。当用户添加到 IMS 并拥有 Adobe 身份后，他们便可以使用 IMS 凭据登录到 AEM 创作服务。

用户登录流程如下所示，用户将被重定向到 IMS，并可以选择性地重定向用于 SSO 的客户 IDP，然后重定向回 AEM。

![IMS 架构](/help/security/assets/ims1.png)

## 如何设置 {#how-to-set-up}

### 将组织载入 Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

使用 Adobe IMS 进行 AEM 身份验证的前提条件是将客户载入 Adobe Admin Console。

第一步，客户需要在 Adobe IMS 中设置组织。Adobe 企业客户在 [Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html) 中表示为 IMS 组织。这是 Adobe 客户管理其用户和组的产品权利的门户。

AEM 客户应已设置组织，作为 IMS 设置的一部分，客户实例将在 Admin Console 中可用，以用于管理用户权利和访问权限。

客户作为 IMS 组织存在后，将必须按照以下概述配置其系统：

![IMS 载入](/help/security/assets/ims2.png)

1. 指定的系统管理员将会收到登录到 Cloud Manager 的邀请。登录 Cloud Manager 后，系统管理员可以选择配置 AEM 程序和环境，或导航到 Admin Console 以执行管理任务。
1. 系统管理员声明一个域以确认相应域（例如 acme.com）的所有权
1. 系统管理员设置用户目录
1. 系统管理员在 Admin Console 中进行 IDP 配置以设置单点登录。
1. AEM 管理员可以像往常一样管理本地组以及权限。

[此处](https://helpx.adobe.com/cn/enterprise/using/set-up-identity.html)介绍了 Adobe 身份管理基础知识，包括 IDP 配置。

[此处](https://helpx.adobe.com/cn/enterprise/managing/user-guide.html)介绍了企业管理和 Admin Console 用法。

### 在 Admin Console 中载入用户 {#onboarding-users-in-admin-console}

根据客户的数量和偏好，可通过三种方式载入用户：在 Admin Console 中手动创建用户，上传 .csv 文件或从客户的企业 Active Directory 同步用户。

**通过 Admin Console UI 手动添加**

可以在 Admin Console UI 中手动创建用户和组。如果要管理的用户数量不多，则可以使用此方法。例如，少于 50 个 AEM 用户，或者如果您已在使用此方法管理其他 Adobe 产品，如 Analytics、Target 或 Creative Cloud 应用程序。

![用户载入](/help/security/assets/ims3.png)

**在 Admin Console UI 中上传文件**

为便于创建用户，可以上传 `.csv` 文件以批量添加用户。

![文件上传](/help/security/assets/ims4.png)

**用户同步工具**

用户同步工具（简称 UST）让我们的企业客户能够利用 Active Directory 创建和管理 Adobe 用户。这也适用于其他经测试的 OpenLDAP 目录服务。目标用户是 IT 标识管理员（企业目录或系统管理员），他们将能够安装和配置该工具。此开放源代码工具可自定义，这样客户就可以修改它以满足您自己的特定要求。

当用户同步运行时，它会从组织的 Active Directory 中获取用户列表，并将其与 Admin Console 中的用户列表进行比较。然后，它会调用 Adobe 用户管理 API，以便将 Admin Console 与组织的目录同步。更改流程完全是单向的。不会将在 Admin Console 中所做的任何编辑推送到该目录。

此工具允许系统管理员将客户目录中的用户组与 Admin Console 中的产品配置的用户组进行映射。

要设置用户同步，组织需要创建一组凭证，其方式与使用[用户管理 API](https://www.adobe.io/apis/experienceplatform/umapi-new.html) 的方式相同。

![用户同步工具](/help/security/assets/ims5.png)

用户同步工具通过位于[此位置](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)的 Adobe Github 存储库分发。

>[!NOTE]
>
>支持创建动态组的预发行版 **2.4RC1** 可供使用，该版本可以在[此处](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)找到。

此版本的主要功能是能够动态映射新的 LDAP 组以在 Admin Console 中获得用户成员资格，以及动态创建用户组。

有关新组功能的更多信息，请访问[此位置](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)。

**用户同步文档**

有关更多详细信息，请参阅 [UST 文档](https://adobe-apiplatform.github.io/user-sync.py/en/)。

用户同步工具需要使用[此处](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)的过程注册为 Adobe I/O 客户端 UMAPI。

Adobe I/O 控制台文档可在[此处](https://www.adobe.io/apis/cloudplatform/console.html)找到。

[此处](https://www.adobe.io/apis/cloudplatform/umapi-new.html)介绍了用户同步工具使用的用户管理 API。

## Adobe Experience as a Cloud Service 配置 {#aem-configuration}

>[!NOTE]
>
>在配置 AEM 环境和实例时，将自动配置所需的 AEM IMS 配置。但是，管理员可以根据自己的需求使用[此处](/help/implementing/deploying/overview.md)描述的方法进行修改。

在配置 AEM 环境和实例时，将自动配置所需的 AEM IMS 配置。客户管理员可以根据自己的要求修改部分配置

大致方法是将 Adobe IMS 配置为 OAuth 提供程序。可以像修改 LDAP 同步一样修改 **Apache Jackrabbit Oak 默认同步处理程序**。

以下是关键的 OSGI 配置，需要更改这些配置才能更改用户自动成员资格或组映射等属性。

<!-- Arun to provide list of osgi configs -->

## 使用方法 {#how-to-use}

### 在 Admin Console 中管理产品和用户访问权限 {#managing-products-and-user-access-in-admin-console}

当产品管理员登录到Admin Console时，他们将看到多个AEM实例作为Cloud Service产品上下文，如下所示。 例如，从&#x200B;**Overview**&#x200B;页面中选择任意产品：

![实例登录](/help/security/assets/ims6.png)

您将看到现有实例的列表：

![实例登录 2](/help/security/assets/ims7.png)

在每个产品上下文实例下，将有跨生产、暂存或开发环境的创作或发布服务的实例。 每个实例都将与产品配置文件或Cloud Manager角色关联。 这些产品配置文件用于为具有所需权限的用户和组分配访问权限。

**Administrator_xxx** 配置文件将用于在关联的 AEM 实例中授予管理员特权，而 **User_xxx** 配置文件用于添加常规用户。

在此产品配置文件下添加的任何用户和组都将能够登录到该特定实例，如下例所示：

![产品配置文件](/help/security/assets/ims8.png)

### 登录 Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**本地管理员登录**

AEM 可继续支持管理员用户在本地登录。登录屏幕具有本地登录选项：

![本地登录](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**基于 IMS 的登录**

对于其他用户，只需在实例上配置 IMS 即可使用基于 IMS 的登录。用户将先需要单击“使用 Adobe 登录”按钮，如下所示：

![IMS 登录](/help/security/assets/ims10.png)


>[!NOTE]
>
>在 IMS 中创建任何用户时，都可以使用 Adobe ID 或 Federated ID 进行创建。如果用户是使用 Adobe ID 设置的，则会使用其公司的身份提供程序对其进行身份验证以登录。

然后，他们将被重定向到 IMS 登录屏幕，并需要输入其凭证：

![IMS 登录 2](/help/security/assets/ims11.png)

![IMS 登录 3](/help/security/assets/ims12.png)

如果在初始 Admin Console 设置过程中配置了联合 IDP，则用户将被重定向到用于 SSO 的客户 IDP：

![IMS 登录 4](/help/security/assets/ims13.png)

身份验证完成后，用户将被重定向回 AEM 并登录：

![IMS 登录 5](/help/security/assets/ims14.png)

### 在 Adobe Experience Manager as a Cloud Service 中管理权限和 ACL {#managing-permissions-in-aem}

ACL 和权限仍将继续在 AEM 中管理。可以将从 IMS 同步的用户组分配给定义 ACL 和权限的本地组。

在以下示例中，我们将同步的组作为示例添加到本地 **Dam_Users** 组。

用户是 IMS 中以下组的一部分：

![ACL1](/help/security/assets/ims15.png)

用户登录时，会同步其组成员资格，如下所示：

![ACL2](/help/security/assets/ims16.png)

在 AEM 中，可以将从 IMS 同步的用户组作为成员添加到现有的本地组，如 **DAM 用户**。

![ACL3](/help/security/assets/ims17.png)

如下所示，组 **AEM-GRP_008** 继承了 **DAM 用户**&#x200B;的权限，这是管理已同步组权限的有效方式，通常也会在基于 LDAP 的身份验证方法中使用。

![ACL3](/help/security/assets/ims18.png)


### 访问 Cloud Manager {#accessing-cloud-manager}

要访问 Cloud Manager 或 AEM as a Cloud Service 环境，必须将您分配到 Cloud Manager 产品的配置文件。

请参阅角色定义，了解有关用于控制 Cloud Manager 中特定功能可用性的用户角色的更多信息。

>[!NOTE]
>Cloud Manager 预配置了一些具有适当权限的角色。要了解有关每个角色及与其关联的特定权限、预配置任务或权限的信息，请参阅[基于角色的权限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html)。

**添加用户的步骤**

1. 从现有用户屏幕或从新用户屏幕将用户添加到特定配置文件。

1. 或者，您也可以从&#x200B;**概述**&#x200B;屏幕添加用户，如下图所示。

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >您可以向用户分配多个配置文件，如下图所示。

   ![ACL3](/help/security/assets/ims22.png)


1. 将您添加到相应的配置文件后，您应能够在 Cloud Manager 中通过用户界面的右上角的 [Adobe Experience Cloud](http://my.cloudmanager.adobe.com) 访问各自的租户。


### 访问 AEM as a Cloud Service 中的实例 {#accessing-instance-cloud-service}

>[!IMPORTANT]
>授予您访问 AEM as a Cloud Service 中的实例权限之前，必须完成上一节中提到的步骤。

要在 **Admin Console** 中访问 AEM 实例，您应在 **Admin Console** 的产品列表中看到 Cloud Manager 计划和该计划中的环境。

例如，在下面的屏幕截图中，您将看到两个可用的环境，即&#x200B;*开发作者*&#x200B;和&#x200B;*发布*。

![ACL3](/help/security/assets/ims19.png)

要访问 AEM 实例，需要将用户添加到相应云服务产品的组中。

每个作者实例都将具有 AEM 管理员和 AEM 用户配置文件，每个发布实例也都将具有 AEM 用户配置文件。您可以根据需要添加其他配置文件。

要获取对 AEM 实例的管理员级别访问权限，请将用户添加到该特定产品的 AEM 管理员配置文件。
