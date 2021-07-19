---
title: 将Dispatcher配置从AMS迁移到AEM as aCloud Service
description: '将Dispatcher配置从AMS迁移到AEM as aCloud Service '
feature: Dispatcher
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 14%

---

# 将Dispatcher配置从AMS迁移到AEM as aCloud Service {#Dispatcher-in-the-cloud}

## AMS Dispatcher与AEM as a Target的主要区别Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

AEM as aCloud Service中的Apache和Dispatcher配置与AMS配置非常相似。 主要区别包括：

* 在AEM as aCloud Service中，不能使用某些Apache指令（例如`Listen`或`LogLevel`）
* 在AEM as a Cloud Service中，只能将部分Dispatcher配置放入包含文件中，其命名很重要。 例如，要在不同主机之间重复使用的过滤器规则必须放入名为`filters/filters.any`的文件中。 有关更多信息，请参阅参考页面。
* 在AEM as aCloud Service中，有额外的验证来禁止使用`/glob`编写的过滤器规则，以防止出现安全问题。 由于将使用`deny *`而不是`allow *`（不能使用），因此客户将从在本地运行Dispatcher以及执行试用和错误中受益，查看日志可准确了解Dispatcher过滤器为了添加这些过滤器而阻止的路径。

## 将调度程序配置从AMS迁移到AEM as aCloud Service的准则

Dispatcher配置结构在Managed Services与AEM as a Dispatcher之间存在差异。 下面提供了关于如何从AMS Dispatcher配置版本2迁移到AEM as aCloud Service的分步指南。

## 如何将AMS转换为AEM as a Cloud Service Dispatcher配置

以下部分提供了有关如何转换AMS配置的分步说明。 它假定
具有与[Cloud Manager Dispatcher配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)中所述结构类似的存档

### 提取存档并删除最后的前缀

将存档解压缩到文件夹中，并确保子文件夹的直接开头为`conf`、`conf.d`、
`conf.dispatcher.d`和`conf.modules.d`。 如果没有，请在层级中向上移动。

### 删除未使用的子文件夹和文件

删除子文件夹`conf`和`conf.modules.d`，以及与`conf.d/*.conf`匹配的文件。

### 删除所有未发布的虚拟主机

删除`conf.d/enabled_vhosts`中具有`author`、`unhealthy`、`health`的所有虚拟主机文件，
`lc`或`flush`。 `conf.d/available_vhosts`中所有非虚拟主机文件
也可以删除链接到的。

### 移除或注释未引用端口 80 的虚拟主机部分

如果虚拟主机文件中仍有部分内容专门引用端口80以外的其他端口，例如：

```
<VirtualHost *:443>
...
</VirtualHost>
```

，
则请移除或注释该部分。这些部分中的语句将不会得到处理，但是如果保留它们，您可能最终仍会对其进行编辑，并且不会有任何效果，这可能会造成混淆。

### 检查 rewrites

进入目录`conf.d/rewrites`。

移除任何名为`base_rewrite.rules`和`xforwarded_forcessl_rewrite.rules`的文件，并记住
删除虚拟主机文件中引用`Include`语句。

如果`conf.d/rewrites`现在包含单个文件，则应将其重命名为`rewrite.rules`，但不应
也请忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用`Include`语句的。

### 检查 variables

进入目录`conf.d/variables`。

移除任何名为`ams_default.vars`的文件，并记住移除虚拟中的`Include`语句
主机文件。

如果`conf.d/variables`现在包含单个文件，则应将其重命名为`custom.vars`，但不应
也请忘记修改虚拟主机文件中引用该文件的`Include`语句。

但是，如果文件夹包含多个特定于虚拟主机的文件，则其内容应为
复制到虚拟主机文件中引用`Include`语句的。

### 删除允许列表

删除文件夹`conf.d/whitelists`，并删除虚拟主机文件中引用的`Include`语句
子文件夹中的一些文件。

### 替换任何不再可用的变量

在所有虚拟主机文件中：

将`PUBLISH_DOCROOT`重命名为`DOCROOT`
删除引用名为`DISP_ID`、`PUBLISH_FORCE_SSL`或`PUBLISH_WHITELIST_ENABLED`的变量的部分

### 通过运行验证器检查状态

使用`httpd`子命令在目录中运行Dispatcher验证器：

