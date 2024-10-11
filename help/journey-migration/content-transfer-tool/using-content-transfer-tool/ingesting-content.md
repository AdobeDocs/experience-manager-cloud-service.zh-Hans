---
title: 将内容提取到云服务中
description: 了解如何使用Cloud Acceleration Manager将内容从迁移集引入目标Cloud Service实例。
exl-id: d8c81152-f05c-46a9-8dd6-842e5232b45e
feature: Migration
role: Admin
source-git-commit: 766573bfeb5190d212e87b18331e41820ddd3e32
workflow-type: tm+mt
source-wordcount: '3137'
ht-degree: 11%

---

# 将内容提取到云服务中 {#ingesting-content}

## Cloud Acceleration Manager 中的引入流程 {#ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion"
>title="内容引入"
>abstract="引入是指将内容从迁移集引入到目标 Cloud Service 实例中。内容传输工具具备支持差异内容增补的功能，借助该功能，您可以仅传输自上次内容传输活动以来所做的更改。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#top-up-extraction-process" text="增补提取"

请按照以下步骤使用Cloud Acceleration Manager摄取迁移集：

1. 转到Cloud Acceleration Manager。 单击项目信息卡，然后单击内容传输信息卡。 导航到&#x200B;**引入作业**&#x200B;并单击&#x200B;**新建引入**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-01.png)

1. 查看摄取核对清单，并确保已完成所有步骤。 要确保成功引入，必须执行以下步骤。 仅当清单完成时，才继续执行&#x200B;**下一步**&#x200B;步骤。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/Ingestion-checklist.png)

1. 提供创建引入所需的信息。

   * **迁移集：**&#x200B;选择包含提取数据的迁移集作为Source。
      * 迁移集将在长时间不活动后过期，因此预计摄取将在执行提取后不久进行。 有关详细信息，请查看[迁移集过期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)。

   >[!TIP]
   > 如果提取正在运行，则对话框将指示该情况。 成功完成提取后，摄取将自动开始。 如果提取失败或停止，则提取作业将撤销。

   * **目标：**&#x200B;选择目标环境。 在此环境中摄取迁移集的内容。
      * 摄取不支持快速开发环境(RDE)或预览类型的目标，并且即使用户有权访问，摄取也不会显示为可能的目标选择。
      * 虽然可将迁移集同时引入到多个目标中，但目标一次只能是一个正在运行或正在等待引入的目标。

   * **层：**&#x200B;选择该层。 (Author/Publish)。
      * 如果源是`Author`，则建议将其摄取到目标上的`Author`层。 同样，如果源为`Publish`，则目标也应是`Publish`。

   >[!NOTE]
   > 如果目标层是`Author`，则创作实例将在摄取期间关闭，并对用户（例如，作者或执行维护的任何人）不可用。 原因是为了保护系统，并防止任何可能丢失或导致引入冲突的更改。 确保您的团队了解此事实。 另请注意，环境在创作引入期间似乎处于休眠状态。

   * **擦除：**&#x200B;选择`Wipe`值
      * **划出**&#x200B;选项设置目标的引入起点。 如果启用了&#x200B;**划出**，则包含其所有内容的目标将重置为Cloud Manager中指定的AEM版本。 如果未启用，则目标会保持其当前内容作为起点。
      * 此选项&#x200B;**不**&#x200B;会影响内容摄取的执行方式。 摄取始终使用内容替换策略和&#x200B;_非_&#x200B;内容合并策略，因此在&#x200B;**擦除**&#x200B;和&#x200B;**非擦除**&#x200B;的情况下，摄取迁移集将覆盖目标上相同路径中的内容。 例如，如果迁移集包含`/content/page1`并且目标已包含`/content/page1/product1`，则引入操作将删除整个`page1`路径及其子页面（包括`product1`），并将其替换为迁移集中的内容。 这意味着，在对包含任何应维护的内容的目标执行&#x200B;**非划出**&#x200B;引入时，必须仔细规划。

   >[!IMPORTANT]
   > 如果为提取启用了&#x200B;**划出**&#x200B;设置，则会重置整个现有Cloud Service库，包括对目标存储库实例的用户权限。 对于添加到&#x200B;**管理员**&#x200B;组的管理员用户，此重置也为true，必须将该用户再次添加到管理员组才能开始引入。

   * **预复制：**&#x200B;选择`Pre-copy`值
      * 您可以运行可选的预复制步骤，以显着加快引入速度。 有关更多详细信息，请参阅[使用AzCopy摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#ingesting-azcopy)。
      * 如果使用预复制引入（对于S3或Azure数据存储），建议先单独运行`Author`引入。 这样可加快稍后运行的`Publish`引入速度。

   >[!IMPORTANT]
   > 仅当属于目标Cloud Service创作服务上的本地&#x200B;**AEM管理员**&#x200B;组时，才能启动到目标环境的引入。 如果无法开始引入，请参阅[无法开始引入](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#unable-to-start-ingestion)以了解更多详细信息。

1. 选择摄取选项后，将会显示其估计持续时间。 这是基于类似摄取的历史数据的最佳估计。

   * 此估算仅在提取的“检查大小”值已收集并且可用时才会计算并显示。
   * 该值是一个估计值，虽然可以智能计算，但不应视为精确值。 各种因素都会改变实际持续时间。
   * 在摄取运行时，此值还将在持续时间对话框中可用，可通过摄取的“**查看持续时间**”操作访问。

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_estimate"
>title="摄入持续时间估计"
>abstract="可以显示特定摄入的大致持续时间，以提供关于需要多长时间的一般概念。其准确性确实存在局限性。"

![图像](/help/journey-migration/content-transfer-tool/assets/estimate.png)

1. 单击&#x200B;**摄取**。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam22.png)

1. 然后，您可以从“摄取作业”列表视图中监视摄取，并使用摄取的操作菜单查看持续时间并记录摄取进度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23.png)

