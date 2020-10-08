---
title: 记录
description: 了解如何为中央日志记录服务配置全局参数、单个服务的特定设置或如何请求数据记录。
translation-type: tm+mt
source-git-commit: 0b648e1a0da141f8393c62cb269e5498e2ecd23f
workflow-type: tm+mt
source-wordcount: '2219'
ht-degree: 3%

---


# 记录 {#logging}

AEM作为Cloud Service，是客户包含自定义代码的平台，可为客户群创建独特的体验。 考虑到这一点，日志记录是调试和了解本地开发和云环境(特别是AEM作为Cloud Service的开发环境)上的代码执行的关键功能。

AEM日志记录和日志级别在配置文件中进行管理，这些配置文件作为AEM项目的一部分存储在Git中，并通过云管理器部署为AEM项目的一部分。 以Cloud Service身份登录AEM可以分为两个逻辑集：

* AEM日志记录，在AEM应用程序级别执行日志记录
* Apache HTTPD Web Server/Dispatcher日志记录，它在发布层执行Web服务器和Dispatcher的日志记录。

## AEM日志记录 {#aem-loggin}

在AEM应用程序级别进行日志记录，由三个日志处理：

1. AEM Java日志，它为AEM应用程序呈现Java日志记录语句。
1. HTTP请求日志，它记录AEM提供的有关HTTP请求及其响应的信息
1. HTTP访问日志，它记录AEM提供的信息和HTTP请求的摘要

>[!NOTE]
>
>从发布层的Dispatcher缓存或上游CDN提供的HTTP请求不会反映在这些日志中。

## AEM Java日志记录 {#aem-java-logging}

AEM作为Cloud Service提供对Java日志语句的访问。 AEM应用程序的开发人员应按照常规的Java日志记录最佳实践，在以下日志级别记录有关自定义代码执行的相关语句：

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
描述应用程序中正在发生的情况。<br>
当DEBUG日志记录处于活动状态时，将记录提供发生活动的清晰画面的语句以及影响处理的任何关键参数。</td>
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
描述可能成为错误的条件。<br>
当WARN日志记录处于活动状态时，只记录指示正在接近次优性的条件语句。</td>
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
描述指示故障并需要解决的条件。<br>
当ERROR日志记录处于活动状态时，只记录指示失败的语句。 ERROR日志语句表示出现严重问题，应尽快解决。</td>
<td>
<ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
<li>生产</li>
</ul></td>
</tr>
</table>

虽然Java日志记录支持其他几个级别的日志记录粒度，但AEM作为Cloud Service建议使用上述三个级别。

AEM日志级别通过OSGi配置按环境类型设置，OSGi配置又提交到Git，并通过云管理器部署到AEM作为Cloud Service。 因此，最好保持日志语句的一致性并保持环境类型的知名度，以确保通过AEM作为Cloud Service提供的日志在最佳日志级别可用，而无需使用更新的日志级别配置重新部署应用程序。

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
<td>AEM作为Cloud Service节点ID</td>
<td>[cm-p1234-e5678-aem-author-5955cb5b8-q7l9s]</td>
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
<td>没有指定的批准者，默认使用[Creative Approvers用户组]</td>
</tr>
</tbody>
</table>

### 配置记录器 {#configuration-loggers}

AEM Java日志定义为OSGi配置，因此将特定AEM目标为使用运行模式文件夹的Cloud Service环境。

通过Sling LogManager工厂的OSGi配置为自定义Java包配置Java日志记录。 支持两种配置属性：

| OSGi配置属性 | 描述 |
|---|---|
| org.apache.sling.commons.log.names | 要为其收集日志语句的Java包。 |
| org.apache.sling.commons.log.level | 记录Java包的日志级别，由org.apache.sling.commons.log.names指定 |

更改其他LogManager OSGi配置属性可能会导致AEM作为Cloud Service的可用性问题。

以下是三个AEM的推荐日志记录配置(使用占位符Java包 `com.example`)的示例，它们作为Cloud Service环境类型。

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

## AEM HTTP请求记录 {#aem-http-request-logging}

AEM作为Cloud Service的HTTP请求日志记录，可以按时间顺序对发送给AEM的HTTP请求及其HTTP响应进行深入的了解。 此日志有助于了解对AEM发出的HTTP请求以及它们的处理和响应顺序。

理解此日志的关键是用ID映射HTTP请求和响应对，用括号中的数值表示。 请注意，通常请求及其相应响应会在日志中插入其他HTTP请求和响应。

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
<td>2020年4月29日：19:14:21 +000</td>
</tr>
<tr>
<td>请求／响应对ID</td>
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
<td>AEM作为Cloud Service节点ID</td>
<td>[cm-p1234-e5678-aem-author-5955cb5b8-q7l9s]</td>
</tr>
</tbody>
</table>

