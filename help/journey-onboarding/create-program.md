---
title: 创建程序
description: 了解如何使用 Cloud Manager 创建您的第一个程序。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: 971ef47b66da6d7e032f6109afb4830d49c00071
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 100%

---

# 创建程序 {#create-program}

在[入门培训历程的这一可选部分中，](overview.md) 您将了解如何使用 Cloud Manager 创建第一个程序。

## 目标 {#objective}

在阅读了本次入门培训历程中的上一篇文档访问 [Cloud Manager](cloud-manager.md) 之后，已确保您有适当权限访问 Cloud Manager。现在您可以创建第一个程序。

阅读本文档后，您将：

* 了解什么是程序。
* 了解生产和沙盒程序之间的区别。
* 能够创建自己的程序。

## 什么是程序？ {#programs}

程序是 Cloud Manager 中最高级别的组织。 根据您的 Adobe 许可证，程序允许您梳理解决方案并授予特定团队成员访问这些程序的权限。

Cloud Manager 程序代表多组 Cloud Manager 环境。这些程序支持业务计划的逻辑集，通常对应于已授予许可的服务水平协议 (SLA)。例如，一个程序可能代表 AEM 资源，用以支持组织的全球公共网站，而另一个程序代表内部中央 DAM。

如果您还记得 WKND 旅游和冒险企业理论示例，一家专注于旅游相关媒体的租户，他们可能有两个程序：一个是 WKND Magazine 部门的 Sites 程序，另一个是为 WKND Media 部门的 Assets 程序。 由于不同的团队成员各自的分工要求，他们对不同的程序具有访问权限。

有两种不同类型的程序：

* 创建&#x200B;**生产程序**，以便为您的站点启用实时流量。 这是您的“真实”环境。
* 通常，创建&#x200B;**沙盒程序**&#x200B;是为了提供培训、运行演示、支持、概念验证 (POC) 或归档等目的。

由于用途不同，因此不同的环境有不同的选项。 然而，创建程序的过程是相似的。 对于此次入门培训历程，我们将创建一个沙盒环境。

>[!TIP]
>
>如果您需要创建生产程序，请参阅[其他资源](#additional-resources)部分，获取详细描述程序的文档链接。

## 创建沙盒程序 {#create-sandbox}

按照以下步骤创建沙盒程序。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 从 Cloud Manager 的登陆页面，单击屏幕右上角的&#x200B;**添加程序**。

   ![Cloud Manager 登陆页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. 在“创建程序向导”中，选择&#x200B;**设置沙盒**，提供程序名称，然后点击&#x200B;**创建**。

   ![程序类型创建](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

随着安装过程的进行，您将在登陆页面上看到一个带有状态指示器的新沙盒程序信息卡。

![从概述页面创建沙盒](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

程序创建完成后，分配给&#x200B;**开发人员**&#x200B;的组织成员可以登录 Cloud Manager 并管理 Cloud Manager git 存储库。

## 后续内容 {#whats-next}

现在您的第一个程序已经创建，您可以为该程序创建环境。 您应该通过进一步查看文档[创建环境](create-environments.md)来继续您的载入之旅。

## 其他资源 {#additional-resources}

根据其他资源了解：

* [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) – 了解 Cloud Manager 的层级，以及不同类型的程序如何适应其结构以及它们之间的差异。
* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) – 了解如何使用 Cloud Manager 创建自己的沙盒程序，用于培训、演示、POC 或其他非生产目的。
* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) – 了解如何使用 Cloud Manager 创建自己的生产程序来托管实时流量。
* [使用 Adobe Cloud Manager – 程序](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) – 程序代表支持业务计划逻辑集的 AEM 环境集，通常与购买的服务水平协议 (SLA) 相对应。
* [AEM as a Cloud Service 团队和生产简介](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品简介，以及如何授予和限制对您许可的 Adobe 解决方案的访问权限。
