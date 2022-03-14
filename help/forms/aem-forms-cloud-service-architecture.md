---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service架构
description: 了解的架构 [!DNL AEM Forms] as a Cloud Service了解该平台的可扩展性、可复原性和性能方面。
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 6%

---


# [!DNL AEM] as a Cloud Service架构 {#architecture}

[!DNL AEM Forms] as a Cloud Service地为所有客户实现部署架构的标准化，目标是让客户完全从架构考虑事项中解脱出来。 例如，虽然新的AEMas a Cloud Service架构仍然依赖于微内核的持久性概念，但客户无需担心从哪个微内核中挑选出来。 在作者和发布端使用的微内核是 [!DNL AEM Cloud Service] 和，否则，客户将无法进行内部部署安装。

AEMas a Cloud Service具有具有可变数量的AEM实例的动态架构。 它提供了开发、暂存、生产和演示环境。 它提供了一些工具来管理AEM实例(Cloud Manager)、维护用户和身份验证(Admin Console和IMS(Adobe身份管理)系统)、配置缓存(Fastly CDN)以及云原生开发环境。 有关架构的更多信息，请参阅 [对 [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html?lang=en).

## Cloud Manager{#cloud-manager}

Cloud Manager是 [AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). 的每个新租户 [!DNL AEM Forms] as a Cloud Service首次配置了Cloud Manager访问权限。 Cloud Manager是客户运营和开发人员角色的单一入口点。 它是管理AEM程序和环境的位置。 Cloud Manager已演变为自助门户，可在其中创建和配置AEMas a Cloud Service的主要组件：

* 创建和管理程序
* 在程序中创建和管理AEM环境
* 创建和管理管道以将客户代码和配置部署到特定环境
* 获取有关这些组件的重要生命周期事件（例如产品更新）的通知。有关Cloud Manager的更多信息，请参阅 [了解AdobeCloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) 和 [Cloud Manager简介](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hans).

## 用户和身份验证 {#users-and-authentication}

AEMas a Cloud Service包括对AEM实例和基于Adobe的Identity Management系统(IMS)身份验证的Admin Console支持。 通过 Admin Console，管理员可以集中管理所有 Experience Cloud 用户。可以将用户和组分配到与 AEM as a Cloud Service 实例相关联的产品配置文件，从而让他们可以登录到该实例。有关用户、身份验证以及访问AEMas a Cloud Service实例的更多信息，请参阅 [对的IMS支持 [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

典型 [!DNL AEM Forms] 项目。 在登录到 [!DNL AEM Forms] as a Cloud Service实例，您可以 [在admin console中添加用户](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) 适用于您的组织或项目的角色，以及 [将用户分配给内置组](forms-groups-privileges-tasks.md) 为他们提供所需的权限。

了解各种内置 [!DNL AEM Forms] 可用的特定用户组和权限 [!DNL AEM Forms] 作为Cloud Services实例，请参阅 [配置、用户、角色和组](forms-groups-privileges-tasks.md).

## 开发人员体验 {#developer-experience}

支持AEMas a Cloud Service的新架构为整个开发人员体验带来了一些关键变化。 对开发人员体验进行更改的主要目标之一是，允许尽快迁移到AEMas a Cloud Service，而对现有自定义代码几乎不做任何修改。

## 云开发 {#cloud-development}

以下是在AEMas a Cloud Service环境中顺利运行现有代码的准则：

* 将您的代码和配置存储到关联的Cloud Manager程序的Git存储库。 它使管理代码和将代码与CI/CD集成变得轻而易举。
* 使应用程序代码和配置与基线兼容 [!DNL AEM Forms] 图像。 使用最新的API有助于构建更快、更安全的应用程序。
* 使用与Cloud Manager环境关联的Cloud Manager管道来构建和部署应用程序。 它可帮助您为 [!DNL AEM Forms] as a Cloud Service于您的环境。
* 请尝试您的自定义应用程序传递管道中强制执行的所有代码质量、安全性和性能门。 它有助于构建安全且性能更好的应用程序，从而改善客户体验。 您可以始终使用Cloud Manager UI跳过一些检查。
此过程通常称为云优先开发。 [!DNL AEM Forms] as a Cloud Service还提供了一个SDK，在云中尝试更改挂起的代码和配置之前，可支持快速开发。
AEM QuickStart之前包含的某些界面不再可供AEMas a Cloud Service环境的用户使用。 例如，管理OSGi包及其关联配置的Web控制台。 CRXDE Lite内容存储库浏览器仅可在非生产环境类型中访问。 开发人员需要的Web控制台功能的子集（特别是在诊断和状态方面）可通过新的开发人员控制台提供。
此外，开发人员最常见的要求之一是快速访问各种环境的日志文件。 使用 [!DNL AEM Cloud Service]，创作发布中不同节点的日志文件可通过Cloud Manager使用（可下载的文件形式或通过API跟踪日志）。 由于代码和内容之间有着明确的分离，开发人员可以利用特定流程在部署中更新内容。 可变内容的典型用例包括：
* 属于客户项目的标准“默认”内容（例如文件夹、模板、工作流……）
* 搜索索引定义
* ACL 和权限
* 服务用户和用户组
设置开发环境， [配置CI/CD管线](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html)，并学习 [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 在环境中。

## 地方发展 {#local-development}

设置和配置 [!DNL AEM Forms] 与环境as a Cloud Service，您可以设置开发、暂存和生产环境。 此外，还设置和配置本地开发环境，以便快速进行迭代和开发。 您可以下载和设置AEM SDK，以及 [!DNL AEM Forms] 附加功能存档以设置本地 [!DNL Forms] as a Cloud Service的开发环境。  有关详细说明，请参阅 [设置本地开发环境](setup-local-development-environment.md).

## 调试 {#debugging}

AEMas a Cloud Service运行于自助式、可扩展的云基础架构上。 它要求AEM开发人员了解和调试AEMas a Cloud Service的各个方面，从构建和部署到获取运行AEM应用程序的详细信息。 有关详细信息，请参阅 [调试AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html?lang=en).
