---
title: AEM as a Cloud Service的日志记录
description: 了解如何使用AEM as a Cloud Service的日志记录功能配置中央日志记录服务的全局参数、各个服务的特定设置以及如何请求数据日志记录。
exl-id: 262939cc-05a5-41c9-86ef-68718d2cd6a9
feature: Log Files, Developing
role: Admin, Architect, Developer
source-git-commit: 7efbdecdddb66611cbde0dc23928a61044cc96d5
workflow-type: tm+mt
source-wordcount: '2377'
ht-degree: 9%

---

# AEM as a Cloud Service的日志记录 {#logging-for-aem-as-a-cloud-service}

AEM as a Cloud Service是一个平台，客户可以在此平台上包含自定义代码，以便为其客户群创建独特的体验。 有鉴于此，日志记录服务是一个关键功能，可用于调试和了解在本地开发和云环境(特别是AEM as a Cloud Service的开发环境)中代码的执行情况。

AEM as a Cloud Service日志记录和日志级别在配置文件中进行管理，这些配置文件作为AEM项目的一部分存储在Git中，并通过Cloud Manager部署为AEM项目的一部分。 AEM as a Cloud Service中的日志记录可以划分为三个逻辑集：

* AEM日志记录，在AEM应用程序级别执行日志记录
* Apache HTTPD Web Server/Dispatcher日志记录，用于在发布层上执行Web服务器和Dispatcher的日志记录。
* CDN日志记录（如其名称所示）在CDN上执行日志记录。

## AEM日志记录 {#aem-logging}

AEM应用程序级别的日志记录由三个日志处理：

1. AEM Java日志，用于呈现AEM应用程序的Java日志记录语句。
1. HTTP请求日志，用于记录有关AEM提供的HTTP请求及其响应的信息
1. HTTP访问日志，用于记录由AEM提供的汇总信息和HTTP请求

>[!NOTE]
>
>从发布层的Dispatcher缓存或上游CDN提供的HTTP请求不会反映在这些日志中。

## AEM Java日志记录 {#aem-java-logging}

AEM as a Cloud Service提供对Java log语句的访问。 AEM应用程序的开发人员应遵循常规Java日志记录最佳实践，在以下日志级别记录有关自定义代码执行的相关声明：

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
当DEBUG日志记录处于活动状态时，将记录语句，以清楚地了解所发生的活动以及影响处理的任何关键参数。</td>
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
描述有可能变为错误的情况。<br>
当WARN日志记录处于活动状态时，只记录指示接近次优的条件语句。</td>
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
描述指示失败并需要解决的情况。<br>
当ERROR日志记录处于活动状态时，只记录指示失败的语句。 错误日志语句指示应尽快解决的严重问题。</td>
<td>
<ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
<li>生产</li>
</ul></td>
</tr>
</table>

虽然Java日志记录支持若干其他级别的日志记录粒度，但AEM as a Cloud Service建议使用上述三个级别。

AEM日志级别是通过OSGi配置为每个环境类型设置的，这反过来会提交到Git，并通过Cloud Manager部署到AEM as a Cloud Service。 因此，最好保持日志语句一致且对于环境类型是众所周知的，以确保通过AEM as Cloud Service提供的日志在最佳日志级别可用，而无需使用更新的日志级别配置重新部署应用程序。

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
<td>AEM as a Cloud Service节点ID</td>
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
<td>未指定审批者，默认为[ Creative审批者用户组]</td>
</tr>
</tbody>
</table>

### 配置记录器 {#configuration-loggers}

AEM Java日志被定义为OSGi配置，因此使用运行模式文件夹定位特定AEM as a Cloud Service环境。

通过Sling LogManager工厂的OSGi配置为自定义Java包配置Java日志记录。 有三种受支持的配置属性：

| OSGi配置属性 | 描述 |
|---|---|
| `org.apache.sling.commons.log.names` | 要为其收集log语句的Java包。 |
| `org.apache.sling.commons.log.level` | `org.apache.sling.commons.log.names`指定的记录Java包的日志级别 |
| `org.apache.sling.commons.log.file` | 指定输出的目标： `logs/error.log` |

更改其他LogManager OSGi配置属性可能会导致AEM as a Cloud Service中出现可用性问题。

