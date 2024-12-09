---
title: 云中的 Dispatcher
description: 了解 Dispatcher 工具、受支持的 Apache 模块以及传统模式和灵活模式。
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 云中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="云中的 Dispatcher"
>abstract="本页介绍如何下载和提取 Dispatcher 工具、受支持的 Apache 模块，并提供对传统架构和灵活架构的高级概述。"

## 简介 {#apache-and-dispatcher-configuration-and-testing}

本页介绍 Dispatcher 工具以及如何下载和提取这些工具、受支持的 Apache 模块，并提供对传统架构和灵活架构的高级概述。此外，还提供了关于验证以及调试 Dispatcher 配置并将其从 AMS 迁移到 AEM as a Cloud Service 的深度引用。<!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Dispatcher 工具 {#dispatcher-sdk}

Dispatcher 工具是整个 AEM as a Cloud Service SDK 的一部分，并提供了：

* 包含要包括在 Dispatcher 的 maven 项目中的配置文件的普通文件结构。
* 供客户用来验证 Dispatcher 配置是否仅包含 AEM as a Cloud Service 支持的指令的工具。此外，该工具还可验证语法是否正确，以便 apache 能够成功启动。
* 本地引出 Dispatcher 的 Docker 图像。

## 下载并提取工具 {#extracting-the-sdk}

可以从[软件分发](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)门户上的 zip 文件中下载 Dispatcher 工具（它是 [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md) 的一部分）。新版本的 Dispatcher 工具中提供的任何新配置都可用于部署到运行该版本的 AEM 或更高版本的云环境。

解压 SDK，它捆绑了适用于 macOS、Linux® 和 Windows 的 Dispatcher 工具。

**对于 macOS/Linux**，使 Dispatcher 工具构件可执行并运行它。它将在您将 Dispatcher 工具存储到的目录下自行提取 Dispatcher 工具文件（其中，`version` 是 Dispatcher 工具的版本）。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**对于 Windows**，提取 Dispatcher 工具 zip 存档。

## 使用 Dispatcher 工具进行验证和调试 {#validation-debug}

Dispatcher 工具用于验证和调试项目的 Dispatcher 配置。了解如何根据您项目的 Dispatcher 配置是在灵活架构还是旧版架构下构建的，在下面引用的页面中使用这些工具的更多信息：

* **灵活架构** - 推荐架构，也是 [AEM 原型 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) 及更高版本的默认架构，Cloud Manager 也将此架构用于创建的新环境（在 Cloud Manager 2021.7.0 版本之后）。客户可以通过添加文件夹和文件 `opt-in/USE_SOURCES_DIRECTLY` 来激活此架构。通过使用这个更灵活的架构，rewrites 文件夹下的文件结构不受任何限制，在旧版架构下需要单个 `rewrite.rules` 文件。此外，可添加的规则数量不受任何限制。有关文件夹结构和本地验证的详细信息，请参阅[使用 Dispatcher 工具进行验证和调试](/help/implementing/dispatcher/validation-debug.md)。

* **传统架构** – 有关 Dispatcher 配置旧版架构的文件夹结构和本地验证的详细信息，请参阅[使用 Dispatcher 工具进行验证和调试（旧版）](/help/implementing/dispatcher/validation-debug-legacy.md)

有关如何从旧版配置模型迁移到更灵活的模型（从 AEM 原型 28 开始附带）的更多信息，请参阅[此文档](/help/implementing/dispatcher/validation-debug.md#migrating)。

## 内容处置 {#content-disposition}

对于发布层，提供 blob 的默认设置是作为附件。使用 Dispatcher 中的标准[内容处置标头](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition)对其进行覆盖。

下面是配置的显示方式的示例：

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## 支持的 Apache 模块 {#supported-directives}

下表显示了支持的 Apache 模块：

| 模块名称 | 引用页面 |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


虽然客户无法添加任意模块，但将来可以考虑包含其他模块。客户可以通过在 SDK 中执行验证器的白名单命令来查找可用于给定 Dispatcher 版本的指令列表。

可以通过运行验证器的白名单命令来列出 Apache 配置文件中允许的指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## 文件夹结构 {#folder-structure}

项目的 Apache 和 Dispatcher 文件夹结构将因项目使用的架构而略为不同，如前面的[使用 Dispatcher 工具进行验证和调试](#validation-debug)部分中所述。

## 从 AMS 迁移 Dispatcher 配置 {#ams-aem}

有关如何将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service 的详细信息，请参阅[将 Dispatcher 配置从 AMS 迁移到 AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service 页面。
