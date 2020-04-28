![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/title.png) <br /><br />
[![jiang111/image](https://jiang111.github.io/images/awesome.svg)](https://github.com/jiang111/awesome-android-tips)   [![](https://badge.juejin.im/entry/57ad3f87c4c9710054687895/likes.svg?style=plastic)](https://juejin.im/entry/57ad3f87c4c9710054687895/detail)
<br />


EnglishVersion ->_->:https://github.com/jiang111/awesome-android-tips/blob/master/README-en.md

值得收藏的AS插件 ->_->:https://github.com/jiang111/awesome-androidstudio-plugins <br />

这里收集了大家常用的一些Android代码,持续更新中,内容来自自己的平时积累和网络上看到的文章，部分原文地址在最下方。如有错误欢迎指正,如有侵权,请联系我删除。里面可能会有重复内容,请忽略或者提醒我删除。<br /><br />

# ![Table of Contents](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/toc.png)

* BuildConfig.DEBUG中的DEBUG值为true或者false不是取决于你的buildType,而是取决于buildTypes中的debuggable字段,比如:
```
buildTypes {
        release {
            debuggable true   //即使是release模式,但是由于debuggable是true,所以它的BuildConfig.DEBUG值依然是true
        }
        debug {
	    debuggable false //即使是debug模式,但是由于debuggable是false,所以它的BuildConfig.DEBUG值依然是false
        }
    }
```
所以正常情况下不要配置debuggable字段


* setBackgroundResource(0) 可以移除 View 的背景色

* Resources.getSystem().getDisplayMetrics().density 可以不用 Context 也能获取屏幕密度哦

* 通过重载 ViewGroup 的 dispatchDraw 可以实现一个简单的蒙版效果。 例如下拉刷新时，可以在 contentView 上加一层遮罩。 canvas.drawRect(0, mContentView.getTranslationY(), getWidth(), getHeight(), mMaskPaint);

* new 出来的 View 可以用 View.generateViewId() （API 17 以上可用）   生成 id，系统保证唯一

* 使用 GridView时 android:padding 和 android:clipToPadding="false" 配合使用效果更好哦。

* 在布局文件中，如果只是为了占位，可以用 Space 来取代 View。 最棒的一点是Space可以跳过 Draw 这个过程。

* TypedValue.applyDimension(int unit, float value, DisplayMetrics metrics) 方便dp, px, sp 之间的转换。

* Activity.startActivities() 这个方法最直接的理解就是使用intent开启多个Activity

* TextUtils.isEmpty() 如果传入的String 为NULL或者Length为0的话就返回 true。

* Html.fromHtml() 如果你对Html熟悉的话，可以很迅速通过这个方法处理一些富文本操作。比如超链接和图文排版等处理。

* TextView.setError() 设置文本框错误提醒

* Build.VERSION_CODES 有些时候我们的app需要根据不同的SDK版本进行执行不同的操作

* PhoneNumberUtils.convertKeypadLettersToDigits 这个方法简单粗暴，会将输入的字母根据键盘上的映射转换为数字。

* ArgbEvaluator ArgbEvaluator.evaluate(float fraction, Object startValue, Object endValue);根据一个起始颜色值和一个结束颜色值以及一个偏移量生成一个新的颜色，分分钟实现类似于微信底部栏滑动颜色渐变。

* ValueAnimator.reverse() 顺畅的取消动画效果

* DateUtils.formatDateTime()) 这个方法可以输出相应格式化的时间或者日期


* Pair 这个类 可以用来存储存储一”组”数据。但不是key和value的关系。

* SparseArray 目前有很多地方从性能优化方说使用SparseArray来替换hashMap，来节省内存，提高性能。

* Linkify.addLinks() 这个类可以更方便的为文本添加超链接。

* android.media.ThumbnailUtils这个类主要是用来处理缩略图相关的工作,比如:用来获取媒体（图片、视频）的缩略图
```
createVideoThumbnail(String filePath, int kind)
extractThumbnail(Bitmap source, int width, int height)
```

* Bitmap.extractAlpha ();返回一个新的Bitmap，capture原始图片的alpha值。有的时候我们需要动态的修改一个元素的背景图片又不希望使用多张图片的时候，通过这个方法，结合Canvas和Paint可以动态的修改一个纯色Bitmap的颜色。

* 模块间有消息需要传递时，使用LocalBroadcastManager替代Listener进行模块解耦。除了解耦，这样发送消息和执行消息差一个线程循环，可以减小方法的调用链，我这就碰到一次方法调用链太长导致StackOverflow的问题。

* 静态变量不要直接或者间接引用Activity、Service等。这会使用Activity以及它所引用的所有对象无法释放，然后，用户操作时间一长，内存就会狂升。

* Handler机制有一个特点是不会随着Activity、Service的生命周期结束而结束。也就是说，如果你Post了一个Delay的Runnable，然后在Runnable执行之前退出了Activity，Runnable到时间之后还是要执行的。如果Runnable里面包含更新View的操作，可能会造成内存泄露,所以可以在 onDestory() 的时候调用removeCallbacksAndMessages来移除这个Handler所对应等待执行的message。

* 不少人在子线程中更新View时喜欢使用Context.runOnUiThread，这个方法有个缺点，就是一但Context生命周期结束，比如Activity已经销毁时，一调用就会崩溃。

* SharedPreferences.Editor.commit这个方法是同步的，一直到把数据同步到Flash上面之后才会返回，由IO操作的不可控，尽量使用apply方法代替。apply只在API Level>=9才会支持，需要做兼容。不过，最新的 `support v4` 包已经为我们做好了处理，使用  `SharedPreferencesCompat.EditorCompat.getInstance().apply(editor)` 即可。

* PackageManager.getInstalledPackages这个方法经常使用，你可能不知道，当获取的结果数量比较多的时候，在某些机型上面调用它花费的时间可能秒级的，所以尽量在子线程中使用。另外，如果结果太多，超过系统设置的Binder数据最大传输量的上限，则会发生TransactionException，如果你使用这个方法获取机器上的己安装应用列表，最好做一下预防。

* 如果使用Context.startActivity启动外部应用，最好做一下异常预防，因为寻找不到对应的应用时，会抛出异常。如果你要打开的是应用内的Activity，不防使用显式Intent，这样能提高系统搜索目标Activity的效率。

* Application的生命周期就是进程的生命周期。只有进程被干掉时，Application才会销毁。哪怕是没有Activity、Service在运行，Application也会存在。所以，为了减少内存压力，尽量不要在Application里面引用大对象、Context等。

* 设置全屏方法有2种:1.通过代码设置，2通过manifest文件设置。用代码设置全屏时app在我们应用运行后，可能会看到短暂的状态栏，然后才全屏，而第二种方法是不会有这种情况的,所以推荐第二种。
```
//方法1: 
//无title   
requestWindowFeature(Window.FEATURE_NO_TITLE);    
getWindow().setFlags(WindowManager.LayoutParams. FLAG_FULLSCREEN,WindowManager.LayoutParams. FLAG_FULLSCREEN);   
//必须在setContentView()之前调用
setContentView(R.layout.main);  
//方法2:
<activity android:name="." 
    android:theme="@android:style/Theme.NoTitleBar.Fullscreen" //全屏主题
    android:label="@string/app_name" />
```

* viewpager 的 setCurrentItem 一定要在 setAdapter 方法之后调用才会有效果.

* 判断手机是不是飞行模式  boolean isEnabled = Settings.System.getInt(context.getContentResolver(), Settings.System.AIRPLANE_MODE_ON, 0) == 1;

* TabLayout 修改字体的方法
官方的 TabLayout 没有提供修改 TextView size 的方法，可以新建一个 style CustomTabLayoutTextAppearance 继承 TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse ，然后增加 item ，设置 android:textAllCaps 为 true ，再设置 android:textSize 为你想设置的大小。
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/custom_style1.jpg)
再在 TabLayout 的布局文件里设置 app:tabTextAppearance="@style/CustomTabLayoutTextAppearance" 即可。
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/custom_style2.jpg)

