---
title: 将Edge Delivery站点添加到Cloud Manager
description: 了解如何将Edge Delivery站点添加到生产程序或沙盒程序。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: c952e69aa637b30abec4deba0e643b4287d84330
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---


# 将Edge Delivery站点添加到Cloud Manager {#adding}

您可以将Edge Delivery站点添加到生产程序或沙盒程序。

需要将Edge Delivery站点添加到Cloud Manager才能[注册您的Edge Delivery项目的支持票证](/help/edge/overview.md##support-ticket)。

另请参阅[Cloud Manager中的Edge Delivery Services简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

**要将Edge Delivery站点添加到Cloud Manager，请执行以下操作：**

1. 在[`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 执行下列操作之一：

   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**&#x200B;选项卡。 然后，在页面的右下角附近，单击&#x200B;**添加Edge Delivery站点**。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。 在页面的右上角附近，单击&#x200B;**添加站点**。

     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加Edge Delivery站点**&#x200B;对话框中，在必填字段中提供以下信息：

   | 文本字段 | 要提供的数据 |
   | --- | --- |
   | 网站名称 | 输入要添加的Edge Delivery站点的名称。 该名称将用作Cloud Manager中站点的唯一标识符。 |
   | 存储库 URL | 此字段是指存储网站代码的Git存储库。 此字段允许Cloud Manager在部署过程中从该存储库中提取代码。 |
   | 网站描述（可选） | 输入要添加的Edge Delivery站点的简短说明。 此描述有助于识别和区分站点，使在您添加的其他站点中更容易管理和识别。 |

1. 单击对话框右下角的&#x200B;**添加**。

1. 将打开&#x200B;**验证存储库所有权**&#x200B;对话框。 打开后，请执行以下步骤：

   1. 将路径和名称为`well-known/adobe/cloudmanager-challenge.txt`的文件添加到&#x200B;**存储库URL**&#x200B;字段中列出的Git存储库的`main`分支。
      * 如有必要，请单击&#x200B;**复制**&#x200B;图标以将路径复制到剪贴板。
      * 请&#x200B;*不*&#x200B;在位置路径的开头添加句点。
   1. 将&#x200B;**Step &amp;amp；num； 1**&#x200B;字段中的代码添加到您在上一步中创建的文件中。
      * 如有必要，请单击&#x200B;**复制**&#x200B;图标以将代码复制到剪贴板。
   1. 在Git存储库中，为刚刚创建的更改创建拉取请求，然后将其合并到`main`。

1. 单击&#x200B;**验证**。

验证存储库后，其在Edge交付站点表格中的状态将更改为绿色圆圈，并在其内部显示白色复选标记。
