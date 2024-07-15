---
title: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
description: 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 7%

---

# 将 Dispatcher 配置从 AMS 迁移到 AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher与AEM as a Cloud Service之间的主要区别 {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM as a Cloud Service中的Apache和Dispatcher配置与AMS配置非常相似。 主要区别包括：

* 在AEM as a Cloud Service中，可能不使用某些Apache指令（例如，`Listen`或`LogLevel`）
* 在AEM as a Cloud Service中，只能将Dispatcher配置的某些部分放入包含文件中，它们的命名很重要。 例如，要跨不同主机重用的过滤器规则必须放入名为`filters/filters.any`的文件中。 有关更多信息，请参阅参考页面。
* 在AEM as a Cloud Service中有额外的验证，不允许使用`/glob`编写筛选规则以防止出现安全问题。 由于`deny *`已使用，而不是`allow *`（无法使用），因此客户可以从本地运行Dispatcher以及进行试错和查看日志以确切了解Dispatcher筛选器阻止了哪些路径以便添加这些路径中获益。
* 在AEM as a Cloud Service中，当前强烈建议[选择使用Dispatcher配置的灵活源模式](/help/implementing/dispatcher/disp-overview.md#validation-debug)，例如，使用Web层配置管道，或者在配置文件的数量和结构方面有更好的灵活性。

## 将Dispatcher配置从AMS迁移到AEM as a Cloud Service的准则

Dispatcher配置结构在Managed Services和AEM as a Cloud Service之间有所不同。 下面提供了有关如何从AMS Dispatcher配置版本2迁移到AEM as a Cloud Service的分步指南。

## 如何将AMS转换为AEM as a Cloud Service Dispatcher配置

以下部分提供了有关如何转换AMS配置的分步说明。 它假定
您有一个存档，其结构与[Cloud Manager Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述的结构相似

### 提取存档并删除最后的前缀

将存档提取到文件夹，并确保直接子文件夹以`conf`、`conf.d`、
`conf.dispatcher.d`和`conf.modules.d`。 如果没有，则将其在层次结构中向上移动。

### 删除未使用的子文件夹和文件

删除子文件夹`conf`和`conf.modules.d`，以及与`conf.d/*.conf`匹配的文件。

### 删除所有未发布的虚拟主机

删除`conf.d/enabled_vhosts`中包含`author`、`unhealthy`、`health`的任何虚拟主机文件
`lc`或`flush`的名称。 `conf.d/available_vhosts`中所有非虚拟主机文件
也可以删除关联的到。

### 移除或注释未引用端口 80 的虚拟主机部分

例如，如果您的虚拟主机文件中仍有部分内容专门引用端口80以外的端口：

```
<VirtualHost *:443>
...
</VirtualHost>
```

请删除或注释它们。 这些部分中的语句将不会得到处理，但如果
保留它们，您最终可能仍会编辑它们，并且不会有任何效果，这令人困惑。

### 检查重写

输入目录`conf.d/rewrites`。

移除任何名为`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的文件并记住
删除虚拟主机文件中引用它们的`Include`语句。

如果`conf.d/rewrites`现在包含单个文件，则应将其重命名为`rewrite.rules`，而不要将其重命名为
忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果该文件夹包含多个特定于虚拟主机的文件，则其内容应该为
已复制到虚拟主机文件中引用它们的`Include`语句中。

### 检查变量

输入目录`conf.d/variables`。

移除任何名为`ams_default.vars`的文件，并记得移除虚拟中的`Include`语句
托管引用这些文件的文件。

如果`conf.d/variables`现在包含单个文件，则应将其重命名为`custom.vars`，而不要将其重命名为
忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果该文件夹包含多个特定于虚拟主机的文件，则其内容应该为
已复制到虚拟主机文件中引用它们的`Include`语句中。

### 移除允许列表

移除文件夹`conf.d/whitelists`并移除虚拟主机文件中引用的`Include`语句
子文件夹中某个文件。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

将`PUBLISH_DOCROOT`重命名为`DOCROOT`
删除引用名为`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`的变量的节

### 通过运行验证器检查状态

使用`httpd`子命令在目录中运行Dispatcher验证器：

```
$ validator httpd .
```

如果看到与缺少包含文件有关的错误，请检查是否正确重命名了这些文件
文件。

如果看到未列入允许列表的Apache指令，请删除它们。

### 删除所有未发布的场

删除`conf.dispatcher.d/enabled_farms`中包含`author`、`unhealthy`、`health`的任何场文件
`lc`或`flush`的名称。 `conf.dispatcher.d/available_farms`中所有非服务器场文件
也可以删除关联的到。

### 重命名场文件

必须重命名`conf.dispatcher.d/enabled_farms`中的所有场以匹配模式`*.farm`，例如
名为`customerX_farm.any`的场文件应重命名为`customerX.farm`。

### 检查缓存

输入目录`conf.dispatcher.d/cache`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/cache`现在为空，请复制文件`conf.dispatcher.d/cache/rules.any`
从标准Dispatcher配置复制到此文件夹。 标准Dispatcher
可在此SDK的文件夹`src`中找到配置。 不要忘记修改
`$include`语句引用场文件中的`ams_*_cache.any`规则文件
也一样。

如果`conf.dispatcher.d/cache`现在包含后缀为`_cache.any`的单个文件，
应将其重命名为`rules.any`，并且不要忘记调整`$include`语句
也将在场文件中引用该文件。

但是，如果文件夹包含多个使用该模式且特定于场的文件，则其内容
应复制到场文件中引用它们的`$include`语句中。

移除任何后缀`_invalidate_allowed.any`的文件。

从默认位置复制文件`conf.dispatcher.d/cache/default_invalidate_any`
将云Dispatcher配置中的AEM引导至该位置。

在每个场文件中，移除`cache/allowedClients`部分中的所有内容并将其替换
替换为：

```
$include "../cache/default_invalidate.any"
```

### 检查客户端标头

输入目录`conf.dispatcher.d/clientheaders`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/clientheaders`现在包含后缀为`_clientheaders.any`的单个文件，
应将其重命名为`clientheaders.any`，并且不要忘记调整`$include`语句
也将在场文件中引用该文件。

但是，如果文件夹包含多个使用该模式且特定于场的文件，则其内容
应复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/clientheaders/default_clientheaders.any`
将AEM as a Cloud Service Dispatcher配置发送到该位置。

在每个场文件中，替换如下所示的所有clientheader include语句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

替换为语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查筛选器

输入目录`conf.dispatcher.d/filters`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/filters`现在包含单个文件，则应将其重命名为
`filters.any`并且不要忘记修改引用该内容的`$include`语句
场文件中的文件。

但是，如果文件夹包含多个使用该模式且特定于场的文件，则其内容
应复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/filters/default_filters.any`
将AEM as a Cloud Service Dispatcher配置发送到该位置。

在每个场文件中，将如下所示的所有filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查renders

输入目录`conf.dispatcher.d/renders`。

移除该文件夹中的所有文件。

从默认位置复制文件`conf.dispatcher.d/renders/default_renders.any`
将AEM as a Cloud Service Dispatcher配置发送到该位置。

在每个场文件中，移除`renders`部分中的所有内容并将其替换
替换为：

```
$include "../renders/default_renders.any"
```

### 检查虚拟主机

将目录`conf.dispatcher.d/vhosts`重命名为`conf.dispatcher.d/virtualhosts`并进入该目录。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/virtualhosts`现在包含单个文件，则应将其重命名为
`virtualhosts.any`并且不要忘记修改引用该内容的`$include`语句
场文件中的文件。

但是，如果文件夹包含多个使用该模式且特定于场的文件，则其内容
应复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/virtualhosts/default_virtualhosts.any`
将AEM as a Cloud Service Dispatcher配置发送到该位置。

在每个场文件中，将如下所示的所有filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

使用`dispatcher`子命令在目录中运行AEM as a Cloud Service Dispatcher验证器：

```
$ validator dispatcher .
```

如果看到与缺少包含文件有关的错误，请检查是否正确重命名了这些文件
文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

对于其他每个错误，请参见
验证器工具文档。

### 在本地部署中测试您的配置（需要安装Docker）

使用AEM as a Cloud Service Dispatcher Tools中的脚本`docker_run.sh`，您可以对其进行测试
您的配置不包含只在中显示的任何其他错误
部署：

### 步骤1：使用验证器生成部署信息

```
validator full -d out .
```

这将验证完整配置并在`out`中生成部署信息

### 步骤2：在Docker映像中使用该部署信息启动Dispatcher

在macOS计算机上运行AEM发布服务器，并监听端口4503时，
您可以在该服务器前面运行启动Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的Dispatcher配置

恭喜！如果验证器不再报告任何问题并且
docker容器启动时没有出现任何故障或警告，您可以
准备好将您的配置移动到`dispatcher/src`子目录
Git存储库的。

**使用AMS Dispatcher配置版本1的客户应联系客户支持，帮助他们从版本1迁移到版本2，以便遵循上述说明。**
