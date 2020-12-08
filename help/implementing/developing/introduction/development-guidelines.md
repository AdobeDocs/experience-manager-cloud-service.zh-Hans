---
title: AEM as a Cloud Service 开发准则
description: AEM as a Cloud Service 开发准则
translation-type: tm+mt
source-git-commit: 2910d5c1d32ca58f6634204bac882fccb3e65bf3
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 1%

---


# AEM as a Cloud Service 开发准则 {#aem-as-a-cloud-service-development-guidelines}

作为Cloud Service在AEM中运行的代码必须知道它始终在群集中运行。 这意味着始终会有多个实例在运行。该代码必须具有弹性，尤其是当实例可能在任何时间点停止时。

在将AEM作为Cloud Service进行更新期间，将存在新旧代码并行运行的实例。 因此，旧代码不能与由新代码创建的内容断开，而新代码必须能够处理旧内容。
<!--

>[!NOTE]
> All of the best practices mentioned here hold true for on-premise deployments of AEM, if not stated otherwise. An instance can always stop due to various reasons. However, with Skyline it is more likely to happen therefore an instance stopping is the rule not an exception.

-->

如果需要在群集中识别主群集，可以使用Apache Sling Discovery API检测它。

## 内存{#state-in-memory}中的状态

状态不能保留在内存中，但必须保留在存储库中。 否则，如果实例停止，则此状态可能会丢失。

## 文件系统{#state-on-the-filesystem}的状态

实例的文件系统不应在AEM中用作Cloud Service。 该磁盘是暂时的，在回收实例时将被丢弃。 对与处理单个请求相关的临时存储使用文件系统是可能的，但不应滥用于大文件。 这是因为它可能对资源使用配额产生负面影响，并且受到磁盘限制。

例如，不支持文件系统使用，发布层应确保需要保留的任何数据都被发送到外部服务，以便进行长期存储。

## 观察{#observation}

类似地，由于异步发生的一切都像在观察事件上行动一样，它无法保证在本地执行，因此必须谨慎使用。 JCR事件和Sling资源事件均是如此。 在发生变化时，该实例可被取下并被另一个实例替换。 当时处于活动状态的拓扑中的其他实例将能够对该事件做出响应。 但在这种情况下，这将不是地方事件，在事件发布后，如果领导人不断当选，甚至可能没有积极的领导人。

## 后台任务和长时间运行作业{#background-tasks-and-long-running-jobs}

作为后台任务执行的代码必须假设它正在运行的实例可以随时关闭。 因此，代码必须具有弹性，且大多数导入都可恢复。 这意味着，如果代码重新执行，它不应从头开始再次开始，而应从离开位置更近。 虽然这不是这种代码的新要求，但在AEM作为Cloud Service，更有可能发生实例撤消。

