---
title: 开发人员和部署管理员任务
description: 一旦系统管理员设置了必要的云资源，就可以了解开发人员和部署经理如何访问 Git 来开发应用程序并使用管道来部署它们。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: bceec9ea6858b1c4c042ecd96f13ae5cac1bbee5
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 98%

---


# 开发人员和部署管理员任务 {#developer-deployment-manager}

在此[入门历程](overview.md) 可选部分，您会了解开发人员和部署经理如何访问 Git 来开发应用程序并使用管道来部署它们。

## 迄今为止的故事 {#story-so-far}

您已经完成了入门历程的很多内容！ 恭喜！系统管理员通过在文档[分配 AEM 产品配置](assign-profiles-aem.md)文件中设置必要的云资源并授予访问权限，已经完成了入门历程。

此时，开发人员和部署管理员可以开始创建自己的应用程序，而 AEM 用户可以开始创建内容。 从这个意义上说，您的载入已经完成，现在可以使用您的新 AEM as a Cloud Service 系统了，本文将对此进行说明。

## 受众 {#audience}

因此，本文档是从&#x200B;**开发人员**&#x200B;和&#x200B;**部署管理员**&#x200B;角度编写的。

系统管理员也可以执行这些相同的任务，但通常这些角色由不同的用户担任。

## 目标 {#objective}

本文档是对载入流程的补充，用于演示系统管理员将所有用户加入系统并创建必要的云资源后，显示开发人员和部署管理员的基本任务。

阅读本文档后，您应：

* 作为开发人员，了解如何访问和管理 Cloud Manager Git 存储库。
* 作为部署管理员，可以在 Cloud manager 中设置管道并部署代码。

## 开发人员和部署管理员 {#roles}

一旦系统管理员完成了创建用户和设置云资源的主要登录任务，通常最渴望访问系统的用户是开发人员和部署管理员。这是因为他们是负责在 AEM as a Cloud Service 的基础上构建自定义应用程序的用户。

* **开发人员** – 这些用户访问 Cloud Manager Git 存储库，他们将在其中管理 AEM 自定义应用程序的代码。
* **部署管理员** – 这些用户使用 Cloud Manager 创建并运行管道，将代码从 Git 存储库部署到运行中的 AEM 环境。

根据您的组织需要，相同的用户可以同时拥有两个角色。

## 前提条件 {#prerequisites}

在您以开发人员或部署管理员的身份开始本文档中描述的任务之前，请确保您的系统管理员已完成此载入流程中的所有步骤。 这意味着：

* 系统管理员已将开发人员和部署管理员分配给他们各自的产品配置文件。
* 开发人员还必须分配到 **AEM用户** 或 **AEM管理员** 产品配置文件也使用AEM。
* 已设置云资源。

## 访问 Git {#accessing-git}