1. 单击行中的&#x200B;**(i)**&#x200B;按钮可了解有关引入作业的详细信息。 通过单击&#x200B;**...**，然后单击&#x200B;**查看持续时间**，可查看摄取操作运行或完成时每个步骤的持续时间。 该提取中的信息还显示出来，以实现所摄取的内容。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam23b.png)

## 增补引入 {#top-up-ingestion-process}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_topup"
>title="增补引入"
>abstract="使用增补功能移动自上次内容转移活动以来修改的内容。引入完毕后，检查日志中是否有任何错误或警告。应立即通过处理所报告的问题或联系 Adobe 客户服务而纠正任何错误。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/viewing-logs.html#" text="查看日志"

内容传输工具具备允许通过执行迁移集的&#x200B;*增补*&#x200B;来提取差异内容的功能。 这样可修改迁移集，使其仅包含自上次提取以来已更改的内容，而无需再次提取所有内容。

>[!NOTE]
>初始内容传输后，建议在Cloud Service上线之前，经常对差异内容进行增补，以缩短最终差异内容传输的内容冻结期。 如果您在第一次摄取中使用了预复制步骤，则可以跳过后续增补摄取的预复制（如果增补迁移集大小小于200 GB）。 原因是它可能会增加整个过程的时间。

要在完成某些提取后提取差异内容，必须运行[增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)，然后使用具有&#x200B;**划出**&#x200B;选项&#x200B;**禁用**&#x200B;的提取方法。 请务必阅读上面的&#x200B;**划出**&#x200B;说明，以避免丢失目标上已有的内容。

从创建引入作业开始，并确保在引入期间禁用了&#x200B;**划出**，如下所示：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam24.png)

## 疑难解答 {#troubleshooting}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_ingestion_troubleshooting"
>title="内容摄取故障排除"
>abstract="请参阅摄取日志和文档以查找针对摄取失败常见原因的解决方案并查找解决该问题的方法。修复后即可再次运行摄取。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html" text="验证内容转移"

### CAM无法检索迁移令牌 {#cam-unable-to-retrieve-the-migration-token}

自动检索迁移令牌可能由于其他原因而失败，包括您[在目标Cloud Service环境中通过Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)设置IP允许列表。 在这种情况下，当您尝试开始摄取时，您将看到以下对话框：

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/troubleshooting-token.png)

通过单击对话框中的“获取令牌”链接，手动检索迁移令牌。 此时将打开另一个显示令牌的选项卡。 然后，您可以复制令牌并将其粘贴到&#x200B;**迁移令牌输入**&#x200B;字段中。 现在，您应该能够开始引入。

>[!NOTE]
>
>该令牌可供属于目标Cloud Service创作服务上的本地&#x200B;**AEM管理员**&#x200B;组的用户使用。

### 无法开始引入 {#unable-to-start-ingestion}

仅当属于目标Cloud Service创作服务上的本地&#x200B;**AEM管理员**&#x200B;组时，才能启动到目标环境的引入。 如果您不属于AEM管理员组，则在尝试开始引入时会看到如下所示的错误。 您可以要求管理员将您添加到本地&#x200B;**AEM管理员**，也可以要求令牌本身，然后可以将它粘贴到&#x200B;**迁移令牌输入**&#x200B;字段中。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_nonadmin_ingestion.png)

### 无法访问迁移服务 {#unable-to-reach-migration-service}

请求引入后，可能会向用户显示如下消息：“无法访问目标环境中的迁移服务。 如果是这样的话，请稍后重试或与Adobe支持人员联系。”

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_cannot_reach_migser.png)

此消息表示Cloud Acceleration Manager无法访问目标环境的迁移服务以开始引入。 这种情况可能由于各种原因出现。

