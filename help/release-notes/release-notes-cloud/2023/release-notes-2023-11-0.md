---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.11.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.11.0 版的发行说明。'
exl-id: 19cff082-80aa-445c-9462-5e319b7fe0e9
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 98%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.11.0 版的发行说明 {#release-notes}

以下部分概述了 2023.11.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前功能版本 (2023.11.0) 的发布日期为 2023 年 11 月 30 日。下一个功能版本 (2023.12.0) 计划于 2023 年 12 月 14 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2023 年 11 月版概述视频可了解在 2023.11.0 版中添加的功能的概要：

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期采用者计划 {#sites-early-adopter}

**[查找和替换内容片段中的字符串](/help/sites-cloud/administering/content-fragments/managing.md#find-and-replace-find-and-replace)**：利用内容片段控制台，用户可以简单直观地一次性替换多个内容片段中出现的字符串，以帮助加快内容速度。

![查找和替换](/help/sites-cloud/administering/content-fragments/assets/cf-managing-find-replace.png)

是否有兴趣试用该功能并分享反馈？从您的官方电子邮件 ID 向 **aemcs-headless-adopter@adobe.com** 发送电子邮件即可详细了解早期采用者计划。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中新增了几项功能 {#assets-view-features}

* **嵌入在 AEM Assets 中的 Adobe Express 编辑器**：有权访问 Express 的用户现在可直接在 AEM Assets 中使用来自 Adobe Express 和 Adobe Firefly 的集成式图像编辑和创建工具以改善内容重用并加快内容速度。

  ![将元数据表单分配给文件夹](/help/assets/assets/adobe-express-aem-assets.png)

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)

-->


* **Insights 中的存储使用情况报告**：管理员现在能够查看作为 Insights 一部分提供的存储使用情况报告。

  ![存储使用情况见解](/help/assets/assets/storage-usage-insights.png)

* **搜索优先主页配置**：现在通过 Experience Manager Assets 可配置组织的主页体验。如果您选择搜索优先作为主页，则可配置组织的搜索栏对齐方式、背景图像和徽标。

  ![搜索优先配置](/help/assets/assets/search-first-configuration.png)

### 管理员视图预发行版中的新增功能 {#admin-view-features-prerelease}

**视频预览**：AEM Assets 现在默认生成所有支持的视频格式的预览演绎版，而无需配置处理配置文件。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新增功能 {#forms-features}

* **[复选框组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：基于核心组件的自适应表单现在包含复选框组件。通过它，用户可二选一，即选择或取消选择特定选项。它一般显示为一个小框，单击或点按它即可在选中和取消选中两种状态之间切换。复选框是一个常见的表单元素，用于提供是/否或 true/false 选择。

* **[条款和条件组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：基于核心组件的自适应表单现在包含条款和条件组件。通过它，表单作者可在表单中引入一个特定的部分，其中为用户展示与使用服务、产品或平台相关的条款、条件或法律协议。此组件旨在通知用户其提交表单即表示同意的规则、法规和义务。

  ![复选框、条款和条件以及垂直选项卡组件](/help/forms/assets/forms-components.png)

* **[垂直选项卡组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：基于核心组件的自适应表单现在可将表单内容整理到选项卡垂直列表中，从而提供结构化的、可导航的布局。在表单中使用垂直选项卡可通过简化导航并改进表单内容的组织而增强整体用户体验，特别是在表单包含多个部分或复杂信息的情况下。



### 中的新增功能 [!DNL Forms] 预发行版 {#prerelease-features-forms}

* **[将自适应表单与 Microsoft® SharePoint 列表建立联系](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**：AEM Forms 提供现成的集成以将表单数据直接提交到 SharePoint 列表，使您可利用 SharePoint 的列表功能。您可以将 Microsoft SharePoint 列表配置为表单数据模型的数据源，并使用&#x200B;**使用表单数据模型提交**&#x200B;提交操作将自适应表单与 SharePoint 列表建立联系。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期采用者计划 {#forms-early-adopter}

* **将自适应表单提交到 Adobe Workfront Fusion 场景**：Forms as a Cloud Service 提供一个现成的选项，可轻松地将自适应表单与 Adobe Workfront 建立联系。这简化了将自适应表单提交到 Adobe Workfront 场景的过程，使您可在提交自适应表单时触发 Workfront Fusion 场景。

* **支持从右向左书写的语言**：现在可用从右向左书写 (RTL) 的语言（如阿拉伯语、波斯语和乌尔都语）展示基于核心组件构建的自适应表单。全球有超过 20 亿人使用 RTL 语言。使用 RTL 语言的表单可扩大您自适应表单的覆盖范围，以满足这些不同受众的需求并开拓 RTL 市场。在某些地区，提供当地语言的表单还是一项法律规定。通过使用当地语言，您不仅可以满足更广泛的受众的需求，还可以确保遵守相关法律法规。

  ![支持从右向左书写的语言](/help/forms/assets/right-to-left-language-support.png)

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-ea@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 现在可以许可WAF流量过滤器规则 {#cdn-waf-license}

流量过滤器规则已于 10 月发布，其中包含一项说明，即今年晚些时候将推出特殊类别的 Web 应用程序防火墙 (WAF) 规则，以补充已对 Sites 和 Forms 客户可用的规则。作为更新，WAF-DDoS 保护产品现在可获得许可。

获得许可后，可以使用 Cloud Manager 配置管道将这些高级 WAF 规则部署到 CDN，以添加一层额外的保护来防御 Web 攻击。

请参阅[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)，包括 WAF。请与您的 AEM 帐户团队联系以了解许可 WAF-DDoS 保护或增强安全性。

### CDN 配置早期采用者计划 {#cdn-config-early-adopter}

除了最近发布的[流量过滤规则（包括 WAF）](/help/security/traffic-filter-rules-including-waf.md)，还有机会使用配置管道来声明和部署其他类型的 CDN 配置。我们很乐意了解您的用例，包括：
* 301/302 客户端重定向
* 将边缘请求代理到任意来源
* URL 转换
* 设置或修改请求或响应标头
* CDN 无法访问 AEM 时显示的自定义错误页面
* 通过用户名/密码进行身份验证
* 任何其他有用的 CDN 配置

从您的官方电子邮件 ID 向 **aemcs-cdn-config-adopter@adobe.com** 发送含有反馈的电子邮件。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。

## 已知问题 {#known-issues}

* 无法提交基于核心组件的自适应表单。使用核心组件版本 2.0.38 - 2.0.60 构建的自适应表单存在该问题。

  要解决该问题，您可以迁移到自适应表单核心组件版本 2.0.62 或更高版本。要为您的环境设置自适应表单核心组件的版本，请在 Forms as a Cloud Service 存储库或基于 AEM 原型的项目中[设置 core.forms.components.version、core.forms.components.af.version 和 core.wcm.components.version 组件](/help/forms/enable-adaptive-forms-core-components.md#2-add-adaptive-forms-core-components-dependencies-to-your-git-repository)依赖项的版本，并[将更改部署到 Forms as a Cloud Service 环境](/help/forms/enable-adaptive-forms-core-components.md#build-and-deploy-updated-code-on-an-aem-forms-as-a-cloud-service-environment)。您可以在[自适应表单核心组件 Git 存储库](https://github.com/adobe/aem-core-forms-components#system-requirements)中找到最新版本的自适应表单核心组件依赖项。
