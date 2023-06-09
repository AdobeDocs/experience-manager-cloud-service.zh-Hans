---
title: 访问存储库
description: 了解如何使用 Cloud Manager 的自助 Git 帐户管理访问和管理 Git 存储库。
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 9ec45753f56d0576e75f148ca0165c0ccd621f23
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 98%

---

# 访问存储库 {#accessing-repos}

了解如何使用 Cloud Manager 的自助 Git 帐户管理访问和管理 Git 存储库。

## 使用自助服务存储库帐户管理 {#self-service-repos}

Cloud Manager 通过使用管道卡上突出显示的&#x200B;**访问存储库信息**&#x200B;按钮，可以轻松检索您的存储库信息。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织和程序。

1. 从&#x200B;**程序概述**&#x200B;页面导航到&#x200B;**管道**&#x200B;信息卡，您将发现&#x200B;**访问存储库信息**&#x200B;按钮，该按钮可用于访问和管理您的 Git 存储库。

   ![访问“环境”信息卡上的“存储库信息”按钮](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

1. 单击&#x200B;**查看存储库信息**&#x200B;按钮，打开查看对话框：

   * Cloud Manager Git 存储库的 URL。
   * Git 用户名。
   * Git 密码，其值在单击&#x200B;**生成密码**&#x200B;按钮时显示。

   ![存储库信息视图](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

使用这些凭据，用户可以克隆存储库的本地副本，并在该本地存储库中进行更改，准备就绪后，可以将任何代码更改提交回 Cloud Manager 中的远程代码存储库。

**访问存储库信息**&#x200B;选项也可在&#x200B;**管道**&#x200B;信息卡的&#x200B;**非生产**&#x200B;管道选项卡上使用。

![访问“非生产”选项卡上的“存储库信息”按钮](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

>[!NOTE]
>
>**访问存储库信息**&#x200B;选项对具有&#x200B;**开发人员**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可见。
