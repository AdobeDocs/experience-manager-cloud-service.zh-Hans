---
title: 自定义 HTTP 标头
description: 配置自定义HTTP头
exl-id: 2cef5d4b-45f6-4d72-a24b-67ca53d9057d
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%

---

# 自定义 HTTP 标头 {#custom-http-headers}

## 概述 {#overview}

为了更好地控制其后端，作者可以配置将发送到商务引擎的自定义HTTP标头，以及CIF已发送的标头。 常见用例包括多商店设置，在这些设置中，您可以使用HTTP标头来控制商务后端的响应。

>[!NOTE]
>
>开发人员始终可以使用GraphQL客户端配置来配置自定义HTTP标头。

## 配置 {#configuration}

要配置自定义HTTP标头，必须先定义它们。 必须首先通过将自定义HTTP标头添加到 `com.adobe.cq.cif.http.internal.HttpHeadersConfigProviderImpl` 使用OSGi配置进行服务配置。

您可以在项目的“Cloud Service配置”页面中配置HTTP标头的值：

1. 转到“工具” — >“Cloud Service” — >“CIF配置”中的Cloud Services配置页面
1. 打开现有配置或创建新配置
1. 转到“高级”选项卡，并找到“自定义HTTP标头”多字段。 您可以选择之前定义的标题并为其分配值。

使用上述云服务配置的组件将随每个GraphQL请求一起发送这些HTTP标头。

## 限制 {#restrictions}

虽然该服务允许定义任何标头名称（包括标准名称），但它们将无法进行配置。 换言之，您无法使用此功能覆盖标准HTTP标头。 可以找到受限标头名称的列表 [此处](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers). 除了这些标头之外，还有两个标头不能使用：

* “商店” — CIF用于标识Adobe Commerce商店
* “Preview-Version” — CIF用于检索暂存产品
