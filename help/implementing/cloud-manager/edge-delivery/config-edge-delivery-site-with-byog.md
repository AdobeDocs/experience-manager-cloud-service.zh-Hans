---
title: 配置 Edge Delivery 网站以使用外部 Git 存储库
description: 了解如何将 Edge Delivery 网站与私有或企业 Git 存储库关联。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%

---

# 配置 Edge Delivery 网站以使用外部 Git 存储库

您可以配置您的 Edge Delivery 网站，从已加入 Cloud Manager 的任何私有 Git 存储库中提取代码。

**受支持的 Git 供应商**

| 支持级别 | 供应商 | 注释 |
| --- | --- | --- |
| 全面可用 | • GitHub Enterprise（自托管版本）<br>• Bitbucket（云版本）<br>• GitLab（云版本和自托管版本） | 无需启用请求即可连接 |
| Alpha 计划 | Azure DevOps（云版本） | [请求访问](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta 计划 | Adobe 托管的存储库（在 Cloud Manager 中创建） | [请求访问](mailto:grp-cloudmanager_byog@adobe.com) |

**要配置 Edge Delivery 网站以使用外部 Git 存储库：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台中，选择已配置了 Edge Delivery Services，并且您要在其中配置一个 Edge Delivery 网站以使用外部 Git 存储库的程序。
1. 在左侧边栏的&#x200B;**程序**&#x200B;标题中，点击&#x200B;**![概述图标](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) 概述**。
1. 在&#x200B;**程序概述**&#x200B;页面上，单击 **Edge Delivery** 选项卡。
1. 在 **Edge Delivery 网站**&#x200B;表中，点击您想为使用外部存储库而配置的网站所在那一行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后点击&#x200B;**自带 Git**。
1. 在“自带 Git”对话框中，在&#x200B;**存储库名称**&#x200B;下拉列表中选择一个状态为 `READY` 的 Git 存储库，然后点击&#x200B;**确认**。

   Cloud Manager 会返回一个一次性机密令牌。如果您重新配置此网站，Cloud Manager 会生成一个新的保密令牌。

1. 复制令牌，将其添加到 **helix-admin** 的网站配置中，如 [BYO Git 指南](https://www.aem.live/developer/byo-git) 中所述。
1. 返回到 Cloud Manager，点击您刚刚为使用外部存储库而配置的网站所在那一行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后点击&#x200B;**同步代码**。
1. 选择要同步的分支，然后点击&#x200B;**同步**。

现在任何分支上的每次提交都会触发自动同步。每当需要完全手动同步时，就再次使用&#x200B;**同步代码**。