* 遍历HashMap的最佳方法
```java
public static void printMap(Map mp) {
    for (Map.Entry m : mp.entrySet()) {
            System.out.println(m.getKey() + ":" + m.getValue());
        }
}
```

* 使用Java在一个区间内产生随机整数数
```java
public static int randInt(int min, int max) {
    Random rand = new Random();
    int randomNum = rand.nextInt((max - min) + 1) + min;
    return randomNum;
}
```

* 如果子类实现Serializable接口而父类未实现时，父类不会被序列化，但此时父类必须有个无参构造方法，否则会抛InvalidClassException异常。

* transient关键字修饰变量可以限制序列化。

* 当使用JakeWharton的TabPageIndicator时，如果需要先做一些耗时的操作，然后再展示TabPageIndicator的话，需要先设置mIndirector.setVisibility(View.GONE);然后耗时任务结束以后再mIndirector.setVisibility(View.VISIBLE);否则会报错

* 类继承之间的调用顺序 父类static成员 -> 子类static成员 -> 父类普通成员初始化和初始化块 -> 父类构造方法 -> 子类普通成员初始化和初始化块 -> 子类构造方法

* 华为手机无法显示log解决方案,.拨号界面输入(\*#\*#2846579#\*#\*) Service menu will appear.Go to "ProjectMenu" -> "Background Setting" -> "Log Setting"Open "Log switch" and set it to ON.Open "Log level setting" and set the log level you wish.

* 后台service经常因为重启之类的出现onStartCommand()中的Intent传递的参数为null， 通过在onStartCommand()中的返回值改成return super.onStartCommand(intent, Service.START_REDELIVER_INTENT, startId); 可以解决问题。下面介绍几个flag的意思<br />

* | flag        | 解释       |
| ------------- |:-------------:|
| START_STICKY | 如果service进程被kill掉，保留service的状态为开始状态，但不保留递送的intent对象。随后系统会尝试重新创建service，由于服务状态为开始状态，所以创建服务后一定会调用onStartCommand(Intent,int,int)方法。如果在此期间没有任何启动命令被传递到service，那么参数Intent将为null。 |
| START_NOT_STICKY | “非粘性的”。使用这个返回值时，如果在执行完onStartCommand后，服务被异常kill掉，系统不会自动重启该服务。 |
|START_REDELIVER_INTENT|重传Intent。使用这个返回值时，如果在执行完onStartCommand后，服务被异常kill掉，系统会自动重启该服务，并将Intent的值传入。|
|START_STICKY_COMPATIBILITY|START_STICKY的兼容版本，但不保证服务被kill后一定能重启。  |

* 不能在Activity没有完全显示时显示PopupWindow和Dialog

* 在多进程之间不要用SharedPreferences共享数据，虽然可以（MODE_MULTI_PROCESS），但极不稳定

* 有些时候不能使用Application的Context，不然会报错（比如启动Activity，显示Dialog等）
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/context_usage.png)

>*备注：大家注意看到有一些NO上添加了一些数字，其实这些从能力上来说是YES，但是为什么说是NO呢？下面一个一个解释：
1. 数字1：启动Activity在这些类中是可以的，但是需要创建一个新的task，一般情况不推荐；
2. 数字2：在这些类中去layout inflate是合法的，但是会使用系统默认的主题样式，如果你自定义了某些样式可能不会被使用；
3. 数字3：在Receiver为null时允许，在4.2或以上的版本中，用于获取黏性广播的当前值。（可以无视）；
4. ContentProvider、BroadcastReceiver之所以在上述表格中，是因为在其内部方法中都有一个context用于使用。

* 谨慎使用Android的透明主题，透明主题会导致很多问题，比如：如果新的Activity采用了透明主题，那么当前Activity的onStop方法不会被调用；在设置为透明主题的Activity界面按Home键时，可能会导致刷屏不干净的问题；进入主题为透明主题的界面会有明显的延时感
* 不要在非UI线程中初始化ViewStub，否则会返回null

* 尽量不要通过Application缓存数据，这不稳定

* 华为手机无法打开USB调试的问题，
1. 插好数据线,拨号界面 输入 *#*#2846579#*#* 进入工程模式
2. projectmenu→3后台设置→4USB端口配置→Balong调试模式,点确定
3. 不要拔线,退出工程模式,直接重启手机,电脑中显示可移动磁盘(若仍未出现,重复步骤1、2)
4. 这个是关闭USB调试的情况下电脑中使用手机的可移动磁盘的方法，使用后下拉菜单中usb选项也回来了。

* android listview中的消息被软键盘遮挡了,在设置listview的时候加上android:transcriptMode="normal"就好了

* TextUtils 是一个非常好用的工具类，把 List<String> 转成字符串，逗号分隔，逗号分隔的 String 字符串，切割成 List<String> ，分别可以用 TextUtils 的 join 和 split 方法。如果要对 List 去重，则可以用 Collection 的 frequency 方法。

