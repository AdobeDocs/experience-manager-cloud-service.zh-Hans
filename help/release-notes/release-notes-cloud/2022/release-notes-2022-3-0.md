---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 版的发行说明。'
description: ' [!DNL Adobe Experience Manager] as a Cloud Service 2022.3.0 版的发行说明。'
exl-id: 761f1605-c421-4f3a-8f90-af23f4f047b1
source-git-commit: b71cd1394260c8ec14b661934199632987a034f6
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 100%

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

[!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 当前版本 (2022.3.0) 的发布日期为 2022 年 3 月 31 日。下一个版本 (2022.4.0) 计划于 2022 年 5 月 5 日发布。

## 发布视频 {#release-video}

请查看 [2022 年 3 月发布概述](https://video.tv.adobe.com/v/341465)视频，了解 2022.3.0 版本中新增功能摘要。

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### [!DNL Sites] 预发行渠道中提供的新功能 {#prerelease-features-sites}

* 现在，可以使用内容模型编辑器中的简单复选框将内容模型数据类型定义为可翻译。 此外，AEM 翻译规则和配置会自动更新。

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### [!DNL Assets] 中的新增功能 {#assets-features}

* [!DNL AEM Dynamic Media] 现在提供了灵活性，让您可以在用户界面中[配置一个别名账户](/help/assets/dynamic-media/dm-alias-account.md)，从而确保开箱即用的 Dynamic Media URL 和查看器嵌入代码获得更新。这会对 SEO 产生积极影响，以反映对您的业务环境（如品牌再造）所做的更新。

* 您现在可以使用 [!DNL Experience Manager Assets] 用户界面执行以下操作：

   * 在存储库中配置[重复资产检测](/help/assets/manage-digital-assets.md#detect-duplicate-assets)。

   * 配置 [添加数字水印](/help/assets/watermark-assets.md) 到图像。

* 管理员现在可以为大型下载配置电子邮件服务。它让用户可以从 [!DNL Experience Manager Assets] 界面[为大型下载启用电子邮件通知](/help/assets/download-assets-from-aem.md#enable-email-notifications-for-large-downloads)。下载过程完成后，用户会收到电子邮件通知，其中包含已存档 zip 文件夹的下载链接。

* [管理发布](/help/assets/manage-publication.md)功能通过改进的用户界面得到增强。用户可以向所选目标发布内容或从中取消发布内容，可以从 DAM 存储库[添加内容](/help/assets/manage-publication.md#add-content)至发布列表，可以[包含文件夹设置](/help/assets/manage-publication.md#include-folder-settings)以发布选定文件夹的内容和应用筛选器，还可以[安排发布](/help/assets/manage-publication.md#publish-assets-later)到晚一点的日期或时间。

### [!DNL Assets] 预发行渠道中提供的新功能 {#prerelease-features-assets}

* 现在，您可以根据标记名称、创建日期或修改日期，在标记选择器窗口中按升序或降序[对标记进行排序](/help/assets/organize-assets.md#use-tags-to-organize-assets)。

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### [!DNL Forms] 的新增功能 {#what-is-new-forms}

* **[!DNL Communications - Document Generation APIs]**：[文档生成 API ](/help/forms/aem-forms-cloud-service-communications.md)帮助合并、重新排列和验证 PDF 文档。该服务允许您以同步模式生成文档。API 使您能够创建应用程序，这些应用程序允许您：

   * 汇编 PDF 文档。
   * 拆分 PDF 文档。
   * 转化为符合 PDF/A 标准的文档并进行验证。

* **自动将超过 15 页的 PDF Forms 转化为自适应表单**：您现在可以使用自动表单转化服务将最多 40 页的 PDF Forms 转化为自适应表单。该服务现在提供了将超过 15 页的表单部分转换为自适应表单片段的选项。它有助于提高转换表单的呈现速度，并使在自适应表单编辑器中加载大型表单变得更容易。

### [!DNL Forms] 预发行渠道中提供的新功能 {#prerelease-features-forms}

* **使用自定义 XCI 生成记录文档**：您现在可以使用自定义 XCI 文件设置记录文档的各种属性。它用自定义更改覆盖主 XCI。

* **以自适应表单使用不可见 CAPTCHA**：只有在可疑活动的情况下，您才可以使用不可见 CAPTCHA 显示 CAPTCHA 挑战。如果未发现可疑活动，则不会显示 CAPTCHA 挑战。

## CIF 加载项 {#cloud-services-cif}

### 新增功能 {#what-is-new-cif}

* 改进了多商店场景的 SEO：PDP/PLP 的 URL 格式现在可以通过 CIF 云配置属性在商店级别进行配置
* 产品挑选器通过 UI 中新的过滤器选项支持阶段性产品。这使内容从业者能够为即将发布的产品准备产品内容管理
* 通过使用 CIF 云配置名称而非配置代理 URL，简化了 CIF 配置管理和错误处理
* 产品列表和轮盘组件的手动类别选择。这允许内容从业者在目录体验之外的内容页面上使用这些组件

### CIF 预发布渠道中提供的新功能 {#prerelease-features-cif}

* AEM CIF 搜索核心组件支持 Commerce Live Search

## [!DNL Experience Manager] as a [!DNL Cloud Service] Foundation {#foundation}

### 新增功能 {#what-is-new-foundation}

* 为了对云环境中的自定义功能进行更高效的故障排除，我们发布了一个新的开发工具——[存储库浏览器](/help/implementing/developing/tools/repository-browser.md)。它是一个轻量级的只读 HTML 浏览器，可以从开发人员控制台启动。在发布者、作者和预览层以及所有环境（包括生产、暂存和开发）中查看内容存储库。浏览内容结构，查看属性，预览和下载二进制文件。

   ![repobrowserrelnotes](/help/release-notes/assets/repobrowserrelnotes.png)

* 用于验证服务器到服务器的 API 调用（例如，用于 GraphQL API 请求）的凭证现在可以在过期前以自助方式从开发人员控制台刷新。如需更多信息，请参阅 [此](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) 文档。

* 以前未启用的版本清除和审核日志清除维护任务，将为新环境启用。请参阅[维护任务](/help/operations/maintenance.md)文章中的相关值。

* AEM as a Cloud Service SDK Dispatcher 工具现在支持带有 M1 芯片的 Mac 电脑

## Cloud Manager {#cloud-manager}

您可以在[此处](/help/implementing/cloud-manager/release-notes-cloud-manager/release-notes-cm-current.md)找到 Cloud Manager 每月发布的完整列表。

## 内容转移工具 {#ctt-release}

### 发布日期 {#release-date-ctt}

内容转移工具版本 1.9.0 的发布日期为 2022 年 2 月 28 日。

### 新增功能 {#what-is-new-ctt}

* 检查“大小护栏” – 内容转移工具检查大小功能有助于减少失败的内容转移。使用检查大小功能，用户可以 1）在提取之前确定`crx-quickstart`子目录中是否有足够的磁盘空间，以及 2）估计迁移集大小并验证其是否受支持。如果违反了其中一项或两项检查，用户将在 CTT UI 中看到警告。有了这道护栏，您可以避免内容转移失败，并主动与 Adobe 客户关怀讨论迁移选项。有关更多详细信息，请参阅[“确定迁移集大小和磁盘空间”](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans#migration-set-size)。

## Best Practices Analyzer {#bpa-release}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.26 的发布日期是 2022 年 3 月 16 日。

### 新增功能 {#what-is-new-bpa}

* 能够监测未处理资源。如果检测到未处理资源，则需要将这些资源设置为已处理，或者在内容转移期间从迁移设置中删除这些资源，以避免在内容摄取期间遇到问题。
* 能够监测内容是否超过 1000 个虚名 URL。使用大量虚名 URL 不是最佳做法，因为它会给 Dispatcher 和 Publish 服务器带来负载。
* 能够识别 Oak 索引定义相关问题并检测与 AEM as a Cloud Service 兼容性。
* 能够检测和报告所使用的外部化程序配置。在 AEM as a Cloud Service 中，外部化程序配置由 Cloud Manager 设置，因此，需要重构现有的外部化程序配置以保持兼容性。

### 错误修复 {#bug-fixes-bpa}

* 在某些情况下，BPA 无法运行，因为 FormsSelectiveFeaturesAnalysis 抛出断言错误。此问题已得到修复。
* BPA 将与 WRK 模式相关的发现报告为 MAJOR 而非 CRITICAL。此问题已得到修复。
* BPA 错误地将 ui.apps 中与 OAK 索引定义有关的发现报告为 CRITICAL。此问题已得到修复
