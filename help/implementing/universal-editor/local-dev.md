---
title: 运行您自己的通用编辑器服务
description: 了解如何运行您自己的通用编辑器服务用于本地开发或者作为您自己的基础架构的一部分。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Developer
source-git-commit: d938abce2b46786343b19113454da1738a824ed0
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 95%

---


# 运行您自己的通用编辑器服务 {#local-ue-service}

了解如何运行您自己的通用编辑器服务用于本地开发或者作为您自己的基础架构的一部分。

>[!NOTE]
>
>使用 Edge Delivery Services 进行 AEM 创作的项目不需要或不支持本地通用编辑器服务。

## 概述 {#overview}

通用编辑器服务的作用是将通用编辑器与后端系统绑定。要为通用编辑器进行本地开发，您必须运行通用编辑器服务的本地副本。这是因为：

* Adobe 的官方通用编辑器服务在全球托管，而您的本地 AEM 实例需要在互联网上公开。
* 使用本地 AEM SDK 开发时，无法从互联网访问 Adobe 的通用编辑器服务。
* 如果您的 AEM 实例有 IP 限制，并且 Adobe 的通用编辑器服务不在一个已定义的 IP 范围内，您可以自行托管它。

## 用例 {#use-cases}

在以下情况下，使用您自己的通用编辑器服务副本会很有用：

* 您想在 AEM 上进行本地开发，以供通用编辑器使用。
* 您想运行您自己的通用编辑器服务，使其成为您自己的基础架构的一部分，独立于 Adobe 的通用编辑器服务。

这两种用例都受支持。本文档介绍如何在 HTTPS 中运行 AEM，并介绍通用编辑器服务的本地副本。

如果您希望将自己的通用编辑器服务作为您自己的基础架构的一部分运行，您可以采用与本地开发示例相同的步骤。

## 将 AEM 设置为在 HTTPS 上运行 {#aem-https}

在通过 HTTPS 保护的外层框架中，无法加载不安全的 HTTP 框架。Universal Editor Service 在 HTTPS 上运行，因此，AEM 或任何其他远程页面也必须在 HTTPS 上运行。

为此，您需要将 AEM 设置为在 HTTPS 上运行。出于开发目的，您可以使用自签名证书。

[请参阅这个文档](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=zh-Hans)，了解如何设置 AEM 在 HTTPS 上运行，包括一份您可使用的自签名证书。

## 安装通用编辑器服务 {#install-ue-service}

通用编辑器服务并不是通用编辑器的完整拷贝，而只是其功能的一个子集，以确保来自您本地 AEM 环境的调用不会通过互联网路由，而是从您控制的一个确定端点路由。

