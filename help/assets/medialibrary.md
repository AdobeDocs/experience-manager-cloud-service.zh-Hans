---
title: AEM Assets 与 AEM MediaLibrary
description: 有关AEM Assets和的常见问题解答。 AEM媒体库，包括两者之间的差异。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e98179379a97e7270b755042928133ddbd8de3fa
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 3%

---


# AEM Assets与AEM MediaLibrary常见问题{#aem-assets-vs-aem-medialibrary}

Adobe Experience Manager(AEM)Assets是AEM平台的一个组成部分。 这种顺畅的集成被视为AEM的一个主要优势，可确保内容作者的内容管理一致性和高工作效率。

## 什么是AEM Assets?{#what-is-aem-assets}

AEM Assets是AEM Platform上的一个应用程序，它允许我们的客户在基于Web的存储库中管理其数字资产(图像、视频、文档和音频剪辑)。 AEM Assets包括元数据支持、演绎版、数字资产管理查找器以及通过用户界面进行的管理。

## 什么是AEM Media Library?{#what-is-the-aem-media-library}

AEM媒体库是AEM WCM内容存储库中存储图像和其他共享资源的指定部分。 媒体库使用AEM WCM的数字资产管理功能。

## 不属于AEM WCM的AEM Assets会为我带来什么？{#what-do-i-get-from-aem-assets-that-is-not-part-of-aem-wcm}

只有AEM Assets客户才能使用的独特功能有：

1. 能够提取和编辑除标题、标记和描述之外的元数据。
1. AEM Assets管理员，单击`siteadmin`旁边的第二个选项即可从欢迎屏幕访问。
1. 与数字资产管理相关的所有工作流步骤，即AEM Assets Ingestion、AEM Assets删除、AEM Assets子资产处理、AEM Assets元数据提取。
1. 包空间中的库，包括“dam”。

使用这些功能需要获得有效的AEM Assets许可。

## AEM Assets是否可作为单独的包提供？{#is-aem-assets-available-as-a-separate-package}

否. 为了简化安装和部署，所有AEM应用程序和加载项都通过一个软件包提供，其中包含所有功能。 这并不意味着您有权使用包中的所有功能。

## 我想编辑数字资产的元数据。 我需要AEM Assets吗？{#i-want-to-edit-metadata-of-digital-assets-do-i-need-aem-assets}

如果您计划编辑除标题、描述和标记之外的元数据，则需要授权AEM Assets。

## 我想在我的网站上使用类别谓词。 我需要AEM Assets吗？{#i-want-to-use-the-category-predicate-on-my-website-do-i-need-aem-assets}

是的，类别谓词以及所有其他组件都是AEM Assets的一部分，需要AEM Assets许可证。

## 我想在导入时自动调整图像大小。 我需要AEM Assets吗？{#i-want-to-automatically-resize-images-upon-import-do-i-need-aem-assets}

是. 图像大小调整和自动工作流驱动的转换以及管理再现的功能是AEM Assets的一部分，需要AEM Assets许可证。

## 我想使用自定义的图像组件调整图像大小。 我需要AEM Assets吗？{#i-want-to-resize-images-using-a-customized-image-component-do-i-need-aem-assets}

图像组件是AEM WCM的一部分。 图像组件(也由AEM Assets使用)使用的图形库是AEM平台的一部分，不需要AEM Assets许可证。

## 如果我未授权AEM Assets，如何阻止我的用户使用AEM Assets?{#how-can-i-prevent-my-users-from-using-aem-assets-if-i-did-not-license-aem-assets}

您可以从AEM中删除所有AEM Assets特定工作流、组件、分类、选项和AEM Assets管理员。 这样做可防止用户意外使用您未授权的AEM Assets功能。

## 我要向页面添加图像，并要裁切这些图像和调整其大小。 我需要AEM Assets吗？{#i-want-to-add-images-to-a-page-and-want-to-crop-and-resize-these-images-do-i-need-aem-assets}

在此用例中，无需购买AEM Assets，即使使用媒体库也不需要在网站上使用图像，因为智能图像组件允许将图像直接上传到页面。

## 详细列表AEM Assets与媒体库{#listoffeatures}中可用功能

**AEM Assets**

* 收藏集和Lightbox
* 高级元数据属性和管理
* Adobe资产链接(连接到企业版Creative Cloud)
* AEM 桌面应用程序
* 处理配置文件
* InDesign服务器集成
* 资产模板和目录制作者框架
* Adobe Photoshop、Illustrator和InDesign链接资源
* 多语言资产管理
* PIM集成
* 权限管理
* Camera Raw支持
* 搜索彩块化管理和配置
* 预建的DAM工作流（例如，照片拍摄）
* 资产报告和分析：资产分析
* 3D资产管理
* 连接的资产
* Brand Portal
* 自助访问
* 浏览、搜索和下载
* 收藏集和文件夹共享
* 管理工具
* 智能标记
* 视觉搜索
* 资产管理员UI

**媒体库**

* 基本元数据属性
* 标记管理
* 版本控制
* 静态演绎版
* 项目、任务、工作流创作
* 活动流（时间轴）
* 查询 Builder(API)
* Marketing Cloud集成
* UI自定义和扩展
* 注释和批注