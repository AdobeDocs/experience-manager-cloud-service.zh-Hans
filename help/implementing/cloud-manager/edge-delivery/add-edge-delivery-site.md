---
title: 将Edge Delivery站点添加到Cloud Manager
description: 了解如何将Edge Delivery站点添加到生产程序或沙盒程序。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 2b384a4233672d69de09b922fcdef6d0f84ff7df
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---


# 将Edge Delivery站点添加到Cloud Manager {#adding}

将Edge Delivery站点添加到生产程序后，即会对其应用Edge Delivery Services许可证。

需要将Edge Delivery站点添加到Cloud Manager才能[注册您的Edge Delivery项目的支持票证](/help/edge/overview.md##support-ticket)。

另请参阅[Cloud Manager中的Edge Delivery Services简介](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)。

**要将Edge Delivery站点添加到Cloud Manager，请执行以下操作：**

1. 在[`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 执行下列操作之一：

   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**&#x200B;选项卡。 然后，在页面的右下角附近，单击&#x200B;**添加Edge Delivery站点**。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * 在页面的左上角，单击![显示或隐藏侧面导航](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)以显示侧面导航菜单。
在**服务**&#x200B;标题下，单击![Edge Delivery网站的网页](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)**Edge Delivery网站**。
在页面的右上角附近，单击**添加站点**。

     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加Edge Delivery站点**&#x200B;对话框中，在必填字段中提供以下信息：

   | 文本字段 | 描述 |
   | - | --- |
   | 网站名称 | 输入要添加的Edge Delivery站点的名称。<br>该名称用作Cloud Manager中网站的唯一标识符。 |
   | 存储库 URL | 输入存储网站代码的Git存储库。<br>此字段允许Cloud Manager在部署过程中从该存储库中提取代码。 |
   | 网站描述（可选） | 输入要添加的Edge Delivery站点的简短说明。<br>描述有助于识别和区分站点，使管理和识别您添加的其他站点更加容易。 |

1. 单击对话框右下角的&#x200B;**添加**。

1. 在&#x200B;**验证存储库所有权**&#x200B;对话框中，执行以下步骤来验证存储库的所有权：

   | 步骤编号 | 描述 |
   | - | - |
   | **1** | 将路径和名称为`well-known/adobe/cloudmanager-challenge.txt`的文件添加到&#x200B;**存储库URL**&#x200B;字段中列出的Git存储库的`main`分支。 请&#x200B;*不*&#x200B;在位置路径的开头添加句点。<br>如有必要，请单击![复制](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以将路径复制到剪贴板。 |
   | **2** | 将步骤2中文本字段中显示的代码添加到您在步骤1中刚创建的文件。<br>如有必要，请单击![复制](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)以将代码复制到剪贴板。 |
   | **3** | 在Git存储库中为刚刚创建的更改创建拉取请求，然后将其合并到`main`以提交代码。 |

1. 单击&#x200B;**验证**。

验证存储库后，它在Edge Delivery sites表中的状态将变为一个绿色圆圈，其内带有白色复选标记。

在同一表中，您可以单击![有关Edge Delivery网站的信息。](https://spectrum.corp.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg)查看有关您站点的详细信息，如已验证的存储库URL以及预览和生产网站的URL。


