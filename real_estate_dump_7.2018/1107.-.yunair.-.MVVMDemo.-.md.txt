# MVVMDemo
## This is a Demo About Google Data Binding Guide
## The URL is https://developer.android.com/intl/zh-cn/tools/data-binding/guide.html
## English Version see [there][0]
---

### 初始化依赖

在 Top-level build 文件中加入以下代码
```gradle
dependencies {
       classpath "com.android.tools.build:gradle:1.3.1"
       classpath "com.android.databinding:dataBinder:1.0-rc1"
   }
```
在 project build 文件中加入以下代码
```gradle
apply plugin: 'com.android.databinding'
```
**如果你gradle sync时遇到了错误，首先尝试升级你的support library**

---

### Data Binding Layout Files

Data-binding layout 文件和之前的layout 文件有轻微的不同, 以layout标签作为根元素，
然后其中放置了data标签和之前的view标签。这个view标签就是你之前不使用Data-binding时的根标签。
下面是一个简单的例子
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android">
   <data>
       <variable name="user" type="com.example.User"/>
   </data>
   <LinearLayout
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.firstName}"/>
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.lastName}"/>
   </LinearLayout>
</layout>
```

这个在`data`标签内被定义的`user`变量可以在这个`layout`中使用
```xml
<variable name="user" type="com.example.User"/>
```
在这个`layout`中使用表达式的语法为："@{}"，
在下面的代码中，`TextView`的文字将会被设置为user.firstName
```xml
<TextView android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="@{user.firstName}"/>
```
上面`layout`文件中使用变量的方式转换成在java文件中的方式为，
```java
com.example.User user = new com.example.User();
```
这种方式我们一般比较少用，除非类名冲突时，我们一般使用的是另外一种方式
```java
import com.example.User;
User user = new User();
```
所以在`data`标签内，你也可以这样写
```xml
<import type="com.example.User"/>
<variable name="user" type="User"/>
```
如果类名冲突，`import`标签有一个子标签叫做`alias`

eg:
```xml
<import type="android.view.View"/>
<import type="com.example.real.estate.View"
        alias="Vista"/>
```
现在, "Vista" 将会作为`com.example.real.estate.View`的引用
"View" 将会作为 `android.view.View`的引用

既然引入了包，当然可以像Java一样使用包内的静态方法了，
例如 : `import`了`View`类, 你可以像下面以下使用View中的static方法
```xml
<TextView
   android:text="@{user.lastName}"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:visibility="@{View.VISIBLE}"/>
```
像在java中一样, `java.lang.*` 会默认被import.

### Data Object

对于上面提到的`User`类来说，可以使用一个
plain-old Java object (POJO) or JavaBeans 对象来表示它

POJO:
```java
public class User {
   public final String firstName;
   public final String lastName;
   public User(String firstName, String lastName) {
       this.firstName = firstName;
       this.lastName = lastName;
   }
}
```
JavaBeans:
```java
public class User {
   private final String firstName;
   private final String lastName;
   public User(String firstName, String lastName) {
       this.firstName = firstName;
       this.lastName = lastName;
   }
   public String getFirstName() {
       return this.firstName;
   }
   public String getLastName() {
       return this.lastName;
   }
}
```

### Binding Data

默认情况下，绑定类的类名依赖`layout`文件，将`layout`文件名转化成驼峰命名，然后接一个"Binding"后缀

eg: `activity_main.xml` 将会产生一个名为 `ActivityMainBinding` 的类

上面的`layout` 文件名为 `main_activity.xml` 所以产生的类为 `MainActivityBinding`.
这个类将会从layout属性中获取所有的绑定变量，layout将会知道在视图中如何给绑定变量赋值
创建一个Binding最简单的方式就是初始化inflating layout的时候
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
   super.onCreate(savedInstanceState);
   MainActivityBinding binding = DataBindingUtil.setContentView(this, R.layout.main_activity);
   User user = new User("Test", "User");
   binding.setUser(user);
}
```

### Custom Binding Class Names

