---
title: Cloud Manager 简介
description: 了解Cloud Manager如何通过其程序、环境和管道支持您的AEM项目。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 2d793f22e554c2a4bde8831b5053d1640ba07c70
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 4%

---

# Cloud Manager 简介 {#intro-cloud-manager}

Cloud Manager是AEMas a Cloud Service的一个基本组件，是您团队的单个入口点。 其专门构建的CI/CD管道可确保彻底的测试和最高的代码质量，以提供卓越的体验。 为确保客户能够快速启动其项目，Cloud Manager以自助方式提供了所需的一切功能，包括创建云资源和环境以及访问git存储库的功能。 这些功能支持企业开发设置，使团队能够致力于频繁执行更改、快速提供卓越的数字体验并加快实现价值的时间。

系统管理员负责设置您的Cloud Manager团队，该团队将包括将创建您的云资源和开发人员的个人。 有关如何设置和扩展企业开发团队以及查看AEM as a Cloud Service如何支持您的开发过程的详细信息，请参阅此文档 [AEMas a Cloud Service的企业团队开发设置。](/help/implementing/cloud-manager/managing-code/enterprise-team-dev-setup.md)

## 导航到Cloud Manager的概述页面 {#navigate-cloud-manager}

按照以下步骤导航到Cloud Manager。

1. 导航到Cloud Manager的登录页面( [`https://my.cloudmanager.adobe.com`.](https://my.cloudmanager.adobe.com/).

1. 从Cloud Manager的 **计划和产品** 页面 **概述** 页面。

您还可以按照以下步骤操作，从Adobe Experience Cloud主页导航到Cloud Manager的“程序和产品”页面。

1. 导航到Adobe Experience Cloud(位于 [`https://experience.adobe.com`](https://experience.adobe.com) 和使用Adobe ID登录。

1. 通过引用工具栏右上角显示的组织名称，确保您处于正确的组织中。

1. 选择 **Experience Manager**.

1. 在 **Cloud Manager** 卡片，单击 **Launch**

## Cloud Manager中基于角色的权限 {#role-based-permissions}

| 权限 | 描述 | 业务所有者 | 部署管理器 | 项目经理 | 开发人员 |
|--- |--- |--- |--- |--- |--- |
| 添加程序<br>编辑程序 | 添加新程序<br>添加或删除解决方案或加载项 | x |  |  |  |
| 创建环境 | 创建生产+暂存和开发环境 | x | x |  |  |
| 更新环境 | 更新生产+暂存和开发环境 | x | x |  |  |
| 删除开发环境 | 删除开发环境 | x | x |  |  |
| 管道设置 | 设置和编辑管道 |  | x |  |  |
| 管道执行 | 启动管道 | x | x |  |  |
| 管道执行 | 拒绝/批准重要的3层质量门故障 | x | x | x |  |
| 管道执行 | 提供上线批准 | x | x | x |  |
| 管道执行 | 计划生产部署 | x | x | x |  |
| 管道删除 | 允许删除管道 |  | x |  |  |
| 执行取消 | 取消当前执行 |  | x |  |  |
| 生成个人访问令牌 | 访问Git |  | x |  | x |

>[!NOTE]
>
>可以将用户分配到多个角色。 例如，分配两者 **业务所有者** 和 **部署管理器** 角色授予用户这些权限的总和。

## Cloud Manager程序 {#cloud-manager-programs}

Cloud Manager计划代表一组Cloud Manager环境，支持业务计划的逻辑分组。 这些分组通常对应于购买的服务级别协议(SLA)。 例如，一个程序可以表示AEM资源以支持组织的公共网站，而另一个程序则表示内部DAM。


看这个 [视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 了解有关使用Cloud Manager程序的更多信息。

用户可以创建 **沙盒** 或 **生产** 项目。

* A **生产计划** 用于在将来的适当时间启用实时流量。
   * 请参阅该文档 [生产计划简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) 以了解更多详细信息。

* A **沙盒程序** 通常创建目的是为培训、运行演示、启用、创建POC或提供文档。
   * 它不用于传输实时流量，并且具有生产程序不会受到的限制。
   * 它包含站点和资产，并且会自动填充一个git分支，该分支包含示例代码、开发环境和非生产管道。
   * 请参阅该文档 [沙盒程序简介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) 以了解更多详细信息。

## Cloud Manager环境 {#cloud-manager-environments}

您的云环境将通过Cloud Manager创建、访问和查看。 这些环境可以是生产、暂存或开发环境。 不同的环境具有不同的用途，可以与不同的CI/CD管道一起使用。 环境由以下服务组成：

* [AEM Authoring Services](#author-services)
* [AEM Publishing Services](#publish-services)
* [Dispatcher Services](#dispatcher-services)

>[!TIP]
>
> 请参阅视频 [使用AdobeCloud Manager环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 可用环境的概述。
>
>请参阅文档 [管理环境](/help/implementing/cloud-manager/manage-environments.md) 要进一步了解用户可以创建的环境类型以及用户如何创建环境。

### AEM创作服务 {#author-services}

在创建、管理和更新网站内容和数字资产的环境中，包含AEM创作服务。 通常，只有内部用户才有权访问创作服务，该服务在登录屏幕后进行维护。 创作服务同时用作创作和预览环境。

### AEM Publishing Service {#publish-services}

AEM发布服务包含在托管最终用户体验的环境中，如网站。 这是网站访客可查看并与之交互的服务。 通常，发布服务是公开提供的。

### AEM Dispatcher Service {#dispatcher-services}

调度程序是 `Apache HTTP Web server` 模块，提供位于AEM发布服务之前的安全性和性能层。
