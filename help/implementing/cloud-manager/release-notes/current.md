---
title: Cloud Manager 2025.7.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.7.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: cf36a5f22132695be47c3d52292f59f785a0fd52
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 59%

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

  参阅[许可证仪表板](/help/implementing/cloud-manager/license-dashboard.md)。

## 早期采用者计划 {#private-beta-program}

参与Cloud Manager的Alpha和Beta计划，在正式发布之前独家提前访问即将推出的功能。

当前提供以下机会：

### 管道部署的一键式回滚 {#one-click-rollback}

如果最新的客户源代码无法按预期工作，请快速还原到以前的部署，而无需重新运行完整管道或手动还原提交。<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![从环境信息卡](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *环境信息卡还原客户源代码，其中显示选定环境的&#x200B;**还原**>**已部署的先前代码**&#x200B;选项。*


![还原先前部署的代码对话框](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*在&#x200B;**还原先前部署的代码**&#x200B;对话框中，查看当前部署的版本以及要还原的版本，然后单击&#x200B;**确认***。


![正在还原激活](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager将环境回滚到以前的生成，保持内容和配置不变，并标记环境&#x200B;**正在还原**，直到部署完成。*


![正在使用的Source代码版本](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *如上所示，“环境”详细信息视图现在也显示了正在使用的活动源代码版本。*

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[restorecode@adobe.com](mailto:restorecode@adobe.com)发送电子邮件。

另请参阅[AEM as a Cloud Service中的内容还原](/help/operations/restore.md)。


### 专用测试环境 {#specialized-test-environment}

Cloud Manager 现已支持添加名为&#x200B;**专用测试环境**&#x200B;的新环境类型。该环境旨在帮助团队在正式上线之前在接近生产的条件下验证功能。此环境类型不同于&#x200B;*生产 + 预发布*、*开发*&#x200B;或&#x200B;*快速开发*&#x200B;环境，而是专为运行高级验证场景提供的集中空间。

最近的增强功能：您现在可以通过更简单、更直观的工作流程在非生产管道上配置专门的测试环境。 简化的设置可加快完成过程并减少配置错误。

请参阅[添加专门的测试环境](/help/implementing/cloud-manager/specialized-test-environment.md)。

![“添加环境”对话框中，其中选中了“专门测试环境”单选按钮](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 相关联的电子邮件地址发送电子邮件至 [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com)。


### 自带 (BYOG) Git - 现支持 Azure DevOps {#gitlab-bitbucket-azure-vsts}

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

