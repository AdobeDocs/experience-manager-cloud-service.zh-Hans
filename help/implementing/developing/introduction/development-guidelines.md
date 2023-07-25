---
title: AEM as a Cloud Service 开发准则
description: 了解在 AEM as a Cloud Service 上进行开发的准则，以及它与本地 AEM 和 AMS 中的 AEM 的重要区别。
exl-id: 94cfdafb-5795-4e6a-8fd6-f36517b27364
source-git-commit: f69b348b7de6c6537a9945793e3397bf4fe30f98
workflow-type: tm+mt
source-wordcount: '2655'
ht-degree: 4%

---

# AEM as a Cloud Service 开发准则 {#aem-as-a-cloud-service-development-guidelines}

>[!CONTEXTUALHELP]
>id="development_guidelines"
>title="AEM as a Cloud Service 开发准则"
>abstract="了解在 AEM as a Cloud Service 上进行开发的准则，以及它与本地 AEM 和 AMS 中的 AEM 的重要区别。"
>additional-url="https://video.tv.adobe.com/v/330555/" text="包结构演示"

本文档介绍了在AEMas a Cloud Service上进行开发的准则，以及它与AEM内部部署和AMS中的AEM不同的重要方式。

## 代码必须能够识别群集 {#cluster-aware}

在AEMas a Cloud Service中运行的代码必须意识到它始终在群集中运行这一事实。 这意味着始终会有多个实例在运行。代码必须是可复原的，尤其是因为实例可能随时停止。

在AEMas a Cloud Service更新期间，有一些实例会并行运行旧代码和新代码。 因此，旧代码不得与新代码创建的内容冲突，新代码必须能够处理旧内容。

如果需要识别群集中的主群集，可以使用Apache Sling Discovery API检测它。

## 内存中的状态 {#state-in-memory}

状态不得保留在内存中，而是必须保留在存储库中。 否则，如果实例停止，此状态可能会丢失。

## 文件系统上的状态 {#state-on-the-filesystem}

实例的文件系统不应在AEMas a Cloud Service中使用。 磁盘是短暂的，当实例被回收时进行处置。 有限地使用文件系统进行与处理单个请求相关的临时存储是可行的，但不应滥用文件系统进行大型存储。 这是因为这可能会对资源使用配额产生负面影响，并遇到磁盘限制。

例如，不支持使用文件系统，发布层应确保将需要保留的任何数据运送到外部服务以进行长期存储。

## 观察 {#observation}

同样，对于诸如对观察事件执行操作之类的异步发生的所有情况，无法保证在本地执行，因此必须谨慎使用。 这对于JCR事件和Sling资源事件均适用。 在进行更改时，可能会删除该实例，然后由其他实例替换。 拓扑中当时处于活动状态的其他实例能够对该事件做出反应。 但是，在这种情况下，这不是本地活动，在发布活动时，甚至可能没有活动的领导者，以防正在进行的领导人选举。

## 后台任务和长时间运行的作业 {#background-tasks-and-long-running-jobs}

作为后台任务执行的代码必须假定运行它的实例可以随时关闭。 因此，代码必须是可复原的，并且最重要的是可恢复的。 这意味着，如果重新执行代码，则不应从头开始，而应从原来的位置开始。 虽然这并非此类代码的新要求，但在AEMas a Cloud Service中，更有可能发生实例删除。

为了最大程度地减少问题，应尽可能避免长时间运行的作业，这些作业应至少可以恢复。 要执行此类作业，请使用Sling作业，它至少有一次保证，因此如果中断，将尽快重新执行。 但它们或许不应从头开始。 要计划此类作业，最好使用 [Sling作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing) 计划程序，因为这再次确保至少一次执行。

Sling Commons Scheduler不应用于调度，因为无法保证执行。 只是更有可能按计划进行。

同样，对于异步发生的所有情况，例如对观察事件执行操作（包括JCR事件或Sling资源事件），无法保证执行，因此必须谨慎使用。 对于当前的AEM部署而言，情况已经如此。

## 传出HTTP连接 {#outgoing-http-connections}

强烈建议任何传出HTTP连接设置合理的连接和读取超时；建议值为连接超时1秒，读取超时5秒。 必须根据处理这些请求的后端系统的性能来确定确切的数量。

