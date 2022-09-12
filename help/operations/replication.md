---
title: 复制
description: 分发和故障排除复制。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 30428716603a53f3a549a18541de593bbfe879df
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 复制 {#replication}

Adobe Experience Manager as a Cloud Service 使用 [Sling 内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)将内容移动到要复制到在 AEM 运行时以外的 Adobe I/O 上运行的管道服务的功能。

>[!NOTE]
>
>阅读[分发](/help/overview/architecture.md#content-distribution)以了解更多信息。

## 发布内容的方法 {#methods-of-publishing-content}

### 快速取消/发布 – 计划取消/发布 {#publish-unpublish}

这允许您立即发布选定的页面，而无需通过“管理发布”方法选择其他选项。

有关更多信息，请参阅[管理发布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)。

### 开启和关闭时间 – 触发器配置 {#on-and-off-times-trigger-configuration}

**开始时间**&#x200B;和&#x200B;**关闭时间**&#x200B;的附加可能性可从[页面属性的“基本”选项卡](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)获得。

要实现自动复制，您需要在 [OSGi 配置](/help/implementing/deploying/configuring-osgi.md)**开启关闭触发器配置**&#x200B;启用&#x200B;**自动复制**：

![OSGi 开启关闭触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 管理发布 {#manage-publication}

与快速发布相比，管理发布提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流，并且还提供了在以后的日期发布的选项。

为“稍后发布”选项包含文件夹的子项将调用发布内容树工作流，如本文所述。

您可以[在出版基础文档](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)中找到有关管理出版的更多详细信息。

### 发布内容树工作流程 {#publish-content-tree-workflow}

您可以通过选择&#x200B;**工具 – 工作流 – 模型**&#x200B;和复制&#x200B;**发布内容树**&#x200B;现成的工作流模型，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

请勿修改或调用原始模型。 相反，请确保首先复制模型，然后修改或调用该副本。

与所有工作流一样，也可以通过 API 调用。 有关更多信息，请参阅[以编程方式与工作流交互](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=zh-Hans#extending-aem)。

或者，您也可以通过创建使用`Publish Content Tree`流程步骤的工作流模型来实现此目的：

1. 从 AEM as a Cloud Service 主页，转到&#x200B;**工具 – 工作流 – 模型**
1. 在“工作流模型”页面中，按屏幕右上角的&#x200B;**创建**
1. 为模型添加标题和名称。 有关更多信息，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. 从列表中选择新创建的模型，然后按&#x200B;**编辑**
1. 在以下窗口中，将“流程步骤”拖放到当前模型流中：

   ![流程步骤](/help/operations/assets/processstep.png)

1. 单击流中的“流程”步骤，然后按扳手图标选择&#x200B;**配置**
1. 单击&#x200B;**流程**&#x200B;选项卡并从下拉列表中选择 `Publish Content Tree`

   ![树激活](/help/operations/assets/newstep.png)

1. 在&#x200B;**参数**&#x200B;字段中设置任何附加参数。 可以将多个以逗号分隔的参数字符串在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >有关参数列表，请参阅&#x200B;**参数**&#x200B;部分。

1. 按&#x200B;**完成**&#x200B;以保存工作流模型。

**参数**

* `includeChildren`（布尔值，默认：`false`）。 false 表示仅发布路径。 true 表示子项也被发布。
* `replicateAsParticipant`（布尔值，默认：`false`）。 如果配置为 `true`，则复制操作将使用 `userid` 执行参与者步骤的主体。
* `enableVersion`（布尔值，默认： `true`）。 此参数可确定复制时是否创建了新版本。
* `agentId`（字符串值，默认表示仅使用发布代理）。 建议明确说明 agentId；例如，将其设置为值：发布。 将代理设置为 `preview` 将发布到预览服务
* `filters`（字符串值，默认表示激活所有路径）。 可用值包括：
   * `onlyActivated`  — 将仅激活标记为已激活的路径。
   * `onlyModified`  – 仅激活已激活且修改日期晚于激活日期的路径。
   * 上面可以用管道字符“|”进行“或”操作。 例如：`onlyActivated|onlyModified`。

**记录**

当树激活工作流步骤启动时，它将在“信息”日志级别记录其配置参数。 激活路径时，也会记录 INFO 语句。

在工作流步骤复制了所有路径后，将记录最终的 INFO 语句。

此外，您可以将以下的记录器的日志级别提高到`com.day.cq.wcm.workflow.process.impl`调试/跟踪以获取更多日志信息。

如果出现错误，工作流步骤以 `WorkflowException` 终止，它封装了基础异常。

在下面，您会找到在示例发布内容树工作流中生成的日志示例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**恢复支持**

该工作流会按块处理内容，每个块表示要发布的完整内容的子集。 如果系统出于任何原因停止了工作流，它将重新启动并处理尚未处理的块。 日志语句将声明内容已从特定路径中恢复。

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

如上例所示，在复制资源时，将仅使用默认处于活动状态的代理。 在 AEM as a Cloud Service 中，这将只是名为“发布”的代理，用于将作者连接到发布层。

为了支持预览功能，已添加名为“预览”的新代理，默认情况下该代理处于非活动状态。 此代理用于将作者连接到预览层。 如果只想通过预览代理复制，则需要通过 `AgentFilter`.

请参阅以下示例，了解如何执行此操作：

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

仅当复制操作包括至少一个默认处于活动状态的代理时，才会修改资源的整体`ReplicationStatus`。 在上例中，情况并非如此，因为复制只是使用“预览”代理。 因此，您需要使用 `getStatusForAgent()` 方法，用于查询特定代理的状态。 此方法也适用于“发布”代理。 如果已使用提供的代理完成任何复制操作，则返回非空值。

### 使内容失效的方法 {#invalidating-content}

您可以直接使内容失效，方法是使用作者的 Sling 内容失效 (SCD)（首选方法），或使用复制 API 调用发布调度程序刷新复制代理。 请参阅[缓存](/help/implementing/dispatcher/caching.md)页面以了解更多详细信息。

**复制 API 容量限制**

建议一次复制不到 100 个路径，其中 500 是硬限制。 超出硬限制，`ReplicationException` 将被抛出。
如果您的应用程序逻辑不需要原子复制，则可以通过设置 `ReplicationOptions.setUseAtomicCalls` 为 false，它将接受任意数量的路径，但在内部创建存储段以保持在此限制以下。

每次复制调用传输的内容大小不得超过 `10 MB`。 这包括节点和属性，但不包括任何二进制文件（工作流包和内容包被视为二进制文件）。


## 疑难解答 {#troubleshooting}

要对复制问题进行故障诊断，请导航到 AEM 创作服务 Web UI 中的复制队列：

1. 从 AEM 开始菜单导航到&#x200B;**工具 > 部署 > 分发**
2. 选择&#x200B;**发布**卡
   ![状态](assets/publish-status.png "状态")
3. 检查应为绿色的队列状态
4. 您可以测试与复制服务的连接
5. 选择&#x200B;**日志**&#x200B;选项卡，其中显示了内容发布的历史记录

![日志](assets/publish-logs.png "日志")

如果内容无法发布，则整个发布将从 AEM 发布服务中恢复。
在这种情况下，可编辑的主队列将显示红色状态，应该进行审核，以确定哪些项目导致取消发布。 通过单击该队列，将显示其待决项目，如果需要，可从中清除单个项目或所有项目。