>[!NOTE]
> 
> 显示“迁移令牌”字段，因为在某些情况下，实际上不允许检索该令牌。 通过允许手动提供，它可让用户无需任何其他帮助即可快速开始引入。 如果提供了令牌，但仍显示消息，则检索令牌不是问题。

* AEM as a Cloud Service会维护环境状态，并且有时必须出于各种正常原因重新启动迁移服务。 如果该服务正在重新启动，则无法访问，但最终可用。
* 可能正在实例上运行另一个进程。 例如，如果[AEM版本更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)正在应用更新，则系统可能忙，并且迁移服务定期不可用。 完成此过程后，可以再次尝试开始引入。
* 列入允许列表如果已通过Cloud Manager应用[IP](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)，则会阻止Cloud Acceleration Manager访问迁移服务。 无法为摄取添加IP地址，因为其地址是动态的。 目前，唯一的解决方案是在摄取和索引过程中禁用IP允许列表。
* 可能有其他原因需要调查。 如果摄取或索引继续失败，请联系Adobe客户关怀部门。

### AEM版本更新和引入 {#aem-version-updates-and-ingestions}

[AEM版本更新](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/aem-version-updates.html)会自动应用于环境，以使其与最新的AEM as a Cloud Service版本保持同步。 如果在执行摄取时触发更新，则可能会导致不可预测的结果，包括环境损坏。

如果“AEM版本更新”已载入目标程序，则摄取进程会尝试在启动之前禁用其队列。 完成摄取后，版本更新程序状态将返回到摄取开始前的状态。

>[!NOTE]
>
> 不再需要记录支持票证即可禁用“AEM版本更新”。

如果“AEM版本更新”处于活动状态（即，更新正在运行或排队等待运行），则摄取将不会开始，并且用户界面会显示以下消息。 更新完成后，可以开始引入。 Cloud Manager可用于查看项目管道的当前状态。

>[!NOTE]
>
> “AEM版本更新”在环境的管道中运行，并等待管道清除完成。 如果更新排队的时间长于预期时间，请确保自定义工作流不会无意中锁定管道。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/error_releaseorchestrator_active.png)

### 因唯一性约束违规导致的追加数据引入失败 {#top-up-ingestion-failure-due-to-uniqueness-constraint-violation}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_uuid"
>title="违反唯一性约束"
>abstract="非擦除引入失败的常见原因是节点 ID 冲突。冲突节点只能存在一个。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加数据引入"

[增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)失败的常见原因是节点ID中存在冲突。 要识别此错误，请使用Cloud Acceleration Manager UI下载摄取日志，并查找如下条目：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakConstraint0030：唯一性约束违反了属性[jcr：uuid]，该属性的值为a1a1a1a1-b2b2-c3c3-d4d4-e5e5e5e5e5： /some/path/jcr：content， /some/other/path/jcr：content

AEM中的每个节点都必须具有一个唯一的uuid。 此错误表示正在摄取的节点具有与目标实例上不同路径中存在的节点相同的uuid。 发生这种情况有两个原因：

