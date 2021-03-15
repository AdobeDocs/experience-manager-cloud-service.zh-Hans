---
title: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
description: 作为Cloud Service的 [!DNL Adobe Experience Manager] 当前发行说明。
translation-type: tm+mt
source-git-commit: 5dabb0f9f119d8c56c4b1b64e1528f03e1a92fac
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager]作为Cloud Service{#release-notes}的当前发行说明

以下部分概述了作为Cloud Service的[!DNL Experience Manager]当前（最新）版本的一般发行说明。

>[!NOTE]
>您可以从此处导航到先前版本的发行说明；例如，2020年、2021年等年。

>[!NOTE]
>
>请参阅[最近文档更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html)，了解与版本不直接相关的文档更新的详细信息。

## 发布日期 {#release-date}

[!DNL Adobe Experience Manager]作为Cloud Service2021.2.0的发布日期为2021年2月25日。
以下版本(2021.3.0)将于2021年3月25日发布。

## [!DNL Adobe Experience Manager Sites] 作为Cloud Service  {#sites}

* **[RemotePage组件](/help/implementing/developing/hybrid/remote-page.md)**:增加了在AEM中使用查看和编辑外部SPA的支持。

* **[在AEM中编辑外部SPA](/help/implementing/developing/hybrid/editing-external-spa.md)**:添加了将独立单页应用程序上传到AEM实例、添加内容的可编辑部分以及启用创作的功能。

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## [!DNL Assets] {#what-is-new-assets}中的新增功能

* 企业现在可以使用[!DNL Brand Portal]来源资产。 资产来源功能利用[!DNL Brand Portal]来帮助客户与代理用户互动，为新的营销活动、照片和项目寻找资产。 请参阅 [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html)中的[资产来源补充。

* [!DNL Brand Portal]使用情况报告现在仅显示活动用户。 不活动的用户现在不显示。 活动用户是将其帐户分配给[!DNL Admin Console]中的产品用户档案的用户。 请参阅[[!DNL Brand Portal] 报告](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html)。

* 在[!DNL Brand Portal]中，引入了新的下载设置，允许您在下载文件夹、集合等时为每个资产创建单独的文件夹。 请参阅[下载设置](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html)。

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## [!DNL Assets] {#bug-fixes-assets}中的错误修复

* 在解决命名冲突后创建现有资产的新版本时，将覆盖原始资产的元数据。 (CQ-4313594)
* 打印带有长注释文本的资产时，即使有空间，注释文本也会被裁切。 (CQ-4314101)
* 当选择多个资产以更新属性时，有时会发生错误，或者取消选择的资产的属性会被更新。 (CQ-4316532)
* 尝试打开[!UICONTROL 资产管理搜索边栏]时，页面仍为空，单击[!UICONTROL 编辑] > [!UICONTROL 设置]会生成错误。 (CQ-4315079)

## Adobe Experience Manager Commerce as aCloud Service{#cloud-services-commerce}

### 新增功能 {#what-is-new-commerce}

* 产品体验管理：使用Experience Fragments单独丰富产品目录页面。

* 可显示链接资产和体验片段的扩展产品控制台属性，包括快速导航到相关内容的操作。

* 已发布CIF委内瑞拉参考站点 — 2021.02.24，其中包括最新的CIF核心组件版本v1.8.0。有关更多详细信息，请参阅[CIF委内瑞拉参考站点](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24)。

* 已发布CIF核心组件v1.8.0。有关更多详细信息，请参阅[CIF核心组件](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0)。

## Cloud Manager {#cloud-manager}

本节概述AEM中作为Cloud Service 2021.3.0的Cloud Manager发行说明。

## 发布日期 {#release-date-cm-march}

AEM中Cloud Manager作为Cloud Service 2021.3.0的发布日期为2021年3月11日。
下一版本计划于2021年4月08日发布。


### 新增功能 {#what-is-new-march}

* 拥有[IP允许列表](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn)、[SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn)和[自定义域名](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn)预存自定义域名配置的环境的客户将看到有关其先前现有配置的消息，并将能够通过UI自助服务。 用户现在可以：
   * 将“站点”解决方案添加到包含资产的现有项目（反之亦然）。
   * 将站点（或资产）从包含站点和资产的现有项目中删除。
   * 将第二个未使用的解决方案授权添加到现有项目或作为新项目。

* 拥有必需权限的用户现在可以编辑项目，允许他们以自助方式执行以下操作。

* **AEM Push** Updatelabel现在将同时显示在Pipeline Executive和 *Activity* 屏幕 ** 上。

* 如果环境已休眠，但也有可用的AEM更新，则&#x200B;**已休眠**&#x200B;状态将优先于&#x200B;**可用更新**。

* 现在，用户在导航至Unified Shell的“用户用户档案”图标（右上方）后，通过选择“视图 Cloud Manager角色”选项，即可查看其Cloud Manager角色。

* 标签&#x200B;**申请批准**&#x200B;已重新标记到&#x200B;**生产批准**，以便更清晰。

* **版本**&#x200B;标签已重新标记到“生产”管线执行屏幕中的&#x200B;**Git标签**。

* 当重要量度未达到定义的阈值时定义行为的标签已重新标记，以反映其真实行为 — **取消立即**&#x200B;和&#x200B;**批准立即**。

* 类和方法弃用列表已根据AEM Cloud Service SDK的`2021.3.4997.20210303T022849Z-210225`版本进行更新。

* Cloud Manager生产渠道现在将包含自定义UI测试功能。

### 错误修复 {#bug-fixes-cm-march}

* 在AEM推送升级期间，在某些情况下跳过了包版本控制。

* 在将包嵌入到其他包中时，未正确发现某些质量问题。

* 在模糊情况下，打开“添加项目”对话框时生成的默认项目名称可能是现有项目名称的重复。

* 有时，如果用户在启动管道后立即从管道执行页面导航离开，将显示一条错误消息，指出操作失败，尽管实际执行会开始。

* 当客户生成导致包无效时，不必要地重新启动生成步骤。

* 有时，即使未部署IP，用户也会在IP旁看到允许列表绿色的“活动”状态。

* 所有现有生产管道将通过体验审核步骤自动启用。


### 发布日期 {#release-date-cm}

AEM中Cloud Manager作为Cloud Service 2021.2.0的发布日期为2021年2月11日。

### 新增功能 {#what-is-new-cloud-manager}


* Assets客户现在可以通过Cloud Manager UI以自助方式选择何时何地部署其Brand Portal实例。 对于具有资产解决方案的常规（非沙箱）项目，现在可以在生产环境上设置Brand Portal。 在生产环境上只能执行一次设置。

* 在“项目”和“沙箱创建”中使用的AEM Project原型已更新为版本25。

* 在代码扫描过程中识别的已弃用API的列表已得到改进，以包括最新Cloud Service SDK版本中已弃用的其他类和方法。

* SonarQube 用户档案 for Cloud Manager已更新以删除Sonar规则squid:S2142。 这不再与“线程中断检查”冲突。

* Cloud Manager UI将通知暂时无法添加/更新域名的用户，因为关联的环境已连接正在运行的管道，或者当前正在等待批准步骤。

* 现在，将动态删除客户`pom.xml`文件中设置的属性，以避免生成和质量扫描失败。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则该用户可能暂时无法选择该证书。

* 已添加其他代码质量规则，以解决Cloud Service兼容性问题。

### 错误修复 {#bug-fixes-cloud-manager}

* 与域名匹配的SSL证书不再区分大小写。

* 现在，如果证书私钥不符合2048位限制，Cloud Manager用户界面将通知用户，并显示相应的错误消息。

* Cloud Manager UI将通知用户，如果当前正在部署的域名正在使用SSL证书，则用户可能暂时无法选择该证书。

* 在某些情况下，内部问题可能导致环境删除卡住。

* 某些管线故障被错误地报告为管线错误。

## 内容传输工具 {#content-transfer-tool}

### 发布日期 {#release-date-ctt-march}

内容传输工具v1.3.0的发布日期为2021年3月04日。

### 内容传输工具{#what-is-new-ctt-march}的新增功能

* CTT现在安装到`/apps`，而不是`/libs`某些页面的浏览器书签可能不再有效。
* 安装CTT后，用户将必须浏览其他级别才能进入“内容传输”页面。 有关详细信息，请参阅[使用内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html)。

### 错误修复 {#bug-fixes-ctt-march}

* 从特定路径迁移内容时，CTT正在调用不相关的资源。 已修复


### 发布日期 {#release-date-ctt}

内容传输工具v1.2.4的发布日期为2021年2月10日。

### 错误修复 {#bug-fixes-ctt}

* 映射多个用户时，某些用户的IMS ID映射不正确。 此问题已解决。

### 发布日期 {#release-date-ctt-feb}

内容传输工具v1.2.2的发布日期为2021年2月01日。

### 内容传输工具{#what-is-new-ctt}的新增功能

* 内容传输工具 — 用户映射工具新增功能和UI。 此功能会自动将现有用户和用户组映射到其AdobeIdentity Management系统ID，作为内容迁移活动的一部分。
有关详细信息，请参阅[使用用户映射工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html)。
* 内容传输工具现在可迁移迁移集中引用的所有组和用户，包括子项。
* 在创建迁移集时，允许用户选择`/etc`下的某些路径。

## 最佳实践分析器{#best-practices-analyzer}

### 发布日期 {#release-date-bpa}

Best Practices Analyzer v2.1.2的发布日期为2021年2月18日。

### 最佳实践分析器{#what-is-new-bpa}的新增功能

* 能够检测AEM Forms和AEM Forms实施的使用情况并指示与作为Cloud Service迁移到AEM Forms相关的领域。
* 能够检测并报告自定义组件和模板的使用情况和计数。
* 能够检测使用的节点存储和数据存储的类型。
* 能够检测Dynamic Media的使用情况。
* 能够检测使用的Java版本。

## 代码重构工具 {#code-refactoring-tools}

### 代码重构工具{#what-is-new-crt}的新增功能

* 已发布AIO-CLI插件的新版本。 此插件的最新版本包括存储库Modernizer和调度程序转换器的几个新增功能和错误修复。    请参阅[统一体验](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits)以了解有关此插件的更多信息。

* Repository Modernizer的新增功能和增强功能。 请参阅[GitHub资源：最新版本的存储库Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)。
   * 将OSGi配置（RepoInit配置除外）标准化为首选.cfg.json格式。
   * 将OSGi配置文件夹重命名为指定格式。
   * 生成ui.apps.structure项目。
   * 创建分析模块。

* Dispatcher Converter的新增功能和增强功能。 请参阅[GitHub资源：调度程序转换器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * 为不同包含创建单独文件，而不是在内容中排列。
   * 能够同时处理vhosts的文件夹路径和vhost文件的路径。
   * 生成客户配置范围在600个以上的农场文件。










