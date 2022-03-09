---
title: 企业开发团队设置
description: 了解如何设置和扩展您的企业开发团队，并了解AEM as a Cloud Service如何支持您的开发流程。
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: a31c3693c9b2af9bd7f9d7f1f6fb0a61a4411df0
workflow-type: tm+mt
source-wordcount: '1444'
ht-degree: 0%

---

# AEM Development Team Setup for as a Cloud Service Enterprise {#enterprise-setup}

了解如何设置和扩展您的企业开发团队，并了解AEM as a Cloud Service如何支持您的开发流程。

## 简介 {#introduction}

为了支持具有企业开发设置的客户，AEM  as a Cloud Service与Cloud Manager及其专门构建的完全集成， [CI/CD管道的意见。](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 这些管道和服务是根据最佳做法构建的，可确保彻底 [测试和最高代码质量。](/help/implementing/cloud-manager/code-quality-testing.md)

## Cloud Manager在企业团队开发设置中的支持 {#cloud-manager}

为确保快速入门，Cloud Manager提供了立即开始开发数字体验所需的一切功能，包括用于存储自定义项的git存储库，这些自定义项随后将由Cloud Manager构建、验证和部署。

使用Cloud Manager，开发团队可以努力频繁提交更改，而不依赖Adobe人员。

Cloud Manager中提供了三种类型的环境。

* 开发
* 暂存
* 生产

可以使用非生产管道将代码部署到开发环境。 对于暂存和生产环境，生产管道始终结合使用，从而确保在生产部署之前进行验证（这是最佳做法） [质量门](/help/implementing/cloud-manager/custom-code-quality-rules.md) 验证应用程序代码和配置更改。

生产管道首先将代码和配置部署到暂存环境，测试应用程序，然后最终部署到生产环境。

Cloud ServiceSDK始终通过最新的AEMas a Cloud Service改进进行更新，从而允许直接利用开发人员的本地硬件进行本地开发。 这样，可在极短的周转时间内实现快速开发。 因此，开发人员可以停留在他们熟悉的本地环境中，从各种开发工具中进行选择，并在认为合适时推送到开发环境或生产环境。

Cloud Manager支持灵活的多团队设置，这些设置可以根据企业的需求进行调整。 为确保与多个团队进行稳定部署，同时避免一个团队影响所有团队的生产情况，Cloud Manager的确知管道始终会验证并测试所有团队的代码。

## 真实世界示例 {#real-world-example}

每个企业有不同的要求，包括不同的团队设置、流程和开发工作流程。 Adobe会将下面描述的设置用于多个基于AEMas a Cloud Service交付体验的项目。

例如，Adobe Creative Cloud应用程序(如Adobe Photoshop或Adobe Illustrator)包括可供最终用户使用的内容资源，如教程、示例和指南。 客户端应用程序使用AEM as a Cloud Service以无头方式使用此内容，方法是对AEM Cloud发布层进行API调用以将结构化内容检索为JSON流，并利用 [AEMas a Cloud Service中的内容交付网络(CDN)](/help/implementing/dispatcher/cdn.md#content-delivery) 以优化性能同时提供结构化和非结构化内容。

为此项目做出贡献的团队遵循以下流程。

每个团队都使用其自己的开发工作流，并有一个单独的git存储库。 其他共享的git存储库用于载入项目。 此git存储库包含Cloud Manager的git存储库的根结构，包括共享的调度程序配置。

载入新项目时，需要将列在共享Git存储库根目录的Reactor Maven项目文件中。 对于Dispatcher配置，会在Dispatcher项目内创建新的配置文件。 然后，此文件将由主调度程序配置包含。 每个团队负责其自己的调度程序配置文件。 对共享的git存储库所做的更改很少，通常仅在载入新项目时才需要进行更改。 主要工作由每个项目团队在其自己的git存储库中完成。

![工作流图](/help/implementing/cloud-manager/assets/team-setup1.png)

每个存储库的git存储库都使用 [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 并因此遵循设置AEM项目的最佳实践。 唯一的例外是在共享的git存储库中完成的调度程序配置，如上所述。

每个团队都使用一个简化的git工作流，该工作流包含两个+ N分支，遵循git流程模型：

* 稳定的发布分支包含生产代码。

* 开发分支包含最新开发。

* 对于每个功能，都会创建新分支。

开发在功能分支中完成。 当特征逐渐完善时，它会合并到开发分支中。 已完成和已验证的功能将从开发分支中选取并合并到稳定分支中。

所有更改均通过拉取请求(PR)完成。 每个PR都由质量门自动验证。 声纳用于质量检查代码，并运行一组测试套件，以确保新代码不引入任何回归。

Cloud Manager的git存储库中的设置具有两个分支。

* 稳定的发行分支包含所有团队的生产代码。
* 开发分支包含所有团队的开发代码。

在开发或稳定分支中，每次向团队的git存储库推送都会触发 [GitHub操作。](/help/implementing/cloud-manager/managing-code/working-with-multiple-source-git-repositories.md#managing-code)

所有项目都遵循稳定分支的相同设置。 对项目稳定分支的推送将自动推送到Cloud Manager的git存储库中的稳定分支。 Cloud Manager中的生产管道配置为通过向稳定分支的推送来触发。 因此，任何团队的每个推入稳定的分支都会执行生产管道，并且如果所有质量门都通过，则会更新生产部署。

![推送图](/help/implementing/cloud-manager/assets/team-setup2.png)

向开发分支推送的处理方式不同。 当团队git存储库中的向开发人员分支推送消息也会触发GitHub操作，并且代码会自动推送到Cloud Manager的git存储库中的开发分支，但代码推送不会自动触发非生产管道。 它由对Cloud Manager API的调用触发。

运行生产管道包括通过提供的质量门检查所有团队的代码。 在将代码部署到暂存环境后，将执行测试和审核，以确保一切按预期运行。 所有门都通过后，更改即会推出到生产环境，不会造成任何中断或停机。

为地方发展， [适用于AEM的SDKas a Cloud Service](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md#developing) 中，将使用。 SDK允许设置本地创作、发布和调度程序。 这样，便于离线开发和快速周转时间。 有时只有创作环境用于开发，但快速设置调度程序和发布环境允许在将所有内容推送到Git存储库之前在本地测试。

每个团队的成员通常从共享的git中签出代码以及他们自己的项目代码。 由于项目是独立的，因此无需签出其他项目。

![本地结帐和SDK](/help/implementing/cloud-manager/assets/team-setup3.png)

此真实环境设置可用作蓝图，然后根据企业的需求进行自定义。 git的灵活分支和合并概念允许根据每个团队的需求自定义上述工作流的变体。 AEM as a Cloud Service支持所有这些变体，而不牺牲有见地的Cloud Manager管道的核心价值。

>[!TIP]
>
>请参阅该文档 [使用多个源Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) 以了解有关此设置的更多信息。

### 有关多团队设置的注意事项 {#considerations}

借助Cloud Manager的git存储库和生产管道，完整的生产代码始终贯穿所有质量门户，并将其视为一个部署单元。 这样，生产系统就始终不间断地运行。

相反，如果没有这样的系统，因为每个团队都可以单独部署，所以单个团队的更新可能会导致生产稳定性问题。 此外，它还需要协调和计划内停机才能推出更新。 随着团队的增加，协调工作将变得复杂得多，并且很快难以管理。

如果在质量门中检测到问题，则不影响生产，并且可以检测并修复该问题，而无需Adobe人员介入。 如果没有Cloud Service，并且不总是测试整个部署，部分部署可能会导致停机，需要请求回滚，甚至需要从备份进行完全恢复。 部分测试还可能导致其他问题，在事实再次需要Adobe人员的协调和支持后，这些问题需要解决。

>[!TIP]
>
>对于任何多团队设置，定义治理模型和一套所有团队都必须遵循的标准都至关重要。 多团队设置的上一个蓝图允许跨更多团队进行扩展，您可以将其用作起点。