* 在activity中调用 moveTaskToBack (boolean nonRoot)方法即可将activity 退到后台，注意不是finish()退出。

* activity中的runOnUiThrea(Runnable action)方法可以直接回到主线程

* listview有个footerDividersEnabled和headerDividersEnabled方法可以设置listview的顶部和底部divide，但是必须保证你设置了headview和footview才会有效果

* Throwable类中的getStackTrace()方法，根据这个方法可以得到函数的逐层调用地址，其返回值为StackTraceElement[]；

* StackTraceElement类，其中四个方法getClassName()，getFileName()，getLineNumber()，getMethodName()在调试程序打印Log时非常有用；

* UncaughtExceptionHandler接口，再好的代码异常难免，利用此接口可以对未捕获的异常善后

* Resources类中的getIdentifier(name, defType, defPackage)方法，根据资源名称获取其ID，做UI时经常用到；

* view的isShown方法，只有当view本身以及它的所有祖先们都是visible时，isShown（）才返回TRUE。而平常我们调用if(view.getVisibility() == View.VISIBLE)只是对view本身而不对祖先的可见性进行判断。

* Arrays类中的一系列关于数组操作的工具方法：binarySearch()，asList()，equals()，sort()，toString()，copyOfRange()等；Collections类中的一系列关于集合操作的工具方法：sort()，reverse()等；

* TextView类中的append(CharSequence)方法，添加文本。一些特殊文本直接用+连接会变成String；

* System类中的arraycopy(src, srcPos, dest, destPos, length)方法，用来copy数组；

* Fragment类中的onHiddenChanged(boolean)方法，使用FragmentTransaction中的hide()，show()时只会调用Fragment中的show和hidden状态,其他生命周期不会调用。

* Activity类中的onWindowFocusChanged(boolean)，onNewIntent(intent)等回调方法；

* TextView类中的setTransformationMethod(TransformationMethod)方法，可用来实现“显示密码”功能

* PageTransformer接口，用来自定义ViewPager页面切换动画，用setPageTransformer(boolean, PageTransformer)方法来进行设置；

* apache提供的一系列jar包：commons-lang.jar，commons-collections.jar，commons-beanutils.jar等，里面很多方法可能是你曾经用几十几百行代码实现过的，但是执行效率或许要差很多，比如：ArrayUtils，StringUtils……；

* ActivityLifecycleCallbacks接口，用于在Application类中监听各Activity的状态变化 [阅读地址点我](http://mp.weixin.qq.com/s?__biz=MzA3ODkzNzM3NQ==&mid=401277907&idx=1&sn=0b2246f5178292596fc3a8295283359c#rd)

* ActionBar.hide()/.show() 顾名思义，隐藏和显示ActionBar，可以优雅地在全屏和带Actionbar之间转换。

* SystemClock.sleep() 这个方法在保证一定时间的 sleep 时很方便，通常我用来进行 debug 和模拟网络延时。

* UrlQuerySanitizer——使用这个工具可以方便对 URL 进行检查。

* ActivityOptions ——方便的定义两个Activity切换的动画。 使用ActivityOptionsCompat 可以很好解决旧版本的兼容问题。

* getParent().requestDisallowInterceptTouchEvent(true);剥夺父view对touch事件的处理权，谁用谁知道。

* HandlerThread，代替不停new Thread开子线程的重复体力写法。
 
* IntentService,一个可以干完活后自己去死且不需要我们去管理子线程的Service

* Executors. newSingleThreadExecutor();这个是java的，之前不知道它，自己花很大功夫去研究了单线程顺序执行的任务队列 

* android:animateLayoutChanges="true"，LinearLayout中添加View的动画的办法，支持通过setLayoutTransition()自定义动画。

* AsyncQueryHandler，如果做系统工具类的开发，比如联系人短信辅助工具等，肯定免不了和ContentProvider打交道，如果数据量不是很大的情况下，随便搞，如果数据量大的情况下，了解下这个类是很有必要的，需要注意的是，这玩意儿吃异常..

* ViewFlipper，实现多个view的切换(循环)，可自定义动画效果，且可针对单个切换指定动画。

* android util包中的Pair类，可以方便的用来存储一"组"数据。注意不是key value

* android:descendantFocusability，ListView的item中CheckBox等元素抢焦点导致item点击事件无法响应时，除了给对应的元素设置 focusable,更简单的是在item根布局加上android:descendantFocusability=”blocksDescendants” 

* includeFontPadding="false"，TextView默认上下是有一定的padding的，有时候我们可能不需要上下这部分留白，加上它即可。

* Messenger，面试的时候通常都会被问到进程间通信，一般情况下大家都是开始背书，AIDL巴拉巴拉。。有一天在鸿神的博客看到这个，嗯，如他所说，又可以装一下了。 

* EditTxt.setImeOptions， 使用EditText弹出软键盘时，修改回车键的显示内容(一直很讨厌用回车键来交互，所以之前一直不知道这玩意儿) 

* java8中新增的LocalDate和LocalTime接口，Date虽然是个万能接口，但是它真的不好用，有了这俩，终于可以愉快的处理日期时间了。

* WeakHashMap，直接使用HashMap有时候会带来内存溢出的风险，使用WaekHashMap实例化Map。当使用者不再有对象引用的时候，WeakHashMap将自动被移除对应Key值的对象。

* 使用SnackBar的时候，不要使用view.getRootView()作为snackbar的view,华为荣耀7 会出问题。

* 设置TextView单行显示的时候不要用Lines=1,而要用singleLine="true" ,因为魅族部分手机在设置Lines=1的时候，然后TextView的值全为数字的时候， 你就会懵逼了.

* TouchDelegate可用于更改View的触摸区域。场景：比如在RecyclerView的ItemView里包含了CheckBox组件, 然后想实现点击ItemView的时候，也可以触发CheckBox，就可以使用此类

* ArgbEvaluator可用于计算不同颜色值之间的插值，配合ValueAnimator.ofObject或者ViewPager.PageTransformer使用，可以实现不同颜色之间的平滑过渡。

* Palette可用于提取一张图片的颜色。

* ViewDragHelper,做过自定义ViewGroup的童鞋都应该知道这个东西吧，用来处理触摸事件的神器，妈妈再也不用担心我自定义控件了。

* PageTransformer用于定义ViewPager页面切换时的动画效果（淡入淡出，放大缩小神马的…）官方有例子，直接看吧。

* Formatter.formatFileSize() 这个方法会格式化数据的大小，根据输入的字节大小，返回 B KB MB GB 等等（最大支持到 PB）。当然要注意的是输入的最大值是 Long.MAX_VALUE.

* Activity.recreate重新创建Activity。有什么用呢？可以在程序更换主题后，立马刷新当前Activity，而不会有明显的重启Activity的动画。

* View.getContext顾名思义，就不用解释了吧…以前在写RecyclerView的Adapter的时候，为了使用LayoutInflater，经常傻乎乎地在构造函数中传入一个外部的context….是不是只有我不知道而已（笑cry脸）

* View.post方便在非UI线程对界面进行修改，与Handler的作用类似。并且由于post的Runnable会保证在该View绘制完成的前提下才调用，所以一般也可以用于获取View的宽高。

* Activity.runOnUiThread与View.post类似，方便在非UI线程中对界面进行修改。

* Fragment在配合PagerAdapter使用的时候可以重写setUserVisibleHintFragment()方法，然后根据参数的布尔值（true的话表示当前Fragment对用户可见),来执行一些逻辑。

