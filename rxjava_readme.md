RxJava使用场景总结

>* Scheduler线程切换

```
observable.subscribeOn(Schedulers.io()).observeOn(AndroidSchedulers.mainThread());
//进行简单的封装
public static <T> Observable<T> applyIOSchedule(Observable<T> observable) {
        return observable.subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread());
    }
```
