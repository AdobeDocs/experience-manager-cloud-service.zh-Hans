---
title: 复制
description: 散佈和疑難排解復寫。
exl-id: c84b4d29-d656-480a-a03a-fbeea16db4cd
source-git-commit: 91a13f8b23136298e0ccf494e51fccf94fa1e0b4
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 46%

---

# 复制 {#replication}

Adobe Experience Manager as a Cloud Service使用 [Sling內容發佈](https://sling.apache.org/documentation/bundles/content-distribution.html) 將內容移動到復寫至AEM執行階段以外的Adobe Developer上執行的管道服務的功能。

>[!NOTE]
>
>阅读[分发](/help/overview/architecture.md#content-distribution)以了解更多信息。

## 发布内容的方法 {#methods-of-publishing-content}

>[!NOTE]
>
>如果您有興趣大量發佈內容，請使用 [發佈內容樹狀工作流程](#publish-content-tree-workflow).
>此工作流程步驟是專為Cloud Service而建置，可有效處理大型裝載。
>不建議建置您自己的大量發佈自訂程式碼。
>如果您因任何原因必須自訂，則可以使用現有的工作流程API來觸發此工作流程/工作流程步驟。
>只發佈必須發佈的內容永遠都是不錯的做法。 如果不需要的話，也請謹慎行事，不要嘗試發佈大量內容。 不過，您可以透過發佈內容樹狀工作流程傳送多少內容並無限制。

### 快速取消/发布 – 计划取消/发布 {#publish-unpublish}

此功能可讓您立即發佈所選頁面，而不需透過「管理發布」方法額外選擇選項。

有关更多信息，请参阅[管理发布](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)。

### 开启和关闭时间 – 触发器配置 {#on-and-off-times-trigger-configuration}

**开始时间**&#x200B;和&#x200B;**关闭时间**&#x200B;的附加可能性可从[页面属性的“基本”选项卡](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)获得。

若要為此功能實現自動複製，請啟用 **自動復寫** 在 [OSGi設定](/help/implementing/deploying/configuring-osgi.md) **開啟關閉觸發器設定**：

![OSGi 开启关闭触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 管理发布 {#manage-publication}

「管理發布」比「快速發佈」提供更多的選項，允許包含子頁面、自訂參照和啟動任何適用的工作流程，並提供稍後發佈的選項。

為「稍後發佈」選項包含資料夾的子項時，會叫用發佈內容樹狀工作流程，如本文所述。

您可以[在出版基础文档](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#manage-publication)中找到有关管理出版的更多详细信息。

### 发布内容树工作流程 {#publish-content-tree-workflow}

您可以通过选择&#x200B;**工具 – 工作流 – 模型**&#x200B;和复制&#x200B;**发布内容树**&#x200B;现成的工作流模型，如下所示：

![](/help/operations/assets/publishcontenttreeworkflow.png)

请勿修改或调用原始模型。 相反，请确保首先复制模型，然后修改或调用该副本。

与所有工作流一样，也可以通过 API 调用。 如需詳細資訊，請參閱 [以程式設計方式與工作流程互動](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-program-interaction.html?lang=zh-Hans#extending-aem).

或者，您也可以建立工作流程模型，此模型使用 `Publish Content Tree` 程式步驟：

1. 从 AEM as a Cloud Service 主页，转到&#x200B;**工具 – 工作流 – 模型**.
1. 在“工作流模型”页面中，按屏幕右上角的&#x200B;**创建.**
1. 为模型添加标题和名称。 有关更多信息，请参阅[创建工作流模型](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/workflows-models.html)。
1. 从列表中选择新创建的模型，然后按&#x200B;**编辑**
1. 在以下窗口中，将“流程步骤”拖放到当前模型流中：

   ![流程步骤](/help/operations/assets/processstep.png)

1. 選取流程中的「處理」步驟，然後選取 **設定** 按一下扳手圖示。
1. 選取 **程式** 標籤並選取 `Publish Content Tree` 從下拉式清單中，然後檢查 **處理常式前進** 核取方塊

   ![树激活](/help/operations/assets/newstep.png)

1. 在&#x200B;**参数**&#x200B;字段中设置任何附加参数。 多個以逗號分隔的引數可串連在一起。 例如：

   `enableVersion=true,agentId=publish,includeChildren=true`


   >[!NOTE]
   >
   >有关参数列表，请参阅&#x200B;**参数**&#x200B;部分。

1. 按&#x200B;**完成**&#x200B;以保存工作流模型。

**参数**

* `includeChildren`（布尔值，默认：`false`）。 值 `false` 表示只會發佈路徑； `true` 表示也會發佈子項。
* `replicateAsParticipant`（布尔值，默认：`false`）。 如果配置为 `true`，则复制操作将使用 `userid` 执行参与者步骤的主体。
* `enableVersion`（布尔值，默认： `true`）。 此参数可确定复制时是否创建了新版本。
* `agentId`（字符串值，默认表示仅使用发布代理）。 建议明确说明 agentId；例如，将其设置为值：发布。 將代理程式設定為 `preview` 發佈至預覽服務。
* `filters` （字串值，預設值代表所有路徑都已啟動）。 可用值包括：
   * `onlyActivated`  — 僅啟動（已）已啟動的頁面。 作為重新啟用的一種形式。
   * `onlyModified`  – 仅激活已激活且修改日期晚于激活日期的路径。
   * 上面可以用管道字符“|”进行“或”操作。 例如：`onlyActivated|onlyModified`。

**记录**

樹狀結構啟動工作流程步驟啟動時，會在INFO記錄層級上記錄其設定引數。 激活路径时，也会记录 INFO 语句。

在工作流程步驟已複製所有路徑之後，會記錄最終的INFO陳述式。

此外，您也可以增加以下記錄器的記錄層級 `com.day.cq.wcm.workflow.process.impl` 偵錯/TRACE以取得更多記錄資訊。

如果有錯誤，工作流程步驟會以 `WorkflowException`，會包裝基礎的例外狀況。

以下是在範例發佈內容樹狀工作流程期間產生的記錄範例：

```
21.04.2021 19:14:55.566 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.treeactivation.TreeActivationWorkflowProcess TreeActivation options: replicateAsParticipant=false(userid=workflow-process-service), agentId=publish, chunkSize=100, filter=, enableVersion=false
```

```
21.04.2021 19:14:58.541 [cm-p123-e456-aem-author-797aaaf-wkkqt] *INFO* [JobHandler: /var/workflow/instances/server60/2021-04-20/brian-tree-replication-test-2_1:/content/wknd/us/en/adventures] com.day.cq.wcm.workflow.process.impl.ChunkedReplicator closing chunkedReplication-VolatileWorkItem_node1_var_workflow_instances_server60_2021-04-20_brian-tree-replication-test-2_1, 17 paths replicated in 2971 ms
```

**恢复支持**

该工作流会按块处理内容，每个块表示要发布的完整内容的子集。 如果系統停止工作流程，它會重新啟動並處理尚未處理的區塊。 記錄陳述式指出內容已從特定路徑恢復。

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

如上例所示，複製資源時，只會使用預設為作用中的代理程式。 在AEMas a Cloud Service中，這僅代表稱為「發佈」的代理程式，此代理程式會將作者連線到發佈層級。

为了支持预览功能，已添加名为“预览”的新代理，默认情况下该代理处于非活动状态。 此代理用于将作者连接到预览层。 如果您只想透過預覽代理程式進行復寫，您必須透過 `AgentFilter`.

請參閱下列範例：

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

仅当复制操作包括至少一个默认处于活动状态的代理时，才会修改资源的整体`ReplicationStatus`。 在上述範例中，此流程並不適用。 復寫只是使用「預覽」代理程式。 因此，您必須使用 `getStatusForAgent()` 方法，允許查詢特定代理程式的狀態。 此方法也适用于“发布”代理。 如果已使用提供的代理完成任何复制操作，则返回非空值。

### 使内容失效的方法 {#invalidating-content}

您可以使用作者的Sling內容失效(SCD) （偏好方法）或使用復寫API叫用發佈Dispatcher Flush復寫代理程式，直接讓內容失效。 请参阅[缓存](/help/implementing/dispatcher/caching.md)页面以了解更多详细信息。

**复制 API 容量限制**

一次復寫少於100個路徑，以500為上限。 超過限制，a `ReplicationException` 擲回。
如果您的應用程式邏輯不需要原子複製，可透過設定 `ReplicationOptions.setUseAtomicCalls` 為false，可接受任何數量的路徑，但在內部建立貯體以保持在此限制以下。

每次复制调用传输的内容大小不得超过 `10 MB`。 此規則包含節點和屬性，但不包含任何二進位檔（工作流程套件和內容套件被視為二進位檔）。


## 疑难解答 {#troubleshooting}

要对复制问题进行故障诊断，请导航到 AEM 创作服务 Web UI 中的复制队列：

1. 從AEM「開始」功能表，瀏覽至 **「工具」>「部署」>「發佈」**
2. 选择&#x200B;**发布**卡
   ![状态](assets/publish-status.png "状态")
3. 检查应为绿色的队列状态
4. 您可以测试与复制服务的连接
5. 选择&#x200B;**日志**&#x200B;选项卡，其中显示了内容发布的历史记录

![日志](assets/publish-logs.png "日志")

如果内容无法发布，则整个发布将从 AEM 发布服务中恢复。
在這種情況下，可編輯的主要佇列會顯示紅色狀態，並應加以檢閱以識別哪些專案導致取消發佈。 按一下該佇列會顯示其暫止專案，視需要可從中清除單一專案或所有專案。
