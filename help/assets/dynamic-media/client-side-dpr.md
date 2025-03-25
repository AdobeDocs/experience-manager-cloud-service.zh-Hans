---
title: 使用具有客户端设备像素比的智能成像
description: 了解如何在Adobe Experience Manager as a Cloud Service的Dynamic Media中将客户端设备像素比与智能成像结合使用。
contentOwner: Rick Brough
feature: Device Pixel Ratio,Smart Imaging
role: Admin,User
exl-id: 556710c7-133c-487a-8cd9-009a5912e94c
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# 关于使用客户端设备像素比(DPR)的智能成像 {#client-side-dpr}

当前的智能成像解决方案使用用户代理字符串来确定正在使用的设备类型（台式机、平板电脑、移动设备等）。

设备检测功能（基于用户代理字符串的DPR）通常不准确，特别是对于Apple设备。 此外，无论新设备何时启动，都必须对其进行验证。

客户端DPR可为您提供100%准确的值，并且适用于任何设备，无论是Apple还是任何其他已启动的新设备。

<!-- See also [About network bandwidth optimization](/help/assets/dynamic-media/imaging-faq.md#network-bandwidth-optimization). -->

## 使用客户端DPR代码

**服务器端渲染的应用程序**

1. 通过在HTML页面的标题部分中包含以下脚本，加载Service Worker初始化(`srvinit.js`)：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe建议您在&#x200B;_之前加载此脚本_，以便立即开始初始化Service Worker。

1. 在HTML页面的body部分的顶部包含以下DPR图像标记代码：

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   您必须在HTML页面中&#x200B;_之前包含此DPR图像标记代码_。

**客户端渲染的应用程序**

1. 在HTML页面的标题部分中包含以下DPR脚本：

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   您可以将两个DPR脚本合并到一个脚本中，以避免多个网络请求。

   Adobe建议您在HTML页面的&#x200B;_之前加载这些脚本_。
Adobe还建议您将应用程序Bootstrap在不同的HTML标记下，而不是在正文元素下。 原因是`dprImageInjection.js`动态注入HTML页面中正文部分顶部的图像标记。

## JavaScript文件下载 {#client-side-dpr-script}

下载中的以下JavaScript文件仅作为示例参考提供给您。 如果您打算在HTML页面中使用这些文件，请务必编辑每个文件的代码以满足您自己的要求。

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[JavaScript文件下载](/help/assets/dynamic-media/assets/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [智能图像处理](/help/assets/dynamic-media/imaging-faq.md)
