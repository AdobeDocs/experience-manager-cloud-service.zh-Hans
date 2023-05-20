---
title: AEM as a Cloud Service 中的维护任务
description: AEM as a Cloud Service 中的维护任务
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: d4d1e97df58f8bd0951f0d5b0bf46e118b163457
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 65%

---

# AEM as a Cloud Service 中的维护任务 {#maintenance-tasks-in-aem-as-a-cloud-service}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_maintenance"
>title="维护任务"
>abstract="维护任务是按计划运行以优化存储库的过程。使用 AEM as a Cloud Service 会大幅减小客户配置维护任务操作属性的需求。 客户可以将资源集中在应用程序级别的问题上，而 Adobe 则会处理基础设施方面的操作。"

维护任务是按计划运行以优化存储库的过程。使用 AEM as a Cloud Service 会大幅减小客户配置维护任务操作属性的需求。 客户可以将资源集中在应用程序级别的问题上，而 Adobe 则会处理基础设施方面的操作。

## 配置维护任务 {#maintenance-tasks-configuring}

在早期版本的 AEM 中，您可以使用维护卡（“工具”>“操作”>“维护”）配置维护任务。对于 AEM as a Cloud Service，维护卡不再可用，因此应由源控件管理配置，并使用云管理器进行部署。Adobe 管理那些具有客户无法配置的设置的维护任务（例如，数据存储垃圾收集、审核日志清除、版本清除）。其他维护任务可由客户配置，如下表所述。

>[!CAUTION]
>
>Adobe 保留覆盖客户维护任务配置设置的权利，以缓解性能下降等问题。

下表说明了 AEM as a Cloud Service 发布时存在的维护任务。

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
    <td>Adobe</td>
    <td>對於現有環境（在2023年6月1日之前建立的環境），清除功能會停用，且日後不會啟用，除非客戶明確啟用，且客戶當時可能也會使用自訂值設定該功能。<br><br> <!--Alexandru: please leave the two line breaks in place, otherwise spacing won't render properly-->新環境（自2023年6月1日起建立的環境）預設會啟用永久刪除，使用下列值，客戶可設定自訂值。
     <ol>
       <li>超过 30 天的版本将会被删除</li>
       <li>保留过去 30 天内的最新 5 个版本</li>
       <li>无论上述规则如何，都会保留最新版本。</li>
       <br>建議有法規要求的客戶將網站頁面完全依照特定日期顯示，並整合專門的外部服務。
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>审核日志清除</td>
    <td>Adobe</td>
    <td>對於現有環境（在2023年6月1日之前建立的環境），清除功能會停用，且日後不會啟用，除非客戶明確啟用，且客戶當時可能也會使用自訂值設定該功能。<br><br> <!-- See above for the two line breaks -->新環境（自2023年6月1日起建立的環境）將預設啟用以下項的清除： <code>/content</code> 存放庫的節點，根據下列行為：
     <ol>
       <li>对于复制审核，将删除超过 3 天的审核日志</li>
       <li>对于 DAM (Assets)，将删除超过 30 天的审核日志</li>
       <li>对于页面审核，将删除超过 3 天的日志。</li>
       <br>建議有法規要求的客戶製作無法編輯的稽核記錄，並與專門的外部服務整合。
     </ol></td>
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
    <p>必须在 git 中完成。覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>.</p>
    <p>有关其他配置详细信息，请参阅下面的维护窗口表。在上面的節點底下新增另一個節點，以啟用維護任務。 將其命名 <code>granite_TaskPurgeTask</code>，具有屬性 <code>sling:resourceType</code> 設定為 <code>granite/operations/components/maintenance/task</code> 和屬性 <code>granite.maintenance.name</code> 設定為 <code>TaskPurge</code>. 設定OSGI屬性，請參閱 <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> 屬性清單。</p>
  </td>
  </tr>
    <tr>
    <td>工作流清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_WorkflowPurgeTask</code>），启用维护任务。配置 OSGI 属性，请参见<a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances"> AEM 6.5 维护任务文档</a>。</p>
  </td>
  </tr>
  <tr>
    <td>项目清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。覆寫下的現成維護視窗設定節點 <code>/libs</code> 在資料夾下建立屬性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_ProjectPurgeTask</code>），启用维护任务。請參閱「Adobe專案清除設定」底下的OSGI屬性清單。</p>
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
  <p>在此時間範圍內，維護任務不能執行超過一次。</p>
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
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =由1-7 （例如[5,5]）中的2個值組成的陣列</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR 节点定义</td>
    <td>
    <p><strong>windowSchedule=每月</strong> （此值不應變更）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务在尚未完成时应何时停止执行。</p>
    <p>在此時間範圍內，維護任務不能執行超過一次。</p>
    <p><strong>windowScheduleWeekdays =由1-7 （例如[5,5]）中的2個值組成的陣列</strong> 陣列的第一個值是排程工作的開始日期，第二個值是停止工作的結束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 表示安排在每月的第一周，或 1 表示安排在每月最后一周。若沒有值，則會有效地將工作排程在windowScheduleWeekdays所管轄的日期（每月）。</p>
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