为了最大限度地减少问题，应尽可能避免长时间的工作，而且至少应该恢复这些工作。 要执行此类作业，请使用Sling作业，Sling作业至少有一次保证，因此如果它们被中断，将尽快重新执行。 但他们可能不应该从头开始开始。 对于安排此类作业，最好使用[Sling作业](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#jobs-guarantee-of-processing)调度程序，作为至少一次执行的再次使用。

Sling Commons调度程序不应用于计划，因为无法保证执行。 只是更有可能安排时间。

同样，由于异步发生的一切，如在观测事件(即JCR事件或Sling资源事件)上采取行动，无法保证执行，因此必须谨慎使用。 目前AEM部署已经如此。

## 传出HTTP连接{#outgoing-http-connections}

强烈建议任何传出HTTP连接都设置合理的连接和读取超时。 对于不应用这些超时的代码，在AEM上作为Cloud Service运行的AEM实例将强制执行全局超时。 这些超时值对于连接调用为10秒，对于下列常用Java库使用的连接为60秒：

Adobe建议使用提供的[Apache HttpComponents客户端4.x库](https://hc.apache.org/httpcomponents-client-ga/)进行HTTP连接。

已知有效但可能需要自行提供依赖项的替代方法有：

* [java.net.](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) URL和/ [或java.net.URLConnection](https://docs.oracle.com/javase/7/docs/api/java/net/URLConnection.html) (由AEM提供)
* [Apache Commons HttpClient 3.x](https://hc.apache.org/httpclient-3.x/) （不建议使用，因为它已过时并替换为4.x版）
* [OK Http](https://square.github.io/okhttp/) (AEM未提供)

## 没有经典UI自定义{#no-classic-ui-customizations}

AEM作为Cloud Service仅支持第三方客户代码的触屏UI。 经典UI不可自定义。

## 避免本机二进制文件{#avoid-native-binaries}

代码在运行时无法下载二进制文件，也无法修改它们。 例如，它无法解压缩`jar`或`tar`文件。

## 没有通过AEM作为Cloud Service{#no-streaming-binaries}的流二进制文件

应通过CDN访问二进制文件，CDN将为核心AEM服务之外的二进制文件提供服务。

例如，请勿使用`asset.getOriginal().getStream()`，它会触发将二进制文件下载到AEM服务的临时磁盘上。

## 没有反向复制代理{#no-reverse-replication-agents}

AEM作为Cloud Service不支持从发布到作者的反向复制。 如果需要此类策略，您可以使用在发布实例场（可能是作者群集）之间共享的外部持久性存储。

## 可能需要移植转发复制代理{#forward-replication-agents}

内容通过pub-sub机制从“作者”复制到“发布”。 不支持自定义复制代理。

## 监视和调试{#monitoring-and-debugging}

### 日志 {#logs}

对于本地开发，日志条目将写入`/crx-quickstart/logs`文件夹中的本地文件。

在云环境上，开发人员可以通过云管理器下载日志或使用命令行工具跟踪日志。<!-- See the [Cloud Manager documentation](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) for more details. Note that custom logs are not supported and so all logs should be output to the error log. -->

**设置日志级别**

要更改云环境的日志级别，应修改Sling日志记录OSGI配置，然后进行完全重新部署。 由于这不是即时的，因此请务必小心为收到大量流量的生产环境启用详细日志。 将来，可能会有一些机制来更快地更改日志级别。

>[!NOTE]
>
>要执行下面列出的配置更改，您需要在本地开发环境创建这些更改，然后将它们作为Cloud Service实例推送到AEM。 有关如何执行此操作的详细信息，请参阅[将AEM部署为Cloud Service](/help/implementing/deploying/overview.md)。

**激活DEBUG日志级别**

默认日志级别为INFO，即不记录DEBUG消息。
要激活DEBUG日志级别，请设置

``` /libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level ```

要调试的属性。 不要将DEBUG日志级别的日志保留得比必需的更长，因为它会生成大量日志。
调试文件中的一行通常与DEBUG开始，然后提供日志级别、安装程序操作和日志消息。 例如：

``` DEBUG 3 WebApp Panel: WebApp successfully deployed ```

日志级别如下：

| 0 | 致命错误 | 操作失败，安装程序无法继续。 |
|---|---|---|
| 1 | 错误 | 操作失败。 安装将继续进行，但CRX的某部分安装不正确，将无法工作。 |
| 2 | 警告 | 操作已成功，但遇到问题。 CRX可能正常工作，也可能无法正常工作。 |
| 3 | 信息 | 操作已成功。 |

### 线程转储{#thread-dumps}

云环境上的线程转储会持续收集，但此时无法以自助方式下载。 同时，如果调试问题时需要线程转储，请与AEM支持联系，指定确切的时间窗口。

## CRX/DE Lite和开发人员控制台{#crxde-lite-and-developer-console}

### 本地开发{#local-development}

对于本地开发，开发人员可以完全访问CRXDE Lite(`/crx/de`)和AEM Web控制台(`/system/console`)。

请注意，在本地开发（使用云就绪型快速启动）中，`/apps`和`/libs`可以直接写入，这与那些顶级文件夹不可变的云环境不同。

### AEM作为Cloud Service开发工具{#aem-as-a-cloud-service-development-tools}

客户可以在创作层的开发环境访问CRXDE lite，但不能在舞台或生产上访问。 不可变的存储库(`/libs`, `/apps`)在运行时无法写入，因此尝试写入将导致错误。

开发人员控制台中提供一组工具，用于将AEM作为Cloud Service开发人员环境进行调试，面向开发人员、舞台和生产环境。 可以通过按如下方式调整作者或发布服务URL来确定URL:

`https://dev-console/-<namespace>.<cluster>.dev.adobeaemcloud.com`

作为快捷方式，以下Cloud Manager CLI命令可用于根据下面描述的环境参数启动开发人员控制台：

`aio cloudmanager:open-developer-console <ENVIRONMENTID> --programId <PROGRAMID>`

有关详细信息，请参阅[此页](/help/release-notes/home.md)。

开发人员可以生成状态信息并解析各种资源。

如下所示，可用状态信息包括捆绑包、组件、OSGI配置、橡树索引、OSGI服务和Sling作业的状态。

![开发控制台1](/help/implementing/developing/introduction/assets/devconsole1.png)

如下图所示，开发人员可以解析包依赖关系和servlet:

![Dev Console 2](/help/implementing/developing/introduction/assets/devconsole2.png)

![Dev Console 3](/help/implementing/developing/introduction/assets/devconsole3.png)

此外，开发人员控制台还有一个指向“解释查询”工具的链接：

![Dev Console 4](/help/implementing/developing/introduction/assets/devconsole4.png)

对于常规项目，对开发人员控制台的访问由Admin Console中的“云管理者——开发人员角色”定义，而对于沙箱项目，开发人员控制台对于具有产品用户档案的任何用户都可用，允许他们以Cloud Service的身份访问AEM。 对于所有项目，状态转储需要“云管理器——开发人员角色”，并且用户还必须在AEM用户或AEM管理员产品用户档案中为创作和发布服务定义，才能从两个服务视图状态转储数据。 有关设置用户权限的详细信息，请参阅[云管理器文档](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。


### AEM Staging and Production Service {#aem-staging-and-production-service}

客户将无权访问用于分阶段和生产环境的开发人员工具。

### 性能监视{#performance-monitoring}

Adobe监视应用程序性能并采取措施在出现恶化时加以解决。 目前，无法观察应用程序指标。

## 专用出口IP地址{#dedicated-egress-ip-address}

应请求，AEM作为Cloud Service将为HTTP（端口80）和HTTPS（端口443）以Java代码编程的出站通信提供静态的专用IP地址。

### 优势{#benefits}

当与SaaS供应商（如CRM供应商）集成或AEM外的其他集成作为优惠IP地址的Cloud Service时，此专用IP地址可允许列表以增强安全性。 通过向添加专用IP地允许列表址，它确保只允许来自客户AEMCloud Service的流量流入外部服务。 这是除了允许的来自任何其他IP的流量之外。

如果没有启用专用IP地址功能，AEM作为Cloud Service发出的流量将流经与其他客户共享的一组IP。

### 配置 {#configuration}

要启用专用IP地址，请向客户支持部门提交请求，客户支持部门将提供IP地址信息。 请求应指定每个环境，如果新环境在初始请求后需要该功能，则应另外提出请求。 不支持沙箱项目环境。

### 功能使用{#feature-usage}

该功能与导致出站流量的Java代码或库兼容，前提是它们使用标准Java系统属性进行代理配置。 实际上，这应包括大多数常用的库。

以下是代码示例：

```
public JSONObject getJsonObject(String relativePath, String queryString) throws IOException, JSONException {
  String relativeUri = queryString.isEmpty() ? relativePath : (relativePath + '?' + queryString);
  URL finalUrl = endpointUri.resolve(relativeUri).toURL();
  URLConnection connection = finalUrl.openConnection();
  connection.addRequestProperty("Accept", "application/json");
  connection.addRequestProperty("X-API-KEY", apiKey);

  try (InputStream responseStream = connection.getInputStream(); Reader responseReader = new BufferedReader(new InputStreamReader(responseStream, Charsets.UTF_8))) {
    return new JSONObject(new JSONTokener(responseReader));
  }
}
```

同一专用IP适用于Adobe组织中的所有项目以及每个项目中的所有环境。 它适用于创作和发布服务。

仅支持HTTP和HTTPS端口。 加密时，这包括HTTP/1.1和HTTP/2。

### 调试注意事项{#debugging-considerations}

为了验证流量是否确实在预期的专用IP地址上传出，请检查目标服务中的日志（如果可用）。 否则，调用调试服务(如[https://ifconfig.me/ip](https://ifconfig.me/ip))可能会很有用，这将返回调用的IP地址。

## 发送电子邮件{#sending-email}

AEM作为Cloud Service，要求对出站邮件进行加密。 以下各节介绍如何请求、配置和发送电子邮件。

### 请求访问{#requesting-access}

默认情况下，出站电子邮件处于禁用状态。 要激活它，请提交支持票证，具有：

1. 邮件服务器的完全限定域名（例如`smtp.sendgrid.net`）
1. 要使用的端口。 如果邮件服务器支持，端口应为465，否则端口587请注意，只有邮件服务器要求并强制使用该端口上的TLS时，端口587才能使用
1. 项目ID和环境ID，用于发送邮件至
1. 创作、发布还是同时使用SMTP访问。

### 发送电子邮件{#sending-emails}

应使用[Day CQ邮件服务OSGI服务](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)，电子邮件必须发送到支持请求中指示的邮件服务器，而不是直接发送给收件人。

AEM CS要求通过端口465发送邮件。 如果邮件服务器不支持端口465，则只要启用TLS选项，就可以使用端口587。

>[!NOTE]
>
>请注意，Adobe不支持通过唯一专用IP地址进行SMTP签名。

### 配置 {#email-configuration}

AEM中的电子邮件应使用[Day CQ Mail Service OSGi服务](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html#configuring-the-mail-service)发送。

有关配置电子邮件设置的详细信息，请参阅[AEM 6.5文档](https://docs.adobe.com/content/help/en/experience-manager-65/administering/operations/notification.html)。 对于AEM CS，必须对`com.day.cq.mailer.DefaultMailService OSGI`服务进行以下调整：

如果已请求端口465:

* 将`smtp.port`设置为`465`
* 将`smtp.ssl`设置为`true`
* 将`smtp.starttls`设置为`false`

如果请求了端口587（仅当邮件服务器不支持端口465时才允许）:

* 将`smtp.port`设置为`587`
* 将`smtp.ssl`设置为`false`
* 将`smtp.starttls`设置为`true`