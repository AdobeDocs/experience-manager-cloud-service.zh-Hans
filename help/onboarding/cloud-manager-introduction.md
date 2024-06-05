---
title: Cloud Manager 简介
description: 了解 Cloud Manager 如何通过其程序、环境和管道支持您的 AEM 项目。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 100%

---


# Cloud Manager 简介 {#intro-cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要组成部分，是您团队的单一入口点。 其专门构建的 CI/CD 管道可确保彻底的测试和最高的代码质量，从而提供卓越的体验。 为了确保客户能够快速启动项目，Cloud Manager 以自助方式提供所需的一切，包括创建云资源和环境以及 Git 存储库访问权限。 这些功能允许企业进行开发设置，因此团队可以经常进行更改，快速提供卓越的数字体验，并加快价值实现。

您的系统管理员负责为您建立云管理团队，其中包括将创建云资源和开发人员的个人。有关如何设置和扩展企业开发团队以及 AEM as a Cloud Service 如何支持您的开发过程的更多信息，请参阅 [AEM as a Cloud Service 的企业团队开发设置。](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## 导航到 Cloud Manager 的概述页面 {#navigate-cloud-manager}

按照以下步骤导航到 Cloud Manager。

1. 导航至 Cloud Manager 的登录页面，网址为 [`https://my.cloudmanager.adobe.com`。](https://my.cloudmanager.adobe.com/)

1. 在 Cloud Manager 的&#x200B;**程序和产品**&#x200B;页面中选择程序，可启动&#x200B;**概述**&#x200B;页面。

您还可以按照以下步骤从 Adobe Experience Cloud 主页导航到 Cloud Manager 的程序和产品页面。

1. 导航至 Adobe Experience Cloud，网址为 [`https://experience.adobe.com`](https://experience.adobe.com) 并使用 Adobe ID 登录。

1. 根据工具栏右上角显示的组织名称，确定您在正确的组织。

1. 选择 **Experience Manager**。

1. 在 **Cloud Manager** 信息卡上，单击&#x200B;**启动**

## Cloud Manager 中基于角色的权限 {#role-based-permissions}

| 权限 | 描述 | 业务负责人 | 部署管理员 | 项目管理员 | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加程序<br>编辑程序 | 添加新程序<br>添加或移除解决方案或插件 | x |  |  |  |
| 创建环境 | 创建生产+暂存和开发环境 | x | x |  |  |
| 更新环境 | 更新生产+暂存和开发环境 | x | x |  |  |
| 删除开发环境 | 删除开发环境 | x | x |  |  |
| 管道设置 | 设置和编辑管道 |  | x |  |  |
| 管道执行 | 启动管道 | x | x |  |  |
| 管道执行 | 拒绝/批准重要的三级质量关卡故障 | x | x | x |  |
| 管道执行 | 提供上线批准 | x | x | x |  |
| 管道执行 | 计划生产部署 | x | x | x |  |
| 管道删除 | 允许删除管道 |  | x |  |  |
| 执行取消 | 取消当前执行 |  | x |  |  |
| 生成个人访问令牌 | 访问 Git |  | x |  | x |
| 创建 RDE | 创建快速开发环境 | x |  |  | x |
| 重置 RDE | 重置快速开发环境 | x |  |  | x |
| 创建/修改内容集 | 为内容复制创建或修改内容集 |  | x |  |  |
| 开始/取消内容复制 | 开始或取消内容复制过程 |  | x |  |  |

>[!NOTE]
>
>一个用户可以分配给多个角色。例如，将&#x200B;**业务负责人**&#x200B;和&#x200B;**部署管理员**&#x200B;角色分配给用户，将为用户提供所有这些权限。

>[!TIP]
>
>还提供具有可配置权限的自定义权限配置文件。有关更多详细信息，请参阅[自定义权限](/help/implementing/cloud-manager/custom-permissions.md)文档。

## Cloud Manager 程序 {#cloud-manager-programs}

Cloud Manager 程序代表一系列支持业务计划逻辑分组的 Cloud Manager 环境。 这些分组通常对应于购买的服务级别协议 (SLA)。 例如，一个程序可能表示支持组织公共网站的 AEM 资源，而另一个程序表示内部 DAM。


观看此[视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)，了解有关使用 Cloud Manager 程序的更多信息。

用户可以创建&#x200B;**沙盒**&#x200B;或&#x200B;**生产**&#x200B;程序。

* 创建&#x200B;**生产程序**，以便在未来适当时间启用实时流量。。
   * 请参阅[生产程序简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)，了解更多详细信息。

* 通常，创建&#x200B;**沙盒程序**&#x200B;是为了提供培训、运行演示、支持、创建概念验证 (POC) 或归档等目的。
   * 该程序并不会承载实时流量，并且会有制作程序所没有的限制。
   * 它包括 Sites 和 Assets，交付时自动填充 Git 分支，其中包括示例代码、开发环境和非生产管道。
   * 请参阅[沙盒简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)，了解更多详细信息。

## Cloud Manager 环境 {#cloud-manager-environments}

您的云环境可通过 Cloud Manager 创建、访问和查看。 这些环境可以是生产、暂存或开发环境。 不同的环境有不同的用途，可以与不同的 CI/CD 管道一起使用。 环境由以下服务组成：

* [AEM 创作服务](#author-services)
* [AEM 发布服务](#publish-services)
* [Dispatcher 服务](#dispatcher-services)

>[!TIP]
>
> 请参阅视频[使用 Adobe Cloud Manager 环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)，了解可用环境的概述。
>
>请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)，了解有关用户可以创建的环境类型以及用户如何创建环境的更多信息。

### AEM 创作服务 {#author-services}

AEM 创作服务包含在创建、管理和更新网站内容和数字资源的环境中。通常只有内部用户可以访问创作服务，并在登录屏幕后进行维护。创作服务同时充当创作和预览环境。

### AEM 发布服务 {#publish-services}

AEM 发布服务包含在承载最终用户体验的环境中，如网站。这是网站访客将查看和交互的服务。通常，发布服务是公开可用的。

### AEM Dispatcher 服务 {#dispatcher-services}

Dispatcher 是`Apache HTTP Web server`提供位于 AEM 发布服务前面的安全和性能层的模块。
