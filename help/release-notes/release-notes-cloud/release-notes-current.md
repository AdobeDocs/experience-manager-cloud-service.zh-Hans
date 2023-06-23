---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 060956eee5136924263e4df5bd756670384e8365
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 57%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>从此处，您可以导航到早期版本（如2021或2022年）的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新功能版本 (2023.4.0) 的发布日期为 2023 年 6 月 7 日。下一个功能版本 (2023.6.0) 计划于 2023 年 6 月 29 日发布。

## 发布视频 {#release-video}

请查看 2023 年 4 月发布概述视频，了解 2023.4.0 版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 以JSON格式将内容片段从AEMas a Cloud Service导出到Adobe Target，并在Target中创建相应的JSON选件。
* 现在，利用对 GraphQL 分页和排序的支持以及内部缓存增强功能，可以在使用复杂的 GraphQL 查询和筛选条件从 AEM 获取大型内容集时帮助提高已解耦客户端应用程序的性能。

### [!DNL Experience Manager Sites] 预发行版本中的新增功能 {#prerelease-sites}

* 内容片段及其引用现在可以使用[内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=zh-Hans)发布到 [AEM 预览服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=zh-Hans#access-preview-service)，允许用户在上线前在解耦的预览应用程序上预览最终体验。
* 现在可以使用AEM GraphQL在Headless场景中为Web投放动态优化图像。 [查询变量](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/images.html?lang=en#query-variables) 可以在GraphQL查询中定义，以允许分离的客户端应用程序从AEM请求相应地优化的图像。
* 上的标记 [内容片段变量](https://experienceleague.adobe.com/docs/experience-manager-65/assets/content-fragments/content-fragments-variations.html?lang=en) 现在可以使用AEM GraphQL内容投放API输出到JSON。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 增加了对 WebP 图像的支持，可自动提取元数据、生成缩略图和自定义演绎版。这些文件现在也支持智能标记功能。WebP 不支持 Dynamic Media 功能作为输入格式。

* [搜索体验增强](/help/assets/search-assets.md#aftersearch) - 您现在可以对搜索结果中显示的资源快速执行以下操作：

   * 创建工作流
   * 创建一个版本
   * 关联或取消关联资源

     您无需导航到资源的位置并查看其属性即可执行这些操作。

* 颜色搜索方面的可用性改进 - 颜色值的输入字段现在是可编辑的，搜索结果仅在您退出拾色器时更新。

* 为Dynamic Media视频交付中的自适应流推出了新的协议支持（DASH — 通过HTTP的动态自适应流）（已启用CMAF）：
   * 自适应流式处理 (DASH/HLS) 可确保最终用户获得更出色的视频观看体验
   * DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用
   * 可在所有地区使用，可通过支持票证启用

* Dynamic Media _快照_  — 试验测试图像或Dynamic Media URL，以查看各种图像修饰符的输出，并评估针对文件大小（使用WebP和AVIF交付）、网络带宽和设备像素比的智能成像优化。 请参阅 [Dynamic Media 快照。](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)

### 中的功能 [!DNL Assets] 预发行版 {#prerelease-feature-assets}

* Dynamic Media — 图像配置文件中一些与智能裁切相关的字段的用户界面现在已更新，以反映当前定义智能裁切的准则。 参见 [裁切选项](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/image-profiles.html?lang=en#crop-options).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[将自适应Forms提交到Microsoft®SharePoint和Microsoft® OneDrive](/help/forms/configuring-submit-actions.md)**：提高企业用户的灵活性，以便您可以快速启动新表单，并将提交的数据存储在其使用的日常工具中，如Microsoft®SharePoint网站或OneDrive文件夹。

### [!DNL Forms] 预发行版本中的功能 {#prerelease-features-forms}

* [AEM 页面编辑器中的自适应表单](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)：您现在可以使用 AEM 页面编辑器快速创建多个表单并将其添加到您的 Sites 页面。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：

   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件来创建自适应表单。
   * 在AEM Sites编辑器中使用“自适应Forms向导”，以便您可以独立于任何Sites页面创建表单，同时让您能够在多个页面中重用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。

     >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* [增强了Adobe Acrobat Sign集成和合规性](/help/forms/adobe-sign-integration-adaptive-forms.md)：AEM Forms现在与面向政府的Adobe Acrobat Sign集成。 这种集成通过为政府关联帐户（政府部门和机构）提交自适应表单，为电子签名提供了高级的合规性和安全性。

  与面向政府的Adobe Acrobat Sign集成使Adobe的合作伙伴和政府客户能够在Adaptive Forms中使用电子签名处理一些任务最关键和最敏感的业务线。 这一额外的安全层确保所有电子签名完全符合FedRAMP Moderate合规性，从而让Adobe的政府客户高枕无忧。

* 增强了规则编辑器中自定义错误处理程序的错误处理能力。 现在，您可以调用自定义函数（使用客户端库）来响应外部服务返回的错误，并为最终用户提供量身定制的响应。 或者，您也可以对服务返回的错误执行特定操作。 例如，您可以在后端中调用自定义工作流以获取特定错误代码，或告知客户服务已停用。

  此功能通过引入基于标准的错误响应，向后兼容OOTB错误处理程序，并具有更大的灵活性和控制能力，从而帮助提高您的整体错误处理能力。

### Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 Headless 自适应表单可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用Adobe Experience Manager Forms的强大功能

您可以使用官方电子邮件 ID 将电子邮件发送到 `aem-forms-headless@adobe.com` 以加入早期采用者计划。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 其他发布区域：除了主要区域之外，Sites 客户最多可以许可三个发布区域。流量被路由到其他发布场，这可以降低某些请求的延迟，并增强针对区域中断的恢复能力。 请联系您的 Adobe 帐户经理，了解有关为您的程序授权[其他发布区域](/help/operations/additional-publish-regions.md)的信息。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 月度发行版本的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
