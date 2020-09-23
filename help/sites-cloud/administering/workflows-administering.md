---
title: 管理工作流实例
description: 了解如何管理工作流实例
translation-type: tm+mt
source-git-commit: c19079b1be36c4e87962491f263ddf97ab98f831
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---


# 管理工作流实例 {#administering-workflow-instances}

工作流控制台提供了多个用于管理工作流实例的工具，以确保它们按预期执行。

您可以使用各种控制台来管理工作流。 使用全 [局导航](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) 打开“工 **具”窗** 格 **，然后选择**&#x200B;工作流：

* **型号**:管理工作流定义
* **实例**:视图和管理正在运行的工作流实例
* **启动器**:管理工作流的启动方式
* **存档**:视图成功完成的工作流历史记录
* **失败**:视图已完成但有错误的工作流的历史记录
* **自动分配**:配置自动分配工作流到模板

## 监视工作流实例的状态 {#monitoring-the-status-of-workflow-instances}

1. 使用导航依次选 **择工**&#x200B;具、工 **作流**。
1. 选择 **实例** ，以显示当前正在进行的工作流实例的列表。

   ![wf-97](/help/sites-cloud/administering/assets/wf-97.png)


## 搜索工作流实例 {#search-workflow-instances}

1. 使用导航依次选 **择工**&#x200B;具、工 **作流**。
1. 选择 **实例** ，以显示当前正在进行的工作流实例的列表。 在顶部边栏的左角，选择 **过滤器**。 或者，您也可以使用按键alt+1。 此时将显示以下对话框：

   ![wf-99-1](/help/sites-cloud/administering/assets/wf-99-1.png)

1. 在筛选器对话框中，选择工作流搜索条件。 您可以根据以下输入进行搜索：

   * 有效负荷路径：选择特定路径
   * 工作流模型：选择工作流模型
   * 被分派人：选择工作流受分派人
   * 类型：任务、工作流项或工作流失败
   * 任务状态：活动、完成或终止
   * 我在哪里：所有者和被分派人，仅限所有者，仅限被分派人
   * 开始日期：开始日期在指定日期之前或之后
   * 结束日期：指定日期之前或之后的结束日期
   * 到期日期：到期日期在指定日期之前或之后
   * 更新日期：在指定日期之前或之后更新的日期

## 挂起、恢复和终止工作流实例 {#suspending-resuming-and-terminating-a-workflow-instance}

1. 使用导航依次选 **择工**&#x200B;具、工 **作流**。
1. 选择 **实例** ，以显示当前正在进行的工作流实例的列表。

   ![wf-96-1](/help/sites-cloud/administering/assets/wf-96-1.png)

1. 选择特定项目，然后根据 **需要使****用**“终止 **”、“暂**&#x200B;停”或“继续”;确认，和／或更多详细信息：

   ![wf-97-1](/help/sites-cloud/administering/assets/wf-97-1.png)

## 查看存档的工作流 {#viewing-archived-workflows}

1. 使用导航依次选 **择工**&#x200B;具、工 **作流**。

1. 选择 **“存档** ”以显示成功完成的工作流实例的列表。

   ![wf-98](/help/sites-cloud/administering/assets/wf-98.png)

   >[!NOTE]
   >中止状态被视为由于用户操作而发生的成功终止；例如：
   >
   >* 使用终止 **操作** 。
   >* 当受工作流约束的页面被（强制）删除时，工作流将终止


1. 选择特定项目，然后选择打 **开历史** ，以查看更多详细信息：

   ![wf-99](/help/sites-cloud/administering/assets/wf-99.png)

## 修复工作流实例失败 {#fixing-workflow-instance-failures}

当工作流失败时，AEM会 **提供** “失败”控制台，允许您在处理原始原因后调查并采取适当的操作：

* **失败详**&#x200B;细信息打开一个窗口以显示 
**故障消息**、 **步骤** 和 **故障堆栈**。

* **打开历史**&#x200B;记录显示工作流历史记录的详细信息。

* **重试步骤** 再次执行脚本步骤组件实例。 在修复了原始错误的原因后，使用“重试步骤”命令。 例如，在修复了执行进程步骤的脚本中的错误后，重试该步骤。
* **终止** 如果错误导致工作流无法协调的情况，则终止工作流。 例如，工作流可以依赖于环境条件，如存储库中对工作流实例不再有效的信息。
* **“终止并重试** ”与“ **终止** ”类似，不同之处在于新的工作流实例是使用原始有效负荷、标题和说明启动的。

要调查失败，然后在之后恢复或终止工作流，请执行以下步骤：

1. 使用导航依次选 **择工**&#x200B;具、工 **作流**。

1. 选择 **失败** ，以显示未成功完成的工作流实例的列表。
1. 选择特定项目，然后选择相应的操作：

   ![wf-47](/help/sites-cloud/administering/assets/wf-47.png)

## 定期清除工作流实例 {#regular-purging-of-workflow-instances}

最小化工作流实例数可提高工作流引擎的性能，因此您可以定期从存储库中清除已完成或正在运行的工作流实例。

配置 **AdobeGranite工作流清除配置** ，以根据工作流实例的年龄和状态清除工作流实例。 您还可以清除所有模型或特定模型的工作流实例。

您还可以创建服务的多个配置来清除满足不同标准的工作流实例。 例如，创建一个配置，当特定工作流模型的实例运行时间比预期时间长时清除这些实例。 创建另一个配置，该配置在特定天数后清除所有已完成的工作流，以最大限度地减小存储库的大小。

要配置服务，可以配置OSGi配置文件，请参阅 [OSGi配置文件](/help/implementing/deploying/configuring-osgi.md)。 下表说明了您对这两种方法都需要的属性。

>[!NOTE]
>要将配置添加到存储库，服务PID为：
>`com.adobe.granite.workflow.purge.Scheduler`
>由于服务是工厂服务，因此节点的名 `sling:OsgiConfig` 称需要一个标识符后缀，例如：
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>属性名称（Web控制台）</th>
   <th>OSGi属性名称</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>作业名称</td>
   <td>scheduledpurge.name</td>
   <td>计划清除的描述性名称。</td>
  </tr>
  <tr>
   <td>工作流状态</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>要清除的工作流实例的状态。 以下值有效：</p>
    <ul>
     <li>已完成：已完成的工作流实例将被清除。</li>
     <li>正在运行：正在运行的工作流实例将被清除。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>要清除的模型</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>要清除的工作流模型的ID。 ID是模型节点的路径，例如：<br /> /conf/global/settings/workflow/models/dam/update_asset/jcr:content/model<br /> 指定不值以清除所有工作流模型的实例。</p> <p>要指定多个模型，请单击Web控制台中的+按钮。 </p> </td>
  </tr>
  <tr>
   <td>工作流年龄</td>
   <td>scheduledpurge.daysold</td>
   <td>要清除的工作流实例的年龄（以天为单位）。</td>
  </tr>
 </tbody>
</table>

## 设置收件箱的最大大小 {#setting-the-maximum-size-of-the-inbox}

您可以通过配置AdobeGranite Workflow Service来设置收件箱 **的最大大小**，请 [参阅将OSGi配置添加到存储库](/help/implementing/deploying/configuring-osgi.md)。 下表介绍了您配置的属性。

>[!NOTE]
>要将配置添加到存储库，服务PID为：
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| 属性名称（Web控制台） | OSGi属性名称 |
|---|---|
| 最大收件箱查询大小 | granite.workflow.inboxQuerySize |

