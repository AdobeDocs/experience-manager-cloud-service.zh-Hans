---
title: 了解程序和程序类型
description: 了解程序和程序类型 — Cloud Services
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: d7d138c7442ee8bee7a1ad69144b26d74d364eee
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# 了解程序和程序类型 {#understanding-programs}

在Cloud Manager中，租户实体位于最顶部，该实体中可包含多个程序。 每个计划最多只能包含一个生产环境和多个非生产环境。

下图显示了Cloud Manager中实体的层次结构。

![图像](assets/program-types1.png)

## 源代码存储库 {#source-code-repository}

Cloud Manager程序将自动配置其自己的git存储库。

对于用户访问Cloud Manager git存储库，需要将Git客户端与命令行工具、独立的可视Git客户端或用户的IDE（如Eclipse、IntelliJ、NetBeans）一起使用。

设置Git客户端后，您可以从Cloud Manager UI中管理您的git存储库。 要了解如何使用Cloud Manager UI管理Git，请参阅[访问Git](/help/implementing/cloud-manager/accessing-git.md)。

要开始开发AEM Cloud应用程序，必须通过将应用程序代码从Cloud Manager存储库签出到其本地计算机上要创建其存储库的位置，来制作应用程序代码的本地副本。

```java
$ git clone {URL}
```

>[!NOTE]
>用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回Cloud Manager中的远程代码存储库。

## 程序类型 {#program-types}

用户可以创建&#x200B;**Sandbox**&#x200B;或&#x200B;**Production**&#x200B;程序。

* 创建&#x200B;*生产程序*以在将来的适当时间启用实时流量。
有关更多详细信息，请参阅生产计划简介。


* 通常，创建&#x200B;*沙盒项目*是为了用于培训、运行演示、启用、POC或文档目的。 它不用于传输实时流量，并且将具有生产程序不会受到的限制。 它将包含站点和资产，并且将使用自动填充的Git分支来交付，该分支包含示例代码、开发环境和非生产管道。
有关更多详细信息，请参阅沙盒项目简介。
