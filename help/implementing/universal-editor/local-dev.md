---
title: 使用 Universal Editor 进行本地 AEM 开发
description: 了解 Universal Editor 如何支持在本地 AEM 实例上进行编辑以进行开发。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 61%

---


# 使用 Universal Editor 进行本地 AEM 开发 {#local-dev-ue}

了解 Universal Editor 如何支持在本地 AEM 实例上进行编辑以进行开发。

## 概述 {#overview}

Universal Editor Service 是一项用于将 Universal Editor 与后端系统绑定的服务。要能够在本地开发通用编辑器，必须运行通用编辑器服务的本地副本。 这是因为：

* Adobe的官方通用编辑器服务在全球托管，并且您的本地AEM实例需要向Internet公开。
* 使用本地AEM SDK进行开发时，无法从Internet访问Adobe的通用编辑器服务。
* 如果您的AEM实例具有IP限制，并且Adobe的Universal Editor服务不在定义的IP范围内，则可以自行托管。

本文档介绍如何在HTTPS中将AEM与通用编辑器服务的本地副本一起运行，以便您可以在AEM上本地开发以用于通用编辑器。

## 将 AEM 设置为在 HTTPS 上运行 {#aem-https}

在使用HTTPS固定的外部帧中，无法加载不安全的HTTP帧。 Universal Editor Service 在 HTTPS 上运行，因此，AEM 或任何其他远程页面也必须在 HTTPS 上运行。

为此，您需要将 AEM 设置为在 HTTPS 上运行。出于开发目的，您可以使用自签名证书。

[请参阅此文档](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html) 介绍如何设置在HTTPS上运行的AEM，包括您可以使用的自签名证书。

## 安装 Universal Editor Service {#install-ue-service}

Universal Editor服务不是Universal Editor的完整副本，而只是其功能的子集，以确保来自本地AEM环境的调用不会通过Internet进行路由，而是从您控制的已定义端点进行路由。

[NodeJS版本16](https://nodejs.org/en/download/releases) 运行Universal Editor服务的本地副本时需要。

Universal Editor服务可通过Software Distribution使用。 请参阅 [Software Distribution文档](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html) 以获取有关如何访问的详细信息。

保存 `universal-editor-service.cjs` 从Software Distribution到本地开发环境的文件。

## 创建证书以通过 HTTPS 运行 Universal Editor Service {#ue-https}

Universal Editor Service 还需要证书才能在开发环境中的 HTTPS 上运行。

运行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

该命令生成一个 `key.pem` 文件和一个 `certificate.pem` 文件。将这两个文件保存到与 `universal-editor-service.cjs` 文件相同的路径。

## 设置 Universal Editor Service 配置 {#setting-up-service}

必须在 NodeJS 中设置大量环境变量才能在本地运行 Universal Editor Service。

在与 `universal-editor-service.cjs`、`key.pem` 和 `certificate.pem` 文件相同的路径上，创建具有以下内容的 `.env` 文件。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

该变量的含义如下：

* `EXPRESS_PORT`：定义 Universal Editor Service 侦听的端口
* `EXPRESS_PRIVATE`：指向您的[之前创建的私钥，](#ue-https)`key.pem`
* `EXPRESS_CERT`：指向您的[之前创建的证书，](#ue-https)`certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：接受自签名证书

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
>尝试直接访问 `https://localhost:8000` 结果位于 `404` 错误。 这是预期行为。
>
>要测试对本地通用编辑器服务的访问，请使用 `https://localhost:8000/corslib/LATEST`. 请参阅 [下一节](#editing) 以了解详细信息。

>[!TIP]
>
>有关如何检查页面以使用全局 Universal Editor Service 的更多详细信息，请参阅文档 [AEM Universal Editor 快速入门](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本地 Universal Editor Service 编辑页面 {#editing}

在[本地运行 Universal Editor Service](#running-ue) 并且您的[内容页面经过检测可使用本地服务后，](#using-loca-ue)您现在可以启动编辑器。

1. 打开您的浏览器以转至 `https://localhost:8000/corslib/LATEST`。
1. 指示您的浏览器接受[您的自签名证书。](#ue-https)
1. 在自签名证书获得信任后，您可以使用本地 Universal Editor Service 编辑页面。

