@title[Kotlin vs Java]

![Kotlin vs Java](https://github.com/manneohlund/kotlin-vs-java/blob/master/assets/kotlin-vs-java.png?raw=true)

---

### Why Kotlin?

Modern, Less code, More readable, Smarter

---

@title[Kotlin fixes]

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
- Singletons + Companion objects
- Extension functions
- Range expressions
- Data classes
- String templates
- Other cool stuff 🍿

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

### Null safe Java

```java
public String getLastFour(Employee employee) {
    if(employee != null) {
        Address address = employee.getPrimaryAddress();
        if(address != null) {
            ZipCode zip = address.getZipCode();
            if(zip != null) {
                return zip.getLastFour()
            }
        }
    }
    throw new Exception("Missing data");
}
```

---

### Null safe Java 8

```java
public String getLastFour(Optional<Employee> employee) {
    return employee.flatMap(employee -> employee.getPrimaryAddress())
                   .flatMap(address -> address.getZipCode())
                   .flatMap(zip -> zip.getLastFour())
                   .orElseThrow(() -> new FMLException("Missing data"));
}
```

---

### Null safe Kotlin 🚀

Can be as one line single expression

```Kotlin
fun getLastFour(employee: Employee?) = 
  employee?.address?.zip?.lastFour 
    ?: throw Exception("Missing data")
```

---

### Null safe Kotlin

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

### [Range expressions](https://kotlinlang.org/docs/reference/ranges.html)

```Kotlin
for (i in 1..4) print(i)     // prints "1234"
for (i in 4..1)              // prints nothing
for (i in 4 downTo 1)        // prints "4321"
for (i in 1..4 step 2)       // prints "13"
for (i in 4 downTo 1 step 2) // prints "42"
for (i in 1 until 10)        // i in [1, 10), 10 is excluded
```

---

### [Data Classes](https://kotlinlang.org/docs/reference/data-classes.html)

We frequently create classes whose main purpose is to hold data. 
In such a class some standard functionality and utility functions are often mechanically derivable from the data.

```Kotlin
data class User(val name: String, val age: Int)
```

+++

### Data Classes and Destructuring Declarations

```Kotlin
val jane = User("Jane", 35) 
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"
```

---

### Other cool stuff 🍿

Traversing a map/list of pairs

```Kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
```

+++

Execute if not null

```Kotlin
val value = ...

value?.let {
    ... // execute this block if not null
}
```

+++

Return on when statement

```Kotlin
fun transform(color: String): Int {
    return when (color) {
        "Red" -> 0
        "Green" -> 1
        "Blue" -> 2
        else -> throw IllegalArgumentException("Invalid color param value")
    }
}
```
or
```kotlin
fun transform(color: String) = when (color) {
    "Red" -> 0
    "Green" -> 1
    "Blue" -> 2
    else -> throw IllegalArgumentException("Invalid color param value")
}
```

+++

'if' expression

```Kotlin
fun foo(i: Int) {
    val result = if (i == 1) {
        "one"
    } else if (i == 2) {
        "two"
    } else {
        "three"
    }
}
```

+++

Typealias

```Kotlin
typealias JsonData = String
typealias StatusCode = Int
typealias Error = String

typealias Success = (JsonData) -> Unit
typealias Error = (StatusCode, Error) -> Unit
```

+++

Generics

```kotlin
inline fun <reified T : Any> loadStyle(inputStream: InputStream): T {
  return Gson().fromJson(InputStreamReader(inputStream), object : TypeToken<T>() {}.type)
}
```

---

### Kotlin Android

Java

```Java
public class MainActivity extends AppCompatActivity {
 
   @Override
   protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
       setContentView(R.layout.activity_main);
       Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
       setSupportActionBar(toolbar);
   }
}
```

+++

Kotlin

No findViewById or Butterknife needed

```Java
class MainActivity : AppCompatActivity() {
 
   override fun onCreate(savedInstanceState: Bundle?) {
       super.onCreate(savedInstanceState)
       setContentView(R.layout.activity_main)
       setSupportActionBar(toolbar)
   }
}
```

---

@title[The End]

Ok 👋

---

@title[Links]

[Frost Mobile Guide](https://github.com/FrostDigital/frost-mobile-guide)

[Frost Android Kotlin Style Guide](https://github.com/FrostDigital/frost-mobile-guide/wiki/Frost-Android-Kotlin-Style-Guide)

---

### [Lets see some code online](https://try.kotlinlang.org/#/Examples/Hello,%20world!/Reading%20a%20name%20from%20the%20command%20line/Reading%20a%20name%20from%20the%20command%20line.kt)
