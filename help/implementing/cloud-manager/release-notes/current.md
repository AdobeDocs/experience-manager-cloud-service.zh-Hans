---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2024.10.0 发行说明。
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.10.0 版本的发行说明。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发布日期 {#release-date}

AEM as a Cloud Service 中 Cloud Manager 2023.10.0 版本的发布日期为 2024 年 10 月 3 日。

下一个版本计划于 2024 年 11 月 14 日发布。

## 新增功能 {#what-is-new}

* <!-- BOTH CS & AMS --> Cloud Manager 中使用的 AEM Archetype 版本现已更新到版本 26。请参阅 [https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> 添加新的自定义域时，以前的验证方法涉及漫长的 DNS 验证过程。Adobe 已为客户简化了这一流程。现在，您只需要提供有效的 SSL 证书（EV 或 OV）作为所有权证明。不再需要更新 DNS 中的 TXT 记录。

  >[!NOTE]
  >
  >此功能仅适用于客户管理的 EV 和 OV 证书。Adobe 管理的 DV 证书仍然需要存在 CNAME 记录。

  参见[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

  ![验证客户管理的 EV/OV 证书的域名](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> 当您添加或编辑网络基础设施时，IP 地址和网络掩码字段中的值将根据以下规则进行验证：

   * 该地址空间不能与连接地址空间中定义的地址重叠。
   * DNS 地址必须属于连接地址空间中定义的网络掩码或者是公共的。

  ![添加网络基础结构对话框](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> 正在对索引、安装可变内容和转换作业的环境部署日志的格式进行更改。

  >[!NOTE]
  >
  >该变更计划分阶段推出，预计于 2024 年 12 月完成。

  ![部署到生产卡](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  日志的格式将从如下所示的简单条目改变：

  ![显示简单条目的日志文件](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  对于如下所示的 JSON 条目：

  ![显示 json 条目的日志文件](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## 早期采用计划 {#early-adoption}

加入 Cloud Manager 早期采用计划，即有机会测试即将推出的功能。

### 自带 Git - 现支持 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带 Git** 功能已得到扩展，包括对 GitLab 和 Bitbucket 等外部存储库的支持。这项新的支持是对专用和企业 GitHub 存储库现有支持的补充。添加这些新的存储库时，您还可以将它们直接链接到管道。您可以在公共云平台、专用云平台或基础架构中托管这些存储库。这种集成还消除了与 Adobe 存储库持续同步代码的需要，并提供了在提取请求合并到主分支之前对其进行验证的功能。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的提取请求代码质量检查仅限于 GitHub 托管的存储库，但正在计划将此功能扩展到其他 Git 供应商的更新。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。


<!-- ## Bug fixes




## Known issues {#known-issues} -->
