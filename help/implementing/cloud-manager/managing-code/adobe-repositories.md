---
title: 在 Cloud Manager 中添加 Adobe 存储库
description: 了解如何在 Cloud Manager 中添加 Adobe 管理的存储库。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 100%

---

# 在 Cloud Manager 中添加 Adobe 存储库 {#adobe-repositories}

了解如何在 Cloud Manager 中添加 Adobe 管理的存储库。

通过&#x200B;**存储库**&#x200B;页面，可以轻松地将其他 Adobe 管理的存储库添加到选定的程序。

**在 Cloud Manager 中添加 Adobe 存储库：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)上登录到 Cloud Manager，然后选择适当的组织以及您想要添加 Adobe 管理存储库的程序。

1. 在 **程序概述** 页面的侧面菜单中，单击 ![文件夹图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存储库**。

1. 在 **存储库** 页面的右上角附近，点击 **添加存储库**。

   ![添加“存储库”按钮](assets/add-repository.png)

1. 在 **添加存储库** 对话框中，确保选择 **Adobe 存储库** 作为存储库类型。

1. 在相应的文本字段中输入以下内容：

   * **存储库名称** - 新存储库的富有表现力的名称。
   * **存储库 URL 预览** - 您无需输入 URL 路径或编辑现有路径，因为存储库基础结构已经到位并由 Adobe 完全集成和管理。
   * **描述（可选）** - 存储库的详细描述。

   ![添加“存储库”对话框](assets/add-adobe-repository.png)

1. 单击&#x200B;**保存**。您的新存储库将显示在 **存储库** 页面的表格中。

您现在可以将 [CI/CD 管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)与其关联，或在&#x200B;[**存储库**&#x200B;页面内对其进行管理](managing-repositories.md)。

>[!TIP]
>
>您还可以将自己管理的 GitHub 存储库添加为[专用存储库](private-repositories.md)。
