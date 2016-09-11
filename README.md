# DavidSwipeRefreshLayout
【Android】SwipeRefreshLayout的简单使用教程。下拉刷新控件炫酷效果。

作者：程序员小冰，GitHub主页：https://github.com/QQ986945193 
新浪微博：http://weibo.com/mcxiaobing 
首先给大家看一下我们今天这个最终实现的效果图： 
![这里写图片描述](http://img.blog.csdn.net/20160911103900257)

好了，简单的介绍一下，SwipeRefreshLayout是android系统自带的一个控件，
可以看到现在App好多刷新都有这样类似的效果。其实它的使用还是比较
简单的，就是在我们的listview的控件上面加上就行了，然后再在java代码
中设置它的颜色，以及监听它的刷新事件。我这里随便用了一个list集合。
还有刷新结束后没有操作什么内容，但是实际项目中大家按例套进去即可。
首先SwipeRefreshLayout是V4包下的，我们xml引用它的时候可以是这样：

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <android.support.v4.widget.SwipeRefreshLayout
        android:id="@+id/swipe_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ListView
            android:id="@+id/listview"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:padding="16dp" />

    </android.support.v4.widget.SwipeRefreshLayout>
</RelativeLayout>

```

然后，我们再在java代码中进行监听事件，以及设置刷新颜色：

```
package davidswiperefreshlayout.qq986945193.davidswiperefreshlayout;

import android.app.Activity;
import android.os.Bundle;
import android.os.Handler;
import android.support.v4.widget.SwipeRefreshLayout;
import android.widget.ArrayAdapter;
import android.widget.ListView;

import java.util.ArrayList;

/**
 * @author ：程序员小冰
 * @新浪微博 ：http://weibo.com/mcxiaobing
 * @GitHub: https://github.com/QQ986945193
 * @CSDN博客: http://blog.csdn.net/qq_21376985
 * @码云OsChina ：http://git.oschina.net/MCXIAOBING
 */
public class MainActivity extends Activity implements SwipeRefreshLayout.OnRefreshListener {

    private SwipeRefreshLayout mSwipeLayout;
    private ListView mListView;
    private ArrayList<String> list = new ArrayList<String>();
    private ArrayAdapter<String> adapter;

    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mListView = (ListView) findViewById(R.id.listview);
        /**
         * listview绑定adapter
         */
        adapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, getData());
        mListView.setAdapter(adapter);

        mSwipeLayout = (SwipeRefreshLayout) findViewById(R.id.swipe_container);
        //绑定刷新时间
        mSwipeLayout.setOnRefreshListener(this);
        //设置颜色
        mSwipeLayout.setColorSchemeResources(android.R.color.holo_blue_bright,
                android.R.color.holo_green_light, android.R.color.holo_orange_light,
                android.R.color.holo_red_light);
    }

    private ArrayList<String> getData() {
        list.add("Hello world!");
        list.add("CSDN:程序员小冰");
        list.add("An Android Developer");
        list.add("http://weibo.com/mcxiaobing");
        list.add("http://git.oschina.net/MCXIAOBING");
        list.add("https://github.com/QQ986945193");
        list.add("An Android Developer");
        list.add("http://weibo.com/mcxiaobing");
        list.add("http://git.oschina.net/MCXIAOBING");
        list.add("https://github.com/QQ986945193");
        list.add("An Android Developer");
        list.add("http://weibo.com/mcxiaobing");
        list.add("http://git.oschina.net/MCXIAOBING");
        list.add("https://github.com/QQ986945193");
        return list;
    }

    public void onRefresh() {
        new Handler().postDelayed(new Runnable() {
            @Override
            public void run() {
                //停止刷新 
                mSwipeLayout.setRefreshing(false);

            }
        }, 3000);
    }
}

```
好了，最后直接运行即可看到上面的效果。如果对您有帮助，欢迎star，fork。。。
