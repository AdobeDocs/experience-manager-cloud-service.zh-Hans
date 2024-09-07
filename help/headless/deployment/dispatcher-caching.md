---
title: GraphQL 持久化查询 - 在 Dispatcher 中启用缓存
description: Dispatcher 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。您可以在 AEM Headless 中为持久化查询启用缓存。
feature: Headless, Dispatcher, GraphQL API
exl-id: 30a97e56-6699-41c4-a4eb-fc6236667f8f
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: ht
source-wordcount: '339'
ht-degree: 100%

---

# GraphQL 持久化查询 - 在 Dispatcher 中启用缓存 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果在 Dispatcher 中启用了缓存，则不需要 [CORS 筛选条件](/help/headless/deployment/cross-origin-resource-sharing.md)，并且可以忽略该部分。

默认情况下，Dispatcher 中未启用持久化查询的缓存。无法实施默认启用，因为对多个源使用 CORS（跨源资源共享）的客户需要检查并（可能需要）更新其 Dispatcher 配置。

>[!NOTE]
>
>Dispatcher 不会缓存 `Vary` 标头。
>
>可以在 Dispatcher 中启用其他 CORS 相关标头的缓存，但如果存在多个 CORS 源，则可能不够。

>[!NOTE]
>
>有关 Dispatcher 的详细文档，请参阅 [Dispatcher 指南](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)。

## 启用持久化查询的缓存 {#enable-caching-persisted-queries}

要启用持久化查询的缓存，请定义 Dispatcher 变量 `CACHE_GRAPHQL_PERSISTED_QUERIES`：

1. 将该变量添加到 Dispatcher 文件 `global.vars` 中：

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>为了对缓存的持久查询实现单独的 `ETag` 标头计算（对于 *每个* 唯一的响应），必须在 Dispatcher 配置虚拟主机配置中使用 `FileETag Digest` 设置（如果它尚不存在）：
>
>```xml
><Directory />    
>   ...    
>   FileETag Digest
></Directory> 
>```

>[!NOTE]
>
>为了符合 [Dispatcher 对可缓存文档的要求](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html?lang=zh-Hans#how-does-the-dispatcher-return-documents%3F)，Dispatcher 将后缀 `.json` 添加到所有持久化查询 URL，以便能够缓存结果。
>
>在启用持久化查询缓存后，将通过重写规则添加此后缀。

## Dispatcher 中的 CORS 配置 {#cors-configuration-in-dispatcher}

使用 CORS 请求的客户可能需要在 Dispatcher 中查看和更新其 CORS 配置。

* `Origin` 标头不得通过 Dispatcher 传递到 AEM 发布：
   * 检查 `clientheaders.any` 文件。
* 相反，必须在 Dispatcher 级别为允许的源评估 CORS 请求。此方法还可确保在所有情况下，在一个位置正确设置 CORS 相关标头。
   * 应将此类配置添加到 `vhost` 文件。下面提供了一个示例配置；为简单起见，仅提供了 CORS 相关部分。您可以根据特定用例进行调整。

  ```xml
  <VirtualHost *:80>
     ServerName "publish"
  
     # ...
  
     <IfModule mod_headers.c>
         Header add X-Vhost "publish"
  
          ################## Start of the CORS specific configuration ##################
  
          SetEnvIfExpr "req_novary('Origin') == ''"  CORSType=none CORSProcessing=false
          SetEnvIfExpr "req_novary('Origin') != ''"  CORSType=cors CORSProcessing=true CORSTrusted=false
  
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') == '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=invalidpreflight CORSProcessing=false
          SetEnvIfExpr "req_novary('Access-Control-Request-Method') != '' && %{REQUEST_METHOD} == 'OPTIONS' && req_novary('Origin') != ''  " CORSType=preflight CORSProcessing=true CORSTrusted=false
          SetEnvIfExpr "req_novary('Origin') -strcmatch 'https://%{HTTP_HOST}*'"  CORSType=samedomain CORSProcessing=false
  
          # For requests that require CORS processing, check if the Origin can be trusted
          SetEnvIfExpr "%{HTTP_HOST} =~ /(.*)/ " ParsedHost=$1
  
          ################## Adapt the regex to match CORS origin for your environment
          SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*.your-domain.tld(:\d+)?$)#" CORSTrusted=true
  
          # Extract the Origin header 
          SetEnvIfNoCase ^Origin$ ^https://(.*)$ CORSTrustedOrigin=https://$1
  
          # Flush If already set
          Header unset Access-Control-Allow-Origin
          Header unset Access-Control-Allow-Credentials
  
          # Trusted
          Header always set Access-Control-Allow-Credentials "true" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Origin "%{CORSTrustedOrigin}e" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Methods "GET" "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Max-Age 1800 "expr=reqenv('CORSTrusted') == 'true'"
          Header always set Access-Control-Allow-Headers "Origin, Accept, X-Requested-With, Content-Type, Access-Control-Request-Method, Access-Control-Request-Headers" "expr=reqenv('CORSTrusted') == 'true'"
  
          # Non-CORS or Not Trusted
          Header unset Access-Control-Allow-Credentials "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Origin "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Allow-Methods "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
          Header unset Access-Control-Max-Age "expr=reqenv('CORSProcessing') == 'false' || reqenv('CORSTrusted') == 'false'"
  
          # Always vary on origin, even if its not there.
          Header merge Vary Origin
  
          # CORS - send 204 for CORS requests which are not trusted
          RewriteCond expr "reqenv('CORSProcessing') == 'true' && reqenv('CORSTrusted') == 'false'"
          RewriteRule "^(.*)" - [R=204,L]
  
          ################## End of the CORS specific configuration ##################
  
     </IfModule>
  
     <Directory />
  
         # ...
  
     </Directory>
  
     # ...
  
  </VirtualHost>
  ```
