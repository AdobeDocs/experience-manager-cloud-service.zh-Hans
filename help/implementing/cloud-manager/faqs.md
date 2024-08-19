---
title: Cloud Manager 常见问题解答
description: 在 AEM as a Cloud Service 中查找有关 Cloud Manager 的最常见问题的答案。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: ht
source-wordcount: '974'
ht-degree: 100%

---


# Cloud Manager 常见问题解答 {#cloud-manager-faqs}

本文档提供有关 AEM as a Cloud Service 中 Cloud Manager 最常见问题的解答。

## 是否可以将 Java™ 11 与 Cloud Manager 构建一起使用？ {#java-11-cloud-manager}

是。添加 `maven-toolchains-plugin` 和恰当的 Java™ 11 设置。

该过程已记录 - 请参阅 [Project Creation Wizard](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started)。

有关示例，请参阅 [wknd 示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

## 从 Java™ 8 切换到 Java™ 11 后，我的构建失败，并显示一个有关 maven-scr-plugin 的错误。我该怎么办？ {#build-fails-maven-scr-plugin}

尝试将构建从 Java™ 8 切换到 Java™ 11 时，您的 AEM Cloud Manager 构建可能会失败。 如果您遇到以下错误，则需要移除 `maven-scr-plugin` 并将所有 OSGi 注释转换为 OSGi R6 注释。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 > [Help 1]
```

有关如何删除此插件的说明，请参阅 [从 SCR 注释到 OSGI 注释](https://cqdump.joerghoh.de/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

## 从 Java™ 8 切换到 Java™ 11 后，我的构建失败，并显示一个有关 RequireJavaVersion 的错误。 我该怎么办？ {#build-fails-requirejavaversion}

对于 Cloud Manager 构建，`maven-enforcer-plugin` 可能会失败，并显示此错误。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

这是一个已知问题，导致此问题的原因是 Cloud Manager 使用其他版本的 Java™ 来运行 maven 命令而不是编译代码。 只需从 `maven-enforcer-plugin` 配置中忽略 `requireJavaVersion`。

## 代码质量检查失败，并且部署出现卡滞。 是否能通过某种方式绕过此检查？ {#deployment-stuck}

是。除了安全性评级之外，所有代码质量检查故障都是非关键量度，因此，可以在部署管道中，通过扩展结果 UI 中的项目来绕过它们。

具有[部署经理、项目经理或业务负责人](/help/onboarding/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)角色的用户既可以覆盖问题，也可以接受问题，在前一种情况下，管道将继续运行，在后一种情况下，管道将停止并显示故障。

有关更多详细信息，请参阅[代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md#three-tiered-gate)和[配置非生产管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md#non-production-pipelines)。

## 我是否能将 SNAPSHOT 用于 Maven 项目版本？ {#use-snapshot}

是。对于开发人员部署，Git 分支 `pom.xml` 文件必须在 `<version>` 值的末尾包含 `-SNAPSHOT`。

在版本未更改的情况下，通过该值仍能安装后续部署。 在开发人员部署中，不会为 Maven 构建添加或生成自动版本。

您也可以为暂存和生产构建或部署将版本设置为 `-SNAPSHOT`。 Cloud Manager 会自动设置适当的版本号并在 Git 中为您创建标记。 如果需要，可以稍后参考此标记。

有关版本处理的更多详细信息，请参阅 [Maven Project 版本处理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)。

## 包和捆绑包版本控制如何用于阶段和生产部署？ {#snapshot-version}

在阶段和生产部署中，会生成一个自动版本 - 请参阅 [Maven Project 版本处理](/help/implementing/cloud-manager/managing-code/project-version-handling.md)。

对于暂存和生产部署中的自定义版本控制，请设置适当的三部分 maven 版本，如 `1.0.0`。 每次部署到生产环境时提高版本。

Cloud Manager 自动将其版本添加到暂存和生产构建，并创建 Git 分支。 无需特殊配置。 如果您未如前所述设置 maven 版本，部署仍会成功，并且会自动设置版本。

## 虽然在 Cloud Manager 部署中，我的 maven 构建失败，但它会在本地构建，并且不会产生错误。 有什么问题吗？ {#maven-build-fail}

有关更多详细信息，请参阅此 [Git 资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 如果 Cloud Manager 部署在 AEM as a Cloud Service 的部署步骤失败，我该怎么办？ {#cloud-manager-deployment-cloud-service}

部署失败的最常见原因是 `sling-distribution-importer` 用户权限不足。 在这种情况下，部署步骤在 Cloud Manager 部署期间失败，并导致以下错误。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

`sling-distribution-importer` 用户需要对 `ui.content package` 中定义的内容路径拥有附加权限。  该规则通常意味着您必须为 `/conf` 和 `/var`添加权限。

解决方案是向应用程序部署包中添加 [RepositoryInitializer OSGi 配置](/help/implementing/deploying/overview.md#repoint)脚本，为 `sling-distribution-importer` 用户添加 ACL。

在前面的示例错误中，包 `myapp-base.ui.content-*.zip` 包括 `/conf` 和 `/var/workflow` 下的内容。 为了成功部署，需要这些路径下的 `sling-distribution-importer` 的权限。

以下是 [`org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config`](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) OSGi 配置的示例，该配置为 `sling-distribution-importer` 用户添加附加权限。  该配置在 `/var` 下添加权限。  此类配置必须添加到 `/apps/myapp/config`（其中 myapp 是存储应用程序代码的文件夹）下的应用程序包中。

## 我的 Cloud Manager 部署在 AEM as a Cloud Service 的部署步骤失败，而且我已经添加了 RepositoryInitializer OSGi 配置。我还能做什么？ {#build-failures}

如果[添加 RepositoryInitializer OSGi 配置](#cloud-manager-deployment-cloud-service)并未修复错误，则可能是由于这些附加问题之一。

* 部署可能失败，因为 OSGi 配置不正确，中断了现成的服务。
   * 在部署期间检查日志，查看是否存在任何明显错误。

* 由于 Dispatcher 或 Apache 配置不正确，部署可能会失败。
   * 确保使用 SDK 中包含的 Docker 映像在本地测试 Apache 和 Dispatcher 配置。
   * 请参阅[云中 Dispatcher](/help/implementing/dispatcher/disp-overview.md#content-delivery)，了解如何设置 Dispatcher Docker 容器可促进本地测试。

* 在将内容包（Sling 分发）从作者复制到发布实例的过程中，由于其他一些故障，部署可能会失败。
   * 按照以下步骤在本地设置上模拟问题。
      1. 使用最新的 AEM SDK jar 在本地安装作者和发布实例。
      1. 登录作者实例。
      1. 转至&#x200B;**工具** > **部署** > **分发**。
      1. 分发作为代码库一部分的内容包，并查看队列是否因错误而阻塞。

## 我无法使用 aio 命令设置变量。 我该怎么办？ {#set-variable}

在尝试通过 `aio` 命令列出或设置管道变量时，您可能会收到如下所示的 `403` 错误。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在此情况下，必须在 Admin Console 中将运行这些命令的用户添加到&#x200B;**部署经理**&#x200B;角色。

有关更多详细信息，请参阅 [API 权限](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/permissions/)。
