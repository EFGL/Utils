#随手记

 * D:\Android\workspace\gz_key\SXgangzhangKey\bin

 * AsyncTask
 * android提供给我们的一个多线程编程框架,用来进行耗时的操作。防止ANR（Application not responding）
 * 内部实现了Handler和多线程的线程池，线程池会通过根据当前机器运行CUP的个数决定线程池中的线程个数
 * 我们需要定义一个类来继承AsyncTask这个抽象类，并实现其唯一的一个doInBackgroud抽象方法
 *
 * onPreExecute(): 这个方法是在执行异步任务之前的时候执行，并且是在UI Thread当中执行的
 * 通常我们在这个方法里做一些UI控件的初始化的操作，例如弹出ProgressDialog
 *
 * doInBackground(Params… params): 在onPreExecute()方法执行完后，会马上执行这个方法，这个方法就是来处理异步任务的方法
 * Android操作系统会在后台的线程池当中开启一个worker thread来执行这个方法（即在worker thread当中执行），
 * 执行完后将执行结果发送给最后一个 onPostExecute 方法，在这个方法里，我们可以从网络当中获取数据等一些耗时的操作
 *
 * onPostExecute(Result… result): 当异步任务执行完之后，就会将结果返回给这个方法，这个方法也是在UI Thread当中调用的，
 * 我们可以将返回的结果显示在UI控件上
 *
 * onProgressUpdate(Progess… values): 这个方法也是在UI Thread当中执行的，在异步任务执行的时候，有时需要将执行的进度返回给UI界面，
 * 例如下载一张网络图片，我们需要时刻显示其下载的进度，就可以使用这个方法来更新进度。这个方法在调用之前，我们需要在 doInBackground
 * 方法中调用一个 publishProgress(Progress) 的方法来将进度时时刻刻传递给 onProgressUpdate 方法来更新
 
----------------------------------------------------------------------------------------------

网址：

* RecyclerView 刷新
https://github.com/android-cjj/Android-MaterialRefreshLayout/blob/master/README-cn.md
https://github.com/jianghejie/XRecyclerView
https://github.com/dinuscxj/RecyclerRefreshLayout
----------------------------------------------------------------------------------------------
* 各种刷新				      
https://github.com/android-cjj/BeautifulRefreshLayout
* ProgressBar		    		
https://github.com/lsjwzh/MaterialLoadingProgressBar
* CircularProgressView		
https://github.com/rahatarmanahmed/CircularProgressView
* NumberProgressBar	  		
https://github.com/daimajia/NumberProgressBar
* 开源框架				      	
http://gank.io/
* MaterialSearchBar		  
https://github.com/mancj/MaterialSearchBar
* BottomDialog		    	
https://github.com/Curzibn/BottomDialog?
* IndexableListView		 
https://github.com/woozzu/IndexableListView
* MaterialDrawer侧滑菜单	
https://github.com/mikepenz/MaterialDrawer
* PersistentSearch		  
https://github.com/Quinny898/PersistentSearch
* sweet-alert-dialog	
https://github.com/pedant/sweet-alert-dialog
* android-floating-action-button
https://github.com/futuresimple/android-floating-action-button
* quicksidebar索引	
https://github.com/saiwu-bigkoo/Android-QuickSideBar
* JellyToggleButton		   
https://github.com/Nightonke/JellyToggleButton/blob/master/README-ZH.md
* PickerView时间选择控件	  
https://github.com/saiwu-bigkoo/Android-PickerView
* LoonAndroid3封装的常用功能 
https://github.com/gdpancheng/LoonAndroid3
----------------------------------------------------------------------------------------------
#actionbar左侧导航动画 
* LDrawer	
https://github.com/keklikhasan/LDrawer
* android-ui		  
https://github.com/markushi/android-ui
* material-menu	  	
https://github.com/balysv/material-menu
* ActionBarDrawerToggle	
Android自带
*　uCrop图片裁剪				
https://github.com/Yalantis/uCrop


* 各种图片处理			
http://www.jianshu.com/p/2720ad8d74da


Android安卓开发知识库汇总	http://blog.csdn.net/asmcvc/article/details/51914982
《Android 开发工程师面试指南》	http://www.diycode.cc/wiki/androidinterview
国内一线互联网公司内部面试题库	https://github.com/JackyAndroid/AndroidInterview-Q-A/blob/master/README-CN.md
笔记				https://github.com/jiang111/awesome-android-tips


reactnative开发				http://reactnative.cn/
					http://www.w3ctech.com/topic/909?utm_source=tuicool&utm_medium=referral
蓝灯					https://github.com/getlantern/lantern
FlycoDialog_Master			https://github.com/H07000223/FlycoDialog_Master
NiftyDialogEffects			https://github.com/sd6352051/NiftyDialogEffects
AndroidViewAnimations动画	https://github.com/daimajia/AndroidViewAnimations
AndroidUtil					https://github.com/Blankj/AndroidUtilCode
免费VPN						http://blog.csdn.net/hellohaifei/article/details/8965477
as插件						http://blog.csdn.net/liang5630/article/details/51867553
吴晓龙个人技术				http://wuxiaolong.me/
BRVAH分享吧					https://github.com/CymChad/BRVAHST

#开源项目集合							0.http://link.zhihu.com/?target=https%3A//github.com/Trinea/android-open-project
1. http://www.androidviews.net/
2. https://github.com/Trinea/android-open-project
3.android DevAppsDirect apk几乎把Android的开源项目收集齐了 谷歌下载，百度下载
4.http://blog.tisa7.com/android_open_source_projects
5.http://blog.daimajia.com/?page_id=60
6.http://www.23code.com/
7.https://f-droid.org/ 一个很好的网站，种类比较多不只局限于UI
8.https://github.com/Freelander/Android_Data/blob/master/Android-Librarys-Top-100.md
9.http://blog.daimajia.com/android-library-collection/
10.http://m.blog.csdn.net/article/details?id=50542590


