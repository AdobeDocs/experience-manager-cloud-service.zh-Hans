---
title: 复制
description: 了解AEM as a Cloud Service中的分发和故障排除复制。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
feature: Operations
role: Admin
source-git-commit: 60006b0e0b5215263b53cbb7fec840c47fcef1a8
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 31%

---

# 复制 {#replication}

Adobe Experience Manager as a Cloud Service使用[Sling内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)功能将内容移动到要复制到在AEM运行时以外的Adobe Developer上运行的管道服务。

>[!NOTE]
>
>阅读[分发](/help/overview/architecture.md#content-distribution)以了解更多信息。

## 发布内容的方法 {#methods-of-publishing-content}

>[!NOTE]
>
>如果您有兴趣批量发布内容，请使用[树激活工作流步骤](#tree-activation)创建工作流，以便有效地处理大型负载。
>不建议自行构建批量发布自定义代码。
>如果您必须出于任何原因进行自定义，则可以使用现有工作流API通过此步骤触发工作流。
>始终最好是仅发布必须发布的内容。 如果不需要的话，谨慎不要尝试发布大量内容。 但是，使用树激活工作流步骤可以通过工作流发送的内容数量没有限制。

### 快速取消/发布 – 计划取消/发布 {#publish-unpublish}

此功能允许您立即发布选定的页面，而无需通过“管理发布”方法选择其他选项。

有关更多信息，请参阅[管理发布](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)。

### 开启和关闭时间 – 触发器配置 {#on-and-off-times-trigger-configuration}

**开始时间**&#x200B;和&#x200B;**关闭时间**&#x200B;的附加可能性可从[页面属性的“基本”选项卡](/help/sites-cloud/authoring/sites-console/page-properties.md#basic)获得。

若要实现此功能的自动复制，请在[OSGi配置](/help/implementing/deploying/configuring-osgi.md) **开启关闭触发器配置**&#x200B;中启用&#x200B;**自动复制**：

![OSGi 开启关闭触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 管理发布 {#manage-publication}

与快速Publish相比，管理发布提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流，并且还提供了以后发布的选项。

为“稍后发布”选项包含文件夹的子项会调用Publish内容树工作流，如本文所述。

您可以[在出版基础文档](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)中找到有关管理出版的更多详细信息。

### 树激活工作流步骤 {#tree-activation}

树激活工作流步骤旨在高效复制内容节点的深层层次结构。 当队列变得过大时，它会自动暂停，以允许以最小的延迟并行执行其他复制。

创建使用`TreeActivation`流程步骤的工作流模型：

1. 从AEM as a Cloud Service主页，转到&#x200B;**工具 — 工作流 — 模型**。
1. 在“工作流模型”页面中，按屏幕右上角的&#x200B;**创建**。
1. 为模型添加标题和名称。 有关详细信息，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)。
1. 从列表中选择已创建的模型，然后按&#x200B;**编辑**
1. 在以下窗口中，删除默认显示的步骤
1. 将“流程步骤”拖放到当前模型流中：

   ![流程步骤](/help/operations/assets/processstep.png)

1. 选择流中的“流程”步骤，然后按扳手图标选择&#x200B;**配置**。
1. 选择&#x200B;**进程**&#x200B;选项卡并从下拉列表中选择`Publish Content Tree`，然后选中&#x200B;**处理程序前进**&#x200B;复选框

   ![树激活](/help/operations/assets/new-treeactivationstep.png)

1. 在&#x200B;**参数**&#x200B;字段中设置任何附加参数。 可以将多个以逗号分隔的参数字符串在一起。 例如：

   `enableVersion=false,agentId=publish,chunkSize=50,maxTreeSize=500000,dryRun=false,filters=onlyModified,maxQueueSize=10`

   >[!NOTE]
   >
   >有关参数列表，请参阅&#x200B;**参数**&#x200B;部分。

1. 按&#x200B;**完成**&#x200B;以保存工作流模型。

**参数**

| 名称 | 默认 | 说明 |
| -------------- | ------- | --------------------------------------------------------------- |
| 路径 |         | 要从其开始的根路径 |
| agentId | 发布 | 要使用的复制代理名称 |
| chunkSize | 50 | 要捆绑到单个复制中的路径数 |
| maxTreeSize | 500000 | 树的最大节点数（视为小） |
| maxQueueSize | 10 | 复制队列中的最大项目数 |
| enableVersion | false | 启用版本控制 |
| dryRun | false | 当设置为true时，实际上不调用复制 |
| userId |         | 仅适用于作业。 在工作流中，使用调用工作流的用户 |
| 个筛选条件 |         | 节点筛选器名称列表。 请参阅下面的支持的过滤器 |

**支持筛选器**

| 名称 | 说明 |
| ------------- | ------------------------------------------- |
| onlyModified | 自上次发布后修改的节点 |
| onlyPublished | 之前发布的节点 |


**恢复支持**

该工作流会按块处理内容，每个块表示要发布的完整内容的子集。  如果系统停止了工作流，工作流将从之前停止的位置继续。

**监视工作流进度**

1. 从AEM as a Cloud Service主页，转到&#x200B;**工具 — 常规 — 作业**。
1. 查看与您的工作流对应的行。 *progress*&#x200B;列指示复制进度。 例如，它可以显示41/564，并且在刷新时，它可以更新为52/564。

   ![树激活进度](/help/operations/assets/treeactivation-progress.png)


1. 选择行并打开它可提供有关工作流执行状态的更多详细信息。

   ![树激活状态详细信息](/help/operations/assets/treeactivation-progress-details.png)



### 发布内容树工作流程 {#publish-content-tree-workflow}

>[!NOTE]
>
>此功能已弃用，支持更高效的树激活步骤，此步骤可包含在自定义工作流中。

<details>
<summary>单击此处了解有关此已弃用功能的更多信息。</summary>

您可以通过选择&#x200B;**工具 – 工作流 – 模型**&#x200B;和复制&#x200B;**发布内容树**&#x200B;现成的工作流模型，如下所示：

![Publish内容树工作流信息卡](/help/operations/assets/publishcontenttreeworkflow.png)

请勿调用原始模型。 相反，请确保首先复制模型并调用该副本。

与所有工作流一样，也可以通过 API 调用。 有关详细信息，请参阅[以编程方式与工作流交互](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html#extending-aem)。

或者，您也可以创建使用`Publish Content Tree`进程步骤的工作流模型。

1. 从AEM as a Cloud Service主页，转到&#x200B;**工具 — 工作流 — 模型**。
1. 在“工作流模型”页面中，按屏幕右上角的&#x200B;**创建**。
1. 为模型添加标题和名称。 有关详细信息，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)。
1. 从列表中选择已创建的模型，然后按&#x200B;**编辑**
1. 在以下窗口中，将“流程步骤”拖放到当前模型流中：

   ![流程步骤](/help/operations/assets/processstep.png)

1. 选择流中的“流程”步骤，然后按扳手图标选择&#x200B;**配置**。
1. 选择&#x200B;**进程**&#x200B;选项卡并从下拉列表中选择`Publish Content Tree`，然后选中&#x200B;**处理程序前进**&#x200B;复选框

   ![树激活](/help/operations/assets/newstep.png)

1. 在&#x200B;**参数**&#x200B;字段中设置任何附加参数。 可以将多个以逗号分隔的参数字符串在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >有关参数列表，请参阅&#x200B;**参数**&#x200B;部分。

1. 按&#x200B;**完成**&#x200B;以保存工作流模型。

**参数**

* `includeChildren`（布尔值，默认：`false`）。 值`false`表示仅发布路径；`true`表示子项也发布。
* `replicateAsParticipant`（布尔值，默认：`false`）。 如果配置为 `true`，则复制操作将使用 `userid` 执行参与者步骤的主体。
* `enableVersion`（布尔值，默认： `false`）。 此参数可确定复制时是否创建了新版本。
* `agentId`（字符串值，默认表示仅使用发布代理）。 建议明确说明 agentId；例如，将其设置为值：发布。 正在将代理设置为`preview`发布到预览服务。
* `filters` （字符串值，默认表示激活所有路径）。 可用值包括：
   * `onlyActivated` — 仅激活已（已）激活的页面。 作为重新激活的一种形式。
   * `onlyModified`  – 仅激活已激活且修改日期晚于激活日期的路径。
   * 上面可以用管道字符“|”进行“或”操作。 例如：`onlyActivated|onlyModified`。

**记录**

当树激活工作流步骤启动时，它将在“信息”日志级别记录其配置参数。 激活路径时，也会记录 INFO 语句。

在工作流步骤复制了所有路径之后，将记录最终的INFO语句。

此外，您还可以将低于`com.day.cq.wcm.workflow.process.impl`的记录器的日志级别增加到DEBUG/TRACE以获取更多日志信息。

如果存在错误，工作流步骤将以`WorkflowException`终止，它封装了基础异常。

以下是在示例发布内容树工作流中生成的日志示例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```
</details>

### 复制 API {#replication-api}

您可以使用 AEM as a Cloud Service 中提供的复制 API 发布内容。

有关详细信息，请参阅 [API 文档](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html)。

**API 的基本用法**

```
@Reference
Replicator replicator;
@Reference
ReplicationStatusProvider replicationStatusProvider;

....
Session session = ...
// Activate a single page to all agents, which are active by default
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en");
// Activate multiple pages (but try to limit it to approx 100 at max)
replicator.replicate(session,ReplicationActionType.ACTIVATE, new String[]{"/content/we-retail/en","/content/we-retail/de"});

// ways to get the replication status
Resource enResource = resourceResolver.getResource("/content/we-retail/en");
Resource deResource = resourceResolver.getResource("/content/we-retail/de");
ReplicationStatus enStatus = enResource.adaptTo(ReplicationStatus.class);
// if you need to get the status for more more than 1 resource at once, this approach is more performant
Map<String,ReplicationStatus> allStatus = replicationStatusProvider.getBatchReplicationStatus(enResource,deResource);
```

**使用特定代理进行复制**

如上面的示例所示，在复制资源时，将只使用默认处于活动状态的代理。 在AEM as a Cloud Service中，它仅意味着称为“发布”的代理，用于将作者连接到发布层。

为了支持预览功能，已添加名为“预览”的新代理，默认情况下该代理处于非活动状态。 此代理用于将作者连接到预览层。 如果只想通过预览代理复制，则必须通过`AgentFilter`明确选择此预览代理。

请参阅以下示例：

```
private static final String PREVIEW_AGENT = "preview";

ReplicationStatus beforeStatus = enResource.adaptTo(ReplicationStatus.class); // beforeStatus.isActivated == false

ReplicationOptions options = new ReplicationOptions();
options.setFilter(new AgentFilter() {
  @Override
  public boolean isIncluded (Agent agent) {
    return agent.getId().equals(PREVIEW_AGENT);
  }
});
// will replicate only to preview
replicator.replicate(session,ReplicationActionType.ACTIVATE,"/content/we-retail/en", options);

ReplicationStatus afterStatus = enResource.adaptTo(ReplicationStatus.class); // afterStatus.isActivated == false
ReplicationStatus previewStatus = afterStatus.getStatusForAgent(PREVIEW_AGENT); // previewStatus.isActivated == true
```

如果您没有提供此类过滤器，并且只使用“发布”代理，则不使用“预览”代理，并且复制操作不会影响预览层。

仅当复制操作包括至少一个默认处于活动状态的代理时，才会修改资源的整体`ReplicationStatus`。 在上面的示例中，此流不是这种情况。 复制只是使用“预览”代理。 因此，您必须使用新的`getStatusForAgent()`方法，该方法允许查询特定代理的状态。 此方法也适用于“发布”代理。 如果已使用提供的代理完成任何复制操作，则返回非空值。

### 使内容失效的方法 {#invalidating-content}

您可以直接使内容失效，方法是使用作者的Sling内容失效(SCD)（首选方法），或使用复制API调用发布Dispatcher Flush复制代理。 有关更多详细信息，请参阅[缓存](/help/implementing/dispatcher/caching.md)页面。

**复制 API 容量限制**

一次复制不到100个路径，以500为限制。 超出限制，将引发`ReplicationException`。
如果您的应用程序逻辑不需要原子复制，则可以通过将`ReplicationOptions.setUseAtomicCalls`设置为false（它接受任意数量的路径，但在内部创建存储段以保持在此限制以下）来克服此限制。

每次复制调用传输的内容大小不得超过 `10 MB`。 此规则包括节点和属性，但不包括任何二进制文件（工作流包和内容包被视为二进制文件）。


## 疑难解答 {#troubleshooting}

要对复制问题进行故障诊断，请导航到 AEM 创作服务 Web UI 中的复制队列：

1. 从AEM“开始”菜单中，导航到&#x200B;**工具** > **部署** > **分发**
1. 选择&#x200B;**发布**&#x200B;卡

   ![状态](assets/publish-status.png "状态")

1. 检查应为绿色的队列状态
1. 您可以测试与复制服务的连接
1. 选择&#x200B;**日志**&#x200B;选项卡，其中显示了内容发布的历史记录

![日志](assets/publish-logs.png "日志")

如果内容无法发布，则整个发布将从AEM Publish服务中恢复。

在这种情况下，可编辑的主队列将显示红色状态，应该进行审查以确定哪些项目导致取消发布。 通过单击该队列，将显示其待处理项目，如果需要，可从中清除单个项目或所有项目。
