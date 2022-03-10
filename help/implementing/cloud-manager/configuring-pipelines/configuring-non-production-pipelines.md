---
title: 配置非生产管道
description: 了解如何在部署到生产环境之前配置非生产管道以测试代码质量。
index: true
exl-id: eba608eb-a19e-4bff-82ff-05860ceabe6e
source-git-commit: 428bba062fcfb44ebfbbf3c1d05ce1a4634fb429
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---

# 配置非生产管道 {#configuring-non-production-pipelines}

了解如何在部署到生产环境之前配置非生产管道以测试代码质量。

## 非生产管道 {#non-production-pipelines}

除 [生产管道](#configuring-production-pipelines.md) 它部署到暂存和生产环境，您还可以设置非生产管道来验证您的代码。

非生产管道有两种类型：

* **代码质量管道**  — 这些操作会在git分支中扫描代码，并执行生成和代码质量步骤。
* **部署管道**  — 除了执行构建和代码质量步骤（如代码质量管道）之外，这些管道还会将代码部署到非生产环境。

>[!NOTE]
>
>您可以 [编辑管道设置](managing-pipelines.md) 在初始设置之后。

## 添加新的非生产管道 {#adding-non-production-pipeline}

在您设置了程序并且使用Cloud Manager UI至少拥有一个环境后，便可以按照以下步骤添加非生产管道。

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织和程序。

1. 访问 **管道** Cloud Manager主屏幕中的信息卡。 单击 **+添加** 选择 **添加非生产管道**.

   ![添加非生产管道](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. 在 **配置** 选项卡 **添加非生产管道** 对话框中，选择要添加的非生产管道类型 **代码质量管道** 或 **部署管道**.

   ![“添加非生产管道”对话框](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-config.png)

1. 提供 **非生产管道名称** 以标识您的管道以及以下其他信息。

   * **部署触发器**  — 在定义部署触发器以启动管道时，您可以使用以下选项。

      * **手动**  — 使用此选项手动启动管道。
      * **在Git更改时**  — 只要将提交添加到配置的git分支，此选项就会启动CI/CD管道。 通过此选项，您仍可以根据需要手动启动管道。

1. 单击 **继续**.

1. 在 **源代码** 选项卡 **添加非生产管道** 对话框中，必须选择管道应处理的代码类型。

   * **[前端代码](#front-end-code)**
   * **[完整堆栈代码](#full-stack-code)**
   * **[网层配置](#web-tier-config)**

完成创建非生产管道的步骤因 **源代码** 已选择。 按照上面的链接跳转到本文档的下一部分，以完成管道的配置。

### 前端代码 {#front-end-code}

前端代码管道部署包含一个或多个客户端UI应用程序的前端代码内部版本。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 有关此类管道的详细信息。

要完成前端代码非生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **符合条件的部署环境**  — 如果您的管道是部署管道，则必须选择应将其部署到的环境。
   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。

   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
   * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。

   ![前端管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-front-end.png)

1. 单击&#x200B;**保存**。

管道已保存，您现在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **计划概述** 页面。

### 完整堆栈代码 {#full-stack-code}

全栈代码管道可同时部署包含一个或多个AEM服务器应用程序以及HTTPD/Dispatcher配置的后端和前端代码内部版本。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline) 有关此类管道的详细信息。

>[!NOTE]
>
>如果所选环境已存在全栈代码管道，则将禁用此选择。

要完成全栈代码非生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **符合条件的部署环境**  — 如果您的管道是部署管道，则必须选择应将其部署到的环境。
   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。

   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
   * **忽略网层配置** -

   ![全栈管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-full-stack.png)

1. 单击&#x200B;**保存**。

管道已保存，您现在可以 [管理管道](managing-pipelines.md) 在 **管道** 卡 **计划概述** 页面。

### 网层配置 {#web-tier-config}

Web层配置管道部署HTTPD/Dispatcher配置。 查看文档 [CI/CD管线](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#web-tier-config-pipeline) 有关此类管道的详细信息。

>[!NOTE]
>
>如果所选环境已存在Web层代码管道，则将禁用此选择。

要完成Web层代码非生产管道的配置，请执行以下步骤。

1. 在 **源代码** 选项卡，则必须定义以下选项。

   * **符合条件的部署环境**  — 如果您的管道是部署管道，则必须选择应将其部署到的环境。
   * **存储库**  — 此选项定义管道应从哪个git存储库检索代码。

   >[!TIP]
   > 
   >查看文档 [添加和管理存储库](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 了解如何在Cloud Manager中添加和管理存储库。

   * **Git分支**  — 此选项定义所选管道中的分支应从中检索代码。
   * **代码位置**  — 此选项定义选定存储库的分支中的路径，管道应从中检索代码。
      * 对于Web层配置管道，这通常是包含 `conf.d`, `conf.dispatcher.d`和 `opt-in` 目录。
      * 例如，如果项目结构是从 [AEM项目原型、](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) 路就是 `/dispatcher/src`.

   ![Web层管道](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-pipeline-web-tier.png)

1. 单击&#x200B;**保存**。

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
