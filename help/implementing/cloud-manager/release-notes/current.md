---
title: Cloud Manager 2025.5.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 95%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2025.5.0 的发布日期是 2025 年 5 月 8 日星期四。

下一个版本计划于 2025 年 6 月 5 日星期四发布。

## 新增功能 {#what-is-new}

### 一键配置 Edge Delivery Services 的内容源

Adobe Experience Manager (AEM) Edge Delivery Services 允许使用一个全球分布的快速边缘网络从多个来源（例如 Google Drive、SharePoint 或 AEM 本身）传递内容。

Helix 4和Helix 5的内容源配置不同。 了解这两个版本的区别，并按照全面的配置步骤、示例和验证说明进行操作。

请参阅[配置内容源](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md)。


## 早期采用者计划 {#early-adoption}

参与 Cloud Manager 的早期采用者计划，在即将推出的功能正式发布之前获得独家访问权限。

目前提供以下早期采用者机会：

### 添加 Edge Delivery 配置管道 {#add-eds-pipeline}

现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

![添加“添加管道”下拉列表中的 Edge Delivery 管道](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。

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


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

