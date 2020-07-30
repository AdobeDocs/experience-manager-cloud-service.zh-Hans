---
title: 作为Cloud Service的2020.7.0版本 [!DNL Adobe Experience Manager] 的发行说明。
description: '[!DNLAdobe Experience Manager]作为2020.7.0的Cloud Service发行说明。'
translation-type: tm+mt
source-git-commit: 5103d54bcb71d6c78894a30edafccf288a51368f
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 7%

---


# Release Notes for [!DNL Adobe Experience Manager] as a Cloud Service 2020.7.0 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.7.0 的常规发行说明。

## 发布日期 {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.7.0 is July 30, 2020.

## Adobe Experience Manager SitesCloud Service {#cloud-services-sites}

### 新增功能 {#what-is-new-sites}

[!DNL Experience Manager] 作为Cloud Service连接 [!DNL Adobe Target] 器， [!DNL Adobe Analytics] 并通过以下方式进行增强：

* 新的用户界面实现取代了基于经典UI的实现。

* 简化的用户界面对话框，将创建框架留给变量映射和其他配置 [!DNL Adobe Launch]。

* 配置现在存储在Experience Manager `/conf` 存储库中 `/etc/cloudsettings` ，而不是存储在数据库中。

## Adobe Experience Manager Assets 云服务 {#assets}

>[!NOTE]
>AEM Assets作为Cloud Service功能将在未来几天内推出。

### 新增功能 {#what-is-new-assets}

* [!DNL Asset Compute Service] 是一种可扩展的可扩展服务，用于处理资产。 管理员可以配置Experience Manager以调用使用创建的自定义工作 [!DNL Asset Compute Service]器。 开发人员可以使用该服务来创建专门的自定义工作器，它们适合复杂的用例。 此Web服务可以为不同文件类型生成缩略图，从Adobe文件格式生成高质量图像渲染，对视频（将来）进行编码，提取元数据，提取全文作为索引的前奏，并通过所有可用的Sensei服务运行资产。 请参 [阅使用资产微型服务和处理用户档案](/help/assets/asset-microservices-configure-and-use.md)。

* 将初始配置 [!DNL Dynamic Media] 改 [!DNL Experience Manager] 进为Cloud Service，使其更加健壮。 现在，它向管理员提供进程进度。

* 通过使用资产微服务 [!DNL Dynamic Media] 和改进批处理发布后端，将资产作为整个资产处理管道的一个组成部分，简化了资产发布并使其更加健壮。

* 与Cloud Service部署不兼容的工作流步骤现在在工作流模型编辑器中标 [!UICONTROL 有警告] 。 此外，在Cloud Service环境上执行现有工作流时，将跳过不兼容的工作流步骤。

* 由部署到与云管理器中的环境关 `/conf/global` 联的Git项目中的关联的客户创建的工作流模型将自动部署到Experience Manager, `/var` 因此可在中使用。 客户更改的 `/libs` 产品工作流模型不会自动部署到 `/var`。

## 核心组件 {#core-components}

### 新增功能 {#what-is-new-core-components}

[核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)版本 2.11.0 现已作为 AEM Sites 的一部分提供，包括：

* 新PDF查看器 [组件简介](https://aemcomponents.dev/content/core-components-examples/library/page-authoring/pdf-viewer.html)

* [核心组件的加速移动页面(AMP)支持](https://docs.adobe.com/content/help/en/experience-manager-core-components/developing/amp.html) ，通过在从Google移动搜索结果进入网站时即时创建页面过渡，有助于提高用户参与度和SEO，从而加快客户体验。

* 与Adobe客户端数据层1.0.2 [版的兼容性](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/data-layer/overview.html)

* 错误修复和代码质量改进

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

Cloud Manager Version 2020  .7.0的发布日期为2020年7月9日。

### 新增功能 {#what-is-new-cloud-manager}

* 环境页面已重新设计。

* 冬眠环境在冬眠后，现在在Cloud Manager中显示离散状态。

* 每个环境的环境变量数已增加到200个。

* Cloud Manager管道现在支持客户集变量和秘密。

   有关更多 [详细信息](/help/onboarding/getting-access-to-aem-in-cloud/creating-aem-application-project.md#pipeline-variables) ，请参阅管道变量。

### 错误修复 {#bug-fixes-cm}

* 在完全创建环境之前，从云管理器到开发人员控制台的链接未正确激活。

* 直接从云管理器链接到开发人员控制台时，未显示用于将沙箱项目的环境解除休眠／休眠的选项。

* “非 **生** 产管道 **** ”编辑页面上的“取消”和“保存”选项并不总是可见。

* 代码质量过程中的某些失败可能导致日志文件无法正确生成。

* 创建新项目时，建议的名称有时会返回现有项目名称的重复。

* 无法通过用户界面一致地下载某些大型管道步骤日志。

* 验证环境名称时出现非按一错误。

* 环境页有时会显示发布和调度程序段（当不存在时）。

### 已知问题 {#known-issues}

* 由于代码覆盖率的计算方式发生 *更改* ,Jacoco插件的最低版本现在为0.7.5.201505241946（发布于2015年5月）。 明确引用旧版本的客户在代码质量过程中会收到错误消息。


## Adobe Experience Manager作为Cloud Service基础 {#cloud-foundation}

### 新增功能 {#what-is-new-foundations}

* [日志可以转发给Splunk帐户](/help/implementing/developing/introduction/logging.md#splunk-logs)，使组织能够利用其Splunk投资。

* [可为以Java代码编程的出站流量](/help/implementing/developing/introduction/development-guidelines.md#dedicated-egress-ip-address) （这对于某些集成可能非常有用）分配静态的专用出站IP地址。

* 已移植AEMAnalytics云服务UI从经典UI到新的AEM UI。 还将Analytics云服务在AEM存储库中的位置从移 `/etc` 动到 `/conf`其他AEM cloud services，以与其他保持一致。

* 已移植AEM目标云服务UI从经典UI到新的AEM UI。 还将目标云服务在AEM存储库中的位置从移 `/etc` 动到 `/conf`其他AEM cloud services，以与其他保持一致。

## 云就绪分析器 {#cloud-readiness-analyzer}

可查看本节以了解新增功能以及Cloud Readiness Analyzer Release 1.0.2版的更新。

### 错误修复 {#cra-bug-fixes}

* 无法在Adobe Experience Manager(AEM)6.1上运行CRA的早期版本。添加了允许管理员组中用户的明确支持。

   有关详 [细信息，请参阅在AEM 6.1上安装](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/cloud-migration/cloud-readiness-analyzer/using-cloud-readiness-analyzer.html#installing-on-aem61) CRA。

* 摘要报告上显示的过期时间戳不正确。

* CRA正在检测重复的定制组件。

* 在AEM 6.1上，内容检查在完成完整检查之前已退出。 添加了异常处理，以允许检查员跳过并继续，直到完成完整检查。
