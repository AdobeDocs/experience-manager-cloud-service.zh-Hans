---
title: 作为Cloud Service的2020.7.0版本 [!DNL Adobe Experience Manager] 的发行说明。
description: '[!DNLAdobe Experience Manager]作为2020.7.0的Cloud Service发行说明。'
translation-type: tm+mt
source-git-commit: a2b7ca2ab6ab3c95b07de49a43c8b119a792a7ac
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 37%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.7.0 的常规发行说明。

## 发布日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager SitesCloud Service {#cloud-services-sites}

### 新增功能 {#what-is-new-sites}

[!DNL Experience Manager] 作为Cloud Service连接 [!DNL Adobe Target] 器， [!DNL Adobe Analytics] 并通过以下方式进行增强：

* 新的用户界面实现取代了基于经典UI的实现。

* 简化的用户界面对话框，将创建框架留给变量映射和其他配置 [!DNL Adobe Launch]。 请参 [阅整合Adobe Analytics](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-analytics.html) 和 [整合Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/integrations/integrating-adobe-target.html)。

* 配置现在存储在Experience Manager `/conf` 存储库中 `/etc/cloudsettings` ，而不是存储在数据库中。

## Adobe Experience Manager Assets 云服务 {#assets}

### 新增功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是一种可扩展的可扩展服务，用于处理资产。 管理员可以配置Experience Manager以调用使用创建的自定义应用 [!DNL Asset Compute Service]程序。 开发人员可以使用该服务创建满足复杂用例的专用自定义应用程序。 此Web服务可以为不同文件类型生成缩略图，从Adobe文件格式生成高质量图像渲染，对视频（将来）进行编码，提取元数据，提取全文作为索引的前奏，并通过所有可用的Sensei服务运行资产。 请参 [阅使用资产微型服务和处理用户档案](/help/assets/asset-microservices-configure-and-use.md)。

* 将初始配置 [!DNL Dynamic Media] 改 [!DNL Experience Manager] 进为Cloud Service，使其更加健壮。 现在，它向管理员提供进程进度。

* 通过使用资产微服务 [!DNL Dynamic Media] 和改进批处理发布后端，将资产作为整个资产处理管道的一个组成部分，简化了资产发布并使其更加健壮。

* 与Cloud Service部署不兼容的工作流步骤现在在工作流模型编辑器中标 [!UICONTROL 有警告] 。 此外，在Cloud Service环境上执行现有工作流时，将跳过不兼容的工作流步骤。

* 由部署到与云管理器中的环境关 `/conf/global` 联的Git项目中的关联的客户创建的工作流模型将自动部署到Experience Manager, `/var` 因此可在中使用。 客户更改的 `/libs` 产品工作流模型不会自动部署到 `/var`。

## 核心组件 {#core-components}

### 新增功能 {#what-is-new-core-components}

Release 2.11.0 of the [AEM Core Components](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) is now available as part of AEM Sites including:

* 新PDF查看器 [组件简介](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)。

* 核心组件的加速移动页面(AMP)支持现已可用。 通过在从Google移动搜索结果进入网站时即时创建页面过渡，有助于提高用户参与度和SEO，从而提高客户体验。
有关更 [多详细信息，请参阅](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/amp.html) “AMP Support for the Core Components”。

* 与Adobe客户端数据层1.0.2 [版的兼容性](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)。

* 错误修复和代码质量改进。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

[!UICONTROL Cloud Manager] 版本 2020.7.0 的发行日期为 2020 年 7 月 9 日。

### 新增功能 {#what-is-new-cloud-manager}

* “环境”页面已重新设计。

* 现在，进入休眠状态的环境在 Cloud Manager 中会显示离散状态。

* 每个环境的环境变量数量已增加至 200 个。

* Cloud Manager 管道现在支持由客户设置的变量和密钥。


   有关更多详细信息，请参阅[管道变量](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables)。

### 错误修复 {#bug-fixes-cm}

* 在完全环境创建之前，从 Cloud Manager 到开发人员控制台的链接错误地处于活动状态。

* 直接从 Cloud Manager 链接到开发人员控制台不显示用于将沙盒项目的环境解除休眠/休眠的选项。

* 非生产管道编辑页面上的&#x200B;**取消**&#x200B;和&#x200B;**保存**&#x200B;选项并非一直可见。

* 代码质量控制过程中出现的某些问题可能会导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回与现有项目名称重复的名称。

* 无法始终通过用户界面下载一些大型管道步骤日志文件。

* 验证环境名称时出现差一错误。

* “环境”页有时会显示不存在的 Publish 和 Dispatcher 段。

### 已知问题 {#known-issues}

* 由于代码覆盖率的计算方式发生了变化，Jacoco 插件的&#x200B;*最低*&#x200B;版本现在为 0.7.5.201505241946（于 2015 年 5 月发行）。明确引用旧版本的客户在代码质量过程中会收到错误消息。

## Adobe Experience Manager作为Cloud Service基金会 {#cloud-foundation}

### 新增功能 {#what-is-new-foundations}

* [日志可以转发给Splunk帐户](/help/implementing/developing/introduction/logging.md#splunk-logs)，使组织能够利用其Splunk投资。

* [可为以Java代码编程的出站流量](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) （这对于某些集成可能非常有用）分配静态的专用出站IP地址。

* 将AEM Analytics云服务UI从经典UI移植到新的AEM UI。 还将AEM存储库中Analytics云服务的位置从移动 `/etc` 到 `/conf`，以与其他AEM云服务保持一致。

* 已移植AEM目标云服务UI从经典UI到新的AEM UI。 还将目标云服务在AEM存储库中的位置 `/etc` 从移 `/conf`动到其他AEM云服务的位置。

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

AEM Commerce现在在Cloud Service上可用。

有关更 [多详细信息，请参阅AEM Commerce入门](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/commerce/getting-started.html) (Cloud Service)。

## 云就绪分析器 {#cloud-readiness-analyzer}

请阅读本章内容，了解 Cloud Readiness Analyzer v1.0.2 版的新增功能和更新。

### 错误修复 {#cra-bug-fixes}

* 无法在 Adobe Experience Manager (AEM) 6.1 上运行早期版本的云就绪分析器 (CRA)。明确向管理员组中的用户增加了允许他们运行 CRA 的相关支持。

   有关更多详细信息，请参阅[在 AEM 6.1 上安装 CRA](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61)。

* 摘要报告上显示的到期时间戳不正确。

* CRA 检测到重复的自定义组件。

* 在 AEM 6.1 上，内容检查在完成全部检查之前退出。添加了异常处理功能，以允许检查员跳过并继续，直到完成全部检查。
