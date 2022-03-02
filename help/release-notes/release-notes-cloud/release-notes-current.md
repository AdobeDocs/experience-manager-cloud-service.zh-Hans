---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明。'
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 2693022e5745b5c2bb2166f0833c6b1af4337815
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 99%

---


# [!DNL Adobe Experience Manager] as a Cloud Service 的最新发行说明 {#release-notes}

以下部分概述了当前（最新）版本的 [!DNL Experience Manager] as a Cloud Service 的一般发行说明。

>[!NOTE]
>
>您可以在此部分中导航到早期版本的发行说明；例如，2020 版、2021 版等的发行说明。

>[!NOTE]
>
>有关未与版本直接相关的文档更新的详细信息，请参阅[最新文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=zh-Hans)。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 最新版本 (2022.1.0) 的发布日期为 2022 年 2 月 3 日。以下版本(2022.2.0)发布于2022年3月3日。

## 发布视频 {#release-video}

观看 [2022 年 1 月版概述](https://video.tv.adobe.com/v/340120)视频，大致了解 2022.1.0 版的新增功能。

## Adobe Experience Manager Sites as a Cloud Service {#sites}

* 对于使用页面核心组件 v2 的站点，**[启用前端管道](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md)**&#x200B;按钮在 Sites 控制台的&#x200B;**站点**&#x200B;侧边栏中可用。使用此按钮可配置站点，以加载使用前端管道部署在现有客户端库之上的主题。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL Dynamic Media] - 您现在可以使用 AEM Dynamic Media 界面配置常规设置和发布设置，而不必使用 Dynamic Media Classic 桌面应用程序。

* [!DNL Dynamic Media] 现在支持 MXF 视频的提取、预览、播放和发布。尚不支持 MXF 视频的注释和可购买视频。

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行[更新、删除、重命名和移动操作](/help/assets/use-assets-across-connected-assets-instances.md)。相关更新会在 Sites 部署中自动提供，但会有一些延迟。

### [!DNL Assets] 预发行渠道中的新功能 {#assets-prerelease-features}

* [!DNL AEM Dynamic Media] 现在提供了灵活性，让您可以在用户界面中[配置一个别名账户](../../assets/dynamic-media/dm-alias-account.md)，从而确保开箱即用的 Dynamic Media URL 和查看器嵌入代码获得更新。这会对 SEO 产生积极影响，以反映对您的业务环境（如品牌再造）所做的更新。

* 您现在可以使用 [!DNL Experience Manager Assets] 用户界面执行以下操作：

   * 配置对存储库中重复资源的检测。

   * 配置向图像添加数字水印。

* 管理员现在可以为大型下载配置电子邮件服务。它让用户可以从 [!DNL Experience Manager Assets] 界面[为大型下载启用电子邮件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads)。下载过程完成后，用户会收到电子邮件通知，其中包含已存档 zip 文件夹的下载链接。


* [管理发布](/help/assets/manage-publication.md)功能通过改进的用户界面得到增强。用户可以向所选目标发布内容或从中取消发布内容，可以从 DAM 存储库[添加内容](/help/assets/manage-publication.md#add-content)至发布列表，可以[包含文件夹设置](/help/assets/manage-publication.md#include-folder-settings)以发布选定文件夹的内容和应用筛选器，还可以[安排发布](/help/assets/manage-publication.md#publish-assets-later)到晚一点的日期或时间。

### 错误修复 {#bug-fixes}

* 将资源从本地 AEM 迁移到云服务时，没有原始演绎版的未处理资源将被发送到 Asset Compute 进行处理。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **[!DNL AEM Forms as a Cloud Service - Communications]**：[Communication API](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/using-communications/aem-forms-cloud-service-communications.html?lang=zh-Hans) 可帮助您组合模板和 XML 数据，以生成各种格式的打印文档。该服务允许您以同步模式和批处理模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 使用 XML 数据填充模板文件来生成文档。
   * 生成各种格式的表单，包括非交互式 PDF 打印流。
   * 从 XFA 表单 PDF 生成打印 PDF。
   * 通过将多组数据与源模板合并，批量生成 PDF、PostScript、PCL 和 ZPL 文档。

* **使用 Communications API 创建的记录文档和 PDF 文档的自定义字体**：您现在可以在使用 Communications API 生成的 PDF 文档中使用品牌批准的字体，以满足贵企业的要求。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **[Assembler API](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/)**：Assembler API 用于组合、重新排列、扩充和获取有关 PDF 文档的信息。


## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 增强的 myAccount 组件
* “产品推荐”组件支持额外的页面类型（主页、购物车、订单确认）
* **愿望清单**
   * 登录的访客可以将产品添加到愿望清单
   * 可以通过 myAccount 管理愿望清单及其产品
   * 可以通过策略（例如产品预告片、产品详细信息）在组件级别启用/禁用“添加到愿望清单”按钮
   * 作为核心组件提供，位于 AEM Venia Storefront 中

![愿望清单](/help/assets/CIF/wishlist.png)

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service 2022.01.0 中的 Cloud Manager 的发布日期是 2022 年 1 月 20 日。下一个版本计划于 2022 年 2 月 10 日发布。

### 新增功能 {#what-is-new-cm}

* 当检测到在多个全栈管道执行中使用了相同的 git commit 时，Cloud Manager 将[避免重建代码库](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)。
* 访问 AEM 环境日志现在需要 **Deployment Manager** 产品配置文件。没有此配置文件的用户将在用户界面中看到一个禁用的按钮。
* 对于未将 Sites 作为解决方案启用的程序，该 UI 不允许进行前端管道配置。
* 生成 git 密码时，将显示到期日期。

### 错误修复 {#bug-fixes-cm}

* 某些前端管道部署遇到的空指针异常已得到纠正。
* 现在可以在环境运行过时版本的 AEM 时添加、更新和删除环境变量。
* 对于在某些极少数情况下使用计划步骤的管道，“构建映像”步骤不再被标记为错误。
* 对于只有一个存储库的程序，管道执行屏幕现在将显示存储库名称。

## 内容传输工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容传输工具版本 1.8.6 的发布日期为 2022 年 2 月 3 日。

### 新增功能 {#what-is-new-ctt}

* 内容验证 - 用户能够可靠地确定内容传输工具提取的所有内容是否已成功引入到目标实例中。要使用此功能，您需要在源 AEM 环境的 `System Console` 中启用它。有关更多详细信息，请参阅[验证内容传输 - 快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/validating-content-transfers.html?lang=zh-Hans#getting-started)。

### 错误修复 {#bug-fixes-ctt}

* 某些用户未被映射，因为用户映射区分大小写。此问题已得到修复。用户映射不再区分大小写。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.24 的发布日期是 2022 年 2 月 1 日。

### 新增功能 {#what-is-new-bpa}

* 能够检测和报告带有和不带有智能标签的资源的数量。
* 能够检测和报告所使用的核心组件版本。
* 能够检测和报告执行 BPA 的源层的类型（创作或发布）。

### 错误修复 {#bug-fixes-bpa}

* BPA 大小调整逻辑变得更快、更高效。
* 在某些情况下，BPA 在运行时没有增加分析的计数。此问题已得到修复。
