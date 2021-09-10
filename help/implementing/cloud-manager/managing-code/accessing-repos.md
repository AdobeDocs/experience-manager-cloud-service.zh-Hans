---
title: 访问存储库
seo-title: Accessing Repositories
description: 本页介绍如何访问和管理Git存储库。
seo-description: Follow this page to learn how to access and manage your Git repository.
exl-id: 0c0671a3-e400-46f3-ad86-166a6cfdd44b
source-git-commit: 3cdee254eebcf45762feff8fe081b006a803ef1b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 5%

---

# 访问存储库 {#accessing-repos}

您可以使用Cloud Manager UI中的Git自助服务帐户管理来访问和管理Git存储库。

## 使用自助存储库帐户管理 {#self-service-repos}

使用Cloud Manager UI中提供的&#x200B;**访问存储库信息**&#x200B;按钮，其中最突出的是管道卡。

1. 从&#x200B;**项目概述**&#x200B;页面导航到&#x200B;**Pipelines**&#x200B;卡。

1. 您将查看&#x200B;**访问存储库信息**&#x200B;选项，以访问和管理您的Git存储库。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo1.png)

   此外，如果选择&#x200B;**非生产**&#x200B;管道选项卡，您还将在此处查看&#x200B;**访问存储库信息**&#x200B;选项。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-nonprod.png)

   >[!NOTE]
   >在“开发人员”或“部署管理器”角色中，用户可以看到&#x200B;**访问存储库信息**&#x200B;选项。 单击此按钮会打开一个对话框，通过该对话框，用户可以查找其Cloud Manager Git存储库的URL及其用户名和密码。

   ![](/help/implementing/cloud-manager/assets/repos/access-repo-create.png)

   在Cloud Manager中管理Git的重要注意事项包括：

   * **URL**:存储库URL
   * **用户名**:用户名
   * **密码**:单击“生成口令 **”按钮时显示** 的值。


      >[!NOTE]
      >用户可以签出其代码的副本，并在本地代码存储库中进行更改。 准备就绪后，用户可以将其代码更改提交回Cloud Manager中的远程代码存储库。
