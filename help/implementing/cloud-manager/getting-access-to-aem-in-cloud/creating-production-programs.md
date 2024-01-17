---
title: 创建生产程序
description: 了解如何使用 Cloud Manager 创建自己的生产程序来托管实时流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
source-git-commit: 79d3ec7f5ede84fd989b7d5440739ec9560a547f
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 64%

---


# 创建生产程序 {#create-production-program}

生产程序面向熟悉 AEM 和 Cloud Manager 并准备好开始编写、构建和测试代码的用户，目的是将其部署到托管实时流量。

请参阅[了解程序和程序类型](program-types.md)文档，了解有关程序类型的更多信息。

## 创建生产程序 {#create}

按照以下步骤创建生产程序。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在 **[我的项目群](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** 屏幕，点击或单击 **添加项目** 在屏幕的右上角。

   ![Cloud Manager 登陆页面](assets/log-in.png)

1. 在“创建项目向导”中，选择&#x200B;**设置生产**，以创建生产项目 并提供项目名称。

   ![创建项目向导](assets/create-production-program.png)

1. 或者，您也可以将图像文件拖放到&#x200B;**添加项目图像**&#x200B;目标，或单击它以从文件浏览器中选择图像，从而将图像添加到项目中。选择&#x200B;**继续**。

1. 如果您拥有必要的权限， **安全性** 选项卡，并提供激活的选项 **HIPAA** 和/或 **WAF-DDOS保护** 用于您的生产程序。 如果您正在创建的程序有需要，请勾选适用的选项，然后选择 **继续**.

   * 程序创建后无法启用或禁用HIPAA。
      * [详细了解](https://www.adobe.com/go/hipaa-ready_cn) Adobe 的 HIPAA 就绪解决方案实施。
   * 激活后，可以通过设置 [非生产管道。](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)

   ![安全选项](assets/create-production-program-security.png)

1. 在&#x200B;**解决方案和插件** 选项卡，选择要包含在程序中的解决方案。

   * 如果您不确定是否需要一个或多个项目来提供各种解决方案，请选择您最感兴趣的项目。您可以稍后通过[编辑项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)来激活其他解决方案。有关更多项目设置建议，请参阅[生产项目简介文件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
   * 如果您之前选择了&#x200B;**启用增强安全性**，您只能选择 HIPAA 权利可用的解决方案。

   ![选择解决方案](assets/setup-prod-select.png)

1. 单击解决方案名称前的>形符号显示可选的插件，例如选择 **商务** 下的附加选项 **站点**.

   ![选择“插件”](assets/setup-prod-commerce.png)

1. 选择了解决方案和加载项后，单击&#x200B;**继续**。

1. 在&#x200B;**上线日期**&#x200B;选项卡，输入您计划生产程序上线的日期。

   ![定义计划上线日期](assets/setup-go-live.png)

   * 可以随时编辑此日期。
   * 此日期仅供参考，并触发上的上线构件 [**项目概述** 页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview) 及时提供产品内链接到AEMas a Cloud Service最佳实践文档，配合您的入门培训历程，最终获得成功、流畅的上线体验。

1. 单击&#x200B;**创建**。

您的程序由 Cloud Manager 创建，并在登陆页面上显示和选择。

![Cloud Manager 概述](assets/navigate-cm.png)

## 访问您的程序 {#accessing}

1. 在登陆页面上看到项目卡时，选择省略号按钮以查看可用的菜单选项。

   ![程序概述](assets/program-overview.png)

1. 选择&#x200B;**程序概述**&#x200B;信息卡，可导航至 Cloud Manager **概述**&#x200B;页面。

1. 概述页面上的主要行动号召信息卡将指导您创建环境、非生产管道，最后创建生产管道。

   ![程序概述](assets/set-up-prod5.png)

如果在任何时候您需要切换到另一个程序或返回概述页面创建另一个程序，请单击屏幕左上角的程序名称，可显示 **导航到** 选项。

![导航至](assets/create-program-a1.png)

>[!NOTE]
>
>与[沙盒程序不同，](introduction-sandbox-programs.md#auto-creation)生产程序将要求具有相应 Cloud Manager 角色的用户通过自助服务 UI 创建项目并添加环境。