默认情况下，通过`layout`文件名生成的类将会被放置在当前模块的`databinging`包下，

例如，`layout`文件名为 `contact_item.xml` 将会产生名为`ContactItemBinding`的类。
如果模块的包名为 `com.example.my.app`,那么这个类将会被放置在 `com.example.my.app.databinding`包中.

如果你想自定义自动生成的类所在的名字和位置，可以通过在`data`标签内添加`class`属性来实现

eg:
```xml
<data class="ContactItem">
    ...
</data>
```
上面这种情况将会在当前模块的`databinding`包内生成`ContactItem`类
如果想要在当前模块的包内生成`ContactItem`类,只需要加一个“.”前缀：
```xml
<data class=".ContactItem">
    ...
</data>
```
如果想指定在哪个包内生成绑定的类，使用包的全名+类名的形式
```xml
<data class="com.example.ContactItem">
    ...
</data>
```
你可以在[CustomBindingClassNameActivity][1]中看到其中的区别

### Binding Event

如果想绑定事件(eg: View.OnClickListener),
和绑定数据类似，定义一个Handler类来处理事件，然后将对应的事件在`@{}`中声明，
同时记得在java文件中set那个Handler，你可以在[BaseActivity][2]中看到具体的用法

### Includes

使用最外部bind属性和`data`标签内的变量，可以将需要的变量从当前`layout`传入被include的`layout`
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:bind="http://schemas.android.com/apk/res-auto">
   <data>
       <variable name="user" type="com.example.User"/>
   </data>
   <LinearLayout
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <include layout="@layout/name"
           bind:user="@{user}"/>
       <include layout="@layout/contact"
           bind:user="@{user}"/>
   </LinearLayout>
</layout>
```

在你的`name.xml`和`contact.xml`的`data`标签内，必须也拥有`user`变量，该Demo参见[IncludeActivity][3]

### Expression Language

#### Common Features

DataBinding的表达式就像Java的表达式类似，下面这些是相同的:

- Mathematical + - / * %
- String concatenation +
- Logical && ||
- Binary & | ^
- Unary + - ! ~
- Shift >> >>> <<
- Comparison == > < >= <=
- instanceof
- Grouping ()
- Literals - character, String, numeric, null
- Cast
- Method calls
- Field access
- Array access []
- Ternary operator ?:

#### Missing Operations

下面的表达式从Java中去掉了

- this
- super
- new
- Explicit generic invocation

#### Null Coalescing Operator

这就是简化的null判断表达式，使用(`??`)来表示，如果左边的值为null，则使用右边的值。
下面两个表达式是相同的
```xml
android:text="@{user.displayName ?? user.lastName}"
android:text="@{user.displayName != null ? user.displayName : user.lastName}"
```

#### Collections

通用的集合: arrays, lists, sparse lists, and maps 可以通过[]操作符来使用
```xml
<data>
    <import type="android.util.SparseArray"/>
    <import type="java.util.Map"/>
    <import type="java.util.List"/>
    <variable name="list" type="List&lt;String>"/>
    <variable name="sparse" type="SparseArray&lt;String>"/>
    <variable name="map" type="Map&lt;String, String>"/>
    <variable name="index" type="int"/>
    <variable name="key" type="String"/>
</data>
…
android:text="@{list[index]}"
…
android:text="@{sparse[index]}"
…
android:text="@{map[key]}"
```
可以看到我使用了`&lt;`来代替`<`，因为在xml里面，不允许在`""`内使用`<`,所以使用了xml的特殊字符来替代，
下面也有类似的情况

#### String Literals

你有三种方式来使用String
```xml
android:text='@{map["firstName"]}'
android:text="@{map[`firstName`]}"
android:text="@{map[&quot;firstName&quot;]}"
```
- 使用单引号`'`作为最外层包裹
- 使用双引号`"`作为最外层包裹，但是内部使用反引号```
- 使用双引号`"`作为最外层包裹，但是内部使用xml的特殊字符`&quot;`来代替需要的双引号

