# Git Toolkit

> 人类懒惰的本性和不满足的本性是驱使科技发展的源泉......

<!-- TOC -->

- [Git Toolkit](#git-toolkit)
  - [安装](#安装)
  - [git toolkit 介绍](#git-toolkit-介绍)
    - [自定义命令](#自定义命令)
      - [git toolkit](#git-toolkit)
      - [git ci](#git-ci)
      - [git clog](#git-clog)
    - [Hook 脚本](#hook-脚本)
      - [commit-msg](#commit-msg)
    - [配置](#配置)
      - [git config --global commit.template](#git-config---global-committemplate)
      - [git config --global core.hooksPath](#git-config---global-corehookspath)
  - [Q&A](#qa)
    - [linux 上提示缺失 zh_CN.UTF-8 的 LC 问题](#linux-上提示缺失-zh_cnutf-8-的-lc-问题)

<!-- /TOC -->

## 安装

**使用 curl**

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/highkay/git-toolkit/master/installer.sh)"
```

**使用 wget**

```bash
bash -c "$(wget https://raw.githubusercontent.com/highkay/git-toolkit/master/installer.sh -O -)"
```

## git toolkit 介绍

本工具集包含几个部分，自定义命令，Hook 脚本，以及配置模板

### 自定义命令

#### git toolkit

提供本工具集的管理命令。

**查看帮助**

```bash
git toolkit help
```

**卸载本工具集**

```bash
git toolkit uninstall
```

**更新本工具集**

```bash
git toolkit update
```

#### git ci

提供交互式`git commit`的命令，用于定制统一`commit message`。

> 用于替换[Commitizen](https://github.com/commitizen/cz-cli)

```bash
git ci

选择您正在提交的类型:
        1. Add: 新增一个项目 e.g. 功能, 测试, 依赖
        2. Drop: 移除一个项目 e.g. 功能, 测试, 依赖
        3. Fix: 修复一个问题 e.g. bug, 文本, 事故, 误报.
        4. Document: 只包含文档的变更, e.g. 帮助文件.
        5. Refactor: 只有重构的变更.
        6. Bump: 增加某项目的版本 e.g. a 依赖.
        7. Make: 变更构建流程，工具或者设施.
        8. Optimize: 只包含性能优化的变更, e.g. 提高代码运行速度.
        9. Reformat: 只有格式样式的变更, e.g. 变更空格.
        0. quit: 退出 ( Exit )
```

#### git clog

提供项目的`CHANGELOG`输出，支持输出到终端或指定文件中，可以使用`git clog -h`来查看帮助信息。

如果要使用该特性务必需要把 tag 写成`项目名称-tag`形式

```
git clog -o ./changelog.md -v "项目名称-tag"
```

输出的格式大致如下，符合`Markdown`语法([查看样例](changelog_new.md))：

```
# tag

#### [author](mailto:email) (commit_count)

* commit message (commit date) [commit_short_sha1](commit_url)
* commit message (commit date) [commit_short_sha1](commit_url)
```

显示效果如下：

![git-toolkit changelog](changelog.jpg)

### Hook 脚本

#### commit-msg

用于验证每次提交的`commit message`是否符合规范，如果不符合规范，则提交不成功

### 配置

#### git config --global commit.template

配置统一的`commit message`模板

参考`https://github.com/joelparkerhenderson/git_commit_message`进行一些裁剪

#### git config --global core.hooksPath

配置制定的 Hook 脚本的目录，使用本项目的 git hook 脚本

## Q&A

### linux 上提示缺失 zh_CN.UTF-8 的 LC 问题

```
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_COLLATE: cannot change locale (zh_CN.UTF-8): No such file or directory
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_CTYPE: cannot change locale (zh_CN.UTF-8): No such file or directory
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_MESSAGES: cannot change locale (zh_CN.UTF-8): No such file or directory
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_NUMERIC: cannot change locale (zh_CN.UTF-8): No such file or directory
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_TIME: cannot change locale (zh_CN.UTF-8): No such file or directory
/usr/local/bin/git-ci: line 6: warning: setlocale: LC_ALL: cannot change locale (zh_CN.UTF-8)
```

运行

```
sudo locale-gen "zh_CN.UTF-8"
```

生成对应的 Locale 即可
