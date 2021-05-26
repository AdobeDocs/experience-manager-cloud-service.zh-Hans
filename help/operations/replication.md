---
title: 复制
description: 分发 和复制故障排除。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 1ba960a930e180f4114f78607a3eb4bd5ec3edaf
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# 复制 {#replication}

Adobe Experience Manager as aCloud Service使用[Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html)功能将内容移动到在AEM运行时以外的Adobe I/O上运行的管道服务。

>[!NOTE]
>
>有关详细信息，请阅读[Distribution](/help/core-concepts/architecture.md#content-distribution)。

## 发布内容的方法{#methods-of-publishing-content}

### 快速取消/发布 — 计划取消/发布{#publish-unpublish}

作者的这些标准AEM功能不会随AEMCloud Service而发生更改。

### 开启和关闭时间 — 触发器配置{#on-and-off-times-trigger-configuration}

从“页面属性”的“基本”选项卡的“[”中，可以找到&#x200B;**开机时间**&#x200B;和&#x200B;**结束时间**&#x200B;的其他可能性。](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)

要实现自动复制，您需要在[OSGi配置](/help/implementing/deploying/configuring-osgi.md) **开关触发器配置**&#x200B;中启用&#x200B;**自动复制**:

![OSGi On Off触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 树激活{#tree-activation}

要执行树激活，请执行以下操作：

1. 从AEM开始菜单导航到&#x200B;**工具>部署>分发**
2. 选择卡&#x200B;**forwardPublisher**
3. 进入forwardPublisher Web控制台UI后，**选择Distribute**

   ![](assets/distribute.png "DistributeDistribute")
4. 在路径浏览器中选择路径，根据需要选择添加节点、树或删除，然后选择&#x200B;**Submit**

### 发布内容树工作流{#publish-content-tree-workflow}

您可以通过选择&#x200B;**工具 — 工作流 — 模型**&#x200B;并复制&#x200B;**发布内容树**&#x200B;现成工作流模型来触发树复制，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

请勿修改或调用原始模型。 相反，请确保首先复制模型，然后修改或调用该副本。

与所有工作流一样，也可以通过API调用。 有关更多信息，请参阅[以编程方式与工作流交互](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=en#extending-aem)。

或者，您也可以通过创建使用`Publish Content Tree`流程步骤的工作流模型来实现此目的：

1. 从AEM as aCloud Service主页，转到&#x200B;**工具 — 工作流 — 模型**
1. 在“工作流模型”页面中，按屏幕右上角的&#x200B;**创建**
1. 为模型添加标题和名称。 有关更多信息，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)
1. 从列表中选择新创建的模型，然后按&#x200B;**Edit**
1. 在以下窗口中，将“流程步骤”(Process Step)拖放到当前模型流中：

   ![进程步骤](/help/operations/assets/processstep.png)

1. 单击流程中的“处理”步骤，然后按扳手图标选择&#x200B;**配置**
1. 单击&#x200B;**Process**&#x200B;选项卡，然后从下拉列表中选择`Publish Content Tree`

   ![树状激活](/help/operations/assets/newstep.png)

1. 在&#x200B;**参数**&#x200B;字段中设置任何其他参数。 可以将多个以逗号分隔的参数字符串在一起。 例如：

   `enableVersion=true,agentId=publish`


   >[!NOTE]
   >
   >有关参数列表，请参阅下面的&#x200B;**Parameters**&#x200B;部分。

1. 按&#x200B;**Done**&#x200B;保存工作流模型。

**参数**

* `replicateAsParticipant` (布尔值，默认值： `false`)。如果配置为`true`，则复制将使用执行参与者步骤的主体的`userid`。
* `enableVersion` (布尔值，默认值： `true`)。此参数可确定复制时是否创建了新版本。
* `agentId` （字符串值，默认表示使用所有已启用的代理）。建议明确说明agentId;例如，将其设置为值：发布
* `filters` （字符串值，默认表示激活所有路径）。可用值包括：
   * `onlyActivated`  — 将只激活未标记为已激活的路径。
   * `onlyModified`  — 仅激活已激活且修改日期晚于激活日期的路径。
   * 上面可以用管道字符“|”进行OR。 例如，`onlyActivated|onlyModified`。

**记录**

当树激活工作流步骤启动时，它将在“信息”日志级别记录其配置参数。 激活路径时，也会记录INFO语句。

在工作流步骤复制了所有路径后，将记录最终的INFO语句。

此外，您还可以将`com.day.cq.wcm.workflow.process.impl`以下日志记录器的日志级别增加到DEBUG/TRACE，以获取更多日志信息。

如果出现错误，工作流步骤将以`WorkflowException`终止，该步骤将包含基础Exception。

在下面，您会找到在示例发布内容树工作流中生成的日志示例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**恢复支持**

该工作流会按块处理内容，每个块表示要发布的完整内容的子集。 如果系统出于任何原因停止了工作流，它将重新启动并处理尚未处理的块。 日志语句将声明内容已从特定路径中恢复。

## 疑难解答 {#troubleshooting}

要对复制问题进行故障诊断，请导航到AEM创作服务Web UI中的复制队列：

1. 从AEM开始菜单导航到&#x200B;**工具>部署>分发**
2. 选择卡&#x200B;**forwardPublisher**
   ![](assets/status.png "StatusStatus")
3. 检查应为绿色的队列状态
4. 您可以测试与复制服务的连接
5. 选择&#x200B;**日志**&#x200B;选项卡，以显示内容发布的历史记录

![](assets/logs.png "LogsLogs")

如果内容无法发布，则整个发布将从AEM发布服务中恢复。
在这种情况下，应审查队列，以确定哪些项目导致取消发布。 通过单击显示红色状态的队列，将显示具有待处理项目的队列，如果需要，可从该队列中清除单个或所有项目。
