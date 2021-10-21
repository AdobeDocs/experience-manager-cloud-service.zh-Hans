---
title: AEM as a Cloud Service 开发准则
description: AEM as a Cloud Service 开发准则
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: 333ebbed52577a82eb9b65b20a173e4e65e09537
workflow-type: tm+mt
source-wordcount: '2177'
ht-degree: 1%

---

# AEM as a Cloud Service 开发准则 {#aem-as-a-cloud-service-development-guidelines}

在AEMas a Cloud Service中运行的代码必须知道它始终在群集中运行这一事实。 这意味着始终会有多个实例在运行。代码必须具有弹性，尤其是当实例可能在任何时间点停止时。

在更新AEMas a Cloud Service期间，将有旧代码和新代码并行运行的实例。 因此，旧代码不得与由新代码创建的内容中断，而新代码必须能够处理旧内容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要识别群集中的主群集，则可以使用Apache Sling Discovery API来检测该群集。

## 内存中的状态 {#state-in-memory}

状态不得保留在内存中，但保留在存储库中。 否则，如果实例停止，此状态可能会丢失。

## 文件系统上的状态 {#state-on-the-filesystem}

实例的文件系统不应用于AEMas a Cloud Service。 该磁盘是短暂的，在实例循环使用时将进行处置。 对与处理单个请求相关的临时存储使用文件系统是可能的，但不应滥用它来获取大文件。 这是因为它可能对资源使用配额产生负面影响，并且会遇到磁盘限制。

例如，不支持文件系统使用，发布层应确保将需要保留的任何数据发送到外部服务，以便进行较长期的存储。

## 观察 {#observation}

类似地，由于异步发生的一切（如对观察事件执行操作），无法保证在本地执行，因此必须谨慎使用。 对于JCR事件和Sling资源事件，均是如此。 在发生更改时，该实例可能会被拆除并被其他实例替换。 拓扑中其他在当时处于活动状态的实例将能够对该事件做出响应。 但是，在这种情况下，这将不是一个地方性事件，甚至在发布该事件时，如果正在进行的领导人选举，也可能没有积极的领导人。

## 后台任务和长时间运行的作业 {#background-tasks-and-long-running-jobs}

作为后台任务执行的代码必须假定它正在运行的实例可以随时关闭。 因此，代码必须具有弹性，且导入次数最多可恢复。 这意味着如果重新执行代码，则不应再次从开头开始，而应从离开的位置开始。 虽然这不是此类代码的新要求，但在AEMas a Cloud Service中，更有可能发生实例停用。

为了将问题降至最低，应尽可能避免长时间运行的作业，并且应至少恢复这些作业。 要执行此类作业，请使用Sling作业，Sling作业可至少保证一次，因此，如果中断，将尽快重新执行。 但它们或许不应该从头开始。 对于安排此类作业，最好使用 [Sling作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) 调度程序，这样至少执行一次。

不应使用Sling Commons Scheduler进行计划，因为无法保证执行。 只是更有可能会安排时间。

同样，由于异步发生的所有事件(例如对观察事件执行操作（即JCR事件或Sling资源事件）)，无法保证会执行，因此必须谨慎使用。 目前，AEM部署已存在这种情况。

## 传出HTTP连接 {#outgoing-http-connections}

强烈建议任何传出HTTP连接设置合理的连接和读取超时。 对于不应用这些超时的代码，在AEMas a Cloud Service上运行的AEM实例将强制执行全局超时。 以下超时值是连接调用的10秒，以及下列常用Java库使用的连接的读取调用的60秒：

