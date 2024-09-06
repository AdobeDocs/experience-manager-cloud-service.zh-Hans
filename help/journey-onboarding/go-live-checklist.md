---
title: 上线清单
description: 了解成功使用AEM as a Cloud Service所需具备的所有元素。
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 56%

---

# 上线清单 {#Go-Live-Checklist}

查看此活动列表以确保您顺利且成功地执行 Go-Live。

* 运行具有功能和 UI 测试的端到端生产管道，以确保&#x200B;**总是最新的** AEM 产品体验。请参阅以下资源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自定义功能测试](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 测试](/help/implementing/cloud-manager/ui-testing.md)
* 如果您要从 AEM 6.5 迁移，则应将内容迁移到生产环境，并确保在测试阶段有相关的子集可用。
   * AEM 的 DevOps 最佳实践意味着代码从开发环境移动到生产环境，而内容从生产环境向下移动。
* 设定代码和内容冻结期。
   * 另见 [迁移的代码和内容冻结时间线](#code-content-freeze)部分
* 执行最终内容增补。
* 验证Dispatcher配置。
   * 使用有助于在本地配置、验证和模拟Dispatcher的本地Dispatcher验证器
      * [设置本地Dispatcher工具](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites)。
   * 仔细检查虚拟主机配置。
      * 最简单（也是默认）的解决方案是在`/dispatcher/src/conf.d/available_vhostsfolder`中的虚拟主机文件中包含`ServerAlias *`。 这样做可以使产品功能测试、Dispatcher缓存失效和克隆使用的主机别名正常运行。
      * 但是，如果不能接受`ServerAlias *`，则除了自定义域之外，必须至少允许以下`ServerAlias`个条目：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 配置 CDN、SSL 和 DNS。
   * 如果您使用自己的 CDN，请输入支持票以配置适当的路由。
      * 见章节 [客户 CDN 指向 AEM 托管 CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)在 CDN 文档中了解详细信息。
      * 根据 CDN 供应商的文档配置 SSL 和 DNS。
   * 如果您不使用其他 CDN，请按照以下文档管理 SSL 和 DNS：
      * 管理 SSL 证书
         * [管理SSL证书简介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL证书](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自定义域名（DNS）
         * 确保DNS直接转换不会引发意外问题。 在上线并进行一轮UAT测试之前，请创建一个测试子域以将生产实例连接到。 因此，如果您的域是example.com，则可以创建一个子域test.example.com并将其应用于生产环境。 在对域进行UAT测试期间，应查找适当的链接重定向、缓存和Dispatcher配置等内容。
         * [自定义域名简介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [添加自定义域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自定义域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 请记住验证为您的 DNS 记录设置的 TTL。
      * TTL 是 DNS 记录在请求服务器更新之前保留在缓存中的时间量。
      * 如果您的TTL非常高，则传播对DNS记录的更新需要较长时间。
* 运行满足您的业务需求和目标的性能和安全测试。
   * 在暂存环境中执行测试。  它的规模与生产环境相同。
   * 开发环境的规模与阶段和生产环境的规模不同。
* 切换并确保在没有任何新部署或内容更新的情况下执行实际上线。
* 创建Admin Console用户通知配置文件。 参见 [通知轮廓](/help/journey-onboarding/notification-profiles.md)
* 考虑配置流量过滤规则来控制哪些流量不允许进入您的网站。
   * 速率限制流量过滤规则是防御DDoS攻击的有效工具。 一种称为WAF （Web应用程序防火墙）的特殊流量过滤器规则需要单独的许可证。
   * 请参阅文档以了解一些 [建议的入门规则](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules)。

如果您需要在上线期间重新调整任务，您可以随时参考该列表。
