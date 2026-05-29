# Learning Go - An Idiomatic Approach To Real World Go Programming

## Chapter 1 - Setting Your Go Environment
The first thing you need to do is create a directory to hold your program. Call it Proj1.  On the command line, enter the new directory. Inside the directory, run the go mod init command to mark this directory as a Go module.

```bash 
mkdir Proj1
cd Proj1
go mod init hello_world
```

The go.mod file declares the name of the module, the minimum supported version of Go for the module, and any other modules that your module depends on. You can think of it as being similar to the requirements.txt file used by Python or the Gemfile used by Ruby. You shouldn’t edit the go.mod file directly. Instead, use the go get and go mod tidy  commands to manage changes to the file. The main package in a Go module contains the code that starts a Go program. All Go programs start from the main function in the main package. You declare this function with func main() and a left brace. Like Java, JavaScript, and C, Go uses braces to mark the start and end of code blocks.

```bash
go build
```

This creates an executable called as the name of the module (here is hello_world. remember `go mod init hello_world`). then run it like this:
```bash
./hello_world
```

The Go development tools include a command, go fmt, which automatically fixes the whitespace in your code to match the standard format. Using ./... tells a Go tool to apply the command to all the files in the current directory and all subdirectories.
```bash 
go fmt ./...
```


In one class of bugs, the code is syntactically valid but quite likely incorrect. The go tool includes a command called go vet to detect these kinds of errors. One of the things that go vet detects is whether a value exists for every placeholder in a formatting template.
```bash
go vet ./... 
```

## Chapter 2 - Predeclared Types and Declerations
Let's start by looking at the types that are built into Go and how to declare variables of those types. 
### Literals
literals in Go are untyped.<br>
An **integer** literal is a sequence of numbers. Integer literals are base 10 by default, but different prefixes are used to indicate other bases: 0b for binary (base 2), 0o for octal (base 8), or 0x for hexadecimal (base 16). You can use either upper- or lowercase letters for the prefix. 
To make it easier to read longer integer literals, Go allows you to put underscores in the middle of your literal. This allows you to, for example, group by thousands in base 10 (1_234). <br>

A **floating-point** literal has a decimal point to indicate the fractional portion of the value. They can also have an exponent specified with the letter e and a positive or negative number (such as 6.03e23). As integer literals, you can use underscores to format your floating-point literals. <br>

A **rune** literal represents a character and is surrounded by single quotes. Unlike many other languages, in Go single quotes and double quotes are not interchangeable. Rune literals can be written as single Unicode characters ('a'), 8-bit octal numbers ('\141'), 8-bit hexadecimal numbers ('\x61'), 16-bit hexadecimal numbers ('\u0061'), or 32-bit Unicode numbers ('\U00000061'). There are also several backslash-escaped rune literals, with the most useful ones being newline ('\n'), tab ('\t'), single quote ('\\\''), and backslash ('\\\\').<br>

There are two ways to indicate **string** literals. Most of the time, you should use double quotes to create an interpreted string literal (e.g., type "Greetings and Salutations"). These contain zero or more rune literals. They are called “interpreted” because they interpret rune literals (both numeric and backslash escaped) into single characters. The only characters that cannot appear in an interpreted string literal are **unescaped backslashes, unescaped newlines, and unescaped double quotes.**

### Booleans
The bool type represents Boolean variables. Variables of bool type can have one of two values: true or false. The zero value for a bool is false.

### Numeric Types
Go has a large number of numeric types: 12 types (and a few special names) that are grouped into three categories.
#### Integer types
Go provides both signed and unsigned integers in a variety of sizes, from one to eight bytes. the zero value for all of the integer types is 0. <br> A **byte** is an alias for uint8; The second special name is **int**. On a 32-bit CPU, int is a 32-bit signed integer like an int32. On most 64-bit CPUs, int is a 64-bit signed integer, just like an int64. Because int isn’t consistent from platform to platform, it is a compile-time error to assign, compare, or perform mathematical operations between an int and an int32 or int64 without a type conversion. The third special name is **uint**. It follows the same rules as int, only it is unsigned (the values are always 0 or positive).

| Type | Value Range |
|---|---|
| int8   | –128 to 127 |
| int16  | –32768 to 32767 |
| int32  | –2147483648 to 2147483647 |
| int64  | –9223372036854775808 to 9223372036854775807 |
| uint8  | 0 to 255 |
| uint16 | 0 to 65535 |
| uint32 | 0 to 4294967295 |
| uint64 | 0 to 18446744073709551615 |