可以在[QuoteActivity.java][4]类看具体的用法

#### Resources

当然，在`@{}`使用常规的语法访问资源文件是没问题的
但是，如果是strings和plurals类型，在xml里定义了格式化参数，就需要将参数传入其中
```xml
android:padding="@{large? @dimen/largePadding : @dimen/smallPadding}"
android:text="@{@string/nameFormat(firstName, lastName)}"
android:text="@{@plurals/banana(bananaCount)}"
```

一些元素需要明确的类型

|Type	            |Normal Reference  |Expression Reference
| :---:             | :---:            | :---:
|String[]	        |@array	           |@stringArray
|int[]	            |@array	           |@intArray
|TypedArray	        |@array	           |@typedArray
|Animator	        |@animator	       |@animator
|StateListAnimator	|@animator	       |@stateListAnimator
|color int	        |@color	           |@color
|ColorStateList	    |@color	           |@colorStateList


### Data Objects

一个POJO可以被用在数据绑定中，但是，修改POJO的时候UI不会更新
数据绑定最方便的一点在于给了你数据对象通知的能力，当你的数据改变时。
有三种不同的数据改变通知机制，`Observable objects`, `observable fields`, and `observable collections`.

当这些可以观察的数据对象绑定到UI，当数据改变时，UI也会被自动的改变

#### Observable Objects

一个实现`Observable`接口的类将会

`Observable` 接口拥有添加和移除监听者的方法,但是，什么时候通知这些监听者则由开发者决定。
为了更容易的完成开发, 创造了`BaseObservable`这个基类实现了接口注册监听者的方法。
这些数据类的编写者们需要决定何时通知监听者数据改变了，做法就是把`Bindable`注解赋值给对应的get方法，在set方法里发送通知。

```java
private static class User extends BaseObservable {
   private String firstName;
   private String lastName;
   @Bindable
   public String getFirstName() {
       return this.firstName;
   }
   @Bindable
   public String getLastName() {
       return this.lastName;
   }
   public void setFirstName(String firstName) {
       this.firstName = firstName;
       notifyPropertyChanged(BR.firstName);
   }
   public void setLastName(String lastName) {
       this.lastName = lastName;
       notifyPropertyChanged(BR.lastName);
   }
}
```
在编辑的时候，`Bindable`注解将会在`BR`类文件内产生一个实体，`BR`类文件将会被生成在当前模块的包内。
如果数据类的基类不能被改变，使用`PropertyChangeRegistry`类来有效的储存和通知监听者来达到实现`Observable`接口的目的

#### ObservableFields

创建 `Observable` 类需要做一些额外的工作, 所以，如果开发者们想省时间或者数据类中只有很少的属性，
可以使用`ObservableField`和它的兄弟姐妹们`ObservableBoolean`,`ObservableByte`, `ObservableChar`,
`ObservableShort`, `ObservableInt`, `ObservableLong`, `ObservableFloat`,`ObservableDouble`, 和 `ObservableParcelable`.
`ObservableFields`是一个有单一变量的可观察的字段。
(不知道怎么翻译，直接把原文放在此做比对`ObservableFields` are self-contained observable objects that have a single field.)
对于原始类型，在访问的时候会防止自动装箱和拆箱操作。
使用方法，创建一个public final字段在数据类中：
```java
private static class User {
   public final ObservableField<String> firstName =
       new ObservableField<>();
   public final ObservableField<String> lastName =
       new ObservableField<>();
   public final ObservableInt age = new ObservableInt();
}
```
通过get和set方法访问它的值
```java
user.firstName.set("Google");
int age = user.age.get();
```

#### Observable Collections

一些应用需要更灵活的结构来储存数据。Observable集合允许通过key来访问这些数据
集合提供里两种方式：`ObservableArrayMap` and `ObservableArrayList`

