---
title: 验证内容转移
description: 使用内容传输工具验证内容传输
exl-id: a12059c3-c15a-4b6d-b2f4-df128ed0eea5
feature: Migration
role: Admin
source-git-commit: e1089810b3bf3db0cc440bb397e5549ade6eac37
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---


# 验证内容转移 {#validating-content-transfers}

## 快速入门 {#getting-started}

用户可以可靠地确定内容传输工具提取的所有内容是否已成功引入到目标实例中。 此验证功能的工作方式是，比较提取期间涉及的所有节点的路径摘要，以及提取期间涉及的所有节点的路径摘要。 如果提取摘要中包含的任何节点路径在摄取摘要中缺失，则验证被视为已失败，可能需要额外的手动验证。

>[!INFO]
>
>此功能将在内容传输工具(CTT)版本1.8.x发布后可用。 AEM Cloud Service目标环境必须至少运行版本6158或更高版本。 还需要设置源环境以运行[预复制](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#setting-up-pre-copy-step)。 验证功能在源上查找azcopy.config文件。 如果找不到此文件，将不会运行验证。 要了解有关如何配置azcopy.config文件的更多信息，请参阅[处理大型内容存储库 — 配置azcopy.config文件](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md#configure-azcopy-config-file)。

验证内容传输是一项可选功能。 启用此功能将增加执行提取和摄取所需的时间。 要使用该功能，请在源AEM环境的System Console中启用该功能，请执行以下步骤：

1. 通过转到&#x200B;**工具 — 操作 — Web控制台**&#x200B;导航到源实例上的Adobe Experience Manager Web控制台，或直接导航到&#x200B;*https://serveraddress:serverport/system/console/configMgr*&#x200B;上的URL
1. 搜索&#x200B;**内容传输工具提取服务配置**
1. 使用铅笔图标按钮编辑其配置值
1. 启用&#x200B;**在提取期间启用迁移验证**&#x200B;设置，然后按&#x200B;**保存**：

   ![图像](/help/journey-migration/content-transfer-tool/assets/CTTvalidation1.png)

如果启用此设置，并且目标AEM云服务环境运行兼容版本，则在随后的所有提取和引入期间将进行迁移验证。

有关如何安装内容传输工具的更多信息，请参阅[内容传输工具快速入门](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)。

## 如何验证内容传输 {#how-to-validate-a-content-transfer}

在源AEM环境中启用迁移验证后，开始提取。

如果启用了&#x200B;**在提取期间覆盖暂存容器**，则与提取相关的所有节点都将记录到提取路径摘要。 使用此设置时，请务必在摄取期间启用&#x200B;**在摄取之前擦除云实例上的现有内容**&#x200B;设置，否则摄取摘要中可能缺少节点。 这些是先前摄取中在目标上已存在的节点。

有关这方面的图形说明，请参阅以下示例：

### 示例 1 {#example-1}

* **提取（覆盖）**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/example1-extraction.png)

* **引入（擦除）**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-02.png)

* **注释**

  此“覆盖”和“划出”的组合将产生一致的验证结果，即使对于重复摄取也是如此。

### 示例 2 {#example-2}

* **提取**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/example2-extraction.png)

* **引入**

  ![图像](/help/journey-migration/content-transfer-tool/assets-ctt/validation-04.png)

* **注释**

  此“覆盖”和“划出”的组合将为初始引入生成一致的验证结果。

  如果重复引入，则引入摘要为空，并且验证似乎已失败。 摄取摘要为空，因为此提取中的所有节点都将已存在于目标上。

提取完成后，开始引入。

摄取日志的顶部将包含一个条目，类似于`aem-ethos/tools:1.2.438`。 请确保此版本号为&#x200B;**1.2.438**&#x200B;或更高版本，否则您使用的AEM as a Cloud Service版本不支持验证。

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

除了包含在引入日志中之外，还可以从Cloud Acceleration Manager中的&#x200B;**引入作业**&#x200B;用户界面访问验证报告。 为此，请单击三个圆点(**...**)，然后单击下拉列表中的&#x200B;**验证报告**&#x200B;以查看验证报告。


![图像](/help/journey-migration/content-transfer-tool/assets-ctt/CTTvalidationreportnew.png)

## 如何验证主体迁移 {#how-to-validate-group-migration}

请参阅[组迁移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)以了解主体迁移的详细信息以及为什么需要这样做。

成功完成提取和引入后，即可使用主体迁移的摘要和报告。 此信息可用于验证哪些组已成功迁移，也可用于确定为什么有些组没有迁移。

要查看此信息，请转到Cloud Acceleration Manager。 单击项目信息卡，然后单击内容传输信息卡。 导航到&#x200B;**引入作业**，并找到要验证的引入。 单击该摄取的三个圆点(**...**)，然后在下拉列表中单击&#x200B;**查看主体摘要**。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-action.png)

您会看到一个包含摘要信息的对话框。 使用帮助图标阅读更完整的说明。 单击&#x200B;**下载报表**&#x200B;按钮可下载完整的逗号分隔(CSV)报表。  另请注意，此报表末尾是用户报表，可用于迁移后的用户管理。

![图像](/help/journey-migration/content-transfer-tool/assets-ctt/ingestion-principal-dialog.png)

“Principal Migration”报告将报告：

* 每个组都已迁移，并且是第一个触发该组迁移的内容路径；该组可能还位于其他路径上，但只报告为给定组找到的第一个路径。 它还会报告是否在ACL或CUG策略中找到它。
* 每个组均未迁移，以及未迁移的原因。  通常，这可能是以下原因之一：
   * 它是一个内置组
   * 已在目标系统上
   * 它不在正在迁移的内容的ACL或CUG策略中
   * 它有一个重复的唯一字段（rep：principalName、rep：authorizableId、jcr：uuid或rep：externalId中的一个已在目标上，但所有这些字段都必须是唯一的）

## 疑难解答 {#troubleshooting}

### 验证失败。 现在怎么办？ {#validation-fail}

第一步是确定摄取是否真的失败，或者提取的内容是否已存在于目标环境中。 如果在禁用引入&#x200B;**选项之前重复引入，并且**&#x200B;擦除云实例上的现有内容，则可能会发生这种情况。

要进行验证，请从验证报表中选择一个路径，并检查该路径是否存在于目标环境中。 如果这是发布环境，则可能会限制您直接检查页面和资产。 如果您在此步骤中需要帮助，请向客户关怀部门提交工单。

### 节点数低于我的预期。 为什么？ {#node-count-lower-than-expected}

有意排除提取和摄取摘要中的某些路径，以保持这些文件的大小可控，目标是能够在摄取完成后的两小时内计算迁移验证结果。

我们当前从摘要中排除的路径包括： `cqdam.text.txt`演绎版、`/home`中的节点和`/jcr:system`中的节点。

### 已关闭的用户组 {#validating-cugs}

有关使用封闭用户组(CUG)策略时的额外注意事项，请参阅[迁移封闭用户组](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)。
