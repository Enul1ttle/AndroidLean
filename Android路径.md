## 手机存储
**手机分为内部存储和外部存储**
### 0x01 内部存储

```
Environment.getDataDirectory()                    /data
Environment.getDownloadCacheDirectory()           /cache
Environment.getRootDirectory()                    /system (无ROOT无法打开)
```
### 0x02 外部存储
**外部存储又分为SD卡和扩展卡内存**
#### (1)SD卡
获取路径方式是`Environment.getExternalStorageDirectory()  /storage/sdcard0`
```
//SD卡九大公有目录
Environment.getExternalStoragePublicDirectory(DIRECTORY_ALARMS)	/storage/sdcard0/Alarms
Environment.getExternalStoragePublicDirectory(DIRECTORY_DCIM)	/storage/sdcard0/DCIM
Environment.getExternalStoragePublicDirectory(DIRECTORY_DOWNLOADS)	/storage/sdcard0/Download
Environment.getExternalStoragePublicDirectory(DIRECTORY_MOVIES)	/storage/sdcard0/Movies
Environment.getExternalStoragePublicDirectory(DIRECTORY_MUSIC)	/storage/sdcard0/Music
Environment.getExternalStoragePublicDirectory(DIRECTORY_NOTIFICATIONS)	/storage/sdcard0/Notifications
Environment.getExternalStoragePublicDirectory(DIRECTORY_PICTURES)	/storage/sdcard0/Pictures
Environment.getExternalStoragePublicDirectory(DIRECTORY_PODCASTS)	/storage/sdcard0/Podcasts
Environment.getExternalStoragePublicDirectory(DIRECTORY_RINGTONES)	/storage/sdcard0/Ringtones

//私有目录
getExternalFilesDir()	/storage/emulated/0/Android/data/cwj.test(包名)/files/test
getExternalCacheDir	/storage/emulated/0/Android/data/cwj.test(包名)/cache/test
```
#### (2)扩展卡内存
扩展内存就是我们插入的外置SD卡,代码如下：
```
private static String getExtendedMemoryPath(Context mContext) {  
      StorageManager mStorageManager = (StorageManager) mContext.getSystemService(Context.STORAGE_SERVICE);
        Class storageVolumeClazz = null;
        try {
            storageVolumeClazz = Class.forName("android.os.storage.StorageVolume");
            Method getVolumeList = mStorageManager.getClass().getMethod("getVolumeList");
            Method getPath = storageVolumeClazz.getMethod("getPath");
            Method isRemovable = storageVolumeClazz.getMethod("isRemovable");
            Object result = getVolumeList.invoke(mStorageManager);
            final int length = Array.getLength(result);
            for (int i = 0; i < length; i++) {
                Object storageVolumeElement = Array.get(result, i);
                String path = (String) getPath.invoke(storageVolumeElement);
                boolean removable = (Boolean) isRemovable.invoke(storageVolumeElement);
                if (removable) {
                    return path;
                }
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
        return null;
}
```
### 路径测试：
```
Log.e("cwj", "外置SD卡路径 = " + getStoragePath(this));
Log.e("cwj", "内置SD卡路径 = " + Environment.getExternalStorageDirectory().getAbsolutePath());
Log.e("cwj", "手机内存根目录路径  = " + Environment.getDataDirectory().getParentFile().getAbsolutePath());
```

### Honor 9的测试的结果
```
Log.i("codecraeer","getFilesDir = "+ getFilesDir());
//getFilesDir = /data/user/0/com.example.test1/files
//获取的是某个应用data/fata/files

Log.i("codecraeer","getExternalFilesDir = "+ getExternalFilesDir("exter_test").getAbsolutePath());
//getExternalFilesDir = /storage/emulated/0/Android/data/com.example.test1/files/exter_test

Log.i("codecraeer","getDownloadCacheDirectory = "+ Environment.getDownloadCacheDirectory().getAbsolutePath());
//getDownloadCacheDirectory = /data/cache

Log.i("codecraeer","getDataDirectory = "+ Environment.getDataDirectory().getAbsolutePath());
//getDataDirectory = /data

Log.i("codecraeer","getExternalStorageDirectory = "+ Environment.getExternalStorageDirectory().getAbsolutePath());
//getExternalStorageDirectory = /storage/emulated/0

Log.i("codecraeer","getExternalStoragePublicDirectory = "+ Environment.getExternalStoragePublicDirectory("pub_test"));
//getExternalStoragePublicDirectory = /storage/emulated/0/pub_test
```
### 文章
android文件路径最全知识点：https://www.jianshu.com/p/24747fec19f0
Android 存储路径你了解多少：https://juejin.im/entry/58cb92415c497d0057b6c1a9
android中的文件操作详解：http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2013/0923/1557.html
