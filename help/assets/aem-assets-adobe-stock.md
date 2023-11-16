---
title: 管理 [!DNL Adobe Stock] 中的资产 [!DNL Assets].
description: 搜索、获取、许可和管理 [!DNL Adobe Stock] 中的资产 [!DNL Adobe Experience Manager]. 将许可资产用作任何其他数字资产。
contentOwner: Vishabh Gupta
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 8%

---

# 使用 [!DNL Adobe Stock] 中的资产 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/aem-assets-adobe-stock.html?lang=en) |
| AEM as a Cloud Service | 本文 |

[!DNL Adobe Stock] 通过此服务，设计人员和企业可为其所有创意项目访问数百万张高质量、精选且免版税的照片、矢量、插图、视频、模板和3D资产。

[!DNL Adobe Stock] 默认情况下，企业产品包括在组织内共享权限。 资产获得组织用户的许可后，组织的其他用户便可以识别、下载和使用此资产，而无需再次许可。 一旦您的组织对资产进行了许可，该资产的使用权即永久有效。

组织可以集成其企业 [!DNL Adobe Stock] 计划 [!DNL Experience Manager Assets] 利用的强大资产管理功能，确保许可资产可广泛用于其创意和营销项目。 [!DNL Experience Manager]. [!DNL Experience Manager] 用户可以快速查找、预览和许可保存在中的Adobe Stock资源 [!DNL Experience Manager]，而不离开 [!DNL Experience Manager] 界面。

## 集成 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] 允许用户搜索、预览、保存和许可 [!DNL Adobe Stock] 资产直接来自 [!DNL Experience Manager].

**前提条件**

集成需要：

