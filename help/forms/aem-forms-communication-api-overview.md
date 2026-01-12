---
title: AEM Forms Communications API — 概述
description: AEM Forms通信API概述，包括身份验证方法和完整的API参考
role: Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: d9eb9a93aba71a5ef5940c9d1d75cfd4e738c26b
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 4%

---


# AEM Forms Communications API — 概述

AEM Forms API提供了一整套云原生API，旨在帮助企业自动执行文档工作流。

AEM Forms API通过两个主控制台进行结构化和访问：

* [Adobe Developer Console (ADC)](https://developer.adobe.com/developer-console/) - Adobe Developer Console是Adobe API、事件、运行时和App Builder的网关。

* [AEM Developer Console](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console) - AEM Developer Console提供对环境级别的详细信息、配置、技术帐户和服务凭据的访问权限，以支持操作和集成任务。

不同的API支持不同的[身份验证方法](#authentication-methods)。

## 身份验证方法

不同的Forms API根据其发布时间线使用不同的身份验证方法：

* [OAuth 服务器到服务器](/help/forms/oauth-api-authetication.md)
* [JWT （JSON Web令牌）服务器到服务器](/help/forms/jwt-api-authentication.md)

早期的API支持基于JWT的服务器到服务器身份验证，该身份验证通过AEM Developer Console进行配置和管理。 较新的API使用OAuth服务器到服务器身份验证，并通过Adobe Developer Console进行配置。

<!--
>[!NOTE]
>
> Adobe is standardizing authentication method across all APIs and is gradually onboarding APIs to the Adobe Developer Console, which supports the OAuth Server-to-Server authentication method.-->

## API分类概述

所有AEM Forms API都分为两个主要部分：

* [自适应表单交付和运行时API](https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/)

* [AEM Forms通信API](#aem-forms-communications-apis)

| 详细信息 | 自适应表单交付和运行时API | 通信API |
|--------------|----------------------------|--------------------------|
| 用途 | 处理自适应表单交付和运行时操作 | 文档生成和处理 |
| 用例 |  — 表单渲染<br> — 数据预填充<br> — 表单提交<br> — 草稿管理 |  — 生成PDF<br> — 文档合并<br> — 批次处理<br> — 打印操作 |
| 授权方法 | 支持OAuth服务器到服务器/用户身份验证方法。 | 根据API，支持服务器到服务器的身份验证，即JWT或OAuth。 API不能同时支持两种身份验证方法。 |

### AEM Forms通信API

通信API是以文档为中心的操作的主要重点。

下表列出了所有[AEM Forms Communications API](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/)及其支持的身份验证方法和执行模型：

#### 文档生成API


| API端点 | 描述 | 执行模型 | 身份验证方法 |
| ----- | ------ |------- | ------ |
| [/adobe/forms/batch/output/config](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig) | 为文档生成作业创建新的批次配置。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetBatchConfigbyName) | 检索特定批次配置的详细信息。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/configs](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Configuration/operation/GetAllBatchConfigs) | 返回所有可用批处理配置的列表。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/StartBatchRun) | 使用配置启动批量输出生成运行。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/execution/{executionId}](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetBatchRunInstanceState) | 检索批处理作业的执行状态。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/batch/output/config/{configName}/executions](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-batch/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 列出特定批处理配置的所有正在运行的实例。 | 异步/批处理 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePDFOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePDFOutput/post) | 根据模板和数据同步生成PDF输出。 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generatePrintedOutput](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Batch-Execution/operation/GetAllRunningInstancesForBatch) | 生成可供打印的输出格式(例如，PCL、PostScript)。 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/doc/v1/generate/afp](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generate~1afp/post) | 为大容量打印生成AFP输出。 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/document/generate/pdfform](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) | 呈现具有合并数据的PDF表单(XFA/XDP)。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/status](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobStatus) | 检索PDF表单生成作业的状态。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/generate/pdfform/jobs/{id}/result](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFFormJobResult) | 获取已完成的PDF表单作业的输出/结果。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |


#### 文档操作API

| API端点 | 描述 | 执行模型 | 身份验证方法 |
| ------------------ | ---------------- | ----------| ---------- |
| [/adobe/forms/assembler/ddx/invoke](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/DDX-execution/operation/InvokeDDX) | 执行DDX指令以组合、拆分或处理PDF。 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/convert](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA) | 将PDF文档转换为PDF/A格式。 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |
| [/adobe/forms/assembler/pdfa/validate](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/api/assembler-sync/#tag/Document-validation/operation/CheckIsPDFA) | 验证PDF是否符合PDF/A标准 | 同步 | [JWT](/help/forms/jwt-api-authentication.md) |

#### 文档转换API

| API端点 | 描述 | 执行模型 | 身份验证方法 |
|--------- | -------|---------|----------------------|
| [/adobe/document/convert/pdftoxdp](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Conversion/paths/~1convert~1pdftoxdp/post) | 将PDF表单转换为XDP格式。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### 文档提取API

| API端点 | 描述 | 执行模型 | 身份验证方法 |
|---------| -------|---------|----------------------|
| [/adobe/forms/doc/v1/extract/pdfproperties](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1pdfproperties/post) | 从PDF中提取属性和结构信息。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/extractUsageRights) | 提取嵌入到PDF中的使用权限。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1metadata/post) | 提取元数据，例如标题、作者和关键字。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/forms/doc/v1/extract/data](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/exportData) | 从PDF forms中提取表单数据(XML/JSON)。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/extract/security](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Extraction/paths/~1extract~1security/post) | 提取安全设置，如权限和加密。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### Document Transformation API


| API端点 | 描述 | 执行模型 | 身份验证方法 |
|--------|---------|---------|----------------------|
| [/adobe/document/transform/metadata](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1transform~1metadata/post) | 在PDF文档中更新或添加元数据。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/add](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1add/post) | 向PDF添加数字签名字段。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/clear](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1clear/post) | 清除签名字段的内容。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/field/signature/remove](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Transformation/paths/~1field~1signature~1remove/post) | 从PDF中删除签名字段。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |

#### 文档Assurance API

| API端点 | 描述 | 执行模型 | 身份验证方法 |
|---------|-------|---------|----------------------|
| [/adobe/document/assure/usagerights](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/applyUsageRights) | 将使用权限应用于PDF（例如，注释、填充、签名）。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/encrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1encrypt/post) | 使用密码或证书安全对PDF进行加密。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/decrypt](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1decrypt/post) | 解密受保护的PDF文档。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/sign](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1sign/post) | 对PDF文档进行数字签名。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |
| [/adobe/document/assure/certify](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#tag/Document-Assurance/paths/~1assure~1certify/post) | 使用数字证书认证PDF。 | 同步 | [OAuth](/help/forms/oauth-api-authetication.md) |


## 相关步骤

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
