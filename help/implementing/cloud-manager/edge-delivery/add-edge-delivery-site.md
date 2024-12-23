---
title: 将 Edge Delivery 网站添加到 Cloud Manager
description: 了解如何将 Edge Delivery 网站添加到您的生产程序或沙盒程序。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 96%

---

# 将 Edge Delivery 网站添加到 Cloud Manager {#adding}

将 Edge Delivery 网站添加到生产程序后，您的 Edge Delivery Services 许可证将会应用于该网站。

需要将 Edge Delivery 网站添加到 Cloud Manager，才能[为您的 Edge Delivery 项目注册支持工单](/help/edge/overview.md##support-ticket)。

请参阅 [Cloud Manager 中的 Edge Delivery Services 简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

**若要将 Edge Delivery 网站添加到 Cloud Manager：**

1. 通过 [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的程序。
1. 执行下列操作之一：

   * 从&#x200B;**程序概览**&#x200B;页面，单击 **Edge Delivery** 选项卡。然后，单击页面右下角附近的&#x200B;**添加 Edge Delivery 网站**。

     ![从 Edge Delivery 选项卡添加 Edge Delivery 网站](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在页面左上角，单击![显示菜单图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)，以显示左侧菜单。
在**服务**&#x200B;标题下，单击![网页图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery 网站**。

在页面的右上角附近，单击**添加网站**。

     ![通过 Edge Delivery 网站按钮添加 Edge Delivery 网站](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加 Edge Delivery 网站**&#x200B;对话框中，在必填字段中提供以下信息：

   | 文本字段 | 描述 |
   | - | --- |
   | 网站名称 | 输入您要添加的 Edge Delivery 网站的名称。<br>该名称是 Cloud Manager 内网站的唯一标识符。 |
   | 存储库 URL | 进入存储您网站代码的 Git 存储库。<br>此字段允许 Cloud Manager 在部署过程中从该存储库中提取代码。 |
   | 网站描述（可选） | 输入您要添加的 Edge Delivery 网站的简短描述。<br>描述信息有助于识别和区分网站，使您在添加的其他网站中更容易管理和识别该网站。 |

1. 在对话框的右下角，单击&#x200B;**保存**。

1. 在&#x200B;**验证存储库所有权**&#x200B;对话框中，通过执行以下步骤验证存储库的所有权：

   | 步骤数 | 描述 |
   | - | - |
   | **1** | 将路径和名称为 `well-known/adobe/cloudmanager-challenge.txt` 的文件添加到 Git 存储库的 `main` 分支，该分支列在&#x200B;**存储库 URL** 字段中。请&#x200B;*不要*&#x200B;在位置路径的开头添加句点。<br>如有必要，请单击![复制](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)将该路径复制到剪贴板。 |
   | **2** | 将步骤 2 中文本字段中看到的代码添加到您在步骤 1 中刚刚创建的文件中。<br>如有必要，单击![复制](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)将代码复制到剪贴板。 |
   | **3** | 在 Git 存储库中为您刚才创建的更改创建一个拉取请求，然后将其合并到 `main` 以提交代码。 |

1. 单击&#x200B;**验证**。

验证存储库后，其在Edge Delivery站点表中的状态会更新。 内部带有白色复选标记的绿色圆圈表示状态。

在同一个表中，单击![Edge Delivery 网站信息](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)，以查看网站详情。此信息包括经过验证的存储库 URL，以及预览和生产网站 URL。
