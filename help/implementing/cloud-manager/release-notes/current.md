---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的发行说明
description: 了解AEM as a Cloud Service中Cloud Manager 2024.10.0的发行说明。
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 12%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的发行说明 {#release-notes}

本页记载 AEM as a Cloud Service 中 Cloud Manager 2024.10.0 版本的发行说明。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发布日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.10.0版的发布日期是2024年10月3日。

下一个版本计划于2024年11月14日发布。

## 新增功能 {#what-is-new}

* <!-- BOTH CS & AMS --> Cloud Manager中使用的AEM原型版本现已更新到版本26。 请参阅[https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> 添加新的自定义域时，以前的验证方法涉及漫长的DNS验证过程。 Adobe为客户简化了此过程。 现在，您只需要提供有效的SSL证书（EV或OV），用作所有权证明。 不再需要更新DNS中的TXT记录。

  >[!NOTE]
  >
  >此功能仅适用于客户管理的EV和OV证书。 由Adobe管理的DV证书仍要求存在CNAME记录。

  请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

  ![验证客户管理的EV/OV证书的域](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> 添加或编辑网络基础架构时，将根据以下规则验证IP地址和网络掩码字段中的值：

   * 地址空间不得与连接地址空间中定义的地址重叠。
   * DNS地址必须属于连接地址空间中定义的网络掩码或公用。

  ![添加网络基础结构对话框](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> 正在更改用于编制索引、安装可变内容和转换作业的环境部署日志的格式。

  >[!NOTE]
  >
  >这项变更计划分阶段推出，预计完成日期为2024年12月。

  ![部署到生产卡](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  日志的格式将从以下所示的简单条目更改：

  ![显示简单条目的日志文件](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  到下面所示的JSON条目：

  ![日志文件，显示json条目](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## 早期采用计划 {#early-adoption}

加入Cloud Manager的早期采用计划，并有机会测试即将推出的功能。

### 自带Git — 现在支持GitLab和Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带Git**&#x200B;功能已扩展到包括对GitLab和Bitbucket等外部存储库的支持。 此新支持是对专用和企业GitHub存储库的现有支持之外的支持。 添加这些新存储库时，您还可以将其直接链接到管道。 您可以在公共云平台上或私有云或基础架构内托管这些存储库。 此集成还消除了对与Adobe存储库进行持续代码同步的需求，并提供了在合并到主分支之前验证拉取请求的功能。

请参阅[在Cloud Manager中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的拉取请求代码质量检查专供GitHub托管的存储库使用，但正在研究如何将此功能扩展到其他Git供应商。

如果您有兴趣测试这项新功能并分享您的反馈，请从与Adobe ID关联的电子邮件地址向[Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)发送电子邮件。 请务必包括您要使用的Git平台，以及您使用的是专用/公共还是企业存储库结构。


<!-- ## Bug fixes




## Known issues {#known-issues} -->
