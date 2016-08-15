
awesome-android-tips

中文版:https://github.com/jiang111/awesome-android-tips

this is some useful android tips.Most of the content by the google translation, if wrong, please correct me, thank you

>* setBackgroundResource(0) can remove the background of View

>* Resources.getSystem().getDisplayMetrics().density can get the Screen density without the Context

>* overload ViewGroup `s dispatchDraw can implement a simple 
Mask effect ; such as: when pull 2 refresh ,we can add mask in contentView 。source code: canvas.drawRect(0, mContentView.getTranslationY(), getWidth(), getHeight(), mMaskPaint);

>* we can use view.generateViewId() to generate a unique id.(API >= 17)

>*  android:padding and android:clipToPadding="false"  is very useful when we use GridView.

>* in layout file. use Instead of View to Space ad a placeholder is a good idea, because Spcae can skip the process ondraw 

>* TypedValue.applyDimension(int unit, float value, DisplayMetrics metrics) is very convenient to do the conversion between dp,px,sp


>* Activity.startActivities() can start multiple activities

>* TextUtils.isEmpty() if the string is null or of length 0 ,return true

>* Html.fromHtml() is very convenient to deal with some rich text manipulation

>* TextView.setError() can set a error reminder  with text box

>* use Build.VERSION_CODES can obtain various versions of android in version_code

>* PhoneNumberUtils.convertKeypadLettersToDigits ,Enter the letters on the keyboard according to the mapping conversion to digital.

>* ArgbEvaluator ArgbEvaluator.evaluate(float fraction, Object startValue, Object endValue); Generate a new color based on the color values of a starting and an ending color value and an offset quickly.

>* ValueAnimator.reverse(); cancel animation smoothly.

>* DateUtils.formatDateTime()); Corresponding output formatted time or date.

>* Formatter.formatFileSize(); The size of the formatted data, based on the input size in bytes, returns B KB MB GB, etc. (maximum support to PB). It is noted that the maximum value of the input is Long.MAX_VALUE.

>* Pair; this class can be used to store to store a "set" of data. But not the relationship between the key and value.

>* Instead of HashMap to SparseArray can Save memory and improve performance.

>* Linkify.addLinks(); Easily add hyperlinks to text.

>* ThumbnailUtils; This class is mainly used to deal with associated thumbnails

>* Bitmap.extractAlpha ();Returns a new Bitmap, capture the original image alpha value. Sometimes we need to dynamically modify a background image element do not want to use more than one picture when, by this method, combined with Canvas and Paint dynamically modify a solid Bitmap color.

>* There need to pass messages between modules, use LocalBroadcastManager replace the module Listener decoupling. In addition to decoupling, and send messages, and perform message difference between a thread loop, you can reduce the call chain method, I'll run into one method call chain is too long cause StackOverflow questions.

>* Static variables do not directly or indirectly reference Activity, Service and so on. It will use the Activity and all the objects it refers can not be released, and then, the user operates over time, the memory will be spiraling.

>* Handler has a characteristic mechanism is not with the end of Activity, Service life cycle ends. That is, if you a Post Delay of Runnable, then withdrew before the Runnable implementation of Activity, Runnable to later time or to be executed. If Runnable which contains updates View operation, the program crashes.

>* Many people in the sub update View thread like to use Context.runOnUiThread, but there is a drawback,  such a Context end of life, such as when Activity have been destroyed, it will collapse.

>* SharedPreferences.Editor.commit This method is synchronous, synchronized to the data until after the Flash above will return by the IO operation, it is uncontrollable, try to apply the method to use instead. apply only in the API Level> = 9 will support, you need to do is compatible. However, the latest support v4 package ready for us to deal with, the use of SharedPreferencesCompat.EditorCompat.getInstance (). Apply (editor) to complete.


>* PackageManager.getInstalledPackages This method is often used. You may not know, when the number of results obtained more time, in some models above the call time it may take several seconds, so try to use in the sub-thread. In addition, if too many results, limit Binder data exceeds system set the maximum amount of transmission can occur TransactionException, if you use this method to get a list of applications already installed on the machine, it is best to do some prevention.

>* If Context.startActivity launch an external application, it is best to do something abnormal prevention, because find no corresponding application, it will throw an exception. If you want to open an Activity within the application, consider using explicit Intent, this can improve the efficiency of the system Activity search target.

>* Application life cycle is the process life cycle. Only when the process is to kill, Application will be destroyed. Even if there is no Activity, Service is running, Application will be present. Therefore, in order to reduce memory pressure, try not referenced in the Application Large objects, Context and the like.

>* getWindow().setLayout(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT); Be sure to call after setContentView

>* boolean isEnabled = Settings.System.getInt(context.getContentResolver(), Settings.System.AIRPLANE_MODE_ON, 0) == 1; Analyzing phone is not flight mode

>* The official did not provide TabLayout modify TextView size method, you can create a style CustomTabLayoutTextAppearance inheritance TextAppearance.AppCompat.Widget.ActionBar.Title.Inverse, then increase the item, set the android: textAllCaps is true, then set the android: textSize you want to set size.
![](https://camo.githubusercontent.com/4f6cb736aab110981320e0350a9677f8acae3803/687474703a2f2f7777312e73696e61696d672e636e2f6c617267652f36343066303361666a7731657830743137616a36376a3230756b3035383075662e6a7067)
Then set the app in TabLayout layout file: tabTextAppearance = "@ style / CustomTabLayoutTextAppearance" can be.
![](https://camo.githubusercontent.com/d174f31172b7390ac02f97030bf916e10b9d5e8f/687474703a2f2f7777312e73696e61696d672e636e2f6c617267652f36343066303361666a7731657830743167756239336a323072753061343737712e6a7067)

>* The best way to traverse the HashMap

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

>* Use Java generate random integer number within a range

```java
public static int randInt(int min, int max) {
    Random rand;
    int randomNum = rand.nextInt((max - min) + 1) + min;
    return randomNum;
}
```

>* If the child class implements Serializable interface and the parent class does not implement, the parent will not be serialized, but this time the parent class must have a constructor with no arguments, otherwise it will throw an exception InvalidClassException.

>* transient keyword modified variables can limit serialized.

>* When used TabPageIndicator, if you need to do some time-consuming operation, and then display TabPageIndicator then you need to set mIndirector.setVisibility (View.GONE); then mIndirector.setVisibility after the end of time-consuming tasks (View.VISIBLE) ; otherwise it will error

>* Calling sequence parent class static member class inheritance, between -> subclass static member -> ordinary members of the parent class initialization and initialization block -> parent class constructor -> subclass ordinary member initialization and initialization block -> subclass constructors

>* Huawei cell phone can not display log solutions. dialing interface input (* # * # 2846579 # * # *) Service menu will appear.Go to "ProjectMenu" -.> "Background Setting" -> "Log Setting" Open "Log switch" and set it to ON.Open "log level setting" and set the log level you wish.

>* Background service often because () the parameters passed Intent appear onStartCommand restart such as null, by onStartCommand () return value changed to return super.onStartCommand (intent, Service.START_REDELIVER_INTENT, startId); can solve the problem. Here are a few flag meaning

>* | flag        | 解释       |
| ------------- |:-------------:|
| START_STICKY | If the process is to kill off the service, reservations service status start state, but does not retain the delivery of intent objects. The system then attempts to re-create the service, since the service started state status, so the service will create a call onStartCommand (Intent, int, int) method. If during this time there is no start command is transmitted to the service, it will be null parameter Intent。 |
| START_NOT_STICKY | "Non-tacky." When using this return value, if onStartCommand After execution, the service is abnormal kill off, the system does not automatically restart the service。 |
|START_REDELIVER_INTENT|Retransmission Intent. When using this return value, if onStartCommand After execution, the service is abnormal kill off, the system will automatically restart the service, value and incoming Intent。|
|START_STICKY_COMPATIBILITY|START_STICKY compatible version, but does not guarantee the service is restarted after the kill。  |

>* Can not show PopupWindow Activity and Dialog when not fully display

>* Between multiple processes do not share data with SharedPreferences, although (MODE_MULTI_PROCESS), but is very unstable

>* Sometimes you can not use the Application Context, or will be error (such as start Activity, display Dialog, etc.)
![](https://camo.githubusercontent.com/569dbb708117e17ec54db210ccafab96b06a1899/68747470733a2f2f706963332e7a68696d672e636f6d2f65336633323336636264393663363963646561313064303134626163626561655f622e706e67)
*Note: NO attention to see some added some figures, in fact, these are from the ability for YES, NO, but why is it? Explained one by one below: 1. Digital 1: Start Activity in these classes is possible, but you need to create a new task, generally not recommended; 2. Digital 2: In these classes to layout inflate is legal, but will use the system default theme style, if you customize some styles may not be used; 3. the number 3: is null allow the Receiver, in version 4.2 or above for obtaining the current sticky broadcast value. (Can ignore); 4. ContentProvider, BroadcastReceiver reason in the above table, because its internal process has a context for use.

>* Android theme prudent use transparent, transparent theme will cause a lot of problems, such as: if the new Activity using a transparent theme, then the current Activity of onStop method is never called; press the Home key to set the theme of the Activity transparent interface, the may cause the refresh is not clean; transparent theme into the theme of the interface will be significantly delayed

>* Do non-UI thread initialization ViewStub, because it will return null

>* Try not to cache data through the Application, which is unstable

>* Huawei phone can not turn on USB debugging problems,
Plugged data cable, dial-up interface ## 2,846,579 ## input into the engineering model
projectmenu → 3 → 4USB background set the port configuration → Balong debug mode, click OK
Do not pull cord exit engineering mode, direct restart the phone, the computer displays a removable disk (if still does not appear, repeat steps 1 and 2)
This is the method the computer using the phone's removable disk USB debugging closed the case, the use of drop-down menu usb option is also back.

>* When android listview contents of the soft keyboard is blocked, setting listview when adding android: transcriptMode = "normal"

>* TextUtils is a very useful tools, it can turn into a List string, comma-delimited String string, cut List, respectively, can be used TextUtils the join and split method. If you want to go heavy on the List, you can use Collection of frequency method.

>* Call moveTaskToBack (boolean non Root) method in activity to the activity retreated to the background, attention is not finish () to exit.

>* activity in runOnUiThrea (Runnable action) method can return directly to the main thread

>* listview there footerDividersEnabled and headerDividersEnabled method to set the top and bottom listview divide, but make sure you set the headview and footview will have effect

>* Throwable class getStackTrace () method, according to this method can be invoked layer by layer address of the function, which returns a value of StackTraceElement [];

>* StackTraceElement class, four methods getClassName (), getFileName (), getLineNumber (), getMethodName () is very useful when debugging Print Log;

>* UncaughtExceptionHandler the interface, even the best code exception is inevitable, you can use this interface with the aftermath of an uncaught exception

>* Resources class getIdentifier (name, defType, defPackage) method to get an ID based on the resource name, often used when doing UI;

>* isShown method in view only when the view itself and all of its ancestors are visible, isShown () does not return TRUE.
And usually we call if (view.getVisibility () == View.VISIBLE) view themselves not just be on the visibility of the ancestors of judgment.

>*Arrays class set of tools on the method of operation of the array: binarySearch (), asList (), equals (), sort (), toString (), copyOfRange (), etc; Collections class set of tools on the collection method of operation
: sort (), reverse (), etc;

>* TextView class append (CharSequence) method, add text.
Some special text directly connected will become String;

>* TextView class append (CharSequence) method, add text.
Some special text directly connected will become String;

>* TextView class setTransformationMethod (TransformationMethod) method can be used to achieve the "Show password" feature

>* PageTransformer interface used to customize the page switching animation ViewPager with setPageTransformer (boolean, PageTransformer) method to set up;

>* apache package offers a series of jar: commons-lang.jar, commons-collections.jar, commons-beanutils.jar etc., there may be many ways you have used dozens of hundreds of lines of code before, but perhaps efficiency much worse, such as: ArrayUtils, StringUtils ......;

>* ActivityLifecycleCallbacks interface for monitoring the status of each change in the Application Activity class!  [article](http://mp.weixin.qq.com/s?__biz=MzA3ODkzNzM3NQ==&mid=401277907&idx=1&sn=0b2246f5178292596fc3a8295283359c#rd)

>* ActionBar.hide () /. Show () As the name suggests, hide and show ActionBar, gracefully between full screen and with Actionbar conversion.

>* SystemClock.sleep () method to ensure that a certain period of sleep when it is convenient, I usually used for debug and simulate network delay.

>* UrlQuerySanitizer-- Use this tool to facilitate the URL to be checked.

>* ActivityOptions - easily define two animated Activity handover.
ActivityOptionsCompat can be solved using an older version compatibility issues.

>* getParent () requestDisallowInterceptTouchEvent (true);. deprive the parent view for touch event handling right, with who knows who.

>* HandlerThread, instead of constantly opening new Thread subthreads repeated physical writing.

>* IntentService, an own die after the work was done and we do not need to manage the child thread Service

>* Executors newSingleThreadExecutor (); This is the java, and did not know it before, he spent a lot of effort to study the single-threaded task queue implementation of the order

>* android: animateLayoutChanges = "true", LinearLayout added View animation approach, supported by setLayoutTransition () Custom Animation.

>* AsyncQueryHandler, if you do system development tools, such as contacts SMS and other aids, and certainly inevitable ContentProvider deal if the large amount of data is not the case, just do, if the next large amount of data, the understanding of this class is
necessary to note that this stuff eat exception ..

>* ViewFlipper, view of multiple switching (cycling), customizable animation effects, and can specify the animation for a single switch.

>* android util package Pair class can easily be used to store a "set" of data.
Note that not key value

>* android: descendantFocusability, ListView CheckBox and other elements of the item in focus grab lead item can not respond to a click event, in addition to the corresponding element is set focusable, simpler layout is the root item plus android: descendantFocusability = "blocksDescendants"

>* includeFontPadding = "false", TextView default padding up and down there is a certain, sometimes we may not need up and down this part of the blank, plus it can be.

>* Messenger, interview rooms are usually asked interprocess communication, under normal circumstances we are beginning endorsement, AIDL barabara.One day to see this blog hung God, ah, as he said, they can hold a little longer.

>* EditTxt.setImeOptions, when using the soft keyboard pops up EditText, modify the display of the contents of the Enter key (always hate to use the Enter key to interact, so before you did not know this stuff)

>* java8 new in LocalDate and LocalTime interfaces, Date though a universal interface, but it really does not work well, with maybe, finally happy date processing time.

>* WeakHashMap, direct use HashMap sometimes pose a risk of memory overflow, use WaekHashMap instantiate Map.
When the user no longer has an object reference time, WeakHashMap will be removed object corresponds Key values.

>* Use SnackBar, do not use view.getRootView () as the snackbar of view, Huawei glory 7 will go wrong.

>* Setting TextView single-line display when not to use Lines = 1, and use singleLine = "true", as part of the phone Meizu setting Lines = 1, when then TextView value of all numbers, you will be forced to rip up.

>* TouchDelegate View can be used to change the touch area.
Scene: For example, in the ItemView RecyclerView contains a CheckBox component, and then click ItemView when you want to achieve, can also trigger CheckBox, you can use such

>* ArgbEvaluator can be used to interpolate between the values ​​of different colors, with ValueAnimator.ofObject or ViewPager.PageTransformer use, you can achieve a smooth transition between the different colors.

>* Palette can be used to extract the color of picture.

>* ViewDragHelper, done custom ViewGroup children's shoes should know this thing right to handle touch events artifact, my mother no longer have to worry about me a custom control.

>* PageTransformer for animation effects when switching to define ViewPager page (fade, zoom god of horses ...) there are examples of official directly see.

>* Activity.recreate recreate Activity.
What use is it?
You can change the theme in the program, and immediately refresh the current Activity, without significant restarted Activity animation.

>* View.getContext() , can get a Context :)

>* View.post facilitate non-UI thread interface modifications, and Handler similar role.
And since the post would ensure the Runnable only called at the finish drawing View premise, it is generally to be used to obtain View width and height.

>* Activity.runOnUiThread View.post with similar convenience in a non-UI thread of the interface changes.

>* Fragment mating PagerAdapter use when you can rewrite setUserVisibleHintFragment () method, and then (representing the current Fragment visible to the user if true) to perform some logic based on Boolean parameter.

>* android: animateLayoutChanges This is a very cool property.
The parent layout plus android: animateLayoutChanges = "true", if triggered layout methods (such as its sub-View is set to GONE), the system will automatically help you add animation effects to change the layout of the time!

>* android: clipToPadding set the parent allows its child to view it in view of padding (in this case is the parent View of padding) is plotted.
Is not it about?
For the actual scene you: if there is a ListView, we want in the initial position, the first top 10dp Item from a distance, you can add in android ListView layout: clipToPadding = "false" android: paddingTop = "
10dp "can be.
Is not it convenient?

>* rv's Layoutmanager directly stated in xml, the specific code to view RecyclerView.createLayoutManager methods.
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/recycler_1.jpeg)
![](https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/recycler_2.jpeg)

>* RecyclerView new in version 23.2 of the automatic measurement function, due to the new automatic measurement, the layout of its roots in the item to be measured can not write match_parent direction, the need to change wrap_conte

>* getParent () requestDisallowInterceptTouchEvent (true);. deprive the parent view for touch event handling right, with who knows who.

>* Canvas in clipRect, clipPath and clipRegion shear zone API.
 
>* GradientDrawable have a shadow effect is also good, that is a cut image, a look at the code, what the hell = =!

>* A friend mentioned in the Custom View when some hardware acceleration in the open method has no effect when the problem after API16 indeed there are many ways does not support hardware acceleration, we usually turn off hardware acceleration through in the manifest file, in fact, also android
Close View provides specific hardware acceleration approach, calling View.setLayerType (View.LAYER_TYPE_SOFTWARE, null); can be.

>* PointF, graphics package, a class that we often see in dealing Touch events are defined a downX, a downY for storing a coordinate, if the coordinates little better, if you want to record the coordinates of that code does not look good too a.With PointF (float x, float y); to describe a coordinate point will be much clear.

>* StateListDrawable, the usual approach is to define Selector xml file, but sometimes our image resources may be dynamically obtained from the server, such as the skin of a lot of so-called app, this time can only be accomplished through StateListDrawable the various addState
can.

>* android: duplicateParentState = "true", so that the child follow the status of their Parent View, such as pressed and so on.
Common usage scenarios is sometimes a little button, when we want to expand their hit areas are usually wrapped in a layer to give its layout, a click event written on the Parent, this time if you want to be wrapped in a button click effect
corresponding Selector remain in force, then it comes in handy when duplicateParentState.

>* ViewConfiguration.getScaledTouchSlop (); when the minimum distance between trigger event moving, custom View handle touch events, sometimes need to determine whether the user really exists movie, the system provides such a method.

>* ViewStub, a region sometimes need to display different layouts depending on the circumstances, we usually go through the setVisibility way to show and hide different layouts, but this acquiescence is fully loaded, you can improve performance by better ViewStub.

>* onTrimMemory, rewrite Activity in this method, the callback will be running out of memory (support multiple levels), we took the initiative to facilitate the release of resources, avoid OOM.

>* TextView.setCompoundDrawablePadding, the code sets TextView drawable padding.

>* ImageSwitcher, can be used for a class picture switch, similar to the slide.

>* In the custom of the time, can be drawable to draw a circle, or any other style, try to use drawable, because the effect is far better than the drawable canvas.drawXXX ().

>* If you want to customize the View support SwipeRefreshLayout, only need to declare and implement interfaces to ScrollingView, RecyclerView and NestedScrollView already implements this interface.


>* AtomicFile-- backup file by using the atomic operation file.
Before this knowledge I also wrote, but better to have an official version better.

>* DatabaseUtils-- a database containing a variety of operations using the tool.

>* Activity.isChangingConfigurations () - If the Activity in the configuration will change often, then you can not use this method to manually do the job of the state saved.

>* SearchRecentSuggestionsProvider-- recent tips can create effects provider, it is a simple and fast way.

>* android: clipChildren (ViewGroup) - If this property is not available, then the sub View ViewGroup when drawing will go beyond its scope, the need to use when doing animation.

>* android: fillViewport (ScrollView) - links to articles are detailed in this article, can solve the problem of insufficient time in ScrollView be filled when the content of the screen.

>* android: tileMode (BitmapDrawable) - You can assign a picture to use refillable mode.

>* android: enterFadeDuration / android: exitFadeDuration (Drawables) - This attribute Drawable have multiple states, you can define the fade-out effect before it shows.

>* Log.wtf () means What a Terrible Failure, instead of What The Fuck!

>* Use RenderScript image blur effect.
If your app is minSDK is 16 or less, you need to use the support mode, because a lot of methods are added after the API 17.renderscriptTargetApi up to 23, but you should set it to use the script to maintain the functional integrity of the lowest API.If you want to target API 21 under support mode you must use gradle-plugin 2.1.0 and buildToolsVersion "23.0.3" or above.We need to add renderscriptTargetApi 18 in gradle in, renderscriptSupportModeEnabled true two sentences

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
>* The view is converted into bitmap

```java
public void captureView(){
    int height = getStatusHeight(mContext);
    Bitmap bmp1 = Bitmap.createBitmap(tempView.getWidth(), tempView.getHeight(),
                        Bitmap.Config.ARGB_8888);
                Canvas canvas = new Canvas(bmp1);
                tempView.draw(canvas);
                int currentapiVersion = android.os.Build.VERSION.SDK_INT;
                Bitmap bmp2 = null;
                /**
                 * 如果版本是5.0以上,要去掉状态栏
                 */
                if (currentapiVersion >= Build.VERSION_CODES.LOLLIPOP) {
                    bmp2 = Bitmap.createBitmap(bmp1, 0, height, bmp1.getWidth(), bmp1.getHeight() - height);
                } else {
                    bmp2 = Bitmap.createBitmap(bmp1);
                }
                bmp1.recycle();
}
private int getStatusHeight(Context ct) {
        int result = 0;
        int resourceId = ct.getResources().getIdentifier("status_bar_height", "dimen", "android");
        if (resourceId > 0) {
            result = ct.getResources().getDimensionPixelSize(resourceId);
        }
        return result;
    }
