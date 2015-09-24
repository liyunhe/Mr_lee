---
layout: post
title: "有关IOS生命周期简述"
description: "IOS基础"
tags: 
modified: 2015-9-24
image:
  feature:
---
# 应用生明周期
作为应用程序的代理对象 Appdelegate类在应用程序的不同阶段调用不同的代理方法。先来说说应用程序的5种状态
## Not Running (非运行状态) 
应用没有运行或者被系统终止
## Inactive (前台非活跃状态) 
应用正在前台运行但还没有接受事件处理
## Action (前台活跃状态)
应用进入前台，并且可以接受事件的处理
## Suspended（挂起状态）
挂起状态是一种冷冻状态，不能执行代码，如果系统内存不够就会被终止

### 在Appdelegate 中又相关的回调，每个回调都会确认APP当前的状态，可以测试看看！

# view生命周期于视图控制器的关系

我们已视图控制器的4种状态为基础，进而去看视图控制器。
视图的4种状态为: 

## 视图的创建

在视图已经被实例化并且已经加到内存中这个时候系统调用 viewDidLoad: 方法这个时候View还没有渲染成功，

## 视图可见 

通常是对视图的初始化进行处理。视图可见之前还要调用ViewWillAppear
该方法是视图将要渲染到屏幕，ViewDidAppear:该方法说明视图已经渲染完成，视图这时已经出现在屏幕上。

## 视图不可见 

视图不可见将调用ViewWillDisAppear方法，该方法只是告诉系统我将要移除该View,但还没有移除，ViewDidDisAppear:是将view彻底移除渲染层。

## 系统低内存

在低内存的情况下，一般会先调用ViewDidLoad方法，didReceiveMemoryWarning。

#IOS 开发 loadView 和 viewDidLoad 的区别

viewDidLoad 此方法只有当view从nib文件初始化的时候才被调用。

loadView 此方法在控制器的view为nil的时候被调用。 此方法用于以编程的方式创建view的时候用到。 如：

 
- ( void ) loadView {
    UIView *view = [ [ UIView alloc] initWithFrame:[ UIScreen
mainScreen] .applicationFrame] ;
    [ view setBackgroundColor:_color] ;
    self.view = view;
    [ view release] ;
}
 
你在控制器中实现了loadView方法，那么你可能会在应用运行的某个时候被内存管理控制调用。 如果设备内存不足的时候， view 控制器会收到didReceiveMemoryWarning的消息。 默认的实现是检查当前控制器的view是否在使用。如果它的view不在当前正在使用的view hierarchy里面，且你的控制器实现了loadView方法，那么这个view将被release, loadView方法将被再次调用来创建一个新的view。

 

--------------------------------------------------------------------------------------------------------------------------------------------

Don't read self.view in -loadView. Only set it, don't get it.

The self.view property accessor calls -loadView if the view isn't currently loaded. There's your infinite recursion.

The usual way to build the view programmatically in -loadView, as demonstrated in Apple's pre-Interface-Builder examples, is more like this:

UIView   * view  =   [[ UIView alloc ] init ...]; 
 ... 
 [ view addSubview : whatever ]; 
 [ view addSubview : whatever2 ]; 
 ... 
 self . view  = view ; 
 [ view release ]; 
  

<div xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/" about="http://subtlepatterns.com" class="notice">Background images from <span property="dct:title">Subtle Patterns</span> (<a rel="cc:attributionURL" property="cc:attributionName" href="http://subtlepatterns.com">Subtle Patterns</a>) / <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">CC BY-SA 3.0</a></div>


