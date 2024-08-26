---
title: 添加IP允许列表
description: 了解如何使用Cloud Manager添加您自己的IP允许列表。
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 12%

---


# 添加 IP 允许列表 {#add-ip-allow-list}

了解如何使用Cloud Manager添加您自己的IP允许列表。

具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以按照这些步骤添加IP允许列表。

{{add-cm-allowlist-frontend-pipeline}}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**程序概述**&#x200B;页面，使用左侧的侧面板（您可能需要单击左上角的汉堡图标才能看到面板），单击&#x200B;**IP允许列表**。

   侧面板中的![IP允许列表选项](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. 在“IP允许列表”页面的右上角附近，单击&#x200B;**添加IP允许列表**。

   ![“添加 IP 允许列表”对话框](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. 在&#x200B;**添加IP允许列表**&#x200B;对话框的&#x200B;**IP允许列表名称**&#x200B;字段中，输入要用于引用IP允许列表的名称。 此名称仅供参考。 请确保其描述性足以帮助您识别列表。

1. 在&#x200B;**IP地址/ CIDR**&#x200B;字段中，输入IP或IP CIDR块。 用逗号或制表符分隔多个块。

1. 单击&#x200B;**保存**。

保存后，新创建的IP允许列表将在&#x200B;**IP允许列表**&#x200B;页的表中显示为一行。

## 添加Cloud Manager IP允许列表 {#add-cm-allowlist}

前端管道要求预先添加以下Cloud Manager IP允许列表。

**Cloud Manager IP允许列表**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

为避免运行前端管道中断，请确保在启用该管道之前&#x200B;*添加此Cloud Manager IP允许列表，并将其应用于环境*&#x200B;的创作服务。

**添加Cloud Manager IP允许列表：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择该程序。

1. 从&#x200B;**程序概述**&#x200B;页面，使用左侧的侧面板（您可能需要单击左上角的汉堡图标才能看到面板），单击&#x200B;**IP允许列表**。

1. 在“IP允许列表”页面的右上角附近，单击&#x200B;**添加IP允许列表**。

1. 在&#x200B;**添加IP允许列表**&#x200B;对话框的&#x200B;**IP允许列表名称**&#x200B;字段中，键入&#x200B;*`Cloud Manager`*。

1. 复制上面的Cloud Manager IP允许列表地址块。 每个地址已经用逗号分隔。

1. 在&#x200B;**添加IP允许列表**&#x200B;对话框中，将块粘贴到&#x200B;**IP地址/ CIDR**&#x200B;字段中。

1. 将光标放在地址列表中的第一个逗号之后，然后按&#x200B;**Enter**。

1. 单击&#x200B;**保存**。

现在，[将Cloud Manager IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md)应用于您的程序环境。



