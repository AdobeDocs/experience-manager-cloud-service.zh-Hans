---
title: 向前端开发人员授予访问权限
description: 将前端开发人员载入 Cloud Manager 以便他们能够访问 AEM 站点 Git 存储库和管道。
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: ht
source-wordcount: '785'
ht-degree: 100%

---

# 向前端开发人员授予访问权限 {#grant-fed-access}

将前端开发人员载入 Cloud Manager 以便他们能够访问 AEM 站点 Git 存储库和管道。

## 迄今为止的故事 {#story-so-far}

在 AEM 快速站点创建历程的上一个文档[设置您的管道](pipeline-setup.md)中，您已了解如何创建前端管道来管理站点主题的自定义，现在应：

* 了解什么是前端管道。
* 了解如何在 Cloud Manager 中设置前端管道。

您现在需要通过载入流程向前端开发人员授予对 Cloud Manager 的访问权限，以便前端开发人员能够访问 AEM Git 存储库和您创建的管道。

## 目标 {#objective}

向用户授予对 Cloud Manager 的访问权限并将用户角色分配给用户的过程称为载入。本文档将概述载入前端开发人员的最重要步骤，阅读后您将了解：

* 如何将前端开发人员添加为用户。
* 如何向前端开发人员授予所需的角色。

>[!TIP]
>
>提供了有关将团队载入 AEM as a Cloud Service 的历程的完整文档，如果您想了解有关此过程的其他详细信息，请参阅本文档的[其他资源](#additional-resources)部分。

## 负责角色 {#responsible-role}

此历程的这一部分适用于 Cloud Manager 管理员。

## 要求 {#requirements}

* 您需要成为 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色的成员。
* 您需要成为 Cloud Manager 中的&#x200B;**系统管理员**。
* 您需要具有对 Admin Console 的访问权限。

## 将前端开发人员添加为用户 {#add-fed-user}

首先，您需要使用 Admin Console 将前端开发人员添加为用户。

1. 在 [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/) 登录到 Admin Console。

1. 登录后，您会看到类似于下图的概述页面。

   ![Admin Console 概述](assets/admin-console.png)

1. 通过查看屏幕右上角的组织名称，确保您在适当的组织中。

   ![查看组织名称](assets/correct-org.png)

1. 从&#x200B;**产品和服务**&#x200B;卡中选择 **Adobe Experience Manager as a Cloud Service**。

   ![选择 AEMaaCS](assets/select-aemaacs.png)

1. 您会看到预配置的 Cloud Manager 产品配置文件的列表。如果您未看到这些配置文件，请联系您的 Cloud Manager 管理员，因为您可能在组织中没有正确的权限。

   ![产品配置文件](assets/product-profiles.png)

1. 要将前端开发人员分配给正确的配置文件，请点按或单击&#x200B;**用户**&#x200B;选项卡，然后点按或单击&#x200B;**添加用户**&#x200B;按钮。

   ![添加用户](assets/add-user.png)

1. 在&#x200B;**将用户添加到团队**&#x200B;对话框中，键入要添加的用户的电子邮件 ID。对于 ID 类型，如果尚未为团队成员设置 Federated ID，请选择 Adobe ID。

   ![将用户添加到团队](assets/add-to-team.png)

1. 在&#x200B;**产品**&#x200B;选择中，点按或单击加号，再选择 **Adobe Experience Manager as a Cloud Service**，并将&#x200B;**部署经理**&#x200B;和&#x200B;**开发人员**&#x200B;产品配置文件分配给用户。

   ![分配团队配置文件](assets/assign-team.png)

1. 点按或单击&#x200B;**保存**，这将向已添加为用户的前端开发人员发送欢迎电子邮件。

受邀的前端开发人员可以通过单击欢迎电子邮件中的链接并使用其 Adobe ID 登录来访问 Cloud Manager。

## 移交给前端开发人员 {#handover}

通过在移交给前端开发人员的过程中向 Cloud Manager 发送电子邮件邀请，您和 AEM 管理员现在可以向前端开发人员提供开始自定义所需的剩余信息。

* [典型内容的路径](#example-page)
* [您下载的](#download-theme)主题源
* [代理用户凭据](#proxy-user)
* [从 Cloud Manager 复制的](pipeline-setup.md#login)项目的名称或 URL
* 前端设计要求

## 下一步 {#what-is-next}

现在您已完成 AEM 快速站点创建历程的这一部分，您应了解：

* 如何将前端开发人员添加为用户。
* 如何向前端开发人员授予所需的角色。

在此知识的基础上继续您的 AEM 快速站点创建历程，接下来查看文档[检索 Git 存储库访问信息](retrieve-access.md)，此文档将视角专门切换到前端开发人员，并说明了前端开发人员如何使用 Cloud Manager 访问 Git 存储库信息。

## 其他资源 {#additional-resources}

我们建议您查看文档[检索前端开发人员凭据](retrieve-access.md)来继续快速站点创建历程的下一部分，以下是一些其他可选资源，这些资源对本文档中提到的一些概念进行了更深入的探究，但并非继续此历程所必需的。

* [载入历程](/help/journey-onboarding/overview.md) – 本指南可作为您的起点，确保您的团队已建立并有权访问 AEM as a Cloud Service。
