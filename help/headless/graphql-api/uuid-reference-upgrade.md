---
title: 升级您的内容片段以获取UUID引用
description: 了解如何在Adobe Experience Manager as a Cloud Service中升级内容片段以优化UUID引用，从而提供Headless内容。
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: 5aa04f3b042f8e9f9af97148ceab0288ff210238
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 2%

---

# 升级您的内容片段以获取UUID引用 {#upgrade-content-fragments-for-UUID-references}

>[!IMPORTANT]
>
>与内容片段一起使用的GraphQL API的各种功能可通过早期采用者计划获取。
>
>要查看状态以及如果您有兴趣如何应用，请查看[发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

为了优化GraphQL过滤器的稳定性，您可以升级内容片段中的内容和片段引用，以便它们使用通用唯一标识符(UUID)。

内容片段模型最初提供了&#x200B;**内容引用**&#x200B;和&#x200B;**片段引用**&#x200B;的数据类型。 这两个引用都使用路径指向引用的资源，如果移动该资源，此路径可能会过期。 尽管此类引用在大多数情况下已经远远不够，但内容片段模型已得到扩展，还可根据UUID提供引用：

* **内容引用(UUID)**
* **片段引用(UUID)**。

这些新引用类型既可用于新内容片段模型，也可用于扩展现有实例。

要升级现有内容片段和模型，您可以运行此处介绍的过程。

>[!CAUTION]
>
>在运行升级过程之前，您应该始终[执行试运行](#execute-a-dry-run)，以突出显示内容的任何潜在问题。

## 升级的内容 {#what-is-upgraded}

进行了以下更新：

* 数据类型的字段：
   * **内容引用**&#x200B;已转换为&#x200B;**内容引用(UUID)**
   * **片段引用**&#x200B;已转换为&#x200B;**片段引用(UUID)**
* 保存在这些字段中的基于路径的引用的值会被相应的UUID替换

>[!NOTE]
>
>升级后，两种数据类型在内容片段模型编辑器中仍可用。 您可以基于这两种类型创建新字段（尽管预计您将使用基于UUID的类型），并在需要时重新运行升级。

## 未升级的内容 {#what-is-not-upgraded}

以下引用不会升级：

* 页面引用 — 尚不支持UUID
* 任何无效引用；例如，不存在内容片段路径或资产路径的目标

   * 不升级无效引用，就像内容片段路径或资产路径无效一样，没有要分配的相应UUID。 原始参考保持不变。

   * 使用[练习](#execute-a-dry-run)来检测任何无效的引用。

  >[!NOTE]
  >
  >由于无效，无论是否升级，它们都不可用。

## 何时不应升级 {#when-you-should-not-upgrade}

不升级：

* 当您的任何内容片段使用页面引用时；作为UUID，页面引用尚不受支持

## UUID引用的限制 {#limitations-of-uuid-references}

目前，在使用基于UUID的引用时，以下限制适用：

* 模型

   * 无法通过OpenAPI创建具有内容片段UUID或内容引用UUID字段的新内容片段模型。
   * 模型的`id`字段尚未更改为基于UUID。 它使用模型的base64解码路径。 无法移动模型，因此，该值仍保持稳定。

* 资源

   * 在通过OpenAPI创建内容片段时，`fragment-reference`或`content-reference`字段类型必须用于分别指定对片段或资产的引用 — 即使设置基于UUID的引用字段的值时也是如此。

## 升级计划 {#upgrade-planning}

运行升级之前，需要执行一些准备步骤。

### 执行试运行 {#execute-a-dry-run}

建议&#x200B;*每次*&#x200B;升级内容时，首先执行试运行。 这将创建日志文件，其条目会突出显示任何潜在问题：

* 无效引用
* 页面引用

在`dryRun`模式下运行内容升级以：

* 识别任何无效引用；通过在日志文件中列出它们
然后，您可以在运行实际内容升级之前修复这些引用。
* 识别任何页面引用；通过在日志文件中列出它们
检测到页面引用时，[不应运行内容升级](#when-you-should-not-upgrade)。


### 强制内容冻结 {#enforce-a-content-freeze}

应计划在内容冻结期间执行内容升级。

内容冻结的持续时间取决于要升级的内容片段的数量。 因此，升级可能从几分钟到几小时不等，并且还取决于开始内容升级时使用的参数。

## 运行内容升级 {#running-the-content-upgrade}

可以使用终结点管理内容升级： `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>您的帐户需要`Administrator`角色才能访问端点。

### 开始内容升级 {#start-a-content-upgrade}

| 端点 | HTTP请求类型 | 注释 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **请求参数** | **值** | |
| action | `start` | |
| serviceTypeId | `uuidUpgradeService` | 服务类型ID（预定义的固定值）。 |
|  segmentSize | `1000` | 一个区段（批次）中将升级的内容片段或模型的数量。 |
| 基本路径 | `/conf` | 指定以下任一项：<ul><li>根`/conf`升级所有AEM配置</li><li>选定的AEM配置路径。 对其执行内容升级<br>例如： `/conf/wknd-shared`仅升级单个租户`wknd-shared`</li></ul> |
| 间隔 | `10` | 以秒为单位的间隔，在此之后将升级下一个内容片段或模型。 |
| 模式 | `replicate`、`noReplicate` | <ul><li>`replicate`：在所有AEM Publish实例上复制相同的作业</li><li>`noReplicate`：仅在AEM创作实例上运行作业</li></ul> |
| dryRun |  `true`，`false` | <ul><li>`false`：模拟内容升级，不保存任何内容更改</li><li>`true`：执行内容升级，并保存内容更改</li></ul> |
| **响应详细信息** | **值** | |
| jobId | `UUID` |  执行内容升级的作业的ID。<ul><li>任何与此执行相关的后续调用都需要此ID。</li><li>如果`mode`值设置为`replicate`，则在AEM Publish实例上执行也需要位于同一`jobId`下。</li></ul> |
| 参数 | 内容升级参数 | 这些包括为启动内容升级而提供的初始参数，以及一些内部默认值。 |


### 示例内容升级请求 {#example-content-upgrade-request}

+++请求

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++响应

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### 获取内容升级的状态 {#get-the-status-of-a-content-upgrade}

| 端点 | HTTP请求类型 | 注释 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **请求参数** | **值** | |
| action | 状态 | |
| jobId | `<UUID>` | 从开始内容升级的调用返回的`jobId`。 |
| **响应详细信息** | **值** | |
| 状态 | JSON值 | 包含内容升级的详细状态：<ul><li>每隔间隔（秒）更新一次。</li><li>`uuidUpgradeService`执行有两个阶段：<ol><li>阶段–0以升级内容片段模型</li><li>升级内容片段的阶段1</li></ol></li><li>在每个阶段中，统计信息会在每个间隔后更新。</li><li>“jobStatus”：“COMPLETED”将升级标记为已成功完成。</li><li>其他状态值不言自明。</li></ul> |

### 示例内容升级状态请求 {#example-content-upgrade-status-request}

+++请求

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++响应

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++示例日志文件

除了从HTTP端点获得的正在运行的内容升级的状态之外，AEM日志还提供有关内容级别进度的详细信息。 例如：

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

此外，在处理内容片段和模型的每个区段（批次）后，将记录累积状态，以总结迄今为止的进度。 例如：

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### 中止内容升级 {#abort-a-content-upgrade}

>[!CAUTION]
>
>中止内容升级（这不是演习）：
>
>* 不还原已做出的任何更改
>* 可能会使您的内容处于混合状态
>
>请谨慎使用此操作。

| 端点 | HTTP请求类型 | 注释 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **请求参数** | **值** | |
| action | abort | |
| jobId | `<UUID>` | 从开始内容升级的调用返回的`jobId`。 |
| **响应详细信息** | **值** | |
| 状态 | JSON值 | 包含内容升级的详细状态：<ul><li>要注意的状态是“jobStatus”：“ABORTED”。<br>中止操作后，将不会处理任何挂起的数据段。</li><li>如果jobStatus在中止之前为“COMPLETED”，则调用没有任何效果。</li></ul> |

### 中止内容升级请求的示例 {#example-abort-content-upgrade-request}

+++请求

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++响应

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
