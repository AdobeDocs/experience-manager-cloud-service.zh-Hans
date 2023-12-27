---
title: 使用 Universal Editor 进行本地 AEM 开发
description: 了解 Universal Editor 如何支持在本地 AEM 实例上进行编辑以进行开发。
exl-id: ba1bf015-7768-4129-8372-adfb86e5a120
source-git-commit: 0546f3cee8df3d7134021e32670b40030d56cd84
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 92%

---


# 使用 Universal Editor 进行本地 AEM 开发 {#local-dev-ue}

了解 Universal Editor 如何支持在本地 AEM 实例上进行编辑以进行开发。

本文档将说明如何在 HTTPS 中将 AEM 与 Universal Editor Service 的本地副本一起运行，以便您能使用 Universal Editor 在 AEM 上进行本地开发。

## 将 AEM 设置为在 HTTPS 上运行 {#aem-https}

在使用HTTPS固定的外部帧中，无法加载不安全的HTTP帧。 Universal Editor Service 在 HTTPS 上运行，因此，AEM 或任何其他远程页面也必须在 HTTPS 上运行。

为此，您需要将 AEM 设置为在 HTTPS 上运行。出于开发目的，您可以使用自签名证书。

请参阅此文档，了解如何设置在HTTPS上运行的AEM，包括您可以使用的自签名证书。

## 安装 Universal Editor Service {#install-ue-service}

Universal Editor Service 是一项用于将 Universal Editor 与后端系统绑定的服务。由于官方 Universal Editor Service 在全球范围内托管，因此，您的本地 AEM 实例需要在 Internet 上公开。为了避免此情况，您可以运行 Universal Editor Service 的本地副本。

需要 [NodeJS 版本 16](https://nodejs.org/en/download/releases)才能运行 Universal Editor Service 的本地副本

Universal Editor Service 由 AEM Engineering 直接分发。请与VIP项目中的工程师联系以获取本地副本。

工程部将为您提供 `universal-editor-service.cjs` 文件。将该文件保存到您的本地开发环境中。

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

>[!TIP]
>
>有关如何检查页面以使用全局 Universal Editor Service 的更多详细信息，请参阅文档 [AEM Universal Editor 快速入门](/help/implementing/universal-editor/getting-started.md#instrument-page)

## 使用本地 Universal Editor Service 编辑页面 {#editing}

在[本地运行 Universal Editor Service](#running-ue) 并且您的[内容页面经过检测可使用本地服务后，](#using-loca-ue)您现在可以启动编辑器。

1. 打开您的浏览器以转至 `https://localhost:8000/`。
1. 指示您的浏览器接受[您的自签名证书。](#ue-https)
1. 在自签名证书获得信任后，您可以使用本地 Universal Editor Service 编辑页面。
