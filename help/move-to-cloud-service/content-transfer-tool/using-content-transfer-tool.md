---
title: 使用内容传输工具
description: 使用内容传输工具
translation-type: tm+mt
source-git-commit: f154ffacbeeee1993a9cc3bd3bd274be33dca7a7
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 1%

---


# 使用内容传输工具 {#using-content-transfer-tool}

## 使用内容传输工具的重要注意事项 {#pre-reqs}

请按照以下部分了解运行内容传输工具时的重要注意事项：

* 内容传输工具的最低系统要求是AEM 6.3 +和JAVA 8。 如果您使用的是较低版本的AEM，则需要将内容存储库升级到AEM 6.5，才能使用内容传输工具。

* 如果您使用沙 *箱环境*，请确保环境已升级到2020年5月29日版本或更高版本。 如果您使用的是 *生产环境*，它会自动更新。

* 要使用内容传输工具，您必须是源实例上的管理员用户，并且属于要将内容传输到的云服务实例中的管理组。 无权限用户将无法检索访问令牌以使用内容传输工具。

* 在提取阶段，内容传输工具将在活动AEM源实例上执行。

* 作 *者的摄取阶段* ，将缩小整个作者部署。 这意味着作者AEM在整个摄取过程中将不可用。

## 可用性 {#availability}

内容传输工具可从软件分发门户下载为zip文件。 您可以通过源Adobe Experience Manager(AEM)实例上的包管理器安装该包。

>[!NOTE]
>从Adobe Experience Cloud下载内 [容传输工具](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)。

## 运行内容传输工具 {#running-tool}

可查看本节以了解如何使用内容传输工具将内容作为云服务（作者／发布）迁移到AEM:

1. 选择Adobe Experience Manager并导航到工具->操 **作** ->内 **容传输**。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/content1.png)

1. 单击“ **创建迁移集** ”以创建新迁移集。 此时将显示 **内容迁移集详细信息** 。

   >[!NOTE]
   >您将视图此屏幕上的现有迁移集及其当前状态。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

1. 按如下所述填 **充“内容迁移集** ”详细信息屏幕中的字段。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/content-3.png)


   1. **名称**: 输入迁移集的名称。
      >[!NOTE]
      >迁移集名称不允许使用特殊字符。

   1. **云服务配置**: 输入目标AEM作为云服务作者URL。

      >[!NOTE]
      >在内容传输活动，您最多一次可以创建和维护四个迁移集。
      >此外，您还必须为每个特定环境(Stage、Development *或Production*) *单独*&#x200B;创建 *迁移*。

   1. **访问令牌**: 输入访问令牌。

      >[!NOTE]
      >您可以通过导航到，从创作实例检索访问令牌 `/libs/granite/migration/token.json`。

   1. **参数**: 选择以下参数以创建迁移集：

      1. **包括版本**: 根据需要进行选择。

      1. **要包含的路径**: 使用路径浏览器选择需要迁移的路径。

         >[!IMPORTANT]
         >创建迁移集时，以下路径受到限制：
         >* `/apps`
         >* `/libs`
         >* `/home`
         >* `/etc`


1. 在内 **容迁移** 集详细信息屏幕中填充所 **有字段后，单击保存** 。

1. 您将在“概述”页面视图 *迁移* 集。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img4.png)

   此屏幕上的所有现有迁移集都显示在“概 *述* ”页面上，并显示其当前状态和状态信息。

   * 红 *色云* 表示您无法完成提取过程。
   * 绿 *色云* 表示您可以完成提取流程。
   * 黄 *色图标* ，表示您未创建现有迁移集，特定迁移集由同一实例中的其他用户创建。

1. 从概述页面选择迁移集，然后单 **击属性** 以视图或编辑迁移集属性。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ctt-img6.png)

### 内容传输中的提取过程 {#extraction-process}

请按照以下步骤从内容传输工具提取迁移集：

1. 从“概述”页面选 *择迁移集* ，然后单 **击“提取** 到开始”提取。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. 将显 **示“迁移集提取** ”对话框，并单 **击“提取** ”以完成提取阶段。

   >[!NOTE]
   >您可以选择在提取阶段覆盖临时容器。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-2.png)

1. 现 **在，** 提取 **字段显示正在进** 行的提取进程的RUNNING状态。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-3.png)

   提取完成后，迁移状态将更新为“已完成 **** ”,INFO字 *段下将显* 示一个 **纯绿云** 图标。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-4.png)

   >[!NOTE]
   >您必须刷新页面才能视图更新的状态。
   >提取阶段启动后，将创建写锁定并在60秒后 *释放*。 因此，如果提取停止，您需要等待一分钟才能释放锁定，然后再次开始提取。

#### 向上提取 {#top-up-extraction-process}

