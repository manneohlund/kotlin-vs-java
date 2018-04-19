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

### What Kotlin has that Java does not

@ul

- Null-safety
- Smart casts
- Extension functions
- String templates
- Singletons
- Lambda expressions + Inline functions = performant custom control structures
- Properties
- Primary constructors
- Range expressions
- Companion objects
- Data classes
- First-class delegation
- Type inference for variable and property types
- Declaration-site variance & Type projections
- Operator overloading
- Separate interfaces for read-only and mutable collections
- Coroutines

@ulend

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

val & var

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

@title[Null safe]

> "I call it my billion-dollar mistake. It was the invention of the null reference in 1965." // Sir Tony Hoare




---

@title[Generics]

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
