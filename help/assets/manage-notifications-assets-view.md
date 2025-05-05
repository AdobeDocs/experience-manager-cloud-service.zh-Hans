---
title: 管理通知
description: 使用Assets查看通知，监控对存储库中可用的资源或文件夹执行的操作。
exl-id: 1fe6a845-37d5-43c2-bb96-c5b149c238ab
feature: Assets Essentials
role: User, Leader
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 68%

---

# 监视资产、文件夹和收藏集 {#watch-assets-folders}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets与Edge Delivery Services的集成</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI可扩展性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新建</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>启用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜索最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>元数据最佳实践</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 开发人员文档</b></a>
        </td>
    </tr>
</table>

通过Assets查看通知，您可以监视对存储库中可用的资源、文件夹或收藏集执行的操作。 需要选择并订阅将向您发送其通知的内容。还可配置向您发送其通知的类别。

## 订阅通知类别 {#subscribe-to-notification-categories}

可从要接收通知的类别的列表中选择并订阅。Assets视图仅向您发送您从可用选项中选择的类别的通知：

<table>
    <tbody>
     <tr>
      <th><strong>通知类别</strong></th>
      <th><strong>描述</strong></th>
     </tr>
     <tr>
      <td>请求</td>
      <td>将任务分配给用户时，当该用户对该任务执行了操作时，您将收到通知。</td>
     </tr>
     <tr>
      <td>分配给我</td>
      <td>当有任务从另一用户分配给您时，您将收到通知。</td>
     </tr>
     <tr>
      <td>对订阅的内容发表评论</td>
      <td>当用户对您订阅的资源发表评论时，您将收到通知。</td>
     </tr>
     <tr>
      <td>删除订阅的内容</td>
      <td>当用户删除您订阅的资产、文件夹或收藏集时，您将收到通知。</td>
     </tr>
     <tr>
      <td>外部共享订阅的内容</td>
      <td>当用户为您订阅的资产、文件夹或收藏集生成公共链接时，您将收到通知。</td>
     </tr>
     <tr>
      <td>修改订阅的内容</td>
      <td>当用户为您订阅的资源创建新版本时，您将收到通知。</td>
     </tr>
     <tr>
      <td>移动/重命名订阅的内容</td>
      <td>当用户移动或重命名您订阅的资源或文件夹时，您将收到通知。</td>
     </tr>
     <tr>
      <td>更新订阅的文件夹和收藏集</td>
      <td>当用户从订阅的文件夹或收藏集中添加或删除资产时，您将收到通知。</td>
     </tr>    
    </tbody>
   </table>

要订阅通知类别，请执行以下操作：

1. 在Assets视图用户界面上的菜单栏右端单击![铃铛图标](assets/bell-icon.svg)。

1. 单击 ![设置图标](assets/settings-icon.svg) 以查看 [!UICONTROL Experience Cloud 首选项]页面。

1. 单击可在左窗格中找到的&#x200B;**[!UICONTROL 通知]**&#x200B;选项。

1. 在&#x200B;**[!UICONTROL 通知]**&#x200B;部分中，导航到[!UICONTROL Assets视图]部分，并确保已将切换选项切换到“开”状态。

   Assets视图中的![通知](assets/enable-notifications.png)

1. 单击&#x200B;**[!UICONTROL 自定义]**&#x200B;以查看通知类别。
   Assets视图中的![通知](assets/enable-notification-categories.png)

1. 选择需要通知您的通知类别。

## 关注和取消关注文件夹、资产或收藏集 {#watch-unwatch-assets}

在[订阅通知类别](#subscribe-to-notification-categories)之后，必须订阅内容才能开始接收通知。

>[!NOTE]
>
>* 对于&#x200B;**[!UICONTROL 请求]**&#x200B;和&#x200B;**[!UICONTROL 分配给我]**&#x200B;通知类别，在订阅通知类别之后，无需订阅内容。对于您创建的请求以及在有任务分配给您时，自动向您发送通知。
>* Assets视图仅在其他用户对订阅的内容执行操作时发送通知。 您不会收到您对订阅的内容执行的操作的通知。

要订阅内容，请选择需要订阅的文件夹、资产或收藏集，然后单击&#x200B;**[!UICONTROL “关注”]**。

Assets视图显示一条成功消息。 可单击可在成功消息上找到的&#x200B;**[!UICONTROL 转到通知首选项]**&#x200B;以编辑您[对通知类别的订阅](#subscribe-to-notification-categories)。

Assets视图中的![通知](assets/watch-assets.png)

Assets视图现在发送订阅类别的通知。 您还可以选择多个资产、文件夹或收藏集，然后单击&#x200B;**[!UICONTROL “关注”]**&#x200B;以节省时间。但是，如果选择多个实体，并且其中有实体已订阅某些资源或文件夹，则不显示&#x200B;**[!UICONTROL 关注]**&#x200B;选项。

同样，要取消订阅，请选择已订阅的资产或文件夹，然后单击&#x200B;**[!UICONTROL “取消关注]**。

## 查看通知 {#view-notifications}

通知显示在Assets视图用户界面的菜单栏右端。

Assets视图中的![通知](assets/notifications-assets-essentials.png)

单击通知后，Assets视图会将您导航到通知中引用的相应资源或文件夹。
