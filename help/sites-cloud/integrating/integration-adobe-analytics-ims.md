---
title: 与Adobe Analytics集成时使用的IMS配置
description: 了解与Adobe Analytics集成时使用的IMS配置
source-git-commit: 7686329de2ef621f69899e07efa9af16e50a35f9
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 3%

---

# 与Adobe Analytics集成时使用的IMS配置 {#ims-configuration-for-integration-with-adobe-analytics}

要通过Analytics Standard API将Adobe Experience Manager as a Cloud Service(AEMaCS)与Adobe Analytics集成，需要配置Adobe IMS(Identity Management系统)。 配置可通过Adobe开发人员控制台实现。

>[!NOTE]
> 
>此功能在预发行渠道中提供。
>
>请参阅 [预发行渠道文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#enable-prerelease) 以了解有关如何为环境启用该功能的信息。

>[!NOTE]
>
>AEMaaCS 2022.2.0中新增了对Adobe Analytics Standard API 2.0的支持。此版本的API支持IMS身份验证。
>
>API选择由用于AEM/Analytics集成的身份验证方法驱动。
>
>详情见 [迁移到2.0 API](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/).

## 前提条件 {#prerequisites}

在开始此过程之前：

* [Adobe支持](https://helpx.adobe.com/cn/contact/enterprise-support.ec.html) 必须为您的帐户配置：

   * Adobe控制台
   * Adobe Developer Console
   * Adobe Analytics和
   * Adobe IMS(Identity Management系统)

* 贵组织的系统管理员应使用Admin Console将组织中所需的开发人员添加到相关的产品配置文件中。

   * 这为特定开发人员提供了使用Adobe开发人员控制台启用集成的权限。
   * 有关更多详细信息，请参阅 [管理开发人员](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).


## 配置IMS配置 — 生成公钥 {#configuring-ims-generating-a-public-key}

配置的第一步是在AEM中创建IMS配置并生成公钥。

1. 在AEM中，打开 **工具** 菜单。
1. 在 **安全性** 部分选择 **Adobe IMS配置**.
1. 选择 **创建** 打开 **Adobe IMS技术帐户配置**.
1. 使用下拉菜单 **云配置**，选择 **Adobe Analytics**.
1. 激活 **创建新证书** 并输入新别名。
1. 使用确认 **创建证书**.

   ![创建证书](assets/integrate-analytics-ims-01.png)

1. 选择 **下载** (或 **下载公钥**)将文件下载到本地驱动器，以便在 [为Adobe Analytics与AEM集成配置IMS](#configuring-ims-adobe-analytics-integration-with-aem).

   >[!CAUTION]
   >
   >保持此配置处于打开状态，在 [在AEM中完成IMS配置](#completing-the-ims-configuration-in-aem).

   ![下载证书](assets/integrate-analytics-ims-02.png)

## 为Adobe Analytics与AEM集成配置IMS {#configuring-ims-adobe-analytics-integration-with-aem}

使用Adobe开发人员控制台，您需要与Adobe Analytics(供AEM使用)创建项目（集成），然后分配所需的权限。

### 创建项目 {#creating-the-project}

打开Adobe开发人员控制台，以使用AEM将使用的Adobe Analytics创建项目：

1. 打开项目的Adobe开发人员控制台：

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 您所有的项目都将显示出来。 选择 **创建新项目**  — 位置和使用情况取决于：

   * 如果您还没有任何项目， **创建新项目** 中间，底部。
      ![新建项目 — 第一个项目](assets/integration-analytics-ims-02.png)
   * 如果您已经拥有现有项目，则将列出这些项目，并 **创建新项目** 右上方。
      ![创建新项目 — 多个项目](assets/integration-analytics-ims-03.png)


1. 选择 **添加到项目** 后跟 **API**:

   ![开始使用新项目](assets/integration-analytics-ims-10.png)

1. 选择 **Adobe Analytics**，则 **下一个**:

   >[!NOTE]
   >
   >如果您订阅了Adobe Analytics，但未在列表中看到它，则应查看 [先决条件](#prerequisites).

   ![添加API](assets/integration-analytics-ims-12.png)

1. 选择 **服务帐户(JWT)** 作为身份验证类型，然后继续 **下一个**:

   ![选择身份验证类型](assets/integration-analytics-ims-12a.png)

1. **上传您的公钥**，完成后，继续 **下一个**:

   ![上传您的公钥](assets/integration-analytics-ims-13.png)

1. 查看凭据，并继续 **下一个**:

   ![查看凭据](assets/integration-analytics-ims-15.png)

1. 选择所需的产品配置文件，然后继续 **保存配置的API**:

   ![选择所需的产品配置文件](assets/integration-analytics-ims-16.png)

1. 将确认配置。

### 为集成分配权限 {#assigning-privileges-to-the-integration}

您现在必须为集成分配所需的权限：

1. 打开Adobe **Admin Console**:

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. 导航到 **产品** （顶部工具栏），然后选择 **Adobe Analytics - &lt;*your-tenant-id*>** （从左侧面板）。
1. 选择 **产品配置文件**，则会从显示的列表中找到所需的工作区。 例如，默认工作区。
1. 选择 **API凭据**，则是所需的集成配置。
1. 选择 **编辑器** 作为 **产品角色**;而不是 **观察者**.

## 存储的Adobe开发人员控制台集成项目的详细信息 {#details-stored-for-the-ims-integration-project}

从Adobe开发人员控制台 — 项目中，您可以看到所有集成项目的列表：

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

选择特定项目条目以显示有关配置的更多详细信息。 这些功能包括：

* 项目概述
* 分析
* 凭据
   * 服务帐户(JWT)
      * 凭据详细信息
      * 生成JWT
* API
   * 例如，Adobe Analytics

其中一些功能需要基于IMS完成AEM中Adobe Analytics的集成。

## 在AEM中完成IMS配置 {#completing-the-ims-configuration-in-aem}

返回AEM后，您可以通过从Analytics的IMS集成添加所需值来完成IMS配置：

1. 返回到 [在AEM中打开IMS配置](#configuring-ims-generating-a-public-key).
1. 选择&#x200B;**下一步**。

1. 在此，您可以使用 [有关Adobe开发人员控制台中项目配置的详细信息](#details-stored-for-the-ims-integration-project):

   * **标题**:你的短信。
   * **授权服务器**:从 `aud` 行 **负载** ，例如 `https://ims-na1.adobelogin.com` 在以下示例中
   * **API密钥**:从 **凭据** 部分 [项目概述](#details-stored-for-the-ims-integration-project)
   * **客户端密钥**:在 [服务帐户(JWT)部分的“客户端密钥”选项卡](#details-stored-for-the-ims-integration-project)，和复制
   * **负载**:从 [生成服务帐户(JWT)部分的JWT选项卡](#details-stored-for-the-ims-integration-project)

   ![AEM IMS配置详细信息](assets/integrate-analytics-ims-10.png)

1. 选择&#x200B;**创建**&#x200B;来确认。

1. 您的Adobe Analytics配置将显示在AEM控制台中。

   ![IMS 配置](assets/integrate-analytics-ims-11.png)

## 确认IMS配置 {#confirming-the-ims-configuration}

要确认配置可按预期运行，请执行以下操作：

1. 打开：

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   例如：

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 选择您的配置。
1. 选择 **检查运行状况** ，然后 **检查**.

   ![IMS配置 — 检查运行状况](assets/integrate-analytics-ims-12.png)

1. 如果成功，您将看到一条确认消息。

## 完成与Adobe Analytics的集成 {#complete-the-integration-with-adobe-analytics}

您现在可以使用此IMS配置来完成 [与Adobe Analytics集成](/help/sites-cloud/integrating/integrating-adobe-analytics.md).

<!--
## Configuring the Adobe Analytics Cloud Service {#configuring-the-adobe-analytics-cloud-service}

The configuration can now be referenced for a Cloud Service to use the Analytics Standard API:

1. Open the **Tools** menu. Then, within the **Cloud Services** section, select **Legacy Cloud Services**.
1. Scroll down to **Adobe Analytics** and select **Configure now**.

   The **Create Configuration** dialog will open.

1. Enter a **Title** and, if you want, a **Name** (if left blank this will be generated from the title).

   You can also select the required template (if more than one is available).

1. Confirm with **Create**.

   The **Edit Component** dialog will open.

1. Enter the details in the **Analytics Settings** tab:

    * **Authentication**: IMS

    * **IMS Configuration**: select the name of the IMS Configuration

1. Click **Connect to Analytics** to initialize the connection with Adobe Analytics.

   If the connection is successful, the message **Connection successful** is displayed.

1. Select **OK** on the message.

1. Complete other parameters as required, followed by **OK** on the dialog to confirm the configuration.

1. You can now proceed to [Adding an Analytics Framework](/help/sites-administering/adobeanalytics-connect.md) to configure parameters that will be sent to Adobe Analytics. 
-->
