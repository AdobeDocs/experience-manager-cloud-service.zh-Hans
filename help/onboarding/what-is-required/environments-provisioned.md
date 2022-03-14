---
title: 环境配置 — 需要什么
description: 环境配置 — 需要什么
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# 已设置的环境 {#environments-provisioning}

## 配置 {#provisioning}

客户购买的所有AEM云环境都将按Adobe自动进行配置，并且会关联回他们在Cloud Manager中的项目。 这些AEM云环境包含在每个Adobe Managed Services订阅中，通常至少由一个生产环境、一个阶段环境以及可选的一个或多个开发或测试环境组成。

## 欢迎电子邮件 {#welcome-email}

环境配置过程完成后，指定的客户管理员将收到一封欢迎电子邮件，确认他们已获得访问Adobe Experience Cloud的权限。 此电子邮件包含有关如何开始使用Experience Cloud服务和Cloud Manager自助服务门户的详细信息。 此外，电子邮件还包含重要信息，例如在何处获取支持资源、论坛或常见问题解答等。 在电子邮件中提供的资源列表中，您还将获取有关如何访问Cloud Manager或AEM云环境的详细信息。

## 后续步骤 {#next-steps}

收到欢迎电子邮件后，您便可以使用Adobe IMS凭据以管理员身份登录Cloud Manager。 登录后，您将能够验证AEM云生产和非生产环境是否可用且运行成功。

在部署代码时，Cloud Manager将使用这些AEM云环境来执行CI/CD管道，从Cloud Manager的Git存储库开始、通过暂存环境，一直到AEM生产环境。 当您准备好开始为Web资产创建数字体验时，您还可以直接从Cloud Manager访问AEM云环境。