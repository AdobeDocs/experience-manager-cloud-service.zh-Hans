---
title: 企业开发团队设置
description: 了解如何建立和扩展您的企业开发团队，并了解 AEM as a Cloud Service 如何支持您的开发过程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: cbeb3d8f5fa5cbf1839e1e8c5e651329b06e60a4
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 40%

---

# AEM as a Cloud Service的企业开发团队设置 {#enterprise-setup}

了解如何设置和扩展企业开发团队，并了解AEM (Adobe Experience Manager)as a Cloud Service如何支持您的开发过程。

## 简介 {#introduction}

为了支持客户进行企业开发设置，AEM as a Cloud Service 与 Cloud Manager 及其特设[专用 CI/CD 管道完全集成。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)这些管道和服务是基于最佳实践构建的，确保全面[测试和最佳代码质量。](/help/implementing/cloud-manager/code-quality-testing.md)

## Cloud Manager在企业团队开发设置中的支持 {#cloud-manager}

为了确保快速入门，Cloud Manager提供了立即开始开发数字体验所需的一切，包括用于存储自定义项的Git存储库，然后由Cloud Manager构建、验证和部署。

使用 Cloud Manager，开发团队可以在不依赖 Adobe 人员的情况下多次提交更改。

Cloud Manager 中提供了三种类型的环境。

* 开发
* 暂存
* 生产

可以使用非生产管道将代码部署到开发环境中。 暂存和生产环境总是同时存在，确保在作为最佳实践的生产部署之前进行验证，对此，生产管道使用[质量检验关](/help/implementing/cloud-manager/custom-code-quality-rules.md)来验证应用程序代码和配置更改。

生产管道首先将代码和配置部署到暂存环境，测试应用程序，最后部署到生产环境。

始终使用最新AEM as a Cloud Service改进功能更新的Cloud ServiceSDK允许直接使用开发人员的本地硬件进行本地开发。 这种方法可以在很短的周转时间内实现快速开发。 因此，开发人员可以留在他们熟悉的本地环境中，从各种各样的开发工具中进行选择，并在他们认为合适的时候推动开发环境或生产。

Cloud Manager支持灵活的多团队设置，可以根据企业的需求进行调整。 为了确保跨多个团队的稳定部署，Cloud Manager专用管道一起验证和测试来自所有团队的代码。 此方法有助于防止一个团队的更改影响所有团队的生产。

## 现实世界示例 {#real-world-example}

每个企业都有不同的需求，包括不同的团队设置、流程和开发工作流。 Adobe 将下面描述的设置用于几个项目，这些项目基于 AEM as a Cloud Service 提供体验。

例如，Adobe Creative Cloud 桌面版，如 Adobe Photoshop 或 Adobe Illustrator，包括可供最终用户使用的教程、示例和指南等内容资源。客户端应用程序以Headless方式使用AEM as a Cloud Service中的内容。 他们对AEM云发布层进行API调用，以将结构化内容检索为JSON流。 此外，AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#content-delivery)中的[内容交付网络(CDN)用于以最佳性能为结构化和非结构化内容提供服务。

参与该项目的团队遵循以下流程。

每个团队都使用自己的开发工作流，并有一个单独的Git存储库。 额外的共享Git存储库用于载入项目。 此Git存储库包含Cloud Manager Git存储库的根结构，包括共享的Dispatcher配置。

加入新项目需要在共享Git存储库根目录下的反应器Maven项目文件中列出。 对于Dispatcher配置，将在Dispatcher项目内创建一个新的配置文件。 然后，主Dispatcher配置将包含此文件。 每个团队负责自己的Dispatcher配置文件。 对共享Git存储库的更改很少，通常仅当载入新项目时才需要更改。 主要工作由每个项目团队在自己的Git存储库中完成。

![工作流程图](/help/implementing/cloud-manager/assets/team-setup1.png)

每个Git存储库都使用[AEM项目原型](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/developing/archetype/overview)设置，因此遵循设置AEM项目的最佳实践。 唯一的例外是Dispatcher配置，如上所述，该配置在共享Git存储库中完成。

