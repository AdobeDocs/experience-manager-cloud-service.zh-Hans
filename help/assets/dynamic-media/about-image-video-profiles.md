---
title: 关于Dynamic Media图像配置文件和视频配置文件
description: 图像配置文件或视频配置文件是将哪些选项应用到您上传到文件夹的资产的方法。 例如，您可以指定要应用于您上传的Dynamic Media视频资产的视频编码。 或者，要应用于Dynamic Media图像资产以正确裁剪图像的图像配置文件。
feature: 资产管理，图像配置文件，视频配置文件
role: Administrator,Business Practitioner
exl-id: 8c8f0a57-13f5-4903-8d76-bfb6ee83323c
source-git-commit: fdfcaf7ba99ec54e1bdf1c97764da8c766701498
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 2%

---

# 关于Dynamic Media图像配置文件和视频配置文件{#about-dm-image-video-profiles}

图像配置文件或视频配置文件是将哪些选项应用到您上传到文件夹的资产的方法。 例如，您可以指定要应用于您上传的Dynamic Media视频资产的视频编码。 或者，要应用于Dynamic Media图像资产以正确裁剪图像的图像配置文件。

在Dynamic Media中，您可以创建两种类型的用户档案，以下链接详细介绍了这些用户档案：

* [Dynamic Media图像配置文件](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media视频配置文件](/help/assets/dynamic-media/video-profiles.md)

另请参阅[元数据配置文件](/help/assets/metadata-profiles.md)。

您必须拥有管理员权限，才能创建、编辑和删除Dynamic Media图像配置文件或Dynamic Media视频配置文件。

创建图像配置文件或视频配置文件后，您可以将其分配给一个或多个用于新上传Dynamic Media资产的文件夹。

另请参阅[组织数字资产以使用图像配置文件或视频配置文件的最佳实践](/help/assets/dynamic-media/best-practices-for-file-management.md)。

>[!NOTE]
>
>从一个文件夹移动到另一个文件夹的资产不再重新处理。例如，假定您的文件夹1中分配了配置文件A，而文件夹2中分配了配置文件B。 如果将资产从文件夹1移动到文件夹2，则被移动的资产将保留其在文件夹1中的原始处理。
>
>即使在两个文件夹之间移动资产时，也是如此，因为这两个文件夹分配了相同的配置文件。

## 重新处理文件夹{#reprocessing-assets}中的Dynamic Media资产

您可以重新处理文件夹中的资产，该文件夹中已有Dynamic Media图像配置文件或您稍后更改的Dynamic Media视频配置文件。

例如，假定您创建了一个Dynamic Media图像配置文件，并将其分配给文件夹。 您上传到文件夹的任何图像资产都会自动将图像配置文件应用到这些资产。 但是，之后您决定向图像配置文件添加新的智能裁剪比例。 现在，您只需运行&#x200B;*Scene7即可，而不必再次选择资产并将其重新上传到文件夹：重新处理资产*&#x200B;工作流。

您可以对首次处理失败的资产运行重新处理工作流。 即使您未编辑图像配置文件或视频配置文件，或者已经应用了图像配置文件或视频配置文件，您仍可以随时对资产文件夹运行重新处理工作流。

您可以（可选）从默认的50个资产（最多1000个资产）调整重新处理工作流的批大小。 运行&#x200B;_Scene7时：在文件夹上重新处理资产_&#x200B;工作流，会将资产分批分组，然后将其发送到Dynamic Media服务器进行处理。 处理后，整个批处理集中每个资产的元数据都会在[!DNL Adobe Experience Manager]上更新。 如果批次大小较大，则处理过程可能会延迟。 或者，如果批次大小过小，则可能会导致到Dynamic Media服务器的往返次数过多。