#### Integer operators
Go integers support the usual arithmetic operators: **+, -, *, /, with %** for modulus. The result of an integer division is an **integer**; if you want to get a floating-point result, you need to use a type conversion to make your integers into floating-point numbers. You can combine any of the arithmetic operators with = to modify a variable: +=, -=, *=, /=, and %=.
You can compare integers with ==, !=, >, >=, <, and <=.
Go also has bit-manipulation operators for integers. You can bit shift left and right with << and >>, or do bit masks with & (bitwise AND), | (bitwise OR), ^ (bitwise XOR), and &^ (bitwise AND NOT). As with the arithmetic operators, you can also combine all the bitwise operators with = to modify a variable: &=, |=, ^=, &^=, <<=, and >>=.

#### Floating-point types
Go has two floating-point types. **float32** and **float64**. Like the integer types, the zero value for the floating-point types is 0. unless you have to be compatible with an existing format, use float64. Floating-point literals have a default type of float64, so always using float64 is the simplest option.
Just like other languages, Go floating-point numbers have a huge range, but they cannot store every value in that range; **they store the nearest approximation.** Because floats aren’t exact, they can be used only in situations where inexact values are acceptable or the rules of floating point are well understood.
You can use all the standard mathematical and comparison operators with floats, **except %.**
While Go lets you use == and != to compare floats, **don’t do it**. Because of the inexact nature of floats, two floating-point values might not be equal when you think they should be. Instead, define a maximum allowed variance and see if the difference between two floats is less than that (the epsilon technique). 

#### Complex numbers
Go defines two complex number types. **complex64** uses float32 values to represent the real and imaginary part, and **complex128** uses float64 values. Both are declared with the complex built-in function. All the standard floating-point arithmetic operators work on complex numbers. Just as with floats, you can use == or != to compare them, but they have the same precision limitations, so it’s best to use the epsilon technique. You can extract the real and imaginary portions of a complex number with the **real** and **imag** built-in functions, respectively. The math/cmplx package has additional functions for manipulating complex128 values.
```bash
var complexNum = complex(20.3, 10.2)
```

