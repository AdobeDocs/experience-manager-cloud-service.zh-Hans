---
title: IMS支持将Adobe Experience manager作为云服务
description: 'IMS支持将Adobe Experience manager作为云服务 '
translation-type: tm+mt
source-git-commit: bef17376f0b7de79511f9ad6ceb00e9f084f45d2

---


# IMS支持将Adobe Experience manager作为云服务 {#ims-support-for-aem-as-a-cloud-service}

## 简介 {#introduction}

* AEM作为云服务，包括对AEM实例和Adobe Identity Management System（简称IMS）身份验证的Admin console支持。
* 通过Admin Console，管理员可以集中管理所有Experience cloud用户。
* 用户和用户组可以作为云服务实例分配到与AEM关联的产品配置，以便他们登录到该实例。

## 主要亮点 {#key-highlights}

AEM作为云服务仅为作者、管理员和开发人员用户提供IMS身份验证支持。 它不为客户站点（如站点访问者）的外部最终用户提供支持。

* Admin Console将客户作为IMS组织、在环境中的作者实例和发布实例表示为产品上下文实例。 这将允许系统和产品管理员管理对实例的访问。
* Admin Console中的产品配置将决定用户可以访问的实例。
* 客户将能够使用自己的符合SAML 2规范的标识提供者（简称IDP）进行单点登录。
* 仅支持客户单点登录的Enterprise ID或Federated ID，不支持个人Adobe ID。

## 架构 {#architecture}

IMS身份验证在AEM和Adobe IMS端点之间使用OAuth协议。 将用户添加到IMS并拥有Adobe Identity后，他们便可以使用IMS凭据登录到AEM作者服务。

用户登录流程如下所示，用户将被重定向到IMS，并（可选）重定向到SSO的客户IDP，然后重定向回AEM。

![IMS架构](/help/security/assets/ims1.png)

## 如何设置 {#how-to-set-up}

### 将组织载入Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

使用Adobe IMS进行AEM身份验证的前提条件是客户开始使用Adobe Admin Console。

