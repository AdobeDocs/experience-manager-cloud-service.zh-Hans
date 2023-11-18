---
title: 异步作业
description: Adobe Experience Manager通过以后台操作方式异步完成某些资源密集型任务来优化性能。
exl-id: 9c5c4604-1290-4dea-a14d-08f3ab3ef829
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 70%

---

# 异步操作 {#asynchronous-operations}

为了减少对性能的负面影响，AdobeExperience Manger将某些长时间运行且资源密集型操作异步作为后台操作来处理。 异步处理包括将多个作业排入队列，并以序列方式运行它们，但受到系统资源可用性的限制。

这些操作包括：

* 删除许多资产
* 移动许多资产或包含许多引用的资产
* 批量导出/导入资产元数据
* 从远程 Experience Manager 部署获取超过阈值限制设置的资产
* 转出 Live Copy

您可以从以下位置查看异步作业的状态 **[!UICONTROL 后台操作]** 仪表板位置 **全局导航** > **工具** > **常规** > **作业**.

>[!NOTE]
>
>默认情况下，异步作业并行运行。如果 *`n`* 是 CPU 核心的数量，则默认情况下，*`n/2`* 作业可以并行运行。要对作业队列使用自定义设置，请从 Web 控制台修改&#x200B;**[!UICONTROL 异步操作默认队列配置]**&#x200B;和&#x200B;**异步操作页面移动和转出配置**。
>
>有关更多信息，请参阅[队列配置](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations)。

## 监测异步操作的状态 {#monitor-the-status-of-asynchronous-operations}

每当 AEM 异步处理操作时，您都会在[收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)中通过电子邮件收到通知（如果已启用）。

要查看异步操作状态的详细信息，请导航至 **[!UICONTROL 后台操作]** 页面。

1. 在Experience Manager界面中，选择 **全局导航** > **工具** > **常规** > **作业**.

1. 在 **[!UICONTROL 后台操作]** 页中，查看操作的详细信息。

   ![异步操作的状态和详细信息](assets/async-operation-status.png)

   要确定特定操作的进度，请参阅&#x200B;**[!UICONTROL 状态]**&#x200B;列中的值。根据进度，将显示以下状态之一：

   * **[!UICONTROL 活动]**：正在处理操作

   * **[!UICONTROL 成功]**：操作已完成

   * **[!UICONTROL 失败]**&#x200B;或&#x200B;**[!UICONTROL 错误]**：无法处理该操作

   * **[!UICONTROL 已计划]**：该操作计划稍后处理

1. 要停止活动操作，请从列表中选择该操作，然后单击工具栏中的&#x200B;**[!UICONTROL 停止]**。

   ![stop_icon](assets/async-stop-icon.png)

1. 要查看其他详细信息（例如，说明和日志），请选择操作，然后单击工具栏中的&#x200B;**[!UICONTROL 打开]**。

   ![open_icon](assets/async-open-icon.png)

   此时会显示作业详细信息页面。

   ![job_details](assets/async-job-details.png)

1. 要从列表中删除该操作，请从工具栏中选择&#x200B;**[!UICONTROL 删除]**。要以 CSV 文件下载详细信息，请单击&#x200B;**[!UICONTROL 下载]**。

   >[!NOTE]
   >
   >无法删除状态为&#x200B;**活动**&#x200B;或&#x200B;**已排队**&#x200B;有作业。

## 配置异步作业处理选项 {#configure}

可以配置多个有关异步作业的选项。 以下示例说明如何在本地开发系统上使用Configuration Manager执行此操作。

>[!NOTE]
>
>[OSGi配置](/help/implementing/deploying/configuring-osgi.md#creating-osgi-configurations) 被视为可变内容，任何此类配置必须部署为生产环境的内容包。

### 清除已完成的作业 {#purging-completed-jobs}

AEM每天01:00运行清除作业，以删除已完成的已超过一天的异步作业。

您可以修改清除作业的计划，以及删除之前保留已完成作业详细信息的持续时间。您还可以配置在任何时间点保留详细信息的已完成作业的最大数量。

1. 登录到AEM SDK快速入门Jar的AEM Web控制台，网址为 `https://<host>:<port>/system/console` 作为管理员用户。
1. 导航到 **osgi** > **配置**
1. 打开 **[!UICONTROL Adobe Granite 异步作业清除计划作业]**。
1. 指定：
   * 删除已完成作业后的天数阈值。
   * 历史记录中保留详细信息的最大作业数量。
   * 应运行清除时的 CRON 表达式。

   ![计划清除异步作业的配置](assets/async-purge-job.png)

1. 保存更改。

### 配置异步资产删除操作 {#configuring-synchronous-delete-operations}

如果要删除的资产或文件夹数量超过阈值数，将异步执行删除操作。

1. 登录到AEM SDK快速入门Jar的AEM Web控制台，网址为 `https://<host>:<port>/system/console` 作为管理员用户。
1. 导航到 **osgi** > **配置**
1. 从 Web 控制台中，打开&#x200B;**[!UICONTROL 异步进程默认队列配置。]**
1. 在&#x200B;**[!UICONTROL 资产的阈值数]**&#x200B;框中，指定用于异步处理删除操作的资产/文件夹的阈值数。

   ![资产删除阈值](assets/async-delete-threshold.png)

1. 选中选项&#x200B;**启用电子邮件通知**，以接收此作业状态的电子邮件通知。例如，成功、失败。
1. 保存更改。

### 配置异步资产移动操作 {#configuring-asynchronous-move-operations}

如果要移动的资产/文件夹或引用数量超过阈值数，将异步执行移动操作。

1. 登录到AEM SDK快速入门Jar的AEM Web控制台，网址为 `https://<host>:<port>/system/console` 作为管理员用户。
1. 导航到 **osgi** > **配置**
1. 从 Web 控制台中，打开&#x200B;**[!UICONTROL 异步移动操作作业处理配置。]**
1. 在&#x200B;**[!UICONTROL 资产/参考的阈值数]**&#x200B;框中，指定用于异步处理移动操作的资产/文件夹的阈值数。

   ![资产移动阈值](assets/async-move-threshold.png)

1. 选中选项&#x200B;**启用电子邮件通知**，以接收此作业状态的电子邮件通知。例如，成功、失败。
1. 保存更改。

### 配置异步 MSM 操作 {#configuring-asynchronous-msm-operations}

1. 登录到AEM SDK快速入门Jar的AEM Web控制台，网址为 `https://<host>:<port>/system/console` 作为管理员用户。
1. 导航到 **osgi** > **配置**
1. 从 Web 控制台中，打开&#x200B;**[!UICONTROL 异步页面移动操作作业处理配置。]**
1. 选中选项&#x200B;**启用电子邮件通知**，以接收此作业状态的电子邮件通知。例如，成功、失败。

   ![MSM 配置](assets/async-msm.png)

1. 保存更改。

>[!MORELIKETHIS]
>
>* [创建和组织页面](/help/sites-cloud/authoring/fundamentals/organizing-pages.md)
>* [批量导入和导出资产元数据](/help/assets/metadata-import-export.md)。
>* [使用“连接的资产”从远程部署中共享 DAM 资产](/help/assets/use-assets-across-connected-assets-instances.md)。
