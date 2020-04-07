---
title: AEM 云服务开发准则
description: '待完成 '
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# AEM 云服务开发准则 {#aem-as-a-cloud-service-development-guidelines}

作为云服务在AEM中运行的代码必须知道它始终在群集中运行。 这意味着始终有多个实例在运行。 该代码必须具有弹性，特别是当实例可能在任何时间点停止时。

在将AEM作为云服务进行更新期间，将会有新旧代码并行运行的实例。 因此，旧代码不能与新代码创建的内容断开，而新代码必须能够处理旧内容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要在群集中识别主设备，则可以使用Apache Sling Discovery API检测主设备。

## 内存中的状态 {#state-in-memory}

状态不得保留在内存中，而应保留在存储库中。 否则，如果实例停止，则此状态可能会丢失。

## 文件系统状态 {#state-on-the-filesystem}

在AEM中，实例的文件系统不应用作云服务。 盘片是短暂的，当实例被循环使用时，盘片将被丢弃。 对与处理单个请求相关的临时存储使用文件系统是可能的，但不应滥用于大型文件。 这是因为它可能会对资源使用配额产生负面影响，并且会遇到磁盘限制。

例如，不支持文件系统使用，发布层应确保需要持续保留的任何数据将发送到外部服务以进行长期存储。

## 观察 {#observation}

类似地，由于异步发生的一切都像在观测事件上行动一样，它无法保证在本地执行，因此必须谨慎使用。 JCR事件和Sling资源事件均是如此。 在发生变化时，该实例可被取下并由另一实例替换。 拓扑中当时处于活动状态的其他实例将能够对该事件做出响应。 但在这种情况下，这将不是地方事件，在事件颁布后，如果领导人选举正在进行，甚至可能没有积极的领导人。

## 后台任务和长时间运行的作业 {#background-tasks-and-long-running-jobs}

作为后台任务执行的代码必须假设它正在运行的实例可以随时关闭。 因此，代码必须具有弹性，且大多数导入都可恢复。 这意味着，如果代码重新执行，它不应从头开始再次开始，而是从离开位置更近。 虽然这不是此类代码的新要求，但在AEM中，作为云服务，更有可能发生实例撤消。

为了尽可能减少麻烦，应尽可能避免长时间的工作，而且至少应该恢复这些工作。 要执行此类作业，请使用Sling Jobs,Sling Jobs具有至少一次保证，因此如果它们中断，将尽快重新执行。 但他们可能不应该从头开始再次开始。 为了安排此类作业，最好使用 [Sling Jobs](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) 调度程序，这再次作为至少一次执行。

Sling Commons调度程序不应用于计划，因为无法保证执行。 只是，它更有可能被安排好。

同样，由于异步发生的一切，如根据观察事件(即JCR事件或Sling资源事件)，无法保证执行，因此必须谨慎使用。 目前的AEM部署已经如此。

## 传出HTTP连接 {#outgoing-http-connections}

强烈建议任何传出HTTP连接设置合理的连接和读取超时。 对于不应用这些超时的代码，在AEM上作为云服务运行的AEM实例将强制执行全局超时。 这些超时值对于连接调用为10秒，对于下列常用Java库使用的连接为60秒：

Adobe建议使用提供的 [Apache HttpComponents Client 4.x库进行HTTP连接](https://hc.apache.org/httpcomponents-client-ga/) 。

已知有效但可能需要自行提供依赖性的替代方案包括：

* [java.net.URL和](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) /或java.net.UR [LConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) （由AEM提供）
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建议使用，因为它已过时并由4.x版取代）
* [确定Http](https://square.github.io/okhttp/) （AEM未提供）

## 无经典UI自定义 {#no-classic-ui-customizations}

AEM作为云服务，仅支持第三方客户代码的触屏UI。 经典UI不可用于自定义。

## 避免本机二进制文件 {#avoid-native-binaries}

代码在运行时无法下载二进制文件，也无法修改它们。 例如，它将无法解压缩或解压 `jar` 缩文 `tar` 件。

## AEM作为云服务无流二进制文件 {#no-streaming-binaries}

应通过CDN访问二进制文件，CDN将在核心AEM服务之外提供二进制文件。

例如，请勿使用，这 `asset.getOriginal().getStream()`会触发将二进制文件下载到AEM服务的短暂磁盘上。

## 无反向复制代理 {#no-reverse-replication-agents}

AEM中不支持将“发布到作者”反向复制为云服务。 如果需要此类策略，您可以使用在Publish实例群（可能还有作者群集）之间共享的外部持久存储。

## 可能需要移植转发复制代理 {#forward-replication-agents}

内容通过pub-sub机制从“作者”复制到“发布”。 不支持自定义复制代理。

## 监视和调试 {#monitoring-and-debugging}

### 日志 {#logs}

对于本地开发，日志条目将写入文件夹中的本地 `/crx-quickstart/logs` 文件。

在Cloud环境中，开发人员可以通过Cloud Manager下载日志，或使用命令行工具跟踪日志。 <!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**设置日志级别**

要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后进行完全重新部署。 由于这不是即时的，因此请务必小心为收到大量流量的生产环境启用详细日志。 将来，可能会有一些机制来更快速地更改日志级别。

> [!NOTE]
> 
> 要执行下面列出的配置更改，您需要在本地开发环境上创建这些更改，然后将其作为云服务实例推送到AEM。 有关如何执行此操作的详细信息，请参 [阅将AEM部署为云服务](/help/implementing/deploying/overview.md)。

**激活调试日志级别**

默认日志级别为INFO，即DEBUG消息未记录。
要激活调试日志级别，请设置

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

要调试的属性。 不要将DEBUG日志级别的日志保留得比必需的时间长，因为它会生成大量日志。
调试文件中的一行通常与DEBUG开始，然后提供日志级别、安装程序操作和日志消息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作已失败。 安装将继续进行，但CRX的某部分安装不正确，将无法正常工作。 |
| 2 | 警告 | 该操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 该操作已成功。 |

### 线程转储 {#thread-dumps}

云环境上的线程转储会持续收集，但此时无法以自助方式下载。 同时，如果调试问题时需要线程转储，请与AEM支持部门联系，指定确切的时间窗口。

## CRX/DE Lite和系统控制台 {#crxde-lite-and-system-console}

### 本地开发 {#local-development}

对于本地开发，开发人员可以完全访问CRXDE Lite(`/crx/de`)和AEM Web控制台(`/system/console`)。

请注意，在本地开发（使用云就绪快速入门）中， `/apps``/libs` 可以直接写入，这与那些顶级文件夹不可变的云环境不同。

### AEM as a Cloud Service Development tools {#aem-as-a-cloud-service-development-tools}

客户可以在开发环境上访问CRXDE lite，但不能在舞台或生产上访问。 不可变的存储库(`/libs`, `/apps`)无法在运行时写入，因此尝试写入将导致错误。

开发人员控制台中提供了一组工具，用于将AEM作为云服务开发人员环境进行调试，以用于开发、暂存和生产环境。 可以通过按如下方式调整作者或发布服务URL来确定URL:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

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

### AEM Staging和Production Service {#aem-staging-and-production-service}

客户将无权访问用于分阶段和生产环境的开发人员工具。

### 性能监控 {#performance-monitoring}

Adobe监控应用程序性能并采取措施在出现恶化时予以解决。 目前，无法查看应用程序指标。