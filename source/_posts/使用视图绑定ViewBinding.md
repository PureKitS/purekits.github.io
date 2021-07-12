---
title: Android视图绑定ViewBinding的使用
date:  2021-02-25 19:58:36
cover: https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/image-20210225200047263.png
tags: 
- Android
- Java
- viewBinding
- 编程
- 水博客
categories: Android

---







## 概述

> 在我们的开发过程中需要获取`XML`布局文件中的`ViewId`以便其赋值显示，所以我们习惯了使用`findViewById`进行操作
>
> 从`Android Studio 3.6 ` 开始，视图绑定能够通过生成绑定对象来替代 `findViewById`，从而可以帮您简化代码、移除 bug，并且从`findViewById`  的模版代码中解脱出来。

<!-- more -->

## 在`build.gradle`中开启视图绑定

> 开启视图绑定无需引入任何额外依赖，从`Android Studio 3.6`开始，视图绑定将会内建于`Anroid Gradle`插件中。需要打开视图绑定的话只需要在`build.gradle`文件中配置`viewBinding`选项

````groovy
// 需要 Android Gradle Plugin 3.6.0
android {
 viewBinding {
  enabled = true
 }
}
````

> 在`Android Studio 4.0`中，`viewBinding`变成属性被整合到了`buildFeatures`选项中所以配置要改正；

````groovy
// Android Studio 4.0
android {
 buildFeatures {
  viewBinding = true
 }
}
````

> 配置完成后，视图绑定就会为所有布局文件自动生成对应的绑定类。无需修改原有的`XML`布局文件，视图绑定将根据你现有的布局自动完成所有工作。
>
> 视图绑定将会根据现有的`XML`布局文件，为`Module`内所有的布局文件生成绑定对象。

## 在`Activity`中使用视图绑定

> 假设你有一个布局文件叫做`activity_main.xml`,开启视图绑定后就会自动生成相应的`ActivityMainBinding`绑定类

````java
package io.pure.myapplication;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import io.pure.myapplication.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {
    private ActivityMainBinding binding;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //通过调用生成的绑定类中包含的静态 inflate() 方法，创建该绑定类的实例以供 Activity使用
        binding = ActivityMainBinding.inflate(getLayoutInflater());
        //调用 getRoot() 方法获取对根视图的引用 将根视图传递到 setContentView() 使其成为屏幕上的活动视图
        setContentView(binding.getRoot());
        //获取控件ID并执行操作
        binding.textView01.setText("Hello World");
    }

}
````

![image-20210225200047263](https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/image-20210225200047263.png)