JBHeaderScroll
================
An Android library that provides the functionality to allow scrollable containers to show or hide headers while scrolling.

![JBHeaderScroll](https://github.com/JohannBlake/JBHeaderScroll/blob/master/Graphics/JBHeaderScroll-Demo.gif)



### Description

A growing tendency in improving the user experience in Android apps is to maximize the amount of screen real estate when viewing content that requires scrolling. Examples of this are image galleries, contact lists and browsing web pages. On many of these screens, a section at the top of the screen may be used for things like a toolbar. Lists may have a header showing column names. Sometimes these headers remain fixed at the top of the list while sometimes they scroll with the list items.

Collectively, toolbars, list headers and any other type of view that appears above some scrollable area are referred to in JBHeaderScroll as "headers". Area beneath the header can be any kind of scrollable content such as a ListView, ScrollView, RecyclerView, WebView or even a LinearLayout or RelativeLayout. Collectively, these scrollable containers are referred to in JBHeaderScroll as "scrollers". The only scroller that JBHeaderScroll has not been tested on is the ActionBar. If you are using an ActionBar, you should replace it with a Toolbar as ActionBar has been deprecated. ActionBar also has its own built-in scrollable hiding/showing although this is apparently very difficult to implement.

When a header at the top of a list remains fixed, that is often a desirable feature because as the user scrolls the list, they may want to see at glance the name of a column that data in a list item belongs to (presuming you're showing columns of data). But if you had a list that was only showing images or data that isn't laid out in a column, the header might be used to act as a toolbar to provide contextual features such as selecting list items or sliding out a navigation view from the right or left side of the list. In these cases, having the header remain in a fixed location all the time reduces the height of the area beneath the header that is used for the scrollable content. When scrolling content that contains images, some images are large enough to cover the entire height of the screen. Often it's nice to see the entire image at a glance but this would not be possible if a fixed header was reducing the amount of visible space. You could however just let the user tap on the image and show the image in a view that takes up the entire screen. But that may be unnecessary and somewhat messy if the image was embedded in HTML content shown in a WebView.

A better way to increase screen area is to hide the header as the user scrolls down but then show it when they scroll up. Apps like Google's Newstand do this.

While it may seem trivial to code, showing and hiding the header during scrolling is indeed a complex undertaking due to how Android passes motion events from the screen through the view hierarchy. It is also complicated by the fact that there is no consistent way scrolling events can be intercepted in controls that provide scrolling capabilities. For example, a ListView has built in scrolling events that can indicate where the current scroll position is but this is based upon the item position. The absolute position of the top item can be computed as a workaround but other problems eventually crop up. A ScrollView has a different mechanism to report the scrolling position. And a WebView has a completely different one as well.

Attempting to resize and reposition controls during scrolling can be tricky as this can actually interfere with the motion events that are being received.

JBHeaderScroll provides a unified means to show or hide the header while the user scrolls the scroller content. If the user scrolls only a small amount and releases their finger but the header is still partially showing, JBHeaderScroll will automatically either show the entire header or hide it all together and this is done by animating it into or out of view. A header will not remain partially visible. Whether it shows or hides the header depends on how much of the header is visible when the user releases their finger. If more than half of the header is visible, it will be animated downward to be shown entirely. If less than half is shown, it will be animated upward until it is no longer visible.


### Demo & Integration

To try out the widget, just install the demo app *JBHeaderScroll-Demo-x.x.x.apk* located in the root directory. The source code for the widget is located under the folder *jbheaderscrolllib*. If you don't want to bother downloading and compiling the library, you can download the compiled version, *jbheaderscrolllib-x.x.x.aar*, located in the root directory.

The demo contains four separate demos:

1. A ListView with a Toolbar.
2. A ScrollView with a Toolbar.
3. A WebView with a Toolbar.
4. Two ListViews with a Toolbar common to both and one ListView having its own header (a LinearLayout).


### Integration

Currently you need to download the source and compile the project. The project consists of the library, *jbheaderscrolllib*, and the sample app for testing out the library, which is the root project. The source code for the sample app is located under the foler app > src > main

### Usage

JBHeaderScroll requires that you subclass your scroller and override the dispatchTouchEvent method. In this example, a ListView is used as the scroller:


``` xml
import android.content.Context;
import android.util.AttributeSet;
import android.view.MotionEvent;
import android.widget.ListView;
import info.johannblake.widgets.jbheaderscrolllib.JBHeaderScroll;

public class CustomListView extends ListView
{
  private JBHeaderScroll jbHeaderScroll;

  public CustomListView(Context context, AttributeSet attrs)
  {
    super(context, attrs);
  }

  public CustomListView(Context context, AttributeSet attrs, int defStyleAttr)
  {
    super(context, attrs, defStyleAttr);
  }

  @Override
  public boolean dispatchTouchEvent(MotionEvent ev)
  {
    if (this.jbHeaderScroll != null)
      this.jbHeaderScroll.onScrollerDispatchTouchEventListener(this, ev);

    return super.dispatchTouchEvent(ev);
  }

  public void setJBHeaderRef(JBHeaderScroll jbHeaderScroll)
  {
    this.jbHeaderScroll = jbHeaderScroll;
  }
}
```

In this layout file, a toolbar acts as the header while the CustomListView is used for the scroller:

``` xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:tools="http://schemas.android.com/tools"
                android:layout_width="match_parent"
                android:layout_height="match_parent">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        style="@style/ToolbarStyle"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:minHeight="?attr/actionBarSize">

    </android.support.v7.widget.Toolbar>

    <info.johannblake.jbheaderscrollsample.CustomListView
        android:id="@+id/listview"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_below="@id/toolbar"
        android:background="#ffffffff"
        android:cacheColorHint="#00000000"
        android:divider="#c0c0c0"
        android:dividerHeight="1dp"
        android:scrollingCache="true" />

</RelativeLayout>
```

IMPORTANT: In the example above, a RelativeLayout is used. You must make sure that the code used to reposition your scroller uses the appropriate LayoutParams, as shown below. In the code below, RelativeLayout.LayoutParams is being used because the CustomListView shown above uses a RelativeLayout as its parent. If you end up using the wrong type of LayoutParams, your code will generate an exception. Avoid using a LinearLayout for the parent container. A LinearLayout can only position items adjacent to each other. It is necessary to use a ViewGroup that allows the scroller's top edge to move up and behind the header. A RelativeLayout allows you to position views at any location.

What is important to realize is that the scroller (in this case the CustomListView) must fill it's parent container. Notice that the top edge of the CustomListView is not aligned with the bottom edge of the toolbar. The top edge of your scroller should be aligned with the top edge of your header (here, the toolbar). JBHeaderScroll along with some additional code in your activity (shown below) will automatically reposition the scroller so that its top edge is somewhere between the top and bottom edge of the header. When the scroller is initially displayed, the top edge of the scroller will be aligned with the bottom edge of the header but then be adjusted as the user scrolls. Regardless how you lay out your views, it must be possible for the scroller's top edge to move up to the top edge of the header. This means that the scroller and header should be sibling views in the same container. If you need to place the scroller, such as a ListView, inside of another container, you should subclass that container as you did with the CustomListView (but not subclass ListView). In this case, the container is acting as your scroller.

In your activity's onCreate method, you initialize the JBHeaderScroll:

``` xml
  @Override
  protected void onCreate(Bundle savedInstanceState)
  {
    try
    {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_listview_demo);

      // Fill the listview with some data.
      final CustomListView listview = (CustomListView) findViewById(R.id.listview);
      List<String> items = new ArrayList<>();

      for (int i = 0; i < 100; i++)
        items.add(String.valueOf(i));

      ArrayAdapter<String> arrayAdapter = new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, items);
      listview.setAdapter(arrayAdapter);

      // Setup a JBHeaderScroll.
      final Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);

      toolbar.getViewTreeObserver().addOnGlobalLayoutListener(new ViewTreeObserver.OnGlobalLayoutListener()
      {
        @Override
        public void onGlobalLayout()
        {
          try
          {
            listview.setY(toolbar.getHeight());
            jbHeaderScroll = new JBHeaderScroll(toolbar, 0);
            jbHeaderScroll.registerScroller(listview, new JBHeaderScroll.IJBHeaderScroll()
            {
              @Override
              public void onReposition(float top, boolean scrollingUp, float scrollDelta)
              {
                try
                {
                  // The list's view top edge must be adjusted during scrolling.
                  // IMPORTANT: Make sure you use the correct type of LayoutParams which is the type that applies to the parent
                  // container of the listview.

                  // When the user releases their finger while scrolling very slowly, the jitter from their finger
                  // may result in a slight amount of scrolling downward. This can result in a side effect of the
                  // header animating down when it might have animated up depending on its current position. To
                  // avoid this, avoid repositioning the scroller for small amounts of scrolling. You may need to
                  // play with this value.

                  if (scrollingUp || (!scrollingUp && (scrollDelta > 5)))
                  {
                    RelativeLayout.LayoutParams layoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.MATCH_PARENT, RelativeLayout.LayoutParams.MATCH_PARENT);
                    layoutParams.setMargins(0, (int) top, 0, 0);
                    listview.setLayoutParams(layoutParams);
                    toolbar.bringToFront(); // Necessary if your scroller is rendered last.
                  }
                }
                catch (Exception ex)
                {
                  Log.e(LOG_TAG, "onReposition: " + ex.toString());
                }
              }

              @Override
              public int onHeaderBeforeAnimation(boolean scrollingUp, float scrollDelta)
              {
                return JBHeaderScroll.ANIMATE_HEADER_USE_DEFAULT;
              }

              @Override
              public void onHeaderAfterAnimation(boolean animatedUp, float scrollDelta)
              {
              }
            });

            listview.setJBHeaderRef(jbHeaderScroll);
            toolbar.getViewTreeObserver().removeOnGlobalLayoutListener(this);
          }
          catch (Exception ex)
          {
            Log.e(LOG_TAG, "onGlobalLayout: " + ex.toString());
          }
        }
      });
    }
    catch (Exception ex)
    {
      Log.e(LOG_TAG, "showListViewDemo: " + ex.toString());
    }
  }
```

The onGlobalLayout method is needed because during onCreate, the height of controls is zero because Android hasn't actually completed its layout rendering. Only in onGlobalLayout is the height of the header known. JBHeaderScroll needs to know the height of the header in order to properly reposition it as the user scrolls the scroller.

Instaniating the JBHeaderScroll is done with:

``` xml
jbHeaderScroll = new JBHeaderScroll(toolbar, 0);
```

The second parameter in the registerScroller method is used to indicate the header's "visual" top edge's offset. In most cases, the top edge of the header will be aligned to the top edge of its parent container, in which case the offset is zero. But in some rare cases, if you need to visually offset the header's top header, you need to indicate how much offset is being used. This is specified in dp units. It is possible to create a layout where the header has padding around the top edge making it look like the header is offset within its parent container. If you left the offset to zero in the second parameter and began scrolling, the scroller would start to show beyond the top edge of the header. So if you had a top padding of 10dp, you should set the second parameter to 10.

You also need to initially change the top edge of the scroller:

``` xml
listview.setY(toolbar.getHeight());
```

You then register your scroller with:

``` xml
jbHeaderScroll.registerScroller
```

In this example, we are only using a Toolbar and a ListView, so only one scroller is being registered. But you can have a case where you want to have multiple scrollers that might share a common header and when one scroller is scrolled, JBHeaderScroll will make sure that no gap remains above any of the other scrollers. If you are using multiple scrollers and want them synchronized, you only use a single JBHeaderScroll instance and register each scroller. An example of this might be where you have two scrollers laid out horizontally next to each other. The left scroller might be a ListView while the right scroller might be a ScrollView. Both might share a common Toolbar that stretches across the top of both scrollers. When you scroll the left scroller up, JBHeaderScroll will automatically scroll the right one up but only until the header is no longer visible and stop scrolling the right scroller. If you then began scrolling down, the header will scroll down but the right scroller will not scroll down. It only scrolls up initially to prevent a gap from showing above it. But if your scroll the right scroller down, you will see the top position of the scroller.

If a scroller were to contain a custom control that had its own header and own scroller but you don't want it synchronized with the parent scroller, you need to use a separate JBHeaderScroll instance to manage its scrolling. You would not use the parent scroller's JBHeaderScroll instance to register the child scroller. The nested header demo illustrates using two scrollers sharing a common JBHeaderScroll instance while one of the scrollers has a ListView with its own JBHeaderScroll.

In the onReposition method shown above, you need to provide code that will reposition your scroller. This method gets called when the user scrolls the scroller. JBHeaderScroll will provide the Top position that you need to move your scroller to. JBHeaderScroll cannot do this for you because it doesn't know anything about your layout. Your scroller may be embedded in some complex hierarchy view. JBHeaderScroll only tracks scrolling positions but you must reposition and possibly resize your scroller. Whether you move your scroller by setting using setY() or modifying the top margin will depend on how your views are laid out. The example above sets the margin (even though initially we used setY(). The nested header demo however uses setY().

When the user releases their finger from scrolling, JBHeaderScroll will decide whether the header needs to be animated fully into view or fully out of view. Before animating in one of these directions, you have the option of overriding the decision made by JBHeaderScroll and indicate whether you prefer to have the header shown or hidden.

In the onHeaderBeforeAnimation method, you can return either:

``` xml
ANIMATE_HEADER_USE_DEFAULT
ANIMATE_HEADER_UP
ANIMATE_HEADER_DOWN
```

The onHeaderBeforeAnimation method has two parameters - scrollingUp and scrollDelta. If scrolling up is set to true, it means that JBHeaderScroll is about to scroll the header up. False means it will be scrolled down. scrollDelta indicate the amount of scrolling that took place from the original location when the user pressed their finger down to the location where they released their finger. onHeaderBeforeAnimation is only called after the user releases their finger.

The onHeaderAfterAnimation gets called after the header has been animated either fully up or down. You can use this for whatever purpose you need. onHeaderAfterAnimation is only called after the user releases their finger.

Finally, you need to call setJBHeaderRef on the scroller. This stores a reference of the JBHeaderScroll with the scroller and is needed to communicate motion events with the JBHeaderScroll.

In your activity you also need to override the dispatchTouchEvent method:

``` xml
@Override
public boolean dispatchTouchEvent(MotionEvent ev)
{
  if (this.jbHeaderScroll != null)
    this.jbHeaderScroll.onRootDispatchTouchEventListener(ev);

  return super.dispatchTouchEvent(ev);
}
```

You need to call the onRootDispatchTouchEventListener method for each JBHeaderScroll instance that you have.


### MIT License

```
    The MIT License (MIT)

    Copyright (c) 2015 Johann Blake

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in
    all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
    THE SOFTWARE.
```
