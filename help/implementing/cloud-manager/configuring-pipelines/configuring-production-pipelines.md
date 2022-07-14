---
title: 配置生产管道
description: 了解如何配置生产管道以构建代码并将其部署到生产环境。
index: true
exl-id: 67edca16-159e-469f-815e-d55cf9063aa4
source-git-commit: 13cb8ae059f0a77e517d2e64eae96a08f88ac075
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---

# 配置生产管道 {#configure-production-pipeline}

了解如何配置生产管道以构建代码并将其部署到生产环境。 生产管道首先将代码部署到暂存环境，并在获得批准后将相同的代码部署到生产环境。

用户必须具有 **[部署管理器](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** 配置生产管道的角色。

>[!NOTE]
>
>在程序创建完成、git存储库至少具有一个分支，并且创建了生产和暂存环境集之前，无法设置生产管道。

在开始部署代码之前，必须先从 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>您可以 [编辑管道设置](managing-pipelines.md) 在初始设置之后。

## 添加新的生产管道 {#adding-production-pipeline}

设置程序并使用 [!UICONTROL Cloud Manager] UI中，您可以按照以下步骤添加生产管道。

>[!TIP]
>
>在配置前端管道之前，请参阅 [AEM快速网站创建历程](/help/journey-sites/quick-site/overview.md) ，以获取易于使用的AEM快速站点创建工具的端到端指南。 此历程将帮助您简化AEM网站的前端开发，从而让您无需AEM后端知识即可快速自定义网站。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 导航到 **管道** 卡 **计划概述** 页面，单击 **添加** 选择 **添加生产管道**.

   ![项目管理器概述中的管道卡](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. 的 **添加生产管道** 对话框。 提供 **管道名称** 以标识管道以及以下选项。 单击 **继续**.

   **部署触发器**  — 在定义部署触发器以启动管道时，您可以使用以下选项。

   * **手动**  — 使用此选项手动启动管道。
   * **在Git更改时**  — 只要将提交添加到配置的git分支，此选项就会启动CI/CD管道。 通过此选项，您仍可以根据需要手动启动管道。

   **重要量度失败行为**  — 在管道设置或编辑期间， **部署管理器** 具有在任何质量门中遇到重要故障时定义管道行为的选项。 可用选项包括：

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即失败**  — 如果选中，则每当发生重要故障时，将取消管道。 这实质上是在模拟用户手动拒绝每个故障。
   * **立即继续**  — 如果选中，则每当发生重要故障时，管道将自动继续。 这实质上是在模拟用户手动批准每次失败。

   ![生产管道配置](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. 在 **源代码** 选项卡，您必须定义管道应检索其代码的位置以及代码类型。

   * **[前端代码](#front-end-code)**
   * **[完整堆栈代码](#full-stack-code)**
   * **[网层配置](#web-tier-config)**

完成创建生产管道的步骤因 **源代码** 已选择。 按照上面的链接跳转到本文档的下一部分，以完成管道的配置。

### 前端代码 {#front-end-code}

前端代码管道部署包含一个或多个客户端UI应用程序的前端代码内部版本。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 有关此类管道的详细信息。

要完成前端代码生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
      * 输入分支名称的前几个字符，此字段的自动完成功能将找到匹配的分支以帮助您选择。
   * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。
   * **部署到生产之前暂停**  — 此选项在部署到生产之前会暂停管道。

   ![前端代码](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-frontend.png)

1. 单击 **保存** 来保存管道。

管道已保存，您现在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **计划概述** 页面。

### 完整堆栈代码 {#full-stack-code}

全栈代码管道可同时部署包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置的后端和前端代码内部版本。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 有关此类管道的详细信息。

>[!NOTE]
>
>如果所选环境已存在全栈代码管道，则将禁用此选择。

要完成全栈代码生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
      * 输入分支名称的前几个字符，此字段的自动完成功能将找到匹配的分支以帮助您选择。
   * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。
   * **部署到生产之前暂停**  — 此选项在部署到生产之前会暂停管道。
   * **已计划**  — 此选项允许用户启用计划的生产部署。

   ![完整堆栈代码](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-fullstack.png)

1. 单击 **继续** 向 **体验审核** 选项卡，您可以在此定义应始终包含在体验审核中的路径。

   ![添加体验审核](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit.png)

1. 提供要包含在体验审核中的路径。

   * 页面路径必须以开头 `/`.
   * 例如，如果您希望包含 `https://wknd.site/us/en/about-us.html` 在体验审核中，输入路径 `/us/en/about-us.html`.

   ![定义体验审核的路径](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit3.png)

1. 单击 **添加页面** 并且该路径将使用您的环境地址自动完成并添加到路径表中。

   ![保存表的路径](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-audit4.png)

1. 重复前两个步骤，以根据需要继续添加路径。

   * 最多可添加25个路径。
   * 如果您未定义任何路径，则默认情况下网站的主页将包含在体验审核中。

1. 单击 **保存** 来保存管道。

为体验审核配置的路径将提交到服务，并在管道运行时根据性能、辅助功能、SEO（搜索引擎优化）、最佳实践和PWA（渐进式Web应用程序）测试进行评估。 请参阅 [了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md) 以了解更多详细信息。

管道已保存，您现在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **计划概述** 页面。

### 网层配置 {#web-tier-config}

Web层配置管道部署HTTPD/Dispatcher配置。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 有关此类管道的详细信息。

要完成全栈代码生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。
   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
      * 输入分支名称的前几个字符，此字段的自动完成功能将找到匹配的分支以帮助您选择。
   * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。
      * 对于Web层配置管道，这通常是包含 `conf.d`, `conf.dispatcher.d`和 `opt-in` 目录。
      * 例如，如果项目结构是从 [AEM项目原型、](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 路就是 `/dispatcher/src`.
   * **部署到生产之前暂停**  — 此选项在部署到生产之前会暂停管道。
   * **已计划**  — 此选项允许用户启用计划的生产部署。

   ![Web层代码](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-webtier.png)

1. 单击 **保存** 来保存管道。

>[!NOTE]
>
>如果现有的全堆栈管道部署到某个环境，则为同一环境创建Web层配置管道时，将忽略全堆栈管道中的现有Web层配置。

管道已保存，您现在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **计划概述** 页面。

## 跳过调度程序包 {#skip-dispatcher-packages}

如果您希望在管道中构建调度程序包，但不希望将它们发布到生成存储，则可以禁用发布它们，这可能会缩短管道运行持续时间。

必须通过您的项目添加以下用于禁用发布调度程序包的配置 `pom.xml` 文件。 它基于环境变量，该变量用作标记，您可以在Cloud Manager生成容器中设置该标记，以定义何时应忽略调度程序包。

```xml
<profile>
  <id>only-include-dispatcher-when-it-isnt-ignored</id>
  <activation>
    <property>
      <name>env.IGNORE_DISPATCHER_PACKAGES</name>
      <value>!true</value>
    </property>
  </activation>
  <modules>
    <module>dispatcher</module>
  </modules>
</profile>
```