```
$ validator httpd .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到未的Apache指列入允许列表令，请删除它们。

### 删除所有未发布的场

删除`conf.dispatcher.d/enabled_farms`中具有`author`、`unhealthy`、`health`、
`lc`或`flush`。 `conf.dispatcher.d/available_farms`中所有非
也可以删除链接到的。

### 重命名场文件

必须重命名`conf.d/enabled_farms`中的所有场以匹配模式`*.farm`，例如
名为`customerX_farm.any`的场文件应重命名为`customerX.farm`。

### 检查 cache

进入目录`conf.dispatcher.d/cache`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/cache`现在为空，请复制文件`conf.dispatcher.d/cache/rules.any`
从标准Dispatcher配置到此文件夹。 标准Dispatcher
可在此SDK的文件夹`src`中找到配置。 不要忘记调整
引用场文件中`ams_*_cache.any`规则文件的`$include`语句
也是。

相反，如果`conf.dispatcher.d/cache`现在包含一个后缀为`_cache.any`的文件，
它应重命名为`rules.any`，并且不要忘记修改`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

移除所有后缀为`_invalidate_allowed.any`的文件。

从默认位置复制文件`conf.dispatcher.d/cache/default_invalidate_any`
AEM中的。

在每个场文件中，删除`cache/allowedClients`部分中的所有内容并将其替换
与：

```
$include "../cache/default_invalidate.any"
```

### 检查 client headers

进入目录`conf.dispatcher.d/clientheaders`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/clientheaders`现在包含一个后缀为`_clientheaders.any`的文件，
它应重命名为`clientheaders.any`，并且不要忘记修改`$include`语句
在场文件中也引用该文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/clientheaders/default_clientheaders.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何clientheader include语句：

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

替换为语句：

```
$include "../clientheaders/default_clientheaders.any"
```

### 检查 filter

进入目录`conf.dispatcher.d/filters`。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/filters`现在包含单个文件，则应将其重命名为
`filters.any`，并且不要忘记修改引用该变量的`$include`语句
文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/filters/default_filters.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

替换为语句：

```
$include "../filters/default_filters.any"
```

### 检查 renders

进入目录`conf.dispatcher.d/renders`。

移除该文件夹中的所有文件。

从默认位置复制文件`conf.dispatcher.d/renders/default_renders.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，删除`renders`部分中的所有内容并将其替换
与：

```
$include "../renders/default_renders.any"
```

### 检查 virtualhosts

将目录`conf.dispatcher.d/vhosts`重命名为`conf.dispatcher.d/virtualhosts`并输入。

移除所有前缀为 `ams_` 的文件。

如果`conf.dispatcher.d/virtualhosts`现在包含单个文件，则应将其重命名为
`virtualhosts.any`，并且不要忘记修改引用该变量的`$include`语句
文件。

但是，如果文件夹包含多个具有该模式且特定于场的文件，则其内容为
应该复制到场文件中引用它们的`$include`语句中。

从默认位置复制文件`conf.dispatcher/virtualhosts/default_virtualhosts.any`
AEM作为该位置的Cloud ServiceDispatcher配置。

在每个场文件中，将如下所示的任何filter include语句：

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

替换为语句：

```
$include "../virtualhosts/default_virtualhosts.any"
```

### 通过运行验证器检查状态

使用`dispatcher`子命令在目录中将AEM作为Cloud ServiceDispatcher验证器运行：

```
$ validator dispatcher .
```

如果看到有关缺少包含文件的错误，请检查是否正确重命名了这些文件。

如果看到有关未定义变量 `PUBLISH_DOCROOT` 的错误，请将该变量重命名为 `DOCROOT`。

有关其他每个错误，请参阅验证器工具文档的“疑难解答”部分。

### 在本地部署中测试您的配置（需要安装Docker）

使用AEM中的脚本`docker_run.sh`作为Cloud Service调度程序工具，您可以测试
您的配置不包含只会在
部署：

### 步骤1:使用验证器生成部署信息

```
validator full -d out .
```


这将验证完整配置并在 中生成部署信息`out`

### 步骤2:使用该部署信息在Docker映像中启动Dispatcher

当您的AEM发布服务器在macOS计算机上运行，监听端口4503时，
您可以在该服务器前面运行启动Dispatcher，如下所示：

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

这将启动容器并在本地端口 8080 上公开 Apache。

### 使用新的Dispatcher配置

恭喜！ 如果验证器不再报告任何问题，并且
docker容器启动时没有出现任何故障或警告，您
已准备好将配置移动到`dispatcher/src`子目录
的URL。

**使用AMS Dispatcher配置版本1的客户应联系客户支持，以帮助他们从版本1迁移到版本2，以便按照上述说明操作。**
