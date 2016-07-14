# awesome-android-tips
Android tips    

中文版:https://github.com/jiang111/awesome-android-tips

>* setBackgroundResource(0) can remove the background of View

>* Resources.getSystem().getDisplayMetrics().density can get the Screen density without the Context

>* overload ViewGroup `s dispatchDraw can implement a simple Mask effect; such as: when pull to refresh ,we can add mask in contentView 。source code: canvas.drawRect(0, mContentView.getTranslationY(), getWidth(), getHeight(), mMaskPaint);

>* we can use view.generateViewId() to generate a unique id.(API level 17)

>*  android:padding and android:clipToPadding="false"  is very useful with GridView.

>* in layout file. use Instead of View to Space ad a placeholder is a good idea, because Spcae can skip the process ondraw 
