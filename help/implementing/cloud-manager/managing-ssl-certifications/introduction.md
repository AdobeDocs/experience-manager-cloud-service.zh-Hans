---
title: 简介——管理SSL证书
description: 简介——管理SSL证书
translation-type: tm+mt
source-git-commit: 74cc587874c4d0a0ef9b542549801198d4f2d7a5
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# 简介 {#introduction}

Cloud Manager为客户提供通过Cloud Manager UI安装SSL证书的自助服务功能。 Cloud Manager使用平台TLS服务管理客户拥有的SSL证书和私钥，通常从第三方认证中心获取，例如，让我们加密。

>[!IMPORTANT]
>云管理器不提供SSL证书或私钥。 这些许可证必须从第三方认证机构获得。 请参阅如何获取SSL证书以了解更多信息。 插入链接

>[!NOTE]
>AEM作为Cloud Service仅支持安全的https站点。 具有多个自定义域的客户不希望在每次添加域时上传证书。 因此，此类客户将从获得一个具有多个域的证书中受益。

Cloud Manager支持以下客户SSL证书要求：

* SSL证书可以由多个环境使用——添加一次并使用多次。
* 每个Cloud Manager环境都可使用多个证书。
* 私钥可以发出多个SSL证书。
* 每个证书通常包含多个域。
* 平台TLS服务根据用于终止的SSL证书和托管该域的CDN服务将请求路由到客户的CDN服务。

使用“云管理器UI SSL证书”页，具有权限的用户可以执行多个任务来管理项目的SSL证书：

* 添加SSL证书。
* 查看、更新或替换SSL证书。 这些操作允许您视图详细信息或替换即将过期的证书。
* 删除SSL证书。