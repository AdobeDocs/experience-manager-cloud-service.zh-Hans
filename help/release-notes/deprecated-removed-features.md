---
title: 已弃用和已删除的功能
description: 特定于  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已弃用和已删除的功能的发行说明。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: c4809bcbeae5339427b1da588021606d18b482a5
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 91%

---

# 已弃用和已删除的功能 {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已弃用和已删除的功能"
>abstract="AEM as a Cloud Service 具有云原生部署模型。某些功能和特性已由云原生对应功能和特性取代，此选项卡显示了它们。"


Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外，由于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供了云原生部署模型，因此某些功能和特性已由云原生对应功能和特性取代。

为了传达即将删除/替换 [!DNL Experience Manager] 功能，以下规则适用：

1. 首先宣布弃用。已弃用的功能仍然可用，但不会进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

此部分列出了在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中标记为已弃用的特性和功能。通常，会先将计划在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | **社交媒体状态**&#x200B;的体验片段属性。 | 该功能将很快被删除。 |
| [!DNL Sites] | 基于模板的简单内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资源提取现在使用[资源微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资源直接上传到 [!DNL Experience Manager]。请参阅[已弃用的资源上传 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支持 `DAM Asset Update` 工作流中的[某些工作流步骤](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)，包括 [!DNL ImageMagick] 等调用命令行工具。 | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资产微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 复制代理的“分发”选项卡下的树复制 UI（在 2021 年 9 月 30 日后被删除） | [管理出版物](/help/operations/replication.md#manage-publication)或[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)方法 |
| [!DNL Foundation] | 复制代理管理屏幕的“分发”选项卡和复制API都不能用于复制超过10MB的内容包（2022年9月12日之后实施） | [管理出版物](/help/operations/replication.md#manage-publication)或[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)方法 |


| [!DNL Foundation]       |复制代理管理屏幕的“分发”选项卡和复制API都不能用于复制超过10MB的内容包。 请改用 [管理发布](/help/operations/replication.md#manage-publication) 或 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) |

## 已删除功能 {#removed-features}

此部分列出了使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 从 [!DNL Experience Manager] 中删除的特性和功能。

| 区域 | 功能 | 替换 | 目标删除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 用户界面 | 从产品用户界面中删除经典 UI。一些经典 UI 对话框可用于一些选择功能，例如“链接检查器”、“版本清除”和一些 Cloud Service 配置。即将发布的[产品更新](/help/release-notes/home.md)可能会进一步删除经典 UI 可用性。 | 标准 UI | 已删除 |
| [!DNL Dynamic Media] | 以前与 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=zh-Hans#integration) 和 [Dynamic Media Hybrid 模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=zh-Hans#dynamic)的集成在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中不可用。 | 使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供的 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)。 | 已删除 |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 这些功能在 [!DNL Experience Manager] 6.4 中已弃用，现已从 [!DNL Experience Manager] 中删除。 | 已删除 |
| [!DNL Sites] | 设计导入程序 | 此功能已被删除，因为 [!DNL Experience Manager] 存储库的不可更改部分在运行时无法访问。 | 已删除 |
| [!DNL Assets] | [!DNL Assets] 无法与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务进行共享。 | 要与 [!DNL Adobe Creative Cloud] 集成，请使用 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 | 已删除 |
| [!DNL Foundation] | 对 Apache Sling 数据源（OSGi 包 org.apache.sling.datasource）的支持 | 不适用 | 已删除 |
| [!DNL Foundation] | 对 JST 脚本模板（OSGi 包 org.apache.sling.scripting.jst）的支持 | 不适用 | 已删除 |
| [!DNL Foundation] | 对 Apache Felix Http Whiteboard 的支持 | OSGi Http Whiteboard | 2022 年 3 月 |

## Java API {#java-api}

请参阅[此页面](/help/release-notes/deprecated-apis.md)，了解偶尔引入的任何已弃用或已删除的 Java API。

## OSGI 配置 {#osgi-configuration}

请参阅[本文](/help/implementing/deploying/osgi-configuration-api.md)，了解有关 OSGI 属性配置的任何限制，其中一些限制可能会随着时间的推移而引入。