### 配置日志 {#configuring-the-log}

在AEM中，AEM HTTP请求日志不能配置为Cloud Service。

## AEM HTTP访问记录 {#aem-http-access-logging}

AEM asCloud ServiceHTTP访问记录按时间顺序显示HTTP请求。 每个日志条目表示访问AEM的HTTP请求。

如果AEM通过查看随附的HTTP响应状态代码获得成功，以及HTTP请求完成所用的时间，此日志有助于快速了解向发出的HTTP请求。 此日志还有助于通过按用户筛选日志条目来调试特定用户的活动。

**日志输出示例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

**日志格式**

<table>
<tbody>
<tr>
<td>AEM作为Cloud Service节点ID</td>
<td>cm-p1235-e2644-aem-author-5955cb5b8-8kgr2</td>
</tr>
<tr>
<td>客户端的IP地址</td>
<td>-</td>
</tr>
<tr>
<td>用户</td>
<td>myuser@adobe.com</td>
</tr>
<tr>
<td>日期和时间</td>
<td>2020年4月30日：17:37:14 +0000</td>
</tr>
<tr>
<td>HTTP方法</td>
<td>GET</td>
</tr>
<tr>
<td>URL</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
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
<td>HTTP请求时间（以毫秒为单位）</td>
<td>1141</td>
</tr>
<tr>
<td>引用</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
</tr>
<tr>
<td>用户代理</td>
<td>“Mozilla/5.0(Macintosh;Intel Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如Gecko）Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### 配置HTTP访问日志 {#configuring-the-http-access-log}

在AEM中，HTTP访问日志不能配置为Cloud Service。

## Apache Web Server和调度程序日志记录 {#apache-web-server-and-dispatcher-logging}

AEM as aCloud Service在发布中为Apache Web Server和调度程序层提供三个日志：

* Apache HTTPD Web Server访问日志
* Apache HTTPD Web Server错误日志
* 调度程序日志

请注意，这些日志仅对发布层可用。

此日志集提供对AEM的HTTP请求的洞察，在这些请求到达AEM应用程序之前，将其作为Cloud Service发布层。 理想情况下，大多数发布层服务器的HTTP请求都由Apache HTTPD Web Server和AEM Dispatcher缓存的内容提供，并且永远无法到达AEM应用程序本身，这一点很重要。 因此，AEM Java、请求或访问日志中没有这些请求的日志语句。

### Apache HTTPD Web Server访问日志 {#apache-httpd-web-server-access-log}

Apache HTTP Web Server访问日志为到达发布层的Web服务器／调度程序的每个HTTP请求提供语句。 请注意，从上游CDN提供的请求不会反映在这些日志中。

请参阅官方apache文档中的错误日志 [格式的相关信息](https://httpd.apache.org/docs/2.4/logs.html#accesslog)。

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
<td>AEM作为云服务节点ID</td>
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
<td>2020年5月01日：00:09:46 +0000</td>
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
<td>“Mozilla/5.0(Macintosh;Intel Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如Gecko）Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web Server访问日志 {#configuring-the-apache-httpd-webs-server-access-log}

此日志在AEM中不能配置为Cloud Service。

## Apache HTTPD Web Server错误日志 {#apache-httpd-web-server-error-log}

Apache HTTP Web Server错误日志为发布层的Web服务器／调度程序中的每个错误提供语句。

请参阅官方apache文档中的错误日志 [格式的相关信息](https://httpd.apache.org/docs/2.4/logs.html#errorlog)。

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
<td>周五7月17日02:16:42.608913 2020</td>
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
<td>窗格名称</td>
<td>[cm-p1234-e56789-aem-publish-b86c6b466-qpfvp]</td>
</tr>
<tr>
<td>消息</td>
<td>AH00094:命令行：'httpd -d /etc/httpd -f /etc/httpd/conf/httpd.conf -D FOREGROUND -D </td>
</tr>
</tbody>
</table>

### 配置Apache HTTPD Web Server错误日志 {#configuring-the-apache-httpd-web-server-error-log}

mod_rewrite日志级别由文件中的变量REWRITE_LOG_LEVEL定义 `conf.d/variables/global.var`。

它可以设置为“错误”、“警告”、“信息”、“调试”和“跟踪1”-“跟踪8”，默认值为“警告”。 要调试RewriteRules，建议将日志级别提升到Trace2。

有关详 [细信息，请参阅mod_rewrite模块文档](https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging) 。

要设置每个环境的日志级别，请在global.var文件中使用相应的条件分支，如下所述：

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
<td>[2020年7月17日：23:48:16 +000]</td>
</tr>
<tr>
<td>窗格名称</td>
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
<td>1949ms</td>
</tr>
<tr>
<td>农场</td>
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

调度程序日志级别由文件中的变量DISP_LOG_LEVEL定义 `conf.d/variables/global.var`。

它可以设置为“错误”、“警告”、“信息”、“调试”和“跟踪1”，默认值为“警告”。

虽然调度程序日志记录支持其他几个级别的日志记录粒度，但AEM作为Cloud Service建议使用下面描述的级别。

要设置每个环境的日志级别，请在文件中使用相应的条 `global.var` 件分支，如下所述：

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

AEM作为云服务的Cloud Service日志，可通过Cloud Manager界面下载或使用AdobeI/O命令行界面跟踪命令行日志来访问。 有关详细信息，请参 [阅Cloud Manager日志记录文档](/help/implementing/cloud-manager/manage-logs.md)。

### 本地SDK {#local-sdk}

AEM作为Cloud ServiceSDK提供日志文件以支持本地开发。

AEM日志位于文件夹 `crx-quickstart/logs`中，可在该文件夹中查看以下日志：

* AEM Java日志： `error.log`
* AEM HTTP请求日志： `request.log`
* AEM HTTP访问日志： `access.log`

Apache层日志（包括调度程序）位于保存调度程序的Docker容器中。 有关如 [何开始](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html) Dispatcher的信息，请参阅Dispatcher文档。

要检索日志，请执行以下操作：

1. 在命令行中，键入 `docker ps` 以列表容器
1. 要登录容器，请键入“`docker exec -it <container> /bin/sh`”，其 `<container>` 中是上一步的调度程序容器ID
1. 导航到下面的缓存根 `/mnt/var/www/html`
1. 日志在 `/etc/httpd/logs`
1. Inspect:可以在文件夹XYZ下访问这些日志，在该文件夹中可以查看以下日志：
   * Apache HTTPD Web服务器访问日志- `httpd_access.log`
   * Apache HTTPD Web服务器错误日志- `httpd_error.log`
   * 调度程序日志- `dispatcher.log`

日志也直接打印到终端输出。 大多数情况下，这些日志应为DEBUG，这可以通过在运行Docker时以参数的形式传入调试级别来完成。 例如：

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

## 调试生产和舞台 {#debugging-production-and-stage}

在特殊情况下，需要更改日志级别，以在Stage或Production环境中以更精细的粒度进行日志记录。

尽管这是可能的，但它需要对Git中的配置文件中的日志级别从“警告”和“错误”更改为“调试”，并作为Cloud Service执行部署到AEM以向环境注册这些配置更改。

根据调试所编写的流量和日志语句的数量，这可能会对环境造成不利的性能影响，因此，建议对舞台和生产调试级别进行更改：

* 谨慎行事，只有在绝对必要时
* 还原到适当的级别并尽快重新部署

## 拆分日志 {#splunk-logs}

拥有Splunk帐户的客户可以通过客户支持票证请求将其AEMCloud Service日志转发到相应的索引。 日志记录数据等同于Cloud Manager日志下载中可用的数据，但客户可能会发现利用Splunk产品中提供的查询功能非常方便。

与发送到Splunk的日志关联的网络带宽被视为客户网络I/O使用的一部分。

### 启用跳转转发 {#enabling-splunk-forwarding}

在支持请求中，客户应指明：

* Splunk HEC端点地址
* Splunk指数
* 斯普隆克港
* Splunk HEC代号。 请参 [阅本页](https://docs.splunk.com/Documentation/Splunk/8.0.4/Data/HECExamples) ，了解详细信息。

应为每个相关项目/环境类型组合指定上述属性。  例如，如果客户需要开发、升级和生产环境，他们应提供三组信息，如下所示。

>[!NOTE]
>
>不支持沙箱项目环境的跳转转发。

您将在下面找到客户支持请求示例：

项目123，生产环境

* Splunk HEC端点地址： `splunk-hec-ext.acme.com`
* Splunk指数：acme_123prod（客户可以选择其希望的任何命名规范）
* Splunk端口：443
* Splunk HEC代号：ABC123

项目123，舞台环境

* Splunk HEC端点地址： `splunk-hec-ext.acme.com`
* Splunk指数：acme_123stage
* Splunk端口：443
* Splunk HEC代号：ABC123

项目123，开发人员

* Splunk HEC端点地址： `splunk-hec-ext.acme.com`
* Splunk指数：acme_123dev
* Splunk端口：443
* Splunk HEC代号：ABC123

对于每个环境都使用同一个Splunk索引可能已足够，在这种情况下，可以 `aem_env_type` 使用任一字段根据dev、stage和prod值进行区分。 如果有多个开发环境, `aem_env_id` 也可以使用该字段。 如果关联的索引限制对精简的Splunk用户集的访问，某些组织可能会为生产环境的日志选择单独的索引。

以下是一个日志条目示例：

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
