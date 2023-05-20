---
title: 解决 AEM 中有关创作方面的问题
description: 使用AEM時可能會遇到的一些問題
exl-id: b9c0584d-255e-486d-b829-09e07499ecd2
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 68%

---

# 解决 AEM 中有关创作方面的问题 {#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

## 发布站点上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：
   * 您已经更改了一个页面，并将该页面发布到发布站点，但发布站点中仍显示&#x200B;*旧*&#x200B;版页面。
* **原因**:
   * 這可能有多種原因，最常見的是快取（本機瀏覽器或Dispatcher），不過有時復寫佇列可能會出現問題。
* **解决方案**：
   * 這裡有多種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並視需要檢查復寫佇列的狀態。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * 向页面 URL 的结尾处添加 `?`。例如：
      * `http://<host>:<port>/sites.html/content?`
      * 这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。
   * 如果复制队列存在问题，请与系统管理员联系。

## 组件操作在工具栏上不可见 {#component-actions-not-visible-on-toolbar}

* **问题**：
   * 在创作环境中编辑内容页面时，所有适用的组件操作均不可见。
* **原因**:
   * 在極少數情況下，先前的動作可能會影響工具列。
* **解决方案**:
   * 重新整理頁面。
