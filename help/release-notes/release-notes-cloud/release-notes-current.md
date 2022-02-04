---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 5731337ff0edf5825860e6f76ed919b90402d88b
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 33%

---


# [!DNL Adobe Experience Manager]as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

的发行日期 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本(2022.1.0)是2022年2月3日发行的。
以下版本(2022.2.0)发布于2022年2月24日。

## 发布视频 {#release-video}

请查看 [2022年1月版概述](https://video.tv.adobe.com/v/340120) 视频，了解2022.1.0版本中添加的功能摘要。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL Dynamic Media] - 您现在可以使用 AEM Dynamic Media 界面配置常规设置和发布设置，而不必使用 Dynamic Media Classic 桌面应用程序。

* [!DNL Dynamic Media] 现在支持 MXF 视频的提取、预览、播放和发布。尚不支持 MXF 视频的注释和可购买视频。

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行[更新、删除、重命名和移动操作](/help/assets/use-assets-across-connected-assets-instances.md)。更新会在 Sites 部署中自动提供，但会有一些延迟。

### [!DNL Assets] 预发行渠道中的新功能 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] 现在可以灵活地 [配置一个别名帐户](../../assets/dynamic-media/dm-alias-account.md) ，从而确保更新现成的Dynamic Media URL和查看器嵌入代码。 这对SEO产生了积极影响，可反映对您的业务上下文所做的更新，如品牌重新定位。

* 您现在可以使用 [!DNL Experience Manager Assets] 用户界面：

   * 配置存储库中重复资产的检测。

   * 配置向图像添加数字水印。

* 管理员现在可以配置电子邮件服务以进行大量下载。 它允许用户 [为大量下载启用电子邮件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads) 从 [!DNL Experience Manager Assets] 界面。 用户在下载过程完成后会收到一封电子邮件通知，其中包含已存档zip文件夹的下载链接。


* 的 [管理发布](/help/assets/manage-publication.md) 通过改进的用户界面增强了功能。 用户可以向选定目标发布或取消发布内容， [添加内容](/help/assets/manage-publication.md#add-content) 从DAM存储库的发布列表， [包含文件夹设置](/help/assets/manage-publication.md#include-folder-settings) 发布选定文件夹的内容并应用过滤器，以及 [计划发布](/help/assets/manage-publication.md#publish-assets-later) 日期或时间。

### 错误修复 {#bug-fixes}

* 将资产从AEM内部部署迁移到云服务时，不含原始呈现版本的未处理资产会发送到Asset compute进行处理。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[Communication API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hans) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务允许您以同步模式和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 使用 XML 数据填充模板文件来生成文档。
   * 以各种格式生成表单，包括非交互式PDF打印流。
   * 从 XFA 表单 PDF 生成打印 PDF。
   * 通过将多组数据与源模板合并，批量生成PDF、 PostScript、PCL和ZPL文档。

* **使用 Communications API 创建的记录文档和 PDF 文档的自定义字体**：您现在可以在使用 Communications API 生成的 PDF 文档中使用品牌批准的字体，以满足贵企业的要求。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **[汇编程序API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**:汇编程序API，用于组合、重新排列、扩充和获取有关PDF文档的信息。


## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 增强的myAccount组件
* 产品推荐组件支持其他页面类型（主页、购物车、订单确认）
* **愿望清单**
   * 已登录的访客可以将产品添加到愿望列表
   * 通过myAccount可以修改该愿望清单及其产品
   * 可以通过策略（示例产品预告、产品详细信息）在组件级别启用/禁用“添加到愿望列表”按钮
   * 可作为核心组件和在AEM Venia Storefront中使用

![愿望清单](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM Manager在as a Cloud Service中的发布日期为2022.01.0 2022年1月20日。 下一版本计划于2022年2月10日发布。

### 新增功能 {#what-is-new-cm}

* Cloud Manager将 [当检测到使用了相同的git提交时，请避免重建代码库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 执行多个全栈管道。
* 访问AEM环境日志现在需要 **部署管理器** 产品配置文件。 没有此配置文件的用户将在用户界面中看到一个禁用的按钮。
* UI将不允许为未启用站点作为解决方案的程序配置前端管道。
* 生成git密码后，将显示过期日期。

### 错误修复 {#bug-fixes-cm}

* 已更正某些前端管道部署遇到的空指针异常。
* 现在，当环境运行的AEM版本已过时时，可以添加、更新和删除环境变量。
* 对于在某些极少数情况下使用计划步骤的管道，构建图像步骤将不再被标记为“错误”。
* 对于仅具有一个存储库的程序，管道执行屏幕现在将显示存储库名称。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具v1.8.6的发布日期是2022年2月3日。

### 新增功能 {#what-is-new-ctt}

* 内容验证 — 用户能够可靠地确定是否已将内容传输工具提取的所有内容成功摄取到目标实例。 要使用此功能，您需要在 `System Console` 源AEM环境的。 请参阅 [验证内容传输 — 快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=en#getting-started) 以了解更多详细信息。

### 错误修复 {#bug-fixes-ctt}

* 由于用户映射区分大小写，因此未映射某些用户。 此问题已修复。 用户映射不再区分大小写。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24的发布日期是2022年2月1日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告具有和不具有智能标记的资产数量。
* 能够检测并报告所使用的核心组件版本。
* 能够检测并报告执行BPA的源层（创作或发布）类型。

### 错误修复 {#bug-fixes-bpa}

* BPA大小调整逻辑的制作速度更快、效率更高。
* 在某些情况下，BPA在运行时不会递增分析计数。 此问题已修复。
