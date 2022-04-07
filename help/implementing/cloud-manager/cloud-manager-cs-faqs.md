---
title: Cloud Manager 常见问题解答
description: 在AEMas a Cloud Service中查找有关Cloud Manager的最常见问题的解答。
exl-id: eed148a3-4a40-4dce-bc72-c7210e8fd550
source-git-commit: 5f4bbedaa5c4630d6f955bb0986e8b32444d6aa3
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---


# Cloud Manager 常见问题解答 {#cloud-manager-faqs}

本文档提供了有关AEMas a Cloud Service中Cloud Manager的最常见问题的解答。

## 能否将Java 11与Cloud Manager内部版本结合使用？ {#java-11-cloud-manager}

是。您需要将 `maven-toolchains-plugin` ，以正确设置Java 11。

* 这已记录 [此处](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/using-the-wizard.md#getting-started).
* 例如，请参阅 [wknd项目示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75).

## 从Java 8切换到Java 11后，我的生成失败，并出现有关maven-scr-plugin的错误。 我能做什么？ {#build-fails-maven-scr-plugin}

尝试将AEM Cloud Manager内部版本从Java 8切换到11时，该内部版本可能会失败。 如果您遇到以下错误，则需要删除 `maven-scr-plugin` 并将所有OSGi批注转换为OSGi R6批注。

```text
[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]
```

有关如何删除此插件的说明，请参阅 [这里。](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)

## 从Java 8切换到Java 11后，我的生成失败，并出现有关RequireJavaVersion的错误。 我能做什么？ {#build-fails-requirejavaversion}

对于Cloud Manager内部版本， `maven-enforcer-plugin` 失败，并出现此错误。

```text
"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion".
```

这是一个已知问题，因为Cloud Manager使用不同版本的Java来运行maven命令而不是编译代码。 只是省略 `requireJavaVersion` 从 `maven-enforcer-plugin` 配置。

## 代码质量检查失败，我们的部署卡住。 有办法绕过这张支票吗？ {#deployment-stuck}

是。除安全评级之外的所有代码质量检查失败都是非关键量度，因此可以通过扩展结果UI中的项目来绕过这些失败。

查看文档 [代码质量测试](/help/implementing/cloud-manager/code-quality-testing.md) 以了解更多详细信息。

## 我能否将SNAPSHOT用于Maven项目的版本？ {#use-snapshot}

是。对于开发人员部署，请使用git分支 `pom.xml` 文件必须包含 `-SNAPSHOT` 在 `<version>` 值。

这样，当版本未发生更改时，仍然可以安装后续部署。 在开发人员部署中，不会为Maven内部版本添加或生成自动版本。

您还可以将版本设置为 `-SNAPSHOT` 用于暂存和生产内部版本或部署。 Cloud Manager会自动设置正确的版本号，并在git中为您创建一个标记。 如果需要，可以稍后引用此标记。

## 包和捆绑版本控制在暂存和生产部署中如何工作？ {#snapshot-version}

在暂存和生产部署中，自动版本将生成为 [记录在此。](/help/implementing/cloud-manager/managing-code/project-version-handling.md)

要在暂存和生产部署中进行自定义版本控制，请设置一个由三部分组成的适当版本，如 `1.0.0`. 每次部署到生产环境时，请增加该版本。

Cloud Manager会自动将其版本添加到暂存和生产内部版本并创建git分支。 无需特殊配置。 如果您没有按照之前所述设置Maven版本，部署仍将成功，并且会自动设置版本。

## 我的Maven内部版本在Cloud Manager部署中失败，但它在本地生成，并且没有错误。 怎么了？ {#maven-build-fail}

请参阅 [此git资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md) 以了解更多详细信息。

## 如果Cloud Manager部署在AEMas a Cloud Service的部署步骤中失败，我该怎么做？ {#cloud-manager-deployment-cloud-service}

部署失败的最常见原因是 `sling-distribution-importer` 用户。 在这种情况下，部署步骤在Cloud Manager部署期间失败，并生成以下错误。

```text
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10
[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item
org.apache.sling.distribution.common.DistributionException: Error processing distribution package
dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.
Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.
Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.
```

的 `sling-distribution-importer` 用户需要对 `ui.content package`.  这通常意味着您需要为这两者添加权限 `/conf` 和 `/var`.

解决方案是 [RepositoryInitializer OSGi配置](/help/implementing/deploying/overview.md#repoint) 脚本添加到应用程序部署包，以为 `sling-distribution-importer` 用户。

在上一个示例错误中，包 `myapp-base.ui.content-*.zip` 包含内容 `/conf` 和 `/var/workflow`. 为使部署成功， `sling-distribution-importer` 这些路径下需要。

以下是一个示例 [org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config) 添加 `sling-distribution-importer` 用户。  此配置将在 `/var`.  下面的此xml文件 [1] 需要添加到下的应用程序包中 `/apps/myapp/config` （其中， myapp是存储应用程序代码的文件夹）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

## 在AEMas a Cloud Service的部署步骤中，我的Cloud Manager部署失败，并且我已经拥有RepositoryInitializer OSGi配置。 我还能做什么？ {#build-failures}

如果 [添加RepositoryInitializer OSGi配置](##cloud-manager-deployment-cloud-service) 没有解决错误，可能是由于这些其他问题之一所致。

* 部署可能由于OSGi配置错误而失败，该配置会中断开箱即用的服务。
   * 在部署期间检查日志，以查看是否存在任何明显的错误。

* 部署可能因调度程序或Apache配置错误而失败。
   * 请确保使用SDK中包含的Docker图像在本地测试Apache和调度程序配置。
   * 请参阅 [云中的调度程序](/help/implementing/dispatcher/disp-overview.md#content-delivery) 关于如何设置调度程序Docker容器以便进行轻松的本地测试。

* 部署可能会因在将内容包(Sling distribution)从创作实例复制到发布实例期间出现其他一些故障而失败。
   * 按照以下步骤在本地设置中模拟问题。
      1. 使用最新的AEM SDK jar在本地安装创作和发布实例。
      1. 登录创作实例。
      1. 转到 **工具** -> **部署** -> **分发**.
      1. 分发属于代码库一部分的内容包，并查看队列是否因错误而被阻止。

## 我无法使用aio命令设置变量。 我能做什么？ {#set-variable}

您可能会收到 `403` 尝试通过列出或设置管道变量时，出现以下错误 `aio` 中。

```shell
$ aio cloudmanager:list-pipeline-variables 222

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1

Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)

$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1

setting variables... !

Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)
```

在这种情况下，执行这些命令的用户需要添加到 **部署管理** 角色。

请参阅 [API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md) 以了解更多详细信息。
