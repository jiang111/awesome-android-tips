# awesome-android-tips
Android tips

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


####摘自如下地址： 

>* http://oakzmm.com/2015/08/04/cool-Android-api/
>* http://oakzmm.com/2015/08/11/cool-Android-api-2/
>* http://weibo.com/liangfeizc?from=feed&loc=nickname











