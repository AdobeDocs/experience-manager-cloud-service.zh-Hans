---
title: 创建项目
description: 了解如何使用Cloud Manager创建您的第一个项目。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 4%

---

# 创建项目 {#create-program}

在 [入门历程，](overview.md) 您将了解如何使用Cloud Manager创建您的第一个项目。

## 目标 {#objective}

在此入门历程中查看之前的文档后， [访问Cloud Manager、](cloud-manager.md) 您已确保您有权访问Cloud Manager。 现在，您可以创建您的第一个项目。

阅读本文档后，您将：

* 了解程序是什么。
* 了解制作和沙盒程序之间的差异。
* 能够创建您自己的程序。

## 什么是程序？ {#programs}

项目是Cloud Manager中组织级别最高的项目。 根据您的Adobe许可证，程序允许您组织解决方案并授予特定团队成员访问这些程序的权限。

Cloud Manager程序表示一组Cloud Manager环境。 这些计划支持逻辑上的业务计划集，通常对应于许可的服务级别协议(SLA)。 例如，一个程序可以表示AEM资源以支持组织的全局公共网站，而另一个程序则表示一个内部的中央DAM。

如果您回顾WKND旅游和冒险企业理论的例子，他们是一家以旅游相关媒体为重点的租户，他们可能有两个项目：其WKND杂志部的一个站点方案和WKND媒体部的一个资产方案。 然后，由于各自的分工要求，不同的团队成员将能够参加不同的方案。

有两种不同类型的程序：

* A **生产计划** 用于启用网站的实时流量。 这是您的“真实”环境。
* A **沙盒程序** 通常创建用于提供培训、运行演示、启用、POC或文档目的。

由于它们的用途不同，因此不同的环境具有不同的选项。 但是，创建它们的过程是相似的。 对于此入门历程，我们将创建一个沙盒环境。

>[!NOTE]
>
>默认情况下，有权访问AEM环境的用户也将具有Cloud > Manager用户角色。 此角色本身及其本身不足以授予用户访问项目详细信息视图的权限。 此类仅具有Cloud Manager用户角色的用户能够通过项目菜单选项导航到AEM环境创作URL（如果存在环境）。 如果此类用户希望获得程序级访问权限，则必须联系其管理员。

## 创建沙盒程序 {#create-sandbox}

按照以下步骤创建沙盒项目。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 从Cloud Manager的登陆页面，单击 **添加程序** 中。

   ![Cloud Manager登录页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. 从创建程序向导中，选择 **设置沙盒**，请提供项目名称，然后单击 **创建**.

   ![程序类型创建](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

随着设置过程的进行，您将在登陆页面上看到一个新的沙盒项目卡，其中包含状态指示器。

![从概述页面创建沙盒](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

项目完成后，组织的成员将分配给 **开发人员** 产品配置文件可以登录到Cloud Manager并管理Cloud Manager git存储库。

## 下一步 {#whats-next}

现在，您已创建第一个项目，接下来便可以为其创建环境。 您应该通过下一步审阅文档来继续入门历程 [创建环境。](create-environments.md)

## 其他资源 {#additional-resources}

请查看其他资源以了解：

* [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)  — 了解Cloud Manager的层级结构以及不同类型的程序如何适合其结构以及它们有何不同。
* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)  — 了解如何使用Cloud Manager创建您自己的沙盒计划，以用于培训、演示、POC或其他非生产目的。
* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)  — 了解如何使用Cloud Manager创建您自己的生产程序来托管实时流量。
* [使用Adobe云管理器 — 程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Cloud Manager计划表示支持逻辑业务计划集的AEM环境集，通常对应于购买的服务级别协议(SLA)。
