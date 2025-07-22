---
title: 恢复之前部署的Source代码
description: 了解如何将环境恢复到其上次成功构建&amp；ndash；而无需运行管道。
feature: Operations
role: Admin
badge: label="英文字母" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md网站#gitlab-bitbucket"
exl-id: 8f804f55-a66d-47ad-a48d-61b861cef4f7
source-git-commit: f3e31d1f17283086cd6fe9e73d67feac938d6567
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 4%

---

# 恢复之前在AEM as a Cloud Service中部署的源代码 {#restore-previous-code-deployed}

>[!NOTE]
>
>本文中介绍的功能只能通过alpha程序使用。 要注册Alpha，请参阅管道部署的[一键式回滚](/help/implementing/cloud-manager/release-notes/current.md##one-click-rollback)。

使用&#x200B;**还原先前部署的代码**&#x200B;将环境立即回滚到其上次成功生成 — 无需运行管道。

只需打开所选环境的![更多图标或省略号菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)菜单，然后选择&#x200B;**还原** > **已部署以前的代码**&#x200B;即可回滚最近部署的源代码（以秒为单位）。

>[!TIP]
>
>您可以在&#x200B;**常规**&#x200B;选项卡下的环境详细信息视图中查看正在使用的活动源代码版本。 查看[查看环境的详细信息](/help/implementing/cloud-manager/manage-environments.md#viewing-environment)。
>
>![Source代码版本正在使用中](/help/operations/assets/environments-view-details-sourcecodeversion.png)

仅当下面的&#x200B;**every**&#x200B;条件为true时，**还原先前部署的代码**&#x200B;功能才可用：

* 您拥有&#x200B;**环境还原创建**&#x200B;权限。 有关管理权限的详细信息，请参阅[自定义权限](/help/implementing/cloud-manager/custom-permissions.md)。
* 您的组织已注册Alpha计划，并且功能标记已启用。
* 程序在AEM as a Cloud Service上运行。
* 选择的环境是`Development`环境(临时Alpha限制)。
* 该环境的最后一个管道已成功完成，并在&#x200B;**天内**&#x200B;前运行。
* 环境状态为&#x200B;*正在运行*，没有管道正在进行中。

如果任何检查失败，Cloud Manager将打开以下对话框，其中列出了一个或多个未满足的条件，并禁用&#x200B;**确认**，从而阻止还原。

![还原以前的代码部署失败对话框](/help/operations/assets/restore-previous-code-deployment-not-allowed.png)。

如果您只想将已丢失、损坏或意外删除的数据恢复到其原始状态，则可以使用[在AEM as a Cloud Service中恢复内容](/help/operations/restore.md)。 此恢复过程仅影响内容，而不会更改您的源代码和AEM版本。

**要还原先前部署的代码，请执行以下操作：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要启动还原的程序。

1. 通过执行以下操作之一，列出程序的所有环境：

   * 从左侧菜单的&#x200B;**服务**&#x200B;下，单击![数据图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **环境**。

     ![“环境”信息卡](assets/environments-1.png)

   * 从左侧菜单的&#x200B;**程序**&#x200B;下，单击&#x200B;**概述**，然后从&#x200B;**环境**&#x200B;信息卡中，单击![工作流图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) **显示所有**。

     ![显示所有选项](assets/environments-2.png)

     >[!NOTE]
     >
     >**环境**&#x200B;信息卡仅列出三个环境。 单击卡片中的&#x200B;**显示全部**&#x200B;以查看程序的&#x200B;*全部*&#x200B;环境。

1. 在“环境”表格中，在要还原其源代码的环境右侧，单击![更多图标或省略号菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**还原** > **已部署以前的代码**。

   ![从省略号菜单还原以前部署的代码选项](/help/operations/assets/restore-previous-code-deployed-menu.png)

1. 在&#x200B;**还原先前部署的代码**&#x200B;对话框中，查看当前部署的版本以及要还原的版本，然后单击&#x200B;**确认**。

   ![还原先前部署的代码对话框](/help/operations/assets/restore-previous-code-deployed-dialogbox.png)

1. Cloud Manager将环境回滚到以前的版本，保持内容和配置不变，并在“环境”页面上标记环境&#x200B;**正在恢复**，直到部署完成。

   ![正在还原激活](/help/operations/assets/restore-previous-code-deployed-restoring.png)