内容传输工具具有支持不同内容的上调功能，在该功能中，仅传输自上一内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输后，建议在云服务上线之前，对不同内容进行频繁的补充，以缩短最终差异内容传输的内容冻结时间。

完成提取过程后，您可以使用向上提取方法传输增量内容。 按照以下步骤操作：

1. 导航到 *概述* 页，然后选择要对其执行顶部提取的迁移集。

1. 单 **击** “提取”以开始顶部提取。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extraction-img1.png)

1. 将显 **示“迁移集提取** ”对话框。

   >[!IMPORTANT]
   >您应禁用“在容器 **期间覆盖暂存提取** ”选项。
   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/extract-topup-1.png)

### 内容传输中的摄取过程 {#ingestion-process}

请按照以下步骤从内容传输工具中摄取迁移集：

1. 从“概述”页面选 *择迁移集* ，然后单 **击“将** 集收录到提取”。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. 将显 **示“迁移集** ”摄取对话框。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-2.png)

   出于演示目的，禁用“ **将内容收录到作者实例** ”选项。 可以同时将内容收录到“作者”和“发布”。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-3.png)

   单击“ **摄取** ”以完成摄取阶段。

1. 完成摄取后，AUTHOR INGESTION字段中的 **状态将更** 新 **为FINISHED** ,INFO下将显示一个纯绿 **云图标**。
   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-4.png)

   >[!NOTE]
   > 您必须刷新页面才能视图更新的状态。

#### 自上而上摄取 {#top-up-ingestion-process}

内容传输工具具有支持不同内容 *的自上而下的功* 能，在该功能中，仅传输自上一内容传输活动以来所做的更改。

>[!NOTE]
>初始内容传输后，建议在云服务上线之前，对不同内容进行频繁的补充，以缩短最终差异内容传输的内容冻结时间。

完成摄取过程后，您可以使用增量内容，方法为从上而上摄取。 按照以下步骤操作：

1. 导航到 *概述* 页，然后选择要为其执行顶部摄取的迁移集。

1. 单 **击** “摄取”以开始顶部提取。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-1.png)

1. 将显 **示“迁移集摄取** ”对话框。

   >[!NOTE]
   >您应禁用“ *擦除* ”选项，以防止从以前的摄取活动中删除现有内容。
   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/ingest-topup-1.png)

### 查看迁移集的日志 {#viewing-logs-migration-set}

您可以从“概述”页面视图现有迁移集 *的日* 志。
按照以下步骤操作：

1. 导航到 *概述* 页，选择要删除的迁移集，然后单击操 **作栏中的** 视图日志。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log1.png)

1. 将显 **示** “日志”对话框。 单击 **提取日志** ，以在新选项卡中视图日志。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log2.png)或，

   您还可以从概述屏幕视图迁移集 *的日* 志。 选择迁移集，然后单击“提取”字 **段下** 的状态。 在这种情况下，单击 **“完成** ”以在新选项卡中视图日志。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/view-log3.png)

### 删除迁移集 {#deleting-migration-set}

您可以从“概述”页面删除 *迁移集* 。
按照以下步骤操作：

1. 导航到 *概述* 页，选择要删除的迁移集，然后单击操 **作栏** 中的“删除”。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-1.png)

1. 单击 **从** “删除 **迁移集** ”对话框中删除以确认删除。

   ![图像](/help/move-to-cloud-service/content-transfer-tool/assets/delete-3.png)

## 疑难解答 {#troubleshooting}

### 缺少Blob ID {#missing-blobs}

如下所述，如果报告了缺失的blob ID，则需要在现有存储库中执行一致性检查并恢复缺失的blob。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

将执行以下命令

>[!NOTE]
> `--verbose` 报告引用blob的节点路径时需要标记。

**对于存储库AEM 6.5（Oak 1.8及更低版本）**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**对于Oak> 1.10的存储库**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

有关更多 [详细信息，请参](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) 阅Oak Runnable Jar。

然后，可以检查在上 *面指定的* OUT_DIR中创建的一致性文件，以查找缺少二进制文件的路径以及采取的适当操作，如从备份中恢复、删除路径、重新编制索引等。

### UI行为 {#ui-behavior}

作为用户，您可能会在内容传输工具的用户界面(UI)中看到以下行为更改：

* 用户为作者URL（开发／阶段／生产）创建迁移集，并成功执行提取和摄取。

* 然后，用户为同一作者URL创建新的迁移集，并对新迁移集执行提取和摄取。 UI显示第一个迁移集的摄取状态变为“失败 **”** ，并且没有可用日志。

* 这并不意味着第一个迁移集的摄取失败。 出现此行为是因为启动新的摄取作业时，它会删除以前的摄取作业。 因此，应忽略第一个迁移集上的更改状态。

* 内容传输工具UI中的图标可能与本指南中显示的屏幕截图有所不同，或者根本不会显示，具体取决于源AEM实例的版本。


