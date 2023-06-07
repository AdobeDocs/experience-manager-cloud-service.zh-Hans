---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 3a17f02b6544669e07adabfd4f50905eb6afd51e
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 40%

---

# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的功能发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2021 版、2022 版等的发行说明。
>
>查看 [Experience Manager 版本发行路线图](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html)，了解即将推出的 [!DNL Experience Manager] as a Cloud Service 的功能激活。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)。

## 发布日期 {#release-date}

的发布日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前功能版本(2023.4.0)为2023年6月7日。 下一个功能版本 (2023.6.0) 计划于 2023 年 6 月 29 日发布。

## 发布视频 {#release-video}

请查看2023年4月发布概述视频，了解2023.4.0版本中新增功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/3418681/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Experience Manager Sites] 中的新增功能 {#sites-features}

* 将内容片段作为 JSON 选件从 AEM as a Cloud Service 导出到 Adobe Target。
* 现在，利用对 GraphQL 分页和排序的支持以及内部缓存增强功能，可以在使用复杂的 GraphQL 查询和筛选条件从 AEM 获取大型内容集时帮助提高已解耦客户端应用程序的性能。

### 中的新增功能 [!DNL Experience Manager Sites] 预租赁 {#prerelease-sites}

* 内容片段及其引用现在可以发布到 [AEM预览服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=en#access-preview-service) 使用 [内容片段控制台](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en)，允许用户在分离预览应用程序上线前预览最终体验。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* 增加了对 WebP 图像的支持，可自动提取元数据、生成缩略图和自定义演绎版。这些文件现在还支持智能标记功能。 WebP不支持将Dynamic Media功能作为输入格式。

* [搜索体验增强功能](/help/assets/search-assets.md#aftersearch)  — 您现在可以对搜索结果中显示的资源快速执行以下操作：

   * 创建工作流
   * 创建新版本
   * 关联或取消关联资源

      您无需导航到资产位置并查看其属性即可执行这些操作。

* 颜色搜索Facet可用性改进 — 颜色值的输入字段现在可编辑，搜索结果仅在退出拾色器时更新。

* 推出了面向 Dynamic Media 视频交付（已启用 CMAF）中的自适应流式处理的新协议（DASH – 基于 HTTP 的动态自适应流式处理）支持：
   * 自适应流式处理 (DASH/HLS) 可确保最终用户获得更出色的视频观看体验
   * DASH 是自适应视频流式处理的国际标准协议，在业界得到广泛应用
   * 可在所有区域使用，可通过支持票证启用

* Dynamic Media _快照_  — 试验测试图像或Dynamic Media URL，以查看各种图像修饰符的输出，并对文件大小（使用WebP和AVIF交付）、网络带宽和设备像素比进行智能成像优化。 参见 [Dynamic Media快照](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html).

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 中的新增功能 {#new-features-available-in-channel}

* **[将自适应表单提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**：提高业务用户的敏捷性，以快速启用新表单并将提交的数据存储在日常使用工具中，例如 Microsoft SharePoint 站点或 OneDrive 文件夹。

![将自适应表单提交到 Microsoft SharePoint 和 Microsoft OneDrive](/help/forms/assets/onedrive-and-sharepoint.jpg)


### [!DNL Forms] 预发行版本中的功能 {#prerelease-features-forms}

* 增强的Adobe Acrobat Sign集成和合规性：AEM Forms现在与面向政府的Adobe Acrobat Sign集成，为电子签名提供了更高级别的合规性和安全性，并为政府关联帐户（政府部门和机构）提供了自适应表单提交。

与面向政府的Adobe Acrobat Sign集成使我们的合作伙伴和政府客户能够在Adaptive Forms中使用电子签名处理一些最关键和最敏感的业务线。 这一额外的安全层确保所有电子签名完全符合FedRAMP Moderate合规性，使我们的政府客户高枕无忧。

* AEM Sites编辑器中的自适应Forms：您现在可以使用AEM Sites编辑器快速创建多个表单并将其添加到站点页面。 此功能允许内容作者利用自适应表单组件的强大功能（包括动态行为、验证、数据集成、生成记录文档以及业务流程自动化），在Sites页面内创建无缝的数据捕获体验。 您可以：

   * 通过将表单组件拖放到AEM Sites编辑器中的自适应Forms容器组件来创建自适应表单。
   * 使用AEM Sites编辑器中的“自适应Forms向导”可创建独立于任何Sites页面的表单，从而让您自由地在多个页面中重用此类表单。
   * 将多个表单添加到Sites页面，从而简化用户体验并提供更大的灵活性。

   >[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

* 使用规则编辑器中的自定义错误处理程序增强错误处理：您现在可以调用自定义函数（使用客户端库）来响应外部服务返回的错误，并为最终用户提供量身定制的响应，或者对服务返回的错误采取特定操作。 例如，您可以在后端中调用自定义工作流以获取特定错误代码，或告知客户服务已停用。

通过引入基于标准的错误响应（可向后兼容OOTB错误处理程序），以及更大的灵活性和控制力，这有助于提高您的整体错误处理能力。

## Headless 自适应表单早期采用者计划 {#forms-early-adopter}

使用 Headless 自适应表单可让您的开发人员创建、发布和管理交互式表单，这些交互式表单可通过 API 而不是传统的图形用户界面进行访问和交互。Headless 自适应表单可帮助您：

* 使用选定的编程语言构建高质量的多渠道表单
* 将表单本机集成到您的桌面和移动应用程序、网站和聊天应用程序
* 在表单应用程序中重复使用您的专有 UI 组件
* 利用 Adobe Experience Manager Forms 的强大功能

您可以发送电子邮件至 `aem-forms-headless@adobe.com` 从您的官方电子邮件ID加入率先采用者计划。

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 附加发布区域：除了主要区域外，地点客户最多还可以授权三个发布区域。 流量被路由到其他发布场，这可以降低某些请求的延迟，并增强针对区域中断的恢复能力。 有关许可的信息，请联系您的Adobe客户经理 [其他发布区域](/help/operations/additional-publish-regions.md) 您的项目的。

## 维护发行说明 {#maintenance}

您可以在[此处](/help/release-notes/maintenance/latest.md)找到最新的维护发行说明。

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes/current.md)找到 Cloud Manager 月度发行版本的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
