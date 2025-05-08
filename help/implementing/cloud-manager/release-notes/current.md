---
title: Cloud Manager 2025.4.0 版的发行说明
description: 了解 Adobe Experience Manager as a Cloud Service 中的 Cloud Manager 2025.4.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 7ae9d2bb3cf6066d13567c54b18f21fd4b1eff9e
workflow-type: ht
source-wordcount: '614'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.4.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.4.0 版本。


另请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 2025.4.0 的发布日期是 2025 年 4 月 10 日星期四。

下一次计划发布时间为 2025 年 5 月 8 日星期四。

## 新增功能 {#what-is-new}

* **（UI）改进的部署可见性**

  当一个部署正在等待另一个部署完成时，Cloud Manager 中的管道执行详细信息页面现在会显示一条状态消息（“*等待 - 其他更新正在进行中*”）。此工作流程使得理解环境部署期间的排序变得更加容易。<!-- CMGR-66890 -->

  ![显示详细信息和细分的开发部署对话框](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **（UI）域验证增强**

  添加域时，如果域已安装在 Fastly 帐户中，Cloud Manager 现在会显示错误：“*该域已安装在 Fastly 帐户中。请先将其从那里删除，然后再添加到 Cloud Service。*”

## 早期采用计划 {#early-adoption}

参与 Cloud Manager 的早期采用计划，在即将推出的功能正式发布之前获得独家访问权。

目前有以下早期采用机会可用：

### 自带 Git：现支持 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带 Git** 功能已得到扩展，包括对 GitLab 和 Bitbucket 等外部存储库的支持。这项新的支持是对专用和企业 GitHub 存储库现有支持的补充。添加这些新的存储库时，您还可以将它们直接链接到管道。您可以在公共云平台、专用云平台或基础架构中托管这些存储库。这种集成还消除了与 Adobe 存储库持续同步代码的需要，并提供了在提取请求合并到主分支之前对其进行验证的功能。

使用外部存储库（不包括 GitHub 托管的存储库）和&#x200B;**部署触发器**&#x200B;设置为&#x200B;**在 Git 发生更改时**&#x200B;的管道现在会自动启动。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的提取请求代码质量检查仅限于 GitHub 托管的存储库，但正在计划将此功能扩展到其他 Git 供应商的更新。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

<!--
### AEM Home {#aem-home}

AEM Home introduces a centralized starting point for managing content, assets, and sites within Adobe Experience Manager. Designed to deliver a personalized experience, AEM Home lets you navigate the AEM ecosystem seamlessly according to your roles and goals. Acting as a guide, it provides key insights and recommended actions to help you achieve your objectives efficiently. With a clear, persona-driven layout, AEM Home ensures quick access to essential tools, supporting a streamlined and effective experience across all AEM features.

Available to early adopters, AEM Home offers an optimized experience focused on improving workflows, prioritizing goals, and delivering results. Opting in lets you influence AEM Home's development by providing feedback that helps shape its future and enhances its value for the entire AEM community.

If you are interested in testing this new capability and sharing your feedback, send an email to [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com) from your email address associated with your Adobe ID. Be sure to include the following information:

* The role that best fits your profile: Content author, Developer, Business owner, Admin, or Other (provide a description).
* Your primary AEM access surface: AEM Sites, AEM Assets, AEM Forms, Cloud Manager, or Other (provide a description). -->

## 错误修复

* **证书缺少通用名称 (CN) 字段的问题**

  在处理主题字段中不包含通用名称 (CN) 的 EV/OV 证书时，Cloud Manager 不再抛出 NullPointerException (NPE) 和 500 HTTP 响应。现代证书通常省略 CN，而是使用主题备用名称 (SAN)。此修复可确保当存在 SAN 时，CN 的缺失不再导致配置构建过程中出现故障。<!-- CMGR-67548 -->

* **证书匹配不正确的域验证问题**

  Cloud Manager 不再使用错误的证书错误地验证域。以前，验证逻辑使用基于模式的匹配，而不是精确匹配，这导致像 `should-not-be-verified.example.com` 由于与有效证书重叠而显示为已验证 `example.com`。此修复确保域验证现在检查完全匹配，从而防止错误的证书关联。<!-- CMGR-67225 -->

* **强制高级网络端口转发名称的唯一性**

  Cloud Manager 现在强制对高级网络端口转发进行唯一命名。以前，允许重复的名称，这可能会导致冲突。此修复确保每个端口转发条目都有一个不同的名称，符合网络配置完整性的最佳实践。<!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

