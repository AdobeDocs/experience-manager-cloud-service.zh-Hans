---
title: 创建生产程序
description: 了解如何使用 Cloud Manager 创建自己的生产程序来托管实时流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 11%

---


# 创建生产程序 {#create-production-program}

生产程序适用于熟悉Adobe Experience Manager (AEM)和Cloud Manager的用户，这些用户可随时编写、构建和测试代码，其目的是将其部署为处理实时流量。

请参阅文档[了解程序和程序类型](program-types.md)以了解有关程序类型的更多信息。

## 创建生产程序 {#create}

根据您组织的权限，在添加程序时，您可能会看到其他生产程序选项。
查看[其他生产程序选项](#options)。

**创建生产程序：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台右上角附近，单击&#x200B;**添加程序**。

   ![Cloud Manager 登陆页面](assets/log-in.png)

1. 在&#x200B;*让我们创建程序*&#x200B;向导的&#x200B;**程序名称**&#x200B;文本字段中，键入您希望程序的名称。

1. 在&#x200B;**项目目标**&#x200B;下，选择![地球图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg)**为生产设置**。

   ![创建项目向导](assets/create-production-program.png)

1. （可选）在向导对话框的右下角，执行以下任一操作：

   * 将图像文件拖放到![图像图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **添加程序图像**&#x200B;目标上。
   * 单击![图像图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Image_18_N.svg) **添加程序图像**，然后从文件浏览器中选择图像。
   * 单击![删除图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_DeleteOutline_18_N.svg)可删除您添加的图像。

1. 单击&#x200B;**继续**。

1. 在&#x200B;**解决方案和加载项**&#x200B;列表框中，选择要包含在程序中的一个或多个解决方案。

   * 如果您不确定是否需要一个或多个项目来提供各种解决方案，请选择您最感兴趣的项目。您可以稍后通过[编辑项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)来激活其他解决方案。有关更多项目设置建议，请参阅[生产项目简介文件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
   * 需要您至少选择一个解决方案来创建程序。 例如，您可以选择为优化数字体验的完全托管的CDN解决方案选择&#x200B;**Edge Delivery Services**。 查看[关于使用Edge Delivery Services交付您的Cloud Manager项目](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md)

   ![选择解决方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/add-production-program-with-edge-v2.png)




   <!-- * If you selected the **[Enable Enhanced Security](#security)** option, you can select only as many solutions for which HIPAA entitlements are available. -->



   * 单击解决方案名称左侧的![300号的V形图标](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize300.svg)以显示任何可选的加载项。<!-- such as the **Commerce** add-on option under **Sites**. -->

   ![选择“插件”](assets/setup-prod-commerce.png)

1. 选择完解决方案和加载项后，单击&#x200B;**继续**。

1. 在&#x200B;**上线日期**&#x200B;选项卡上，输入您计划让生产程序上线的日期。

   ![定义计划上线日期](assets/set-up-go-live.png)

   * 您可以随时编辑此日期。
   * 日期用于提供信息并触发&#x200B;[**项目概述**&#x200B;页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview)上的上线构件。 此功能提供了到AEM as a Cloud Service最佳实践的及时产品内链接，以支持流畅的上线体验。

1. 单击&#x200B;**创建**。Cloud Manager会创建您的项目并将其显示在登录页面上以供选择。

   ![Cloud Manager 概述](assets/navigate-cm.png)

## 其他生产程序选项 {#options}

根据组织可用的权利，在创建生产程序时，您可能具有以下其他可用选项。

### 安全性 {#security}

如果您拥有必要的权限，**安全**&#x200B;选项卡在&#x200B;**`Set up for production`**&#x200B;对话框中会显示为第一个选项卡。

![安全选项](assets/create-production-program-security.png)

“**安全性**”选项卡提供用于为生产程序激活&#x200B;**HIPAA**&#x200B;或&#x200B;**WAF-DDOS保护**，或同时激活这两者的选项。

Adobe HIPAA兼容和WAF-DDOS（Web应用程序防火墙 — 分布式拒绝服务）促进了基于云的安全性，这是针对漏洞的多层防护方法的一部分。

* **HIPAA** — 此选项启用Adobe的HIPAA就绪解决方案实施。
   * [详细了解](https://www.adobe.com/trust/compliance/hipaa-ready.html) Adobe 的 HIPAA 就绪解决方案实施。
   * 程序创建后无法启用或禁用HIPAA。
* **WAF-DDOS保护** — 此选项通过规则启用Web应用程序防火墙以保护您的应用程序。
   * 激活后，可通过设置[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)来配置WAF-DDOS保护。
   * 请参阅[流量过滤器规则(包括WAF规则)](/help/security/traffic-filter-rules-including-waf.md)，了解如何管理存储库中的流量过滤器规则，以便正确部署这些规则。

### SLA {#sla}

如果您拥有必要的权限，**SLA**&#x200B;选项卡在&#x200B;**`Set up for production`**&#x200B;对话框中将显示为第二个或第三个选项卡。

![SLA选项](assets/create-production-program-sla.png)

Sites和Forms提供标准的99.9%service level agreement (SLA)。 **99.99% Service level agreement**&#x200B;选项可确保您的生产环境正常运行时间至少为99.99%，无论是Sites、Forms、Edge Delivery Services还是所有这三个环境。

99.99%的SLA可提供更高的可用性和更低的延迟。

对于Sites和Forms程序，99.99%的SLA要求将[附加发布区域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)应用于程序中的生产环境。 在满足启用99.99%SLA的[要求](#sla-requirements)时，必须运行[全栈管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)才能激活它。

对于Edge Delivery Services，除了在程序上配置99.99%的SLA许可证外，还有&#x200B;*否*&#x200B;要求。

#### SLA要求99.99% {#sla-requirements}

除了所需权利之外，使用适用于站点或Forms程序的99.99% SLA还附带以下其他要求：

* 在将99.99%的SLA应用于计划时，该组织必须具有99.99%的SLA和附加的发布区域权利。
* Cloud Manager在将99.99%的SLA应用于程序之前，验证未使用的[附加发布区域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)权利是否可用。
* 在编辑项目时，如果项目已包含至少具有一个其他发布区域的生产环境，则Cloud Manager仅检查99.99%的SLA权利的可用性。
* 为了激活99.99%的SLA和报表，必须已创建[生产/暂存环境](/help/implementing/cloud-manager/manage-environments.md#adding-environments)，并且必须在生产/暂存环境中至少应用了一个附加发布区域。
   * 如果使用[高级联网](/help/security/configuring-advanced-networking.md)，请务必查看[将多个发布区域添加到新环境](/help/implementing/cloud-manager/manage-environments.md#adding-regions)文档以获取建议，以便在出现区域故障时保持连接。
* 您的99.99%SLA计划必须始终包括至少一个额外的发布区域。 不允许用户从项目群中删除剩余的最后一个附加发布区域。
* 对于已启用Sites或SLA解决方案的生产程序，您的99.99%的Forms受支持。
* 运行[全栈管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)以激活或在编辑程序时停用99.99%的SLA。

## 访问您的项目 {#accessing}

1. 当您在登录页面上看到您的项目卡时，请单击![更多图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)以查看您可用的菜单选项。

   ![程序概述](assets/program-overview.png)

1. 选择&#x200B;**程序概述**&#x200B;信息卡，可导航至 Cloud Manager **概述**&#x200B;页面。

1. 概述页面上的主call-to-action信息卡将指导您创建环境、非生产管道，最后创建生产管道。

   ![程序概述](assets/set-up-prod5.png)

>[!TIP]
>
>有关如何导航Cloud Manager以及了解[我的程序](/help/implementing/cloud-manager/navigation.md)控制台的详细信息，请参阅&#x200B;**导航Cloud Manager UI**。

>[!NOTE]
>
>与[沙盒程序](introduction-sandbox-programs.md#auto-creation)不同，生产程序要求具有相应Cloud Manager角色的用户通过自助服务UI创建项目并添加环境。


