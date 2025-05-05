---
title: 创建程序
description: 了解如何设置新程序和管道以部署加载项。
exl-id: 06287618-0328-40b1-bba8-84002283f23f
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: ht
source-wordcount: '688'
ht-degree: 100%

---


# 创建程序 {#creating-a-program}

了解如何设置新程序和管道以部署加载项。

## 迄今为止的故事 {#story-so-far}

在 Adobe Experience Manager (AEM) 参考演示加载项历程的上一个文档[了解参考演示加载项安装](installation.md)中，您已了解参考演示加载项安装过程的工作原理，并说明了各个部分的协作方式。现在应：

* 基本了解 Cloud Manager。
* 了解管道如何将内容和配置交付给 AEM。
* 了解如何通过单击几下来使用模板创建已预填充演示内容的 Site。

本文基于这些基础知识之上，并执行第一个配置步骤来创建程序以进行测试，并使用管道部署加载项内容。

## 目标 {#objective}

本文档有助于您了解如何设置新程序和管道以部署加载项。阅读完后，您应能够执行以下操作：

* 了解并说明如何使用 Cloud Manager 创建程序。
* 为新程序激活参考演示加载项。
* 运行管道以便部署加载项内容。

## 创建程序 {#create-program}

登录 Cloud Manager 后，您可以创建一个沙盒程序来进行测试和演示。

>[!NOTE]
>
>您的用户必须是组织的 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色成员才能创建程序。

1. 登录 Adobe Cloud Manager，网址为 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。

1. 登录后，通过在屏幕右上角查看组织，确保您在正确的组织中。如果您只是一个组织的成员，则无需执行此步骤。

   ![Cloud Manager 概述](assets/cloud-manager.png)

1. 在窗口的右上角选择&#x200B;**添加程序**。

1. 在&#x200B;**让我们创建程序**&#x200B;对话框中：

   1. 提供&#x200B;**程序名称**&#x200B;以描述您的程序。
   1. 为&#x200B;**程序目标**&#x200B;选择&#x200B;**设置沙盒**
   1. 选择&#x200B;**继续**。

   ![“创建程序”对话框](assets/create-program.png)

1. 在&#x200B;**设置沙盒**&#x200B;对话框中的&#x200B;**解决方案和加载项**&#x200B;表中，通过点击或单击列表中的 **Site** 条目以将其展开，然后选中&#x200B;**参考演示**。

   * 如果您还要为 AEM Screens 创建演示，请也选中列表中的 **Screens** 选项。选择&#x200B;**更新**。

   ![在程序设置中选择用于参考演示的附加组件](assets/select-reference-demo-add-on.png)


1. 选择&#x200B;**创建**，Cloud Manager 将开始设置沙盒程序。随后您将进入程序概述屏幕，其中有一个简短的横幅通知指示该过程已开始。一张卡片已添加到新程序的概述页面。完成该设置过程将耗时数分钟。

1. 设置完毕后，概述页面上的环境信息卡将其状态显示为&#x200B;**就绪**。选择该信息卡，以使您可打开环境。

   ![程序创建完成](assets/ready.png)

1. 您的环境准备就绪，并且现在启用了该附加组件作为一个选项，但必须将演示的内容部署到 AEM 才可用。为此，请选择&#x200B;**管道**&#x200B;信息卡中的“部署到开发”管道旁的省略号按钮，然后选择&#x200B;**运行**。

   ![启动](assets/run.png)

1. 管道将启动，并且您将进入一个详细说明部署进度的页面。您可以在创建程序的过程中退出此屏幕，并稍后返回（如有必要）。

   ![部署](assets/deployment.png)

完成该管道可能耗时数分钟。完成后，即可在 AEM 创作环境中使用加载项及其演示内容。

## 后续内容 {#what-is-next}

现在您已完成 AEM 参考演示加载项历程的这一部分，您应：

* 了解如何使用 Cloud Manager 创建程序。
* 了解如何为程序激活参考演示加载项。
* 能够运行管道以便部署加载项内容。

在此知识的基础上继续您的 AEM 参考演示加载项历程，接下来查看[创建演示 Site](create-site.md)。查看完后，您将了解如何根据管道部署的预配置模板库在 AEM 中创建演示 Site。

## 其他资源 {#additional-resources}

* [Cloud Manager 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=zh-Hans) – 如果您想了解有关 Cloud Manager 功能的更多详细信息，您可能需要直接参阅深入的技术文档。
