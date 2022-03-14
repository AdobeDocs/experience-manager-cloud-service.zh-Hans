---
title: 维护 AEM 连接器
description: 维护 AEM 连接器
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 20%

---

维护 AEM 连接器
============================

本文包含有关维护 AEM 连接器的信息，应结合有关[实施](implement.md)和[提交](submit.md)连接器的文章阅读这些信息。

即使在初次提交后，合作伙伴仍可能有理由更新其AEM Connector，这要么是因为AEM的新版本所致，要么是因为该版本与之无关，例如添加功能或修复错误。 本文概述了两种情况的过程，并介绍了客户在升级AEM时验证连接器的典型过程。

AEMas a Cloud Service应用程序每天都会使用AEM维护修补程序进行更新，在功能发布期间，会每月激活更大的更改。 虽然AEM更新旨在向后兼容，从而不会破坏应用程序，但建议供应商合作伙伴定期验证其连接器是否按预期运行。 对AEM计划/环境的访问权限将由合作伙伴团队确定。
