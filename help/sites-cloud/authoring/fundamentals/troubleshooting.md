---
title: 解决 AEM 中有关创作方面的问题
description: 使用 AEM 时可能遇到的一些问题
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# 解决 AEM 中有关创作方面的问题 {#troubleshooting-aem-when-authoring}

以下部分涵盖您在使用 AEM 时可能遇到的一些问题，以及有关如何解决这些问题的建议。

## 发布网站上仍显示旧的页面版本 {#old-page-version-still-on-published-site}

* **问题**：
   * You have made changes to a page and published the page to the publish site, but the *old* version of the page is still being shown on the publish site.
* **原因**：
   * 这种情况可能有几个原因，最常见的原因是本地浏览器或调度程序缓存问题，但有时也可能是复制队列的问题。
* **解决方案**：
   * 这里列举了各种可能的情况：
   * 确认页面复制正确。检查页面状态，如有必要，检查复制队列的状态。
   * 清除本地浏览器中的缓存，然后再次访问页面。
   * Add `?` to the end of the page URL. For example:
      * `http://<host>:<port>/sites.html/content?`
      * 这将会绕过调度程序而直接从 AEM 请求页面。如果收到更新的页面，则表示应清除调度程序缓存。
   * 如果复制队列存在问题，请与系统管理员联系。

## 组件操作在工具栏上不可见 {#component-actions-not-visible-on-toolbar}

* **问题**：
   * 在创作环境中编辑内容页面时，所有适用的组件操作均不可见。
* **原因**：
   * 在极少数的情况下，之前的操作可能会影响工具栏。
* **解决方案**：
   * 刷新页面。
