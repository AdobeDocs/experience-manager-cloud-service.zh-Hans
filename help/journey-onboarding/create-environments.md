---
title: 创建环境
description: 了解如何使用Cloud Manager创建您的第一个环境。
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 创建环境 {#create-environments}

在 [入门历程，](overview.md) 您将了解如何使用Cloud Manager创建您的第一个环境。

## 目标 {#objective}

阅读此入门历程中的上一个文档后， [创建程序，](create-program.md) 您现在有自己的Cloud Manager程序。 现在，您可以了解如何使用Cloud Manager为该项目创建第一个环境。

阅读本文档后，您将：

* 了解环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

## 什么是环境？ {#environments}

环境位于Cloud Manager层级中的程序下方。 虽然程序允许您组织解决方案并授予特定团队成员访问这些程序的权限，但环境属于特定程序，属于这些程序中Adobe解决方案的各个实例。 环境用于特定目的，例如创作内容或测试新开发。 Cloud Manager的CI/CD管道有助于从git存储库将代码部署到这些环境。

如果您回顾WKND旅游和冒险企业理论的例子，他们是一家以旅游相关媒体为重点的租户，他们可能有两个项目：其WKND杂志部的一个站点方案和WKND媒体部的一个资产方案。 每个计划都可能有几个环境，例如一个用于提供网站实际流量的生产环境和一个用于测试新应用程序代码的开发环境。

环境有三种类型：

* **生产和暂存**  — 生产和暂存环境可作为一对使用，并分别用于生产和测试目的。
* **开发**  — 开发环境可用于开发和测试目的，并且只能与非生产管道关联。

在此入门历程中，您将创建一个开发环境。

## 创建环境 {#creating-environments}

1. 登录Cloud Manager(位于 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 并选择相应的组织。

1. 单击要为其添加环境的程序。

1. 从 **计划概述** 页面，单击 **添加环境** 在 **环境** 卡以添加环境。

   ![环境卡](/help/implementing/cloud-manager/assets/no-environments.png)

   * 的 **添加环境** 选项 **环境** 选项卡。

      ![“环境”选项卡](/help/implementing/cloud-manager/assets/environments-tab.png)

   * 的 **添加环境** 选项可能会因缺少权限或取决于授权资源而被禁用。

1. 在 **添加环境** 对话框：

   * 选择 **环境类型**.
      * 可用/已用环境的数量显示在开发环境类型后面的括号中。
   * 提供 **环境名称**.
   * 提供 **环境描述**.
   * 选择 **云区域**.

   ![“添加环境”对话框](/help/implementing/cloud-manager/assets/add-environment2.png)

1. 单击 **保存** 添加指定的环境。

环境可用后，组织的成员即会分配到 **开发人员** 产品配置文件可以登录到Cloud Manager并管理Cloud Manager git存储库。

## 下一步 {#whats-next}

现在，您已阅读入门历程的这一部分，接下来应：

* 了解环境。
* 了解不同环境之间的差异。
* 能够创建自己的环境。

您的云资源已创建完成，可供您的团队访问。 作为系统管理员，您必须首先将您的团队成员分配给Adobe Admin Console中的AEMas a Cloud Service产品配置文件，以便他们访问这些资源。

因此，您应通过下一步审阅文档来继续入门历程 [将团队成员分配给AEMas a Cloud Service产品配置文件。](assign-profiles-aem.md)  在该文档中，您将学习如何授予团队成员访问新环境所需的权限。

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [管理环境](/help/implementing/cloud-manager/manage-environments.md)  — 了解您可以创建的环境类型以及如何为Cloud Manager项目创建环境
* [使用AdobeCloud Manager — 环境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) - Cloud Manager环境由AEM创作、发布和调度程序服务组成。 了解不同的环境如何支持角色，以及如何使用不同的CI/CD管道参与。
