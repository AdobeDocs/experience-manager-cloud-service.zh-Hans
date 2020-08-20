---
title: 部署代码-Cloud Services
description: 部署代码-Cloud Services
translation-type: tm+mt
source-git-commit: 18ef67e6b8450e4220a5d40c1da8b126136e39f2
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---


# 部署代码 {#deploy-your-code}

## 使用Cloud Manager部署代码 {#deploying-code-with-cloud-manager}

配置Production Pipeline(存储库、环境和测试环境)后，即可部署代码。

1. 单 **击** “从云管理器部署”以开始部署过程。

   ![](assets/deploy-code1.png)


1. 将显 **示“管道** 执行”屏幕。

   单击 **“构建** ”以开始该过程。

   ![](assets/deploy-code2.png)

1. 整个构建过程会部署您的代码。

   构建过程中涉及以下阶段：

   1. 阶段部署
   1. Stage Testing
   1. 生产部署

   >[!NOTE]
   >
   >此外，您还可以查看日志或查看测试标准的结果，来查看各个部署流程中的步骤。

   Stage **Deployment**，涉及以下步骤：

   * 验证：此步骤确保管道配置为使用当前可用的资源，例如，已配置的分支存在，环境可用。
   * 构建和单元测试：此步骤运行容器化构建过程。 有关 [构建环境的详细信](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#build-environment-details) 息，请参阅构建环境详细信息。
   * 代码扫描：此步骤将评估应用程序代码的质量。 有关 [测试过程的详细信](/help/implementing/cloud-manager/code-quality-testing.md) 息，请参阅代码质量测试。
   * 构建图像：此步骤包含用于构建图像的进程中的日志文件。 此过程负责将构建步骤生成的内容和调度程序包转换为Docker图像和Kubernetes配置。
   * 部署到舞台

      ![](assets/stage-deployment.png)
   舞 **台测试**，涉及以下步骤：

   * 产品功能测试：Cloud Manager管道执行将支持执行针对舞台环境运行的测试。
有关更多 [详细信息，请参](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) 阅产品功能测试。

   * 自定义功能测试：管道中的此步骤始终存在，无法跳过。 但是，如果生成未生成测试JAR，则默认情况下测试通过。\
      有关更多 [详细信息，请参](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 阅自定义功能测试。

   * 内容审核：管道中的此步骤始终存在，无法跳过。 在执行生产管道时，在将运行检查的自定义功能测试之后包括内容审核步骤。 配置的页面将提交到服务并进行评估。 结果是信息性的，允许用户查看当前得分和先前得分之间的变化。 此洞察对于确定当前部署中是否会引入退化，很有价值。
有关更多 [详细信息，请参阅](/help/implementing/cloud-manager/content-audit-testing.md) “了解内容审核结果”。

      ![](assets/testing-tab.png)





## 部署流程 {#deployment-process}

以下部分介绍如何在阶段和生产阶段部署AEM和调度程序包。

Cloud Manager将构建过程生成的所有目标/*.zip文件上传到存储位置。  在管道的部署阶段从此位置检索这些对象。

当Cloud Manager部署到非生产拓扑时，其目标是尽快完成部署，因此将对象同时部署到所有节点，如下所示：

1. Cloud Manager确定每个对象是AEM还是调度程序包。
1. Cloud Manager从负载平衡器中删除所有调度程序，以在部署过程中隔离环境。

   除非另外配置，否则您可以跳过开发和阶段部署中的负载平衡器更改，即分离和附加非生产管道中的步骤，以用于开发环境和生产管道中的阶段环境。

   >[!NOTE]
   >
   >此功能主要由1-1-1客户使用。

1. 每个AEM对象都通过包管理器API部署到每个AEM实例，包依赖关系决定部署顺序。

   要进一步了解如何使用包安装新功能、在实例之间传输内容以及备份存储库内容，请参阅如何使用包。

   >[!NOTE]
   >
   >所有AEM对象都部署到作者和发布者。 需要特定于节点的配置时，应利用运行模式。 要进一步了解运行模式如何允许您针对特定目的调整AEM实例，请参阅运行模式。

1. 调度程序对象将按如下方式部署到每个调度程序：

   1. 当前配置被备份并复制到临时位置
   1. 除不可变文件外，所有配置都将被删除。 有关更多详细信息，请参阅管理调度程序配置。 这将清除目录，以确保不留下任何孤立文件。
   1. 对象会被提取到目 `httpd` 录。  不可改写的文件不会被覆盖。 在部署时，您对git存储库中不可变文件所做的任何更改都将被忽略。  这些文件是AMS调度程序框架的核心，无法更改。
   1. Apache执行配置测试。 如果未找到错误，则重新加载服务。 如果发生错误，则从备份中恢复配置，重新加载服务，并将错误报告回云管理器。
   1. 管道配置中指定的每个路径都无效或从调度程序缓存中刷新。

   >[!NOTE]
   >
   >Cloud Manager希望调度程序对象包含完整的文件集。  所有调度程序配置文件都必须在git存储库中。 缺少文件或文件夹将导致部署失败。

1. 成功将所有AEM和调度程序包部署到所有节点后，调度程序将添加回负载平衡器，部署完成。

   >[!NOTE]
   >
   >您可以跳过开发和阶段部署中的负载平衡器更改，即在非生产管道中为开发人员环境分离和附加步骤，在生产管道中为阶段环境分离和附加步骤。

### 部署到生产阶段 {#deployment-production-phase}

部署到生产拓扑的过程略有不同，以最大限度地减少对AEM站点访客的影响。

生产部署通常遵循与上述步骤相同的步骤，但是采用滚动方式：

1. 部署AEM包以进行创作。
1. 从负载平衡器中分离调度程序1。
1. 将AEM包部署到publish1，将调度程序包部署到dispatcher1，刷新调度程序缓存。
1. 将dispatcher1放回负载平衡器中。
1. 调度程序1恢复服务后，请从负载平衡器中分离调度程序2。
1. 将AEM包部署到publish2，将调度程序包部署到dispatcher2，刷新调度程序缓存。
1. 将dispatcher2放回负载平衡器中。
此过程将一直持续到部署到达拓扑中的所有发布者和调度程序为止。