* android:animateLayoutChanges 这是一个非常酷炫的属性。在父布局加上 android:animateLayoutChanges="true" 后，如果触发了layout方法（比如它的子View设置为GONE），系统就会自动帮你加上布局改变时的动画特效！！

* android:clipToPadding 设置父view是否允许其子view在它的padding（这里指的是父View的padding）中绘制。是不是有点绕？举个实际场景吧：假如有个ListView，我们想要在初始位置时，第一项Item离顶部有10dp的距离，就可以在ListView的布局中加入android:clipToPadding="false" android:paddingTop="10dp"即可。是不是很方便呢？

* rv 的 Layoutmanager 可以直接申明在 xml 中,具体代码可查看RecyclerView.createLayoutManager 方法.
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/recycler_1.jpeg)
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/recycler_2.jpeg)

* RecyclerView在23.2.+的版本中新增了自动测量的功能，由于新增了自动测量，那么它的item的根布局在需要测量的方向上就不能写match_parent了，需要改成wrap_content

* getParent().requestDisallowInterceptTouchEvent(true);剥夺父view对touch事件的处理权，谁用谁知道。

* Canvas中clipRect、clipPath和clipRegion剪切区域的API。

* GradientDrawable 有个阴影效果还不错，以为是切的图片，一看代码，什么鬼= =！

* 有朋友提到了在自定义View时有些方法在开启硬件加速的时候没有效果的问题，在API16之后确实有很多方法不支持硬件加速，通常我们关闭硬件加速都是在清单文件中通过<application android:hardwareAccelerated="false" ...>，其实android也提供了针对特定View关闭硬件加速的方法,调用View.setLayerType(View.LAYER_TYPE_SOFTWARE, null);即可。

* PointF，graphics包中的一个类，我们经常见到在处理Touch事件的时候分别定义一个downX，一个downY用来存储一个坐标，如果坐标少还好，如果要记录的坐标过多那代码就不好看了。用PointF(float x, float y);来描述一个坐标点会清楚很多。

* StateListDrawable，定义Selector通常的办法都是xml文件，但是有的时候我们的图片资源可能是从服务器动态获取的，比如很多app所谓的皮肤，这种时候就只能通StateListDrawable来完成了，各种addState即可。

* android:duplicateParentState="true"，让子View跟随其Parent的状态，如pressed等。常见的使用场景是某些时候一个按钮很小，我们想要扩大其点击区域的时候通常会再给其包裹一层布局，将点击事件写到Parent上，这时候如果希望被包裹按钮的点击效果对应的Selector继续生效的话，这时候duplicateParentState就派上用场了。

* ViewConfiguration.getScaledTouchSlop();触发移动事件的最小距离，自定义View处理touch事件的时候，有的时候需要判断用户是否真的存在movie，系统提供了这样的方法。

* ViewStub，有的时候一块区域需要根据情况显示不同的布局，通常我们都会通过setVisibility的方法来显示和隐藏不同的布局，但是这样默认是全部加载的，用ViewStub可以更好的提升性能。

* onTrimMemory，在Activity中重写此方法，会在内存紧张的时候回调（支持多个级别），便于我们主动的进行资源释放，避免OOM。

* TextView.setCompoundDrawablePadding，代码设置TextView的drawable padding。

* ImageSwitcher，可以用来做图片切换的一个类，类似于幻灯片。

* 在自定义控件的时候,能用drawable来绘制圆，或者其他样式的时候,尽量用drawable,因为drawable的效果要远胜于canvas.drawXXX().

* 如果想要自定义View支持SwipeRefreshLayout，只需要声明并实现ScrollingView接口即可，RecyclerView和NestedScrollView已经实现此接口。

* AtomicFile——通过使用备份文件进行文件的原子化操作。这个知识点之前我也写过，不过最好还是有出一个官方的版本比较好。

* DatabaseUtils——一个包含各种数据库操作的使用工具。

* Activity.isChangingConfigurations ()——如果在 Activity 中 configuration 会经常改变的话，使用这个方法就可以不用手动做保存状态的工作了。

* SearchRecentSuggestionsProvider——可以创建最近提示效果的 provider，是一个简单快速的方法。

* android:clipChildren (ViewGroup)——如果此属性设置为不可用，那么 ViewGroup 的子 View 在绘制的时候会超出它的范围，在做动画的时候需要用到。

* android:fillViewport (ScrollView)——在这片文章中有详细介绍文章链接，可以解决在 ScrollView 中当内容不足的时候填不满屏幕的问题。

* android:tileMode (BitmapDrawable)——可以指定图片使用重复填充的模式。

* android:enterFadeDuration/android:exitFadeDuration (Drawables)——此属性在 Drawable 具有多种状态的时候，可以定义它展示前的淡入淡出效果。

* Log.wtf()的意思是What a Terrible Failure,而不是What The Fuck!

