---
title: 关于Dynamic Media图像配置文件和视频配置文件
description: 图像配置文件或视频配置文件是将哪些选项应用于您上传到文件夹的资源的脚本。 例如，您可以指定将什么视频编码应用于您上传的Dynamic Media视频资产。 或者，什么图像配置文件可应用于Dynamic Media图像资源以正确裁剪它们。
contentOwner: Rick Brough
feature: Asset Management,Image Profiles,Video Profiles
role: Admin,User
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: 34038d954802b7f8e31441d5c5e4ea90380e7a20
workflow-type: tm+mt
source-wordcount: '1391'
ht-degree: 0%

---

# 关于Dynamic Media图像配置文件和视频配置文件{#about-dm-image-video-profiles}

图像配置文件或视频配置文件是将哪些选项应用于您上传到文件夹的资源的脚本。 例如，您可以指定将什么视频编码应用于您上传的Dynamic Media视频资产。 或者，什么图像配置文件可应用于Dynamic Media图像资源以正确裁剪它们。

在Dynamic Media中，您可以创建两种类型的用户档案，以下链接将详细介绍这两种用户档案：

* [Dynamic Media图像配置文件](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media视频配置文件](/help/assets/dynamic-media/video-profiles.md)

另请参阅 [元数据配置文件](/help/assets/metadata-profiles.md).

您必须具有管理员权限才能创建、编辑和删除Dynamic Media图像配置文件或Dynamic Media视频配置文件。

创建图像配置文件或视频配置文件后，可将其分配给一个或多个用于新上传的Dynamic Media资源的文件夹。

另请参阅 [组织数字资产以使用处理配置文件的最佳实践](/help/assets/organize-assets.md).


>[!NOTE]
>
>您从一个文件夹移动到另一个文件夹的资源不会重新处理。 例如，假设文件夹1具有分配给它的配置文件A，而文件夹2具有分配给它的配置文件B。 如果将资产从文件夹1移至文件夹2，则已移动的资产会保留其从文件夹1进行的原始处理。
>
>即使在分配了相同配置文件的两个文件夹之间移动资产时，也是如此。

## 重新处理文件夹中的Dynamic Media资源 {#reprocessing-assets}

如果文件夹已具有现有的Dynamic Media图像配置文件或您后来更改的Dynamic Media视频配置文件，您可以重新处理该文件夹中的资产。

例如，假设您创建了一个Dynamic Media图像配置文件并将其分配到某个文件夹。 您上传到文件夹的任何图像资产都会自动将图像配置文件应用于资产。 但是，稍后您决定向图像配置文件中添加新的智能裁切比率。 现在，您只需运行 *Dynamic Media重新处理* 工作流。

您可以对首次处理失败的资产运行重新处理工作流。 即使您尚未编辑图像配置文件或视频配置文件，或者您已经应用了图像配置文件或视频配置文件，您仍可以随时对资产的文件夹运行重新处理工作流。

您可以选择将重新处理工作流的批大小从默认的50个资产调整到1000个资产。 当您运行 _Dynamic Media重新处理_ 工作流中，资产会进行批量分组，然后发送到Dynamic Media服务器以供处理。 处理后，整个批次集中每个资源的元数据将在更新 [!DNL Adobe Experience Manager]. 如果批次大小很大，处理可能会延迟。 或者，如果批次大小太小，可能会导致到Dynamic Media服务器的往返次数过多。

