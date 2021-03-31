---
title: 配置 Dynamic Media 云服务
description: 了解如何将Adobe Experience Manager中的Dynamic Media配置为Cloud Service。
topic: 管理员
role: 管理员，业务从业者
translation-type: tm+mt
source-git-commit: 6fa911f39d707687e453de270bc0f3ece208d380
workflow-type: tm+mt
source-wordcount: '4057'
ht-degree: 4%

---


# 关于配置Dynamic Media Cloud Service {#configuring-dynamic-media}

如果您将Adobe Experience Manager用于不同的环境，如开发、升级和实时生产，请为这些环境中的每个配置Dynamic MediaCloud Services。

## Dynamic Media{#architecture-diagram-of-dynamic-media}的架构图

以下架构图描述了Dynamic Media的工作方式。

借助新的架构，Experience Manager负责主源资源并与Dynamic Media同步以处理和发布资源：

1. 将主源资产作为Cloud Service上传到Adobe Experience Manager时，该资产将复制到Dynamic Media。 此时，Dynamic Media将处理所有资产处理和再现生成，如图像的视频编码和动态变体。
1. 生成演绎版后，Experience Manager作为Cloud Service可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件作为Cloud Service实例发送回Experience Manager)。
1. 在内容准备好发布和批准后，它会触发Dynamic Media服务，将内容推送到投放服务器并在CDN(内容投放网络)缓存内容。

![chlimage_1-550](assets/chlimage_1-550.png)

>[!NOTE]
>
>以下功能列表要求您使用与Adobe Experience Manager - Dynamic Media捆绑的现成CDN。 这些功能不支持任何其他自定义CDN。
>
>* [智能图像处理](/help/assets/dynamic-media/imaging-faq.md)
>* [缓存失效](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md)
>* [热链接保护](/help/assets/dynamic-media/hotlink-protection.md)
>* [HTTP/2 内容交付](/help/assets/dynamic-media/http2faq.md)
>* 在CDN级别重定向URL
>* Akamai ChinaCDN(在中国实现最佳投放)


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

## 在Cloud Services{#configuring-dynamic-media-cloud-services}中创建Dynamic Media配置

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manager作为Cloud Service时，点按Experience Manager作为Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，点按工具图标，然后点按&#x200B;**[!UICONTROL Cloud Services> Dynamic Media配置]**。
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，点按&#x200B;**[!UICONTROL global]**（请勿点按或选择&#x200B;**[!UICONTROL global]**&#x200B;左侧的文件夹图标）。 然后点按&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;页面中，输入标题、Dynamic Media帐户电子邮件地址和密码，然后选择您的区域。 此信息是通过供应电子邮件中的Adobe提供给您的。 如果您未收到此电子邮件，请与Adobe客户服务联系。
1. 单击&#x200B;**[!UICONTROL 连接到Dynamic Media]**。
1. 在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框的&#x200B;**[!UICONTROL 新密码]**&#x200B;字段中，输入包含8-25个字符的新密码。 密码必须至少包含以下各项之一：

   * 大写字母
   * 小写字母
   * 数字
   * 特殊字符：`# $ & . - _ : { }`

   **[!UICONTROL 当前密码]**&#x200B;字段有意预填充并隐藏在交互中。

   如有必要，您可以通过点击密码眼睛图标来显示密码来检查您键入或重新键入的密码的拼写。 再次点按图标以隐藏密码。

