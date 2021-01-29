---
title: 使用用户映射工具
description: 使用用户映射工具
translation-type: tm+mt
source-git-commit: 2ceaaa4db35ab793392ae3644db9b862cbf9af2b
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 3%

---


# 使用用户映射工具{#user-mapping-tool}

## 概述 {#overview}

在以Cloud Service身份访问Adobe Experience Manager(AEM)的过渡旅程中，您需要将用户和组从现有的AEM系统移至作为Cloud Service。 这由内容传输工具完成。

对AEM作为Cloud Service的一个重大改变是完全集成地使用AdobeID访问创作层。  这需要使用[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)管理用户和用户组。 AdobeIdentity Management系统(IMS)中集中了用户用户档案信息，该系统可在所有Adobe云应用程序中提供单一登录。 有关详细信息，请参阅[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 由于此更改，现有用户和用户组需要映射到其IMS ID，以避免重复用户和Cloud Service作者实例上的用户组。

## 重要注意事项{#important-considerations}

有一些例外情况需要考虑。 将记录以下特定案例，并且不会映射有关的用户或组：

1. 如果用户在其&#x200B;*jcr*&#x200B;节点的`profile/email`字段中没有电子邮件地址。

1. 如果在AdobeIdentity Management系统(IMS)系统上找不到所使用的组织ID的给定电子邮件（或者，由于其他原因无法检索IMS ID）。

1. 如果用户当前处于禁用状态，则会将其视为与未禁用状态相同。 它将按正常方式进行映射和迁移，并在云实例上保持禁用状态。

## 使用用户映射工具{#using-user-mapping-tool}

用户映射工具使用一个API，它允许它通过电子邮件查找AdobeIdentity Management系统(IMS)用户并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端机密以及访问令牌或承载令牌。

请按照以下步骤进行设置：

1. 使用您的Adobe ID导航到[Adobe开发人员控制台](https://console.adobe.io)。
1. 创建新项目或打开现有项目。
1. 添加API。
1. 选择“用户管理API”。
1. 创建JWT凭据。
1. 生成密钥对或上传公钥（rsa不行）。
1. 生成访问令牌（或JWT令牌或载体令牌）。
1. 保存所有这些信息，如&#x200B;**客户端ID**、**客户端机密**、**技术帐户ID**、**技术帐户电子邮件**、**组织ID**&#x200B;和&#x200B;**访问令牌**&#x200B;安全。

## 用户界面 {#user-interface}

用户映射工具集成到内容传输工具中。 您可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载内容传输工具。 有关最新版本的详细信息，请参阅[当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 选择选择Adobe Experience Manager并导航到工具-> **操作** -> **内容传输**。
1. 单击&#x200B;**创建用户映射配置**。

   >[!NOTE]
   >如果您跳过此步骤，则在提取阶段将跳过用户和组映射。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   按如下所述填充用户管理API配置中的字段：

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **组织ID**:输入要迁移用户的组织的AdobeIdentity Management系统(IMS)组织ID。

      >[!NOTE]
      >要获取组织ID，请登录[Admin Console](https://adminconsole.adobe.com/)，并选择您的组织（在右上方区域）（如果您属于多个组织）。 组织ID将以`xx@AdobeOrg`的格式显示在该页的URL中，其中xx是IMS组织ID。  或者，您也可以在[Adobe开发者控制台](https://console.adobe.io)页面中找到组织ID，您可以在该页面中生成访问令牌。

   * **客户端ID**:输入您从设置步骤保存的客户端ID。

   * **访问令牌**:输入您从设置步骤保存的访问令牌。

      >[!NOTE]
      >该访问令牌每24小时过期一次，需要创建新的订阅。 要创建新令牌，请返回[Adobe开发者控制台](https://console.adobe.io)，选择您的项目，单击&#x200B;**用户管理API**&#x200B;并将同一私钥粘贴到框中。

1. 输入上述信息后，单击&#x200B;**保存**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. 通过单击&#x200B;**创建迁移集**&#x200B;并填充字段，然后单击&#x200B;**保存**，创建迁移集。 有关详细信息，请参阅[运行内容传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。

   >[!NOTE]
   >默认情况下，用于包括IMS用户和用户组映射用户的切换开关处于开启状态。 通过此设置，当对此迁移集执行提取时，用户映射工具将作为提取阶段的一部分运行。 这是运行内容传输工具的提取阶段的推荐方式。 如果此切换被关闭且／或未创建用户映射配置，则在提取阶段将跳过用户和用户组映射。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 要运行提取阶段，请参阅[运行内容传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。



