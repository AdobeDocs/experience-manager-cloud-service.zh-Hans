---
title: 在发布实例（旧版）上运行内容传输工具
description: 在发布实例上运行内容转移工具
hide: true
hidefromtoc: true
exl-id: 0a699dc1-9977-4cf9-a1b0-7b503ea2fc69
source-git-commit: 22bbf15e33ab3d5608dc01ed293bb04b07cb6c8c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 4%

---

# 在发布实例（旧版）上运行内容传输工具 {#run-content-transfer-tool-publish-instance}

## 简介 {#introduction}

内容传输工具(CTT)在将内容从源实例传输到目标实例之前，不会执行任何类型的内容分析。 例如，CTT在将内容摄取到发布环境时，不会区分已发布和未发布的内容。 迁移集中指定的任何内容都将被摄取到所选目标实例中。 用户能够将迁移集摄取到创作实例或发布实例中，或同时摄取到两者中。

>[!NOTE]
>建议在将内容移动到生产实例时，在源创作实例上安装内容传输工具以将内容移动到目标创作实例，同样，在源发布实例上安装内容传输工具以将内容移动到目标发布实例。 请参阅 [推荐的方法](#recommended-approach) 部分以了解更多详细信息。

## 推荐的方法 {#recommended-approach}

按照如下所述的建议方法操作：

* 使用与创作实例中使用的内容传输工具的相同版本。

* 只需迁移一个发布节点。 应在开始提取之前从负载平衡器中删除该数据集。

* 创建迁移集时，请使用创作AEMas a Cloud Service环境的URL。

* 在摄取以发布期间，不会缩小发布层（与作者不同）。

   >[!IMPORTANT]
   >为防患于未然，请避免任何用户启动写操作，例如：
   > * 在该环境中从AEMas a Cloud Service作者到发布的内容分发
   > * 发布实例之间的用户同步