```

>* When Activity LauncherMode as singleTask singleInstance, use startActivityForResult will immediately return, it can not be called normal.
Specific look http://www.360doc.com/content/15/0123/14/12928831_443085580.shtml

>* When PopupWindow there EditText control because Popupwindow not get the focus by default, you need to manually set the focus, so to get to the sub-view monitor events.
So you need to set his focus After creating popwindow, popupWindow.setFocusable (true); it can make EditText gets focus.

>* When PopupWindow Default Click outside does not disappear, you need to set a background image PopupWindow popWindow.setBackgroundDrawable (new BitmapDrawable ()); To create an empty object set to null is not enough, or just create a fully transparent background.

>* android serialized official recommendation Parceble, in fact Parceble best used to exchange data between the memory, and if we want to write data to the hard disk, then recommend implements Serializable

>* Tags can be good tools to help developers real-time preview of the effect of xml, and later to run the content label tools will not be displayed, for example:

````java
<TextView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    tools:text="This passage can be seen only in the preview, after running to see it" />
```

>* android studio 2.1 has support from the jdk8, use the time to add in gradle, we need to update the buildToolsVersion 24 or later

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

>* After 6.0 getResources (). GetColor () method was abandoned, we can ContextCompat.getColor (context, R.color.color_name) replaced with, ContextCompat is v4 bag, ease of use, plus getDrawable () methods

