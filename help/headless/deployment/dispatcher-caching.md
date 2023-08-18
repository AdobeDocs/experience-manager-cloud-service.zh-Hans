---
title: GraphQL持久查询 — 在Dispatcher中启用缓存
description: Dispatcher 是位于 Adobe Experience Manager 发布环境前的缓存和安全层。您可以在AEM Headless中为持久查询启用缓存。
feature: Dispatcher, GraphQL API
source-git-commit: 6f07089812e587834784aeda7e62d3e4614f45a1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 5%

---


# GraphQL持久查询 — 在Dispatcher中启用缓存 {#graphql-persisted-queries-enabling-caching-dispatcher}

>[!CAUTION]
>
>如果启用了Dispatcher中的缓存，则 [CORS过滤器](/help/headless/deployment/cross-origin-resource-sharing.md) 不需要，因此该部分可以忽略。

默认情况下，Dispatcher中未启用持久查询的缓存。 无法启用默认功能，因为使用具有多个源的CORS（跨源资源共享）的客户需要查看和更新其Dispatcher配置。

>[!NOTE]
>
>Dispatcher不缓存 `Vary` 标题。
>
>可以在Dispatcher中启用其他CORS相关标头的缓存，但是当有多个CORS源时，该功能可能不够。

## 启用持久查询的缓存 {#enable-caching-persisted-queries}

要启用持久查询的缓存，请定义Dispatcher变量 `CACHE_GRAPHQL_PERSISTED_QUERIES`：

1. 将变量添加到Dispatcher文件 `global.vars`：

   ```xml
   Define CACHE_GRAPHQL_PERSISTED_QUERIES
   ```

>[!NOTE]
>
>要符合 [Dispatcher对可缓存文档的要求](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/troubleshooting/dispatcher-faq.html#how-does-the-dispatcher-return-documents%3F)，Dispatcher添加后缀 `.json` 到所有持久查询URL，以便可以缓存结果。
>
>启用持久查询缓存后，此后缀将由重写规则添加。

## Dispatcher中的CORS配置 {#cors-configuration-in-dispatcher}

使用CORS请求的客户可能需要在Dispatcher中查看和更新其CORS配置。

* 此 `Origin` 不得通过Dispatcher将标头传递到AEM发布：
   * 查看 `clientheaders.any` 文件。
* 相反，必须在Dispatcher级别评估CORS请求是否为允许的源。 此方法还可以确保在所有情况下都在一个位置正确设置与CORS相关的标头。
   * 此类配置应添加到 `vhost` 文件。 下面给出了一个配置示例；为简单起见，仅提供了CORS相关部分。 您可以根据特定用例调整它。

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
