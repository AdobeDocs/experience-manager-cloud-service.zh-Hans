---
title: 源代码存储库——云服务
description: 源代码存储库——云服务
translation-type: tm+mt
source-git-commit: 114bc678fc1c6e3570d6d2a29bc034feb68aa56d

---


# 源代码存储库 {#source-code-repository}

Cloud Manager项目将自动配置自己的git存储库。

用户要访问Cloud Manager的Git存储库，需要将Git客户端与命令行工具、独立的可视Git客户端或用户的IDE（如Eclipse、IntelliJ、NetBeans）一起使用。

设置Git客户端后，您便可以从Cloud Manager UI管理您的git存储库。 要了解如何使用Cloud Manager UI管理Git，请参阅访 [问Git](/help/implementing/cloud-manager/accessing-git.md)。

要开始开发AEM Cloud应用程序，必须将应用程序代码的本地副本从Cloud Manager存储库签出到其本地计算机上希望创建其存储库的位置。

```java
$ git clone {URL}
```

>[!NOTE]
>
> 用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回云管理器中的远程代码存储库。
