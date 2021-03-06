---
title: 内容传输工具快速入门（旧版）
description: 内容传输工具快速入门
hide: true
hidefromtoc: true
source-git-commit: 1fb4d0f2a3b3f9a27f5ab1228ec2d419149e0764
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 22%

---

# 内容传输工具快速入门（旧版） {#getting-started-content-transfer-tool}


## 可用性 {#availability}

内容传输工具可以从软件分发门户以zip文件的形式下载。 您可以通过 [包管理器](/help/implementing/developing/tools/package-manager.md) 在源Adobe Experience Manager(AEM)实例上。 确保下载最新版本。 有关最新版本的更多详细信息，请参阅 [发行说明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html?lang=zh-Hans).

>[!NOTE]
>从[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户下载内容传输工具。

## 源环境连接 {#source-environment-connectivity}

源AEM实例可能在防火墙后运行，在防火墙中，它只能访问已添加到允许列表的特定主机。 要成功运行提取，需要从运行AEM的实例访问以下端点：

* 目标AEMas a Cloud Service环境： `author-p<program_id>-e<env_id>.adobeaemcloud.com`
* Azure Blob存储服务： `*.blob.core.windows.net`
* 用户映射IO端点： `usermanagement.adobe.io`

要测试与目标AEMas a Cloud Service环境的连接，请从源实例的shell发出以下cURL命令(替换 `program_id`, `environment_id`和 `migration_token`):

`curl -i https://author-p<program_id>-e<environment_id>.adobeaemcloud.com/api/migration/migrationSet -H "Authorization: Bearer <migration_token>"`

>[!NOTE]
>如果 `HTTP/2 200` 已收到，连接到AEMas a Cloud Service成功。

## 运行内容传输工具 {#running-tool}

>[!VIDEO](https://video.tv.adobe.com/v/35460/?quality=12&learn=on)


请阅读以下章节，了解如何使用内容传输工具将内容迁移至 AEM as a Cloud Service （创作/发布）：

1. 选择Adobe Experience Manager并导航到工具 — > **操作** -> **内容迁移**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt01.png)

1. 选择 **内容传输** 选项自 **内容迁移** 向导。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt02.png)


1. 创建第一个迁移集时，将显示以下控制台。 单击&#x200B;**创建迁移集**&#x200B;以创建新的迁移集。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt03.png)

   >[!NOTE]
   >如果您有现有迁移集，控制台将显示现有迁移集的列表及其当前状态。


1. 填充 **创建迁移集** 屏幕，如下所述。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt04.png)

   1. **名称**：输入迁移集的名称。
      >[!NOTE]
      >迁移集名称不允许使用特殊字符。

   1. **Cloud Service 配置**：输入目标 AEM as a Cloud Service 作者 URL。

      >[!NOTE]
      >在内容传输活动期间，您一次最多可以创建和维护10个迁移集。
      >此外，您还必须为每个特定的环境（*暂存*、*开发*&#x200B;或&#x200B;*生产*）单独创建迁移。

   1. **访问令牌**：输入访问令牌。

      >[!NOTE]
      >您可以使用 **打开访问令牌** 按钮。 您需要确保属于目标Cloud Service实例中的“管理员”组。

   1. **参数**：选择以下参数以创建迁移集：

      1. **包含版本**：根据需要选择。包含版本时，路径 `/var/audit` 会自动包含在内以迁移审核事件。

         ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt05.png)

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

1. 您将在 **内容传输** 向导，如下图所示。

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt07.png)

   所有现有迁移集都显示在 **内容传输** 向导及其当前状态和状态信息。 您可能会看到下面描述的一些图标。

   * *红色云*&#x200B;表示您无法完成提取流程。
   * A *绿云* 表示您可以完成提取流程。
   * *黄色图标*&#x200B;表示您没有创建现有迁移集，而特定迁移集是由同一实例中的其他用户创建的。

1. 选择迁移集并单击 **属性** 查看或编辑迁移集属性。 在编辑属性时，无法更改 **迁移集名称** 或 **服务URL**.

   ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ctt06.png)

### 确定迁移集大小和磁盘空间 {#migration-set-size}

创建迁移集后，强烈建议在开始提取流程之前对迁移集运行大小检查。
通过对迁移集运行大小检查，您将能够：
* 确定 `crx-quickstart` 子目录成功完成提取。
* 确定迁移集大小是否在支持的产品限制范围内，并避免内容摄取失败。

请按照以下步骤运行大小检查：

1. 选择迁移集并单击 **检查大小**.

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image1.png)

1. 这将打开 **检查大小** 对话框。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image2.png)

1. 单击 **检查大小** 以启动该过程。 然后，您将返回到迁移集列表视图，并且您应会看到一条消息，指示 **检查大小** 正在运行。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image3.png)


1. 一次 **检查大小** 处理完成后，状态将更改为 **已完成**. 选择同一迁移集并单击 **检查大小** 查看结果。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image4.png)

   以下示例 **检查大小** 结果没有警告。

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image5.png)

1. 如果 **检查大小** 结果表明，磁盘空间不足和/或迁移集超出产品限制， **警告** 将显示状态。

![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image6.png)

以下示例 **检查大小** 结果中显示警告。

![图像](/help/journey-migration/content-transfer-tool/assets/CTT_CheckSize_image7.png)


## 接下来呢？ {#whats-next}

了解如何创建迁移集后，您现在便可以了解内容传输工具中的提取和摄取流程。 在了解这些流程之前，您必须先查看 [处理大型内容存储库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/handling-large-content-repositories.html?lang=en) 可显着加快内容传输活动的提取和摄取阶段，以将内容移动到AEMas a Cloud Service。
