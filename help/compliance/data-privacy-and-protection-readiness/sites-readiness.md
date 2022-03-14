---
title: 数据保护和数据隐私条例 - Adobe Experience Manager as a Cloud Service Sites 准备工作
description: 了解 Adobe Experience Manager as a Cloud Service Sites 对各种数据保护和数据隐私条例的支持，包括欧盟通用数据保护条例 (GDPR)、加州消费者隐私法案以及如何在实施新的 AEM as a Cloud Service 项目时实现合规性。
exl-id: fdcad111-0cdd-46cc-964c-3f8669ca2030
source-git-commit: e9c1ec6807f86ab00f89ef292a89a0c8efdf802b
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 100%

---

# 数据保护和数据隐私条例的 Adobe Experience Manager as a Cloud Service Sites 准备工作 {#aem-sites-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文档的内容不构成法律建议，也不会代替法律建议。
>
>请咨询您公司的法律部门，以获取关于数据保护和数据隐私条例的建议。

>[!NOTE]
>
>要详细了解 Adobe 对隐私问题的响应以及这对于您这样的 Adobe 客户的意义，请参阅 [Adobe 隐私中心](https://www.adobe.com/cn/privacy.html)。

Adobe Experience Manager as a Cloud Service Sites 可以帮助客户履行其数据隐私和保护合规性义务。此页面将指导客户完成在 AEM Sites 中处理此类请求的过程。它描述了私有数据的存储位置，以及如何手动或使用代码删除私有数据。

有关更多信息，请参阅 [Adobe 隐私中心](https://www.adobe.com/privacy.html)。

>[!NOTE]
>
>有关更多详细信息，请参阅[数据保护和数据隐私条例的 Adobe Experience Manager as a Cloud Service 准备工作](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)。

## AEM 创作层 {#aem-author-tier}

[AEM Foundation 文档](/help/compliance/data-privacy-and-protection-readiness/foundation-readiness.md)涵盖了创作服务器上的用户帐户和 UGC 内容。

## AEM 发布层 {#aem-publish-tier}

[AEM Foundation 文档](/help/compliance/data-privacy-and-protection-readiness/aem-readiness.md)涵盖了发布服务器上用于验证网站访客的用户帐户和 UGC 内容。

默认情况下，AEM Sites 组件不会存储访客在发布服务器上输入的表单数据。建议将数据转发到第三方系统或 Adobe Campaign 以供进一步处理。

## 选择加入/选择退出 {#opt-in-opt-out}

<!--
AEM has a [cookie opt-out service](/help/sites-developing/cookie-optout.md ) that can be used for managing the opt-in/opt-out for users.
-->

Adobe Experience Manager 受 Cookie 选择退出服务的约束，该服务用于管理用户的选择加入/选择退出操作。

要选择退出，请执行以下操作：

1. 导航至：
   [Adobe 隐私中心 - 选择退出](https://www.adobe.com/cn/privacy/opt-out.html)

1. 向下滚动到&#x200B;**服务** - **Experience Cloud 服务使用情况数据**。

1. 选择引用的链接；当前名为&#x200B;**此处**。

1. 您将看到以下详细信息以及用于选择退出或选择加入的选项：

   * 要选择退出对有关您访问本网站的数据进行聚合和分析，必须在浏览器上安装 Cookie。此 Cookie 表明您已选择退出。

      如果您删除选择退出 Cookie，或者如果您更换计算机或 Web 浏览器，则需要再次选择退出。

      选择退出 - 从访客会话聚合和分析中将我排除（安装 `amcglobal.sc.omtrdc.net` 选择退出 Cookie）- 单击此处。

      选择加入 - 将我包含在访客会话聚合和分析中（不要安装 `amcglobal.sc.omtrdc.net` 选择退出 Cookie）- 单击此处。
   执行上述步骤以访问实际链接。

   >[!NOTE]
   >
   > 有关深入的描述，请参阅 **2. 隐私。**&#x200B;部分（位于 [Adobe 一般使用条款](https://www.adobe.com/cn/legal/terms.html)中）。

## Analytics Foundation {#analytics-foundation}

AEM Sites 包括与 Analytics Foundation 的可选集成，该集成使用 Adobe Analytics On-demand Service 中的功能。

有关管理与 Adobe Analytics 相关的数据主题请求的更多信息，请参阅 [Adobe Analytics 和数据隐私](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-view-settings.html)。

## Personalization Foundation by Target {#personalization-foundation-by-target}

AEM Sites 包括与 Personalization Foundation by Target 的可选集成，该集成使用 Adobe Target On-demand Service 中的功能。

有关管理与 Adobe Target 相关的数据主题请求的更多信息，请参阅 [Adobe Target - 隐私和一般数据保护条例](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)。

## ContextHub {#contexthub}

<!--
AEM provides an optional data layer with [ContextHub](/help/sites-developing/contexthub.md).
-->

AEM 为 ContextHub 提供了一个可选的数据层。这会将特定于访客的数据保留在浏览器中，以用于基于规则的个性化。

默认情况下，此访客数据不会存储在 AEM 中；AEM 将规则发送到数据层，以在浏览器中做出个性化决策。

### 实施选择加入/选择退出 {#implementing-opt-in-opt-out}

网站所有者需要根据以下指南实施选择退出组件。

这些指南将选择加入作为默认设置加以实施。因此，必须先获得网站访客的明确同意，之后才能将任何个人数据存储在浏览器（客户端）的持久存储中。

* 每次包含 ContextHub 组件时都应包含选择退出组件。
* 必须向网站访客显示与网站的数据保护和隐私相关的条款和条件，以便访客：

   * 接受
   * 拒绝
   * 更改其上一个选择

* 如果网站访客接受网站的条款和条件，则应删除 ContextHub 选择退出 Cookie：

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* 如果网站访客不接受网站的条款和条件，则应设置 ContextHub 选择退出 Cookie：

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* 要检查 ContextHub 是否正在选择退出模式下运行，应在浏览器的控制台中进行以下调用：

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### 预览 ContextHub 的持久存储 {#previewing-persistence-of-contexthub}

要预览使用 ContextHub 的持久存储，用户可以：

* 例如，使用浏览器的控制台：

   * Chrome：

      * 打开“开发人员工具”>“应用程序”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”
   * Firefox：

      * 打开“开发人员工具”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”
   * Safari：

      * 在菜单栏中打开“偏好设置”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示 JavaScript 控制台”

         * “控制台”>“存储”>“本地存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“会话存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“Cookie”>“（网站）”>“ContextHubPersistence”
   * Internet Explorer：

      * 打开“开发人员工具”>“控制台”

         * `localStorage.getItem('ContextHubPersistence')`
         * `sessionStorage.getItem('ContextHubPersistence')`
         * `document.cookie`




* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL`（默认）
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub 存储定义将使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。


例如，要查看存储在 localStorage 中的数据，请执行以下操作：

要预览使用 ContextHub 的持久存储，用户可以：

* 使用浏览器的控制台：

   * Chrome - 打开“开发人员工具”>“应用程序”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”
   * Firefox - 打开“开发人员工具”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”


* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * `ContextHub.Utils.Persistence.Modes.LOCAL`（默认）
      * `ContextHub.Utils.Persistence.Modes.SESSION`
      * `ContextHub.Utils.Persistence.Modes.COOKIE`
      * `ContextHub.Utils.Persistence.Modes.WINDOW`

      ContextHub 存储定义将使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。


例如，要查看存储在 localStorage 中的数据，请执行以下操作：

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持久存储 {#clearing-persistence-of-contexthub}

要清除 ContextHub 持久存储，请执行以下操作：

* 要清除当前加载的持久存储，请执行以下操作：

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* 要清除特定的持久层（例如 sessionStorage），请执行以下操作：

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* 要清除所有 ContextHub 持久层，必须为所有层调用适当的代码：

   * `ContextHub.Utils.Persistence.Modes.LOCAL`（默认）
   * `ContextHub.Utils.Persistence.Modes.SESSION`
   * `ContextHub.Utils.Persistence.Modes.COOKIE`
   * `ContextHub.Utils.Persistence.Modes.WINDOW`
