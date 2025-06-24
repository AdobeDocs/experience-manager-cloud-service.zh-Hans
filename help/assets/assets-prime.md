---
title: Assets Prime
description: 详细了解Assets Prime的主要方面，如主要优势、用户类型及其权限。
feature: Asset Management
role: User, Admin
exl-id: 012f94c5-b1c3-4799-8eaf-af68d06c036f
source-git-commit: 47afd8f95eee2815f82c429e9800e1e533210a47
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 18%

---

# [!DNL Assets] as a Cloud Service Prime  {#assets-prime}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 和 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 与 Edge Delivery Services 集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI 可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用 Dynamic Media Prime 和 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

![AEM Assets Prime横幅图像](/help/assets/assets/aem-assets-prime-package-banner.png)

Assets as a Cloud Service Prime包括轻量级DAM，可让您执行各种关键功能，例如：

* **资产管理和库服务**：让用户能够在集中存储库中引入、存储、分类、控制、管理和治理品牌数字资产的工具

* **搜索、发现和协作**：使用户能够浏览、发现、共享和协作创建丰富客户体验所需资产的工具。

* **安全性和 Rights Management**：用于管理访问、权限、权利和安全性的工具，以确保合规性、一致性和品牌完整性。

* **Creative Cloud Connections**：使营销和创意团队能够通过简化的访问、评论、审核和注释进行协作以更新或完成数字资产的工具。

* **Experience Cloud 连接**：支持从其他 Experience Cloud 应用程序和服务本地访问数字资产的工具。

* **没有可扩展性选项的分发门户体验(Content Hub)**：用于向扩展的利益相关者扩展对品牌批准的数字资产的访问权限以确保使用和品牌一致性。

* **集成**：与其他 Adobe 和非 Adobe 应用程序的集成。

* **Dynamic Media（插件）**：用于转换和传递图像、视频和其他新兴内容的工具，可为任何设备大规模提供丰富的交互式多媒体体验。

  >[!NOTE]
  >
  >带有OpenAPI功能的Dynamic Media还通过Assets Prime提供对基本图像修饰符的访问，例如旋转、裁切（仅限手动 — 无智能裁切）、翻转、高度、宽度、质量、格式和自适应视频流。 请联系Adobe客户团队以了解更多信息。

1. [创建新程序](/help/journey-onboarding/create-program.md)。

但是，随着DAM需求的增长以及您对更多功能（如UI可扩展性、API驱动的自动化和自定义代码部署）的需求，您必须考虑升级到[Assets Ultimate](/help/assets/assets-ultimate-overview.md)。

本文提供了一个用于启用Assets as a Cloud Service Prime的端到端工作流程。

## 启用Assets as a Cloud Service Prime{#enable-assets-prime}

在使用Assets创建新程序时启用Cloud Manager Prime。 执行以下步骤：

1. 作为系统管理员，登录到Cloud Manager。 确保在登录时选择正确的组织。

   >[!NOTE]
   >
   >确保已将您添加到相应的Cloud Manager产品配置文件以添加新项目。 有关详细信息，请参阅Cloud Manager中基于[角色的权限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)。

1. [创建新程序](/help/journey-onboarding/create-program.md)。

   创建新程序时，在&#x200B;**[!UICONTROL 解决方案和加载项]**&#x200B;选项卡中，选择&#x200B;**[!UICONTROL Assets Prime]**。 您还可以展开&#x200B;**[!UICONTROL Assets Prime]**&#x200B;并选择&#x200B;**[!UICONTROL Content Hub]**&#x200B;以启用[Content Hub](/help/assets/product-overview.md)的资源分发。

   ![AEM Assets Ultimate](assets/aem-assets-prime.png)


1. 单击&#x200B;**[!UICONTROL 创建]**&#x200B;以创建程序。

1. 单击程序卡，然后单击&#x200B;**[!UICONTROL 添加环境]**。

1. 指定环境名称，定义一个区域，然后单击&#x200B;**[!UICONTROL 保存]**&#x200B;以创建环境。

   ![将环境添加到Assets Prime](assets/aem-assets-prime-add-environment.png)

>[!NOTE]
>
>Assets Prime仅允许您创建生产环境。 成功创建生产环境后，“添加环境”选项将不再可用。

Assets Prime现已为Experience Manager Assets as a Cloud Service启用。

