---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.11.0 的发行说明
description: 了解AEM as a Cloud Service中的Cloud Manager 2024.11.0版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: db661281831dcb07491dca16e73e835b487814a6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 29%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.11.0 的发行说明 {#release-notes}

了解AEM (Adobe Experience Manager)as a Cloud Service中的Cloud Manager 2024.11.0版本。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.11.0的发布日期是2024年11月7日。

下一个计划发布日期为2024年12月5日。

## 新增功能 {#what-is-new}

* 使用AEM Cloud Service体验Edge Delivery Services创新的最新进展 — 现在可在您的沙盒项目中探索。 [了解详情](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md#auto-creation) <!-- (CMGR-62319) -->
* AEM Cloud Manager中的“域设置”页面现在包含一个搜索功能，可让您按名称快速查找域。 您可以在搜索字段中输入关键字以筛选和显示匹配的域，从而更轻松地有效管理多个域。 此外，该页面还提供状态筛选器，如&#x200B;**已验证**&#x200B;和&#x200B;**未验证**，以进一步细化搜索结果。<!-- (CMGR-62615) -->

域设置中的![搜索字段](/help/implementing/cloud-manager/assets/domain-settings-search.png)

## 早期采用计划 {#early-adoption}

加入 Cloud Manager 早期采用计划，即有机会测试即将推出的功能。

### AEM主页 {#aem-home}

AEM主页是一个新的集中式起点，用于管理Adobe Experience Manager中的内容、资源和站点。 AEM Home旨在提供个性化体验，帮助用户根据其角色和目标无缝导航AEM生态系统。 它旨在成为您的指南，提供关键见解和建议的行动以高效地实现预期结果。 通过展示清晰、角色驱动的路线图，AEM主页确保用户快速找到实现目标所需的内容，从而在所有AEM功能中支持更简化和更有效的体验。

早期采用者客户可以使用AEM主页来初步了解优化工作流、确定目标优先级和推动结果的增强体验。 通过选择加入，您有机会塑造AEM主页的发展，提供反馈以影响其演变，从而最好地服务AEM社区。

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com)发送电子邮件。 请务必包含以下信息：

* 最适合您个人资料的角色：内容作者、开发人员、业务负责人、管理员或其他（提供描述）。
* 您的主要AEM访问表面：AEM Sites、AEM Assets、AEM Forms、Cloud Manager或其他（提供描述）。

### 自带 Git - 现支持 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带 Git** 功能已得到扩展，包括对 GitLab 和 Bitbucket 等外部存储库的支持。这项新的支持是对专用和企业 GitHub 存储库现有支持的补充。添加这些新的存储库时，您还可以将它们直接链接到管道。您可以在公共云平台、专用云平台或基础架构中托管这些存储库。这种集成还消除了与 Adobe 存储库持续同步代码的需要，并提供了在提取请求合并到主分支之前对其进行验证的功能。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的提取请求代码质量检查仅限于 GitHub 托管的存储库，但正在计划将此功能扩展到其他 Git 供应商的更新。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)。请务必包括您要使用的Git平台，以及您使用的是专用/公共还是企业存储库结构。—>


## 错误修复

* 最近的一项更新解决了SonarQube中的一个问题：在某些情况下，无法检测到硬编码密码。 该修复现在包括扩展的模式检查，并与SonarQube中的默认检测标准保持一致。<!-- CMGR-62682 -->
* 尝试在Cloud Manager中更新SSL证书时，在&#x200B;**[!UICONTROL 查看和更新SSL证书]**&#x200B;对话框中单击&#x200B;**[!UICONTROL 更新]**&#x200B;后出现未知错误。<!-- CMGR-62848 -->
* 在Cloud Manager中，即使域相同但字母大小写（大写或小写）存在差异，SSL证书更新也会失败，并出现错误“新证书与现有域不匹配”。 该更新现在将域识别为不区分大小写，符合RFC标准。<!-- CMGR-62844 -->
* 在Cloud Manager列入允许列表中，由于缺少到域配置的外键链接，IP绑定在运行状态下仍然卡住。 现在，此修复可确保IP允许列表绑定正确链接到关联的域配置。<!-- CMGR-62838 -->
* Cloud Manager验证SSL证书的OCSP（在线证书状态协议）状态。 Adobe建议您在通过Cloud Manager安装证书之前，也使用诸如`openssl verify -untrusted intermediate.pem certificate.pem`之类的工具在本地验证证书的完整性。 有关更多详细信息，请参阅[SSL证书要求文档](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates#requirements)。<!-- CMGR-62341  -->



<!-- ## Known issues {#known-issues} -->