* 使用RenderScript虚化图片效果。如果你的app的minSDK为16或者更低，你需要使用support模式，因为很多方法都是在API 17之后添加的。renderscriptTargetApi最高到23，但是你应该把它设置到能保持脚本中使用到的功能完整的最低API。如果你想在support模式下target API 21+你必须使用gradle-plugin 2.1.0 和 buildToolsVersion “23.0.3” 或者以上。需要在gradle中添加renderscriptTargetApi 18,renderscriptSupportModeEnabled true 这两句话
```java
public static Bitmap blurBitmap(Context context, Bitmap src, int radius) {
        Bitmap dest = src.copy(src.getConfig(), true);
        RenderScript rs = RenderScript.create(context);
        Allocation allocation = Allocation.createFromBitmap(rs, src);
        Type t = allocation.getType();
        Allocation blurredAllocation = Allocation.createTyped(rs, t);
        ScriptIntrinsicBlur blurScript = ScriptIntrinsicBlur.create(rs, Element.U8_4(rs));
        blurScript.setRadius(radius);
        blurScript.setInput(allocation);
        blurScript.forEach(blurredAllocation);
        blurredAllocation.copyTo(dest);
        allocation.destroy();
        blurredAllocation.destroy();
        blurScript.destroy();
        t.destroy();
        rs.destroy();
        return dest;
    }
```

* 如果想把一个view保存为Bitmap，正常情况下用第一种方法就可以了，但是如果是ScrollView，则必须采用第二种方法。 <br />
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/capture_view_1.jpg)
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/capture_view_2.jpg)

* 当Activity LauncherMode 为singleTask singleInstance时,使用startActivityForResult会立马返回，不能正常调用。具体请看http://www.360doc.com/content/15/0123/14/12928831_443085580.shtml

* 当PopupWindow中有EditText控件时,因为Popupwindow 默认没有获取到焦点，需要手动设置焦点，这样子view才能获取到事件的监听。所以你需要在创建完popwindow后设置他的焦点，popupWindow.setFocusable(true);就可以让EditText获取焦点。

* PopupWindow默认点击外部的时候不消失，需要对PopupWindow 设置一个背景图popWindow.setBackgroundDrawable(new BitmapDrawable());要创建一个空对象，设置为null是不行的，或者就创建一个全透明的背景图。

* android中的序列化官方推荐Parceble,其实Parceble最好用于内存之间数据的交换,如果要把数据写入硬盘的话,推荐实现Serializable

* tools标签可以很好的帮助开发者实时预览xml的效果,通过tools:background可以预览控件所占的控件,tools:visibility可以把一个gone的控件在预览的时候展示出来,并且运行以后tools标签的内容不会展示出来.例如:
```xml
<TextView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    tools:background="#FF00FF"
    tools:visibility="visible"
    tools:text="这段话只在预览时能看到,运行以后就看不到了" />
```

* android studio 2.1起已经支持jdk8了,使用的时候要在gradle中加上,需要把buildToolsVersion更新到24以上的版本
```
android {
    defaultConfig {
    ...
            jackOptions {
                enabled true
            }
        }
   ...
    compileOptions {
        targetCompatibility 1.8
        sourceCompatibility 1.8
    }
}
```

* 6.0之后getResources().getColor()方法被废弃了，大家可以用ContextCompat.getColor(context, R.color.color_name)替换，ContextCompat 是 v4 包里的，请放心使用，另外还有getDrawable()等方法

* 图片的资源文件官方推荐只把launcher放在mipmap文件夹下面，而app用到的资源文件建议放在drawable下面。

* SharedPreference.Editor的apply是异步操作，不会返回成功的状态，而commit是同步操作，因此，在多个并发的提交commit的时候，他们会等待正在处理的commit保存到磁盘后再操作下一个数据，从而降低了效率。

* 如果你在 manifest 中把一个 activity 设置成 android:windowSoftInputMode="adjustResize"，那么 ScrollView（或者其它可伸缩的 ViewGroups）会缩小，从而为软键盘腾出空间。但是，如果你在 activity 的主题中设置了 android:windowFullscreen="true"，那么 ScrollView 不会缩小。这是因为该属性强制 ScrollView 全屏显示。然而在主题中设置 android:fitsSystemWindows="false" 也会导致 adjustResize 不起作用

* 在Android 4.0以后，在Manifest.xml中静态注册的广播，程序安装后必须启动一次才能接收到广播，比如你的应用监听开机启动的广播，必须要你的程序被运行过才能监听到

* Activity的onDestory方法调用时机是不确定的（有时候离开界面很久之后才会调用onDestory方法），应该避免指望通过onDestory方法去释放与Activity相关的资源，否则会导致一些随机bug

* 2.X时代Bitmap对象虽然存储在堆内存中，但是用了一个byte数组存储其像素信息。通过计数器来记录该像素信息被引用的个数。有人认为这个byte数组在native堆中，但事实上它也在堆中。只有在使用者调用recycle()后，Bitmap对象才会释放像素信息，才会在失去引用后被垃圾回收机制销毁。再加上DVM的heap size有严格的阀值，所以在使用大量图片资源的时候，及其容易发生OOM。解决办法一般都是，用一个哈希表存储Bitmap对象的软引用，作为内存缓存，并在适当时机掉用其recycle()。3.0以上版本Bitmap对象可以通过垃圾回收机制完全销毁，理论上不用再调用recycle()。

* .gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未track状态），然后再提交：
```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

* 时间戳请使用long或者String类型接收，遇到的坑,由于项目中的model好多都是通过GsonFormat生成的，服务器给的json中的时间戳都是10位的，导致了GsonFormat自动解析成了int, 当测试人员选择时间为2100年的时候时间戳是4开头的十位 用int类型接收越界了,导致报错

* 为你的app添加默认布局样式,比如:每一个控件都需要写width和height属性,然而很多的控件的宽高属性都是wrap_content,那么我们可以通过在style文件添加如下样式:
```
<style name="Theme.YourApp" parent="android:style/Theme.Light">
    <item name="android:layout_width">wrap_content</item>
    <item name="android:layout_height">wrap_content</item>
</style>
```
这样,控件的宽高默认都是wrap_content样式啦。

* 在style中写的样式通过视同parent标签来扩展你的样式,这样更高效,这里官方的建议是，只有Android自带的style才用parent标签，如果是自定义的style，直接用.符号来连接就行。如Fill.Height。
```
<style name="Fill">
    <item name="android:layout_width">fill_parent</item>
    <item name="android:layout_height">fill_parent</item>
</style>
<style name="Fill.Height" >
    <item name="android:orientation">vertical</item>
