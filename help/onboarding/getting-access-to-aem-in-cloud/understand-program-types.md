---
title: 了解项目和项目类型
description: 了解项目和项目类型 — Cloud Services
translation-type: tm+mt
source-git-commit: 6e8cf08ec3f85437a8472a45895f3818e473e98c
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---


# 了解程序和程序类型 {#understanding-programs}

在云管理器中，最上方是租户实体，该实体中可包含多个项目。 每个项目不能包含多个生产环境和多个非生产环境。

下图显示了Cloud Manager中的实体层次结构。

![图像](assets/program-types1.png)

## 源代码存储库 {#source-code-repository}

Cloud Manager项目将自动配置其自己的git存储库。

要使用户访问Cloud Manager的Git存储库，用户需要使用带有命令行工具的Git客户端、独立的可视Git客户端或用户的IDE（如Eclipse、IntelliJ、NetBeans）。

设置Git客户端后，您便可以从云管理器UI管理您的git存储库。 要了解如何使用Cloud Manager UI管理Git，请参阅[访问Git](/help/implementing/cloud-manager/accessing-git.md)。

要开始开发AEM Cloud应用程序，必须将应用程序代码的本地副本从Cloud Manager存储库签出到其本地计算机上要创建存储库的位置。

```java
$ git clone {URL}
```

>[!NOTE]
>用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回云管理器中的远程代码存储库。

## 项目类型{#program-types}

用户可以创建&#x200B;**沙箱**&#x200B;或&#x200B;**生产**&#x200B;项目。

* 创建&#x200B;*生产项目*以在将来的适当时间启用实时通信。
有关详细信息，请参阅[生产项目简介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)。


* *沙箱项目*通常用于培训、运行演示、启用、POC或文档目的。 它不用于传输实时流量，并且将具有生产项目不会的限制。 它将包括站点和资产，并将自动填充包含示例代码、开发环境和非生产渠道的Git分支。
有关详细信息，请参阅[沙箱项目简介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。

