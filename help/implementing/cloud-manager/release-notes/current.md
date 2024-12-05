---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.12.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2024.12.0 发行。
feature: Release Information
role: Admin
source-git-commit: ea1aa471a4fcb2ace6e4079715ac88af2d296e18
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.12.0 的发行说明 {#release-notes}

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2024.12.0 发行。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2024.12.0的发布日期是2024年12月5日星期四。

下一个计划发行日期为2024年1月。

## 新增功能 {#what-is-new}

* **Java 21支持：**&#x200B;客户现在可以选择使用Java 17或Java 21进行构建，从而受益于性能改进和新的语言功能。 有关配置步骤（包括更新Maven项目描述和某些库版本），请参阅[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。 当内部版本设置为Java 17或Java 21时，运行时默认为Java 21。

  从2025年2月开始，沙盒和开发环境升级到Java 21运行时，而不考虑内部版本（Java 8、11、17或21）。 生产环境随后在2025年4月进行升级。

* **已添加对A记录类型的支持：**&#x200B;以改进使用AEM Cloud Manager中的CDN配置的域的上线准备工作。 现在，您可以选择通过添加CNAME记录类型或代表Fastly的IP的A记录类型来上线，从而简化域路由。 此增强消除了仅依赖CNAME记录来使用Fastly设置域的限制。

  请参阅[添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。<!-- CMGR-63076 -->

* **将多个域添加到Edge Delivery站点：**&#x200B;您现在可以在AEM Cloud Manager中将多个域（包括Apex域和非Apex域）添加到Edge Delivery站点(EDS)。 此增强功能解决了以前的限制，即无法将多个域与EDS源关联起来。 此更新确保更灵活地管理域配置，并简化了具有复杂域设置的站点的上线流程。<!-- CMGR-63007 -->

* **高级筛选选项：**&#x200B;在AEM Cloud Manager的管道执行页面和SSL证书页面上引入了高级筛选选项。 您现在可以按多个标准进行筛选，使您能够更快地访问相关数据并提高部署效率。<!-- CMGR-26263 -->

   * **管道活动筛选：**包含管道活动筛选，可让您优化特定管道活动的搜索结果。 可用的过滤器包括管道、操作和状态。
     ![管道活动正在筛选](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **SSL证书过滤：**包括SSL证书过滤，用于优化特定证书的搜索结果。 可用的过滤器包括SSL证书名称、所有权和状态。
     ![SSL证书筛选](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## 早期采用计划 {#early-adoption}

加入 Cloud Manager 早期采用计划，即有机会测试即将推出的功能。

### 自带 Git - 现支持 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自带Git**&#x200B;功能已扩展到包括对外部存储库（如GitLab和Bitbucket）的支持。 这项新的支持是对专用和企业 GitHub 存储库现有支持的补充。添加这些新的存储库时，您还可以将它们直接链接到管道。您可以在公共云平台、专用云平台或基础架构中托管这些存储库。这种集成还消除了与 Adobe 存储库持续同步代码的需要，并提供了在提取请求合并到主分支之前对其进行验证的功能。

使用外部存储库（不包括GitHub托管的存储库）且&#x200B;**部署触发器**&#x200B;在Git更改&#x200B;**上设置为**&#x200B;的管道现在会自动启动。

请参阅[在 Cloud Manager 中添加外部存储库](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![添加“存储库”对话框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，开箱即用的提取请求代码质量检查仅限于 GitHub 托管的存储库，但正在计划将此功能扩展到其他 Git 供应商的更新。

如果您有兴趣测试此新功能并分享您的反馈，请从与您的 Adobe ID 关联的电子邮件地址发送电子邮件至 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)。请务必注明您想要使用的 Git 平台以及您是处于专用/公共还是企业存储库结构中。

## 错误修复

* 添加了阻止删除AEM Cloud Manager中具有活动域映射的域的保护措施。 尝试删除此类域的用户现在会收到一条错误消息，指示他们先删除域映射，然后再继续删除域。 此工作流可确保域完整性并防止意外配置错误。<!-- CMGR-63033 -->
* 在少数情况下，用户无法添加域名或更新SSL证书，因为各个情况中关联的状态不正确。<!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->