</style>
```

* Android上的应用切换按钮列出的其实不是应用而是Task，所以你会看到有的应用在切换视图里有多个任务。如果你的应用中有逻辑上相互独立的部分，或者想在多窗口环境下并排显示应用的两个不同部分，这种情况就适合多任务了。使用manifest属性(静态)或者 intent flags(动态)可以实现这一点,详见视频: http://v.youku.com/v_show/id_XMTU2ODk4NDg2NA==.html?f=26587294

<img src="https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/multy_task1.jpg" width = "50%" height="300px" /><img src="https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/multy_task2.jpg" width = "50%"  height="300px"/>

* 当app的theme用的是NoActionBar,但是在layout中仍然用到toolbar的时候,不要在style文件中加fitsSystemWindows属性,而是在用到toolbar的layout最外层加fitsSystemWindows,否则当你使用EditText,在小米手机上长按EditText调出系统粘贴功能的时候,粘贴的layout的布局会错位.

* 当WebView与ScrollView嵌套使用,并且WebView有字体放大缩小的功能时,当切换webview的字体后,webview的高度并不能很好的计算出来,这时候可以通过注入的方式,让js算出高度,经测试,这样是最可靠的,代码地址:http://blog.csdn.net/jys1115/article/details/43525979

* Context类中的createPackageContext(packageName, flags)方法，可用来获取指定包名应用程序的Context对象。

* TextView类的setKeyListener(KeyListener)方法；
其中DigitsKeyListener类，使用getInstance(String accepted)方法即可指定EditText可输入字符集；

* View类中的getLocationInWindow(int[])方法和getLocationOnScreen(int[])方法，获取View在窗口/屏幕中的位置；

* Context.getCacheDir() - 可以获取到app默认的缓存路径。

* StaticLayout 在自定义控件绘制文本的时候很有用。

* Android中的四大组件千万不要通过new的方式创建出来。

* 测试app的时候,我们大都想要将debug和release版本同时安装到手机里,可以通过在gradle中修改applicationid来实现:
```
android {
    buildTypes {
        debug {
            applicationIdSuffix '.debug'
            versionNameSuffix '-DEBUG'
        }
        release {
            //...
        }
    }
}
```

* 在大多数的登陆界面中，都提供了用户是否让密码可见的选项，Support Library 24.2.0 提供了官方的实现，TextInputLayout 中添加了 passwordToggleEnabled 属性来开启此功能，并且可以通过 passwordToggleDrawable 设置图标。(摘自:Android笔记的微博)

* 同样,在Support Library 24.2.0中增加RecyclerView 在快速滚动时的回调接口,SnapHelper是官方的一个实现OnFlingListener 的 一个抽象类,LinearSnapHelper 则是一个完整的实现.LinearSnapHelper默认实现的功能是类似ViewPager,在滚动结束后,会选择列表某一条居中展示(这里有开始位置展示,或者结束位置显示[点我](https://github.com/rubensousa/RecyclerViewSnap)).例如:
```
    LinearLayoutManager linearLayoutManager = new LinearLayoutManager(getContext(), LinearLayoutManager.HORIZONTAL, false);
    recyclerView.setLayoutManager(linearLayoutManager);
    LinearSnapHelper snapHelper = new LinearSnapHelper();
    snapHelper.attachToRecyclerView(recyclerView);
```

* Android中推荐使用的数据结构 :
```
ArrayMap<K,V> in place of HashMap<K,V> 
ArraySet<K,V> in place of HashSet<K,V> 
SparseArray<V> in place of HashMap<Integer,V> 
SparseBooleanArray in place of HashMap<Integer,Boolean> 
SparseIntArray in place of HashMap<Integer,Integer>  
SparseLongArray in place of HashMap<Integer,Long>  
LongSparseArray<V> in place of HashMap<Long,V>
```

* 生成GUID(由于java中只能生成UUID,所以这里要转换一下):
```
    return UUID.randomUUID().toString().toUpperCase().replaceAll("-", "");
```

* 业务场景：需要定时后台扫描数据库，上传本地照片至云端，定时任务采用何种模式: 
1.Handler或者Timer定时一般为秒级别的任务,Timer会启动额外线程，而Handler可以不用。
2.无论是Handler还是Timer都需要依赖于进程存活 
3.利用Handler实现定时任务的类:HandlerTimer 
4.如果时间较长，则需要使用AlarmManager 
5.另外，我们对于这种业务应该优先考虑是否可以基于事件通知。
6.如果是加入媒体库的文件，我们可以使用registerContentObserver监听媒体库文件变化。

* 把Activity作为参数传给一个静态方法,会影响这个Activity的正常销毁吗?
1.内存泄露与方法是否是静态与否无关，与内部的方法体实现有关系。
2.内存泄露可以简单理解成：生命周期长的对象不正确持有了持有了生命周期短的对象，导致生命周期短的对象无法回收。
3.比如Activity实例被Application对象持有，Activity实例被静态变量持有。

* 在assets文件夹下存放单个文件的大小不能超过1M，如果读取超过1M的文件会报 "Data exceeds UNCOMPRESS_DATA_MAX (1314625 vs 1048576)" 的IOException。如果一定要存储，可以分割文件，再去合并文件

* 在Android library中不能使用switch-case语句访问资源ID，因为case分支后面跟的参数必须是常数，而library中的每一个资源ID都没有被声明为final。

* 当前Activity的onPause方法执行结束后才会执行下一个Activity的onCreate方法，所以在onPause方法中不适合做耗时较长的工作，这会影响到页面之间的跳转效率；

* 不要通过Bundle传递大块的数据，否则会报TransactionTooLargeException异常

* （AnimationDrawable在Android5.0及以上的版本已有明显的优化）尽量不要使用AnimationDrawable，它在初始化的时候就将所有图片加载到内存中，特别占内存，并且还不能释放，释放之后下次进入再次加载时会报错；

* .9图不能通过tinypng压缩，不然会有问题；

* genymotion模拟器快是因为它是基于x86架构的，如果你的应用中用到了so，但没有x86架构的so，只能放弃使用它；Android Studio的模拟器也一样；

* 使用Toast时，建议定义一个全局的Toast对象，这样可以避免连续显示Toast时不能取消上一次Toast消息的情况（如果你有连续弹出Toast的情况，避免使用Toast.makeText）；

* 尽量避免给window和Activity同时都设置了背景，这样会造成过渡绘制，可以通过在给Activity设置主题时，去掉windowBackground背景的方式减少一层过渡绘制，有时候为了避免进入Activity时会黑屏或者白屏（和主题有关），会在给Activity设置主题的时候给window设置背景，如果这种情况下给Activity也设置了背景，是会增加一倍内存的：
```
<item name="android:windowBackground">@null</item>
```

* 设置中更改字体为特大之类的会影响到app的字体样式，解决方法有: 1.将所有字体使用的单位换成dp，不再使用sp.这样不是很靠谱，并不是所有人都能做到。
2.
```
 Configuration configuration = getResources().getConfiguration();
  configuration.fontScale = (float) 1; 
  //0.85 小, 1 标准大小, 1.15 大，1.3 超大 ，1.45 特大 
  DisplayMetrics metrics = new DisplayMetrics();
  getWindowManager().getDefaultDisplay().getMetrics(metrics); 
  metrics.scaledDensity = configuration.fontScale * metrics.density;
  getBaseContext().getResources().updateConfiguration(configuration, metrics); 
  //（ps:dialog popupwindow 除外,这两种需要在控件中重新设置fontScale)
