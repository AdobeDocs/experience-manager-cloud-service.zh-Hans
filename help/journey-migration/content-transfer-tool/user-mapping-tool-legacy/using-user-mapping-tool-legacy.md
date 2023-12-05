---
title: 使用用户映射工具（旧版）
description: 使用用户映射工具（旧版）
exl-id: dcb750c4-0f81-4d11-ac6c-0592162b683d
hide: true
hidefromtoc: true
source-git-commit: abe5f8a4b19473c3dddfb79674fb5f5ab7e52fbf
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---

# 使用用户映射工具（旧版） {#using-user-mapping-tool}

>[!INFO]
>
>本文档参考该工具的已弃用版本。 有关最新版本的更多信息，请参阅 [用户映射和主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

用户映射工具使用的API允许其通过电子邮件查找AdobeIdentity Management System (IMS)用户并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端密钥以及访问或持有者令牌。

## 设置用户映射工具 {#setting-up-user-mapping}

**先决条件：** 用户映射要求每个要映射到其IMS ID的用户在其AEM和IMS中的配置文件中均有一个电子邮件地址。 即使用户使用电子邮件地址作为用户ID登录，映射也对该用户不起作用，除非该电子邮件地址也位于配置文件中以及IMS中。

请按照以下步骤进行此设置：

1. 导航到 [Adobe Developer控制台](https://developer.adobe.com/console/) 使用您的Adobe ID。
1. 创建一个项目或打开一个现有项目。
1. 添加API — 单击 **添加到项目** 并选择 **API**
1. 选择用户管理API。 您必须具有系统管理员权限才能使用此选项。
1. 创建JWT凭据。
1. 生成密钥对或上传公钥（rsa没有用）。 有个按钮， **生成公钥/私钥对** 会为您创建此密钥对。 确保同时保存公钥和私钥。
1. 导航到用户管理API。
1. 通过将私钥内容粘贴到文本框并单击，生成访问令牌（或持有者令牌） **生成令牌**.
1. 保存所有这些信息，例如 **客户端ID**， **客户端密码**， **技术帐户ID**， **技术帐户电子邮件**， **组织ID**、和 **访问令牌** 安全无虞。

## 访问用户映射工具的用户界面 {#user-interface}

用户映射工具已集成到内容传输工具中。 您可以从以下位置下载内容传输工具 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 有关最新版本的更多详细信息，请参阅 [最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. 选择Adobe Experience Manager并导航到工具> **操作** > **内容迁移**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 单击 **用户映射** 卡片。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 单击 **创建用户映射配置**.

   >[!NOTE]
   >如果跳过此步骤，则在提取阶段将跳过用户和组映射。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填充中的字段 **用户管理API配置**，如下所述。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **组织ID**：输入要迁移用户的组织的Identity Management System (IMS)组织IDAdobe。

     >[!NOTE]
     >要获取组织ID，请登录 [Admin Console](https://adminconsole.adobe.com/) 如果您属于多个组织，请选择您的组织（位于右上角区域）。 组织ID位于该页面的URL中，格式如下 `xx@AdobeOrg`，其中xx是IMS组织ID。 或者，您可以在以下位置找到组织ID： [Adobe Developer控制台](https://developer.adobe.com/console/) 生成访问令牌的页面。

   * **客户端ID**：输入您在设置步骤中保存的客户端ID。

   * **访问令牌**：输入您在设置步骤中保存的访问令牌。

     >[!NOTE]
     >访问令牌每24小时过期一次，必须创建新的访问令牌。 要创建令牌，请返回到 [Adobe Developer控制台](https://developer.adobe.com/console/)，选择您的项目，然后单击 **用户管理API**，并将相同的私钥粘贴到框中。

1. 填充字段后，单击 **测试配置** 以测试与用户管理API服务的连接。 如果连接成功，可以单击 **保存** 以保存配置。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 保存配置后，选择配置并单击 **开始用户映射**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 单击 **开始** 从对话框中启动“用户映射”过程。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它显示 **状态** 作为 **正在运行**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 用户映射完成后，单击 **结果** 以查看摘要。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >
   >* 用户映射完成后，您可以使用痕迹导航导航导航返回内容迁移页面。 用户映射信息卡显示状态和时间戳。 单击 **内容传输** 以便创建迁移集以运行提取。 请参阅 [运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=en#running-tool) 以了解更多详细信息。

### 恢复用户映射过程 {#resume-user-mapping-process}

如果用户映射进程由于以下任何原因而停止：

* 选项 **停止用户映射** 已被用户选择。
* 访问令牌在此过程中过期。
* 或者，其他原因。

  >[!NOTE]
  >将从进程停止的位置保存进度。

请按照以下步骤继续用户映射过程：

1. 单击 **查看日志** 查看用户映射日志，以便查看保存的进度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 单击 **开始用户映射** 再次按钮以从之前停止的位置恢复。

   >[!NOTE]
   >在重新启动之前，请确保访问令牌仍然有效或已刷新。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 单击 **开始** 从对话框中恢复“用户映射”过程。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   用户映射过程完成后，您可以查看 **状态** 作为 **已完成** 的特定配置。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
