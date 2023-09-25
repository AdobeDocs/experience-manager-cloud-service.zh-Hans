---
title: 使用通用编辑器进行本地AEM开发
description: 了解通用编辑器如何支持在本地AEM实例上编辑以进行开发。
source-git-commit: bf09c31baf209f5315e35f47c0d79c2b4365d3d3
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# 使用通用编辑器进行本地AEM开发 {#local-dev-ue}

了解通用编辑器如何支持在本地AEM实例上编辑以进行开发。

本文档将说明如何在HTTPS中将AEM与通用编辑器服务的本地副本一起运行，以便您可以使用通用编辑器在AEM上进行本地开发。

## 设置AEM以在HTTPS上运行 {#aem-https}

在使用HTTPS固定的外部帧中，无法加载不安全的HTTP帧。 Universal Editor服务在HTTPS上运行，因此AEM或任何其他远程页面也必须在HTTPS上运行。

为此，您需要将AEM设置为在HTTPS上运行。 出于开发目的，您可以使用自签名证书。

请参阅本文档，了解如何设置在HTTPS上运行的AEM，包括您可以使用的自签名证书。

## 安装通用编辑器服务 {#install-ue-service}

通用编辑器服务用于绑定通用编辑器和后端系统。 由于官方通用编辑器服务托管在全球范围内，因此您的本地AEM实例需要向Internet公开。 要避免此问题，您可以运行Universal Editor服务的本地副本。

[NodeJS版本16](https://nodejs.org/en/download/releases) 运行Universal Editor服务的本地副本时需要

Universal Editor服务由AEM Engineering直接分发。 请联系您在VIP项目中的工程联系人以获取本地副本。

工程部会为您提供 `universal-editor-service.cjs` 文件。 将此项目保存到您的本地开发环境。

## 创建证书以使用HTTPS运行通用编辑器服务 {#ue-https}

通用编辑器服务还需要证书才能在开发环境的HTTPS上运行。

运行以下命令。

```text
$ openssl req -newkey rsa:2048 -nodes -keyout key.pem -x509 -days 365 -out certificate.pem
```

该命令会生成 `key.pem` 和 `certificate.pem` 文件。 将这些文件保存到与 `universal-editor-service.cjs` 文件。

## 设置通用编辑器服务配置 {#setting-up-service}

必须在NodeJS中设置许多环境变量，才能在本地运行Universal Editor服务。

与您的路径相同 `universal-editor-service.cjs`， `key.pem` 和 `certificate.pem` 文件，创建 `.env` 文件包含以下内容。

```text
EXPRESS_PORT=8000
EXPRESS_PRIVATE_KEY=./key.pem
EXPRESS_CERT=./certificate.pem
NODE_TLS_REJECT_UNAUTHORIZED=0
```

此变量具有以下含义：

* `EXPRESS_PORT`：定义Universal Editor服务侦听的端口
* `EXPRESS_PRIVATE`：指向您的 [以前创建的私钥，](#ue-https) `key.pem`
* `EXPRESS_CERT`：指向您的 [以前创建的证书，](#ue-https) `certificate.pem`
* `NODE_TLS_REJECT_UNAUTHORIZED=0`：接受自签名证书

## 运行Universal Editor服务 {#running-ue}

要启动Universal Editor服务，请执行以下步骤：

```text
$ node ./universal-editor-service.cjs
```

它应该将以下内容输出到您的终端：

```text
Universal Editor Service listening on port 8000 as HTTPS Server
```

确保服务启动HTTPS服务器而不是HTTP服务器。

## 使用本地通用编辑器服务而不是全局服务 {#using-local-ue}

通用编辑器知道要使用哪项通用编辑器服务根据页面的检测方式编辑页面。 此操作可通过在通用编辑器中加载的页面中的meta标记来完成。

对于要使用本地Universal Editor服务编辑的页面，必须设置以下meta标记：

```
<meta name="urn:adobe:aem:editor:endpoint" content="https://localhost:8000">
```

设置后，您应该会看到每个内容更新调用转到 `https://localhost:8000` 而不是默认的Universal Editor服务。

>[!TIP]
>
>有关如何使用全局通用编辑器服务检测页面的更多详细信息，请参阅文档 [AEM中的通用编辑器快速入门](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本地通用编辑器服务编辑页面 {#editing}

使用 [在本地运行的通用编辑器服务](#running-ue) 和您的 [用于使用本地服务的内容页面，](#using-loca-ue) 您现在可以启动编辑器了。

1. 打开浏览器，以访问 `https://localhost:8000/`.
1. 指示浏览器接受 [您的自签名证书。](#ue-https)
1. 一旦自签名证书受到信任，您就可以使用本地通用编辑器服务编辑该页面。
