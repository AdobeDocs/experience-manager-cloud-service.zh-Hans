---
title: Adobe Experience Manager as a Cloud Service的微前端内容片段选择器属性
description: 属性，用于将微前端内容片段选择器配置为从应用程序中搜索、查找和检索内容片段。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: a3d8961b6006903c42d983c82debb63ce8abe9ad
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 3%

---

# 内容片段选择器 — 相关属性 {#content-fragment-selector-related-properties}

微型前端内容片段选择器允许您浏览或搜索存储库中的内容片段，并在您的应用程序中使用它们。

您可以使用以下属性自定义内容片段选择器的呈现方式及其使用方式：

## 内容片段选择器属性 {#content-fragment-selector-properties}

| 属性 | 类型 | 必需 | 默认 | 描述 |
|--- |--- |--- |--- |--- |
| `imsToken` | 字符串 | 否 | | 用于身份验证的IMS令牌。 |
| `repoId` | 字符串 | 否 | | 用于身份验证的存储库ID。 |
| `orgId` | 字符串 | 是 | | 用于身份验证的组织ID。 |
| `locale` | 字符串 | 否 | | 区域设置数据。 |
| `env` | 环境 | 否 | | 内容片段选择器部署环境。 |
| `filters` | Fragmentfilter | 否 | | 要应用于内容片段列表的过滤器。 默认情况下，将显示`/content/dam`下的片段。 默认值： `{ folder: "/content/dam" }` |
| `isOpen` | 布尔型 | 是 | `false` | 用于触发打开或关闭选择器的标志。 |
| `onDismiss` | () =>空白 | 是 | | 选择&#x200B;**解除**&#x200B;时要调用的函数。 |
| `onSubmit` | ({ contentFragments： `{id: string, path: string}[]`， domainNames： `string[]` }) => void | 是 | | 在选择一个或多个内容片段后使用&#x200B;**Select**&#x200B;时要调用的函数。 <br><br>函数将接收：<br><ul><li> 选定的内容片段，包含`id`和`path`字段</li><li>和与存储库的程序ID和环境ID相关的域名，其状态为`ready`和`tier`发布</li></ul><br>如果没有域名，它将使用发布实例作为回退域。 |
| `theme` | “浅色”或“深色” | 否 | | 内容片段选择器的主题。 默认主题设置为UnifiedShell环境的主题。 |
| `selectionType` | “单个”或“多个” | 否 | `single` | 可用于限制FragmentSelector的选择类型。 |
| `dialogSize` | &quot;fullscreen&quot;或&quot;fullscreenTakeover&quot; | 否 | `fullscreen` | 用于控制对话框大小的可选属性。 |
| `waitForImsToken` | 布尔型 | 否 | `false` | 指示内容片段选择器是否在SUSI流的上下文中渲染，并需要等待`imsToken`准备就绪。 |
| `imsAuthInfo` | ImsAuthInfo | 否 | | 包含登录用户的IMS身份验证信息的对象。 |
| `runningInUnifiedShell` | 布尔型 | 否 | | 指示内容片段选择器是在UnifiedShell下运行还是独立运行。 |
| `readonlyFilters` | ResourceReadonlyFiltersField | 否 | | 可应用于内容列表的只读过滤器 — 无法删除。 |

## ImsAuthProps属性 {#imsauthprops-properties}

`ImsAuthProps`属性定义内容片段选择器用于获取`imsToken`的身份验证信息和流程。 通过设置这些属性，您可以控制身份验证流程的行为方式，并为各种身份验证事件注册侦听器。

| 属性名称 | 描述 |
|--- |--- |
| `imsClientId` | 表示用于身份验证的IMS客户端ID的字符串值。 此值由Adobe提供，特定于您的Adobe AEM CS组织。 |
| `imsScope` | 描述身份验证中使用的范围。 范围决定了应用程序对组织资源的访问级别。 多个范围可以用逗号分隔。 |
| `redirectUrl` | 表示验证后用户被重定向到的URL。 此值通常设置为应用程序的当前URL。 如果未提供`redirectUrl`，`ImsAuthService`将使用用于注册`imsClientId`的redirectUrl |
| `modalMode` | 布尔值，指示是否应在模态（弹出窗口）中显示身份验证流程。 如果设置为`true`，则身份验证流程将在弹出窗口中显示。 如果设置为`false`，则身份验证流程将以整页重新加载方式显示。<br>**注意：**&#x200B;为获得更好的UX，如果用户禁用了浏览器弹出窗口，则可以动态控制此值。 |
| `onImsServiceInitialized` | Adobe IMS身份验证服务初始化时调用的回调函数。 此函数接受一个参数`service`，该参数是表示Adobe IMS服务的对象。 有关更多详细信息，请参阅[`ImsAuthService`](#imsauthservice-ims-auth-service)。 |
| `onAccessTokenReceived` | 在从Adobe IMS身份验证服务收到`imsToken`时调用的回调函数。 此函数接受一个参数`imsToken`，该参数是一个表示访问令牌的字符串。 |
| `onAccessTokenExpired` | 访问令牌过期时调用的回调函数。 此函数通常用于触发新的身份验证流程以获取新的访问令牌。 |
| `onErrorReceived` | 身份验证期间发生错误时调用的回调函数。 此函数采用两个参数：错误类型和错误消息。 错误类型是表示错误类型的字符串，错误消息是表示错误消息的字符串。 |

## ImsAuthService属性 {#imsauthservice-properties}

`ImsAuthService`类处理内容片段选择器的身份验证流程。 它负责从Adobe IMS身份验证服务获取`imsToken`。 `imsToken`用于验证用户并授权访问Adobe Experience Manager (AEM) CS存储库。 ImsAuthService使用`ImsAuthProps`属性来控制身份验证流并注册各种身份验证事件的侦听器。 您可以使用方便的`registerContentFragmentSelectorAuthService`函数在内容片段选择器中注册`ImsAuthService`实例。 `ImsAuthService`类中有以下函数可用。 但是，如果您使用`registerContentFragmentSelectorAuthService`函数，则无需直接调用这些函数。

| 函数名称 | 描述 |
|--- |--- |
| `isSignedInUser` | 确定用户当前是否已登录到服务并相应地返回布尔值。 |
| `getImsToken` | 检索当前登录用户的身份验证`imsToken`，该身份验证可用于验证其他服务的请求，如生成资产&#x200B;_演绎版。_ |
| `signIn` | 启动用户的登录流程。 此函数使用`ImsAuthProps`在弹出窗口或全页重新加载中显示身份验证。 |
| `signOut` | 将用户签出服务，使其身份验证令牌失效，并要求他们再次登录以访问受保护的资源。 调用此函数将重新加载当前页面。 |
| `refreshToken` | 刷新当前登录用户的身份验证令牌，防止该令牌过期，并确保对受保护资源的访问不会中断。 返回可用于后续请求的新身份验证令牌。 |