当key是引用类型的时候，(例如String)，推荐使用`ObservableArrayMap`
```java
ObservableArrayMap<String, Object> user = new ObservableArrayMap<>();
user.put("firstName", "Google");
user.put("lastName", "Inc.");
user.put("age", 17);
```
在layout中, map通过字符串的keys来访问:
```xml
<data>
    <import type="android.databinding.ObservableMap"/>
    <variable name="user" type="ObservableMap&lt;String, Object>"/>
</data>
…
<TextView
   android:text='@{user["lastName"]}'
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
<TextView
   android:text='@{String.valueOf(1 + (Integer)user["age"])}'
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```
当key是int类型的时候，推荐使用`ObservableArrayList` :
```java
ObservableArrayList<Object> user = new ObservableArrayList<>();
user.add("Google");
user.add("Inc.");
user.add(17);
```
在layout中, list通过indices来访问:
```xml
<data>
    <import type="android.databinding.ObservableList"/>
    <import type="com.example.my.app.Fields"/>
    <variable name="user" type="ObservableList&lt;Object>"/>
</data>
…
<TextView
   android:text='@{user[Fields.LAST_NAME]}'
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
<TextView
   android:text='@{String.valueOf(1 + (Integer)user[Fields.AGE])}'
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```

该Demo参见[ObservableModel][5]`

### Generated Binding

产生的绑定类连接到layout中带有变量的Views
像之前提到的一样，绑定类的名字和其所属的包名都可以自定义。所有生成的绑定类都继承自`ViewDataBinding`

#### Creating

**个人觉得在`Fragment`中比较常用**

绑定类需要在inflate之后立刻被创建。
这里有一些方式来实现绑定`layout`。
最常用的方式是使用`Binding`类提供的静态方法，inflate方法在一步之内完成了inflate了View层级以及绑定到对应的`layout`。
还有一个简单的版本只需要`LayoutInflater`参数
only takes a LayoutInflater and one that takes a ViewGroup as well:

```java
MyLayoutBinding binding = MyLayoutBinding.inflate(layoutInflater);
MyLayoutBinding binding = MyLayoutBinding.inflate(layoutInflater, viewGroup, false);
```
如果该`layout`被其他的方式inflate了，它需要单独的绑定
```java
MyLayoutBinding binding = MyLayoutBinding.bind(viewRoot);
```
某些时候，不能提前知道绑定到哪个`layout`上。在这种情况下，可以通过使用`DataBindingUtil`类来进行绑定
```java
ViewDataBinding binding = DataBindingUtil.inflate(LayoutInflater, layoutId,
    parent, attachToParent);
ViewDataBinding binding = DataBindingUtil.bindTo(viewRoot, layoutId);
```

#### Views With IDs

在`layout`中对每个有ID的View，在对应的绑定类中会产生一个public final字段。
数据绑定会提取出这些View的Id，通过在View层级上使用单向传递，这个方式会比对一堆View使用`findViewById`快一些

```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android">
   <data>
       <variable name="user" type="com.example.User"/>
   </data>
   <LinearLayout
       android:orientation="vertical"
       android:layout_width="match_parent"
       android:layout_height="match_parent">
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.firstName}"
   android:id="@+id/firstName"/>
       <TextView android:layout_width="wrap_content"
           android:layout_height="wrap_content"
           android:text="@{user.lastName}"
  android:id="@+id/lastName"/>
   </LinearLayout>
</layout>
```
将会在绑定类中产生这样如下的变量
```java
public final TextView firstName;
public final TextView lastName;
```
使用数据绑定，几乎不需要ID，但是在某些情况下，仍然有通过代码访问View的需要。

### Variables

每个在`data`标签内的变量都会被给予`get`和`set`方法
```xml
<data>
    <import type="android.graphics.drawable.Drawable"/>
    <variable name="user"  type="com.example.User"/>
    <variable name="image" type="Drawable"/>
    <variable name="note"  type="String"/>
