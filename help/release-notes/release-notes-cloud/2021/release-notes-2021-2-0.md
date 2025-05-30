---
title: ' [!DNL Adobe Experience Manager] as a Cloud Service 2021.2.0 版的发行说明。'
description: "[!DNL Adobe Experience Manager]个2021.2.0版as a Cloud Service发行说明。"
exl-id: 88dac54b-cc12-44a0-b429-6e691221f806
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 32%

---


# [!DNL Adobe Experience Manager]as a Cloud Service的发行说明 {#release-notes}

以下部分概述了[!DNL Experience Manager]as a Cloud Service的常规发行说明。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]as a Cloud Service2021.2.0的发布日期是2021年2月25日。
下一个版本(2021.3.0)将于2021年3月25日发布。

## [!DNL Adobe Experience Manager Sites]个as a Cloud Service {#sites}

### Headless内容管理 {#headless}

* **[用于内容片段投放的GraphQL API](/help/headless/graphql-api/content-fragments.md)**：能够使用GraphQL语法和基于内容片段模型的架构查询内容片段，以便按JSON格式输出。

* **[GraphQL API请求支持身份验证](/help/headless/security/authentication.md)**：能够通过服务器端API的访问令牌验证GraphQL API请求的身份。

* **[RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)**：已添加对在AEM中查看和编辑外部SPA的支持。

