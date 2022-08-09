---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.4.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.4.0 版的发行说明。'
exl-id: 6c86838a-cabf-4770-b1ae-618af70193a2
source-git-commit: f42cf1b82f7cf42be2afd30d69d71354fe0afeb3
workflow-type: ht
source-wordcount: '573'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本 (2022.4.0) 的发布日期是 2022 年 5 月 5 日。下一个版本 (2022.5.0) 计划于 2022 年 6 月 9 日发布。

## 发布视频 {#release-video}

请查看 [2022 年 4 月发布概述](https://video.tv.adobe.com/v/342612?quality=12)视频，了解 2022.4.0 版本中新增功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 现在可以使用内容模型编辑器中的简单复选框将内容模型数据类型定义为[可翻译](/help/assets/content-fragments/content-fragments-models.md#properties)。 此外，AEM 翻译规则和配置会自动更新。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 现在，您可以根据标记名称、创建日期或修改日期，在标记选择器窗口中按升序或降序[对标记进行排序](/help/assets/organize-assets.md#use-tags-to-organize-assets)。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **通信 – Forms as a Cloud Service SDK 中的文档操作 API 支持**：[文档操作 API](/help/forms/aem-forms-cloud-service-communications.md) 有助于合并、重新排列和验证 PDF 文档。 现在，您可以借助 AEM Forms as a Cloud Service SDK 在本地开发环境中使用通信 – 文档生成 API。

* **使用自定义 XCI 生成记录文档**：您现在可以[使用自定义 XCI 文件设置记录文档的各种属性](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file)。 它用自定义更改覆盖主 XCI。它可以更好地控制记录文档的生成，增加个性化和定制机会。

* **以自适应表单使用不可见 CAPTCHA**：只有在可疑活动的情况下，您才可以使用[不可见 CAPTCHA 显示 CAPTCHA 挑战](/help/forms/captcha-adaptive-forms.md)。 如果未发现可疑活动，则不会显示 CAPTCHA 挑战。 它有助于评估人工表单的完成情况，而无需使用复选框要求，减少自定义工作，并改善最终用户体验。

* **表单数据模型配置**：您现在可以[跨环境重用表单数据模型配置](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)，从而简化数据集成并降低 IT 成本。


## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### SDK 内部版本分析程序 {#sdk-build-analyzers}

AEM as a Cloud Service SDK 生成分析器 Maven 插件可检测 Maven 项目中的问题，包括缺少依赖项的问题。 它使开发人员有机会在使用 Cloud Manager 部署到云环境之前，在本地开发期间发现问题。

最近添加了一个新分析器：

* `content-packages-validation` – 验证在部署期间安装的包的格式正确的内容语法和结构

强烈建议使用最新版本的分析器更新您的 maven 项目，或者包含分析器（如果尚未更新）。 有关更多信息，请参阅此文档[此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础安全性 {#foundation-security}

### 弃用 TLS 1.0、1.1

从 2022 年 6 月 30 日开始，Experience Manager as a Cloud Service 将需要与用户系统进行更加安全的网络通信和数据交换。 AEM 将专门使用传输层安全性 (TLS) 1.2 协议。 弃用旧版 TLS 1.0 和 1.1。

如果您继续将旧版 TLS 用作 1.0、1.1，则可能会失去对 Experience Manager as a Cloud Service 的访问权限。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
