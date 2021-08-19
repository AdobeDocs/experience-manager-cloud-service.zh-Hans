---
title: 实施阶段
description: 实施阶段
exl-id: 176dd79d-0d72-443c-87db-dab24fb48b96
source-git-commit: 82e22f0a0684491b5071fa232a0f90fb87da6992
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 90%

---

# 实施 {#implementation-phase}

在开始执行阶段之前，您应该先了解云服务。您还需要熟悉 Cloud Manager，因为它是将代码部署到 AEM 云服务的唯一机制。

Cloud Manager 使组织能够在云中自行管理 AEM。它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。

有关更多信息，请参阅以下资源：

* [Experience Manager as a Cloud Service 入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html)，了解有关 Experience Manager as a Cloud Service 入门的自助资源。

* [将 Git 与 Adobe Cloud Manager 集成](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)，了解使用 Single Git 存储库来部署代码的相关信息。

* [Adobe Experience as a Cloud Service 配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html#aem-configuration)，了解有关在 Admin Console 中管理产品和用户访问权限的信息。


## 简介 {#introduction}

您过渡到云服务的确切步骤取决于您所购买的系统以及所遵循的软件开发生命周期惯例。

下图显示了执行阶段所包含的主要步骤：

![图像](/help/move-to-cloud-service/assets/exec-image1.png)

## 内容传输 {#content-transfer}

要将内容从当前 AEM 实例传输到 Cloud Service 实例，您可以使用 Adobe 的内容传输工具。

利用此工具，您可以指定要从源 AEM 实例传输到 AEM 云服务实例的所需内容子集。

>[!NOTE]
>建议在云服务上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。

有关更多信息，请参阅[内容传输工具](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md)。

>[!IMPORTANT]
>内容传输工具的最低系统要求为 AEM 6.3 + 和 JAVA 8。如果您使用的是较低版本的 AEM，则需要将内容存储库升级到 AEM 6.5，才能使用内容传输工具。

## 代码重构 {#code-refactor}

在 AEM as a Cloud Service 中开发和运行代码时，需要改变思维定式。需要注意的是，代码必须是可复原的，尤其是在实例可能随时停止时。在云服务中运行的代码必须意识到它始终在群集中运行这一事实。这意味着始终会有多个实例在运行。

AEM Maven 项目需要进行某些更改才能与 AEM as a Cloud Service 兼容。AEM as a Cloud Service 需要将&#x200B;*内容*&#x200B;和&#x200B;*代码*&#x200B;分离到单独的包中，才能将其部署到 AEM 中。

* `/apps` 和 `/libs` 被视为 AEM 中的不可变区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。运行时对不可改变区域所做的任何更改尝试都将失败。

* 存储库中的其他所有内容，`/content`、`/conf`、`/var`、`/home`、`/etc`、`/oak:index`、`/system`、`/tmp` 等都是可变区域，这意味着可在运行时对这些区域进行更改。

有关更多信息，请参阅[推荐的包结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure)。

在 AEM as a Cloud Service 上进行开发时，还需要了解一些其他开发准则。请参阅 [AEM as a Cloud Service 开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)，以了解详情。

从规划阶段开始，您就应该确定一个需要进行重构才能与云服务兼容的区域列表。您还应该查看[开发准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html)，了解更多有关如何重构和优化代码以移动到云服务的详细信息。

要帮助加速某些代码重构任务，您可以使用以下工具：

* [资产工作流迁移](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [现代化工具](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

建议先在本地重构和测试代码，然后再通过 Cloud Manager Git 将代码推送到云服务环境。

查看 [AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) 文档以了解更多信息。

下面列出了一些其他资源：

* 观看安装 Dispatcher SDK 视频，了解如何安装 Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 观看配置 Dispatcher SDK 视频，了解如何配置 Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* 查看[本地开发设置](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)文档以设置本地开发环境


要管理活动 AEM 上正在进行的代码开发以及过渡历程中的代码重构任务，建议在完成 Maven 项目重组以与 AEM as a Cloud Service 兼容之前，设置一个代码冻结期。

项目重组完成后，您可以基于这个新结构继续新的代码开发。这将减少在代码部署和测试期间出现的 Cloud Manager 管道故障。

>[!NOTE]
>内容传输和代码重构任务不必按顺序完成。这些任务可以相互独立地完成。但是，需要使用正确的项目结构来确保内容在云服务环境中成功呈现。

## 代码部署和测试的最佳实践 {#best-practices}

云服务的 Cloud Manager 管道执行将支持执行针对暂存环境运行的测试。

请参阅[代码质量测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing)，了解有关编写测试脚本以及建议覆盖率至少为 50% 的信息。

另外，请参阅[了解自定义代码质量规则](/help/implementing/cloud-manager/custom-code-quality-rules.md)，以了解与基于 AEM Engineering 中的最佳实践创建并由 Cloud Manager 执行的自定义代码质量规则有关的更多信息。

使用 Cloud Manager 是将代码部署到云服务环境的唯一机制。

请访问以下资源，了解如何使用 Cloud Manager 来管理和部署您的代码。

* [管理环境](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [配置 CI-CD 管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [部署代码](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)


