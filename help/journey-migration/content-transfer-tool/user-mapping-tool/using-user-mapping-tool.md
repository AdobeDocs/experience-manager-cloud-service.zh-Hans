---
title: 使用用户映射工具
description: 使用用户映射工具
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 3%

---


# 使用用户映射工具 {#using-user-mapping-tool}

用户映射工具使用一个API，它允许通过电子邮件查找AdobeIdentity Management系统(IMS)用户，并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端密钥和访问令牌或载体令牌。

## 设置用户映射工具 {#setting-up-user-mapping}

请按照以下步骤进行设置：

1. 导航到 [Adobe开发人员控制台](https://console.adobe.io) 用你的Adobe ID。
1. 创建新项目或打开现有项目。
1. 添加API — 单击 **添加到项目** 选择 **API**
1. 选择用户管理API。  您可能需要获得权限才能使用此选项。
1. 创建JWT凭据。
1. 生成密钥对，或上传公钥（rsa不是好方法）。  有个按钮， **生成公共/私有密钥对**，这将为您执行此操作。  确保同时保存公钥和私钥。
1. 导航到用户管理API。
1. 通过将您的私钥内容粘贴到文本框并单击，生成访问令牌（或载体令牌） **生成令牌**.
1. 保存所有这些信息，例如 **客户端ID**, **客户端密钥**, **技术帐户ID**, **技术帐户电子邮件**, **组织ID**&#x200B;和 **访问令牌** 安全。

## 访问用户映射工具的用户界面 {#user-interface}

用户映射工具已集成到内容传输工具中。 您可以从下载内容传输工具 [软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html). 有关最新版本的更多详细信息，请参阅 [最新发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md).

1. 选择Adobe Experience Manager并导航到工具 — > **操作** -> **内容迁移**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 单击 **用户映射** 卡。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 单击 **创建用户映射配置**.

   >[!NOTE]
   >如果跳过此步骤，则在提取阶段会跳过用户和组映射。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   填充 **用户管理API配置**，如下所述。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **组织ID**:输入要迁移Adobe的组织的Identity Management系统(IMS)组织ID。

      >[!NOTE]
      >要获取组织ID，请登录 [Admin Console](https://adminconsole.adobe.com/) 如果您属于多个组织，请选择您的组织（在右上方）。 组织ID将位于该页面的URL中，格式如下 `xx@AdobeOrg`，其中xx是IMS组织ID。  或者，您也可以在 [Adobe开发人员控制台](https://console.adobe.io) 页面。

   * **客户端ID**:输入您在设置步骤中保存的客户端ID。

   * **访问令牌**:输入您在设置步骤中保存的访问令牌。

      >[!NOTE]
      >访问令牌每24小时过期一次，并且需要创建一个新令牌。 要创建新令牌，请返回 [Adobe开发人员控制台](https://console.adobe.io)，选择项目，单击 **用户管理API** 并将相同的私钥粘贴到框中。

1. 填充字段后，单击 **测试配置** 以测试与用户管理API服务的连接。 如果连接成功，您将能够单击 **保存** 以保存配置。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 保存配置后，选择配置并单击 **开始用户映射**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 单击 **开始** ，以启动用户映射流程。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   它会显示 **状态** as **正在运行**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-start1.png)


1. 用户映射完成后，单击 **结果** 查看摘要。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* 完成用户映射后，您可以使用痕迹导航导航导航导航回内容迁移页面。 用户映射卡显示状态和时间戳。 单击 **内容传输** 创建要运行提取的迁移集。 请参阅 [运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool) 以了解更多详细信息。


### 恢复用户映射过程 {#resume-user-mapping-process}

如果由于以下任何原因而停止了用户映射过程：

* 所选用户 **停止用户映射**
* 访问令牌在过程中过期，或
* 其他原因

   >[!NOTE]
   >进程从进程停止的位置保存。

请按照以下步骤继续用户映射流程：

1. 单击 **查看日志** 查看用户映射日志以检查保存的进度。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 单击 **开始用户映射** 按钮以从其停止的位置恢复。

   >[!NOTE]
   >在重新启动之前，请确保访问令牌仍然有效或已刷新。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 单击 **开始** 来恢复用户映射进程。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

   用户映射过程完成后，您将查看 **状态** as **已完成** 对于该特定配置。

   ![图像](/help/journey-migration/content-transfer-tool/assets-user-mapping/resume-user-mapping4.png)
