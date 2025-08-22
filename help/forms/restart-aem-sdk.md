---
title: 如何重新启动AEM SDK？
description: 重新启动AEM SDK的最佳实践
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 2%

---

# 重新启动AEM SDK

如果通过停止Java™进程来重新启动AEM SDK，可能会导致AEM开发环境不一致，并出现以下错误：

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![重新启动 — aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## 解决办法

要重新启动AEM SDK，请转到活动命令窗口，然后按`Ctrl + C`命令重新启动SDK。

建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法(例如，停止Java™进程)重新启动AEM SDK可能会导致AEM开发环境不一致。

## 另请参阅

* [为AEM Forms设置本地开发环境](/help/forms/setup-local-development-environment.md)

