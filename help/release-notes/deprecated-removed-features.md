---
title: 已弃用和已删除的功能
description: 特定于  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已弃用和已删除的功能的发行说明。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 55b7029ccdd0da08566066c02c8f7b8eff1e032f
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 90%

---

# 已弃用和已删除的功能和 API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已弃用和已删除的功能"
>abstract="AEM as a Cloud Service 具有云原生部署模型。此选项卡突出显示了由云原生对应取代的功能和特性。"

Adobe 在不断地评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。由于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 使用了云原生部署模型，因此用云原生对应取代了某些功能和特性。

为了传达即将删除/替换 [!DNL Experience Manager] 功能，以下规则适用：

1. 首先宣布弃用。已弃用的功能仍然可用，但不会进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

此部分列出了在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中标记为已弃用的特性和功能。通常，会先将计划在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| Sites | [PWA 功能](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | 无 |
| Sites | [SPA 编辑器](/help/implementing/developing/hybrid/introduction.md) | 管理 AEM 中的 Headless 内容时首选以下编辑器：<br>- [通用编辑器](/help/edge/wysiwyg-authoring/authoring.md)，用于可视化编辑。<br>- [内容片段编辑器](/help/assets/content-fragments/content-fragments-managing.md)，用于以基于表单的方法编辑。 |
| [!DNL Sites] | [JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [Java Use API](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | **社交媒体状态**&#x200B;的体验片段属性。 | 此功能计划很快被删除。 |
| Sites | [Experience Cloud 设置自动化](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | 无 |
| [!DNL Sites] | 基于模板的简单内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资产提取现在使用[资产微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资产直接上传至 [!DNL Experience Manager]。请参阅[已弃用的资产上传 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支持 `DAM Asset Update` 工作流中的[某些工作流步骤](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)，包括 [!DNL ImageMagick] 等调用命令行工具。 | [资产微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资产微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 复制代理的“分发”选项卡下的树复制 UI（在 2021 年 9 月 30 日后被删除） | [管理出版物](/help/operations/replication.md#manage-publication)或[树激活工作流步骤](/help/operations/replication.md#tree-activation)方法。 |
| [!DNL Foundation] | 复制代理管理屏幕的“分发”选项卡和复制 API 都不能复制大于 10MB 的内容包。 | [管理出版物](/help/operations/replication.md#manage-publication)或[树激活工作流步骤](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | 使用从 Adobe Developer Console 项目生成的凭据的集成正在逐步失去对服务帐户（JWT）凭据的支持。自 2024 年 5 月 1 日起，无法在 Adobe Developer Console 中创建新的服务帐户（JWT）凭据。现有的服务帐户（JWT）凭据在 2025 年 1 月 1 日前仍可用于已配置的集成，之后将停止使用，客户需要迁移到 OAuth 服务器到服务器凭据。[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console)。 | [迁移](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)到 OAuth 服务器到服务器凭据。 |
| [!DNL Foundation] | 发布内容树工作流和相关的发布内容树工作流步骤，用于复制内容层次结构。 | 使用[树激活工作流步骤](/help/operations/replication.md#tree-activation)，其性能更佳。 |
| [!DNL Foundation] | 使用YUI压缩/缩小JavaScript客户端库。 Adobe不打算进一步更新YUI库。 | Adobe建议客户切换到Google Closure Compiler (GCC)以便进行实施。 |

## 已删除功能 {#removed-features}

此部分列出了使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 从 [!DNL Experience Manager] 中删除的特性和功能。

| 区域 | 专题 | 替换 | 目标删除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 用户界面 | 从产品用户界面中删除经典 UI。一些经典 UI 对话框可用于一些选择功能，例如“链接检查器”、“版本清除”和一些 Cloud Service 配置。即将发布的[产品更新](/help/release-notes/home.md)可能会进一步删除经典 UI 可用性。 | 标准 UI | 已删除 |
| [!DNL Dynamic Media] | 以前与 [Dynamic Media Classic](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) 和 [Dynamic Media Hybrid 模式](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic)的集成在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中不可用。 | 使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供的 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)。 | 已删除 |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 这些功能在 [!DNL Experience Manager] 6.4 中已弃用，现已从 [!DNL Experience Manager] 中删除。 | 已删除 |
| [!DNL Sites] | 设计导入程序 | 此功能已被删除，因为 [!DNL Experience Manager] 存储库的不可更改部分在运行时无法访问。 | 已删除 |
| [!DNL Assets] | [!DNL Assets] 无法与 Assets 核心服务和 Creative Cloud 服务进行共享。 | 要与 [!DNL Adobe Creative Cloud] 集成，请使用 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 | 已删除 |
| [!DNL Foundation] | 支持 Apache Sling 数据源（OSGi 包 org.apache.sling.datasource） | 不适用 | 已删除 |
| [!DNL Foundation] | 支持 JST 脚本模板（OSGi 包 org.apache.sling.scripting.jst） | 不适用 | 已删除 |
| [!DNL Foundation] | 支持 Apache Felix Http Whiteboard | OSGi Http Whiteboard | 2022 年 3 月 |
| [!DNL Foundation] | 支持 com.adobe.granite.oauth.server | Adobe IMS 集成 | 2023 年 3 月 |
| [!DNL Foundation] | 支持 org.apache.sling.serviceusermapping 功能，以[获取服务用户 ID](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | 不适用 | 8/30/24 |


## AEM API {#aem-apis}

以下是已弃用的 AEM API 及其预计删除日期的详尽列表。客户应在目标删除日期之前从其代码中删除 API。如果在删除日期之后使用 API，都会在本地 SDK/开发环境和 Cloud Manager 构建过程中生成错误。

<details>
  <summary>展开以查看已弃用的 API 的列表。</summary>
<table style="table-layout:auto">
  <tr>
    <th>包/类</th>
    <th>评论</th>
    <th>弃用日期</th>
    <th>目标删除日期</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>使用 Sling 的 Auth Core/Auth Core SPI 接口作为替代方案。<a href="#org.apache.sling.commons.auth">请参阅下面的删除说明。</a></td>
    <td>2015</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/2021</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>推荐并应使用 <a href="https://johnzon.apache.org/index.html">javax.json</a> 的 Apache Johnzon 实施。 </td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 处于维护模式。应改用Commons Lang 3。 <a href="#apache.commons">请参阅下面的删除说明。</a></td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 处于维护模式。应改用Commons Collections 4。 <a href="#apache.commons">请参阅下面的删除说明。</a></td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>云环境中不支持Felix Web控制台。 <a href="#org.apache.felix.webconsole">请参阅下面的删除说明。</a></td>
    <td>4/30/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org. eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.ecli pse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>不再支持 Eclipse Jetty 和 Felix Http Jetty 包。<a href="#org.eclipse.jetty">请参阅下面的删除说明。</a></td>
    <td>5/27/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>不支持在 AEM as a Cloud Service 中使用此 API。<a href="#com.mongodb">请参阅下面的删除说明。</a></td>
    <td>5/27/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>此 API 已被弃用，因为 Apache Abdera 自 2017 年起已停用。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">请参阅下面的删除说明。</a></td>
    <td>7/29/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>此 API 已被弃用，因为 Apache Abdera 自 2017 年起已停用。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">请参阅下面的删除说明。</a></td>
    <td>4/8/2019</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http Whiteboard 不再受支持。将您的代码迁移到 OSGi Http Whiteboard。<a href="#org.apache.felix.http.whiteboard">请参阅下面的删除说明。</a></td>
    <td>1/27/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>该 API 已弃用。将您的代码迁移到 JDK 提供的 XML API。</td>
    <td>1/27/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service不支持此内部返回API。 <a href="#ch.qos.logback">请参阅下面的删除说明。</a></td>
    <td>1/27/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service不支持此内部log4j API。 <a href="#org.slf4j">请参阅下面的删除说明。</a></td>
    <td>1/27/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1已于2015年终止生命周期，不再受支持。 <a href="#org.apache.log4j">请参阅下面的删除说明。</a></td>
    <td>1/27/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>该 API 已弃用。 请改用 Apache Sling 的构建器。</td>
    <td>10/31/2022</td>
    <td>1/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service 不支持此 API。</td>
    <td>5/15/2023</td>
    <td>6/15/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava 核心库已弃用。</td>
    <td>5/15/2023</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>AEM as a Cloud Service不支持此内部slf4j API。 <a href="#org.slf4j">请参阅下面的删除说明。</a></td>
    <td>4/11/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>改用 org.apache.sling.xss。</td>
    <td>12/12=2023</td>
    <td>6/30/2024</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>改用 org.apache.sling.xss。</td>
    <td>12/12=2023</td>
    <td>6/30/2024</td>
  </tr>
  <tr>
    <td>com.drew。*</td>
    <td>从图像和视频中提取元数据应该通过 Cloud Service 中的 Asset Compute 或通过 Apache POI 或 Apache Tika 完成。</td>
    <td>9/17/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob。*</td>
    <td>此 API 仅供内部使用。</td>
    <td>9/23/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>此 API 仅供内部使用。</td>
    <td>9/23/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>不支持在 AEM as a Cloud Service 中使用此 API。</td>
    <td>10/31/2022</td>
    <td>8/31/2025</td>
  </tr>
</tbody>
</table>
</details>

以下是已移除的 AEM API 的详细列表。

<details>
  <summary>展开以查看已移除的 API 的列表。</summary>
<table style="table-layout:auto">
  <tr>
    <th>包/类</th>
    <th>评论</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>使用 Sling 的 Discovery API 作为替代方案</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service 不支持自定义持久性管理器。</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>建议您改用 Apache Felix HealthCheck API</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty。websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>o rg.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.ecli pse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>不再支持 Eclipse Jetty 和 Felix Http Jetty 包。</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>已弃用 Apache Felix 元类型和 SCR API。请改用 OSGi 元类型和 Declarative Service API。</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>日志实施类与 AEM as a Cloud Service 不兼容。</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>旧版 AEM 6.x API。</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Cloud Service 中不支持此 API。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>后续版本中已删除与 Apache Xerces 相关的 Util 类，导致了主要版本更改。由于这些 util 供 Filevault 内部使用，因此，公共 API 表面已弃用 API。</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>旧版 AEM 6.x API。<a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">请参阅下面的删除说明。</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service 不支持此内部 logback API。</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>由于安全漏洞，需要从 4.0.5 升级到 4.3.0。此包不再存在于升级的 handlebar 中。</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>不再支持此 API。 请改用 org.apache.sling.api.resource.ResourceResolverFactory。</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>不支持在 AEM as a Cloud Service 中使用此 API。</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>此 API 仅供内部使用。</td>
  </tr>
</tbody>
</table>
</details>

### 移除 `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

如果您正在使用 `org.apache.sling.commons.auth`、`org.apache.sling.commons.auth.spi` 或二者皆用，则可以通过将代码迁移到 `org.apache.sling.auth` 来替换用法。`org.apache.sling.auth.spi`。如果您正在使用旧版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，请确保将其更新到最新版本。

操作列表：

* 将ACS AEM Commons更新到最新版本（至少6.11.0）
* 分别从 `org.apache.sling.commons.auth` 和/或 `org.apache.sling.commons.auth.spi` 迁移到 `org.apache.sling.auth`。`org.apache.sling.auth.spi`。

### 移除 `org.apache.felix.webconsole*` {#org.apache.felix.webconsole}

如果您使用`org.apache.felix.webconsole*`中的包，请从项目中移除此代码。 无法在Cloud Service中访问Web控制台。

操作列表：

* 从`org.apache.felix.webconsole*`中使用包删除代码

### 移除 `org.eclipse.jetty*` {#org.eclipse.jetty}

如果您使用 `org.eclipse.jetty` 包或其子包中的任何内容，可能需要迁移到具有类似功能的其他第三方库。如果迁移不可行，请将下面列表中所需的包添加到您的项目中。

操作列表：

* 使用其他第三方库/自有代码替换 `org.eclipse.jetty` 包的用法
* 从此列表中选择所需的包并将其添加到您的项目中：
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### 移除 `com.mongodb` {#com.mongodb}

将 Mongo 客户端 API 添加到您的项目。

操作列表：

* 将此包添加到您的项目中
   * `org.mongodb:mongo-java-driver:3.12.7`

### 移除 `Apache Commons Lang 2 and Apache Commons Collections 3` {#apache.commons}

移除未维护的Apache Commons库的使用情况，并将其替换为支持版本的使用情况。 在大多数情况下，这只需要调整包的导入，仅在某些情况下重命名了类或方法。 如果您正在使用旧版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，请确保将其更新到最新版本。

操作列表：

* 将ACS AEM Commons更新到最新版本（至少6.11.0）
* 将`org.apache.commons.lang*`的导入替换为`org.apache.commons.lang3`
* 将`org.apache.commons.collections*`的导入替换为`org.apache.commons.collecitons4`

### `org.apache.abdera*` 和 `org.apache.sling.atom.taglib` 的使用 {#org.apache.abdera_or_org.apache.sling.atom.taglib}

使用提供类似功能或自有代码的第三方库替换 `org.apache.abdera` 和 `org.apache.sling.atom.taglib` 中任何包的用法。

操作列表：

* 使用其他第三方库/自有代码替换 `org.apache.abdera` 和 `org.apache.sling.atom.taglib` 中包的用法。

### 使用 `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

将 `org.apache.felix.http.whiteboard` 的用法替换为 [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)。官方 OSGi API 具有类似的功能，并且大多数情况下的替换只需要更改服务注册属性。

操作列表：

* 将 `org.apache.felix.http.whiteboard` 的用法替换为 [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

### 使用 `ch.qos.logback*` {#ch.qos.logback}

Cloud Service不支持Logback，请删除它的所有用法。 如果您正在使用旧版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，请确保将其更新到最新版本。

操作列表：

* 将ACS AEM Commons更新到最新版本（至少6.11.0）
* 从`ch.qos.logback`中使用包删除代码

### 使用 `org.slf4j.event and org.slf4j.spi` {#org.slf4j}

如果您使用的是`org.slf4j.event`或`org.slf4j.spi`，请删除它的所有用法。 如果您正在使用旧版本的 [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/)，请确保将其更新到最新版本。

操作列表：

* 将ACS AEM Commons更新到最新版本（至少6.11.0）
* 使用`org.slf4j.event`和`org.slf4j.spi`删除代码

### 使用 `org.apache.log4j` {#org.apache.log4j}

如果您使用`org.apache.log4j`，请切换到SLF4J (`org.slf4j`)或Log4J 2.x (`org.apache.logging.log4j`)。

操作列表：

* 使用`org.slf4j` （推荐）或`org.apache.logging.log4j`替换`org.apache.log4j`的使用

## OSGI 配置 {#osgi-configuration}

下面的两个列表反映 AEM as a Cloud Service OSGi 配置表面，并描述客户可配置的内容。

1. 客户代码不得配置列出的 OSGi 配置。
1. 可配置其属性但必须遵守所示验证规则的 OSGi 配置的列表。这些规则包括是否需要属性声明、其类型，在某些情况下还包括其允许的值范围。

客户代码可以配置未列出的任何 OSGi 配置。

在 Cloud Manager 构建过程中验证这些规则。可能逐渐添加其他规则，并在表中注明预期的实施日期。客户应在目标实施日期之前遵守这些规则。在删除日期后不遵守这些规则会在 Cloud Manager 构建过程中产生错误。Maven 项目应包括 [AEM as a Cloud Service SDK 构建分析器 Maven 插件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin)以在开发本地 SDK 期间标出 OSGI 配置错误。

可在[此位置](/help/implementing/deploying/configuring-osgi.md)找到有关 OSGI 配置的其他信息。

+++无法修改的 OSGi 配置。

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
* **`com.day.cq.auth.impl.cug.CugSupportImpl`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
* **`org.apache.felix.http (Factory)`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`**（公告日期：2021 年 8 月 25 日，实施日期：2021 年 11 月 26 日）
+++

+++OSGi 配置受构建验证规则的约束。

* **`org.apache.felix.eventadmin.impl.EventAdmin`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * 类型：整数
   * 要求的范围：2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * 类型：双精度
* `org.apache.felix.eventadmin.Timeout`
   * 类型：整数
* `org.apache.felix.eventadmin.RequireTopic`
   * 类型：布尔值
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * 必填
   * 类型：字符串数组
   * 要求的范围：必须包括至少 `org.apache.felix*`、`org.apache.sling*`、`come.day*`、`com.adobe*` 所有这些
* `org.apache.felix.eventadmin.IgnoreTopic`
   * 类型：字符串数组
* **`org.apache.felix.http`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
   * `org.apache.felix.http.timeout`
      * 类型：整数
   * `org.apache.felix.http.session.timeout`
      * 类型：整数
   * `org.apache.felix.http.jetty.threadpool.max`
      * 类型：整数
   * `org.apache.felix.http.jetty.headerBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.requestBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.responseBufferSize`
      * 类型：整数
   * `org.apache.felix.http.jetty.maxFormSize`
      * 类型：整数
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * 类型：布尔值
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * 类型：布尔值
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * 类型：布尔值
   * `org.eclipse.jetty.servlet.SessionCookie`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.SessionDomain`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.SessionPath`
      * 类型：字符串
   * `org.eclipse.jetty.servlet.MaxAge`
      * 类型：整数
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * 类型：整数
   * `org.apache.felix.jetty.gziphandler.enable`
      * 类型：布尔值
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * 类型：整数
   * `org.apache.felix.jetty.gzip.syncFlush`
      * 类型：布尔值
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * 类型：字符串
   * `org.apache.felix.jetty.gzip.includedMethods`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.includedPaths`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * 类型：字符串数组
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * 类型：字符串数组
   * `org.apache.felix.http.session.invalidate`
      * 类型：布尔值
   * `org.apache.felix.http.session.container.attribute`
      * 类型：字符串数组
   * `org.apache.felix.http.session.uniqueid`
      * 类型：布尔值
* **`org.apache.sling.scripting.cache`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
   * `org.apache.sling.scripting.cache.size`
      * 类型：整数
      * 要求的范围：>= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * 必填
      * 类型：字符串数组
      * 要求的范围：必须包括 js
* **`com.day.cq.mailer.DefaultMailService`**（公告日期：2021 年 4 月 30 日，实施日期：2021 年 7 月 31 日）
   * `smtp.host`
      * 类型：字符串
   * `smtp.port`
      * 类型：整数
      * 要求的范围：465、587 或 25
   * `smtp.user`
      * 类型：字符串
   * `smtp.password`
      * 类型：字符串
   * `from.address`
      * 类型：字符串
   * `smtp.ssl`
      * 类型：字符串
   * `smtp.starttls`
      * 类型：布尔值
   * `smtp.requiretls`
      * 类型：布尔值
   * `debug.email`
      * 类型：布尔值
   * `oauth.flow`
      * 类型：布尔值
* **`org.apache.sling.commons.log.LogManager.factory.config`**（公告日期：2021 年 11 月 16 日，实施日期：2021 年 2 月 16 日）
   * `org.apache.sling.commons.log.level`
      * 类型：明细列表
      * 要求的范围：INFO、DEBUG 或 TRACE
   * `org.apache.sling.commons.log.names`
      * 类型：字符串
   * `org.apache.sling.commons.log.file`
      * 类型：字符串
   * `org.apache.sling.commons.log.additiv`
      * 类型：布尔值
+++

## Java 运行时更新至版本 21 {#java-runtime-update-21}

Adobe Experience Manager as a Cloud Service 正在转换到 Java 21 运行时。为了确保兼容性，请按照[运行时要求](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements)中所述更新库版本至关重要。

<!-- (OLD Removed from here to end of topic 1/16/25 as per instruction in https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3359689801) AEM as a Cloud Service will be moving to Java 21 runtime. In order to ensure compatibility, it is essential to make the following adjustments:

### Runtime Requirements

These adjustments are required to ensure compatibility with the Java 21 runtime. The libraries can be updated at any time as they are compatible with older versions of Java.

#### Minimum version of org.objectweb.asm {#org.objectweb.asm}

Update the usage of org.objectweb.asm to version 9.5 or higher to ensure support for newer JVM runtimes.

#### Minimum version of org.apache.groovy {#org.apache.groovy}

Update the usage of org.apache.groovy to version 4.0.22 or higher to ensure support for newer JVM runtimes.

This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

### Build-time Requirements

These adjustments are required to allow building the project with newer versions of Java but not required for runtime compatibility. The Maven plug-ins can be updated at any time as they are compatible with older versions of Java.

#### Minimum version of bnd-maven-plugin {#bnd-maven-plugin}

Update the usage of bnd-maven-plugin to version 6.4.0 to ensure support for newer JVM runtimes. Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended at this time.

#### Minimum version of aemanalyser-maven-plugin {#aemanalyser-maven-plugin}

Update the usage of aemanalyser-maven-plugin to version 1.6.6 or higher to ensure support for newer JVM runtimes.

#### Minimum version of maven-bundle-plugin  {#maven-bundle-plugin}

Update the usage of maven-bundle-plugin to version 5.1.5 or higher to ensure support for newer JVM runtimes.

#### Update dependencies in maven-scr-plugin  {#maven-scr-plugin}

The `maven-scr-plugin` is not directly compatible with Java 17 and 21. However, it is possible to generate the descriptor files by updating the ASM dependency version within the plugin configuration, similar to the snippet below:

```
[source,xml]
 <project>
   ...
   <build>
     ...
     <plugins>
       ...
       <plugin>
         <groupId>org.apache.felix</groupId>
         <artifactId>maven-scr-plugin</artifactId>
         <version>1.26.4</version>
         <executions>
           <execution>
             <id>generate-scr-scrdescriptor</id>
             <goals>
               <goal>scr</goal>
             </goals>
           </execution>
         </executions>
         <dependencies>
           <dependency>
             <groupId>org.ow2.asm</groupId>
             <artifactId>asm-analysis</artifactId>
             <version>9.7.1</version>
             <scope>compile</scope>
           </dependency>
         </dependencies>
       </plugin>
       ...
     </plugins>
     ...
   </build>
   ...
 </project>
```
-->
