---
title: 记录
description: 了解如何为中央日志记录服务配置全局参数、单个服务的特定设置或如何请求数据记录。
translation-type: tm+mt
source-git-commit: bbcadf29dbac89191a3a1ad31ee6721f8f57ef95
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 3%

---


# 记录 {#logging}

AEM作为Cloud Service，是客户包含自定义代码的平台，可为客户群创建独特的体验。 考虑到这一点，日志记录是调试和了解本地开发和云环境(特别是AEM作为Cloud Service的开发环境)上的代码执行的关键功能。

AEM日志记录和日志级别在配置文件中进行管理，这些配置文件作为AEM项目的一部分存储在Git中，并通过云管理器部署为AEM项目的一部分。 以Cloud Service身份登录AEM可以分为两个逻辑集：

* AEM日志记录，在AEM应用程序级别执行日志记录
* Apache HTTPD Web Server/Dispatcher记录，执行Web服务器的记录并在发布层Dispatcher。

## AEM日志记录 {#aem-loggin}

在AEM应用程序级别进行日志记录，由三个日志处理：

1. AEM Java日志，它为AEM应用程序呈现Java日志记录语句。
1. HTTP请求日志，它记录AEM提供的有关HTTP请求及其响应的信息
1. HTTP访问日志，它记录AEM提供的信息和HTTP请求的摘要

请注意，从发布层的Dispatcher缓存或上游CDN提供的HTTP请求不会反映在这些日志中。

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

### 日志格式 {#log-format}

| 日期和时间 | AEM作为Cloud ServiceID | 日志级别 | 线程 | Java类 | 日志消息 |
|---|---|---|---|---|---|
| 29.04.2020 21:50:13.398 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` | `*DEBUG*` | qtp2130572036-1472 | com.example.approval.workflow.impl.CustomApprovalWorkflow | `No specified approver, defaulting to [ Creative Approvers user group ]` |

**日志输出示例**

```
22.06.2020 18:33:30.120 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *ERROR* [qtp501076283-1809] io.prometheus.client.dropwizard.DropwizardExports Failed to get value from Gauge
22.06.2020 18:33:30.229 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [qtp501076283-1805] org.apache.sling.auth.core.impl.SlingAuthenticator getAnonymousResolver: Anonymous access not allowed by configuration - requesting credentials
22.06.2020 18:33:30.370 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] org.apache.sling.i18n.impl.JcrResourceBundle Finished loading 0 entries for 'en_US' (basename: <none>) in 4ms
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *INFO* [FelixLogListener] org.apache.sling.i18n Service [5126, [java.util.ResourceBundle]] ServiceEvent REGISTERED
22.06.2020 18:33:30.372 [cm-p12345-e6789-aem-author-86657cbb55-xrnzq] *WARN* [73.91.59.34 [1592850810364] GET /libs/granite/core/content/login.html HTTP/1.1] libs.granite.core.components.login.login$jsp j_reason param value 'unknown' cannot be mapped to a valid reason message: ignoring
```

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

### 日志格式 {#http-request-logging-format}

| 日期和时间 | 请求／响应对ID |  | HTTP 方法 | URL | 协议 | AEM作为Cloud Service节点ID |
|---|---|---|---|---|---|---|
| 2020年4月29日：19:14:21 +000 | `[137]` | -> | POST | /conf/global/settings/dam/adminui-extension/metadataprofile/ | HTTP/1.1 | `[cm-p1234-e5678-aem-author-59555cb5b8-q7l9s]` |

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

### 配置日志 {#configuring-the-log}

在AEM中，AEM HTTP请求日志不能配置为Cloud Service。

## AEM HTTP访问记录 {#aem-http-access-logging}

AEM asCloud ServiceHTTP访问记录按时间顺序显示HTTP请求。 每个日志条目表示访问AEM的HTTP请求。

如果AEM通过查看随附的HTTP响应状态代码获得成功，以及HTTP请求完成所用的时间，此日志有助于快速了解向发出的HTTP请求。 此日志还有助于通过按用户筛选日志条目来调试特定用户的活动。

### 日志格式 {#access-log-format}

<table>
<tbody>
<tr>
<td><b>AEM作为Cloud Service节点ID</b></td>
<td><b>客户端的IP地址</b></td>
<td><b>用户</b></td>
<td><b>日期和时间</b></td>
<td><b>空白</b></td>
<td><b>HTTP方法</b></td>
<td><b>URL</b></td>
<td><b>协议</b></td>
<td><b>空白</b></td>
<td><b>HTTP响应状态</b></td>
<td><b>HTTP响应时间（毫秒）</b></td>
<td><b>引用</b></td>
<td><b>用户代理</b></td>
</tr>
<tr>
<td>cm-p1235-e2644-aem-author-5955cb5b8-8kgr2</td>
<td>-</td>
<td>myuser@adobe.com</td>
<td>2020年4月30日：17:37:14 +0000</td>
<td>"</td>
<td>GET</td>
<td>/libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css</td>
<td>HTTP/1.1</td>
<td>"</td>
<td>200</td>
<td>1141</td>
<td><code>"https://author-p1234-e4444.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/wknd/en/adventures/surf-camp-in-costa-rica/adobestock_266405335.jpeg&_charset_=utf8"</code></td>
<td>“Mozilla/5.0(Macintosh; Intel Mac OS X 10_15_4)AppleWebKit/537.36（KHTML，如Gecko）Chrome/81.0.4044.122 Safari/537.36"</td>
</tr>
</tbody>
</table>


**示例**

```
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/granite/ui/references/clientlibs/references.lc-5188e85840c529149e6cd29d94e74ad5-lc.min.css HTTP/1.1" 200 1141 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/customthumb/clientlibs.lc-60e4443805c37afa0c74b674b141f1df-lc.min.css HTTP/1.1" 200 809 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
cm-p1234-e26813-aem-author-59555cb5b8-8kgr2 - example@adobe.com 30/Apr/2020:17:37:14 +0000  "GET /libs/dam/gui/coral/components/admin/metadataeditor/clientlibs/metadataeditor.lc-4a2226d8232f8b7ab27d24820b9ddd64-lc.min.js HTTP/1.1" 200 7965 "https://author-p10711-e26813.adobeaemcloud.com/mnt/overlay/dam/gui/content/assets/metadataeditor.external.html?item=/content/dam/en/images/example.jpeg&_charset_=utf8" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.122 Safari/537.36"
```

### 配置HTTP访问日志 {#configuring-the-http-access-log}

在AEM中，HTTP访问日志不能配置为Cloud Service。

## Apache Web Server/Dispatcher记录 {#dispatcher-logging}

AEM as aCloud Service在发布中为Apache Web Server和调度程序层提供三个日志：

* Apache HTTPD Web Server访问日志
* Apache HTTPD Web Server错误日志
* Dispatcher日志

请注意，这些日志仅对发布层可用。

此日志集提供对AEM的HTTP请求的洞察，在这些请求到达AEM应用程序之前，将其作为Cloud Service发布层。 这很重要，因为Apache HTTPD Web Server和AEMDispatcher为发布层服务器提供的大多数HTTP请求都由缓存内容提供，并且永远不能到达AEM应用程序本身，因此AEM Java、请求或访问日志中没有这些请求的日志语句。