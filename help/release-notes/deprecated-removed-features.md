---
title: 已弃用和已删除的功能
description: 针对 [!DNL Adobe Experience Manager] 中已弃用和已删除功能(a [!DNL Cloud Service])的发行说明。
translation-type: tm+mt
source-git-commit: e6ad571b7428f6fb7a11907e752ba670a722057c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 45%

---


# 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外，由于[!DNL Adobe Experience Manager]作为[!DNL Cloud Service]提供云本机部署模型，某些功能和功能被云本机对应部署所取代。

要传达即将移除/替换[!DNL Experience Manager]功能，请遵循以下规则：

1. 首先宣布弃用。已弃用的功能仍然可用，但未进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本节列表了在[!DNL Experience Manager]中标记为[!DNL Cloud Service]已弃用的特性和功能。 通常，将在未来版本中删除的功能首先设置为已弃用，并提供替代功能。

建议客户查看他们是否在当前部署中使用了该功能/功能，并制定计划更改其实施以使用提供的替代方案。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资产摄取现在使用[资产微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资产直接上传到[!DNL Experience Manager]。请参阅[已弃用的资产上传API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支持[工作流中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流步骤`DAM Asset Update`，包括如 ImageMagick 这类调用命令行工具。 | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资产微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |

## 已删除功能 {#removed-features}

本节列表了从[!DNL Experience Manager]中删除的特性和功能，[!DNL Experience Manager]为[!DNL Cloud Service]。

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| 用户界面 | 经典UI将从产品用户界面中删除。 几个经典UI对话框可用于一些选择功能，如链接检查器、版本清除和一些Cloud Service配置。 即将发布的[产品更新](/help/release-notes/home.md)可能会进一步删除经典UI的可用性。 | 标准 UI |
| [!DNL Dynamic Media] | 以前与[Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration)和[Dynamic Media混合模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic)的集成在[!DNL Experience Manager]中不可用作[!DNL Cloud Service]。 | 使用随[!DNL Experience Manager]提供的[Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)作为[!DNL Cloud Service]。 |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 这些功能在[!DNL Experience Manager] 6.4中已弃用，现在已从[!DNL Experience Manager]中删除。 |
| [!DNL Sites] | 设计导入程序 | 此功能已被删除，因为在运行时无法访问[!DNL Experience Manager]存储库的不可变部分。 |
| [!DNL Assets] | [[!DNL Assets]  与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务共享](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html)功能不可用。 | 要与[!DNL Adobe Creative Cloud]集成，请使用[Adobe资产链接](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 |
