---
title: 使用内容传输工具
description: 使用内容传输工具
exl-id: a19b8424-33ab-488a-91b3-47f0d3c8abf5
source-git-commit: 5b569ab1b1cca7e5ec46b872f8726fddfc8b8d14
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 57%

---

# 使用内容传输工具 {#using-content-transfer-tool}

## 在发布实例上运行内容传输工具 {#running-ctt-on-publish}

建议在将内容移动到发布实例时，在源发布实例上安装CTT，以将内容移动到目标发布实例。 按照如下所述的建议方法操作：

* 使用在创作实例中使用的相同版本的CTT。

* 只需迁移一个发布节点。 应在开始提取之前从负载平衡器中删除该数据集。

* 创建迁移集时，请使用创作AEMaCS环境的URL。

* 在摄取到发布期间，不会缩小发布层（与作者不同）。 为防患于未然，请避免任何用户启动写操作，例如：

   * 从AEMaaCS创作到在该环境中发布的内容分发
   * 发布实例之间的用户同步


## 疑难解答 {#troubleshooting}

### 缺少 Blob ID {#missing-blobs}

如果报告缺少的 Blob ID（如下所述），则表明需要在现有存储库中执行一致性检查并还原缺少的 Blob。
`ERROR o.a.j.o.p.b.AbstractSharedCachingDataStore - Error retrieving record [ba45c53f8b687e7056c85dceebf8156a0e6abc7e]`

执行以下命令

>[!NOTE]
>
>`--verbose`标记在报告从中引用 Blob 的节点路径时需要使用。

**对于存储库 AEM 6.5（Oak 1.8 及更低版本）**

```shell
java -jar oak-run.jar datastorecheck --consistency --store [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds] <DATASTORE_CFG> --verbose <OUT_DIR> --dump
```

**对于拥有 Oak 1.10 以上版本的存储库**

```shell
java -jar oak-run.jar datastore --check-consistency [<SEGMENT_STORE_PATH>|<MONGO_URI>] --[s3ds|fds|azureds] <DATASTORE_CFG> --out-dir <OUT_DIR> --work-dir <TEMP_DIR> --verbose
```

有关更多详细信息，请参阅 [Oak Runnable Jar](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)。

可以检查在上述指定 *OUT_DIR* 中为保持一致性而创建的文件是否存在缺少二进制文件的路径，以及是否执行了相应操作，例如从备份中还原、删除路径、重建索引等。


### UI 行为 {#ui-behavior}

作为用户，您可能会在内容传输工具的用户界面 (UI) 中看到以下行为更改：

* 内容传输工具 UI 中的图标可能与本指南中显示的屏幕截图有所不同，也可能根本不显示，这取决于源 AEM 实例的版本。
