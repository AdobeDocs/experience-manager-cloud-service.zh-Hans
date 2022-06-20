---
title: 创建项目
description: 了解如何设置新项目和管道以部署加载项。
exl-id: 06287618-0328-40b1-bba8-84002283f23f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: ht
source-wordcount: '715'
ht-degree: 100%

---

# 创建项目 {#creating-a-program}

了解如何设置新项目和管道以部署加载项。

## 迄今为止的故事 {#story-so-far}

在 AEM 参考演示加载项历程的上一个文档[了解参考演示加载项安装](installation.md)中，您已了解参考演示加载项安装过程的工作原理，并说明了各个部分的协作方式。您现在应：

* 基本了解 Cloud Manager。
* 了解管道如何将内容和配置交付给 AEM。
* 了解如何通过单击几下来使用模板创建已预填充演示内容的新站点。

本文基于这些基础知识之上，并执行第一个配置步骤来创建项目以进行测试，并使用管道部署加载项内容。

## 目标 {#objective}

本文档有助于您了解如何设置新项目和管道以部署加载项。阅读本文档后，您应：

* 了解如何使用 Cloud Manager 创建新项目。
* 了解如何为新项目激活参考演示加载项。
* 能够运行管道以部署加载项内容。

## 创建项目 {#create-program}

登录 Cloud Manager 后，您可以创建一个新的沙盒项目来进行测试和演示。

>[!NOTE]
>
>您的用户必须是组织的 Cloud Manager 中的&#x200B;**业务负责人**&#x200B;角色的成员才能创建项目。

1. 登录 Adobe Cloud Manager，网址为 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。

1. 登录后，通过在屏幕右上角查看组织，确保您在正确的组织中。如果您只是一个组织的成员，则无需执行此步骤。

   ![Cloud Manager 概述](assets/cloud-manager.png)

1. 点按或单击窗口右上方的&#x200B;**添加项目**。

1. 在&#x200B;**让我们创建项目**&#x200B;对话框中，确保选中&#x200B;**产品**&#x200B;下的 **Adobe Experience Manager**，然后点按或单击&#x200B;**继续**。

   ![“创建项目”对话框](assets/create-program.png)

1. 在下一个对话框中：

   * 提供&#x200B;**项目名称**&#x200B;以描述您的项目。
   * 为&#x200B;**项目目标**&#x200B;点按或单击&#x200B;**设置沙盒**

   点按或单击&#x200B;**创建**。

   ![项目名称](assets/program-name.png)

1. 您将进入项目概述屏幕，可以在其中观察项目的创建过程。Cloud Manager 提供了剩余时间估计值。您可以在创建项目的过程中退出此屏幕，并稍后返回（如有必要）。

   ![项目创建](assets/program-creation.png)

1. 完成后，Cloud Manager 会提供一个概览，包括自动创建的环境和管道。

   ![项目创建完成](assets/creation-complete.png)

1. 通过单击页面左上方的项目名称来编辑项目详细信息，然后在下拉列表中，选择&#x200B;**编辑项目**。

   ![编辑项目](assets/edit-program.png)

1. 在&#x200B;**编辑项目**&#x200B;对话框中，切换到&#x200B;**解决方案和加载项**&#x200B;选项卡。

   ![“编辑项目”对话框](assets/edit-program-dialog.png)

1. 在&#x200B;**解决方案和加载项**&#x200B;选项卡上，展开列表中的 **Sites** 条目，然后选中&#x200B;**参考演示**。如果您还想为 AEM Screens 创建演示，请也选中列表中的 **Screens** 选项。点按或单击&#x200B;**更新**。

   ![选中参考演示选项](assets/edit-program-add-on.png)

1. 虽然该加载项现已作为选项启用，但其内容必须部署到 AEM 才可用。返回项目概述页面，点按或单击&#x200B;**启动**，启动管道并将加载项内容部署到 AEM。

   ![启动](assets/deploy.png)

1. 管道将启动，并且您将进入一个详细说明部署进度的页面。您可以在创建项目的过程中退出此屏幕，并稍后返回（如有必要）。

   ![部署](assets/deployment.png)

管道完成后，即可在 AEM 创作环境中使用加载项及其演示内容。

## 下一步 {#what-is-next}

现在您已完成 AEM 参考演示加载项历程的这一部分，您应：

* 了解如何使用 Cloud Manager 创建新项目。
* 了解如何为新项目激活参考演示加载项。
* 能够运行管道以部署加载项内容。

在此知识的基础上继续您的 AEM 参考演示加载项历程，接下来查看文档[创建演示站点](create-site.md)，了解如何基于管道所部署的预配置模板库在 AEM 中创建演示站点。

## 其他资源 {#additional-resources}

* [Cloud Manager 文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) – 如果您想了解有关 Cloud Manager 功能的更多详细信息，您可能需要直接参阅深入的技术文档。
