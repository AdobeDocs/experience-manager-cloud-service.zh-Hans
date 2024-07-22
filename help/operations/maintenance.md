---
title: AEM as a Cloud Service 中的维护任务
description: 了解AEM as a Cloud Service中的维护任务以及如何配置它们。
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
feature: Operations
role: Admin
source-git-commit: b8bed4acf895f1cf04ea92ae27b87c7bfb38863d
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 30%

---

# AEM as a Cloud Service 中的维护任务 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="维护任务"
>abstract="维护任务是按计划运行以优化存储库的过程。使用 AEM as a Cloud Service 会大幅减小客户配置维护任务操作属性的需求。 客户可以将资源集中在应用程序级别的问题上，而 Adobe 则会处理基础设施方面的操作。"

维护任务是按计划运行以优化存储库的过程。使用 AEM as a Cloud Service 会大幅减小客户配置维护任务操作属性的需求。 客户可以将资源集中在应用程序级别的问题上，而 Adobe 则会处理基础设施方面的操作。

## 配置维护任务 {#maintenance-tasks-configuring}

在早期版本的 AEM 中，您可以使用维护卡（“工具”>“操作”>“维护”）配置维护任务。对于 AEM as a Cloud Service，维护卡不再可用，因此应由源控件管理配置，并使用云管理器进行部署。Adobe管理那些其设置无法由客户配置的维护任务（例如，数据存储垃圾收集）。 其他维护任务可由客户配置，如下表所述。

>[!CAUTION]
>
>Adobe保留覆盖客户维护任务配置设置的权利，以缓解性能下降等问题。

下表说明了可用的维护任务。

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>维护任务</th>
    <th>谁拥有配置</th>
    <th>如何配置（可选）</th>
  </tr>  
  <tr>
    <td>数据存储垃圾收集</td>
    <td>Adobe</td>
    <td>不适用 – 完全由 Adobe 所有</td>
  </td> 
  </tr>
  <tr>
    <td>版本清除</td>
    <td>客户</td>
    <td>当前默认禁用版本清除，但可以配置策略，如<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本清除和审核日志清除维护任务</a>部分中所述。<br/><br/>默认情况下将很快启用清除，这些值可覆盖。<br>
   </td>
  </td>
  </tr>
  <tr>
    <td>审核日志清除</td>
    <td>客户</td>
    <td>审核日志清除当前默认处于禁用状态，但可以配置策略，如<a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance#purge_tasks">版本清除和审核日志清除维护任务</a>部分中所述。<br/><br/>默认情况下将很快启用清除，这些值可覆盖。<br>
   </td>
   </td>
  </tr>
  <tr>
    <td>Lucene 二进制文件清理</td>
    <td>Adobe</td>
    <td>未使用，因此被 Adobe 禁用。</td>
  </td>
  </tr>
  <tr>
    <td>临时任务清理</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。通过在文件夹<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下创建属性，覆盖<code>/libs</code>下的开箱即用维护窗口配置节点。</p>
    <p>有关其他配置详细信息，请参阅下面的维护窗口表。通过在上述节点下添加另一个节点来启用维护任务。 将其命名为<code>granite_TaskPurgeTask</code>，属性<code>sling:resourceType</code>设置为<code>granite/operations/components/maintenance/task</code>，属性<code>granite.maintenance.name</code>设置为<code>TaskPurge</code>。 配置OSGI属性，请参阅<code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code>以获取属性列表。</p>
  </td>
  </tr>
    <tr>
    <td>工作流清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。通过在文件夹<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下创建属性，覆盖<code>/libs</code>下的开箱即用维护窗口配置节点。 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_WorkflowPurgeTask</code>），启用维护任务。配置 OSGI 属性，请参见<a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances"> AEM 6.5 维护任务文档</a>。</p>
  </td>
  </tr>
  <tr>
    <td>项目清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。通过在文件夹<code>/apps/settings/granite/operations/maintenance/granite_weekly</code>、<code>granite_daily</code>或<code>granite_monthly</code>下创建属性，覆盖<code>/libs</code>下的开箱即用维护窗口配置节点。 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_ProjectPurgeTask</code>），启用维护任务。请参阅**Adobe项目清除配置**下的[OSGI属性](/help/implementing/deploying/configuring-osgi.md)列表。</p>
  </td>
  </tr>
  </tbody>
