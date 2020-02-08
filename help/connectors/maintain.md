---
title: 维护AEM连接器
description: 维护AEM连接器
translation-type: tm+mt
source-git-commit: 629de3a9f55d2e4c52ef91c9e0bb5d439aebe84f

---


维护AEM连接器
============================

本文包含有关维护AEM Connector的信息，应与有关实施和提交连接器的文章一 [起阅读](implement.md)[这一信](submit.md) 息。

即使在初次提交后，合作伙伴也可能因AEM的新版本或独立于该版本而更新其AEM Connector（例如，添加功能或修复错误）。 本文概述了两种情况的过程，并描述了客户在升级AEM时验证连接器的典型过程。

AEM作为云服务应用程序每天都会使用AEM维护修补程序进行更新，在功能发布期间，每月会激活更多更改。 虽然AEM更新旨在向后兼容，因此不会中断应用程序，但建议供应商合作伙伴定期验证其连接器是否如预期那样工作。 对AEM计划／环境的访问权限将由合作伙伴团队决定。