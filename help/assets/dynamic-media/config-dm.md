---
title: 配置Dynamic MediaCloud Service
description: 了解如何在Adobe Experience Manager as a Cloud Service中配置Dynamic Media。
contentOwner: Rick Brough
feature: Configuration,Dynamic Media
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 26afff3a39a2a80c1f730287b99f3fb33bff0673
workflow-type: tm+mt
source-wordcount: '3811'
ht-degree: 2%

---

# 关于配置Dynamic MediaCloud Service {#configuring-dynamic-media}

如果您将Adobe Experience Manager用于不同的环境，例如开发、暂存和实时生产，则请为每个环境配置Dynamic MediaCloud Service。

另请参阅 [配置Dynamic Media公司别名帐户](/help/assets/dynamic-media/dm-alias-account.md)

## Dynamic Media的架构图 {#architecture-diagram-of-dynamic-media}

以下架构图描述了Dynamic Media的工作方式。

凭借新的架构，Experience Manager负责主要源资产，并与Dynamic Media同步，以进行资产处理和发布：

1. 将主要源资产上传到Adobe Experience Manager as a Cloud Service后，将会将其复制到Dynamic Media。 届时，Dynamic Media将处理所有资源处理和演绎版生成，例如视频编码和图像的动态变量。
1. 生成呈现版本后，Experience Manageras a Cloud Service可以安全地访问和预览远程Dynamic Media呈现版本(不会将二进制文件发送回Experience Manageras a Cloud Service实例)。
1. 内容准备发布并批准后，它会触发Dynamic Media服务将内容推送到交付服务器并在CDN（内容交付网络）处缓存内容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>以下功能列表要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成CDN。 这些功能不支持任何其他自定义CDN。
>
>* [智能图像处理](/help/assets/dynamic-media/imaging-faq.md)
>* [缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2内容交付](/help/assets/dynamic-media/http2faq.md)
>* CDN级别的URL重定向
>* Akamai ChinaCDN（用于在中国实现最佳交付）

<!-- OBSOLETE CONTENT

## (Optional) Migrating Dynamic Media presets and configurations from 6.3 to 6.5 Zero Downtime {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

If you are upgrading Experience Manager as a Cloud Service Dynamic Media from 6.3 to 6.4 or 6.5 (which now includes the ability for zero downtime deployments), you are required to run the following curl command to migrate all your presets and configurations from `/etc` to `/conf` in CRXDE Lite.

>[!NOTE]
>
>If you run your Experience Manager as a Cloud Service instance in compatibility mode--that is, you have the compatibility packaged installed--you do not need to run these commands.

For all upgrades, either with or without the compatibility package, you can copy the default, out-of-the-box viewer presets that originally came with Dynamic Media by running the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

To migrate any custom viewer presets and configurations that you have created from `/etc` to `/conf`, run the following Linux curl command:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

-->

## 在Cloud Service中创建Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manageras a Cloud Service中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择“工具”图标，然后转到 **[!UICONTROL Cloud Service> Dynamic Media配置]**.
1. 在Dynamic Media配置浏览器页面的左侧窗格中，选择 **[!UICONTROL 全局]** (请勿选择左侧的文件夹图标 **[!UICONTROL 全局]**)。 然后选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建Dynamic Media配置]** 页面上，输入Dynamic Media帐户的公司管理员的标题、Dynamic Media帐户的电子邮件地址和密码，然后选择您所在的区域。 此信息通过在预配电子邮件中的Adobe向您提供。 如果您没有收到此电子邮件，请联系Adobe客户支持。
1. 选择 **[!UICONTROL 连接到Dynamic Media]**.
1. 在 **[!UICONTROL 更改密码]** 对话框，在 **[!UICONTROL 新密码]** 字段中，输入包含8-25个字符的新密码。 密码必须至少包含以下项之一：

   * 大写字母
   * 小写字母
   * 数字
   * 特殊字符： `# $ & . - _ : { }`

   此 **[!UICONTROL 当前密码]** 字段会刻意预填充并隐藏在交互中。

   如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

