---
title: Cloud Manager -Cloud Services常见问题解答
seo-title: Cloud Manager常见问题解答
description: 有关Cloud Services的常见问题解答，请参阅Cloud Manager以获取一些疑难解答提示
seo-description: 可查看本页以获取有关Cloud Manager -Cloud Services常见问题解答的解答
translation-type: tm+mt
source-git-commit: 75a5ff02e5f7c0e0e3ba42c8559851d3c98c3c8d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---


# Cloud Manager常见问题解答{#cloud-manager-faqs}

以下部分为Cloud Services提供与Cloud Manager相关的常见问题解答。

## 是否可以将Java 11与Cloud Manager内部版本一起使用？{#java-11-cloud-manager}

AEM Cloud Manager在尝试将内部版本从Java 8切换到11时，生成失败。 问题可能有许多原因，最常见的原因如下：

* 按照[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/create-application-project/using-the-wizard.html?lang=en#getting-started)的说明，添加具有Java 11正确设置的maven-toolchains-plugin。  例如，请参阅[wknd示例项目代码](https://github.com/adobe/aem-guides-wknd/commit/6cb5238cb6b932735dcf91b21b0d835ae3a7fe75)。

* 如果您遇到以下错误，则需要删除`maven-scr-plugin`的使用，并将所有OSGi注释转换为OSGi R6注释。 有关说明，请参阅[此处](https://cqdump.wordpress.com/2019/01/03/from-scr-annotations-to-osgi-annotations/)。

   `[main] [ERROR] Failed to execute goal org.apache.felix:maven-scr-plugin:1.26.4:scr (generate-scr-scrdescriptor) on project helloworld.core: /build_root/build/testsite/src/main/java/com/adobe/HelloWorldServiceImpl.java : Unable to load compiled class: com.adobe.HelloWorldServiceImpl: com/adobe/HelloWorldServiceImpl has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0 -> [Help 1]`

* 对于Cloud Manager构建，maven enforcer插件失败，错误为`"[main] [WARNING] Rule 1: org.apache.maven.plugins.enforcer.RequireJavaVersion"`。 这是一个已知问题，因为Cloud Manager使用不同版本的Java运行maven命令而不是编译代码。 目前，请在maven-enforcer-plugin配置中忽略`requireJavaVersion`。

## 由于代码质量检查失败，我们的部署卡住。 有办法绕过这张支票吗？{#deployment-stuck}

除&#x200B;*安全等级*&#x200B;之外的所有代码质量故障都是非关键量度，因此可以通过扩展结果UI中的项来绕过这些故障。

具有[部署管理器、项目经理或业务所有者](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html?lang=en#requirements)角色的用户可以覆盖问题，在这种情况下，管道继续运行，或者他们可以接受问题，在这种情况下，管道会因故障而停止。  有关详细信息，请参阅[运行管线时的三层门。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#how-to-use)


## 我们是否允许在Maven项目版本中使用SNAPSHOT? 包和捆绑jar文件的版本控制如何用于Stage和Production部署？{#snapshot-version}

要了解用于Stage和Production部署的包和捆绑jar文件的版本控制，请参阅以下场景：

1. 对于开发人员部署，Git分支`pom.xml`文件必须在`<version>`值末尾包含`-SNAPSHOT`。 这样，版本未更改的后续部署仍可继续安装。 在开发人员部署中，不会为主版本添加或生成任何自动版本。

1. 在Stage和Production部署中，自动生成的版本将作为文档[此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/managing-code/activating-maven-project.html?lang=en#managing-code)生成。

1. 对于Stage和Production部署中的自定义版本控制，请设置3个部件正确的授权版本，如`1.0.0`。 每次您必须进行其他部署到生产时都增加版本。

1. Cloud Manager会自动将其版本添加到Stage和Production构建中，甚至创建Git分支。 无需特殊配置。 如果跳过上述步骤3，部署仍可正常工作，并且会自动设置一个版本。

1. 如果将版本保留在`-SNAPSHOT`中用于Stage和Production内部版本或部署，则不存在问题。 Cloud Manager会自动设置适当的版本号，并在Git中为您创建标记。 如果需要，可以稍后引用此标记。

1. 如果要在“开发”环境上尝试一些实验性代码，您可以创建一个新的Git分支并设置管道以使用该不同的分支。 当部署开始失败，并且您希望使用旧版本的代码进行测试，以查看代码何时断开时，此功能非常有用。

   下面的Git命令针对特定的预先存在的提交`485548e4fbafbc83b11c3cb12b035c9d26b6532b`创建名为&#x200B;*testbranch1*&#x200B;的远程分支。  此特殊分支可在Cloud Manager中使用，而不会影响任何其他分支：

   `git push origin 485548e4fbafbc83b11c3cb12b035c9d26b6532b:refs/heads/testbranch1`

   有关详细信息，请参阅[Git文档](https://git-scm.com/book/en/v2/Git-Internals-Git-References)。

   如果稍后要删除测试分支，则使用delete命令：

   `git push origin --delete testbranch1`

## 在Cloud Manager部署中，强制生成失败，但在本地生成时不会出错。 如何调试？{#maven-build-fail}

有关详细信息，请参阅[Git资源](https://github.com/cqsupport/cloud-manager/blob/main/cm-build-step-fails.md)。

## 在AEM中部署步骤中，如果Cloud Manager部署失败，该怎么办？{#cloud-manager-deployment-cloud-service}

部署失败的最常见原因是&#x200B;*sling-distribution-importer*用户权限不足。
请参阅以下示例，了解问题、原因和解决方案：

**问**
题在AEM上部署Cloud Manager作为Cloud Service环境时，部署步骤会失败，并会发现以下错误。

`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.jackrabbit.vault.fs.io.Importer Error while committing changes. Retrying import from checkpoint at /. Retries 4/10`
`[Queue Processor for Subscriber agent forwardPublisherSubscriber] org.apache.sling.distribution.journal.impl.subscriber DistributionSubscriber Error processing queue item`
`org.apache.sling.distribution.common.DistributionException: Error processing distribution package`
`dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 162/infinite.`
`Caused by: org.apache.sling.api.resource.PersistenceException: Unable to commit changes to session.`
`Caused by: javax.jcr.AccessDeniedException: OakAccess0000: Access denied [EventAdminAsyncThread #7] org.apache.sling.distribution.journal.impl.publisher.DistributionPublisher [null] Error processing distribution package` `dstrpck-1583514457813-c81e7751-2da6-4d00-9814-434187f08d32. Retry attempts 344/infinite. Message: Error trying to extract package at path /etc/packages/com.myapp/myapp-base.ui.content-5.1.0-SNAPSHOT.`

**原因**

sling-distribution-importer用户需要针对ui.content包中定义的内容路径获得其他权限。  这通常意味着我们需要添加/conf和/var的权限。

**解**
决方案解决方案是将RepositoryInitializer OSGi配置 [脚本](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying) 添加到您的应用程序部署包，以为sling-distribution-importer用户添加ACL。在上面的示例错误中，包myapp-base.ui.content-*.zip包含`/conf`和`/var/workflow`下的内容。 为了使部署不失败，我们需要在这些路径下添加sling-distribution-importer的权限。
以下是某个此类OSGi配置的示例[org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config](https://github.com/cqsupport/cloud-manager/blob/main/org.apache.sling.jcr.repoinit.RepositoryInitializer-distribution.config)，该配置为sling-distribution-importer用户添加了其他权限。  此配置在/var下添加权限。  [1]下的此xml文件需要添加到`/apps/myapp/config`下的应用程序包中（其中myapp是存储应用程序代码的文件夹）。
org.apache.sling.jcr.repoinit.RepositoryInitializer-DistributionService.config

1. 如果&#x200B;*sling-distribution-importer*&#x200B;不是原因，则部署可能会因OSGi配置错误而失败，因为该配置会破坏开箱服务。 在部署过程中检查日志，查看是否存在明显错误。

1. 部署可能因调度程序或apache配置错误而失败。 确保使用SDK中包含的Docker图像在本地测试Apache配置和调度程序配置。 有关如何设置调度程序Docker容器以轻松进行本地测试，请参阅Cloud](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html?lang=en#content-delivery)中的[调度程序。

1. 在从创作到发布实例的内容包(sling distribution)复制过程中，部署可能会因某些其他故障而失败。

   请参阅以下步骤以在本地设置中模拟此操作：

   * 安装作者和发布实例(使用最新的AEM SDK jar)
   * 登录到作者实例
   * 转至&#x200B;**工具** -> **部署** -> **分发**
   * 分发属于代码库的内容包，查看队列是否因错误而被阻止

## 无法通过aio cloud manager设置管道变量来设置变量。 如何调试这些问题？{#set-variable}

如果您在尝试通过类似于以下命令的命令列表或设置管道变量时遇到`403`错误，则需要在Admin Console中将您添加为&#x200B;*部署管理器*&#x200B;云管理器产品角色。\
有关详细信息，请参阅[API权限](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/permissions.md)。

相关命令和错误：

`$ aio cloudmanager:list-pipeline-variables 222`

*错误*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-pipeline-variables 222 --variable TEST 1`

*错误*:  `Cannot get variables: https://cloudmanager.adobe.io/api/program/111/pipeline/222/variables (403 Forbidden)`

`$ aio cloudmanager:set-environment-variables 1755 --variable TEST 1`

`setting variables... !`

*错误*:  `Cannot set variables: https://cloudmanager.adobe.io/api/program/111/environment/222/variables (403 Forbidden)`