</table>

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>维护窗口配置</th>
    <th>谁拥有配置</th>
    <th>配置类型</th>
    <th>参数</th>
  </tr>
  <tr>
    <td>每日</td>
    <td>客户</td>
    <td>JCR 节点定义</td>
  <td>
  <p><strong>windowSchedule=daily</strong>（此值不应更改）</p>
  <p><strong>windowStartTime=HH:MM</strong> 用作 24 小时时钟。定义与每日维护窗口相关联的维护任务何时开始执行。</p>
  <p><strong>windowEndTime=HH:MM</strong> 用作 24 小时时钟。定义与每日维护窗口关联的维护任务在尚未完成时应何时停止执行。</p>
  <p>在此时间范围内，维护任务不能执行多次。</p>
  </td> 
  </tr>
  <tr>
    <td>每周</td>
    <td>客户</td>
    <td>JCR 节点定义</td>
    <td>
    <p><strong>windowSchedule=weekly</strong>（此值不应更改）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作 24 小时时钟。定义与每周维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作 24 小时时钟。定义与每周维护窗口关联的维护任务在尚未完成时应何时停止执行。</p>
    <p>在此时间范围内，维护任务不能执行多次。</p>
    <p><strong>windowScheduleWeekdays =由1 - 7（例如，[5,5]）中的两个值组成的数组</strong>数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR 节点定义</td>
    <td>
    <p><strong>windowSchedule=monthly</strong> （此值不应更改）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务在尚未完成时应何时停止执行。</p>
    <p>在此时间范围内，维护任务不能执行多次。</p>
    <p><strong>windowScheduleWeekdays =由1 - 7（例如，[5,5]）中的两个值组成的数组</strong>数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 表示安排在每月的第一周，或 1 表示安排在每月最后一周。如果没有值，则会有效地在受windowScheduleWeekdays控制的日期（每月）计划作业。</p>
    </td>
    </tr>
    </tbody>
</table>

**位置**：

* 每天 - /apps/settings/granite/operations/maintenance/granite_daily
* 每周 - /apps/settings/granite/operations/maintenance/granite_weekly
* 每月 - /apps/settings/granite/operations/maintenance/granite_monthly

**代码示例**：

代码示例 1（每日）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
  xmlns:jcr="http://www.jcp.org/jcr/1.0" 
  jcr:primaryType="sling:Folder"
  sling:configCollectionInherit="true"
  sling:configPropertyInherit="true"
  windowSchedule="daily"
  windowStartTime="03:00"
  windowEndTime="05:00"
 />
```

代码示例 2（每周）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="weekly"
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

代码示例 3（每月）

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" 
   xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="sling:Folder"
   sling:configCollectionInherit="true"
   sling:configPropertyInherit="true"
   windowEndTime="15:30"
   windowSchedule="monthly"
   windowFirstLastStartDay=0
   windowScheduleWeekdays="[5,5]"
   windowStartTime="14:30"/>
```

## 版本清除和审核日志清除维护任务 {#purge-tasks}

清除版本和审核日志会减小存储库的大小，在某些情况下，可以提高性能。

>[!NOTE]
>
>AEM Guides客户不应配置版本清除。

### 默认 {#defaults}

当前，默认情况下不启用清除，但未来将更改此设置。 在启用默认清除之前创建的环境具有更保守的阈值，因此清除不会意外发生。 有关默认清除策略的更多详细信息，请参阅下面的版本清除和审核日志清除部分。
<!-- Version purging and audit log purging are on by default, with different default values for environments with ids higher than **TBD** versus those with ids lower than that value. -->

<!-- ### Overriding the default values with a new configuration {#override} -->

可以通过声明配置文件并部署它来覆盖默认的清除值，如下所述。

<!-- The reason for this behavior is to clarify the ambiguity over whether the default purge values would take effect once you remove the declaration. -->

### 应用配置 {#configure-purge}

声明配置文件并按照以下步骤中所述进行部署。

>[!NOTE]
>在配置文件中部署版本清除节点后，必须将其保留为已声明状态，不得将其删除。 如果尝试这样做，配置管道将失败。
> 
>同样，在配置文件中部署审核日志清除节点后，必须将其保留为已声明状态而不是将其删除。

