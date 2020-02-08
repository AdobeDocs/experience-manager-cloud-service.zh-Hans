---
title: 源代码存储库——云服务
description: 源代码存储库——云服务
translation-type: tm+mt
source-git-commit: 6f323f33663f83043eb8a15fe00e6ed872c3cac1

---


# 源代码存储库 {#source-code-repository}

Cloud manager计划将自动配置自己的git存储库。

用户要访问Cloud manager的Git存储库，需要将Git客户端与命令行工具、独立的可视Git客户端或用户的IDE（如Eclipse、IntelliJ、NetBeans）一起使用。

设置Git客户端后，您便可以从Cloud Manager UI管理您的git存储库。 要了解如何使用Cloud Manager UI管理Git，请参阅访 [问Git](/help/implementing/cloud-manager/accessing-git.md)。

要开始开发AEM cloud应用程序，必须将应用程序代码的本地副本从Cloud manager存储库签出到其本地计算机上希望创建其存储库的位置。

```java
$ git clone {URL}
```

> [!NOTE]
> 用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回云管理器中的远程代码存储库。
