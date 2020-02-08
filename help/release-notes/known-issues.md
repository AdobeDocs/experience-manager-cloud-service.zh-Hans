---
title: 已知问题
description: Adobe Experience manager作为云服务的已知问题特定发行说明
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 已知问题 {#known-issues}

本文将Adobe Experience manager的已知问题列为云服务产品。 该列表会随每个连续版本的Experience Manager进行修订和更新。

[有关已知问题的更多信息](https://helpx.adobe.com/support/experience-manager.html) ，请与支持部门联系。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## 资产 {#assets}

<!-- Jira label: assets-cloud-known-issues -->

一些已知问题包括：

* **元数据架构**:资产评级构件可能导致JSP编译错误。 解决方法是从元数据架构中删除资产评级组件。 <!-- CQ-4282865 -->

资产功能的一些限制包括：

* 将AEM Assets作为云服务，当AEM 6.5站点部署到AMS时，“已连接资产”功能会正常工作。

### 即将推出的资产功能 {#upcoming-assets-capabilities}

Adobe Experience Manager资产中的一些功能（这些功能在Experience manager中尚未作为云服务部署架构提供）将在稍后阶段启用，具体取决于基础功能：

* 此阶段未启用发布到Brand Portal。 您可以扩展和部署 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) Implementation，以用于资产分发用例。
* 增强的智能标记功能利用Adobe I/O的AI服务目前不可用。
* 由于依赖于Commerce Integration Framework API，此阶段未启用功能：
   * 照片拍摄工作流模型。
   * 资产属性用户界面中的产品信息选项卡未填充。
* 由于依赖于InDesign server集成，此阶段未启用功能：
   * 资产模板和资产目录。
   * InDesign文件的多页预览。

>[!MORELIKETHIS]
>
>* [AEM中的主要更改](aem-cloud-changes.md)
>* [已弃用和已删除的功能](deprecated-removed-features.md)
>* [发行说明](home.md)

