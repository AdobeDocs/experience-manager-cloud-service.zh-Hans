---
title: 使用规则集转换URL
description: 了解如何在Dynamic Media中部署规则集以转换URL。 规则集是使用脚本语言(如JavaScript™)编写的一组说明，这些说明可评估XML数据并在数据满足特定条件时采取某些操作。
role: Business Practitioner
exl-id: f8010125-ba89-406a-bede-f6aa2f858c70
source-git-commit: d3ee23917eba4a2e4ae1f2bd44f5476d2ff7dce1
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 5%

---

# 使用规则集转换URL {#using-rulesets-to-transform-urls}

您可以在Dynamic Media中部署规则集以转换URL。 规则集是使用脚本语言(如JavaScript™)编写的一组说明，这些说明可评估XML数据并在数据满足特定条件时采取某些操作。 每个规则都至少包含一个条件和一个操作。 规则会根据条件来评估XML数据，如果满足条件，则会采取相应的操作。 规则集示例包括：

* 添加MIME类型后缀。 许多服务和网站都需要图像后缀，例如向URL添加`.jpg`。
* 为SEO（搜索引擎优化）创建URL的文件夹路径。

   请参阅[AdobeDynamic Media Classic如何支持SEO](/help/assets/dynamic-media/assets/s7_seo.pdf)。

* 将元数据添加到URL以进行SEO（搜索引擎优化）。

   请参阅[AdobeDynamic Media Classic如何支持SEO](/help/assets/dynamic-media/assets/s7_seo.pdf)。

* 设置内容处置以触发下载。
* 简化图像提供模板URL以进行个性化。 例如，将`rgb{XX,YY,ZZ}`转换为RTF就绪型`\redXX\greenYY\blueZZ`

* 请求要编码的某些字符（如`$`、`{`和`}`），以及某些要向ImageServer解码的字符。 例如，Facebook不适用于包含特殊字符的URL。

   请参阅[从URL中删除特殊字符](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html)。

在Dynamic Media上下文中，使用基于XML的系统来管理资产信息的网站可以将XML文件上传到Dynamic Media。 您可以将其中一个文件指定为用于提供Dynamic Media资产的预处理规则集文件。 此文件会重新构建标准URL协议格式，以符合与Dynamic Media集成的系统的公司逻辑。 指定XML文件作为规则集定义文件路径。

>[!CAUTION]
>
>使用规则集时请务必谨慎；它们可阻止Dynamic Media内容显示在您的网站上。

有一些示例规则集可以帮助您创建自己的规则集。
请参阅[规则集引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html)。

与创建所有规则集一样，在使用XML验证程序（如xmlvalid）上载XML文件之前，请确保XML文件有效。
另请参阅[规则集疑难解答](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html)。

此外，请确保首先在暂存环境中测试规则集，该测试环境不会影响您的实时生产环境。
生产环境和暂存环境通常需要不同的登录方式。

请参阅[AdobeDynamic Media Classic桌面应用程序以了解登录信息](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app)。

<!-- OBSOLETE CONTENT * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

另请参阅[在规则集](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html)中使用“asset”而不是“is”图像。

**要部署XML规则集，请执行以下操作：**

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   您的凭据和登录详细信息由Adobe在配置时提供。 如果您没有此信息，请联系技术支持。

1. 通过执行以下操作，上传规则集文件：

   * 在全局导航栏上，单击&#x200B;**[!UICONTROL Upload]**。
   * 在&#x200B;**[!UICONTROL Upload]**&#x200B;页面左上角附近，单击&#x200B;**[!UICONTROL Browse]**。
   * 在&#x200B;**[!UICONTROL 打开]**&#x200B;对话框中，浏览到您的规则集文件(XML)。
   * 选择文件，然后单击&#x200B;**[!UICONTROL Open]**。
   * 在&#x200B;**[!UICONTROL Upload]**&#x200B;页面的右侧，为规则集文件选择目标文件夹。
   * 在页面底部附近，确保选中上传后发布。
   * 在页面的右下角，单击&#x200B;**[!UICONTROL 提交上传]**。
   * 在全局导航栏上，单击&#x200B;**[!UICONTROL 作业]**&#x200B;以检查上传作业的状态。 当&#x200B;**[!UICONTROL 作业]**&#x200B;页面上的&#x200B;**[!UICONTROL 状态]**&#x200B;列显示上传完成时，请继续执行后续步骤。

1. 在页面顶部附近的导航栏中，单击&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**。
1. 在&#x200B;**[!UICONTROL 图像服务器发布]**&#x200B;页面的&#x200B;**[!UICONTROL 目录管理]**&#x200B;组下，找到&#x200B;**[!UICONTROL 规则集定义文件路径]**，然后单击&#x200B;**[!UICONTROL 选择]**。
1. 在&#x200B;**[!UICONTROL 择规则集定义文件 (XML)]** 页面上，浏览至您的规则集文件，然后在页面的右下角单击&#x200B;**[!UICONTROL 选择]**。
1. 在“设置”页的右下角，单击&#x200B;**[!UICONTROL 关闭]**。
1. 运行图像服务器发布作业。

   规则集条件将应用于对实时Dynamic Media图像服务器的请求。

   如果更改规则集文件，则当您重新上传和重新发布更新的规则集文件时，将立即应用更改。
