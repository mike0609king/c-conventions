# C Conventions 
Those are some rules that I have for how I structure my C-Code. Most
of this should be common sense or conventions that I have seen in 
some projects. Those "conventions" do not only include conventions 
per se. They also include best practices that I think of as important.

It's important to note that C is not C++. You might need to extend or
change some rules to adapt them to C++, because C++ is more complex
and has other additional structures in comparison to C 
(reference standards proposed by Sutter or Holub)

## Naming Conventions
- Macros are all upper case letters and underscores.
- Use i, j, k, l, n and m for local indizes in a while- or for-loop. 
In that particular order.
- Try to avoid using n and m as local indizes if possible, because
your code is screwed if you really have to resort to using n and m.
If you want to use local upper bounds for for- or while-loops use 
n and m.
- Variable prefixes:
    - `g_`: global variables.
    - `flag`: flags.
- Functions start with a verb
- Structures are nouns and end with `_t`. The reason being that you can
then name the variable similar to the structures without confusion.
- Use typedef to declare structs for easier usage.
- Be consistent with shorthand notations and try to reduce them if 
you don't use them often. Specify them in a table.
- Modules should be snake case (like variable names).
- Declare functions that you use outside of a module in the header-file.
- Header end with `.h` and source wiles end with `.c`
- Header of a source file should only differ in the suffix `.h` from
the source. Therefore each source can only have at most one header file.
- The header of a source are only allowed to contain:
    - Constants
    - typedefs
    - data structure specification
    - function declarations
- A header **should not** contain: 
    - dynamic allocation of storage
    - declaration of variables should be strictly avoided 
- Always use a preprocessor guard in the following format:
```
#ifndef FILE_NAME_BIG_LETTERS_H
#define FILE_NAME_BIG_LETTERS_H

// code

#endif /* FILE_NAME_BIG_LETTERS_H */

```
- Naming conflicts in module names should be avoided at all cost. 
The names should be different from those that already exist.
- If you use a main function then you have to include `main` in the
name of the file. You shall not include `main` in the file if the 
file doesn't contain any main-function
- Each source corresponding header should have one functionality:
    - manipulate one data structure that is declared in the header
    - run one algorithm (or a few algorithms that are extremly 
    similar [this should be done after careful consideration])
- Header file general structure guidelines:
    - Headers start with constants
    - Functions that manipulate one datastructure should follow 
    immediately after the declaration of the datastructure
    - Functions and datastructure declarations have to be commented 
    in the header. 
- Source general structure:
    - include statement of the corresponding header if existent
    - include statements
    - typedefs, constants and macros
    - declaration of data types
    - private function prototypes and comment block for their usage
    - functions that are declared in the header
    - functions that are private
- Source files should never include other source files

## Structure
- Try your best not to exceed 100 characters in a line 
- Try not to have too many lines in a function.
- A function should only do one thing
- Opening and closing curly brackets "{" and "}" after control structures 
and functions should always be on a separate line. The reason being that 
it is more readable if your parameterlist or logical expression has multiple 
lines:
```C
void foo(
    int my_first_somewhat_long_variable_name, 
    int my_second_somewhat_long_varialbe_name)
{
    // code
}
```
There are other ways to be able to immediately identify where the code starts 
and this is one of them.
- Only empty code blocks can have curly brackets on the same line as the 
control structure. Therefore the following code should be used for readablility:
```C
while (5 > t.next()) {}
```
- Even use curly brackets for one liners after a control structure:
```C
if (5 == x)
{
    // code
}
```