* **[在AEM内编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**：添加了将独立单页应用程序上传到AEM实例、添加内容的可编辑部分以及启用创作的功能。

* 增强了GraphQL API的JSON输出，包括以JSON格式和区域设置输出富文本的功能。

* 支持嵌套内容片段模型，以允许通过多行文本字段中内嵌的专用内容片段引用数据类型或内容片段引用创建嵌套的内容片段结构。

* 内容片段模型数据类型中有其他可用的验证规则，包括“唯一”、“必需”和“可翻译”。

* 可标记内容片段模型，并允许在文件夹中按标记或路径使用策略创建内容片段。

* 在内容片段编辑器中增强了可用性，包括片段所基于的模型的发布操作和显示。

* 能够直接在内容片段编辑器中预览JSON输出。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/sites-console/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] 的新增功能 {#what-is-new-assets}

* 可使用[!DNL Experience Manager Assets Brand Portal]来获取Assets。 它有助于从机构用户那里获得用于新营销活动、照片拍摄和项目的资产。

* [!DNL Experience Manager Assets]作为[!DNL Cloud Service]有权拥有预配置的[!DNL Brand Portal]实例。 [!DNL Cloud Manager]用户可以在[!DNL Experience Manager Assets]上将[!DNL Brand Portal]激活为[!DNL Cloud Service]。 请参阅[激活Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=zh-Hans)。

* 企业现在可以使用[!DNL Brand Portal]获取资源。 资源获取功能使用[!DNL Brand Portal]帮助客户与机构用户接洽，为新营销活动、照片拍摄和项目获取资源。 请参阅 [!DNL Brand Portal][&#128279;](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=zh-Hans)中的资源源。

* [!DNL Brand Portal]使用情况报告现在仅显示活动用户。 现在不显示非活动用户。 活动用户是其帐户在[!DNL Admin Console]中被分配给产品配置文件的用户。 查看[[!DNL Brand Portal] 报告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html?lang=zh-Hans)。

* 在[!DNL Brand Portal]中引入了一个新的下载设置，通过该设置，在下载文件夹、收藏集等内容时，您可以为每个资源创建单独的文件夹。 请参阅[下载设置](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html?lang=zh-Hans)。

## [!DNL Assets] 中的错误修复 {#bug-fixes-assets}

* 选择多个资源以更新属性时，有时会发生错误或取消选择的资源的属性会更新。 (CQ-4316532)
* 尝试打开[!UICONTROL Assets管理员搜索边栏]时，页面保持空白，单击[!UICONTROL 编辑] > [!UICONTROL 设置]将生成错误。 (CQ-4315079)
* 解决命名冲突后创建现有资源的新版本时，原始资源的元数据将被覆盖。 (CQ-4313594)
* 打印具有长批注文本的资源时，即使空间可用，批注文本也会被裁剪。 (CQ-4314101)

## Adobe Experience Manager Commerceas a Cloud Service {#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：使用体验片段单独丰富产品目录页面。

* 扩展了产品控制台属性，可显示链接的Assets和体验片段，包括快速导航到关联内容的操作。

* 发布了CIF Venia参考网站 — 2021.02.24，其中包括最新的CIF核心组件版本v1.8.0。有关详细信息，请参阅[CIF Venia引用站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)。

* 已发布CIF核心组件v1.8.0。有关详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)。

## Cloud Manager {#cloud-manager}

### 发布日期 {#release-date-cm}

AEM as a Cloud Service 2021.2.0 中的 Cloud Manager 的发布日期是 2021 年 2 月 11 日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets 客户现在可以通过 Cloud Manager UI 以自助方式选择何时何地部署其 Brand Portal 实例。 对于具有 Assets 解决方案的常规（非沙盒）计划，现在可以在生产环境中配置 Brand Portal。 在生产环境中只能进行一次资源调配。

* 项目和沙盒创建中使用的 AEM 项目原型已更新至版本 25。

* 代码扫描期间确定的不推荐使用的 API 列表已经过优化，现包括最新 Cloud Service SDK 版本中不推荐的其他类和方法。

* 已更新 Cloud Manager 的 SonarQube 配置文件，移除 Sonar 规则 squid:S2142。 这将不再与“会话中断”检查冲突。

* Cloud Manager UI 将通知暂时无法添加/更新域名的用户，因为关联的环境已连接正在运行的管道，或者当前正在等待批准步骤。

* 以 Sonar 为前缀的客户 `pom.xml` 文件中设置的属性现已动态移除，以避免构建和质量扫描失败。

* 如果 SSL 证书正由当前部署的域名使用，Cloud Manager UI 将通知暂时无法选择该证书的用户。

* 添加了其他代码质量规则，涵盖 Cloud Service 兼容性问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 根据域名匹配 SSL 证书不再区分大小写。

* 如果证书私钥不符合 2048 位限制，Cloud Manager UI 将通知用户并显示相应的错误消息。

* 如果 SSL 证书正由当前部署的域名使用，Cloud Manager UI 将通知暂时无法选择该证书的用户。

* 在某些情况下，内部问题可能会导致环境删除被卡住。

* 某些管道故障被错误地报告为管道错误。

## 内容转移工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt}

内容传输工具版本1.2.4的发布日期为2021年2月10日。

### 错误修复 {#bug-fixes-ctt}

* 映射多个用户时，某些用户的IMS ID映射不正确。 此问题已得到修复。

### 发布日期 {#release-date-ctt-feb}

内容传输工具版本1.2.2的发布日期为2021年2月1日。

### 内容传输工具的新增功能 {#what-is-new-ctt}

* 向内容传输工具添加了新功能和UI — 用户映射工具。 此功能在内容迁移活动中自动将现有用户和组映射到其AdobeIdentity Management系统ID。
有关更多详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=zh-Hans)。
* 内容传输工具现在迁移在迁移集中引用的所有组和用户，包括儿童。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。

## Best Practices Analyzer {#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的发布日期是2021年2月18日。

### Best Practices Analyzer的新增功能 {#what-is-new-bpa}

* 能够检测AEM Forms和AEM Forms实施的使用，并指示与迁移到AEM Formsas a Cloud Service相关的区域。
* 能够检测和报告自定义组件和模板的使用情况和计数。
* 能够检测使用的节点存储和数据存储的类型。
* 能够检测Dynamic Media的使用情况。
* 能够检测使用的Java版本。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具的新增功能 {#what-is-new-crt}

* 发布了AIO-CLI插件的新版本。 此插件的最新版本包括针对Repository Modernizer的多个错误修复。
请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=zh-Hans#benefits)，了解有关此插件的更多信息。

### 错误修复 {#bug-fixes-crt}

* 对Repository Modernizer进行了若干错误修复。
有关更多详细信息，请参阅[GitHub资源：aem-cloud-service-source-migration](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
