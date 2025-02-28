---
title: 创建程序
description: 了解如何使用 Cloud Manager 创建您的第一个项目。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
feature: Onboarding
source-git-commit: bd05433bb4d92a4120b19ad99d211a4a5e1f06ca
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 78%

---

# 创建项目 {#create-program}

在[加入历程](overview.md)的这一部分中，您将了解如何使用 Cloud Manager 创建第一个程序。

## 目标 {#objective}

在阅读了本次加入历程中的上一篇文档访问 [Cloud Manager](cloud-manager.md) 之后，已确保您有适当权限访问 Cloud Manager。现在，您可以创建您的第一个程序。

阅读本文档后，您将能够：

* 理解并说明什么是程序。
* 了解生产和沙盒程序之间的区别。
* 创建您自己的程序。

## 什么是程序？ {#programs}

程序是 Cloud Manager 中最高级别的组织。 根据您的 Adobe 许可证，程序允许您梳理解决方案并授予特定团队成员访问这些程序的权限。

Cloud Manager 程序代表多组 Cloud Manager 环境。这些程序支持业务计划的逻辑集，通常对应于已授予许可的服务水平协议 (SLA)。例如，一个项目可能代表 Adobe Experience Manager (AEM) 资源，用以支持组织的全球公共网站，而另一个项目代表内部中央 DAM。

以理论上的WKND Travel and Adventure Enterprises为例，这是一个专门从事旅游相关媒体业务的租户。 他们可能有两个程序。 WKND 杂志部门的一个 AEM Site 项目和 WKND 媒体部门的一个 AEM Assets 项目。由于不同的团队成员各自的分工要求，他们对不同的项目具有访问权限。

有两种不同类型的项目：

* 创建&#x200B;**生产程序**，以便为您的 Site 启用实时流量。 该项目是您的“真实”环境。
* 通常，创建&#x200B;**沙盒程序**&#x200B;是为了提供培训、运行演示、支持、概念验证 (POC) 或归档等目的。

由于用途不同，因此不同的环境有不同的选项。 但是，创建它们的过程是相似的。 对于此次加入历程，您将创建一个沙盒环境。

>[!TIP]
>
>如果您必须创建生产项目，请参阅[其他资源](#additional-resources)部分，获取详细描述项目的文档链接。

## 创建沙盒程序 {#create-sandbox}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 从 Cloud Manager 的登陆页面，单击屏幕右上角的&#x200B;**添加项目**。

   ![Cloud Manager 登陆页面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/cloud-manager-my-programs.png)

1. 从创建程序向导中，选择&#x200B;**设置沙盒**，然后提供程序名称并选择&#x200B;**继续**。

   ![项目类型创建](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

1. 在&#x200B;**设置沙盒**&#x200B;对话框中，您可以选择要在沙盒程序中启用的解决方案。 **Site** 和 **Assets** 解决方案始终包含在沙盒项目中并会自动选中。这些解决方案足以作为您的载入示例。 单击&#x200B;**创建**。

   ![解决方案选择](assets/set-up-sandbox-onboarding.png)

在安装过程中，您会在登陆页面上看到一个带有状态指示器的新沙盒程序信息卡。

![从概述页面创建沙盒](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

程序完成后，分配给&#x200B;**开发人员**&#x200B;产品配置文件的组织成员可以登录Cloud Manager并管理Cloud Manager Git存储库。

## 后续内容 {#whats-next}

创建第一个程序后，您现在即可为其创建环境。 通过进一步查看文档[创建环境](create-environments.md)来继续加入历程。

另请参阅[载入Edge Delivery Services站点](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)。

## 其他资源 {#additional-resources}

如果您想了解加入历程以外的内容，以下是额外的可选资源。

* [程序和程序类型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md) – 了解 Cloud Manager 的层级，以及不同类型的程序如何适应其结构以及它们之间的差异。
* [创建沙盒程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md) – 了解如何使用 Cloud Manager 创建自己的沙盒程序，用于培训、演示、POC 或其他非生产目的。
* [创建生产程序](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md) – 了解如何使用 Cloud Manager 创建自己的生产程序来托管实时流量。
* [使用 Adobe Cloud Manager – 程序](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/cloud-manager/programs) – 程序代表支持业务计划逻辑集的 AEM 环境集，通常与购买的服务水平协议 (SLA) 相对应。
* [AEM as a Cloud Service 团队和产品配置文件](/help/onboarding/aem-cs-team-product-profiles.md) – 了解 AEM as a Cloud Service 团队和产品配置文件如何授予和限制访问您经许可的 Adobe 解决方案。
