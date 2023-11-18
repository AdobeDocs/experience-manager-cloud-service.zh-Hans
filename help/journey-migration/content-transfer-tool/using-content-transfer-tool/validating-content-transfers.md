---
title: 验证内容转移
description: 使用内容传输工具验证内容传输
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 2%

---

# 验证内容转移 {#validating-content-transfers}

## 快速入门 {#getting-started}

用户可以可靠地确定内容传输工具提取的所有内容是否已成功引入到目标实例中。 此验证功能的工作方式是，比较提取期间涉及的所有节点的路径摘要，以及提取期间涉及的所有节点的路径摘要。 如果提取摘要中包含的任何节点路径在摄取摘要中缺失，则验证被视为已失败，可能需要额外的手动验证。

>[!INFO]
>
>此功能将在内容传输工具(CTT)版本1.8.x发布后可用。 AEM Cloud Service目标环境必须至少运行版本6158或更高版本。 它还需要设置源环境才能运行 [预复制](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step). 验证功能在源上查找azcopy.config文件。 如果找不到此文件，将不会运行验证。 要了解有关如何配置azcopy.config文件的更多信息，请参阅 [此页面](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file).

验证内容传输是一项可选功能。 启用此功能将增加执行提取和摄取所需的时间。 要使用该功能，请在源AEM环境的System Console中启用该功能，请执行以下步骤：

1. 通过转到，导航到源实例上的Adobe Experience Manager Web Console **工具 — 操作 — Web控制台** 或直接访问位于的URL *https://serveraddress:serverport/system/console/configMgr*
1. 搜索 **内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用 **在提取期间启用迁移验证** 设置，然后按 **保存**：

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

如果启用此设置，并且目标AEM Cloud Service环境运行兼容版本，则在随后的所有提取和引入期间将进行迁移验证。

有关如何安装内容传输工具的更多信息，请参阅 [内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md).

## 如何验证内容传输 {#how-to-validate-a-content-transfer}

在源AEM环境中启用迁移验证后，开始提取。

如果 **提取期间覆盖暂存容器** 如果启用了，则与提取相关的所有节点都将记录到提取路径摘要中。 使用此设置时，请务必启用 **请擦除云实例上的现有内容后再引入** 在摄取期间设置，否则，摄取摘要中可能会显示缺少节点。 这些是先前摄取中在目标上已存在的节点。

有关这方面的图形说明，请参阅以下示例：

### 示例 1 {#example-1}

* **提取（覆盖）**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-01.png)

* **引入（擦除）**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **注释**

  此“覆盖”和“划出”的组合将产生一致的验证结果，即使对于重复摄取也是如此。

### 示例 2 {#example-2}

* **提取**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-03.png)

* **摄取**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **注释**

  此“覆盖”和“划出”的组合将为初始引入生成一致的验证结果。

  如果重复引入，则引入摘要为空，并且验证似乎已失败。 摄取摘要为空，因为此提取中的所有节点都将已存在于目标上。

提取完成后，开始引入。

摄取日志的顶部将包含一个条目，类似于 `aem-ethos/tools:1.2.438`. 确保此版本号为 **1.2.438** 或更高版本，否则您使用的AEMas a Cloud Service版本不支持验证。

完成摄取并开始验证后，将在摄取日志中记录以下日志条目：

```
Gathering artifacts for migration validation...
```

验证详细信息将在此条目之后。 请从下面的大迁移中找到示例：

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

这是已成功验证的示例，因为提取摘要中不存在缺失的条目。

要进行比较，下面显示了验证失败（或执行增补迁移）时验证报表的外观：

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
See our Migration Validation FAQ (https://www.adobe.com/go/aem_cloud_ctt_validation_en) or open a ticket with Customer Care.
There are 4635 entries present in the extraction digest that are missing from the ingestion digest.
/content/dam/bruce
/content/dam/bruce-assets
... more paths listed (up to 10k) ...
----------------------------------------------------------
Comparing the path digests took 0 seconds
Migration validation took 0 minutes
```

上述故障示例是通过运行引入来实现的，然后在禁用划出功能的情况下再次重新运行相同的引入，以便在引入期间不涉及节点 — 目标上已存在所有节点。

除了包含在摄取日志中，还可以从访问验证报告 **引入作业** Cloud Acceleration Manager中的用户界面。 为此，请单击三个圆点(**...**)，然后单击 **验证报告** ，以查看验证报告。


![图像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## 如何验证主体迁移 {#how-to-validate-principal-migration}

请参阅 [用户映射和主体迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md) 以了解主要迁移的详细信息以及为什么需要这样做。

成功完成提取和引入后，即可使用主体迁移的摘要和报告。 此信息可用于验证哪些用户和组已成功迁移，也许还可用于确定为什么有些用户和组没有迁移。

要查看此信息，请转到Cloud Acceleration Manager。 单击项目信息卡，然后单击内容传输信息卡。 导航到 **引入作业** 并找到要验证的引入。 单击三个圆点(**...**)进行摄取，然后单击 **查看主体摘要** 下拉菜单中。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

您会看到一个包含摘要信息的对话框。 使用帮助图标阅读更完整的说明。 单击 **下载报表** 按钮以下载完整的逗号分隔(CSV)报表。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

>[!NOTE]
>
>如果禁用了用户映射，则会显示此对话框的另一个变体。 它将指示用户映射已被禁用，并且不会显示给出用户映射值的3个字段。

## 疑难解答 {#troubleshooting}

### 验证失败. 现在该做什么？ {#validation-fail}

第一步是确定摄取是否真的失败，或者提取的内容是否已存在于目标环境中。 如果通过重复引入，则可能会发生这种情况 **请擦除云实例上的现有内容后再引入** 选项已禁用。

要进行验证，请从验证报表中选择一个路径，并检查该路径是否存在于目标环境中。 如果这是发布环境，则可能会限制您直接检查页面和资产。 如果您在此步骤中需要帮助，请向客户关怀部门提交工单。

### 节点数低于我的预期。 为什么？ {#node-count-lower-than-expected}

有意排除提取和摄取摘要中的某些路径，以保持这些文件的大小可控，目标是能够在摄取完成后的两小时内计算迁移验证结果。

我们当前从摘要中排除的路径包括： `cqdam.text.txt` 演绎版，内的节点 `/home`，以及中的节点 `/jcr:system`.

### 封闭用户组无法正常运行 {#validating-cugs}

请参阅 [迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) 有关使用封闭用户组(CUG)策略时的额外注意事项。
