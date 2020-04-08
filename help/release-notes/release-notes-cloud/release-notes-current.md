---
title: 2020.4.0 版发行说明
description: 2020.4.0 版发行说明
translation-type: tm+mt
source-git-commit: c6c0e93d881762a2b501abb3d8c8356046a5f082

---


# AEM 云服务 2020.4.0 发行说明 {#release-notes}

以下部分概述了 Experience Manager 云服务 2020.4.0 的常规发行说明。

## Release Date {#release-date}

Experience Manager作为云服务2020.4.0的发布日期为2020年4月9日。

## 资产 {#assets}

请按照本节的说明，了解AEM中Experience Manager资产和Dynamic Media的新增功能以及2020.4.0版云服务的更新。

### 新增功能 {#assets-what-is-new}

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) 可作为云服务资产提供给AEM，支持资产分发使用案例。 Brand Portal 可以将获得批准的品牌和产品资产安全地分发给外部代理、合作伙伴、内部团队和经销商进行下载，从而帮助组织满足其营销需求。
   * 品牌门户配置通过Adobe I/O控制台完成
   * AEM作为云服务尚不支持品牌门户中的资产来源补充
* AEM作为云服务支持 [新版本的Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html) 2.0。 Adobe Asset Link通过应用程序内资产链接面板将AEM资产与Creative Cloud桌面应用程序Photoshop、Illustrator和InDesign相连，从而简化了创意人员与营销人员在内容创建过程中的协作。
   * AEM作为云服务已为Adobe Asset Link预配置，从而简化了 [配置](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)。
   * 资产链接现在支持 [AEM环境切换程序](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)，允许创意用户更轻松地连接到不同的AEM环境（例如，当代理设计人员使用AEM资产与多个客户端协作时）
* 可以在特定文件夹 [层次结构的文件夹属性](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) UI中为后处理工作流配置自动开始。
   * 文件夹属性UI已经简化，新的“资产处理”选项卡包含元数据用户档案、处理用户档案和新的自动开始工作流配置
* 资产重新处理对话框允许您选择特定的处理用户档案并决定在子文件夹中重新处理
* Dynamic Media:添加了选择性发布配置，这意味着资产仅为安全预览而自动发布，并且可以显式发布到AEM，而不发布到DMS7以在公共域中投放。

### 错误修复 {#assets-bug-fixes}

* 资产处理中的修复
* 修复了Dynamic Media配置问题并将资产发布到Dynamic Media投放服务
