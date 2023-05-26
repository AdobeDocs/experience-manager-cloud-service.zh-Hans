---
title: AEM日志as a Cloud Service
description: 了解如何使用AEMas a Cloud Service的日志记录功能，为中央日志记录服务配置全局参数、为各个服务配置特定设置或者如何请求数据日志记录。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 9e67b4f68fe450e80249c3959e3517c6cba3275d
workflow-type: tm+mt
source-wordcount: '2382'
ht-degree: 3%

---

# AEM日志as a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEMas a Cloud Service是一个平台，让客户可以包含自定义代码，以便为其客户群创建独特的体验。 考虑到这一点，日志服务是一个关键功能，可用于在本地开发和云环境(特别是AEMas a Cloud Service的开发环境)中调试和了解代码执行。

AEMas a Cloud Service日志设置和日志级别在配置文件中进行管理，这些配置文件作为Git中AEM项目的一部分存储，并通过Cloud Manager部署为AEM项目的一部分。 AEMas a Cloud Service中的日志记录可以划分为两个逻辑集：

* AEM日志记录，在AEM应用程序级别执行日志记录
* Apache HTTPD Web Server/Dispatcher日志记录，用于在发布层上执行Web服务器和Dispatcher的日志记录。

## AEM日志记录 {#aem-logging}

AEM应用程序级别的日志记录由三个日志处理：

1. AEM Java日志，用于渲染AEM应用程序的Java日志记录语句。
1. HTTP请求日志，用于记录有关AEM提供的HTTP请求及其响应的信息
1. HTTP访问日志，用于记录由AEM提供的汇总信息和HTTP请求

>[!NOTE]
>
>从发布层的Dispatcher缓存或上游CDN提供的HTTP请求不会反映在这些日志中。

## AEM Java日志记录 {#aem-java-logging}

AEMas a Cloud Service提供对Java log语句的访问。 AEM应用程序的开发人员应遵循常规Java记录最佳实践，在下列日志级别记录有关自定义代码执行的相关语句：

<table>
<tr>
<td>
<b>AEM环境</b></td>
<td>
<b>日志级别</b></td>
<td>
<b>描述</b></td>
<td>
<b>日志语句可用性</b></td>
</tr>
<tr>
<td>
开发</td>
<td>
调试</td>
<td>
描述应用程序中发生的情况。<br>
当DEBUG日志记录处于活动状态时，将记录提供所发生活动的清晰图示以及任何影响处理的关键参数的语句。</td>
<td>
<ul>
<li> 本地开发</li>
<li>开发</li>
</ul></td>
</tr>
<tr>
<td>
暂存</td>
<td>
警告</td>
<td>
描述有可能出错的情况。<br>
当WARN日志记录处于活动状态时，只记录指示接近子最优性的条件的语句。</td>
<td>
<ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
</ul></td>
</tr>
<tr>
<td>
生产</td>
<td>
错误</td>
<td>
描述指示故障并需要解决的情况。<br>
当ERROR记录处于活动状态时，只记录指示失败的语句。 错误日志语句指示应尽快解决的严重问题。</td>
<td>
<ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
<li>生产</li>
</ul></td>
</tr>
</table>

虽然Java日志记录支持其他多个级别的日志记录粒度，但AEMas a Cloud Service建议使用上述三个级别。

AEM日志级别是通过OSGi配置为每个环境类型设置的，这些配置将提交到Git，并通过Cloud Manager部署到AEMas a Cloud Service。 因此，最好保持日志语句的一致性并且让环境类型熟悉，以确保通过AEM as Environment提供的日志在最佳日志级别可用，而无需使用更新的日志级别配置重新部署应用程序。Cloud Service

**示例日志输出**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

**日志格式**

<table>
<tbody>
<tr>
<td>日期和时间</td>
<td>29.04.2020 21:50:13.398</td>
</tr>
<tr>
<td>AEMas a Cloud Service节点编号</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>日志级别</td>
<td>调试</td>
</tr>
<tr>
<td>跟帖</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java类</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>日志消息</td>
<td>未指定审批者，默认为[ Creative Approvers用户组]</td>
</tr>
</tbody>
</table>