作为第一步，客户需要在Adobe IMS中设置组织。 Adobe Enterprise客户在 [Adobe Admin Console中表示为IMS组织](https://helpx.adobe.com/enterprise/using/admin-console.html) 。这是Adobe客户用来管理其用户和组的产品授权的门户。

AEM客户应已设置组织，作为IMS设置的一部分，客户实例将在Admin Console中提供，用于管理用户权利和访问权限。

客户作为IMS组织存在后，将必须按照以下概述配置其系统：

![IMS入门](/help/security/assets/ims2.png)

1. 指定的系统管理员将收到登录到Cloud Manager的邀请。 登录Cloud Manager后，系统管理员可以选择配置AEM程序和环境，或导航到Admin Console以执行管理任务。
1. 系统管理员声明一个域以确认相应域的所有权（例如acme.com）
1. 系统管理员设置用户目录
1. 系统管理员在管理控制台中进行IDP配置以设置单点登录。
1. AEM管理员可以像往常一样管理本地用户组以及权限和权限。

此处介绍包括IDP配置在内的Adobe身份管理基 [础知识](https://helpx.adobe.com/enterprise/using/set-up-identity.html)。

此处介绍企业管理和管理控制台的 [使用](https://helpx.adobe.com/enterprise/managing/user-guide.html)。

### Admin Console中的入职用户 {#onboarding-users-in-admin-console}

根据客户的规模和偏好，可通过三种方式建立用户：在Admin Console中手动创建用户，上传。csv文件或从客户的企业Active Directory同步用户。

**通过Admin Console UI手动添加**

用户和用户组可以在Admin Console UI中手动创建。 如果您没有大量用户可以管理，则可以使用此方法。 例如，少于50个AEM用户，或者如果您已使用此方法管理其他Adobe产品，如Analytics、Target或Creative cloud应用程序。

![用户入职](/help/security/assets/ims3.png)

**在Admin Console UI中上传文件**

为便于用户创建，可以上 `.csv` 传文件以批量添加用户。

![文件上传](/help/security/assets/ims4.png)

**用户同步工具**

用户同步工具（简称UST）使我们的企业客户能够利用Active Directory创建和管理Adobe用户。 这也适用于其他经测试的OpenLDAP目录服务。 目标用户是IT标识管理员（企业目录或系统管理员），他们将能够安装和配置该工具。 开放源代码工具可自定义，这样客户就可以修改它以满足您自己的特定要求。

当用户同步运行时，它会从单位的Active Directory中获取用户列表，并将其与Admin Console中的用户列表进行比较。  然后，它调用Adobe用户管理API，以便Admin Console与组织的目录同步。 改变流程完全是单向的。 在Admin Console中所做的任何编辑不会推送到该目录。

此工具允许系统管理员在客户目录中将用户组与Admin Console中的产品配置和用户组进行映射。

要设置用户同步，组织需要创建一组凭据，其方式与使用用户管理API [的方式相同](https://www.adobe.io/apis/experienceplatform/umapi-new.html)。

![用户同步工具](/help/security/assets/ims5.png)

用户同步工具通过Adobe Github存储库分 [发到此位置](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)。

>[!NOTE]
>
> 预发行版 **本2.4RC1支持** ，可在此处找到动态组创建 [支持](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)。

此版本的主要功能是能够在Admin Console中动态地映射新的LDAP用户组以作为用户成员，以及创建动态用户组。

有关新组功能的更多信息，请访 [问此位置](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)。

**用户同步文档**

有关更多详细 [信息，请参阅](https://adobe-apiplatform.github.io/user-sync.py/en/) UST文档。

用户同步工具需要使用此处的过程注册为Adobe I/O客户端UMAPI [](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)。

Adobe I/O Console文档可在此处找 [到](https://www.adobe.io/apis/cloudplatform/console.html)。

此处介绍用户同步工具使用的用户管理API [](https://www.adobe.io/apis/cloudplatform/umapi-new.html)。

## Adobe Experience作为云服务配置 {#aem-configuration}

> [!NOTE]
>
>在配置AEM环境和实例时，将自动配置所需的AEM IMS配置。 但是，管理员可以根据自己的要求使用此处描述的方法修改 [它](/help/implementing/deploying/overview.md)。

在配置AEM环境和实例时，将自动配置所需的AEM IMS配置。  客户管理员可以根据自己的要求修改部分配置

整体方法是将Adobe IMS配置为OAuth提供商。 可以 **像LDAP同步一样修改Apache Jackrabbit Oak默认同步处理程序** 。

以下是需要修改以更改“用户自动成员关系”或“组映射”等属性的关键OSGI配置。

<!-- Arun to provide list of osgi configs -->

## 使用方法 {#how-to-use}

### 在Admin Console中管理产品和用户访问 {#managing-products-and-user-access-in-admin-console}

当产品管理员登录到Admin Console时，他们将看到AEM Managed services产品上下文的多个实例，如下所示：

![实例登录](/help/security/assets/ims6.png)

在此示例中，组织 **** AEM-MS-Onboard有32个实例，这些实例跨不同的拓扑和环境（如Stage或Prod）。

![实例登录2](/help/security/assets/ims7.png)

在每个Product Context实例下，将有关联的Product Profiles。 这些产品配置文件用于为具有所需权限的用户和组分配访问权限。

Administrator_xxx **(** Administrator_xxx **** )配置文件将用于添加常规用户，用于在关联的AEM实例中授予管理员权限。

在此产品配置文件下添加的任何用户和用户组都将能够登录到该特定实例，如下例所示：

![产品简介](/help/security/assets/ims8.png)

### 以云服务的形式登录Adobe Experience Manager(#logging-in-to-aem)

**本地管理员登录**

AEM可继续支持管理员用户的本地登录。 登录屏幕具有本地登录选项：

![本地登录](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**基于IMS的登录**

对于其他用户，一旦在实例上配置了IMS，就可以使用基于IMS的登录。 用户将首先单击“使用Adobe登录”按钮，如下所示：

![IMS登录](/help/security/assets/ims10.png)

然后，他们将被重定向到IMS登录屏幕，并需要输入其凭据：

![IMS登录名2](/help/security/assets/ims11.png)

![IMS Login3](/help/security/assets/ims12.png)

如果在初始Admin Console设置过程中配置了联合IDP，则用户将被重定向到客户IDP以进行SSO:

![IMS登录4](/help/security/assets/ims13.png)

身份验证完成后，用户将被重定向回AEM并登录：

![IMS登录5](/help/security/assets/ims14.png)

### 在Adobe Experience manager中作为云服务管理权限和ACL {#managing-permissions-in-aem}

AEM中将继续管理ACL和权限。 可以将从IMS同步的用户组分配给定义ACL和权限的本地组。

在以下示例中，我们将同步的组添加到本地 **Dam_Users** 组作为示例。

用户是IMS中以下组的一部分：

![ACL1](/help/security/assets/ims15.png)

用户登录时，会同步其用户组成员关系，如下所示：

![ACL2](/help/security/assets/ims16.png)

在AEM中，可以将从IMS同步的用户组作为成员添加到现有的本地组，如 **DAM用户**。

![ACL3](/help/security/assets/ims17.png)

如下所示，组 **AEM-GRP_008** 继承了 **DAM用户的权限和权限**，这是管理已同步组权限的有效方式，也常用于基于LDAP的身份验证方法。

![ACL3](/help/security/assets/ims18.png)