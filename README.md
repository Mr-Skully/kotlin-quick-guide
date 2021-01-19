![Kotlin Quick Guide](https://socialify.git.ci/Mr-Skully/kotlin-quick-guide/image?description=1&font=Raleway&owner=1&pattern=Floating%20Cogs&theme=Light)
![visitors](https://visitor-badge.glitch.me/badge?page_id=mr-skully.kotlin-quick-guide)  ![license](https://img.shields.io/github/license/Mr-Skully/kotlin-quick-guide)

This is a quick start guide to Kotlin for people with prior coding experience (in any other language). I compiled what I learned from different sources like Kotlin Koans and JetBrains Academy, as a quick reference while working on coding challenges or Android applications. This guide is in no way a complete reference to Kotlin, but it probably will be sufficient for new users. I've assumed you already know programming in some other language, so I have skipped *explanations* for concepts like mutability and lambda expressions. However, if you are new to such terms, a simple web search will definitely help you undertand them.   

A sample [Hello-World](https://github.com/Mr-Skully/kotlin-quick-guide/tree/main/src) program has been included in the `src` directory to give you an idea of how Kotlin files and packages look like.  

| Table of Contents |
| ----------------- |
| [Basic Facts](#basic-facts) |
| [Values and Variables](#values-and-variables) |
| [Data Types](#data-types) |
| [Type Conversion](#type-conversion) |
| [Type Inference](#type-inference) |
| [Ranges](#ranges) |
| [Regex](#regex) |
| [BigInteger](#biginteger) |
| [Null Safety](#null-safety) |
| [Conventions](#conventions) |
| [Standard Input/Output](#standard-inputoutput) |
| [Functions and Lambda Expressions](#functions-and-lambda-expressions) |
| [Standard Library](#standard-library) |
| [Arrays](#arrays) |
| [Control Flow Statements](#control-flow-statements) |
| [Object Oriented Programming](#object-oriented-programming) |
| [Collections](#collections) |
| [Exceptions](#exceptions) |
| [Working With Files](#working-with-files) |
| [References](#references) |
| [Learn Kotlin](#learn-kotlin) |
  
  
## Basic Facts
- Blocks of code are enclosed in curly braces, `{...}`

- Each statement should start on a new line

- There are three types of comments in Kotlin:
```kotlin
// This is a single line comment

/* This is an example of
   a multiline comment. */

/**
  * These are
  * documentation comments.
  */
```

- `&&`, `||`, `!` and `xor` represent the logical operators - *and*, *or*, *not* and *xor*.


## Values and Variables
- `val` is used to declare **read-only** values.
```kotlin
val name = "Kotlin"
name = "Programming"   // won't work, as 'name' is read-only and cannot be reassigned
```

- `var` is used to declare **mutable** variables. You can reassign the variables with values of the same type as the initial value.
```kotlin
var language = "English"
language = "Klingon"   // this is possible
language = 10   // won't work, as language is a String variable
```

- The variables type is inferred by the compiler. This is called **type inference**.

- The type of a variable can be specified, if required, while declaring it. The type should be specified if the variable is not initialized during declaration, as the compiler cannot automatically infer the type.
```kotlin
var name: String = "Kotlin"
val num: Int = 999
val foo   // won't work, as type can't be inferred
val character: Char
character = 'A'   // works as expected
```
- If you create a variable and assign an object to it, the new variable can point to the same object as well. This is called **copying by reference**. In other words, the `=` sign does not copy the object itself, it only copies a reference to it.
```kotlin
val msg1 = "Hey"
val msg2 = msg1
// msg1 and msg2 will both point to a single object in memory, the String "Hey".
```

- If the object is **immutable**, you cannot change it, but you can use another object and assign this new object to the same variable. When you reassign the variable, it will point to the new object and other variables will still point to the old object. Standard types such as strings or numbers are immutable, so it's safe to copy them by reference. The behavior of mutable objects is different. If you modify an object from one variable, the other assigned variables continue to point to that object, so they will also reflect the same changes.

- The comparison operators `==` and `!=` checks for **structual equality**, while `===` and `!==` checks for **referential equality**.
```kotlin
val blue = Box(3)
val green = blue   // object reference is copied
val red = Box(3)

println(blue == green)  // true
println(blue === green) // true, as both point (refer) to the same object
println(blue == red)   // true
println(blue === red)  // false, they point (refer) to different objects

var two = 2
var anotherTwo = 2

println(two === anotherTwo) // true, because the '===' equality check is equivalent to the '==' check for primitive types
two = two + 1
println(two === anotherTwo) // false
```

- The `val` keyword implies an **immutable reference** to the object. The `var` keyword implies a **mutable reference** to a variable, so you can reassign it.

- Kotlin supports prefix and postfix increment/decrement operators (`++` and `--`) on variables.

## Data Types

- The names of Kotlin datatypes start with a capital letter.

- Types:   
`Byte`: 8 bits (1 byte), Range: -128 to 127  
`Short`: 16 bits (2 bytes), Range: -32768 to 32767  
`Int`: 32 bits (4 bytes), Range: −(2<sup>31</sup>) to (2<sup>31</sup>)−1  
`Long`: 64 bits (8 bytes), Range: −(2<sup>63</sup>) to (2<sup>63</sup>)−1  
`Float`: 32 bits (4 bytes), 6-7 significant decimal digits  
`Double`: 64 bits (8 bytes), 15-16 significant decimal digits  
`Char`: 16 bits (2 bytes), represents a 16-bit Unicode character  
`Boolean`: size is machine-dependent  
`String`: size depends on the string

- Strings are enclosed in double quotes, `"..."`.

- Characters are enclosed in single quotes, `'_'`.

- Fractional numbers are inferred as `Double` by default. Explicitly specify the type, or use the suffix `f` or `F` to use `Float` instead.

- `Long` is used by the compiler only if the value won't fit in an `Int` variable. To use `Long` with a small value, explicitly specify the type of the variable, or use the suffix `l` or `L` with the value.

- Underscores can be used to divide the a number into blocks for easier readability. `1_000_000` is the same as `1000000`.

- Types in Kotlin are organized into a hierarchy of subtype-supertype relationships. Supertype is a type that specifies some common characteristics and rules of behavior that every subtype will follow.

- `Number` is a supertype for all types that represent numeric value. For example, `Int`, `Float` and `Double` are subtypes of `Number` type.

- The type checker of the Kotlin compiler also enforces supertype-subtype relationships. For example, to a function  waiting for an argument of type `Number`, you can pass its subtype, `Int`:
```Kotlin
fun calc(number: Number) { /*...*/ }

val number: Int = 1
calculate(number)
```

- `Any` is a supertype for all non-nullable types in Kotlin. `Any?` is a supertype for `Any` that includes every other nullable type.

- `Unit` is the equivalent of the `void` type found in many other programming languages. It is the return type of a function that does not return any meaningful value. If the return type of a function is not specified, it is inferred to be `Unit`. A `return` statement is not required for such functions as they are returned implicitly. `Unit` is also a subtype of `Any`.

- `Nothing` is a type that has no instances, and are used in functions like `fail()` or expressions like `throw`, which doesn't return control. Any code following an expression of type `Nothing` is unreachable. When you call a function with a `Nothing` return type, the compiler won't execute any code beyond this call.

- If you use `null` to initialize a value of an inferred type and there's no other information that can be used to determine a more specific type, the compiler will infer the `Nothing?` type:
```kotlin
val x = null           // type: Nothing?
val l = listOf(null, null)   // type: List<Nothing?>
```

- In Kotlin, `0` is not the same as `false`. So you cannot assign a `Int` value to a `Boolean` variable.

- Small errors may accumulate after operations involving `Float` and `Double` types. Generally, avoid using `==` in expressions involving floating-point operations.
```kotlin
val one = 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1 + 0.1
println(one) // 0.9999999999999999
// one == 1.0 will return false
```

- A `Char` can be also created by using its hexadecimal code in the [Unicode table](https://unicode-table.com/en/). They are interconvertible with `Int` values.
```kotlin
val alphabet = '\u0041'     // represents 'A'
```

- `Int` numbers can be added to characters, but the reverse is not true.
```kotlin
var ch = 'a'

val ch1 = ch + 1      // 'b'
val ch2 = 1 + ch      // Error

ch += 2               // 'c'
```

- You can compare `Char` using relational operators according to their position in the Unicode table.

- The `Char` class has built-in utility functions like `isDigit()`, `isLetter()`, `isLetterOrDigit()`, `isWhitespace()`, `isUpperCase()`, `isLowerCase()`, `toUpperCase()` and `toLowerCase()`.

- `String` has a property `length` that stores the number of characters in the string. Individual elements can be accessed using their indices. It also has functions like `first()`, `last()` and `lastIndex()` to improve readability.
```kotlin
val text = "Hello!"

println(text.length)      // 6
println(text.first())     // H
println(text.last())      // !
println(text.lastIndex()) // 5
```

- Individual characters of a `String` can't be changed, because it is an immutable type.

- `String` objects can be concatenated using the `+` operator. Values of other types can also be appended to a `String` using the `+` operator, but the expression must start with the `String`.
```kotlin
val firstName = "John"
val lastName = "Doe"
val fullName = lastName + ", " + firstName      // Doe, John
val userName = "johnny" + true + 69             // johnnytrue69
val nickname = 8 + "ball"                   // Error, as a string can't be added to an Int
```

- Kotlin supports string templates. Variables can be used directly in a `String` by prefixing the dollar sign (`$`) to the variable name. Similarly, expressions can be used in a `String` by enclosing them in curly braces after the dollar sign.
```kotlin
val name = "John"

println("My name is $name.")                      // My name is John.
println("My name has ${name.length} letters.")    // My name has 4 letters.
```

- The `substring()` method of a `String` accepts **startIndex** and **lastIndex** as arguments and returns the substring that starts at the **startIndex** and ends right before the **lastIndex**. If **lastIndex** is omitted, the default value (length of the original string) is used.

- The `substringBefore()` and `substringAfter()` functions of `String` accept a **delimiter** as argument and return a `String` before/after the *first occurrence* of the specified **delimiter**. If the `String` does not contain the delimiter, the entire `String` is returned. Similarly, the `substringBeforeLast()` and `substringAfterLast()` methods return a `String` before or after the *last occurrence* of the delimiter. If a second argument is provided to these methods, it is returned if the **delimiter** is not found in the `String`.

- The `replace()` method of a `String` replaces all occurrences of the first argument in the `String` with the second argument. Similarly, `replaceFirst()` replaces the first occurrence of the first argument with the second, and skips the rest.

- The `toLowerCase()` and `toUpperCase()` methods of a `String` returns a `String` with its case converted accordingly.

- The `repeat()` method of `String` allows you to repeat a `String` without using loops.
```kotlin
print("Hey".repeat(5))      // HeyHeyHeyHeyHey
```

- A `CharArray` can be converted to a `String` using `String()`, and a `String` can be converted to a `CharArray` using the `toCharArray()` method. The `toTypedArray()` method can be used to convert an list of `String` to a `TypedArray`.
```kotlin
val chars = charArrayOf('A', 'B', ' ', 'C', 'D')
val text = String(chars)                                        // "AB CD"
val charsFromString = text.toCharArray()                        // { 'A', 'B', ' ', 'C', 'D' }
val words1: List<String> =  text.split(" ")                     // { "AB", "CD" }
val words2: Array<String> = text.split(" ").toTypedArray()      // { "AB", "CD" }
```

- You can iterate through a `String` using a range of indices, array of indices, or using the characters of the `String`.
```kotlin
val text = "Hello World"

for (i in 0 until text.length) {
    print("${text[i]} ")              // H e l l o  W o r l d
}

for (index in text.indices) {
    print("${text[index]} ")          // H e l l o  W o r l d
}

for (i in text) {
    print("$i ")                      // H e l l o  W o r l d
}
```

## Type Conversion
- Unlike some other programming languages, there are no implicit widening conversions for numbers in Kotlin. For example, an `Int` variable cannot be initialized with a `Short` or `Byte` variable. A function with a Double parameter can be called only on Double values, but not Float, Int, or other numeric values. The compiler will not perform any automatic type conversion in these cases.

- There are methods built into the datatypes for explicit type conversion. It will not affect the type of the original variables.  

- Every number type supports the following conversions:  
`toByte()`, `toShort()`, `toInt()`, `toLong()`, `toFloat()`, `toDouble()` and `toChar()`.

- Numbers are converted to `Char` and vice versa using the [Unicode Table](https://unicode-table.com/en/).

- When you convert a larger type to smaller type, the value may be truncated.

- All datatypes can be converted to a string using `toString()`.

- Strings can be converted to numbers if they are in the correct format of the type.

- If the string is "true" or "false" (case insensitive), it can be converted to a Boolean using `toBoolean()`. Any value other than "true" will be a false Boolean.

## Type Inference
- In expressions involving variables of different datatypes, the widest type in the expression is inferred by the compiler as the type of the result.  
`Double` > `Float` > `Long` > `Int` > (`Byte`, `Short`)  

- The result of an expression involving `Byte` or `Short` variables is of the type `Int` (or an even larger type), unless explicitly casted.

## Ranges
- Kotlin lets you create ranges of values using `rangeTo()` from the `kotlin.ranges` package, and its operator form `..`.

- `a..b` is a range from `a` to `b` (inclusive), and `in` is a keyword used to check whether a value is within a range.
```kotlin
if (i in 1..5) {  // equivalent of 1 <= i && i <= 5
    print(i)
}
```

- If you need to exclude the right border, you should subtract one from it:
```kotlin
val within = c in a..b - 1
// equivalent of a <= c && c < b
```

- If you need to check that a value is not within a range, use `!in`:
```kotlin
val notWithin = 100 !in 10..99   // true
```

- You can assign a range to a variable and use it later somewhere in the code:
```kotlin
val range = 1..5
print(3 in range)   // true
```

- You can also use ranges of characters and strings (in dictionary order):
```kotlin
println('b' in 'a'..'c') // true
println("hello" in "he".."hi") // true
```

- Integral type ranges can be iterated over using `for` loops:
```kotlin
for (i in 1..5) print(i)   // 12345
```

- To iterate numbers in reverse order, use the `downTo` function instead of `..`:
```kotlin
for (i in 5 downTo 1) print(i)   // 54321
```

- To iterate over numbers with an arbitrary step, use the `step` function:
```kotlin
for (i in 1..10 step 2) {
    print(i)   // 13579
}
```

- To iterate a number range which does not include its end element, use the `until` function:
```kotlin
for (i in 1 until 10) {   // i in [1, 10), 10 is excluded
    print(i)
}
```

## Regex
- A regex instance can be created using the `toRegex()` method of a `String` or by calling the `Regex` constructor:
```kotlin
val string = "ing"
val regex1 = string.toRegex()
val regex2 = Regex("ing")
// regex1 and regex2 represent the same regular expression
```

- `matches()` method of a string returns `true` if the string is **full match** for the regex specified:
```kotlin
val regex = Regex("ing")
val string1 = "ing"
val string2 = "running"

println(string1.matches(regex))   // true
println(string2.matches(regex))   // false
```

- The dot character (`.`) can match any character except a newline. A question mark (`?`) denotes that the preceding character is optional. A double backslash (`\\`) is used to escape special characters. A single backslash (`\`) is used to escape double quotes (`"`).

- To match `\`, the regexp is `\\\\`.

## BigInteger
- The Java Class Library provides a `BigInteger` class for processing very large numbers, limited only by the memory available. It is immutable.
```kotlin
import java.math.BigInteger

val number1 = BigInteger("52955871795228763416553091")   // initialized using constructor
val number2 = BigInteger.valueOf(1000000000)   // initialized from a Long value using the valueOf() method
val number3 = 1234.toBigInteger()   // initialized from an Int vlaue using the toBigInteger() method

// Some constants defined in the BigInteger class:
val zero = BigInteger.ZERO // 0
val one = BigInteger.ONE   // 1
val ten = BigInteger.TEN   // 10
```

- The `divideAndRemainder()` function returns an array consisting of the result of integer division and its remainder.
```kotlin
val (result, remainder) = oneHundredTen.divideAndRemainder(nine) // 12 and 2
```

-  The `abs()` function returns a new BigInteger whose value is the absolute value of the initial BigInteger. The `gcd()` function returns the greatest common divisor of two numbers.
```kotlin
val number = BigInteger("-1")
println(number.abs()) // 1

val twelve = BigInteger.valueOf(12)
val fifteen = BigInteger.valueOf(15)
println(twelve.gcd(fifteen)) // 3
```

## Null Safety
- In Kotlin, the type system distinguishes between references that can hold `null` (nullable references) and those that can not (non-null references).

- To allow nulls, we have to declare a variable as nullable by defining the type of the variable as `<type>?`.
```kotlin
var b: String? = "abc" // can be set null
```

- You can generally handle operations using nullable variables in three ways:
  - You can explicitly check whether the variable is null.
  ```kotlin
  var a: String? = "abc"
  val l = if (a != null) a.length else -1
  ```
  - Use the safe call operator, `?.`.
  ```kotlin
  val b: String? = null
  println(b?.length)      // returns b.length if b is not null, and null otherwise
  // the type of this expression is Int?
  ```
  Safe calls are useful in chains. For example, if Bob (Employee) may be assigned to a Department, that in turn may have another Employee as a department head, then to obtain the name of Bob's department head (if any), we write:
  ```kotlin
  bob?.department?.head?.name     // returns null if any of the properties is null
  ```
  To perform an operation only for non-null values, you can use the safe call operator together with `let`:
  ```kotlin
  val listWithNulls: List<String?> = listOf("Kotlin", null)
  for (item in listWithNulls) {
    item?.let { println(it) } // prints Kotlin and ignores null
  }
  ```
  A safe call can also be placed on the left side of an assignment. If one of the receivers in the safe calls chain is null, the assignment is skipped, and the expression on the right is not evaluated at all:
  ```kotlin
  // If either `person` or `person.department` is null, the function is not called
  person?.department?.head = managersPool.getManager()
  ```
  We can also use the Elvis operator (`?:`) in place of an if-expression. The expression to the right of `?:` is evaluated only if the left-hand side is null.
  ```Kotlin
  val l = a?.length ?: -1
  // Equivalent to:
  // val l: Int = if (a != null) a.length else -1
  
  // Other examples:
  val parent = node.getParent() ?: return null
  val name = node.getName() ?: throw IllegalArgumentException("name expected")
  ```
  - The not-null assertion operator (`!!`) can be used to  convert any value to a non-null type and throw an exception if the value is `null`.
  ```kotlin
  val l = a!!.length
  ```
- Regular casting may result in a `ClassCastException` if the object is not of the target type. You can use safe casts that return null if the attempt was unsuccessful:
```kotlin
var a: String? = "abc"
val n: Int? = a as? Int     // null, as the String can't be casted to an Int type
```

- If you have a collection of elements of a nullable type and want to filter non-null elements, you can use `filterNotNull()`:
```kotlin
val nullableList: List<Int?> = listOf(1, 2, null, 4)
val intList: List<Int> = nullableList.filterNotNull()     // [1, 2, 4]
```

## Conventions
- Four spaces are used for indentation. Do not use tabs.
- Omit semicolons (`;`) wherever possible, as they are optional.
- Put spaces around binary operators, for example, `a + b`.
- Put spaces between control flow keywords (`if`, `when`, `for` and `while`) and the corresponding opening parenthesis.
- If a variable or function name is a single word, it should be in **lowercase**; if the name has multiple words, it should be in **lowerCamelCase**.
- For curly braces, put the opening brace in the end of the line where the construct begins, and the closing brace on a separate line aligned horizontally with the opening construct.
```kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```
- More conventions can be found in the [official documentation](https://kotlinlang.org/docs/reference/coding-conventions.html).

## Standard Input/Output
- `print(message: Any?)` can be used to print the given message to the standard output stream.

- `println(message: Any?)` prints the given message to the standard output stream along with a newline at the end.

- `readLine()` reads a whole line from standard input and returns it as a `String`. The returned string can be casted to the required type using casting function like `toInt()` or `toBoolean()`. You can use two exclamation marks at the end of the function call to force a non-null return value.
```kotlin
val line = readLine()   // can be null
val line2 = readLine()!!    // not null; commonly used
```

- A Java Scanner object can be used to read input:
```kotlin
import java.util.Scanner      // or import java.util.*

val scanner = Scanner(System.`in`)
val line = scanner.nextLine() // read a line
val integer = scanner.nextInt()   // read a number
val word = scanner.next()   // read a string
```

## Functions and Lambda Expressions
- A function definition in Kotlin looks like:
```kotlin
fun functionName(param1: Type1, param2: Type2, ...): ReturnType {
    // body of the function
    return result     // optional
}
// ReturnType is optional if the return type is Unit
```

- If the function returns a single expression, you can avoid the curly braces:
```kotlin
fun sum(a: Int, b: Int) = a + b
fun hello() = print("Hello World")
fun isNegative(num: Int): Boolean = num < 0
// the return types of these functions can be inferred automatically
```

- The `main()` function is the entry point in a Kotlin program.
```kotlin
fun main(args: Array<String>) {
    // body
}
// args is optional
```

- Kotlin supports default arguments in function declarations and named arguments in function calls:
```kotlin
fun horizontalRule(symbol: Char = '-', count: Int = 10, end: Char = '\n') {
    for (i in 1..count) {
        print(symbol)
    }
    print(end)  
}

fun main() {
    horizontalRule()                // ----------
    horizontalRule('_', end = '?')  // __________?
}
```

- The default value for a parameter of a function can also be another named argument, or a function:
```kotlin
fun sum(a: Int, b: Int = a) = a + b
```

- Kotlin uses the call stack (execution stack) of the JVM to store information about functions that are being executed. Each function and its associated data (like function address, argument references and local variables) is stored as a stack frame in the stack. A `StackOverflowError` occurs when the number function invocations exhaust the memory available to the stack.

- Functions are first-class citizens in Kotlin. They can be stored in variables, and passed to or returned by other functions.

- The type of a function is given as:  
`(types of parameters, comma separated) -> return type of the function`
```kotlin
fun sum(a: Int, b: Int): Int = a + b
// Type is:
// (Int, Int) -> Int

fun hello() = print("Hello World")
// Type is:
// () -> Unit
}
```

- Reference to a function can be obtained by prefixing a double colon (`::`) to the function name.
```kotlin
fun sum(a: Int, b: Int): Int = a + b
var newSum = ::sum
// newSum(1, 2) will return 3
```

- The `filter()` method of `String` or collections can accept references to other functions to act as the filtering criteria.

- Anonymous functions in Kotlin are of the form `fun(arguments): ReturnType { body }`

- Lambda expressions in Kotlin are of the form `{ arguments -> body }`.  
If the lambda doesn't have arguments, it's written in the form `{ body }`.  

- When the lambda is the last argument to a function, it can be placed outside the parenthesis. If the function has no other arguments other than the lambda, you can omit the parenthesis altogether. If there is only a single argument for the lambda, `it` can be used to refer to the parameter rather than assigning a name to it.
```kotlin
val someText = "L-o-r-e-m I-p-s-u-m"

print(   someText.filter({ ch -> ch != '-' })    )    // Lorem Ipsum
print(   someText.filter() { ch -> ch != '-' }   )    // Lorem Ipsum
print(   someText.filter { ch -> ch != '-' }     )    // Lorem Ipsum
print(   someText.filter { it != '-' }           )    // Lorem Ipsum
```

- If the lambda has multiple lines of code, its last line is treated as the return value. The `return` keyword is not required in this case.

- If you use `return` in a lambda expression, a non-local return happens to the nearest enclosing function.
```kotlin
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return              // non-local return directly to the caller of foo()
        print(it)
    }
    println("this point is unreachable")
}
```

- To return just from a lambda expression and not the enclosing function, you need to use a fully qualified return statement.
```kotlin
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach lit@{
        if (it == 3) return@lit           // local return to the caller of the lambda, the forEach loop
        print(it)
    }
    print(" done with explicit label")
}

fun bar() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return@forEach       // local return to the caller of the lambda, the forEach loop
        print(it)
    }
    print(" done with implicit label")
}
```

- A `return` statement in an anonymous function will return from the anonymous function itself.
```kotlin
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach(fun(value: Int) {
        if (value == 3) return            // local return to the caller of the anonymous function, the forEach loop
        print(value)
    })
    print(" done with anonymous function")
}
```

- The variables and values visible where the lambda is created are also visible inside the lambda, i.e. lambda *captures* variables. So if a variable is changed inside the lambda, the changes are also reflected outside it.
```kotlin
fun placeArgument(value: Int, f: (Int, Int) -> Int): (Int) -> Int {
    return { i -> f(value, i) }
}

val mul = { a: Int, b: Int -> a * b }
val double = placeArgument(2, mul)
print(double(5))      // 10
```

## Standard Library
- The `Math` (inherited from Java) and `kotlin.math` libraries contains implementation of common mathematical functions and constants.
```kotlin
val sqrt = Math.sqrt(2.0)   // 1.4142...
```

- Random numbers can be generated using the `Random` class in the kotlin.random package.
```kotlin
import kotlin.random.Random

fun main() {
    println( Random.nextInt() )       // generates a random Int number
    println( Random.nextLong() )      // generates a random Long number
    println( Random.nextFloat() )     // generates a random Float number between 0 (inclusive) and 1.0 (exclusive)
    println( Random.nextDouble() )    // generates a random Double number between 0 (inclusive) and 1.0 (exclusive)
    println( Random.nextInt(10) )     // generates a non-negative Int value less than 10
    println( Random.nextInt(1, 10) )  // generates an Int value between 1 (inclusive) and 10 (exclusive)
    // ranges can be specified for all these functions except nextFloat()
}
```

- You can set the seed for the pseudorandom number generator using the `Random()` class constructor.
```kotlin
val generator = Random(42)      // setting the seed 42
for (i in 0..4) {
    print(generator.nextInt(10).toString() + " ")     // "3 0 1 2 1 " will always be the sequence generated for this seed if the same Kotlin runtime and architecture is used
}
```

- A generator initialized using `Random.Default` will have a different seed each time it is used.

## Arrays
- Kotlin supports the following native arrays for primitive types: `IntArray`, `LongArray`, `DoubleArray`, `FloatArray`, `CharArray`, `ShortArray`, `ByteArray` and `BooleanArray`. There is no `StringArray`.

- To create an array of a specified type, pass the elements as parameters to functions like `intArrayOf()`, `charArrayOf()` and `booleanArrayOf()`. To initialize an array with a single value, use a lambda expression along with the type constructor.
```kotlin
val numbers1 = intArrayOf(1, 2, 3, 4, 5)      // Array<Int>: { 1, 2, 3, 4, 5 }
println(numbers.joinToString())               // 1, 2, 3, 4, 5

val numbers2 = IntArray(5)                    // { 0, 0, 0, 0, 0 }
val numbers3 = IntArray(5) {1}                // { 1, 1, 1, 1, 1 }
```

- You cannot change the size of an array, but you can modify its elements.

- The size of an array can be obtained using the `size` property.
```kotlin
val numbers = intArrayOf(1, 2, 3, 4, 5)
println(numbers.size)       // 5
```

- Arrays also have the `first()`, `last()` and `lastIndex()` methods, and it works in the same way it does for `String`.

- Arrays can be compared using the `contentEquals()` method, as `==` only compares the references and not the contents of the object.
```kotlin
val numbers1 = intArrayOf(1, 2, 3, 4)
val numbers2 = intArrayOf(1, 2, 3, 4)

println(numbers1.contentEquals(numbers2))     // true
println(numbers1 == numbers2)                 // false
```

- The `Array<T>` class lets you create an array of any object. The `arrayOf()` and `emptyArray()` functions can be used to create an `Array`.
```kotlin
val array1 = arrayOf("Hello", "World")
val array2 = arrayOf<String>("Hello", "World")      // if you want to enforce the type
val array3 = emptyArray<String>()
```

- The `joinToString()` method returns a `String` containing the elements of the array, separated using commas. The `contentEquals()` method can be used to compare the `Array` with another `Array`.

- The size of an array can be changed (by adding or removing elements) only if it was declared using `var`, and not `val`. However, you can change the elements in both cases.

- Arrays can be nested to create multidimensional arrays. The nested arrays can even be of different types.
```kotlin
val array = arrayOf(
    arrayOf(0),
    arrayOf(1, 2),
    arrayOf(3, 4, 5))
```
- The `contentDeepToString()` method can be used to get the entire content of a multidimensional array as a single `String`.

## Control Flow Statements

- In Kotlin, `if` is also treated as an expression, and not just a statement. It can return the result of some computation, by specifying the result as the last expression in the body. If `if` is used as an expression, it must have an `else` branch.
```kotlin
val max = if (a > b) {
    println("a wins!")
    a
} else {
    println("b wins!")
    b
}
```

- The braces can be omitted if the body has only one statement.
```kotlin
println( if (a == b) "a equal b"
         else if (a > b) "a is greater than b"
         else "a is less than b" )
```

- The `when` construct is the alternative to the **switch-case** statement found in many languages. The `else` keyword specifies the **default** (fallback) argument for the construct. You can use multiple statements in a branch by enclosing them in curly braces. They can also be used as expressions, and the `else` branch is required in such cases.
```kotlin
when (alphabet) {
        "a", "A" -> println("Alpha")
        "b", "B" -> println("Beta")
        "c" -> { println("Gamma")
                 alphabet = "C"
               }
        else -> println("Unknown")
    }
```

- The branch conditions of a `when` construct can also be expressions. It can also be used without an argument; in this case, the branch conditions are evaluated as boolean expressions.
```kotlin
val a = 5
val b = 6
val c = 11    

println(when (c) {
        a + b -> "$c equals $a plus $b"
        a - b -> "$c equals $a minus $b"
        a * b -> "$c equals $a times $b"
        else -> "We do not know how to calculate $c"
        })                                            // "11 equals 5 plus 6"
        
when (c) {
        in 0..10 -> println("c is between 0 and 10 (inclusive).")
        else -> println("c is not between 0 and 10.")
        }
```

- The `repeat` block simply executes its body over and over again for the specified number of times.
```kotlin
import java.util.*

val scanner = Scanner(System.`in`)
val n = 10
val sum = 0

repeat(n) {
        val num = scanner.nextInt()
        sum += num
    }
```

- A `for` loop is used to iterate through ranges, arrays or collections of elements.
```kotlin
for (i in 1..4) {
    println(i)    
}
```

- Kotlin supports the standard `while` and `do..while` loops. The `break` and `continue` statements also work as expected.

- Any expression in Kotlin may be marked with a label. Labels have the form of an identifier followed by the `@` sign. You can use `break`, `continue` and `return` statements using these labels.
```kotlin
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (i == 10 && j == 10) break@loop      // breaks out from both loops
    }
}

fun foo() {                                     // prints "1245"
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return@forEach // local return to the forEach loop
        print(it)
    }
}

fun foobar() {                                  // prints "12"
    run loop@{
        listOf(1, 2, 3, 4, 5).forEach {
            if (it == 3) return@loop // non-local return from the lambda passed to run
            print(it)
        }
    }
}
```

## Object Oriented Programming
- A class is defined using the `class` keyword. If the body of the class is empty, the curly braces can be omitted.
```kotlin
class ClassName {
  // class properties and methods
}

val object = ClassName()
```

- The default values of the properties can be specified in the class definition itself. The properties can be accessed by using the `object.property` format.
```kotlin
class Solid {
  var color = "red"
  var count = 10
  var shape = "sphere"
}

val object = Solid()
println(object.shape)     // sphere
```

- A class in Kotlin has one primary constructor, and zero or more secondary constructors. The primary constructor is a part of the class header, and does not have to be defined separately. Optionally, the primary constructor can also take parameters.
```kotlin
class Person(name: String) { /*...*/ }
// Same as:
// class Person constructor(name: String) { /*...*/ }
```

- Any initialization code for the primary constructor has to be put in one or more `init` blocks. These  `init` blocks are executed in the order in which they appear.
```kotlin
class InitOrderDemo(name: String) {
    val firstProperty = "First property: $name".also(::println)

    init {
        println("First initializer block that prints ${name}")
    }

    val secondProperty = "Second property: ${name.length}".also(::println)

    init {
        println("Second initializer block that prints ${name.length}")
    }
}
```

- The parameters passed to the primary constructor can be used as class properties by adding `val` or `var` keywords to the parameters list.
```kotlin
class Name(val firstName: String, val lastName: String)     // example of a data class, used to store structured data
```

- The primary constructor also takes default values in the arguments list.
```kotlin
class Solid(val shape = "sphere", val color = "red") { /*...*/ }
val object = Solid(color = "blue")
```

- Class methods are called *member functions* in Kotlin. They are defined inside the class definition block. The `this` keyword can be used to refer to the current instance.
```kotlin
class Color(var color = "red") {
  fun printColor() {
    print(this.color)     // you can omit the 'this' keyword if the property name is unique
  }
}

val obj = Color("green")
obj.printColor()      // prints "green"
```

- When you access a property, a getter function is invoked implicitly. Similarly, a setter function is invoked when the value of a property is changed. Each property has their own getter and setter functions. They are automatically defined by the compiler, but you can define custom functions if required. Inside the getter and setter function, the keyword `field` has to be used in place of the actual property name to avoid an infinite recursive call of getter/setter functions.
```kotlin
class Person {
    var name: String = "John"
        get() = field
        set(value) {
          print("Changed name from $field to $value.")
          field = value
        }
}

val guy = Person()
guy.name = "Ron"      // prints "Changed name from John to Ron"
```

- If a class is to be inherited (extended), it has to be declared with the `open` keyword. We can pass parameters to the constructor of the parent class, if required.
```kotlin
open class Person(var name: String, var age: Int = 25)

class Employee(name: String, dept: String) : Person(name) {
    var department = dept
}
```

- Any function that accepts a parent class also accepts a child class as its parameter.

- To override a function from the parent class in a child class, the `open` modifier has to be used in the function definition in the parent class, and the `override` modifier has to be used in the function definition in the child class. An overridden method is automatically `open` to all subclasses (if any). The `final` modifier can be used to close such implicitly `open` functions. Overriding properties works in a similar way.
```kotlin
open class Shape {
    open val vertices: Int = 0
}

class Rectangle : Shape() {
    final override val vertices = 4
}
```

- Code in a derived class can call its superclass functions and property accessors implementations using the `super` keyword.
```kotlin
open class Rectangle {
    open fun draw() { println("Drawing a rectangle") }
}

class FilledRectangle : Rectangle() {
    override fun draw() {
        super.draw()
        println("Filling the rectangle")
    }
}
```

- Secondary constructors are declared as `constructor()`. A class can have more than one secondary constructors, provided they all have unique function signatures.
```kotlin
class Person {
    var children: MutableList<Person> = mutableListOf()
    constructor(parent: Person) {
        parent.children.add(this)
    }
}
```

- If the class has a primary constructor, each secondary constructor needs to delegate to the primary constructor, either directly or indirectly through another secondary constructor(s). The `this` keyword can be used to delegate to another constructor of the same class. Delegation to the primary constructor happens as the first statement of a secondary constructor, so the code in `init` blocks and property initializers is executed before the secondary constructor body.
```kotlin
class Person(val name: String) {
    var children: MutableList<Person> = mutableListOf()
    init {                                        
        println("Initializing..")     // always runs before the secondary constructor
    }
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
```

- A singleton class is a special class with a only single instance globally. Singletons are implemented in Kotlin by using *object declarations*. The singleton is declared like a regular class declaration, but with the keyword `object` in place of `class`. Such classes doesn't need instantiation, and can be accessed directly using the class name.
```kotlin
object President {
  val name = "Abraham Lincoln"
  fun printMsg() {
    println("$name was a former US President.")
  }
}

President.printMsg()
```

- Classes can be nested. As a singleton is also a special type of class, objects declarations can also be nested in class or object declarations.

- Extensions are used to extend a class with new functionality without having to inherit from the class. You can declare methods and properties for a class without modifying the actual class declaration. To declare an extension, we prefix its name with the receiver type (the class being extended). Extensions do not actually modify the classes being extended, and are resolved statically.  
```kotlin
fun MutableList<Int>.swap(index1: Int, index2: Int) {
    val tmp = this[index1] // 'this' corresponds to the list
    this[index1] = this[index2]
    this[index2] = tmp
}

val list = mutableListOf(1, 2, 3)
list.swap(0, 2) // [3, 2, 1]
```

- If an extension for a class is defined with the same name (and signature) as a member, the member always wins. However, functions can be overloaded by using a different signature.
```kotlin
class Example {
    fun printFunctionType() { println("Class method") }
}

fun Example.printFunctionType() = println("Extension function")

Example().printFunctionType()     // Class method
```
- Extensions can also be defined with a nullable receiver type.
```kotlin
fun Any?.toString(): String {
    if (this == null) return "null"
    // after the null check, 'this' is autocast to a non-null type, so the toString() below
    // resolves to the member function of the Any class
    return toString()
}
```

- Extension properties can have getters and setters, but cannot have initializers.
```kotlin
  val <T> List<T>.lastIndex: Int
    get() = size - 1
```

- The `toString()` method of classes are invoked implicitly by when you try to print them. You can override the `toString()` method of a class to change the default behavior (which is a string of the form <class_name>@<pointer>). This modified function is inherited by the child classes, if any.   

```kotlin
open class Toy(val type: String = "ball", val color: String = "blue") {
  override fun toString(): String {
    return "$color $type"
  }
}

class ToyOwner(val name: String, type: String = "ball", color: String = "blue") : Toy(type, color) {
  override fun toString(): String {
    return "${name}'s ${super.toString()}"
  }
}

val blueBall = ToyOwner("John")
print(blueBall)   // John's blue ball
```

- An object declaration inside a class can be marked with the `companion` keyword. Members of the companion object can be called by using simply the class name as the qualifier. The name of the companion object can be omitted, in which case the name `Companion` will be automatically.
```kotlin
class SampleClass {
    companion object {
        fun create(): SampleClass = SampleClass()
    }
}

val instance1 = SampleClass.create()
val instance2 = SampleClass.Companion.create()
// both function calls refer to the same function, and creates different instances of the class
```

- Properties from the outer class will shadow the properties of the companion if they have the same name. Only one companion object can be created for a class. A companion class cannot be nested inside another companion class or object declaration.

- The `enum` keyword is used to create enumeration classes.
```kotlin
enum class Rainbow {
    RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
}
```

- Enum classes can be used to store multiple parameters per member, and even add member functions.
```kotlin
enum class Rainbow(val color: String, val rgb: String) {
    RED("Red", "#FF0000"),
    ORANGE("Orange", "#FF7F00"),
    YELLOW("Yellow", "#FFFF00"),
    GREEN("Green", "#00FF00"),
    BLUE("Blue", "#0000FF"),
    INDIGO("Indigo", "#4B0082"),
    VIOLET("Violet", "#8B00FF");

    fun printFullInfo() {
        println("Color: $color --- RGB: $rgb")
    }
}

val rgb = Rainbow.RED.rgb
```

- Enum classes also contain some methods and properties implicitly defined by Kotlin.
```kotlin
val color: Rainbow = Rainbow.BLUE
println(color.name)     // returns the enum instance's name, "BLUE"
println(color.ordinal)      // returns the postion (index) of the instance in the class declaration, 4
fun isRainbowColor(color: String) : Boolean {
    for (enum in Rainbow.values()) {      // returrns a list of instances in the enum class
        if (color.toUpperCase() == enum.name) return true
    }
    return false
}

println(isRainbowColor("Pink"))     // false
```

- Data classes declared with the modifier `data` is used to store data in an organized manner. These classes automatically support methods like `equals()`, `hashCode()`, `toString()` and `copy()`. However, such built-in methods only consider the properties listed in the constructor, and ignores any properties found in the body of the class. All the methods except `copy()` can be overridden if required.
```kotlin
data class Toy(var type = "Ball", var color = "Blue")

val blueBall = Toy()
val redBall = blueBall.copy(color = "Red")
```

- Data classes can be unpacked, or *destructured*. A destructuring declaration uses a `componentN()` operator that returns the n-th element in the data class.
```kotlin
data class Toy(var type = "Ball", var color = "Blue")

val blueBall = Toy()
val (toyType, toyColor) = blueBall
// Same as:
// val toyType = blueBall.component1()
// val toyColor = blueBall.component2()

println(toyType)      // Ball
println(toyColor)     // Blue
```

- Regular classes can also be destructured if you explicitly define `componentN()` operators.
```kotlin
class Toy(var type = "Ball", var color = "Blue") {
    operator fun component1(): String = type
    operator fun component2(): String = color
}
```

- Destructuring also works with arrays. If there are less variables than the size of the array, it will skip the remaining elements of the array. If there are more variables, the expression will result in an error. If you don't need a variable in the destructuring declaration, you can place an underscore instead of its name.

## Collections

- The following properties and methods are supported by all the standard collections in Kotlin:
  - `size`
  - `contains(element)` → checks if `element` is in the collection
  - `containsAll(col)` → checks whether all the elements in the collection `col` is in the current collection
  - `isEmpty()`
  - `joinToString()` returns a string consisting of the elements of the collection.
  - `indexOf(element)` returns the index of the first occurrence of `element` in the collection, and `-1` if `element` is not present in the collection.

- Mutable collections have some more common methods:
  - `clear()` removes all the elements in the collection
  - `remove(element)` removes the first occurrence of `element`
  - `removeAll(col)` removes all elements of the collection `col` from the current collection


- `List<T>` stores elements in a specified order and provides indexed access to them. A `List` can contain duplicate elements, even `null`.
```kotlin
val numbers = listOf("one", "two", "three", "four")
val empty = emptyList<String>()     // to initialize an empty list

println("Number of elements: ${numbers.size}")
println("Third element: ${numbers.get(2)}")
println("Fourth element: ${numbers[3]}")
println("Index of element \"two\" ${numbers.indexOf("two")}")
```

- A `MutableList<T>` is a mutable `List`, i.e supports adding or removing elements. A `List` can be converted to a `MutableList` using the `toMutableList()` method of a `List`.
```kotlin
val numbers = mutableListOf(1, 2, 3, 4)
numbers.add(5)    // 1, 2, 3, 4, 5
numbers.removeAt(1)   // 1, 3, 4, 5
numbers[0] = 0    // 0, 3, 4, 5
numbers.shuffle()   // list is shuffled in a random order
println(numbers)
```

- A `Set<T>` is used an unordered collection of unique elements. Even `null` can occur only once in a `Set`. Two sets are equal if they have the same size, and for each element of a set there is an equal element in the other set. The default implementation of a `Set` is a `LinkedHashSet`, which remembers the order of insertion of elements. So it also supports methods like `first()` and `last()`.
```kotlin
val numbers = setOf(1, 2, 3, 4)
println("Number of elements: ${numbers.size}")

if (numbers.contains(1)) println("1 is in the set")

val numbersBackwards = setOf(4, 3, 2, 1)
println("${numbers == numbersBackwards}")
```

- A `MutableSet` allows you to add or remove values.
```kotlin
val empty = mutableSetOf<Int>()     // declare an empty mutable set for Int elements
```

- `Map<K, V>` stores key-value (`K`-`V`) pairs. The keys in a `Map` should be unique. Two maps containing the equal pairs are equal regardless of the order in which the pairs are found in the maps.  
```kotlin
val numbersMap = mapOf<String, Int>("key1" to 1, "key2" to 2, "key3" to 3, "key4" to 1)     // the type specification can be omitted as it is automatically inferred
println("All keys: ${numbersMap.keys}")
println("All values: ${numbersMap.values}")
if ("key2" in numbersMap) println("Value of \"key2\": ${numbersMap["key2"]}")    
if (1 in numbersMap.values) println("The value 1 is in the map")
if (numbersMap.containsValue(1)) println("The value 1 is in the map") // same as previous
```

- A `MutableMap` allows you to add new key-value pairs and update existing ones.
```kotlin
val numbersMap = mutableMapOf("one" to 1, "two" to 2)
numbersMap.put("three", 3)
numbersMap["one"] = 11
println(numbersMap)     // {one=11, two=2, three=3}
numbersMap.remove("four")     // nothing happens
numbersMap.remove("three", 4)     // removes the pair only if the value associated with "three" is 4
println(numbersMap.containsValue(3))      // true
println(numbersMap.containsKey(3))      // false
```

- Collections support iteration. When iterating over maps, a pair of values is returned in each iteration, which can be destructured into two separate variables.

- A description of all the properties and methods supported by [lists](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-list/), [mutable lists](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-list/index.html), [sets](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-set/index.html), [mutable sets](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-set/index.html), [maps](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-map/index.html) and [mutable maps](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/-mutable-map/index.html) can be found in the official documentation.

## Exceptions

- You can throw exceptions using the `throw` keyword.
```kotlin
throw ArithmeticException
```

- The `Exception` class is used to create custom exceptions.
```kotlin
val customException = Exception("A custom error message.")
throw customException

// Same as:
// throw Exception("A custom error message.")
```

- Kotlin supports try-catch blocks. They can have multiple handlers (`catch` blocks) if required. The `message` property stores the error message related to an Exception. When an exception occurs in the `try` block, the suitable handler is determined by trying to match the exception types from the first `catch` block to the last. So specialized handlers like `IOException` should come before general handlers like `Exception` (which can catch every type of exception). After the exception is handled, code execution resumes from the line immediately after the try-catch block.
```kotlin
try {
    print(10 / 0)
}
catch (e: IOException) {
    // handles IOException and its subtypes
}
catch (e: Exception) {
    // handles all subtypes of Exception
    println(e.message)      // "/ by zero"
}
```

- A `finally` block is executed irrespective of whether an exception was encounter in a `try` or `catch` block.
```kotlin
try {
    // code that may throw an exception
}
catch (e: Exception) {
    // exception handler
}
finally {
    // always executed
}
```

- A try-catch block can also be used as an expression in Kotlin.
```kotlin
val number: Int = try { "abc".toInt() } catch (e: NumberFormatException) { 0 }
println(number)     // 0
```

## Working With Files
- Files are handled using the `File` class from the `java.io` package. A `File` object contains a pointer to the specified file. When a method (except write methods) is called and the file does not exist, and a `NoSuchFileException` is thrown.

- The `readText()` method returns the entire contents of the file as a `String`.
```kotlin
import java.io.File

val file = File("file.txt")       // file is not opened, only a reference to the file is returned
val content = file.readText()     // file is opened and closed automatically by the method
print(content)                    // entire content of the text file is displayed
```

- The `readLines()` method returns a `List` with each line of the file as an element of the list.

- The `readBytes()` method returns the entire content of the file as a byte array.

- The `forEachLine()` method executes an action for each line in the file. This is recommended for very large files, as directly trying to read the entire file in one go may exhaust the system memory.
```kotlin
val fileName = "file.txt"
File(fileName).forEachLine { println(it) }
```

- The `writeText()` method is used to write a `String` to file. If the file does not exists, it is created automatically. If the file already exists, its contents are overwritten.

- The `appendText()` method is used to append a `String` to an existing file.

- The `writeBytes()` and `appendBytes()` methods are used to write a `ByteArray` to file.

- The `length()` method returns the number of characters in the file.

- The `exists()` method of the `File` class can be used to check whether a file exists.

- A list of all methods supported by the `File` class can be found in the [official documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/java.io.-file/).

## References
[Basic Syntax](https://kotlinlang.org/docs/reference/basic-syntax.html) - Kotlin Official Documentation  
[Kotlin Programming Language Reference](https://kotlinlang.org/docs/reference/) - Kotlin Official Documentation  
NOTE: A lot of code samples have been taken directly from the official documentations.

## Learn Kotlin
- [JetBrains Academy](https://hyperskill.org/) has a Kotlin track that helps you learn by working on a project in Kotlin. The course is current in a public beta phase, and available for free at the time of writing.
- [Kotlin Koans](https://play.kotlinlang.org/koans/overview) is great way for Java developers to learn Kotlin, by working on a curated series of exercises in Kotlin.
