---
title: 了解参考演示加载项安装
description: 了解 Cloud Manager 以及如何使用它安装加载项。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 100%

---

# 了解参考演示加载项安装 {#understand-installation}

了解 Cloud Manager 以及如何使用它安装加载项。

>[!TIP]
>
>如果您已体验 Cloud Manager 或希望直接了解加载项的配置和使用，则可以跳到[创建项目和管道](create-program.md)
>
>如果您想了解 Cloud Manager 和 AEM 如何协作以创建您的演示环境以及如何设置和使用您自己的环境，请继续阅读当前文档。

## 目标 {#objective}

本文档可帮助您了解参考演示加载项安装过程的工作原理，并说明了各个部分的协作方式。阅读本文档后，您应：

* 基本了解 Cloud Manager。
* 了解管道如何将内容和配置交付给 AEM。
* 了解如何通过单击几下来使用模板创建已预填充演示内容的新站点。

在继续此历程的下一步来开始安装之前，可通过本文档了解 AEM 参考演示加载项的这些基本部分。

虽然建议您逐步完成此历程，但如果您已体验 Cloud Manager 或希望直接了解加载项的配置和使用，则可以跳到[创建项目和管道](create-program.md)

## 负责角色 {#responsible-role}

此历程适用于作为组织的 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色成员的系统管理员。

## 要求和先决条件 {#requirements-prerequisites}

只需达到最低要求即可了解并开始使用参考演示加载项。

### 知识 {#knowledge}

* Cloud Manager 的基本知识

### 工具 {#tools}

* 成为组织的 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色的成员

## 了解 Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的必要组件，并且充当平台的单一入口点。

Cloud Manager 用于管理支持您的 AEM 项目的云资源，包括所需的环境和工具。在此历程中，无需全面了解 Cloud Manager。但您需要熟悉一些基本概念。

>[!TIP]
>
>如果您希望深入了解 Cloud Manager，请参阅本文的[其他资源](#additional-resources)部分，获取指向更多信息的链接。

### 项目 {#programs}

登录 Cloud Manager 时，您可以访问一个或多个&#x200B;**项目**。虽然可以通过多种不同的方式定义项目，但最简单的方式是将它视为与某个品牌标识相关的站点和体验相关联。

如果您登录表示 **WKND 旅游和冒险企业**&#x200B;的 Cloud Manager，则可以创建 **WKND Nightlife** 项目和 **WKND Backyard Projects** 项目。这两个项目都将具有用于管理其关联站点的 AEM 环境。

### 沙盒 {#sandboxes}

项目可以是生产项目或沙盒项目。

* 当您的项目准备好上线时，将创建一个&#x200B;**生产项目**&#x200B;以最终允许实时流量。
* 创建&#x200B;**沙盒项目**&#x200B;以实施培训、运行演示、支持、POC 等，而不是用于实时流量。

要安装 AEM 参考演示加载项，您需要创建一个新的沙盒项目。

>[!NOTE]
>
>AEM 参考演示加载项仅适用于沙盒项目。

## 安装和使用流 {#installation-flow}

现在，您已了解 Cloud Manager 的一些基本概念，从概念上说，AEM 参考演示加载项的安装很简单。

1. 登录 Cloud Manager。
1. 创建一个新的沙盒 AEM 项目，并激活 AEM 参考演示加载项作为项目的一个选项。
1. 演示内容和配置将部署到项目中。演示内容包含：
   * 用于使用 AEM 功能创建各种 AEM 站点的站点模板，其中预填充了最佳实践示例。
   * 用于管理演示内容的配置工具。
1. 在您的新沙盒项目中登录 AEM，使用快速站点创建工具并基于模板创建演示站点。
1. 使用配置工具管理这些演示站点和模板，包括在不再需要它们时将其删除。

## AEM 站点模板 {#site-templates}

AEM 站点模板是包含站点的预定义内容和结构的包。可以自定义站点模板以满足特定项目的需求，这使得在 AEM 管理员创建新站点时，他们可以从适用于其业务案例的模板中进行选择。

AEM 参考演示加载项包括多个模板，可满足各种测试和演示需求。在创建项目并部署管道以安装加载项后，您可以登录 AEM 并基于多个演示模板创建站点

## 下一步 {#what-is-next}

现在您已完成 AEM 参考演示加载项历程的这一部分，您应：

* 基本了解 Cloud Manager。
* 了解管道如何将内容和配置交付给 AEM。
* 了解如何通过单击几下来使用模板创建已预填充演示内容的新站点。

在此知识的基础上继续您的 AEM 快速站点创建历程，接下来查看文档[创建项目和管道](create-program.md)，您将了解如何设置新项目和管道以部署加载项。

## 其他资源 {#additional-resources}

我们建议您查看文档[创建项目和管道](create-program.md)来继续快速站点创建历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [了解项目和项目类型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html) – 从这里开始了解实时项目和沙盒项目之间的区别。
* [站点模板](/help/sites-cloud/administering/site-creation/site-templates.md) – 如果您想详细了解站点模板的结构以及如何使用它们创建站点，请参阅本文档。
* [Cloud Manager 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) – 如果您想了解有关 Cloud Manager 功能的更多详细信息，您可能需要直接参阅深入的技术文档。
