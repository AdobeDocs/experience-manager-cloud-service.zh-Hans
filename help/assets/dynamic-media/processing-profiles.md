---
title: 用于处理元数据、图像和视频的用户档案
description: 用户档案一组规则，围绕要应用于上传到文件夹的资产的选项。 指定要应用于您上传的视频资产的元数据用户档案和视频编码用户档案。 对于图像资产，您还可以指定要应用于图像资产的图像用户档案，以便对图像资产进行正确裁剪。
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 6%

---


# 用于处理元数据、图像和视频的用户档案{#profiles-for-processing-metadata-images-and-videos}

用户档案是将哪些选项应用到上传到文件夹的资产的菜谱。 例如，您可以指定特定的元数据配置文件和视频编码配置文件，并将这些配置文件应用到您上传的视频资产。您还可以指定特定的图像配置文件，并将配置文件应用到图像资产，以便对图像资产进行适当的裁剪。

这些规则可以包括添加元数据、智能裁剪图像或建立视频编码用户档案。 在AEM中，您可以创建三种类型的用户档案，下面的链接将详细介绍这些类型：

* [元数据配置文件](/help/assets/metadata-profiles.md)
* [图像配置文件](/help/assets/dynamic-media/image-profiles.md)
* [视频配置文件](/help/assets/dynamic-media/video-profiles.md)

您必须具有管理员权限才能创建、编辑和删除元数据、图像或视频用户档案。

创建元数据、图像或视频用户档案后，您可以将其分配给一个或多个文件夹，这些文件夹用作新上传资产的目标。

See also [Best Practices for Organizing your Digital Assets for using Processing Profiles](/help/assets/dynamic-media/best-practices-for-file-management.md).

>[!NOTE]
>
>从一个文件夹移动到另一个文件夹的资产不再重新处理。例如，假定您的文件夹1分配了用户档案A，文件夹2分配了用户档案B。 如果将资产从文件夹1移动到文件夹2，则被移动的资产将保留其从文件夹1的原始处理。
>
>即使在分配了相同用户档案的两个文件夹之间移动资产，情况也是如此。

## 重新处理文件夹中的资产 {#reprocessing-assets}

您可以重新处理文件夹中的资产，该文件夹已经存在您稍后更改的现有处理用户档案。

例如，假定您创建了一个图像用户档案并将其分配给文件夹。 您上传到该文件夹的任何图像资产都会自动将图像用户档案应用到资产。 但是，稍后您决定向用户档案添加新的智能裁剪比率。 现在，您只需运行Scene7，而不是再次选择资产并将其重新上传到 *文件夹： 重新处理资产* 工作流。

您可以对首次处理失败的资产运行重新处理工作流。 因此，即使您尚未编辑处理用户档案或应用处理用户档案，您仍可以随时对资产文件夹运行重新处理工作流。

您可以选择调整重新处理工作流的批大小，默认值为50个资产，最多为1000个资产。 运行Scene7 _时： 在文件夹_ 上重新处理资产工作流时，资产会分批分组在一起，然后发送到Dynamic Media服务器进行处理。 处理后，整个批集中每个资产的元数据都将在AEM上更新。 如果批量很大，您可能会遇到处理延迟。 或者，如果批量太小，可能会导致往返到Dynamic Media服务器的次数过多。

