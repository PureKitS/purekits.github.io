---
title: 开始学习Laravel
date:  2021-07-11 15:00:36
tags: 
- PHP
- Laravel
- Cmposer
categories: Laravel
---



## 前言

> Laravel是 Taylor Otwell 开发的一款基于 PHP 语言的 Web 开源框架，旨在实现的Web软件的MVC架构。让你可以通过简单、优雅的表达式语法开发出很棒的Web应用，Laravel同时拥有更富有表现力的语法、高质量的文档、丰富的扩展包，可以让你从杂乱的代码中解脱出来。

<!-- more -->

## 安装

### 安装composer

> Laravel 使用 [Composer](https://getcomposer.org/) 来管理项目依赖。因此，在使用 Laravel 之前，请确保您的机器上已经安装了 Composer。

### 通过composer全局安装laravel

````
composer global require laravel/installer
````

### 使用laravel new blog（you project name)

> Laravel 使用 [Composer](https://getcomposer.org/) 来管理项目依赖。因此，在使用 Laravel 之前，请确保您的机器上已经安装了 Composer。

````
laravel new blog(you project name)
````

### 使用PHP内置服务器提供服务

> 如果你在本地安装了 PHP，并且你想使用 PHP 内置的服务器来为你的应用程序提供服务，则可以使用 Artisan 命令 serve。该命令会在 http://localhost:8000 上启动开发服务器：

````
php artisan serve
````



## 配置数据库

### 修改数据库的连接配置文件

> 数据库的连接配置文件位于 `config/database.php`，和很多其他 Laravel 配置一样，你可以为数据库配置多个「连接」，然后决定将哪个「连接」作为默认连接。

````php

    /*
    |--------------------------------------------------------------------------
    | Default Database Connection Name
    |--------------------------------------------------------------------------
    |
    | Here you may specify which of the database connections below you wish
    | to use as your default connection for all database work. Of course
    | you may use many connections at once using the Database library.
    |
    */

    'default' => env('DB_CONNECTION', 'mysql'),

````



### 修改 `.env`文件内的变量

> 当然，默认数据库连接、数据库名称以及数据库用户名和密码等敏感信息都保存到 `.env` 文件中了，然后通过 `env` 辅助函数读取：

````
DB_CONNECTION=mysql 	//laravel默认使用mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_demo //数据库
DB_USERNAME=root	//mysql用户名
DB_PASSWORD=rootme	//mysql密码
````



### 运行命令迁移数据库

> 修改好`.env`配置文件的变量,需要在MySQL中创建一个`laravel_demo`的数据库,然后运行数据库迁移命令行执行数据库迁移

````php
php artisan migrate 
````

 



## 快速入门安装基本入门套件

### Laravel Breeze

> Laravel Breeze 是一个最小化的 Laravel 认证功能完整实现扩展包，包含了登录、注册、密码重置、邮箱验证和密码确认等功能。Laravel Breeze 的视图层通过 Blade 模板 + Tailwind CSS 实现。Breeze 为构建一个全新的 Laravel 应用提供了一个良好的起点。

> 首先需要创建一个新的`laravel`应用,并且配置好数据库,然后运行数据库迁移;

````
laravel new blog

cd blog

配置数据库配置文件，运行命令行进行迁移
php artisan migrate
````



> 创建好新的laravel应用后，你可以通过Composer来安装Laravel breeze：

````
composer require laravel/breeze --dev
````



> 安装好 Laravel Breeze 扩展包后，可以运行 `breeze:install` Artisan 命令，这个命令会发布认证视图、路由和控制器等资源到项目目录，这样一来，你可以可以完全接管这些认证代码的功能实现和自定义了。此外，还需要编译前端资源让 JavaScript 和 CSS 代码生效：

````
php artisan breeze:install //发布认证视图、路由和控制器等资源到项目目录；

npm install && npm run dev //编译前端资源让JavaScript 和 css 代码生效
````

> 接下来，你就可以在浏览器中访问 `/login` 和 `/register` URL 了，所有的 Breeze 路由都定义在 `routes/auth.php` 文件中。





## `laravel`路由入门

> 对任何一个 Web 应用框架而言，通过 HTTP 协议处理用户请求并返回响应都是核心必备功能，也就是说，对于我们学习和使用一个 Web 框架，第一件要做的事情就是定义应用路由，否则，将无法与终端用户进行交互。而我们的 Laravel 从入门到精通系列教程之旅也将从路由开始，在这篇真正意义上的开篇教程中，我们将学习如何定义路由，然后将其指向要执行的代码，并处理各种路由;需求。



### 路由入门

> 在创建的laravel应用中，定义路由有两个入口，一个是`routes/web.php`,用于处理终端用户通`Web`浏览器直接访问的请求，另一个是`routes/api.php`,用于处理其他接入方的`API`请求；



> 定义路由最简单的方式就是在`routes/web.php`中定义一个路径以及一个映射到该路径的闭包函数：

````php
//routes/web.php
Route::get('/', function(){
	return 'Hello, World!';
});
````

> 运行`php artisan serve`访问应用首页时，就可以看到页面显示`Hello，World！`这一行字符串。
>
> 这就是一个简单的`laravel`路由定义，但是涵盖了一个`Web`框架的基本功能：处理请求，返回响应；



> 使用`match`和`any`实现相应多个或所有`HTTP`请求的路由；

````
Route::match(['post', 'get'], 'match', function(){
	echo 'match';
});

Route::any('any', function(){
	echo 'any';
});
````





## 控制器`Controller`

### 控制器的基本构造

> 命名空间
>
> 引入命名空间
>
> 类名 继承基类





> 使用命令在应用的`app/Http/Controllers`目录下创建一个`UserController`控制器

````
//使用命令创建 名为 UserController的控制器
php artisan make:controller UserController 
````

> 使用路由调用控制器方法

````php
//Route::请求方法（'请求的url地址'，[控制器::class, '引用的控制器方法']);

//在 UserController 控制器中编写 Test 类
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    public function Test(){
        return phpinfo();
    }
}

//路由引用控制器内的方法
//Route::请求方法（'请求的url地址'，[控制器::class, '引用的控制器方法']);

//调用控制器方法 UserController
Route::get('Controller', [UserController::class, 'Test']);


````



## 视图，数据库操作



### 简单的数据库操作

> 在应用中新建的`UserController`控制器中编写insert类

````php
    public function insert(){
        return DB::table("users")
        ->insert([
        'name' => 'haohongxin',
        'email' => 'purekit.ahcme@outlook.com',
        'password' => 'hhxrootme'
        ]);
    }
````

 

> 编写路由调用insert类

```php

//调用insert方法  crud
Route::get('insert', [UserController::class, 'insert']);

```



> 在应用中新建的`UserController`控制器中编写增删改查 功能类

````php
class UserController extends Controller
{
    //添加数据
    public function insert(){
        return DB::table("users")
        ->insert([
        'name' => '郝宏鑫 ',
        'email' => 'purekit.ahcme@gmail.com',
        'password' => 'hhxrootme'
        ]);
    }


    //修改数据
    public function update(){
        return DB::table("users")
        ->where('id', '1')
        ->update(['name' => 'purekits']);
    }


    //查询数据
    public function select(){
       $customer = DB::table('customer')
       ->get();
       dd($customer);
    }


    //删除数据
    public function delete(){
        return DB::table('users')
        ->where('id','2')
        ->delete();
    }

}
````



> 在`web.php`路由表中引用控制器的功能类

````php
//创建路由组 整理 增删改查
Route::prefix('db')->group(function(){

    //添加数据
    Route::get('insert', [UserController::class, 'insert']);

    //修改数据
    Route::get('update', [UserController::class, "update"]);

    //查询数据
    Route::get('select', [UserController::class, 'select']);

    //删除数据
    Route::get('delete', [UserController::class, 'delete']);
});
````











