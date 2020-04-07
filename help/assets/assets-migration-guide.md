---
title: 资产迁移指南
description: 介绍如何将资产引入AEM、应用元数据、生成演绎版并激活资产以发布实例。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 26833f59f21efa4de33969b7ae2e782fe5db8a14

---


# 资产迁移指南 {#assets-migration-guide}

将资产迁移到AEM时，需要考虑几个步骤。 从当前主页提取资产和元数据不在本文档的范围内，因为实施之间差异很大，但本文档介绍如何将这些资产引入AEM、应用其元数据、生成演绎版并激活它们以发布实例。

## 前提条件 {#prerequisites}

在实际执行任何迁移步骤之前，请检查并实施性能调整指南。 许多步骤（如配置最大并发作业）都极大地提高了服务器在负载下的稳定性和性能。 在系统加载了资产后，其他步骤（如配置文件数据存储）更难执行。

>[!NOTE]
>
>以下资产迁移工具不是AEM的一部分，Adobe支持部门不支持这些工具：
>
>* ACS AEM Tools Tag Maker
>* ACS AEM工具CSV资产导入程序
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成工作流
>
>
These software are open source and covered by the [Apache v2 license](https://adobe-consulting-services.github.io/pages/license.html). To ask a question or report an issue, visit the respective [GitHub issues for ACS AEM tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) and [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## 迁移到AEM {#migrating-to-aem}

将资产迁移到AEM需要多个步骤，并应将其视为一个分阶段的过程。 迁移的阶段如下：

1. 禁用工作流。
1. 加载标记。
1. 摄取资源。
1. 处理再现。
1. 激活资产。
1. 启用工作流。

![chlimage_1-223](assets/chlimage_1-223.png)

### 禁用工作流 {#disabling-workflows}

在开始迁移之前，请禁用DAM更新资产工作流的启动程序。 最好将所有资产引入系统，然后批量运行工作流。 如果迁移期间您已经处于活动状态，则可以计划这些活动在非工作时间运行。

### 加载标记 {#loading-tags}

您可能已经拥有了要应用于图像的标记分类。 虽然CSV资产导入程序和AEM对元数据用户档案的支持等工具可以自动将标记应用到资产的过程，但这些标记需要加载到系统中。 通过 [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) （ACS AEM工具标记生成器）功能，您可以使用加载到系统中的Microsoft Excel电子表格填充标记。

### 摄取资源 {#ingesting-assets}

将资产引入系统时，性能和稳定性是重要的问题。 由于您要将大量数据加载到系统中，您需要确保系统能够正常运行，并尽可能减少所需的时间量并避免系统过载，这会导致系统崩溃，尤其是在已在生产中的系统中。

将资产加载到系统中有两种方法：使用HTTP的基于推送的方法，或使用JCR API的基于拉式的方法。

#### 通过HTTP推送 {#pushing-through-http}

Adobe的Managed Services团队使用一个名为Glutton的工具将数据加载到客户环境中。 Glutton是一个小的Java应用程序，它将所有资源从一个目录加载到AEM实例上的另一个目录中。 您还可以使用Perl脚本等工具将资源发布到存储库中，而不是Glutton。

使用通过https的方法有两个主要的缺点：

1. 资源需要通过HTTP传输到服务器。 这需要相当多的开销，并且耗时，从而延长执行迁移所需的时间。
1. 如果您有必须应用于资产的标记和自定义元数据，则此方法需要再运行一个自定义流程，以便在导入资产后将此元数据应用于资产。

获取资源的另一种方法是从本地文件系统中提取资源。 但是，如果无法将外部驱动器或网络共享装载到服务器以执行基于拉式的方法，则通过HTTP发布资产是最佳选项。

#### 从本地文件系统中提取 {#pulling-from-the-local-filesystem}

[ACS AEM工具CSV资产导入程序从文件系统中提取资产](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ，并从CSV文件中提取资产元数据以用于资产导入。 AEM Asset Manager API用于将资产导入系统并应用配置的元数据属性。 理想情况下，资产通过网络文件安装或通过外部驱动器安装在服务器上。

由于资产无需通过网络传输，因此总体性能显着提高，而且通常认为此方法是将资产加载到存储库中的最有效方法。 此外，由于该工具支持元数据摄取，因此您可以通过一个步骤导入所有资产和元数据，而不是通过另一个工具创建第二个步骤来应用元数据。

### 处理再现 {#processing-renditions}

在将资产加载到系统中后，您需要通过DAM更新资产工作流处理这些资产，以提取元数据并生成演绎版。 在执行此步骤之前，您需要重复和修改DAM更新资产工作流以满足您的需求。 开箱即用的工作流程包含许多您可能不需要的步骤，如Scene7 PTIFF生成或InDesign服务器集成。

根据需要配置工作流后，您有两个用于执行该工作流的选项：

1. 最简单的方法是 [ACS Commons的Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html)。 此工具允许您执行查询并通过工作流处理查询结果。 还有用于设置批大小的选项。
1. 您可以将 [ACS Commons Fast Action Manager与Synthetic Workflows一起使](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) 用 [](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)。 虽然此方法涉及的范围更广，但它允许您在优化服务器资源的使用时删除AEM工作流引擎的开销。 此外，Fast Action manager还通过动态监视服务器资源和限制系统上的负载来进一步提升性能。 ACS Commons功能页上提供了示例脚本。

### 激活资产 {#activating-assets}

对于具有发布层的部署，您需要将资产激活到发布场。 虽然Adobe建议运行多个发布实例，但最好将所有资源复制到单个发布实例，然后克隆该实例。 在激活大量资产时，在触发树状激活后，您可能需要进行干预。 原因如下：在触发激活时，项目会添加到Sling作业／事件队列。 当此队列的大小开始超过约40,000个项目后，处理速度会显着降低。 当此队列的大小超过100,000项后，系统稳定性将受到开始。

要解决此问题，您可以使用 [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) （快速操作管理器）管理资产复制。 这可以在不使用Sling队列的情况下工作，从而降低开销，同时限制工作负载以防止服务器过载。 使用FAM管理复制的示例显示在该功能的文档页上。

将资产转至发布场的其他选项包括使用 [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) 或 [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)，这些选项作为 Jackrabbit 中的工具提供。另一个选项的目的是对 AEM 基础结构使用一个名为 [Grabbit](https://github.com/TWCable/grabbit) 的开放源工具，该工具声称比 vlt 的性能更快。

对于任何这些方法，注意作者实例上的资产不显示为已激活。 要使用正确的激活状态标记这些资产，您还需要运行一个脚本以将资产标记为已激活。

>[!NOTE]
>
>Adobe不维护或支持Grabbit。

### 克隆发布 {#cloning-publish}

在激活资产后，您可以克隆发布实例以创建部署所需数量的副本。 克隆服务器相当简单，但需要记住一些重要步骤。 要克隆发布，请执行以下操作：

1. 备份源实例和数据存储。
1. 将实例和数据存储的备份恢复到目标位置。 以下步骤均引用此新实例。
1. Perform a filesystem search under `crx-quickstart/launchpad/felix` for `sling.id`. 删除此文件。
1. 在数据存储的根路径下，找到并删除任何文 `repository-XXX` 件。
1. 编 `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 辑并 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` 指向新环境上数据存储区的位置。
1. 开始环境。
1. 更新作者上任何复制代理的配置，以指向新实例上的正确发布实例或调度程序刷新代理，以指向新环境的正确调度程序。

### 启用工作流 {#enabling-workflows}

完成迁移后，应重新启用DAM更新资产工作流的启动程序，以支持再现生成和元数据提取，以便持续使用日常系统。

## 跨AEM实例迁移 {#migrating-between-aem-instances}

虽然不像以前那样常见，但有时您需要将大量数据从一个AEM实例迁移到另一个实例；例如，当您执行AEM升级、升级硬件或迁移到新数据中心时，例如AMS迁移。

在这种情况下，您的资产已填充元数据，并且已生成演绎版。 您只需将精力集中在将资产从一个实例移动到另一个实例上。 在AEM实例之间迁移时，您需要执行以下步骤：

1. 由于您正在迁移演绎版以及我们的资产，因此您希望禁用DAM更新资产的工作流启动器。

1. 由于已在源AEM实例中加载了标记，因此您可以在内容包中构建这些标记并将该包安装在目标实例上。

1. 建议使用两种工具将资产从一个AEM实例移至另一个AEM实例：

   * **Vault Remote Copy**（或vlt rcp）允许您跨网络使用vlt。 您可以指定源目录和目标目录，vlt从一个实例下载所有存储库数据并将其加载到另一个实例中。 Vlt rcp在https://jackrabbit.apache.org/filevault/rcp.html上有相关 [文档](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** 是Time Warner Cable为其AEM实施开发的一个开源内容同步工具。 由于它使用连续的数据流，与vlt rcp相比，它具有更低的延迟，并声称速度比vlt rcp快2到10倍。 Grabbit还支持仅同步Delta内容，这允许它在初始迁移通过完成后同步更改。

1. 按照说明激活 [记录到](#activating-assets) AEM的初始迁移资产。

1. 与新迁移一样，加载单个发布实例并克隆它比激活两个节点上的内容更有效。 请参阅 [仿制发布。](#cloning-publish)

1. 完成迁移后，请重新启用DAM更新资产工作流的启动程序，以支持再现生成和元数据提取，以便持续使用日常系统。