请参阅[调整重新处理工作流的批处理大小](#adjusting-load)。

>[!NOTE]
>
>如果您正在将资产从Dynamic Media Classic批量迁移到[!DNL Experience Manager]，请在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
>
>必须在Dynamic Media服务器上禁用迁移发布代理，以便重新处理工作流按预期工作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**要重新处理文件夹中的Dynamic Media资产，请执行以下操作：**
1. 在[!DNL Experience Manager]的“资产”页面中，导航到一个资产文件夹，该文件夹中的图像配置文件或视频配置文件已分配给您要对其应用&#x200B;**Scene7:重新处理资产**&#x200B;工作流。

   如果文件夹分配了图像配置文件或视频配置文件，则其配置文件名称会显示在卡片视图中文件夹名称的正下方。

1. 选择文件夹。

   * 工作流会递归地考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个包含资产的子文件夹，则工作流会重新处理文件夹层次结构中的每个资产。
   * 最佳做法是，避免在资产超过1000个的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中，单击&#x200B;**[!UICONTROL 时间轴]**。
1. 在页面左下角附近，在[!UICONTROL Comment]字段的右侧，点按卡拉图标(**^**)。

   ![重新处理资产工作流1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 单击&#x200B;**[!UICONTROL 启动工作流]**。
1. 从&#x200B;**[!UICONTROL 启动工作流]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。
1. （可选）在&#x200B;**输入工作流**&#x200B;文本字段的标题中，输入工作流的名称。 如有必要，您可以使用名称引用工作流实例。

   ![重新处理资产2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 单击&#x200B;**[!UICONTROL 开始]**，然后单击&#x200B;**[!UICONTROL 确认]**。

   要监视工作流或检查其进度，请从[!DNL Experience Manager]主控制台页面中，单击&#x200B;**[!UICONTROL 工具>工作流]**。 在工作流实例页面上，选择一个工作流。 在菜单栏上，单击&#x200B;**[!UICONTROL 打开历史记录]**。 您还可以从同一工作流实例页面中终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批处理大小{#adjusting-load}

（可选）重新处理工作流中的默认批大小为每个作业50个资产。 此最佳批处理大小受平均资产大小和运行重新处理的资产的MIME类型的约束。 值越高，表示您在一个重新处理作业中拥有许多文件。 因此，处理横幅会在[!DNL Experience Manager]资产上停留较长时间。 但是，如果平均文件大小为1 MB或更小，则建议将该值增加到100，但不要超过1000。 如果文件的平均大小为数百MB，则Adobe建议您将批处理大小降低到10。

**（可选）要调整重新处理工作流的批大小，请执行以下操作：**

1. 在[!DNL Experience Manager]中，点按&#x200B;**[!UICONTROL Adobe Experience Manager]**&#x200B;以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具]**（锤子）图标> **[!UICONTROL 工作流>模型]**。
1. 在“工作流模型”页面的卡片视图或列表视图中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。

   ![工作流模型页面，其中包含Scene7:重新处理在卡片视图中选择的资产工作流](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 编辑]**。 新的浏览器选项卡会打开Scene7:重新处理资产工作流模型页面。
1. 在Scene7上：重新处理资产工作流页面右上角附近，点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以“解锁”工作流。
1. 在工作流中，选择Scene7批量上传组件以打开工具栏，然后点按工具栏中的&#x200B;**[!UICONTROL 配置]** 。

   ![Scene7批量上传组件](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7 — 步骤属性]**&#x200B;对话框中，设置以下内容：
   * 在&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 描述]**&#x200B;文本字段中，根据需要为作业输入新标题和描述。
   * 如果处理程序将前进到下一步，请选择&#x200B;**[!UICONTROL 处理程序Advance]**。
   * 在&#x200B;**[!UICONTROL Timeout]**&#x200B;字段中，输入外部进程超时（秒）。
   * 在&#x200B;**[!UICONTROL Period]**&#x200B;字段中，输入轮询间隔（秒）以测试外部进程的完成情况。
   * 在&#x200B;**[!UICONTROL 批处理字段]**&#x200B;中，输入在Dynamic Media服务器批处理上传作业中要处理的资产最大数量(50-1000)。
   * 如果希望在达到超时时提前，请选择&#x200B;**[!UICONTROL 超时时提前]**。 如果要在达到超时时继续进入收件箱，请取消选择。

   ![“属性”对话框](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7 — 步骤属性]**&#x200B;对话框的右上角，点按&#x200B;**[!UICONTROL 完成]**。

1. 位于Scene7的右上角：重新处理资产工作流模型页面，点按&#x200B;**[!UICONTROL 同步]**。 当您看到&#x200B;**[!UICONTROL Synced]**&#x200B;时，工作流运行时模型已成功同步，并可以重新处理文件夹中的资产。

   ![同步工作流模型](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 关闭显示Scene7的浏览器选项卡：重新处理资产工作流模型。

<!-- MAY BE NEEDED IN THE FUTURE

1. Return to the browser tab that has the open Workflow Models page, then press **Esc** to exit the selection.
1. In the upper-left corner of the page, tap **[!UICONTROL Adobe Experience Manager]** to access the global navigation console, then tap the **[!UICONTROL Tools]** (hammer) icon > **[!UICONTROL General > CRXDE Lite]**.
1. In the folder tree on the left side of the CRXDE Lite page, navigate to the following location:

   `/conf/global/settings/workflow/models/scene7_reprocess_assets/jcr:content/flow/reprocess/metaData`

   ![CRXDE Lite](/help/security/assets/workflow-models9.png)

1. On the right side of the CRXDE Lite page, in the lower portion, enter the following name, type, and value in its respective field:
    * **[!UICONTROL Name]**: `reprocess-batch-size`
    * **[!UICONTROL Type]**: `Long`
    * **[!UICONTROL Value]**: enter a default value (50-1000) for the batch size
1. In the lower-right corner, tap **[!UICONTROL Add]**. The new property appears as the following:

    ![Saving the new property](/help/security/assets/workflow-models10.png)

1. On the menu bar of the CRXDE Lite page, tap **[!UICONTROL Save All]**.
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main Experience Manager console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