```

* Android中新引入的替代枚举的注解有IntDef和StringDef,这里以IntDef做例子说明一下.
```
public class Colors {
    @IntDef({RED, GREEN, YELLOW})
    //声明必要的int常量,使用@IntDef修饰LightColors,参数设置为待枚举的集合
    @Retention(RetentionPolicy.SOURCE)
    //使用@Retention(RetentionPolicy.SOURCE)指定注解仅存在与源码中,不加入到class文件中
    public @interface LightColors{}
    //声明一个注解为LightColors
    public static final int RED = 0;
    public static final int GREEN = 1;
    public static final int YELLOW = 2;
}
//用法
private void setColor(@Colors.LightColors int color) {
        Log.d("MainActivity", "setColor color=" + color);
}
//调用的该方法的时候
setColor(Colors.GREEN);
```

* PathInterpolatorCompat 很方便的使用它来创建各种插值曲线，举个非常简单的例子：
```
Path path = new Path();
path.cubicTo(0.2f, 0f, 0.1f, 1f, 0.5f, 1f);
path.lineTo(1f, 1f);
ObjectAnimator animator = ObjectAnimator.ofFloat(view, View.TRANSLATION_X, 500);
animator.setInterpolator(PathInterpolatorCompat.create(path));
animator.start();
```

* 检测当前网络能否访问远程服务器(国内通过ping百度来检测)
```
public static boolean isNetWorkAvailable(final Context context) {
        try {
            Runtime runtime = Runtime.getRuntime();
            Process pingProcess = runtime.exec("/system/bin/ping -c 1 www.baidu.com");
            int exitCode = pingProcess.waitFor(); //0 代表连通，2代表不通
            return (exitCode == 0);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return false;
    }
```


* 拦截系统返回键(onBackPressed())，使App不退出，而是进入后台运行
```
@Override
  public void onBackPressed() {
    moveTaskToBack(false);
  }
```

* view.performClick() 自动调用 View 点击事件。通常按钮等控件只有在用户点击时才能触发其点击事件，该方法可以由某些特殊条件触发模拟用户点击行为。类似的还有 performLongClick() 方法。

* Linkify.addLinks() 通过 android:autoLink 属性可以为其添加诸如 web、phone 等固定模版的超链接点击事件。但毕竟系统模版有限，而利用 Linkify.addLinks() 方法可以添加一些应用内自定义模版，比如新浪微博中的 "@XXX" 格式的超链接跳转等，都可以通过自定义正则表达式来匹配处理。

* getWindow().addFlags(WindowManager.LayoutParams.FLAG_SECURE) 设置安全窗口，禁用系统截屏。防止 App 中的一些界面被截屏，并显示在其他设备中造成信息泄漏。（常见手机设备系统截屏操作方式为：同时按下电源键和音量键。）

* activity生命周期([Ref Link](https://www.bignerdranch.com/blog/android-activity-lifecycle-onStop/))
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/activityStateDiagram.jpeg)

* ![](https://github.com/jiang111/awesome-android-tips/raw/master/img/complete_activity_fragment_lifecycle.png)

* RecyclerView 调用notifyItem()的时候会有默认的动画,可以通过调用((SimpleItemAnimator)recyclerView.getItemAnimator()).setSupportsChangeAnimations(false);来去掉默认动画.以防止出现闪屏的问题

* Toolbar 使用的主题如果 parent="ThemeOverlay.AppCompat.Light"，只要改一下 <item name="colorControlNormal">@color/white</item> 就可以使 OverflowButton 变为白色，同时点击它展开的菜单背景也可以是白的

*  Android View的生命周期示例图样。来自G+ +Arpit Mathur
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/view_lifecycle.jpg)

* 当需要从资源文件中获取 html 并展示时，使用 Resource#getText() 而不是 Resource#getString()。当需要动态显示 HTML 时，使用 Html.fromHtml() [请看这里](http://saket.me/html-tags-textview/)

* JAVA中时间String转Timestamp
```
try {
	DateFormat format = new SimpleDateFormat("yyyy-MM-dd");
	format.setLenient(false);
	//要转换字符串 str_test  自定义的格式为 yyyy-mm-dd，可以改成你需要的格式
	String str_test ="2011-04-24";
	Timestamp ts = new Timestamp(format.parse(str_test).getTime());
	System.out.println(ts.toString());
} catch (ParseException e) {
e.printStackTrace();
}
```

* 当Activity 继承 FragmentActivity的时候，调用startActivityForResult方法中传递的requestCode范围应该在0-65535范围内，否则会报"Can only use lower 16 bits for requestCode"异常。

* Android有一个隐藏的类可以判断文本输入框内输入的是不是表情，这个类就是 android.text.Emoji类，它的isEmoji(int codePoint)方法可以直接判断出来是不是表情。这个类是隐藏的，如果要用到则需要将它拷贝出来。

*  布局中不得不使用ViewGroup 多重嵌套时，不要使用LinearLayout 嵌套，改用RelativeLayout，可以有效降低嵌套数。

*  不能使用ScrollView 包裹ListView/GridView/ExpandableListVIew;因为这样会把ListView 的所有Item 都加载到内存中，要消耗巨大的内存和cpu 去绘制图面。

*  不要通过Intent 在Android 基础组件之间传递大数据（binder transaction缓存为1MB），可能导致OOM。

*  在Application 的业务初始化代码加入进程判断，确保只在自己需要的进程初始化。特别是后台进程减少不必要的业务初始化。

*  将android:allowbackup 属性设置为false，防止adb backup 导出数据。

* 除非min API level >=17，请注意addJavascriptInterface 的使用
```
说明：
API level>=17，允许js 被调用的函数必须以@JavascriptInterface 进行注解，因此不受影响； 对于API level < 17，尽量不要使用addJavascriptInterface，如果一定要用，那么：
1) 使用https 协议加载URL，使用证书校验，防止访问的页面被篡改挂马；
2) 对加载URL 做白名单过滤、完整性校验等防止访问的页面被篡改；
3) 如果加载本地html,应该会HTML 内置在APK 中，以及对HTML 页面进行完整性校验。

