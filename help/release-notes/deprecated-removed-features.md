---
title: 已弃用和已删除的功能
description: 发行说明特定于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service]中已弃用和已移除的功能。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 8294709d6c5685fd5b88a52835b4082e3e713a51
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 33%

---

# 已弃用和已删除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as aCloud Service中已弃用和已删除的功能"
>abstract="AEM as aCloud Service具有云原生部署模型。 某些功能和特性已由云原生对应功能和特性进行替换，此选项卡会显示这些特性。"


Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外，由于[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]提供云原生部署模型，因此某些功能和特性已被云原生对应功能和特性所取代。

要传达即将移除/替换[!DNL Experience Manager]功能，请应用以下规则：

1. 首先宣布弃用。已弃用的功能仍可用，但不会进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了在[!DNL Experience Manager]中标记为[!DNL Cloud Service]的已弃用的特性和功能。 通常，首先将在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了该功能，并制定计划以更改其实施以使用提供的替代功能。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | 基于模板的简单内容片段。 | [基于模型的结构化内容](/help/assets/content-fragments/content-fragments-models.md) 片段。 |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资产摄取现在使用[资产微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资产直接上传到[!DNL Experience Manager]。请参阅[已弃用的资产上传API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | [不支持工](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) 作流 `DAM Asset Update` 中的某些工作流步骤，包括如调用命令行工 [!DNL ImageMagick]具。 | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资产微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 复制代理的“分发”选项卡下的树复制UI（在2021年9月30日之后删除） | [管理发](/help/operations/replication.md#manage-publication) 布或发 [布内容树工作](/help/operations/replication.md#publish-content-tree-workflow) 流程方法 |

## 已删除功能 {#removed-features}

本部分列出了从[!DNL Experience Manager]中删除的将[!DNL Experience Manager]作为[!DNL Cloud Service]的特性和功能。

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| 用户界面 | 经典UI将从产品用户界面中删除。 一些经典UI对话框可用于一些选择功能，如链接检查器、版本清除和某些Cloud Service配置。 即将发布的[产品更新](/help/release-notes/home.md)可能会进一步删除经典UI的可用性。 | 标准 UI |
| [!DNL Dynamic Media] | 以前与[Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration)和[Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)的集成在[!DNL Experience Manager]中作为[!DNL Cloud Service]不可用。 | 使用[随[!DNL Experience Manager]提供的Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)作为[!DNL Cloud Service]。 |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 这些功能已在[!DNL Experience Manager] 6.4中弃用，现在已从[!DNL Experience Manager]中删除。 |
| [!DNL Sites] | 设计导入程序 | 此功能已被删除，因为[!DNL Experience Manager]存储库的不可更改部分在运行时无法访问。 |
| [!DNL Assets] | [!DNL Assets] 与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务共享功能不可用。 | 要与[!DNL Adobe Creative Cloud]集成，请使用[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 |
| [!DNL Foundation] | 支持Apache Sling数据源（OSGi包org.apache.sling.datasource）。 | 不适用 |

## Java API {#java-api}

有关任何已弃用或已删除的Java API（有时会引入）的信息，请参阅[此页面](/help/release-notes/deprecated-apis.md)。

## OSGI配置 {#osgi-configuration}

有关配置OSGi属性的任何限制，请参阅[本文](/help/implementing/deploying/osgi-configuration-api.md)，其中一些限制可能会随着时间推移引入。
