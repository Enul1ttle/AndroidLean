# Android
#### Intent是什么？
- Android中提供了Intent机制来协助应用间的交互与通讯，或者采用更准确的说法是，Intent不仅可用于应用程序之间，也可用于应用程序内部的activity, service和broadcast receiver之间的交互。
- Intent是一种运行时绑定（runtime binding)机制，它能在程序运行的过程中连接两个不同的组件。通过Intent，你的程序可以向Android表达某种请求或者意愿，Android会根据意愿的内容选择适当的组件来响应。
- activity、service和broadcast receiver之间是通过Intent进行通信

#### Context是什么
- Context是个抽象类，通过类的结构可以看到：Activity、Service、Application都是Context的子类；
- 从Android系统的角度来理解：Context是一个场景，描述的是一个应用程序环境的信息，即上下文，代表与操作系统的交互的一种过程。
- 从程序的角度上来理解：Context是个抽象类，而Activity、Service、Application等都是该类的一个实现。

### Android常见的四大组件（Activity,Service,Content Provider,BroadcastReceiver)
#### Activity 
- Activity是一个应用程序组件，提供一个屏幕，用户可以用来交互为了完成某项任务。
- Activity中所有操作都与用户密切相关，是一个负责与用户交互的组件，可以通过setContentView(View)来显示指定控件。
- 在一个android应用中，一个Activity通常就是一个单独的屏幕，它上面可以显示一些控件也可以监听并处理用户的事件做出响应。Activity之间通过Intent进行通信。


####  BroadcastReceiver
- 定义

即广播，是一个全局的监听器。
>Android 广播分为两个角色：广播发送者、广播接受者

- 作用

监听/接收 应用 app 发出的广播消息，并做出响应

- 应用场景

Android不同组件间的通信、多线程通信、与Android系统在特定情况下的通信
>如：电话呼入时、网络可用时

## OS
#### os.Bundle
Bundle主要用于传递数据；它保存的数据，是以key-value(键值对)的形式存在的。我们经常使用Bundle在Activity之间传递数据，传递的数据可以是boolean、byte、int、long、float、double、string等基本类型或它们对应的数组，也可以是对象或对象数组。当Bundle传递的是对象或对象数组时，必须实现Serializable 或Parcelable接口。下面分别介绍Activity之间如何传递基本类型、传递对象。

#### widget.Toast
android.widget.Toast是android提供的一个用于快显信息的类。这是个比较方便好用的东西，特别是在初步建立Android应用程序的控制或是行为时，可以用来辅助我们进行初步的测试工作。
