---
title: 编辑程序
description: 了解如何在创建生产和沙盒程序后进行编辑，并调整其选项。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 53%

---


# 编辑程序 {#editing-programs}

要管理和编辑程序，请从 [**我的项目群** 控制台。](/help/implementing/cloud-manager/navigation.md) 此 **我的项目群** 页面提供了您有权访问的所有程序的概述。 在选择单个项目时， **项目概述** 页面提供程序的详细信息概览。

从 **项目概述**，具有必要权限的用户可以编辑 [在您的组织中创建的生产程序](creating-production-programs.md) 和 [在您的组织中创建的沙盒程序。](creating-sandbox-programs.md) 通过编辑项目，您可以：

* 将 Sites 解决方案添加到具有 Assets 的现有项目，反之亦然。
* 从具有 Sites 和 Assets 的现有项目中删除 Sites 或 Assets。
* 将另一未使用的解决方案权利添加到现有项目或添加为新项目。
* 删除沙盒项目。

## 权限 {#permissions}

您必须是 **业务负责人** 用于编辑程序或删除沙盒程序以及访问许可证仪表板的角色。

## 编辑程序 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](#my-programs)** 页面上，单击要编辑的程序以显示其详细信息。

1. 单击页面左上方的项目名称，然后选择&#x200B;**编辑项目**。

   ![“编辑程序”选项](assets/edit-program-overview.png)

1. 此 **编辑项目** 页面打开 **常规** 选项卡。

   ![“常规”选项卡](assets/edit-program-prod1.png)

1. 可用于编辑程序的选项与创建程序时的选项相同。
   * 请查看文档 [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) 和 [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) 了解各个选项的详细信息。
   * [其他选项](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#options) 可用于您的生产程序，具体取决于您组织的权利。

1. 单击&#x200B;**更新**&#x200B;以将更改保存到项目。

将保存对程序所做的更改。

>[!NOTE]
>
>无论何时编辑项目，包括添加或删除解决方案或加载项，这些更改都将在下次部署后生效。

## 删除沙盒项目 {#delete-sandbox-program}

删除沙盒项目将删除与其关联的所有环境和管道。

>[!TIP]
>
>具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以选择删除其生产和暂存环境，而非整个沙盒项目。

要删除沙盒项目，请执行以下操作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](#my-programs)** 页面上，单击要编辑的程序以显示其详细信息。

1. 单击页面左上角的程序名称，然后选择 **删除项目群**.

   ![“删除程序”选项](assets/delete-sandbox1.png)

或者，您可以从 Cloud Manager 概述页面单击程序卡上的省略号按钮，然后选择&#x200B;**删除程序**。

![从程序信息卡删除沙盒](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能删除沙盒程序。无法删除生产项目。
