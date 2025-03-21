---
title: Dynamic Media 限制
description: 了解创建图像集、旋转集或上传PDF时的最佳实践和强制的限制。 还了解Dynamic Media不支持的Web浏览器和操作系统组合。
contentOwner: Rick Brough
content-type: reference
products: SG_EXPERIENCEMANAGER/Dynamic-Media-Classic
geptopics: SG_SCENESEVENONDEMAND_PK/categories/ecatalogs
feature: Dynamic Media Classic,Asset Management,Image Sets,Spin Sets,eCatalog
role: User
exl-id: fb63e2d4-2c8c-48dd-a0dc-fdfbbfb57b30
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 13%

---

# Dynamic Media限制

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

以下部分介绍Dynamic Media中的限制。

本主题包含以下部分：

* [Dynamic Media对资产类型的最佳实践和强制限制](#best-practice-enforced-limits)
* [Dynamic Media不支持的Web浏览器和操作系统组合](#unsupported-browser-os)

## Dynamic Media对资产类型的最佳实践和强制限制 {#best-practice-enforced-limits}

在创建旋转集或图像集，或者上传PDF进行页面提取时，Adobe建议以下最佳实践并强制实施以下限制：

| 资源 — 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| **图像** — 每个图像的智能裁剪数 | 5 | 100 |
| **所有集** — 每个集的重复资源数 | 无重复项 | 20 |
| **所有集** — 每个集的最大资源数 | 每组5至10个图像 | 1000 |
| **旋转集** — 每个2D集的最大行数/列数 | 每组12-18个图像 | 1000 |
| **PDF** — 考虑提取的PDF的最大页数 |  | 100（适用于所有PDF） |

<!-- See also [Dynamic Media limitations](/help/assets/limitations.md). -->

## Dynamic Media不支持的Web浏览器和操作系统组合 {#unsupported-browser-os}

Dynamic Media不支持以下Web浏览器和操作系统的组合。

* Internet Explorer 11 + Windows 7
* Internet Explorer 11 + Windows 8.1
* Internet Explorer 11 + Windows Phone 8.1
* Internet Explorer 11 + Windows Phone 8.1更新
* Safari 6 + iOS 6.0.1
* Safari 7 + iOS 7.1
* Safari 7 + OS X 10.9小牛
* Safari 8 + iOS 8.4
* Safari 8 + OS X 10.10 Yosemite

## 停止对Secure Socket Layer 2.0和3.0以及Transport Layer Security 1.0和1.1的支持 {#tls}

<!-- CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->

自2024年4月30日起，Adobe Dynamic Media将停止支持以下内容：

* SSL（安全套接字层）2.0
* SSL 3.0
* TLS（传输层安全性）1.0 和 1.1
* TLS 1.2 中的以下弱密码：
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
   * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_RSA_WITH_AES_256_GCM_SHA384`
   * `TLS_RSA_WITH_AES_256_CBC_SHA256`
   * `TLS_RSA_WITH_AES_256_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_AES_128_GCM_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA256`
   * `TLS_RSA_WITH_AES_128_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
   * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
   * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
   * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`
