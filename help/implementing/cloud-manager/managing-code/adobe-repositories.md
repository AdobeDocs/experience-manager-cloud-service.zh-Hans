---
title: 在Cloud Manager中添加Adobe存储库
description: 了解如何在Cloud Manager中创建Adobe管理的存储库。
source-git-commit: a5179851af8ec88e23d79a74265b10cbce2d50f1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 20%

---


# 在Cloud Manager中添加Adobe存储库 {#adobe-repositories}

了解如何在Cloud Manager中创建Adobe管理的存储库。

## 添加Adobe管理的资源库 {#add-adobe-repository}

此 **存储库** 通过窗口，可以轻松为项目添加其他Adobe管理的存储库。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上登录到 Cloud Manager 并选择适当的组织和项目。

1. 从 **项目概述** 页面上，选择 **存储库** 制表符以切换到 **存储库** 页面。

1. 单击 **添加存储库** 工具栏中。

   ![添加“存储库”按钮](assets/add-repository.png)

1. 输入请求的名称和描述，然后单击&#x200B;**保存**。

   ![添加“存储库”对话框](assets/add-adobe-repository.png)

向导关闭时，您的新存储库将显示在的表格中。 **存储库** 窗口。 您现在可以关联 [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 使用它或在 [**存储库** 窗口。](managing-repositories.md)

>[!TIP]
>
>您还可以添加您自己管理的GitHub存储库 [专用存储库。](private-repositories.md)
