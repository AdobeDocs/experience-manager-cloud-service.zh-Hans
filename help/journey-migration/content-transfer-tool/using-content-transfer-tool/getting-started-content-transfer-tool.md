---
title: 内容传输工具快速入门
description: 内容传输工具快速入门
exl-id: c0cecf65-f419-484b-9d55-3cbd561e8dcd
source-git-commit: 7bebdff5095786005d5c4c91b7b699d71f9813a7
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 9%

---

# 内容传输工具快速入门 {#getting-started-content-transfer-tool}


## 可用性 {#availability}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_download"
>title="下载"
>abstract="内容传输工具可以从软件分发门户以zip文件的形式下载。 您可以通过包管理器在源 Adobe Experience Manager (AEM) 实例上安装该包。确保下载最新版本。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html" text="发行说明"
>additional-url="https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html" text="软件分发门户"

内容传输工具可以从软件分发门户以zip文件的形式下载。 您可以通过 [包管理器](/help/implementing/developing/tools/package-manager.md) 在源Adobe Experience Manager(AEM)实例上。 确保下载最新版本。 有关最新版本的更多详细信息，请参阅 [发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans).

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 源环境连接 {#source-environment-connectivity}

>[!NOTE]
>
>如果从Cloud Acceleration Manager中删除了迁移集，则也会发生连接错误。

源AEM实例可能在防火墙后运行，在防火墙中，它只能访问已添加到允许列表的特定主机。 要成功运行提取，需要从运行AEM的实例访问以下端点：

* 目标AEMas a Cloud Service环境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure Blob存储服务： `*.blob.core.windows.net`
* 用户映射IO端点： `usermanagement.adobe.io`

要测试与目标AEMas a Cloud Service环境的连接，请从源实例的shell发出以下cURL命令(替换 `program_id`, `environment_id`和 `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>如果 `HTTP/2 200` 已收到，连接到AEMas a Cloud Service成功。

### 启用SSL日志记录 {#enable-ssl-logging}

了解SSL/TLS连接问题有时可能会很困难。 要在提取过程中排除连接问题，您可以通过源AEM环境的系统控制台启用SSL日志记录，方法如下：

1. 导航到源实例上的Adobe Experience Manager Web控制台，方法是转到 **工具 — 操作 — Web控制台** 或直接转到URL( *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用 **启用ssl日志记录以进行提取** 设置，然后按 **保存**:

   ![图像](/help/journey-migration/content-transfer-tool/assets/enable_ssl_logging.png)


## 运行内容传输工具 {#running-tool}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_demo"
>title="运行内容传输工具"
>abstract="了解如何使用内容传输工具将内容迁移到AEMas a Cloud Service（创作/发布）。"
>additional-url="https://video.tv.adobe.com/v/35460/?quality=12&amp;learn=on" text=" 请参阅演示"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用内容传输工具"

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)
<!-- Need to remove the video -->

以下部分适用于新版本的内容传输工具。 请阅读本节内容，了解如何使用内容传输工具将内容迁移到AEMas a Cloud Service:

### 提取设置阶段 {#extraction-setup-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_extraction_setup"
>title="提取设置阶段"
>abstract="了解如何创建迁移集并复制提取密钥。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/migration/content-transfer-tool.html?lang=en#migration" text="教程 — 使用内容传输工具"

<!-- Contextualhelp id "aemcloud_ctt_extraction_setup" needs to be added here -->

1. 登录到Cloud Acceleration Manager(CAM)，然后单击您之前创建的CAM项目，以评估您迁移到AEMas a Cloud Service的准备情况。 如果尚未创建CAM项目，请参阅在CAM中创建和管理项目。

1. 单击 **内容传输** 卡。 这会将您转到迁移集列表视图。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam1.png)

1. 通过单击 **创建迁移集**.

   >[!NOTE]
   >
   >在Cloud Acceleration Manager中，每个项目最多可以创建5个迁移集。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam2.png)

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam3.png)

1. 现在，您应该会在列表视图中看到迁移列表。 单击三个圆点符号(**...**)打开下拉菜单，然后单击 **复制提取键值**. 在提取阶段，您将需要此键值。 复制此提取键值。

   >[!NOTE]
   >
   >利用提取密钥，源AEM环境可安全地连接到迁移集。 请像使用密码一样小心地使用此密钥，并且切勿通过电子邮件等不安全的媒介共享此密钥。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam4.png)

### 填充迁移集 {#populating-the-migration-set}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_populate_migrationset"
>title="Populate Migration Set&quot; abstract=&quot;创建迁移集后，需要使用源实例中需要移动到AEMas a Cloud Service环境的内容进行填充。 为此，需要在源实例上安装内容传输工具。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/extracting-content.html" text="提取内容"

要填充在Cloud Acceleration Manager中创建的迁移集，您需要在源Adobe Experience Manager(AEM)实例上安装最新版本的内容传输工具。 请阅读本节内容，了解如何填充迁移集。

1. 在源Adobe Experience Manager实例上安装最新版本(v2.0.10)的内容传输工具后，转到 **操作 — 内容迁移**

1. 单击 **创建迁移集**

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam5.png)

1. 将之前从CAM复制的提取键粘贴到的提取键输入字段中 **创建迁移集** 表单。 执行此操作后，将自动填充迁移集名称和Cloud Acceleration Manager(CAM)项目名称字段。 这些名称应与CAM中的迁移集名称和您创建的CAM项目名称匹配。 您现在可以添加内容路径。 添加内容路径后，您将能够保存迁移集。 您可以运行包含或排除的版本提取。

   >[!NOTE]
   >
   >确保提取键值有效且未接近其过期时间。 您可以在 **创建迁移集** 对话框。 如果出现连接错误，请参阅 [源环境连接](#source-environment-connectivity) 以了解更多信息。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam6.png)

1. 接下来，选择以下参数以创建迁移集：

   1. **包含版本**：根据需要选择。包含版本时，路径 `/var/audit` 会自动包含在内以迁移审核事件。

      ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam7.png)

      >[!NOTE]
      >如果您打算将版本作为迁移集的一部分，并且要通过 `wipe=false`，则由于内容传输工具中的当前限制，您必须禁用版本清除。 如果您希望保持启用版本清除，并在迁移集中执行增补，则必须将摄取作为 `wipe=true`.


   1. **要包含的路径**：使用路径浏览器选择需要迁移的路径。路径选取器通过键入或选择接受输入。

      >[!IMPORTANT]
      >创建迁移集时，以下路径受到限制：
      >* `/apps`
      >* `/libs`
      >* `/home`
      >* `/etc` (部分 `/etc` 允许在CTT中选择路径)


1. 单击 **保存** 填充 **创建迁移集** 详细信息屏幕。

<!-- 1. You will view your migration set in the **Content Transfer** wizard, as shown in the figure below.

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   All the existing migration sets are displayed on the **Content Transfer** wizard with their current status and status information. You may see some of these icons described below.

   * A *red cloud* indicates that you cannot complete the extraction process.
   * A *green cloud* indicates that you can complete the extraction process.
   * A *yellow icon* indicates that you did not create the existing migration set and the specific one is created by some other user in the same instance.

1. Select a migration set and click on **Properties** to view or edit the migration set properties. While editing properties, it is not possible to change the **Migration Set name** or the **Service URL**. 

   ![image](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png) -->

### 确定迁移集大小 {#migration-set-size}

创建迁移集后，强烈建议在开始提取流程之前对迁移集运行大小检查。
通过对迁移集运行大小检查，您将能够：
* 确定 `crx-quickstart` 子目录成功完成提取。
* 确定迁移集大小是否在支持的产品限制范围内，并避免内容摄取失败。

请按照以下步骤运行大小检查：

1. 选择迁移集并单击 **检查大小**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam8.png)

1. 这将打开 **检查大小** 对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam9.png)

1. 单击 **检查大小** 以启动该过程。 然后，您将返回到迁移集列表视图，并且您应会看到一条消息，指示 **检查大小** 正在运行。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam10.png)

1. 一次 **检查大小** 进程完成，状态将更改为 **已完成**. 选择同一迁移集并单击 **检查大小** 查看结果。 以下示例 **检查大小** 结果没有警告。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam11.png)

1. 如果 **检查大小** 结果表明，磁盘空间不足和/或迁移集超出产品限制， **警告** 将显示状态。

<!--   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)
   
   Below is an example of **Check Size** results with warnings.
 
   ![image](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png) -->


## 下一步 {#whats-next}

了解如何创建迁移集后，您现在便可以了解内容传输工具中的提取和摄取流程。 在了解这些流程之前，您必须先查看 [处理大型内容存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 可显着加快内容传输活动的提取和摄取阶段，以将内容移动到AEMas a Cloud Service。
