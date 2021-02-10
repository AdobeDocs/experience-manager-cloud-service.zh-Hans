---
title: 关于Dynamic Media图像用户档案和视频用户档案
description: 图像用户档案或视频用户档案是将哪些选项应用到您上传到文件夹的资产的菜谱。 例如，您可以指定要应用于您上传的Dynamic Media视频资产的视频编码。 或者，要应用于Dynamic Media图像资产的图像用户档案，以正确裁剪这些图像资产。
translation-type: tm+mt
source-git-commit: dfaaafce8e9a7f0d90e4c3d6967c8236d48e6e40
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 3%

---


# 关于Dynamic Media图像用户档案和视频用户档案{#about-dm-image-video-profiles}

图像用户档案或视频用户档案是将哪些选项应用到您上传到文件夹的资产的菜谱。 例如，您可以指定要应用于您上传的Dynamic Media视频资产的视频编码。 或者，要应用于Dynamic Media图像资产的图像用户档案，以正确裁剪这些图像资产。

在Dynamic Media，您可以创建两种类型的用户档案，其详细信息请参阅以下链接：

* [Dynamic Media图像用户档案](/help/assets/dynamic-media/image-profiles.md)
* [Dynamic Media视频用户档案](/help/assets/dynamic-media/video-profiles.md)

另请参阅[元数据用户档案](/help/assets/metadata-profiles.md)。

您必须具有管理员权限才能创建、编辑和删除Dynamic Media图像用户档案或Dynamic Media视频用户档案。

创建图像用户档案或视频用户档案后，您可以将其分配给一个或多个用于新上传的Dynamic Media资产的文件夹。

另请参阅[组织数字资产以使用图像用户档案或视频用户档案的最佳实践](/help/assets/dynamic-media/best-practices-for-file-management.md)。

>[!NOTE]
>
>从一个文件夹移动到另一个文件夹的资产不再重新处理。例如，假定您的文件夹1分配了用户档案A，文件夹2分配了用户档案B。 如果将资产从文件夹1移动到文件夹2，则被移动的资产将保留其从文件夹1的原始处理。
>
>即使在分配了相同用户档案的两个文件夹之间移动资产，情况也是如此。

## 在文件夹{#reprocessing-assets}中重新处理Dynamic Media资源

您可以重新处理已有Dynamic Media图像用户档案或稍后更改的Dynamic Media视频用户档案的文件夹中的资产。

例如，假定您创建了一个Dynamic Media图像用户档案并将其分配给文件夹。 您上传到该文件夹的任何图像资产都会自动将图像用户档案应用到资产。 但是，稍后您决定向图像用户档案添加新的智能裁剪比率。 现在，您只需运行&#x200B;*Scene7:重新处理资产*&#x200B;工作流。

您可以对首次处理失败的资产运行重新处理工作流。 即使您尚未编辑图像用户档案或视频用户档案，或者您已应用图像用户档案或视频用户档案，您仍然可以随时对资产文件夹运行重新处理工作流。

您可以选择调整重新处理工作流的批大小，默认值为50个资产，最多为1000个资产。 运行&#x200B;_Scene7时：在文件夹中重新处理资产_&#x200B;工作流，资产会分批进行分组，然后发送到Dynamic Media服务器进行处理。 处理后，整个批集中每个资产的元数据会在AEM上更新。 如果批量大，则处理时可能会出现延迟。 或者，如果批量太小，可能导致往返到Dynamic Media服务器的次数过多。