</data>
```
将会在生成的绑定类中产生`get`和`set`如下

```java
public abstract com.example.User getUser();
public abstract void setUser(com.example.User user);
public abstract Drawable getImage();
public abstract void setImage(Drawable image);
public abstract String getNote();
public abstract void setNote(String note);
```

#### ViewStubs

`ViewStub`s 和正常的View是不同的.它们在刚开始的时候是不可见的，当他们变的可见或者被明确的inflate之后，
它们会被另外一个layout中inflate的View替代。

因为`ViewStub`本质上在View层级中是不存在的，所以在绑定对象中的View必须也不存在。
因为Views是final的，所以`ViewStubProxy` 对象替代了`ViewStub`,给了开发者访问`ViewStub`
giving the developer access to the `ViewStub` when it exists and also access to the inflated View hierarchy when the `ViewStub` has been inflated.

当inflate其他的layout时，必须建立一个新的绑定来绑定新的layout。因此，`ViewStubProxy`必须在监听`ViewStub`的 `ViewStub.OnInflateListener`的同时建立绑定。
因为只有一个可以存在， `ViewStubProxy`允许开发者为它设置一个`OnInflateListener`，它会在建立绑定之后被调用

#### Advanced Binding

##### Dynamic Variables

有时候，不能立刻知道具体的绑定类。例如，一个`RecyclerView.Adapter`操作任意layout，这个时候我们不能知道具体的绑定类。
但是它必须被赋值给一个绑定的值在执行`onBindViewHolder(VH, int)`的时候。

在上面的例子中，所有RecyclerView绑定的layout有一个"item"变量，
`BindingHolder`类有一个`getBinding`方法返回基类`ViewDataBinding`
```java
public void onBindViewHolder(BindingHolder holder, int position) {
   final T item = mItems.get(position);
   holder.getBinding().setVariable(BR.item, item);
   holder.getBinding().executePendingBindings();
}
```

##### Immediate Binding

当一个变量或者一个可观察的东西改变时，对应的UI将会在下一帧之前被改变。
然而，有时候UI必须立刻被改变。为了强制进行这个改变，主动调用`executePendingBindings() `方法。

##### Background Thread

你可以修改你的数据model在后台线程中，只要它不是一个集合。
在操作的时候，数据绑定将会把变量/字段变成局部的，防止任何并发的问题发生。

### Attribute Setters

任何时候一个绑定的对象值改变了，在View层面上，产生的绑定类必须通过上面介绍的表达式调用set方法
数据绑定框架有许多方式来自定义调用set方法

#### Automatic Setters

对于某个属性来说，数据绑定尝试寻找`set属性`方法，和这个属性的namespace无关，只和这个属性的名字有关。

例如，一个和`TextView`的属性`android:text`关联的表达式，数据绑定将会寻找`setText(String)`方法，如果表达式返回一个`int`，
数据绑定将会寻找`setText(int)`方法。
注意，让表达式返回合适的类型，如果需要的话，可以使用类型转换。
如果这个属性不存在，数据绑定依旧不会抛出异常。通过数据绑定，你可以很容易的通过set方法，创造对应的属性。
例如，support包中的`DrawerLayout`不含有任何属性，但是有一大堆set方法。你可以使用set后面的属性名来作为对应的属性。
```xml
<android.support.v4.widget.DrawerLayout
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:scrimColor="@{@color/scrim}"
    app:drawerListener="@{fragment.drawerListener}"/>
