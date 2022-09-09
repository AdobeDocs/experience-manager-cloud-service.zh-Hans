---
title: 预览资源
description: 了解如何在Dynamic Media中预览资产。
feature: Asset Management
role: User
exl-id: 3928798d-352a-42a8-a544-7104fc9b3cf1
source-git-commit: a11529886d4b158c19a97ccbcb7d004cf814178d
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 21%

---

# 预览资源{#previewing-assets}

您可以使用“预览”功能查看客户在其Web浏览器中查看您上传的数字资产时的显示方式。 预览时将使用为资产分配的默认嵌入式跨设备查看器。

查看器是各种设置或“预设”的集合。 例如，查看器的显示大小、缩放行为、颜色方案、边框和字体，这些都决定了用户在其计算机屏幕和移动设备上查看富媒体资产的方式。

除了使用专门的“预览”功能预览视频、旋转集和图像集之外，您还可以通过使用自己创建的查看器预设来预览资产。或者，也可以使用图像预设来预览图像的演绎版。

* [应用图像预设](/help/assets/dynamic-media/image-presets.md)
* [应用查看器预设](/help/assets/dynamic-media/viewer-presets.md)

>[!NOTE]
>
>当您位于Adobe Experience Manager的网页（站点）上时，无法在中预览资产 **[!UICONTROL 编辑]** 模式。 相反，通过选择 **[!UICONTROL 预览]** 页面的右上角。

要在用户界面中启用或禁用查看器预设，请参阅 [管理查看器预设](/help/assets/dynamic-media/managing-viewer-presets.md).

**要预览资产，请执行以下操作：**

1. 从 **[!UICONTROL Experience Manager]**，在 **[!UICONTROL 导航]** 页面，选择 **[!UICONTROL 资产]**，则 **[!UICONTROL 文件]** 以访问资产。
1. 在页面的右上角附近，从 **[!UICONTROL 查看]** 下拉列表中，选择 **[!UICONTROL 列表视图]**.
1. （可选）使用 **[!UICONTROL 类型]** 列，按要预览的类型对资产进行排序。
1. 在 **[!UICONTROL 标题]** 列中，选择要预览的资产的标题名称（而非缩略图图像）。
1. 根据您选择的资产类型，执行以下任一操作：

   <table>
    <tbody>
      <tr>
      <td><strong>您选择的资产类型</strong><br /> </td>
      <td><strong>能否预览特定演绎版中的资产？</strong></td>
      <td><strong>能否在特定查看器中预览资产？</strong></td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在维度查看器中预览3D资产</strong></p>
      <ul>
      <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择维查看器。</li>
      <li>要将图像返回到原始缩放图像，请选择 <strong>重置</strong>.</li>
      <li>要在显示设备上最大化查看器，请选择 <strong>全屏</strong>.</li>
      </ul>
      <p><strong>导航3D场景</strong></p>
      <ul>
      <li><p><strong>转动3D相机</strong>  — 围绕3D场景和对象绕行视图。</p> 鼠标：左键单击+拖动。</p> 触摸屏：按+拖动。</p></li>
      <li><p><strong>平移相机</strong>  — 左、右、上、下平移视图。</p> 鼠标：右键单击并拖动。</p> 触摸屏：双指按+拖动。</p></li>
      <li><p><strong>缩放相机</strong>  — 如果要在3D场景中移入和移出区域，请缩放相机。</p> 鼠标：滚轮。</p> 触摸屏：手指捏。</p></li>
      <li><p><strong>重新输入相机</strong>  — 围绕3D场景和对象绕行视图。</p> 鼠标：双击。</p> 触摸屏：双击。</li></ul></td>
      </tr>
      <tr>
      <td><p>图像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>演绎版</strong> 从列表中，选择要预览的特定演绎版。</li>
        </ul> <p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资产的查看器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>-</strong> 图标可分别增大和减小选定图像的缩放比例。要将图像恢复为原始缩放，请选择 <strong>重置</strong>.<br>如果您在触屏上，请双击图像以逐步放大。 当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>多媒体</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>演绎版</strong> 从列表中，选择要预览的特定演绎版。</li>
        </ul><p>选择要预览的高分辨率视频演绎版可能会导致视频显示被截断。 原因是演绎版预览在用于预览的嵌入式查看器上下文中，向您显示了客户所看到的确切分辨率。</p><p>在资产级别预览自适应视频集时，演绎版会分组为一个播放体验。 也就是说，自适应视频的大小会被适当地调整，以便观看，并在观看设备和连接速度的上下文中使用最佳分辨率进行回放。<br /></p><p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资产的查看器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>图像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资产的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 图标可分别增大和减小选定图像的缩放比例。要将图像恢复为原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触屏上，请双击图像以逐步放大。 当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p></td>
      </tr>
      <tr>
      <td>旋转集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资产的查看器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>-</strong> 图标可分别增大和减小选定图像的缩放比例。要将图像恢复为原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触屏上，请双击图像以逐步放大。 当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>混合媒体集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong> 从列表中，选择要应用于资产的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 图标可分别增大和减小选定图像的缩放比例。要将图像恢复为原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触屏上，请双击图像以逐步放大。 当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
      <tr>
      <td>轮播集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定查看器中预览资产</strong>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择要应用于资产的查看器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360视频<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>预览特定演绎版中的资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>演绎版</strong>，然后选择要预览的演绎版。</li>
        </ul> <p><strong>在特定查看器中预览资产</strong></p>
        <ul>
        <li>在页面的左上角附近，选择图标以显示下拉列表。 选择 <strong>查看器</strong>，然后选择要应用于资产的查看器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>-</strong> 图标可分别增大和减小选定图像的缩放比例。要将图像恢复为原始缩放，请选择 <strong>重置</strong>.<br /> 如果您在触屏上，请双击图像以逐步放大。 当您达到最大缩放比例时，再连按两次图像可重置缩放状态。横向拖动图像可进行平移。
</p> </td>
      </tr>
    </tbody>
    </table>
