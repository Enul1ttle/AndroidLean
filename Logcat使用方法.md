## Tips
>很多高版本的系统的手机都默认禁用Logcat,需要自己开启

>eclipse打开LogCat`windows->show view -> other->Android->LogCat`

### 常见的日志纪录方法包括
```
v(String,String) (vervbose)	       #显示全部信息
d(String,String)(debug)	           #显示调试信息
i(String,String)(information)      #显示一般信息
w(String,String)(waning)	         #显示警告信息
e(String,String)(error)	           #显示错误信息
```
### 使用例子
```
//开发过程中获取log
Log.i("MyActivity","MyClass.getView() - get item number"+position);
//adb获取log
adb logcat
```
