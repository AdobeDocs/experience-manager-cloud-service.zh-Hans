---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.5.0 版的发行说明。'
exl-id: 1b867582-e34c-435b-b8f8-fc71dddcaccb
source-git-commit: 097c17b37cc308dc906cd4af7dc7c5d51862bdfa
workflow-type: tm+mt
source-wordcount: '805'
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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本 (2022.5.0) 的发布日期是 2022 年 6 月 9 日。
下一个版本 (2022.6.0) 计划于 2022 年 6 月 30 日发布。

## 发布视频 {#release-video}

请查看 2022 年 5 月发布概述视频，了解 2022.5.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/343321/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 预发行渠道中提供的新功能 {#prerelease-features-sites}

* 各种 GraphQL 功能
* [新控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)针对内容片段的 Headless 使用进行了优化

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [Dynamic Media 智能图像](https://medium.com/adobetech/one-solution-fits-all-smart-imaging-with-aem-dynamic-media-be690b62df9f)现在支持 AVIF 文件格式 – 进一步改进 Google Core Web Vital（最大内容绘制），与 WebP 相比，AVIF 提供了 20% 的额外尺寸缩减。 与 JPEG 相比，AVIF 的平均大小缩减率高达 41%（在某些图像中甚至高达 76%）。

* [!UICONTROL Experience Manager Assets Brand Portal] 现在，每十二小时执行一次自动作业，以删除发布到 AEM 的所有 Brand Portal 资产。 因此，您无需手动删除“贡献”文件夹中的资产，即可将文件夹大小保持在阈值限制以下。 请参阅 [Experience Manager Assets·Brand Portal 的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html)。

### [!DNL Assets] 预发行渠道中提供的新功能 {#prerelease-features-assets}

Experience Manager Assets 现在使用 Adobe Sensei AI 功能[区分图像中的颜色，并在摄取时自动将这些颜色作为标记应用](/help/assets/color-tag-images.md)。 这些标记可根据图像颜色组合来增强搜索体验。 您可以配置标记为图像的颜色数量（在 1 到 40 之间），以便以后可以根据这些颜色搜索图像。


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **将自适应表单与 Microsoft® Power Automate 集成**：现在，您可以配置自适应表单以在提交时运行 Microsoft® Power Automate Cloud Flow。 配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automation Cloud Flow 进行处理。 它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。

* **创建自适应表单的向导**：您可以使用商业用户友好向导快速创作自适应表单。 该向导提供了快速的选项卡导航，以便轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

   ![创建自适应表单的向导](/help/release-notes/assets/wizard.png)

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 快速访问产品驾驶舱：在站点编辑器中，通过一键单击即可轻松访问完整的详细产品信息

   ![启用愿望清单](/help/assets/CIF/enable-wishlist.png)

* 支持其他营销商务组件：组件可以配置为显示添加到购物车和添加到愿望清单的号召性用语

   ![站点编辑器到产品驾驶舱的快捷键](/help/assets/CIF/sites-editor-shortcut-to-cockpit.png)


## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 复制代理管理屏幕&#x200B;**“分发”选项卡**&#x200B;下的“添加树”选项，之前宣布为已弃用，将于 2022 年 6 月 20 日或不久之后删除。 而应使用以树层次结构表示的内容包进行复制[管理发布](/help/operations/replication.md#manage-publication)或 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)。

* 使用复制代理管理屏幕或复制 API 分发大于 10 MB 的内容包（具有属性的节点，不包括二进制文件）已被弃用，并将在 2022 年 9 月 12 日或之后不久实施。相反，必须使用[管理发布](/help/operations/replication.md#manage-publication)或[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)来复制这些大型内容包。7 月，如果尝试复制这些大型内容包，复制代理管理屏幕的&#x200B;**分发选项卡**&#x200B;中将显示一条警告消息，并且每当使用复制 API 复制这些大型内容包时，AEM 错误日志中也会显示一条警告消息。在 9 月，警告将被替换为错误。 请相应地调整您的流程。

### [!DNL Experience Manager] 预发行渠道中提供的新功能 {#prerelease-features-foundation}

* AEM as a Cloud Service 现已与 Unified Shell 集成，以改进用户体验并将其与所有其他 Experience Cloud 应用程序相统一。 请参阅 [Unified Shell 上的 AEM as a Cloud Service](/help/overview/aem-cloud-service-on-unified-shell.md) 以了解更多详细信息。

## [!DNL Experience Manager] as a [!DNL Cloud Service] 基础安全性 {#foundation-security}

### 弃用 TLS 1.0、1.1

从 2022 年 6 月 30 日开始，Experience Manager as a Cloud Service 将需要与用户系统进行更加安全的网络通信和数据交换。 AEM 将专门使用传输层安全性 (TLS) 1.2 协议。 弃用旧版 TLS 1.0 和 1.1。

如果您继续将旧版 TLS 用作 1.0、1.1，则可能会失去对 Experience Manager as a Cloud Service 的访问权限。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
