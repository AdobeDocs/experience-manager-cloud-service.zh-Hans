---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.12.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2023.12.0 版的发行说明。'
exl-id: b36add58-a2ba-4299-94be-e0026e9c553c
source-git-commit: 559b4afa975dcd2204cd06c95f19ed38da00033e
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 2023.12.0 版的发行说明 {#release-notes}

以下部分概述了 2023.12.0 版的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版或 2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前功能版本 (2023.12.0) 的发布日期为 2023 年 12 月 14 日。下一个功能版本 (2024.1.0) 计划于 2024 年 1 月 25 日发布。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

<!-- 

## Release Video {#release-video}

Have a look at the December 2023 Release Overview video for a summary of the features added in the 2023.12.0 release:

>[!VIDEO](https://video.tv.adobe.com/v/3425864?quality=12)

-->

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### 早期采用者计划 {#sites-early-adopter}

**您可以利用[真实用户监控 (RUM) 数据服务](/help/implementing/cloud-manager/content-requests.md#real-user-monitoring-for-aem-as-a-cloud-service)**&#x200B;为 AEM as a Cloud Service 启用客户端收集。

真实用户监控 (RUM) 数据服务能够更准确地反映用户交互，确保可靠地衡量网站参与度。这是一个深入了解页面性能的绝佳机会。而这对于使用 Adobe 管理的 CDN 或非 Adobe 管理的 CDN 的客户都很有用。此外，对于使用非 Adobe 管理的 CDN 的客户，现在可为其启用自动流量报告，这样即无需与 Adobe 共享任何流量报告。

如果您有兴趣测试这项新功能并共享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址将包含生产、暂存和开发环境的域名的电子邮件发送到 `aemcs-rum-adopter@adobe.com`。Adobe 的产品团队随后将为您启用真实用户监控 (RUM) 数据服务。


## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### 资源视图中新增了几项功能 {#assets-view-features}

**用 Adobe Firefly 创建生成式 AI 图像**

通过集成 Adobe Firefly 文字生成图像功能（需要 Adobe Firefly 许可证），根据搜索查询创建新图像。

![Assets Firefly 集成](/help/assets/assets/assets-firefly-integration.png)

**查找相似图像**

现在只需选择一幅图像，然后在 Experience Manager Assets 存储库中查看类似的图像，即可轻松地找到内容。

<!--

* **Smart tags blocklist**: Experience Manager Assets now enables you to define a list of blocked tags. These tags are automatically removed from the auto-generated smart tags when you upload assets to the repository. This capability performs tags governance and saves a lot of time as you can add a tag to the block list and AEM Assets automatically excludes it from the list of tags for any of the assets that are added to the repository.

  ![storage usage insights](/help/assets/assets/block-tags.png)


**Video Preview**: AEM Assets now generates preview renditions of all supported video formats by default, without the need to configure a processing profile.

-->

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Experience Manager Forms] 中的新增功能 {#forms-features}

* **[将自适应表单与 Microsoft® SharePoint 列表建立联系](/help/forms/configure-submit-actions-core-components.md#submit-to-sharepoint)**：AEM Forms 提供现成的集成以将表单数据直接提交到 SharePoint 列表，使您可利用 SharePoint 的列表功能。您可以将 Microsoft SharePoint 列表配置为表单数据模型的数据源，并使用&#x200B;**使用表单数据模型提交**&#x200B;提交操作将自适应表单与 SharePoint 列表建立联系。

<!-- 

* **Configure a shard for Adobe Sign for AEM Forms**: Adobe distributes Acrobat Sign API around the globe in many deployment units called "shards." Each shard serves a customer's account, such as NA1, NA2, NA3, EU1, JP1, AU1, IN1, and others. The shard names correspond to geographic locations. You can now use more than one shard while using Adobe Sign integration with AEM Forms. 

-->

### 早期采用者计划 {#forms-early-adopter}

* **[将自适应表单提交到 Adobe Workfront Fusion 场景](/help/forms/submit-adaptive-form-to-workfront-fusion.md)**：Forms as a Cloud Service 提供一个现成的选项，可轻松地将自适应表单与 Adobe Workfront 建立联系。这简化了将自适应表单提交到 Adobe Workfront 场景的过程，使您可在提交自适应表单时触发 Workfront Fusion 场景。

* **[支持从右向左书写的语言](/help/forms/supporting-new-language-localization-core-components.md)**：现在可用从右向左书写 (RTL) 的语言（如阿拉伯语、波斯语和乌尔都语）展示基于核心组件构建的自适应表单。全球有超过 20 亿人使用 RTL 语言。使用 RTL 语言的表单可扩大您自适应表单的覆盖范围，以满足这些不同受众的需求并选择进入 RTL 市场。在某些地区，提供当地语言的表单还是一项法律规定。通过使用当地语言，您不仅可以满足更广泛的受众的需求，还可以确保遵守相关法律法规。

  ![支持从右向左书写的语言](/help/forms/assets/right-to-left-language-support.png)

* **[用 DocAssurance API（Communication API 的一部分）保护文档](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**：DocAssurance API 使您能够通过为文档签名和加密来保护敏感信息。通过加密，可将文档内容转换为无法读取的格式，从而确保只有获得授权的用户可访问。这一层加强的保护不仅防止未经授权地查看宝贵的数据，还能让人安心。利用 Signature API，您的组织可以保护其分发和接收的 Adobe PDF 文档的安全和隐私。此服务使用数字签名和认证确保只有预期的接收者可更改文档。

  您可以通过您的官方电子邮件 ID 向 `aem-forms-ea@adobe.com` 发送电子邮件，以加入早期采用者计划并请求对该功能的访问权限。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### CDN 配置早期采用者计划 {#cdn-config-early-adopter}

除了最近发布的[流量过滤规则](/help/security/traffic-filter-rules-including-waf.md)（包括可许可的 Web 应用程序防火墙 (WAF) 规则），还有机会使用配置管道声明和部署其他类型的 CDN 配置。我们很乐意了解您的用例，包括：
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
