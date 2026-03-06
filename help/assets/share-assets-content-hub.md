---
title: 在 [!DNL the Content Hub]中共享Assets
description: 在 [!DNL the Content Hub]中共享Assets
role: User
exl-id: 5284d229-1596-40bf-aa5f-af4b6500ebdf
source-git-commit: 12bb550ff275c84bc60869e91e953993aab57aa5
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 2%

---

# 在 Content Hub 共享资产 {#search-assets-as-a-link}

创建指向所选资产的链接以轻松与他人共享。 作为授权[!DNL Content Hub]用户，请选择您的[!DNL Content Hub]环境中可用的一个或多个资源，生成链接，并将其发送给其他专用或公共用户。

>[!VIDEO](https://video.tv.adobe.com/v/3474890/?learn=on&enablevpops=on){transcript=true}

## 先决条件 {#prerequisites}

[Content Hub用户](deploy-content-hub.md#onboard-content-hub-users)可以创建指向所选资源的链接并与其他用户共享。

## 共享资产 {#share-assets}

要与专用或公共用户共享一个或多个资产，请执行以下步骤：

1. 导航到您的[!DNL Content Hub]主页，选择一个或多个资源并单击![共享](/help/assets/assets/share.svg) **[!UICONTROL 共享]**&#x200B;以在&#x200B;**[!UICONTROL 共享资源]**&#x200B;对话框中显示单个选定资源或多个选定资源的列表。

   您还可以选择并共享![收藏集](/help/assets/assets/Smock_Collection_18_N.svg) **[!UICONTROL 收藏集]**&#x200B;中可用的资产。

1. 在&#x200B;**[!UICONTROL 共享资源]**&#x200B;对话框中查看资源或查看可用资源列表。 单击资产旁边的![取消选择](/help/assets/assets/Close.svg)以将其从列表中删除。

1. 指定标题和可选描述，以定义所选资源集。

1. 选择&#x200B;**[!UICONTROL 过期时段]**。

1. 在&#x200B;**[!UICONTROL 谁可以访问]**&#x200B;下拉列表下，选择访问选项并单击&#x200B;**[!UICONTROL 获取链接]**&#x200B;以生成链接并与所选用户共享。 个人用户需要登录到其[!DNL Content Hub]环境才能访问共享资源页面。 而公共用户作为来宾无需登录到[!DNL Content Hub]即可访问共享资源页面。

<!--1. Select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Get Link]** to generate a link to share with private users. Private users sign in to their [!DNL Content Hub] environment to access the shared assets page.-->

![专用和公开链接](/help/assets/assets/shared-link-for-assets.png)

<!--Enable the **[!UICONTROL Public Link]** toggle, select a **[!UICONTROL period of expiration]** and click **[!UICONTROL Generate Public Link]** to generate a link to share with public users. Public users, as guests, access the shared assets page without signing in to [!DNL Content Hub].-->

>[!NOTE]
> 
> [从配置页面](/help/assets/configure-content-hub-ui-options.md#enable-public-link-sharing)启用公共链接共享，以在&#x200B;**[!UICONTROL 共享资源]**&#x200B;对话框上显示&#x200B;**[!UICONTROL 公共链接]**&#x200B;切换开关。

## 从其预览页面共享资源 {#share-asset-from-preview-page}

执行以下步骤以在预览资产时共享资产：

1. 导航到[!DNL Content Hub]主页，然后单击资产缩略图以预览资产，并在对话框的右侧窗格中显示菜单选项。
1. 选择![共享](/help/assets/assets/share.svg)以显示&#x200B;**[!UICONTROL 共享]**面板。
   预览资产时![共享资产](/help/assets/assets/share-link-asset-preview.png)
1. 按照[共享资产](#share-assets)部分中的步骤3至5，从此&#x200B;**[!UICONTROL 共享]**&#x200B;面板生成并共享资产链接（私有或公共）。

## 访问共享资源 {#access-shared-assets}

通过链接访问共享资源页面，并执行以下操作：

* 选择一个或多个资源并单击![下载](/help/assets/assets/download-icon.svg) **[!UICONTROL 下载]**&#x200B;从可用下载选项中选择&#x200B;**[!UICONTROL 原始]**、**[!UICONTROL 静态]**或两个呈现版本。
  ![](/help/assets/assets/download-shared-assets.png)
* 单击资源缩略图可查看资源的元数据。
* 在共享资源页面（[通过专用链接访问](#share-assets)）上，单击资源缩略图并选择![下载](/help/assets/assets/download-icon.svg)以在&#x200B;**[!UICONTROL 下载]**面板上选择和查看资源的可用动态演绎版，然后再选择并下载。
  ![](/help/assets/assets/download-renditions-shared-assets-page.png)

## 常见问题解答 {#faqs-share-assets-content-hub}

### 在AEM Assets Content Hub中共享资源是什么意思？

在AEM Assets Content Hub中共享资源允许授权用户通过生成链接轻松与他人共享一个或多个资源或整个收藏集。 此链接可以发送给私人用户（必须登录）或公共用户（可以来宾身份访问），让收件人直接查看和下载所选资源。

### 如何使用AEM Assets Content Hub与他人共享资源或收藏集？

要在Content Hub中共享资源或收藏集，请导航到Content Hub主页，选择一个或多个资源（或转到收藏集的收藏集选项卡），然后单击共享图标。 在“共享”对话框中，您可以预览资源，根据需要删除任何资源，添加标题和描述，选择可以访问链接的人员（私有或公共），设置有效期，然后单击“获取链接”以生成和复制可共享URL。 然后，可以将链接发送给团队成员或利益相关者。

### 在AEM Assets Content Hub中共享资源时，有哪些访问选项可用，它们之间有何差异？

Content Hub允许您为共享链接选择两个访问选项：私有和公共。 专用链接要求收件人登录到其Content Hub环境才能查看和下载资源，从而提供更高的安全性。 拥有公共链接的任何人都可以访问该链接，而无需登录。 每种链接类型都带有自己的过期设置，例如，公共链接为24小时到一周，专用链接为自定义日期。

### 管理员是否管理任何配置以便能够为AEM Assets Content Hub中的资源生成公共链接？

可以，管理员可以启用或禁用配置UI上&#x200B;**收藏集和共享**&#x200B;选项卡中提供的&#x200B;**启用公共链接**&#x200B;切换功能，以管理在AEM Assets Content Hub中为资源生成的公共链接。

### 我能否在AEM Assets Content Hub中设置共享资源链接的过期日期？这为何很重要？

能，您可以在Content Hub中设置私有和公共共享链接的过期日期。 对于公共链接，您可以从24小时到一周等预设中进行选择，而专用链接允许您从预设中进行选择或设置自定义过期日期。 过期日期很重要，因为一旦链接过期，就无法再用来访问或下载资产，这有助于维护内容的安全性和控制力。

### 收件人可以对使用AEM Assets Content Hub创建的共享资源链接执行什么操作，以及是否有下载各种演绎版的选项？

接收共享资产链接的收件人可以在浏览器中打开该链接以进行预览、选择和下载提供的资产。 如果在Content Hub中启用了资源演绎版，则收件人可以选择要下载的演绎版（例如原始演绎版或静态演绎版）。 资源和演绎版将下载为zip文件，并且可以通过单击资源缩略图查看元数据。 在设置的到期日期之前，链接将一直正常运行。




