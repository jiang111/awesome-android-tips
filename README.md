# awesome-android-tips
Android tips

这里收集了大家常用的一些Android代码,内容摘自网络，部分原文地址在最下方。如有错误欢迎指正

>* setBackgroundResource(0) 可以移除 View 的背景色

>* Resources.getSystem().getDisplayMetrics().density 可以不用 Context 也能获取屏幕密度哦

>* 通过重载 ViewGroup 的 dispatchDraw 可以实现一个简单的蒙版效果。 例如下拉刷新时，可以在 contentView 上加一层遮罩。 canvas.drawRect(0, mContentView.getTranslationY(), getWidth(), getHeight(), mMaskPaint);

>* new 出来的 View 可以用 View.generateViewId() 生成 id，系统保证唯一。

>* 使用 GridView时 android:padding 和 android:clipToPadding="false" 配合使用效果更好哦。

>* 在布局文件中，如果只是为了占位，可以用 Space 来取代 View。 最棒的一点是Space可以跳过 Draw 这个过程。

>* applyDimension(int unit, float value, DisplayMetrics metrics) 方便dp, px, sp 之间的转换。

>* Activity.startActivities() 这个方法最直接的理解就是使用intent开启多个Activity

>* TextUtils.isEmpty() 如果传入的String 为NULL或者Length为0的话就返回 true。

>* Html.fromHtml() 如果你对Html熟悉的话，可以很迅速通过这个方法处理一些富文本操作。比如超链接和图文排版等处理。

>* TextView.setError() 设置文本框错误提醒

>* Build.VERSION_CODES 有些时候我们的app需要根据不同的SDK版本进行执行不同的操作

>* PhoneNumberUtils.convertKeypadLettersToDigits 这个方法简单粗暴，会将输入的字母根据键盘上的映射转换为数字。

>* ArgbEvaluator ArgbEvaluator.evaluate(float fraction, Object startValue, Object endValue);根据一个起始颜色值和一个结束颜色值以及一个偏移量生成一个新的颜色，分分钟实现类似于微信底部栏滑动颜色渐变。

>* ValueAnimator.reverse() 顺畅的取消动画效果

>* DateUtils.formatDateTime()) 这个方法可以输出相应格式化的时间或者日期

>* Formatter.formatFileSize() 这个方法会格式化数据的大小，根据输入的字节大小，返回 B KB MB GB 等等（最大支持到 PB）。当然要注意的是输入的最大值是 Long.MAX_VALUE.

>* TypedValue.applyDimension() 首先这个方法我们可以用来对sp dp 和 px 之间的单位转换。应该是有不少同学用过的

>* Pair.create()  这个类 可以用来存储存储一”组”数据。但不是key和value的关系。

>* SparseArray 目前有很多地方从性能优化方说使用SparseArray来替换hashMap，来节省内存，提高性能。

>* Linkify.addLinks() 这个类可以更方便的为文本添加超链接。

>* android.text.Spanned

>* ThumbnailUtils 这个类主要是用来处理缩略图相关的，有过这方面需求的，应该是用过这个类的。

>* Bitmap.extractAlpha() 返回一个新的位图，该位图从源图中捕获了alpha值。这个方法可能跟Canvas.drawBitmap()一起被画，颜色值从传递过来的画笔中获取。

>* 模块间有消息需要传递时，使用LocalBroadcastManager替代Listener进行模块解耦。除了解耦，这样发送消息和执行消息差一个线程循环，可以减小方法的调用链，我这就碰到一次方法调用链太长导致StackOverflow的问题。

>* 静态变量不要直接或者间接引用Activity、Service等。这会使用Activity以及它所引用的所有对象无法释放，然后，用户操作时间一长，内存就会狂升。

>* Handler机制有一个特点是不会随着Activity、Service的生命周期结束而结束。也就是说，如果你Post了一个Delay的Runnable，然后在Runnable执行之前退出了Activity，Runnable到时间之后还是要执行的。如果Runnable里面包含更新View的操作，程序崩溃了。

>* 不少人在子线程中更新View时喜欢使用Context.runOnUiThread，这个方法有个缺点，就是一但Context生命周期结束，比如Activity已经销毁时，一调用就会崩溃。

>* SharedPreferences.Editor.commit这个方法是同步的，一直到把数据同步到Flash上面之后才会返回，由IO操作的不可控，尽量使用apply方法代替。apply只在API Level>=9才会支持，需要做兼容。

>* PackageManager.getInstalledPackages这个方法经常使用，你可能不知道，当获取的结果数量比较多的时候，在某些机型上面调用它花费的时间可能秒级的，所以尽量在子线程中使用。另外，如果结果太多，超过系统设置的Binder数据最大传输量的上限，则会发生TransactionException，如果你使用这个方法获取机器上的己安装应用列表，最好做一下预防。

