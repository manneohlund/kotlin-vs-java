@title[Kotlin vs Java]

![Kotlin vs Java](https://github.com/manneohlund/kotlin-vs-java/blob/master/assets/kotlin-vs-java.png?raw=true)

An language feature battle

---

### Why Kotlin?

Kotlin fixes a series of issues that Java suffers from

@ul

- Null references are controlled by the type system.
- No raw types
- Arrays in Kotlin are invariant
- Kotlin has proper function types, as opposed to Java's SAM-conversions
- Use-site variance without wildcards
- Kotlin does not have checked exceptions

@ulend

---

### What Kotlin has that Java does not 🍒

@ul

- Null-safety
- Smart casts
- Singletons
- Extension functions
- Range expressions
- Companion objects
- Data classes
- String templates

@ulend

---

### More what Kotlin has that Java does not

- Lambda expressions + Inline functions
- First-class delegation
- Type inference for variable and property types
- Declaration-site variance & Type projections
- Operator overloading
- Separate interfaces for read-only and mutable collections
- Coroutines

---

### What Java has that Kotlin does not

@ul

- Checked exceptions
- Primitive types that are not classes
- Static members
- Non-private fields
- Wildcard-types
- Ternary-operator a ? b : c

@ulend

---

@title[Syntax]

Kotlin

```Kotlin
fun main(args: Array<String>) {
  println("Hello, ${args[0]}")
}
```

Java

```java
public static final void main(String[] args) {
  System.out.println(String.format("Hello, %s", args[0]))
}
```

---

@title[Kotlin variable syntax]

val & var [Properties](https://kotlinlang.org/docs/reference/properties.html)

```Kotlin
// Explicit
const val hello: String = "World" // Compile time constant
val hello: String = "World" // Runtime constant
var android: String = "Kotlin"

// Implicit
val hello = "World" // Runtime constant
var android = "Kotlin"

// Nullable ?
var name: String? = null

// Lateinit
lateinit var name: String // Assign later in code, can't be null
```

[Basic types](https://kotlinlang.org/docs/reference/basic-types.html)

---

@title[Kotlin vs Java syntax]

Dry, clean, readable

Kotlin

```Kotlin
const val file = File()
```

Java

```java
static final File file = new File()
```

---

### [Primary constructor](https://kotlinlang.org/docs/reference/classes.html#constructors)

```Kotlin
class Person(val name: String) { // Primary constructor in header
    constructor(name: String, parent: Person) : this(name) { // Secondary constructor
        ...
    }
}
```

---

### Open & Override

Classes and functions are by default always final and must have open modifier to be inherited or overridden.

```Kotlin
open class A {
    open fun foo(i: Int = 10) { }
}
```

```Kotlin
class B : A() {
    override fun foo(i: Int) {  }  // no default value allowed
}
```

---

### [Functions](https://kotlinlang.org/docs/reference/functions.html)

```Kotlin
fun multiply(multiplicator: Int, multiplicand: Int): Int {
    return multiplicator * multiplicand
}
```

Usage
```Kotlin
multiply(1,2)
multiply(multiplicator = 1, multiplicand = 2)
multiply(multiplicand = 2, multiplicator = 1)
```

---

@title[Null safe quote]

> "I call it my billion-dollar mistake. It was the invention of the null reference in 1965."
Sir Tony Hoare

---

### Null safe

```Kotlin
var a: String = "abc"
a = null // compilation error

var b: String? = "abc"
b = null // ok
```

Usage

```Kotlin
val l = a.length // ok
val l = b.length // error: variable 'b' can be null
```

---

### Checking for null in conditions

Explicitly check if b is null

```Kotlin
val l = if (b != null) b.length else -1
```

Safe call operator, ?.

```Kotlin
b?.length
```

---

### Elvis operator

?:

```Kotlin
val name = bob?.department?.head?.name ?: "Unknown"
```

---

### The !! Operator

Throws an NPE if b is null

```Kotlin
val l = b!!.length
```

---

### Safe & smart cast

Safe casts that return null

```Kotlin
val aInt: Int? = a as? Int
```

Smart cast, no ((String)x).length

```Kotlin
fun demo(x: Any) {
    if (x is String) {
        print(x.length) // x is automatically cast to String
    }
}
```

---

### Singletons & Extensions

MySingleton.kt
```Kotlin
object MySingleton { // Note object
    fun add(number: Int): Int = 10 + number
}
```

MySingleton+Extensions.kt
```Kotlin
fun MySingleton.multiply(multiplicand: Int, multiplicator: Int) -> Int {
    return multiplicand * multiplicator
}
```

Usage
```Kotlin
val sum = MySingleton.add(2)
val product = MySingleton.multiply(1, 2)
```

---

### Generics

```kotlin
inline fun <reified T : Any> loadStyle(inputStream: InputStream): T {
  return Gson().fromJson(InputStreamReader(inputStream), object : TypeToken<T>() {}.type)
}
```

---

@title[Links]

[Frost Mobile Guide](https://github.com/FrostDigital/frost-mobile-guide)

[Frost Android Kotlin Style Guide](https://github.com/FrostDigital/frost-mobile-guide/wiki/Frost-Android-Kotlin-Style-Guide)

---

### [Lets see some code online](https://try.kotlinlang.org/#/Examples/Hello,%20world!/Reading%20a%20name%20from%20the%20command%20line/Reading%20a%20name%20from%20the%20command%20line.kt)
