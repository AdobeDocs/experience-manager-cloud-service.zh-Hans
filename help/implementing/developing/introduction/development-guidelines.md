---
title: AEM作为云服务开发准则
description: '待完成 '
translation-type: tm+mt
source-git-commit: cedc14b0d71431988238d6cb4256936a5ceb759b

---


# AEM作为云服务开发准则 {#aem-as-a-cloud-service-development-guidelines}

## 后台任务和长时间运行的作业 {#background-tasks-and-long-running-jobs}

作为后台任务执行的代码必须假设它正在运行的实例可以随时关闭。 因此，代码必须具有弹性，且大多数导入都可恢复。 这意味着，如果重新执行代码，它不应从头开始，而应从离开位置更近。 虽然这不是此类代码的新要求，但在AEM中，作为云服务，更有可能发生实例撤消。

为了尽可能减少麻烦，应尽可能避免长时间的工作，而且至少应该恢复这些工作。 要执行此类作业，请使用Sling Jobs,Sling Jobs具有至少一次保证，因此如果它们中断，将尽快重新执行。 但它们可能不应该从头开始。 为了调度此类作业，最好使用 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) （作业调度程序），这样至少执行一次。

Sling Commons Scheduler不应用于调度，因为执行无法保证。 只是，它更有可能被安排好。

同样，由于异步发生的一切，如对观测事件（即JCR事件或Sling资源事件）采取行动，无法保证执行，因此必须谨慎使用。 目前的AEM部署已经如此。

## 传出HTTP连接 {#outgoing-http-connections}

强烈建议任何传出HTTP连接设置合理的连接和读取超时。 对于不应用这些超时的代码，在AEM上作为云服务运行的AEM实例将强制执行全局超时。 这些超时值对于连接调用为10秒，对于下列常用Java库使用的连接为60秒：

Adobe建议使用提供的 [Apache httpComponents Client 4.x库进行HTTP连接](https://hc.apache.org/httpcomponents-client-ga/) 。

已知有效但可能需要自行提供依赖性的替代方案包括：

* [java.net.URL和](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) /或java.net.UR [LConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （由AEM提供）
* [Apache Commons httpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建议使用，因为它已过时并由4.x版取代）
* [OK Http](OK Http（AEM未提供）)（AEM未提供）

## 监视和调试 {#monitoring-and-debugging}

### 日志 {#logs}

* 对于本地开发，日志条目将写入本地文件
   * `./crx-quickstart/logs`
* 在云环境中，开发人员可以通过Cloud manager下载日志，或使用命令行工具跟踪日志。 <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->
* 要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后完全重新部署。 由于这不是即时的，因此请务必小心在收到大量流量的生产环境中启用详细日志。 将来，可能会有一些机制来更快速地更改日志级别。

### 线程转储 {#thread-dumps}

云环境中的线程转储会持续收集，但此时无法以自助方式下载。 同时，如果调试问题时需要线程转储，请与AEM支持部门联系，指定确切的时间窗口。

### CRX/DE Lite和系统控制台 {#crxde-lite-and-system-console}

## 本地开发 {#local-development}

对于本地开发，开发人员可以完全访问CRXDE Lite(`/crx/de`)和AEM web控制台(`/system/console`)。

请注意，在本地开发（使用云就绪快速入门）中， `/apps``/libs` 可以直接写入，这与那些顶级文件夹不可变的云环境不同。

## AEM作为云服务开发工具 {#aem-as-a-cloud-service-development-tools}

客户可以在开发环境中访问CRXDE lite，但不能在舞台或生产环境中访问。 不可变的存储库(`/libs`, `/apps`)无法在运行时写入，因此尝试写入将导致错误。

开发人员控制台中提供了一组工具，用于将AEM作为云服务开发人员环境进行调试，以用于开发、暂存和生产环境。 可以通过按如下方式调整作者或发布服务URL来确定URL:

`https://dev-console>-<namespace>.<cluster>.dev.adobeaemcloud.com`

作为快捷方式，可以使用以下Cloud Manager CLI命令根据下面描述的环境参数启动开发人员控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

有关 [详细信息](/help/release-notes/home.md) ，请参阅此页。

开发人员可以生成状态信息并解析各种资源。

如下图所示，可用状态信息包括捆绑、组件、OSGI配置、Oak索引、OSGI服务和Sling作业的状态。

![Dev Console 1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下图所示，开发人员可以解析包依赖关系和Servlet:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，开发人员控制台还有一个指向“解释查询”工具的链接，该链接对于调试也很有用：

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

**AEM Staging和Production Service**

客户将无权访问用于暂存和生产环境的开发人员工具集。

### 诊断 {#diagnostics}

系统控制台可用于开发环境。 但是，暂存和生产的诊断转储不可用。