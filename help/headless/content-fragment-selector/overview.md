---
title: 适用于Adobe Experience Manager as a Cloud Service的微前端内容片段选择器
description: 使用微前端内容片段选择器来搜索、查找和检索应用程序中的内容片段。
role: Admin, User
source-git-commit: 32e1b3cef768b420f32b70202ddadc80db2b74e8
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 11%

---


# 微前端内容片段选择器 {#micro-frontend-content-fragment-selector}

微前端内容片段选择器提供了一个用户界面，可轻松与Adobe Experience Manager (AEM) as a Cloud Service存储库集成。 利用界面，您可以浏览或搜索存储库中的内容片段，并在应用程序中使用它们。

微型前端用户界面可在您的应用程序中使用内容片段选择器包。 对包的任何更新都会自动导入并加载到您的应用程序中。

![微前端内容片段选择器 — 概述](/help/headless/assets/content-fragment-selector-overview.png)

内容片段选择器提供了许多好处，例如：

* 轻松与任何Adobe应用程序集成。
* 易于维护，因为内容片段选择器包的更新会自动部署到您的应用程序可用的内容片段选择器。 这意味着您的应用程序无需采取措施来加载最新修改。
* 使用用于控制内容片段选择器在您的应用程序中显示的属性，轻松进行自定义。
* 全文搜索与可自定义的筛选器一起，允许在创作体验中快速导航内容片段。
* 能够在IMS组织内切换存储库以进行内容片段选择。
* 能够排序内容片段并在所选视图中查看它们。

## 先决条件 {#prerequisites}

### IMS身份验证 {#ims-authentication}

如果您需要IMS身份验证工作流，则必须确保：

* 应用程序正在`HTTPS`上运行。
* 应用程序的URL在IMS客户端允许的重定向URL列表中。
* 使用 Web 浏览器上的弹出窗口配置和呈现 IMS 登录流。因此，应在目标浏览器上启用或允许弹出窗口。

或者，如果您的应用程序已经通过IMS工作流身份验证，则可以添加相应的IMS信息。

## 安装 {#installation}

使用`ContentFragmentSelector`组件。 有几个安装选项：

1. NPM注册表(专用Adobe注册表)

   * 将以下内容添加到`.npmrc`：

     ```html
     @aem-sites:registry=https://artifactory.corp.adobe.com/artifactory/api/npm/npm-aem-sites-release/
     ```

   * 然后安装

     ```html
     npm install @aem-sites/content-fragment-selector
     ```

1. Git 存储库

   * 将以下项添加到`package.json`依赖项：

     ```html
     "@aem-sites/content-fragment-selector": "git+https://github.com/adobe/<your-private-repo-url>.git#version"
     ```

## 使用内容片段选择器 {#using-the-Content-Fragment-selector}

一旦设置内容片段选择器并通过身份验证而将AEM as a Cloud Service应用程序与内容片段选择器结合使用，您就可以选择内容片段或执行各种其他操作以在存储库中搜索您的片段：

![内容片段选择器](/help/headless/assets/content-fragment-selector-using.png)

* 通过右上角的&#x200B;**存储库**&#x200B;选择器，您可以选择要使用的存储库
* 在最左侧的面板中，您可以：
   * 隐藏或显示选定存储库中的文件夹
   * 选择特定文件夹以显示该文件夹中的内容片段
* 在主面板中，您可以：
   * 选择内容片段
   * 搜索内容片段
   * 根据不同的列对当前列表进行排序；升序或降序
   * 查看视图格式指示器
   * 显示、隐藏和指定筛选器

### 隐藏/显示面板 {#hide-show-panel}

要隐藏左侧导航中的文件夹，请单击 **隐藏文件夹**&#x200B;图标。要撤消更改，请再次单击 **隐藏文件夹**&#x200B;图标。

### 存储库切换器 {#repository-switcher}

使用内容片段选择器，您可以选择要进行片段选择的存储库。

您可以从主面板顶部的&#x200B;**存储库**&#x200B;下拉列表中选择您选择的存储库。

![内容片段选择器](/help/headless/assets/content-fragment-repository-selector.png)

下拉列表中可用的存储库选项基于 `repositoryId` 文件中定义的 `index.html` 属性。此属性基于当前登录用户访问的选定IMS组织的环境。

使用者可以从特定存储库传递首选的`repositoryID`以呈现片段，并停止呈现存储库切换器。

### 内容片段文件夹 {#content-fragments-folders}

内容片段存储库是可用于执行操作的内容片段文件夹的集合。

### 过滤器 {#filters}

内容片段选择器还提供了现成的过滤器选项来优化您的搜索结果。 可以使用各种过滤器，包括：

* **片段模型**
* **本地化**
* **状态**：片段的当前状态；`New`、`Draft`、`Published`、`Modified`、`Unpublished`
* 标记
* 用户
* 时间和日期

![筛选器选项](/help/headless/assets/content-selector-filters.png)

您还可以创建默认搜索筛选器以保存以供将来使用。 要为内容片段创建自定义搜索过滤器，您可以使用`filterSchema`属性。

### 搜索栏 {#search-bar}

使用内容片段选择器，您可以对选定存储库中的片段执行全文搜索。 例如，如果您在搜索栏中键入关键字`wave`，则会显示任何元数据属性中提到的所有包含`wave`关键字的片段。

### 排序 {#sorting}

您可以在内容片段选择器中按各种属性对片段进行排序。 您还可以按升序或降序对片段进行排序。

### 视图类型 {#view-type}

内容片段选择器允许您在中查看片段：

* **表视图**
