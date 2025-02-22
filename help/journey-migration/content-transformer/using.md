---
title: 使用内容转换器
description: 了解如何转换内容结构为迁移到AEM as a Cloud Service做准备。
exl-id: 40516ff7-5686-42e6-bdd1-c9c6de432b09
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# 使用内容转换器 {#using-ct}

## 使用内容转换器的重要注意事项 {#imp-considerations-ct}

请阅读以下章节，以了解使用内容转换器(CT)的重要注意事项：

* 要使用Content Transformer，您必须先在Adobe Experience Manager (AEM)环境中运行最佳实践分析器。
* 虽然您可以在生产环境中运行内容转换器，但建议您在克隆的生产环境中运行内容转换器。 更重要的是，您需要确保BPA和CT在同一环境中运行。
* 您需要是您希望运行内容转换器的环境的管理员。
* 默认情况下，任何可以更改源内容的操作（移动/删除/重命名）都将在转换之前在`/etc/packages/content-transformation`下创建源路径的备份包。 尽管每个操作对话框都有一个禁用/启用备份包创建的选项，但严格建议始终选择启用包创建。
* 内容转换器中的每个页面都配置为列出最多50个查找结果，因此一次最多可以转换50个查找结果。 这样做是为了在UI上提供及时响应。

## 可用性 {#availability-ct}

内容转换器与[内容传输工具](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/getting-started-content-transfer-tool.md)捆绑在一起，该工具可以从软件分发门户以zip文件的形式下载。 您可以通过包管理器在源AEM实例上安装该包。

>[!NOTE]
>内容转换器在内容传输工具v2.0.20或更高版本中可用。

## 打开内容转换器 {#opening-ct}

1. 以管理员身份登录到源AEM实例，然后转到起始页：https://host:port/aem/start.html。
1. 导航到工具>操作>内容迁移

   ![图像](/help/journey-migration/content-transformer/assets/ct-1.png)

   >[!NOTE]
   > 确保您以前运行过BPA报表，并使用URL http://host:port/apps/best-practices-analyzer/content/BestPracticesReport.html进行验证

1. 单击标题为&#x200B;**BPA报告的内容转换器**&#x200B;的卡片

   ![图像](/help/journey-migration/content-transformer/assets/ct-2.png)

   下面是一个示例，说明BPA报告创建成功后以及发现内容相关问题后内容转换器概述页面的外观。

   BPA报告的剩余到期时间显示在侧边栏中。 建议使用最新的BPA报告运行内容转换器，以避免缺少任何与内容相关的发现。

   ![图像](/help/journey-migration/content-transformer/assets/ct-3.png)

1. 您可以根据`Pattern Code`、`Subtype`、`Importance`和`Source`筛选问题。

   ![图像](/help/journey-migration/content-transformer/assets/ct-4.png)

1. 您可以选择所有问题或特定问题，然后移动、移除或重命名以解决这些问题。 也可以使用右上角的&#x200B;**添加路径**&#x200B;按钮添加自定义路径。

   >[!NOTE]
   > 在使用移动操作时，建议将所有路径仅移动到一个文件夹（例如，在`/etc/packages/content-transformation/paths`下），因此，在安装备份包以将实例恢复到原始状态时，可以使用删除操作删除文件夹(`/etc/packages/content-transformation/paths`)以减小存储库大小。

   ![图像](/help/journey-migration/content-transformer/assets/ct-5.png)
   ![图像](/help/journey-migration/content-transformer/assets/ct-6.png)

   >[!NOTE]
   > 默认情况下，任何可以更改源内容的操作(`move`/`remove`/`rename`)都将在转换前在`/etc/packages/content-transformation`下创建源路径的备份包。 尽管每个操作对话框都有一个禁用/启用备份包创建的选项，但严格建议始终选择启用包创建。

1. 下面显示了为路径移动操作创建的备份包的示例，单击install以恢复源路径。 安装过程只会将源路径带回其原始位置，而不会删除在转换过程中移动它们的路径。 要删除所移动位置中的路径，请单击&#x200B;**添加路径**&#x200B;按钮以添加位置（例如，`/etc/packages/content-transformation/paths`），选择位置并单击&#x200B;**删除**。

   >[!CAUTION]
   > 请勿删除`/etc/packages/content-transformation`，因为这是备份包所在的位置。 只有在您确定不再需要这些包时，才能删除此位置以减小存储库大小。

   ![图像](/help/journey-migration/content-transformer/assets/ct-7.png)
   ![图像](/help/journey-migration/content-transformer/assets/ct-8.png)
