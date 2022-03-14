---
title: 源代码存储库 — Cloud Services
description: 源代码存储库 — Cloud Services
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# 源代码存储库 {#source-code-repository}

Cloud Manager程序将自动配置其自己的git存储库。

对于用户访问Cloud Manager git存储库，需要将Git客户端与命令行工具、独立的可视Git客户端或用户的IDE（如Eclipse、IntelliJ、NetBeans）一起使用。

设置Git客户端后，您可以从Cloud Manager UI中管理您的git存储库。 要了解如何使用Cloud Manager UI管理Git，请参阅 [访问Git](/help/implementing/cloud-manager/accessing-git.md).

要开始开发AEM Cloud应用程序，必须通过将应用程序代码从Cloud Manager存储库签出到其本地计算机上要创建其存储库的位置，来制作应用程序代码的本地副本。

```java
$ git clone {URL}
```

>[!NOTE]
>
>用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回Cloud Manager中的远程代码存储库。
