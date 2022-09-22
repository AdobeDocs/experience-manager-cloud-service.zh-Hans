---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 397747469970f6385e7a846fd40cacc52b0dd151
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 98%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 的当前版本 (2022.8.0) 的发布日期为 2022 年 9 月 1 日。下一版本(2022.9.0)计划于2022年10月6日发布。

## 发布视频 {#release-video}

请查看 2022 年 8 月发布概述视频，了解 2022.8.0 版本中新增功能的摘要：

>[!VIDEO](https://video.tv.adobe.com/v/346608/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 中的新增功能 {#sites-features}

* 通过电子邮件组件，可在 AEM 中创建内容，然后通过 Campaign Classic 以电子邮件的形式发送该内容。核心电子邮件组件：
   * 基于支持可编辑模板和样式系统的[核心 WCM 组件](https://github.com/adobe/aem-core-wcm-components)。
   * 提供 10 个为电子邮件优化的生产就绪组件（页面、容器、标题、文本、图像、按钮、Teaser、体验片段、内容片段、分段）。
   * 通过大多数对话框字段上的[插入 Campaign 变量](https://github.com/adobe/aem-core-email-components/wiki/RTE-Personalization)以及灵活的[分段组件](https://github.com/adobe/aem-core-email-components/wiki/Segmentation-component-(Technical-Documentation))，提供高级个性化和分段。
   * 借助 [CSS 样式内联器](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)、[HTML 属性内联器](https://github.com/adobe/aem-core-email-components/wiki/HTML-Inliner:-Technical-documentation)和 [HTML 清理器](https://github.com/adobe/aem-core-email-components/wiki/HTML-sanitizing:-Technical-documentation)，提供最佳的电子邮件友好的 HTML 输出
   * 使得可随时随地创建电子邮件。

### [!DNL Sites]预发行渠道中提供的新功能 {#prerelease-features-sites}

* [内容片段控制台](/help/sites-cloud/administering/content-fragments/content-fragments-console.md)为用户提供一个选项，用于显示与某个内容片段关联的语言副本总数。还提供一键访问以查看所有语言副本。用户还可按其感兴趣的区域设置筛选表格视图。

![内容片段语言](/help/release-notes/assets/cfconsole-languages.png)

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#features-assets}

* 您现在可以将 Adobe Experience Manager Assets 配置为[根据 MIME 类型限制用户可以上传的资源类型](/help/assets/configure-asset-upload-restrictions.md)。

   ![资产上传限制](/help/assets/assets/asset-upload-restrictions.png)

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* [自适应表单向导](/help/forms/creating-adaptive-form.md)：AEM Forms 提供便于企业用户使用的向导以快速创作自适应表单。该向导可快速地在选项卡之间导航，从而轻松地选择预先配置的模板、样式、字段和提交选项以创建自适应表单。此版本的向导有以下改进：

   * 选择或取消选择字段：可在向导中创建基于 JSON 和表单数据模型架构的自适应表单。现在可选择架构中的一部分字段以包括在自适应表单中。所选的字段被转换为相应的自适应表单数据捕获组件以快速创建所需的自定义表单。

   * 使用静态模板：在传统静态模板中有长期投入的客户可通过在模板中使用静态模板创作自适应表单，继续其采用云的历程。这样使客户有更多时间可将旧有的静态模板迁移到现代的可编辑模板。

* [在服务器端处理时从记录文档 (DoR) 删除隐藏的字段](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)：您可为最终用户生成记录文档 PDF，其中仅包含在数据捕获体验期间对最终用户可见的那些字段。在提交表单时，服务器根据所提交的数据验证对最终用户隐藏了哪些字段，并从记录文档中排除以达到一致。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 通过 AEM 页面属性以及产品主控室中的概述将 AEM 页面与产品和类别关联
   ![产品主控室页面关联](/help/assets/CIF/product_cockpit_page_association.png)

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 迁移工具 {#migration-tools}

您可以在[此处](/help/journey-migration/release-notes/release-notes-migration-tools-current.md)找到迁移工具版本的完整列表。
