---
title: 已弃用和已删除的功能
description: 以下发行说明特定于 Adobe Experience Manager 云服务中已弃用和已删除的功能。
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外，由于 Adobe Experience Manager 云服务提供了云原生部署模型，因此某些功能和特性已被云原生对应功能和特性所取代。

为了传达即将删除/替换 AEM 功能，以下规则适用：

1. 首先宣布弃用。已弃用的功能仍然可用，但不会进一步进行增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

本部分列出了在 Experience Manager 云服务中标记为已弃用的特性和功能。通常，会先将计划在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划以将其实施更改为使用提供的备选方案。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| 资产 | `DAM Asset Update` 处理摄取的图像的工作流。 | 资产摄取现在使用[资产微服务](/help/assets/asset-microservices-overview.md)。 |
| 资产 | Upload assets directly to AEM. See [deprecated asset upload APIs](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | 使用 [直接二进制上传](/help/assets/add-assets.md)。 有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。 |
| 资产 | 不支持 [ 工作流中的](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)某些工作流步骤`DAM Asset Update`，包括如 ImageMagick 这类调用命令行工具。 | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| 资产 | 视频的FFmpeg转码。 | 对于FFmpeg缩略图生成，请使 [用Asset microservices](/help/assets/asset-microservices-overview.md)。 对于FFmpeg转码，请 [使用Dynamic Media](/help/assets/manage-video-assets.md)。 |

## 已删除功能 {#removed-features}

本部分列出了使用 Experience Manager 云服务从 AEM 中删除的特性和功能。

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| UI | 虽然某些经典 UI 对话框目前仍保留某些选择功能（如链接检查程序、版本清除和某些云服务配置）中，但在 AEM 产品 UI 中通常已删除对经典 UI 的访问。 | 标准 UI |
| Dynamic Media | 以前与 [Dynamic Media Classic(Scene7)](https://helpx.adobe.com/cn/experience-manager/6-5/sites/administering/using/scene7.html) 和 [Dynamic Media Hybrid](https://helpx.adobe.com/cn/experience-manager/6-5/assets/using/config-dynamic.html) 模式的集成在 AEM 云服务中不可用。 | 使用 Experience Manager 云服务提供的 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)。 |
| 站点 | Portal Director 和 Portlet 组件 | 这些功能在 AEM 6.4 中已弃用，现已从 AEM 中删除。 |
| 站点 | 设计导入程序 | 此功能已被删除，因为 AEM 存储库的不可更改部分在运行时无法访问。 |
| 资产 | [AEM Assets 与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务共享](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html)功能不可用。 | 要与 Creative Cloud 集成，请使用 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 |
