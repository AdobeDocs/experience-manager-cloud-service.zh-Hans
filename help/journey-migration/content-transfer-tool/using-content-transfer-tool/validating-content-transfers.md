---
title: 验证内容传输
description: 使用内容传输工具验证内容传输
source-git-commit: c542b631a94b9fcbda4790ca9ca5a461d104c790
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 2%

---


# 验证内容传输 {#validating-content-transfers}

## 快速入门 {#getting-started}

用户能够可靠地确定是否已将内容传输工具提取的所有内容成功摄取到目标实例。 此验证功能的工作方式是比较提取过程中涉及的节点的摘要和摄取过程中涉及的节点的摘要。 如果提取摘要中包含的任何节点路径在摄取摘要中缺失，则验证会被视为失败，可能需要进行额外的手动验证。

>[!INFO]
>
>此功能将自内容传输工具(CTT)版本1.8.x起提供。 AEM Cloud Service目标环境必须至少运行版本6158或更高版本。 它还要求设置源环境以运行 [预拷贝](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). 验证功能在源上查找azcopy.config文件。 如果找不到此文件，则不会运行验证。 要详细了解如何配置azcopy.config文件，请参阅 [本页](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

验证内容传输是一项可选功能。 启用此功能将增加执行提取和摄取所花费的时间。 要使用该功能，请按照以下步骤在源AEM环境的系统控制台中启用该功能：

1. 导航到源实例上的Adobe Experience Manager Web控制台，方法是转到 **工具 — 操作 — Web控制台** 或直接转到URL( *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用 **在提取期间启用迁移验证** 设置，然后按 **保存**:

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

启用此设置后，并且目标AEM Cloud Service环境运行的是兼容版本，则将在后续的所有提取和摄取期间进行迁移验证。

有关如何安装内容传输工具的更多信息，请参阅 [内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## 如何验证内容传输 {#how-to-validate-a-content-transfer}

在源AEM环境中启用迁移验证后，开始提取。

如果 **在提取期间覆盖暂存容器** 启用后，所有与提取相关的节点都将记录到提取路径摘要中。 使用此设置时，务必要启用 **摄取前擦除云实例上的现有内容** 在摄取期间进行设置，否则，可能会显示摄取摘要中缺少节点。 这些节点是以前摄取的目标上已存在的节点。

有关此示例的图形说明，请参阅以下示例：

### 示例1 {#example-1}

* **提取（覆盖）**

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTextractionoverwrite.png)

* **摄取（划出）**

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTingestionwipe.png)

* **注释**

   “覆盖”和“划出”的这种组合将产生一致的验证结果，即使重复摄取也是如此。

### 示例2 {#example-2}

* **提取**

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTextraction.png)

* **摄取**

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTingestion.png)

* **注释**

   “覆盖”和“划出”的这种组合，将产生一致的初始摄取验证结果。

   如果重复摄取，则摄取摘要将为空，并且验证似乎失败。 摄取摘要将为空，因为此提取中的所有节点都将存在于目标上。

提取完成后，开始摄取。

摄取日志的顶部将包含一个条目，类似于 `aem-ethos/tools:1.2.438`. 确保此版本号为 **1.2.438** 或更高版本，否则您使用的AEMas a Cloud Service版本不支持验证。

完成摄取并开始验证后，将在摄取日志中记录以下日志条目：

```
Gathering artifacts for migration validation...  
```

验证的详细信息将遵循此条目。 请查找以下大型迁移示例：

```
Beginning publish migration validation. Migration job id=[3aba1f96-84b6-4bd0-8642-c61c0d528387]
Extraction path digest is being processed...
Extraction path digest processing took 982 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 999 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 51674784
INGESTION: Number of nodes ingested: 51674784
----------------------------------------------------------
Validation succeeded! No entries were detected to be missing from the ingestion digest.
----------------------------------------------------------
Comparing the path digests took 29 seconds
Migration validation took 33 minutes
```

这是验证成功的示例，因为提取摘要中不存在摄取摘要中缺少的条目。

要进行比较，请看验证报表在验证失败时的外观：

```
Beginning publish migration validation. Migration job id=[ac217e5a-a08d-4e81-cbd6-f39f88b174ce]
Extraction path digest is being processed...
Extraction path digest processing took 0 seconds
Ingestion path digest is being processed...
Ingestion path digest processing took 0 seconds
Comparing the Extraction and Ingestion path digests...
----------------------------------------------------------
EXTRACTION: Number of nodes extracted: 4635
INGESTION: Number of nodes ingested: 0
----------------------------------------------------------
Validation failed. However, the following nodes may already be present in the target environment.
Please refer to our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上述失败示例是通过运行摄取，然后在禁用划出的情况下再次运行同一摄取来实现的，这样在摄取期间就不涉及任何节点 — 目标上已存在所有内容。

除了包含在摄取日志中之外，还可以从内容传输工具用户界面访问验证报表。 要执行此操作，请选择迁移集，然后单击 **验证** 按钮：


![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidatebutton.png)

将打开验证日志对话框：

![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidationlogs.png)

使用 **验证发布/创作报表** 按钮以查看最近向目标环境的给定层摄取的验证报表。 请参阅下面来自小型发布摄取的示例：

![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidationreport.png)

>[!NOTE]
>
>的 **验证发布/创作报表** 摄取完成后，将显示链接。 此外，验证报表会保留，以便不会像摄取日志那样在摄取完成后过期。

## 疑难解答 {#troubleshooting}

### 验证失败。现在该做什么？ {#validation-fail}

第一步是确定摄取是否确实失败，或提取的内容是否已存在于目标环境中。 如果重复使用 **摄取前擦除云实例上的现有内容** 选项已禁用。

要进行验证，请从验证报表中选择一个路径，并检查该路径是否存在于目标环境中。 如果这是发布环境，则您可能只能直接检查页面和资产。 如果您需要此步骤的帮助，请与客户关怀部门打开票证。

### 节点计数低于我预期的值。 为什么？ {#node-count-lower-than-expected}

有目的地排除提取和摄取摘要中的某些路径，以便保持这些文件的大小可管理，其目标是能够在摄取完成后的两小时内计算迁移验证结果。

我们当前从摘要中排除的路径包括： `cqdam.text.txt` 演绎版，节点在 `/home`和中的节点 `/jcr:system`.




