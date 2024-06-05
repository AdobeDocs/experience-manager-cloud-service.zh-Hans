---
title: 使用多个存储库
description: 了解如何在使用 Cloud Manager 时管理多个 Git 存储库。
exl-id: 1b9cca36-c2d7-4f9e-9733-3f1f4f8b2c7a
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 100%

---

# 使用多个存储库 {#working-with-multiple-source-git-repos}

了解如何在使用 Cloud Manager 时管理多个 Git 存储库。

## 同步客户管理的 Git 存储库 {#syncing-customer-managed-git-repositories}

[客户可以使用自己的一个或多个 Git 存储库](integrating-with-git.md)，而不是直接使用 Cloud Manager 的 Git 存储库。 在这些情况下，应设置自动同步过程以确保 Cloud Manager 的 Git 存储库始终保持最新。

根据在何处托管客户的 Git 存储库，可能使用了 GitHub 操作或 Jenkins 等持续集成解决方案设置自动化。有了自动化，每次推送到归客户所有的 Git 存储库都会自动转发到 Cloud Manager 的 Git 存储库。

虽然为单个归客户所有的 Git 存储库实施此类自动化并不复杂，但为多个存储库配置此类自动化还是需要进行初始设置。必须将多个 Git 存储库中的内容映射到单个 Cloud Manager Git 存储库中的不同目录。必须为 Cloud Manager 的 Git 存储库提供根 Maven `pom.xml`，并在 modules 部分中列出不同的子项目。

以下是两个归客户所有的 Git 存储库的示例 `pom.xml` 文件。

* 第一个项目放入名为 `project-a` 的目录中。
* 第二个项目放入名为 `project-b` 的目录中。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
  
    <groupId>customer.group.id</groupId>
    <artifactId>customer-reactor</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
  
    <modules>
        <module>project-a</module>
        <module>project-b</module>
    </modules>
  
</project>
```

此类根 `pom.xml` 将推送到 Cloud Manager 的 Git 存储库中的分支。 随后，必须设置这两个项目以自动将更改转发到 Cloud Manager 的 Git 存储库。

可能的解决方案如下。

1. GitHub 操作可以通过推送到项目 A 中的分支来触发。
1. 该操作检查项目 A 和 Cloud Manager Git 存储库，并将项目 A 中的所有内容都复制到 Cloud Manager 的 Git 存储库中的 `project-a` 目录。
1. 然后该操作提交（即推送）更改。

例如，将项目 A 中主分支的更改自动推送到 Cloud Manager 的 Git 存储库中的主分支。分支之间可能会存在映射，比如在推送到项目 A 中一个名为 `dev` 的分支将推送到 Cloud Manager 的 Git 存储库中一个名为 `development` 的分支。对于项目 B，需要执行类似的步骤。

根据分支策略和工作流，可以为不同的分支配置同步。 如果使用的 Git 存储库未提供类似于 GitHub 操作的概念，则也可以通过 Jenkins（或类似方法）进行集成。在此情况下，webhook 触发 Jenkins 作业，后者完成该工作。

执行以下这些步骤，以使您可添加新的（第三个）源或存储库。

1. 将 GitHub 操作添加到这个新的存储库，这样将更改从该存储库推送到 Cloud Manager 的 Git 存储库。
1. 至少执行一次该操作，确保项目代码位于 Cloud Manager 的 Git 存储库中。
1. 在 Cloud Manager Git 存储库的根 Maven `pom.xml` 中添加对新目录的引用。

## 示例 GitHub 操作 {#sample-github-action}

这是推送到主分支，然后推送到 Cloud Manager 的 Git 存储库的子目录中所触发的一个示例 GitHub 操作。必须为 GitHub 操作提供 `MAIN_USER` 和 `MAIN_PASSWORD` 这两个机密，这些操作才能连接并推送到 Cloud Manager 的 Git 存储库。

```java
name: SYNC
env:
  # Username/email used to commit to Cloud Manager's Git repository
  USER_NAME: <NAME>
  USER_EMAIL: <EMAIL>
  # Directory within the Cloud Manager Git repository
  PROJECT_DIR: project-a
  # Cloud Manager's Git repository
  MAIN_REPOSITORY: https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
  # The branch in Cloud Manager's Git repository to push to
  MAIN_BRANCH : <BRANCH_NAME>
 
