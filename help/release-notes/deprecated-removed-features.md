---
title: 已弃用和已删除的功能
description: 发行说明特定于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: e613ba71347d60dd9c4a2cdd6da8bd0696b00070
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 32%

---

# 已弃用和已删除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service中已弃用和已删除的功能"
>abstract="AEMas a Cloud Service具有云原生部署模型。 某些功能和特性已由云原生对应功能和特性进行替换，此选项卡会显示这些特性。"


Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外， [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供云原生部署模型，某些功能和特性已被云原生对应功能和特性所取代。

传达即将移除/替换 [!DNL Experience Manager] 功能，则应用以下规则：

1. 首先宣布弃用。已弃用的功能仍可用，但不会进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了在 [!DNL Experience Manager] as a [!DNL Cloud Service]. 通常，首先将在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了该功能，并制定计划以更改其实施以使用提供的替代功能。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | 的体验片段属性 **社交媒体状态**. | 该功能很快将被删除。 |
| [!DNL Sites] | 基于模板的简单内容片段。 | [基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md) 现在。 |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资产摄取现在使用[资产微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资产直接上传到 [!DNL Experience Manager].请参阅 [已弃用的资产上传API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | [某些工作流步骤](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) in `DAM Asset Update` 不支持工作流，包括如调用命令行工具 [!DNL ImageMagick]. | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资产微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 复制代理的“分发”选项卡下的树复制UI（在2021年9月30日之后删除） | [管理发布](/help/operations/replication.md#manage-publication) 或 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) 方法 |

## 已删除功能 {#removed-features}

本节列出了从 [!DNL Experience Manager] with [!DNL Experience Manager] as a [!DNL Cloud Service].

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| 用户界面 | 经典UI将从产品用户界面中删除。 一些经典UI对话框可用于一些选择功能，如链接检查器、版本清除和某些Cloud Service配置。 即将推出 [产品更新](/help/release-notes/home.md) 可能会进一步删除经典UI的可用性。 | 标准 UI |
| [!DNL Dynamic Media] | 以前与 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) 和 [Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) 在 [!DNL Experience Manager] as a [!DNL Cloud Service]. | 使用 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) 提供 [!DNL Experience Manager] as a [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 在 [!DNL Experience Manager] 6.4，现已从 [!DNL Experience Manager]. |
| [!DNL Sites] | 设计导入程序 | 此功能已作为 [!DNL Experience Manager] 存储库在运行时无法访问。 |
| [!DNL Assets] | [!DNL Assets] 与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务共享功能不可用。 | 与集成 [!DNL Adobe Creative Cloud]，使用 [Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html). |
| [!DNL Foundation] | 支持Apache Sling数据源（OSGi包org.apache.sling.datasource） | 不适用 |
| [!DNL Foundation] | 支持JST脚本模板（OSGi包org.apache.sling.scripting.jst） | 不适用 |

## Java API {#java-api}

请参阅 [本页](/help/release-notes/deprecated-apis.md) 已弃用或已删除的Java API的URL，这些API有时会引入。

## OSGI配置 {#osgi-configuration}

请参阅 [本文](/help/implementing/deploying/osgi-configuration-api.md) ，以了解有关配置OSGi属性的任何限制，其中某些限制可能会随时间推移而引入。