![AEM Assets Prime可用](assets/aem-assets-prime-setup-complete.png)

系统管理员自动获得AEM管理员的权限，并会收到一封电子邮件，导航到Admin Console以管理产品配置文件。


Admin Console上的AEM as a Cloud Service实例包含以下产品配置文件：

* AEM 管理员

* AEM 用户

* [AEM Assets 协作者用户](#onboard-collaborator-users)

* [AEM Assets 高级用户](#onboard-power-users)


![AEM Assets产品配置文件](assets/aem-assets-product-profiles.png)

您可以开始将用户或用户组添加到AEM Assets Collaborator用户和AEM Assets超级用户产品配置文件。 有关详细信息，请参阅[载入AEM Assets Collaborator用户](#onboard-collaborator-users)和[载入AEM Assets超级用户](#onboard-power-users)。

如果您已经为Assets as a Cloud Service启用了Content Hub，则在Admin Console上的AEM Assets as a Cloud Service中会创建一个新实例，其后缀为`delivery`：

![Content Hub的新实例](assets/new-instance-content-hub.png)

>[!NOTE]
>
>如果您在2024年8月14日之前配置了Content Hub，则会创建新实例，并将`contenthub`作为后缀。

请注意，Content Hub的实例名称中没有`author`或`publish`。

单击实例名称以查看`AEM Assets Limited Users` Content Hub产品配置文件。

![Content Hub产品配置文件](assets/content-hub-product-profile.png)

您可以开始将用户或用户组添加到此产品配置文件，以便他们能够访问Content Hub。

>[!NOTE]
>
>如果您在2024年8月14日之前配置了Content Hub，则Content Hub产品配置文件在`Limited Users`之后提及`contenthub`，而不是`delivery`。

## 载入AEM Assets协作者用户 {#onboard-collaborator-users}

AEM Assets Collaborator用户可以通过贵组织在其他Assets产品和非Adobe应用程序中提供的Adobe集成来使用Experience Manager中的资产，使用内置的Adobe Express和Firefly创建和编辑资产，利用专业设计的模板、品牌工具包、Adobe Stock资产等，以及使用AEM Assets Content Hub门户访问和利用贵组织批准的资产。

要载入Collaborator用户：

1. 通过单击Experience Manager Assets产品列表中的AEM as a Cloud Service产品名称，访问Admin Console产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

1. 单击Collaborators用户产品配置文件，然后单击&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将该用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-assets-collaborator-user-permissions.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

您还可以访问和查看分配给Collaborator用户的服务，如下图所示：

为Collaborator用户提供![服务](assets/aem-assets-collaborator-users.png)

默认情况下已启用`Adobe Express`和`AEM Assets Collaborator Users`服务。 您可以根据自己的要求关闭和打开切换开关，但是Adobe建议使用为产品配置文件启用的默认服务。

## 载入AEM Assets高级用户 {#onboard-power-users}

AEM Assets高级用户可以访问所有AEM Assets功能，包括管理资产、权限、元数据以及有关数字资产的整体管理和自动化，通过其他Adobe和非Adobe应用程序中提供给贵组织的Assets集成使用Experience Manager中的资产，使用内置的Adobe Express和Firefly利用专业设计的模板、品牌工具包、Adobe Stock资产等创建和编辑资产，以及使用AEM Assets Content Hub门户访问和利用贵组织批准的资产。

要载入超级用户，请执行以下操作：

1. 通过单击Experience Manager Assets产品列表中的AEM as a Cloud Service产品名称，访问Admin Console产品配置文件。

1. 单击AEM as a Cloud Service的生产创作实例：
   AEM as a Cloud Service的![产品配置文件](assets/aem-cloud-service-instances.png)

1. 单击Power users产品配置文件，然后单击&#x200B;**[!UICONTROL 添加用户]**&#x200B;以将用户添加到产品配置文件。
   ![用户产品配置文件](assets/aem-assets-power-user-permissions.png)

1. 单击&#x200B;**[!UICONTROL 保存]**&#x200B;即可保存更改。

您还可以访问和查看分配给超级用户的服务，如下图所示：

超级用户![服务](assets/aem-assets-power-users.png)

默认情况下已启用`Adobe Express`和`AEM Assets Power Users`服务。 您可以根据自己的要求关闭和打开切换开关，但是Adobe建议使用为产品配置文件启用的默认服务。
