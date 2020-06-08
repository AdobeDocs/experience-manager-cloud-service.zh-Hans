---
title: 环境配置——需要什么
description: 环境配置——需要什么
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# 已设置的环境 {#environments-provisioning}

## 设置 {#provisioning}

客户购买的所有AEM云环境将由Adobe自动设置，并链接回Cloud Manager中的项目。 这些AEM云环境包含在每个Adobe Managed Services订阅中，并且通常至少包含一个生产环境、一个阶段环境，以及（可选）一个或多个开发或测试环境。

## 欢迎电子邮件 {#welcome-email}

在环境配置流程完成后，指定的客户管理员将收到一封欢迎电子邮件，确认他们已被授予对Adobe Experience Cloud的访问权限。 该电子邮件包含有关如何开始使用Experience Cloud服务和Cloud Manager自助服务门户的详细信息。 此外，电子邮件还包含重要信息，如支持资源、论坛或常见问题解答等。 在电子邮件中提供的资源列表中，您还将获取有关如何访问Cloud Manager或AEM Cloud环境的详细信息。

## 后续步骤 {#next-steps}

收到欢迎电子邮件后，您可以以管理员身份使用Adobe IMS凭据登录Cloud Manager。 登录后，您将能够验证AEM云生产和非生产环境是否可用并成功运行。

在部署代码时，Cloud Manager将使用这些AEM云环境执行CI/CD管道(从Cloud Manager的Git存储库开始，到暂存环境，再到AEM生产环境)。 当您准备好开始为Web属性创建数字体验时，您还可以直接从Cloud Manager访问AEM云环境。