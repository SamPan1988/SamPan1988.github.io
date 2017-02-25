---
layout: post
title: 用 Jekyll X GitPages 遇上的坑
description: "快速避免使用Jekyll建blog的坑"
modified: 2017-02-25T14:19:00
tags: [Tips, gitpage, jekyll]
image:
  feature: writtingBlog.jpg
---
### 因为便宜

本来是想用简书搭建博客的，但后来觉得这玩意显得不够码农，然后通过一通搜索发现有个叫Jekyll的工具很强大，就算你对网页一窍不通，也可以通过这玩意生成一个优美的静态网页，结合GitPage，你就可以有一个扩展方便，版式自定义，免费的博客。
最重要是免费，你懂的！！

### 没想到跟着说明走不通

不要误会，Jekyll真是个神器，只是我没想到跟着它的说明书走会出问题.
首先Jekyll是个ruby写的Gem工具，我使用的是macOS，自带ruby，所以在命令端里敲以下命令，就可以安装了
```bash
gem install jekyll bundler
```
然后报警了。。。
```bash
ERROR:  While executing gem ... (Errno::EACCES)
    Permission denied @ rb_sysopen - /usr/local/lib/ruby/gems/2.4.0/gems/jekyll-3.4.0/.rubocop.yml
```
虽然在Quick star guide 里没有任何提示，但官网的trouble shooting里还是很良心的记录怎么解决这个问题。

大家有时间可以看看<https://jekyllrb.com/docs/troubleshooting/#jekyll--mac-os-x-1011> 

简略的说，起因就是苹果在EI Captin版本后，引入了一个System Integrity Protection，所以系统自带的Ruby就没法改了。
所以，对于macOS，应该敲以下命令进行 jekyll 和 bundler的安装
```bash
sudo gem install jekyll bundler
```
然后请不要再看star guide的余下部分了，博主在这部分浪费了不小时间，因为默认主题是个gem theme，虽然gitpage里的指南很详细地说怎么换gem theme，但我真的没有成功过。

### 正确的姿势

1. 直接在github中搜索关键字 jekyll theme，然后你会发现有很多好心人已经做好了各种模板，免费，还特别漂亮！
2. clone 到你的电脑上，解压到你喜欢的位置
3. 打开Terminal，按以下敲命令
```bash
cd <the folder store the theme>
bundle install 
```
4. 提示 bundle 安装完成后，敲以下命令预览你的网站
```bash
jekyll s
```
5. 之后再用你喜欢的编辑器修改网站的相应部分，比如标题，简历之类，强烈建议你使用Atom，Vim，Emac,VSCode之类，而不是系统自带的编辑器，因为他们可以搜索整个文件夹，跟Git的整合也好。
6. 将整个文件夹推送回你GitPage的托管repository中，cheer！