* 在提取和后续的[增补提取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/extracting-content.md#top-up-extraction-process)之间在源上移动节点
   * _记住_：对于增补提取，该节点仍将存在于迁移集中，即使它不再存在于源中。
* 目标上的节点会在摄取和后续增补摄取之间移动。

必须手动解决此冲突。 熟悉内容的用户必须确定必须删除这两个节点中的哪个节点，并牢记引用该节点的其他内容。 解决方案可能要求再次执行增补提取而不考虑违规节点。

### 无法删除引用节点导致追加数据引入失败 {#top-up-ingestion-failure-due-to-unable-to-delete-referenced-node}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_referenced_node"
>title="无法删除引用的节点"
>abstract="非擦除引入失败的常见原因是目标实例上特定节点的版本冲突。必须修复节点的版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html#top-up-ingestion-process" text="追加数据引入"

[增补摄取](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md#top-up-ingestion-process)失败的另一个常见原因是目标实例上特定节点的版本冲突。 要识别此错误，请使用Cloud Acceleration Manager UI下载摄取日志，并查找如下条目：

>java.lang.RuntimeException： org.apache.jackrabbit.oak.api.CommitFailedException： OakIntegrity0001：无法删除引用的节点：8a2289f4-b904-4bd0-8410-15e41e0976a8

如果在摄取和后续&#x200B;**非划出**&#x200B;摄取之间修改了目标上的节点，从而创建了新版本，则可能会发生这种情况。 如果在启用“包含版本”的情况下提取迁移集，则可能会发生冲突，因为目标现在具有版本历史记录和其他内容所引用的较新版本。 摄取进程无法删除违规版本节点，因为它已被引用。

解决方案可能要求再次执行增补提取而不考虑违规节点。 或者，创建一个包含违规节点的小型迁移集，但禁用“包含版本”。

最佳实践表明，如果必须使用包含版本的迁移集运行&#x200B;**非划出**&#x200B;引入，则在迁移历程完成之前，必须尽可能少地修改目标上的内容。 否则，可能会发生这些冲突。

### 由于节点属性值过大导致引入失败 {#ingestion-failure-due-to-large-node-property-values}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_bson"
>title="大节点属性"
>abstract="引入失败的常见原因是节点属性值超过了最大值。请遵循文档（包括与 BPA 报告相关的文档）来纠正这种情况。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html" text="迁移先决条件"

MongoDB中存储的节点属性值不能超过16 MB。 如果节点值超过支持的大小，摄取将失败，并且日志将包含以下任一值：

* 出现`BSONObjectTooLarge`错误并指定哪个节点超过了最大值，或者
* `BsonMaximumSizeExceededException`错误，表示节点可能包含超过最大大小**的unicode字符

这是MongoDB限制。

有关更多信息以及有助于查找所有大型节点的Oak工具链接，请参阅[内容传输工具先决条件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/prerequisites-content-transfer-tool.md)中的`Node property value in MongoDB`注释。 修复所有大小较大的节点后，再次运行提取和摄取。

要避免此限制，请在源AEM实例上运行[最佳实践分析器](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md)并查看它提供的结果，特别是[“不支持的存储库结构”(URS)](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/urs)模式。

>[!NOTE]
>
>[Best Practices Analyzer](/help/journey-migration/best-practices-analyzer/using-best-practices-analyzer.md) 2.1.50+版将报告包含超过最大大小的Unicode字符的大型节点。 请确保您运行的是最新版本。 低于2.1.50的BPA版本将不会识别和报告这些大型节点，并且需要使用上述先决条件Oak工具单独发现它们。

### 由于意外的间歇性错误导致摄取失败 {#ingestion-failure-due-to-unexpected-intermittent-errors}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_intermittent_errors"
>title="意外的间歇性错误"
>abstract="有时可能会发生意外的间歇性下游服务错误，不幸的是，唯一的解决办法是简单地重试引入。"

有时，意外的间歇性问题可能会导致摄取失败，很遗憾，唯一的解决办法是重试摄取。 调查摄取日志以找出失败的原因，并查看它是否与下面列出的任何错误一致，其中应尝试重试。

## MongoDB问题 {#mongo-db-issues}

* `Atlas prescale timeout error` — 摄取阶段将尝试将目标云数据库预缩放到与正在摄取的迁移集内容大小一致的合适大小。 在少数情况下，此操作未在预期时间范围内完成。
* `Exhausted mongo restore retries` — 尝试将引入的迁移集内容的本地转储恢复到云数据库的尝试已耗尽。 这表示MongoDB的整体运行状况/网络问题，该问题通常会在几分钟后自行修复。

### 引入已取消 {#ingestion-rescinded}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_ingestion_troubleshooting_rescinded"
>title="引入已取消"
>abstract="等待中的数据引入提取并未成功完成。引入操作已撤销，无法继续执行。"

使用正在运行的提取作为其源迁移集创建的摄取将耐心等待，直到提取成功，此时将正常开始。 如果提取失败或停止，则不会开始摄取及其索引作业，而是将取消摄取及其索引作业。 在这种情况下，请检查提取以确定其失败的原因，修复问题并重新开始提取。 运行固定提取后，可以计划新的引入。

### 重新运行引入后已删除的资源不存在

通常，不建议在两次引入之间修改云环境数据。

使用Assets触屏UI从Cloud Service目标中删除资源时，虽然会删除节点数据，但不会立即删除包含图像的资源blob。 它被标记为删除，因此不再出现在UI中；但是，它一直保留在数据存储中，直到发生垃圾收集并删除blob为止。

在删除以前迁移的资产，并在垃圾回收器完成删除资产之前运行下次摄取的情况下，摄取同一迁移集将不会恢复已删除的资产。 当摄取在云环境中检查资产时，没有节点数据；因此，摄取会将节点数据复制到云环境。 但是，当检查blob存储时，它会看到blob存在，并跳过对blob的复制。 这就是为什么当您从触屏UI查看资产时，元数据在摄取后出现，而图像却没有。 请记住，迁移集和内容摄取并非旨在处理这种情况。 他们的目标是向云环境添加新内容，而不是恢复以前迁移的内容。

## 后续内容 {#whats-next}

摄取成功后，AEM索引将自动开始。 有关详细信息，请参阅迁移内容后的[索引](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/indexing-content.md)。

完成将内容摄取到Cloud Service中后，您可以查看每个步骤（提取和摄取）的日志并查找错误。 有关详细信息，请参阅[查看迁移集的日志](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/viewing-logs.md)。
