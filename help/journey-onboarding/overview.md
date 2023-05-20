---
title: AEM as a Cloud Service 入门培训历程简介
description: 您可以在此处了解 AEM as a Cloud Service 入门培训历程的指导概述。
exl-id: 892577db-05dc-49ff-bb2c-203efdb89c8c
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 58%

---


# 入门培训历程 {#onboarding-journey}

恭喜您选择 AEM as a Cloud Service！ 本文档是指导您整个入门培训历程的起点。 無論您是部署新應用程式還是移轉現有應用程式，此入門歷程可確保您的團隊已建立並可存取AEMas a Cloud Service。

## 简介 {#introduction}

载入是指定的系统管理员未您的组织设置 AEM as a Cloud Service 的过程。 此程式包括雲端資源的初始設定，以及根據使用者的工作職責為其指派角色。 因此，每個成員都能在AEMas a Cloud Service上登入並存取其資源。

![入门培训历程](/help/journey-onboarding/assets/onboarding-journey.png)

本指南將引導您瞭解最重要的入門主題，完成後您將獲得以下內容：

* 全面了解载入流程中涉及的不同术语、服务和用户。
* 使您的团队能够启动并运行，开始学习如何为 AEM as a Cloud Service 应用程序编写和开发内容。

因此：

* 您的團隊已設定並可以存取雲端資源。
* AEM作者可以存取AEMas a Cloud Service，並可以開始建立內容。
* AEM開發人員和部署管理員可以存取AEMas a Cloud Service，並可以開始建立和部署自訂應用程式。

## 概念和目标 {#concepts}

虽然在开始使用 AEM as a Cloud Service 时，似乎有很多东西需要学习，但从概念上讲，只有少数几个逻辑部分。

* **合約**  — 您必須熟悉Adobe合約，因為它定義了入門流程的各方面內容。
* **Admin Console**  — 管理使用者和指派角色的位置。
* **Cloud Manager**  — 設定計畫和環境等資源的工具。 它也是您访问 Git 并创建管道，以便管理和部署自定义代码的地方。

這些概念在這次入門歷程中詳細闡述。 目标是在历程结束时，您：

* 已授予必要使用者存取AEMas a Cloud Service的許可權。
* 已为您的项目设置了第一个云资源.
* 知道如何部署第一个代码并创作第一个内容。

基本上，您已經著手執行新的AEMas a Cloud Service專案！

## 受众 {#audience}

该入门培训历程是专门为新加入 AEM as a Cloud Service 和 AEM 的客户的&#x200B;**系统管理员**&#x200B;编写的。 系統管理員是Adobe在您的AEMas a Cloud Service合約簽署後首先聯絡的個人。 他們通常是第一個在AEMas a Cloud Service上存取和設定資源的人。 如果您閱讀本主題，您可能是系統管理員。

系统管理员管理其组织的 AEMaaCS 用户的各个方面，从访问到权限。 然而，系统管理员必须在过程中与其他角色进行交互。

| 角色 | 描述 | 历程中的角色 |
|---|---|---|
| 系统管理员 | 此次历程的目标，提供云资源的初始配置，并根据用户的工作职责将其分配给适当的角色 | 管理用户从访问到权限的各个方面 |
| 内容作者 | 创建并查看 AEM 中的内容 | 一旦系统管理员授予权限，作者就可以开始自己的创作之旅 |
| 开发人员 | 开发使用不同来源内容的 AEM 应用程序 | 一旦系统管理员授予权限，开发人员就可以开始自己开发解决方案的历程 |
| 部署管理员 | 添加或更新环境，运行管道，并将代码部署到 AEM 环境或代码质量。 | 一旦系统管理员授予权限，部署管理员就可以开始自己管理部署的历程 |

本载入指南说明了作为系统管理员载入的完整过程。 作为历程的附加可选部分，对 AEM 用户、开发人员和部署管理员的角色进行了简要探讨。

>[!TIP]
>
>如果您是初次使用AEMas a Cloud Service且熟悉AEM，並且正從內部部署或Adobe Managed Services移轉，請務必參閱 [AEMas a Cloud Service移轉歷程](/help/journey-migration/getting-started.md).

## 入门培训历程概述 {#overview}

以下文章详细描述了核心载入概念，并为您提供了 AEM as a Cloud Service 的基本知识。 虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是新手，Adobe建議您從頭開始，然後循序漸進。

| # | 文章 | 描述 | 受众 |
|---|---|---|---|
| 0 | 入门培训历程 | 本文档 | 系统管理员 |
| 1 | [载入准备](preparation.md) | 在载入流程开始之前，系统管理员必须了解一些步骤或准备步骤，然后才能登录系统。 | 系统管理员 |
| 2 | [AEM as a Cloud Service 术语](terminology.md) | 在首次登录 AEMaaCS 之前，了解系统的一些术语及其基本结构会很有帮助。 | 系统管理员 |
| 3 | [Admin Console](admin-console.md) | 了解什么是 Admin Console，如何登录，以及如何以系统管理员身份验证您的配置文件。 | 系统管理员 |
| 4 | [分配 Cloud Manager 产品配置文件](assign-profiles-cloud-manager.md) | 查看 Cloud Manager 产品配置文件，了解如何将团队成员分配给 Cloud Manager 产品配置文件。 | 系统管理员 |
| 5 | [访问 Cloud Manager](cloud-manager.md) | 了解如何访问 Cloud Manager，以便您可以设置项目资源。 | 系统管理员 |
| 6 | [创建项目](create-program.md) | 了解如何使用 Cloud Manager 创建程序。 | 系统管理员 |
| 7 | [创建环境](create-environments.md) | 了解如何使用 Cloud Manager 创建环境。 | 系统管理员 |
| 8 | [分配 AEM 产品配置文件](assign-profiles-aem.md) | 瞭解系統管理員如何在AEMas a Cloud Service中將您的團隊成員指派給產品設定檔。 | 系统管理员 |
| 9 | [开发人员和部署管理员任务](developers.md) | 可選 — 作為開發人員，瞭解如何存取和管理Cloud Manager Git，以及作為部署管理員如何在Cloud Manager中設定管道和部署計畫碼。 | 开发人员和部署管理员 |
| 10 | [AEM 用户任务](aem-users.md) | 可選 — 作為AEM作者，瞭解如何存取AEMas a Cloud Service執行個體並熟悉AEMas a Cloud Service的撰寫內容。 | AEM 用户 |

## 后续内容 {#what-is-next}

您现在已经准备好开始您的 AEM as a Cloud Service 入门培训历程。 我們鼓勵您繼續下一段歷程並閱讀文章 [入門準備](preparation.md)

## AEM 文档历程 {#documentation-journeys}

[檔案歷程](/help/journey-documentation/documentation-journeys.md) 連結許多不同、複雜的主題和功能。 它提供的敘述有助於初次接觸AEM的讀者徹底理解和解決業務問題，同時假定讀者擁有最少的主題或AEM知識。

文档历程是围绕最佳实践准则而设计的，其中包含了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及来自客户项目的反馈。

如果您想瞭解有關如何將您的團隊上線到您的新AEMas a Cloud Service應用程式的Adobe建議，請從這裡開始！

<!-- ERROR: Not Found (HTTP error 404)
## Additional Resources {#additional-resources}

The following are additional, optional resources if you would like to go beyond the content of the onboarding journey.

* [AEM Champion Tips and Tricks - Cloud Manager Onboarding Playbook](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/expert-resources/aem-champions/onboarding-playbook.md) - Watch this video to learn Cloud Manager onboarding tips and trick from an AEM champion. -->


