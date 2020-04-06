---
title: 将资产、文件夹和收藏集共享为链接
description: 本文介绍如何在Experience Manager资产中以超链接的形式共享资产、文件夹和收藏集。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 配置资产链接共享 {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

要为要与用户共享的资产生成URL，请使用“链接共享”对话框。 具有管理员权限或在位置具有读取权 `/var/dam/share` 限的用户可以视图与他们共享的链接。 通过链接共享资产是一种方便的方式，使外部方无需先登录AEM资产即可获得资源。

>[!NOTE]
>
>如果要将AEM作者实例中的链接共享到外部实体，请确保仅提供以下请求URL `GET` 。 阻止其他URL以确保AEM作者实例的安全。
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## 配置Day CQ邮件服务 {#configmailservice}

在将资产共享为链接之前，请配置电子邮件服务。

1. 单击或点按 AEM 徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web Console]**。
1. 在服务列表中，找到 **[!UICONTROL Day CQ Mail Service]**。
1. 单击服务旁边的&#x200B;**[!UICONTROL 编辑]**&#x200B;图标，并为 **Day CQ Mail Service]** 配置以下参数，并针对其名称提供详细信息。

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器口令

1. Click/tap **Save**.

## 配置最大数据大小 {#maxdatasize}

当您使用“链接共享”功能从共享的链接下载资产时，AEM会从存储库压缩资产层次结构，然后以ZIP文件格式返回资产。 但是，在ZIP文件中压缩的数据量没有限制的情况下，大量数据会受到压缩，这会导致JVM中内存不足错误。 要防止系统因此受到潜在的拒绝服务攻击，请在配置管理器中使用Day CQ DAM Adhoc Asset Share Proxy Servlet的 **Max Content Size(uncompressed)** （未压缩）参数配置最大大小。 如果资产的未压缩大小超出配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击/点按 AEM 徽标，然后转到&#x200B;**工具** > **操作** > **Web Console**。
1. 从Web控制台中，找到 **Day CQ DAM临时资产共享代理Servlet配置** 。
1. 在编辑模式下打开 **Day CQ DAM 临时资产共享代理 Servlet** 配置，并修改&#x200B;**最大内容大小（未压缩）**&#x200B;参数的值。
1. 保存更改。

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