## Spaces
- tabs are 4 spaces
- No spaces at end of lines
- Use parentheses to make it more clear in which order operations are executed
(you don't need it when using only +,-,\* and / in an operation)
- If you use a subset of +,-,\* and / use spaces to indicate which operation
is intended to be exectued first (`x*y + 3*x`)
- After control statements (e.g. `while`, `switch`, `if`, `else`) you always 
have to put a space: `while (...)`
- All binary operators should have the equal amount of space before and after
If it doesn't make the expression more readable you should use 1 space before 
and after
- Parentheses (`(` and `)`) and brackets (`[` and `]`) shouldn't have a space 
inside e.g. this the following is wrong `int func( int a )`
- `.` and `->` should have no spaces before and after when used as member operators
- When separating items with commas use one space
- When having a multiline statement the statements after the first line should belong
indented in a way that make the statement more readable. You don't have to only use
tabs in order to indent (you may also use spaces if it makes the statement more readable):
```
here_long_variable_name =   long_variable_name
                          + long variable_name2
                          + another_long_variable_name
                            * another_variable
                          + last_variable;
```

### Lines
- Segments that logically belong with each other are separated by one blank line
- Functions that logically belong together should be close to eachother. Those
functions should only be separated by one blank line. Groups of functions should
be separated with two blank lines.
- There is a blank line at the end of a file


## Comments
- Comment your functions in the header file. Template:
```C
/**
 * This is the description of what the function is supposed to do.
 * 
 * @param param1 This is the description of the first parameter.
 * @param param2 This is the description of the second parameter.
 * @return This is a description of the return values.
*/
void
do_something(int param1, int param2, int param3) {
    // something gets done in here
}
```
- If you have functions that you haven't declared in the header 
then you should comment them wherever you declare those functions
- If you assume something of parameters in a functions you also have to 
name it.
- Generally assumtions that are not checked should be commented.
- Comments can also reference documentation. Try not to give specific paths,
because those might change. It is okay to reference the file by name
- Keywords of comments "TODO", "WARNING" (explains risks) and "NOTE" 
(explains why happens). If no comments are give then it's only described
what the code does
- Don't contain preprocessor tokens "/\*", "//" or "\\"
- Pushing commented code is illegal. Preprocessor guards should be used.
- Comment development decisions that you have made. For instance if you
implemented a somewhat ugly workaround for a problem.
- Compare floating point variables with a tolerance value instead of directly
with equal sign.

## Pointers and memory allocation
- If your array has a resonable fixed upper bound for its size. Then
initialize it (define a preprocessor constant for it). This simplifies
approximating the maximum amount of necessary memory that your program
might need to use.
- Initialize allocated memory with 0. Only don't do it if you have a
valid reason not to.
- Don't leave pointers uninitialize. Initialize them with NULL if you 
don't want to initialize it yet.
- 

## Exception handling
- Be aware of invalid operations e.g. dividing by zero accessing NULL 
pointer

## Optimizing
- Use bit fields to save computer memory (there is probably a reason
why you are writing your program in C instead of another language. 
So you should use it's strengths)
- 

## Others
- Constants are always placed on the left side of the comparator 
(e.g. ==, >=,...). In case you have a type the compiler will 
detect it more easily.
- Avoid using assembly if possible. Try to keep number of modules
that you use assembly in.
- Cast return value to `void` if you don't intend to use them. 
`(void)printf(...)`
- Use keywords like `goto` and `continue` only if truly necessary
and always comment them to make clear why you use them.
- Don't use `register` dn `auto`
- Always use `static` if you don't want functions and varialbes to 
be accessed outside of the module
- Always use `const` for:
    - function calls where the value shouldn't be changed 
    - variables that don't change
- Always use `volatile` when: 
    - variable is used by multiple threads:
        - memory mapped I/O peripheral register set
        - global variable used by interrupts
- Use `DEBUG` to define functions that should only be used when in 
debug mode. You should also also use this to comment out code blocks.
Example:
```
#ifdef DEBUG
void deb_function(...)
{
    // meaningful code
}
#else
void deb_function(...) {}
#endif
```
- Avoid using abolute paths as much as reasonably possible!
- If integer size matters use fixed-width integer types. This is also the
reason why you should never use `short` or `long`.
- If individual bits are important e.g. you may use bit-operations on an
integer, then you have to make the integer unsigned.
- NEVER mix signed datatypes with unsigned datatypes. This can cause errors.
- If a verialbe is a boolean, declare or cast it to a boolean.
- Functions are not longer than 100 lines.
- Function exit points should be minimal. Try to keep it at one if possible,
where the exit point is at the bottom of the function.
- Return types in function definitions should be put on a separate line for
readability.
- Use parameterized macros sparingly.
- Don't nest control structures more than three levels. If this is the case
then auxilery functions should be used to make the code more readable.
- Don't declare multiple variables in one line. This makes it easier to change
in the future. The following shouldn't be
allowed:
```
int a, b, c;
```
- When declaring a pointer the asterisk should be close to the variable name:
`int *number;`.
- Avoid embedded assignments if it doesn't affect readability too much,
where `++` and `--` count as assignments.


## Guidelines and principles for reference
- MISRA C: If malfunction can have very serious consequences.
- BARR C guidelines: I used a lot of concepts that are described in here.


## TODO
- read mcinglis/c-style