>* Pictures of the resource files on the officially recommended only the launcher mipmap folder, use the resource file and app recommendations on drawable below.

>* SharedPreference.Editor apply the asynchronous operation does not return a successful state, and commit a synchronous operation, therefore, multiple concurrent submitted commit, they will wait for the commit is being processed and then saved to disk with the next data
, thereby reducing the efficiency.

>* If you manifest that the one activity set android: windowSoftInputMode = "adjustResize", then ScrollView (or any other scalable ViewGroups) will be reduced to make room for the soft keyboard.
However, if you set the android in the activity topics: windowFullscreen = "true", then ScrollView not shrink.
This is because the property is mandatory ScrollView full screen.
However, in setting android theme: fitsSystemWindows = "false" will lead to ineffective adjustResize

>* In Android 4.0 later broadcast in Manifest.xml static registration, you must start again in order to receive the broadcast after the program is installed, such as your application to listen radio boot, you have to run through the program is to listen to

>* Activity of onDestory method call timing is uncertain (sometimes will be called after a long time away from the interface onDestory method) should be avoided expect to release the resources associated with the Activity by onDestory method, otherwise it will lead to some random bug

>* 2.X era Bitmap objects stored in the heap memory though, but with a byte array to store its pixel information. By a counter to record the number of the pixel information is referenced. Some people think that this byte array in native heap, but in fact it is also heap. Only after a user calling recycle (), Bitmap objects will release pixel information, reference will be lost after the garbage collection mechanism destroyed. Coupled with the heap size DVM strict threshold, so we use a lot of pictures resources when and prone OOM. Solutions are generally, reference to a hash table with a soft storage Bitmap object as a memory cache, and at the appropriate time off with their recycle (). 3.0+ Bitmap object can be completely destroyed by the garbage collection mechanism, in theory, no longer calling recycle ().

