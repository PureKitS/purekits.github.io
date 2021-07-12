---
title: Android Studio && Android 开发笔记
date:  2021-02-25 15:00:36
tags: 
- Android
- Android Studio
- 笔记
categories: Android
---





一名沙雕大学生的Android学习笔记

<!-- more -->



## 第一章: 活动``Activity``

> 活动 ``Acitivity`` 是最吸引用户的地方，它是一种可以包含用户界面的组件，主要用于和用户交互

> > 创建活动布局 勾选``Generate Layout File``表示会自动为此 活动 创建一个对应的布局文件， 勾选``Launcher Acitivity``表示会自动为此活动设置为当前项目的主要活动

### 活动的基本用法

#### 创建和加载布局

> 创建布局文件时选择了``LinearLayout``作为根元素，因此布局文件中已经有一个``LinearLayout``元素了，现在我们对这个布局稍做编辑，添加一个按钮：

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button_1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button 1"/>

</LinearLayout>
````

> ``android:id``：是给当前元素定义一个唯一标识符，`@+id/id_name`用于在`XML`中定义一个`id` ， `@id`则是需要在`XML`中引用一个`id`.

> `android:layout_width`：指定了当前元素的宽度，这里使用了`match_parent`表示让当前元素和父元素一样宽此时父元素则是整个布局页面.

> `android:layout_height`：指定了当前元素的高度，这里使用了`wrap_content`表示当前元素的高度只要刚好包含里面的内容就行.

> `android:text`：指定了元素的中显示的文字内容.

#### 在`AndroidManifest`文件中注册

> 活动注册声明要放在`<application>`标签内，通过`<activity>`标签来对活动进行注册的

````xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="io.pure.firsttestacitivity">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.FirstTestAcitivity">
        <activity android:name=".FirstAcitivity"
            android:label="This is FirstAcitivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN">
                </action>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>

        </activity>
    </application>

</manifest>
````

> `<activity>`标签中我们使用`android:name`来指定具体注册那一个活动，由于最外层的的`<manifest>`标签中已经通过`package`属性指定了程序的包名是`io.pure.firsttestacitivity`因此注册活动时就可以省略前一部分，直接使用`.FirstActivity`.

> `<intent-filter>`标签里添加`<android:name="android.intent.action.MAIN"/> && <category android:name="android.intent.category.LAUNCHER"/>`用来声明程序主活动.



#### 在活动中使用`Toast`

> `Toast`是`Android`系统提供的一种非常好的提醒方式，在程序中可以使用它将一些短小的信息通知给用户，这些信息会在一段时间后自动消失，并且不会占用任何屏幕空间

````java
  @Override
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.first_test_layout);

      Button button1 = (Button) findViewById(R.id.button_1);
      	// 调用setOnClickListener() 方法为 button1 注册监听器
      button1.setOnClickListener(new View.OnClickListener(){

          @Override
          public void onClick(View v) {
              Toast.makeText(FirstAcitivity.this, "You clicked Button 1", Toast.LENGTH_SHORT).show();
          }
      });
    }
````

> 通过静态方法`makeText()`创建出一个`Toast`对象，然后调用`show()`将`Toast`显示出来，`makeText()`方法需要传入3个参数， 第一个参数是`Context`也就是`Toast`要求的上下文，第二个参数是`Toast`显示的文本内容：文本内容太也可以用通过`app/src/res/values/string.xml`文件内定义，使用`getResouces().getString(R.string.value)`获取到，第三个参数是`Toast`显示的时长，有两个内置常量可以选择`Toast.LENGTH_SHORT>默认显示2秒 && Toast.LENGTH_LONG>默认显示3.5秒`.



#### 在活动中使用`Menu`

> 首先在 `res`目录下面创建一个`menu`文件夹，接着在此文件夹下再新建一个名叫`main`菜单文件，右击`menu > New > Menu resouces fil > main.xml`.

````xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/add_item"
        android:title="Add"/>
    <item
        android:id="@+id/remove_item"
        android:title="Remove"/>

</menu>
````

> 这里我们创建了两个菜单项，其中`<item>`标签就是用来创建具体某一个菜单项，然后通过`android:id`给这个`<item>`指定一个唯一的标识符，通过`android:title`给`<item>`指定一个名称.



