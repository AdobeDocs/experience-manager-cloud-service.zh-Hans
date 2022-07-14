---
title: 开发人员和部署管理器任务
description: 系统管理员设置必要的云资源后，了解开发人员和部署经理如何访问git以开发应用程序并使用管道来部署它们。
feature: Onboarding
role: Admin, User, Developer
exl-id: f57a856b-0932-4e8f-be59-a19fe692e2ab
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 2%

---


# 开发人员和部署管理器任务 {#developer-deployment-manager}

在 [入门历程，](overview.md) 您将了解开发人员和部署管理器如何访问git以开发应用程序并使用管道来部署它们。

## 迄今为止的故事 {#story-so-far}

你的登机之旅已经走过了很长的路！ 恭喜！系统管理员已通过设置必要的云资源并授予文档中的访问权限，完成了载入历程 [分配AEM产品配置文件。](assign-profiles-aem.md)

此时，您的开发人员和部署经理可以开始创建您自己的应用程序，而AEM用户则可以开始创建内容。 从这个意义上讲，您的入门操作已完成，现在该使用新的AEMas a Cloud Service系统了，本文档将说明这一点。

## 受众 {#audience}

因此，本文件是从 **开发人员** 和 **部署管理器**.

系统管理员也可以执行这些相同的任务，但通常这些角色由不同的用户担任。

## 目标 {#objective}

本文档是载入历程的补充，旨在演示系统管理员载入所有用户并创建必要的云资源后，开发人员和部署经理的基本任务。

阅读本文档后，您应：

* 作为开发人员，了解如何访问和管理Cloud Manager git存储库。
* 作为部署管理器，您可以在Cloud Manager中设置管道并部署代码。

## 开发人员和部署管理器 {#roles}

系统管理员完成创建用户和设置云资源等主要入门任务后，通常最渴望访问系统的用户是开发人员和部署经理。 这是因为他们是负责基于AEMas a Cloud Service构建自定义应用程序的用户。

* **开发人员**  — 这些用户访问Cloud Manager git存储库，以管理您的AEM自定义应用程序的代码。
* **部署管理器**  — 这些用户使用Cloud Manager创建并运行管道，以将代码从git存储库部署到运行的AEM环境。

根据您的组织需求，同一用户可以同时具有两个角色。

## 前提条件 {#prerequisites}

在您以开发人员或部署管理员的身份开始本文档中描述的任务之前，请确保系统管理员已完成此载入历程中的所有步骤。 这意味着：

* 系统管理员已将开发人员和部署经理分配给各自的产品配置文件。
* 此外，开发人员还必须分配到 **AEM用户** 或 **AEM管理员** 产品配置文件，以便也使用AEM。
* 云资源已设置。

## 访问Git {#accessing-git}