### Strings and Runes
Like integers and floats, strings are compared for equality using ==, difference with !=, or ordering with >, >=, <, or <=. They are concatenated by using the + operator. Strings in Go are **immutable**; you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it (for example you can't change the variable s value from hello to Hello by `s[0] = 'H'`). 
Go also has a type that represents a single code point. The **rune** type is an alias for the int32 type, just as byte is an alias for uint8. If you are referring to a character, use the rune type, not the int32 type. They might be the same to the compiler, but you want to use the type that clarifies the intent of your code.

### Explicit Type Conversions
Go doesn’t allow automatic type promotion between variables. You must use **a type conversion** when variable types do not match. Even different-sized integers and floats must be converted to the same type to interact. Also , **no other type can be converted to a bool, implicitly or explicitly.**
```bash
var x int = 10
var y float64 = 30.2
var sum1 float64 = float64(x) + y # sum1 is now 40.2 
```

### var Versus :=
The most verbose way to declare a variable in Go uses the var keyword, an explicit type, and an assignment. if you want to declare a variable and **assign it the zero value**, you can keep the type and drop the = on the righthand side.
```bash 
var x int8 = 10
var x, y int32
var (
    x int
    y = 20
    z int = 30
    d, e = 40, "hello"
    f, g string
)
```
When you are within a function, you can use the **:=** operator to replace a var declaration that uses type inference. The := operator can do one trick that you cannot do with var: it allows you to assign values to existing variables too. As long as at least one new variable is on the lefthand side of the :=, any of the other variables can already exist.
Using := has one limitation. If you are declaring a variable at the package level, you must use var because := is not legal outside of functions.
While it is legal to use a type conversion to specify the type of the value and use := to write `x := byte(20)`, it is idiomatic to write `var x byte = 20`.    

**Package-level variables** whose values change are a bad idea. When you have a variable outside of a function, it can be difficult to track the changes made to it, which makes it hard to understand how data is flowing through your program.

### Using const
Many languages have a way to declare a value as immutable. In Go, this is done with the const keyword. Be aware that const in Go is very limited. Constants in Go are a way to give names to literals.

### Unused Variables
Another Go requirement is that every declared local variable **must be read**. It is a compile-time error to declare a local variable and to not read its value. As long as a variable is read once, the compiler won’t complain, even if there are writes to the variable that are never read.

### Naming 
**idiomatic Go uses camel case (names like indexCounter or numberTries) when an identifier name consists of multiple words.** Also, don't use unknown names or names start with numbers or underscore for regular variables you declare. An underscore by itself (_) is a special identifier name in Go (will discuss in future). 
The smaller the scope for a variable, the shorter the name that’s used for it. For example, it is common in Go to see single-letter variable names used with for loops. 
These short names serve two purposes. The first is that they eliminate repetitive typing, keeping your code shorter. Second, they serve as a check on how complicated your code is. If you find it hard to keep track of your short-named variables, your block of code is likely doing too much.


## Chapter 3 - Composite Types
### Arrays
arrays are rarely used directly in Go. All elements in the array must be of the type that’s specified. because they come with an unusual limitation: Go considers the size of the array to be part of the type of the array. This makes an array that’s declared to be [3]int a different type from an array that’s declared to be [4]int.
declaration styles:
In the first, you specify the size of the array and the type of the elements in the array. If you have initial values for the array, you can also specify them with an array literal:
```bash
var x [3]int
var x = [3]int{10, 20, 30}
```
When using an array literal to initialize an array, you can replace the number that specifies the number of elements in the array with ...:
```bash
var x = [...]int{10, 20, 30}
```
Go has only one-dimensional arrays, but you can simulate multidimensional arrays. This declares x to be an array of length 2 whose type is an array of ints of length 3.
```bash
var x [2][3]int
```
An out-of-bounds read or write with a variable index compiles but fails at runtime with a panic.

### Slices
Most of the time, when you want a data structure that holds a sequence of values, a slice is what you should use. What makes slices so useful is that you can grow slices as needed. This is because the length of a slice is not part of its type.
```bash
var x []int
var x = []int{10, 20, 30}
```
When no value is assigned, x is assigned the zero value for a slice, which is something you haven’t seen before: **nil**. In Go, nil is an identifier that represents the lack of a value for some types. Like the untyped numeric constants you saw in the previous chapter, nil has no type, so it can be assigned or compared against values of different types. A nil slice contains nothing.
You can simulate multidimensional slices and make a slice of slices:
```bash
var x [][]int
```
A slice is the first type you’ve seen that isn’t comparable. The only thing you can compare a slice with using == is nil. The **slices.Equal** function takes in two slices and returns true if the slices are the same length, and all of the elements are equal.

#### len
Go provides several built-in functions to work with slices. You’ve already seen the built-in len function when looking at arrays. It works for slices too. Passing a nil slice to len returns 0.
#### append
The built-in append function is used to grow slices. One slice is appended onto another by using the ... operator to expand the source slice into individual values
```bash
var x []int
x = append(x, 10)
x = append(x, 5, 6, 7)
y := []int{20, 30, 40}
x = append(x, y...)
```

#### capacity
Every slice also has a **capacity**, which is the number of consecutive memory locations reserved. This can be larger than the length. Each time you append to a slice, one or more values is added to the end of the slice. Each value added increases the length by one. When the length reaches the capacity, there’s no more room to put values. If you try to add additional values when the length equals the capacity, the append function uses the Go runtime to allocate a new backing array for the slice with a larger capacity (the capacity doubles). The values in the original backing array are copied to the new one, the new values are added to the end of the new backing array, and the slice is updated to refer to the new backing array. Finally, the updated slice is returned.
```bash
var x []int
fmt.Println(x, len(x), cap(x))
```

#### make
the built-in make function allows you to specify the type, length, and, optionally, the capacity. Let’s take a look (In the last case, you have a non-nil slice with a length of 0 but a capacity of 10.):
```bash
x := make([]int, 5)
x := make([]int, 5, 10)
x := make([]int, 0, 10)
```

One common beginner mistake is to try to populate those initial elements using append:
```bash 
x := make([]int, 5)
x = append(x, 10)
```
The 10 is placed at the end of the slice, after the zero values in elements 0–4 because append always increases the length of a slice. The value of x is now [0 0 0 0 0 10].

#### emptying an slice
Go 1.21 added a clear function that takes in a slice and sets all of the slice’s elements to their zero value.

#### Slicing Slices
A slice expression creates a slice from a slice. It’s written inside brackets and consists of a starting offset and an ending offset, separated by a colon (:). The starting offset is the first position in the slice that is included in the new slice, and the ending offset is one past the last position to include. If you leave off the starting offset, 0 is assumed. Likewise, if you leave off the ending offset, the end of the slice is substituted.

```bash
x := []string{"a", "b", "c", "d"}
y := x[:2]
z := x[1:]
d := x[1:3]
e := x[:]
```
When you take a slice from a slice, you are not making a copy of the data. Instead, you now have two variables that are sharing memory. **This means that changes to an element in a slice affect all slices that share that element.**

#### copy
If you need to create a slice that’s independent of the original, use the built-in `copy` function.

### Maps
