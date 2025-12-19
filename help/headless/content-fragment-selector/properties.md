---
title: Adobe Experience Manager as a Cloud Service的微前端内容片段选择器属性
description: 属性，用于将微前端内容片段选择器配置为从应用程序中搜索、查找和检索内容片段。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 74b9493fc3cdba4a1fc64d1137f5c50c6bebca0a
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 4%

---

# 内容片段选择器——相关属性 {#content-fragment-selector-related-properties}

微型前端内容片段选择器允许您浏览或搜索存储库中的内容片段，并在您的应用程序中使用它们。

您可以使用以下属性自定义内容片段选择器的呈现方式及其使用方式：

## 内容片段选择器属性 {#content-fragment-selector-properties}

| 属性 | 类型 | 必需 | 默认 | 描述 |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | 引用`ContentFragmentSelector`实例，允许访问提供的功能，如`reload`。 |
| `imsToken` | 字符串 | 否 | | 用于身份验证的IMS令牌。 如果未提供，将启动IMS登录流程。 |
| `repoId` | 字符串 | 否 | | 用于片段选择器的存储库ID。 如果提供，选择器会自动连接到指定的存储库，并且存储库下拉列表将隐藏。 如果未提供，则用户可以从其有权访问的可用存储库列表中选择存储库。 |
| `defaultRepoId` | 字符串 | 否 | | 显示存储库选择器时，默认选定的存储库ID。 仅在未提供`repoId`时使用。 如果设置`repoId`，则隐藏存储库选择器，此值将被忽略。 |
| `orgId` | 字符串 | 否 | | 用于身份验证的组织ID。 如果未提供，则用户可以从他们有权访问的不同组织中选择存储库。 如果用户无权访问任何存储库或组织，则不会加载内容。 |
| `locale` | 字符串 | 否 | `en-US` | 区域设置。 |
| `env` | 字符串 | 否 | | 部署环境。 查看允许的环境名称的`Env`类型。 |
| `filters` | Fragmentfilter | 否 | `{ folder: "/content/dam" }` | 要应用于内容片段列表的过滤器。 默认情况下，将显示`/content/dam`下的片段。 |
| `isOpen` | 布尔型 | 否 | `false` | 用于控制选择器是打开还是关闭的标记。 |
| `noWrap` | 布尔型 | 否 | `false` | 确定是否在没有封装对话框的情况下呈现片段选择器。 当设置为`true`时，片段选择器将直接嵌入到父容器中。 用于将选择器集成到自定义布局或工作流中。 |
| `onSelectionChange` | ({ contentFragments： `ContentFragmentSelection`， domainName？： `string`， tenantInfo？： `string`， repoId？： `string`， deliveryRepos？： `DeliveryRepository[]` }) => void | 否 | | 每当选择内容片段发生更改时触发的回调函数。 提供当前选定的片段、域名、租户信息、存储库ID和投放存储库。 |
| `onDismiss` | () =>空白 | 否 | | 执行解除操作时触发的回调函数；例如，关闭选择器。 |
| `onSubmit` | ({ contentFragments： `ContentFragmentSelection`， domainName？： `string`， tenantInfo？： `string`， repoId？： `string`， deliveryRepos？： `DeliveryRepository[]` }) => void | 否 | | 用户确认选择时触发的回调函数。 接收选定的内容片段、域名、租户信息、存储库ID和投放存储库。 |
| `theme` | “浅色”或“深色” | 否 | | 片段选择器的主题。 默认情况下，它被设置为unifiedShell环境主题。 |
| `selectionType` | “单个”或“多个” | 否 | `single` | 选择类型可用于限制片段选择器的选择。 |
| `dialogSize` | &quot;fullscreen&quot;或&quot;fullscreenTakeover&quot; | 否 | `fullscreen` | 用于控制对话框大小的可选prop。 |
| `runningInUnifiedShell` | 布尔型 | 否 | | DestinationSelector是在UnifiedShell下运行还是独立运行。 |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | 否 | | 应用于内容片段列表的只读过滤器。 用户无法删除这些过滤器。 |
| `selectedFragments` | ContentFragmentIdentifier[] | 否 | `[]` | 初始选择内容片段，将在选择器打开时预先选择。 |
| `hipaaEnabled` | 布尔型 | 否 | `false` | 指示是否已启用HIPAA合规性。 |
| `inventoryView` | InventoryViewType | 否 | `table` | 要在选择器中使用的库存默认视图类型。 |
| `inventoryViewToggleEnabled` | 布尔型 | 否 | `false` | 指示是否启用库存视图切换，允许用户在表格视图和网格视图之间切换。 |

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
