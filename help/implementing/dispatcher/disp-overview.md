---
title: 云中的 Dispatcher
description: 云中的 Dispatcher
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 10da82c572682156534f7a897715d703ba3bde3d
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 7%

---

# 云中的 Dispatcher {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="云中的 Dispatcher"
>abstract="本页介绍如何下载和提取调度程序工具（即支持的Apache模块），并提供旧版和灵活模式的高级概述。"

## 简介 {#apache-and-dispatcher-configuration-and-testing}

本页介绍了Dispatcher工具以及如何下载和提取它们、支持的Apache模块，并简要概述了旧版和灵活模式。 此外，还进一步参考了验证和调试以及将Dispatcher配置从AMS迁移到AEMas a Cloud Service。 另请参阅 [此视频](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) 有关在云服务环境中部署dispatcher文件的其他详细信息。

## Dispatcher工具 {#dispatcher-sdk}

Dispatcher工具是整个AEMas a Cloud ServiceSDK的一部分，它提供：

* 一种原版文件结构，其中包含要包含在Dispatcher的Maven项目中的配置文件。
* 客户验证Dispatcher配置是否仅包含AEMas a Cloud Service支持的指令的工具。        此外，工具还会验证语法是否正确，以便Apache可以成功启动。
* 在本地调度程序的Docker图像。

## 下载和提取工具 {#extracting-the-sdk}

调度程序工具， [AEMas a Cloud ServiceSDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md)，可从位于 [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) 门户。 该新Dispatcher工具版本中可用的任何新配置都可用于部署到在云或更高版本中运行该AEM版本的云环境。

解压缩SDK，该SDK捆绑了适用于macOS、Linux和Windows的Dispatcher工具。

**对于macOS/Linux**，使调度程序工具对象可执行并运行它。 它将自解压缩存储到的目录下的调度程序工具文件(其中 `version` 是Dispatcher工具的版本)。

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**对于Windows**，提取Dispatcher工具zip存档。

## 使用Dispatcher工具进行验证和调试 {#validation-debug}

调度程序工具用于验证和调试项目的调度程序配置。 根据项目的调度程序配置是以灵活模式还是旧版模式构建，进一步了解如何在以下引用的页面中使用这些工具：

* **灵活模式**  — 推荐的模式，默认为 [AEM原型28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hans) 和更高版本，Cloud Manager也会将它用于在Cloud Manager 2021.7.0版本之后创建的新环境。 客户可以通过添加文件夹和文件来激活此模式 `opt-in/USE_SOURCES_DIRECTLY`. 通过使用这种更灵活的模式，在旧版模式下，重写文件夹下的文件结构没有任何限制，只需单个 `rewrite.rules` 文件。 此外，您可以添加的规则数量没有限制。 有关文件夹结构和本地验证的详细信息，请参阅 [使用Dispatcher工具验证和调试](/help/implementing/dispatcher/validation-debug.md).

* **旧版模式**  — 有关调度程序配置旧版模式的文件夹结构和本地验证的详细信息，请参阅 [使用Dispatcher工具验证和调试（旧版）](/help/implementing/dispatcher/validation-debug-legacy.md)

有关如何从AEM原型28提供的从旧版配置模型迁移到更灵活的配置模型的更多信息，请参阅 [本文档](/help/implementing/dispatcher/validation-debug.md#migrating).

## 内容处置 {#content-disposition}

对于发布层，提供Blob的默认值是作为附件。 可以使用标准 [内容处置标题](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition) 在调度程序中。

以下是配置外观的示例：

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## 支持的Apache模块 {#supported-directives}

下表显示了支持的Apache模块：

| 模块名称 | 参考页 |
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


客户无法添加任意模块，但将来可能会考虑添加其他模块以包含在内。 客户可以通过在SDK中执行验证器的命令，找到适用于给定Dispatcher版允许列表本的指令列表。

通过运行验证器的命令，可以列出Apache配置文件中允许的允许列表指令：

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## 文件夹结构 {#folder-structure}

项目的apache和dispatcher文件夹结构将因项目使用的模式而略有不同，如 [使用Dispatcher工具进行验证和调试](#validation-debug) 部分。

## 从AMS迁移Dispatcher配置 {#ams-aem}

有关如何将Dispatcher配置从AMS迁移到AEM  as a Cloud Service的详细信息，请参阅 [将Dispatcher配置从AMS迁移到AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service页面。
