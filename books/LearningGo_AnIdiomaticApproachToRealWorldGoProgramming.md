# Learning Go - An Idiomatic Approach To Real World Go Programming
- [Learning Go - An Idiomatic Approach To Real World Go Programming](#learning-go---an-idiomatic-approach-to-real-world-go-programming)
  - [Chapter 1 - Setting Your Go Environment](#chapter-1---setting-your-go-environment)
  - [Chapter 2 - Predeclared Types and Declerations](#chapter-2---predeclared-types-and-declerations)
    - [Literals](#literals)
    - [Booleans](#booleans)
    - [Numeric Types](#numeric-types)
      - [Integer types](#integer-types)
      - [Integer operators](#integer-operators)
      - [Floating-point types](#floating-point-types)
      - [Complex numbers](#complex-numbers)
    - [Strings and Runes](#strings-and-runes)
    - [Explicit Type Conversions](#explicit-type-conversions)
    - [var Versus :=](#var-versus-)
    - [Using const](#using-const)
    - [Unused Variables](#unused-variables)
    - [Naming](#naming)
  - [Chapter 3 - Composite Types](#chapter-3---composite-types)
    - [Arrays](#arrays)
    - [Slices](#slices)
      - [len](#len)
      - [append](#append)
      - [capacity](#capacity)
      - [make](#make)
      - [Emptying an slice](#emptying-an-slice)
      - [Slicing Slices](#slicing-slices)
      - [copy](#copy)
    - [Maps](#maps)
      - [When should you use a map, and when should you use a slice?](#when-should-you-use-a-map-and-when-should-you-use-a-slice)
      - [The comma ok Idiom](#the-comma-ok-idiom)
      - [Deleting from Maps](#deleting-from-maps)
      - [Emptying a Map](#emptying-a-map)
      - [Using Maps as Sets](#using-maps-as-sets)
    - [Structs](#structs)
      - [Anonymous Structs](#anonymous-structs)
      - [Comparing and Converting Structs](#comparing-and-converting-structs)
  - [Chapter 4 - Blocks, Shadows, and Control Structures](#chapter-4---blocks-shadows-and-control-structures)
    - [Blocks](#blocks)
    - [Shadowing Variables](#shadowing-variables)
    - [if](#if)
    - [for, Four Ways](#for-four-ways)
      - [The Complete for Statement](#the-complete-for-statement)
      - [The Condition-Only for Statement](#the-condition-only-for-statement)
      - [The Infinite for Statement](#the-infinite-for-statement)
      - [break and continue](#break-and-continue)
      - [The for-range Statement](#the-for-range-statement)



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
<br> <br> <br>

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
Go integers support the usual arithmetic operators: **+, -, *, /, with %** for modulus. The result of an integer division is an **integer**; if you want to get a floating-point result, you need to use a type conversion to make your integers into floating-point numbers. You can combine any of the arithmetic operators with = to modify a variable: +=, -=, *=, /=, and %=. <br>
You can compare integers with ==, !=, >, >=, <, and <=. <br>
Go also has bit-manipulation operators for integers. You can bit shift left and right with << and >>, or do bit masks with & (bitwise AND), | (bitwise OR), ^ (bitwise XOR), and &^ (bitwise AND NOT). As with the arithmetic operators, you can also combine all the bitwise operators with = to modify a variable: &=, |=, ^=, &^=, <<=, and >>=.

#### Floating-point types
Go has two floating-point types. **float32** and **float64**. Like the integer types, the zero value for the floating-point types is 0. unless you have to be compatible with an existing format, use float64. Floating-point literals have a default type of float64, so always using float64 is the simplest option. <br>
Just like other languages, Go floating-point numbers have a huge range, but they cannot store every value in that range; **they store the nearest approximation.** Because floats aren’t exact, they can be used only in situations where inexact values are acceptable or the rules of floating point are well understood. <br>
You can use all the standard mathematical and comparison operators with floats, **except %.** <br>
While Go lets you use == and != to compare floats, **don’t do it**. Because of the inexact nature of floats, two floating-point values might not be equal when you think they should be. Instead, define a maximum allowed variance and see if the difference between two floats is less than that (the epsilon technique). 

#### Complex numbers
Go defines two complex number types. **complex64** uses float32 values to represent the real and imaginary part, and **complex128** uses float64 values. Both are declared with the complex built-in function. All the standard floating-point arithmetic operators work on complex numbers. Just as with floats, you can use == or != to compare them, but they have the same precision limitations, so it’s best to use the epsilon technique. You can extract the real and imaginary portions of a complex number with the **real** and **imag** built-in functions, respectively. The math/cmplx package has additional functions for manipulating complex128 values.
```Go
var complexNum = complex(20.3, 10.2)
```

### Strings and Runes
Like integers and floats, strings are compared for equality using ==, difference with !=, or ordering with >, >=, <, or <=. They are concatenated by using the + operator. Strings in Go are **immutable**; you can reassign the value of a string variable, but you cannot change the value of the string that is assigned to it (for example you can't change the variable s value from hello to Hello by `s[0] = 'H'`). 
Go also has a type that represents a single code point. The **rune** type is an alias for the int32 type, just as byte is an alias for uint8. If you are referring to a character, use the rune type, not the int32 type. They might be the same to the compiler, but you want to use the type that clarifies the intent of your code.

### Explicit Type Conversions
Go doesn’t allow automatic type promotion between variables. You must use **a type conversion** when variable types do not match. Even different-sized integers and floats must be converted to the same type to interact. Also , **no other type can be converted to a bool, implicitly or explicitly.**
```Go
var x int = 10
var y float64 = 30.2
var sum1 float64 = float64(x) + y # sum1 is now 40.2 
```

### var Versus :=
The most verbose way to declare a variable in Go uses the var keyword, an explicit type, and an assignment. if you want to declare a variable and **assign it the zero value**, you can keep the type and drop the = on the righthand side.
```Go 
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
When you are within a function, you can use the **:=** operator to replace a var declaration that uses type inference. The := operator can do one trick that you cannot do with var: it allows you to assign values to existing variables too. As long as at least one new variable is on the lefthand side of the :=, any of the other variables can already exist. <br>
Using := has one limitation. If you are declaring a variable at the package level, you must use var because := is not legal outside of functions.
While it is legal to use a type conversion to specify the type of the value and use := to write `x := byte(20)`, it is idiomatic to write `var x byte = 20`.    <br>

**Package-level variables** whose values change are a bad idea. When you have a variable outside of a function, it can be difficult to track the changes made to it, which makes it hard to understand how data is flowing through your program.

### Using const
Many languages have a way to declare a value as immutable. In Go, this is done with the const keyword. Be aware that const in Go is very limited. Constants in Go are a way to give names to literals.

### Unused Variables
Another Go requirement is that every declared local variable **must be read**. It is a compile-time error to declare a local variable and to not read its value. As long as a variable is read once, the compiler won’t complain, even if there are writes to the variable that are never read.

### Naming 
**idiomatic Go uses camel case (names like indexCounter or numberTries) when an identifier name consists of multiple words.** Also, don't use unknown names or names start with numbers or underscore for regular variables you declare. An underscore by itself (_) is a special identifier name in Go (will discuss in future).  <br>
The smaller the scope for a variable, the shorter the name that’s used for it. For example, it is common in Go to see single-letter variable names used with for loops.  <br>
These short names serve two purposes. The first is that they eliminate repetitive typing, keeping your code shorter. Second, they serve as a check on how complicated your code is. If you find it hard to keep track of your short-named variables, your block of code is likely doing too much. <br> <br> <br>


## Chapter 3 - Composite Types
### Arrays
arrays are rarely used directly in Go. All elements in the array must be of the type that’s specified. because they come with an unusual limitation: Go considers the size of the array to be part of the type of the array. This makes an array that’s declared to be [3]int a different type from an array that’s declared to be [4]int.
declaration styles:
In the first, you specify the size of the array and the type of the elements in the array. If you have initial values for the array, you can also specify them with an array literal:
```Go
var x [3]int
var x = [3]int{10, 20, 30}
```
When using an array literal to initialize an array, you can replace the number that specifies the number of elements in the array with ...:
```Go
var x = [...]int{10, 20, 30}
```
Go has only one-dimensional arrays, but you can simulate multidimensional arrays. This declares x to be an array of length 2 whose type is an array of ints of length 3.
```Go
var x [2][3]int
```
An out-of-bounds read or write with a variable index compiles but fails at runtime with a panic.

### Slices
Most of the time, when you want a data structure that holds a sequence of values, a slice is what you should use. What makes slices so useful is that you can grow slices as needed. This is because the length of a slice is not part of its type.
```Go
var x []int
var x = []int{10, 20, 30}
```
When no value is assigned, x is assigned the zero value for a slice, which is something you haven’t seen before: **nil**. In Go, nil is an identifier that represents the lack of a value for some types. Like the untyped numeric constants you saw in the previous chapter, nil has no type, so it can be assigned or compared against values of different types. A nil slice contains nothing.
You can simulate multidimensional slices and make a slice of slices:
```Go
var x [][]int
```
A slice is the first type you’ve seen that isn’t comparable. The only thing you can compare a slice with using == is nil. The **slices.Equal** function takes in two slices and returns true if the slices are the same length, and all of the elements are equal.

#### len
Go provides several built-in functions to work with slices. You’ve already seen the built-in len function when looking at arrays. It works for slices too. Passing a nil slice to len returns 0.
#### append
The built-in append function is used to grow slices. One slice is appended onto another by using the ... operator to expand the source slice into individual values
```Go
var x []int
x = append(x, 10)
x = append(x, 5, 6, 7)
y := []int{20, 30, 40}
x = append(x, y...)
```

#### capacity
Every slice also has a **capacity**, which is the number of consecutive memory locations reserved. This can be larger than the length. Each time you append to a slice, one or more values is added to the end of the slice. Each value added increases the length by one. When the length reaches the capacity, there’s no more room to put values. If you try to add additional values when the length equals the capacity, the append function uses the Go runtime to allocate a new backing array for the slice with a larger capacity (the capacity doubles). The values in the original backing array are copied to the new one, the new values are added to the end of the new backing array, and the slice is updated to refer to the new backing array. Finally, the updated slice is returned.
```Go
var x []int
fmt.Println(x, len(x), cap(x))
```

#### make
the built-in make function allows you to specify the type, length, and, optionally, the capacity. Let’s take a look (In the last case, you have a non-nil slice with a length of 0 but a capacity of 10.):
```Go
x := make([]int, 5)
x := make([]int, 5, 10)
x := make([]int, 0, 10)
```

One common beginner mistake is to try to populate those initial elements using append:
```Go 
x := make([]int, 5)
x = append(x, 10)
```
The 10 is placed at the end of the slice, after the zero values in elements 0–4 because append always increases the length of a slice. The value of x is now [0 0 0 0 0 10].

#### Emptying an slice
Go 1.21 added a `clear` function that takes in a slice and sets all of the slice’s elements to their zero value. **The length of the slice remains **unchanged.

#### Slicing Slices
A slice expression creates a slice from a slice. It’s written inside brackets and consists of a starting offset and an ending offset, separated by a colon (:). The starting offset is the first position in the slice that is included in the new slice, and the ending offset is one past the last position to include. If you leave off the starting offset, 0 is assumed. Likewise, if you leave off the ending offset, the end of the slice is substituted.

```Go
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
Like most languages, Go provides a built-in data type for situations where you want to associate one value to another. The zero value for a map is nil. A nil map has a length of 0. In the code below, nilMap is declared to be a map with string keys and int values:
```Go
var nilMap map[string]int
```
**NOTE**: Attempting to read a nil map always returns the zero value for the map’s value type. However, attempting to write to a nil map variable causes a panic. <br>
**NOTE**: The key for a map can be **any comparable type**. This means you cannot use a slice or a map as the key for a map.
**NOTE**: you cannot have duplicate key in maps.

You can use a := declaration to create a map variable by assigning it a map literal:
```Go
totalWins := map[string]int{}
```
In this case, you are using an empty map literal. This is not the same as a nil map. It has a length of 0, but you can read and write to a map assigned an empty map literal. <br>

A map literal’s body is written as the key, followed by a colon (:), then the value. A comma separates each key-value pair in the map, even on the last line. Here’s what a nonempty map literal looks like:
```Go
teams := map[string][]string {
    "Orcas": []string{"Fred", "Ralph", "Bijou"},
    "Lions": []string{"Sarah", "Peter", "Billie"},
    "Kittens": []string{"Waldo", "Raul", "Ze"},
}
```

If you know how many key-value pairs you intend to put in the map but don’t know the exact values, you can use make to create a map with a default size. Maps created with make still have a length of 0, and they can grow past the initially specified size:
```go
ages := make(map[int][]string, 10)
```

Maps are like slices in several ways:
- Maps automatically grow as you add key-value pairs to them.
- If you know how many key-value pairs you plan to insert into a map, you can use make to create a map with a specific initial size.
- Passing a map to the len function tells you the number of key-value pairs in a map.
- The zero value for a map is nil.
- Maps are not comparable. You can check if they are equal to nil, but you cannot check if two maps have identical keys and values using == or differ using !=.


#### When should you use a map, and when should you use a slice? 
You should use slices for lists of data when the data should be processed sequentially or the order of the elements is important.  <br>
Maps are useful when you need to organize values using something other than an increasing integer value, such as a name. <br> 
You assign a value to a map key by putting the key within brackets and using = to specify the value, and you read the value assigned to a map key by putting the key within brackets. <br>
**Note**: you cannot use := to assign a value to a map key.

```go
totalWins := map[string]int{}
totalWins["Orcas"] = 1
totalWins["Lions"] = 2
fmt.Println(totalWins["Orcas"])   // Prints 1
fmt.Println(totalWins["Kittens"]) // Prints 0
fmt.Printf("%v\n", totalWins)     // Prints map[Lions:2 Orcas:1]
totalWins["Kittens"]++
totalWins["Lions"] = 3
fmt.Printf("%v\n", totalWins) // Prints map[Kittens:1 Lions:3 Orcas:1]
```

Because a map returns its zero value by default, this works even when there’s no existing value associated with the key.

#### The comma ok Idiom
Go provides the comma ok idiom to tell the difference between a key that’s associated with a zero value and a key that’s not in the map. If ok is false, the key is not present in the map.
```go 
m := map[string]int{
	"hello": 5,
	"world": 0,
}
v, ok := m["hello"]
fmt.Println(v, ok) // 5 true
v, ok = m["world"]
fmt.Println(v, ok) // 0 true
v, ok = m["goodbye"]
fmt.Println(v, ok) // 0 false
```

#### Deleting from Maps
Key-value pairs are removed from a map via the built-in delete function. The delete function takes a map and a key and then removes the key-value pair with the specified key. If the key isn’t present in the map or if the map is nil, **nothing happens**. The delete function doesn’t return a value.
```go
m := map[string]int{
"hello": 5,
"world": 10,
}
delete(m, "hello")
```

#### Emptying a Map
The clear function that you saw in “Emptying an slice” works on maps also. A cleared map has its length set to zero, unlike a cleared slice:
```go
m := map[string]int{
    "hello": 5,
    "world": 10,
}
fmt.Println(m, len(m)) // map[hello:5 world:10] 2
clear(m)
fmt.Println(m, len(m)) // map[] 0
```

#### Using Maps as Sets
Many languages include a set in their standard library. A set is a data type that ensures there is at most one of a value, but doesn’t guarantee that the values are in any particular order. <br> 
Go doesn’t include a set, but you can use a map to simulate some of its features. Use the key of the map for the type that you want to put into the set and use a bool for the value.

```go
intSet := map[int]bool{}
vals := []int{5, 10, 2, 5, 8, 7, 3, 9, 1, 2, 10}
for _, v := range vals {
    intSet[v] = true
}
fmt.Println(len(vals), len(intSet)) // 11 8
fmt.Println(intSet[5]) // true
fmt.Println(intSet[500]) // false
if intSet[100] {
    fmt.Println("100 is in the set")
}
```

### Structs 
When you have related data that you want to group together, you should define a struct. A struct type is defined with the keyword type, the name of the struct type, the keyword struct, and a pair of braces ({}). Within the braces, you list the fields in the struct. Also note that unlike in map literals, no commas separate the fields in a struct declaration.
```go
type person struct {
    name string
    age int 
    pet string
}
```
Once a struct type is declared, you can define variables of that type. A zero value struct has every field set to the field’s zero value. Unlike maps, there is no difference between assigning an empty struct literal and not assigning a value at all. Both initialize all fields in the struct to their zero values.
```go
var fred person
bob := person{}
```

here are two styles for a nonempty struct literal. You cannot mix the two struct literal styles: either all fields are specified with names, or none of them are.
```go 
julia := person{
    "Julia",
    40,
    "cat",
}
beth := person{
    age: 30,
    Name: "Ann",
}
```
In the second style, you use the names of the fields in the struct to specify the values. This style has some advantages. It allows you to specify the fields in any order, and you don’t need to provide a value for all fields. Any field not specified is set to its zero value.


#### Anonymous Structs
You can also declare that a variable implements a struct type without first giving the struct type a name. This is called an anonymous struct. In this example, the types of the variables person and pet are anonymous structs:
```go
var person struct {
    name string
    age int
    pet string
}

person.name = "bob"
person.age = 50
person.pet = "dog"

pet := struct {
    name string
    kind string
}{
    name: "Fido",
    kind: "dog",
}
```
Anonymous structs are handy in two common situations. The first is when you translate external data into a struct or a struct into external data (like JSON or Protocol Buffers). This is called unmarshaling and marshaling data, respectively.

#### Comparing and Converting Structs
Structs that are entirely composed of comparable types are comparable; those with slice or map fields are not. 

Go doesn’t allow comparisons between variables that represent structs of different types. Go does allow you to perform a type conversion from one struct type to another if the fields of both structs have the same names, order, and types.



<br><br><br>

## Chapter 4 - Blocks, Shadows, and Control Structures
### Blocks
Each place where a declaration occurs is called a block. Variables, constants, types, and functions declared outside of any functions are placed in the package block.
 

### Shadowing Variables 
A shadowing variable is a variable that has the same name as a variable in a containing block. For as long as the shadowing variable exists, you cannot access a shadowed variable.

### if
```go
n := rand.Intn(10)
if n == 0 {
    fmt.Println("That's too low")
} else if n > 5 {
    fmt.Println("That's too big:", n)
} else {
    fmt.Println("That's a good number:", n)
}
```

Scoping a variable to the if statement:
```go
if n := rand.Intn(10); n == 0 {
    fmt.Println("That's too low")
} else if n > 5 {
    fmt.Println("That's too big:", n)
} else {
f   mt.Println("That's a good number:", n)
}
```

### for, Four Ways
- A complete, C-style for
- A condition-only for
- An infinite for
- for-range

#### The Complete for Statement
```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

i := 0
for ; i < 10; i++ {
    fmt.Println(i)
}

for i := 0; i < 10; {
    fmt.Println(i)
    if i % 2 == 0 {
        i++
    } else {
        i+=2
    }
}
```

#### The Condition-Only for Statement
```go
i := 1
for i < 100 {
    fmt.Println(i)
    i = i * 2
}
```



#### The Infinite for Statement
```go
for {
    fmt.Println("Hello")
}
```


#### break and continue 
How do you get out of an infinite for loop without using the keyboard or turning off your computer? That’s the job of the **break** statement. It exits the loop immediately, just like the break statement in other languages.

If you want to iterate at least once, the cleanest way is to use an infinite for loop that ends with an if statement:
```go
for {
// things to do in the loop
    if !CONDITION {
        break
    }
}   
```

Go also includes the **continue** keyword, which skips over the rest of the for loop’s body and proceeds directly to the next iteration.

Go encourages short if statement bodies, as left-aligned as possible. Nested code is more difficult to follow. Using a continue statement makes it easier to understand what’s going on:
```go 
for i := 1; i <= 100; i++ {
    if i%3 == 0 && i%5 == 0 {
        fmt.Println("FizzBuzz")
        continue
    }
    if i%3 == 0 {
        fmt.Println("Fizz")
        continue
    }
    if i%5 == 0 {
        fmt.Println("Buzz")
        continue
    }
    fmt.Println(i)
}
```

#### The for-range Statement
The fourth for statement format is for iterating over elements in some of Go’s built-in types. It is called a for-range loop and resembles the iterators found in other languages. The first variable is the position in the data structure being iterated, while the second is the value at that position.

```go
evenVals := []int{2, 4, 6, 8, 10, 12}
for i, v := range evenVals {
    fmt.Println(i, v)
}
```
