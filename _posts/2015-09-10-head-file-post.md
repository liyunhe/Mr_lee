---
layout: post
title: gitHub 编写高效率的IOS代码之在类的头文件中尽量少引用其他的头文件
description: "《编写高质量的ios代码52个有效发法》读书心得"
tags: [sample post]
image:
background: triangular.png
---
##在类的头文件中尽量少引用其他的头文件
与C和C++一样Objective-C也是使用头文件（header file）与实现文件（implementation file）来区隔代码其中代码如下：
{% highlight yaml %}
//OneClass.h
#import <Foundation/Foundation.h>
@interface OneClass : NSObject
@property(nonatomic,copy)NSString *str_one;
@property(nonatomic,copy)NSString *str_two;
@end
{% endhighlight %}

{% highlight yaml %}
//OneClass.m
#import "OneClass.h"

@implementation OneClass
@end
{% endhighlight %}
在Objective-C几乎任何类都需要引用`<Foundation/Foundation.h>`如果不引用这个框架的化，就要引用与其超类所对应得框架。例如`<UIViewController>`需要引用`<UIKit.h>`,OK,过一段时间你又创建了一个`<TwoClass>`然后你觉得每个类`<OneClass>`OneClass里有应该存在一个`<TwoClas>`一般都会为`<OneClass>`添加一条属性
{% highlight yaml %}
//OneClass.h
#import <Foundation/Foundation.h>
#import "TwoClass.h"
@interface OneClass : NSObject
@property(nonatomic,copy)NSString *str_one;
@property(nonatomic,copy)NSString *str_two;
@property(nonatomic,strong)TwoClass *two_obj;
@end
{% endhighlight %}
OK！！ 这样的确完成了我们的需求，但是存在一个问题：在编译一个使用`<OneClass>`文件时，我们不用知道`<TwoClass>`的全部细节，我们只要知道有以类名叫`<TwoClass>`存在就好了！SO！！有一个办法可以将这种情况告诉编译器：
{% highlight yaml %}
//OneClass.h

@class TwoClass; //向前声明该类

#import <Foundation/Foundation.h>
@interface OneClass : NSObject
@property(nonatomic,copy)NSString *str_one;
@property(nonatomic,copy)NSString *str_two;
@property(nonatomic,strong)TwoClass *two_obj;
@end
{% endhighlight %}
`<OneClass>`则要引用`<TwoClas>`的头文件，因为如果你想使用后者，就要必须知道他的所有详细的接口，于是实现问加就是:
{% highlight yaml %}
//OneClass.m

#import "OneClass.h"
#import "TwoClass.h"
@implementation OneClass
@end
{% endhighlight %}
	将引用头文件的时间尽量延后，只在确有需要的时候在引用，这样就可以减少类的使用者所需要因入头文件的数量，加入把`<TwoClas>`引入到`<OneClass>`的头文件中，那么没引用一次`<OneClass>`就相当与引用
`<TwoClas>`和`<OneClass>`2个文件，若这种情况持续下去，则要引用许多根本永不到的内容，会增加编译时间。
	向前声明也解决了2个类相互引用的问题。假如`<TwoClas>`添加新增和删除`<OneClass>`对象的方法。
{% highlight yaml %}

@interface TwoClass : NSObject
-(void)addObj:(OneClass *)add_obj;
-(void)removeObj:(OneClass *)add_obj;
@end
{% endhighlight %}
此时，若要编译`<OneClass>`，则编译器必须知道`<TwoClas>`这个类，而要编译器编译`<OneClass>`，则有知道`<TwoClas>`如果在各自的头文件引用对方的头文件，则会导致循环引用，如果使用`<import>`而非`<include>`不会导致死循环，如果使用`<include>`则会死循环，可以测试一下。如果`<TwoClas>`继承`<OneClass>`，这种情况是要在头文件中去声明。
##要点：
	##1.除非却又必要，否侧不要引入头文件，一般来说，应在某个类的头文件中使用向前声明来提起别的类，并在实现文件中引用引用那些头文件，这样做可以尽量降低类之间的耦合。
	##2.有时无法使用向前声明，比如要声明某个类遵循一项协议。这种情况下，尽量把该类遵循这个协议的申明转移到分类中进行，最后不行，就把协议单独放在一个头文件中，然后使用！
