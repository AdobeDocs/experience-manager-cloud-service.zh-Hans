---
title: 使用用户映射工具
description: 使用用户映射工具
exl-id: 88ce7ed3-46fe-4b3f-8e18-c7c8423faf24
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 2%

---

# 使用用户映射工具 {#user-mapping-tool}

## 概述 {#overview}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="用户映射工具"
>abstract="内容传输工具可帮助您将用户和组从现有AEM系统移至AEMas a Cloud Service。 现有用户和组需要映射到其IMS ID，以避免Cloud Service创作实例上出现重复的用户和组。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#important-considerations" text="使用用户映射工具的重要注意事项"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#using-user-mapping-tool" text="使用用户映射工具"

在过渡到Adobe Experience Manager(AEM)as a Cloud Service的历程中，您需要将用户和组从现有AEM系统移至AEMas a Cloud Service。 这由内容传输工具完成。

AEMas a Cloud Service的一项主要更改是完全集成地使用AdobeID访问创作层。  这需要使用[Adobe Admin Console](https://helpx.adobe.com/cn/enterprise/using/admin-console.html)管理用户和用户组。 AdobeIdentity Management系统(IMS)中集中了用户配置文件信息，该系统可在所有Adobe云应用程序中提供单点登录。 有关更多详细信息，请参阅[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html?lang=en#identity-management)。 由于进行了这项更改，现有用户和组需要映射到其IMS ID，以避免Cloud Service创作实例上出现重复的用户和组。

### 用户映射工具 {#mapping-tool}

内容传输工具（无用户映射）将迁移与所迁移内容关联的任何用户和组。 用户映射工具是内容传输工具的一部分，其唯一目的是修改用户和组，以便IMS(AEMas a Cloud Service使用的单点登录功能)能够正确识别它们。 完成这些修改后，内容传输工具会照常迁移指定内容的用户和组。

## 重要注意事项 {#important-considerations}

### 特殊情况 {#exceptional-cases}

将记录以下特定案例：

1. 如果用户的&#x200B;*jcr*&#x200B;节点的`profile/email`字段中没有电子邮件地址，则将迁移相关用户或组，但未映射。

1. 如果在AdobeIdentity Management系统(IMS)系统中没有找到所用组织ID的给定电子邮件（或者，如果IMS ID因其他原因无法检索），则相关用户或组将被迁移，但未映射。

1. 如果用户当前处于禁用状态，则其处理方式与未禁用时相同。 它将照常进行映射和迁移，并在云实例上保持禁用状态。

1. 如果目标AEM Cloud Service实例上存在与源AEM实例上的某个用户同名(rep:principalName)的用户，则将不会迁移相关用户或组。

### 其他注意事项 {#additional-considerations}

* 如果设置&#x200B;**在摄取**&#x200B;之前擦除云实例上的现有内容，则Cloud Service实例上已转移的用户将与整个现有存储库一起删除，并将创建新存储库以将内容摄取到中。 此外，这还会重置所有设置，包括目标Cloud Service实例的权限，对于添加到&#x200B;**administrators**&#x200B;组的管理员用户，设置为true。 需要将管理员用户重新添加到&#x200B;**administrators**&#x200B;组，以检索CTT的访问令牌。

* 建议在通过“用户映射”运行CTT之前，从目标Cloud ServiceAEM实例中删除任何现有用户。 这是为了防止将用户从源AEM实例迁移到目标AEM实例之间发生任何冲突。 如果源AEM实例和目标AEM实例上存在相同的用户，则在摄取期间将会发生冲突。

* 执行内容增补时，如果内容自上次传输后未发生更改而未进行传输，则与该内容关联的用户和组也将不会进行传输，即使用户和组在此期间发生更改也是如此。 这是因为用户和组以及与其关联的内容一起进行迁移。

* 如果目标AEM Cloud Service实例的用户与源AEM实例上的某个用户具有不同的用户名，但其电子邮件地址与该用户中的某个用户相同，并且启用了“用户映射”，则日志中将写入一条错误消息，并且不会传输源AEM用户，因为目标系统上只允许一个具有给定电子邮件地址的用户。

* 如果源AEM实例上的两个用户具有相同的电子邮件地址，并且启用了“用户映射”，则日志中将写入一条错误消息，并且不会传输源AEM用户之一，因为目标系统上只允许一个具有给定电子邮件地址的用户。


## 使用用户映射工具 {#using-user-mapping-tool}

用户映射工具使用一个API，它允许通过电子邮件查找AdobeIdentity Management系统(IMS)用户，并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端密钥和访问令牌或载体令牌。

请按照以下步骤进行设置：

1. 使用您的Adobe ID导航到[Adobe开发人员控制台](https://console.adobe.io)。
1. 创建新项目或打开现有项目。
1. 添加API — 单击&#x200B;**添加到项目**&#x200B;并选择&#x200B;**API**
1. 选择用户管理API。  您可能需要获得权限才能使用此选项。
1. 创建JWT凭据。
1. 生成密钥对，或上传公钥（rsa不是好方法）。  有一个按钮， **生成公共/私有密钥对**，它将为您执行此操作。  确保同时保存公钥和私钥。
1. 导航到用户管理API。
1. 通过将您的私钥内容粘贴到文本框中并单击&#x200B;**生成令牌**&#x200B;来生成访问令牌（或载体令牌）。
1. 安全保存所有这些信息，如&#x200B;**客户端ID**、**客户端密钥**、**技术帐户ID**、**技术帐户电子邮件**、**组织ID**&#x200B;和&#x200B;**访问令牌**。

## 用户界面 {#user-interface}

用户映射工具已集成到内容传输工具中。 您可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载内容传输工具。 有关最新版本的更多详细信息，请参阅[当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 选择 Adobe Experience Manager 并导航到工具 -> **操作** -> **内容传输**。
1. 单击&#x200B;**创建用户映射配置**。

   >[!NOTE]
   >如果跳过此步骤，则在提取阶段会跳过用户和组映射。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-1.png)

   按如下所述填充用户管理API配置中的字段：

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-2.png)

   * **组织ID**:输入要迁移Adobe的组织的Identity Management系统(IMS)组织ID。

      >[!NOTE]
      >要获取组织ID，请登录[Admin Console](https://adminconsole.adobe.com/)，并选择您的组织（位于右上方）（如果您属于多个组织）。 组织ID将位于该页面的URL中，格式如`xx@AdobeOrg`，其中xx是IMS组织ID。  或者，您也可以在[Adobe开发人员控制台](https://console.adobe.io)页面中找到组织ID，您可以在该页面中生成访问令牌。

   * **客户端ID**:输入您在设置步骤中保存的客户端ID。

   * **访问令牌**:输入您在设置步骤中保存的访问令牌。

      >[!NOTE]
      >访问令牌每24小时过期一次，并且需要创建一个新令牌。 要创建新令牌，请返回至[Adobe开发人员控制台](https://console.adobe.io)，选择您的项目，单击&#x200B;**用户管理API**&#x200B;并将相同的私钥粘贴到框中。

1. 在输入上述信息后，单击&#x200B;**Save**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-3.png)


1. 通过单击&#x200B;**创建迁移集**&#x200B;并填充字段，然后单击&#x200B;**保存**&#x200B;来创建迁移集。 有关更多详细信息，请参阅[运行内容传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。

   >[!NOTE]
   >默认情况下，用于包括从IMS用户和组映射用户的切换开关处于开启状态。 通过此设置，在对此迁移集执行提取时，用户映射工具将作为提取阶段的一部分运行。 这是运行内容传输工具提取阶段的推荐方法。 如果此切换开关处于关闭状态，并且/或未创建用户映射配置，则在提取阶段期间将跳过用户和组映射。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-4.png)

1. 要运行提取阶段，请参阅[运行内容传输工具](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#running-tool)。
