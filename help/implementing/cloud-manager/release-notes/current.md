---
title: Cloud Manager 2025.6.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.6.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 52c8745d3a3cc4bc41003a258a85a817e7ccb48b
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 89%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.6.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.6.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2025.6.0 的发布日期是 2025 年 6 月 5 日星期四。

下一个版本计划于 2025 年 7 月 10 日星期四发布。

## 新增功能 {#what-is-new}

* **许可证仪表板现在包含Edge Delivery Services许可证**

  许可仪表板现已显示 Edge Delivery Services 的许可使用情况，帮助您更清晰地了解您的授权权益与当前状态。<!-- CMGR-67686 -->

  ![许可证仪表板](/help/implementing/cloud-manager/assets/license-dashboard.png)

  参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

* **Edge Delivery站点配置已更新**

  通过请求 **Edge Delivery 原始地址**，而非&#x200B;**存储库 URL**，简化了添加 Edge Delivery 站点的流程，使入门与配置更加快捷直观<!-- CMGR-67686 -->。

  ![添加 Edge Delivery 站点对话框](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  请参阅[添加 Edge Delivery 站点](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md)。

* **管道收藏夹**

  在本次版本更新中，Cloud Manager 引入了管道收藏功能，您可以将特定的 Pipeline 标记为收藏项，使其显示在&#x200B;**管道**&#x200B;页面列表的顶部。此项增强功能可帮助您更轻松地查找并运行常用的管道。<!-- CMGR-68293 -->

  ![标记为收藏的管道](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *已标记为收藏的两个管道。*

  请参阅[将管道标记为收藏](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites)。


## 早期采用者计划 {#early-adoption}

参与 Cloud Manager 的早期采用者计划，在即将推出的功能正式发布之前获得独家访问权限。

目前提供以下早期采用者机会：


### 专用测试环境 {#specialized-test-environment}

Cloud Manager 现已支持添加名为&#x200B;**专用测试环境**&#x200B;的新环境类型。该环境旨在帮助团队在正式上线之前在接近生产的条件下验证功能。此环境类型不同于&#x200B;*生产 + 预发布*、*开发*&#x200B;或&#x200B;*快速开发*&#x200B;环境，而是专为运行高级验证场景提供的集中空间。

请参阅[添加专门的测试环境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![“添加环境”对话框中，其中选中了“专门测试环境”单选按钮](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)。


### 自带Git (BYOG) — 现在支持Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将他们的 Azure DevOps Git 存储库加入到 Cloud Manager 中，同时支持现代 Azure DevOps 和旧版 VSTS（Visual Studio Team Services）两种存储库。

* Edge Delivery Services 用户可以使用已加入的存储库来同步和部署网站代码。
* 对于 AEM as a Cloud Service 和 Adobe Managed Services (AMS) 用户，该存储库可以链接到全栈和前端两种管道。

对其他管道类型以及通过代码质量管道进行提取请求验证的支持即将推出。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。


**有关BYOG的常见问题解答**

| 问题 | 解答 |
|---|---|
| *需要时，应如何将项目切换回 Adobe 管理的 Git 存储库？* | 切换回来很简单。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，使其指向 Adobe 存储库，如果不再需要外部存储库，可将其删除。 |
| *是否可以为不同的环境（例如非生产环境与生产环境）配置不同的存储库，以允许首先在非生产环境中进行测试？* | 是的，可以为不同的环境配置不同的存储库。例如，开发或代码质量管道可以指向外部存储库，生产管道可继续连接到 Adobe 存储库。确保在使用此配置期间两个存储库之间的同步作业保持活跃。 |
| *IP 允许列表等现有设置是否继续有效？* | 是的，现有的 IP 允许列表仍会照常工作。但是如果外部 Git 存储库受到防火墙保护，必要的 [Adobe IP 地址就必须添加到允许列表中](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存储库 URL 都有效吗？使用的存储库 URL 采用此格式 `https://gitlab_dedicated_url.com/path/repo-name.git`，这与文档中的示例不同。* | 是的，任何支持 API V3 或 V4 的 GitLab 存储库都受支持，包括自托管的 GitLab URL，例如[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)中描述的存储库（`https://git-vendor-name.com/org-name/repo-name.git`）。 |


#### 管理访问令牌{#manage-access-tokens}

在Cloud Manager中使用&#x200B;**管理访问令牌**&#x200B;查看、重命名和删除与外部BYOG存储库（例如GitHub Enterprise、GitLab、Bitbucket和Azure DevOps）关联的访问令牌。

请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)发送电子邮件。


### 添加 Edge Delivery 配置管道 {#add-eds-pipeline}

现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

![在“添加管道”下拉列表中添加 Edge Delivery 管道](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *从&#x200B;**程序概览**&#x200B;页面的&#x200B;**管道**&#x200B;卡片中添加 Edge Delivery 管道。*

![添加 Edge Delivery 管道对话框](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *添加 Edge Delivery 管道对话框。*

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 错误修复

* 先前标记为 `HIBERNATED` 的沙盒环境不再停留在该状态，从而允许管道执行或部署按预期进行。 <!-- CMGR-67705 -->
* AEM Cloud Manager 现在能够正确地将由于在获取客户工件时发生 409 错误（冲突）导致的 Maven 构建失败，映射为客户导致的失败。这一变更通过区分内部错误和与客户环境设置相关的问题，改进了错误消息的显示方式。<!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

