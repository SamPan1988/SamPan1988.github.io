---
layout: post
title: "环信EMSDK_Not_Found报警最快解决姿势"
description: "快速集成环信时出现的报错"
tags: [Tips, 环信, 编译错误]
image:
  feature: killerInRed.jpg
---

### 不废话，直接上正确姿势

环信官方提供库CocoaPod导入环信的方式，请在Podfile里加入下边两行
```bash
pod 'Hyphenate'

pod 'EaseUI', :git => 'https://github.com/easemob/easeui-ios-hyphenate-cocoapods.git'
```

一编译，就报警！！ 呃，缺少依赖了。一通百度Google之后，网上都会跟你不停重复说用PCH文件导入这个头文件就可以了
![EMSDKNotFound](https://github.com/SamPan1988/imageStore/raw/master/环信报警jpg.jpg)

但我发现更快的方法，既然是缺少依赖了，直接让EaseUI依赖Hyphenate不就好了？
点击侧栏上Pod的project文件，点击target，Genral-》Linked framework and libarary栏下，按+号添加Hyphenate.framework(在pod文件夹里找找就好，不在列表上的)
![AddFramework](https://github.com/SamPan1988/imageStore/raw/master/addFrameworkJPG.jpg)

编译一下，是不是没事了？

### 下面的您可以不看

英明神武的同学应该会注意到编译后会有个运行时的输出，长下面这样
![DuplicateClass](https://github.com/SamPan1988/imageStore/raw/master/duplicateJPG.jpg)

看报警信息是说，有一个类在两个私有库中重复实现了，OC是没有name space，或者应该说是flat name space，当一个类在runtime里注册了两次就会出现这个问题。

stackoverflow 里有个答案说得很好很详细
[Duplicate class in mutiple target](http://stackoverflow.com/questions/6149673/class-foo-is-implemented-in-both-myapp-and-myapptestcase-one-of-the-two-will-be)

不过这里原因跟用户无关，是苹果的锅，很多人反映在升级到Xcode8后就出现类似的信息，而图中提示的两个私有库都是iOS runtime环境的私有库，不过苹果员工拍胸口保证应该可以忽略，暂时就信了吧

[苹果员工拍胸口现场](https://forums.developer.apple.com/thread/63254)