**1** — 在Git中项目的顶级文件夹中创建以下文件夹和文件结构：

```
config/
     mt.yaml
```

**2** — 在配置文件中声明属性，包括：

* 值为“MaintenanceTasks”的“kind”属性。
* “版本”资产（当前为版本1）。
* 具有属性`envTypes`的可选“元数据”对象，该对象具有此配置对其有效的环境类型(dev、stage、prod)的逗号分隔列表。 如果未声明任何元数据对象，则该配置对所有环境类型都有效。
* 同时具有`versionPurge`和`auditLogPurge`对象的数据对象。

请参阅下面的`versionPurge`和`auditLogPurge`对象的定义和语法。

您应构建类似于以下示例的配置：

```
kind: "MaintenanceTasks"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  versionPurge:
    maximumVersions: 15
    maximumAgeDays: 20
    paths: ["/content"]
    minimumVersions: 1
    retainLabelledVersions: false
  auditLogPurge:
    rules:
      - replication:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["Activate", "Deactivate", "Delete", "Test", "Reverse", "Internal Poll"]
      - pages:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["PageCreated", "PageModified", "PageMoved", "PageDeleted", "VersionCreated", "PageRestored", "PageValid", "PageInvalid"]
      - dam:
          maximumAgeDays: 15
          contentPath: "/content"
          types: ["ASSET_EXPIRING", "METADATA_UPDATED", "ASSET_EXPIRED", "ASSET_REMOVED", "RESTORED", "ASSET_MOVED", "ASSET_VIEWED", "PROJECT_VIEWED", "PUBLISHED_EXTERNAL", "COLLECTION_VIEWED", "VERSIONED", "ADDED_COMMENT", "RENDITION_UPDATED", "ACCEPTED", "DOWNLOADED", "SUBASSET_UPDATED", "SUBASSET_REMOVED", "ASSET_CREATED", "ASSET_SHARED", "RENDITION_REMOVED", "ASSET_PUBLISHED", "ORIGINAL_UPDATED", "RENDITION_DOWNLOADED", "REJECTED"]
```

请记住，为了使配置有效：

* 必须定义所有属性。 没有继承的默认值。
* 必须遵循以下属性表中的类型（整数、字符串、布尔值等）。

>[!NOTE]
>您可以使用`yq`在本地验证配置文件的YAML格式（例如，`yq mt.yaml`）。

**3** — 配置非生产和生产配置管道。

快速开发环境(RDE)不支持清除。 对于生产（非沙盒）程序中的其他环境类型，请在Cloud Manager中创建目标部署配置管道。

有关详细信息，请参阅[配置生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)和[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)。

### 版本清除 {#version-purge}

>[!NOTE]
>
>AEM Guides客户不应配置版本清除。

#### 版本清除默认值 {#version-purge-defaults}

<!-- For version purging, environments with an id higher than **TBD** have the following default values: -->

当前，默认情况下不启用清除，但未来将更改此设置。

启用默认清除后创建的环境将具有以下默认值：

* 超过30天的版本将被删除。
* 保留过去30天内的最新5个版本。
* 无论上述规则如何，都会保留最新版本（以及当前文件）。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

在启用默认清除之前创建的环境将具有下面列出的默认值，但建议降低这些值以优化性能。

* 超过7年的版本将被删除。
* 保留过去7年的所有版本。
* 7年后，除最新版本（以及当前文件）以外的版本将被删除。

#### 版本清除属性 {#version-purge-properties}

下面列出了允许的属性。

指示&#x200B;*default*&#x200B;的列指示将来应用默认值时的默认值；*TBD*&#x200B;反映了一个仍未确定的环境ID。