每个团队使用一个简化的Git工作流，带有两个+ N分支，遵循Git流模型：

* 稳定发行版分支包含生产代码。

* 开发分支包含最新开发。

* 对于每个功能，都会创建一个新分支。

开发是在功能分支中完成的。 当功能完善时，将合并到开发分支中。 从开发分支中挑选已完成并验证的功能，并将其合并到稳定分支中。

所有更改均通过PR（拉取请求）完成。 质量关卡自动验证每个PR。 Sonar 用于代码的质量检查，并运行一组测试套件，确保新代码不会引入任何回归。

Cloud Manager Git存储库中的设置包含两个分支。

* 稳定发行版分支包含来自所有团队的生产代码。
* 开发分支包含来自所有团队的开发代码。

在开发或稳定分支中，每次推送到团队的Git存储库都会触发[GitHub操作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)。

所有项目都遵循稳定分支的相同设置。 推送到项目的稳定分支会自动推送到Cloud Manager Git存储库中的稳定分支。 推送到稳定分支会触发Cloud Manager中的生产管道。 任何团队每次推送到稳定分支都会触发生产管道。 如果所有质量关卡都通过，则会更新生产部署。

![推送图表](/help/implementing/cloud-manager/assets/team-setup2.png)

对开发分支的推送处理方式不同。 推送到团队Git存储库中的开发人员分支也会触发GitHub操作。 此操作会自动将代码推送到Cloud Manager Git存储库中的开发分支。 但是，此代码推送不会自动触发非生产管道。 对Cloud Manager API的调用会触发该事件。

运行生产管道包括通过提供的质量关卡检查所有团队的代码。 在代码部署到暂存环境后，将运行测试和审核，以使所有内容都按预期运行。 通过所有关卡后，这些更改将在没有任何中断或停机的情况下推广到生产环境。

对于本地开发，使用 [AEM as a Cloud Service 的 SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing)。 该SDK允许设置本地创作、发布和Dispatcher。 此工作流支持离线开发和快速回访。 有时只使用创作环境进行开发，但快速设置Dispatcher和发布环境允许在推送到Git存储库之前在本地测试所有内容。

每个团队的成员通常会从共享Git中签出代码，以获取自己的项目代码。 无需签出其他项目，因为这些项目是独立的。

![本地签出及 SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

这种真实的设置可以用作蓝图，然后根据企业的需要进行定制。 Git灵活的分支和合并概念允许根据每个团队的需求自定义上述工作流的变化。 AEM as a Cloud Service 支持所有这些变化，而不牺牲专用的 Cloud Manager 管道的核心价值。

>[!TIP]
>
>请参阅[使用多个Source Git存储库](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/managing-code/multiple-git-repos#managing-code)，了解有关此设置的更多信息。

### 多团队设置的注意事项 {#considerations}

使用Cloud Manager的Git存储库和生产管道，完整的生产代码始终通过所有质量关卡，并将其视为一个部署单元。 这样，生产系统始终处于运行状态，没有中断或停机。

相反，如果没有这样的系统，因为每个团队都可以单独部署，所以单个团队的更新可能会导致生产稳定性问题。 此外，需要协调和计划内停机才能推出更新。 随着团队数量的增加，协调工作会变得更加复杂，并且很快就无法管理。

如果在质量关卡中发现问题，生产不会受到影响，并且可以检测并修复问题，而无需 Adobe 人员介入。如果没有 Cloud Service，也未始终测试整个部署，部分部署可能会导致停机，需要请求回滚，甚至从备份进行完全恢复。部分测试还会导致其他问题，这些问题必须在以后解决，再次需要Adobe人员的协调和支持。

>[!TIP]
>
>对于任何多团队设置，定义一个治理模型和所有团队都必须遵循的一组标准至关重要。 之前的多团队设置蓝图允许跨更多团队进行扩展，您可以将其用作起点。