请参阅 [调整重新处理工作流的批次大小](#adjusting-load).

>[!NOTE]
>
>如果您要将资源从Dynamic Media Classic批量迁移到 [!DNL Experience Manager]，在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
>
>必须在Dynamic Media服务器上禁用迁移发布代理，以便重新处理工作流可按预期运行。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media's Image Production System) job. When you run the Dynamic Media Reprocess workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**要重新处理文件夹中的Dynamic Media资源，请执行以下操作：**

1. 在 [!DNL Experience Manager]，在资产页面中，导航到分配了图像配置文件或视频配置文件的资产文件夹，您要对其应用 **Dynamic Media重新处理** 工作流。

   分配了图像配置文件或视频配置文件的文件夹，其配置文件的名称将直接显示在卡片视图的文件夹名称下方。

1. 选择文件夹。

   * 工作流会递归考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个具有资产的子文件夹，则工作流会重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，请避免在具有超过1000个资产的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中选择 **[!UICONTROL 时间线]**.
1. 在页面的左下角附近， [!UICONTROL 注释] 字段中，选择克拉图标( **^** ) 。

   ![Experience Manager中资产的屏幕截图显示了资产的选定文件夹，突出显示了“时间轴”下拉列表，突出显示了“启动工作流”按钮，并且还突出显示了“评论”字段右侧的克拉图标](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. 选择 **[!UICONTROL 启动工作流]**.
1. 从 **[!UICONTROL 启动工作流]** 下拉列表，选择 **[!UICONTROL Dynamic Media重新处理]**.
1. （可选）在 **输入工作流的标题** 文本字段，输入工作流的名称。 如有必要，您可以使用名称来引用工作流实例。

   ![从“开始工作流”下拉列表中选择“Dynamic Media重新处理”并突出显示“开始”按钮的时间线用户界面的屏幕截图](/help/assets/dynamic-media/assets/reprocess-assets2.png).

1. 选择 **[!UICONTROL 开始]**，然后选择 **[!UICONTROL 确认]**.

   要监视工作流或检查其进度，请从 [!DNL Experience Manager] 主控台页面，选择 **[!UICONTROL “工具”>“工作流”]**. 在“工作流实例”页面上，选择一个工作流。 在菜单栏上，选择 **[!UICONTROL 打开历史记录]**. 您还可以从同一个“工作流实例”页面终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批次大小（可选） {#adjusting-load}

（可选）重新处理工作流中的默认批次大小是每个作业50个资产。 此最佳批次大小由平均资源大小以及运行重新处理的资源的MIME类型控制。 值越高，表示在单个重新处理作业中有多个文件。 因此，处理横幅将保持不变 [!DNL Experience Manager] 资产保留较长时间。 但是，如果平均文件大小为1 MB或更小，则Adobe建议将该值增加到几个100，但不能超过1000。 如果平均文件大小为数百MB，Adobe建议您将批次大小降低到10。

**要根据需要调整重新处理工作流的批大小，请执行以下操作：**

1. 在 [!DNL Experience Manager]，选择 **[!UICONTROL Adobe Experience Manager]** 要访问全局导航控制台，请选择 **[!UICONTROL 工具]** （锤子）图标> **[!UICONTROL 工作流>模型]**.
1. 在“工作流模型”页面的卡片视图或列表视图中，选择 **[!UICONTROL Dynamic Media重新处理]**.

   ![在Experience Manager的卡片视图中选择了“Dynamic Media重新处理”工作流的“工作流模型”页面的屏幕截图](/help/assets/dynamic-media/assets/reprocess-assets7.png).

1. 在工具栏中，选择 **[!UICONTROL 编辑]**. 新的浏览器选项卡将打开Dynamic Media重新处理工作流模型页面。
1. 在Dynamic Media重新处理工作流页面的右上角附近，选择 **[!UICONTROL 编辑]** 以“解锁”工作流。
1. 在工作流中，选择Scene7批量上传组件以打开工具栏，然后选择 **[!UICONTROL 配置]** 工具栏中。

   ![“Scene7重新处理”页面上的“Dynamic Media批量上传”组件屏幕截图，其中鼠标指针悬停在“配置”图标上](/help/assets/dynamic-media/assets/reprocess-assets8.png).

1. 在 **[!UICONTROL 批量上传至Scene7 — 步骤属性]** 对话框，请设置以下内容：
   * 在 **[!UICONTROL 标题]** 和 **[!UICONTROL 描述]** 文本字段，根据需要输入作业的新标题和描述。
   * 选择 **[!UICONTROL 处理程序前进]** 如果您的处理程序将进行到下一步。
   * 在 **[!UICONTROL 超时]** 字段中，输入外部进程超时（秒）。
   * 在 **[!UICONTROL 期间]** 字段中，输入轮询间隔（秒）以测试外部进程的完成情况。
   * 在 **[!UICONTROL 批次字段]**，输入在Dynamic Media服务器批处理上传作业中要处理的资源最大数量(50-1000)。
   * 选择 **[!UICONTROL 超时后前进]** 如果要在达到超时后前进，请执行以下操作。 如果要在达到超时后转至收件箱，请取消选择。

   ![“批量上传至Scene7 — 步骤属性”页面的屏幕截图](/help/assets/dynamic-media/assets/reprocess-assets3.png).

1. 在右上角 **[!UICONTROL 批量上传至Scene7 — 步骤属性]** 对话框，选择 **[!UICONTROL 完成]**.

1. 在“Dynamic Media重新处理工作流模型”页面的右上角，选择 **[!UICONTROL 同步]**. 当您看到 **[!UICONTROL 已同步]**，则工作流运行时模型已成功同步并准备好重新处理文件夹中的资产。

   ![Experience Manager中资产的屏幕截图显示了资产的选定文件夹，突出显示了“时间轴”下拉列表，突出显示了“启动工作流”按钮，并且还突出显示了“评论”字段右侧的克拉图标](/help/assets/dynamic-media/assets/reprocess-assets1.png).

1. 关闭显示Dynamic Media重新处理工作流模型的浏览器选项卡。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, select **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then select the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, select **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, select **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, select **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Dynamic Media Reprocess workflow model.

-->
