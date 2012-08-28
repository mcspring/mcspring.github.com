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

##缘起
需要一个多ruby版本共存的环境；或出于系统安全管理需要无法分配给用户更高的权限，但用户却需要使用ruby环境。

##目标
使用`rvm`命令行工具方便快捷的管理多个Ruby版本环境以及gem包。

##计划
提供`rvm`命令的简单使用教程。

##成员
[mcspring](https://twitter.com/mcspring)

##定义
暂无

##成果

###1. 安装rvm
<pre class="prettyprint lang-bash">
$curl -L get.rvm.io | bash -s stable
$source ~/.bashrc &amp;&amp; source ~/.bash_profile
</pre>
>注意：安装*rvm*后你可以在`.bash_profile`中加入`[[ -s "$HOME/.rvm/scripts/rvm" ]] && . "$HOME/.rvm/scripts/rvm"`命令，之后rvm命令便可以在所有shell中自动生效。

###2. 使用rvm
**a) 列出所有可用的ruby版本**
<pre class="prettyprint lang-bash">
$rvm list known
</pre>

>注意：`rvm list known`返回结果的所有ruby版本都可以通过以下`rvm install verb`方式进行安装，且无需系统管理员权限。

**b) 列出当前所有已安装的ruby版本**
<pre class="prettyprint lang-bash">
$rvm list
</pre>

**c) 安装某指定的ruby版本**
<pre class="prettyprint lang-bash">
$rvm install 1.9.3
</pre>

>注意：`rvm install verb`会将指定的ruby环境安装到用户的`~/.rvm/rubies/verb`路径下。

**d) 选择已安装的某的ruby版本**
<pre class="prettyprint lang-bash">
$rvm use 1.9.3
</pre>

>注意：你可以使用`rvm use 1.9.3 --default`命令同时将其设为系统默认版本。

**e) 卸载某指定的ruby版本**
<pre class="prettyprint lang-bash">
$rvm remove 1.9.3
</pre>

**f) 列出当前ruby环境下的gemset**
<pre class="prettyprint lang-bash">
$rvm gemset list
</pre>

>注意：gemset是限定在ruby版本下的，即你在ruby 1.9.3下创建的*gemset-name*，当你切换到ruby 1.8.7下时就无法访问了。

**g) 创建gemset**
<pre class="prettyprint lang-bash">
$rvm use 1.8.7
$rvm gemset create rails309
</pre>

**h) 切换gemset**
<pre class="prettyprint lang-bash">
$rvm use 1.8.7
$rvm gemset use rails309
</pre>

>注意：<br/>
>1) 目标*gemset-name*在当前ruby环境下必须已经存在，否则你使用`rvm gemset use gemset-name --create`命令在*gemset-name*不存在时自动创建。<br/>
>2) 你可以在切换ruby环境时使用`rvm use 1.8.7@rails309`命令指定默认使用的gemset。

**i) 清空指定的gemset**
<pre class="prettyprint lang-bash">
$rvm use 1.8.7
$rvm gemset empty rails309
</pre>

>注意：你可以使用`rvm gemset empty 1.8.7@rails309`命令清空指定ruby环境下的某个gemset。

**j) 删除指定的gemset**
<pre class="prettyprint lang-bash">
$rvm use 1.8.7
$rvm gemset delete rails309
</pre>

**k) rvm项目配置文件**

如果在项目根目录下创建`.rvmrc`文件，`rvm`会在进入当前目录时自动执行其中的命令。如果当前项目使用ruby 1.9.3环境，并且使用名为*rails32*的gemset，则可以创建如下脚本：

<pre class="prettyprint lang-ruby">
rvm install 1.9.3
rvm use 1.9.3
rvm gemset use rails32 --create
</pre>
