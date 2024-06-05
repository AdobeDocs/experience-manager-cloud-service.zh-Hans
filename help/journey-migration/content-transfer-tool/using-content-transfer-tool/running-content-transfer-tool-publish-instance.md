---
title: 在发布实例上运行内容转移工具
description: 在发布实例上运行内容转移工具
exl-id: 01faab94-a939-4004-b094-e9eb8f67b96e
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 11%

---

# 在发布实例上运行内容转移工具 {#run-content-transfer-tool-publish-instance}

## 简介 {#introduction}

在将内容从源实例传输到目标实例之前，内容传输工具(CTT)不执行任何类型的内容分析。 例如，将内容摄取到Publish环境时，CTT不区分已发布和未发布的内容。 迁移集中指定的任何内容都将摄取到所选的目标实例中。 用户能够将迁移集摄取到创作实例和/或发布实例中。

>[!NOTE]
>建议在将内容移动到生产实例时，在源作者实例上安装内容传输工具以将内容移动到目标作者实例，同样，在源发布实例上安装内容传输工具以将内容移动到目标发布实例。 请参阅 [推荐的方法](#recommended-approach) 部分，以了解更多详细信息。

## 推荐的方法 {#recommended-approach}

请遵循下述建议方法：

* 使用在创作实例上使用的相同版本的内容传输工具。

* 只能迁移单个发布节点。 应在开始提取之前将其从负载平衡器中移除。

* 在引入以发布期间，发布层不会按比例缩小（与作者不同）。

  >[!IMPORTANT]
  >作为预防措施，请避免任何用户启动的写入操作，例如：
  > * 从AEMas a Cloud Service创作环境分发内容以在该环境中发布
  > * 发布实例之间的用户同步
