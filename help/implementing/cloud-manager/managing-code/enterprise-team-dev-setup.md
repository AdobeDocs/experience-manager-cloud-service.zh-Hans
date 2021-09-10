---
title: 企业团队开发设置 — Cloud Services
description: 可查看本页以了解有关企业团队开发设置的更多信息
exl-id: 85f8779b-12cb-441b-a34d-04641184497a
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '1525'
ht-degree: 0%

---

# AEM as aCloud Service的企业团队开发设置 {#enterprise-setup}

## 简介 {#introduction}

AEM as Cloud Service是一种云原生产品，可提供AEM as a service，旨在从为企业团队提供企业软件满10年并满足其特定要求的过程中受益。 它将AEM推向云原生世界，具有始终开启、始终保持最新、始终保持安全且始终保持规模等新价值，同时它保留了AEM作为客户可自定义平台提供的主要价值主张，并允许企业级团队在其开发和交付过程中进行集成。

为支持我们的客户进行企业开发设置，AEM as a Manager与Cloud Manager及其专门构建的有见地CI/CD管道充分集成，这些管道配备了最佳实践，并从企业级开发和部署的多年经验中汲取了经验，从而确保了全面的测试和最高的代码质量，以提供出众的体验。

## Cloud Manager在企业团队开发设置中的支持 {#cloud-manager}

为确保客户快速入门，Cloud Manager提供了立即开始开发体验所需的一切功能，包括用于存储自定义项的git存储库，这些自定义项随后将由Cloud Manager构建、验证和部署。
使用Cloud Manager，开发团队可以努力频繁提交更改，而不依赖Adobe人员。

Cloud Manager中提供了三种环境类型：

* 开发
* 暂存
* 生产

可以使用非生产管道将代码部署到开发环境。 对于Stage和Production ，它们始终结合在一起，从而确保在生产部署之前进行验证（最佳做法是），生产管道使用质量门来验证应用程序代码和配置更改。

生产管道首先将代码和配置部署到暂存环境，测试应用程序，然后最终部署到生产环境。
Cloud ServiceSDK始终通过最新Cloud Service改进进行更新，它允许直接利用开发人员的本地硬件进行本地开发。 这样，可在极短的周转时间内实现快速开发。 因此，开发人员可以停留在他们熟悉的本地环境中，从各种开发工具中进行选择，并在认为合适时推送到开发环境或生产环境。

Cloud Manager支持灵活的多团队设置，这些设置可以根据企业的需求进行调整。 这适用于Cloud Service和AMS。 为确保通过多个团队进行稳定部署并避免一个团队影响所有团队的生产，确信的云管理人员将始终一起验证和测试所有团队的代码。


## 真实世界示例 {#real-world-example}

每个企业有不同的要求，包括不同的团队设置、流程和开发工作流程。 Adobe会将下面描述的设置用于多个项目，这些项目将体验以AEM作为Cloud Service交付。

例如，Adobe Creative Cloud应用程序(如Adobe Photoshop或Adobe Illustrator)包括可供最终用户使用的内容资源，如教程、示例和指南。 客户端应用程序以&#x200B;*headless*&#x200B;的方式将AEM用作Cloud Service，通过对AEM Cloud发布层进行API调用以将结构化内容检索为JSON流，以及将AEM中的[内容交付网络(CDN)用作Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/cdn.html?lang=en#content-delivery)以最佳性能提供结构化和非结构化内容，来使用此内容。

为此项目做出贡献的团队遵循以下所述的流程。

