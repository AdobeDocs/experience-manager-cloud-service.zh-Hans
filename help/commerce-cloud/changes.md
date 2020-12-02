---
title: 对AEM Commerce作为Cloud Service的显着变化
description: 与Adobe Experience Manager6.5相比，AEM Commerce作为Cloud Service的变化显着。
translation-type: tm+mt
source-git-commit: 2934d0d8d3977bb7884bae9654ac26e9fa57b34f
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 5%

---


# 对AEM Commerce作为Cloud Service{#notable-changes}的显着更改

Adobe Experience Manager作为Cloud Service，为管理AEM项目提供了许多新功能和可能性。 本文档强调了内部部署、Adobe托管服务和Experience Manager作为Cloud Service的商务集成框架(CIF)之间商务功能的重要区别。 有关其他更改，请参阅通用[将Experience Manager更改为Cloud Service](/help/release-notes/aem-cloud-changes.md)。

与Experience Manager6.5相比，主要区别在于：
* [支持CIF Classic](#cif-classic)
* [部署CIF创作工具](#cif-tools)
* [从本地和Adobe托管服务转变](#moving-cif-cs)

## 支持将CIF经典／快速启动Experience Manager作为Cloud Service{#cif-classic}

在Experience Manager中，不再以Cloud Service形式提供包含产品导入程序以导入和存储产品目录的经典商务集成框架。 在Experience Manager中不支持使用经典CIF作为Cloud Service，使用经典CIF的项目必须用Experience Manager上的[CIF作为Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/architecture/magento.html#overview)所述的支持版本取代经典CIF实施

## 部署CIF {#deployment}

下面显示了不同AEM产品的商务集成框架的不同部署模型：

|  | AEM内部部署 | AEMManaged Services | AEMCloud Service |
|-------------     |-----------|-----------|-----------|
| 如何为Magento后端部署CIF创作工具 | [请参阅AEM ](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 6.5上支持的CIF连接器 | [请参阅AEM ](https://github.com/adobe/commerce-cif-connector/blob/master/README.md) 6.5上支持的CIF连接器 | AEM作为Cloud Service，需要随CIF加载项提供。 有关更多详细信息，请与销售代表联系 |
| 如何部署[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) | AEM包安装 | 通过[云管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)完成部署 | 项目已移入[Cloud Manager Git存储库](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)，并通过[ Cloud Manager](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/deploying/overview.html)完成部署 |

>[!NOTE]
>
>有关如何将CIF与AEM Managed Service或AEM内部部署一起使用的其他文档，请参阅[商务集成框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)

>[!NOTE]
>
>CIF Classic/Quickstart版本的商务集成框架可用于AEM内部部署产品，但用例非常有限。 但是，这不是推荐的解决方案。

## 从内部部署和Managed Services{#moving-cif-cs}移至AEM Commerce作为Cloud Service

从AEM内部部署或Managed Services安装到AEM作为Cloud Service的客户需要对AEM项目进行一些细微调整。

如上所述，CIF连接器需要进行第一次调整。 CIF连接器由CIF附加组件取代，CIF附加组件由Adobe部署。 因此，请勿将CIF连接器作为Cloud Service安装在AEM上。 此外，不支持与本地AEM Cloud SDK一起使用，Adobe还为[本地开发](develop.md)提供CIF加载项。

其次，了解[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)和AEM作为Cloud Service的特性。 将项目设置调整为AEM作为Cloud Service布局。
主要区别在于：

* GraphQL客户端OSGI包&#x200B;**不能再**&#x200B;包含在AEM项目中，它通过CIF加载项进行部署
* GraphQL客户端和Graphql数据服务&#x200B;**的OSGI配置不能再**&#x200B;包含在AEM项目中

>[!TIP]
>
>查看GitHub上的[AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)项目。 此项目为AEM的Maven用户档案提供了Cloud Service和内部部署，其中考虑了不同的框架条件。
