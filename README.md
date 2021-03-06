# Effective Objective-C 2.0 源码及相关注解

## 简介

本库 `fork` 自 [Effective Objective-C 2.0](https://item.jd.com/11402853.html) 一书的`代码仓库` https://github.com/effectiveobjc/code.

## 为什么

既然作者已经提供了含源码的仓库, 为何还要再 `fork` 并修改它? 

因为作者提供的源码是 `txt` 格式的, 没有语法高亮, 并且每个 `txt` 中可能包含多段关联不紧密的代码, 读起来较费劲. 本仓库将这些代码做了拆分, 放在独立的 `.h` 和 `.m` 中, 并在 `README` 中添加了一些相关注解, 以协助购买了正版书籍的小伙伴们阅读.

## 52个方法的简述

#### 第45条: 使用 dispatch_once 来执行只需要运行一次的线程安全代码

```objc
// `dispatch_once' singleton initialisation
+ (id)sharedInstance {
    static EOCClass *sharedInstance = nil;
    static dispatch_once_t onceToken;
    dispatch_once(&onceToken, ^{
        sharedInstance = [[self alloc] init];
    });
    return sharedInstance;
}
```

`dispatch_once` 函数的原型是: 


```c
void dispatch_once(dispatch_once_t *predicate, dispatch_block_t block);
```

其中, `dispatch_once_t` 是 `long` 的 `typedef` (它和 `dispatch_once` 搭配使用并且只能声明在 `static` 或 `global` 作用域里, 如果声明为其他作用域, 则其行为是未定义的):

```c
typedef long dispatch_once_t;
```

`dispatch_block_t` 是一个无参无返回值 `block` 的 `typedef`:

```objc
typedef void (^dispatch_block_t)(void);
```



