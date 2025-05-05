---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 2020.7.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2020.7.0版as a Cloud Service发行说明。"
exl-id: 75d354a3-6987-4de0-aec8-24043461c516
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 73%

---

# [!DNL Adobe Experience Manager]as a Cloud Service2020.7.0版发行说明 {#release-notes}

以下部分概述了 Experience Manager as a Cloud Service 2020.7.0 的常规发行说明。

## 发布日期 {#release-date}

[!DNL Experience Manager] as a Cloud Service 2020.7.0 版的发布日期是 2020 年 7 月 30 日。

## Adobe Experience Manager Sites as a Cloud Service {#cloud-services-sites}

### 新增功能 {#what-is-new-sites}

适用于 [!DNL Adobe Target] 和 [!DNL Adobe Analytics] 的 [!DNL Experience Manager] as a Cloud Service 连接器在以下方面得到了增强：

* 新的用户界面实施取代了基于经典 UI 的实施。

* 简化的用户界面对话框，将用于变量映射的框架创建和其他配置留给 [!DNL Adobe Launch]。请参阅[集成 Adobe Analytics](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html?lang=zh-Hans) 和[集成 Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html?lang=zh-Hans)。

* 如今，配置是存储在 Experience Manager 存储库的 `/conf` 中，而不是 `/etc/cloudsettings` 中。

## [!DNL Adobe Experience Manager Assets]个as a Cloud Service {#assets}

### [!DNL Assets] 的新增功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是一项用于处理资产的可缩放且可扩展的服务。管理员可以配置[!DNL Experience Manager]以调用使用[!DNL Asset Compute Service]创建的自定义应用程序。 开发人员可以使用此服务来创建专门的自定义应用程序，以满足复杂用例的需求。 此Web服务可以为各种文件类型生成缩略图、从Adobe文件格式生成高质量图像渲染、对视频进行编码（将来推出）、提取元数据、提取全文作为索引的前导，以及通过所有可用的[!DNL Sensei]服务运行资产。 请参阅[使用资产微服务和处理配置文件](/help/assets/asset-microservices-configure-and-use.md)。

* 改进了 [!DNL Experience Manager] as a Cloud Service 中 [!DNL Dynamic Media] 的初始配置，使其更加稳健。如今，它可以向管理员提供进程进度。

* 通过使用资产微服务并改进批量处理发布后端，可以让资产发布成为整体资产处理管道必不可少的组成部分，从而简化资产发布到 [!DNL Dynamic Media] 的过程并使其更加稳健。

* 如今在[!UICONTROL 工作流程模型]编辑器中，与云服务部署不兼容的工作流程步骤将会带有警告标记。此外，在Cloud Service环境中执行现有工作流时，将跳过不兼容的工作流步骤。

* 在与[!DNL Cloud Manager]中的环境关联的Git项目中，由部署到`/conf/global`的客户创建的工作流模型会自动部署到`/var`，因此在[!DNL Experience Manager]中可用。 客户更改的 `/libs` 下的产品工作流程模型不会自动部署到 `/var`。

### 修复的错误 {#assets-bugs-fixed}

* “移动资产”向导未按预期为“收藏集”中包含的资产加载。 (CQ-4296756)
* 从XMP写回中排除了`dam:size`和`dam:sha1`的值。 (CQ-4237355)
* 批量取消发布资产时，[!DNL Brand Portal]生成一个错误，表明请求URI太长。 (CQ-4299474)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

AEM Commerce现已在Cloud Service上可用。

有关更多详细信息，请参阅[AEM Commerceas a Cloud Service入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/commerce/getting-started.html?lang=zh-Hans)。

## 核心组件 {#core-components}

### 新增功能 {#what-is-new-core-components}

[AEM 核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)版本 2.11.0 现已作为 AEM Sites 的一部分提供，其中包括：

* 推出了新的 [PDF 查看器组件](https://www.aemcomponents.dev/content/core-components-examples/library/core-content/pdf-viewer.html)。

* 核心组件的加速移动页面 (AMP) 支持功能现已可用。通过输入来自 Google 移动设备搜索结果的站点，可实现页面即时转换，这有助于提高用户参与度和 SEO，从而实现更快速的客户体验。
有关更多详细信息，请参阅核心组件的[AMP支持](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/amp.html?lang=zh-Hans)。

* 与 [Adobe 客户端数据层](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/data-layer/overview.html?lang=zh-Hans)版本 1.0.2 的兼容性。

* 错误修复和代码质量改进。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 版本 2020.7.0 的发行日期为 2020 年 7 月 9 日。

### 新增功能 {#what-is-new-cloud-manager}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* 每个环境的环境变量数量已增加至 200 个。

* Cloud Manager 管道现在支持由客户设置的变量和密钥。


  有关更多详细信息，请参阅“管道变量”。

* 现在支持绑定身份验证的专用 Maven 存储库。

* Cloud Manager 内部版本容器现在同时支持 Java 8 和 Java 11。有关更多详细信息，请参阅“使用 Java 11 支持”。

### 错误修复 {#bug-fixes-cm}

* 在完全环境创建之前，从 Cloud Manager 到 Developer Console 的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到 Developer Console 不显示用于将沙盒程序的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的&#x200B;**取消**&#x200B;和&#x200B;**保存**&#x200B;选项并非一直可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 在创建项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。

### 已知问题 {#known-issues}

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;*最低*&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户将会在代码质量控制过程中收到一条错误消息。

## Adobe Experience Manager as a Cloud Service 基础 {#cloud-foundation}

### 新增功能 {#what-is-new-foundations}

* [日志可以转发到Splunk帐户](/help/implementing/developing/introduction/logging.md#splunk-logs)，从而允许组织使用其Splunk投资。

* 可以为使用 Java 代码编程的出站流量分配[静态的专用出口 IP 地址](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address)，这对于某些集成来说，可能非常有用。

* 将 AEM Analytics 云服务 UI 从经典 UI 移植到新的 AEM UI。此外，还将 AEM 存储库中 Analytics 云服务的位置从 `/etc` 移动到 `/conf`，以便与其他 AEM 云服务保持一致。

* 将 AEM Target 云服务 UI 从经典 UI 移植到新的 AEM UI。此外，还将 AEM 存储库中 Target 云服务的位置从 `/etc` 移动到 `/conf`，以便与其他 AEM 云服务保持一致。

## 云就绪分析器 {#cloud-readiness-analyzer}

请阅读本章内容，了解 Cloud Readiness Analyzer v1.0.2 版的新增功能和更新。

### 错误修复 {#cra-bug-fixes}

* 无法在 Adobe Experience Manager (AEM) 6.1 上运行早期版本的云就绪分析器 (CRA)。明确向管理员组中的用户增加了允许他们运行 CRA 的相关支持。

  有关更多详细信息，请参阅[在AEM 6.1](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html?lang=zh-Hans#installing-on-aem61)上安装CRA 。

* 摘要报告上显示的到期时间戳不正确。

* CRA 检测到重复的自定义组件。

* 在 AEM 6.1 上，内容检查在完成全部检查之前退出。添加了异常处理功能，以允许检查员跳过并继续，直到完成全部检查。
