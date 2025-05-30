---
title: 配置Dynamic Media Cloud Service
description: 了解如何在Adobe Experience Manager as a Cloud Service中配置Dynamic Media。
contentOwner: Rick Brough
feature: Configuration,Dynamic Media
role: Admin,User
exl-id: 8e07bc85-ef26-4df4-8e64-3c69eae91e11
source-git-commit: 2ca425f9a142432a5d3bcce8ce522c97e4c2cf2d
workflow-type: tm+mt
source-wordcount: '3721'
ht-degree: 2%

---

# 关于配置Dynamic Media Cloud Service {#configuring-dynamic-media}

{{work-with-dynamic-media}}

如果您将Adobe Experience Manager as a Cloud Service用于不同的环境，例如开发、暂存和实时生产，请为每个环境配置Dynamic Media云服务。

另请参阅[配置Dynamic Media公司别名帐户](/help/assets/dynamic-media/dm-alias-account.md)

>[!IMPORTANT]
>
>增强的安全环境中不支持&#x200B;**Dynamic Media (Scene7)**
>
>AEM as a Cloud Service上的Dynamic Media (Scene7)不符合HIPAA要求，并且无法在启用了增强安全性的AEM环境中使用。
>
>从2025年4月版AEM as a Cloud Service开始，技术限制会阻止在具有增强安全性的环境中配置Dynamic Media (Scene7)。 因此，**工具** > **云服务**&#x200B;下的&#x200B;**Dynamic Media配置**&#x200B;卡在这些环境中不再可见。
>
>此外，使用AEM 6.5的客户应该知道Dynamic Media (Scene7)栈栈未就绪，无法用于HIPAA。

## Dynamic Media的架构图 {#architecture-diagram-of-dynamic-media}

以下架构图描述了Dynamic Media的工作方式。

借助新架构，Experience Manager负责主源资源并与Dynamic Media同步，以进行资源处理和发布：

1. 将主源资产上传到Adobe Experience Manager as a Cloud Service后，会将其复制到Dynamic Media。 届时，Dynamic Media将处理所有资源处理和演绎版生成，例如视频编码和图像的动态变量。
1. 生成演绎版后，Experience Manager as a Cloud Service可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager as a Cloud Service实例)。
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

## 在Cloud Services中创建Dynamic Media配置 {#configuring-dynamic-media-cloud-services}

<!-- **Before you creating a Dynamic Media Configuration in Cloud Services**: After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hans#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials. -->

1. 在Experience Manager as a Cloud Service中，选择Experience Manager as a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择“工具”图标，然后转到&#x200B;**[!UICONTROL 云服务> Dynamic Media配置]**。
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择&#x200B;**[!UICONTROL 全局]** （不要选择&#x200B;**[!UICONTROL 全局]**&#x200B;左侧的文件夹图标）。 然后选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;页面上，输入Dynamic Media帐户的公司管理员的标题、Dynamic Media帐户电子邮件地址和密码，然后选择您所在的区域。 此信息由Adobe在配置电子邮件中提供给您。 如果您没有收到此电子邮件，请联系Adobe客户支持。
1. 选择&#x200B;**[!UICONTROL 连接到Dynamic Media]**。
1. 在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框的&#x200B;**[!UICONTROL 新密码]**&#x200B;字段中，输入包含8-25个字符的新密码。 密码必须至少包含以下项之一：

   * 大写字母
   * 小写字母
   * 数字
   * 特殊字符： `# $ & . - _ : { }`

   **[!UICONTROL 当前密码]**&#x200B;字段刻意预填充并隐藏在交互中。

   如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