# Only run on a push to this branch
on:
  push:
     branches: [ main ]
 
jobs:
  build:
    runs-on: ubuntu-latest
 
    steps:
      # Checkout this project into a sub folder
      - uses: actions/checkout@v2
        with:
          path: sub
      # Cleanup sub project
      - name: Clean project
        run: |
          git -C sub log --format="%an : %s" -n 1 > commit.txt
          rm -rf sub/.git
          rm -rf sub/.github
      # Set global git configuration
      - name: Set git config
        run: |
          git config --global credential.helper cache
          git config --global user.email ${USER_EMAIL}
          git config --global user.name ${USER_NAME}
      # Checkout the main project
      - name: Checkout main project
        run:
          git clone -b ${MAIN_BRANCH} ${MAIN_REPOSITORY} ${MAIN_BRANCH} 
      # Move sub project
      - name: Move project to main project
        run: |
          rm -rf ${MAIN_BRANCH}/${PROJECT_DIR} 
          mv sub ${MAIN_BRANCH}/${PROJECT_DIR}
      - name: Commit Changes
        run: |
          git -C ${MAIN_BRANCH} add -f ${PROJECT_DIR}
          git -C ${MAIN_BRANCH} commit -F ../commit.txt
          git -C ${MAIN_BRANCH} push
```

可灵活地使用 GitHub 操作。可以执行 Git 存储库的分支之间的任何映射，以及将单独的 Git 项目映射到主项目的目录布局中。

>[!NOTE]
>
>示例脚本使用 `git add` 更新存储库。 这种情况假设包括移除操作。 根据 Git 的默认配置，必须将此项替换为 `git add --all`。

## 示例 Jenkins 作业 {#sample-jenkins-job}

这是一个示例脚本，可用于 Jenkins 作业或类似作业，其流程如下：

1. 它由 Git 存储库中的更改触发。
1. Jenkins 作业将签出该项目或分支的最新状态。
1. 然后，作业将触发此脚本。
1. 此脚本依次签出 Cloud Manager 的 Git 存储库并将项目代码提交到子目录。

必须为 Jenkins 作业提供 `MAIN_USER` 和 `MAIN_PASSWORD` 这两个机密，这些作业才能连接并推送到 Cloud Manager 的 Git 存储库。

```java
# Username/email used to commit to Cloud Manager's Git repository
export USER_NAME=<NAME>
export USER_EMAIL=<EMAIL>
# Directory within the Cloud Manager Git repository
export PROJECT_DIR=project-a
# Cloud Manager's Git repository
export MAIN_REPOSITORY=https://$MAIN_USER:$MAIN_PASSWORD@git.cloudmanager.adobe.com/<PATH>
# The branch in Cloud Manager's Git repository to push to
export MAIN_BRANCH=<BRANCH_NAME>
 
# clean up and init
rm -rf target
mkdir target
 
# mv project to sub folder
mkdir target/sub
for f in .* *
do
    if [ "$f" != "." -a "$f" != ".." -a "$f" != "target" ]
    then
        mv "$f" target/sub
    fi
done
cd target
 
# capture log and remove git info
cd sub
git log --format="%an : %s" -n 1 > ../commit.txt
rm -rf .git
rm -rf .github
cd ..
 
# checkout main repository
git clone -b $MAIN_BRANCH $MAIN_REPOSITORY main
cd main
 
# configure main repository
git config credential.helper cache
git config user.email $USER_EMAIL
git config user.name $USER_NAME
 
# update project in main
rm -rf $PROJECT_DIR
mv ../sub $PROJECT_DIR
 
# commit changes to main
git add -f $PROJECT_DIR
git commit -F ../commit.txt
git push
```

可灵活地使用 Jenkins 作业。可以执行 Git 存储库的分支之间的任何映射，以及将单独的 Git 项目映射到主项目的目录布局中。

>[!NOTE]
>
>示例脚本使用 `git add` 更新存储库。 这种情况假设包括移除操作。 根据 Git 的默认配置，必须将此项替换为 `git add --all`。
