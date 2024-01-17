---
title: 部署代码
description: 了解如何使用 AEM as a Cloud Service 中的 Cloud Manager 管道部署代码。
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 93%

---


# 部署代码 {#deploy-your-code}

了解如何使用 AEM as a Cloud Service 中的 Cloud Manager 管道将代码部署到生产环境中。

![非生产管道图标](./assets/configure-pipeline/production-pipeline-diagram.png)

通过生产管道将代码无缝部署到暂存环境，然后再部署到生产环境。生产管道执行分为两个逻辑阶段。

1. 部署到暂存环境
   * 构建并部署代码到暂存环境中，用于自动化功能测试、UI 测试、体验审计和用户验收测试 (UAT)。
1. 部署到生产环境
   * 一旦构建在暂存环境中进行了验证，并批准升级为生产环境，那么相同的构建工件就会部署到生产环境中。

_只有“完整堆栈代码”管道类型支持代码扫描、功能测试、UI 测试和体验审核。_

## 使用 AEM as a Cloud Service 中的 Cloud Manager 部署您的代码 {#deploying-code-with-cloud-manager}

[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)（包括存储库、环境和测试环境）后，便可以部署代码。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 屏幕上，点按或单击要为其部署代码的程序。

1. 在&#x200B;**概述**&#x200B;屏幕上，从行动号召中单击&#x200B;**部署**&#x200B;启动部署过程。

   ![行动号召 (CTA)](assets/deploy-code1.png)

1. 这将显示&#x200B;**管道执行**&#x200B;屏幕。单击&#x200B;**构建**&#x200B;开始此流程。

   ![管道执行屏幕](assets/deploy-code2.png)

构建过程通过三个阶段部署代码。

