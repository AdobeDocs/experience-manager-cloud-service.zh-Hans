---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的发行说明
description: 了解 AEM as a Cloud Service 中的 Cloud Manager 2025.1.0 发行。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: befb092169e2278a9e84c183d342003ef325c71e
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 9%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.1.0 的发行说明 {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中的 Cloud Manager 2025.1.0 发行。

>[!NOTE]
>
>请参阅 [Adobe Experience Manager as a Cloud Service 的当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 发行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.1.0的发布日期是2025年1月22日星期三。

下一个计划发布于2025年2月13日星期四。


## 新增功能 {#what-is-new}

* **代码质量规则 — SonarQube服务器升级：** Cloud Manager代码质量步骤将开始将SonarQube Server 9.9与Cloud Manager 2025.2.0版本一起使用，该版本计划于2025年2月13日星期四发布。

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
      * 使用Java 11构建的客户希望采用Java 21运行时&#x200B;*提前*，可以通过[aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com)联系Adobe。

* **“CDN配置”已重命名为“域映射”：**&#x200B;作为AEM Cloud Manager用户界面改进的一部分，标签“CDN配置”现在已重命名为“域映射”。 此更改改进了术语与功能的协调性。<!-- CMGR-64738 -->

  ![“CDN配置”在用户界面中被重命名为“域映射”](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **通过一次单击设置Edge Delivery站点：** Cloud Manager现在允许具有相应权限和许可证的用户通过一次单击即可创建示例Edge Delivery Services站点。 这一简化的流程提供了以下自动化功能：

   * **GitHub集成** — 在现有组织中自动创建GitHub存储库，预配置了Edge Delivery Services的样板模板。
   * **AEM代码同步应用程序安装** — 在存储库上安装AEM代码同步应用程序，以确保无缝同步和部署。
   * **内容Collaboration安装程序** — 链接指定的Google Drive文件夹以进行内容存储，从而为内容管理提供协作环境。
   * **内容发布** — 用户现在可以直接从Cloud Manager用户界面发布已设置站点的内容，从而简化工作流并提高效率。
   * **增强型Collaboration** — 该平台允许用户向Google Drive内容存储文件夹添加多个协作者，从而促进团队合作和内容贡献。

  这些增强功能旨在提高自动化程度、简化设置过程并增强Edge Delivery Services用户的协作能力。<!-- CMGR-59362 -->

  ![配置Edge Delivery站点](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![设置Edge Delivery站点对话框](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **对Edge Delivery Services站点的增强支持：** Cloud Manager现在支持加入最新的Edge Delivery Services站点。 此更新包括对CDN和投放栈栈的全面重构，从而提高稳健性和可维护性。

* **早期采用者程序更新 — 对Bitbucket和GitLab的PR验证支持：** Cloud Manager现在对Bitbucket和GitLab的云版本和自托管版本都支持拉取请求(PR)验证。 通过此功能，客户可在合并PR之前根据Adobe的代码质量阈值测试其代码更改。 通过在合并之前确保较高的代码质量，此增强功能显着提高了生产管道中代码更改的成功率，从而缩短上市时间并简化开发工作流。

有关“自带Git”（现在支持GitLab和Bitbucket）以及注册为率先采用者的更多信息，请参阅[Cloud Manager 2024年10月发行说明](/help/implementing/cloud-manager/release-notes/2024/2024-10-0.md##gitlab-bitbucket)。

* **管道的高级筛选选项：** Cloud Manager现在在管道页面上提供了高级筛选选项，可让您快速访问相关数据并提高部署效率。 几项主要功能包括：

   * **多标准筛选：**&#x200B;使用管道名称、环境和部署代码等筛选条件优化搜索结果。
   * **简化的管道搜索：**&#x200B;轻松找到特定管道，以便更快导航和改进工作流管理。

  总之，这些增强功能使管道的管理和部署更加高效和用户友好。

  ![管道筛选器功能](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Edge Delivery服务的自助服务CDN配置：** Edge Delivery服务的新采用者现在可以通过Cloud Manager独立配置其CDN。 此更新将支持范围从`.hlx.page/live`扩展到新`.aem.page/live`，从而为用户提供了更大的灵活性和简化的设置。


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