Adobe建议使用提供的 [Apache HttpComponents客户端4.x库](https://hc.apache.org/httpcomponents-client-ga/) 用于建立HTTP连接。

已知有效但可能需要自行提供依赖关系的替代方案包括：

* [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) 和/或 [java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (由AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不推荐，因为它已过时并由版本4.x替换）
* [确定Http](https://square.github.io/okhttp/) (AEM未提供)

## 无经典UI自定义 {#no-classic-ui-customizations}

AEMas a Cloud Service仅支持第三方客户代码的触屏UI。 经典UI无法进行自定义。

## 避免本机二进制文件 {#avoid-native-binaries}

代码在运行时将无法下载或修改二进制文件。 例如，无法解包 `jar` 或 `tar` 文件。

## 无通过AEMas a Cloud Service的流二进制文件 {#no-streaming-binaries}

应通过CDN访问二进制文件，CDN将在核心AEM服务之外提供二进制文件。

例如，请勿使用 `asset.getOriginal().getStream()`，这会触发将二进制文件下载到AEM服务的临时磁盘。

## 无反向复制代理 {#no-reverse-replication-agents}

AEMas a Cloud Service不支持从“发布到作者”进行反向复制。 如果需要此类策略，您可以使用在发布实例场（可能是创作群集）之间共享的外部持久性存储。

## 可能需要移植转发复制代理 {#forward-replication-agents}

内容通过pub-sub机制从“创作”复制到“发布”。 不支持自定义复制代理。

## 监控和调试 {#monitoring-and-debugging}

### 日志 {#logs}

对于本地开发，日志条目将写入 `/crx-quickstart/logs` 文件夹。

在云环境中，开发人员可以通过Cloud Manager下载日志，或使用命令行工具跟踪日志。 <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**设置日志级别**

要更改云环境的日志级别，应修改Sling日志记录OSGi配置，然后完全重新部署。 由于这不是即时的，请谨慎在接收大量流量的生产环境中启用详细日志。 将来，可能会有一些机制来更快地更改日志级别。

>[!NOTE]
>
>要执行下面列出的配置更改，您需要在本地开发环境中创建配置更改，然后将它们推送到AEMas a Cloud Service实例。 有关如何执行此操作的更多信息，请参阅 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md).

**激活DEBUG日志级别**

默认日志级别为“信息”，即不记录DEBUG消息。
要激活“调试”日志级别，请将

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

要调试的属性。 请勿将日志保留在DEBUG日志级别，因为该日志会生成大量日志，所以不要将其保留在必要的时间以内。
调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装将继续进行，但CRX的一部分安装不正确，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作成功。 |

### 线程转储 {#thread-dumps}

云环境中的线程转储会持续收集，但此时无法以自助方式下载。 同时，如果调试问题时需要线程转储，请联系AEM支持人员，并指定确切的时间窗口。

## CRX/DE Lite和开发人员控制台 {#crxde-lite-and-developer-console}

### 地方发展 {#local-development}

对于本地开发，开发人员拥有对CRXDE Lite(`/crx/de`)和AEM Web控制台(`/system/console`)。

请注意，在进行本地开发（使用SDK）时， `/apps` 和 `/libs` 可以直接写入，这与顶级文件夹不可更改的云环境不同。

### AEMas a Cloud Service开发工具 {#aem-as-a-cloud-service-development-tools}

客户可以在创作层的开发环境中访问CRXDE lite，但不能在暂存或生产环境中访问。 不可变存储库(`/libs`, `/apps`)无法在运行时写入，因此尝试执行此操作将导致错误。

开发人员控制台中提供了一组用于调试AEMas a Cloud Service开发人员环境的工具，可用于开发、暂存和生产环境。 可通过调整创作或发布服务URL来确定该URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作为快捷方式，可以使用以下Cloud Manager CLI命令根据下面描述的环境参数启动开发人员控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

请参阅 [本页](/help/release-notes/home.md) 以了解更多信息。

开发人员可以生成状态信息并解析各种资源。

如下图所示，可用状态信息包括包的状态、组件、OSGi配置、Oak索引、OSGi服务和Sling作业。

![开发控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下所示，开发人员可以解决包依赖项和Servlet:

![开发控制台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![开发控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，开发人员控制台还有一个指向“解释查询”工具的链接，这对于调试非常有用：

![开发控制台4](/help/implementing/developing/introduction/assets/devconsole4.png)

对于生产程序，开发人员控制台的访问权限由Admin Console中的“云管理器 — 开发人员角色”定义，而对于沙盒程序，任何具有产品配置文件且有权访问AEMas a Cloud Service的用户都可以使用开发人员控制台。 对于所有程序，状态转储需要“Cloud Manager — 开发人员角色”，并且还必须在创作和发布服务的AEM用户或AEM管理员产品配置文件中定义用户，才能查看两个服务中的状态转储数据。 有关设置用户权限的更多信息，请参阅 [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### AEM Staging和Production Service {#aem-staging-and-production-service}

客户将无法访问用于暂存和生产环境的开发人员工具。

### 性能监控 {#performance-monitoring}

Adobe监控应用程序性能，并采取措施在出现恶化时加以解决。 此时，无法查看应用程序量度。

## 发送电子邮件 {#sending-email}

以下各节介绍如何请求、配置和发送电子邮件。

>[!NOTE]
>
>可以为邮件服务配置OAuth2支持。 有关更多信息，请参阅 [对邮件服务的OAuth2支持](/help/security/oauth2-support-for-mail-service.md).

### 启用出站电子邮件 {#enabling-outbound-email}

默认情况下，用于发送电子邮件的端口处于禁用状态。 要激活端口，请配置 [高级联网](/help/security/configuring-advanced-networking.md)，请确保为每个需要的环境设置 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点的端口转发规则，该规则将目标端口（例如，465或587）映射到代理端口。

建议使用 `kind` 参数设置为 `flexiblePortEgress` 因为Adobe可以优化灵活的端口出口流量的性能。 如果需要唯一的出口IP地址，请选择 `kind` 参数 `dedicatedEgressIp`. 如果您出于其他原因配置了VPN，则还可以使用该高级网络变体提供的唯一IP地址。

您必须通过邮件服务器发送电子邮件，而不是直接通过电子邮件客户端发送。 否则，可能会阻止电子邮件。

### 发送电子邮件 {#sending-emails}

的 [Day CQ Mail Service OSGi服务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) ，并且必须将电子邮件发送到支持请求中指示的邮件服务器，而不是直接发送给收件人。

### 配置 {#email-configuration}

AEM中的电子邮件应使用 [Day CQ Mail Service OSGi服务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

请参阅 [AEM 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) 有关配置电子邮件设置的详细信息。 对于AEMas a Cloud Service，请注意 `com.day.cq.mailer.DefaultMailService OSGI` 服务：

* SMTP服务器主机名应设置为$[env:AEM_PROXY_HOST]
* 配置高级网络时，SMTP服务器端口应设置为在API调用中使用的portForwards参数中设置的原始代理端口值。 例如，30465（而不是465）

如果已请求端口465，则还建议：

* set `smtp.port` to `465`
* set `smtp.ssl` to `true`

如果已请求端口587:

* set `smtp.port` to `587`
* set `smtp.ssl` to `false`

的 `smtp.starttls` 属性将由AEMas a Cloud Service在运行时自动设置为相应的值。 因此，如果 `smtp.ssl` 设置为true时， `smtp.startls` 将被忽略。 如果 `smtp.ssl` 设置为false时， `smtp.starttls` 设置为true。 这与 `smtp.starttls` 值。


可以选择为邮件服务配置OAuth2支持。 有关更多信息，请参阅 [对邮件服务的OAuth2支持](/help/security/oauth2-support-for-mail-service.md).

### 旧版电子邮件配置 {#legacy-email-configuration}

在2021.9.0版本之前，电子邮件是通过客户支持请求配置的。 请注意以下必要调整 `com.day.cq.mailer.DefaultMailService OSGI` 服务：

AEMas a Cloud Service要求通过端口465发送邮件。 如果邮件服务器不支持端口465，则只要启用了TLS选项，就可以使用端口587。

如果已请求端口465:

* set `smtp.port` to `465`
* set `smtp.ssl` to `true`

如果已请求端口587:

* set `smtp.port` to `587`
* set `smtp.ssl` to `false`

的 `smtp.starttls` 属性将由AEMas a Cloud Service在运行时自动设置为相应的值。 因此，如果 `smtp.ssl` 设置为true时， `smtp.startls` 将被忽略。 如果 `smtp.ssl` 设置为false时， `smtp.starttls` 设置为true。 这与 `smtp.starttls` 值。

应将SMTP服务器主机设置为邮件服务器的主机。


## [!DNL Assets] 开发指南和用例 {#use-cases-assets}

要了解资产as a Cloud Service的开发用例、建议和参考材料，请参阅 [资产的开发人员参考](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