对于未应用这些超时的代码，在AEMas a Cloud Service上运行的AEM实例将强制执行全局超时。 这些超时值对于连接调用为10秒，对于连接读取调用为60秒。

Adobe建议使用提供的 [Apache HttpComponents Client 4.x库](https://hc.apache.org/httpcomponents-client-ga/) 用于建立HTTP连接。

已知有效，但可能需要自己提供依赖的替代方案是：

* [java.net.URL](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URL.html) 和/或 [java.net.URLConnection](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/net/URLConnection.html) (AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不推荐，因为它已过时且已被版本4.x替换）
* [确定Http](https://square.github.io/okhttp/) (AEM未提供)

除了提供超时之外，还应该实施对此类超时和意外HTTP状态代码的正确处理。

## 处理请求速率限制 {#rate-limit-handling}

>[!NOTE]
>在2023年8月7日当周，HTTP错误响应将从503更改为429。
>
当AEM传入请求的速率超过正常级别时，AEM将使用HTTP错误代码429响应新请求。 对AEM进行程序化调用的应用程序可以考虑进行防御性编码，在几秒钟后使用指数回退策略重试。 在2023年8月中旬之前，AEM使用HTTP错误代码503响应相同的条件。

## 无经典UI自定义 {#no-classic-ui-customizations}

AEMas a Cloud Service仅支持第三方客户代码的Touch UI。 经典UI不可自定义。

## 无本机二进制文件或本机库 {#avoid-native-binaries}

本机二进制文件和库不得部署到云环境中或安装在云环境中。

此外，代码不应在运行时尝试下载本机二进制文件或本机Java扩展（例如JNI）。

## 没有流二进制文件通过AEMas a Cloud Service {#no-streaming-binaries}

应通过CDN访问二进制文件，该CDN将提供核心AEM服务之外的二进制文件。

例如，请勿使用 `asset.getOriginal().getStream()`，它会触发将二进制文件下载到AEM服务的临时磁盘上。

## 无反向复制代理 {#no-reverse-replication-agents}

AEMas a Cloud Service不支持从“发布”到“创作”的反向复制。 如果需要此类策略，您可以使用在发布实例场之间共享的外部持久性存储，可能还有创作聚类。

## 可能需要移植转发复制代理 {#forward-replication-agents}

内容通过pub-sub机制从Author复制到Publish。 不支持自定义复制代理。

## 监控和调试 {#monitoring-and-debugging}

### 日志 {#logs}

对于本地开发，日志条目将写入本地文件 `/crx-quickstart/logs` 文件夹。

在云环境中，开发人员可以通过Cloud Manager下载日志，或使用命令行工具跟踪日志。 <!-- See the [Cloud Manager documentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**设置日志级别**

要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后完全重新部署。 由于这不是即时的，因此对于在接收大量流量的生产环境中启用详细日志，请务必谨慎。 将来，可能会有更快地更改日志级别的机制。

>[!NOTE]
>
>要执行下面列出的配置更改，请在本地开发环境中创建这些更改，然后将它们推送到AEMas a Cloud Service实例。 有关如何执行此操作的更多信息，请参阅 [部署到AEMas a Cloud Service](/help/implementing/deploying/overview.md).

**激活DEBUG日志级别**

默认日志级别为INFO，即不记录DEBUG消息。 要激活DEBUG日志级别，请更新以下属性以调试模式。

`/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level`

例如，设置 `/apps/<example>/config/org.apache.sling.commons.log.LogManager.factory.config~<example>.cfg.json` ，其值如下。

```json
{
   "org.apache.sling.commons.log.names": [
      "com.example"
   ],
   "org.apache.sling.commons.log.level": "DEBUG",
   "org.apache.sling.commons.log.file": "logs/error.log",
   "org.apache.sling.commons.log.additiv": "false"
}
```

不要将日志保留在DEBUG日志级别的时间长于必要的时间，因为这会生成大量条目。

如果需要始终登录，可以使用基于运行模式的OSGi配置定位为不同的AEM环境设置离散日志级别 `DEBUG` 在开发过程中。 例如：

| 环境 | 按运行模式列出的OSGi配置位置 | `org.apache.sling.commons.log.level` 属性值 |
| - | - | - |
| 开发 | /apps/example/config/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 调试 |
| 暂存 | /apps/example/config.stage/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 警告 |
| 生产 | /apps/example/config.prod/org.apache.sling.commons.log.LogManager.factory.config~example.cfg.json | 错误 |

调试文件中的一行通常以DEBUG开头，然后提供日志级别、安装程序操作和日志消息。 例如：

```text
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装会继续，但部分CRX安装不正确，无法正常工作。 |
| 2 | 警告 | 操作已成功，但遇到了问题。 CRX可能会正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作已成功。 |

### 线程转储 {#thread-dumps}

云环境中的线程转储是持续收集的，但目前无法自助下载。 同时，如果调试问题需要线程转储，请联系AEM支持，并指定确切的时间范围。

## CRX/DE Lite和开发人员控制台 {#crxde-lite-and-developer-console}

### 本地开发 {#local-development}

对于本地开发，开发人员拥有CRXDE Lite(`/crx/de`)和AEM Web Console (`/system/console`)。

请注意，在本地开发（使用SDK）中， `/apps` 和 `/libs` 可以直接写入，这与云环境不同，在云环境中，这些顶级文件夹不可更改。

### AEM as a Cloud Service 开发工具 {#aem-as-a-cloud-service-development-tools}

客户可以在创作层的开发环境中访问CRXDE Lite，但不能在暂存或生产环境中访问。 不可变存储库(`/libs`， `/apps`)无法在运行时写入，因此尝试这样做将导致错误。

相反，可以从开发人员控制台启动存储库浏览器，为创作、发布和预览层上的所有环境提供到存储库的只读视图。 阅读有关存储库浏览器的更多信息 [此处](/help/implementing/developing/tools/repository-browser.md).

适用于RDE、开发、暂存和生产环境的开发人员控制台中提供了一组用于调试AEMas a Cloud Service开发人员环境的工具。 可以通过调整创作或发布服务URL来确定URL，如下所示：

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作为快捷方式，可以使用以下Cloud Manager CLI命令根据如下所述的环境参数启动开发人员控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

参见 [此页面](/help/release-notes/home.md) 了解更多信息。

开发人员可以生成状态信息，并解析各种资源。

如下图所示，可用状态信息包括包、组件、OSGI配置、Oak索引、OSGI服务和Sling作业的状态。

![开发控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下图所示，开发人员可以解析包依赖项和servlet：

![开发控制台2](/help/implementing/developing/introduction/assets/devconsole2.png)

![开发控制台3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，开发人员控制台还有一个指向Explain查询工具的链接，这对调试很有用：

![开发控制台4](/help/implementing/developing/introduction/assets/devconsole4.png)

对于生产程序，对开发人员控制台的访问权限由Admin Console中的“Cloud Manager — 开发人员角色”定义，而对于沙盒程序，开发人员控制台可供任何拥有产品配置文件的用户访问AEMas a Cloud Service。 对于所有程序，状态转储需要“Cloud Manager — 开发人员角色”，并且还必须在创作和发布服务的AEM用户或AEM管理员产品配置文件中定义存储库浏览器和用户，才能查看来自这两个服务的数据。 有关设置用户权限的更多信息，请参阅 [Cloud Manager文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 性能监控 {#performance-monitoring}

Adobe监控应用程序性能并在出现性能下降时采取措施解决此问题。 目前，无法观察应用程序量度。

## 发送电子邮件 {#sending-email}

以下各节介绍如何请求、配置和发送电子邮件。

>[!NOTE]
>
>可以配置邮件服务以支持OAuth2。 有关更多信息，请参阅 [对邮件服务的OAuth2支持](/help/security/oauth2-support-for-mail-service.md).

### 启用出站电子邮件 {#enabling-outbound-email}

默认情况下，用于发送电子邮件的端口处于禁用状态。 要激活端口，请配置 [高级联网](/help/security/configuring-advanced-networking.md)，确保为每个所需的环境设置 `PUT /program/<program_id>/environment/<environment_id>/advancedNetworking` 端点的端口转发规则，用于将预期端口（例如，465或587）映射到代理端口。

建议使用配置高级网络 `kind` 参数设置为 `flexiblePortEgress` 因为Adobe可以优化灵活端口出口流量的性能。 如果需要唯一的出口IP地址，请选择 `kind` 参数 `dedicatedEgressIp`. 如果您已出于其他原因配置了VPN，则也可以使用该高级网络变体提供的唯一IP地址。

您必须通过邮件服务器发送电子邮件，而不是直接发送给电子邮件客户端。 否则，可能会阻止电子邮件。

### 发送电子邮件 {#sending-emails}

此 [Day CQ邮件服务OSGI服务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service) ，并且必须将电子邮件发送到支持请求中所述的邮件服务器，而不是直接发送给收件人。

### 配置 {#email-configuration}

AEM中的电子邮件应使用 [Day CQ邮件服务OSGi服务](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service).

请参阅 [AEM 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65/administering/operations/notification.html) 以了解有关配置电子邮件设置的详细信息。 对于AEMas a Cloud Service，请注意以下对 `com.day.cq.mailer.DefaultMailService OSGI` 服务：

* SMTP服务器主机名应设置为$[env：AEM_PROXY_HOST；default=proxy.tunnel]
* 在配置高级联网时，SMTP服务器端口应设置为API调用中使用的portForwards参数中设置的原始代理端口的值。 例如，30465（而不是465）

SMTP服务器端口应设置为 `portDest` 在配置高级联网和 `portOrig` 值应当是一个有意义的值，且必须在30000 - 30999的所需范围内。 例如，如果SMTP服务器端口为465，则端口30465应用作 `portOrig` 值。

在这种情况下，并假定需要在的配置中启用SSL **Day CQ邮件服务OSGI** 服务：

* 设置 `smtp.port` 到 `30465`
* 设置 `smtp.ssl` 到 `true`

或者，如果目标端口为587，则将 `portOrig` 应使用30587的值。 并且假定应禁用SSL，Day CQ邮件服务OSGI服务的配置如下：

* 设置 `smtp.port` 到 `30587`
* 设置 `smtp.ssl` 到 `false`

此 `smtp.starttls` 属性将由AEMas a Cloud Service在运行时自动设置为适当的值。 因此，如果 `smtp.ssl` 设置为true， `smtp.startls` 将被忽略。 如果 `smtp.ssl` 设置为false， `smtp.starttls` 设置为true。 这与 `smtp.starttls` 在OSGI配置中设置的值。


可以选择配置邮件服务以支持OAuth2。 有关更多信息，请参阅 [对邮件服务的OAuth2支持](/help/security/oauth2-support-for-mail-service.md).

### 旧版电子邮件配置 {#legacy-email-configuration}

在2021.9.0版之前，电子邮件是通过客户支持请求配置的。 请注意以下必要的调整 `com.day.cq.mailer.DefaultMailService OSGI` 服务：

AEMas a Cloud Service要求通过端口465发送邮件。 如果邮件服务器不支持端口465，只要启用TLS选项，就可以使用端口587。

如果已请求端口465：

* 设置 `smtp.port` 到 `465`
* 设置 `smtp.ssl` 到 `true`

如果已请求端口587，则：

* 设置 `smtp.port` 到 `587`
* 设置 `smtp.ssl` 到 `false`

此 `smtp.starttls` 属性将由AEMas a Cloud Service在运行时自动设置为适当的值。 因此，如果 `smtp.ssl` 设置为true， `smtp.startls` 将被忽略。 如果 `smtp.ssl` 设置为false， `smtp.starttls` 设置为true。 这与 `smtp.starttls` 在OSGI配置中设置的值。

SMTP服务器主机应设置为邮件服务器的主机。

## 避免使用大型多值属性 {#avoid-large-mvps}

AEMas a Cloud Service下的Oak内容存储库不会与过多的多值属性(MVP)一起使用。 经验法则是将最有价值人选保持在1000人以下。 然而，实际性能取决于许多因素。

在超过1000个之后，默认情况下会记录警告。 它们与以下内容类似。

```text
org.apache.jackrabbit.oak.jcr.session.NodeImpl Large multi valued property [/path/to/property] detected (1029 values). 
```

大型MVP可能会导致错误，因为MongoDB文档超过16 MB，从而导致类似于以下内容的错误。

```text
Caused by: com.mongodb.MongoWriteException: Resulting document after update is larger than 16777216
```

请参阅 [Apache Oak文档](https://jackrabbit.apache.org/oak/docs/dos_and_donts.html#Large_Multi_Value_Property) 了解更多详细信息。

## [!DNL Assets] 开发指南和用例 {#use-cases-assets}

要了解Assetsas a Cloud Service的开发用例、建议和参考材料，请参阅 [Assets开发人员参考](/help/assets/developer-reference-material-apis.md#assets-cloud-service-apis).
