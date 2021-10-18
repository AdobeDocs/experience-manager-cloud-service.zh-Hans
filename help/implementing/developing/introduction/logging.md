---
title: 记录AEMas a Cloud Service
description: 了解如何使用AEM Logging为中央日志记录服务配置全局参数、各个服务的特定设置或如何请求数据记录。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
source-git-commit: 790feb2e43c60733a9f57062b014d67cc33ac2f9
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 2%

---

# 记录AEMas a Cloud Service {#logging-for-aem-as-a-cloud-service}

AEMas a Cloud Service是一个平台，可让客户包含自定义代码，以为其客户群创建独特体验。 考虑到这一点，日志记录服务是调试和了解本地开发和云环境(特别是AEMas a Cloud Service的开发环境)中代码执行的关键功能。

AEMas a Cloud Service日志记录设置和日志级别在配置文件中进行管理，这些配置文件作为AEM项目的一部分存储在Git中，并通过Cloud Manager部署为AEM项目的一部分。 登录AEMas a Cloud Service可以划分为两个逻辑集：

* AEM日志记录，在AEM应用程序级别执行日志记录
* Apache HTTPD Web Server/Dispatcher日志记录，用于在发布层上执行Web服务器和Dispatcher的日志记录。

## AEM日志记录 {#aem-logging}

AEM应用程序级别的日志记录由三个日志处理：

1. AEM Java日志，用于呈现AEM应用程序的Java日志记录语句。
1. HTTP请求日志，用于记录有关AEM提供的HTTP请求及其响应的信息
1. HTTP访问日志，记录AEM提供的汇总信息和HTTP请求

>[!NOTE]
>
>从发布层的Dispatcher缓存或上游CDN提供的HTTP请求不会反映在这些日志中。

## AEM Java日志记录 {#aem-java-logging}

AEM as a Cloud Service提供对Java log语句的访问。 AEM应用程序的开发人员应遵循以下日志级别的一般Java日志记录最佳实践，记录有关自定义代码执行的相关语句：

<table>
<tr>
<td>
<b>AEM Environment</b></td>
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
当DEBUG日志记录处于活动状态时，将记录提供活动发生情况以及影响处理的任何关键参数的清晰画面的语句。</td>
<td>
<ul>
<li> 地方发展</li>
<li>开发</li>
</ul></td>
</tr>
<tr>
<td>
暂存</td>
<td>
警告</td>
<td>
描述可能会出错的条件。<br>
当WARN日志记录处于活动状态时，只会记录指示接近次优性的条件语句。</td>
<td>
<ul>
<li> 地方发展</li>
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
描述指示失败且需要解决的条件。<br>
当错误日志记录处于活动状态时，只记录表示失败的语句。错误日志语句表示应尽快解决的严重问题。</td>
<td>
<ul>
<li> 地方发展</li>
<li>开发</li>
<li>暂存</li>
<li>生产</li>
</ul></td>
</tr>
</table>

虽然AEM日志记录支持其他几个级别的日志记录粒度，但Java日志as a Cloud Service建议使用上述三个级别。

AEM日志级别是通过OSGi配置按环境类型设置的，OSGi配置反过来会提交到Git，并通过Cloud Manager部署到AEMas a Cloud Service。 因此，最好保持日志语句一致且环境类型已知，以确保通过AEM作为Cloud Service提供的日志在最佳日志级别可用，而无需使用更新的日志级别配置重新部署应用程序。

**日志输出示例**

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
<td>AEMas a Cloud Service节点ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
<tr>
<td>日志级别</td>
<td>调试</td>
</tr>
<tr>
<td>线程</td>
<td>qtp2130572036-1472</td>
</tr>
<tr>
<td>Java类</td>
<td>com.example.approval.workflow.impl.CustomApprovalWorkflow</td>
</tr>
<tr>
<td>日志消息</td>
<td>没有指定的审批者，默认使用[ Creative Approvers用户组]</td>
</tr>
</tbody>
</table>

### 配置记录器 {#configuration-loggers}

AEM Java日志被定义为OSGi配置，因此可使用运行模式文件夹定位特定的AEMas a Cloud Service环境。

通过Sling LogManager工厂的OSGi配置为自定义Java包配置Java日志记录。 支持以下两个配置属性：

| OSGi配置属性 | 描述 |
|---|---|
| org.apache.sling.commons.log.names | 要收集日志语句的Java包。 |
| org.apache.sling.commons.log.level | 记录Java包的日志级别，由org.apache.sling.commons.log.names指定 |

更改其他LogManager OSGi配置属性可能会导致AEMas a Cloud Service中出现可用性问题。

以下是针对三种AEMas a Cloud Service环境类型推荐的日志记录配置示例（使用`com.example`的占位符Java包）。

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

AEMas a Cloud Service的HTTP请求日志记录可以深入分析对AEM发出的HTTP请求及其按时间顺序的HTTP响应。 此日志有助于了解对AEM发出的HTTP请求以及这些请求的处理和响应顺序。

