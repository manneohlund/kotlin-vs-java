@title[Kotlin vs Java]

![Kotlin vs Java](https://github.com/manneohlund/kotlin-vs-java/blob/master/assets/kotlin-vs-java.png?raw=true)

---

### Why Kotlin?

Modern, Less code, More readable, Smarter

---

@title[Kotlin fixes]

Kotlin fixes a series of issues that Java suffers from

@ul

- [Null references are controlled by the type system](https://kotlinlang.org/docs/reference/null-safety.html)
- [No raw types](https://kotlinlang.org/docs/reference/java-interop.html#java-generics-in-kotlin)
- [Arrays in Kotlin are invariant](https://kotlinlang.org/docs/reference/basic-types.html#arrays)
- [Kotlin has proper function types, as opposed to Java's SAM-conversions](https://kotlinlang.org/docs/reference/lambdas.html#function-types)
- [Use-site variance without wildcards](https://kotlinlang.org/docs/reference/generics.html#use-site-variance-type-projections)
- [Kotlin does not have checked exceptions](https://kotlinlang.org/docs/reference/exceptions.html#exceptions)

@ulend

---

### What Kotlin has that Java does not 🍒

@ul

- [Null-safety](https://kotlinlang.org/docs/reference/null-safety.html)
- [Smart casts](https://kotlinlang.org/docs/reference/typecasts.html)
- [Singletons + Companion objects](https://kotlinlang.org/docs/reference/object-declarations.html)
- [Extension functions](https://kotlinlang.org/docs/reference/extensions.html)
- [Range expressions](https://kotlinlang.org/docs/reference/ranges.html)
- [Data classes](https://kotlinlang.org/docs/reference/data-classes.html)
- [String templates](https://kotlinlang.org/docs/reference/basic-types.html#strings)
- [Other cool stuff](https://kotlinlang.org/docs/reference/idioms.html) 🍿

@ulend

---

### More what Kotlin has that Java does not

- [Lambda expressions](https://kotlinlang.org/docs/reference/lambdas.html) + [Inline functions](https://kotlinlang.org/docs/reference/inline-functions.html)
- [First-class delegation](https://kotlinlang.org/docs/reference/delegation.html)
- [Type inference for variable and property types](https://kotlinlang.org/docs/reference/basic-types.html)
- [Declaration-site variance & Type projections](https://kotlinlang.org/docs/reference/generics.html)
- [Operator overloading](https://kotlinlang.org/docs/reference/operator-overloading.html)
- [Separate interfaces for read-only and mutable collections](https://kotlinlang.org/docs/reference/collections.html)
- [Coroutines](https://kotlinlang.org/docs/reference/coroutines.html)

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

### Kotlin is 100% interoperable with Java

![Kotlin java](https://cdn-images-1.medium.com/max/1200/1*HYEQHnCinTfXmOV0TopK6A.jpeg)

---

@title[Syntax]

Kotlin

```kotlin
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

```kotlin
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

```kotlin
val file = File()
```

Java

```java
public static final File file = new File()
```

[Kotlin visibility modifiers](https://kotlinlang.org/docs/reference/visibility-modifiers.html#visibility-modifiers)

---

### [Primary constructor](https://kotlinlang.org/docs/reference/classes.html#constructors)

```kotlin
class Person(val name: String) { // Primary constructor in header
    constructor(name: String, parent: Person) : this(name) { // Secondary constructor
        ...
    }
}
```

---

### Open & Override

Classes and functions are by default always final and must have open modifier to be inherited or overridden.

```kotlin
open class A {
    open fun foo(i: Int = 10) { }
}
```

```kotlin
class B : A() {
    override fun foo(i: Int) {  }  // no default value allowed
}
```

---

### [Functions](https://kotlinlang.org/docs/reference/functions.html)

```kotlin
fun multiply(multiplicator: Int, multiplicand: Int): Int {
    return multiplicator * multiplicand
}
```

Usage
```kotlin
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

```kotlin
fun getLastFour(employee: Employee?) = 
  employee?.address?.zip?.lastFour 
    ?: throw Exception("Missing data")
```

---

### Null safe Kotlin

```kotlin
var a: String = "abc"
a = null // compilation error

var b: String? = "abc"
b = null // ok
```

Usage

```kotlin
val l = a.length // ok
val l = b.length // error: variable 'b' can be null
```

---

### Checking for null in conditions

Explicitly check if b is null

```kotlin
val l = if (b != null) b.length else -1
```

Safe call operator, ?.

```kotlin
b?.length
```

---

### Elvis operator

?:

```kotlin
val name = bob?.department?.head?.name ?: "Unknown"
```

---

### The !! Operator

Throws an NPE if b is null

```kotlin
val l = b!!.length
```

---

### Safe & smart cast

Safe casts that return null

```kotlin
val aInt: Int? = a as? Int
```

Smart cast, no ((String)x).length

```kotlin
fun demo(x: Any) {
    if (x is String) {
        print(x.length) // x is automatically cast to String
    }
}
```

---

### Singletons & Extensions

MySingleton.kt
```kotlin
object MySingleton { // Note object
    fun add(number: Int): Int = 10 + number
}
```

MySingleton+Extensions.kt
```kotlin
fun MySingleton.multiply(multiplicand: Int, multiplicator: Int) -> Int {
    return multiplicand * multiplicator
}
```

Usage
```kotlin
val sum = MySingleton.add(2)
val product = MySingleton.multiply(1, 2)
```

---

### [Range expressions](https://kotlinlang.org/docs/reference/ranges.html)

```kotlin
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

```kotlin
data class Person(val name: String, val age: Int)
```

equals(), hashCode(), toString(), copy()

+++

### Data Classes and Destructuring Declarations

```kotlin
val jane = Person("Jane", 35) 
val (name, age) = jane
println("$name, $age years of age") // prints "Jane, 35 years of age"
```

+++

### Java POJO

```kotlin
data class Person(val name: String, val age: Int)
```

```java
public class Person {
   private String name;
   private int age = 0;

   public Person(String name, int age) {
       this.name = name;
       this.age = age;
   }

   public String getName() {
       return name;
   }

   public void setName(String name) {
       this.name = name;
   }

   public int getAge() {
       return age;
   }

   public void setAge(int age) {
       this.age = age;
   }

   @Override
   public boolean equals(Object o) {
       if (this == o) return true;
       if (o == null || getClass() != o.getClass()) return false;

       Person person = (Person) o;

       if (name != null ? !name.equals(person.name) : person.name != null) return false;
       if (age != 0 ? age != person.age : person.age != 0) return false;
   }

   @Override
   public int hashCode() {
       int result = name != null ? name.hashCode() : 0;
       result = 31 * result + age;
       return result;
   }

   @Override
   public String toString() {
       return "Person{" +
               "name='" + name + '\'' +
               ", age='" + age + '\'' +
               '}';
   }
}
```

---

### Other cool stuff 🍿

Traversing a map/list of pairs

```kotlin
for ((k, v) in map) {
    println("$k -> $v")
}
```

+++

Execute if not null

```kotlin
val value = ...

value?.let {
    ... // execute this block if not null
}
```

+++

Return on when statement

```kotlin
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

```kotlin
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

```kotlin
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

@title[Links]

[Frost Mobile Guide](https://github.com/FrostDigital/frost-mobile-guide)

[Frost Android Kotlin Style Guide](https://github.com/FrostDigital/frost-mobile-guide/wiki/Frost-Android-Kotlin-Style-Guide)

---

### [Lets see some code online](https://try.kotlinlang.org/#/Examples/Hello,%20world!/Reading%20a%20name%20from%20the%20command%20line/Reading%20a%20name%20from%20the%20command%20line.kt)

@title[The End]

Ok 👋

---
