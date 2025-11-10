---
title: AEM Forms Communications API — 概述
description: AEM Forms通信API概述，包括身份验证方法和完整的API参考
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 8%

---


# AEM Forms Communications API — 概述

AEM Forms Communications API提供了一整套云原生API，旨在帮助企业自动执行文档工作流。

AEM Forms API通过两个主控制台进行结构化和访问：

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console是Adobe API、事件、运行时和App Builder的网关。

* [AEM Developer Console](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console提供了用于调试和检查AEM as a Cloud Service环境的工具。

每个控制台提供对不同API和服务的访问，用于文档处理、生成、转换、加密和通信任务。 API支持不同的[身份验证方法](#authentication-methods)。

## 身份验证方法

API支持多种身份验证方法，以便您的应用程序与Adobe服务之间进行安全集成：

| 方面 | OAuth服务器到服务器（推荐） | JWT（JSON Web令牌） |
|-------------|------------------------------------------|---------------------------|
| 描述 | 无需用户交互即可进行API访问的现代安全方法。 | 使用签名令牌进行访问的旧方法。 |
| 设置位置 | Adobe Developer Console和AEM Developer Console | 仅限AEM Developer Console |
| 安全性 | 高 — 使用客户端凭据和范围 | 中等 — 取决于密钥管理 |
| 可扩展性 | 高度可扩展的后端集成 | 有限，适合旧版使用 |
| 令牌管理 | 自动生成和续订 | 手动令牌签名和轮换 |
| 状态 | 推荐 | 已弃用 |


>[!NOTE]
>
> 单击以下链接了解有关:-的更多信息
> 
> * [OAuth服务器到服务器（推荐）](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)
> * [JWT （JSON Web令牌）](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/)

<!--### Execution Models

The following table highlights the key differences between Synchronous (On-Demand) and Asynchronous (Batch) execution models supported in AEM Forms Communications APIs:

| Feature | Synchronous (On-Demand) | Batch (Asynchronous) |
|---------|-------------------------|----------------------|
| **Execution Model** | Real-time, immediate | Queued, scheduled |
| **Response Time** | Seconds | Minutes to hours |
| **Volume** | Single or few documents | Hundreds to thousands |
| **Testing Environment** | Author & Publish | Author Only |
| **Use Case** | User-triggered actions | Scheduled bulk operations |
| **Console Access** | ADC & AEM Developer Console | AEM Developer Console Only |-->

## API分类概述

所有AEM Forms API都分为两个主要部分：

* [自适应表单交付和运行时API](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms通信API](#aem-forms-communications-apis)

| 详细信息 | 自适应表单交付和运行时API | 通信API |
|--------------|----------------------------|--------------------------|
| 用途 | 处理自适应表单交付和运行时操作 | 文档生成和处理 |
| 用例 |  — 表单渲染<br> — 数据预填充<br> — 表单提交<br> — 草稿管理 |  — 生成PDF<br> — 文档合并<br> — 批次处理<br> — 打印操作 |
| 授权方法 | 支持OAuth服务器到服务器/用户身份验证方法。 | 仅支持OAuth服务器到服务器身份验证。 |

### AEM Forms通信API

通信API是以文档为中心的操作的主要重点。

下表列出了所有[AEM Forms Communications API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/)及其支持的身份验证方法和执行模型：

#### 文档生成API

| API端点 | 执行模型 | 身份验证方法 |
| ------------------ | ---------------- | --------------------------- |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 异步/批处理 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


#### 文档操作API

| API端点 | 执行模型 | 身份验证方法 |
| ------------------ | ---------------- | --------------------------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)/[JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) |

#### 文档转换API

| API端点 | 执行模型 | 身份验证方法 |
|----------------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### 文档提取API

| API端点 | 执行模型 | 身份验证方法 |
|----------------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### Document Transformation API


| API端点 | 执行模型 | 身份验证方法 |
|----------------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |

#### 文档Assurance API

| API端点 | 执行模型 | 身份验证方法 |
|----------------|---------|----------------------|
| [/adobe/document/assure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |
| [/adobe/document/assure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | 同步 | [OAuth服务器到服务器](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation) |


## 后续步骤

了解如何为同步（按需）和异步（批处理） Forms Communications API设置环境：

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="同步API" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="同步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API — 同步">AEM Forms Communications API — 同步</a>
                    </p>
                    <p class="is-size-6">了解如何为同步（按需）Forms Communications API设置环境，以即时生成或处理文档。 </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API — 异步" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="异步API"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="异步API">AEM Forms Communications API — 异步（批次）</a>
                    </p>
                    <p class="is-size-6">了解如何为异步（批处理）Forms Communications API设置环境，以计划方式生成或处理多个文档。</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">了解详情</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


>[!MORELIKETHIS]
>
>* [AEM Forms as a Cloud Service Communications简介](/help/forms/aem-forms-cloud-service-communications-introduction.md)
>* 自适应AEM Forms和通信API的[Forms as a Cloud Service架构](/help/forms/aem-forms-cloud-service-architecture.md)
>* [通信处理 — 同步API](/help/forms/aem-forms-cloud-service-communications.md)
>* [通信处理 — 批处理API](/help/forms/aem-forms-cloud-service-communications-batch-processing.md)
>* [通信处理 — 按需API](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md)