>[!NOTE]
>请参阅[使用多个源Git存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html#managing-code) ，了解有关该设置的更多信息。

每个团队都使用其自己的开发工作流，并有一个单独的git存储库。 其他共享的git存储库用于项目载入。 此git存储库包含Cloud Manager的git存储库的根结构，包括共享的调度程序配置。 载入新项目时，需要将列在共享Git存储库根目录的Reactor Maven项目文件中。 对于Dispatcher配置，会在Dispatcher项目内创建新的配置文件。 然后，此文件将由主调度程序配置包含。 每个团队负责其自己的调度程序配置文件。 对共享的git存储库所做的更改很少，通常仅在载入新项目时才需要进行更改。 主要工作由每个项目团队在其自己的git存储库中完成。

![](/help/implementing/cloud-manager/assets/team-setup1.png)

每个团队的git存储库都已使用AEM Maven原型进行设置，因此遵循了设置AEM项目的最佳实践。 唯一的例外是处理调度程序配置，该配置在共享的git存储库中完成，如上所述。
每个团队都使用一个简化的git工作流，该工作流包含两个+ N分支，遵循Git流程模型：

* 稳定的发布分支包含生产代码

* 开发分支包含最新开发

* 对于每个功能，都会创建新分支


开发在特征分支中完成，当特征逐渐完善时，它将合并到开发分支中。 已完成和已验证的功能将从开发分支中选取并合并到稳定分支中。 所有更改均通过拉取请求(PR)完成。 每个PR都由质量门自动验证。 声纳用于质量检查代码，并运行一组测试套件，以确保新代码不引入任何回归。

Cloud Manager的git存储库中的设置具有两个分支：

* *稳定发行分支*，包含所有团队的生产代码
* *开发分支*，包含所有团队的开发代码

对开发或稳定分支中团队的git存储库的每次推送都将触发[github操作](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/working-with-multiple-source-git-repos.html?lang=en#managing-code)。 所有项目都遵循稳定分支的相同设置。 对项目稳定分支的推送将自动推送到Cloud Manager的git存储库中的稳定分支。 Cloud Manager中的生产管道配置为通过向稳定分支的推送触发。 因此，任何团队的每个推入稳定的分支都会执行生产管道，并且如果所有质量门都通过，则会更新生产部署。

![](/help/implementing/cloud-manager/assets/team-setup2.png)

向开发分支推送的处理方式不同。 当团队git存储库中的推送到开发人员分支也会触发github操作，并且代码会自动推送到Cloud Manager的git存储库中的开发分支，但代码推送不会自动触发非生产管道。 它由对Cloud Manager api的调用触发。
运行生产管道包括通过提供的质量门检查所有团队的代码。 在将代码部署到暂存环境后，将执行测试和审核，以确保一切按预期运行。 所有门都通过后，更改即会推出到生产环境，不会造成任何中断或停机。
对于本地开发，将使用[SDK for AEM as aCloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#developing)。 SDK允许设置本地作者、发布和调度程序。 这样，便于离线开发和快速周转时间。 有时只有作者用于开发，但快速设置调度程序和发布允许在将内容推送到Git存储库之前在本地测试所有内容。 每个团队的成员通常从共享的git中签出代码以及他们自己的项目代码。 由于项目是独立的，因此无需签出其他项目。

![](/help/implementing/cloud-manager/assets/team-setup3.png)

此真实环境设置可用作蓝图，然后根据企业的需求进行自定义。 git的灵活分支和合并概念允许根据每个团队的需求自定义上述工作流的变体。 AEM as a ManagerCloud Service支持所有这些变体，同时不牺牲有见地的Cloud Manager管道的核心价值。

### 有关多团队设置的注意事项 {#considerations}

>[!NOTE]
>对于任何多团队设置，定义治理模型和一套所有团队都必须遵循的标准都至关重要。 上述多团队设置的蓝图允许跨更多团队进行扩展，您可以将此蓝图用作起点。

借助Cloud Manager的git存储库和生产管道，始终通过所有质量门运行完整的生产代码，将其视为一个部署单元。 这样，生产系统将始终保持&#x200B;*处于*状态，不会中断或停机。
相反，如果没有这样的系统，因为每个团队都可以单独部署，所以单个团队的更新可能会导致生产稳定性问题。 此外，它还需要协调和计划内停机才能推出更新。 随着团队的增加，协调工作将变得复杂得多，并且很快难以管理。

如果在质量门中检测到问题，则不影响生产，并且可以检测并修复该问题，而无需Adobe人员介入。 如果没有Cloud Service，并且不总是测试整个部署，部分部署可能会导致停机，需要请求回滚，甚至需要从备份进行完全恢复。 部分测试还可能导致其他问题，在事实再次需要Adobe人员的协调和支持后，这些问题需要解决。
