---
title: 环境配置——需要什么
description: 环境配置——需要什么
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# 已设置的环境 {#environments-provisioning}

## 配置 {#provisioning}

客户购买的所有AEM云环境都将由Adobe自动配置，并且会在Cloud manager中链接回其计划。 这些AEM云环境包含在每个Adobe Managed services订阅中，通常由至少一个生产环境、一个阶段环境以及（可选）一个或多个开发或测试环境组成。

## 欢迎电子邮件 {#welcome-email}

在环境配置过程完成后，指定的客户管理员将收到一封欢迎电子邮件，确认他们已获得对Adobe Experience cloud的访问权限。 该电子邮件包含有关如何开始使用Experience cloud服务和Cloud manager自助服务门户的详细信息。 此外，电子邮件还包含重要信息，如支持资源、论坛或常见问题解答等。 在电子邮件中提供的资源列表中，您还将获取有关如何访问Cloud manager或AEM云环境的详细信息。

## 后续步骤 {#next-steps}

在收到欢迎电子邮件后，您可以使用Adobe IMS凭据以管理员身份登录到Cloud Manager。 登录后，您将能够验证AEM云生产和非生产环境是否可用并成功运行。

在部署代码时，Cloud manager将使用这些AEM云环境执行CI/CD管道（从Cloud Manager的Git存储库开始，通过分阶段环境，直至AEM生产环境）。 当您准备好开始为Web属性创建数字体验时，您还可以直接从Cloud manager访问AEM云环境。