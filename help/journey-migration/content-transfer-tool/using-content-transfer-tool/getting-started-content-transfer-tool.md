---
title: 内容转移工具快速入门
description: 了解如何开始使用内容传输工具
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
feature: Migration
role: Admin
source-git-commit: 67bc538fe174034c05808d4a62c51c404dfaf38c
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 16%

---

# 内容转移工具快速入门 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下载"
>abstract="可从软件分发门户下载 zip 文件形式的内容转移工具。可通过包管理器将该包安装在源 Adobe Experience Manager (AEM) 实例上。确保下载最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html" text="发行说明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="软件分发门户"

可从软件分发门户下载 zip 文件形式的内容转移工具。您可以通过源Adobe Experience Manager (AEM)实例上的[包管理器](/help/implementing/developing/tools/package-manager.md)安装该包。 确保下载最新版本。 有关最新版本的更多详细信息，请参阅[发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/release-notes/release-notes-current.html)。

仅支持版本2.0.0及更高版本，建议使用最新版本。

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## Source环境连接 {#source-environment-connectivity}

>[!NOTE]
>
>如果从Cloud Acceleration Manager中删除了迁移集，也可能会发生连接错误。

源AEM实例可能正在防火墙后面运行，在该防火墙中，它只能访问已添加到允许列表的特定主机。 要成功运行提取，需要从运行AEM的实例访问以下端点：

* Azure Blob存储服务： `casstorageprod.blob.core.windows.net`

>[!NOTE]
>如果提取由于以下错误而失败：“javax.net.ssl.SSLHandshakeException： sun.security.validator.ValidatorException： PKIX路径构建失败： sun.security.provider.certpath.SunCertPathBuilderException：无法找到请求的目标的有效证书路径”，则可以通过导入相关的CA证书来解决此问题。

### 启用SSL日志记录 {#enable-ssl-logging}

了解SSL/TLS连接问题有时可能很困难。 要对提取过程中的连接问题进行故障诊断，可通过源AEM环境的“系统控制台”启用SSL日志记录，步骤如下：

1. 通过转到&#x200B;**工具>操作> Web控制台**&#x200B;导航到源实例上的Adobe Experience Manager Web控制台，或直接导航到&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;上的URL
1. 搜索&#x200B;**内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用&#x200B;**为提取启用SSL日志记录**&#x200B;设置，然后按&#x200B;**保存**：

   ![图像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)

>[!NOTE]
>此标记仅用于调试SSL问题。 请确保在运行提取之前禁用该标志，因为它可能需要大量磁盘空间。 这可能会占用驱动器容量，并导致提取过程失败。

## 运行内容转移工具 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="运行内容转移工具"
>abstract="了解如何使用内容转移工具将内容迁移到 AEM as a Cloud Service（创作/发布）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 观看演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教程 - 使用内容转移工具"

以下部分适用于内容传输工具的新版本。 请阅读以下章节，了解如何使用内容传输工具将内容迁移到AEM as a Cloud Service：

### 提取设置阶段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取设置阶段"
>abstract="了解如何创建和管理迁移集以及如何复制提取密钥。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html#migration" text="教程 - 使用内容转移工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" must be added here -->

1. 登录Cloud Acceleration Manager (CAM)，然后单击之前创建的CAM项目，以评估您为迁移到AEM as a Cloud Service所做的准备工作。 如果尚未创建CAM项目，请参阅在CAM中创建和管理项目。

1. 单击&#x200B;**内容传输**&#x200B;卡以打开迁移集列表视图。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 通过单击&#x200B;**创建迁移集**&#x200B;创建迁移集。

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每个项目最多可以创建10个迁移集，包括过期的迁移集。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   将显示以下对话框。 请注意，迁移集将在长时间不活动后过期。 在项目信息卡和迁移作业表行上显示一段时间内的警告后，迁移集将过期，并且其数据将不再可用。 有关详细信息，请查看[迁移集过期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry)。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

   >[!NOTE]
   >
   >名称必须遵循与AEM节点相同的约定，因此不能包含以下任何字符： . / ： [ ] | *

