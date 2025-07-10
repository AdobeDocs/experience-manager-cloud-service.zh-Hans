---
title: Cloud Manager 2025.7.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.7.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 26fbc60b1348e8c5f42adc8fd0e596b639fe9b44
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 64%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.7.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.7.0 版本。

另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.7.0的发布日期是2025年7月10日星期四。

下一个计划发布于2025年8月7日星期四。

## 新增功能 {#what-is-new}

* **Cloud Manager添加了ECDSA（椭圆曲线数字签名算法）SSL证书支持**

  Cloud Manager现在支持ECDSA证书。 该功能通过较小的密钥大小提供强大的安全性，使客户能够在其CDN配置中应用轻量级现代加密。<!-- https://jira.corp.adobe.com/browse/CMGR-62399 -->

* **下载网站许可证使用情况报告**

  在&#x200B;**站点使用情况详细信息**&#x200B;页面(在Cloud Manager中，单击&#x200B;**许可证**)。 在“解决方案”表的&#x200B;**站点**&#x200B;行中，单击&#x200B;**查看使用情况详细信息**，客户现在可以单击&#x200B;**下载报表**，将其数据导出为CSV文件。 此下载可简化分析和共享使用趋势。<!-- https://jira.corp.adobe.com/browse/CMGR-42274 -->

  ![站点使用情况详细信息页面](/help/implementing/cloud-manager/release-notes/assets/sites-license-usage-page.png)

## 早期采用者计划 {#private-beta-program}

参与Cloud Manager的Alpha和Beta计划，在正式发布之前独家提前访问即将推出的功能。

当前提供以下机会：


### 管道部署的一键式回滚 {#one-click-rollback}

如果最新的代码无法按预期工作，请快速还原到以前的部署，而无需重新运行完整管道或手动还原提交。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

<!-- Add link to topic within the affected article ==>


### Specialized Testing Environment {#specialized-test-environment}

Cloud Manager now supports the addition of a new environment type called **Specialized Testing Environment**. The environment is designed to help teams validate features under near-production conditions before going live. This environment type is distinct from *Production + Stage*, *Development*, or *Rapid Development* environments and offers a focused space for running advanced validation scenarios.

Recent enhancement: You can now configure specialized testing environments on a non-production pipeline through a simpler, more intuitive workflow. The streamlined setup speeds completion and reduces configuration errors.

See [Add a Specialized Testing Environment](/help/implementing/cloud-manager/specialized-test-environment.md).

![Add environment dialog box with Specialized Testing Environment radio button selected](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID.


### Bring Your Own Git (BYOG) - now with support for Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

客户现在可以将他们的 Azure DevOps Git 存储库加入到 Cloud Manager 中，同时支持现代 Azure DevOps 和旧版 VSTS（Visual Studio Team Services）两种存储库。

* Edge Delivery Services 用户可以使用已加入的存储库来同步和部署网站代码。
* 对于 AEM as a Cloud Service 和 Adobe Managed Services (AMS) 用户，该存储库可以链接到全栈和前端两种管道。

对其他管道类型以及通过代码质量管道进行提取请求验证的支持即将推出。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。


**有关 BYOG 的常见问题解答**

| 问题 | 解答 |
|---|---|
| *需要时，应如何将项目切换回 Adobe 管理的 Git 存储库？* | 切换回来很简单。[更新管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md)，使其指向 Adobe 存储库，如果不再需要外部存储库，可将其删除。 |
| *是否可以为不同的环境（例如非生产环境与生产环境）配置不同的存储库，以允许首先在非生产环境中进行测试？* | 是的，可以为不同的环境配置不同的存储库。例如，开发或代码质量管道可以指向外部存储库，生产管道可继续连接到 Adobe 存储库。确保在使用此配置期间两个存储库之间的同步作业保持活跃。 |
| *IP 允许列表等现有设置是否继续有效？* | 是的，现有的 IP 允许列表仍会照常工作。但是如果外部 Git 存储库受到防火墙保护，必要的 [Adobe IP 地址就必须添加到允许列表中](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)。 |
| *所有 GitLab 存储库 URL 都有效吗？使用的存储库 URL 采用此格式 `https://gitlab_dedicated_url.com/path/repo-name.git`，这与文档中的示例不同。* | 是的，任何支持 API V3 或 V4 的 GitLab 存储库都受支持，包括自托管的 GitLab URL，例如[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)中描述的存储库（`https://git-vendor-name.com/org-name/repo-name.git`）。 |


#### 管理访问令牌{#manage-access-tokens}

在 Cloud Manager 中使用&#x200B;**管理访问令牌**&#x200B;功能，可查看、重命名并删除与外部自带 Git 存储库（如 GitHub Enterprise、GitLab、Bitbucket 和 Azure DevOps）关联的访问令牌。

请参阅[管理访问令牌](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。


### 添加 Edge Delivery 配置管道 {#add-eds-pipeline}

现在，使用 Edge Delivery Services 构建的站点支持配置管道，将此功能扩展到云服务环境之外。您可以使用&#x200B;**配置管道**&#x200B;来管理设置，例如流量过滤规则和 Web 应用程序防火墙 (WAF) 配置（如适用）。请参阅[受支持的配置](/help/operations/config-pipeline.md#configurations)。

![在“添加管道”下拉列表中添加 Edge Delivery 管道](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *从&#x200B;**程序概览**&#x200B;页面的&#x200B;**管道**&#x200B;卡片中添加 Edge Delivery 管道。*

![添加 Edge Delivery 管道对话框](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *添加 Edge Delivery 管道对话框。*

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com)。


## 错误修复

* Cloud Manager现在会在环境升级期间更新所有管道的发行版本，以确保在所有管道类型间进行一致的版本跟踪。<!-- CMGR-69043 -->
* 现在，当域验证(DV) SSL证书失败时，UI会显示状态和详细错误消息，这有助于了解并解决证书问题。<!-- CMGR-68872 -->
* 在编辑域映射时，UI现在会阻止选择与所选域不匹配的SSL证书，从而减少错误配置并提高安装期间的可靠性。<!-- CMGR-64307 -->
* 在某些情况下，证书未被正确删除，维护域仍处于活动状态。<!-- CMGR-69867 -->
* 修复了在某些情况下可能阻止从&#x200B;*Adobe Assets*&#x200B;升级到&#x200B;*Adobe Assets Ultimate*&#x200B;的问题。 现在，过渡更加顺畅、更加可靠。<!-- CMGR-69506 -->
* 解决了在创建多区域环境时自动设置关键区域字段以支持顺利的下游服务和部署的问题。<!-- CMGR-69471 -->
* 解决了某些配置管道在执行后未正确停止的问题。 现在，管道已成功完成并按预期关闭，提高了可靠性。<!-- CMGR-69344 -->


<!-- ## Known issues {#known-issues} -->

