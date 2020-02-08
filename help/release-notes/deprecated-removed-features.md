---
title: 已弃用和已删除的功能
description: 特定于Adobe Experience manager中已弃用和已删除云服务功能的发行说明。
translation-type: tm+mt
source-git-commit: b31ae32285080075d2531edd2c4976cf801d1c89

---


# Deprecated and removed features {#deprecated-and-removed-features}

Adobe不断评估产品功能，以不断地用更现代的替代方法来重新开发或替换旧功能，以提高整体客户价值，同时要谨慎考虑向后兼容性。 此外，由于Adobe Experience manager作为云服务提供了云本机部署模型，因此某些功能和功能已被云本机相关人员所取代。

为了传达即将删除/替换 AEM 功能，以下规则适用：

1. 首先宣布弃用。已弃用的功能仍然可用，但未进一步增强。
1. 在后续的主要发行版中，最早会删除已宣布弃用的功能。 将宣布删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## Deprecated features {#deprecated-features}

本节列出在Experience manager中标记为已弃用的云服务的特性和功能。 通常，计划在未来版本中删除的功能会首先设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划以将其实施更改为使用提供的备选方案。

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| 资产 | 资产摄取和处理不再使用工作流 `DAM Asset Update` 程 | 资产摄取现在 [使用资产微服务](/help/assets/asset-microservices-overview.md) 。 |
| 资产 | 将资产直接上传到AEM —— 请参阅已弃 [用的资产上传API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api) | [Experience Manager中使用](/help/assets/add-assets.md) “直接二进制上传”作为云服务。 有关技术详细信息，请参 [阅直接上传API](/help/assets/developer-reference-material-apis.md#overview-binary-upload)。 |
| 资产 | [工作流中的某些工作流步骤](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) , `DAM Asset Update` 包括调用命令行工具（如ImageMagick），不受支持 | [Asset microservices](/help/assets/asset-microservices-overview.md) 为许多工作流程提供了替代。 对于自定义处理，请使 [用后期处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |

## Removed features {#removed-features}

本节列出从AEM中作为云服务使用Experience manager删除的功能和特性。

| 区域 | 功能 | 替换 |
| ------------ | ------------------ | ----------- |
| UI | 虽然某些经典UI对话框仍保留在某些选择功能（如链接检查器、版本清除和某些云服务配置）中，但对经典UI的访问在AEM产品UI中通常已被删除。 | 标准UI |
| Dynamic Media | 以前与 [Dynamic Media Classic(Scene7)](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/scene7.html) 、 [](https://helpx.adobe.com/experience-manager/6-5/assets/using/config-dynamic.html) Dynamic Media Hybrid模式的集成在AEM中不作为云服务提供。 | 将随 [Experience Manager提供的Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) 用作云服务。 |
| 站点 | 门户控制器和Portlet组件 | 这些功能在AEM 6.4中已弃用，现在已从AEM中删除。 |
| 站点 | 设计导入程序 | 此功能已被删除，因为AEM存储库的不可更改部分在运行时无法访问。 |
| 资产 | [AEM Assets与Marketing Cloud Assets Core service及Creative cloud服务共享](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) ，不可用。 | 要与Creative cloud集成，请使用 [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)。 |