```

* 如何动态修改AlertDialog的Button样式,
```
//监听Dialog的setOnShowListener方法
dialog.setOnShowListener(new DialogInterface.OnShowListener() {
    @Override
    public void onShow(final DialogInterface dialog) {
      Button negativeButton = ((AlertDialog)dialog).getButton(DialogInterface.BUTTON_NEGATIVE);
      Button positiveButton = ((AlertDialog)dialog).getButton(DialogInterface.BUTTON_POSITIVE);
      negativeButton.invalidate();
      positiveButton.invalidate();
    }
});
dialog.show();

```

* 升级 RecycleView 版本到 25.1.0 及以上使用 Prefetch 功能，可[参考 RecyclerView 数据预取](https://juejin.im/entry/58a3f4f62f301e0069908d8f)。

* 如果 Item 高度是固定的话，可以使用 RecyclerView.setHasFixedSize(true); 来避免 requestLayout 浪费资源；

* 如果不要求动画，可以通过 ((SimpleItemAnimator) rv.getItemAnimator()).setSupportsChangeAnimations(false); 把默认动画关闭来提升效率。

* 通过 RecycleView.setItemViewCacheSize(size); 来加大 RecyclerView 的缓存，用空间换时间来提高滚动的流畅性。

* 如果多个 RecycledView 的 Adapter 是一样的，比如嵌套的 RecyclerView 中存在一样的 Adapter，可以通过设置 RecyclerView.setRecycledViewPool(pool); 来共用一个 RecycledViewPool。

* 对 ItemView 设置监听器，不要对每个 Item 都调用 addXxListener，应该大家公用一个 XxListener，根据 ID 来进行不同的操作，优化了对象的频繁创建带来的资源消耗。

* 通过 getExtraLayoutSpace 来增加 RecyclerView 预留的额外空间（显示范围之外，应该额外缓存的空间），如下所示
```
new LinearLayoutManager(this) {
    @Override
    protected int getExtraLayoutSpace(RecyclerView.State state) {
        return size;
    }
};

```

* WebView 在 API 21之后,写Cookie的时候默认禁止了跨域写cookie,需要通过代码,来设置开启跨域请求
```
 if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
            CookieManager.getInstance().setAcceptThirdPartyCookies(WebView, true);
        }
```

* 使用IdleHandler,替代Handler.postDelay(),IdleHandler是在我们的onResume和measure, layout, draw这么message执行结束之后， 提供了他们执行完毕的回调. [看这里](https://wetest.qq.com/lab/view/352.html)
```
 Looper.myQueue().addIdleHandler(new MessageQueue.IdleHandler() {
            @Override
            public boolean queueIdle() {
                //TODO...
                return false;
            }
        });
```


* 在Multidex分包的时候,如果主dex过大, 5.0以下的机型可能会出现multidex installation failure错误,这时需要让主dex方法数小一点.,配置方法

```
配置正常的multiDex库之后,在主模块的gradle文件添加如下代码:
Android{
     ...//其他代码
    dexOptions {
        javaMaxHeapSize "4g"
        preDexLibraries = false
        additionalParameters += '--multi-dex'
        additionalParameters += '--set-max-idx-number=35000'//(35000可根据自己的需求更改)来适配4.0-4.4一些低端机型，因为拆分的dex太大，这些低端机型加载不了dex
        additionalParameters += '--minimal-main-dex'
    }

}
```

注意:在gradle版本3.1.0之后dex编译采用D8,可能会导致这种分包不成功。将gradle的版本降到3.0.0之后，分包成功。另外也可以采用gradle3.1.0或者以上的版本，然后将项目的gradle配置为android.enableD8=false //暂时关闭 即可

* 高版本android中，可以使用Application启动Activity并且不设置FLAG，但在低版本中必须要设置FLAG,所以建议大家使用application的context去startActivity的时候添加FLAG_ACTIVITY_NEW_TASK

* 不要滥用
```
<item name="android:windowIsTranslucent">true</item>
```
属性,切勿为app设置该属性,而仅针对具体的activity进行设置.公司有位开发为整个app设置了该属性,我们有个签名的横屏页面,其他是强制竖屏页面,有个需求是进入该竖屏页面后某些特殊原因需要自动跳转到签名页面,而跳转到横屏页面后导致整个app的所有页面生命周期全部重新走了一遍,该签名页面无限循环打开.


* 当你在多module中使用了多个三方库,而这些三方库使用了多个版本的Recyclerview,我们可以通过exclude group: 'com.android.support', module: 'recyclerview-v7' 来实现使用项目中的版本,但是这样造成的问题是每添加一个库就得写一下exclude,这样很不友好,而gradle为我们提供了依赖替换规则.
如下代码实现了全局替换recyclerview的版本
```
configurations.all {
    resolutionStrategy.eachDependency { DependencyResolveDetails details ->
        def requested = details.requested
        if (requested.group == 'com.android.support') {
            if (requested.name.startsWith("recyclerview-v7")) {
                details.useVersion "28.0.0"
            }
        }
    }
}

```
当然,依赖替换规则还允许我们在本地库和远程库之间进行切换.
```
configurations.all {
    resolutionStrategy.dependencySubstitution {
        if (useLocal) { //如果使用本地仓库,系统将会把org.utils:api依赖替换为本地api的project
            substitute module("org.utils:api") because "we work with the unreleased development version" with project(":api")
        }
    }
}
```

* Android library中的混淆需要使用consumerProguardFiles来配置,而不是proguardFiles


* ViewPager结合SwipeRefreshLayout的时候,建议对ViewPager添加如下代码:
```
viewpager.addOnPageChangeListener(new ViewPager.OnPageChangeListener() {
            @Override
            public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {

            }

            @Override
            public void onPageSelected(int position) {

            }

            @Override
            public void onPageScrollStateChanged(int state) {
	    //禁止swipeRefreshLayout拿上下滑动的手势
                swipeRefreshLayout.setEnabled(state == ViewPager.SCROLL_STATE_IDLE);

            }
        });
```


#### 摘自[如下地址](https://github.com/jiang111/awesome-android-tips/blob/master/Authors.md)


### 捐赠
如果您觉得本项目对您有帮助，欢迎请作者一杯咖啡 <br /><br />
![](https://raw.githubusercontent.com/jiang111/RxJavaApp/master/qrcode/wechat_alipay.png)

### License

    Copyright 2018 NewTab

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