```

#### Renamed Setters

一些属性有set方法，但命名方式不是set+属性名的方式。
对于这种方法，使用`BindingMethods`注解将属性和对应的set方法关联起来，
它会将一个带有`BindingMethod`注解的类，属性名称，该属性对应的方法名称三者关联起来。
例如，`android:tint`属性和`setImageTintList(ColorStateList)`方法相关联，不和`setTint()`方法关联
```java
@BindingMethods({
       @BindingMethod(type = android.widget.ImageView.class,
                      attribute = "android:tint",
                      method = "setImageTintList"),
})
```
由于Android框架属性名已经被确定，开发者重命名set方法是不可能的。

#### Custom Setters

一些属性需要自定义绑定逻辑。
例如， `android:paddingLeft`属性没有一个关联的set方法，但是有一个`setPadding(left, top, right, bottom)`方法存在。
一个有 `BindingAdapter`注解的 静态的绑定适配器方法 允许开发者定义 当调用set方法时 如何给这个属性赋值。

在Android属性中，`BindingAdapter`早已出现。例如，对于`paddingLeft`属性
```java
@BindingAdapter("android:paddingLeft")
public static void setPaddingLeft(View view, int padding) {
   view.setPadding(padding,
                   view.getPaddingTop(),
                   view.getPaddingRight(),
                   view.getPaddingBottom());
}
```
绑定适配器对自定义其他类型很有用。
例如，一个自定义loader可以加载完图片之后关闭这个线程。

当开发者创建的绑定适配器和数据绑定框架提供的默认适配器冲突时，将会覆盖默认适配器

你当然可以有一个接收多个参数的适配器
```java
@BindingAdapter({"bind:imageUrl", "bind:error"})
public static void loadImage(ImageView view, String url, Drawable error) {
   Picasso.with(view.getContext()).load(url).error(error).into(view);
}
```
```xml
<ImageView app:imageUrl="@{venue.imageUrl}"
                       app:error="@{@drawable/venueError}"/>
```
当imageUrl是一个string、error是一个drawable并且ImageView使用了**imageUrl** 和 **error**的时候，这个适配器将会被调用。

- 在进行匹配的时候，自定义namespaces将会被忽略.
- 你可以为Android namespace写对应的适配器.

在绑定适配器方法的handlers中，可以随意的获取旧的值。
一个获取旧的值和新的值的方法需要先声明该属性的所有旧的值，接着跟新的值
```java
@BindingAdapter("android:paddingLeft")
public static void setPaddingLeft(View view, int oldPadding, int newPadding) {
   if (oldPadding != newPadding) {
       view.setPadding(newPadding,
                       view.getPaddingTop(),
                       view.getPaddingRight(),
                       view.getPaddingBottom());
   }
}
```

可以参考[AttributeSettersActivity][6]

事件处理只被用于接口或者抽象类中的抽象方法。例如：
```java
@BindingAdapter("android:onLayoutChange")
public static void setOnLayoutChangeListener(View view, View.OnLayoutChangeListener oldValue,
       View.OnLayoutChangeListener newValue) {
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.HONEYCOMB) {
        if (oldValue != null) {
            view.removeOnLayoutChangeListener(oldValue);
        }
        if (newValue != null) {
            view.addOnLayoutChangeListener(newValue);
        }
    }
}
```
当一个listener有许多方法时，它必须被分离成多个listeners。
例如，`View.OnAttachStateChangeListener`有两个方法：
`onViewAttachedToWindow()` 和 `onViewDetachedFromWindow()`.
我们必须创建两个接口来区分他们不同的属性和handlers。
```java
@TargetApi(VERSION_CODES.HONEYCOMB_MR1)
public interface OnViewDetachedFromWindow {
    void onViewDetachedFromWindow(View v);
}

@TargetApi(VERSION_CODES.HONEYCOMB_MR1)
public interface OnViewAttachedToWindow {
    void onViewAttachedToWindow(View v);
}
```
为了让所有的属性都可以被设置，我们必须有三个不同的绑定适配器。因为修改一个listener将会影响另一个，
一个对应所有，然后另外两个分别对应每个属性。
```java
@BindingAdapter("android:onViewAttachedToWindow")
public static void setListener(View view, OnViewAttachedToWindow attached) {
    setListener(view, null, attached);
}

@BindingAdapter("android:onViewDetachedFromWindow")
public static void setListener(View view, OnViewDetachedFromWindow detached) {
    setListener(view, detached, null);
}