>* .gitignore only ignored those who had not track the files if some files have been included in the version management, the modified .gitignore is invalid.
Then the solution is to first remove the local cache (not track changes to the state), and then submitted to:

```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

>* Use long timestamp or String type reception pit encountered since the project model many of which were generated by GsonFormat server to the json timestamp is 10, resulting in GsonFormat automatically parse it became int when testers select time in 2100, when the timestamp is the beginning of the ten with 4 int type receiver out of bounds, resulting in an error

>* Your app to add a default layout style, for example: Each control width and height attributes need to write, but a lot of width and height attribute controls are wrap_content, so we can add the following style in the style file:

```
<style name="Theme.YourApp" parent="android:style/Theme.Light">
    <item name="android:layout_width">wrap_content</item>
    <item name="android:layout_height">wrap_content</item>
</style>
```

Thus, the width and height of the default controls are wrap_content style friends.

>* In the style of writing styles by deemed to extend your parent label style, which is more efficient.

```
<style name="Fill">
    <item name="android:layout_width">fill_parent</item>
    <item name="android:layout_height">fill_parent</item>
</style>
<style name="Fill.Height" parent="@style/Fill">
    <item name="android:orientation">vertical</item>
</style>
```

>* Android application switching button on the application but is not actually listed Task, so you will see some applications in switching view, there are several tasks.
If your application has logically independent parts, or you want to display side by side in two different parts of the application in a multi-window environment, this situation is suitable for multi-task.
Use manifest attribute (static) or intent flags (dynamic) can achieve this
<img src="https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/multy_task1.jpg" width = "50%" height="300px" /><img src="https://raw.githubusercontent.com/jiang111/awesome-android-tips/master/img/multy_task2.jpg" width = "50%"  height="300px"/>

>* When using the app's theme is NoActionBar, but is still used in the layout toolbar, do not add fitsSystemWindows property in style file, but in the use of the toolbar layout outermost plus fitsSystemWindows, or when you use EditText, in long press to bring up the system EditText paste function on millet phone when pasted layout layout will be misplaced.

>* When WebView and ScrollView nest, and WebView have font zoom function, when after switching fonts webview, webview height and not well calculated, this time by way of injection, let js height calculated by test, this is the most reliable code address: http: //blog.csdn.net/jys1115/article/details/43525979

>* Context class createPackageContext (packageName, flags) method can be used to obtain the specified package name for the application Context object.

>* TextView.class has a method called setKeyListener (KeyListener) ; wherein DigitsKeyListener class, use getInstance (String accepted) method to specify the EditText can input character set;

>* View.class has methods called getLocationInWindow (int []) & getLocationOnScreen (int []) ,They can get View position in the window / screen;

>* Context.getCacheDir() - Use the cache dir for caching data. Simple enough but some don't know it exists.

>* StaticLayout - Useful for measuring text that you're about to render into a custom View.

####From the following address :( portion of the address)
>* http://oakzmm.com/2015/08/04/cool-Android-api/
>* http://oakzmm.com/2015/08/11/cool-Android-api-2/
>* http://weibo.com/liangfeizc?from=feed&loc=nickname
>* http://zhuanlan.zhihu.com/zmywly8866/20309921
>* http://www.zhihu.com/question/33636939
>* http://gold.xitu.io/entry/56c2b9b779bc4400540894ac
>* https://www.zhihu.com/question/33636939/answer/57239990?group_id=612750833369153536
>* http://mp.weixin.qq.com/s?__biz=MzA4MTM2MjE2MA==&mid=2650836293&idx=3&sn=2624066ababb6b613634015f54ea19b6&scene=0#wechat_redirect
>* http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2016/0504/4205.html
>* https://zhuanlan.zhihu.com/p/20309921
>* http://www.pfeng.org/archives/840#123-tsina-1-92600-1bb80a0982f5c2ea1fcaf67d7fdce2f1
>* http://blog.danlew.net/2014/03/30/android-tips-round-up-part-1/

### License

    Copyright 2016 NewTab

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

