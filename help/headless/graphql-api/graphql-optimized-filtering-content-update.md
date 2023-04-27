---
title: 更新内容片段以进行优化的 GraphQL 筛选
description: 了解如何在 Adobe Experience Manager as a Cloud Service 中更新内容片段以进行优化的 GraphQL 筛选，从而进行 Headless 内容投放。
exl-id: 211f079e-d129-4905-a56a-4fddc11551cc
source-git-commit: e18a60197aab3866b839ff7b923f1aa135c594cc
workflow-type: ht
source-wordcount: '738'
ht-degree: 100%

---

# 更新内容片段以进行优化的 GraphQL 筛选 {#updating-content-fragments-for-optimized-graphql-filtering}

要优化 GraphQL 筛选的性能，您需要运行一个程序来更新内容片段。

>[!NOTE]
>
>更新内容片段后，您可以按照以下建议进行操作来[优化 GraphQL 查询](/help/headless/graphql-api/graphql-optimization.md)。


## 前提条件 {#prerequisites}

确保您至少拥有 2023.1.0 版本的 AEM as a Cloud Service。

## 更新内容片段 {#updating-content-fragments}

要运行该程序，请执行以下步骤：

1. 使用 Cloud Manager UI 为实例设置以下变量来启用更新：

   ![Cloud Manager 环境配置](assets/cfm-graphql-update-01.png "Cloud Manager 环境配置")

   可用变量包括：

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名称</th>
      <th>值</th>
      <th>默认值</th>
      <th>服务</th>
      <th>已应用</th>
      <th>类型</th>
      <th>注释</th>
     </tr>
     <tr>
      <td>1</td>
      <td>`AEM_RELEASE_CHANNEL` </td>
      <td>`prerelease` </td>
      <td> </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>需要此变量来启用功能。 </td>
     </tr>
     <tr>
      <td>2</td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>Enables(!=0) 或 disables(0) 触发内容片段迁移作业。 </td>
     </tr>
     <tr>
      <td>3</td>
      <td>`CF_MIGRATION_ENFORCE` </td>
      <td>`1` </td>
      <td>`0` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>Enforce (!=0) 重新迁移内容片段。<br>将此标志设置为 0 会执行 CF 的增量迁移。这意味着，如果作业因任意原因终止，则作业的下一次运行将从它终止的位置开始迁移。请注意，建议强制执行第一次迁移 (value=1)。 </td>
     </tr>
     <tr>
      <td>4</td>
      <td>`CF_MIGRATION_BATCH` </td>
      <td>`50` </td>
      <td>`50` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>用于在迁移后保存内容片段数量的批次大小。<br>这与将在一个批次中保存到存储库的 CF 数量有关，并且可以用于优化对存储库的写入次数。 </td>
     </tr>
     <tr>
      <td>5</td>
      <td>`CF_MIGRATION_LIMIT` </td>
      <td>`1000` </td>
      <td>`1000` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>一次处理的内容片段的最大数目。<br>另请参阅 `CF_MIGRATION_INTERVAL` 的注释。 </td>
     </tr>
     <tr>
      <td>6</td>
      <td>`CF_MIGRATION_INTERVAL` </td>
      <td>`60` </td>
      <td>`600` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>处理剩余内容片段直到下一个限制的时间间隔（秒）<br>此时间间隔也被视为开始作业之前的等待时间，以及处理每个后续 CF_MIGRATION_LIMIT 个 CF 之间的延迟。<br>(*)</td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >(*)
   >
   >`CF_MIGRATION_INTERVAL` 的值还可以帮助估算迁移作业的总执行时间。
   >
   >例如：
   >
   >* 内容片段总数 = 20,000
   >* CF_MIGRATION_LIMIT = 1000
   >* CF_MIGRATION_INTERNAL = 60（秒）
   >* 完成迁移大约所需的时间 = 60 + (20,000/1000 * 60) = 1260 秒 = 21 分钟
   >  在开始时增加的额外“60”秒是因开始作业时的初始延迟导致的。
   >
   >您还应了解一点，这只是完成作业所需的&#x200B;*最少*&#x200B;时间，并且不包括 I/O 时间。实际花费的时间可能远远超过此估计值。

