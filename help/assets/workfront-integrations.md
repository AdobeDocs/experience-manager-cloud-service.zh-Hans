---
title: ’[!DNL Experience Manager Assets] 与集成 [!DNL Adobe Workfront]’
description: 集成简介 [!DNL Assets] 和 [!DNL Workfront]
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: ab2cf8007546f538ce54ff3e0b92bb0ef399c758
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] 与集成 [!DNL Adobe Workfront] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Workfront] 是一个工作管理应用程序，帮助您在一个地方管理整个工作生命周期。 之间的集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 允许组织通过将工作和数字资产管理内在地联系起来，提高内容速度和上市时间。 在Workfront中管理其工作的情况下，用户有权访问所需的文档和图像。

Adobe优惠至 [集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] 本机(as a Cloud Service支持Assets Essentials和资源)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html).

通过本机Experience Manager集成，您可以：

* 在Workfront中快速设置集成。

* 自动创建在Workfront和Experience Manager之间链接的文件夹。

* 轻松同步现有链接资源的元数据。

* 当项目元数据在Workfront中进行更改时自动更新。

* 跨组织ID将多个Experience Manager Assets存储库顺利连接到一个Workfront环境，或将多个Workfront环境顺利连接到一个Experience Manager Assets存储库。


## Adobe WorkfrontExperience Manager增强型连接器 {#enhanced-connector-information}


自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assetsas a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来Workfront与AEM Assetsas a Cloud Service连接的增强型连接器（1.9.8及更高版本）的任何新实施。 有关如何设置此集成的更多信息，请参阅 [配置Experience Manager Assetsas a Cloud Service集成](workfront-connector-configure.md).

>[!NOTE]
>
>Adobe不支持将Workfront用于Experience Manager增强型连接器和Experience Manager并行集成。

对于2022年6月之前的安装，请注意以下关于部署和配置的要点 [!DNL Adobe Workfront for Experience Manager enhanced connector]：

* Adobe需要部署和配置 [!DNL Adobe Workfront for Experience Manager enhanced connector] 仅通过认证合作伙伴或 [!DNL Adobe Professional Services]. 如果部署与配置时没有认证合作伙伴或 [!DNL Adobe Professional Services]，Adobe不支持它。
* Adobe可能会将更新发布到 [!DNL Adobe Workfront] 和 [!DNL Adobe Experience Manager] 使此连接器成为冗余连接器；如果发生这种情况，客户可能需要从使用此连接器过渡到使用此连接器。
* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强的连接器版本，请参阅的步骤5(a) [增强型连接器安装说明](workfront-connector-install.md).
* 请参阅 [Workfront for Experience Manager Assets增强型连接器的合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). 有关考试的信息，请参见 [考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).