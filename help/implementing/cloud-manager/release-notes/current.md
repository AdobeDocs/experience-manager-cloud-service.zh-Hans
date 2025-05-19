---
title: Cloud Manager 2025.5.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 21%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.5.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.5.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.5.0的发布日期是2025年5月8日星期四。

下一个计划发布于2025年6月5日星期四。

## 新增功能 {#what-is-new}

### 通过一次单击为Edge Delivery Services配置内容源

Adobe Experience Manager (AEM) Edge Delivery Services允许使用全球分布式快速边缘网络从多个来源(如Google Drive、SharePoint或AEM本身)进行内容交付。

Helix 4和Helix 5的内容源配置不同。 了解这两个版本的区别，并按照全面的配置步骤、示例和验证说明进行操作。

请参阅[配置内容源](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md)。


## 早期采用者计划 {#early-adoption}

参与Cloud Manager的早期采用者计划，在即将发布的功能正式发布之前获得对这些功能的独家访问权。

目前提供以下早期采用商机：

### 添加Edge Delivery配置管道 {#add-eds-pipeline}

使用Edge Delivery Services构建的站点现在支持配置管道，从而扩展此功能而不只是Cloud Service环境。 在适用的情况下，您可以使用&#x200B;**配置管道**&#x200B;来管理流量过滤规则和Web应用程序防火墙(WAF)配置等设置。 请参阅[支持的配置](/help/operations/config-pipeline.md#configurations)。

![在添加管道下拉列表中添加Edge Delivery管道](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)发送电子邮件。

### 自带Git — 现在支持Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将其Azure DevOps Git存储库载入到Cloud Manager中，并支持现代Azure DevOps和旧版VSTS (Visual Studio Team Services)存储库。

* 对于Edge Delivery Services用户，已载入的存储库可用于同步和部署网站代码。
* 对于AEM as a Cloud Service和Adobe Managed Services (AMS)用户，存储库可以同时链接到全栈管道和前端管道。

即将支持其他管道类型以及通过代码质量管道进行拉取请求验证。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

#### 关于自带Git的常见问题解答

| 问题 | 答案 |
|---|---|
| *如果需要，项目如何切换回Adobe管理的Git存储库？* | 切换回是简单直接的。 [更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)以指向Adobe存储库，如果不再需要外部存储库，则将其移除。 |
| *是否可以针对不同的环境（例如，非生产环境与生产环境）配置不同的存储库以允许首先在非生产环境中进行测试？* | 可以，可以为不同的环境配置不同的存储库。 例如，当生产管道保持连接到Adobe存储库时，开发或代码质量管道可以指向外部存储库。 在此配置期间，请确保两个存储库之间的同步作业保持活动状态。 |
| *现有设置(如IP允许列表)是否继续工作？* | 是的，现有的IP允许列表仍可照常工作。 但是，如果外部Git存储库受防火墙保护，则必须将必要的[Adobe IP地址添加到允许列表](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有GitLab存储库URL是否都有效？ 使用的存储库URL格式为`https://gitlab_dedicated_url.com/path/repo-name.git`，这与文档中的示例不同。* | 是，支持任何支持API V3或V4的GitLab存储库，包括自托管的GitLab URL，如[在Cloud Manager中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`)中所述。 |


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

