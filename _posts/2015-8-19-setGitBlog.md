---
layout: post
title: gitHub 设置自己的专属博客
description: "你要有一个与众不同的博客"
tags: [sample post]
image:
  background: triangular.png
---
如果想有自己的专属博客在这里 推荐你可以gitHubPages+jekyll 来生成，jekyll 理解成简单静态博客网站生成器.
我们要做一些准备工作(以mac平台为例)
# 1.检查一下mac有没有安装ruby(mac默认是安装的)
{% highlight yaml %}
$ruby -v
ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin14]
{% endhighlight %}
我的已经安装，如果没有安装请安装
# 2.安装 Homebrew(网上有好多例子)
安装完成后检查一下有没有安装成功
{% highlight yaml %}
$brew -v
Homebrew 0.9.5
{% endhighlight %}
这代表已经成功
# 3. 安装 jekyll
{% highlight yaml %}
$brew install jekyll
Homebrew 0.9.5
{% endhighlight %}
# 4你需要有一个GitHub账号，并在上面申创建一个repositories 名字叫TestDomo
# 5在本地创建文件并且与远程仓库关联
具体操作
***
 打开终端
1. cd 到桌面（个人喜好  放在那都可以）
{% highlight yaml %}
$mkdir TestDomo
$cd TestDomo
$git init 
$ git checkout --orphan gh-pages
$ git remote add origin https://github.com/username/TestDomo.git
{% endhighlight %}
***
# 6在TestDomo文件夹下创几个文件夹 分别是这里请参考[阮一峰大神的博客](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
# 将自己的搞好的代码提交到gitHub
{% highlight yaml %}
$ git add .
$ git commit -m "first"
$ git remote add origin https://github.com/username/TestDomo.git
$ git push origin gh-pages
{% endhighlight %}
# 最后登陆gitHub 在seting可以看到自己的博客！！

<div xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/" about="http://subtlepatterns.com" class="notice">Background images from <span property="dct:title">Subtle Patterns</span> (<a rel="cc:attributionURL" property="cc:attributionName" href="http://subtlepatterns.com">Subtle Patterns</a>) / <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">CC BY-SA 3.0</a></div>