请参阅[调整重新处理工作流的批处理大小](#adjusting-load)。

>[!NOTE]
>
>如果您正在执行从Dynamic Media经典到Experience Manager的资产批量迁移，请在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
>
>必须在Dynamic Media服务器上禁用迁移发布代理，以便重新处理工作流按预期工作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**要重新处理文件夹中的Dynamic Media资产**:
1. 在Adobe Experience Manager，从“资产”页面，导航到Dynamic Media资产的一个文件夹，该文件夹中分配了图像用户档案或视频用户档案，并且您要对其应用&#x200B;**Scene7:重新处理资产**&#x200B;工作流，

   为其分配了图像用户档案或视频用户档案的文件夹具有用户档案的名称，该名称会直接显示在卡视图中的文件夹名称下方。

1. 选择文件夹。

   * 该工作流会递归地考虑选定文件夹中的所有文件。
   * 如果主选定文件夹中存在一个或多个包含资产的子文件夹，该工作流将重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，请避免在资产超过1000个的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中，单击&#x200B;**[!UICONTROL 时间轴]**。
1. 在页面左下角附近，在[!UICONTROL 注释]字段的右侧，点按克拉图标(**^**)。

   ![重新处理资产工作流1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 单击&#x200B;**[!UICONTROL 开始工作流]**。
1. 从&#x200B;**[!UICONTROL 开始工作流]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。
1. （可选）在&#x200B;**输入工作流的标题**&#x200B;文本字段中，输入工作流的名称。 如有必要，您可以使用该名称引用工作流实例。

   ![重新处理资产2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 单击&#x200B;**[!UICONTROL 开始]**，然后单击&#x200B;**[!UICONTROL 确认]**。

   要监视工作流或检查其进度，请从Experience Manager主控制台页面，单击&#x200B;**[!UICONTROL 工具>工作流]**。 在“工作流实例”页面上，选择一个工作流。 在菜单栏上，单击&#x200B;**[!UICONTROL 打开历史记录]**。 您还可以从同一“工作流实例”页面终止、暂停或重命名选定的工作流。

### 调整重新处理工作流{#adjusting-load}的批处理大小

（可选）重新处理工作流中的默认批大小为每个作业50个资产。 此最佳批处理大小受平均资产大小和运行重新处理的资产的MIME类型所管辖。 值越高，表示您在一个重新处理作业中拥有许多文件。 因此，处理横幅在Experience Manager资产上停留的时间更长。 但是，如果平均文件大小为小-1 MB或小Adobe，则建议将该值增加到几百，但不要超过1000。 如果文件的平均大小为数百MB，则Adobe建议您将批处理大小减小到10。

**（可选）要调整重新处理工作流的批大小**:

1. 在 Experience Manager 中，点按 **[!UICONTROL Adobe Experience Manager]**，以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具]**（锤子）图标 > **[!UICONTROL 工作流 > 模型]**。
1. 在“工作流模型”页面的卡片视图或列表视图中，选择&#x200B;**[!UICONTROL Scene7:重新处理资产]**。

   ![工作流模型页面，带有Scene7:在卡视图中重新处理选定的资产工作流](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具栏中，单击&#x200B;**[!UICONTROL 编辑]**。 新的浏览器选项卡打开Scene7:重新处理资产工作流模型页面。
1. Scene7:重新处理资产工作流页面，在右上角附近，点按&#x200B;**[!UICONTROL 编辑]**&#x200B;以“解锁”工作流。
1. 在工作流中，选择“Scene7批量上传”组件以打开工具栏，然后点按工具栏中的&#x200B;**[!UICONTROL 配置]**。

   ![Scene7批上传组件](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7—步骤属性]**&#x200B;对话框中，设置以下内容：
   * 在&#x200B;**[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 说明]**&#x200B;文本字段中，根据需要输入新标题和作业说明。
   * 如果处理函数将前进到下一步，请选择&#x200B;**[!UICONTROL 处理函数高级]**。
   * 在&#x200B;**[!UICONTROL 超时]**&#x200B;字段中，输入外部进程超时（秒）。
   * 在&#x200B;**[!UICONTROL Period]**&#x200B;字段中，输入轮询间隔（秒）以测试外部进程是否完成。
   * 在&#x200B;**[!UICONTROL 批处理字段]**&#x200B;中，输入要在Dynamic Media服务器批处理上传作业中处理的最大资产数(50-1000)。
   * 如果希望在达到超时时前进，请选择&#x200B;**[!UICONTROL 超时时前进]**。 如果要在达到超时时继续进入收件箱，请取消选择。

   ![属性对话框](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 在&#x200B;**[!UICONTROL 批量上传到Scene7-步骤属性]**&#x200B;对话框的右上角，点按&#x200B;**[!UICONTROL 完成]**。

1. 在Scene7的右上角：重新处理资产工作流模型页，点按&#x200B;**[!UICONTROL 同步]**。 当您看到&#x200B;**[!UICONTROL 已同步]**&#x200B;时，工作流运行时模型已成功同步，并可以重新处理文件夹中的资产。

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