了解此日志的键值是用ID映射HTTP请求和响应对，由括号中的数值表示。 请注意，请求及其相应响应通常会在日志中插入其他HTTP请求和响应。

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
<td>请求/响应对ID</td>
<td><code>[137]</code></td>
</tr>
<tr>
<td>HTTP 方法</td>
<td>POST</td>
</tr>
<tr>
<td>URL</td>
<td>/conf/global/settings/dam/adminui扩展/metadataprofile/</td>
</tr>
<tr>
<td>协议</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEMas a Cloud Service节点ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日志 {#configuring-the-log}

AEM HTTP请求日志在AEMas a Cloud Service中不可配置。

## AEM HTTP访问日志记录 {#aem-http-access-logging}

AEM asCloud ServiceHTTP访问日志记录按时间顺序显示HTTP请求。 每个日志条目表示用于访问AEM的HTTP请求。

此日志有助于快速了解向AEM发出的HTTP请求（如果通过查看随附的HTTP响应状态代码成功，以及HTTP请求完成所用的时间）。 此日志还有助于通过按用户筛选日志条目来调试特定用户的活动。

**日志输出示例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEMas a Cloud Service节点ID | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| 客户端的IP地址 | - |
| 用户 | myuser@adobe.com |
| 日期和时间 | 2020年4月30日:17:37:14 +0000 |
| HTTP方法 | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| 协议 | HTTP/1.1 |
| HTTP响应状态 | 200 |
| HTTP请求时间（以毫秒为单位） | 1141 |
| 引用 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| 用户代理 | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### 配置HTTP访问日志 {#configuring-the-http-access-log}

无法在AEMas a Cloud Service中配置HTTP访问日志。

## Apache Web Server和Dispatcher日志记录 {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service为Apache Web Server和Dispatcher层在发布上提供了三个日志：

* Apache HTTPD Web服务器访问日志
* Apache HTTPD Web服务器错误日志
* 调度程序日志

请注意，这些日志仅可用于发布层。

此日志集可在AEMas a Cloud Service发布层收到HTTP请求之前，对这些请求进行分析。 理想情况下，对发布层服务器的大多数HTTP请求都由Apache HTTPD Web Server和AEM Dispatcher缓存的内容提供，并且永远无法访问AEM应用程序本身，这一点非常重要。 因此，AEM Java、Request或Access日志中没有这些请求的log语句。

### Apache HTTPD Web服务器访问日志 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server访问日志为到达发布层的Web服务器/调度程序的每个HTTP请求提供语句。 请注意，来自上游CDN的请求不会反映在这些日志中。

请参阅[官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#accesslog)中有关错误日志格式的信息。

**日志输出示例**

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
<td>“Mozilla/5.0(Macintosh;英特尔Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如Gecko）Chrome/81.0.4044.122 Safari/537.36英寸</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web服务器访问日志 {#configuring-the-apache-httpd-webs-server-access-log}

无法在AEMas a Cloud Service中配置此日志。

## Apache HTTPD Web服务器错误日志 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server错误日志为发布层的Web服务器/调度程序中的每个错误提供语句。

请参阅[官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#errorlog)中有关错误日志格式的信息。

**日志输出示例**

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
<td>2020年7月17日星期五02:16:42.608913 2020</td>
</tr>
<tr>
<td>事件级别</td>
<td>[mpm_worker:notice]</td>
</tr>
<tr>
<td>进程ID</td>
<td>[pid 1:tid 140715149343624]</td>
</tr>
<tr>
<td>面板名称</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>消息</td>
<td>AH00094:命令行：'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D前台 — D </td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web服务器错误日志 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日志级别由文件`conf.d/variables/global.var`中的变量REWRITE_LOG_LEVEL定义。

它可以设置为Error、Warn、Info、Debug和Trace1 - Trace8，默认值为Warn。 要调试RewriteRules，建议将日志级别提升到Trace2。

有关更多信息，请参阅[mod_rewrite模块文档](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) 。

要为每个环境设置日志级别，请在global.var文件中使用相应的条件分支，如下所述：

```
Define REWRITE_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define REWRITE_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define REWRITE_LOG_LEVEL Error
  ...
</IfDefine>
```

## 调度程序日志 {#dispatcher-log}

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
<td>调度程序响应状态代码</td>
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
<td>[未决行动]</td>
</tr>
<tr>
<td>主机</td>
<td>"publish-p12904-e25628.adobeemcloud.com"</td>
</tr>
</tbody>
</table>

### 配置调度程序错误日志 {#configuring-the-dispatcher-error-log}

调度程序日志级别由文件`conf.d/variables/global.var`中的变量DISP_LOG_LEVEL定义。

它可以设置为“错误”、“警告”、“信息”、“调试”和“跟踪”1，其默认值为“警告”。

虽然AEM日志记录支持其他几个级别的日志记录粒度，但Dispatcheras a Cloud Service建议使用下述级别。

要设置每个环境的日志级别，请在`global.var`文件中使用相应的条件分支，如下所述：

```
Define DISP_LOG_LEVEL Debug
  
<IfDefine ENVIRONMENT_STAGE>
  ...
  Define DISP_LOG_LEVEL Warn
  ...
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  ...
  Define DISP_LOG_LEVEL Error
  ...
</IfDefine>
```

## 如何访问日志 {#how-to-access-logs}

### 云环境 {#cloud-environments}

AEM云服务的as a Cloud Service日志可以通过以下两种方式访问：通过Cloud Manager界面下载，或使用Adobe I/O命令行界面跟踪命令行上的日志。 有关更多信息，请参阅[Cloud Manager日志记录文档](/help/implementing/cloud-manager/manage-logs.md)。

### 本地 SDK {#local-sdk}

AEMas a Cloud ServiceSDK提供日志文件以支持本地开发。

AEM日志位于文件夹`crx-quickstart/logs`中，可在该文件夹中查看以下日志：

* AEM Java日志：`error.log`
* AEM HTTP请求日志：`request.log`
* AEM HTTP访问日志：`access.log`

Apache层日志（包括调度程序）位于包含调度程序的Docker容器中。 有关如何启动Dispatcher的信息，请参阅[Dispatcher文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

要检索日志，请执行以下操作：

1. 在命令行中，键入`docker ps`以列出容器
1. 要登录容器，请键入“`docker exec -it <container> /bin/sh`”，其中`<container>`是上一步中的调度程序容器id
1. 导航到`/mnt/var/www/html`下的缓存根
1. 日志位于`/etc/httpd/logs`下
1. Inspect日志：可在文件夹XYZ下访问这些日志，在该文件夹中可以查看以下日志：
   * Apache HTTPD Web服务器访问日志 — `httpd_access.log`
   * Apache HTTPD Web服务器错误日志 — `httpd_error.log`
   * 调度程序日志 — `dispatcher.log`

日志也直接打印到终端输出。 大多数情况下，这些日志应为DEBUG，在运行Docker时，可以通过将调试级别作为参数进行传递来完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 调试生产和暂存 {#debugging-production-and-stage}

在特殊情况下，需要更改日志级别，以便在暂存或生产环境中以更精细的粒度进行登录。

虽然这是可能的，但它需要对Git中配置文件中的日志级别从“警告”和“错误”更改为“调试”，然后执行到AEMas a Cloud Service的部署，以在环境中注册这些配置更改。

根据Debug编写的流量和日志语句的数量，这可能会对环境产生不利的性能影响，因此建议对暂存和生产调试级别进行以下更改：

* 要谨慎行事，而且必须绝对必要
* 还原到相应级别并尽快重新部署

## Splunk日志 {#splunk-logs}

拥有Splunk帐户的客户可以通过客户支持票证请求将其AEM Cloud Service日志转发到相应的索引。 日志记录数据等同于Cloud Manager日志下载中提供的内容，但客户可能会发现利用Splunk产品中提供的查询功能非常方便。

与发送到Splunk的日志关联的网络带宽被视为客户网络I/O使用的一部分。

### 启用Splunk转发 {#enabling-splunk-forwarding}

在支持请求中，客户应指示：

* Splunk HEC端点地址
* Splunk索引
* Splunk端口
* Splunk HEC令牌。 有关详细信息，请参阅[此页面](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples)。

应为每个相关的程序/环境类型组合指定上述属性。  例如，如果客户需要开发、暂存和生产环境，则他们应提供三组信息，如下所示。

>[!NOTE]
>
>不支持沙盒程序环境的Splunk转发。

除了暂存/生产环境外，您还应确保初始请求包含所有应启用的开发环境。

如果在初始请求后创建的任何新开发环境都打算启用Splunk转发，但未启用它，则应再发出一个请求。

另请注意，如果已请求开发环境，则请求中甚至不包含沙盒环境中的其他开发环境可能会启用Splunk转发，并将共享Splunk索引。 客户可以使用`aem_env_id`字段区分这些环境。

在下面，您将找到客户支持请求的示例：

程序123，生产环境

* Splunk HEC端点地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123prod（客户可以选择它希望的任何命名约定）
* Splunk端口：443
* Splunk HEC令牌：ABC123

程序123，阶段环境

* Splunk HEC端点地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123stage
* Splunk端口：443
* Splunk HEC令牌：ABC123

程序123，开发设备

* Splunk HEC端点地址：`splunk-hec-ext.acme.com`
* Splunk索引：acme_123dev
* Splunk端口：443
* Splunk HEC令牌：ABC123

对于每个环境使用相同的Splunk索引可能已足够，在这种情况下，可以使用`aem_env_type`字段根据dev、stage和prod值进行区分。 如果存在多个开发环境，则还可以使用`aem_env_id`字段。 如果关联的索引限制了对精简的Splunk用户集的访问，则某些组织可能会为生产环境的日志选择单独的索引。

以下是日志条目示例：

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
