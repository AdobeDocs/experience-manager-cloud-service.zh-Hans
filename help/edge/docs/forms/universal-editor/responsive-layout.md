---
title: 了解通用编辑器 — 响应模式
description: 本文介绍了如何使用通用编辑器中的不同模拟器预览表单，以在创作过程中可视化表单的外观。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# WYSIWYG创作中的响应模式

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将您的正式地址中的电子邮件发送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub组织名称和存储库名称。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>


[通用编辑器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)允许您使用不同的模拟器预览Edge Delivery Services Forms，以便在创作过程中查看表单的外观。

响应模式允许开发人员设计自动适应不同屏幕大小的布局，包括台式机、平板电脑和移动设备。 通用编辑器支持适用于台式机、平板电脑和移动设备的模拟器。 您可以根据屏幕大小设置高度和宽度，然后执行以下操作：

* 设置方向
* 指定宽度和高度
* 更改方向

## 在不同设备的响应模式下预览Forms

通用编辑器在屏幕的右上角提供了&#x200B;**模拟器**&#x200B;图标，允许您预览不同设备大小的页面，并测试响应式设计的行为，以获得更好的用户体验。

要了解通用编辑器如何在不同屏幕大小上呈现表单，请执行以下步骤：

1. 在通用编辑器中打开窗体以进行编辑。
1. 选择通用编辑器工具栏上可用的![模拟器图标](/help/edge/docs/forms/universal-editor/assets/emulator.png){height=2%，width=2%}，然后单击模拟器图标以显示该选项。

   ![响应模式](/help/edge/docs/forms/universal-editor/assets/universal-editor-emulator.png)

1. 选择一个选项以在选定的设备上在通用编辑器中模拟表单：桌面、平板电脑、移动设备。

   ![响应模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=40%，height=40%}

   默认情况下，编辑器会在桌面布局中打开，其高度和宽度由浏览器自动确定。 或者，您可以在移动或平板电脑设备上模拟表单。 您还可以自定义自定义设备的屏幕宽度和高度。

通用编辑器提供了不同的模拟器来预览各种设备上的表单。 下表列出了可用的模拟器类型及其相应的设备表示形式：

<table border="1" style="text-align:" left; border-collapse: collapse;">
    <tr>
        <th style="width: 20%">模拟器类型</th>
        <th style="width: 80%">设备图像</th>
    </tr>
    <tr>
        <td style="width: 20%">桌面</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-desktop.png" alt="桌面模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">平板电脑</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-tab.png" alt="平板电脑模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">移动设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-mobile.png" alt="移动设备模拟器" style="width: auto; height: auto"></td>
    </tr>
    <tr>
        <td style="width: 20%">自定义设备</td>
        <td style="width: 80%"><img src="/help/edge/docs/forms/universal-editor/assets/universal-editor-custom.png" alt="自定义设备模拟器" style="width: auto; height: auto"></td>
    </tr>
</table>

在不同设备上预览表单时，可以使用&#x200B;**屏幕旋转器**&#x200B;图标在纵向和横向之间切换。 它可帮助开发人员测试响应式设计如何适应各种设备上的屏幕旋转。

## 另请参阅

{{universal-editor-see-also}}