以下是三种AEM as a Cloud Service环境类型的推荐日志记录配置示例（使用`com.example`的占位符Java包）。

### 开发 {#development}

/apps/my-app/config/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "debug"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### 暂存 {#stage}

/apps/my-app/config.stage/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "warn"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

### 生产 {#productiomn}

/apps/my-app/config.prod/org.apache.sling.commons.log.LogManager.factory.config-example.cfg.json

```
{
    "org.apache.sling.commons.log.names": ["com.example"],
    "org.apache.sling.commons.log.level": "error"
    "org.apache.sling.commons.log.file": "logs/error.log"
}
```

## AEM HTTP请求日志记录 {#aem-http-request-logging}

AEM as a Cloud Service的HTTP请求日志记录可按时间顺序将insight添加到向AEM发出的HTTP请求及其HTTP响应。 此日志有助于了解向AEM发出的HTTP请求以及处理和响应这些请求的顺序。

了解此日志的关键是按其ID映射HTTP请求和响应对，这些ID由括号中的数值表示。 请求及其相应响应在日志中通常具有其他HTTP请求和响应。

**示例日志**

```
29/Apr/2020:19:14:21 +0000 [137] > POST /conf/global/settings/dam/adminui-extension/metadataprofile/ HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
...
29/Apr/2020:19:14:22 +0000 [139] > GET /mnt/overlay/dam/gui/content/processingprofilepage/metadataprofiles/editor.html/conf/global/settings/dam/adminui-extension/metadataprofile/main HTTP/1.1 [cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]
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
<td>/conf/global/settings/dam/adminui-extension/metadataprofile/</td>
</tr>
<tr>
<td>协议</td>
<td>HTTP/1.1
</td>
</tr>
<tr>
<td>AEM as a Cloud Service节点ID</td>
<td>[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日志 {#configuring-the-log}

无法在AEM as a Cloud Service中配置AEM HTTP请求日志。

## AEM HTTP访问日志记录 {#aem-http-access-logging}

AEM as Cloud Service HTTP访问日志记录按时间顺序显示HTTP请求。 每个日志条目表示访问AEM的HTTP请求。

此日志有助于快速了解向AEM发出的哪些HTTP请求（如果这些请求通过查看随附的HTTP响应状态代码成功）以及HTTP请求完成所用的时间。 通过按用户筛选日志条目，此日志还有助于调试特定用户的活动。

**示例日志输出**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

| AEM as a Cloud Service节点ID | cm-p1235-e2644-aem-author-59555cb5b8-8kgr2 |
|---|---|
| 客户端的IP地址 | - |
| 用户 | myuser@adobe.com |
| 日期和时间 | 2020年4月30日:17:37:14 +0000 |
| HTTP方法 | GET |
| URL | `/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css` |
| 协议 | HTTP/1.1 |
| HTTP响应状态 | 200 |
| 响应正文的大小（以字节为单位） | 1141 |
| 反向链接 | `"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"` |
| 用户代理 | `"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"` |

### 配置HTTP访问日志 {#configuring-the-http-access-log}

无法在AEM as a Cloud Service中配置HTTP访问日志。

## Apache Web Server和Dispatcher日志记录 {#apache-web-server-and-dispatcher-logging}

AEM as a Cloud Service在发布上为Apache Web Server和Dispatcher层提供三个日志：

* Apache HTTPD Web Server访问日志
* Apache HTTPD Web Server错误日志
* Dispatcher日志

这些日志仅适用于发布层。

这组日志提供了在向AEM as a Cloud Service发布层发送HTTP请求以访问AEM应用程序之前的见解。 这一点非常重要，因为理想情况下，对发布层服务器的大多数HTTP请求都由Apache HTTPD Web Server和AEM Dispatcher缓存的内容提供，并且永远不会访问AEM应用程序本身。 因此，AEM的Java、请求或访问日志中不包含这些请求的日志语句。

### Apache HTTPD Web Server访问日志 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server访问日志为到达发布层的Web服务器/Dispatcher的每个HTTP请求提供语句。 从上游CDN提供的请求不会反映在这些日志中。

请参阅[官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#accesslog)中有关错误日志格式的信息。

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
<td>反向链接</td>
<td>-</td>
</tr>
<tr>
<td>用户代理</td>
<td>“Mozilla/5.0(Macintosh；英特尔Mac OS X 10_15_4) AppleWebKit/537.36（KHTML，如Gecko） Chrome/81.0.4044.122 Safari/537.36”</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web Server访问日志 {#configuring-the-apache-httpd-webs-server-access-log}

此日志无法在AEM as a Cloud Service中进行配置。

## Apache HTTPD Web Server错误日志 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server错误日志为发布层的Web服务器/Dispatcher中的每个错误提供语句。

请参阅[官方Apache文档](https://httpd.apache.org/docs/2.4/logs.html#errorlog)中有关错误日志格式的信息。

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
<td>2020年7月17日星期五02:16:42.608913</td>
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

mod_rewrite日志级别由文件`conf.d/variables/global.var`中的变量REWRITE_LOG_LEVEL定义。

可将其设置为error、warn、info、debug和trace1 - trace8，默认值为warn。 要调试RewriteRules，建议将日志级别提升为trace2。 建议使用[Dispatcher SDK](../../dispatcher/validation-debug.md)调试重写规则。 AEM as a Cloud Service的最大日志级别为`debug`。 因此，当前不可能在云中有效调试重写规则。

有关详细信息，请参阅[mod_rewrite模块文档](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging)。

要为每个环境设置日志级别，请使用global.var文件中相应的条件分支，如下所述：

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
<td>1949毫秒</td>
</tr>
<tr>
<td>场</td>
<td>[publishfarm/0]</td>
</tr>
<tr>
<td>缓存状态</td>
<td>[操作未命中]</td>
</tr>
<tr>
<td>主机</td>
<td>"publish-p12904-e25628.adobeaemcloud.com"</td>
</tr>
</tbody>
</table>

### 配置Dispatcher错误日志 {#configuring-the-dispatcher-error-log}

调度程序日志级别由文件`conf.d/variables/global.var`中的变量DISP_LOG_LEVEL定义。

可将其设置为error 、 warn 、 info 、 debug和trace1 ，默认值为warn。

虽然Dispatcher日志记录支持几个其他级别的日志记录粒度，但AEM as a Cloud Service建议使用以下所述的级别。

要为每个环境设置日志级别，请在`global.var`文件中使用相应的条件分支，如下所述：

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
>对于AEM as a Cloud Service环境，debug是最高详细级别。 不支持跟踪日志级别，因此当在云环境中工作时，应避免设置跟踪日志级别。

## CDN日志 {#cdn-log}

AEM as a Cloud Service提供对CDN日志的访问，这些日志对于包括缓存命中率优化在内的用例非常有用。 无法自定义CDN日志格式，并且没有将其设置为不同模式（例如“信息”、“警告”或“错误”）的概念。

**示例**

```
{
"timestamp": "2023-05-26T09:20:01+0000",
"ttfb": 19,
"cli_ip": "147.160.230.112",
"cli_country": "CH",
"rid": "974e67f6",
"req_ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.3 Safari/605.1.15",
"host": "example.com",
"url": "/content/hello.png",
"method": "GET",
"res_ctype": "image/png",
"cache": "PASS",
"status": 200,
"res_age": 0,
"pop": "PAR",
"rules": "match=Enable-SQL-Injection-and-XSS-waf-rules-globally,waf=SQLI,action=blocked"
}
```

**日志格式**

CDN日志不同于其他日志，它遵循JSON格式。

| **字段名** | **描述** |
|---|---|
| *timestamp* | TLS 终止后请求开始的时间 |
| *ttfb* | *首字节时间*&#x200B;的缩写。从请求开始到响应正文开始流式传输之前的时间间隔。 |
| *cli_ip* | 客户端 IP 地址。 |
| *cli_country* | 客户国家/地区的两字母 [ISO 3166-1](https://zh.wikipedia.org/wiki/cn/ISO_3166-1) alpha-2 国家/地区代码。 |
| *rid* | 用于唯一标识请求的请求头的值。 |
| *req_ua* | 负责发出给定 HTTP 请求的用户代理。 |
| *host* | 请求所针对的颁发机构。 |
| *url* | 完整路径，包括查询参数。 |
| *method* | 客户端发送的 HTTP 方法，例如“GET”或“POST”。 |
| *res_ctype* | 用于指示资源的原始媒体类型的 Content-Type。 |
| *cache* | 缓存的状态。可能的值为 HIT、MISS 或 PASS |
| *status* | 整数值形式的 HTTP 状态代码。 |
| *res_age* | 响应已缓存（在所有节点中）的时间量（以秒为单位）。 |
| *pop* | CDN 缓存服务器的数据中心。 |
| *rules* | 任何匹配的[流量过滤器规则](/help/security/traffic-filter-rules-including-waf.md)和WAF标志的名称，也指示匹配是否导致阻塞。 如果没有匹配的规则，则为空。 |

可以使用[请求/响应转换](/help/implementing/dispatcher/cdn-configuring-traffic.md#logproperty)用您自己的属性扩展CDN日志。

## 如何访问日志 {#how-to-access-logs}

### 云环境 {#cloud-environments}

可通过以下方式访问云服务的AEM as a Cloud Service日志：通过Cloud Manager界面下载，或者使用Adobe I/O命令行界面在命令行跟踪日志。 有关详细信息，请参阅[Cloud Manager日志记录文档](/help/implementing/cloud-manager/manage-logs.md)。

### 其他发布区域的日志 {#logs-for-additional-publish-regions}

如果为特定环境启用了其他发布区域，则可以从Cloud Manager下载每个区域的日志，如上所述。

其他发布区域的AEM日志和Dispatcher日志将在环境ID之后的前3个字母中指定该区域，以下示例中的&#x200B;**nld2**&#x200B;就是一个例子，它是指位于荷兰的其他AEM发布实例：

```
cm-p7613-e12700-nld2-aem-publish-bcbb77549-5qmmt 127.0.0.1 - 07/Nov/2023:23:57:11 +0000 "HEAD /libs/granite/security/currentuser.json HTTP/1.1" 200 - "-" "Java/11.0.19"
```

### 本地 SDK {#local-sdk}

AEM as a Cloud Service SDK提供日志文件以支持本地开发。

AEM日志位于文件夹`crx-quickstart/logs`中，可以在其中查看以下日志：

* AEM Java日志： `error.log`
* AEM HTTP请求日志： `request.log`
* AEM HTTP访问日志： `access.log`

Apache层日志（包括Dispatcher）位于保存Dispatcher的Docker容器中。 有关如何启动Dispatcher的信息，请参阅[Dispatcher文档](/help/implementing/dispatcher/disp-overview.md)。

要检索日志，请执行以下操作：

1. 在命令行中，键入`docker ps`以列出容器
1. 要登录到容器，请键入“`docker exec -it <container> /bin/sh`”，其中`<container>`是上一步骤中的调度程序容器ID
1. 导航到`/mnt/var/www/html`下的缓存根
1. 日志位于`/etc/httpd/logs`下
1. 检查日志：可以在XYZ文件夹下访问日志，在其中可以查看以下日志：
   * Apache HTTPD Web服务器访问日志 — `httpd_access.log`
   * Apache HTTPD Web Server错误日志 — `httpd_error.log`
   * Dispatcher日志 — `dispatcher.log`

日志也直接打印到终端输出上。 大多数情况下，这些日志应该为DEBUG，可通过在运行Docker时作为参数传递Debug级别来实现此目的。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 调试生产和暂存 {#debugging-production-and-stage}

在特殊情况下，需要更改日志级别，以便在暂存或生产环境中以更精细的粒度进行记录。

虽然这是可能的，但需要更改Git中配置文件的日志级别（从Warn和Error更改为Debug），并执行部署到AEM as a Cloud Service以将这些配置更改注册到环境中。

根据由Debug写入的流量和日志语句的数量，这可能会导致对环境的性能产生负面影响，因此，建议对暂存和生产调试级别进行以下更改：

* 谨慎行事，而且只在绝对必要时
* 恢复到适当级别并尽快重新部署

## 日志转发 {#log-forwarding}

虽然可以从Cloud Manager下载日志，但一些组织认为将这些日志转发到首选日志记录目标比较有利。 AEM支持将日志流式传输到以下目标：

* Azure Blob存储
* Datadog
* HTTPD
* Elasticsearch（和OpenSearch）
* Splunk

有关如何配置此功能的详细信息，请参阅[日志转发文章](/help/implementing/developing/introduction/log-forwarding.md)。

>[!NOTE]
>
>不支持沙盒程序环境的日志转发。