### 配置记录器 {#configuration-loggers}

AEM Java日志被定义为OSGi配置，因此使用运行模式文件夹定位特定的AEMas a Cloud Service环境。

通过Sling LogManager工厂的OSGi配置为自定义Java包配置Java日志记录。 有两个受支持的配置属性：

| OSGi配置属性 | 描述 |
|---|---|
| org.apache.sling.commons.log.names | 要为其收集log语句的Java包。 |
| org.apache.sling.commons.log.level | 记录Java包的日志级别，由org.apache.sling.commons.log.names指定 |

更改其他LogManager OSGi配置属性可能会导致AEMas a Cloud Service出现可用性问题。

以下是推荐的日志记录配置示例(使用占位符Java包： `com.example`)，以了解三种AEMas a Cloud Service的环境类型。

### 开发 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
}
```

### 暂存 {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
}
```

### 生产 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
}
```

## AEM HTTP请求日志记录 {#aem-http-request-logging}

AEMas a Cloud Service的HTTP请求日志记录按时间顺序深入分析向AEM发出的HTTP请求及其HTTP响应。 此日志有助于了解向AEM发出的HTTP请求以及处理和响应这些请求的顺序。

了解此日志的关键是按其ID映射HTTP请求和响应对，这些ID由括号中的数值表示。 请注意，请求及其相应响应在日志中经常会插入其他HTTP请求和响应。

**示例日志**

```
29/Apr/2020:19:14:21 +0000 [137] -> POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] -> GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:21 +0000 [137] <- 201 text/html 111ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] <- 200 text/html;charset=utf-8 637ms [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
```

**日志格式**

<table>
<tbody>
<tr>
<td>日期和时间</td>
<td>2020年4月29日:19:14:21 +0000</td>
</tr>
<tr>
<td>请求/响应对Id</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>协议</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEMas a Cloud Service节点编号</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日志 {#configuring-the-log}

无法在AEMas a Cloud Service中配置AEM HTTP请求日志。

## AEM HTTP访问日志记录 {#aem-http-access-logging}

AEM as aCloud ServiceHTTP访问日志记录按时间顺序显示HTTP请求。 每个日志条目表示访问AEM的HTTP请求。

此日志有助于快速了解向AEM发出的HTTP请求（如果这些请求通过查看随附的HTTP响应状态代码成功）以及HTTP请求完成所用的时间。 通过按用户筛选日志条目，此日志还有助于调试特定用户的活动。

**示例日志输出**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEMas a Cloud Service节点编号 | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| 客户端的IP地址 | - |
| 用户 | myuser@adobe.com |
| 日期和时间 | 2020年4月30日:17:37:14 +0000 |
| HTTP方法 | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| 协议 | HTTP/1.1 |
| HTTP响应状态 | 200 |
| 响应正文的大小（以字节为单位） | 1141 |
| 引用 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| 用户代理 | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### 配置HTTP访问日志 {#configuring-the-http-access-log}

无法在AEMas a Cloud Service中配置HTTP访问日志。

## Apache Web Server和Dispatcher日志记录 {#apache-web-server-and-dispatcher-logging}

AEMas a Cloud Service在发布上为Apache Web Server和Dispatcher层提供三个日志：

* Apache HTTPD Web Server访问日志
* Apache HTTPD Web Server错误日志
* Dispatcher日志

请注意，这些日志仅适用于发布层。

通过这组日志，您可以在向AEMas a Cloud Service发布层发出请求之前，获得这些请求到达AEM应用程序的HTTP请求的洞察。 这一点非常重要，因为理想情况下，对发布层服务器的大多数HTTP请求都由Apache HTTPD Web Server和AEM Dispatcher缓存的内容提供，并且永远不会访问AEM应用程序本身。 因此，AEM Java、请求或访问日志中没有这些请求的日志语句。

### Apache HTTPD Web Server访问日志 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server访问日志为到达发布层的Web服务器/Dispatcher的每个HTTP请求提供语句。 请注意，从上游CDN提供的请求不会反映在这些日志中。

请参阅中有关错误日志格式的信息 [官方apache文档](https://httpd.apache.org/docs/2.4/logs.html#accesslog).

**示例日志输出**

```
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-32.png HTTP/1.1" 200 715 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:41 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/favicons/favicon-512.png HTTP/1.1" 200 9631 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
cm-p1234-e5678-aem-publish-b86c6b466-qpfvp - - 17/Jul/2020:09:14:42 +0000  "GET /etc.clientlibs/wknd/clientlibs/clientlib-site/resources/images/country-flags/US.svg HTTP/1.1" 200 810 "https://publish-p6902-e30226.adobeaemcloud.com/content/wknd/us/en.html" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0"
```

**日志格式**

<table>
<tbody>
<tr>
<td>AEM as a Cloud Service节点ID</td>
<td>cm-p1234-e26813-aem-publish-5c787687c-lqlxr</td>
</tr>
<tr>
<td>客户端的IP地址</td>
<td>-</td>
</tr>
<tr>
<td>用户</td>
<td>-</td>
</tr>
<tr>
<td>日期和时间</td>
<td>2020年5月01日:00:09:46 +0000</td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/example.html</td>
</tr>
<tr>
<td>协议</td>
<td>HTTP/1.1</td>
</tr>
<tr>
<td>HTTP响应状态</td>
<td>200</td>
</tr>
<tr>
<td>大小</td>
<td>310</td>
</tr>
<tr>
<td>Referer</td>
<td>-</td>
</tr>
<tr>
<td>用户代理</td>
<td>“Mozilla/5.0(Macintosh；英特尔Mac OS X 10_15_4) AppleWebKit/537.36（KHTML，如Gecko） Chrome/81.0.4044.122 Safari/537.36”</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web Server访问日志 {#configuring-the-apache-httpd-webs-server-access-log}

此日志无法在AEMas a Cloud Service中进行配置。

## Apache HTTPD Web Server错误日志 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server错误日志为发布层的Web服务器/Dispatcher中的每个错误提供语句。

请参阅中有关错误日志格式的信息 [官方apache文档](https://httpd.apache.org/docs/2.4/logs.html#errorlog).

**示例日志输出**

```
Fri Jul 17 02:19:48.093820 2020 [mpm_worker:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00292: Apache/2.4.43 (Unix) Communique/4.3.4-20200424 mod_qos/11.63 configured -- resuming normal operations
Fri Jul 17 02:19:48.093874 2020 [core:notice] [pid 1:tid 140272153361288] [cm-p1234-e30226-aem-publish-b86c6b466-b9427] AH00094: Command line: 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D ENVIRONMENT_PROD'
Fri Jul 17 02:29:34.517189 2020 [mpm_worker:notice] [pid 1:tid 140293638175624] [cm-p1234-e30226-aem-publish-b496f64bf-5vckp] AH00295: caught SIGTERM, shutting down
```

**日志格式**

<table>
<tbody>
<tr>
<td>日期和时间</td>
<td>2017年7月17日星期五02:16:42.608913 2020</td>
</tr>
<tr>
<td>事件级别</td>
<td>[mpm_worker：notice]</td>
</tr>
<tr>
<td>进程ID</td>
<td>[pid 1：tid 140715149343624]</td>
</tr>
<tr>
<td>Pod名称</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>消息</td>
<td>AH00094：命令行： 'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web Server错误日志 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日志级别由文件中的变量REWRITE_LOG_LEVEL定义 `conf.d/variables/global.var`.

可将其设置为error 、 warn 、 info 、 debug和trace1 - trace8 ，默认值为warn。 要调试RewriteRules，建议将日志级别提升为trace2。

请参阅 [mod_rewrite模块文档](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) 了解更多信息。

要为每个环境设置日志级别，请在global.var文件中使用相应的条件分支，如下所述：

```
Define REWRITE_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL error
  ...
</IfDefine>
```

## Dispatcher日志 {#dispatcher-log}

**示例**

```
[17/Jul/2020:23:48:06 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures.html" - 475ms [publishfarm/0] [action miss] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/climbing-new-zealand/_jcr_content/root/responsivegrid/carousel/item_1571266094599.coreimg.jpeg/1473680817282/sport-climbing.jpeg" 302 10ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
[17/Jul/2020:23:48:07 +0000] [I] [cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr] "GET /content/wknd/us/en/adventures/ski-touring-mont-blanc/_jcr_content/root/responsivegrid/carousel/item_1571168419252.coreimg.jpeg/1572047288089/adobestock-238230356.jpeg" 302 11ms [publishfarm/0] [action none] "publish-p12904-e25628.adobeaemcloud.com"
```

**日志格式**

<table>
<tbody>
<tr>
<td>日期和时间</td>
<td>[2020年7月17日:23:48:16 +0000]</td>
</tr>
<tr>
<td>面板名称</td>
<td>[cm-p12904-e25628-aem-publish-6c5f7c9dbd-mzcvr]</td>
</tr>
<tr>
<td>协议</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>Dispatcher响应状态代码</td>
<td>/content/experience-fragments/wknd/language-masters/en/contributors/sofia-sjoeberg/master/_jcr_content/root/responsivegrid/image.coreimg.100.500.jpeg/1572236359031/ayo-ogunseinde-237739.jpeg</td>
</tr>
<tr>
<td>持续时间</td>
<td>1949 毫秒</td>
</tr>
<tr>
<td>场</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>缓存状态</td>
<td>[操作失败]</td>
</tr>
<tr>
<td>主机</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### 配置Dispatcher错误日志 {#configuring-the-dispatcher-error-log}

调度程序日志级别由文件中的变量DISP_LOG_LEVEL定义 `conf.d/variables/global.var`.

可将其设置为error 、 warn 、 info 、 debug和trace1 ，默认值为warn。

虽然Dispatcher日志记录支持其他多个级别的日志记录粒度，但AEMas a Cloud Service建议使用以下描述的级别。

要为每个环境设置日志级别，请在 `global.var` 文件，如下所述：

```
Define DISP_LOG_LEVEL debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL error
  ...
</IfDefine>
```

>[!NOTE]
>
>对于AEMas a Cloud Service环境，debug是最高详细级别。 不支持跟踪日志级别，因此您应避免在云环境中工作时设置跟踪日志级别。

## 如何访问日志 {#how-to-access-logs}

### 云环境 {#cloud-environments}

可以通过Cloud Manager界面下载或者使用Adobe I/O命令行界面在命令行跟踪日志，来访问AEM云服务的as a Cloud Service日志。 欲了解更多信息，请参见 [Cloud Manager日志记录文档](/help/implementing/cloud-manager/manage-logs.md).

### 本地 SDK {#local-sdk}

AEMas a Cloud ServiceSDK提供日志文件以支持本地开发。

AEM日志位于文件夹中 `crx-quickstart/logs`，可以查看以下日志：

* AEM Java日志： `error.log`
* AEM HTTP请求日志： `request.log`
* AEM HTTP访问日志： `access.log`

Apache层日志（包括Dispatcher）位于包含Dispatcher的Docker容器中。 请参阅 [Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) 有关如何启动Dispatcher的信息。

要检索日志，请执行以下操作：

1. 在命令行中，键入 `docker ps` 列出容器
1. 要登录到容器，请键入&#39;&#39;`docker exec -it <container> /bin/sh`“”，其中 `<container>` 是上一步中的Dispatcher容器ID
1. 导航到下的缓存根 `/mnt/var/www/html`
1. 日志位于 `/etc/httpd/logs`
1. Inspect日志：这些日志可在XYZ文件夹下访问，在其中可以查看以下日志：
   * Apache HTTPD Web服务器访问日志 —  `httpd_access.log`
   * Apache HTTPD Web Server错误日志 —  `httpd_error.log`
   * Dispatcher日志 —  `dispatcher.log`

日志也直接打印到终端输出上。 大多数情况下，这些日志应该是DEBUG，可通过在运行Docker时作为Debug参数传递调试级别来实现。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 调试生产和暂存 {#debugging-production-and-stage}

在特殊情况下，需要更改日志级别，以便在暂存或生产环境中以更精细的粒度进行记录。

虽然这是可能的，但需要更改Git中配置文件的日志级别（从Warn和Error更改为Debug ），并执行部署到AEMas a Cloud Service以向环境注册这些配置更改。

根据Debug写入的流量和日志语句的数量，这可能会导致对环境的性能产生不利影响，因此，建议对暂存和生产调试级别进行以下更改：

* 谨慎行事，而且只在绝对必要的时候
* 恢复到相应的级别并尽快重新部署

## Splunk日志 {#splunk-logs}

拥有Splunk帐户的客户可以通过客户支持票证请求将其AEM Cloud Service日志转发到相应的索引。 日志记录数据等同于通过Cloud Manager日志下载提供的数据，但客户可能会发现使用Splunk产品中提供的查询功能很方便。

与发送到Splunk的日志关联的网络带宽被视为客户网络I/O使用的一部分。

### 启用Splunk转发 {#enabling-splunk-forwarding}

在支持请求中，客户应说明：

* Splunk HEC终结点地址。 此端点必须具有有效的SSL证书并且可以公开访问。
* Splunk索引
* Splunk端口
* Splunk HEC令牌。 参见 [此页面](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) 了解更多信息。

应为每个相关的程序/环境类型组合指定上述属性。 例如，如果客户需要开发、暂存和生产环境，他们应提供三组信息，如下所示。

>[!NOTE]
>
>不支持沙盒程序环境的Splunk转发。

>[!NOTE]
>
>无法对专用出口 IP 地址使用 Splunk 转发功能。

您应确保初始请求除了暂存/生产环境之外，还包括所有应该启用的开发环境。 Splunk必须具有SSL证书，并且是面向公众的。

如果在初始请求后创建的任何新开发环境打算启用Splunk转发，但未启用它，则应提出其他请求。

另请注意，如果请求了开发环境，则不在请求甚至沙盒环境中的其他开发环境可能会启用Splunk转发，并且将共享Splunk索引。 客户可以使用 `aem_env_id` 用于区分这些环境的字段。

下面是一个示例客户支持请求：

方案123，生产环境

* Splunk HEC终结点地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123prod（客户可以选择所需的任何命名约定）
* Splunk端口：443
* Splunk HEC令牌： ABC123

123号方案，Stage Env

* Splunk HEC终结点地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123stage
* Splunk端口：443
* Splunk HEC令牌： ABC123

项目123，开发环境

* Splunk HEC终结点地址： `splunk-hec-ext.acme.com`
* Splunk索引：acme_123dev
* Splunk端口：443
* Splunk HEC令牌： ABC123

对于每个环境使用相同的Splunk索引可能就足够了，在这种情况下，可以 `aem_env_type` 字段可用于根据值dev、stage和prod进行区分。 如果有多个开发环境， `aem_env_id` 字段也可使用。 如果关联的索引限制访问缩减的Splunk用户集，则某些组织可能会为生产环境的日志选择单独的索引。

以下是示例日志条目：

```
aem_env_id: 1242
aem_env_type: dev
aem_program_id: 12314
aem_tier: author
file_path: /var/log/aem/error.log
host: 172.34.200.12 
level: INFO
msg: [FelixLogListener] com.adobe.granite.repository Service [5091, [org.apache.jackrabbit.oak.api.jmx.SessionMBean]] ServiceEvent REGISTERED
orig_time: 16.07.2020 08:35:32.346
pod_name: aemloggingall-aem-author-77797d55d4-74zvt
splunk_customer: true
```
