---
title: '[!DNL Experience Manager Assets]与 [!DNL Adobe Workfront]集成'
description: ' [!DNL Assets] 和 [!DNL Workfront]之间的集成简介'
role: Admin, Leader, Architect
feature: Workfront Integrations and Apps
exl-id: 365de3dc-51db-4dcf-94e2-104b5a5d33a8
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 7%

---

# [!DNL Adobe Experience Manager]作为[!DNL Cloud Service] [!DNL Assets]与[!DNL Adobe Workfront]集成 {#assets-integration-overview}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=zh-Hans) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Workfront]是一个工作管理应用程序，它帮助您在一个地方管理整个工作生命周期。 [!DNL Workfront]和[!DNL Adobe Experience Manager Assets]之间的集成使组织能够通过将工作和数字资产管理内在地连接起来，提高内容速度和上市时间。 在Workfront中管理其工作的情况下，用户有权访问所需的文档和图像。

Adobe选件与[原生集成 [!DNL Workfront] 和 [!DNL Adobe Experience Manager Assets] (支持Assets Essentials和Assets as a Cloud Service)](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=zh-Hans)。

通过本机Experience Manager集成，您可以：

* 在Workfront中快速设置集成。

* 自动创建在Workfront和Experience Manager之间链接的文件夹。

* 轻松同步现有链接资源的元数据。

* 当项目元数据在Workfront中进行更改时自动更新。

* 跨组织ID将多个Experience Manager Assets存储库顺利连接到一个Workfront环境，或将多个Workfront环境顺利连接到一个Experience Manager Assets存储库。


## Adobe Workfront for Experience Manager增强型连接器 {#enhanced-connector-information}


自2022年6月起，Adobe发布了一个新的原生集成，用于将Workfront与Adobe Experience Manager Assets as a Cloud Service连接。 这种集成已成为连接这两种解决方案的必需方法。 阻止将来Workfront与AEM Assets as a Cloud Service连接的增强型连接器（1.9.8及更高版本）的任何新实施。 有关如何设置此集成的更多信息，请参阅[配置Experience Manager Assets as a Cloud Service集成](workfront-connector-configure.md)。

>[!NOTE]
>
>Adobe不支持并行使用Workfront for Experience Manager增强型连接器和Experience Manager集成。

对于2022年6月之前的安装，请注意以下关于[!DNL Adobe Workfront for Experience Manager enhanced connector]部署和配置的要点：

* Adobe仅需要通过认证合作伙伴或[!DNL Adobe Professional Services]来部署和配置[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用认证合作伙伴或[!DNL Adobe Professional Services]进行部署和配置，则Adobe不支持该功能。
* Adobe可能会发布对[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]的更新，使此连接器冗余；如果发生这种情况，客户可能需要从使用此连接器过渡。
* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请参阅[增强型连接器安装说明](workfront-connector-install.md)的步骤5(a)。
* 查看Experience Manager Assets增强型连接器的[Workfront合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有关考试的信息，请参阅[考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。