请参 [阅调整重新处理工作流的批大小](#adjusting-load)。

>[!NOTE]
>
>如果要将资产从Dynamic Media Classic批量迁移到AEM，则必须在Dynamic Media服务器上启用迁移复制代理。 迁移完成后，请确保禁用代理。
迁移发布代理必须在Dynamic Media服务器上禁用，这样重新处理工作流就可以按预期工作。

<!-- LEAVE IN PLACE, MAY BE USED IN THE FUTURE

Batch size is the number of assets that are amalgamated into a single IPS (Dynamic Media’s Image Production System) job. When you run the Scene7: Reprocess Assets workflow, the job is triggered on IPS. The number of IPS jobs that are triggered is based on the total number of assets in the folder, divided by the batch size. For example, suppose you had a folder with 150 assets and a batch size of 50. In this case, three IPS jobs are triggered. The assets are updated when the entire batch size (50 in our example) is processed in IPS. The job then moves onto the next IPS job and so on until complete. If you increase the batch size, you may notice a longer delay with assets getting updated. 

-->

**要重新处理文件夹中的资产，请执行以下操作**:
1. 在AEM中，从“资产”页面导航到一个资产文件夹，该文件夹已为资产分配了处理用户档案，并且您要为其应用 **Scene7: 重新处理资产** 工作流，

   如果文件夹已经分配了处理用户档案，则卡视图中文件夹名称的正下方会显示该用户档案的名称。

1. 选择文件夹。

   * 该工作流会递归地考虑选定文件夹中的所有文件。
   * 如果在主选定文件夹中存在一个或多个资产子文件夹，则该工作流将重新处理文件夹层次结构中的每个资产。
   * 作为最佳实践，您应避免在资产超过1000个的文件夹层次结构上运行此工作流。

1. 在页面的左上角附近，从下拉列表中，单击&#x200B;**[!UICONTROL 时间轴]**。
1. 在页面左下角附近，在“评论”字段的右侧，单击“加载”图标( **^** )。

   ![重新处理资产工作流1](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 单击 **[!UICONTROL 开始工作流]**。
1. 从“ **[!UICONTROL 开始工作流]** ”下拉列表中，选 **[!UICONTROL 择Scene7: 重新处理资产]**。
1. （可选）在输 **入工作流标题文本** 字段中，输入工作流的名称。 如有必要，您可以使用该名称引用工作流实例。

   ![重新处理资产2](/help/assets/dynamic-media/assets/reprocess-assets2.png)

1. 单击 **[!UICONTROL 开始]**，然后单 **[!UICONTROL 击确认]**。

   要监视工作流或检查其进度，请在AEM主控制台页面中，单击工具> **[!UICONTROL 工作流]**。 在“工作流实例”页面上，选择一个工作流。 在菜单栏上，单击“打 **[!UICONTROL 开历史记录]**”。 您还可以从同一“工作流实例”页面终止、暂停或重命名选定的工作流。

### 调整重新处理工作流的批大小 {#adjusting-load}

（可选）重新处理工作流中的默认批大小为每个作业50个资产。 此最佳批处理大小受平均资产大小和运行重新处理的资产的MIME类型的约束。 值越高，意味着您在一个重新处理作业中将拥有许多文件。 因此，处理横幅在AEM资产上停留的时间会更长。 但是，如果平均文件大小为1 MB或更小，Adobe建议您将该值增加到几百，但不要超过1000。 如果文件的平均大小是大到数百兆字节，Adobe建议您将批处理大小减小到10。

**（可选）要调整重新处理工作流的批大小**

1. 在 Experience Manager 中，点按 **[!UICONTROL Adobe Experience Manager]**，以访问全局导航控制台，然后点按&#x200B;**[!UICONTROL 工具]**（锤子）图标 > **[!UICONTROL 工作流 > 模型]**。
1. 在“工作流模型”页面的卡片视图或列表视图中，选 **[!UICONTROL 择Scene7: 重新处理资产]**。

   ![“工作流模型”页（带有Scene7）: 在卡视图中重新处理选定的资产工作流](/help/assets/dynamic-media/assets/reprocess-assets7.png)

1. 在工具栏上，单击“编 **[!UICONTROL 辑”]**。 新的浏览器选项卡会打开Scene7: 重新处理资产工作流模型页面。
1. 在Scene7上： 重新处理资产工作流页面，在右上角附近，点 **[!UICONTROL 按编辑]** ，以“解锁”工作流。
1. 在工作流中，选择Scene7批量上传组件以打开工具栏，然后点按工 **[!UICONTROL 具栏]** 上的配置。

   ![Scene7批量上传组件](/help/assets/dynamic-media/assets/reprocess-assets8.png)

1. 在“批 **[!UICONTROL 量上传到Scene7 —— 步骤属性]** ”对话框中，设置以下内容：
   * In the **[!UICONTROL Title]** and **[!UICONTROL Description]** text fields, enter a new title and description for the job, if desired.
   * 如果处 **[!UICONTROL 理程序将进]** 入下一步，请选择“处理程序前进”。
   * 在超时 **[!UICONTROL 字段中]** ，输入外部进程超时（秒）。
   * 在“ **[!UICONTROL 期间]** ”字段中，输入轮询间隔（秒）以测试外部进程的完成情况。
   * In the **[!UICONTROL Batch field]**, enter the maximum number of assets (50-1000) to process in a Dynamic Media server batch processing upload job.
   * 如果 **[!UICONTROL 要在达到超时]** 时提前，请选择“超时时提前”。 如果要在达到超时时继续进入收件箱，请取消选择。
   ![属性对话框](/help/assets/dynamic-media/assets/reprocess-assets3.png)

1. 在“批量上传到Scene7 —— 步 **[!UICONTROL 骤属性”对话框的右上角]** ，点按 **[!UICONTROL 完成]**。

1. 在Scene7的右上角： 重新处理资产工作流模型页，点按 **[!UICONTROL 同步]**。 当您看到已 **[!UICONTROL 同步]**，工作流运行时模型将成功同步并准备好重新处理文件夹中的资产。

   ![同步工作流模型](/help/assets/dynamic-media/assets/reprocess-assets1.png)

1. 关闭显示Scene7的浏览器选项卡： 重新处理资产工作流模型。

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
1. In the upper-left corner of the page, tap **[!UICONTROL CRXDE Lite]** to return to the main AEM console
1. Repeat steps 1-7 to re-synchronize the new batch size to the Scene7: Reprocess Assets workflow model.

-->
