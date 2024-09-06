---
title: 创建生产程序
description: 了解如何使用 Cloud Manager 创建自己的生产程序来托管实时流量。
exl-id: 4ccefb80-de77-4998-8a9d-e68d29772bb4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6a3d2d484bde20586b329010cdfe156570e736f5
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 12%

---


# 创建生产程序 {#create-production-program}

生产程序适用于熟悉AEM和Cloud Manager、可以随时编写、构建和测试代码的用户，目标是将其部署到处理实时流量。

请参阅文档[了解程序和程序类型](program-types.md)以了解有关程序类型的更多信息。

## 创建生产程序 {#create}

根据您组织的权限，您在添加项目时可能会看到[其他选项](#options)。

**创建生产程序：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 在&#x200B;**[我的程序](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;控制台右上角附近，单击&#x200B;**添加程序**。

   ![Cloud Manager 登陆页面](assets/log-in.png)

1. 在&#x200B;*让我们创建程序*&#x200B;向导的&#x200B;**程序名称**&#x200B;文本字段中，键入您希望程序的名称。

1. 在&#x200B;**项目目标**&#x200B;下，选择&#x200B;**`Set up for production`**。

   ![创建项目向导](assets/create-production-program.png)

1. （可选）在向导对话框的右下角，执行以下任一操作：

   * 将图像文件拖放到&#x200B;**添加项目图像**&#x200B;目标上。
   * 单击&#x200B;**添加程序图像**，然后从文件浏览器中选择图像。
   * 单击垃圾桶图标可删除您添加的图像。

1. 单击&#x200B;**继续**。

1. 在&#x200B;**解决方案和加载项**&#x200B;列表框中，选择要包含在程序中的一个或多个解决方案。

   * 如果您不确定是否需要一个或多个项目来提供各种解决方案，请选择您最感兴趣的项目。您可以稍后通过[编辑项目](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md)来激活其他解决方案。有关更多项目设置建议，请参阅[生产项目简介文件](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
   * 程序创建至少需要一个解决方案。
   * 为优化数字体验的完全托管的CDN解决方案选择&#x200B;**Edge Deliver Services**。 查看[关于使用Edge Delivery Services交付您的Cloud Manager项目](#edge-overview)
   * 如果您选择了&#x200B;**[启用增强安全性](#security)**&#x200B;选项，则您只能选择HIPAA权利可用的解决方案。

   ![选择解决方案](/help/implementing/cloud-manager/assets/add-production-program-with-edge.png)

1. 单击解决方案名称左侧的>形标记可显示任何可选的加载项，例如&#x200B;**站点**&#x200B;下的&#x200B;**Commerce**&#x200B;加载项选项。

   ![选择“插件”](assets/setup-prod-commerce.png)

1. 选择了解决方案和加载项后，单击&#x200B;**继续**。

1. 在&#x200B;**上线日期**&#x200B;选项卡上，输入您计划让生产程序上线的日期。

   ![定义计划上线日期](assets/set-up-go-live.png)

   * 您可以随时编辑此日期。
   * 日期用于提供信息并触发&#x200B;[**项目概述**&#x200B;页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#program-overview)上的上线构件。 此功能提供了到AEM as a Cloud Service最佳实践的及时产品内链接，以支持流畅的上线体验。

1. 单击&#x200B;**创建**。Cloud Manager会创建您的项目并将其显示在登录页面上以供选择。

![Cloud Manager 概述](assets/navigate-cm.png)

## 其他生产程序选项 {#options}

根据组织可用的权利，在创建生产程序时，您可能还有其他可用选项。

### 安全性 {#security}

如果您拥有必要的权限，**安全**&#x200B;选项卡在&#x200B;**`Set up for production`**&#x200B;对话框中会显示为第一个选项卡。

![安全选项](assets/create-production-program-security.png)

“**安全性**”选项卡提供用于为生产程序激活&#x200B;**HIPAA**&#x200B;或&#x200B;**WAF-DDOS保护**，或同时激活这两者的选项。

符合AdobeHIPAA标准且WAF-DDOS（Web应用程序防火墙 — 分布式拒绝服务）作为针对漏洞的多层防护方法的一部分促进了基于云的安全性。

* **HIPAA** — 此选项启用Adobe的HIPPA就绪解决方案实现。
   * [详细了解](https://www.adobe.com/trust/compliance/hipaa-ready.html) Adobe 的 HIPAA 就绪解决方案实施。
   * 程序创建后无法启用或禁用HIPAA。
* **WAF-DDOS保护** — 此选项通过规则启用Web应用程序防火墙以保护您的应用程序。
   * 激活后，可通过设置[非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)来配置WAF-DDOS保护。
   * 请参阅[流量过滤器规则(包括WAF规则)](/help/security/traffic-filter-rules-including-waf.md)，了解如何管理存储库中的流量过滤器规则，以便正确部署这些规则。

### SLA {#sla}

如果您拥有必要的权限，**SLA**&#x200B;选项卡在&#x200B;**`Set up for production`**&#x200B;对话框中将显示为第二个或第三个选项卡。

![SLA选项](assets/create-production-program-sla.png)

AEM Sites和Forms之间签订了标准的99.9%服务级别协议(SLA)。 **99.99%服务级别协议**&#x200B;选项允许将您的生产环境的最短正常运行时间百分比设为99.99%用于Sites和/或Forms。

99.99%的SLA可提供更高的可用性和更低的延迟，并需要将[额外的发布区域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)应用于程序中的生产环境。

在满足启用99.99%SLA的[要求](#sla-requirements)时，必须运行[全栈管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)才能激活它。

#### SLA要求99.99% {#sla-requirements}

在所需权利之外，99.99%的SLA还有额外的使用要求。

* 在将99.99%的SLA应用于计划时，该组织必须具有99.99%的SLA和附加的发布区域权利。
* Cloud Manager在将99.99%的SLA应用于程序之前，验证未使用的[附加发布区域](/help/implementing/cloud-manager/manage-environments.md#multiple-regions)权利是否可用。
* 在编辑项目时，如果项目已包含至少具有一个其他发布区域的生产环境，则Cloud Manager仅检查99.99%的SLA权利的可用性。
* 为了激活99.99%的SLA和报表，必须已创建[生产/暂存环境](/help/implementing/cloud-manager/manage-environments.md#adding-environments)，并且必须在生产/暂存环境中至少应用了一个附加发布区域。
   * 如果使用[高级联网](/help/security/configuring-advanced-networking.md)，请务必查看[将多个Publish区域添加到新环境](/help/implementing/cloud-manager/manage-environments.md#adding-regions)文档以获取建议，以便在出现区域故障时保持连接。
* 您的99.99%SLA项目中必须保留至少一个其他发布区域。 不允许用户从99.99%的SLA程序中删除最后一个附加发布区域。
* 99.99%的SLA都支持启用了Sites或Forms解决方案的生产程序。
* 运行[全栈管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md)以激活或在编辑程序时停用99.99%的SLA。

## 访问您的项目 {#accessing}

1. 在登陆页面上看到项目卡时，选择省略号按钮以查看可用的菜单选项。

   ![程序概述](assets/program-overview.png)

1. 选择&#x200B;**程序概述**&#x200B;信息卡，可导航至 Cloud Manager **概述**&#x200B;页面。

1. 概述页面上的主要行动号召信息卡将指导您完成创建环境、非生产管道，最后创建生产管道。

   ![程序概述](assets/set-up-prod5.png)

>[!TIP]
>
>有关如何导航Cloud Manager以及了解&#x200B;**我的程序**&#x200B;控制台的详细信息，请参阅[导航Cloud Manager UI](/help/implementing/cloud-manager/navigation.md)。

>[!NOTE]
>
>与[沙盒程序](introduction-sandbox-programs.md#auto-creation)不同，生产程序要求具有相应Cloud Manager角色的用户通过自助服务UI创建项目并添加环境。


