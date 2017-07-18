---
layout: post
title: "RVM 简明教程"
tagline: for the beginer
description: ""
category: tutorial
tags: [rvm, ruby]
prettify: true
---
{% include JB/setup %}

## 缘起

需要一个多 ruby 版本共存的环境；或出于系统安全管理需要无法分配给用户更高的权限，但用户却需要使用 ruby 环境。

## 目标

使用 `rvm` 命令行工具方便快捷的管理多个 Ruby 版本环境以及 gem 包。

## 计划

提供 `rvm` 命令的简单使用教程。

## 成员

[mcspring](https://twitter.com/mcspring)

## 定义

暂无

## 成果

### 1. 安装rvm

<pre class="prettyprint lang-bash">
$curl -L get.rvm.io | bash -s stable
$source ~/.bashrc &amp;&amp; source ~/.bash_profile
</pre>

>注意：安装 *rvm* 后推荐在 `.bash_profile` 中加入 `[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"` 命令，之后 `rvm` 命令便可以在shell中自动生效。

### 2. 使用rvm

**a) 列出所有可用的ruby版本**

<pre class="prettyprint lang-bash">
$rvm get stable
$rvm list known
</pre>

>注意：`rvm list known` 返回结果的所有 ruby 版本都可以通过以下 `rvm install verb` 方式进行安装，且无需系统管理员权限。

**b) 列出当前所有已安装的 ruby 版本**

<pre class="prettyprint lang-bash">
$rvm list
</pre>

**c) 安装某指定的 ruby 版本**

<pre class="prettyprint lang-bash">
$rvm install 2.0.0
</pre>

>注意：<br>
>1) `rvm install verb` 会将指定的ruby环境安装到用户的 `~/.rvm/rubies/verb` 路径下。<br>
>2) 如果 `rvm install verb` 出错，你可以运行 `rvm requirements` 查看并解决 *rvm* 的安装问题。

**d) 选择已安装的某的 ruby 版本**

<pre class="prettyprint lang-bash">
$rvm use 2.0.0
</pre>

>注意：你可以使用 `rvm use 2.0.0 --default` 命令同时将其设为系统默认版本。

**e) 卸载某指定的 ruby 版本**

<pre class="prettyprint lang-bash">
$rvm remove 2.0.0
</pre>

**f) 列出当前 ruby 环境下的 gemset**

<pre class="prettyprint lang-bash">
$rvm gemset list
</pre>

>注意：gemset 是限定在 ruby 版本下的，如你在 ruby 2.0.0 下创建的 *gemset-name*，当你切换到 ruby 1.9.3 下时就无法访问了。

**g) 创建 gemset**

<pre class="prettyprint lang-bash">
$rvm use 2.0.0
$rvm gemset create rails3
</pre>

**h) 切换 gemset**

<pre class="prettyprint lang-bash">
$rvm use 1.9.3
$rvm gemset use rails3
</pre>

>注意：<br/>
>1) 目标 *gemset-name* 在当前 ruby 环境下必须已经存在，否则你使用 `rvm gemset use gemset-name --create` 命令在 *gemset-name* 不存在时自动创建。<br/>
>2) 你可以在切换ruby环境时使用 `rvm use 1.9.3@rails3` 命令指定默认使用的 gemset。

**i) 清空指定的 gemset**

<pre class="prettyprint lang-bash">
$rvm use 1.9.3
$rvm gemset empty rails3
</pre>

>注意：你可以使用 `rvm gemset empty 1.9.3@rails3` 命令清空指定 ruby 环境下的某个 gemset。

**j) 删除指定的 gemset**

<pre class="prettyprint lang-bash">
$rvm use 1.9.3
$rvm gemset delete rails3
</pre>

**k) rvm 项目配置文件**

如果在项目根目录下创建 `.rvmrc` 文件，`rvm` 会在进入当前目录时自动执行其中的命令。如果当前项目使用 ruby 1.9.3 环境，并且使用名为 *rails32* 的 gemset，则可以创建如下脚本：

<pre class="prettyprint lang-ruby">
rvm install 1.9.3
rvm use 1.9.3
rvm gemset use rails32 --create
</pre>

>注意：最新版的 *rvm* 支持通用的 *ruby version* 格式配置文件，你可以通过 `rvm rvmrc create 2.0.0@rails3 --ruby-version` 指令自动创建项目配置文件。
