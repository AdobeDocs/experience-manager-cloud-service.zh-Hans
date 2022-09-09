---
title: 访问存储库
description: 了解如何使用Cloud Manager中的自助式git帐户管理来访问和管理您的git存储库。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 4729574eb31e01077f0d2a35efcef6d134f6aa5c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---

# 访问存储库 {#accessing-repos}

了解如何使用Cloud Manager中的自助式git帐户管理来访问和管理您的git存储库。

## 使用自助存储库帐户管理 {#self-service-repos}

Cloud Manager允许您轻松地使用 **访问存储库信息** 按钮。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡片 **计划概述** 页面并查找 **访问存储库信息** 按钮以访问和管理您的git存储库。

   ![“环境”卡上的“访问Repo信息”按钮](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 单击 **查看存储库信息** 按钮以打开要查看的对话框：

   * 指向Cloud Manager git存储库的URL。
   * git用户名。
   * git密码，其值在 **生成密码** 按钮。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用这些凭据，用户可以克隆存储库的本地副本，并在该本地存储库中进行更改，准备就绪后，可以将任何代码更改提交回Cloud Manager中的远程代码存储库。

的 **访问存储库信息** 选项 **非生产** 管道选项卡 **管道** 卡。

![“访问存储库信息”按钮（位于非生产选项卡中）](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>的 **访问存储库信息** 选项对具有 **开发人员** 或 **部署管理器** 角色。
