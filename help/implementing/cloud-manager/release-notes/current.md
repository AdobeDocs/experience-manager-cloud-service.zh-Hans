---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2025.1.0 发行。
feature: Release Information
role: Admin
source-git-commit: bf12306969581723e4e9ce1517a8f0d445f26521
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 20%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的发行说明 {#release-notes}

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.1.0 发行。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.1.0的发布日期是2025年1月22日星期三。

下一个计划发布于2025年2月13日星期四。


## 新增功能 {#what-is-new}

* **代码质量规则：** Cloud Manager代码质量步骤将开始将SonarQube Server 9.9与Cloud Manager 2025.2.0版本一起使用，该版本计划于2025年2月13日星期四发布。

为了准备，更新的SonarQube规则现在可在[代码质量规则](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)中获取。

您可以通过设置以下管道文本变量“提前检查”新规则：

`CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

此外，设置以下变量以确保为同一提交运行代码质量步骤（通常为同一`commitId`跳过）：

`CM_DISABLE_BUILD_REUSE` = `true`

![变量配置页面](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe建议创建一个新的CI/CD代码质量管道，并将其配置为与主生产管道位于同一分支。 在&#x200B;*2025年2月13日版本之前*&#x200B;设置适当的变量，以验证新的强制执行规则不会引入阻止程序。

* **Java 17和Java 21内部版本支持：**&#x200B;客户现在可以使用Java 17或Java 21进行内部版本，从而获得性能增强功能和新的语言功能。 有关配置步骤，包括更新Maven项目和库版本，请参阅[构建环境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)。 当内部版本设置为Java 17或Java 21时，部署的运行时是Java 21。

   * **功能启用**
      * 此功能将在2025年2月13日星期四为所有客户启用，同时默认推出新的SonarQube版本。
      * 客户可以通过设置上述两个变量配置来升级SonarQube 9.9版本，从而立即启用它&#x200B;**。

   * **Java 21运行时部署**
      * 使用Java 17或Java 21构建时会部署Java 21运行时。
      * Cloud Manager沙盒和开发环境的逐步推出将于2月份开始，并将在4月份扩展到生产环境。
      * 希望采用Java 21运行时&#x200B;*提前*&#x200B;的客户可通过[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)联系Adobe。


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
