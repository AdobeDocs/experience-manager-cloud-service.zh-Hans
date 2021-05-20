---
title: 部署代码 — Cloud Services
description: 部署代码 — Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 782035708467693ec7648b1fd701c329a0b5f7c8
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# 部署代码 {#deploy-your-code}

## 在AEM as a Cloud Manager中使用Cloud Manager部署代码{#deploying-code-with-cloud-manager}

配置生产管道（存储库、环境和测试环境）后，您便可以部署代码。

1. 从Cloud Manager中单击&#x200B;**部署**&#x200B;以开始部署过程。

   ![](assets/deploy-code1.png)


1. 此时将显示&#x200B;**Pipeline Execution**&#x200B;屏幕。

   单击&#x200B;**Build**&#x200B;以开始该过程。

   ![](assets/deploy-code2.png)

1. 整个构建过程会部署您的代码。

   构建过程中涉及以下阶段：

   1. Stage Deployment
   1. 阶段测试
   1. 生产部署

   >[!NOTE]
   >
   >此外，您还可以通过查看日志或查看结果来查看各种部署流程中的步骤，以了解测试标准。

   Stage **Deployment**，涉及以下步骤：

   * 验证：此步骤可确保将管道配置为使用当前可用的资源，例如，配置的分支存在，且环境可用。
   * 构建和单元测试：此步骤将运行容器化生成流程。 有关构建环境的详细信息，请参阅[构建环境详细信息](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md)。
   * 代码扫描：此步骤将评估应用程序代码的质量。 有关测试过程的详细信息，请参阅[代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md)。
   * 构建图像：此步骤包含用于构建图像的流程中的日志文件。 此过程负责将生成步骤生成的内容和调度程序包转换为Docker图像和Kubernetes配置。
   * 部署到暂存环境

      ![](assets/stage-deployment.png)
   舞 **台测试**，涉及以下步骤：

   * **产品功能测试**:Cloud Manager管道执行将支持执行针对暂存环境运行的测试。有关更多详细信息，请参阅[产品功能测试](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。

   * **自定义功能测试**:管道中的此步骤始终存在，无法跳过。但是，如果内部版本未生成测试JAR，则测试默认通过。\
      有关更多详细信息，请参阅[自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。

   * **自定义UI测试**:此步骤是一项可选功能，允许我们的客户为其应用程序创建并自动运行UI测试。UI测试是在Docker图像中打包的基于硒的测试，以便允许在语言和框架（如Java和Maven、Node和WebDriver.io，或任何基于Selenium构建的其他框架和技术）中进行广泛选择。
有关更多详细信息，请参阅[自定义UI测试](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=en#custom-ui-testing) 。


   * **体验审核**:管道中的此步骤始终存在，无法跳过。执行生产管道时，在将运行检查的自定义功能测试之后，将包含体验审核步骤。 配置的页面将被提交到服务并进行评估。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否引入回归参数非常有价值。
有关更多详细信息，请参阅[了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md)。

      ![](assets/stage-testing.png)





## 部署过程{#deployment-process}

以下部分介绍如何在阶段和生产阶段部署AEM和调度程序包。

Cloud Manager将构建过程生成的所有target/*.zip文件上传到存储位置。  这些工件在管道的部署阶段期间从此位置进行检索。

当Cloud Manager部署到非生产拓扑时，其目标是尽快完成部署，从而将工件同时部署到所有节点，如下所示：

1. Cloud Manager确定每个对象是AEM还是调度程序包。
1. Cloud Manager从负载平衡器中删除所有调度程序，以在部署期间隔离环境。

   除非另外配置，否则您可以在开发部署和暂存部署中跳过负载平衡器更改，即在非生产管道、开发环境和生产管道的暂存环境中分离和附加步骤。

   >[!NOTE]
   >
   >此功能预计主要由1-1-1个客户使用。

1. 每个AEM对象都会通过包管理器API部署到每个AEM实例，并且包依赖关系会确定部署顺序。

   要详细了解如何使用软件包来安装新功能、在实例之间传输内容以及备份存储库内容，请参阅如何使用软件包。

   >[!NOTE]
   >
   >所有AEM对象都会部署到作者和发布者。 当需要特定于节点的配置时，应使用运行模式。 要了解有关运行模式如何允许您针对特定目的优化AEM实例的更多信息，请参阅运行模式。

1. 调度程序对象将部署到每个调度程序，如下所示：

   1. 当前配置将被备份并复制到临时位置
   1. 除不可变文件外，所有配置都将被删除。 有关更多详细信息，请参阅管理调度程序配置。 这会清除目录，以确保不会留下任何孤立的文件。
   1. 对象将提取到`httpd`目录。  不可变文件不会被覆盖。 在部署时，您对Git存储库中的不可变文件所做的任何更改都将被忽略。  这些文件是AMS调度程序框架的核心文件，无法更改。
   1. Apache会执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，将从备份还原配置，重新加载服务，并将错误报告回Cloud Manager。
   1. 管道配置中指定的每个路径都将失效或从调度程序缓存中刷新。

   >[!NOTE]
   >
   >Cloud Manager需要调度程序对象包含完整文件集。  所有Dispatcher配置文件都必须存在于Git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，并且部署完成。

   >[!NOTE]
   >
   >您可以在开发和暂存部署中跳过负载平衡器更改，即在非生产管道、开发人员环境和暂存环境的生产管道中分离和附加步骤。

### 部署到生产阶段{#deployment-production-phase}

部署到生产拓扑的流程略有不同，以便最大限度地减少对AEM Site访客的影响。

生产部署通常遵循与上述步骤相同的步骤，但采用滚动方式：

1. 部署AEM包以进行创作。
1. 从负载平衡器中分离Dispatcher1。
1. 将AEM包部署到publish1，将调度程序包部署到dispatcher1，刷新调度程序缓存。
1. 将dispatcher1重新放入负载平衡器中。
1. 调度程序1恢复服务后，从负载平衡器中分离dispatcher2。
1. 将AEM包部署到publish2，将调度程序包部署到dispatcher2，刷新调度程序缓存。
1. 将dispatcher2重新放入负载平衡器中。
此过程会一直持续到部署到达拓扑中的所有发布者和调度程序为止。
