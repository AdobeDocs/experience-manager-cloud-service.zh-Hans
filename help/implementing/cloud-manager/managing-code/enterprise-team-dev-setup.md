---
title: 企业开发团队设置
description: 了解如何建立和扩展您的企业开发团队，并了解 AEM as a Cloud Service 如何支持您的开发过程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: f19c4c71cf3b70331b9ccc56adf0bfd31e7edb2c
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 97%

---

# AEM as a Cloud Service 的企业开发团队设置 {#enterprise-setup}

了解如何建立和扩展您的企业开发团队，并了解 AEM as a Cloud Service 如何支持您的开发过程。

## 简介 {#introduction}

为了支持客户进行企业开发设置，AEM as a Cloud Service 与 Cloud Manager 及其特设[专用 CI/CD 管道完全集成。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 这些管道和服务是基于最佳实践构建的，确保全面[测试和最佳代码质量](/help/implementing/cloud-manager/code-quality-testing.md)。

## Cloud Manager 在企业团队开发设置中的支持 {#cloud-manager}

为了确保快速入门，Cloud Manager 提供了立即开始开发数字体验所需的一切，包括一个 git 存储库，用于存储定制，然后由 Cloud Manager 构建、验证和部署。

使用 Cloud Manager，开发团队可以在不依赖 Adobe 人员的情况下多次提交更改。

Cloud Manager 中提供了三种类型的环境。

* 开发
* 暂存
* 生产

可以使用非生产管道将代码部署到开发环境中。 暂存和生产环境总是同时存在，确保在作为最佳实践的生产部署之前进行验证，对此，生产管道使用[质量检验关](/help/implementing/cloud-manager/custom-code-quality-rules.md)来验证应用程序代码和配置更改。

生产管道首先将代码和配置部署到暂存环境，测试应用程序，最后部署到生产环境。

Cloud Service SDK 始终随着最新的 AEM as a Cloud Service 改进而更新，允许直接利用开发者的本地硬件进行本地开发。 这使得快速开发具有非常低的周转时间。 因此，开发人员可以留在他们熟悉的本地环境中，从各种各样的开发工具中进行选择，并在他们认为合适的时候推动开发环境或生产。

Cloud Manager 支持灵活的多团队设置，可以根据企业需求进行调整。 为了确保多个团队的稳定部署，同时避免一个团队影响所有团队的生产，Cloud Manager 专用管道总是一起验证和测试所有团队的代码。

## 现实世界示例 {#real-world-example}

每个企业都有不同的需求，包括不同的团队设置、流程和开发工作流。 Adobe 将下面描述的设置用于几个项目，这些项目基于 AEM as a Cloud Service 提供体验。

例如，Adobe Creative Cloud 桌面版，如 Adobe Photoshop 或 Adobe Illustrator，包括可供最终用户使用的教程、示例和指南等内容资源。使用 AEM as a Cloud Service 的客户端应用程序以无头方式使用此内容，方法是对 AEM 云发布层进行 API 调用，检索作为 JSON 流的结构化内容，并利用 [AEM as a Cloud Service 中的 Content Delivery Network (CDN)](/help/implementing/dispatcher/cdn.md#content-delivery) 以最佳性能为结构化和非结构化内容提供服务。

参与该项目的团队遵循以下流程。

每个团队都使用自己的开发工作流，并有一个单独的 git 存储库。 还有额外的共享 git 存储库用于载入项目。 此 git 存储库包含 Cloud Manager 的 git 存储库根结构，包括共享分发程序配置。

加入新项目需要在共享 git 存储库根目录下的 Reactor Maven 项目文件中列出。 对于 Dispatcher 配置，将在 Dispatcher 项目内创建一个新的配置文件。 然后，主 Dispatcher 配置将包含此文件。 每个团队负责自己的 Dispatcher 配置文件。 对共享 git 存储库的更改很少，通常只有在新项目上线时才需要更改。 主要工作由每个项目团队在自己的 git 存储库中完成。

![工作流程图](/help/implementing/cloud-manager/assets/team-setup1.png)

每个 git 存储库都是使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)设置的，因此遵循设置 AEM 项目的最佳实践。 唯一的例外是在共享 git 存储库中进行的 Dispatcher 配置，如上所述。

每个团队使用一个简化的 git 工作流，带有两个 + N 分支，遵循 git 流模型：

* 稳定发行版分支包含生产代码。

* 开发分支包含最新开发。

* 为每个功能创建一个新分支。

开发是在功能分支中完成的。 当功能完善时，将被合并到开发分支中。 从开发分支中挑选已完成并验证的功能，并将其合并到稳定分支中。

所有更改都是通过拉取请求 (PR) 完成的。 每份 PR 都由质量关卡自动验证。 Sonar 用于代码的质量检查，并运行一组测试套件，确保新代码不会引入任何回归。

Cloud Manager 的 git 存储库中的设置有两个分支。

* 稳定发行版分支包含来自所有团队的生产代码。
* 开发分支包含来自所有团队的开发代码。

在开发或稳定分支中，每次推送到团队的 git 存储库都会触发一个 [GitHub 操作](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)。

所有项目都遵循稳定分支的相同设置。 推送到项目的稳定分支会自动推送到 Cloud Manager 的 git 存储库中的稳定分支。 Cloud Manager 中的生产管道经配置，可通过推送到稳定分支来触发。 因此，生产管道可由任何团队每次推送到稳定的分支机构来执行，如果所有质量关卡均通过，生产部署就会更新。

![推送图表](/help/implementing/cloud-manager/assets/team-setup2.png)

对开发分支的推送处理方式不同。 虽然推送到团队 git 存储库中的开发人员分支也会触发 GitHub 操作，并且代码会自动推送到 Cloud Manager git 存储库中的开发分支，但非生产管道不会通过代码推送自动触发。 而是由调用 Cloud Manager 的 API 触发。

运行生产管道包括通过提供的质量关卡检查所有团队的代码。 一旦代码部署到暂存环境，就会执行测试和审核，确保一切都按预期进行。 一旦通过了所有的关卡，这些更改就会在不中断或停机的情况下发布到生产环境。

对于本地开发，使用 [AEM as a Cloud Service 的 SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing)。 SDK 允许设置本地作者、发布者和分发者。 这实现了离线开发和快速周转。 有时只使用作者环境进行开发，但快速设置 Dispatcher 和发布环境支持在推送到 git 存储库之前在本地测试所有内容。

每个团队的成员通常会从共享 git 中签出代码以及自己的项目代码。 没有必要签出其他项目，因为这些项目是独立的。

![本地签出及 SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

这种真实的设置可以用作蓝图，然后根据企业的需要进行定制。 Git 灵活的分支和合并概念允许根据每个团队的需要定制上述工作流的变化。 AEM as a Cloud Service 支持所有这些变化，而不牺牲专用的 Cloud Manager 管道的核心价值。

>[!TIP]
>
>请参阅文档[使用多个源 Git 存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code)，了解有关此设置的更多信息。

### 多团队设置的注意事项 {#considerations}

有了 Cloud Manager 的 Git 存储库和生产管道，完整的生产代码总是通过所有质量关卡运行，并将其视为一个部署单元。这样，生产系统始终处于运行状态，没有中断或停机。

相反，如果没有这样的系统，因为每个团队都可以单独部署，那么单个团队的更新可能会导致生产稳定性问题。 此外，需要协调和计划内停机才能推出更新。 随着团队数量的增加，协调工作将变得更加复杂，并且很快就无法管理。

如果在质量关卡中发现问题，生产不会受到影响，并且可以检测并修复问题，而无需 Adobe 人员介入。如果没有Cloud Service并且不始终测试整个部署，部分部署可能会导致中断，需要请求回滚，甚至需要从备份中完全恢复。 部分测试还可能导致其他问题，这些问题需要在事后解决，再次需要 Adobe 人员的协调和支持。

>[!TIP]
>
>对于任何多团队设置来说，定义一个治理模型和一组所有团队都必须遵循的标准是至关重要的。 之前的多团队设置蓝图允许跨更多团队进行扩展，您可以将其用作起点。