1. 监控更新的进度和完成情况。

   为此，请从以下位置监控有关 author 和 golden-publish 的日志：

   * `com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob`

      * Author 日志；例如：

         ```shell
         23.01.2023 13:13:45.926 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<dd9ffdc1-0c28-4d04-9a96-5d4d223e457e> is the leader, will schedule the upgrade schedule job.
         ...
         23.01.2023 13:13:45.941 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         
         23.01.2023 13:20:40.960 *INFO* [sling-threadpool-09cbdb47-4d99-4c4c-b6d5-781b635ee21b-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 6m, slingJobId: 2023/1/23/13/13/50e1a575-4cd7-497b-adf0-62cb5768eedb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```

      * Golden-publish 日志；例如：

         ```shell
         23.01.2023 12:35:05.150 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob This instance<ad1b399e-77be-408e-bc3f-57097498fddb> is the leader, will schedule the upgrade schedule job.
         
         23.01.2023 12:35:05.161 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Scheduling content fragments upgrade from version 0 to 1, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, enforce: true, limit: 1000, batch: 50, interval: 60s
         ...
         23.01.2023 12:40:45.180 *INFO* [sling-threadpool-8abcc1bb-cdcb-46d4-8565-942ad8a73209-(apache-sling-job-thread-pool)-1-Content Fragment Upgrade Job Queue Config(cfm/upgrader)] com.adobe.cq.dam.cfm.impl.upgrade.UpgradeJob Finished content fragments upgrade in 5m, slingJobId: 2023/1/23/12/34/ad1b399e-77be-408e-bc3f-57097498fddb_0, status: MaintenanceJobStatus{jobState=SUCCEEDED, statusMessage='Upgrade to version '1' succeeded.', errors=[], successCount=3781, failedCount=0, skippedCount=0}
         ```

1. 禁用更新程序。

   >[!IMPORTANT]
   >
   >需要执行此步骤才能完成升级。

   更新程序运行后，将云环境变量 `CF_MIGRATION_ENABLED` 重置为“0”以触发所有 pod 的回收。

   <table style="table-layout:auto">
    <tbody>
     <tr>
      <th> </th>
      <th>名称</th>
      <th>值</th>
      <th>默认值</th>
      <th>服务</th>
      <th>已应用</th>
      <th>类型</th>
      <th>注释</th>
     </tr>
     <tr>
      <td></td>
      <td>`CF_MIGRATION_ENABLED` </td>
      <td>`0` </td>
      <td>`0` </td>
      <td>所有 </td>
      <td> </td>
      <td>变量 </td>
      <td>Disables(0)（或 Enables(!=0)）触发内容片段迁移作业。 </td>
     </tr>
    </tbody>
   </table>

   >[!NOTE]
   >
   >这对于发布层特别重要，因为内容更新仅在 golden-publish 上进行，并且在回收 pod 时，所有正常的发布 pod 都基于 golden-publish。

1. 验证更新程序的完成情况。

   您可以使用 Cloud Manager 开发人员控制台中的存储库浏览器来检查内容片段数据，从而验证更新的成功完成情况。

   * 在第一次完整迁移之前，`cfGlobalVersion` 属性将不存在。
因此，JCR 节点 `/content/dam` 上此属性的值为 `1`，确认迁移完成情况。

   * 您也可以检查单个内容片段的以下属性：

      * `_strucVersion` 的值应为 `1`
      * `indexedData` 结构必须存在

      >[!NOTE]
      >
      >该程序将更新创作实例和发布实例上的内容片段。
      >
      >因此，建议通过存储库浏览器&#x200B;*至少*&#x200B;为一个创作实例&#x200B;*和*&#x200B;一个发布实例执行验证。


## 限制 {#limitations}

请注意以下限制：

* 只能在完全更新所有内容片段（由 JCR 节点 `/content/dam` 的 `cfGlobalVersion` 属性指示）后，才能优化 GraphQL 筛选器的性能

* 如果在运行更新过程后从包导入了内容片段（使用 `crx/de`），则直到再次执行更新过程后，才会在 GraphQL 查询结果中再次考虑这些内容片段。
