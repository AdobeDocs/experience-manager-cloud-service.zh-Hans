---
title: content credentials集成
description: 集成到AEM Assets并在Assets View中展现的Content credentials可以提供资源历史记录的上下文，包括资源的创建方式以及参与创建该资源的人员。 就像数字内容的营养标签一样，Content credentials可以帮助提高透明度并与受众建立信任。
role: User
source-git-commit: 1c0ffe9d6e45f1d6b3574d1ac5611b2c2e2d00e0
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# 内容凭据 {#content-credentials}

各品牌比以往任何时候都更关注内容透明度、人工智能披露，以及防止资产被篡改。 Adobe的Content Authenticity Initiative (CAI)计划构建符合[内容来源和真实性联盟](https://c2pa.org/specifications/specifications/1.1/specs/C2PA_Specification.html#_trust_model) (C2PA)技术标准的工具。 content credentials是一种新型加密的、易于篡改的元数据，可帮助查看者了解内容的谱系并确保品牌资产的完整性。 它们可以包含范围广泛的来源数据，用于深入分析数字资产的历史。

此信息可能包括：

* **颁发者或签名者：**&#x200B;颁发数字签名以验证或签署资产的实体或公司的相关信息。
* **问题日期：**&#x200B;将内容凭据应用于资产的日期。
* **点数和使用情况：**&#x200B;有关资产制作者的信息，包括名称、社交媒体句柄或其他与身份相关的信息。
* **进程：**&#x200B;对资源进行任何编辑或修改的记录。
* **设备详细信息：**&#x200B;有关用于创建或编辑资源的应用程序或设备的信息。
* **使用的AI工具：**&#x200B;如果使用创作AI编辑或创建资产，则可能包含所使用的模型的名称。
* **其他相关信息：**&#x200B;可能还包含其他数据以帮助提供有关资产历史记录的更多上下文。

要获得完整的视图，[验证](https://contentcredentials.org/verify)可以提供更全面的资产历史记录洞察。

Adobe Experience Manager Assets现在支持Content credentials，使用户能够直接在AEM的Assets视图中查看Content credentials。 查看资源详细信息时，任何带有Content credentials（例如使用GenAI服务创建的资产）的图像都会在专用面板中显示清单详细信息。 如果下载、发布或共享资源，则这些Content credentials与资源将保持不变。

![资源](/help/assets/assets/content-credentials.png)

## 访问Content credentials {#access-content-credentials}

1. 转到Assets视图UI，然后从左窗格中单击&#x200B;**Assets**。
1. 导航到文件夹，然后选择所需的资产。
1. 单击&#x200B;**详细信息**&#x200B;并从最右边的窗格中选择`Cr pin`。 “Content credentials”选项卡显示有关资源的以下信息。
   1. **生成的图像：**&#x200B;应用Content credentials的日期和时间。
   1. **内容摘要：**指示资源是部分还是完全由AI生成，或者是如何编辑的。
      ![content credentials](/help/assets/assets/content-credentials1.png)
   1. **进程：**详细说明用于生成资源的应用程序、设备和AI工具(如Adobe Firefly)，以及随后进行的更改。
      ![进程](/help/assets/assets/CR-Process.png)
   1. **关于此Content credentials：**颁发者的名称以及颁发的日期和时间。
      ![颁发者](/help/assets/assets/CR-issuer.png)