@BindingAdapter({"android:onViewDetachedFromWindow", "android:onViewAttachedToWindow"})
public static void setListener(View view, final OnViewDetachedFromWindow detach,
        final OnViewAttachedToWindow attach) {
    if (VERSION.SDK_INT >= VERSION_CODES.HONEYCOMB_MR1) {
        final OnAttachStateChangeListener newListener;
        if (detach == null && attach == null) {
            newListener = null;
        } else {
            newListener = new OnAttachStateChangeListener() {
                @Override
                public void onViewAttachedToWindow(View v) {
                    if (attach != null) {
                        attach.onViewAttachedToWindow(v);
                    }
                }

                @Override
                public void onViewDetachedFromWindow(View v) {
                    if (detach != null) {
                        detach.onViewDetachedFromWindow(v);
                    }
                }
            };
        }
        final OnAttachStateChangeListener oldListener = ListenerUtil.trackListener(view,
                newListener, R.id.onAttachStateChangeListener);
        if (oldListener != null) {
            view.removeOnAttachStateChangeListener(oldListener);
        }
        if (newListener != null) {
            view.addOnAttachStateChangeListener(newListener);
        }
    }
}
```
上面的例如有一些复杂，因为对应`View.OnAttachStateChangeListener`，View使用add和remove对应的listener 而不是使用set方法。
`android.databinding.adapters.ListenerUtil`这个类可以帮助你跟踪之前的listeners，所以它们可以在绑定适配器里移除。

用`@TargetApi(VERSION_CODES.HONEYCOMB_MR1)`注解`OnViewDetachedFromWindow` 和 `OnViewAttachedToWindow`，
数据绑定代码生成器知道这个listener只应该在 Honeycomb MR1和更新的版本上生成。
//对于`addOnAttachStateChangeListener(View.OnAttachStateChangeListener)`同样支持。
`setListener(View view, final OnViewDetachedFromWindow detach, final OnViewAttachedToWindow attach)`也能达到同样的效果。

### Converters

#### Object Conversions

当绑定表达式返回一个对象，将会从前面提到[automatic](#automatic-setters) ,[renamed](#renamed-setters),
和[custom](#custom-setters)中的选择set方法。这个对象会通过被选择的set方法转换成参数类型。

使用`ObservableMaps`来储存数据是很方便的一种方式。例如：
```xml
<TextView
   android:text='@{userMap["lastName"]}'
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```
`userMap`返回一个对象这个对象将会被自动转化成在set方法中找到的参数类型`setText(CharSequence)`，即被转化为`CharSequence`类型。
当参数类型存在冲突的时候，开发者需要在表达式中明确转化该类型

#### Custom Conversions

有些时候转化策略会自动转化为特殊的类型。例如，当设置背景颜色的时候
```xml
<View
   android:background="@{isError ? @color/red : @color/white}"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```
背景颜色使用`Drawable`类型，但是`color`属性是`int`类型。当需要一个`Drawable`却返回一个`int`的时候，
`int`会被转换为`ColorDrawable`类型，这个转化通过使用带有BindingConversion注解的静态方法来完成。
```java
@BindingConversion
public static ColorDrawable convertColorToDrawable(int color) {
   return new ColorDrawable(color);
}
```
注意转化只发生在set方法的时候，所以，该框架**不允许**像下面一样混用类型
```xml
<View
   android:background="@{isError ? @drawable/error : @color/white}"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"/>
```

### Contact me

**有谁知道Handler怎么翻译吗？欢迎发邮件到airzhaoyn@gmail.com告知**

**如果看到代码或者翻译中有什么问题，同样欢迎发邮件到airzhaoyn@gmail.com告知**

[0]: ./README_en.md
[1]: app/src/main/java/com/air/mvvmdemo/view/CustomBindingClassNameActivity.java
[2]: app/src/main/java/com/air/mvvmdemo/view/BaseActivity.java
[3]: app/src/main/java/com/air/mvvmdemo/view/IncludeActivity.java
[4]: app/src/main/java/com/air/mvvmdemo/view/QuoteActivity.java
[5]: app/src/main/java/com/air/mvvmdemo/view/ObservableModel.java
[6]: app/src/main/java/com/air/mvvmdemo/view/AttributeSettersActivity.java



