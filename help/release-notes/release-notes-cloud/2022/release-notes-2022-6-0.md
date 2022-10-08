---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.6.0 版的发行说明。'
exl-id: cf2133dc-56cd-4a07-ab11-72e16f015ff5
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 97%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本 (2022.6.0) 的发布日期是 2022 年 6 月 30 日。

下一个版本 (2022.7.0) 计划于 2022 年 8 月 8 日发布。

## 发布视频 {#release-video}

请查看 2022 年 6 月发布概述视频，了解 2022.6.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/344308/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 新的[用户界面](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)现在可供内容管理员和内容作者有效管理（执行发布、取消发布、复制、移动等操作）、搜索/过滤内容片段，并为 Headless 用例创建内容片段。

   ![内容片段控制台](/help/release-notes/assets/cf-ui.png)

* 新[目录组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/tableofcontents.html)不仅可以与核心组件配合使用，还可与所有组件配合使用，以在内容页面上自动呈现目录。 而且，由于它呈现在服务器端并由调度程序完全缓存，因此也可以有效地加载。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

Experience Manager Assets 现在使用 Adobe Sensei AI 功能 [区分图像中的颜色，并在摄取时自动将这些颜色作为标记应用](/help/assets/color-tag-images.md)。 这些标记可根据图像颜色组合来增强搜索体验。 您可以配置标记为图像的颜色数量（在 1 到 40 之间），以便以后可以根据这些颜色搜索图像。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#forms-features}

* **[将自适应表单与 Microsoft® Power Automate 集成](/help/forms/forms-microsoft-power-automate-integration.md)**：您现在可以配置自适应表单以在提交时运行 Microsoft® Power Automate Cloud Flow。 配置的自适应表单将捕获的数据、附件和记录文档发送到 Power Automation Cloud Flow 进行处理。 它可帮助您构建自定义数据捕获体验，同时利用 Microsoft® Power Automate 的强大功能围绕捕获的数据构建业务逻辑并自动执行客户工作流。

* **创建自适应表单的向导**：您可以使用商业用户友好向导快速创作自适应表单。 该向导提供了快速的选项卡导航，以便轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

   ![创建自适应表单的向导](/help/release-notes/assets/wizard.png)

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 新产品驾驶舱属性页面，提供更好、更简化的概述

![产品驾驶舱属性概述](/help/assets/CIF/product_cockpit_properties_overview.png)

* 改进了 I/O 运行时第三方连接器的兼容性和稳健性

* 改进了对GQL客户端配置覆盖的支持（例如，设置自定义缓存行为）

* 现在支持开箱即用的多个商务端点，并且可以通过 Cloud Manager 进行配置。 详情请见[此处](https://medium.com/adobetech/use-aem-as-a-cloud-service-with-multiple-adobe-commerce-systems-9295612a9554)的 CIF 博客。


### 错误修复 {#bug-fixes-cif}

* 多值产品选取器字段将第 2 个和其他产品显示为无效

* 有时，产品选取器会隐藏在组件后面

## 参考演示附加组件 {#cloud-services-demos}

### 新增功能 {#what-is-new-demos}

* 新的 WKND 内容和商务模板扩展了 WKND 的 E2E 购物体验，包括产品目录、购物车、结帐和 myAccount。此模板使用 CIF 及其 CIF 核心组件，因此您还需要安装 CIF 附加组件。 详情请见[此处](https://medium.com/adobetech/learn-how-to-create-a-shoppable-experience-with-the-new-wknd-reference-site-and-cif-b3b2c161f67e)的 CIF 博客。

![WKND 商店](/help/assets/CIF/wknd_shop.png)

![WKND pdp](/help/assets/CIF/wknd_pdp.png)

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 如 5 月 (2022.5.0) 发行说明中所述，复制代理管理屏幕的&#x200B;**分发**&#x200B;选项卡下的“添加树”选项已被删除。 应该使用[管理发布](/help/operations/replication.md#manage-publication)或[发布内容树](/help/operations/replication.md#manage-publication#publish-content-tree-workflow)工作流来复制具有内容树层次结构的包。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
