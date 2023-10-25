---
title: 编辑程序
description: 了解如何在创建生产和沙盒程序后进行编辑，并调整其选项。
exl-id: 819e4a6e-f77a-4594-a402-a300dcbdf510
source-git-commit: ecb168e9261b3e3ed89e4cbe430b3da9f777a795
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 89%

---

# 编辑程序 {#editing-programs}

具有必要权限的用户可以编辑[在您的组织中创建的生产项目](creating-production-programs.md)以及在您的企业中创建的[沙盒项目。](creating-sandbox-programs.md) 通过编辑项目，您可以：

* 将 Sites 解决方案添加到具有 Assets 的现有项目，反之亦然。
* 从具有 Sites 和 Assets 的现有项目中删除 Sites 或 Assets。
* 将另一未使用的解决方案权利添加到现有项目或添加为新项目。
* 删除沙盒项目。

## 权限 {#permissions}

您必须是&#x200B;**业务负责人**&#x200B;角色的成员才能编辑程序或删除沙盒程序。

## 编辑程序 {#editing}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要编辑的项目以显示其详细信息。

1. 单击页面左上方的项目名称，然后选择&#x200B;**编辑项目**。

   ![“编辑程序”选项](assets/edit-program-overview.png)

1. **编辑程序**&#x200B;页面将打开。在&#x200B;**常规**&#x200B;选项卡上，编辑程序名称和描述。

   * 必须为程序选择至少一个解决方案。

   ![“常规”选项卡](assets/edit-program-prod1.png)

1. 在&#x200B;**解决方案和插件**&#x200B;选项卡，修改程序的解决方案。

   ![选择解决方案](assets/edit-prg.png)

1. 单击解决方案名称前的 V 形符号以显示可选的加载项，例如在 **Sites** 下选择 **Commerce** 加载项选项。

   ![编辑插件](assets/edit-program-add-on.png)

1. 在&#x200B;**上线设置**&#x200B;选项卡，修改程序的计划上线日期。

   ![编辑上线设置](assets/edit-program-go-live.png)

   * 该日期仅供参考。它会触发项目概述页面上的“上线”构件。反过来，它提供了 Adobe Experience Manager (AEM) as a Cloud Service 最佳实践文档的产品内链接以与您的历程保持一致，最终提供成功的上线体验。
   * 该选项卡在沙盒项目中不可用。

1. 如果程序有所需的权利， **安全性** 选项卡将显示可在何处修改程序的安全选项。

   ![编辑安全设置](assets/edit-program-security.png)

   * HIPAA在以下时间后无法启用或禁用： [项目创建。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
      * [详细了解](https://www.adobe.com/go/hipaa-ready_cn) Adobe 的 HIPAA 就绪解决方案实施。
   * 激活后，可以通过设置 [非生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   {{waf-limited-release}}

1. 单击&#x200B;**更新**&#x200B;以将更改保存到项目。

无论何时编辑项目，包括添加或删除解决方案或加载项，这些更改都将在下次部署后生效。

## 删除沙盒项目 {#delete-sandbox-program}

删除沙盒项目将删除与其关联的所有环境和管道。

>[!TIP]
>
>具有&#x200B;**业务负责人**&#x200B;或&#x200B;**部署管理员**&#x200B;角色的用户可以选择删除其生产和暂存环境，而非整个沙盒项目。

要删除沙盒项目，请执行以下操作。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击要编辑的项目以显示其详细信息。

1. 单击页面左上方的项目名称，然后选择&#x200B;**删除项目**。

   ![“删除程序”选项](assets/delete-sandbox1.png)

或者，您可以从 Cloud Manager 概述页面单击程序卡上的省略号按钮，然后选择&#x200B;**删除程序**。

![从程序信息卡删除沙盒](assets/delete-sandbox2.png)

>[!NOTE]
>
>只能删除沙盒程序。无法删除生产项目。
