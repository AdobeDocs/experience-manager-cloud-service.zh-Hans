---
title: AEM as a Cloud Service 中的维护任务
description: AEM as a Cloud Service 中的维护任务
exl-id: 5b114f94-be6e-4db4-bad3-d832e4e5a412
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 63%

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
>Adobe保留覆盖客户的维护任务配置设置的权利，以缓解性能下降等问题。

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
    <td>对于现有环境（即2023年6月1日之前创建的环境），清除功能处于禁用状态，并且将来不会启用，除非客户明确启用此功能，届时，他们还可以使用自定义值来配置此功能。<br><br> <!--Alexandru: leave the two line breaks in place, otherwise spacing won't render properly-->新环境（从2023年6月1日开始创建的环境）默认情况下将使用以下值启用清除，客户可以使用自定义值配置。
     <ol>
       <li>超过 30 天的版本将会被删除</li>
       <li>保留过去 30 天内的最新 5 个版本</li>
       <li>无论上述规则如何，都会保留最新版本。</li>
       <br>建议有法规要求的客户将站点页面完全按照特定日期显示，并与专门的外部服务集成。
     </ol></td>
  </td>
  </tr>
  <tr>
    <td>审核日志清除</td>
    <td>Adobe</td>
    <td>对于现有环境（即2023年6月1日之前创建的环境），清除功能处于禁用状态，并且将来不会启用，除非客户明确启用此功能，届时，他们还可以使用自定义值来配置此功能。<br><br> <!-- See above for the two line breaks -->新环境（从2023年6月1日开始创建的环境）将默认启用 <code>/content</code> 节点，具体情况如下：
     <ol>
       <li>对于复制审核，将删除超过 3 天的审核日志</li>
       <li>对于 DAM (Assets)，将删除超过 30 天的审核日志</li>
       <li>对于页面审核，将删除超过 3 天的日志。</li>
       <br>建议有法规要求的客户制作不可编辑的审核日志，并与专门的外部服务集成。
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
    <p>必须在 git 中完成。覆盖下的开箱即用维护窗口配置节点 <code>/libs</code> 方法是在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>.</p>
    <p>有关其他配置详细信息，请参阅下面的维护窗口表。通过在上述节点下添加另一个节点来启用维护任务。 将其命名 <code>granite_TaskPurgeTask</code>，具有属性 <code>sling:resourceType</code> 设置为 <code>granite/operations/components/maintenance/task</code> 和属性 <code>granite.maintenance.name</code> 设置为 <code>TaskPurge</code>. 配置OSGI属性，请参见 <code>com.adobe.granite.taskmanagement.impl.purge.TaskPurgeMaintenanceTask</code> 属性列表。</p>
  </td>
  </tr>
    <tr>
    <td>工作流清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。覆盖下的开箱即用维护窗口配置节点 <code>/libs</code> 方法是在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_WorkflowPurgeTask</code>），启用维护任务。配置 OSGI 属性，请参见<a href="https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/workflows-administering.html#regular-purging-of-workflow-instances"> AEM 6.5 维护任务文档</a>。</p>
  </td>
  </tr>
  <tr>
    <td>项目清除</td>
    <td>客户</td>
    <td>
    <p>必须在 git 中完成。覆盖下的开箱即用维护窗口配置节点 <code>/libs</code> 方法是在文件夹下创建属性 <code>/apps/settings/granite/operations/maintenance/granite_weekly</code>， <code>granite_daily</code> 或 <code>granite_monthly</code>. 有关其他配置详细信息，请参阅下面的维护窗口表。</p>
    <p>通过在上面的节点下添加另一个具有适当属性的节点（将其命名为 <code>granite_ProjectPurgeTask</code>），启用维护任务。请参阅“Adobe项目清除配置”下的OSGI属性列表。</p>
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
    <p><strong>windowScheduleWeekdays =由1-7中的两个值组成的数组（例如，[5,5]）</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    </td>
  </tr>
  <tr>
    <td>每月</td>
    <td>客户</td>
    <td>JCR 节点定义</td>
    <td>
    <p><strong>windowSchedule=每月</strong> （此值不应更改）</p>
    <p><strong>windowStartTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务应何时开始执行。</p>
    <p><strong>windowEndTime=HH:MM</strong> 用作 24 小时时钟。定义与每月维护窗口关联的维护任务在尚未完成时应何时停止执行。</p>
    <p>在此时间范围内，维护任务不能执行多次。</p>
    <p><strong>windowScheduleWeekdays =由1-7中的两个值组成的数组（例如，[5,5]）</strong> 数组的第一个值是计划作业的开始日期，第二个值是停止作业的结束日期。 开始和结束的确切时间分别由 windowStartTime 和 windowEndTime 控制。</p>
    <p><strong>windowFirstLastStartDay= 0/1</strong> 0 表示安排在每月的第一周，或 1 表示安排在每月最后一周。如果没有值，则实际上会将作业调度在受windowScheduleWeekdays控制的日期（每月）。</p>
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
