---
title: 预览资源
description: 了解如何在Dynamic Media中预览资源。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 3928798d-352a-42a8-a544-7104fc9b3cf1
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 2%

---

# 预览资源{#previewing-assets}

您可以使用“预览”来查看客户在自己的Web浏览器中查看您上传的数字资产时该资产的显示方式。 为资源分配的默认嵌入式跨设备查看器将用于预览。

查看器是各种设置或“预设”的集合。 例如，查看器显示大小、缩放行为、颜色方案、边框和字体，这些决定了用户在其计算机屏幕和移动设备上查看富媒体资产的方式。

除了为视频、旋转集和图像集使用专用预览功能外，您还可以使用已创建的查看器预设预览资源。 或者，使用图像预设来预览图像的演绎版。

* [应用图像预设](/help/assets/dynamic-media/image-presets.md)
* [应用查看器预设](/help/assets/dynamic-media/viewer-presets.md)

>[!NOTE]
>
>当您位于Adobe Experience Manager的网页（站点）上时，无法预览以下位置的资源： **[!UICONTROL 编辑]** 模式。 相反，请通过选择以转到预览模式 **[!UICONTROL 预览]** 在页面的右上角。

要在用户界面中启用或禁用查看器预设，请参阅 [管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md).

**要预览资源，请执行以下操作：**

1. 起始日期 **[!UICONTROL Experience Manager]**，位于 **[!UICONTROL 导航]** 页面，选择 **[!UICONTROL 资产]**，则 **[!UICONTROL 文件]** 以访问资产。
1. 在页面的右上角附近，从 **[!UICONTROL 视图]** 下拉列表，选择 **[!UICONTROL 列表视图]**.
1. （可选）使用 **[!UICONTROL 类型]** 列按要预览的类型对资源进行排序。
1. 在 **[!UICONTROL 标题]** 列中，选择要预览的资源的标题名称（不是缩略图图像）。
1. 根据您选择的资源类型，执行以下任一操作：

   <table>
    <tbody>
      <tr>
      <td><strong>您选择的资源类型</strong><br /> </td>
      <td><strong>能否预览特定演绎版中的资源？</strong></td>
      <td><strong>能否预览特定查看器中的资源？</strong></td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在维查看器中预览3D资产</strong></p>
      <ul>
      <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择维查看器。</li>
      <li>要将图像返回到原始缩放图，请选择 <strong>重置</strong>.</li>
      <li>要最大化显示设备上的查看器，请选择 <strong>全屏</strong>.</li>
      </ul>
      <p><strong>浏览3D场景</strong></p>
      <ul>
      <li><p><strong>转动3D摄像头</strong>  — 使视图围绕3D场景和对象旋转。</p> 鼠标：左键单击+拖动。</p> 触摸屏：按+拖动。</p></li>
      <li><p><strong>平移相机</strong>  — 向左、向右、向上和向下平移视图。</p> 鼠标：右键单击+拖动。</p> 触摸屏：双指按下+拖动。</p></li>
      <li><p><strong>缩放相机</strong>  — 如果要在3D场景中移入和移出区域，请缩放相机。</p> 鼠标：滚轮。</p> 触摸屏：手指捏合。</p></li>
      <li><p><strong>重新居中相机</strong>  — 使视图围绕3D场景和对象旋转。</p> 鼠标：双击。</p> 触摸屏：双击。</li></ul></td>
      </tr>
      <tr>
      <td><p>图像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>演绎版</strong> 从列表中，选择要预览的特定演绎版。</li>
        </ul> <p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>-</strong>图标分别增大或减小所选图像的缩放比例。 要将图像返回到原始缩放，请选择 <strong>重置</strong>.<br>如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动跨图像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒体</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>演绎版</strong> 从列表中，选择要预览的特定演绎版。</li>
        </ul><p>选择要预览的更高分辨率视频演绎版可能会导致视频显示被截断。 原因在于，演绎版预览会向您显示客户看到的确切分辨率，所有这些都是在用于预览的嵌入式查看器的上下文中进行的。</p><p>在资源级别预览自适应视频集时，演绎版将分组到一个播放体验中。 也就是说，根据查看设备和连接速度，自适应视频经过适当的调整以适合查看和使用最佳分辨率回放。<br /></p><p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>图像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>图标分别增大或减小所选图像的缩放比例。 要将图像返回到原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动跨图像以平移。</p></td>
      </tr>
      <tr>
      <td>旋转集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>- </strong>图标分别增大或减小所选图像的缩放比例。 要将图像返回到原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动跨图像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒体集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong> 从列表中，选择要应用于资源的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>图标分别增大或减小所选图像的缩放比例。 要将图像返回到原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动跨图像以平移。</p> </td>
      </tr>
      <tr>
      <td>轮播集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>要在特定查看器中预览资源，请执行以下操作</strong>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择要应用于资源的查看器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360视频<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资源</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>演绎版</strong>，然后选择要预览的节目。</li>
        </ul> <p><strong>要在特定查看器中预览资源，请执行以下操作</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标，下拉列表随即显示。 选择 <strong>查看器</strong>，然后选择要应用于资源的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>图标分别增大或减小所选图像的缩放比例。 要将图像返回到原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触摸屏上，请双击图像以按步骤放大。 达到最大缩放时，再次双击图像可重置缩放状态。 拖动跨图像以平移。</p> </td>
      </tr>
    </tbody>
    </table>
