---
title: Cloud Manager 2025.4.0 版的发行说明
description: 了解Adobe Experience Manager as a Cloud Service中的Cloud Manager 2025.4.0版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6d6e3e452b7910148e22d95a222c1a3b674ea83b
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 58%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.4.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.4.0 版本。


另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.4.0的发布日期是2025年4月10日星期四。

下一个计划发布于2025年5月8日星期四。

## 新增功能 {#what-is-new}

* **(UI)改进了部署可见性**

  当部署等待另一个部署完成时，Cloud Manager中的管道执行详细信息页面现在显示状态消息（“*正在等待 — 其他更新正在进行中*”）。 此工作流使环境部署期间的排序更易于理解。 <!-- CMGR-66890 -->

  ![显示详细信息和划分的开发部署对话框](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(UI)域验证增强**

  添加域时，如果该域已安装在Fastly帐户中，则Cloud Manager现在显示错误：“*该域已安装在Fastly帐户中。 请先将它从此处删除，然后再添加到Cloud Service。*”

## 早期采用计划 {#early-adoption}

参与Cloud Manager的早期采用计划，在即将发布的功能正式发布之前获得独家访问权。

目前提供以下早期采用机会：

### 自带 Git：现支持 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带 Git** 功能已得到扩展，包括对 GitLab 和 Bitbucket 等外部存储库的支持。这项新的支持是对专用和企业 GitHub 存储库现有支持的补充。添加这些新的存储库时，您还可以将它们直接链接到管道。您可以在公共云平台、专用云平台或基础架构中托管这些存储库。这种集成还消除了与 Adobe 存储库持续同步代码的需要，并提供了在提取请求合并到主分支之前对其进行验证的功能。

使用外部存储库（不包括 GitHub 托管的存储库）和&#x200B;**部署触发器**&#x200B;设置为&#x200B;**在 Git 发生更改时**&#x200B;的管道现在会自动启动。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的提取请求代码质量检查仅限于 GitHub 托管的存储库，但正在计划将此功能扩展到其他 Git 供应商的更新。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

### AEM 主页 {#aem-home}

AEM 主页为在 Adobe Experience Manager 中管理内容、资产和网站引入了一个集中的起点。AEM 主页旨在提供个性化体验，让您可以根据自己的角色和目标无缝浏览 AEM 生态系统。作为指南，它可以提供关键洞察和建议操作，帮助您高效实现目标。AEM 主页采用清晰的、以角色为导向的版面，可确保快速访问基本工具，支持简化和有效地体验 AEM 的所有功能。

AEM 主页向早期采用者提供优化的体验，专注于改善工作流、确定目标优先级和交付成果。选择加入后，您可以通过提供反馈来影响 AEM 主页的发展，从而帮助它塑造未来，提高它对整个 AEM 社区的价值。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com)。请务必包含以下信息：

* 最适合您轮廓的角色：内容作者、开发人员、业务负责人、管理员或其他（提供描述）。
* 您的主要 AEM 访问界面：AEM Sites、AEM Assets、AEM Forms、Cloud Manager 或其他（提供描述）。

## 错误修复

* **证书缺少公用名(CN)字段的问题**

  处理主题字段中不包含公用名称(CN)的EV/OV证书时，Cloud Manager不再引发NullPointerException (NPE)和500 HTTP响应。 现代证书通常省略CN，而是使用主题替代名称(SAN)。 此修复确保当存在SAN时，在配置构建过程中缺少CN不再导致故障。<!-- CMGR-67548 -->

* **与不正确的证书匹配的域验证问题**

  Cloud Manager不再使用错误的证书错误地验证域。 以前，验证逻辑使用基于模式的匹配而不是完全匹配，这会导致`should-not-be-verified.example.com`等域由于与`example.com`的有效证书重叠而显示为已验证。 此修复确保域验证现在检查完全匹配项，从而防止错误的证书关联。<!-- CMGR-67225 -->

* **高级网络端口转发名称的强制唯一性**

  Cloud Manager现在对高级网络端口转发实施唯一命名。 以前，允许使用重复的名称，这可能会导致冲突。 此修复确保每个端口转发条目都有一个不同的名称，符合网络配置完整性的最佳实践。<!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

