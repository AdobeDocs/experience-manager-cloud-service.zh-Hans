---
title: '安装和配置疑难解答  '
seo-title: Troubleshooting installation and configuration
description: 安装和配置疑难解答
seo-description: Troubleshooting installation and configuration
contentOwner: khsingh
exl-id: 249ec8f2-4176-428a-bfcf-80b381ec7263
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 配置 {#installation-and-configuration}

在配置Cloud Service环境时，您可能会遇到以下一些问题：

## Forms选项不可用

的 **[!UICONTROL Forms]** 选项在 **[!UICONTROL 导航]** 页面。

![Forms选项不可用](assets/installation-configuration-forms-option-unavailable-troubleshooting.png)

启用 **[!UICONTROL Forms]** 选项：

1. 登录到 [Cloud Manager](https://experience.adobe.com/)
1. 找到您的程序，然后单击 ![Forms选项不可用](assets/Smock_Edit_18_N.svg) 图标。 它会打开程序的“编辑程序”(Edit Program)页面。
1. 打开 **[!UICONTROL 解决方案和附加组件]** 选项卡。
1. 选择 **[!UICONTROL Forms]** 选项并单击 **[!UICONTROL 保存]**.

   ![选择Forms选项](assets/installation-configuration-select-forms-option.png)
1. [创建](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html?lang=en#how-to-use) 和 [运行](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) 生产和非生产管道。

构建和部署管道后， **[!UICONTROL Forms]** 选项 **[!UICONTROL 导航]** 页面。

<!--  
## Environment creation fails {#environment-creation-fails}

Users are unable to create an [!DNL AEM Forms] as a Cloud Service environment. The environment creation fails after running for some time.

A missing profile can lead to environment creation failure. Check that the profile exists in Admin Console. If the profile does not exist, perform the following steps to create the profile:

1. Log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not any other ID or Federated ID to login.
1. Click the **[!UICONTROL Automated Forms Conversion Service]** option.
1. Click **[!UICONTROL New Profile]** in the Products tab.
1. Specify Name, Display Name, and Description for the profile. Click **[!UICONTROL Done]**. A profile is created.

If the profile exists and issues still persist, contact Adobe Support. -->

## 生成管道失败 {#build-pipeline-fails}

用户无法运行生成管道。 管道运行一段时间后失败。

要解决此问题，请打开Cloud Manager，选择 **[!UICONTROL 更新]** 选项，然后运行管道。
