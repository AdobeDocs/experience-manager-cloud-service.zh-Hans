---
title: 了解参考演示附加组件安装
description: 了解Cloud Manager以及如何使用它安装附加组件。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 了解参考演示附加组件安装 {#understand-installation}

了解Cloud Manager以及如何使用它安装附加组件。

>[!TIP]
>
>如果您已经经历过Cloud Manager的使用，或者希望直接跳转到加载项的配置和使用情况，则可以跳转到 [创建程序和管道](create-program.md)
>
>如果您想要了解Cloud Manager和AEM如何协同工作来创建您的演示环境，以及如何设置和使用您自己的环境，请继续阅读当前文档。

## 目标 {#objective}

本文档可帮助您了解参考演示附加组件的安装过程如何工作，并说明不同组件如何协同工作。 阅读后，您应该：

* 对Cloud Manager有基本的了解。
* 了解管道如何将内容和配置交付到AEM。
* 了解模板如何通过单击几下即可创建预填充了演示内容的新站点。

本文档重点介绍了在进入开始安装的历程的下一步之前，了解AEM参考演示附加组件的这些基本内容。

尽管建议您分步完成此历程，但如果您已经熟悉Cloud Manager，或者希望直接跳转到加载项的配置和使用，则可以跳到 [创建程序和管道](create-program.md)

## 负责任角色 {#responsible-role}

此历程适用于 **业务所有者** 角色。

## 要求和先决条件 {#requirements-prerequisites}

要了解并开始使用参考演示附加组件，只需满足最低要求。

### 知识 {#knowledge}

* Cloud Manager基本知识

### 工具 {#tools}

* 是 **业务所有者** 在Cloud Manager中为您的组织提供的角色

## 了解Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的一个基本组件，是平台的单个入口点。

Cloud Manager用于管理支持您的AEM项目的云资源，包括所需的环境和工具。 在此历程中，无需完全了解Cloud Manager。 但是，您需要熟悉一些基本概念。

>[!TIP]
>
>如果您希望深入了解Cloud Manager，请参阅 [其他资源](#additional-resources) ，以获取指向更多信息的链接。

### 程序 {#programs}

登录Cloud Manager后，您可以访问一个或多个 **项目**. 可以通过多种不同的方式来定义项目，但最简单的方法是将其视为与与一个品牌标识相关联的网站和体验相关联。

如果您登录Cloud Manager，表示 **WKND旅游和冒险企业**，您可以创建 **WKND夜生活** 程序和 **WKND后院项目** 项目。 这两个计划都将具有用于管理其关联站点的AEM环境。

### 沙箱 {#sandboxes}

程序可以是生产程序或沙盒程序。

* **生产计划** 将创建为在您的程序准备就绪后最终允许实时流量。
* **沙盒项目** 是为培训、运行演示、支持、POC等而创建的。 且不适用于实时流量。

要安装AEM参考演示加载项，您需要创建一个新的沙盒程序。

>[!NOTE]
>
>AEM参考演示加载项仅在沙盒项目中提供。

## 安装和使用流程 {#installation-flow}

既然您了解了Cloud Manager的一些基本概念，那么从概念上讲，安装AEM参考演示附加组件非常简单。

1. 登录Cloud Manager。
1. 创建新的沙盒AEM程序，并激活AEM参考演示附加组件以作为程序的选项。
1. 演示内容和配置已部署到程序。 演示内容包含：
   * 用于使用AEM功能创建各种AEM网站的网站模板，已预填充最佳实践示例。
   * 用于管理演示内容的配置工具。
1. 在新的沙盒项目中登录AEM，然后使用快速网站创建工具并根据模板创建演示网站。
1. 使用配置工具管理这些演示网站和模板，包括在不再需要时删除它们。

## AEM网站模板 {#site-templates}

AEM网站模板是指包含网站预定义内容和结构的包。 可以自定义网站模板以满足特定项目的需求，以便AEM管理员在创建新网站时，可以从适用于其业务案例的模板中进行选择。

AEM参考演示加载项包含多个模板，可满足各种测试和演示需求。 创建程序并部署管道以安装加载项后，您便可以登录AEM并根据许多演示模板创建站点

## 下一步 {#what-is-next}

现在，您已完成AEM参考演示附加组件历程的这一部分，接下来您应该：

* 对Cloud Manager有基本的了解。
* 了解管道如何将内容和配置交付到AEM。
* 了解模板如何通过单击几下即可创建预填充了演示内容的新站点。

在此知识的基础上，通过下一步审阅文档，继续您的AEM快速网站创建历程 [创建程序和管道，](create-program.md) 您将在此处了解如何设置新项目和管道以部署加载项。

## 其他资源 {#additional-resources}

同时，建议您通过审阅文档来转到快速网站创建历程的下一部分 [创建程序和管道，](create-program.md) 以下是一些其他可选资源，可更深入地了解本文档中提到的某些概念，但无需继续访问这些概念。

* [了解程序和程序类型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html)  — 从此处开始了解实时项目和沙盒项目之间的差异。
* [网站模板](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想进一步了解网站模板的结构以及如何使用它们来创建网站，请参阅此文档。
* [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您希望了解有关Cloud Manager功能的更多详细信息，则可能需要直接查阅深入的技术文档。
