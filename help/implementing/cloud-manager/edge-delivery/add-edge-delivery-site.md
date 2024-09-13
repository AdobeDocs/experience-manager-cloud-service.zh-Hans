---
title: 将Edge Delivery站点添加到Cloud Manager
description: 了解如何将Edge Delivery站点添加到生产程序或沙盒程序。
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


## 将Edge Delivery站点添加到Cloud Manager {#eds-add-site}

将Edge Delivery Services添加到生产程序后，您的Edge Delivery Services许可证将应用于该程序。

“概述”页面上显示名为&#x200B;**Edge Delivery**&#x200B;的可单击选项卡。 单击选项卡会显示一个表格，其中列出了您已添加的每个Edge Delivery站点。 在左侧导航面板的&#x200B;**服务**&#x200B;分组下，注意名为&#x200B;**Edge Delivery Sites**&#x200B;的菜单选项。

![概述页面在左侧导航面板中显示Edge Delivery Sites，并在“Publish交付”选项卡右侧显示Edge Delivery选项卡](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**要将Edge Delivery站点添加到Cloud Manager，请执行以下操作：**

1. 在[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)登录Cloud Manager并选择适当的程序。
1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台上，选择已配置Edge Delivery Services的程序，并从中添加Edge Delivery站点。
1. 执行以下任一操作：
   * 从&#x200B;**项目概述**&#x200B;页面，单击&#x200B;**Edge Delivery**&#x200B;选项卡。 然后，在页面的右下角附近，单击&#x200B;**添加Edge Delivery站点**。

     ![从Edge Delivery选项卡添加Edge Delivery站点](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     **Edge Delivery待办事项列表**&#x200B;是可选的入门清单指南，旨在帮助您开始使用Edge Delivery，如上图所示。 请参阅[关于Edge Delivery待办事项列表](#ed-todo-list)。

   * 在页面的左上角，单击汉堡图标以显示左侧导航菜单。 在&#x200B;**服务**&#x200B;标题下，单击&#x200B;**Edge Delivery站点**。 在页面的右上角附近，单击&#x200B;**添加站点**。

     ![从Edge Delivery站点添加Edge Delivery站点按钮](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. 在&#x200B;**添加Edge Delivery站点**&#x200B;对话框中，执行以下操作：

   | 文本字段 | 要做什么 |
   | --- | --- |
   | 网站名称 | 输入要添加的Edge Delivery站点的名称。 该名称将用作Cloud Manager中站点的唯一标识符。 |
   | 存储库 URL | 此字段是指存储网站代码的Git存储库。<br>输入Git存储库的URL，该URL包含您的Edge Delivery站点所需的文件和资源(例如HTML、CSS、JavaScript和其他Web资源)。 这种安排允许Cloud Manager在部署过程中从该存储库中提取代码。 |
   | 网站描述（可选） | 输入要添加的Edge Delivery站点的简短说明。<br>此描述有助于识别和区分站点，使管理和识别您添加的其他站点更加容易。 您可能希望包括有关站点用途、内容的详细信息，或任何其他有助于阐明其功能或范围的相关信息。 |

1. 单击对话框右下角的&#x200B;**添加**。

1. 在&#x200B;**验证存储库所有权**&#x200B;对话框中，执行以下任一操作：

   | 步骤 | 描述 |
   | --- | --- |
   | 1 | 添加文件，该文件具有在&#x200B;**存储库URL**&#x200B;字段中列出的Git存储库的`main`分支的位置路径。 如有必要，请单击复制图标以将路径复制到剪贴板。<br>位置路径为：<br>`well-known/adobe/cloudmanager-challenge.txt`。<br><br>请&#x200B;*不*&#x200B;添加位置路径开头的句点，位于：<br>`.well-known/adobe/cloudmanager-challenge.txt` |
   | 2 | 将生成的代码添加到您在步骤1中创建的文件中。 如有必要，请单击复制图标以将代码复制到剪贴板。 |
   | 3 | 在Git存储库中，创建拉取请求，然后将其合并以提交代码。 |

1. 单击&#x200B;**验证**。 验证存储库后，其在Edge交付站点表格中的状态将更改为绿色圆圈，并在其内部显示白色复选标记。
