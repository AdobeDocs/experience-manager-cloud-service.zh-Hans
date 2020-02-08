---
title: 将水印添加到数字资产
description: 了解如何使用“水印”功能向资产添加数字水印。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# 添加水印 {#watermarking}

Adobe Experience Manager(AEM)资产中的水印功能允许您向资产添加数字水印，从而帮助用户验证资产的真实性和版权所有权。 AEM资产支持用作PNG和JPEG文件上的水印的文本。

要能够对资产应用水印，请在DAM更新资产工作流中添加水印步骤。

1. 点按／单击AEM徽标，然后转到工具 **** >工 **[!UICONTROL 作流]** >模 **[!UICONTROL 型]**。
1. 在“工作流模型”页面中，选择“ **[!UICONTROL DAM更新资产”工作流]** ，然后单击 **[!UICONTROL 编辑]**。

1. 从侧面板中，将添加水 **[!UICONTROL 印步骤拖到]** DAM更新资产工作流。

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>将“添加水印”步骤放在“进程缩略图”步骤之前的任意位置。

1. 打开添 **[!UICONTROL 加水印]** ，以显示其属性。
1. 在“参 **[!UICONTROL 数]** ”选项卡中，在各个字段中指定有效值，包括文本、字体类型、大小、颜色、位置、方向等。 要确认更改，请点按／单击完成图标。

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. 使用“水 **[!UICONTROL 印”步骤保存]** DAM更新资产工作流。
1. 从资产用户界面中，上传示例资产。 在您在上述步骤中配置的位置，将显示带有字体大小、颜色等的水印。
