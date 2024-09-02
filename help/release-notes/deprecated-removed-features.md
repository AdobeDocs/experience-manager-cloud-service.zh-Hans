---
title: 已弃用和已删除的功能
description: 特定于  [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中已弃用和已删除的功能的发行说明。
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: d80872b1df4d31d784745dabeb0e1680fc921cb8
workflow-type: tm+mt
source-wordcount: '2172'
ht-degree: 100%

---

# 已弃用和已删除的功能和 API {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="AEM as a Cloud Service 中已弃用和已删除的功能"
>abstract="AEM as a Cloud Service 具有云原生部署模型。某些功能和特性已由云原生对应功能和特性取代，此选项卡显示了它们。"


Adobe 不断评估产品功能，以便随着时间的推移，使用更现代的替代方案重塑或替换旧功能，从而提高整体客户价值，此过程中将始终谨慎考虑功能的向后兼容性。此外，由于 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供了云原生部署模型，因此某些功能和特性已由云原生对应功能和特性取代。

为了传达即将删除/替换 [!DNL Experience Manager] 功能，以下规则适用：

1. 首先宣布弃用。已弃用的功能仍然可用，但不会进一步增强。
1. 最早会在后续的主要发行版中删除已宣布弃用的功能。将会宣布进行删除的实际目标日期。

在实际删除之前，此过程将为客户提供至少一个发行周期时间，使其实施适应已弃用功能的新版本或后续版本。

## 已弃用功能 {#deprecated-features}

此部分列出了在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中标记为已弃用的特性和功能。通常，会先将计划在未来版本中删除的功能设置为已弃用，并提供替代功能。

建议客户检查其当前部署中是否使用了此类特性/功能，然后制定相应的计划，将其实施更改为使用提供的备选方案。

| 功能 | 已弃用功能 | 替换 |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | **社交媒体状态**&#x200B;的体验片段属性。 | 该功能将很快被删除。 |
| [!DNL Sites] | 基于模板的简单内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 |
| [!DNL Assets] | `DAM Asset Update` 工作流处理摄取的图像。 | 资源提取现在使用[资源微服务](/help/assets/asset-microservices-overview.md)。 |
| [!DNL Assets] | 将资源直接上传至 [!DNL Experience Manager]。请参阅[已弃用的资源上传 API](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api)。 | 使用[直接二进制上传](/help/assets/add-assets.md)。有关技术详细信息，请参阅[直接上传 API](/help/assets/developer-reference-material-apis.md#upload-binary)。 |
| [!DNL Assets] | 不支持 `DAM Asset Update` 工作流中的[某些工作流步骤](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps)，包括 [!DNL ImageMagick] 等调用命令行工具。 | [资源微服务](/help/assets/asset-microservices-overview.md)可替代许多工作流程。对于自定义处理，请使用[后处理工作流](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)。 |
| [!DNL Assets] | FFmpeg 视频转码。 | 对于 FFmpeg 缩略图生成，请使用[资源微服务](/help/assets/asset-microservices-overview.md)。对于 FFmpeg 转码，请使用 [Dynamic Media](/help/assets/manage-video-assets.md)。 |
| [!DNL Foundation] | 复制代理的“分发”选项卡下的树复制 UI（在 2021 年 9 月 30 日后被删除） | [管理出版物](/help/operations/replication.md#manage-publication)或[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)方法 |
| [!DNL Foundation] | 复制代理管理屏幕的“分发”选项卡和复制 API 都不能用于复制超过 10MB 的内容包。请改用[管理发布](/help/operations/replication.md#manage-publication)或[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | 使用从 Adobe Developer Console 项目生成的凭据的集成将会逐步失去对服务帐户 (JWT) 凭据的支持。2024 年 5 月 1 日或之后，无法在 Adobe Developer Console 中创建新的服务帐户 (JWT) 凭据，但在 2025 年 1 月 1 日之前，现有服务帐户 (JWT) 凭据仍可用于已配置的集成，届时现有服务帐户 (JWT) 凭据将不再有效，客户必须迁移到 OAuth 服务器到服务器凭据。[了解详情](https://experienceleague.adobe.com/cn/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console)。 | [迁移](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview)到 OAuth 服务器到服务器凭据。 |

## 已删除功能 {#removed-features}

此部分列出了使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 从 [!DNL Experience Manager] 中删除的特性和功能。

| 区域 | 专题 | 替换 | 目标删除日期 |
| ------------ | ------------------ | ----------- | ------------------- |
| 用户界面 | 从产品用户界面中删除经典 UI。一些经典 UI 对话框可用于一些选择功能，例如“链接检查器”、“版本清除”和一些 Cloud Service 配置。即将发布的[产品更新](/help/release-notes/home.md)可能会进一步删除经典 UI 可用性。 | 标准 UI | 已删除 |
| [!DNL Dynamic Media] | 以前与 [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html?lang=zh-Hans#integration) 和 [Dynamic Media Hybrid 模式](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html?lang=zh-Hans#dynamic)的集成在 [!DNL Experience Manager] as a [!DNL Cloud Service] 中不可用。 | 使用 [!DNL Experience Manager] as a [!DNL Cloud Service] 提供的 [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md)。 | 已删除 |
| [!DNL Sites] | Portal Director 和 Portlet 组件 | 这些功能在 [!DNL Experience Manager] 6.4 中已弃用，现已从 [!DNL Experience Manager] 中删除。 | 已删除 |
| [!DNL Sites] | 设计导入程序 | 此功能已被删除，因为 [!DNL Experience Manager] 存储库的不可更改部分在运行时无法访问。 | 已删除 |
| [!DNL Assets] | [!DNL Assets] 无法与 Marketing Cloud Assets 核心服务和 Creative Cloud 服务进行共享。 | 要与 [!DNL Adobe Creative Cloud] 集成，请使用 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。 | 已删除 |
| [!DNL Foundation] | 对 Apache Sling 数据源（OSGi 包 org.apache.sling.datasource）的支持 | 不适用 | 已删除 |
| [!DNL Foundation] | 对 JST 脚本模板（OSGi 包 org.apache.sling.scripting.jst）的支持 | 不适用 | 已删除 |
| [!DNL Foundation] | 对 Apache Felix Http Whiteboard 的支持 | OSGi Http Whiteboard | 2022 年 3 月 |
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
    <td>使用 Sling 的 Auth Core/Auth Core SPI 接口作为替代方案</td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>使用 Sling 的 Discovery API 作为替代方案</td>
    <td>2015</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>3/1/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>3/5/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>推荐并应使用 <a href="https://johnzon.apache.org/index.html">javax.json</a> 的 Apache Johnzon 实施。 </td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>AEM as a Cloud Service 不支持自定义持久性管理器。</td>
    <td>4/30/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 处于维护模式。应改用 Commons Lang 3。</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 处于维护模式。应改用 Commons Collections 4。</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>建议您改用 Apache Felix HealthCheck API</td>
    <td>4/30/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>云环境中不支持 Felix Web 控制台</td>
    <td>4/30/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml<br>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.client.util</td>
    <td>不再支持 Eclipse Jetty 和 Felix Http Jetty 包。</td>
    <td>5/27/21</td>
    <td>8/26/21</td>
  </tr>
  <tr>
    <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>不支持在 AEM as a Cloud Service 中使用此 API。</td>
    <td>5/27/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>已弃用 Apache Felix 元类型和 SCR API。请改用 OSGi 元类型和 Declarative Service API。</td>
    <td>5/27/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>日志实施类与 AEM as a Cloud Service 不兼容。</td>
    <td>7/4/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>此 API 已被弃用，因为 Apache Abdera 自 2017 年起已停用。</td>
    <td>7/29/21</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>此 API 已被弃用，因为 Apache Abdera 自 2017 年起已停用。</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>旧版 AEM 6.x API。</td>
    <td>4/8/19</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Cloud Service 中不支持此 API。</td>
    <td>9/30/21</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>后续版本中已删除与 Apache Xerces 相关的 Util 类，导致了主要版本更改。由于这些 util 供 Filevault 内部使用，因此，公共 API 表面已弃用 API。</td>
    <td>9/1/21</td>
    <td>已删除</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>旧版 AEM 6.x API。</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http Whiteboard 不再受支持。请将代码迁移到 OSGi Http Whiteboard。</td>
    <td>1/27/2022</td>
    <td>03/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>此 API 已被弃用，请将您的代码迁移到 JDK 提供的 XML API。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>此内部 logback API 不再受 AEM as a Cloud Service 支持。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>此内部 log4j API 不再受 AEM as a Cloud Service 支持。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 已于 2015 年终止生命周期，不再受支持。</td>
    <td>1/27/2022</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>此内部 logback API 不再受 AEM as a Cloud Service 支持。</td>
    <td>1/27/2022</td>
    <td>已删除</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>由于安全漏洞，需要从 4.0.5 升级到 4.3.0。 此包不再存在于升级的 handlebar 中。</td>
    <td>5/5/2022</td>
    <td>8/5/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>不再支持此 API。 请改用 org.apache.sling.api.resource.ResourceResolverFactory。</td>
    <td>9/29/2022</td>
    <td>11/24/2022</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>该 API 已弃用。 请改用 Apache Sling 的构建器。</td>
    <td>10/31/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>此 API 不再受 AEM as a Cloud Service 支持。</td>
    <td>5/15/2023</td>
    <td>6/15/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava 核心库已弃用。</td>
    <td>5/15/2023</td>
    <td>6/15/2023</td>
  </tr>
  <tr>
    <td>org.slf4j.event	</td>
    <td>此内部 slf4j API 不再受 AEM as a Cloud Service 支持</td>
    <td>4/11/2022</td>
    <td>8/30/2024</td>
  </tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>不支持在 AEM as a Cloud Service 中使用此 API。</td>
    <td>5/17/2024</td>
    <td>6/30/2024</td>
  </tr>  
</tbody>
</table>
</details>

## OSGI 配置 {#osgi-configuration}

下面的两个列表反映 AEM as a Cloud Service OSGi 配置表面，并描述客户可配置的内容。

1. 不得由客户代码配置的 OSGi 配置的列表
1. 可配置其属性但必须遵守所示验证规则的 OSGi 配置的列表。这些规则包括是否需要属性声明、其类型，在某些情况下还包括其允许的值范围。

如果未列出某项 OSGI 配置，则可由客户代码配置它。

在 Cloud Manager 构建过程中验证这些规则。可能逐渐添加其他规则，并在表中注明预期的实施日期。客户应在目标实施日期之前遵守这些规则。在删除日期后不遵守这些规则将在 Cloud Manager 构建过程中产生错误。Maven 项目应包括 [AEM as a Cloud Service SDK 构建分析器 Maven 插件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html)以在开发本地 SDK 期间标出 OSGI 配置错误。

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

