---
title: 对AEM Commerce作为Cloud Service的显着变化
description: 与Adobe Experience Manager6.5相比，AEM Commerce作为Cloud Service的变化显着。
translation-type: tm+mt
source-git-commit: 5a90db8791dd92cceb811b9ed2beda3ecb4a974d
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 5%

---


# Notable changes to AEM Commerce as a Cloud Service {#notable-changes}

Adobe Experience Manager作为Cloud Service，为管理AEM项目提供了许多新功能和可能性。 本文档强调了内部部署、Adobe托管服务和Experience Manager作为Cloud Service的商务集成框架(CIF)之间商务功能的重要区别。 有关其他更改，请参阅将 [Experience Manager作为Cloud Service的常规更改](/help/release-notes/aem-cloud-changes.md)。

与Experience Manager6.5相比，主要区别在于：
* [支持CIF Classic](#cif-classic)
* [部署CIF创作工具](#cif-tools)
* [从本地和Adobe托管服务转变](#moving-cif-cs)

## 支持CIF经典／快速启动Experience Manager作为Cloud Service {#cif-classic}

在Experience Manager中，不再以Cloud Service形式提供包含产品导入程序以导入和存储产品目录的经典商务集成框架。 在Experience Manager中不支持使用经典CIF作为Cloud Service，使用经典CIF的项目必须用支持的版本取代经典CIF实施，如在Experience Manager上 [CIF作为Cloud Service所述](https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.en/blob/cif/help/commerce-cloud/architecture.md)

## 部署CIF {#deployment}

下面显示了不同AEM产品的商务集成框架的不同部署模型：

|  | AEM内部部署 | AEMManaged Services | AEMCloud Service |
|-------------     |-----------|-----------|-----------|
| 如何为Magento后端部署CIF创作工具 | [请参阅AEM](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 6.5支持的CIF连接器 | [请参阅AEM](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 6.5支持的CIF连接器 | AEM作为Cloud Service，需要随CIF加载项提供。 有关更多详细信息，请与销售代表联系 |
| 如何部署 [CIF Venia项目](https://github.com/adobe/aem-cif-guides-venia) | AEM包安装 | 通过Cloud Manager完 [成部署](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) | 项目已移 [入Cloud Manager Git存储库](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) ，并通过Cloud Manager [完成部署](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/deploying/overview.html) |

>[!NOTE]
>
>CIF Classic/Quickstart版本的商务集成框架可用于AEM内部部署产品，但用例非常有限。 但是，这不是推荐的解决方案。

## 从内部部署和Managed Services转向AEM商务作为Cloud Service {#moving-cif-cs}

从AEM内部部署或Managed Services安装到AEM作为Cloud Service的客户需要对AEM项目进行一些细微调整。

如上所述，CIF连接器需要进行第一次调整。 CIF连接器由CIF附加组件取代，CIF附加组件由Adobe部署。 因此，请勿将CIF连接器作为Cloud Service安装在AEM上。 此外，不支持与本地AEM Cloud SDK一起使用，Adobe还为本地开发提供CIF附 [加组件](develop.md)。

其次，了解AEM [项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) ，以及AEM作为Cloud Service的特点。 将项目设置调整为AEM作为Cloud Service布局。
主要区别在于：

* GraphQL客户端OSGI **捆绑** 不能再包含在AEM项目中，它通过CIF加载项进行部署
* GraphQL客户端和Graphql数据服务的OSGI **配置不** 能再包含到AEM项目中

>[!TIP]
>
>查看GitHub [上的AEM](https://github.com/adobe/aem-cif-guides-venia) Venia Reference Store项目。 此项目为AEM的Maven用户档案提供了Cloud Service和内部部署，其中考虑了不同的框架条件。