> 接着我们重新回到`FirstAcitivity`中来重写`onCreateOptionsMenu()`方法，重写方法可以使用`Ctrl + O`快捷键

````java
 //重写 onCreateOptionsMenu() 方法用于调用菜单资源文件 显示菜单
@Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
````

> 通过`getMenuInflater()`方法能够得到`MenuInflater`对象，再调用它的`Inflater()`方法就可以给当前活动创建才当了，`Inflater()`方法接收两个参数，第一个参数用于指定我们通过那一个资源文件来创建菜单，这里传入`R.menu.main`，第二个参数用于指定我们的菜单项将添加到哪一个`Menu`对象当中，这里直接使用`onCreateOptionsMenu()`方法传入的`menu`参数，然后给这个方法返回`true`, `true`用来表示允许创建的菜单显示出来，如果返回了`false`,创建的菜单将无法显示.

> 定义显示菜单响应事件， 在``FirstActivity`中重写`onOptionsItemSelected()`方法：

```java
 //重写 onOptionsItemSelected() 方法定义菜单响应事件
@Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {
        switch (item.getItemId()) {
            case R.id.add_item:
                Toast.makeText(this, "You clicked Add", Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(this, "You clicked Remove", Toast.LENGTH_LONG).show();
                break;
            default:
        }
        return true;
    }
```

> 在 `onOptionsItemSelected()`方法中，通过调用`item.getItemId()`来判断我们点击的是哪一个菜单项，然后给每个菜单项加入子的逻辑处理，这里我们弹出一个刚学的的`Toast`.



#### 销毁一个活动

> 通过点击`Back`键销毁当前活动，不过如果你不想通过按键的方式，而是希望使用代码的方式来销毁活动，`Acitivity`类提供了一个`finish()`方法，在活动中调用此方法就可以销毁活动.

````java
 button1.setOnClickListener(new View.OnClickListener() {

            @Override
            public void onClick(View v) {
                finish();
            }
        });
````

> 再次运行程序，这是点击一下按钮， 当前活动就被成功销毁了，效果同按下`Back`键.



### 使用`Intent`在活动之间穿梭

#### 使用显式`Intent`

> 创建活动，右击`app > New > Acitivity > Empty Acitivity`我们为此活动命名`SecondAcitivity`并且勾选`Generate Layout File`为此活动添加布局文件，但不要勾选`Launcher Acitivity`.

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SecondActivity">

    <Button
        android:id="@+id/button_2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Button 2"/>

</LinearLayout>
````

> 为生成的`activity_second.xml`布局文件替换成以上代码，同时还手动定义了一个按钮按钮显示为`Button 2`,  查看`AndroidManifest.xml`文件中是否注册`SecondAcitivity`活动，如果`Android Studio`没有自动完成，我们手动添加`<activity>`标签写入`<android:name />`属性.

> 由于`SecondAcitivity`不是主活动，因此不需要配置`<intent-filter>`标签。



> `Intent`是`Android`程序中各组件之间进行交互的一种重要方式，它不仅可以指明当前组件想要执行的动作，还可以在不同组件之间传递数据，`Intent`一般可被用于启动活动、启动服务以及发送广播等场景.

> `Intent`大致可以分为两种：显式`Intent`和隐式`Intent`，现在学习显式`Intent`如何使用.

> `Intent`有多个构造函数的重载，其中一个是`Intent(Context packageContext, Class<?>cls)`这个构造函数接收两个参数，其中第一个参数是`Context`要求提供一个启动活动的上下文，第二个参数`Class`则是指定想要启动的目标活动，通过这个构造函数就可以构建出`Intent`的“意图”， `Acitivity`类中提供了一个`startAcitivity()`方法用于启动活动，它接收一个`Intent`参数，这里我们将构建好的`Intent`传入`startAcitivity()`方法就可以启动目标活动了.

````java
  //为 button1 注册监听器
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(FirstAcitivity.this, SecondActivity.class);
                startActivity(intent);
            }
        });
````



#### 使用隐式`Intent`

> 相比于显式`Intent`，隐式`Intent`含蓄了许多，他不明确指出我们想要启动哪一个活动，而是制定了一系列更为抽象的`action && category`等信息然后交由系统去分析这个`Intent`并帮我们找出合适的活动去启动，
>
> 合适的活动：简单来说就是可以响应我们这个隐式`Intent`的活动，那么目前我们的`SecondAcitivity`可以响应什么养的隐式`Intent`呢？

> 通过在`<activity>  >  <intent-filter>`标签内配置的内容，可以指定当前活动能够相应的`action && categroy`打开`AndroidManifest.xml`添加如下代码：

````xml
  <activity android:name=".SecondActivity"
            android:label="This is SecondAcitvity">
            <intent-filter>
                <action android:name="io.pure.firsttestacitivity.ACTION_START"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
````



> 在`<action>`标签中我们指明了当前活动可以响应`io.pure.firsttestactivity.ACTION_START`这个`action`，而`<category>`标签中包含了一些附加信息，更加精确的指明了当前的活动能够响应的`Intent`中还可能带有的`category`，只有`<action> && <category>`中的内容同时能够匹配上`Intent`中指定的`action && <category>`时，这个活动才能响应`Intent`，修改`FirstTestActivity`中的按钮点击事件：

````java
  //为 button1 注册监听器
        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent("io.pure.firsttestacitivity.ACTION_START");
                startActivity(intent);
            }
        });
````

> 可以看到，我们使用了`Intent`的另一个构造函数，直接而将`action`的字符串传了进去，可以看见现在`Android Studio`中的`Intent`参数提示为`action`,表明我们想要启动能够响应`io.pure.firsttestacitivity.ACTION_START`这个`action`活动，前面说了需要`<action> && <category>`同时匹配才可以响应，为什么这里没有看见指定`category`，这是因为我们在`AndroidManifest.xml`中`<category>`标签中的`android.intent.category.DEFAULT`是一种默认的`category`在调用`startActivity()`方法时会自动将这个`category`添加到`Intent`中.
>
> 现在重新运行程序发现你使用隐式`Intent`已经成功了，在`<action> && <category>`中的内容已经生效了.



> 每个`Intent`中只能指定一个`action`但却能指定多个`category`这里我们指定了一个自定义的`category`值为`io.pure.fifsttestacitivity.MY_CATEGORY`，重新运行程序你会发现，程序崩溃了！`Android Studio` 中使用`Alt + 6`
>
> 打开`logcat`查看错误日志，

````
2020-12-27 20:08:52.801 25783-25783/io.pure.firsttestacitivity E/AndroidRuntime: FATAL EXCEPTION: main
    Process: io.pure.firsttestacitivity, PID: 25783
    android.content.ActivityNotFoundException: No Activity found to handle Intent { act=io.pure.firsttestacitivity.ACTION_START cat=[io.pure.firsttestactivity.MY_CATEGORY] }

````



> 错误信息提醒我们没有发现处理意图的活动即是没有任何一个活动可以响应我们的`Intent`，这是因为我们刚刚在`Intent`中新增了一个`category`,  而`AndroidManifest.xml > SecondActivity >  <intent-filter>`标签中并没有声明可以响应这个`category` 所以就出现了没有任何活动可以响应该`Intent`的情况，

````xml
 <activity android:name=".SecondActivity"
            android:label="This is SecondAcitvity">
            <intent-filter>
                <action android:name="io.pure.firsttestacitivity.ACTION_START"/>
                <category android:name="android.intent.category.DEFAULT"/>
                <category android:name="io.pure.firsttestactivity.MY_CATEGORY"/>
            </intent-filter>
        </activity>
````

> 我们向`<intent-filter>`中在添加一个`category`的声明，要保留默认声明哦！





#### 更多隐式`Intent`的用法

>使用隐式`Intent`我们不仅可以启动自己程序内的活动，还可以启动其他程序的活动，这使多个应用程序之间的功能共享成为了可能，比如说你的程序中要站是一个网页这是你没必要自己去实现一个浏览器，而是只需要调用系统的浏览器来打开这个网页就行了，修改`FirstTestAcitivity`中的按钮点击事件代码如下：

````java
  button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Intent.ACTION_VIEW);
                intent.setData(Uri.parse("https://baidu.com"));
                startActivity(intent);
            }
        });
````

> 首先指定了`Intent`的`action`是`Intent.ACTION_VIEW`，这是一个`Android`系统内置的动作，其常量值为`android.intent.action.VIEW`，然后通过`Url.parse()`这个方法将一个网址字符串解析成一个`Uri`对象，再调用`setData()`方法将这个`Uri`对象传递进去，
>
> 重新运行程序， 点击按钮就会可以看见打开了系统浏览器，方法其实并不复杂，他接收一个`Uri`对象，主要用于指定当前`Intent`正在操作的数据，而这些数据同城都是以字符串的形式传入到`Uri.parse()`方法中解析产生的.



> 于此对应我们还可以在`<intent-filter>`中在配置一个`<data>`标签，用于更精确的指定当前活动能够响应什么类型的数据，`<data>`标签中主要可以配置一下内容：

- `android:scheme` > 用于指定数据的协议部分，如上面的`http`部分.
- `android:host` > 用于指定数据的主机名部分，如上面的`baidu.com`部分.
- `android:port` > 用于指定数据的端口部分，一般紧随在主机名之后.
- `android:path` > 用于指定主机名和端口之后的部分，如一段网址跟在域名之后的内容地址.
- `android:mimeType` > 用于指定可以处理的数据类型，允许使用通配符的方式进行指定.

> 只有`<data>`标签中指定的内容和`Intent`中携带的`Data`完全一致时，当前活动才能够响应该`Intent`，不过一般的`<data>`标签中都不会指定太多内容，如上面例子中 其实只需要指定`android:scheme="http"`就可以响应所有的`http`协议的`Intent`了.



> 除了指定`http`协议外，我们还可以指定很多其他协议，比如`geo && tel`等，下面的代码展示了如何在我们的程序中调用系统拨号界面.

````java
   button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(Intent.ACTION_DIAL);
                intent.setData(Uri.parse("tel:5556"));
                startActivity(intent);
            }
        });
````





#### 向下一个活动传递数据

> `Intent`中提供了一系列`putExtra()`方法的重载，可以把我们想要的传递的数据暂存在`Intent`中，启动了另一个活动后，只需要把这些数据再从`Intent`中去取出就可以.

````java
 button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String data = "HelloWorld!";
                Intent intent = new Intent(FirstAcitivity.this, SecondActivity.class);
                intent.putExtra("extra_data", data);
                startActivity(intent);
            }
        });
````



> 这里还是使用显示`Intent`的方式启动`SecondAcitivity`，并通过`putExtra()`方法传递了一个字符串，`putExtra()`方法这里接收了两个参数，第一个参数是`key`，第二个是`value`，然后我们在`SecondAcitivity`中将传递的数据取出并打印出来：

````java
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        Intent intent = getIntent();
        String data = intent.getStringExtra("extra_data");
        Log.d("SecondAcitivity",  data);
    }
````

> 首先可以通过`getIntent()`方法获取到用于启动`SecondAcitivity`的`Intent`然后调用`getStringExtra()`方法传入对应的`key`就可以得到相应的数据了，这里由于我们传递的是字符串所以使用的`getStringExtra()`方法来获取传递的数据，如果传递的整形数据则使用`getIntExtra()`方法，如果传递的是布尔类型数据，则使用`getBooleanExtra()`方法，以此类推.

> 重新运行程序，打开`logcat`选择到`Debug`可以看见我们从`FirstAcitivity`中传递过来并打印的数据.





#### 返回数据给上一个活动

> 返回上一个活动只需要按一下`Back`键就可以，并没有一个用于启动活动`Intent`来传递数据，通过查阅文档你会发现，`Acitivity`中还有一个`startAcitivityForResult()`方法也适用于启动活动的但这个方法期望在活动销毁的时候能够返回一个结果给上一个活动，
>
> `startAcitivityForResult()`方法接收两个参数，第一个参数还是`Intent`，第二个参数是请求码`requestCode`，用于在之后回调中判断数据的来源，修改`FirstAcitivity`中按钮的点击事件：

````java
  button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String data = "HelloWorld!";
                Intent intent = new Intent(FirstAcitivity.this, SecondActivity.class);
                startActivityForResult(intent, 1);
            }
        });
````

> 这里我们使用了`startAcitivityForResult()`方法启动`SecondAcitivity`请求码只要是一个唯一值就可以了，这里传入了`1`，接下来我们在`SecondAcitivity`中给按钮注册事件：

````java
  btn2 = (Button) findViewById(R.id.button_2);
        btn2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
               Intent intent = new Intent();
               intent.putExtra("data_return", "HelloWorld!");
               setResult(RESULT_OK, intent);
               finish();
            }
        });
````

> 可以看见我们还是构建了一个`Intent`不过这个`Intent`仅仅是用于传递数据而已，他并没有指定意图，然后调用了`setResult()`方法用于向上一个活动返回数据的，`setResult()`方法接收两个参数，第一个参数用于向上一个活动返回处理结果，一般只使用`RESULT_OK  && RESULT_CANCELED`这两个值，第二个参数则是把带有数据的`Intent`传递回去，然后调用了`finish()`方法来销毁当前的活动



> 由于我们使用`startAcitivityForResult()`方法来启动`SecondAcitivity`，在`SecondAcitivity`被销毁之后会回调上一个活动的`onAcitivityResult()`方法因此我们需要在`FirstAcitivity`中重写这个方法来获取返回的数据，

````java
 @SuppressLint("MissingSuperCall")
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
       switch (requestCode){
           case 1:
               if (resultCode == RESULT_OK){
                   String returnedData = data.getStringExtra("data_return");
                   Log.d("FirstAcitivity", returnedData);
               }
               break;
           default:
       }
    }
````

> `onAcitivityResult()`带有三个参数，第一个参数是`requestCode`，第二个参数是`resultCode`，即是我们在启动活动传入的请求码，第二个参数即是我们在返回数据时传入的处理结果，第三个参数是`data`即是携带返回数据的`Intent`由于在一个活动中有可能调用`startAcitivityForResult()`方法来启动很多不同的活动每一个活动返回的数据都会回调到`onAcitivityResult()`方法中因此我们首先要做的就是通过检查`requestCode`来判断数据来源，确定数据是`SecondAcitivity`返回的我们在通过`resultCode`的值判断处理结果是否成功，最后从`data`中取值并打印出来.

> 重新运行程序，在`FirstAcitivity`界面点击按钮会打开`SecondAcitivity`然后在`SecondAcitivity`界面中点击按钮会回到`FirstAcitivity`，这时查看`logcat`的打印信息.



> 如果用户在`SecondAcitivity`中并不是通过点击按钮而是通过按下`Back`返回到`FirstAcitivity`这样数据不就没法返回了吗，我们可以通过在`SecondAcitivity`中重写`onBackPressed()`方法来解决问题：

````java
@Override
    public void onBackPressed() {
        Intent intent = new Intent();
        intent.putExtra("data_return", "HelloWorld!");
        setResult(RESULT_OK, intent);
        finish();
    }
````

> 当用户按下`Back`键，就回去执行`onBackPerssed()`方法中的代码.





### 活动的生命周期

> 活动的生命周期对任何`Android`开发者来说都非常重要，只有深入理解了活动的生命周期才可以写出更加连贯流畅地程序，

#### 返回栈

> 堆栈都已经很熟悉了，经过前面活动的学习，也发现了这一点，`Android`中的活动是可以层叠的，我们每启动一个新的活动，就会覆盖在原活动之上，然后点击`Back` 键会销毁最上面的活动，下面的一个活动就会重新显示出来，
>
> `Android`是使用任务`Task`来管理活动的，一个任务就是一组存放在栈里的活动的集合，这个栈也被称作返回栈`Back Stack`，栈是一种后进先出的数据结构，在默认情况下，每当我们启动了一个新的活动，他会在返回栈中入栈，并处于栈顶的位置，而每当我们按下`Back`键或调用`finish()`方法去销毁一个活动时，处于栈顶的活动会出栈，这时前一个入栈的活动就会重新处于栈顶的位置，系统总会显示处于栈顶的活动给用户，

![有关任务中的每个新 Activity 如何添加到返回堆栈的图示。当用户按**返回**按钮时，当前 Activity 会销毁，上一个 Activity 将恢复。](https://developer.android.com/images/fundamentals/diagram_backstack.png?hl=zh-cn)





#### 活动状态

> 每个活动在其生命周期中最多可能会有`4`种状态.



1. 运行状态

   > 当一个活动位于返回栈的栈顶时，这时活动就处于运行状态，系统最不愿意回收的就是处于运行状态的活动，因为这会带来非常差的用于体验.

2. 暂停状态

   > 当一个活动不在处于栈顶位置，但仍然可见时，这时活动就进入了暂停状态，处于暂停状态的活动是完全存活的，系统也不愿意去回收这种活动，因为太还是可见的活动，回收可见的东西都会在用户体验方面有不好的影响，只有在内存极低的情况下，系统才会考虑回收这种活动.

3. 停止状态

   > 当一个活动不再处于栈顶位置，并且完全不可见的时候，就进入了停止状态，系统仍然会给这种活动保存相应的状态和成员变量，但是这并不是完全可靠，如果其他地方需要内存，处于停止状态的活动就可能会被系统回收.

4. 销毁活动

   > 当一个活动从返回栈中移除后就变成了销毁状态，系统会最倾向于回收这种状态的活动，从而去保证手机内存充足.



#### 活动的生存期

> `Acitivity`类中定义了`7`回调方法，覆盖了活动生命周期的每一个环节：

+ > `onCreate()`： 这个方法你已经看到很多次了，每个活动中我们都重写了这个活动，他会在活动第一次被创建的时候调用，你应该在这个方法中完成活动的初始化操作，比如加载布局资源，绑定事件等.

+ > `onStart()`：这个方法在活动有不可见变为可见的时候调用.

+ > `onResume()`：这个方法在活动准备好和用户进行交互的时候调用，此时的活动一定位于返回栈的栈顶，并且处于运行状态.

+ > `onPause()`：这个方法在系统准备去启动给或者恢复另一个活动的时候调用，我们通常会再这个方法中将一些消耗`CPU`的资源释放掉，以及保存一些关键数据，但这个方法执行速度一定要快，不然会影响到新的栈顶活动的使用.

+ > `onStop()`：这个方法再活动完全不不可见的时候调用，他和`onPause()`方法的主要区别在于如果启动的新活动是一个对话框式的活动，那么`onPause()`方法会得到执行，而`onStop()`方法并不会执行.

+ > `onDestory()`：这个方法在活动被销毁之前调用，之后活动状态将变为销毁状态.

+ > `onRestart()`：这个方法再活动由停止状态变为运行状态之前调用，也就是活动被重新启动了

![Activity 生命周期的简化图示](https://developer.android.com/guide/components/images/activity_lifecycle.png?hl=zh-cn)

> 以上7个方法中除了`onRestart()`方法，其他方法都是两两相对的，从而又可以将活动分为3种生存期.

+ > 完整生存期：活动在`onCreate()`方法和`onDestory()`方法之间所经历的，就是完整生存期，一般情况下，一个活动会在`onCreate()`方法种完成各种初始化操作，而在`onDestory()`方法种完成释放内存的操作.

+ > 可见生存期：活动在`onStart()`方法和`onStop()`方法之间所经历的，就是可见生存期，在可见生存期内，活动对于用户总是可见的，即使有可能无法和用户进行交互4





## 第二章 UI开发点滴



### `TextView`

> 我们在布局文件中添加`TextView`控件，修改布局文件如下

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    
    <TextView
        android:id="@+id/text_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="This is TextView"/>

</LinearLayout>
````

`android:id`：给控件定义一个唯一标识符

`match_parent`：表示让当前控价大小和父布局大小一样

`fill_parent`：同`match_parent` 但是现在官方更推荐用`match_parent`

`wrap_content`：表示让当前控件的大小能够刚好包含住里面的内容







### 最常用也最难用的控件`ListView`

#### `ListView`的简单用法

> 首先创建一个`ListViewTest`项目，修改布局文件种根元素为`LinearLayout`手动添加`ListView`控件如下
>
> 设置宽高都为`match_parent`这样就占满了整个布局空间

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <ListView
        android:id="@+id/list_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</LinearLayout>
````

> 接下来修改`MainAcitivity`中的代码
>
> 我们使用了`ArrayAdapter`,它可以通过泛型来指定要适配的数据类型，然后在构造函数中把要适配的数据传入，`ArrayAdapter`有多个构造函数的重载，可以根据情况来选择最合适的，`ArrayAdapter`中依次传入上下文，`ListView`子项布局的`id`以及要适配的数据，这里我们使用了`android.R.layout.simple_list_view_1`作为`ListView`子项布局的`id`，这是一个`Android`内置的布局文件，里面只有一个`TextView`可用于简单的显示一段文本，
>
> 最后还需要调用`ListView`的`setAdapter()`方法将构建好的适配器对象传递进去，这样`ListView`和数据之间就建立起了关联

````java
public class MainActivity extends AppCompatActivity {
    private String[] data = {"Apple", "Banana", "Orange", "Mango", "Cherry",
            "Pear", "Mango","Apple", "Banana", "Orange", "Mango", "Cherry", "Pear"};

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                MainActivity.this, android.R.layout.simple_list_item_1, data);
        ListView listView = (ListView)findViewById(R.id.list_view);
        listView.setAdapter(adapter);
    }
}
````





#### 定制`ListView`的界面

>  定义一个实体类，作为`ListView`适配器的适配类型，新建类`Fruit`如下
>
> `Fruit`类中只有两个字段，`name`表示水果的名字，`imageId`表示水果对应图片的资源`id`

````java
public class Fruit {
    private String name;
    private int imageId;

    public Fruit(String name, int imageId) {
        this.name = name;
        this.imageId = imageId;
    }

    public String getName() {
        return name;
    }

    public int getImageId() {
        return imageId;
    }
}

````



> 新建`fruit_item.xml`文件，为`ListView`的子项绑定自定义布局
>
> 在这个布局中我们定义了一个`ImageView  & TextView`用于显示水果的图片和水果的名称，

````xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <ImageView
        android:id="@+id/fruit_image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <TextView
        android:id="@+id/fruit_name"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_vertical"
        android:layout_marginLeft="10dp" />

</LinearLayout>
````



> 创建一个自定义的适配器，这个适配器继承自 `ArrayAdapter`，并将泛型指定`Fruit`类，新建类`FruitAdapter`

````java
public class FruitAdapter extends ArrayAdapter<Fruit> {
    private int resourceId;

    public FruitAdapter(Context context, int textViewResourceId,
                        List<Fruit> objects) {
        super(context, textViewResourceId, objects);
        resourceId = textViewResourceId;

    }

    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = getItem(position); //获取当前项的Fruit实例
        View view = LayoutInflater.from(getContext()).inflate(resourceId, parent, false);
        ImageView fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
        TextView fruitName = (TextView) view.findViewById(R.id.fruit_name);
        fruitImage.setImageResource(fruit.getImageId());
        fruitName.setText(fruit.getName());
        return view;
    }
````

> 重写`getView()`方法，通过`getItem()`得到当前项的`Fruit`实例，然后使用`LayoutInflater`为子项加载我们传入的布局，这里`LayoutInflater`的`inflater()`方法接收`3`参数，这里就不多去阐述说明参数意义



> 接下来修改`MainAcitivity`中的代码为

````java
public class MainActivity extends AppCompatActivity {
    private List<Fruit> fruitList = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initFruits(); //初始化水果数据
        FruitAdapter adapter =
                new FruitAdapter(MainActivity.this, R.layout.fruit_item, fruitList);
        ListView listView = (ListView) findViewById(R.id.list_view);
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Fruit fruit = fruitList.get(position);
                Toast.makeText(MainActivity.this, fruit.getName(),Toast.LENGTH_SHORT).show();
            }
        });
    }


    private void initFruits() {
        //添加for循环使水果数据充满整个屏幕达到更好的测试效果
        for (int i = 0; i < 4; i++) {
            Fruit apple = new Fruit("Apple", R.drawable.apple);
            fruitList.add(apple);
            Fruit banana = new Fruit("Banana", R.drawable.banana);
            fruitList.add(banana);
            Fruit orange = new Fruit("Orange", R.drawable.orange);
            fruitList.add(orange);
            Fruit cherry = new Fruit("Cherry", R.drawable.cherry);
            fruitList.add(cherry);
            Fruit mango = new Fruit("Mango", R.drawable.mango);
            fruitList.add(mango);
            Fruit pear = new Fruit("Pear", R.drawable.pear);
            fruitList.add(pear);
        }
    }
}
````

> `initFruits()`初始化水果数据，在`Fruit`类中将水果的图片`id`和水果名字传入，我们还使用了`for`循环将所有水果数据添加了`4`遍这是因为如果只添加一遍的话，这点数据量不足以充满整个屏幕，







































































