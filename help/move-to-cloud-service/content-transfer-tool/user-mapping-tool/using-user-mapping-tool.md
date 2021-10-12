---
title: 使用用户映射工具
description: 使用用户映射工具
source-git-commit: 25b4bfb624866cb615fca32377e43c05a597cd67
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 3%

---


# 使用用户映射工具 {#using-user-mapping-tool}

用户映射工具使用一个API，它允许通过电子邮件查找AdobeIdentity Management系统(IMS)用户，并返回其IMS ID。 此API要求用户为其组织创建客户端ID、客户端密钥和访问令牌或载体令牌。

## 设置用户映射工具 {#setting-up-user-mapping}

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

## 访问用户映射工具的用户界面 {#user-interface}

用户映射工具已集成到内容传输工具中。 您可以从[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)下载内容传输工具。 有关最新版本的更多详细信息，请参阅[当前发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

1. 选择Adobe Experience Manager并导航到工具 — > **操作** -> **内容迁移**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access1.png)

1. 单击&#x200B;**用户映射**&#x200B;卡。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access2.png)

1. 单击&#x200B;**创建用户映射配置**。

   >[!NOTE]
   >如果跳过此步骤，则在提取阶段会跳过用户和组映射。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access5.png)

   按如下所述填充&#x200B;**用户管理API配置**&#x200B;中的字段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access3.png)


   * **组织ID**:输入要迁移Adobe的组织的Identity Management系统(IMS)组织ID。

      >[!NOTE]
      >要获取组织ID，请登录[Admin Console](https://adminconsole.adobe.com/)，并选择您的组织（位于右上方）（如果您属于多个组织）。 组织ID将位于该页面的URL中，格式如`xx@AdobeOrg`，其中xx是IMS组织ID。  或者，您也可以在[Adobe开发人员控制台](https://console.adobe.io)页面中找到组织ID，您可以在该页面中生成访问令牌。

   * **客户端ID**:输入您在设置步骤中保存的客户端ID。

   * **访问令牌**:输入您在设置步骤中保存的访问令牌。

      >[!NOTE]
      >访问令牌每24小时过期一次，并且需要创建一个新令牌。 要创建新令牌，请返回至[Adobe开发人员控制台](https://console.adobe.io)，选择您的项目，单击&#x200B;**用户管理API**&#x200B;并将相同的私钥粘贴到框中。

1. 填充字段后，单击&#x200B;**测试配置**&#x200B;以测试与用户管理API服务的连接。 如果连接成功，您将能够单击&#x200B;**Save**&#x200B;以保存配置。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-access4.png)

1. 保存配置后，选择配置并单击&#x200B;**启动用户映射**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing4.png)

1. 单击对话框中的&#x200B;**启动**&#x200B;以启动“用户映射”进程。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)

1. 完成用户映射后，单击&#x200B;**Results**&#x200B;以查看摘要。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/user-mapping-landing5.png)

   >[!IMPORTANT]
   >* 完成用户映射后，您可以使用痕迹导航导航导航导航回内容迁移页面。 用户映射卡显示状态和时间戳。 单击&#x200B;**内容传输**&#x200B;以创建要运行提取的迁移集。 有关更多详细信息，请参阅[运行内容传输工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=en#running-tool)。


### 恢复用户映射过程 {#resume-user-mapping-process}

如果由于以下任何原因而停止了用户映射过程：

* 用户选择了&#x200B;**停止用户映射**
* 访问令牌在过程中过期，或
* 其他原因

   >[!NOTE]
   >进程从进程停止的位置保存。

请按照以下步骤继续用户映射过程：

1. 单击&#x200B;**查看日志**&#x200B;以查看用户映射日志以检查保存的进度。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping1.png)

1. 再次单击&#x200B;**开始用户映射**&#x200B;按钮以从其停止的位置恢复。

   >[!NOTE]
   >在重新启动之前，请确保访问令牌仍然有效或已刷新。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping2.png)

1. 单击对话框中的&#x200B;**开始**&#x200B;以继续“用户映射”进程。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets-user-mapping/resume-user-mapping3.png)
