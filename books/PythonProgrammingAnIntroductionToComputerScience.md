# Python Programming: An Introduction To Computer Science

- [Python Programming: An Introduction To Computer Science](#python-programming-an-introduction-to-computer-science)
  - [Chapter 1 - Computers and Programs](#chapter-1---computers-and-programs)
    - [1.1 The Universal Machine](#11-the-universal-machine)
    - [1.2 Program Power](#12-program-power)
    - [1.3 What Is Computer Science?](#13-what-is-computer-science)
    - [1.4 Computer Hardware](#14-computer-hardware)
    - [1.5 Programing Language](#15-programing-language)
    - [1.6 The Magic of Python](#16-the-magic-of-python)


## Chapter 1 - Computers and Programs
### 1.1 The Universal Machine
A modern computer can be defined as "a machine that stores and **manipu­lates information** under the control of **a changeable program**."


A **computer program** is a detailed, step-by-step set of instructions telling a computer exactly what to do. If we change the program, then the computer performs a different sequence of actions, and hence, performs a different task (this is the difference between a computer and a simple calculator).


One of the remarkable discoveries of computer science is the realization that all of these different com­puters have the same power; with suitable programming, each computer can basically do all the things that any other computer can do. In this sense, the PC that you might have sitting on your desk is really **a universal machine**.

<br>

### 1.2 Program Power
Software (pro­grams) rules the hardware (the physical machine). Without software, computers would just be expensive paperweights. Good programming re­quires an ability to see the big picture while paying attention to minute detail.

### 1.3 What Is Computer Science?
The com­puter is an important tool in computer science, but it is not itself the object of study.

The three main techniques of investigation to answer "What can be computed?" are **design, analysis, and experimentation.**

**Algorithm:** One way to demonstrate that a particular problem can be solved is to actu­ally design a solution. That is, we develop a step-by-step process for achieving the desired result. Computer scientists call this an **algorithm**.

**analysis:** failing to find an algorithm does not mean that a problem is unsolvable. It may mean that I'm just not smart enough, or I haven't hit upon the right idea yet. This is where **analysis** comes in. 
- Analysis is the process of examining algorithms and problems mathemati­cally.

**Experimentation:** Some problems are too complex or ill-defined to lend themselves to anal­ysis. In such cases, computer scientists rely on experimentation; they actually implement systems and then study the resulting behavior.


### 1.4 Computer Hardware
- The central processing unit (CPU) is the "brain" of the machine. This is where all the basic operations of the computer are carried out.
- The memory stores programs and data. The CPU can directly access only information that is stored in main memory (called RAM for Random Access Mem­ory). Main memory is fast, but it is also volatile. That is, when the power is turned off, the information in the memory is lost. Thus, there must also be some secondary memory that provides more permanent storage.
- the principal secondary memory is typically an internal hard disk drive (HOD) or a solid state drive (SSD).
    - An HDD stores information as magnetic patterns on a spinning disk, while an SSD employs elec­ tronic circuits known as flash memory.
    - Most computers also support removeable media for secondary memory such as USB memory "sticks" (also a form of flash memory) and DVDs (digital versatile discs), which store information as optical patterns that are read and written by a laser. 
- Information from input devices (a keyboard or a mouse) is processed by the CPU and may be shuffled off to the main or secondary memory. Similarly, when information needs to be displayed, the CPU sends it to one or more output devices (a monitor or a speaker).
- what happens when you fire up your favorite game or word processing program?
    - First, the instructions that comprise the program are copied from the (more) permanent secondary memory into the main memory of the computer. 
    - Once the instructions are loaded, the CPU starts executing the program. 
    - Technically the CPU follows a process called the **fetch-execute cycle**:
        - The first instruction is retrieved from memory, decoded to figure out what it represents, and the appropriate action carried out. Then the next instruction is fetched, decoded, and executed. The cycle continues, instruction after instruction (fetch, decode, execute).

### 1.5 Programing Language
we need to provide a sequence of instructions in a language that a computer can understand. 

Even if computers could understand us, human languages are not very well suited for describing complex algorithms.

Every structure in a programming language has a precise form (**its syntax**) and a precise meaning (**its semantics**).

**compiler or interpreter:** computer hardware can understand only a very low-level language known as machine language. In a high-level language like Python, the addition of two numbers can be expressed more naturally: c = a + b. That's a lot easier for us to understand, but we need some way to translate the high-level language into the machine language that the computer can execute.
- A **compiler** is a complex computer program that takes another program writ­ ten in a high-level language and translates it into an equivalent program in the machine language of some computer.
- An **interpreter** is a program that simulates a computer that understands a high-level language. Rather than translating the source program into a machine language equivalent, the interpreter analyzes and executes the source code in­ struction by instruction as necessary.
- The **difference** between interpreting and compiling is that compiling is a one­ shot translation; once a program is compiled, it may be run over and over again without further need for the compiler or the source code. In the interpreted case, the interpreter and the source are needed every time the program runs. Compiled programs tend to be faster, since the translation is done once and for all, but interpreted languages lend themselves to a more flexible programming environment as programs can be developed and run interactively.
- a program written in a high-level language can be run on many different kinds of computers as long as there is a suitable compiler or interpreter.

### 1.6 The Magic of Python
**module or script:** One problem with entering functions interactively into a Python shell as we did with the hello and greet examples is that the definitions are lost when we quit the shell. If we want to use them again the next time, we have to type them. all over again. Programs are usually created by typing definitions into a separate file called **a module or script**. This file is saved in secondary memory so that it can be used over and over again.
- A module file is just a file of text, and you can create one using any ap­plication for editing text, such as notepad or a word processor, provided you save your program as a "plain text" file.
- A special type of application known as an **Integrated Development Environment (IDE)** simplifies the process. An IDE is specifically designed to help programmers write programs and includes features such as automatic indenting, color highlighting, and interactive development.
- The . py extension indicates that this is a Python module.
- Our programs can be run in a number of different ways that depend on the actual operating system and programming environment that you are using. you can probably run a Python program by clicking (or double-clicking) on the module file's icon. Also, in a command line situation, you might type a command like ` python chaos.py `.


## Chapter 2 - Writing simple programs
### 2.1 The Software Development Process
The process of creating a program is often broken down into stages according to the information that is produced in each phase.
- **Analyze the Problem**: Figure out exactly what the problem to be solved is.
- **Determine Specifications**: Describe exactly what your program will do. At this point, you should not worry about how your program will work, but rather about deciding exactly what it will accomplish.
- **Create a Design**: Formulate the overall structure of the program. This is where the how of the program gets worked out. The main task is to design the algorithm (s) that will meet the specifications.
- **Implement the Design**: Translate the design into a computer language and put it into the computer.
- **Test/Debug the Program**: Try out your program and see whether it works as expected. If there are any errors (often called bugs), then you should go back and fix them. The process of locating and fixing errors is called debugging a program.
- **Maintain the Program**: Continue developing the program in response to the needs of your users. Most programs are never really finished; they keep evolving over years of use.

### 2.3 Elements of Programs

#### Names

We give names to modules (e.g., convert) and to the functions within modules (e.g., main). Variables are used to give names to values (e.g., celsius and fahrenheit). Technically, all these names are called **identifiers**.' <br> Every identifier must **begin with a letter or underscore** (the "_" character) which may be followed by any sequence of letters, digits, or underscores. <br> Identifiers are **case-sensitive**. <br> **Good programmers always try to choose names that describe the thing being named.** <br>
some identifiers are part of Python itself and are called reserved words or keywords and cannot be used as ordinary identifiers:

| Column 1 | Column 2 | Column 3 | Column 4 | Column 5 | Column 6 |
|----------|----------|----------|----------|----------|----------|
| False    | break    | for      | is       | not      | try      |
| None     | class    | from     | lambda   | or       | while    |
| True     | continue | global   | nonlocal | pass     | with     |
| and      | def      | if       | ra1se    | return   | yield    |
| as       | del      | import   | 1n       | finally  | except   |
| assert   | elif     | else     |          |          |          |

Python also includes quite a number of built-in functions, such as the print function that we've already been using. <br> 
While it's technically legal to (re)use the built-in function-name identifiers for other purposes, it's generally a very bad idea to do so. <br>

---
#### Expressions

all data has to be stored on the computer in some digital format, and different types of data are stored in different ways.
The fragments of program code that produce or calculate new data values are called **expressions**. <br>
The simplest kind of expression is a **literal**. A literal is used to indicate a specific value. <br>
The numbers 3.9 and 9 are all examples of **numeric literals.** <br>
Com­puter scientists refer to textual data as **strings**. You can think of a string as just a sequence of printable characters. A string literal is indicated in Python by en­closing the characters in quotation marks (""). <br>
The process of turning an expression into an underlying data type is called evaluation. <br>
More complex and interesting expressions can be constructed by combin­ing simpler expressions with **operators**.
- addition, subtraction, multiplication, divi­sion, and exponentiation (+, -, *, /, and **).
- Python also provides operators for strings. For example, you can "add" strings. For example, "bat" + "man" becomes "batman". This is called **concatenation**. <br>
- A template for the print statement including the **keyword** parameter to
specify the ending text looks like this: <br> `print (<expr>, <e xpr>, . . . , <expr>, end="\n") ` <br>


### 2.5 Assignment Statements
The basic assignment statement has this form:
```python
<variable> = <expr>
```
Python assignment statements are actually slightly different from the "vari­able as a box" model. In Python, values may end up anywhere in memory, and variables are used to refer to them. Assigning a variable is like putting one of those little yellow sticky notes on the value and saying, "this is x."
