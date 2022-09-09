---
title: 维护 AEM 连接器
description: 维护 AEM 连接器
exl-id: 8122a8c8-6577-4907-8f6e-52711eed3970
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 100%

---

维护 AEM 连接器
============================

本文包含有关维护 AEM 连接器的信息，应结合有关[实施](implement.md)和[提交](submit.md)连接器的文章阅读这些信息。

即使在最初提交之后，合作伙伴也可能有理由更新其 AEM 连接器，比如由于 AEM 的新版本或与此无关 – 例如，添加功能或修复错误。 本文概述了针对这两种方案的过程，还描述了客户在升级 AEM 时验证连接器的典型过程。

AEM as a Cloud Service 应用程序每天通过 AEM 维护补丁进行更新，在功能发布期间每月会激活大量更改。虽然 AEM 更新旨在向后兼容，因此不会破坏应用程序，但建议供应商合作伙伴定期验证其连接器的行为是否符合预期。对 AEM 项目/环境的访问将由合作伙伴团队决定。
