---
title: 记录
description: 了解如何为中央日志记录服务配置全局参数、单个服务的特定设置或如何请求数据记录。
translation-type: tm+mt
source-git-commit: a7c8e1ab8e0196a3a79d8e0963192775e64a2400
workflow-type: tm+mt
source-wordcount: '386'
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

### AEM Java日志记录 {#aem-java-logging}

AEM作为Cloud Service提供对Java日志语句的访问。 AEM应用程序的开发人员应按照常规的Java日志记录最佳实践，在以下日志级别记录有关自定义代码执行的相关语句：

<table>
<tbody>
<tr>
<td> <b>AEM环境</b></td>
<td> <b>日志级别</b></td>
<td> <b>描述</b></td>
<td> <b>日志语句可用性</b></td>
</tr>
<tr>
<td> 开发</td>
<td> 调试</td>
<td> 描述应用程序中正在发生的情况。

当DEBUG日志记录处于活动状态时，将记录提供发生活动的清晰画面的语句以及影响处理的任何关键参数。</td>
<td> <ul>
<li> 本地开发</li>
<li>开发</li>
</ul></td>
</tr>
<tr>
<td> 暂存</td>
<td> 警告</td>
<td> 描述可能成为错误的条件。

当WARN日志记录处于活动状态时，只记录指示正在接近次优性的条件语句。</td>
<td> <ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
</ul></td>
</tr>
<tr>
<td> 生产</td>
<td> 错误</td>
<td> 描述指示故障并需要解决的条件。

当ERROR日志记录处于活动状态时，只记录指示失败的语句。 ERROR日志语句表示出现严重问题，应尽快解决。</td>
<td> <ul>
<li> 本地开发</li>
<li>开发</li>
<li>暂存</li>
<li>生产</li>
</ul></td>
</tr>
</tbody>
</table>