* 启动并运行 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 实例
* An [企业 [!DNL Adobe Stock] 计划](https://stockenterprise.adobe.com/)
* 具有默认Stock产品配置文件Admin Console权限的用户
* 在Adobe Developer Console中拥有用于创建集成的开发人员访问配置文件权限的用户

企业 [!DNL Adobe Stock] 计划，

* 提供产品权利 [!DNL Adobe Stock] (与Experience Manager相关的股票)
* 购买到的积分 [!DNL Adobe Admin Console] 您股票权益的
* 在中启用服务帐户(JWT)身份验证 [!DNL Adobe Developer Console] 您股票权益的
* 支持从内部全局管理信用和许可 [!DNL Adobe Admin Console]

在该权利中，默认产品配置文件 [!DNL Adobe Stock] 存在于 [!DNL Admin Console]. 可以创建多个配置文件，这些配置文件确定谁可以许可Stock资产。 对产品配置文件具有直接访问权限的用户可以访问 [https://stock.adobe.com/](https://stock.adobe.com/) 并许可Stock资产。 而则可以使用开发人员访问权限创建集成(API)的其他方法。 此集成验证与 [!DNL Experience Manager Assets] 和 [!DNL Adobe Stock].

>[!NOTE]
>
>Stock服务帐户(JWT)身份验证随企业Stock权利提供。
>
>该集成不支持企业股票权利的Oauth身份验证。


<!--
### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->
<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in User Preferences panel. To access the panel from Experience Manager home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.

-->

## 集成步骤 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integration-steps}

要集成 [!DNL Experience Manager] 和 [!DNL Adobe Stock]，请按列出的顺序执行以下步骤：

1. [获取公共证书](#public-certificate)

   在 [!DNL Experience Manager]，创建IMS帐户并生成公共证书（公共密钥）。

1. [创建服务帐户(JWT)连接](#createnewintegration)

   在 [!DNL Adobe Developer Console]，为您的创建一个项目 [!DNL Adobe Stock] 组织。 在项目下，使用公钥配置API以创建服务帐户(JWT)连接。 获取服务帐户凭据和JWT有效负载信息。

1. [配置IMS帐户](#create-ims-account-configuration)

   在 [!DNL Experience Manager]，使用服务帐户凭据和JWT有效负载配置IMS帐户。

1. [配置云服务](#configure-the-cloud-service)

   在 [!DNL Experience Manager]，配置 [!DNL Adobe Stock] 使用IMS帐户的云服务。


### 创建IMS配置 {#create-an-ims-configuration}

IMS配置对您的进行身份验证 [!DNL Experience Manager Assets] 使用的创作实例 [!DNL Adobe Stock] 权利。

IMS 配置包括两个步骤：

* [获取公共证书](#public-certificate)
* [配置IMS帐户](#create-ims-account-configuration)

### 获取公共证书 {#public-certificate}

公钥（证书）用于在Adobe Developer控制台中验证您的产品配置文件。

1. 登录 [!DNL Experience Manager Assets] 云实例。

1. 从 **[!UICONTROL 工具]** 面板，导航到 **[!UICONTROL 安全性]** > **[!UICONTROL Adobe IMS配置]**.

1. 在“Adobe IMS配置”页面中，单击 **[!UICONTROL 创建]**. 此 **[!UICONTROL Adobe IMS技术帐户配置]** 页面将打开。

1. 在 **[!UICONTROL 证书]** 选项卡，选择 **[!UICONTROL Adobe Stock]** 从 **[!UICONTROL 云解决方案]** 下拉列表。

1. 您可以创建证书或为配置重用现有证书。

   要创建证书，请选择 **[!UICONTROL 创建新证书]** 复选框，并指定 **别名** 用于公共密钥。 别名将用作公钥的名称。

1. 单击&#x200B;**[!UICONTROL 创建证书]**。然后，单击 **[!UICONTROL 确定]** 以生成公钥。

1. 单击 **[!UICONTROL 下载公钥]** 图标并将公钥(.crt)文件保存在计算机上。 公钥稍后用于为Brand Portal租户配置API并在Adobe Developer控制台中生成服务帐户凭据。

   单击&#x200B;**[!UICONTROL 下一步]**。

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. 在 **帐户** 选项卡，将创建Adobe IMS帐户，这需要服务帐户凭据。

   打开新选项卡并 [在Adobe Developer控制台中创建服务帐户(JWT)连接](#createnewintegration).

### 创建服务帐户(JWT)连接 {#createnewintegration}

在Adobe Developer控制台中，项目和API在组织级别进行配置。 配置API将创建服务帐户(JWT)连接。 配置API的方法有两种：生成密钥对（私钥和公钥）或上传公钥。 在此示例中，服务帐户凭据是通过上传公钥生成的。

要生成服务帐户凭据和JWT有效负载，请执行以下操作：

1. 使用系统管理员权限登录到Adobe Developer控制台。 默认URL为 [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   确保您从下拉列表（组织）中选择了正确的IMS组织（库存权利）。

1. 单击 **[!UICONTROL 创建新项目]**. 系统会为您的组织创建一个名称由系统生成的空白项目。

   单击 **[!UICONTROL 编辑项目]**. 更新 **[!UICONTROL 项目标题]** 和 **[!UICONTROL 描述]**，然后单击 **[!UICONTROL 保存]**.

1. 在 **[!UICONTROL 项目概述]** 选项卡，单击 **[!UICONTROL 添加API]**.

1. 在 **[!UICONTROL 添加API窗口]**，选择 **[!UICONTROL Adobe Stock]**. 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 配置API]** 窗口，选择 **[!UICONTROL 服务帐户(JWT)]** 身份验证。 单击&#x200B;**[!UICONTROL 下一步]**。

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. 单击 **[!UICONTROL 上传公钥]**. 单击 **[!UICONTROL 选择文件]** 并上传您在中下载的公共密钥（.crt文件） [获取公共证书](#public-certificate) 部分。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 验证公钥并单击 **[!UICONTROL 下一个]**.

1. 选择默认值 **[!UICONTROL Adobe Stock]** 产品配置文件并单击 **[!UICONTROL 保存配置的API]**.

1. 配置API后，您将被重定向到API概述页面。 从左侧导航栏中的 **[!UICONTROL 凭据]**，单击 **[!UICONTROL 服务帐户(JWT)]** 选项。 在这里，您可以查看凭据并执行操作，如生成JWT令牌、复制凭据详细信息和检索客户端密码。

1. 从 **[!UICONTROL 客户端凭据]** 选项卡，复制 **[!UICONTROL 客户端ID]**.

   单击 **[!UICONTROL 检索客户端密码]** 并复制 **[!UICONTROL 客户端密码]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. 导航至 **[!UICONTROL 生成JWT]** 制表并复制 **[!UICONTROL JWT有效负荷]** 信息。

您现在可以将客户端ID（API密钥）、客户端密钥和JWT有效负载用于 [配置IMS帐户](#create-ims-account-configuration) 在 [!DNL Experience Manager Assets].

### 配置IMS帐户 {#create-ims-account-configuration}

您必须拥有 [证书](#public-certificate) 和 [服务帐户(JWT)凭据](#createnewintegration) 配置IMS帐户。

配置IMS帐户：

1. 打开IMS配置并导航到 **[!UICONTROL 帐户]** 选项卡。 你保持页面打开 [获取公共证书](#public-certificate).

1. 为 IMS 帐户指定&#x200B;**[!UICONTROL 标题]**。

   在 **[!UICONTROL 授权服务器]** 字段中，输入URL： [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   在中输入客户端ID **[!UICONTROL API密钥]** 字段， **[!UICONTROL 客户端密码]**、和 **[!UICONTROL 有效负荷]** （JWT有效负荷）您已复制的时间 [创建服务帐户(JWT)连接](#createnewintegration).

1. 单击&#x200B;**[!UICONTROL 创建]**。将创建IMS帐户配置。

   ![configure-ims-account](assets/aem-stock-ims-config.png)

1. 选择IMS帐户配置并单击 **[!UICONTROL 检查运行状况]**.

   单击 **[!UICONTROL Check]** 对话框中。 成功配置时，将显示一条消息： *已成功检索令牌*.

   ![运行状况检查](assets/aem-stock-healthcheck.png)


### 配置云服务 {#configure-the-cloud-service}

配置 [!DNL Adobe Stock] 云服务：

1. 在 [!DNL Experience Manager] 用户界面，导航至 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**.

1. 在 [!DNL Adobe Stock Configurations] 页面，单击 **[!UICONTROL 创建]**.

1. 指定 **[!UICONTROL 标题]** 用于云配置。

   选择您已在以下时间创建的IMS配置： [配置IMS帐户](#create-ims-account-configuration).

   从下拉列表中选择您的区域设置。

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. 单击“**[!UICONTROL 保存并关闭]**”。

   您的 [!DNL Experience Manager Assets] 创作实例现已与集成 [!DNL Adobe Stock]. 您可以创建多个 [!DNL Adobe Stock] 配置（例如，基于区域设置的配置）。 您现在可以访问、搜索和许可 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager] 用户界面。

   ![search-stock-assets](assets/aem-stock-searchstocks.png)

   >[!NOTE]
   >
   >在集成的此阶段，只有管理员才能访问 [!DNL Adobe Stock] 资产，搜索Stock资产（使用Omnisearch），并许可 [!DNL Adobe Stock] 资产。
   >
   >管理员可以将用户或组进一步添加到 [!DNL Adobe Stock] cloud service并将权限授予中的这些非管理员用户 [!DNL Experience Manager] 以访问Stock配置。

1. 要添加用户或组，请选择 [!DNL Adobe Stock] 云配置并单击 **[!UICONTROL 属性]**.

1. 搜索以添加您为其分配了访问Adobe Stock配置的权限的用户或组。 请参阅 [向用户组分配权限](#assign-permissions-to-group).


## 向用户组分配权限 {#assign-permissions-to-group}

管理员可以创建用户组，并将权限授予特定用户或组，以访问 [!DNL Adobe Stock] 云服务。

以下是用户搜索和许可Adobe Stock资源所需的权限：

* 配置路径： `/conf/global/settings/stock`
* 特权: `jcr:read`
* 权限类型: `Allow`

您可以创建用户组或向现有用户组分配权限。 可以从以下位置分配权限 [!DNL Experience Manager Assets] 界面或从 [!DNL User Admin] 控制台。

**要提供对用户组的访问权限，请执行以下操作： [!DNL Experience Manager]：**

1. 在 [!DNL Experience Manager] 用户界面，导航至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 组]**. 创建用户组 [!DNL Adobe Stock].

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 权限]**.

1. 在左侧面板中搜索用户组并新增 **[!UICONTROL 访问控制条目(ACE)]** 用于Adobe Stock。

   * 配置路径： `/conf/global/settings/stock`
   * 特权: `jcr:read`
   * 权限类型: `Allow`

   单击&#x200B;**[!UICONTROL 添加]**。

   ![user-permissions](assets/aem-stock-user-permissions.png)

1. 导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Stock]**. 选择 [!DNL Adobe Stock] 云配置并单击 **[!UICONTROL 属性]**.

1. 将新创建的用户组添加到 [!DNL Adobe Stock] 配置。 单击“**[!UICONTROL 保存并关闭]**”。

   ![assign-user](assets/aem-stock-adduser.png)

**要提供对用户的访问权限，请执行以下操作： [!DNL User Admin Console]：**

1. 打开 [!DNL Experience Manager] 用户Admin Console。 默认URL为 `http://localhost:4502/userdamin`.

1. 在左侧面板中，通过输入 `user_id` 或 `name`. 双击以打开用户属性。

1. 导航至 **[!UICONTROL 权限]** 制表符并允许 `read` 的权限 [!DNL Adobe Stock] 云配置： `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >如果不允许云配置，则用户只能访问 **[!UICONTROL 资产]** 在 [!DNL Experience Manager] 界面。
   >
   >要允许访问 [!UICONTROL 资产] 和 [!DNL Adobe Stock] 资源，确保用户允许云配置。

1. 单击 **[!UICONTROL 保存]** 以更新权限。

   ![assign-user-in-user-admin](assets/aem-stock-user-admin-console.png)

1. 将用户或组添加到 [!DNL Adobe Stock] 云配置。


## 访问Adobe Stock资源 {#access-stock-assets}

非管理员用户具有对的权限 [!DNL Adobe Stock] 云配置可以搜索并许可 [!DNL Adobe Stock] 来自以下各项的资产： [!DNL Experience Manager] 界面。

用户必须执行额外的步骤来激活 [!DNL Adobe Stock] 访问之前的云配置 [!DNL Adobe Stock] 资产。 这是一次性活动。 如果用户被分配了多个权限 [!DNL Adobe Stock] 云配置中，用户可以从中选择所需的配置 **[!UICONTROL 用户首选项]**.

激活 [!DNL Adobe Stock] 云配置：

1. 登录 [!DNL Experience Manager].

1. 单击右上角的用户图标，然后单击 **[!UICONTROL 我的首选项]**. 此 **[!UICONTROL 用户首选项]** 窗口打开。

1. 选择所需的 **[!UICONTROL Stock配置]** ，然后单击 **[!UICONTROL Accept]** 以激活配置。

   ![用户首选项](assets/aem-stock-preferences.png)

1. 导航到 **[!UICONTROL 资产]** > **[!UICONTROL Adobe Stock]**. 您现在可以查看、搜索和获取许可证 [!DNL Adobe Stock] 资产。

下表说明了访问时用户权限的工作方式 [!DNL Adobe Stock] 资产：

| 用户 | 组 | 权限 | 在用户首选项中接受Stock配置 | 访问资源 | 访问Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| 管理员 | 不适用 | 所有 | 不适用 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 是 | 是 | 是 |
| test-doc1 | DAM 用户 | /conf/global/settings/stock/cloud-config | 否 | 错误：无法加载数据 | 否 |
| test-doc1 | DAM 用户 | **允许**： /conf/global/settings/stock **拒绝**： /cloud-config | Stock配置不可见 | 是 | 否 |

## 使用和管理 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager] {#usemanage}

利用此功能，组织可允许其用户使用 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager Assets]. 从 [!DNL Experience Manager] 用户界面，用户可以进行搜索 [!DNL Adobe Stock] 并许可所需的资产。

一次 [!DNL Adobe Stock] 资产许可位置 [!DNL Experience Manager]，可以像典型资源一样对其进行使用和管理。 在 [!DNL Experience Manager]用户可以搜索并预览资产；复制并发布资产；共享资产 [!DNL Brand Portal]；通过以下方式访问和使用资源 [!DNL Experience Manager] 桌面应用程序；等等。

![搜索 [!DNL Adobe Stock] 资源并从筛选结果 [!DNL Adobe Experience Manager] 工作区](assets/adobe-stock-search-results-workspace.png)

**A.**[!DNL Adobe Stock] 搜索与提供 ID 的资产类似的资产。**B.** 搜索与您选择的形状或方向匹配的资产。**C.** 搜索一种或多种受支持的资产类型 **D.** 打开或折叠过滤器窗格 **E.** 在 中授权并保存选定的资产 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 在 中保存带水印的资产 **G.**[!DNL Adobe Stock] 在 网站上浏览与选定资产类似的资产 **H.**[!DNL Adobe Stock] 在 网站上查看选定资产 **I.** 搜索结果中的选定资产数 **J.** 在卡片视图和列表视图之间切换

### 查找资源 {#find-assets}

您的 [!DNL Experience Manager] 用户可以在以下两个位置搜索资产： [!DNL Experience Manager] 和 [!DNL Adobe Stock]. 当搜索位置不限于 [!DNL Adobe Stock]，则搜索结果来自 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 将显示。

* 要搜索 [!DNL Adobe Stock] 资产，请单击 **[!UICONTROL 导航]** > **[!UICONTROL 资产]** > **[!UICONTROL 搜索Adobe Stock]**.

* 要搜索中的资产，请执行以下操作 [!DNL Adobe Stock] 和 [!DNL Experience Manager Assets]，单击搜索 ![搜索](assets/do-not-localize/search_icon.png).

或者，开始键入 `Location: Adobe Stock` 在搜索栏中选择 [!DNL Adobe Stock] 资产。 [!DNL Experience Manager] 对搜索的资产提供高级筛选功能，允许用户使用筛选器快速聚焦于所需的资产，如支持的资产类型、图像方向和许可状态。

>[!NOTE]
>
>搜索自以下位置的资源： [!DNL Adobe Stock] 显示于 [!DNL Experience Manager]. [!DNL Adobe Stock] 资源获取并存储在 [!DNL Experience Manager] 仅在用户出现以下任一情况后创建存储库： [保存资产](/help/assets/aem-assets-adobe-stock.md#saveassets) 或 [许可并保存资产](/help/assets/aem-assets-adobe-stock.md#licenseassets). 已存储在中的资产 [!DNL Experience Manager] 为了便于引用和访问，将显示和突出显示。 此外， [!DNL Stock] 资源会与一些其他元数据一起保存，以将源指示为 [!DNL Stock].

![在中搜索筛选器 [!DNL Experience Manager] 和突出显示 [!DNL Adobe Stock] 搜索结果中的资源](assets/aem-search-filters2.jpg)

### 保存并查看所需的资产 {#saveassets}

选择要保存到的资源 [!DNL Experience Manager]. 单击 [!UICONTROL 保存] 并提供资源的名称和位置。 未授权的资产将带有水印保存在本地。

下次搜索资源时，保存的资源将带徽章突出显示，以指示此类资源在中可用 [!DNL Experience Manager Assets].

>[!NOTE]
>
>最近添加的资产显示“新”徽章，而不是“已许可”徽章。

### 许可资产 {#licenseassets}

用户可以许可 [!DNL Adobe Stock] 资源(通过使用其资源的 [!DNL Adobe Stock] 企业计划。 当您许可资产时，该资产会保存而不加水印，并且可用于搜索和使用中 [!DNL Experience Manager Assets].

![用于许可和保存的对话框 [!DNL Adobe Stock] 中的资产 [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### 访问元数据和资源属性 {#access-metadata-and-asset-properties}

用户可以访问和预览元数据，包括 [!DNL Adobe Stock] 保存在中的资源的元数据属性 [!DNL Experience Manager]，并添加 **[!UICONTROL 许可证引用]** 对于资产。 但是，对许可证引用的更新不会在 [!DNL Experience Manager] 和 [!DNL Adobe Stock] 网站。

用户可以查看已许可和未许可资产的属性。

![查看和访问已保存资产的元数据和许可证引用](assets/metadata_properties.jpg)


## 已知限制 {#known-limitations}

* **限制用户进行许可的功能无法正常工作**：所有用户都具有 `read` 允许stock配置的权限来搜索和许可 [!DNL Adobe Stock] 资产。

* **非管理员用户必须手动激活 [!DNL Adobe Stock] 云配置**：在 **[!UICONTROL 用户首选项]** 窗口， **[!UICONTROL Stock配置]** 显示 [!DNL Adobe Stock] 云配置已启用，但对于非管理员用户不起作用。 用户必须单击 **[!UICONTROL Accept]** 按钮以激活Stock配置。 如果不执行此步骤，系统会在访问时显示错误消息 **[!UICONTROL 资产]**.

* **不显示编辑图像警告**：在许可图像时，用户无法检查图像是否仅用于编辑。 为防止可能的滥用，管理员可以从Admin Console中关闭对编辑资源的访问权限。

* **显示的许可证类型错误**：可能在中显示不正确的许可证类型 [!DNL Experience Manager] 对于资产。 用户可以登录到 [!DNL Adobe Stock] 网站以查看许可证类型。

* **引用字段和元数据未同步**：当用户更新许可证引用字段时，许可证引用信息在中更新 [!DNL Experience Manager] 但不会在 [!DNL Adobe Stock] 网站。 同样，如果用户在 [!DNL Adobe Stock] 网站中，更新未同步 [!DNL Experience Manager].

<!--
## Use and manage [!DNL Adobe Stock] assets in [!DNL Experience Manager] {#usemanage}

Using this capability, organizations users can work using [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets]. From within the [!DNL Experience Manager] user interface, users can search [!DNL Adobe Stock] assets and license the required assets.

Once an [!DNL Adobe Stock] asset is licensed in [!DNL Experience Manager], it can be used and managed like a typical asset. In [!DNL Experience Manager], the users can search and preview the assets; copy and publish the assets; share the assets on [!DNL Brand Portal]; access and use the assets via [!DNL Experience Manager] desktop app; and so on.
-->

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

<!--
### Find assets {#find-assets}

Your [!DNL Experience Manager] users, can search for assets in both, [!DNL Experience Manager] and [!DNL Adobe Stock]. When the search location is not limited to [!DNL Adobe Stock], the search results from [!DNL Experience Manager] and [!DNL Adobe Stock] are displayed.

* To search for [!DNL Adobe Stock] assets, click **[!UICONTROL Navigation]** > **[!UICONTROL Assets]** > **[!UICONTROL Search Adobe Stock]**.

* To search for assets across [!DNL Adobe Stock] and [!DNL Experience Manager Assets], click search ![search](assets/do-not-localize/search_icon.png).

Alternatively, start typing `Location: Adobe Stock` in the search bar to select [!DNL Adobe Stock] assets. [!DNL Experience Manager] offers advanced filtering capabilities on the searched assets, allowing users to quickly zero-in on the required assets using filters, such as types of supported assets, image orientation, and licensed state.

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] assets are fetched and stored in [!DNL Experience Manager] repository only after a user either [saves an asset](/help/assets/aem-assets-adobe-stock.md#saveassets) or [licenses and saves an asset](/help/assets/aem-assets-adobe-stock.md#licenseassets). Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![Search filters in Experience Manager and highlighted Adobe Stock assets in search results](assets/aem-search-filters2.jpg)

*Figure: Search filters in [!DNL Experience Manager] and highlighted [!DNL Adobe Stock] assets in search results.*

### Save and view the required assets {#saveassets}

Select an asset that you want to save in [!DNL Experience Manager]. Click [!UICONTROL Save] in the toolbar at the top and provide the name and location of the asset. The unlicensed assets are saved locally with a watermark.

Next time when you search for assets, the saved assets are highlighted with a badge, to indicate that such assets are available in [!DNL Experience Manager Assets].

>[!NOTE]
>
>The recently added assets display a New badge instead of Licensed badge.

### License assets {#licenseassets}

Users can license [!DNL Adobe Stock] assets by using the quota of their [!DNL Adobe Stock] enterprise plan. When you license an asset, it is saved without a watermark and is available for searching and using in [!DNL Experience Manager Assets].

![Dialog to license and save Adobe Stock assets in Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figure: Dialog to license and save [!DNL Adobe Stock] assets in [!DNL Experience Manager Assets].*

### Access metadata and asset properties {#access-metadata-and-asset-properties}

Users can access and preview the metadata, including the [!DNL Adobe Stock] metadata properties for the assets saved in [!DNL Experience Manager], and add **[!UICONTROL License References]** for an asset. However, the updates to license reference are not synced between [!DNL Experience Manager] and [!DNL Adobe Stock] website.

Users can see the properties for both, licensed and unlicensed assets.

![View and access metadata and license references of saved assets](assets/metadata_properties.jpg)

*Figure: View and access metadata and license references of saved assets.*

## Known limitations {#known-limitations}

* **Editorial image warning is not displayed**: When licensing an image, users cannot check if an image is Editorial Use Only. To prevent possible misuse, the administrators can turn off the access to editorial assets from the Admin Console.

* **Wrong license type is displayed**: It is possible that an incorrect license type is displayed in [!DNL Experience Manager] for an asset. Users can log into the [!DNL Adobe Stock] website to see the license type.

* **Reference fields and metadata are not synced**: When a user updates a license reference field, the license reference information is updated in [!DNL Experience Manager] but not on the [!DNL Adobe Stock] website. Similarly, if the user updates the reference fields on the [!DNL Adobe Stock] website, the updates are not synchronized in [!DNL Experience Manager].
-->

**另请参阅**

* [翻译资源](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [资源支持的文件格式](file-format-support.md)
* [搜索资源](search-assets.md)
* [连接的资源](use-assets-across-connected-assets-instances.md)
* [资源报告](asset-reports.md)
* [元数据架构](metadata-schemas.md)
* [下载资源](download-assets-from-aem.md)
* [管理元数据](manage-metadata.md)
* [搜索 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [批量元数据导入](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [有关将Adobe Stock资源与Experience Manager Assets结合使用的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Adobe Stock企业计划帮助](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常见问题解答](https://helpx.adobe.com/stock/faq.html)
