---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 9857376cb196b8aaa9fac64636727b5ad20a0360
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 23%

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

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2022.4.0)是2022年5月5日。
下一版本(2022.5.0)计划于2022年5月26日发布。

## 发布视频 {#release-video}

请查看 [2022年4月版概述](https://video.tv.adobe.com/v/342612?quality=12) 视频，了解2022.4.0版本中添加的功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 内容模型数据类型现在可定义为 [可翻译](/help/assets/content-fragments/content-fragments-models.md#properties) 使用内容模型编辑器中的简单复选框。 此外，AEM翻译规则和配置会自动更新。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 您现在可以 [排序标记](/help/assets/organize-assets.md#use-tags-to-organize-assets) 根据标记名称、创建日期或修改日期，在标记选取器窗口中以升序或降序显示。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **通信 — Formsas a Cloud ServiceSDK中的文档操作API支持**: [文档操作API](/help/forms/aem-forms-cloud-service-communications.md) 帮助合并、重新排列和验证PDF文档。 现在，您可以借助AEM Forms as a Cloud ServiceSDK在本地开发环境中使用通信 — 文档生成API。

* **使用自定义XCI生成记录文档**:您现在可以 [使用自定义XCI文件设置记录文档的各种属性](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). 它用自定义更改覆盖主 XCI。它可以更好地控制记录文档的生成，增加个性化和定制机会。

* **在自适应表单中使用不可见的CAPTCHA**:您可以使用 [隐形验证码，仅在可疑活动时显示验证码挑战](/help/forms/captcha-adaptive-forms.md). 如果未发现可疑活动，则不会显示 CAPTCHA 挑战。它有助于评估人工表单的完成情况，而无需使用复选框要求，减少自定义工作，并改善最终用户体验。

* **表单数据模型配置**:您现在可以 [跨环境重复使用表单数据模型配置](/help/forms/create-form-data-models.md#runmode-specific-context-aware-config)，简化数据集成并降低IT成本。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速访问产品驾驶舱：在站点编辑器中，通过一键单击即可轻松访问完整的详细产品信息

   ![启用愿望清单](/help/assets/CIF/enable-wishlist.png)

* 支持其他营销商务组件：组件可配置为显示加货车和加货车清单行动动员

   ![站点编辑器到产品驾驶舱的快捷键](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)

## [!DNL Experience Manager]as a[!DNL Cloud Service] Foundation {#foundation}

### SDK内部版本分析程序 {#sdk-build-analyzers}

AEMas a Cloud ServiceSDK生成分析器Maven插件可检测Maven项目中的问题，包括缺少依赖项的问题。 它使开发人员有机会在本地开发过程中发现问题，而且在使用Cloud Manager部署到云环境之前就已经很早。

最近添加了一个新分析器：

* `content-packages-validation`  — 验证在部署期间安装的包的格式正确的内容语法和结构

强烈建议使用最新版本的分析器更新您的maven项目，或者包含分析器（如果尚未更新）。 有关更多信息，请参阅此文档 [此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html).

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础安全 {#foundation-security}

### 弃用TLS 1.0、1.1

从2022年6月30日开始，Experience Manageras a Cloud Service将需要与用户系统进行更加安全的网络通信和数据交换。 AEM将专门使用传输层安全性(TLS)1.2协议。 弃用旧版TLS 1.0和1.1。

如果您继续将旧版TLS用作1.0、1.1，则可能会失去对Experience Manageras a Cloud Service的访问权限。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以找到迁移工具版本的完整列表 [此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
