---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.2.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2025.2.0 版本。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aaef376b733c10643e44205e55a0921c22008990
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 15%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.2.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.2.0 版本。


另请参阅[当前的Adobe Experience Manager as a Cloud Service发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中Cloud Manager 2025.2.0的发布日期是2025年2月13日星期四。

下一个计划发布于2025年3月13日星期四。

## 新增功能 {#what-is-new}

* **更新代码质量规则**

  从2025年2月13日星期四开始，Cloud Manager代码质量步骤现在使用SonarQube 9.9.5.90363。

  更新后的规则适用于AEM as a Cloud Service上的Cloud Manager，位于[此链接](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)，这些规则确定Cloud Manager管道的安全分数和代码质量。

* SonarQube 9.9现在是所有客户的默认代码质量扫描引擎。

* **Java 17和Java 21内部版本支持**

  客户现在可以使用Java 17或Java 21进行构建，从而访问性能增强功能和新的语言功能。 有关配置步骤（包括更新 Maven 项目和库版本），请参阅[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。当构建版本设置为 Java 17 或 Java 21 时，部署的运行时为 Java 21。

* Edge Delivery Services的&#x200B;**99.99% SLA正常运行时间报告**

  高可用性99.99%的正常运行时间报告现在可用于符合条件的Edge Delivery Services计划。 要启用此功能，客户必须成功载入其Edge Delivery Services站点，并在Cloud Manager中应用其99.99%的Service level agreement (SLA)。

  另请参阅[SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)。

* **改进了Edge Delivery Services的用户邀请体验**

  邀请用户访问与Edge Delivery Services关联的内容存储库的体验得到了改进。<!-- CMGR-65331 -->

* **在发布实例上自动创建管理员配置文件**

  以前，Cloud Manager允许在发布实例上手动创建管理员配置文件，但默认情况下不支持自动创建。 通过此更新，现在可在发布实例上自动创建管理员配置文件，从而提高可用性并缩短客户的设置时间。

  有关详细信息，请参阅[自定义权限](/help/implementing/cloud-manager/custom-permissions.md)。

  ![管道活动筛选](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **过渡到Cloud Service环境的OAuth**

  新的Cloud Service环境现在为Adobe Developer Console集成项目使用基于OAuth的服务到服务身份验证，而不是以前使用的JWT身份验证方法。 JWT身份验证已弃用，计划于2025年6月结束生命周期。

* **支持EC（椭圆曲线）私钥(secp384r1)**

  Cloud Manager现在支持`secp384r1`椭圆曲线(EC)私钥，从而改进了客户管理的OV/EV SSL证书的安全性和合规性。
有关更多详细信息，请参阅[客户管理的OV/EV SSL证书的要求](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)。<!-- CMGR-63636 -->

* **专门的测试环境**

  2025年2月27日起，率先采用者将获得资源增强的新开发环境。


<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## 错误修复

* **(UI)修复了阻止在Cloud Manager中配置域的CDN的问题。**
尝试在Cloud Manager中添加CDN配置的客户在从下拉菜单中选择域时遇到了屏幕错误。 此用户界面错误会阻止在生产环境中进行域映射，从而阻止配置过程。

  此外，尽管从用户界面中删除了某些域，但这些域在后端仍无法访问。 此问题会导致与现有CDN配置冲突。

  通过此修复，您现在可以从下拉列表中成功选择域，而不会遇到错误。 解决了阻止重新配置域的后端不一致问题。 最后，改进的验证现在可确保冲突域在重新添加之前被正确删除。<!-- CMGR-64888 -->
* **（后端）修复了导致多次发送SSL到期通知的问题。**
已识别出以下错误：SSL到期通知计划程序设计为在午夜每天运行一次，但在午夜错误地触发了每天两次，在上午12:30再次触发。 此问题导致发送多个有关过期SSL证书的冗余通知。

  现在，通知计划程序每天只能按预期正确运行一次。 并且，您不会再收到重复的SSL到期通知。<!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
