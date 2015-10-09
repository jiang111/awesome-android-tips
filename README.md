# awesome-android-tips
Android tips

###1.


>* setBackgroundResource(0) 可以移除 View 的背景色

>* Resources.getSystem().getDisplayMetrics().density 可以不用 Context 也能获取屏幕密度哦

>* 通过重载 ViewGroup 的 dispatchDraw 可以实现一个简单的蒙版效果。 例如下拉刷新时，可以在 contentView 上加一层遮罩。 canvas.drawRect(0, mContentView.getTranslationY(), getWidth(), getHeight(), mMaskPaint);

>* new 出来的 View 可以用 View.generateViewId() 生成 id，系统保证唯一。

>* 使用 GridView时 android:padding 和 android:clipToPadding="false" 配合使用效果更好哦。

>* 在布局文件中，如果只是为了占位，可以用 Space 来取代 View。

>* applyDimension(int unit, float value, DisplayMetrics metrics) 方便dp, px, sp 之间的转换。