1. [暂存部署](#stage-deployment)
1. [暂存测试](#stage-testing)
1. [生产部署](#production-deployment)

>[!TIP]
>
>您可以通过查看日志或依据测试标准审查结果来审查各种部署过程的步骤。

## 暂存部署阶段 {#stage-deployment}

**暂存部署**&#x200B;阶段。包括这些步骤。

* **验证** – 此步骤可确保将管道配置为使用当前可用的资源。例如，测试配置的分支存在其中且环境可用的资源。
* **构建和单元测试** – 此步骤运行容器化的构建过程。
   * 有关构件环境的详细信息，请参阅[构建环境详细信息。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)
* **代码扫描** – 此步骤评估应用程序代码的质量。
   * 有关测试过程的详细信息，请参阅[代码质量测试。](/help/implementing/cloud-manager/code-quality-testing.md)
* **构建图像** – 此过程负责将构建步骤生成的内容和 Dispatcher 程序包转换为 Docker 图像和 Kubernetes 配置。
* **部署到暂存环境** – 将图像部署到暂存环境，为[暂存测试阶段做准备。](#stage-testing)

![暂存部署](assets/stage-deployment.png)

## 暂存测试阶段 {#stage-testing}

**暂存测试**&#x200B;阶段包含这些步骤。

* **产品功能测试** – Cloud Manager 管道执行针对暂存环境运行的测试。
   * 有关详细信息，请参阅[产品功能测试。](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)

* **自定义功能测试** – 管道中的此步骤始终执行，不能跳过。如果构建没有生成测试 JAR，则默认情况下测试通过。
   * 有关详细信息，请参阅[自定义功能测试。](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)

* **自定义 UI 测试** – 此步骤是一个可选功能，可自动运行为自定义应用程序创建的 UI 测试。
   * UI 测试是打包在 Docker 图像中的基于 Selenium 的测试，允许在语言和框架（如 Java 和 Maven、Node 和 WebDriver.io，或任何其他基于 Selenium 构建的框架和技术）中进行广泛选择。
   * 有关详细信息，请参阅[自定义 UI 测试。](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)

* **体验审核** – 管道中的此步骤始终执行，不能跳过。在执行生产管道时，在将运行检查的自定义功能测试之后，会包含体验审核步骤。
   * 配置的页面将提交给服务并进行评估。
   * 审核结果是信息性的，显示分数以及当前分数和以前分数之间的变化。
   * 此细节对于确定当前部署中是否会引入回归非常有用。
   * 有关更多详细信息，请参阅[了解体验审核结果。](/help/implementing/cloud-manager/experience-audit-testing.md)

![暂存测试](assets/stage-testing.png)

## 生产部署阶段 {#deployment-production}

部署到生产拓扑的过程略有不同，旨在尽量减小对 AEM 网站访客产生的影响。

生产部署通常遵循与前述相同的步骤，但它采用的是滚动方式。

1. 将 AEM 包部署到作者。
1. 从负载平衡器分离 dispatcher1。
1. 以并行方式将 AEM 包部署到 publish1，并将 Dispatcher 包部署到 dispatcher1，同时刷新 Dispatcher 缓存。
1. 将 dispatcher1 放回负载平衡器中。
1. 在将 dispatcher1 重新投入使用后，就会从负载平衡器中分离 dispatcher2。
1. 以并行方式将 AEM 包部署到 publish2，并将 Dispatcher 包部署到 dispatcher2，同时刷新 Dispatcher 缓存。
1. 将 dispatcher2 放回负载平衡器中。

此过程将持续进行，直到部署到达拓扑中的所有发布者和 Dispatcher 为止。

![生产部署阶段](assets/production-deployment.png)

## 超时 {#timeouts}

如果继续等待用户反馈，则以下步骤将超时：

| 步骤 | 超时 |
|--- |--- |
| 代码质量测试 | 14 天 |
| 安全性测试 | 14 天 |
| 性能测试 | 14 天 |
| 申请批准 | 14 天 |
| 计划生产部署 | 14 天 |
| CSE 支持 | 14 天 |

## 部署过程 {#deployment-process}

所有 Cloud Service 部署都遵循滚动过程，以确保零停机。请参阅[滚动部署的工作原理](/help/implementing/deploying/overview.md#how-rolling-deployments-work)，以了解更多信息。

>[!NOTE]
>
>每次部署都会清除 Dispatcher 缓存。随后在新发布节点接受流量之前对其进行预热。

## 重新执行生产部署 {#reexecute-deployment}

在罕见的情况下，生产部署步骤可能会因短暂的原因而失败。在这种情况下，只要生产部署步骤已完成，则支持重新执行生产部署步骤，而不管完成类型如何（例如，已取消或不成功）。 重新执行将使用包含三个步骤的同一管道创建新的执行。

1. 验证步骤 - 此步骤基本上就是在正常管道执行期间进行的相同验证。
1. 构建步骤 - 在重新执行的上下文中，构建步骤复制工件，但实际上并不执行新的构建过程。
1. 生产部署步骤 - 此步骤使用与正常管道执行中的生产部署步骤相同的配置和选项。

在此类能够重新执行的情况下，生产管道状态页面在平常的&#x200B;**下载构建日志**&#x200B;选项旁提供&#x200B;**重新执行**&#x200B;选项。

![管道概述窗口中的“重新执行”选项](assets/re-execute.png)

>[!NOTE]
>
>在重新执行中，在 UI 中为构建步骤加上标签以反映它复制工件而非重新构建。

### 限制 {#limitations}

* 生产部署步骤的重新执行仅适用于上一次执行。
* 重新执行不适用于推送更新执行。
   * 如果最后一次执行是推送更新执行，则不可能重新执行。
* 如果上一次执行在生产部署步骤前的任何时间点失败，则无法重新执行。

### 重新执行 API {#reexecute-API}

除了在UI中可用之外，您还可以使用 [Cloud Manager API](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/#tag/Pipeline-Execution) 用于触发重新执行并标识作为重新执行触发的执行。

#### 触发重新执行 {#reexecute-deployment-api}

要触发重新执行，请在生产部署步骤状态的 HAL 链接 `https://ns.adobe.com/adobecloud/rel/pipeline/reExecute` 发出 PUT 请求。

* 如果存在此链接，则可以从该步骤重新开始执行。
* 如果此链接不存在，则无法从该步骤重新开始执行。

此链接仅适用于生产部署步骤。

```JavaScript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```

HAL 链接的 href 值的语法只是一个示例。应始终从 HAL 链接读取而不是生成实际值。

通过将 PUT 请求提交到此端点，会产生 201 响应（如果成功），并且响应正文会是新执行的表示形式。这类似于通过 API 开始常规执行。

#### 识别“重新执行”的执行 {#identify-reexecution}

可以通过 `trigger` 字段中的 `RE_EXECUTE` 值识别重新执行的执行。