* google color	https://material.google.com/style/color.html#color-color-palette

* XUtils 异常信息(callback没写模版)
```
java.lang.IllegalArgumentException:
FindGenericType:class com.gz.repair.LoginActivity$1, declaredClass:
interface org.xutils.common.Callback$CommonCallback, index: 0
```



* PopupWindow 的用法
```
        // 下拉选择框 显示一个listView 宽：200 高：400
        PopupWindow popupWindow = new PopupWindow(listView,200 ,400);

        // 点击pop意外的区域自动消失  第一步先设置一个透明背景 目的是让让pop有外部区域
        popupWindow.setBackgroundDrawable(new BitmapDrawable());
        popupWindow.setOutsideTouchable(true);// 第二步 设置外部区域可被点击

        // pop条目可以被点击 防止获取不到焦点
        popupWindow.setFocusable(true);

        // pop显示在指定view 下面，0，0代表偏移量
        popupWindow.showAsDropDown(view, 0, 0);
//        popupWindow.showAtLocation((View parent, int gravity, int x, int y); // 另一种显示方式 (指定位置)

		// 让 pop 消失的方法
		popupWindow.dismiss();
```

* Andorid L theme colorPrimary 
不能使用带有alpha的颜色值，否则会有异常抛出，直接判断了是否alpha是否等于0或者255，其他都会异常
```
Caused by: java.lang.RuntimeException:
			 A TaskDescription's primary color should be opaque
```


* invisibie与gone区别
```
	不可见与隐藏,一个占位一个不占位
	gone这里不占位是指view完全隐藏,包括margin所占距离的属性,
	invisibie不行,即使view不可见了,但view所占额外距离(margin)仍在
	```
	
* SwipRefreshLayout
```
	被包裹的view要有值,指RecyclerView等,没值显示异常
```

* Menu
```
	<item
	        android:id="@+id/action_search"
	        android:orderInCategory="10" // 该值越小，越靠前
	        android:title="search"
	        app:showAsAction="never" />
```


* github 提交新项目
```
	VCS->Import into Version Control->Share Project on GitHub
```
* github 提交更新代码
```
	右键java类 点git 先add到git库 才能conmmit and push
```
http://www.shaoqun.com/a/161180.aspx


* CardView 设置点击效果(作为item)
```
		android:foreground="?android:attr/selectableItemBackground"
		android:clickable="true"
```
```
android:fitsSystemWindows="true" //通知栏颜色适应屏幕的颜色变化而变化(设置在根布局) 
```

```
Button或ImageButton等自带按钮功能的控件会抢夺所在Layout的焦点.导致其他区域点击不生效.
在所在layout声明一个属性 android:descendantFocusability="blocksDescendants" // 该属性意为：子孙View分区域获取焦点 
```


* 二维码：
本质是一段字符串。
二维码由黑格白格组成，就代表着计算机的0和1.
扫描二维码就是读取了图中的0和1数据，在将0和1拼接，最后转为字符串。
所以稀疏的二维码代表数据少，秘籍的二维码代表数据多。
二维码外侧三个最大的黑框，不是数据，是来锁定二维码的范围。


```
TelephonyManager tm = (TelephonyManager)getSystemService(TELEPHONY_SERVICE); 
String deviceId = tm.getDeviceId();
```


```
measure(int widthMeasureSpec, int heightMeasureSpec)
```

```
// measure(0,0);
//参数是Android自定义的常量MeasureSpec.UNSPECIFIED	MeasureSpec.AT_MOST	MeasureSpec.EXACTLY
//0是UNSPECIFIED，1是EXACTLY，2是AT_MOST
```

#如果你正在用Gradle插件v2.0或者更高，我有一个简洁方法去启用它：
```
			android {
			  defaultConfig {
				vectorDrawables.useSupportLibrary = true
			  }
			}
```
#如果你还没有更新，在用v1.5后者更低的版本，你需要在你的build.gradle文件里添加以下内容:
```
android {
			  defaultConfig {
				
				generatedDensities = []
			  }
			  
			  aaptOptions {
				additionalParameters "--no-version-vectors"
			  }
			}
```


* 随机色:
```
int color = Color.rgb((int)(Math.Random()*256),(int)(Math.Random()*256),(int)(Math.Random()*256));
```


* 内部存储;存储目录在 packageName/file/文件名
```
// 写数据
FileOutputStream fos = context.openFileOutput(fileName,Context.MODE_PRIVATE);
fos.write(String.getBytes());
fos.close();

// 读数据
FileInputStream fis = context.openFileInput(fileName);
byte [] b = new byte[fis.available()];
fis.red(b);
fis.close();

String str = new String(b);
```
----------------------------------------------------------------------------------------------
//android studio assets资产目录
//src\main\assets\file

//assets file copy
```
        // File 目录下创建数据同名文件
        File files = getFilesDir();
        File file = new File(files, "tenement_passing_manager.db");
        if (file.exists()){
            return;
        }
        InputStream inputStream = null;
        FileOutputStream fos = null;
        try {
            // 读取assets资产目录下的数据库文件
            inputStream = getAssets().open("tenement_passing_manager.db");
            // 将读取到的写到指定file
            fos = new FileOutputStream(file);
            byte [] bs = new byte[1024];
            int temp = -1;
            while ((temp = inputStream.read(bs))!=-1){
                fos.write(bs,0,temp);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if (inputStream!=null&&fos!=null){

                try {
                    inputStream.close();
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
  ```
----------------------------------------------------------------------------------------------
