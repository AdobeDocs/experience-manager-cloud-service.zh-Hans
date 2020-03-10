---
title: 已知问题
description: 特定于 Adobe Experience Manager 云服务已知问题的发行说明
translation-type: ht
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 已知问题 {#known-issues}

本文列出了 Adobe Experience Manager 云服务产品的已知问题。该列表会随每次连续发行的 Experience Manager 进行修订和更新。

有关已知问题的详细信息，请[联系支持人员](https://helpx.adobe.com/cn/support/experience-manager.html)。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## 资产 {#assets}

<!-- Jira label: assets-cloud-known-issues -->

一些已知问题包括：

* **元数据架构**：资产评级小部件可能导致 JSP 编译错误。解决方法是从元数据架构中删除资产评级组件。<!-- CQ-4282865 -->

资产功能的一些限制包括：

* 通过 AEM Assets 云服务，当在 AMS 上部署 AEM 6.5 站点时，“连接的资产”功能可正常工作。

### 即将推出的资产功能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assets 中有一些依赖于基础功能的功能在 Experience Manager 云服务部署架构尚不可用，这些功能预计将在稍后的阶段中启用：

* 当前未启用发布到 Brand Portal。您可以针对资产分发用例扩展和部署[资产共享共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)实施。
* 利用 Adobe I/O 的 AI 服务的增强型智能标记功能暂时不可用。
* 由于依赖于商务集成框架 API，当前未启用以下功能：
   * 照片拍摄工作流模型。
   * 未填充资产属性用户界面中的“产品信息”选项卡。
* 由于依赖于 InDesign 服务器集成，当前未启用以下功能：
   * 资产模板和资产目录。
   * InDesign 文件的多页预览。

>[!MORELIKETHIS]
>
>* [AEM 中的主要更改](aem-cloud-changes.md)
>* [已弃用和已删除的功能](deprecated-removed-features.md)
>* [发行说明](home.md)

