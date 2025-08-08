---
title: 配置Edge Delivery站点以使用外部Git存储库
description: 了解如何将Edge Delivery站点链接到专用或企业Git存储库。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 62134c5b67d610f801c407e696e761ed05e02c87
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 7%

---


# 配置Edge Delivery站点以使用外部Git存储库

您可以将Edge Delivery站点配置为从已在Cloud Manager中载入的任何专用Git存储库中提取代码。

**支持的Git供应商**

| 支持级别 | 供应商 | 注释 |
| --- | --- | --- |
| 正式发布 | · GitHub Enterprise（自托管版本）<br>· Bitbucket（云版本）<br>· GitLab（云和自托管版本） | 在不启用请求的情况下连接 |
| Alpha项目 | Azure DevOps（云版本） | [请求访问](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta项目 | Adobe托管的存储库(在Cloud Manager中创建) | [请求访问](mailto:grp-cloudmanager_byog@adobe.com) |

**要将Edge Delivery站点配置为使用外部Git存储库：**

1. 登录 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 上的 Cloud Manager，然后选择合适的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择配置了Edge Delivery Services的程序，您要将Edge Delivery站点配置为使用外部Git存储库。
1. 在左边栏中的&#x200B;**项目**&#x200B;标题下，单击&#x200B;**![概述图标](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg)概述**。
1. 在&#x200B;**程序概述**&#x200B;页面上，单击 **Edge Delivery** 选项卡。
1. 在&#x200B;**Edge Delivery站点**&#x200B;表中，单击要将其站点配置为使用外部存储库的行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**自带Git**。
1. 在“自带Git”对话框的&#x200B;**存储库名称**&#x200B;下拉列表中，选择一个状态为`READY`的Git存储库，然后单击&#x200B;**确认**。

   Cloud Manager返回一次性密码令牌。 如果重新配置站点，Cloud Manager会生成一个新的机密令牌。

1. 复制令牌并将其添加到&#x200B;**helix-admin**&#x200B;中的站点配置，如[BYO Git指南](https://www.aem.live/developer/byo-git)中所述。
1. 返回Cloud Manager，单击您刚刚配置为使用外部存储库的一行末尾的![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)，然后单击&#x200B;**同步代码**。
1. 选择要同步的分支，然后单击&#x200B;**同步**。

现在，任何分支上的每次提交都会触发自动同步。 在需要完全手动同步时再次使用&#x200B;**同步代码**。
