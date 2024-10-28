C is one of the most popular and widely used programming languages. It's known for being simple, fast, and powerful. This page will walk you through the basic concepts of C in the simplest terms possible (no big words).

```
An idiot admires complexity, a genius admires simplicit, a physicist tries to make it simple, for an idiot the more complicated something is the more he will admire it, if you make something so clusterfucked he can't understand it he's gonna think you're a god. That's how they write journals in Academics, they try to make it complicated, so people think they're a genius

― Terry Davis, Creator of Temple OS
```

## What is C?

C is a high-level programming language developed in the 1970s. It's known for its efficiency and control over computer memory. Many modern languages like C++, Java, Python and especially Rust have roots in C. Learning C surprisingly although might seem a bit redundant now a days can massively help your understand of these languages.


## Basic Structure

Every C program has a simple structure:

``` c
#include <stdio.h> // imports

int main() {
	// This is where the program starts executing
	printf("Hello, World!\n");
	return 0;
}
```

- `#include <stdio.h>`: This includes the standard input/output library so you can use functions like `printf()`.
- `int main() {}`: Every C program must have a `main()` function, which is where the program starts executing.
- `printf()`: This function prints text to the screen.
- `return 0;`: This tells the system the program has finished successfully.

## Data Types

Data types in c refer to an extensive system used for declaring variables or functions of different types. The type of a variable determines how much space it occupies in storage and how the bit pattern stored is interpreted:

|     | Types & Description                                                                                                                                                                |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Basic Types**<br><br>They are arithmetic types and are further classified into: (a) integer types and (b) floating-point types.                                                  |
| 2   | **Enumerated types**<br><br>They are again arithmetic types and they are used to define variables that can only assign certain discrete integer values throughout the program.<br> |
| 3   | **The type void**<br><br>The type specifier _void_ indicates that no value is available.<br>                                                                                       |
| 4   | **Derived types**<br><br>They include (a) Pointer types, (b) Array types, (c) Structure types, (d) Union types and (e) Function types.                                             |
#### Integer Types
The following table provides the details of standard integer types with their storage sizes and value ranges:

| Type           | Storage size | Value range                                          |
| -------------- | ------------ | ---------------------------------------------------- |
| char           | 1 byte       | -128 to 127 or 0 to 255                              |
| unsigned char  | 1 byte       | 0 to 255                                             |
| signed char    | 1 byte       | -128 to 127                                          |
| int            | 2 or 4 bytes | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
| unsigned int   | 2 or 4 bytes | 0 to 65,535 or 0 to 4,294,967,295                    |
| short          | 2 bytes      | -32,768 to 32,767                                    |
| unsigned short | 2 bytes      | 0 to 65,535                                          |
| long           | 8 bytes      | -9223372036854775808 to 9223372036854775807          |
| unsigned long  | 8 bytes      | 0 to 18446744073709551615                            |
To get the exact size of a type or a variable on a particular platform, you can use the **sizeof** operator. these limits are group together in a `limits.h` header.

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <float.h>

int main(int argc, char** argv) {
    printf("CHAR_BIT    :   %d\n", CHAR_BIT);
    printf("CHAR_MAX    :   %d\n", CHAR_MAX);
    printf("CHAR_MIN    :   %d\n", CHAR_MIN);
    printf("INT_MAX     :   %d\n", INT_MAX);
    printf("INT_MIN     :   %d\n", INT_MIN);
    printf("LONG_MAX    :   %ld\n", (long) LONG_MAX);
    printf("LONG_MIN    :   %ld\n", (long) LONG_MIN);
    printf("SCHAR_MAX   :   %d\n", SCHAR_MAX);
    printf("SCHAR_MIN   :   %d\n", SCHAR_MIN);
    printf("SHRT_MAX    :   %d\n", SHRT_MAX);
    printf("SHRT_MIN    :   %d\n", SHRT_MIN);
    printf("UCHAR_MAX   :   %d\n", UCHAR_MAX);
    printf("UINT_MAX    :   %u\n", (unsigned int) UINT_MAX);
    printf("ULONG_MAX   :   %lu\n", (unsigned long) ULONG_MAX);
    printf("USHRT_MAX   :   %d\n", (unsigned short) USHRT_MAX);

    return 0;
}
```

#### Floating-Point Types
The following table provide the details of standard floating-point types with storage sizes and value ranges and their precision:

|Type|Storage size|Value range|Precision|
|---|---|---|---|
|float|4 byte|1.2E-38 to 3.4E+38|6 decimal places|
|double|8 byte|2.3E-308 to 1.7E+308|15 decimal places|
|long double|10 byte|3.4E-4932 to 1.1E+4932|19 decimal places|
The header file float.h defines macros that allow you to use these values and other details about the binary representation of real numbers in your programs. The following example prints the storage space taken by a float type and its range values:

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <float.h>

int main(int argc, char** argv) {
    printf("Storage size for float : %d \n", (int) sizeof(float));
    printf("FLT_MAX     :   %g\n", (float) FLT_MAX);
    printf("FLT_MIN     :   %g\n", (float) FLT_MIN);
    printf("-FLT_MAX    :   %g\n", (float) -FLT_MAX);
    printf("-FLT_MIN    :   %g\n", (float) -FLT_MIN);
    printf("DBL_MAX     :   %g\n", (double) DBL_MAX);
    printf("DBL_MIN     :   %g\n", (double) DBL_MIN);
    printf("-DBL_MAX     :  %g\n", (double) -DBL_MAX);
    printf("Precision value: %d\n", FLT_DIG );

    return 0;
}
```

