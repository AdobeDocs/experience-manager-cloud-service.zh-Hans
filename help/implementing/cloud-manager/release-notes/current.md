---
title: Cloud Manager 2025.6.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.6.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 9e2be3cabe0a93e6e357ceb5ecf4950c25d034d0
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 57%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.6.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.6.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.6.0的发布日期是2025年6月5日星期四。

下一个计划发布于2025年7月10日星期四。

## 新增功能 {#what-is-new}

* **(UI)许可证仪表板现在包含Edge Delivery Services许可证**

  Edge Delivery Services许可证使用情况现在显示在许可证仪表板中，使您能够更清楚地查看权利和状态。<!-- CMGR-67686 -->

  ![许可证功能板](/help/implementing/cloud-manager/assets/license-dashboard.png)

  查看[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

* **(UI) Edge Delivery站点配置已更新**

  通过请求&#x200B;**Edge Delivery Origin**&#x200B;而不是&#x200B;**存储库URL**，简化了添加Edge Delivery站点的流程，使载入和设置更快、更直观<!-- CMGR-67686 -->

  ![添加Edge Delivery站点对话框](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  请参阅[添加Edge Delivery站点](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。

* **(UI)管道收藏夹**

  在此版本中，Cloud Manager引入了pin收藏管道的功能，允许您将特定管道标记为收藏夹，以便它们显示在&#x200B;**管道**&#x200B;页面上的列表顶部。 此增强功能使经常访问的管道更容易查找和运行。<!-- CMGR-68293 -->

  ![管道标记为收藏](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *两个管道标记为收藏。*

  查看[标记管道收藏夹](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites)。


## 早期采用者计划 {#early-adoption}

参与 Cloud Manager 的早期采用者计划，在即将推出的功能正式发布之前获得独家访问权限。

目前提供以下早期采用者机会：


### 管理访问令牌{#manage-access-tokens}

使用Cloud Manager中的&#x200B;**管理访问令牌**&#x200B;功能查看、重命名和删除与外部自带Git存储库关联的访问令牌，例如GitHub Enterprise、GitLab、Bitbucket和Azure DevOps。

查看[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)

如果您有兴趣测试这项新功能并分享您的反馈，请发送电子邮件至与Adobe ID关联的电子邮件地址。


### 专用测试环境 {#specialized-test-environment}

Cloud Manager现在支持添加名为&#x200B;**Specialized Testing Environment**&#x200B;的新环境类型。 此环境旨在帮助团队在接近生产的情况下验证功能，然后再上线。 此环境类型不同于&#x200B;*生产+暂存*、*开发*&#x200B;或&#x200B;*快速开发*&#x200B;环境，并为运行高级验证方案提供了集中的空间。

请参阅[添加专用测试环境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![已选中“专用测试环境”单选按钮的“添加环境”对话框](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)发送电子邮件。


### 自带 Git - 现支持 Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将他们的 Azure DevOps Git 存储库加入到 Cloud Manager 中，同时支持现代 Azure DevOps 和旧版 VSTS（Visual Studio Team Services）两种存储库。

* Edge Delivery Services 用户可以使用已加入的存储库来同步和部署网站代码。
* 对于 AEM as a Cloud Service 和 Adobe Managed Services (AMS) 用户，该存储库可以链接到全栈和前端两种管道。

对其他管道类型以及通过代码质量管道进行提取请求验证的支持即将推出。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。


#### 关于自带 Git 的常见问题解答

| 问题 | 解答 |
|---|---|
| *需要时，应如何将项目切换回 Adobe 管理的 Git 存储库？* | 切换回来很简单。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，使其指向 Adobe 存储库，如果不再需要外部存储库，可将其删除。 |
| *是否可以为不同的环境（例如非生产环境与生产环境）配置不同的存储库，以允许首先在非生产环境中进行测试？* | 是的，可以为不同的环境配置不同的存储库。例如，开发或代码质量管道可以指向外部存储库，生产管道可继续连接到 Adobe 存储库。确保在使用此配置期间两个存储库之间的同步作业保持活跃。 |
| *IP 允许列表等现有设置是否继续有效？* | 是的，现有的 IP 允许列表仍会照常工作。但是如果外部 Git 存储库受到防火墙保护，必要的 [Adobe IP 地址就必须添加到允许列表中](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存储库 URL 都有效吗？使用的存储库 URL 采用此格式 `https://gitlab_dedicated_url.com/path/repo-name.git`，这与文档中的示例不同。* | 是的，任何支持 API V3 或 V4 的 GitLab 存储库都受支持，包括自托管的 GitLab URL，例如[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)中描述的存储库（`https://git-vendor-name.com/org-name/repo-name.git`）。 |


### 添加 Edge Delivery 配置管道 {#add-eds-pipeline}

现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

![在添加管道下拉列表中添加Edge Delivery管道](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *从&#x200B;**项目概述**页面，**管道**信息卡添加Edge Delivery管道。*

![添加Edge Delivery管道对话框](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *添加Edge Delivery管道对话框。*

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 错误修复

* 以前标记为`HIBERNATED`的沙盒环境不再保持卡在该状态，从而允许管道执行或部署按预期进行。<!-- CMGR-67705 -->
* 现在，AEM Cloud Manager在获取客户工件时将由409错误（冲突）导致的Maven构建失败正确映射到由客户导致的失败。 此更改通过区分内部错误和与客户环境设置相关的问题改进了错误消息传递。<!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

