---
title: 在Cloud Manager中添加Adobe存储库
description: 了解如何在Cloud Manager中添加Adobe管理的存储库。
exl-id: 6c32c4ae-f48d-4440-bfc2-cdc1a3d59599
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f2364de6237ca9f0285815b581bcf3881488188d
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 7%

---

# 在Cloud Manager中添加Adobe存储库 {#adobe-repositories}

了解如何在Cloud Manager中添加Adobe管理的存储库。

通过&#x200B;**存储库**&#x200B;页面，可以轻松地将其他Adobe管理的存储库添加到所选程序。

**要在Cloud Manager中添加Adobe存储库：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择要向其添加Adobe管理的存储库的相应组织和程序。

1. 在&#x200B;**项目概述**&#x200B;页面的侧菜单中，单击![文件夹图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **存储库**&#x200B;选项卡。

1. 在&#x200B;**存储库**&#x200B;页面的右上角附近，单击&#x200B;**添加存储库**。

   ![添加“存储库”按钮](assets/add-repository.png)

1. 在&#x200B;**添加存储库**&#x200B;对话框中，确保选择&#x200B;**Adobe存储库**&#x200B;作为存储库类型。

1. 在相应的文本字段中，输入以下内容：

   * **存储库名称** — 新存储库的表达式名称。
   * **存储库URL预览** — 您无需输入URL路径或编辑现有路径，因为存储库基础结构已就位，并且完全集成并由Adobe管理。
   * **描述（可选）** — 存储库的详细说明。

   ![添加存储库对话框](assets/add-adobe-repository.png)

1. 单击&#x200B;**保存**。
您的新存储库显示在**存储库**&#x200B;页面上的表中。

您现在可以将[CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)与其关联或在&#x200B;[**存储库**&#x200B;页面](managing-repositories.md)中管理它。

>[!TIP]
>
>您还可以将自己管理的 GitHub 存储库添加为[专用存储库](private-repositories.md)。
