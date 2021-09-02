---
title: 了解什么是Cloud Manager
description: 请阅读本页面，了解Cloud Manager、Cloud Manager程序和环境。
exl-id: b743f126-b34e-4f48-a3f0-5dbd4e1ac34e
source-git-commit: 900bcfd2b05b7c996c7ef51118d1f09a16020332
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# Cloud Manager 简介 {#intro-cloud-manager}

Cloud Manager是AEM作为Cloud Service的基本组件，是您团队的单个入口点。

为了支持具有企业开发设置的客户，AEM as a Manager与Cloud Manager及其专门构建的CI/CD管道充分集成，这些管道旨在确保彻底的测试和最高的代码质量，以提供卓越的体验。

为确保客户能够以AEM as a Cloud Service的方式快速入门，Cloud Manager以自助服务方式提供了开始所需的一切功能，包括创建云资源和环境的功能。 通过这种方式，您的AEM开发人员可以通过Cloud Manager访问Git存储库。 使用Cloud Manager，开发团队可以努力以自助方式频繁提交更改。

您的系统管理员将负责设置您的Cloud Manager团队，该团队将包括将创建您的云资源和开发人员的个人。 请参阅[AEM as a Cloud Service的企业团队开发设置](/help/implementing/cloud-manager/enterprise-team-dev-setup.md) ，了解Cloud Manager如何在企业团队开发设置中支持。

## 导航到Cloud Manager的概述页面 {#navigate-cloud-manager}

按照以下步骤导航到Cloud Manager:

1. 从[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)直接导航到Cloud Manager的登录页面。

   >[!NOTE]
   >请将此页面加入书签以供将来参考，并帮助您直接导航到Cloud Manager的登陆页面。

1. 从Cloud Manager的&#x200B;**程序和产品**&#x200B;页面中选择程序，以启动&#x200B;**概述**&#x200B;页面。

此外，您还可以从Adobe Experience Cloud主页导航到Cloud Manager的“程序和产品”页面。 应遵循以下步骤：

1. 直接导航到[Adobe Experience Cloud](https://experience.adobe.com/#/@foundationinternal/home)，然后使用Adobe ID登录。

1. 选择&#x200B;**Experience Manager**。

1. 从Cloud Manager卡片中单击&#x200B;**Launch**。 成功登录到Cloud Manager后，即可使用用户界面(UI)。

成功登录后，系统会将您定向到Cloud Manager的登陆页面。

## Cloud Manager程序 {#cloud-manager-programs}

Cloud Manager计划表示一组Cloud Manager环境，这些环境支持业务计划的逻辑集，通常对应于购买的服务级别协议(SLA)。 例如，一个项目可以表示支持全球公共网站的AEM资源，而另一个项目则表示内部中央DAM。 请观看此[视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)，了解有关使用Cloud Manager程序的更多信息。

用户可以创建&#x200B;**Sandbox**&#x200B;或&#x200B;**Production**&#x200B;程序。

* 创建&#x200B;*生产程序*以在将来的适当时间启用实时流量。
有关更多详细信息，请参阅[生产程序简介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/production-programs/introduction-production-programs.html?lang=en)。

* 通常，创建&#x200B;*沙盒项目*是为了用于培训、运行演示、启用、POC或文档目的。 它不用于传输实时流量，并且将具有生产程序不会受到的限制。 它将包含站点和资产，并且将使用自动填充的Git分支来交付，该分支包含示例代码、开发环境和非生产管道。
有关更多详细信息，请参阅[沙盒程序简介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/sandbox-programs/introduction-sandbox-programs.html?lang=en)。

## Cloud Manager环境 {#cloud-manager-environments}

您的云环境将通过Cloud Manager创建、访问和查看。 这些环境可以是生产环境、暂存环境或开发环境。 不同的环境支持不同的目的，并且可以使用不同的CI/CD管道参与。 环境由以下服务组成：

* [AEM创作服务](#author-services)
* [AEM发布服务](#publish-services)
* [Dispatcher Services](#dispatcher-services)

   >[!NOTE]
   > 请参阅视频[使用Cloud Manager环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager) ，了解有关可用环境的更多信息。 此外，请参阅[管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) ，了解有关用户可以创建的环境类型以及用户如何创建环境的更多信息。

### AEM创作服务 {#author-services}

AEM创作服务包含在创建、管理和更新网站内容和数字资产的环境中。 通常，只有内部用户才有权访问创作服务，并位于登录屏幕后面。 创作服务既可作为创作环境，也可作为预览环境。

### AEM发布服务 {#publish-services}

AEM发布服务包含在托管最终用户体验的环境中，如网站。 这是网站访客可查看并与之交互的服务。 通常，发布服务是公开可用的。

### AEM Dispatcher Service {#dispatcher-services}

Dispatcher是一个`Apache HTTP Web server`模块，提供位于AEM发布服务前面的安全性和性能层。
