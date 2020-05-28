---
title: 执行阶段
description: 执行阶段
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---


# 执行 {#execution-phase}

在开始执行阶段之前，您应已载入云服务。 您还需要熟悉Cloud Manager，因为它是将代码部署到AEM Cloud Service的唯一机制。

Cloud Manager使组织能够在云中自行管理AEM。 它包含一个持续集成和持续交付 (CI/CD) 框架，使 IT 团队和实施合作伙伴能够在不影响性能或安全性的情况下快速交付自定义或更新。

有关更多详细信息，请参阅以下资源：

* [以云服务形式加入Experience](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/onboarding/home.html) Manager，了解有关以云服务形式加入Experience Manager的自助资源。

* [将Git与Adobe Cloud Manager集成](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) ，了解如何使用Single Git存储库部署代码。

* [Adobe Experience as a Cloud Service Configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) ，了解如何在Admin Console中管理产品和用户访问。


## 简介 {#introduction}

过渡到云服务的确切步骤取决于您购买的系统以及遵循的软件开发生命周期惯例。

下图显示了执行阶段涉及的主要步骤：

![图像](/help/move-to-cloud-service/assets/exec-image1.png)

## 内容传输 {#content-transfer}

要将内容从当前AEM实例传输到Cloud Service实例，可使用Adobe的内容传输工具。

利用此工具，您可以指定要从源AEM实例传输到AEM Cloud服务实例的所需内容子集。

>[!NOTE]
>建议在云服务上线之前，频繁进行差异内容补充，以缩短最终差异内容传输的内容冻结期。

有关更多 [详细信息](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) ，请参阅内容传输工具。

>[!IMPORTANT]
>内容传输工具的最低系统要求为AEM 6.3 +和JAVA 8。 如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5，才能使用内容传输工具。

## 代码重构 {#code-refactor}

在AEM中作为云服务开发和运行代码需要改变思路。 应当指出，代码必须具有弹性，尤其是当实例可能随时停止时。 云服务中运行的代码必须知道它始终在群集中运行。 这意味着始终有多个实例在运行。

AEM Maven项目需要进行某些更改才能与AEM作为云服务进行兼容。 AEM作为云服务，需要将内容和 *代码分* 离 *为离* 散包，以部署到AEM。

* `/apps` 和 `/libs` 被视为 AEM 中的不可变区域，因为 AEM 启动后（例如，运行时），无法对其进行更改（创建、更新、删除）。运行时对不可改变区域所做的任何更改尝试都将失败。

* 存储库中的其 `/content` 他所有 `/conf` 内容， `/var` 、 、 `/home` 、 `/etc` 、 `/oak:index` 、 `/system` 、 `/tmp` 、等。 是所有可变区域，这意味着它们可以在运行时更改。

有关更多 [详细信息，请参](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) 阅推荐的包结构。

在AEM上作为云服务进行开发时，您需要了解一些其他开发准则。 请参阅 [AEM云服务开发指南](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) ，了解更多信息。

在规划阶段，您应当有一列表需要重构的区域，以与云服务兼容。 您还应查看开 [发指南](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) ，了解有关如何重新调整和优化代码以迁移到云服务的更多详细信息。

要帮助加速某些代码重构任务，您可以使用以下工具：

* [资产工作流迁移](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [调度程序转换器](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [现代化工具](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

建议在通过Cloud Manager Git将代码推送到云服务环境之前，在本地重新调整并测试该代码。

查 [看AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) 文档以了解更多信息。

下面列出了一些其他资源：

* 观看安装Dispatcher SDK，了解如何安装Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* 观看配置Dispatcher SDK以了解如何配置Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* 查 [看本地开发设置](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) 文档以设置本地开发环境


要在活动AEM上管理正在进行的代码开发以及作为过渡旅程一部分的代码重构任务，建议您计划一个代码冻结期，直到您完成重组Maven项目以与AEM作为云服务进行兼容。

一旦项目重组完成，您就可以基于此新结构恢复新的代码开发。 这将减少代码部署和测试期间Cloud Manager管道故障。

>[!NOTE]
>内容传输和代码重构任务未按顺序完成。 这些任务可以相互独立地完成。 但是，需要正确的项目结构才能确保内容在云服务环境中成功呈现。

## 代码部署和测试的最佳实践 {#best-practices}

Cloud Manager for Cloud Services管道执行将支持执行针对舞台环境运行的测试。

请参阅 [代码质量测试](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) ，了解如何编写测试脚本以及建议的覆盖率至少为50%。

此外，请参阅了 [解自定义代码质量规则](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) ，进一步了解由Cloud Manager根据AEM Engineering的最佳实践创建的自定义代码质量规则。

Cloud Manager使用是将代码部署到云服务环境的唯一机制。

请访问以下资源，了解如何使用Cloud Manager管理和部署您的代码。

* [管理环境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [配置CI-CD管道](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [部署代码](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## 上线准备的最佳实践 {#go-live}

要确保AEM作为云服务顺利、成功地上线，您应考虑执行以下步骤：

* 计划代码和内容冻结期
* 执行最终内容向上
* 完成测试迭代
* 运行性能和安全测试
* 切换