您可以使用Cloud Manager中的自助式git帐户管理来访问和管理git存储库。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡片 **计划概述** 页面并查找 **访问存储库信息** 按钮以访问和管理您的git存储库。

   ![“环境”卡上的“访问Repo信息”按钮](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 单击 **查看存储库信息** 按钮以打开要查看的对话框：

   * 指向Cloud Manager git存储库的URL。
   * git用户名。
   * git密码，其值在 **生成密码** 按钮。

   ![存储库信息](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用这些凭据，用户可以克隆存储库的本地副本，并在该本地存储库中进行更改，准备就绪后，可以将任何代码更改提交回Cloud Manager中的远程代码存储库。

## 管道设置 {#setup-pipeline}

开发人员将其自定义代码添加到您的git存储库后，部署管理器可以创建并执行管道以将该代码部署到您的AEM环境。

按照以下步骤创建您的第一个非生产部署管道。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 访问 **管道** Cloud Manager主屏幕中的信息卡。 单击 **+添加** 选择 **添加非生产管道**.

   ![添加非生产管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **配置** 选项卡 **添加非生产管道** 对话框中，选择要添加的非生产管道类型。 对于此示例，请选择 **部署管道**.

   ![“添加非生产管道”对话框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生产管道名称** 以标识您的管道以及以下其他信息。

1. 对于 **部署触发器** 选择 **手动** 这样管道才会在启动时运行。

1. 单击 **继续**.

1. 在 **源代码** 选项卡 **添加非生产管道** 对话框中，必须选择管道应处理的代码类型。 对于此示例，请选择 **完整堆栈代码**.

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **符合条件的部署环境**  — 必须选择管道应部署到的环境。
   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
      * 输入分支名称的前几个字符，此字段的自动完成功能将找到匹配的分支以帮助您选择。

   ![全栈管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 单击&#x200B;**保存**。

您现在已创建第一个管道！ 具有部署管理员角色的用户现在可以从Cloud Manager UI中启动管道。

## 部署 {#deploy}

现在，开发人员已将其自定义代码添加到git存储库，并且您已创建用于部署该代码的管道，接下来该执行管道以将该代码从git实际移动到您的环境。

![Cloud Manager中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/pipelines-card.png)

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面上，单击在上一部分中创建的管道旁边的省略号按钮，然后选择 **运行** 中。

1. 管道运行开始，并由 **状态** 列。

您可以通过再次单击省略号按钮并选择来查看运行的详细信息 **查看详细信息**.

恭喜！您现在已将代码从git存储库部署到非生产环境！

## 下一步 {#whats-next}

现在，您已阅读本文档，接下来应：

* 作为开发人员，了解如何访问和管理Cloud Manager git存储库。
* 作为部署管理器，您可以在Cloud Manager中设置管道并部署代码。

您不仅具有Cloud Manager的工作知识，还具有工作环境、存储库和管道的知识，因此您已经开始以开发人员或部署管理器的身份运行！ 但是，要了解AEM as a Cloud Service的强大CI/CD工具，还有更多内容。 查看 [其他资源](#additional-resources) 部分以了解更多详细信息。

如果您对内容作者如何访问和使用AEM as a Cloud Service感兴趣，请继续进入入门历程的最后部分， [AEM用户任务。](aem-users.md)

>[!TIP]
>
>现在，您已载入， [了解如何轻松添加AEM参考演示附加组件](/help/journey-sites/demos-add-on/overview.md) 沙盒环境中配置的AEM最少，并且能够根据最佳实践通过丰富的示例测试AEM的强大功能。

## 其他资源 {#additional-resources}

* [访问存储库](/help/implementing/cloud-manager/managing-code/accessing-repos.md)  — 了解如何使用Cloud Manager中的自助式git帐户管理访问和管理您的git存储库。
* [在Cloud Manager中使用Git](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)  — 了解如何使用Cloud Manager的git存储库，以及如何将您自己的内部部署客户管理的git存储库与Cloud Manager集成。
* [本地开发环境设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)  — 本教程将指导您使用AEM AEM SDK为Adobe Experience Manager(as a Cloud Service)设置本地开发环境。
* [AEM Sites入门 — WKND教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)  — 本多部分教程专为初次使用Adobe Experience Manager(AEM)的开发人员设计。 本教程将指导您实施AEM网站，以打造虚构的生活方式品牌WKND。 本教程涵盖一些基本主题，如项目设置、核心组件、可编辑模板、客户端库，以及使用Adobe Experience Manager Sites进行组件开发。
* [AEM中的SPA使用React快速入门](/help/implementing/developing/hybrid/getting-started-react.md)  — 本文提供了一个SPA应用程序示例，介绍了应用程序的组合方式，并允许您使用React框架快速启动并运行自己的SPA。
* [AEM SPA使用Angular入门](/help/implementing/developing/hybrid/getting-started-angular.md)  — 本文提供了一个SPA应用程序示例，介绍了它的组合方式，并允许您使用Angular框架快速启动并运行自己的SPA。
* [无头开发人员历程](/help/journey-headless/developer/overview.md)  — 从此处开始，参加使用AEM开发无头应用程序的指导课程。
