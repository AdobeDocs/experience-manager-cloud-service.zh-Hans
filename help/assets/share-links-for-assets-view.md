---
title: 如何共享资源链接？
description: 生成链接并与无权访问该 [!DNL Assets view] 应用程序的其他人共享资源。
exl-id: 7d7d488b-410b-4e90-bd10-4ffbb5fcec49
feature: Adobe Asset Link, Link Sharing
role: Admin
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 88%

---

# 分享资源链接 {#share-links-assets}

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

[!DNL Assets view]使您能够生成链接并与无权访问[!DNL Assets view]应用程序的外部利益相关者共享资源。您可以定义链接的过期日期，然后使用您喜欢的通信方式（如电子邮件或消息服务）与他人共享。链接的接收者可以预览并下载资源。

## 为资源生成链接 {#generate-link-for-assets}

要为资源或包含资源的文件夹生成链接：

1. 选择包含资源的资源或/和文件夹，然后单击&#x200B;**[!UICONTROL 共享链接]**。

1. 如果要对其进行调整，请单击“日程表”图标以使用&#x200B;**[!UICONTROL 过期日期]**&#x200B;字段定义链接的过期日期。您也可以直接在`yyyy-mm-dd`格式中指定日期。默认情况下，链接的过期日期设置为自共享之日起 2 周。

1. 从&#x200B;**[!UICONTROL 共享链接]**&#x200B;字段复制链接。

   ![裁切和拉直图像的选项](assets/share-asset-link.png)

1. 单击&#x200B;**[!UICONTROL 关闭]**&#x200B;并使用电子邮件或其他协作工具共享链接。

## 访问共享资产 {#access-shared-assets}

分享资产的公共链接后，接收者无需登录到 [!DNL Assets view] 即可在网页浏览器中点击链接预览或下载分享的资产。

单击链接，单击文件夹以导航到资产，然后单击资产进行预览。您可以选择在“列表视图”或“卡片视图”中查看共享资源。

您可以将鼠标悬停在共享资源或共享资源文件夹上以选择或下载资源。

您也可以选择多个资源并单击&#x200B;**[!UICONTROL 下载]**。[!DNL Assets view]将选定的资源下载为 zip 文件。[!DNL Assets view]为您选择下载的每个资源在父 zip 文件中创建一个与资源同名的子文件夹。

要一次下载所有资源，请切换&#x200B;**[!UICONTROL 到列表视图]**，单击&#x200B;**[!UICONTROL 全选]**，然后单击&#x200B;**[!UICONTROL 下载]**。

![预览共享资源](assets/preview-shared-assets.png)

## 后续步骤 {#next-steps}

* [观看视频，了解如何在Assets视图中共享资源链接](https://experienceleague.adobe.com/docs/experience-manager-learn/assets-essentials/basics/link-sharing.html)

* 利用资源视图用户界面上的[!UICONTROL 反馈]选项提供产品反馈

* 通过右侧边栏中的[!UICONTROL 编辑此页面]![编辑页面](assets/do-not-localize/edit-page.png)或[!UICONTROL 记录问题]![创建 GitHub 问题](assets/do-not-localize/github-issue.png)来提供文档反馈

* 联系[客户关怀团队](https://experienceleague.adobe.com/?support-solution=General#support)