1. 在&#x200B;**[!UICONTROL 重复密码]**&#x200B;字段中，重新键入新密码，然后点按&#x200B;**[!UICONTROL 完成。]**

   点按&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;页面右上角的&#x200B;**[!UICONTROL 保存]**&#x200B;时，将保存新密码。

   如果在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框中点击了&#x200B;**[!UICONTROL 取消]**，则在保存新创建的Dynamic Media配置时仍必须输入新密码。

   另请参阅[将密码更改为Dynamic Media](#change-dm-password)。

1. 连接成功后，可以设置以下内容：

   | 属性 | 描述 |
   |---|---|
   | 公司 | Dynamic Media帐户的名称。 您可能为不同子品牌、部门或暂存/生产环境拥有多个Dynamic Media帐户。 |
   | 公司根文件夹路径 | 您的公司的根文件夹路径。 |
   | 发布资产 | 您可以从以下三个选项中进行选择：<br>**[!UICONTROL Immediale ]**:上传资产后，系统会立即收录资产并提供URL/嵌入。 发布资产不需要用户干预。<br>**[!UICONTROL 激活时]**:在提供URL/嵌入链接之前，必须先显式发布资产。<br>**[!UICONTROL 选择性发布&#x200B;]**:资产会自动发布，仅用于安全预览。它们也可以显式发布到Experience Manager作为Cloud Service，而不发布到DMS7以在公共域中投放。 将来，此选项打算将资产作为Cloud Service发布到Experience Manager，并将资产发布到Dynamic Media，它们互不相容。 即，您可以将资产发布到DMS7，以便使用智能裁剪或动态演绎版等功能。 或者，您也可以将仅以Experience Manager形式发布资源作为预览的Cloud Service;DMS7中不发布这些相同的资源，以便在公共域中投放。 |
   | 安全预览服务器 | 允许您指定指向安全再现预览服务器的URL路径。 也就是说，在生成再现后，Experience Manager作为Cloud Service可以安全地访问和预览远程Dynamic Media再现(不会将二进制文件作为Cloud Service实例发送回Experience Manager)。<br>除非您有特殊安排来使用您自己的公司服务器或特殊服务器，否则Adobe建议您按指定的方式保留此设置。 |
   | 同步所有内容 | 默认选中。 如果您希望在同步到Dynamic Media时有选择地包括或排除资源，请取消选择此选项。 取消选择此选项后，您可以从以下两种Dynamic Media同步模式中进行选择：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 默认情况下启用&#x200B;]**:默认情况下，此配置将应用于所有文件夹，除非您专门为排除标记文件夹。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 默认禁用]**:只有显式标记选定的文件夹以同步到Dynamic Media后，配置才会应用于任何文件夹。<br>要将选定的文件夹标记为同步到Dynamic Media，请选择一个资产文件夹，然后在工具栏中点按 **[!UICONTROL 属性]**。在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉列表中，从以下三个选项中进行选择。 完成后，点按&#x200B;**[!UICONTROL 保存]**。 *记住：如果您选择了“同步所有内容”，则这三个&#x200B;**选项将**不可用。* 另请参 [阅在Dynamic Media的文件夹级别使用选择性发布。](/help/assets/dynamic-media/selective-publishing.md)<br>**[!UICONTROL 继承&#x200B;]**:文件夹上没有显式同步值。相反，该文件夹会从其某个祖先文件夹或云配置中的默认模式继承同步值。 通过工具提示显示继承的节目的详细状态。<br>**[!UICONTROL 为子文件夹启用]**:包含此子树中的所有内容以同步到Dynamic Media。特定于文件夹的设置将覆盖云配置中的默认模式。<br>**[!UICONTROL 对子文件夹禁用&#x200B;]**:将此子树中的所有内容排除在同步到Dynamic Media之外。 |

   >[!NOTE]
   >
   >Dynamic Media 不支持版本控制。此外，仅当“编辑Dynamic Media配置”页面中的&#x200B;**[!UICONTROL 发布资产]**&#x200B;设置为&#x200B;**[!UICONTROL 在激活]**&#x200B;时，延迟激活才适用。然后，直到第一次激活资产。
   >
   >
   >激活资产后，所有更新都会立即实时发布到S7投放。

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 点按&#x200B;**[!UICONTROL 保存]**。将保存新Dynamic Media密码和配置。 如果您点击了&#x200B;**[!UICONTROL 取消]**，则不会更新密码。
1. 在&#x200B;**[!UICONTROL 配置Dynamic Media]**&#x200B;对话框中，点按&#x200B;**[!UICONTROL 确定]**&#x200B;开始配置。

   >[!IMPORTANT]
   >
   >当新Dynamic Media配置完成其设置后，您将作为Cloud Service的收件箱在Experience Manager中收到状态通知。
   >
   >此收件箱通知会通知您配置是否成功。
   > 有关详细信息，请参阅[对新Dynamic Media配置](#troubleshoot-dm-config)和[您的收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)进行疑难解答。

1. 要在发布Dynamic Media内容之前安全地进行预览，默认情况下，Experience Manager作为Cloud Service使用基于令牌的身份验证。 但是，您也可以“”允许列表更多IP，以便让用户能够访问安全的预览内容。 要设置此操作，请执行以下操作：<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

   * 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。 您的凭据和登录详细信息由Adobe在设置时提供。 如果您没有此信息，请与Adobe客户关怀部门联系。
   * 在页面右上角附近的导航栏上，点按&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 发布设置]** > **[!UICONTROL 图像服务器]**。
   * 在“图像服务器发布”页面的&#x200B;**[!UICONTROL 发布上下文]**&#x200B;下拉列表中，选择&#x200B;**[!UICONTROL 测试图像服务]**。
   * 对于“客户端地址筛选器”，点按&#x200B;**[!UICONTROL 添加]**。
   * 要启用（打开）该地址，请选中该复选框，然后输入Experience Manager作者实例的IP地址（而非调度程序IP）。
   * 单击&#x200B;**[!UICONTROL 保存]**。

现在您已完成基本配置；您已准备好使用Dynamic Media。

如果要进一步自定义配置，您可以选择在Dynamic Media](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)中的“配置高级设置”下完成任何任务。[

### 对新Dynamic Media配置{#troubleshoot-dm-config}进行疑难解答

当新Dynamic Media配置完成其设置后，您将作为Cloud Service的收件箱在Experience Manager中收到状态通知。 此通知会通知您配置是否成功，如收件箱中的以下各个图像所示。

![Experience Manager收件箱成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件箱失败](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另请参阅[您的收件箱](/help/sites-cloud/authoring/getting-started/inbox.md)。

**对新Dynamic Media配置进行疑难解答**

1. 在Experience Manager右上角附近，点按Cloud Service页，然后点按&#x200B;**[!UICONTROL 视图全部]**。
1. 在“收件箱”页面上，点按成功通知以阅读配置状态和日志的概述。

   如果配置失败，请点按与以下屏幕截图类似的失败通知。

   ![Dynamic Media安装失败](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在&#x200B;**[!UICONTROL DMSETUP]**&#x200B;页上，查看描述故障的配置详细信息。 尤其要注意任何错误消息或错误代码。 请通过此信息与Adobe客户关怀部门联系。

   ![Dynamic Media设置页面](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 将密码更改为Dynamic Media {#change-dm-password}

Dynamic Media中的密码过期时间设置为从当前系统日期起100年。

密码必须至少包含以下各项之一：

* 大写字母
* 小写字母
* 数字
* 特殊字符：`# $ & . - _ : { }`

如有必要，您可以通过点击密码眼睛图标来显示密码来检查您键入或重新键入的密码的拼写。 再次点按图标以隐藏密码。

点按&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面右上角的&#x200B;**[!UICONTROL 保存]**&#x200B;时，将保存更改的密码。

1. 在Experience Manager作为Cloud Service时，点按Experience Manager作为Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，点按工具图标，然后点按&#x200B;**[!UICONTROL Cloud Services> Dynamic Media配置。]**
1. 在“Dynamic Media配置浏览器”页面的左窗格中，点按&#x200B;**[!UICONTROL global]**。请勿点按或选择&#x200B;**[!UICONTROL global]**&#x200B;左侧的文件夹图标。 然后，点按&#x200B;**[!UICONTROL 编辑。]**
1. 在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面中，点按&#x200B;**[!UICONTROL 密码]**&#x200B;字段的正下方，**[!UICONTROL 更改密码。]**
1. 在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框中，执行以下操作：

   * 在&#x200B;**[!UICONTROL 新密码]**&#x200B;字段中，输入新密码。

      **[!UICONTROL 当前密码]**&#x200B;字段有意预填充并隐藏在交互中。

   * 在&#x200B;**[!UICONTROL 重复密码]**&#x200B;字段中，重新键入新密码，然后点按&#x200B;**[!UICONTROL 完成。]**

1. 在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面的右上角，点按&#x200B;**[!UICONTROL 保存]**，然后点按&#x200B;**[!UICONTROL 确定。]**

## （可选）在Dynamic Media{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}中配置高级设置

要进一步自定义Dynamic Media的配置和设置或优化其性能，您可以完成以下一个或多个&#x200B;*可选*&#x200B;任务:

* [设置和配置Dynamic Media设置](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（可选）调整Dynamic Media的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

### （可选）Dynamic Media设置的设置和配置{#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic用户界面更改您的Dynamic Media设置。

上述某些任务要求您打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

设置和配置任务包括：

* [为图像服务器发布设置](#publishing-setup-for-image-server)
* [配置应用程序常规设置](#configuring-application-general-settings)
* [配置色彩管理](#configuring-color-management)
* [编辑支持的格式的MIME类型](#editing-mime-types-for-supported-formats)
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)

<!-- * [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 发布图像服务器{#publishing-setup-for-image-server}的设置

默认情况下，“发布设置”设置会确定如何从Dynamic Media传送资产。 如果未指定任何设置，则Dynamic Media会根据发布设置中定义的默认设置传送资产。 例如，传送不包含分辨率属性的图像的请求将生成具有“默认对象分辨率”设置的图像。

配置发布设置：在Dynamic Media Classic中，单击&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。

“图像服务器”屏幕会为传送图像建立默认设置。 有关每个设置的说明，请参阅UI屏幕。

**[!UICONTROL 请求属性]**  — 这些设置对可以从服务器传送的图像施加限制。**[!UICONTROL 默认请求属性]**  — 这些设置与图像的默认外观有关。**[!UICONTROL 常用缩览图属性]**  — 这些设置与缩览图图像的默认外观有关。**[!UICONTROL 目录字段的默认值]** — 这些设置与图像的分辨率和默认缩略图类型有关。**[!UICONTROL 色彩管理属性]**  — 这些设置决定使用哪些ICC色彩用户档案。**[!UICONTROL 兼容性属性]**  — 通过此设置，文本图层中的前导和尾部段落可以像在版本3.6中一样处理，以实现向后兼容。**[!UICONTROL 本地化支持]**  — 这些设置允许您管理多个区域设置属性。它还允许您指定区域设置映射字符串，以便定义要在查看器中支持各种工具提示的语言。 有关设置&#x200B;**[!UICONTROL 本地化支持]**&#x200B;的详细信息，请参阅[设置资产本地化时的注意事项](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets)。

#### 配置应用程序常规设置{#configuring-application-general-settings}

要打开“应用程序常规设置”页，请在Dynamic Media Classic全局导航栏中，单击&#x200B;**[!UICONTROL 设置>应用程序设置>常规设置。]**

**[!UICONTROL 服务器]**  — 在帐户设置时，Dynamic Media会自动为您的公司提供分配的服务器。这些服务器用于为您的网站和应用程序构建URL字符串。 这些URL调用特定于您的帐户。 除非作为Cloud Service支持的Experience Manager明确指示，否则不要更改任何服务器名称。
**[!UICONTROL 覆盖图像]** - Dynamic Media不允许两个文件具有相同的名称。每个项目的URL ID（文件名减去扩展名）必须唯一。 这些选项指定如何上传替换资产：是替换原始图像，还是变成重复。 重复资产使用“–1”重命名（例如，chair.tif更名为chair-1.tif）。 这些选项会影响上传到与原始文件夹不同的其他文件夹的资产，或具有与原始文件夹不同文件扩展名的资产。
**[!UICONTROL 在当前文件夹中覆盖，基本图像名称/扩展名相同]**  — 此选项是最严格的替换规则。它要求您将替换图像上传到与原始图像相同的文件夹，并且其文件扩展名与原始图像相同。 如果这些要求未得到满足，则会创建重复。 要保持与Experience Manager作为Cloud Service的一致性，请始终选择&#x200B;**[!UICONTROL 在当前文件夹中覆盖，即相同的基本图像名称/扩展名]**。
**[!UICONTROL 在任意文件夹中覆盖，基本资产名称/扩展名相同]**  — 要求替换图像的文件扩展名与原始图像的文件扩展名相同。例如，chair.jpg必须替换chair.jpg，而不是chair.tif。 但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新后的图像驻留在新文件夹中；在文件的原始位置找不到该文件。
**[!UICONTROL 在任意文件夹中覆盖相同的基本资产名称，而不管其扩展名]**  — 此选项是最包容的替换规则。您可以将替换图像上传到与原始图像不同的文件夹，以其他文件扩展名上传文件，并替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将驻留在其上传到的新文件夹中。
**[!UICONTROL 默认颜色用户档案]**  — 有关其 [他信](#configuring-color-management) 息，请参阅配置颜色管理。默认情况下，当您选择&#x200B;**[!UICONTROL 呈现]**&#x200B;时，系统会显示 15 种呈现形式，当您在资产的详细信息视图中选择&#x200B;**[!UICONTROL 查看器]**&#x200B;时，系统会显示 15 个查看器预设。您可以提高此限制。请参阅[增加或减少显示的图像预设数](/help/assets/dynamic-media/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)或[增加或减少显示的查看器预设数](/help/assets/dynamic-media/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display)。

#### 配置色彩管理{#configuring-color-management}

Dynamic Media色彩管理可让您对资源进行色彩校正。 借助颜色校正，摄取的资源可保留其色彩空间（RGB、CMYK、灰色）和嵌入的颜色用户档案。 当您请求动态再现时，图像颜色会使用CMYK、RGB或灰色输出校正到目标色彩空间。 请参阅[配置图像预设](/help/assets/dynamic-media/managing-image-presets.md)。

要配置默认颜色属性，以便在请求图像时启用颜色校正：

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后使用在设置过程中提供的凭据登录到您的帐户。
1. 导航到&#x200B;**[!UICONTROL 设置>应用程序设置]**。
1. 展开&#x200B;**[!UICONTROL 发布设置]**&#x200B;区域，然后选择&#x200B;**[!UICONTROL 图像服务器]**。设置发布实例的默认设置时，将&#x200B;**[!UICONTROL 发布上下文]**&#x200B;设置为&#x200B;**[!UICONTROL 图像提供]**。
1. 滚动到必须更改的属性，例如&#x200B;**[!UICONTROL 色彩管理属性]**区域中的属性。
可以设置以下颜色校正属性：

   | 属性 | 描述 |
   |---|---|
   | CMYK默认色彩空间 | 默认CMYK颜色用户档案的名称。 |
   | 灰度默认色彩空间 | 默认灰色用户档案的名称。 |
   | RGB默认色彩空间 | 默认RGB颜色用户档案的名称。 |
   | 颜色转换渲染方法 | 指定渲染方法。 可接受的值为：**[!UICONTROL 可感知]**、**[!UICONTROL 相对测温]**、**[!UICONTROL 饱和度]**、**[!UICONTROL 绝对测温。]** Adobe建 **** 议使用相对作为默认值。 |

1. 点按&#x200B;**[!UICONTROL 保存]**。

例如，可以将 **[!UICONTROL RGB 默认色彩空间]**&#x200B;设置为 *sRGB*，将 **[!UICONTROL CMYK 默认色彩空间]**&#x200B;设置为 *WebCoated*。

这样做将执行以下操作：

* 启用RGB和CMYK图像的颜色校正。
* 假定没有颜色用户档案的RGB图像位于&#x200B;*sRGB*&#x200B;色彩空间中。
* 假定没有颜色用户档案的CMYK图像位于&#x200B;*WebCoated*&#x200B;色彩空间中。
* 返回RGB输出的动态演绎版，在&#x200B;*sRGB*&#x200B;色彩空间中返回它。
* 返回CMYK输出的动态演绎版，在&#x200B;*WebCoated*&#x200B;色彩空间中返回它。

#### 编辑支持的格式{#editing-mime-types-for-supported-formats}的MIME类型

您可以定义Dynamic Media要处理的资产类型，并自定义高级资产处理参数。 例如，您可以指定资产处理参数以执行以下操作：

* 将Adobe PDF转换为eCatalog资源。
* 将Adobe Photoshop文档(.PSD)转换为横幅模板资产以进行个性化。
* 栅格化Adobe Illustrator文件(.AI)或Adobe Photoshop封装PostScript®文件(.EPS)。
* [视频](/help/assets/dynamic-media/video-profiles.md) 概要 [和](/help/assets/dynamic-media/image-profiles.md) 图像概要文件可用于定义视频和图像的处理。

请参阅[上传资产](/help/assets/add-assets.md)。

**要编辑支持的格式的MIME类型，请执行以下操作**

1. 在Experience Manager作为Cloud Service时，单击Experience Manager作为Cloud Service徽标以访问全局导航控制台，然后单击&#x200B;**[!UICONTROL 常规>CRXDE Lite]**。
1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择MIME类型。
1. 在CRXDE Lite页面的右侧，在下半部分：

   * 多次 — 单击&#x200B;**[!UICONTROL enabled]**&#x200B;字段。 默认情况下，所有资产MIME类型均处于启用状态（设置为&#x200B;**[!UICONTROL true]**），这意味着资产将同步到Dynamic Media进行处理。 如果要排除此资产MIME类型，请将此设置更改为&#x200B;**[!UICONTROL false]**。

   * 多次 — 单击&#x200B;**[!UICONTROL jobParam]**&#x200B;打开其关联的文本字段。 有关可用于给定MIME类型的允许处理参数值的列表，请参阅[支持的MIME类型](/help/assets/file-format-support.md)。

1. 执行下列操作之一：
   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页面的菜单栏上，单击&#x200B;**[!UICONTROL 保存全部。]**

1. 在页面的左上角，点按&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回Experience Manager作为Cloud Service。

#### 为不支持的格式{#adding-mime-types-for-unsupported-formats}添加MIME类型

您可以为Experience Manager资产中不支持的格式添加自定义MIME类型。 要确保在CRXDE Lite中添加的任何新节点不会被Experience Manager删除，请将MIME类型移到`image_`之前。 另外，确保将其启用值设置为&#x200B;**[!UICONTROL false]**。

**为不支持的格式添加MIME类型**

1. 从Experience Manager作为Cloud Service，点按&#x200B;**[!UICONTROL 工具>操作> Web控制台。]**

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 新的浏览器选项卡会打开到&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称 *Adobe CQ Scene7 Asset MIME 类型服务*，如下面的屏幕截图所示。在名称的右侧，点按&#x200B;**[!UICONTROL 编辑配置值]**（铅笔图标）。

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7资产MIME类型服务**&#x200B;页面上，单击任意加号图标&lt;+>。 在表中单击加号以添加新MIME类型的位置很小。

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. 在刚刚添加的空文本字段中键入`DWG=image/vnd.dwg`。

   示例`DWG=image/vnd.dwg`仅供说明之用。 您在此处添加的MIME类型可以是任何其他不支持的格式。

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，点按&#x200B;**[!UICONTROL 保存]**。

   此时，您可以关闭具有打开的Adobe Experience Manager Web Console“配置”页的浏览器选项卡。

1. 返回到将打开的Experience Manager作为Cloud Service控制台的浏览器选项卡。
1. 从Experience Manager作为Cloud Service，点按&#x200B;**[!UICONTROL 工具>常规>CRXDE Lite]**。

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 拖动MIME类型`image_vnd.dwg`并将其直接放在树中`image_`的上方，如下面的屏幕截图所示。

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. 在MIME类型`image_vnd.dwg`仍处于选定状态的&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡中，在&#x200B;**[!UICONTROL enabled]**&#x200B;行的&#x200B;**[!UICONTROL 值]**&#x200B;列标题下，多次单击值。 将打开&#x200B;**[!UICONTROL Value]**&#x200B;下拉列表。
1. 在字段中键入`false`(或从下拉列表中选择&#x200B;**[!UICONTROL false]**)。

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite页的左上角附近，单击&#x200B;**[!UICONTROL 全部保存]**。



### （可选）调整Dynamic Media {#optional-tuning-the-performance-of-dynamic-media-scene-mode}的性能

为了保持Dynamic Media <!--(with `dynamicmedia_scene7` run mode)-->的顺畅运行，Adobe建议使用以下同步性能/可伸缩性微调提示：

* 更新预定义的作业参数以处理不同的文件格式。
* 更新预定义的Granite工作流（视频资产）队列工作线程。
* 更新预定义的Granite临时工作流（图像和非视频资产）队列工作线程。
* 更新到Dynamic Media Classic服务器的最大上载连接数。

#### 更新预定义的作业参数以处理不同的文件格式

您可以调整作业参数，以便在上传文件时加快处理速度。 例如，如果您上传PSD文件，但不想将它们作为模板进行处理，则可以将图层提取设置为false（关闭）。 在这种情况下，调整的作业参数如下所示：`process=None&createTemplate=false`。

如果确实要打开模板创建，请使用以下参数：`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议对PDF、PostScript®和PSD文件使用以下“调整”作业参数：

| 文件类型 | 建议的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新任何这些参数，请参阅[编辑支持的格式的MIME类型](#editing-mime-types-for-supported-formats)。

另请参阅[添加不支持的格式](#adding-mime-types-for-unsupported-formats)的MIME类型。

#### 更新Granite临时工作流队列{#updating-the-granite-transient-workflow-queue}

Granite Transit工作流队列用于&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。 在Dynamic Media中，它用于图像摄取和处理。

**更新Granite临时工作流队列**

1. 导航到[https://&lt;server>/system/console/configMgr](https://localhost:4502/system/console/configMgr)并搜索&#x200B;**队列：Granite临时工作流队列**。

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将数字更改为所需值。

   您可以增加&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;以充分支持将文件重新上载到Dynamic Media。 具体值取决于硬件容量。 在某些情况下（如初始迁移或一次性批量上传），您可以使用大值。 但是，请注意，使用大值（如核心数的2倍）可能会对其他并发活动产生负面影响。 因此，请根据您的特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存]**。

#### 更新Granite Workflow队列{#updating-the-granite-workflow-queue}

Granite工作流队列用于非临时工作流。 在Dynamic Media中，它用于使用&#x200B;**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流处理视频。

要更新Granite工作流队列，请执行以下操作：

1. 导航到`https://<server>/system/console/configMgr`并搜索&#x200B;**队列：Granite工作流队列**。

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要进行文本搜索，而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将数字更改为所需值。

   默认情况下，最大并行作业数取决于可用CPU核心数。 例如，在4核服务器上，它分配两个工作线程。 （介于0.0和1.0之间的值基于比率，或者大于1的任何数字都分配工作线程的数量。）

   对于大多数用例，0.5默认设置已足够。

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存]**。

#### 更新Scene7上载连接{#updating-the-scene-upload-connection}

Scene7上传连接设置将Experience Manager资源同步到Dynamic Media Classic服务器。

要更新Scene7上载连接，请执行以下操作：

1. 导航至 `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 连接数]**&#x200B;字段或&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段中，或同时在这两个字段中，根据需要更改数字。

   **[!UICONTROL 连接数]**&#x200B;设置控制允许Experience ManagerDynamic Media上载的HTTP连接的最大数。 通常，十个连接的预定义值就足够了。

   **[!UICONTROL 活动作业超时]**&#x200B;设置决定了在投放服务器中发布已上传Dynamic Media资产的等待时间。 默认情况下，此值为2100秒或35分钟。

   对于大多数用例，设置2100就足够了。

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. 点按&#x200B;**[!UICONTROL 保存。]**

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

1. In Experience Manager as a Cloud Service, tap the Experience Manager as a Cloud Service logo to access the global navigation console and tap the **[!UICONTROL Tools > General > CRXDE Lite]**.
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