>* 如果使用Context.startActivity启动外部应用，最好做一下异常预防，因为寻找不到对应的应用时，会抛出异常。如果你要打开的是应用内的Activity，不防使用显式Intent，这样能提高系统搜索目标Activity的效率。

>* Application的生命周期就是进程的生命周期。只有进程被干掉时，Application才会销毁。哪怕是没有Activity、Service在运行，Application也会存在。所以，为了减少内存压力，尽量不要在Application里面引用大对象、Context等。

>* getWindow().setLayout(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT);设置全屏方法一定要在setContentView之后

>* viewpager 的 setCurrentItem 一定要在 setAdapter 方法之后调用才会有效果.

>* 判断手机是不是飞行模式  boolean isEnabled = Settings.System.getInt(context.getContentResolver(), Settings.System.AIRPLANE_MODE_ON, 0) == 1;

>* TabLayout 修改字体的方法
官方的 TabLayout 没有提供修改 TextView size 的方法，可以新建一个 style CustomTabLayoutTextAppearance 继承 TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse ，然后增加 item ，设置 android:textAllCaps 为 true ，再设置 android:textSize 为你想设置的大小。
![](http://ww1.sinaimg.cn/large/640f03afjw1ex0t17aj67j20uk0580uf.jpg)
再在 TabLayout 的布局文件里设置 app:tabTextAppearance="@style/CustomTabLayoutTextAppearance" 即可。
![](http://ww1.sinaimg.cn/large/640f03afjw1ex0t1gub93j20ru0a477q.jpg)

>* 遍历HashMap的最佳方法
```java
public static void printMap(Map mp) {
    Iterator it = mp.entrySet().iterator();
    while (it.hasNext()) {
        Map.Entry pair = (Map.Entry)it.next();
        System.out.println(pair.getKey() + " = " + pair.getValue());
        it.remove(); // avoids a ConcurrentModificationException
    }
}
```

>* 使用Java在一个区间内产生随机整数数
```java
public static int randInt(int min, int max) {
    Random rand;
    int randomNum = rand.nextInt((max - min) + 1) + min;
    return randomNum;
}
```


>* 如果子类实现Serializable接口而父类未实现时，父类不会被序列化，但此时父类必须有个无参构造方法，否则会抛InvalidClassException异常。

>* transient关键字修饰变量可以限制序列化。

>* 当使用JakeWharton的TabPageIndicator时，如果需要先做一些耗时的操作，然后再展示TabPageIndicator的话，需要先设置mIndirector.setVisibility(View.GONE);然后耗时任务结束以后再mIndirector.setVisibility(View.VISIBLE);否则会报错


>* 类继承之间的调用顺序 父类static成员 -> 子类static成员 -> 父类普通成员初始化和初始化块 -> 父类构造方法 -> 子类普通成员初始化和初始化块 -> 子类构造方法

>* 华为手机无法显示log解决方案,.拨号界面输入*#*#2846579#*#* Service menu will appear.Go to "ProjectMenu" -> "Background Setting" -> "Log Setting"Open "Log switch" and set it to ON.Open "Log level setting" and set the log level you wish.

>* 后台service经常因为重启之类的出现onStartCommand()中的Intent传递的参数为null， 通过在onStartCommand()中的返回值改成return super.onStartCommand(intent, Service.START_REDELIVER_INTENT, startId); 可以解决问题。下面介绍几个flag的意思<br />

| flag        | 解释       | 
| ------------- |:-------------:|
| START_STICKY | 如果service进程被kill掉，保留service的状态为开始状态，但不保留递送的intent对象。随后系统会尝试重新创建service，由于服务状态为开始状态，所以创建服务后一定会调用onStartCommand(Intent,int,int)方法。如果在此期间没有任何启动命令被传递到service，那么参数Intent将为null。 |
| START_NOT_STICKY | “非粘性的”。使用这个返回值时，如果在执行完onStartCommand后，服务被异常kill掉，系统不会自动重启该服务。 |
|START_REDELIVER_INTENT|重传Intent。使用这个返回值时，如果在执行完onStartCommand后，服务被异常kill掉，系统会自动重启该服务，并将Intent的值传入。|
|START_STICKY_COMPATIBILITY|START_STICKY的兼容版本，但不保证服务被kill后一定能重启。  |



####摘自如下地址：(部分地址)
>* http://oakzmm.com/2015/08/04/cool-Android-api/
>* http://oakzmm.com/2015/08/11/cool-Android-api-2/
>* http://weibo.com/liangfeizc?from=feed&loc=nickname











