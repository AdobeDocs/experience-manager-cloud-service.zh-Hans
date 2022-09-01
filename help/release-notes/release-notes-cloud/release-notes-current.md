---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: bcd62d1d1a66e17585e35c11c12cd72067e0e46e
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 28%

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

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2022.8.0)是2022年9月1日发行的。
下一个版本 (2022.9.0) 计划于 2022 年 9 月 29 日发布。

## 发布视频 {#release-video}

观看2022年8月版概述视频，了解2022.8.0版本中添加的功能摘要：

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 电子邮件组件允许在AEM中创建内容，然后作为电子邮件通过Campaign Classic发送。 核心电子邮件组件：
   * 基于 [核心WCM组件](https://github.com/adobe/aem-core-wcm-components) 支持可编辑的模板和样式系统。
   * 提供了10个电子邮件优化的生产就绪组件（页面、容器、标题、文本、图像、按钮、Teaser、体验片段、内容片段、分段）。
   * 提供高级个性化和分段，这要归功于 [插入促销活动变量](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization) 在大多数对话字段中，以及灵活 [分段组件](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation)).
   * 通过 [CSS样式内嵌](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation), [HTML属性内线](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)和 [HTML消毒剂](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation).
   * 允许在任意位置创建电子邮件。

### [!DNL Sites]预发行渠道中提供的新功能 {#prerelease-features-sites}

* 的 [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md) 为用户提供了一个选项，用于显示与内容片段关联的语言副本总数。 提供了一键式访问，以查看所有语言副本。 用户还能够按其感兴趣的区域设置过滤表视图。

![内容片段语言](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#features-assets}

* 您现在可以将 Adobe Experience Manager Assets 配置为[根据 MIME 类型限制用户可以上传的资源类型](/help/assets/configure-asset-upload-restrictions.md)。

   ![资产上传限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* [自适应Forms向导](/help/forms/creating-adaptive-form.md):AEM Forms提供了业务用户友好向导，可快速创作自适应Forms。 向导具有快速的选项卡导航，可轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。 此版本对向导进行了以下改进：

   * 选择或取消选择字段：利用向导，可基于JSON和表单数据模型架构创建自适应表单。 现在，您可以选择架构中要包含在自适应表单中的字段子集。 所选字段将转换为相应的自适应表单数据捕获组件，以快速创建所需的自适应表单。

   * 使用静态模板：在旧版静态模板方面已有投资的客户可以使用向导中的静态模板创作自适应表单，从而继续其云采用历程。 这为客户提供了将旧静态模板迁移到现代可编辑模板的额外时间。

* [在服务器端处理时，从记录文档(DoR)中删除隐藏字段](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md):您可以为最终用户生成记录PDF文档，其中只包含在数据捕获体验期间对他们可见的字段。 提交表单后，服务器会根据提交的数据验证哪些字段对最终用户隐藏，并从记录文档中排除以保持一致性。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 通过AEM页面属性以及产品驾驶舱中的概述将AEM页面与产品和类别关联
   ![产品驾驶舱页面关联](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