运行通用编辑器服务的本地副本需要 [NodeJS 版本 20](https://nodejs.org/en/download/releases)。

通用编辑器服务可通过软件分发获得。有关访问方法的详细信息，请参阅[软件分发文档](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=zh-Hans)。

将 `universal-editor-service.cjs` 文件从软件分发保存到您的本地开发环境。

## 创建证书以通过 HTTPS 运行 Universal Editor Service {#ue-https}

Universal Editor Service 还需要证书才能在开发环境中的 HTTPS 上运行。

运行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

该命令生成一个 `key.pem` 文件和一个 `certificate.pem` 文件。将这两个文件保存到与 `universal-editor-service.cjs` 文件相同的路径。

## 设置通用编辑器服务的配置 {#setting-up-service}

必须在 NodeJS 中设置大量环境变量才能在本地运行 Universal Editor Service。

在与 `universal-editor-service.cjs`、`key.pem` 和 `certificate.pem` 文件相同的路径上，创建具有以下内容的 `.env` 文件。

```text
UES_PORT=8000
UES_PRIVATE_KEY=./key.pem
UES_CERT=./certificate.pem
UES_TLS_REJECT_UNAUTHORIZED=false
UES_CORS_PRIVATE_NETWORK=true
```

这些是我们示例中的本地开发必需的最小值。

>[!NOTE]
>
>如果您运行的是 Chrome 130 及更高版本，就必须通过 `UES_CORS_PRIVATE_NETWORK` 选项为[专用网络访问权限](https://wicg.github.io/private-network-access/#private-network-request)启用发送 CORS 头部。


下表详细说明了这些值和其他可用值。

| 值 | 可选 | 默认 | 描述 |
|---|---|---|---|
| `UES_PORT` | 是 | `8080` | 服务器运行所在的端口 |
| `UES_PRIVATE_KEY` | 是 | 无 | 至 HTTPS 服务器私钥的路径 |
| `UES_CERT` | 是 | 无 | 至 HTTPS 服务器认证文件的路径 |
| `UES_TLS_REJECT_UNAUTHORIZED` | 是 | `true` | 拒绝未经授权的 TLS 连接 |
| `UES_DISABLE_IMS_VALIDATION` | 是 | `false` | 禁用 IMS 验证 |
| `UES_ENDPOINT_MAPPING` | 是 | 空 | 内部重写的端点映射<br>示例：`UES_ENDPOINT_MAPPING='[{"https://your-public-facing-author-domain.net": "http://10.0.0.1:4502"}]'`<br>结果：通用编辑器服务将连接到 `http://10.0.0.1:4502`，而不是所提供的连接 `https://your-public-facing-author-domain.net` |
| `UES_LOG_LEVEL` | 是 | `info` | 服务器的日志级别，可能的值为 `silly`、`trace`、`debug`、`verbose`、`info`、`log`、`warn`、`error` 和 `fatal` |
| `UES_SPLUNK_HEC_URL` | 是 | 无 | HEC URL 到 Splunk 端点 |
| `UES_SPLUNK_TOKEN` | 是 | 无 | Splunk 令牌 |
| `UES_SPLUNK_INDEX` | 是 | 无 | 写入日志的索引 |
| `UES_SPLUNK_SOURCE` | 是 | `universal-editor-service` | splunk 日志中的源名称 |
| `UES_CORS_PRIVATE_NETWORK` | 是 | `false` | 启用发送 CORS 头部，以允许[专用网络](https://wicg.github.io/private-network-access/#private-network-request)。Chrome 版本 130 及以上的用户必需 |

>[!NOTE]
>
>在通用编辑器 [2024.08.13 版本](/help/release-notes/universal-editor/current.md)发布之前，`.env` 文件中需要以下变量。对这些值的支持截至 2024 年 10 月 1 日，以确保向后兼容。
>
>`EXPRESS_PORT=8000`
>`EXPRESS_PRIVATE_KEY=./key.pem`
>`EXPRESS_CERT=./certificate.pem`
>`NODE_TLS_REJECT_UNAUTHORIZED=0`

## 运行 Universal Editor Service {#running-ue}

要启动 Universal Editor Service，请执行以下命令：

```text
$ node ./universal-editor-service.cjs
```

它应将以下内容输出到终端：

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

确保该服务启动 HTTPS 服务器而不是 HTTP 服务器。

## 使用本地 Universal Editor Service 而不是全局服务 {#using-local-ue}

Universal Editor 根据页面的检测方式了解使用哪个 Universal Editor Service 编辑页面。通过在 Universal Editor 中加载的页面中的元标记完成这一点。

对于要使用本地 Universal Editor Service 编辑的页面，必须设置以下元标记：

```html
<meta name="urn:adobe:aue:config:service" content="https://localhost:8000">
```

设置完成后，您应看到每个内容更新调用都转到 `https://localhost:8000` 而不是默认的 Universal Editor Service。

>[!NOTE]
>
>尝试直接访问 `https://localhost:8000` 会导致 `404` 错误。这个行为符合预期。
>
>要测试访问您本地的通用编辑器服务，请使用 `https://localhost:8000/corslib/LATEST`。有关详细信息请参阅[下一节](#editing)。

>[!TIP]
>
>有关如何检查页面以使用全局 Universal Editor Service 的更多详细信息，请参阅文档 [AEM Universal Editor 快速入门](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本地 Universal Editor Service 编辑页面 {#editing}

[通用编辑器服务已在本地运行](#running-ue)，并且您的[内容页面经过适配后可使用本地服务](/help/implementing/universal-editor/getting-started.md)，现在您可以启动编辑器。

1. 打开您的浏览器以转至 `https://localhost:8000/ping`。
1. 指示您的浏览器接受[您的自签名证书](#ue-https)。
1. 一旦自签名证书受到信任，就会使用本地通用编辑器服务加载该页面。
1. 单击工具栏中的[本地开发人员登录](/help/sites-cloud/authoring/universal-editor/navigation.md#local-developer-login)，并对您的本地AEM实例进行身份验证。

您现在可以使用本地Universal Editor服务在本地AEM测试实例上编辑页面。
