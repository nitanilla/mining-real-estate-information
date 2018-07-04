Gridstone Kotlin Style Guide
============================

A style guide for developers at Gridstone who write in Kotlin.

Naming
------

- Variable names are `camelCase`
- Type names are `CaptialCamelCase`
- Function names are `camelCase`
- Constants are `SCREAMING_SNAKE_CASE`
- Enum entries are `SCREAMING_SNAKE_CASE`

```kotlin
const val GREETING = "Hello, world!"

class Foo {
  private val secret = "shhh"

  fun greetTheWorld() {
    println(GREETING)
  }
}

enum Bar { FIRST_BAR, SECOND_BAR }
```

### Hungarian notation

Do not use [Hungarian notation](http://jakewharton.com/just-say-no-to-hungarian-notation/).

### Acronyms

When naming things, treat acroyms as full words.
```kotlin
// OK
val request = XmlHttpRequest()
// Not OK
val request = XMLHTTPRequest()
```

Formatting
----------

### Line length

Lines may be no more than 100 characters in length.
- Preserves readability for individual lines
- Ensures that two files can be displayed side-by-side on most displays

### Indentation

Use 2 space characters for indentation. Use 4 spaces for continuation indents.

```kotlin
fun foo() {
  val bar = Observable.just(1)
      .map { it.toString() }
}
```

- Using spaces instead of tabs means code must look good regardless of tab-length settings
- Using 2 spaces helps maximise the use of our limited horizontal real estate

### Aligning parameters

When parameters of functions or classes extends into multiple lines those parameters must be
aligned.

```kotlin
data class Foo(val bar1: Int,
               val bar2: String,
               val bar3: Float)

fun bar(baz1: Int,
        baz2: String,
        baz3: Float) {
  // ...
}

val foo = bar(baz1,
              baz2,
              baz3)
```
It's also acceptable to align parameters as
```kotlin
fun foo(bar1, bar2
        bar3, bar4)
```

- Alignment is especially useful for data classes which may have many properties

### Aligning invocations

When methods are invoked in a chain they must be aligned.
```kotlin
// OK
val foo: List<String> = list
    .filter {
      it > 10
    }
    .map {
      it.toString()
    }

// Not OK
val bar: List<String> = list.filter {
    it > 10
}.map {
    it.toString()
}
```

### Short things

Short methods and classes may be declared on a single line.

```kotlin
data class Foo(val foo1: Int, val foo2: String)

fun bar(): String = "What would you like to drink?"
```

### Colons

Use a space either side of a colon when declaring inheritance. Use only a space after a colon
when declaring a variable/method type.
```kotlin
interface Foo<out T : Any> : Bar {
  fun foo(a: Int): T
}
```

### Blank lines

Lines that are intentionally blank for formatting purposes should contain no characters at all.
Never use more than one blank line in a row.

### Imports

Always use explicit imports. Never use wildcard imports.
```kotlin
// OK
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup

// Not OK
import android.view.*
```

Type Inference
--------------

Type inference is powerful but can be easily abused. As a general rule, type inference should
only be used when it's explicitly clear what the resulting type will be.

```kotlin
// OK
fun foo() = "Hello."
val bar = Bar()

// Not OK
val baz = generateBaz()
```

Under any other the circumstances the type must be explicitly declared, even if it's not
necessary for the compiler.

Lambdas
-------

### Avoiding parenthesis

Whenever possible lambdas should be placed outside of parentheses.
```kotlin
// OK
list.filter { it > 10 }
// Not OK
list.filter({ it > 10 })
```

### Using `it`

The implicit `it` parameter given to lambdas should be used judiciously. Unless a lambda is very
short, consider overriding `it` with a more meaningful name.
```kotlin
// Specifying the lambda parameter of `user` rather than `it` helps this code.
webServices.getUsers()
    .flatMapIterable { it }
    .map { user ->
      when {
        user.isAdmin() -> Admin(user)
        user.isManager() -> Manager(user)
      }
    }
```

### Unused parameters

Unused lambda parameters should be replaced with an underscore.
```kotlin
foo { _, _, bar -> println(bar) }
```

### Return statements

Return values inside of lambdas have the potential to be confusing to readers. If a lambda returns a
value and has more than one line then a return tag must be explicitly provided.
```kotlin
// OK
list.filter { it > 3 }
    .map {
      val x = it * 4
      return@map x + 7
    }

// Not OK
list.filter { it > 3 }
    .map {
      val x = it * 4
      x + 7
    }
```

Control Flow
------------

### Prefer an early exit

Whenever possible return from a method rather than creating additional levels of indentation with
conditions.
```kotlin
// OK
fun foo(bar: Int) {
  if (bar < 3) return

  // Do other stuff.
}

// Not OK
fun foo(bar :Int) {
  if (bar >= 3) {
    // Do other stuff.
  }
}
```

### `If` statements

Short `if` statements may be declared on a single line.
```kotlin
fun foo(bar: Bar) {
  if (bar.qualifiesForThing()) bar.doThing()
  else bar.doSomethingElse()
}
```

However if either the `if` or the `else` section take up mutiple lines then both must make use of
curly braces.
```kotlin
// OK
fun foo(bar: Bar): Int {
  if (bar.qualifiesForThing()) {
    val baz = bar.getThing()
    return baz.calcSomeInt()
  } else {
    return 3
  }
}

// Not OK
fun foo(bar: Bar): Int {
  if (bar.qualifiesForThing()) {
    val baz = bar.getThing()
    return baz.calcSomeInt()
  } else return 3
}
```

If a variable is set as the result of an `if` statement then prefer the formatting:
```kotlin
val foo: String = if (something()) bar else baz
```
If the condition is long then prefer:
```kotlin
val foo: String =
    if (someCalculationThatIsLong() > someOtherLongCalculation()) bar
    else baz
```

Comments
--------

It is not manditory to comment every section of code written. People often forget that when writing
comments, they commit to maintaining not only their code but also their documentation. Comments that
are out-of-date with their corresponding code are potentially dangerous.

Methods such as `size()` on a collection don't need comments, as their purpose is immediately apparent
to the user. Adding a commment only adds noise.

### API documentation

When documenting a class, function, or property to be used by others
[KDoc style](https://kotlinlang.org/docs/reference/kotlin-doc.html) should be used.
```kotlin
/**
 * Calculates bounding box that contains both provided [Rect]s
 */
fun getEnclosingBounds(first: Rect, second: Rect): Rect
```
It is often not necessary to provide `@param`,`@return` tags, as they can result in needless duplication.

### Inline documentation

Comments intended to aid someone who is reading code should use C++ style `// comments`. For formatting
purposes there should be a space between the slashes and the content.
```kotlin
// This is a helpful one line comment.
```

### TODO commments

`TODO` Comments should either be in the format of
```kotlin
// TODO Some task that needs to be done.
```
or make use of Kotlin's [TODO()](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-t-o-d-o.html)
function
```kotlin
TODO("Some task that needs to be done.")
```

Function Declarations
---------------------

Many of the assertions below are based on
[John Carmarck's thoughts](http://number-none.com/blow/john_carmack_on_inlined_code.html).

### Length

If a function has explicit inputs, outputs, and doesn't modify external state then don't be afraid of
its length. These are the easiest functions to test and often a long section of linear processing is
neater than declaring many "helper" functions that are only used once.

### Avoid helper functions

If a function is only ever called by one other function, that function should most likely become a
[local function](https://kotlinlang.org/docs/reference/functions.html#local-functions).

If a function is only ever called in one place consider inlining it. This doesn't mean appending
Kotlin's `inline` keyword but rather refers to taking the contents of the method and replacing them
where the function was originally invoked. If that section of code could later be used as a funcion
in many places then consider pulling it out again, but only when necessary.