1. 您现在应在列表视图中看到迁移列表。 选择三点符号(**...**)以打开下拉列表，然后选择&#x200B;**复制提取密钥**。 在提取阶段需要此密钥。 复制此提取密钥。

   >[!NOTE]
   >
   >通过提取密钥，您的源AEM环境可安全地连接到迁移集。 请像对待密码一样谨慎对待此密钥，切勿通过不安全的媒介（如电子邮件）共享此密钥。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填充迁移集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="填充迁移集"
>abstract="创建迁移集后，必须为它填入需从源实例移至 AEM as a Cloud Service 环境的内容。为此，必须在源实例上安装内容转移工具。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html#" text="提取内容"

要填充您在Cloud Acceleration Manager中创建的迁移集，请在源Adobe Experience Manager (AEM)实例上安装最新版本的内容传输工具。 要了解如何填充迁移集，请参阅此部分。

1. 在源Adobe Experience Manager实例上安装最新版本的内容传输工具后，转到&#x200B;**操作 — 内容迁移**

1. 单击&#x200B;**创建迁移集**。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 将之前从CAM复制的提取密钥粘贴到&#x200B;**创建迁移集**&#x200B;表单的提取密钥输入字段中。 执行此操作后，迁移集名称和Cloud Acceleration Manager (CAM)项目名称字段会自动填充。 这些名称应与CAM中的“迁移集”名称和您创建的CAM项目名称匹配。 您现在可以添加内容路径。 添加内容路径后，保存迁移集。 您可以使用包含或排除的版本运行提取。

   >[!NOTE]
   >
   >请确保提取密钥有效并且不在到期之前。 粘贴提取密钥后，您可以在&#x200B;**创建迁移集**&#x200B;对话框中获取此信息。 如果收到连接错误，请参阅[Source环境连接](#source-environment-connectivity)以了解更多信息。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接下来，选择以下参数以创建迁移集：

   1. **包含版本**：根据需要选择。 当包含版本时，将自动包含路径`/var/audit`以迁移审核事件。

      ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >如果您打算将版本包含在迁移集中，并使用`wipe=false`执行增补，则由于“内容传输工具”中的当前限制，必须禁用版本清除。 如果您希望启用版本清除，并且正在对迁移集执行增补，则必须作为`wipe=true`执行引入。


   1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。 路径选取器通过键入或选择接受输入。

      >[!IMPORTANT]
      >创建迁移集时，以下路径受到限制：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` （在CTT中允许选择某些`/etc`路径）

1. 填充&#x200B;**创建迁移集**&#x200B;详细信息屏幕中的所有字段后，单击&#x200B;**保存**。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 确定迁移集大小 {#migration-set-size}

创建迁移集后，强烈建议先对迁移集运行大小检查，然后再启动提取流程。
通过对迁移集运行大小检查，您能够：

* 确定`crx-quickstart`子目录中是否有足够的磁盘空间以成功完成提取。
* 确定迁移集大小是否在受支持的产品限制之内，并避免内容摄取失败。

按照以下步骤运行大小检查：

1. 选择一个迁移集，然后单击&#x200B;**检查大小**。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 这将打开&#x200B;**检查大小**&#x200B;对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 单击&#x200B;**检查大小**&#x200B;以启动进程。 然后，您将返回到迁移集列表视图，并且您应该会看到一条消息，指示&#x200B;**检查大小**&#x200B;正在运行。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. **检查大小**&#x200B;进程完成后，状态将更改为&#x200B;**已完成**。 选择相同的迁移集，然后单击&#x200B;**检查大小**&#x200B;以查看结果。 以下是&#x200B;**检查大小**&#x200B;结果无警告的示例。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 如果&#x200B;**检查大小**&#x200B;结果指示磁盘空间不足，或迁移集超出产品限制，或两者都超出，则会显示&#x200B;**警告**&#x200B;状态。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 后续内容 {#whats-next}

了解如何创建迁移集后，您现在就可以了解内容传输工具中的提取和摄取流程了。 在学习这些流程之前，您必须先查看[处理大型内容存储库](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md)，以显着加快内容传输活动的提取和摄取阶段，从而将内容移动到AEM as a Cloud Service。