#### The Void Type
The void type specifies that no value is available, kinda like how it is used in the `TypeScript` and `Java`. It is used in three kinds of situations:

| Sr.No. | Types & Description                                                                                                                                                                                                                                    |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1      | **Function returns as void**<br><br>There are various functions in C which do not return any value or you can say they return void. A function with no return value has the return type as void. For example, **void exit (int status);**              |
| 2      | **Function arguments as void**<br><br>There are various functions in C which do not accept any parameter. A function with no parameter can accept a void. For example, **int rand(void);**                                                             |
| 3      | **Pointers to void**<br><br>A pointer of type void * represents the address of an object, but not its type. For example, a memory allocation function *_void _malloc( size_t size );__ returns a pointer to void which can be casted to any data type. |

## Variables in C

Variables act similarly to how they do in every other language but C has a few interesting qualities that make it somewhat awkward to work with:

Based on the basic types explained in the [[#Data Types]] section, there will be the following basic variable types:

| Sr.No. | Type & Description                                                         |
| ------ | -------------------------------------------------------------------------- |
| 1      | **char**<br><br>Typically a single octet(one byte). It is an integer type. |
| 2      | **int**<br><br>The most natural size of integer for the machine.           |
| 3      | **float**<br><br>A single-precision floating point value.                  |
| 4      | **double**<br><br>A double-precision floating point value.                 |
| 5      | **void**                                                                   |
#### Variable Definition in C
A variable definition tells the compiler where and how much storage to allocate for the variable. A variable definition specifies a data type and contains a list of one or more variables of that type as follows:

```c
type variable_list;
```

Here, **type** must be a valid C data type including char, w_char, int, float, double, bool, or any user-defined object; and **variable_list** may consist of one or more identifier names separated by commas. Some valid declarations are shown here −

```c
int    i, j, k;
char   c, ch;
float  f, salary;
double d;
```

The line **int i, j, k;** declares and defines the variables i, j, and k; which instruct the compiler to create variables named i, j and k of type int.

Similar to most languages variables can be initialised in their declaration. The initialiser consists of an equal sign followed by a constant expression as follows:

```c
type variable_name = value;
extern int d = 3, f = 5;    // declaration of d and f. 
int d = 3, f = 5;           // definition and initializing d and f. 
byte z = 22;                // definition and initializes z. 
char x = 'x';               // the variable x has the value 'x'.
```

Variables with static storage duration are implicitly initialised with `NULL` the initial value of all other variables are undefined.

#### Variable Declaration in C
A variable declaration provides assurance to the compiler that there exists a variable with the given type and name so that the compiler can proceed for further compilation without requiring the complete detail about the variable.

In this example variables have been defined and used:

```c
#include <stdio.h>

// Variable declaration:
extern int a, b;
extern int c;
extern float f;

int main () {

   /* variable definition: */
   int a, b;
   int c;
   float f;
 
   /* actual initialisation */
   a = 10;
   b = 20;
  
   c = a + b;
   printf("value of c : %d \n", c);

   f = 70.0/3.0;
   printf("value of f : %f \n", f);
 
   return 0;
}
```

The same idea also applies on function declaration where you provide a function name at the time of its declaration and its actual definition can be given anywhere else. For example:

```c
// function declaration
int func();

int main() {

   // function call
   int i = func();
}

// function definition
int func() {
   return 0;
}
```

#### Lvalues and Rvalues in C
In C, there are two types of expressions:

- **LValue** (left value): These refer to a memory location, meaning they represent something that can be stored in memory, like a variable. You can use an lvalue on either side of an assignment (left or right).
    
- **RValue** (right value): These are actual data values stored in memory, like numbers. An rvalue cannot be assigned a value, so it can only appear on the right side of an assignment, not the left.

Variables are lvalues and so they may appear on the left-hand side of an assignment. Numeric literals are rvalues and so they may not be assigned and cannot appear on the left-hand side. Take a look at the following valid and invalid statements −

```c
int g = 20; // valid statement

10 = 20; // invalid statement; would generate compile-time error
```

## Constants and Literals
Constants refer to fixed values that the program may not alter during its execution. These fixed values are also called **literals**.

#### Character Constants
Character literals are enclosed in single quotes, e.g., 'x' can be stored in a simple variable of **char** type.

| Escape sequence | Meaning                                  |
| --------------- | ---------------------------------------- |
| \\              | \ character                              |
| \'              | ' character                              |
| \"              | " character                              |
| \?              | ? character                              |
| \a              | Alert or bell                            |
| \b              | Backspace                                |
| \f              | Form feed                                |
| \n              | Newline                                  |
| \r              | Carriage return                          |
| \t              | Horizontal tab                           |
| \v              | Vertical tab                             |
| \ooo            | Octal number of one to three digits      |
| \xhh …      | Hexadecimal number of one or more digits |
Following is the example to show a few escape sequence characters:

```c
#include <stdio.h>

int main() {
   printf("Hello\tWorld\n\n");

   return 0;
}
```

#### Const Keyword
You can use **const** prefix to declare constants with a specific type as follows. Just like `JavaScript`

```c
const type variable = value;
```

Here's a more in-depth example:

```c
#include <stdio.h>

int main() {
   const int  LENGTH = 10;
   const int  WIDTH = 5;
   const char NEWLINE = '\n';
   int area;  
   
   area = LENGTH * WIDTH;
   printf("value of area : %d", area);
   printf("%c", NEWLINE);

   return 0;
}
```

## Storage Class
A storage class defines the scope (visibility) and life-time of variables and/or functions within a C Program. They precede the type that they modify. We have four different storage classes in a C program.

- Auto
- Register
- Static

**Auto**
The **auto** storage class is the default for all local variables in C. When you declare a variable inside a function, it's automatically considered an "auto" variable, even if you don't explicitly write "auto."

```c
{
   int mount;
   auto int month;
}
```

In the example above, both `mount` and `month` are local variables with the same behavior because "auto" is implied for all local variables. However, the "auto" keyword is rarely used since it's the default. **Auto variables exist only inside the function they are declared in**, and their values are lost once the function finishes.


**The register Storage Class**
The **register** storage class is used to suggest that a variable should be stored in a CPU register instead of RAM. This allows the variable to be accessed faster because CPU registers are faster than RAM. However, there are some limitations:

- The size of the variable can't be larger than the register size, which is usually the size of one word (depending on the machine).
- You **cannot use the '&' operator** (which gives the address of a variable) on a register variable, because it may not have a memory address (it's stored in the CPU register).

```c
{
   register int  miles;
}
```

**When to use:** You should use the `register` keyword for variables that need very fast access, like loop counters. But note that using `register` **doesn't guarantee** that the variable will actually be stored in a register. The compiler decides whether to store it in a register or not, depending on the hardware and other factors.


**The static Storage Class**
The **static** storage class changes how variables behave.

- For **local variables**, the `static` keyword makes the variable keep its value even after the function in which it was declared ends. Normally, local variables are destroyed after a function finishes, but static local variables "remember" their values between function calls.
    
- For **global variables**, `static` restricts their visibility to the file in which they are declared. This means that other files in the program cannot access this global variable.
  
Example with a local static variable:

```c
#include <stdio.h>
 
/* function declaration */
void func(void);
 
static int count = 5; /* global variable */
 
main() {

   while(count--) {
      func();
   }
	
   return 0;
}

/* function definition */
void func( void ) {

   static int i = 5; /* local static variable */
   i++;

   printf("i is %d and count is %d\n", i, count);
}
```

**What happens here:**

1. `count` is a **global static variable**, meaning it's only visible in this file, and its value is shared throughout the program. It starts at 5 and is decremented each time the `main()` loop runs.
    
2. Inside `func()`, the variable `i` is a **local static variable**. Normally, local variables disappear when a function ends, but because `i` is static, it keeps its value between calls. Each time `func()` runs, `i` increases by 1, even though it's declared inside the function.
    

**Use of `static`:**

- For local variables: It helps to maintain a value between function calls (e.g., a counter or state).
- For global variables: It limits access to the variable within the same file, preventing conflicts with other files.

## Operators
Simple stuff same as every other language, there's a few differing types though:

- Arithmetic Operators
- Relational Operators
- Logical Operators
- Bitwise Operators
- Assignment Operators
- Misc Operators

**Arithmetic Operators**
The following table shows all the arithmetic operators supported by the C language.

| Operator | Description                                                  | Example     |
| -------- | ------------------------------------------------------------ | ----------- |
| +        | Adds two operands.                                           | A + B = 30  |
| −        | Subtracts second operand from the first.                     | A − B = -10 |
| *        | Multiplies both operands.                                    | A * B = 200 |
| /        | Divides numerator by de-numerator.                           | B / A = 2   |
| %        | Modulus Operator and remainder of after an integer division. | B % A = 0   |
| ++       | Increment operator increases the integer value by one.       | A++ = 11    |
| --       | Decrement operator decreases the integer value by one.       | A-- = 9     |

**Relational Operators**
The following table shows all the relational operators supported by C.

|Operator|Description|Example|
|---|---|---|
|==|Checks if the values of two operands are equal or not. If yes, then the condition becomes true.|(A == B) is not true.|
|!=|Checks if the values of two operands are equal or not. If the values are not equal, then the condition becomes true.|(A != B) is true.|
|>|Checks if the value of left operand is greater than the value of right operand. If yes, then the condition becomes true.|(A > B) is not true.|
|<|Checks if the value of left operand is less than the value of right operand. If yes, then the condition becomes true.|(A < B) is true.|
|>=|Checks if the value of left operand is greater than or equal to the value of right operand. If yes, then the condition becomes true.|(A >= B) is not true.|
|<=|Checks if the value of left operand is less than or equal to the value of right operand. If yes, then the condition becomes true.|(A <= B) is true.|

**Logical Operators**
Following table shows all the logical operators supported by C language.

|Operator|Description|Example|
|---|---|---|
|&&|Called Logical AND operator. If both the operands are non-zero, then the condition becomes true.|(A && B) is false.|
|\||Called Logical OR Operator. If any of the two operands is non-zero, then the condition becomes true.|(A \| B) is true.|
|!|Called Logical NOT Operator. It is used to reverse the logical state of its operand. If a condition is true, then Logical NOT operator will make it false.|!(A && B) is true.|

**Bitwise Operators**
Bitwise operator works on bits and perform bit-by-bit operation. The truth tables for &, |, and ^ is as follows:

| p   | q   | p & q | p \| q | p ^ q |
| --- | --- | ----- | ------ | ----- |
| 0   | 0   | 0     | 0      | 0     |
| 0   | 1   | 0     | 1      | 1     |
| 1   | 1   | 1     | 1      | 0     |
| 1   | 0   | 0     | 1      | 1     |

| Operator | Description                                                                                                               | Example                        |
| -------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------ |
| &        | Binary AND Operator copies a bit to the result if it exists in both operands.                                             | (A & B) = 12, i.e., 0000 1100  |
| \|       | Binary OR Operator copies a bit if it exists in either operand.                                                           | (A \| B) = 61, i.e., 0011 1101 |
| ^        | Binary XOR Operator copies the bit if it is set in one operand but not both.                                              | (A ^ B) = 49, i.e., 0011 0001  |
| ~        | Binary One's Complement Operator is unary and has the effect of 'flipping' bits.                                          | (~A ) = ~(60), i.e,. -0111101  |
| <<       | Binary Left Shift Operator. The left operands value is moved left by the number of bits specified by the right operand.   | A << 2 = 240 i.e., 1111 0000   |
| >>       | Binary Right Shift Operator. The left operands value is moved right by the number of bits specified by the right operand. | A >> 2 = 15 i.e., 0000 1111    |

**Assignment Operators**
The following table lists the assignment operators:

| Operator | Description                                                                                                                         | Example                                       |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| =        | Simple assignment operator. Assigns values from right side operands to left side operand                                            | C = A + B will assign the value of A + B to C |
| +=       | Add AND assignment operator. It adds the right operand to the left operand and assign the result to the left operand.               | C += A is equivalent to C = C + A             |
| -=       | Subtract AND assignment operator. It subtracts the right operand from the left operand and assigns the result to the left operand.  | C -= A is equivalent to C = C - A             |
| *=       | Multiply AND assignment operator. It multiplies the right operand with the left operand and assigns the result to the left operand. | C *= A is equivalent to C = C * A             |
| /=       | Divide AND assignment operator. It divides the left operand with the right operand and assigns the result to the left operand.      | C /= A is equivalent to C = C / A             |
| %=       | Modulus AND assignment operator. It takes modulus using two operands and assigns the result to the left operand.                    | C %= A is equivalent to C = C % A             |
| <<=      | Left shift AND assignment operator.                                                                                                 | C <<= 2 is same as C = C << 2                 |
| >>=      | Right shift AND assignment operator.                                                                                                | C >>= 2 is same as C = C >> 2                 |
| &=       | Bitwise AND assignment operator.                                                                                                    | C &= 2 is same as C = C & 2                   |
| ^=       | Bitwise exclusive OR and assignment operator.                                                                                       | C ^= 2 is same as C = C ^ 2                   |
| \|=      | Bitwise inclusive OR and assignment operator.                                                                                       | C \|= 2 is same as C = C \| 2                 |

**Misc Operators**
Besides the operators discussed above, there are a few other important operators including **sizeof** and **? :**

|Operator|Description|Example|
|---|---|---|
|sizeof()|Returns the size of a variable.|sizeof(a), where a is integer, will return 4.|
|&|Returns the address of a variable.|&a; returns the actual address of the variable.|
|*|Pointer to a variable.|*a;|
|? :|Conditional Expression.|If Condition is true ? then value X : otherwise value Y|

## Conditional Blocks
Simple stuff same as every other language, in fact it's very similar to JavaScript here:

| Sr.No. | Statement & Description                                                                                                                                                                                                          |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | [if statement](https://www.tutorialspoint.com/cprogramming/if_statement_in_c.htm)<br><br>An **if statement** consists of a boolean expression followed by one or more statements.                                                |
| 2      | [if...else statement](https://www.tutorialspoint.com/cprogramming/if_else_statement_in_c.htm)<br><br>An **if statement** can be followed by an optional **else statement**, which executes when the Boolean expression is false. |
| 3      | [nested if statements](https://www.tutorialspoint.com/cprogramming/nested_if_statements_in_c.htm)<br><br>You can use one **if** or **else if** statement inside another **if** or **else if** statement(s).                      |
| 4      | [switch statement](https://www.tutorialspoint.com/cprogramming/switch_statement_in_c.htm)<br><br>A **switch** statement allows a variable to be tested for equality against a list of values.                                    |
| 5      | [nested switch statements](https://www.tutorialspoint.com/cprogramming/nested_switch_statements_in_c.htm)<br><br>You can use one **switch** statement inside another **switch** statement(s).                                    |

**The ? : Operator**
We have covered **conditional operator ? :** in the previous chapter which can be used to replace **if…else** statements. It has the following general form −

```c
Exp1 ? Exp2 : Exp3;
```

Where Exp1, Exp2, and Exp3 are expressions. Notice the use and placement of the colon.

The value of a ? expression is determined like this:

- Exp1 is evaluated. If it is true, then Exp2 is evaluated and becomes the value of the entire ? expression.
    
- If Exp1 is false, then Exp3 is evaluated and its value becomes the value of the expression.

## Loops
Simple stuff same as every other language, once again it's very similar to JavaScript here:

| Sr.No. | Loop Type & Description                                                                                                                                                                                              |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1      | [while loop](https://www.tutorialspoint.com/cprogramming/c_while_loop.htm)<br><br>Repeats a statement or group of statements while a given condition is true. It tests the condition before executing the loop body. |
| 2      | [for loop](https://www.tutorialspoint.com/cprogramming/c_for_loop.htm)<br><br>Executes a sequence of statements multiple times and abbreviates the code that manages the loop variable.                              |
| 3      | [do...while loop](https://www.tutorialspoint.com/cprogramming/c_do_while_loop.htm)<br><br>It is more like a while statement, except that it tests the condition at the end of the loop body.                         |
| 4      | [nested loops](https://www.tutorialspoint.com/cprogramming/c_nested_loops.htm)<br><br>You can use one or more loops inside any other while, for, or do..while loop.                                                  |

#### Loop Control

| Sr.No. | Control Statement & Description                                                                                                                                                                                                |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1      | [break statement](https://www.tutorialspoint.com/cprogramming/c_break_statement.htm)<br><br>Terminates the **loop** or **switch** statement and transfers execution to the statement immediately following the loop or switch. |
| 2      | [continue statement](https://www.tutorialspoint.com/cprogramming/c_continue_statement.htm)<br><br>Causes the loop to skip the remainder of its body and immediately retest its condition prior to reiterating.                 |
| 3      | [goto statement](https://www.tutorialspoint.com/cprogramming/c_goto_statement.htm)<br><br>Transfers control to the labeled statement.                                                                                          |

#### The Infinite Loop
A loop becomes an infinite loop if a condition never becomes false. The **for** loop is traditionally used for this purpose. Since none of the three expressions that form the 'for' loop are required, you can make an endless loop by leaving the conditional expression empty.

```c
#include <stdio.h>
 
int main () {

   for(; ;) {
      printf("This loop will run forever.\n");
   }

   return 0;
}
```


## Function
A **function** in C is a group of statements that work together to perform a task. Every C program must have at least one function, which is `main()`. You can also create additional functions to organize your code better, where each function performs a specific task.

Functions make your code easier to manage by breaking it into smaller, reusable parts.

#### The Basics
1. **Function Declaration**: This tells the compiler the function's name, return type, and parameters (input).
2. **Function Definition**: This contains the actual code or statements that the function will execute.

C provides several built-in functions, like:
- `strcat()` to concatenate (combine) two strings.
- `memcpy()` to copy memory from one location to another.

#### Defining a Function
Here's the general structure of a function definition in C:

```c
return_type function_name(parameter list) {
	// Body of the function 
}
```

**Parts of a function:**

- **Return Type**: Specifies the data type of the value the function will return (e.g., `int`, `float`). If no value is returned, the return type is `void`.
- **Function Name**: The name of the function, used when calling it.
- **Parameters**: Variables that hold values passed to the function. These are optional.
- **Function Body**: The actual code the function will execute.

#### Example: Function to Find the Maximum of Two Numbers

```c
/* Function that returns the maximum of two numbers */ 
int max(int num1, int num2) {
	int result;
	
	if (num1 > num2) 
		result = num1; 
	else 
		result = num2; 
		
	return result;
}
```
#### Function Declaration
A **function declaration** (also called a function prototype) tells the compiler about the function's name and parameters before it's used. The actual function code can be defined later.

Example of declaring the `max()` function:

```c
int max(int num1, int num2);
```

You don't have to include parameter names in the declaration, just their types:

```c
int max(int, int);
```

Function declarations are important when you define a function in one file but call it from another.

#### Calling a Function
To use a function, you need to **call** it in your program. When a function is called, the program control moves to the function, executes its statements, and then returns control to the main program.

Example of calling the `max()` function:

```c
#include <stdio.h>

/* function declaration */
int max(int num1, int num2);

int main () {
   int a = 100;
   int b = 200;
   int ret;

   /* calling the function to get max value */
   ret = max(a, b);

   printf("Max value is : %d\n", ret);
   
   return 0;
}
 
/* function returning the maximum of two numbers */
int max(int num1, int num2) {
   int result;

   if (num1 > num2)
      result = num1;
   else
      result = num2;

   return result; 
}

```

#### Function Arguments
Functions can take inputs called **arguments**. These arguments are passed to the function when you call it. There are two ways to pass arguments to a function:

1. **Call by Value**: A copy of the argument's value is passed to the function. Changes made inside the function do not affect the original argument.
    
    ```
    void changeValue(int x) {
	    x = 100;
	}
    ```
    
    In this case, changing `x` inside the function doesn't affect the value of the variable passed.
    
2. **Call by Reference**: Instead of passing a value, you pass the **address** of the argument. This allows the function to modify the original variable.
    
    ```
    void changeValue(int *x) {
	    *x = 100;
	}
	```
    
    Here, the function modifies the value of the original variable by working with its address.
    

By default, C uses **call by value**, which means changes made to function parameters do not affect the original values outside the function.
