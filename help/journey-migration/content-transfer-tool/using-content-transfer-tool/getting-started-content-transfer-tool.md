---
title: 内容转移工具快速入门
description: 内容转移工具快速入门
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: b31fe77cd43362b6ad768e8a2b258c23ae84466c
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 22%

---

# 内容转移工具快速入门 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下载"
>abstract="可从软件分发门户下载 zip 文件形式的内容转移工具。您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。确保下载最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans" text="发行说明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="软件分发门户"

可从软件分发门户下载 zip 文件形式的内容转移工具。您可以通过以下方式安装包 [包管理器](/help/implementing/developing/tools/package-manager.md) 源Adobe Experience Manager (AEM)实例上的。 确保下载最新版本。有关最新版本的更多详细信息，请参阅 [发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans).

仅支持版本2.0.0及更高版本，建议使用最新版本。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 源环境连接 {#source-environment-connectivity}

>[!NOTE]
>
>如果从Cloud Acceleration Manager中删除了迁移集，也可能会发生连接错误。

源AEM实例可能运行在防火墙之后，在防火墙中，它只能访问已添加到允许列表的某些主机。 要成功运行提取，需要从运行AEM的实例访问以下端点：

* Azure Blob存储服务： `casstorageprod.blob.core.windows.net`

>[!NOTE]
>如果提取由于以下错误而失败：“javax.net.ssl.SSLHandshakeException： sun.security.validator.ValidatorException： PKIX路径构建失败： sun.security.provider.certpath.SunCertPathBuilderException：无法找到请求的目标的有效证书路径”，则可以通过导入相关的CA证书来解决此问题。

### 启用SSL日志记录 {#enable-ssl-logging}

了解SSL/TLS连接问题有时可能很困难。 要排除提取过程中的连接问题，您可以通过源AEM环境的“系统控制台”启用SSL日志记录，请执行以下步骤：

1. 通过转到，导航到源实例上的Adobe Experience Manager Web Console **工具 — 操作 — Web控制台** 或直接转到URL，网址为 *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用 **为提取启用ssl日志记录** 设置，然后按 **保存**：

   ![图像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## 运行内容传输工具 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="运行内容转移工具"
>abstract="了解如何使用内容转移工具将内容迁移到 AEM as a Cloud Service（创作/发布）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 观看演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教程 - 使用内容转移工具"

以下部分适用于内容传输工具的新版本。 阅读本节内容，了解如何使用内容传输工具将内容迁移到AEMas a Cloud Service：

### 提取设置阶段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取设置阶段"
>abstract="了解如何创建和管理迁移集以及如何复制提取密钥。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教程 - 使用内容转移工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. 登录Cloud Acceleration Manager (CAM)，然后单击之前创建的CAM项目，以评估您为迁移到AEMas a Cloud Service所做的准备工作。 如果尚未创建CAM项目，请参阅在CAM中创建和管理项目。

1. 单击 **内容传输** 信息卡。 这会将您转到迁移集列表视图。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 通过单击 **创建迁移集**.

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每个项目最多可以创建五个迁移集，包括已过期的迁移集。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   将显示以下对话框。 请注意，迁移集将在长时间不活动后过期。 在项目信息卡和迁移作业表行上显示警告一段时间后，迁移集将过期，并且其数据将不再可用。 审核 [迁移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 了解详细信息。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >名称必须遵循与AEM节点相同的约定，因此不能包含以下任何字符： . / ： [ ] | *

1. 现在，您应会在列表视图中看到迁移列表。 单击三点符号(**...**)以打开下拉菜单并单击 **复制提取密钥**. 在提取阶段，您将需要此密钥。 复制此提取密钥。

   >[!NOTE]
   >
   >通过提取密钥，您的源AEM环境可以安全地连接到迁移集。 请像对待密码一样谨慎对待此密钥，切勿通过不安全的媒介（如电子邮件）共享此密钥。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填充迁移集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填充迁移集"
>abstract="创建迁移集后，需要为它填入需要从源实例移至 AEM as a Cloud Service 环境的内容。为此，需要在源实例上安装内容转移工具。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="提取内容"

要填充您在Cloud Acceleration Manager中创建的迁移集，您需要在源Adobe Experience Manager (AEM)实例上安装最新版本的内容传输工具。 阅读本节内容，了解如何填充迁移集。

1. 在源Adobe Experience Manager实例上安装最新版本的内容传输工具后，转到 **操作 — 内容迁移**

1. 单击 **创建迁移集**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 将之前从CAM复制的提取密钥粘贴到的提取密钥输入字段 **创建迁移集** 表单。 执行此操作后，迁移集名称和Cloud Acceleration Manager (CAM)项目名称字段将自动填充。 这些名称应与CAM中的“迁移集”名称和您创建的CAM项目名称匹配。 您现在可以添加内容路径。 添加内容路径后，您将能够保存迁移集。 您可以使用包含或排除的版本运行提取。

   >[!NOTE]
   >
   >确保提取密钥有效并且未接近其到期时间。 您可以将此信息放在 **创建迁移集** 对话框。 如果出现连接错误，请参阅 [源环境连接](#source-environment-connectivity) 了解更多信息。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接下来，选择以下参数以创建迁移集：

   1. **包含版本**：根据需要选择。当包含版本时，路径 `/var/audit` 将自动包含以迁移审核事件。

      ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >如果您打算将版本包含在迁移集中，并使用执行增补 `wipe=false`，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望启用版本清除，并且要对迁移集执行增补，则必须按以下方式执行引入 `wipe=true`.


   1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。路径选取器通过键入或选择来接受输入。

      >[!IMPORTANT]
      >创建迁移集时，以下路径受到限制：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (部分 `/etc` 允许在CTT中选择路径)


1. 单击 **保存** 填充以下位置的所有字段之后： **创建迁移集** 详细信息屏幕。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 确定迁移集大小 {#migration-set-size}

创建迁移集后，强烈建议在开始提取过程之前对迁移集运行大小检查。
通过对迁移集运行大小检查，您将能够：
* 确定中是否有足够的磁盘空间 `crx-quickstart` 子目录以成功完成提取。
* 确定迁移集大小是否在受支持的产品限制范围内，并避免内容摄取失败。

按照以下步骤运行大小检查：

1. 选择一个迁移集并单击 **检查大小**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 这将打开 **检查大小** 对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 单击 **检查大小** 以启动该流程。 然后，您将返回到迁移集列表视图，并且您应该会看到一条消息，指示 **检查大小** 正在运行。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 一次 **检查大小** 进程已完成，状态将更改为 **已完成**. 选择相同的迁移集并单击 **检查大小** 以查看结果。 以下是 **检查大小** 没有警告的结果。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 如果 **检查大小** 结果表示磁盘空间不足和/或迁移集超出产品限制， **警告** 将显示状态。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 后续内容 {#whats-next}

了解如何创建迁移集后，您现在就可以了解内容传输工具中的提取和摄取流程了。 在了解这些流程之前，您必须先查看 [处理大型内容存储库](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 显着加快内容传输活动的提取和摄取阶段，以将内容移动到AEMas a Cloud Service。