您可以使用 Cloud Manager 中的自助 Git 帐户管理来访问和管理 Git 存储库。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡，您将发现&#x200B;**访问存储库信息**&#x200B;按钮，该按钮可用于访问和管理您的 Git 存储库。

   ![访问“环境”信息卡上的“存储库信息”按钮](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 单击&#x200B;**查看存储库信息**&#x200B;按钮，打开查看对话框：

   * Cloud Manager Git 存储库的 URL。
   * Git 用户名。
   * Git 密码，其值在单击&#x200B;**生成密码**&#x200B;按钮时显示。

   ![存储库信息](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用这些凭据，用户可以克隆存储库的本地副本，并在该本地存储库中进行更改，准备就绪后，可以将任何代码更改提交回 Cloud Manager 中的远程代码存储库。

## 管道设置 {#setup-pipeline}

一旦开发人员将其自定义代码添加到您的 Git 存储库中，部署管理员就可以创建并执行管道，将该代码部署到 AEM 环境中。

按照以下步骤创建第一个非生产部署管道。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从 Cloud Manager 主屏幕访问&#x200B;**管道**&#x200B;信息卡。 单击&#x200B;**+ 添加**&#x200B;并选择&#x200B;**添加非生产管道**。

   ![添加非生产管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**配置**&#x200B;选项卡上，选择要添加的非生产管道的类型。 对于此示例，请选择&#x200B;**部署管道**。

   ![“添加非生产管道”对话框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供&#x200B;**非生产管道名称**，识别您的管道以及以下附加信息。

1. 对于&#x200B;**部署触发器**，请选择&#x200B;**手动**，以便管道仅在启动时运行。

1. 单击&#x200B;**“继续”**。

1. 在&#x200B;**添加非生产管道**&#x200B;对话框的&#x200B;**源代码**&#x200B;选项卡上，您必须选择管道应处理的代码类型。对于此示例，请选择&#x200B;**全栈代码**。

1. 在&#x200B;**源代码**&#x200B;选项卡上，必须定义以下选项。

   * **符合条件的部署环境** – 您必须选择管道应部署到的环境。
   * **存储库** – 此选项定义管道应从中检索代码的 Git 存储库。
   * **Git 分支** – 此选项定义管道应从中检索代码的所选存储库的分支。
      * 输入分支名称的前几个字符，此字段的自动完成功能将查找匹配的分支帮助您做选择。

   ![全栈管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 单击“**保存**”。

您现在已经创建了第一条管道！ 具有部署管理员角色的用户现在可以从 Cloud manager UI 启动管道。

## 部署 {#deploy}

现在开发人员已经将他们的自定义代码添加到 Git 存储库中，并且您已经创建了一个管道来部署代码，现在可执行管道来将代码从 Git 实际移动到您的环境中了。

![Cloud Manager 中的管道信息卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 导航到&#x200B;**程序概述**&#x200B;页面中的&#x200B;**管道**&#x200B;信息卡，并单击您在前一节创建的管道旁边的省略号按钮，然后从菜单中选择&#x200B;**运行**。

1. 管道将开始运行，并在&#x200B;**状态**&#x200B;栏中显示运行状态。

您可以通过再次单击省略号按钮并选择&#x200B;**查看详细信息**&#x200B;来查看运行的详细信息。

恭喜！现在，您已经将代码从 Git 存储库部署到了非生产环境中！

## 后续内容 {#whats-next}

现在您已阅读本文档，您应：

* 作为开发人员，了解如何访问和管理 Cloud Manager Git 存储库。
* 作为部署管理员，可以在 Cloud manager 中设置管道并部署代码。

作为开发人员或部署管理员，您不仅具备 Cloud manager 的工作知识，而且还拥有工作环境、存储库和管道！ 但是，对于 AEM as a Cloud Service 强大的 CI/CD 工具，还有更多需要了解的地方。 查看[其他资源](#additional-resources)部分，了解更多详细信息。

如果您对内容作者如何访问和使用 AEM as a Cloud service 感兴趣，请继续进行入门历程的最后一部分 [AEM 用户任务。](aem-users.md)

>[!TIP]
>
>现在您已经成功载入，您可以[学习如何轻松地将 AEM 参考演示插件](/help/journey-sites/demos-add-on/overview.md)添加到具有最低 AEM 配置的沙盒环境中，并能够基于最佳实践通过丰富的示例测试 AEM 的强大功能。

## 其他资源 {#additional-resources}

如果您想了解入门历程以外的内容，以下是额外的可选资源。

* [访问存储库](/help/implementing/cloud-manager/managing-code/accessing-repos.md) – 了解如何使用 Cloud Manager 的自助 Git 帐户管理访问和管理 Git 存储库。
* [将 Git 和 Cloud Manager 结合使用](/help/implementing/cloud-manager/managing-code/integrating-with-git.md) – 了解如何使用 Cloud Manager 的 Git 存储库，以及如何将您自己的本地客户管理的 Git 储存库与 Cloud Manager 集成。
* [本地开发环境设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) – 本教程将指导您使用 AEM as a Cloud Service SDK 为 Adobe Experience Manager (AEM) 设置本地开发环境。
* [AEM Sites 入门 – WKND 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans) – 此教程包含多个部分，是为新加入 Adobe Experience Manager (AEM) 的开发人员设计的。本教程介绍了虚拟生活方式品牌 WKND 的 AEM 站点的实现。 此教程涵盖了项目设置、核心组件、可编辑模板、客户端库和使用 Adobe Experience Manager Sites 进行组件开发等基本主题。
* [在 AEM 中使用 React 快速入门 SPA](/help/implementing/developing/hybrid/getting-started-react.md) – 这篇文章介绍了一个 SPA 应用程序示例，解释 SPA 是如何进行组合，允许您通过 React 框架快速启动和运行自己的 SPA。
* [在 AEM 中使用 Angular 快速入门 SPA](/help/implementing/developing/hybrid/getting-started-angular.md) – 这篇文章介绍了一个 SPA 应用程序示例，解释 SPA 是如何进行组合，允许您通过 Angular 框架快速启动和运行自己的 SPA。
* [无头开发人员历程](/help/journey-headless/developer/overview.md) – 从此处开始，学习使用 AEM 开发无头应用程序的指导课程。
