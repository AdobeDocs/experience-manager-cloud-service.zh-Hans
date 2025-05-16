---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.1.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2024.1.0 版的发行说明。'
exl-id: 9f5d97c6-6536-4593-acbf-cbe8bf9b5eeb
feature: Release Information
role: Admin
source-git-commit: 603602dc70f9d7cdf78b91b39e3b7ff5090a6bc0
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 94%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2024.1.0 版的发行说明 {#release-notes}

以下部分概述了 2024.1.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本 (2024.1.0) 的发布日期为 2024 年 1 月 25 日。下一个功能版本 (2024.3.0) 计划于 2024 年 4 月 11 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## 发布视频 {#release-video}

观看 2024 年 1 月版概述视频，大致了解 2024.1.0 版的新增功能：

>[!VIDEO](https://video.tv.adobe.com/v/3427041?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Extension Manager in AEM Sites {#sites-extension-manager}

**探索新的 [Extension Manager in AEM Sites](https://developer.adobe.com/uix/docs/extension-manager/)** 以通过配置 UI 扩展而使您的 AEM 设置个性化。

![Extension Manager in AEM Sites](/help/assets/sites/extension-manager/homepage.png)

通过 AEM Sites 中的 Extension Manager，开发人员和从业人员可访问、管理和自定义用 [Adobe App Builder](https://developer.adobe.com/app-builder/) 构建的 [UI 扩展](https://developer.adobe.com/uix/docs/)以增强 AEM Sites 的功能。
使用 Extension Manager，您可以：

* 按实例启用或禁用扩展；
* 配置扩展参数；
* 预览扩展并生成可共享的预览链接；
* 通过交互式演示探索 UI 可扩展性功能；
* 通过第一方扩展访问 Adobe 的实验功能。

我们正在积极搜寻 UI 扩展的反馈和新用例。如果您想联系我们，请将电子邮件发送至 `uix@adobe.com`。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 管理视图中的预发布功能 {#admin-view-prerelease}

**所有支持的视频类型都有预览演绎版**

Experience Manager Assets 现在无需处理配置文件配置，即默认生成所有支持的视频类型的预览演绎版

### 资源视图 {#assets-view-features}

**智能标记阻止列表**

现在可在 Assets Essentials 中定义阻止列表，其中包含在将资源上传到存储库时不应作为智能标记添加到资源的字词。此功能帮助您确保品牌合规，从而减少审核智能标记的工作量。

![智能标记阻止列表](/help/assets/assets/block-tags.png)


## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期采用者计划 {#forms-early-adopter}

* **[将自适应表单提交到 Adobe Workfront Fusion 场景](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供一个现成的选项，可轻松地将自适应表单与 Adobe Workfront 建立联系。这简化了将自适应表单提交到 Adobe Workfront 场景的过程，使您可在提交自适应表单时触发 Workfront Fusion 场景。

* **[支持从右向左书写的语言](/help/forms/supporting-new-language-localization-core-components.md)**：现在可用从右向左书写 (RTL) 的语言（如阿拉伯语、波斯语和乌尔都语）展示基于核心组件构建的自适应表单。全球有超过 20 亿人使用 RTL 语言。使用 RTL 语言的表单可扩大您自适应表单的覆盖范围，以满足这些不同受众的需求并选择进入 RTL 市场。在某些地区，提供当地语言的表单还是一项法律规定。通过使用当地语言，您不仅可以满足更广泛的受众的需求，还可以确保遵守相关法律法规。

  ![支持从右向左书写的语言](/help/forms/assets/right-to-left-language-support.png)

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-early-adopter-program@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

* **[您可以利用Real Use Monitoring (RUM)数据服务](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**启用AEM as a Cloud Service的客户端收集。
Real Use Monitoring (RUM) Data Service提供了对用户交互的更精确的反映，从而确保了对网站参与度的可靠衡量。 这是一个深入了解页面性能的绝佳机会。而这对于使用 Adobe 管理的 CDN 或非 Adobe 管理的 CDN 的客户都很有用。此外，对于使用非 Adobe 管理的 CDN 的客户，现在可为其启用自动流量报告，这样即无需与 Adobe 共享任何流量报告。

  如果您有兴趣测试这项新功能并分享您的反馈，请从您与您的 Adobe ID 关联的电子邮件地址将一封电子邮件发送到 `aemcs-rum-adopter@adobe.com`，其中包含您要为其启用 RUM 的每个环境的域名。Adobe的产品团队将为您启用实时监控(RUM)数据服务。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 支持 Dynatrace {#dynatrace}

Dynatrace 客户可监控其 AEM 使用情况。[了解如何](/help/implementing/cloud-manager/dynatrace.md)请求连接您的 Dynatrace 环境以监控应用程序性能。请注意，如果启用 Dynatrace，则可供所有客户使用的 New Relic APM 将停止收集数据。

### RDE 支持使用站点主题和站点模板的前端代码：早期采用者计划 {#rde-frontend-early-adopter}

对于早期采用者，[快速开发环境 (RDE)](/help/implementing/developing/introduction/rapid-development-environments.md) 现在支持基于[站点主题](/help/sites-cloud/administering/site-creation/site-themes.md)和[站点模板](/help/sites-cloud/administering/site-creation/site-templates.md)的前端代码。在 RDE 的情况下，使用命令行指令而非[前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)实现这一点。请联系 **aemcs-rde-support@adobe.com** 以试用并提供反馈。

### 域映射早期采用者计划 {#cdn-config-early-adopter}

除了最近发布的[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)（包括可许可的 Web 应用程序防火墙 (WAF) 规则），还有机会使用配置管道声明和部署[其他类型的 CDN 配置](/help/implementing/dispatcher/cdn-configuring-traffic.md)。发送电子邮件至 **aemcs-cdn-config-adopter@adobe.com**，加入早期采用者计划，即可访问：
* 301/302 客户端重定向
* 将边缘请求代理到任意来源
* URL 转换
* 设置或修改请求或响应标头
* CDN 无法访问 AEM 时显示的自定义错误页面

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