| 属性 | 环境未来的默认值>待定 | 环境&lt;=TBD的未来默认值 | 必填 | 类型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 路径 | [“/content”] | [“/content”] | 是 | 字符串数组 | 指定创建新版本时要在哪些路径下清除版本。  客户必须声明此属性，但唯一允许的值是“/content”。 |
| maximumAgeDay | 30 | 2557（7年+ 2个闰日） | 是 | 整数 | 将删除比配置值更早的任何版本。 如果该值为0，则不会根据版本的存在时间执行清除。 |
| maximumVersions | 5 | 0（无限制） | 是 | 整数 | 第n个最新版本之前的版本将被删除。 如果该值为0，则不会根据版本数执行清除。 |
| minimumVersion | 1 | 1 | 是 | 整数 | 无论使用年限如何，保留的最小版本数。 请注意，始终至少保留1个版本；其值必须为1或更高。 |
| retainLabelledVersioned | false | false | 是 | 布尔型 | 确定是否将从清除中排除明确标记的版本。 为了更好地优化存储库，建议将此值设置为false。 |


**属性交互**

以下示例说明了资产在组合时如何进行交互。

示例：

```
maximumAgeDays = 30
maximumVersions = 10
minimumVersions = 2
```

如果第23天有11个版本，则下次清除维护任务运行时将清除最早的版本，因为`maximumVersions`属性设置为10。

如果第31天有5个版本，则仅清除3个版本，因为`minimumVersions`属性设置为2。

示例：

```
maximumAgeDays = 30
maximumVersions = 0
minimumVersions = 1
```

由于`maximumVersions`属性设置为0，因此不会清除任何超过30天的版本。

将保留30天之前的版本。

### 审核日志清除 {#audit-purge}

#### 审核日志清除默认值 {#audit-purge-defaults}

<!-- For audit log purging, environments with an id higher than **TBD** have the following default values: -->

当前，默认情况下不启用清除，但未来将更改此设置。

启用默认清除后创建的环境将具有以下默认值：

* 超过7天的复制、DAM和页面审核日志将被删除。
* 记录所有可能的事件。

<!-- Environments with an id equal or lower than **TBD** will have the following default values: -->

在启用默认清除之前创建的环境将具有下面列出的默认值，但建议降低这些值以优化性能。

* 超过7年的复制、DAM和页面审核日志将被删除。
* 记录所有可能的事件。

>[!NOTE]
>建议那些有法规要求生成不可编辑的审核日志的客户与专门的外部服务集成。

#### 审核日志清除属性 {#audit-purge-properties}

下面列出了允许的属性。

指示&#x200B;*default*&#x200B;的列指示将来应用默认值时的默认值；*TBD*&#x200B;反映了一个仍未确定的环境ID。


| 属性 | 环境未来的默认值>待定 | 环境&lt;=TBD的未来默认值 | 必填 | 类型 | 值 |
|-----------|--------------------------|-------------|-----------|---------------------|-------------|
| 规则 | - | - | 是 | 对象 | 以下一个或多个节点：复制、页面、dam。 其中每个节点都定义了规则，并具有以下属性。 必须声明所有属性。 |
| maximumAgeDay | 7 天 | 对于所有人，2557年（7年以上2个闰日） | 是 | 整数 | 对于复制、页面或dam：审核日志的保留天数。 将清除早于配置值的审核日志。 |
| 内容路径 | “/content” | “/content” | 是 | 字符串 | 将清除审核日志的路径（针对相关类型）。 必须设置为“/content”。 |
| 类型 | 所有值 | 所有值 | 是 | 枚举数组 | 对于&#x200B;**复制**，枚举值为： Activate、Deactivate、Delete、Test、Reverse、Internal Poll。 对于&#x200B;**页面**，枚举值为： PageCreated、PageModified、PageMoved、PageDeleted、VersionCreated、PageRestored、PageRolled、PageValid、PageInvalid。 对于&#x200B;**dam**，枚举值包括：ASSET_EXPIRING、METADATA_UPDATED、ASSET_EXPIRED、ASSET_REMOVED、RESTORED、ASSET_MOVED、ASSET_VIEWED、PROJECT_VIEWED、PUBLISHED_EXTERNAL、COLLECTION_VIEWED、VERSIONED、ADDED_COMMENT、RENDITION_UPDATED、ACCEPTED、DOWATED、DOWNATED、DOWNATED、SUPATED、SUBONED、SUBASSET_UPDATED、RATED、SUBASSET_REMOVED、REMOVED、ASSET_REMOVED、ASSET已共享、RENDITION_REMOVED、ASSET_PUBLISHED、ORIGINAL_UPDATED、RENDITION_DOWNLOADED、REJECTED。 |
