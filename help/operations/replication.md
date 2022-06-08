---
title: 复制
description: 分发和复制疑难解答。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 50754c886c92a121c5bb20449561694f8e42b0ac
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 4%

---

# 复制 {#replication}

Adobe Experience Manager as a Cloud Service使用 [Sling内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html) 将内容移动到要复制到在AEM运行时以外的Adobe I/O上运行的管道服务的功能。

>[!NOTE]
>
>读取 [分发](/help/overview/architecture.md#content-distribution) 以了解更多信息。

## 发布内容的方法 {#methods-of-publishing-content}

### 快速取消/发布 — 计划取消/发布 {#publish-unpublish}

这允许您立即发布选定的页面，而无需通过“管理发布”方法选择其他选项。

有关更多信息，请参阅 [管理发布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### 开启和关闭时间 — 触发器配置 {#on-and-off-times-trigger-configuration}

的 **开始时间** 和 **关闭时间** 可从 [页面属性的“基本”选项卡](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic).

要实现自动复制，您需要启用 **自动复制** 在 [OSGi配置](/help/implementing/deploying/configuring-osgi.md) **关闭触发器配置**:

![OSGi On Off触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 管理发布 {#manage-publication}

与“快速发布”相比，管理发布提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流，并且还提供了在以后的日期发布的选项。

为“稍后发布”选项包含文件夹的子项将调用发布内容树工作流，如本文所述。

您可以在 [发布基础知识文档](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication).

### 树激活 {#tree-activation}

>[!NOTE]
>
>此方法应视为已弃用，并将于2021年9月30日或之后删除，因为它不会保留状态，且与其他方法相比，其扩展能力较弱。 Adobe的建议是改用管理发布或工作流方法

要执行树激活，请执行以下操作：

1. 从AEM开始菜单导航到 **工具>部署>分发**
2. 选择卡 **发布**
3. 进入发布Web控制台UI后， **选择分发**

   ![分发](assets/publish-distribute.png "分发")
4. 在路径浏览器中选择路径，根据需要选择添加节点、树或删除，然后选择 **提交**

为获得最佳性能，在使用此功能时请遵循以下准则：
* 建议一次复制少于100个路径，且路径硬限制为500个。
* 复制内容的总大小必须低于10 MB。 这只包括节点和属性，但不包括任何二进制文件，它们包括工作流包和内容包。

### 发布内容树工作流程 {#publish-content-tree-workflow}

您可以通过选择 **工具 — 工作流 — 模型** 和复制 **发布内容树** 现成的工作流模型，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

请勿修改或调用原始模型。 相反，请确保首先复制模型，然后修改或调用该副本。

与所有工作流一样，也可以通过API调用。 有关更多信息，请参阅 [以编程方式与工作流交互](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem).

或者，您也可以通过创建使用 `Publish Content Tree` 流程步骤：

1. 从AEMas a Cloud Service主页，转到 **工具 — 工作流 — 模型**
1. 在“工作流模型”页面中，按 **创建** 在屏幕的右上角
1. 为模型添加标题和名称。 有关更多信息，请参阅 [创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. 从列表中选择新创建的模型，然后按 **编辑**
1. 在以下窗口中，将“流程步骤”(Process Step)拖放到当前模型流中：

   ![进程步骤](/help/operations/assets/processstep.png)

1. 单击流程中的“流程”步骤，然后选择 **配置** 按扳手图标
1. 单击 **进程** 选项卡，选择 `Publish Content Tree` 从下拉列表中

   ![树状激活](/help/operations/assets/newstep.png)

1. 在 **参数** 字段。 可以将多个以逗号分隔的参数字符串在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >有关参数列表，请参阅 **参数** 部分。

1. 按 **完成** 以保存工作流模型。

**参数**

* `includeChildren` (布尔值，默认值： `false`)。 false表示仅发布路径。 true表示子项也被发布。
* `replicateAsParticipant` (布尔值，默认值： `false`)。 如果配置为 `true`，则复制操作将使用 `userid` 执行参与者步骤的主体。
* `enableVersion` (布尔值，默认值： `true`)。 此参数可确定复制时是否创建了新版本。
* `agentId` （字符串值，默认值表示仅使用发布代理）。 建议明确说明agentId;例如，将其设置为值：发布。 将代理设置为 `preview` 将发布到预览服务
* `filters` （字符串值，默认表示激活所有路径）。 可用值包括：
   * `onlyActivated`  — 将只激活未标记为已激活的路径。
   * `onlyModified`  — 仅激活已激活且修改日期晚于激活日期的路径。
   * 上面可以用管道字符“|”进行OR。 例如， `onlyActivated|onlyModified`.

**记录**

当树激活工作流步骤启动时，它将在“信息”日志级别记录其配置参数。 激活路径时，也会记录INFO语句。

在工作流步骤复制了所有路径后，将记录最终的INFO语句。

此外，您还可以提高以下日志记录器的日志记录级别 `com.day.cq.wcm.workflow.process.impl` 调试/TRACE以获取更多日志信息。

如果出现错误，工作流步骤将终止，并 `WorkflowException`，该代码封装了基础Exception。

在下面，您会找到在示例发布内容树工作流中生成的日志示例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**恢复支持**

该工作流会按块处理内容，每个块表示要发布的完整内容的子集。 如果系统出于任何原因停止了工作流，它将重新启动并处理尚未处理的块。 日志语句将声明内容已从特定路径中恢复。

### 复制API {#replication-api}

您可以使用AEM as a Cloud Service中特有的复制API发布内容。

有关更多信息，请参阅 [API文档](https://javadoc.io/doc/com.adobe.aem/aem-sdk-api/latest/com/day/cq/replication/package-summary.html).

**API的基本用法**

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

如上例所示，在复制资源时，将仅使用默认处于活动状态的代理。 在AEMas a Cloud Service中，这将只是名为“publish”的代理，用于将作者连接到发布层。

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

整体 `ReplicationStatus` 仅当复制操作包括至少一个默认处于活动状态的代理时，才修改资源的。 在上例中，情况并非如此，因为复制只是使用“预览”代理。 因此，您需要使用 `getStatusForAgent()` 方法，用于查询特定代理的状态。 此方法也适用于“发布”代理。 如果已使用提供的代理完成任何复制操作，则返回非空值。


**复制API路径和大小限制**

建议复制的路径少于100个，其中500个是硬限制。 超出硬限制时，将引发ReplicationException。 如果您的应用程序逻辑不需要原子复制，则可以通过将ReplicationOptions.setUseAtomicCalls设置为false（将接受任意数量的路径，但在内部创建存储段以保持在此限制以下）来克服此限制。 每个复制调用传输的内容量不得超过10 MB，其中包含节点和属性，但不包含任何二进制文件（工作流包和内容包被视为二进制文件）。

## 疑难解答 {#troubleshooting}

要对复制问题进行故障诊断，请导航到AEM创作服务Web UI中的复制队列：

1. 从AEM开始菜单导航到 **工具>部署>分发**
2. 选择卡 **发布**
   ![状态](assets/publish-status.png "状态")
3. 检查应为绿色的队列状态
4. 您可以测试与复制服务的连接
5. 选择 **日志** 选项卡，其中显示了内容发布的历史记录

![日志](assets/publish-logs.png "日志")

如果内容无法发布，则整个发布将从AEM发布服务中恢复。
在这种情况下，可编辑的主队列将显示红色状态，应该进行审核，以确定哪些项目导致取消发布。 通过单击该队列，将显示其待决项目，如果需要，可从中清除单个项目或所有项目。