1. 在&#x200B;**[!UICONTROL 重复密码]**&#x200B;字段中，重新键入新密码，然后选择&#x200B;**[!UICONTROL 完成]**。

   当您在&#x200B;**[!UICONTROL 创建Dynamic Media配置]**&#x200B;页面的右上角选择&#x200B;**[!UICONTROL 保存]**&#x200B;时，将保存新密码。

   如果您在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框中选择了&#x200B;**[!UICONTROL 取消]**，则在保存已创建的Dynamic Media配置时，仍必须输入新密码。

   另请参阅[将密码更改为Dynamic Media](#change-dm-password)。

1. 当连接成功时，可以设置以下内容：

   | 属性 | 描述 |
   |---|---|
   | 公司 | Dynamic Media帐户的名称。<br>**重要信息**：在Experience Manager的实例上仅支持Cloud Services中的一个Dynamic Media配置；请勿添加多个配置。 Adobe *不支持*，或建议在单个Experience Manager实例上配置多个Dynamic Media配置。<!-- CQDOC-19579 and CQDOC-19612 --><br>另请参阅[配置Dynamic Media公司别名帐户](/help/assets/dynamic-media/dm-alias-account.md)。 |
   | 公司根文件夹路径 | 您公司的根文件夹路径。 |
   | 发布Assets | 您可以从以下三个选项中进行选择：<br>**[!UICONTROL 立即&#x200B;]**— 上传资产时，系统会摄取资产并立即提供URL/嵌入。 发布资产无需用户干预。<br>**[!UICONTROL 激活]** — 必须先明确发布资产，然后才能提供URL/嵌入链接。<br>**[!UICONTROL 选择性发布&#x200B;]**— 仅出于安全预览目的自动发布Assets。 它们也可以明确发布到Experience Manager as a Cloud Service，而无需发布到DMS7以供在公共域中交付。 将来，此选项旨在将资产发布到Experience Manager as a Cloud Service，并将资产发布到Dynamic Media，二者相互排斥。 也就是说，您可以将资源发布到DMS7，以便使用智能裁剪或动态呈现版本等功能。 或者，您也可以在Experience Manager as a Cloud Service中专门发布资源以供预览。 这些相同的资产不会发布在DMS7中以在公共域中交付。 |
   | 安全预览服务器 | 它可让您指定安全呈现版本预览服务器的URL路径。 也就是说，在生成演绎版之后，AEM as a Cloud Service可以安全地访问和预览远程Dynamic Media演绎版(不会将二进制文件发送回Experience Manager as a Cloud Service实例)。<br>除非您有特殊安排使用您自己公司的服务器或特殊服务器，否则Adobe建议您保留指定的此设置。 |
   | 同步所有内容 | 默认选中。 如果要在同步到Dynamic Media的过程中选择性地包含或排除资产，请取消选择此选项。 取消选择此选项可以从以下两种Dynamic Media同步模式中进行选择：<br>**[!UICONTROL Dynamic Media同步模式]**<br>**[!UICONTROL 默认情况下启用&#x200B;]**— 默认情况下将配置应用于所有文件夹，除非您特别将文件夹标记为排除。 <!-- you can then deselect the folders that you do not want the configuration applied to.--><br>**[!UICONTROL 默认情况下已禁用]** — 在您明确将选定文件夹标记为同步到Dynamic Media之前，该配置不会应用于任何文件夹。<br>要将选定的文件夹标记为同步到Dynamic Media，请选择一个资源文件夹，然后在工具栏中选择&#x200B;**[!UICONTROL 属性]**。 在&#x200B;**[!UICONTROL 详细信息]**&#x200B;选项卡的&#x200B;**[!UICONTROL Dynamic Media同步模式]**&#x200B;下拉列表中选择以下三个选项。 完成后，选择&#x200B;**[!UICONTROL 保存]**。 _请记住：如果您选择了更早的&#x200B;**同步所有内容**，则这三个选项将不可用。_&#x200B;另请参阅[在Dynamic Media中使用文件夹级别的选择性发布](/help/assets/dynamic-media/selective-publishing.md)。<br>**[!UICONTROL 已继承&#x200B;]**— 文件夹中没有显式同步值。 相反，文件夹会从其上级文件夹之一继承同步值，或者在云配置中继承默认模式。 继承的详细状态通过工具提示显示。<br>**[!UICONTROL 为子文件夹启用]** — 包含此子树中的所有内容，以便同步到Dynamic Media。 文件夹特定的设置会覆盖云配置中的默认模式。<br>**[!UICONTROL 已对子文件夹禁用&#x200B;]**— 排除此子树中的所有内容，禁止同步到Dynamic Media。 |

   >[!NOTE]
   >
   >Dynamic Media 不支持版本控制。此外，仅当“编辑Dynamic Media配置”页面中的&#x200B;**[!UICONTROL 发布Assets]**&#x200B;设置为&#x200B;**[!UICONTROL 激活时]**&#x200B;时，延迟激活才适用。 然后，直到首次激活资产为止。
   >
   >
   >激活资产后，所有更新都会立即实时发布到S7交付。

   ![dynamicmediaconfiguration2updated](/help/assets/assets-dm/dynamicmediaconfigurationupdated.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。新的Dynamic Media密码和配置已保存。 如果您选择了&#x200B;**[!UICONTROL 取消]**，则不会发生密码更新。
1. 在&#x200B;**[!UICONTROL 配置Dynamic Media]**&#x200B;对话框中，选择&#x200B;**[!UICONTROL 确定]**&#x200B;开始配置。

   >[!IMPORTANT]
   >
   >当设置完新的Dynamic Media配置时，您将在Experience Manager as a Cloud Service收件箱中收到相应状态通知。
   >
   >此收件箱通知会告知您配置是否成功。
   > 有关详细信息，请参阅[新Dynamic Media配置疑难解答](#troubleshoot-dm-config)和[您的收件箱](/help/sites-cloud/authoring/inbox.md)。

1. 为了在发布Dynamic Media内容之前安全地预览该内容，Experience Manager as a Cloud Service使用基于令牌的验证，因此默认情况下，Experience Manager Author会预览Dynamic Media内容。 但是，您可以&#x200B;*再允许列表*&#x200B;个IP以向用户提供安全预览内容的访问权限。 要在Experience Manager as a Cloud Service中设置此操作，请参阅[为图像服务器配置Dynamic Media发布设置 — 安全选项卡](/help/assets/dynamic-media/dm-publish-settings.md#security-tab)。<!-- To securely preview Dynamic Media content before it gets published, you must "allowlist" the Experience Manager as a Cloud Service author instance to connect to Dynamic Media. To set up this action, do the following: -->

<!--
    * Open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hans#getting-started), then sign in to your account. Your credentials and sign-in details were provided by Adobe at the time of provisioning. If you do not have this information, contact Adobe Customer Support.
    * On the navigation bar near the upper right corner of the page, go to **[!UICONTROL Setup]** > **[!UICONTROL Application Setup]** > **[!UICONTROL Publish Setup]** > **[!UICONTROL Image Server]**.
    * On the Image Server Publish page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * For the Client Address Filter, select **[!UICONTROL Add]**.
    * To enable (turn on) the address, select the check box, then enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * Select **[!UICONTROL Save]**. -->

您现在已完成基本配置；可以使用Dynamic Media了。

如果您需要进一步自定义配置，例如启用ACL（访问控制列表）权限，您可以选择在Dynamic Media的[配置高级设置](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode)下完成任何任务。

### 新Dynamic Media配置疑难解答 {#troubleshoot-dm-config}

当设置完新的Dynamic Media配置时，您将在Experience Manager as a Cloud Service收件箱中收到相应状态通知。 此通知会告知您配置是否成功，如收件箱中相应图像的内容所示。

![Experience Manager收件箱成功](/help/assets/dynamic-media/assets/dmconfig-inbox-success.png)

![Experience Manager收件箱失败](/help/assets/dynamic-media/assets/dmconfig-inbox-failure.png)

另请参阅[您的收件箱](/help/sites-cloud/authoring/inbox.md)。

**要对新的Dynamic Media配置进行故障排除：**

1. 在Experience Manager as a Cloud Service页面的右上角附近，选择铃铛图标，然后选择&#x200B;**[!UICONTROL 查看全部]**。
1. 在收件箱页面上，选择成功通知以读取配置的状态和日志的概述。

   如果配置失败，请选择与以下屏幕快照类似的失败通知。

   ![Dynamic Media设置失败](/help/assets/dynamic-media/assets/dmconfig-fail-notification.png)

1. 在&#x200B;**[!UICONTROL DMSETUP]**&#x200B;页面上，查看描述该故障的配置详细信息。 特别是，请注意任何错误消息或错误代码。 请联系Adobe客户支持并提供此信息。

   ![Dynamic Media设置页面](/help/assets/dynamic-media/assets/dmconfig-fail-page.png)

### 将密码更改为Dynamic Media {#change-dm-password}

Dynamic Media中的密码过期时间设置为自当前系统日期起100年。

密码必须至少包含以下项之一：

* 大写字母
* 小写字母
* 数字
* 特殊字符： `# $ & . - _ : { }`

如有必要，可以通过选择密码眼睛图标显示密码来检查已键入或重新键入的密码的拼写。 再次选择图标可隐藏密码。

当您在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面的右上角选择&#x200B;**[!UICONTROL 保存]**&#x200B;时，将保存更改的密码。

1. 在Experience Manager as a Cloud Service中，选择Experience Manager as a Cloud Service徽标以访问全局导航控制台。
1. 在控制台左侧，选择“工具”图标，然后转到&#x200B;**[!UICONTROL 云服务> Dynamic Media配置]**。
1. 在“Dynamic Media配置浏览器”页面的左侧窗格中，选择&#x200B;**[!UICONTROL 全局]**。 请勿选择&#x200B;**[!UICONTROL global]**&#x200B;左侧的文件夹图标。 然后选择&#x200B;**[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面的&#x200B;**[!UICONTROL 密码]**&#x200B;字段正下方，选择&#x200B;**[!UICONTROL 更改密码]**。
1. 在&#x200B;**[!UICONTROL 更改密码]**&#x200B;对话框中，执行以下操作：

   * 在&#x200B;**[!UICONTROL 新密码]**&#x200B;字段中，输入新密码。

     **[!UICONTROL 当前密码]**&#x200B;字段刻意预填充并隐藏在交互中。

   * 在&#x200B;**[!UICONTROL 重复密码]**&#x200B;字段中，重新键入新密码，然后选择&#x200B;**[!UICONTROL 完成]**。

1. 在&#x200B;**[!UICONTROL 编辑Dynamic Media配置]**&#x200B;页面的右上角，选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 确定]**。

## （可选）在Dynamic Media中配置高级设置{#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

要进一步自定义Dynamic Media的配置和设置，或优化其性能，您可以完成以下&#x200B;_可选_&#x200B;任务中的一个或多个任务：

* [（可选）在Dynamic Media中启用ACL权限](#optional-enable-acl)
* [（可选）设置和配置Dynamic Media设置](#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings)
* [（可选）调整Dynamic Media的性能](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

<!--

* [(Optional) Filtering assets for replication](#optional-filtering-assets-for-replication)

-->

<!-- Removed as per CQDOC-20701 - May need to revisit and update. In Adobe Experience Manager (AEM) as a Cloud Service, enabling Access Control List (ACL) permissions for Dynamic Media requires a different approach compared to on-premise versions (which was described below), as direct editing of OSGi configurations via the UI is not supported. Not sure how this is done now. For example, you can manage ACLs using tools like the Netcentric Access Control Tool (AC Tool), which simplifies the specification and deployment of complex ACLs in AEM but I doubt that's the recommended method.

### (Optional) Enable Access Control List permissions in Dynamic Media {#optional-enable-acl}

When you run Dynamic Media on AEM as a Cloud Service, it currently forwards `/is/image` requests to Secure Preview Image Serving without checking ACL (Access Control List) permissions on the PlatformServerServlet. You can, however, _enable_ ACL permissions. Doing so forwards the authorized `/is/image` requests. If a user is not authorized to access the asset, a "403 - Forbidden" error is displayed.

**To enable Access Control List permissions in Dynamic Media on AEM as a Cloud Service:**

1. From Adobe Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. A new browser tab opens to the **[!UICONTROL Adobe Experience Manager Web Console Configuration]** page.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. On the page, scroll to the name _Adobe CQ Scene7 PlatformServer_.

1. To the right of the name, select the pencil icon (**[!UICONTROL Edit the configuration values]**).

1. On the **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name** page, select the check box for the following two settings:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` &ndash; When enabled, this setting caches permission results for two minutes (default) to save.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` &ndash; When enabled, this setting validates a user's access while they preview assets by way of Dynamic Media Image Server.

   ![Enable Access Control List settings in Dynamic Media - Scene7 mode](/help/assets/dynamic-media/assets/acl.png)

1. Near the lower-right corner of the page, select **[!UICONTROL Save]**.
-->

### （可选）设置和配置Dynamic Media设置 {#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings}

使用Dynamic Media Classic用户界面更改您的Dynamic Media设置。

<!-- Some of the tasks above require that you open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hans#getting-started), then sign in to your account. -->

安装和配置任务包括：

* [为图像服务器配置Dynamic Media发布设置](#publishing-setup-for-image-server)
* [配置Dynamic Media常规设置](#configuring-application-general-settings)
* [配置颜色管理](#configuring-color-management)
* [编辑所支持格式的MIME类型](#editing-mime-types-for-supported-formats)
* [为不支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)
<!-- OBSOLETE BUT LEAVE FOR POSSIBLE FUTURE* [Creating batch set presets to auto-generate Image Sets and Spin Sets](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) -->

#### 为图像服务器配置Dynamic Media发布设置 {#publishing-setup-for-image-server}

“Dynamic Media发布设置”页面建立了默认设置，用于确定如何将资源从Adobe Dynamic Media服务器传递到网站或应用程序。

请参阅[为图像服务器配置Dynamic Media发布设置](/help/assets/dynamic-media/dm-publish-settings.md)。

#### 配置Dynamic Media常规设置 {#configuring-application-general-settings}

配置Dynamic Media **[!UICONTROL 发布服务器名称]** URL和&#x200B;**[!UICONTROL 原始服务器名称]** URL。 您还可以指定&#x200B;**[!UICONTROL 上载到应用程序]**&#x200B;设置和&#x200B;**[!UICONTROL 默认上载选项]**，所有这些都基于您的特定用例。

请参阅[配置Dynamic Media常规设置](/help/assets/dynamic-media/dm-general-settings.md)。

#### 配置颜色管理 {#configuring-color-management}

通过Dynamic Media色彩管理，您可以对资源进行色彩校正。 通过颜色校正，摄取的资产可保留其颜色空间(RGB、CMYK、灰色)和嵌入的颜色配置文件。 请求动态演绎版时，会使用CMYK、RGB或灰度输出将图像颜色校正到目标颜色空间中。

请参阅[配置图像预设](/help/assets/dynamic-media/managing-image-presets.md)。

要配置默认颜色属性以便在请求图像时启用颜色校正，请执行以下操作：

1. 打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started)，然后使用在配置期间提供的凭据登录到您的帐户。
1. 转到&#x200B;**[!UICONTROL 设置>应用程序设置]**。
1. 展开&#x200B;**[!UICONTROL 发布设置]**&#x200B;区域，然后选择&#x200B;**[!UICONTROL 图像服务器]**。设置发布实例的默认设置时，将&#x200B;**[!UICONTROL 发布上下文]**&#x200B;设置为&#x200B;**[!UICONTROL 图像提供]**。
1. 滚动到必须更改的属性，例如&#x200B;**[!UICONTROL 颜色管理属性]**&#x200B;区域中的属性。
您可以设置以下颜色校正属性：

   | 属性 | 描述 |
   |---|---|
   | CMYK默认颜色空间 | 默认CMYK颜色配置文件的名称。 |
   | 灰度默认颜色空间 | 默认灰色颜色配置文件的名称。 |
   | RGB默认颜色空间 | 默认RGB颜色配置文件的名称。 |
   | 颜色转换调色 | 指定渲染方法。 可接受的值为： **[!UICONTROL 可感知]**、**[!UICONTROL 相对色度]**、**[!UICONTROL 饱和度]**、**[!UICONTROL 绝对色度]**。 Adobe建议使用&#x200B;**[!UICONTROL 相对]**&#x200B;作为默认值。 |

1. 选择&#x200B;**[!UICONTROL 保存]**。

例如，可以将 **[!UICONTROL RGB 默认色彩空间]**&#x200B;设置为 *sRGB*，将 **[!UICONTROL CMYK 默认色彩空间]**&#x200B;设置为 *WebCoated*。

这样做将执行以下操作：

* 为RGB和CMYK图像启用颜色校正。
* 假定没有颜色配置文件的RGB图像在&#x200B;*sRGB*&#x200B;色彩空间中。
* 假定没有颜色配置文件的CMYK图像在&#x200B;*WebCoated*&#x200B;色彩空间中。
* 返回RGB输出的动态演绎版，在&#x200B;*sRGB*&#x200B;色彩空间中返回它。
* 返回CMYK输出的动态演绎版，在&#x200B;*WebCoated*&#x200B;色彩空间中返回它。

#### 编辑所支持格式的MIME类型 {#editing-mime-types-for-supported-formats}

您可以指定Dynamic Media处理的资源类型，并自定义高级资源处理参数。 例如，您可以指定资产处理参数，以执行以下操作：

* 将Adobe PDF转换为eCatalog资源。
* 将Adobe Photoshop文档(.PSD)转换为横幅模板资源以进行个性化。
* 栅格化Adobe Illustrator文件(.AI)或Adobe Photoshop封装的PostScript®文件(.EPS)。
* [视频配置文件](/help/assets/dynamic-media/video-profiles.md)和[图像配置文件](/help/assets/dynamic-media/image-profiles.md)分别可用于定义视频和图像的处理。

查看[上传资源](/help/assets/add-assets.md)。

**要编辑所支持格式的MIME类型：**

1. 以产品管理员身份登录到您的Experience Manager as a Cloud Service 。
1. 在Experience Manager as a Cloud Service中，选择Experience Manager as a Cloud Service徽标以访问全局导航控制台，然后转到&#x200B;**[!UICONTROL 常规> CRXDE Lite]**。

   如果您无权访问CRXDE Lite，请参阅[使用CRXDE Lite](/help/implementing/developing/tools/crxde.md)。

1. 在左边栏中，导航到以下内容：

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![MIME类型](assets/mimetypes.png)

1. 在mimeTypes文件夹下，选择MIME类型。
1. 在CRXDE Lite页面的右侧，位于下部：

   * 双击&#x200B;**[!UICONTROL 已启用]**&#x200B;字段。 默认情况下，将启用所有资源MIME类型（设置为&#x200B;**[!UICONTROL true]**），这意味着资源将同步到Dynamic Media以供处理。 如果要从处理中排除此资源MIME类型，请将此设置更改为&#x200B;**[!UICONTROL false]**。

   * 双击&#x200B;**[!UICONTROL jobParam]**&#x200B;以打开其关联的文本字段。 有关可用于给定MIME类型的允许处理参数值的列表，请参阅[支持的MIME类型](/help/assets/file-format-support.md)。

1. 执行下列操作之一：
   * 重复步骤3-4以编辑更多MIME类型。
   * 在CRXDE Lite页面的菜单栏上，选择&#x200B;**[!UICONTROL 全部保存]**。

1. 在页面的左上角，选择&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;以返回到Experience Manager as a Cloud Service。

#### 为不支持的格式添加MIME类型 {#adding-mime-types-for-unsupported-formats}

您可以为Experience Manager Assets中不支持的格式添加自定义MIME类型。 要阻止Experience Manager删除您在CRXDE Lite中添加的任何新节点，请将MIME类型移动到`image_`之前。 另外，请确保将其启用值设置为&#x200B;**[!UICONTROL false]**。

**为不受支持的格式添加MIME类型：**

1. 以产品管理员身份登录到您的Experience Manager as a Cloud Service 。
1. 从Experience Manager as a Cloud Service转到&#x200B;**[!UICONTROL 工具>操作> Web控制台]**。

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. 此时将打开一个新的浏览器选项卡，以显示&#x200B;**[!UICONTROL Adobe Experience Manager Web控制台配置]**&#x200B;页面。

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. 在页面上，向下滚动到名称&#x200B;*Adobe CQ Scene7 asset MIME类型服务*，如下面的屏幕快照所示。 在名称的右侧，选择&#x200B;**[!UICONTROL 编辑配置值]** （铅笔图标）。

   ![编辑配置值](assets/2019-08-02_16-44-56.png)

1. 在&#x200B;**Adobe CQ Scene7 Asset MIME类型服务**&#x200B;页面上，选择任意加号图标&lt;+>。 在表格中选择加号以添加新MIME类型的位置微不足道。

   ![Adobe CQ Scene7资产Mime类型服务](assets/2019-08-02_16-27-27.png)

1. 在刚刚添加的空文本字段中键入`DWG=image/vnd.dwg`。

   `DWG=image/vnd.dwg` MIME类型仅用于示例目的。 您在此处添加的MIME类型可以是任何其他不受支持的格式。

   ![正在添加DWG MIME类型](assets/2019-08-02_16-36-36.png)

1. 在页面的右下角，选择&#x200B;**[!UICONTROL 保存]**。

   此时，您可以关闭已打开Adobe Experience Manager Web控制台配置页面的浏览器选项卡。

1. 返回到已打开了Experience Manager as a Cloud Service控制台的浏览器选项卡。
1. 从Experience Manager as a Cloud Service转到&#x200B;**[!UICONTROL 工具>常规> CRXDE Lite]**。

   如果您无权访问CRXDE Lite，请参阅[使用CRXDE Lite](/help/implementing/developing/tools/crxde.md)。

   ![工具>常规> CRXDE Lite](assets/2019-08-02_16-55-41.png)

1. 在左边栏中，导航到以下内容：

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. 将MIME类型`image_vnd.dwg`拖放到树中`image_`的正上方，如下面的屏幕快照所示。

   ![在CRXDE Lite中编辑DWG文件](assets/crxdelite_cqdoc-14627.png)

1. 在MIME类型`image_vnd.dwg`仍被选定的情况下，从&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡的&#x200B;**[!UICONTROL 值]**&#x200B;列标题下的&#x200B;**[!UICONTROL 已启用]**&#x200B;行中，双击该值。 **[!UICONTROL 值]**&#x200B;下拉列表已打开。
1. 在字段中键入`false`（或从下拉列表中选择&#x200B;**[!UICONTROL false]**）。

   ![在CRXDE Lite中编辑MIME类型](assets/2019-08-02_16-60-30.png)

1. 在CRXDE Lite页面的左上角附近，选择&#x200B;**[!UICONTROL 全部保存]**。

### （可选）调整Dynamic Media的性能 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

为了保持Dynamic Media顺利运行，Adobe建议执行以下同步性能/可扩展性微调提示：

* [更新预定义的作业参数以处理不同的文件格式](#update-job-para)。
* [更新预定义的Granite工作流队列（视频资产）工作线程](#update-granite-workflow-queue-worker-threads-video)
* [更新预定义的Granite临时工作流队列（图像和非视频资产）工作线程](#update-granite-transient-workflow-queue-worker-threads-images)。
* [更新到Dynamic Media Classic (Scene7)服务器的最大上传连接数](#update-max-s7-upload-connections)。

#### 更新预定义的作业参数以处理不同的文件格式 {#update-job-para}

您可以调整作业参数，以便在上载文件时更快地处理。 例如，如果上传PSD文件，但不希望将它们作为模板处理，则可以将图层提取设置为false（关闭）。 在这种情况下，调谐的作业参数如下所示： `process=None&createTemplate=false`。

如果确实要启用模板创建，请使用以下参数： `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`。

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

Adobe建议为PDF、PostScript®和PSD文件使用以下“优化”作业参数：

| 文件类型 | 建议的作业参数 |
| ---| ---|
| PDF | `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

要更新这些参数中的任意参数，请参阅[编辑所支持格式的MIME类型](#editing-mime-types-for-supported-formats)。

另请参阅[为不受支持的格式添加MIME类型](#adding-mime-types-for-unsupported-formats)。

#### 更新预定义的Granite工作流队列（视频资产）工作线程 {#update-granite-workflow-queue-worker-threads-video}

Granite工作流队列用于非临时工作流。 在Dynamic Media中，用于通过&#x200B;**[!UICONTROL Dynamic Media编码视频]**&#x200B;工作流处理视频。

>[!NOTE]
>
>您必须以产品管理员身份登录到Experience Manager as a Cloud Service才能完成此任务。

如果您无权访问OSGi，请参阅[OSGi配置](/help/implementing/developing/components/overview.md#osgi-configuration)。

**要更新预定义的Granite工作流队列（视频资产）工作线程：**

1. 导航到`https://<server>/system/console/configMgr`并搜索&#x200B;**队列： Granite工作流队列**。

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将该数字更改为所需的值。

   默认情况下，最大并行作业数取决于可用的CPU核心数量。 例如，在4核服务器上，它分配两个工作线程。 （介于0.0和1.0之间的值基于比率，或任何大于1的数字均分配工作线程数。）

   对于大多数用例，0.5的默认设置就足够了。

   ![作业处理队列的配置](assets/chlimage_1-1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新预定义的Granite临时工作流队列工作线程 {#update-granite-transient-workflow-queue-worker-threads-images}

Granite传输工作流队列用于&#x200B;**[!UICONTROL DAM更新资产]**&#x200B;工作流。 在Dynamic Media中，用于图像和非视频资产的摄取和处理。

>[!NOTE]
>
>您必须以产品管理员身份登录到Experience Manager as a Cloud Service才能完成此任务。

**要更新预定义的Granite Transient工作流队列工作线程：**

1. 导航到`http://<host>:<port>/system/console/configMgr`上的&#x200B;**Adobe Experience Manager Web控制台配置**
1. 搜索&#x200B;**队列： Granite临时工作流队列**。

   >[!NOTE]
   >
   >由于OSGi PID是动态生成的，因此需要文本搜索而不是直接URL。

1. 在&#x200B;**[!UICONTROL 最大并行作业]**&#x200B;字段中，将该数字更改为所需的值。

   您可以增加&#x200B;**[!UICONTROL 个最大并行作业]**，以支持向Dynamic Media上载足够多的文件。 具体值取决于硬件容量。 在某些情况下（如初始迁移或一次性批量上传），您可以使用较大的值。 但是，请注意，使用较大的值（例如内核数量的两倍）可能会对其他并发活动产生负面影响。 因此，请根据特定用例测试和调整值。

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic. -->

![chlimage_1](assets/chlimage_1.jpeg)

1. 选择&#x200B;**[!UICONTROL 保存]**。

#### 更新到Dynamic Media Classic (Scene7)服务器的最大上传连接数 {#update-max-s7-upload-connections}

Dynamic Media Classic (Scene7)上传连接设置将Experience Manager资源同步到Dynamic Media Classic服务器。

>[!NOTE]
>
>您必须以产品管理员身份登录到Experience Manager as a Cloud Service才能完成此任务。

**要更新到Dynamic Media Classic (Scene7)服务器的最大上传连接数：**

1. 导航到`https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. 在&#x200B;**[!UICONTROL 连接数]**&#x200B;字段或&#x200B;**[!UICONTROL 活动作业超时]**&#x200B;字段（或同时在这两个字段中）中，根据需要更改连接数。

   **[!UICONTROL 连接数]**&#x200B;设置可控制Experience Manager允许的Dynamic Media上传的最大HTTP连接数。 通常，预定义十个连接值就足够了。

   **[!UICONTROL 活动作业超时]**&#x200B;设置定义系统等待投放服务器发布已上传的Dynamic Media资产的时间。 此值默认为2100秒或35分钟。

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