1. 在 **[!UICONTROL 重复密码]** 字段，重新键入新密码，然后选择 **[!UICONTROL 完成]**.

   新密码会在您选择时保存 **[!UICONTROL 保存]** 位于的右上角 **[!UICONTROL 创建Dynamic Media配置]** 页面。

   如果您选择 **[!UICONTROL 取消]** 在 **[!UICONTROL 更改密码]** 对话框，在保存创建的Dynamic Media配置时，仍必须输入新密码。

   另请参阅 [更改Dynamic Media密码](#change-dm-password).

1. 当连接成功时，可以设置以下内容：

   | 属性 | 描述 |
   |---|---|
   | 公司 | Dynamic Media帐户的名称。<br>**重要**：Experience Manager实例仅支持Cloud Service中的一个Dynamic Media配置；请勿添加多个配置。 一个Experience Manager实例上的多个Dynamic Media配置为 _非_ 受Adobe支持或推荐。<!-- CQDOC-19579 and CQDOC-19612 --><br>另请参阅 [配置Dynamic Media公司别名帐户](/help/assets/dynamic-media/dm-alias-account.md). |
   | 公司根文件夹路径 | 您公司的根文件夹路径。 |
   | 发布资产 | 您可以从以下三个选项中进行选择：<br>**[!UICONTROL 立即&#x200B;]**— 上传资产时，系统会摄取资产并立即提供URL/Embed。 发布资产无需用户干预。<br>**[!UICONTROL 激活]**  — 必须先显式发布资产，然后才能提供URL/嵌入链接。<br>**[!UICONTROL 选择性发布&#x200B;]**— 仅出于安全预览目的自动发布资产。 它们还可以明确发布到Experience Manageras a Cloud Service，而无需发布到DMS7以供在公共域中交付。 将来，此选项旨在将资产发布到Experience Manageras a Cloud Service并将资产发布到Dynamic Media，二者相互排斥。 也就是说，您可以将资源发布到DMS7，以便使用智能裁剪或动态呈现版本等功能。 或者，您也可以仅在Experience Manageras a Cloud Service中发布资源以供预览；在DMS7中不会发布这些相同的资源以供在公共域中交付。 |
   | 安全预览服务器 | 用于指定安全呈现版本预览服务器的URL路径。 也就是说，在生成演绎版之后，Experience Manageras a Cloud Service可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manageras a Cloud Service实例)。<br>除非您有特殊安排使用您自己公司的服务器或特殊服务器，否则Adobe建议您保留指定的此设置。 |
   | 同步所有内容 | 默认选中。 如果您要在同步到Dynamic Media的过程中有选择地包含或排除资源，请取消选择此选项。 取消选择此选项可从以下两种Dynamic Media同步模式中进行选择：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 默认启用&#x200B;]**— 默认情况下，该配置将应用于所有文件夹，除非您专门将文件夹标记为排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 默认禁用]**  — 除非您明确将选定的文件夹标记为同步到Dynamic Media，否则该配置不会应用于任何文件夹。<br>要将选定的文件夹标记为同步到Dynamic Media，请选择一个资源文件夹，然后在工具栏中，选择 **[!UICONTROL 属性]**. 在 **[!UICONTROL 详细信息]** 选项卡，在 **[!UICONTROL Dynamic Media同步模式]** 从以下三个选项中进行选择。 完成后，选择 **[!UICONTROL 保存]**. _请记住：如果选择，则以下三个选项不可用&#x200B;**同步所有内容**更早。_ 另请参阅 [在Dynamic Media中使用文件夹级别的选择性发布](/help/assets/dynamic-media/selective-publishing.md).<br>**[!UICONTROL 已继承&#x200B;]**— 文件夹中没有显式同步值。 相反，文件夹会从其上级文件夹之一继承同步值，或者在云配置中继承默认模式。 继承的详细状态通过工具提示显示。<br>**[!UICONTROL 为子文件夹启用]**  — 包含此子树中的所有内容，以便同步到Dynamic Media。 文件夹特定的设置会覆盖云配置中的默认模式。<br>**[!UICONTROL 已为子文件夹禁用&#x200B;]**— 从同步到Dynamic Media中排除此子树中的所有内容。 |

   >[!NOTE]
   >
   >Dynamic Media 不支持版本控制。此外，仅当出现以下情况时延迟激活才适用 **[!UICONTROL 发布资产]** 在“编辑Dynamic Media配置”页面中，将设置为 **[!UICONTROL 激活时]**. 然后，直到首次激活资产为止。
   >
   >
   >激活资产后，所有更新都会立即实时发布到S7交付。

   ![dynamicmediaconfiguration2已更新](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。新的Dynamic Media密码和配置已保存。 如果您选择 **[!UICONTROL 取消]** 而是不会进行密码更新。
1. 在 **[!UICONTROL 配置Dynamic Media]** 对话框，选择 **[!UICONTROL 确定]** 以开始配置。

   >[!IMPORTANT]
   >
   >当设置完新的Dynamic Media配置时，您将在Experience Manageras a Cloud Service的收件箱中收到状态通知。
   >
   >此收件箱通知会告知您配置是否成功。
   > 请参阅 [新Dynamic Media配置疑难解答](#troubleshoot-dm-config) 和 [您的收件箱](/help/sites-cloud/authoring/inbox.md) 以了解更多信息。

1. 为了在发布Dynamic Media内容之前安全地预览该内容，Experience Manageras a Cloud Service会使用基于令牌的验证，默认情况下，Experience Manager作者会预览Dynamic Media内容。 但是，您可以 *允许列表* 更多IP，以便让用户能够安全地预览内容。 要在Experience Manageras a Cloud Service中设置此操作，请参阅 [为图像服务器配置Dynamic Media发布设置 — “安全”选项卡](/help/assets/dynamic-media/dm-publish-settings.md#security-tab). <!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

现在，您完成了基本配置；接下来可以使用Dynamic Media。

如果您想进一步自定义配置，如启用ACL （访问控制列表）权限，您可以选择完成以下任何任务 [在Dynamic Media中配置高级设置](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

### 新Dynamic Media配置疑难解答 {#troubleshoot-dm-config}

当设置完新的Dynamic Media配置时，您将在Experience Manageras a Cloud Service的收件箱中收到状态通知。 此通知会告知您配置是否成功，如收件箱中相应图像的内容所示。

![Experience Manager收件箱成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件箱失败](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另请参阅 [您的收件箱](/help/sites-cloud/authoring/inbox.md).

**要对新的Dynamic Media配置进行故障排除，请执行以下操作：**

1. 在“Experience Manageras a Cloud Service”页面的右上角附近，选择铃铛图标，然后选择 **[!UICONTROL 查看全部]**.
1. 在收件箱页面上，选择成功通知以读取配置的状态和日志的概述。

   如果配置失败，请选择与以下屏幕快照类似的失败通知。

   ![Dynamic Media设置失败](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在 **[!UICONTROL DMSETUP]** 页中，查看描述故障的配置详细资料。 特别是，请注意任何错误消息或错误代码。 请联系Adobe客户支持并提供此信息。

   ![Dynamic Media设置页面](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 更改Dynamic Media密码 {#change-dm-password}

Dynamic Media中的密码过期时间设置为自当前系统日期起100年。

密码必须至少包含以下项之一：

* 大写字母
* 小写字母
* 数字
* 特殊字符： `# $ & . - _ : { }`

如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

选择后会保存更改后的密码 **[!UICONTROL 保存]** 位于的右上角 **[!UICONTROL 编辑Dynamic Media配置]** 页面。

1. 在Experience Manageras a Cloud Service中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择“工具”图标，然后转到 **[!UICONTROL Cloud Service> Dynamic Media配置]**.
1. 在Dynamic Media配置浏览器页面的左侧窗格中，选择 **[!UICONTROL 全局]**. 请勿选择左侧的文件夹图标 **[!UICONTROL 全局]**. 然后，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL 编辑Dynamic Media配置]** 页面，紧接在 **[!UICONTROL 密码]** 字段，选择 **[!UICONTROL 更改密码]**.
1. 在 **[!UICONTROL 更改密码]** 对话框中，执行以下操作：

   * 在 **[!UICONTROL 新密码]** 字段中，输入新密码。

     此 **[!UICONTROL 当前密码]** 字段会刻意预填充并隐藏在交互中。

   * 在 **[!UICONTROL 重复密码]** 字段，重新键入新密码，然后选择 **[!UICONTROL 完成]**.

1. 在右上角 **[!UICONTROL 编辑Dynamic Media配置]** 页面，选择 **[!UICONTROL 保存]**，然后选择 **[!UICONTROL 确定]**.

## （可选）在Dynamic Media中配置高级设置{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

要进一步自定义Dynamic Media的配置和设置，或优化其性能，您可以完成以下一项或多项操作 _可选_ 任务：

* [（可选）在Dynamic Media中启用ACL权限](#optional-enable-acl)
* [（可选）Dynamic Media设置的设置和配置](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（可选）调整Dynamic Media的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （可选）在Dynamic Media中启用访问控制列表权限 {#optional-enable-acl}

在AEM上运行Dynamic Media时，它会当前转发 `/is/image` 请求无需检查PlatformServerServlet上的ACL（访问控制列表）权限即可安全预览图像服务。 不过，你可以， _启用_ ACL权限。 这样做会转发授权的 `/is/image` 请求。 如果用户无权访问资产，则会显示“403 — 禁止访问”错误。

**要在Dynamic Media中启用ACL权限，请执行以下操作：**

1. 在Experience Manager中，导航到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 此时将打开一个新的浏览器选项卡，并显示 **[!UICONTROL Adobe Experience Manager Web控制台配置]** 页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，滚动到名称 _Adobe CQ Scene7平台服务器_.

1. 在名称的右侧，选择铅笔图标(**[!UICONTROL 编辑配置值]**)。

1. 在 **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** 页面上，选中以下两个设置的复选框：

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name`  — 启用时，此设置将缓存权限结果两分钟（默认值）以保存。
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name`  — 启用后，此设置将在用户通过Dynamic Media图像服务器预览资源时验证用户的访问权限。

   ![在Dynamic Media - Scene7模式下启用访问控制列表设置](/help/assets/dynamic-media/assets/acl.png)

1. 在页面的右下角附近，选择 **[!UICONTROL 保存]**.

### （可选）Dynamic Media设置的设置和配置 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic用户界面更改您的Dynamic Media设置。

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account. -->

安装和配置任务包括：

* [为图像服务器配置Dynamic Media发布设置](#publishing-setup-for-image-server)
* [配置Dynamic Media常规设置](#configuring-application-general-settings)
* [配置颜色管理](#configuring-color-management)
* [编辑所支持格式的MIME类型](#editing-mime-types-for-supported-formats)
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 为图像服务器配置Dynamic Media发布设置 {#publishing-setup-for-image-server}

“Dynamic Media发布设置”页面可建立默认设置，以确定如何将资源从AdobeDynamic Media服务器传递到网站或应用程序。

请参阅 [为图像服务器配置Dynamic Media发布设置](/help/assets/dynamic-media/dm-publish-settings.md).

#### 配置Dynamic Media常规设置 {#configuring-application-general-settings}

配置Dynamic Media **[!UICONTROL 发布服务器名称]** URL和 **[!UICONTROL 原始服务器名称]** URL。 您还可以指定 **[!UICONTROL 上载到应用程序]** 设置和 **[!UICONTROL 默认上载选项]** 所有这一切都基于您的特定用例。

请参阅 [配置Dynamic Media常规设置](/help/assets/dynamic-media/dm-general-settings.md).

#### 配置颜色管理 {#configuring-color-management}

通过Dynamic Media色彩管理，您可以对资源进行色彩校正。 通过颜色校正，摄取的资产可保留其颜色空间(RGB、CMYK、灰色)和嵌入的颜色配置文件。 请求动态演绎版时，将使用CMYK、RGB或灰度输出将图像颜色校正到目标颜色空间中。

请参阅 [配置图像预设](/help/assets/dynamic-media/managing-image-presets.md).

要配置默认颜色属性以便在请求图像时启用颜色校正，请执行以下操作：

1. 打开 [Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后使用在配置期间提供的凭据登录到您的帐户。
1. 转到 **[!UICONTROL 设置>应用程序设置]**.
1. 展开&#x200B;**[!UICONTROL 发布设置]**&#x200B;区域，然后选择&#x200B;**[!UICONTROL 图像服务器]**。设置发布实例的默认设置时，将&#x200B;**[!UICONTROL 发布上下文]**&#x200B;设置为&#x200B;**[!UICONTROL 图像提供]**。
1. 滚动到必须更改的属性，例如 **[!UICONTROL 颜色管理属性]** 区域。
您可以设置以下颜色校正属性：

   | 属性 | 描述 |
   |---|---|
   | CMYK默认颜色空间 | 默认CMYK颜色配置文件的名称。 |
   | 灰度默认颜色空间 | 默认灰色颜色配置文件的名称。 |
   | RGB默认色彩空间 | 默认RGB颜色配置文件的名称。 |
   | 颜色转换调色 | 指定渲染方法。 可接受的值为： **[!UICONTROL 可感知]**， **[!UICONTROL 相对色度]**， **[!UICONTROL 饱和度]**， **[!UICONTROL 绝对色度]**. Adobe推荐 **[!UICONTROL 相对]** 作为默认值。 |

1. 选择&#x200B;**[!UICONTROL 保存]**。

例如，可以将 **[!UICONTROL RGB 默认色彩空间]**&#x200B;设置为 *sRGB*，将 **[!UICONTROL CMYK 默认色彩空间]**&#x200B;设置为 *WebCoated*。

这样做将执行以下操作：

* 为RGB和CMYK图像启用颜色校正。
* 假定没有颜色配置文件的RGB图像在 *sRGB* 颜色空间。
* 假定没有颜色配置文件的CMYK图像在 *WebCoat* 颜色空间。
* 返回RGB输出的动态演绎版，在 *sRGB* 颜色空间。
* 返回CMYK输出的动态演绎版，在 *WebCoat* 颜色空间。

#### 编辑所支持格式的MIME类型 {#editing-mime-types-for-supported-formats}

您可以定义Dynamic Media处理的资源类型，并自定义高级资源处理参数。 例如，您可以指定资产处理参数，以执行以下操作：

* 将Adobe PDF转换为eCatalog资源。
* 将Adobe Photoshop文档(.platform)转换为PSD横幅模板资源以进行个性化。
* 栅格化Adobe Illustrator文件(.AI)或Adobe Photoshop封装的PostScript®文件(.EPS)。
* [视频配置文件](/help/assets/dynamic-media/video-profiles.md) 和 [图像配置文件](/help/assets/dynamic-media/image-profiles.md) 分别用于定义视频和图像的处理。

请参阅 [上传资源](/help/assets/add-assets.md).

**要编辑所支持格式的MIME类型，请执行以下操作：**

1. 以产品管理员身份登录到您的Experience Manageras a Cloud Service。
1. 在Experience Manageras a Cloud Service中，选择Experience Manageras a Cloud Service徽标以访问全局导航控制台，然后转到 **[!UICONTROL 常规>CRXDE Lite]**.

   如果您无权访问CRXDE Lite，请参阅 [使用CRXDE Lite](/help/implementing/developing/tools/crxde.md).

1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择MIME类型。
1. 在CRXDE Lite页面的右侧，位于下部：

   * 双击 **[!UICONTROL 已启用]** 字段。 默认情况下，将启用所有资源MIME类型(设置为 **[!UICONTROL true]**)，这意味着资产将同步到Dynamic Media以供处理。 如果要从处理中排除此资源MIME类型，请将此设置更改为 **[!UICONTROL false]**.

   * 双选 **[!UICONTROL jobParam]** 以打开其关联的文本字段。 请参阅 [支持的MIME类型](/help/assets/file-format-support.md) 以获取可用于给定MIME类型的允许处理参数值列表。

1. 执行下列操作之一：
   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页面的菜单栏上，选择 **[!UICONTROL 全部保存]**.

1. 在页面的左上角，选择 **[!UICONTROL CRXDE Lite]** 以返回Experience Manageras a Cloud Service。

#### 为不支持的格式添加MIME类型 {#adding-mime-types-for-unsupported-formats}

您可以为Experience Manager Assets中不支持的格式添加自定义MIME类型。 要确保Experience Manager不会删除您在CRXDE Lite中添加的任何新节点，请将MIME类型移动到之前 `image_`. 另外，请确保将其启用值设置为 **[!UICONTROL false]**.

**为不支持的格式添加MIME类型：**

1. 以产品管理员身份登录到您的Experience Manageras a Cloud Service。
1. 从Experience Manageras a Cloud Service，转到 **[!UICONTROL “工具”>“操作”>“Web控制台”]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 此时将打开一个新的浏览器选项卡，并显示 **[!UICONTROL Adobe Experience Manager Web控制台配置]** 页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名称的右侧，选择 **[!UICONTROL 编辑配置值]** （铅笔图标）。

   ![编辑配置值](assets/2019-08-02_16-44-56.png)

1. 在 **Adobe CQ Scene7 Asset MIME类型服务** 页面上，选择任意加号图标&lt;+>。 在表格中选择加号以添加新MIME类型的位置微不足道。

   ![Adobe CQ Scene7资源Mime类型服务](assets/2019-08-02_16-27-27.png)

1. 类型 `DWG=image/vnd.dwg` 在刚刚添加的空文本字段中。

   此 `DWG=image/vnd.dwg` MIME类型仅用于示例目的。 您在此处添加的MIME类型可以是任何其他不受支持的格式。

   ![添加DWG MIME类型](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，选择 **[!UICONTROL 保存]**.

   此时，您可以关闭已打开Adobe Experience Manager Web控制台配置页面的浏览器选项卡。

1. 返回到具有已打开的Experience Manageras a Cloud Service控制台的浏览器选项卡。
1. 从Experience Manageras a Cloud Service，转到 **[!UICONTROL “工具”>“常规”>“CRXDE Lite”]**.

   如果您无权访问CRXDE Lite，请参阅 [使用CRXDE Lite](/help/implementing/developing/tools/crxde.md).

   ![“工具”>“常规”>“CRXDE Lite”](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖动MIME类型 `image_vnd.dwg` 将它直接放在上面 `image_` 在树中，如下面的屏幕截图所示。

   ![编辑CRXDE Lite的DWG文件](assets/crxdelite_cqdoc-14627.png)

1. 使用MIME类型 `image_vnd.dwg` 仍被选中，从 **[!UICONTROL 属性]** 选项卡，在 **[!UICONTROL 已启用]** 行，在 **[!UICONTROL 值]** 列标题，双击该值。 此 **[!UICONTROL 值]** 此时将打开下拉列表。
1. 类型 `false` 在字段中(或选择 **[!UICONTROL false]** （从下拉列表中）。

   ![在CRXDE Lite中编辑MIME类型](assets/2019-08-02_16-60-30.png)

1. 在“CRXDE Lite”页面的左上角附近，选择 **[!UICONTROL 全部保存]**.

### （可选）调整Dynamic Media的性能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

保留Dynamic Media <!--(with `dynamicmedia_scene7` run mode)--> Adobe建议通过以下同步性能/可扩展性微调提示来运行顺畅：

* [更新预定义的作业参数以处理不同的文件格式](#update-job-para).
* [更新预定义的Granite工作流队列（视频资产）工作线程](#update-granite-workflow-queue-worker-threads-video)
* [更新预定义的Granite临时工作流队列（图像和非视频资产）工作线程](#update-granite-transient-workflow-queue-worker-threads-images).
* [更新与Dynamic Media Classic (Scene7)服务器的最大上传连接数](#update-max-s7-upload-connections).

#### 更新预定义的作业参数以处理不同的文件格式 {#update-job-para}

您可以调整作业参数，以便在上载文件时更快地处理。 例如，如果上传PSD文件，但不希望将它们作为模板处理，则可以将图层提取设置为false（关闭）。 在这种情况下，所调整的作业参数如下所示： `process=None&createTemplate=false`.

如果确实要启用模板创建，请使用以下参数： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议为PDF、PostScript®和PSD文件使用以下“优化”作业参数：

| 文件类型 | 建议的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新其中的任何参数，请参见 [编辑所支持格式的MIME类型](#editing-mime-types-for-supported-formats).

另请参阅 [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats).

#### 更新预定义的Granite工作流队列（视频资产）工作线程 {#update-granite-workflow-queue-worker-threads-video}

Granite工作流队列用于非临时工作流。 在Dynamic Media中，它以前使用 **[!UICONTROL Dynamic Media编码视频]** 工作流。

>[!NOTE]
>
>您必须以产品管理员身份登录Experience Manager as a Cloud Service才能完成此任务。

如果您无权访问OSGi，请参阅 [OSGi配置](/help/implementing/developing/components/overview.md#osgi-configuration).

**要更新预定义的Granite工作流队列（视频资产）工作线程，请执行以下操作：**

1. 导航到 `https://<server>/system/console/configMgr` 和搜索 **队列： Granite工作流队列**.

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，将数字更改为所需的值。

   默认情况下，最大并行作业数取决于可用CPU核心的数量。 例如，在4核服务器上，它分配两个工作线程。 （介于0.0和1.0之间的值基于比率，或任何大于1的数字均分配工作线程数。）

   对于大多数用例，0.5的默认设置就足够了。

   ![作业处理队列的配置](assets/chlimage_1-1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新预定义的Granite临时工作流队列工作线程 {#update-granite-transient-workflow-queue-worker-threads-images}

Granite传输工作流队列用于 **[!UICONTROL DAM更新资产]** 工作流。 在Dynamic Media中，它用于图像和非视频资源的摄取和处理。

>[!NOTE]
>
>您必须以产品管理员身份登录Experience Manager as a Cloud Service才能完成此任务。

**要更新预定义的Granite临时工作流队列工作线程，请执行以下操作：**

1. 导航至 **Adobe Experience Manager Web控制台配置** 在 `http://<host>:<port>/system/console/configMgr`
1. 搜索 **队列：Granite临时工作流队列**.

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在 **[!UICONTROL 最大并行作业数]** 字段，将数字更改为所需的值。

   您可以增加 **[!UICONTROL 最大并行作业数]** 以充分支持将文件大量上传到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（如初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（例如内核数量的两倍）可能会对其他并发活动产生负面影响。 因此，请根据特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新与Dynamic Media Classic (Scene7)服务器的最大上传连接数 {#update-max-s7-upload-connections}

Dynamic Media Classic (Scene7)上传连接设置将Experience Manager资源同步到Dynamic Media Classic服务器。

>[!NOTE]
>
>您必须以产品管理员身份登录Experience Manager as a Cloud Service才能完成此任务。

**要更新到Dynamic Media Classic (Scene7)服务器的最大上传连接数，请执行以下操作：**

1. 导航到 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在 **[!UICONTROL 连接数]** 字段，或 **[!UICONTROL 活动作业超时]** 字段，或同时使用两者，根据需要更改数字。

   此 **[!UICONTROL 连接数]** 设置可控制Experience Manager到Dynamic Media上传时允许的最大HTTP连接数。 通常，预定义十个连接值就足够了。

   此 **[!UICONTROL 活动作业超时]** 设置确定在投放服务器中发布已上传Dynamic Media资源的等待时间。 此值默认为2100秒或35分钟。

   对于大多数用例，设置2100就足够了。

   ![Adobe Scene7上传服务](assets/chlimage_1-2.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

<!-- NOTE - OBSOLETE that customisations to replication agents to transform content are no longer used; the following content is obsolete now 

### (Optional) Filtering assets for replication {#optional-filtering-assets-for-replication}

In non-Dynamic Media deployments, you replicate *all* assets (both images and video) from your Experience Manager as a Cloud Service author environment to the Experience Manager as a Cloud Service publish node. This workflow is necessary because the Experience Manager as a Cloud Service publish servers also deliver the assets.

However, in Dynamic Media deployments, because assets are delivered by way of the cloud service, there is no need to replicate those same assets to Experience Manager as a Cloud Service publish nodes. Such a "hybrid publishing" workflow avoids extra storage costs and longer processing times to replicate assets. Other content, such as Site pages, continue to be served from the Experience Manager as a Cloud Service publish nodes.

The filters provide a way for you to *exclude* assets from being replicated to the Experience Manager as a Cloud Service publish node.

#### Using default asset filters for replication {#using-default-asset-filters-for-replication}

If you are using Dynamic Media for imaging and/or video, then you can use the default filters that we provide as-is. The following filters are active by default:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Mimetype</strong></td>
   <td><strong>Renditions</strong></td>
  </tr>
  <tr>
   <td>Dynamic Media Image Delivery</td>
   <td><p>filter-images</p> <p>filter-sets</p> <p> </p> </td>
   <td><p>Starts with <strong>image/</strong></p> <p>Contains <strong>application/</strong> and ends with <strong>set</strong>.</p> </td>
   <td>The out-of-the-box "filter-images" (applies to single images assets, including interactive images) and "filter-sets" (applies to Spin Sets, Image Sets, Mixed Media Sets, and Carousel Sets) will:
    <ul>
     <li>Exclude from replication the original image and static image renditions.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Dynamic Media Video Delivery</td>
   <td>filter-video</td>
   <td>Starts with <strong>video/</strong></td>
   <td>The out-of-the-box "filter-video" will:
    <ul>
     <li>Exclude from replication the original video and static thumbnail renditions.<br /> <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Filters apply to mime types and cannot be path specific.

#### Customizing asset filters for replication {#customizing-asset-filters-for-replication}

1. In Experience Manager as a Cloud Service, select the Experience Manager as a Cloud Service logo to access the global navigation console and select the **[!UICONTROL Tools > General > CRXDE Lite]**.
1. In the left folder tree, navigate to `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` to review the filters.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. To define the Mime Type for the filter, you can locate the Mime Type as follows:

   In the left rail, expand `content > dam > <locate_your_asset> > jcr:content > metadata`, and then in the table, locate `dc:format`.

   The following graphic is an example of an asset's path to `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Notice that the `dc:format` for the asset `Fiji Red.jpg` is `image/jpeg`.

   To have this filter apply to all images, regardless of their format, set the value to `image/*` where `*` is a regular expression that is applied to all images of any format.

   To have the filter apply only to images of the type JPEG, enter a value of `image/jpeg`.

1. Define what renditions you want to include or exclude from replication.

   Characters that you can use to filter for replication include the following:

<table>
 <tbody>
  <tr>
   <td><strong>Character to use</strong></td>
   <td><strong>How it filters assets for replication</strong></td>
  </tr>
  <tr>
   <td>*</td>
   <td>Wildcard character<br /> </td>
  </tr>
  <tr>
   <td>+</td>
   <td>Includes assets for replication.</td>
  </tr>
  <tr>
   <td>-</td>
   <td>Excludes assets from replication.</td>
  </tr>
 </tbody>
</table>

   Navigate to `content/dam/<locate your asset>/jcr:content/renditions`.

   The following graphic is an example of an asset's renditions.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   If you only wanted to replicate the original, then you would enter `+original`.

   -->
