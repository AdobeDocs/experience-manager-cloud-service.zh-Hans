---
title: 添加生产管道
description: 添加生产管道
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---


# 创建生产管道 {#create-production-pipeline}

在使用[!UICONTROL Cloud Manager] UI设置程序并至少有一个环境后，您就可以设置部署管道了。

请按照以下步骤配置管道的行为和首选项：

1. 单击&#x200B;**设置管道**&#x200B;以设置和配置管道。

   ![](assets/set-up-pipeline1.png)

1. 此时将显示&#x200B;**设置管道**&#x200B;屏幕。 选择分支并单击&#x200B;**Next**。

   ![](assets/setup-1.png)

1. 配置部署选项。

   ![](assets/setup-pipeline.png)

   您可以定义启动管道的触发器：

   * **手动**  — 使用UI手动启动管道。
   * **在Git更改中**  — 每当向配置的git分支添加提交时，都会启动CI/CD管道。即使选择此选项，也始终可以手动启动管道。

   在管道设置或编辑期间，部署管理器可以选择在任何质量门中遇到重要故障时定义管道的行为。

   这对于希望实现更自动化流程的客户非常有用。 可用选项包括：

   * **每次提问**  — 这是默认设置，需要对任何重要故障进行手动干预。
   * **立即取消**  — 如果选中此选项，则每当发生重要故障时，管道都将被取消。这实质上是在模拟用户手动拒绝每个故障。
   * **立即批准**  — 如果选中此选项，则每当发生重要故障时，管道将自动继续。这实质上是在模拟用户手动批准每次失败。


1. 生产管道设置包含第三个选项卡，标记为&#x200B;**体验审核**。 此选项为应始终包含在体验审核中的URL路径提供了一个表。

   >[!NOTE]
   >必须单击&#x200B;**添加新页面**&#x200B;以定义您自己的自定义链接。

   ![](assets/setup-3.png)

   单击&#x200B;**添加新页面**&#x200B;以提供要包含在体验审核中的URL路径。

   例如，如果要在体验审核中包含`https://wknd.site/us/en/about-us.html`，请在此字段中输入路径`us/en/about-us.html`，然后单击&#x200B;**Save**。

   ![](assets/exp-audit4.png)

   表中显示的URL将为：

   `https://publish-p14253-e43686.adobeaemcloud.com/us/en/about-us.html`

   ![](assets/exp-audit5.png)

   最多可包含25行。 如果用户在此部分中未提交页面，则默认情况下网站的主页将包含在体验审核中。

   有关更多详细信息，请参阅[了解体验审核结果](/help/implementing/cloud-manager/experience-audit-testing.md)。

   >[!NOTE]
   > 将配置的页面提交到服务，并根据性能、辅助功能、SEO（搜索引擎优化）、最佳实践和PWA（渐进式Web应用程序）测试进行评估。

1. 单击&#x200B;**编辑管道**&#x200B;屏幕中的&#x200B;**保存**。 现在， **概述**&#x200B;页面会显示&#x200B;**部署程序**&#x200B;卡。 单击&#x200B;**部署**&#x200B;按钮以部署程序。

   ![](assets/configure-pipeline5.png)

