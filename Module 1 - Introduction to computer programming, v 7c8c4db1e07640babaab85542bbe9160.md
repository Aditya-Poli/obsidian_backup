# Module 1 - Introduction to computer programming, variables, comments, basic I/O operations, flow control (if)External tool

Class: C++
Created: June 5, 2022 12:05 PM
Reviewed: No
Type: Lecture

# **Your first program**

Now we’re going to show you a very simple (and, at the same time, completely useless) program written in the C++ language. We’re going to use this example to present you some basic rules governing the language. The program itself will be modified many times, as it becomes enriched by various additional elements in expanding our programming knowledge. Ready? All right then, let’s go.

First we need to define our expectations for the program. They’ll be very modest. We want a short text to appear on the screen. Let's assume that the text will state:

```
It's me, your first program.
```

**output**

> That’s all we want at the moment

What further steps should our first program perform? Let's try to enumerate them here:

1. to **start**;
2. to **write** the text on the screen;
3. to **stop**

This type of structured and semi-formal description of each step of the program is called an **algorithm**. Sources of the word algorithm can be traced back to the Arabic language and originated in early medieval times, and for us, this represents the beginning of computer programming.

Now it's time to see our program. It’s on the right side of the screen, in the editor.

It looks a bit mysterious, doesn't it? Let’s check out each line of the program carefully, and uncover its meaning and purpose. The description is not particularly accurate and those of you who know a little C++ already will probably conclude that it’s too simplistic and somewhat childish. We did this on purpose – we’re not building Rome in a day. Not even in a week!

Let's move on.

```cpp
#include <iostream>

using namespace std;

int main()
{
  cout << "It's me, your first program.";
  return 0;
}
```

Pay attention to the character # (hash) at the beginning of the first line. It means that the content of this line is the so-called **preprocessor directive**. We’re going to tell you more about the preprocessor later, but for now we’ll only say that it’s a separate part of the compiler whose task is to pre-read the text of the program and make some modifications in it. The prefix "pre" suggests that these operations are performed before the full processing (compilation) takes place.

The changes the **preprocessor** will introduce are fully controlled by its directives. In our program, we are dealing with the ***include* directive**. When the preprocessor meets that directive, it replaces the directive with the content of the file whose name is listed in the directive (in our case, this is the file named `iostream`). The changes made by the preprocessor never modify the content of your source file in any way. Any alterations are made on a volatile copy of your program that disappears immediately after the compiler finishes its work.

So why do need the preprocessor to include the content of a completely unknown file called iostream? Writing a program is similar to building a construction with ready-made blocks. In our program, we are going to use one such block and it will happen when we want to write something on the screen. That block is called `cout` (you can find it inside our code), but the compiler knows nothing about it so far. In particular, the compiler has no idea that `cout` is a valid name for that block while `cuot` isn't. The compiler must be warned about it – it needs to be aware of the fact.

A set of preliminary information that the compiler needs is included in **header files**. These files contain a collection of preliminary information about ready-made blocks which can be used by a program to write text on the screen, or to read letters from the keyboard. So when our program is going to write something, it will use a block called cout, which is able to do the trick (and much more). We don't want the compiler to be surprised, so we need to warn it about that. The compiler’s developers put a set of this anticipatory information in the iostream file. All we have to do is use the file. This is exactly what we expect from the include directive.

But where is the `iostream` file located? The answer is simple, but not as clear as you might want: that’s not our problem. The preprocessor knows where it is. Good job, preprocessor!

In the C++ language, all elements of the standard C++ infrastructure are declared inside the **namespace** called `std`. A namespace is an abstract container or environment created to hold a logical grouping of unique entities (blocks).

An entity defined in a namespace is associated only with that namespace. If you want to use many of the standard C++ entities (we’re going to tell you all about them later) you must insert the `using namespace` instruction at the top of each file, outside of any function.

The instruction should specify the name of the desired namespace (`std` in our case). This will make the standard facilities available throughout the program.

It's worth to add (although you're not obliged to use the knowledge just know) that you may omit putting `using namespace` in your code but the cost of such omission is non-zero. Now you have to inform the compiler where `cout` block come from and you must do it each time you use any of the entities derived from the `std` namespace. In other words, you need to write:

```cpp
std::cout
```

instead of:

```cpp
cout
```

Judge for yourself if it pays off. The compiler doesn't care what you choose. Anyway, we prefer to use `using namespace` as it makes code clearer and more consistent.

We’ve already said something about the blocks. Now let's go a little deeper. One of the most common types of blocks used to build C++ programs are **functions**.

If you associate a function with mathematics, you’re on the right track. Imagine a function as a black box, where you can insert something into it (though this is not always necessary) and take something new out of it, as if from a magic hat. Things to be put into the box are called **function arguments**. Things to be taken out of the box are called **function results**. In addition, a function can do something else on the side.

If this sounds rather vague, don't worry, we’ll talk about functions many times and in much more detail later.

Back to our program. The standard of the C++ language assumes that among many different blocks that may be put into a program, one specific block must always be present, otherwise the program won't be correct. This block is always a function with the same name: `main`.

Every function in C++ begins with the following set of information:

- what is the result of the function?
- what is the name of the function?
- how many arguments does the function accept and what are their names?

Take a close look at our program and try to read it properly, accepting the fact that you won’t yet fully understand everything.

- the result of the function is an **integer** value (we can read it from the word `int`, which is short for integer)
- the name of the function is main (we know why already)
- the function doesn't require any arguments (what we can deduce from the absence of anything between parentheses).

This set of information is sometimes called a **prototype**, and it’s like a label affixed to a function announcing how you can use that function in your program. The prototype says nothing about what the function is intended to do. It’s written inside the function and the interior of the function is called the **function body**. The function body begins with the first opening bracket `{` and ends with the corresponding closing bracket `}`. It might sound surprising, but the function body can be empty, which means that the function does exactly nothing.

We can even create a function that is lazy – it can be encoded like this:

`void lazy() { }`

The word `void` put in front of function's name (`main`) instructs the compiler that the function provides no result. Indeed, laziness rarely has utilizable results so don't be surprised.

Summing up, this drone produces no result (in other words, result is void), its name is "lazy", it doesn't take any arguments (there is nothing between parentheses) and it does absolutely nothing (there is nothing between brackets).

By the way, the names of the functions are subject to some fairly rigid constraints. More on this later.

**TIME MACHINE:** It's worth to mention that previous versions of C++ preferred to use somewhat different notation to declare the fact that a particular function (including main) doesn't accept any arguments. This is how it looked:
`int main(void) {}`
Note the `void` put inside the parentheses. Such a convention derived from C language where the clause `()` had definitely different meaning. We prefere not to stay in the past so you won't see `void` in this role in our snippets.

Inside the main function body we need to write what our function (and thus the program) is supposed to do. If we look inside, we find a reference to a block named `cout`.

Firstly, note the **semicolon** at the end of the line. Each instruction (more precisely, each **statement**) in C++ must end with a semicolon – without it the program will be incorrect.

This particular statement says: instruct the entity named `cout` to show the following text on the screen (as indicated by the `<<` digraph, which specifies the direction in which the text is sent). You might ask – how do we know that `cout` will do that for us? Well, we know it because it says so in the C++ language standards.

The `cout` entity (in fact, it's an **object**, but we don't want to bring up this word too soon – more on it later) must be fed with something that is intended to be shown on the screen. In our example, the feed is just text (**string**). For simplicity, we can assume that strings in the program in C++ are always enclosed in quotes – that way the compiler recognizes the text that is sent to the user of the program, and the text that is intended to be compiled is translated into machine language. This distinction is very important. Take a look:

```cpp
int main();
```

The line above is the main function **prototype** (i.e. a hint saying what can we expect from a particular function).

```cpp
"int main();"
```

The line above is **not** the main function prototype, but a **string** that only looks like part of a source code. The compiler is not interested in what is between the quotes, and therefore doesn’t recognize such strings as code.

How does it work? We can picture it like this: the execution of our main function is suspended (we can say that the main function falls asleep) and during that time `cout`, together with `<<` (this kind of symbol is named **operator**) prints the text on the screen. When the text is printed, the main function wakes up and continues its activity.

The above form of source code is the most natural and perhaps the most easily read by humans, but you’re still free to write it in a different way. For example:

```cpp
cout
<<
"It's me, your first program."
;
```

In the C++ language it isn’t necessary to write just one statement per line. You can place two (or more) statements on the same line, or split one statement into several lines, but bear in mind that **readability** (for humans) is a very important factor. However, compilers, unlike humans, will never complain about your style.

```cpp
#include <iostream>

using namespace std;

int main()
{
  cout << "It's me, your first program.";
  return 0;
}
```

We’re almost at the end now. There’s only one line left in our program. This is:

`return 0;`

This is another (beside the function invocation) statement of the C++ language. Its name is just `return` and that’s what it does. Used in the function, it causes the end of function execution. If you perform return somewhere inside a function, this function immediately interrupts its execution.

The zero after the word return is a result of your function `main`. It's important - this is how your program tells the operating system the following: *I did what I had to do, nothing prevented me from doing this, and everything is okay.*

If you were to write:

`return 1;`

this would mean that something had gone wrong, it did not allow your program to be performed successfully and the operating system could use that information to react appropriately.

Usually, if a function declares itself as a integer value provider (like our `main` function) it's obliged to contain the `return` statement while the `return` statement is obliged to return an integer value. Expect compilation error if you don't see to it. It seems to be clear, doesn't it? It's not fair to promise a value and to break faith (it's not just about functions).

However, the `main` function is exceptional. It **must** be declared as `int` but doesn't have to return it. Sounds weird? Absolutely! Moreover, if there is no `return` statement inside the `main` function, compiler assumes that `return 0` has been implicitly used. Sounds weirder? Not at all - thank to that you don't have to make additional efforts if you're going to point that execution of your code terminated successfully.

Of course, it's a matter of taste in a measure. We definitely prefer to use `return` in `main`. Your preferences may be different.

So is that all? Yes, that’s it! Let's look again at our program and see what’s happening step by step:

- we introduced the function named main into our program - it will be executed when you start the program;
- we made use of an entity named cout inside the main function - it will print the text on the screen;
- the program finishes immediately after printing, indicating that everything you expected to achieve has been achieved.

So hopefully it wasn’t as difficult as it seemed at first glance. Now let’s try to persuade the computer to compute something for us – after all, that’s what they’re for.

# **Numbers and how computers see them**

Do you know how computers perform calculations on numbers? Maybe you've heard of the **binary system** and know that it’s the system computers use for storing numbers and that they can perform any operation upon them. We’re not going to go the intricacies of positional numeral systems here, but we will say that the numbers handled by modern computers are of two types:

- **integers**, that is, those which are devoid of the fractional part;
- **floating-point** numbers (or simply floats), that contain (or are able to contain) the fractional part.

This definition is quite simplistic, but good enough for our purposes. This distinction is very important and the boundary between these two types of numbers is very strict. Both of these kinds of numbers significantly differ in how they are stored in a computer memory and in the range of acceptable values. Additionally, the characteristic of a number which determines its kind, range and application is called **type**.

So now we know two types of the C++ language – an integer type (known as `int`) and a floating point type (known as `float`).

For now, let's leave the floating-point numbers aside (that’s right: more on them later) and let’s consider a question that’s maybe a bit banal at first glance: how does the C++ language recognize the integers?

Well, it’s almost the same as when you write them on a piece of paper – they’re simply a string of digits that make up a number. But there’s a catch – you can’t include any characters that are not digits inside the number. There is only one exception to the rule: if you think that the number contains so many digits that it becomes ambiguous, you can insert as many single quotes (apostrophes) inside the number. These quotes don't change the number's value and compiler ignores them completely.

**TIME MACHINE**Using single quotes as separators enhancing integer numbers readability have been introduced in **C++17** - don't be surprised if an older compiler rejects such a notation

Take for example the number eleven million one hundred and eleven thousand one hundred and eleven. If you took a pencil in your hand right now, you would probably write the number like this:

11,111,111

or (if you are a Pole or a German) like this:

11.111.111

or even like this:

11 111 111

For sure, this makes it easier to read if the number consists of many digits. However, C++doesn’t like this at all. You have to write this number as follows:

`11111111`

or - if you want your number to be extremely legible - you can write it down as:

`11'111'11`

If you don’t, the compiler will shout at you. And how do you code negative numbers in C++? As usual, by adding a minus. You can write:

-`11111111`

Positive numbers don’t need to be preceded by the plus sign, but you can do it if you want. The following lines describe the same number:

`+123`

`123`

For now we’ll deal only with integers – we’ll introduce floating-point numbers very soon.

There are three additional conventions, unknown to the world of mathematics. The first of them allows us to use the numbers in an **octal representation**. If an integer number is preceded by the 0 digit, it will be treated as an octal value. This means that the number must contain digits taken from the 0 to 7 range only.

`0123`

is an octal number with a (decimal) value equal to **83**.

The second allows us to use hexadecimal numbers. Such number should be preceded by the prefix written as `0x` or `0X`.

`0x123`

is a hexadecimal number with the (decimal) value equal to `291`.

The third allows us to introduce binary numbers which are preceded by the prefix written as `0b` or `0B`.

`0B1111`

is a binary number equal to decimal value `15`.

![https://edube.org/uploads/media/default/0001/01/2ff31fd912c7f6f6c027a7fdde1bd4c67fa4ffe7.png](https://edube.org/uploads/media/default/0001/01/2ff31fd912c7f6f6c027a7fdde1bd4c67fa4ffe7.png)

# **A variable is variable**

So the C++ language allows us to write numbers. It probably won't surprise you that we can do some arithmetic operations with these numbers too: add, subtract, multiply and divide. Contain your excitement – we’ll be doing that soon enough. But it’s quite normal to ask how to store the results of such operations in order to use them in other operations. There are special "containers" for that purpose and these containers are called variables. As the name variables suggests, the content of a container can be varied in (almost) any way.

What does every variable have?

- a **name**;
- a **type**;
- a **value**;

Let's start with the issues connected with a variable’s name. Variables don’t magically appear in our program. We (as developers) decide how many, and which variables, we want to have in our program. We also **give them their names**, almost becoming their godparents. If you want to give a name to the variable, you have to follow some strict rules:

- the name of the variable must be composed of **upper-case or lower-case Latin letters, digits and the character** `_` (*underscore*);
- the name of the variable must **begin with a letter**;
- the **underline character is a letter** (strange but true);
- upper- and lower-case letters are treated as **different** (a little differently than in the real world – Alice and ALICE are the same given names but they are two different variable names, consequently, two different variables);

These same restrictions apply to all entity names used in C++

The standard of the C++ language does not impose restrictions on the length of variable names, but a specific compiler may have a different opinion on this matter. Don't worry; usually the limitation is so high that it’s unlikely you would actually want to use such long variable names (or functions).

![https://edube.org/uploads/media/default/0001/01/7836a6449c4fcf177b34451ce7e22c07dd45af62.png](https://edube.org/uploads/media/default/0001/01/7836a6449c4fcf177b34451ce7e22c07dd45af62.png)

Here are some correct, but not always convenient variable names:

• variable
• i
• t10
• Exchange_Rate
• counter
• DaysToTheEndOfTheWorld
• TheNameOfAVariableWhichIsSoLongThatYouWillNotBeAbleToWriteItWithoutMistakes
• _

The last name may be ridiculous from your perspective, but your compiler thinks it’s just great.

And now some incorrect names:

• 10t (does not begin with a letter)
• Adiós_Señora (contains illegal characters)
• Exchange Rate (contains a space)

You can find more information about C++ naming style and conventions in the [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#nl8-use-a-consistent-naming-style).

The **type** is an **attribute** that uniquely defines which values can be stored inside the variable. We’ve already encountered the integer (`int`) and floating point (`float`) types. The value of a variable is what we have put into it. Of course, you can only enter a value that is compatible with the variable’s type. Only an integer value can be assigned to an integer variable (or in other words, to a variable of type `int`). The compiler will not allow us to enter a floating-point number here.

![https://edube.org/uploads/media/default/0001/01/98fb47339c22d76166a9f2a045f1e65ce3427bf4.png](https://edube.org/uploads/media/default/0001/01/98fb47339c22d76166a9f2a045f1e65ce3427bf4.png)

Let's talk now about two important things – how the variables are created and how to enter a value inside them (or rather – how to give them a value).

The variable exists as a result of a **declaration**. A declaration is a syntactic structure that binds a name provided by the programmer with a specific type offered by the C++ language. The construction of such a declaration (or the declaration syntax) is simple: just use the name of the desired type, then the variable name (or variable names separated by commas if there are more than one). The whole statement ends with a semicolon.

Let's try to declare a variable of type *int* named *counter*. The relevant portion of the program looks like this:

`int counter;`

What is declared by the following fragment of a program?

`int variable_1, account_balance, invoices;`

It declares three variables of type *int* named (respectively) `variable_1`, `account_balance` and `invoices`.

Remember that you are allowed to use **as many variable declarations as you need** to achieve your goal.

And how do we give a value to the newly declared variable? You need to use the so-called **assignment operator**. Although this sounds rather mysterious, the operator has a simple syntax and unambiguous interpretation. The assignment operator looks very familiar – here it is:

`=`

Let's look at some examples:

`counter = 1;`

The above statement says: *assign a value of 1 to a variable named counter* or a bit shorter *assign 1 to counter*.

Some programmers use a different convention and read such a statement as: ***counter becomes 1***.

It's worth to mention now that you're are allowed and even encouraged to place the variable declaration and its first assignment in the same place. Look: a piece of code like this:

```cpp
int variable;
variable = 1;
```

can be compacted into the following form:

```cpp
int variable = 1;
```

Such a solution shows some important advantages. The most valuable is that declaring variable with immediate assigning it with its initial value is less error-prone than performing these two activities in two different places. The code is more legible, programmer's intentions are better recognizable and if you're used to declare and initialize variable in one step you minimize the risk of use an uninitialized variable. This is why we prefer such declarations in our code.

As usual on such occasions, a new word arrives into our vocabulary: the part of the declaration placed on the right side of the `=` sign is called an **initiator**.

The initiator you saw before was a simple value, but you can also use more complex expressions, like the one below.

```cpp
int twosquared = 2 * 2;
```

We’ll be using initiators often. They’re extremely convenient, quite useful and can be applied to virtually all C++ data types.

Another assiagnment example:

`result = 100 + 200;`

In this case, the new value of the variable `result` will be the result of adding 100 to 200, but you probably already guessed that, right?

And now a slightly more difficult example:

`x = x + 1;`

Seeing that, a mathematician would probably protest – no value may be equal to itself plus one. This is a contradiction.

But in the "C" language the sign "=" does not mean is equal to, but **assign a value**.

So how do we read such a record in the program?

*Take the current value of the variable x, add 1 to it and store the result in the variable x*

In effect, the value of variable x was **incremented** by one, which has nothing to do with comparing the variable to any value.

# **Keywords – why they are the keys?**

Take a look at the right side of the screen – you’ll see a list of words that play a very special role in every C++ language program. They are called **keywords** or (more precisely) **reserved keywords**. They are reserved because you **can’t use them as names**: neither for your variables, nor for your functions or any other named entities you want to create. The meaning of the reserved word is predefined and can’t be changed in any way.

**TIME MACHINE**

Don't be surprised by the fact that each C++ version uses different set of keywords. As you probably suspects, the list grows with each new C++ standard. The list you see comes from C++17 and some of the keywords aren't present in earlier releases.

Fortunately, because the C++ compiler is case-sensitive, you can modify any of these words by changing the case of any letter, thus creating a new word, which is not reserved any more.

For example - **you can't do this**:

`int int;`

You can’t have a variable named `int` - it’s prohibited. But **you can do this** instead:

`int Int;`

The compiler will be happy, very happy although it's worth to emphasize that using names similar to keywords may leads to troublesome misunderstandings. Moreover, names starting with capital letters may have very specific meanings and in general, are not recommended for naming creations as simple as int variables. Think twice and judge for yourself whether such a name won't look better:

`int int_value;`

![https://edube.org/uploads/media/default/0001/01/7cc9cc38e2beffa963ece6599148cb07e534e680.png](https://edube.org/uploads/media/default/0001/01/7cc9cc38e2beffa963ece6599148cb07e534e680.png)

# **Comments on the comments**

Now we’re going to make some **comments**. We don't mean comments on either your achievements or our achievements, although we’re sure you have many achievements to be proud of. We’re referring to other comments, namely comments on the program and inside the program at the same time.

The developer may want to add a few words addressed not to the compiler but to humans, usually to **explain** to other readers of the code how the tricks used in the code work, or the means of variables and functions, and possibly, to store information on who the author is and when the program was written.

Good and responsible developers describe each newly created important entity; in particular, explaining the role of the parameters and the values modified or returned as results, as well as explaining what the code actually does.

How do we leave something like this in the source code? We have to do it in a way that won't force the compiler to interpret it as part of the code. The remark inserted into the program, which is omitted at the time of compiling, is called a *comment*.

If we want to be precise, we should say that **each comment is lexically equivalent to one space**. Whenever the compiler encounters a comment in your program, the comment is completely transparent to it - from its point of view this is only one space (regardless of how long the real comment is).

The C++ language supports two ways of inserting comments:

`// comment` - **single-line** comments

and

`/* comment */` - **block** comments (also knows as **C-style** comments due to fact that they are in use since the very beginning of the C programming language, the C++ progenitor).

A **single-line comment** discards everything from where the pair of slash signs (`//`) is found up to the end of that same line.

In the C++ language a **block comment** is a text that begins with a pair of the following characters:

`/*`

and ends with a pair of the following characters:

`*/`

The comment can span several lines or can occupy only one line or part of a line.

Here you can see an example in which everything from the pair of slash signs on is ignored by the compiler. The single-line comment can start anywhere on the line. This could be a blank line too, with no content at all.

`int counter; // counts the number of sheep in the meadow`

Look at the snippet below. Here you can see an example of a similar comment, but introduced into the code using the second method.

Any new developer reading the program will be aware of the true meaning of the variable. The developer will read the code faster and it’ll take less time to understand it.

`/* the counter variable counts the number of sheep in the meadow */`

`int counter;`

Developers often place a note at the beginning of the source informing when they write the program stating who amended it and why. The note may appear like this:

```cpp
/* ************************************************************
Counting sheep version 1.0
Author: Ronald Sleepyhead, 2012
email: rs@insomnia.org
Changes:
2012-09-13: Ginny Drowsy: counting black sheep improved
************************************************************ */
```

Note that, despite the complicated structure and the multitude of stars, the condition stating how the comment should be started and finished is fully met.

Comments may be **useful** in another respect - you can use them **to mark a piece of code that you currently don’t need** for whatever reason. We often do this during the testing of the program in order to isolate the place where an error could be hidden.

We’ve just got one more thing to say about comments. Compilers differ in assessing whether another comment may be placed within a single comment. Consider the following program:

`/* int i; /* int j; */ int k; */`

The question is: are you allowed to nest one block comment (like `/* int j; */`) inside another block comment?

The answer is no. Such a notation may not be accepted by a particular compiler and in effect makes our code prone to compiler's whims - we don't want to rely on uncertain assumptions.

We strongly discourage you from use such a construction in your code even if your compiler seems to be indifferent to it.

# **Floating-point numbers**

A word (or 2.0 words) about floating-point numbers in real life and in the C++ language.

Previously, we became acquainted with the concept of **data type**, and learned that one of the basic types known in the C++ language is the integer type named int. Now it's the time to talk about another type, designed to represent and store the numbers that (as a mathematician would say) have a **non-empty decimal fraction**.

These are the numbers that have (or may have) a fractional part after the decimal point, and although this is a very simplistic definition, it is sufficient for our purposes. Whenever we use a term like "two and a half" or "zero point four" we think of numbers which the computer considers to be **floating numbers**.

![https://edube.org/uploads/media/default/0001/01/79481498ef6e4edfbaba7a030dc5a7545a9c1ef0.png](https://edube.org/uploads/media/default/0001/01/79481498ef6e4edfbaba7a030dc5a7545a9c1ef0.png)

Let's go back to the values we quoted a moment ago. "Two and a half" looks normal when you write it in a program, although if your native language uses a comma instead of a point in the number, you should **make sure that your number contains points and not commas**. The compiler will either not accept it or (in very rare circumstances) will misunderstand your intentions, as the comma itself has its own reserved meaning in the C++ language.

If you want to use a value of just "two and a half", you should write it as shown here:

`2.5`

Note once again – there is a point between "2" and "5" - not a comma.

As you can probably imagine, you can write the value of "zero point four" in C++ as:

`.4`

Don’t forget this simple rule – you can **omit zero** when it’s the only digit in front of or after the decimal point. In essence you can write the value `0.4` like on the right.

For example: the value of `4.0` could be written as 4. without changing its type or value.

Note: the decimal point is essential to recognize floating-point numbers in C++. Look at these two numbers:

`4`

`4.0`

You might think that they’re exactly the same, but the C++ compiler sees them completely differently:

`4` is an *int*.

`4.0` is a *float*.

We can say that **the point makes a float**. Don't forget that.

![https://edube.org/uploads/media/default/0001/01/82844052d4ba0de98785dc8d3b51e58c164065ed.png](https://edube.org/uploads/media/default/0001/01/82844052d4ba0de98785dc8d3b51e58c164065ed.png)

When you want to use any numbers that are very large or very small, you can use so-called **scientific notation**. Take, for example, the speed of light expressed in meters per second. Written directly it would look like:

`300000000.`

As you probably suspect, you're also allowed to write the value in a more legible form:

`300'000'000.`

as the single quotes can be used inside floats either.

![https://edube.org/uploads/media/default/0001/01/0b75053dfe66b376fa599e3e7d122e02d4cf9eeb.png](https://edube.org/uploads/media/default/0001/01/0b75053dfe66b376fa599e3e7d122e02d4cf9eeb.png)

To avoid the tedious job of writing of so many zeros, physics textbooks use an abbreviated form, which you’ve probably seen already:

$3 • 10^8$

It reads: "*three times ten to the power of eight*"

In the C++ language, the same effect is achieved in a slightly different form – take a look:

`3E8`

The letter *E* (you can also use the lower case letter *e* – it comes from the word exponent) is a concise version of the phrase "*times ten to the power of*".

Note:                                                                                                                                                   

- the exponent (the value after the "*E*") **has to be** an integer.
- the base (the value in front of the "*E*") **may or may not be** an integer; in other words, not only dot makes float - *E* (even alone) can do it too.

Let's see how we use this convention to record numbers that are very small (in the sense of their absolute value, which is close to zero). A physical constant called *Planck's constant* (and denoted as *h*) has, according to the textbooks, the value of:

$$
{\displaystyle {{6.62607} {*} {10}^{-34}}}
$$

If you would like to use it in a program, you would write it this way:

`6.62607E-34`

And that’s it. Not so hard, right?

![https://edube.org/uploads/media/default/0001/01/8b8012b9cbed9f03de07d5da90d4ff9f82c94cf8.png](https://edube.org/uploads/media/default/0001/01/8b8012b9cbed9f03de07d5da90d4ff9f82c94cf8.png)

Let's go back to the floating-point values. We already know what a variable is, and we also know how to declare an integer variable, so now it’s time to declare variables of a floating-point type.

We do this using the keyword `float`. Knowing that we can declare two floating-point variables, named `PI` (we can't name it `Π` because - as you already know - the C++ language freaks out when variable names are written with Greek letters) and `Field`:

`float PI, Field;`

As you can see, the difference in declaring the integer and float variables is quite small from the syntax's point of view.

This difference in terms of semantics is significant, as you can see in the example below. With a little thought, we can figure out that the symbol (more precisely - the **operator**) that performs the mathematical **division** is a single character **/** (slash). Take a look at the code:

```cpp
int i = 10 / 4;
float x = 10.0 / 4.0;
```

It might be a bit surprising for you to know that the value that will be entered in the variable `i` is `2` (yes - just `2`!) while the variable `x` will be equal to `2.5`. Look at the example carefully, because it illustrates a very important difference between these two data types.

What happens when we have to convert integer values into float values or vice versa? We can always transform from `int` into `float`, but it can lead to a **loss of accuracy**. Consider the example below:

```cpp
int i = 100;
float f = i;
```

After changing from `int` to `float`, the value of the variable `f` is `100.0`, because the value of type `int` (`100`) is automatically converted into a `float` (`100.0`).

The transformation affects the internal (machine) representation of those values as **computers use different methods for storing floats and ints in their memory**.

Let's consider the opposite situation now.

As you’ve probably guessed, these substitutions will result in a loss of accuracy - the value of the variable `i` will be `100`. Twenty-five hundredths has no meaning in the ints world. Furthermore, **converting a `float` into an `int` is not always feasible**.

`float f = 100.25;`

`int i = f;`

Integer variables (like *floats*) have a limited capacity. They cannot contain arbitrarily large (or arbitrarily small) numbers.

For example, if a certain type of computer uses four bytes (i.e. 32 bits) to store integer values, you can only use the numbers from the range of *-2147483648* to *2147483647*.

Let's consider the following snippet:

`float f = 1E10;`

`int i = f;`

The `i` variable is unable to store such a large value, but it isn’t clear what will happen during the assignment. Certainly a **loss of accuracy** will occur, but the value assigned to the variable `i` is not known in advance.

In some systems it may be the maximum permissible `int` value, while in others an error occurs, and in others still the value assigned can be completely random.

This is what we call an **implementation dependent issue**. It's the second (and uglier) face of software portability.

# **Operators**

An **operator** is a symbol of the programming language, which is able to operate on the values. For example, **an assignment operator** is the `=` sign. We already know that it can assign values to variables.

Now let’s look at some other operators available in the C++ language and find out which rules govern their use and how to interpret the operations they perform. Let’s begin with the operators associated with widely recognizable arithmetic operations. The order of their appearance is not accidental. We’ll talk more about this afterward.

![https://edube.org/uploads/media/default/0001/01/f195e1808a0995193105e9faf466d6278733ef39.png](https://edube.org/uploads/media/default/0001/01/f195e1808a0995193105e9faf466d6278733ef39.png)

# **Multiplication**

An asterisk `*` is **a multiplication operator**. If you take a look at the code here, you’ll see that the variable `k` will be set to the value of `120`, while the `z` variable will be set to `0.625`.

```cpp
int i = 10, j = 12;
float x = 1.25, y = 0.5;

int k = i * j;
float z = x * y;
```

# **Division**

A slash ("`/`") is a **divisional** operator. The value in front of the slash is a **dividend**, the value behind the slash, a **divisor**. Look at the snippet of the program below: of course, `k` will be set to `2`, `z` to `0.5`.

```cpp
int i = 10, j = 5;
float x = 1.0, y = 2.0;
int k = i / j;
float z = x / y;
```

![https://edube.org/uploads/media/default/0001/01/5039ce826db71ec5ec0b07a8fa70cfd512ef84bf.png](https://edube.org/uploads/media/default/0001/01/5039ce826db71ec5ec0b07a8fa70cfd512ef84bf.png)

# **Division by zero**

As you’ve probably guessed, dividing by zero is strictly **forbidden**, but the penalty for violating that rule will come to you at different times.

```cpp
float x = 1.0 / 0.0;
```

If you dare to write something like that, the compiler will go nuts – you’ll get a compilation error, runtime error or some message at runtime, possibly also a few choice words about your programming capabilities. OK, the last one was a joke. Still, in some cases you won't be able to run your program. As a general rule, you shouldn't divide by zero.

In the following example the compiler won't tell you a thing, but when you try to execute that code, the result of the operation may be surprising. It’s not a number. It’s a special featured value named `inf` (as in **infinitive**). Generally, this kind of illegal operation is a so-called **exception**.

```cpp
float x = 0.0;
float y = 1.0 / x;
```

When you find exceptions in your program, you should react accordingly. We’ll discuss this later.

# **Addition**

The **addition** operator is the "`+`" (plus) sign, which most of us already know from maths class. Again, take a look at the snippet of the program – as you can surmise, `k` is equal to `102` and `z` to `1.02`.

```cpp
int i = 100, j = 2;
float x = 1.0, y = 0.02;
int k = i + j;
float z = x + y;
```

# **Substraction**

The **subtraction** operator is obviously the "`-`" (minus) sign, although you should note that this operator also has another meaning – it can change the sign of a number. This is a good time to show you a very important distinction between **unary** and **binary** operators (in the C++ language there is also **a ternary operator** – more on that a bit later).

As usual, let’s get acquainted with a snippet of the program – you can guess that `k` will be equal to `-100`, while `z` will be equal to `0.0`.

```cpp
int i = 100, j = 200;
float x = 1.0, y = 1.0;
int k = i - j;
float z = x - y;
```

# **Unary minus**

In "subtracting" applications, the minus operator expects two arguments: the left (a **minuend** in arithmetic terms) and the right (a **subtrahend**). For this reason, the subtraction operator is considered one of the binary operators, just like the addition, multiplication and division operators. But the minus operator may be used in a different way – take a look at the snippet.

```cpp
int i = -100;
int j = -i;
```

As you’ve probably guessed, the variable `j` will be assigned the value of `100`. We used the minus operator as a **unary** operator, as it expects only one argument – the right one.

# **Unary plus**

The same dual nature is expressed by the "`+`" operator, which can be also used as a unary operator – its role is to **preserve** the sign. Take a look at the snippet.

```cpp
int i = 100;
int j = +i;
```

Although such a construction is **syntactically correct**, using it doesn’t make much sense and it would be hard to find a good rationale for doing so.

# **Remainder**

The **remainder** operator is quite peculiar, because it has no equivalent among traditional arithmetic operators.

Its graphical representation in the C++ language is the `%` (percent) character, which may look a bit confusing, although you have to admit that its appearance resembles the `/` operator which is responsible for the division while finding the remainder forces the computer to perform a division.

`%` a binary operator (it performs the **modulo operation**) and both arguments cannot be floats (don't forget that!). Look at the example:

`int i = 13;`

`int j = 5;`

`int k = i % j;`

The `k` variable is set to the value of `3` (because *2 * 5 + 3 = 13*).

Oh, and one more thing you need to remember: **you cannot compute the remainder with the right argument equal to zero**. Can you guess why? Click *Check* below to see if you were right:

`**Check**`

You probably remember what we said earlier about dividing by zero. And because division by `0` invokes undefined behaviour, the modulo operation, which relies on division, is undefined, too.Well, that’s what the C++ Standard says. We have to accept that.

![https://edube.org/uploads/media/default/0001/01/01868e454b2f25a38ec783d0474d787c231ae5c1.png](https://edube.org/uploads/media/default/0001/01/01868e454b2f25a38ec783d0474d787c231ae5c1.png)

# **Priorities**

So far, we’ve treated each operator as if it had no connection with the others. Of course, in real programming, nothing is ever as simple as that. Also, we very often find more than one operator in an **expression** and then things can get complicated very quickly. Consider the following expression:

`2 + 3 * 5`

If your memory hasn't failed you, you should remember from school that multiplications precede additions. You probably remember that you have to multiply `3` by `5`, keep the `15` in your memory, add it to `2`, thus getting the result of `17`.

The phenomenon that causes some operators to act before others is known as the **hierarchy of priorities**. The C++ language precisely defines the priorities of all operators and assumes that **operators of larger (higher) priority perform their operations before the operators with lower priority**.

So if we know that `*` has a higher priority than `+`, we can figure out how the final result will be computed.

# **Bindings**

The **binding** of the operator determines the order of computations performed by some operators with equal priority, put side by side in one expression. Most operators in the C++ language have the **left-sided binding**, which means that the calculation of this sample expression is conducted from left to right, i.e. `3` will be added to `2`, and `5` will be added to the result.

`2 + 3 + 5`

Now at this point you might be snorting and saying that all children know perfectly well that addition is commutative and it doesn’t matter in which order the additions are performed. And yes, you're right, but not quite. Additions performed by the computer are not always commutative. Really. We’ll show you this in more detail later. But for now, be patient and trust us.

# **Priorities**

Since you're new to C++ language operators, presenting a complete list of operators' priorities may not be a good idea. Instead, we’ll show you its truncated form, and we’ll expand on it consistently during the introduction of new operators.

This table now looks as follows:

[Untitled](Module%201%20-%20Introduction%20to%20computer%20programming,%20v%207c8c4db1e07640babaab85542bbe9160/Untitled%20Database%20e4452a5fced445e1a3e5d33651aaba02.csv)

Note: we’ve gone through the operators in order **from the highest to the lowest priority**.

We want to check if you understand the concept of binding. Try to work through the following expression:

`2 * 3 % 5`

Both operators (`*` and `%`) have the same priority, so the result could be guessed only when you know the binding direction.

Do you know the result? Click *Check* below to see if you were right:

`**Check**`

`1`

**Yes, the result is 1. Congratulations!**

# **Parentheses**

Of course, we’re always allowed to use **parentheses**, which can change the natural order of calculation. Just like with arithmetic rules, **subexpressions in parentheses are always calculated first**. You can use as many parentheses as you need and we often use them to improve the readability of an expression, even if they don't change the order of operations.

An example expression involving multiple parentheses is given below. Try to compute the value given to the `l` variable.

```cpp
int i = 100;
int j = 25;
int k = 13;
int l = (5 * ((j % k) + i) / (2 * k)) / 2;
```

Click *Check* below to see if you were right:

`**Check**`

`10`

**Yes, it's 10.**

# **Operators continued**

![https://edube.org/uploads/media/default/0001/01/0c2fc9d32ded951d260bd05e81699656fd81ea4a.png](https://edube.org/uploads/media/default/0001/01/0c2fc9d32ded951d260bd05e81699656fd81ea4a.png)

Here are some operators in the C++ language which you won’t find in maths textbooks. Some of them are frequently used **to increment a variable by one**. This is often done when we’re counting something (e.g. sheep). Let's consider the following snippet:

`int sheep_counter = 0;`

Every time a sheep runs through our thoughts we want the variable to be incremented, like this:

`sheep_counter = sheep_counter + 1;`

Similar operations appear very frequently in typical programs, so the creators of the C++ language introduced a set of special operators for these actions. One of them is the `++` (plus plus) operator. You can achieve the same effect in a shorter way:

`sheep_counter++;`

It looks much more elegant now, doesn't it?

Similarly, you can also decrease the value of a chosen variable. For example, if we can hardly wait for our holiday, our mind does the following operation every morning:

`days_until_holiday = days_until_holiday - 1;`

We can write it in a more compact way:

`days_until_holiday--;`

![https://edube.org/uploads/media/default/0001/01/e9f989a475364d7bf83c467e5abb23333e734e79.png](https://edube.org/uploads/media/default/0001/01/e9f989a475364d7bf83c467e5abb23333e734e79.png)

Sorry, but now we have to introduce a few new words.

The "`++`" is called the **increment operator**.

The "`--`" is called the **decrement operator**.

We’ve shown you the `++` and `--` operators after a variable (a specialist in the syntax of programming languages would say that they’re used as postfix operators). However, both operators can be placed in front of a variable as well (as prefix operators), like this:

`++sheep_counter;`

`--days_until_holiday;`

The effect will be exactly the same: `sheep_counter` will be increased by 1, `days_until_holiday` decremented by 1. There’s a fairly significant difference, however, which is described by the precise names of these operators.

Here they are.

That may seem a little weird to you, but it’ll only take a short time to understand. Let's discuss the effects of these operators.

**Operation:**

`++variable`

`--variable`

**Effect:**

Increment/decrement the variable by 1 and return its value **already** increased/reduced.

**Operation:**

`variable++`

`variable--`

**Effect:**

Return the original (unchanged) variable's value and then increment/decrement the variable by 1.

This behavior justifies the presence of the prefix *pre-* (before) and *post-* (after) in the operators’ names: *pre-* because the variable is modified **first** and then its value is **used**; *post-* because the variable's value is **used** and then **modified**.

# **Pre-and post-operators and their priorities**

Take a look at two simple examples.

`int i = 1;`

`int j = i++;`

First, the variable `i` is set to `1`. In the second statement, we’ll see the following steps:

- the value of `i` will be taken (as we use the *post-incrementation*);
- the variable `i` will be increased by `1`.

In effect, `j` will receive the value of `1` and `i` the value of `2`.

Things go a bit differently here.

`int i = 1;`

`int j = ++i;`

The variable `i` is assigned with the value of `1`; next, the `i` variable is incremented and is equal to `2`; next, the increased value is assigned to the `j` variable.

In effect, both `i` and `j` will be equal to `2`.

Look carefully at this program. Let’s trace its execution step by step.

```cpp
int i = 4;
int j = 2 * i++;
i = 2 * --j;
```

1. The `i` variable is assigned the value of `4`;
2. We take the original value of `i` (`4`), multiply it by `2`, assign the result (`8`) to `j` and eventually (post-)increment the `i` variable (it equals `5` now);
3. We (pre-)decrement the value of `j` (it equals `7` now); this reduced value is taken and multiplied by `2` and the result (`14`) is assigned to the variable `i`.

What else do you need to know about the new operators? Firstly, their priority is quite high – higher than the `*`, `/` and `%` operators. Secondly, their binding depends on whether you use the prefix or postfix version. The prefix version operators have a right-to-left binding, while the postfix operators bind from left to right.

Our priority table now reads as follows:

[Untitled](Module%201%20-%20Introduction%20to%20computer%20programming,%20v%207c8c4db1e07640babaab85542bbe9160/Untitled%20Database%20e7a9d0b9e1474118abda58acb618aa84.csv)

# **Shortcut operators**

Now it's time for the next set of operators, ones that make a developer's life easier. The one’s we’ve already described deal with addition and subtraction of one.

`i = i * 2;`

However, we often need something other than addition or subtraction, or we want to use a different value; we can use this operator when we want to calculate a series of successive values of powers of 2.

Here’s another example. We use this expression when our herd is extremely numerous:

`sheep_counter = sheep_counter + 10;`

In the C++ language there is a short way to write these operations. You can write them as follows:

`i *= 2;`

`sheep_counter += 10;`

Let's try to present a general description for such operations. If `op` is a **two-argument operator** (this is a very important condition!) and the operator is used in the following context:

`variable = variable op expression;`

then this expression can be **simplified** as follows:

`variable op= expression;`

Take a look at the examples here:

![https://edube.org/uploads/media/default/0001/01/7109fef0443a377df09803a5475917c00f5ef06c.png](https://edube.org/uploads/media/default/0001/01/7109fef0443a377df09803a5475917c00f5ef06c.png)

Make sure you understand them all. And relax, because we still have a lot of work ahead.

# **Character type**

So far we have treated the C++ language (and the computer itself) as a tool for performing calculations on numbers. This is consistent with a common belief that a computer is just a calculator, albeit a very smart one. You know it’s not true, as the computer can be easily used for word processing, too.

![https://edube.org/uploads/media/default/0001/01/06233f7f9d116332ba067d8807098d871f73b3f3.png](https://edube.org/uploads/media/default/0001/01/06233f7f9d116332ba067d8807098d871f73b3f3.png)

We can define a *word* as a string of characters (letters, numbers, punctuation marks, etc.). We dealt with such strings in the first lesson when we used `cout` to write some text on the computer screen.

Now, however, we’ll ignore the string consisting of multiple characters and we’ll focus our attention on single characters. We’ll come back to the problem of processing strings when we start working on arrays, because in the C++ language strings behave in a very similar way.

To store and manipulate characters, the C++ language provides a special type of data. This type is called `char`, which is an abbreviation of the word *character* and according to [Bjarne Stroustrup's hint](http://www.stroustrup.com/bs_faq2.html#char) should be pronounced as *"tchar"*, not *"kar"*.

Let's try to declare a variable for storing a single character.

`char character;`

Looks familiar, doesn't it? Now let's talk a bit about how computers store characters.

# **ASCII code**

![https://edube.org/uploads/media/default/0001/01/9d33281420838c9978dd47e3e875efe906ad2fe5.png](https://edube.org/uploads/media/default/0001/01/9d33281420838c9978dd47e3e875efe906ad2fe5.png)

**Computers store characters as numbers**. Every character used by a computer corresponds to a unique number, and vice versa. This system of assignments includes more characters than you would probably expect. Many of them are invisible to humans but essential for computers. Some of these characters are called **white spaces**, while others are named **control characters**, because their purpose is to **control** the input/output devices. An example of a white space that is completely invisible to the naked eye is a special code, or a pair of codes (different operating systems may treat this issue differently), which are used to mark the ends of lines inside text files. People don’t see this sign (or these signs), but they can see their effect where the lines are broken.

We can create virtually any number of assignments, but a world in which each computer type uses different character encoding would be extremely inconvenient. This has created a need to introduce a universal and widely accepted standard implemented by (almost) all computers and operating systems all over the world. **ASCII** (which is a short for *American Standard Code for Information Interchange* and is usually probounced as *"ASS-kee"*) is the most widely used system in the world, and it’s safe to assume that nearly all modern devices (like computers, printers, mobile phones, tablets, etc.) use this code. The code provides space for 256 different characters, but we’re only interested in the first 128. If you want to see how the code is constructed, go to the table on the right.

Look at it carefully – there are some interesting facts about it that you might notice. We'll show you one. Do you see what the code of the most common character is – the space? Yes – it’s 32. Now look at what the code of the lower-case letter “a” is. It’s 97, right? And now let's find the upper-case “A”. Its code is 65. What’s the difference between the code of “a” and “A”? It’s 32. Yes, that's the code of a space. We’ll use that interesting feature of the ASCII code soon.

Also, note that the letters are arranged in **the same order** as in the **Latin alphabet**.

By the way, ASCII code is being superseded (or rather extended) by a new international standard named UNICODE.

Fortunately, the ASCII set is a [UNICODE](https://en.wikipedia.org/wiki/Unicode) subset. UNICODE is able to represent virtually all characters used throughout the world. We’ll spend a little more time on this later.

![Untitled](Module%201%20-%20Introduction%20to%20computer%20programming,%20v%207c8c4db1e07640babaab85542bbe9160/Untitled.png)

![Untitled](Module%201%20-%20Introduction%20to%20computer%20programming,%20v%207c8c4db1e07640babaab85542bbe9160/Untitled%201.png)

![Untitled](Module%201%20-%20Introduction%20to%20computer%20programming,%20v%207c8c4db1e07640babaab85542bbe9160/Untitled%202.png)

# **Character type values**

How do we use the values of the `char` type in the C++ language? We can do it in two ways, which are not entirely equivalent.

The first way allows us to specify the character itself, but **enclosed in single quotes** (apostrophes). Let’s assume that we want the variable we declared a few slides earlier to be assigned the value of the upper-case letter `A`.

We do this as follows:

`character = 'A';`

You’re not allowed to omit apostrophes under any circumstances.

Now let’s assign an asterisk to our variable. We do this as follows:

`character = '*';`

The second method consists of assigning a **non-negative integer value** that is the code of the desired character. This means that the assignment below will put an “`A`” into the character variable.

`character = 65;`

The second solution, however, is less recommended and if you can avoid it, you should. Why?

First, because it is illegible. Without knowing the ASCII code, it is impossible to guess what that “65” really means. Perhaps this is the code for a character, but it can also happen that a sociopathic programmer used this devious way to save the number of already counted sheep.

The second reason is more exotic, but still true. There’s a significant number of computers in the world which use codes **other than ASCII**. For example, many of the IBM mainframes use a code commonly called [EBCDIC](https://en.wikipedia.org/wiki/EBCDIC) (*Extended Binary Coded Decimal Interchange Code* - we won't dare to instruct you how to pronounce this abbreviation, sorry) which is very different from ASCII and is based on radically different concepts.

![https://edube.org/uploads/media/default/0001/01/eac3daa523af9441a81b6de96ef2146f9db4958f.png](https://edube.org/uploads/media/default/0001/01/eac3daa523af9441a81b6de96ef2146f9db4958f.png)

# **ASCII vs EBCDIC**

Now imagine that you’ve written a wonderful program and decided to compile and run it on a computer utilizing the EBCDIC code. If you wrote something like this, the compiler running on that computer would notice the question mark and use the appropriate EBCDIC code for that character.

`character = '?';`

But if you wrote it like this:

`character = 63;`

# **Literal**

Now’s probably a good time to bring a new term into the mix: a **literal**. The literal is a symbol which **uniquely identifies its value**. Some prefer to use a different definition: the **literal means itself**. Choose the definition that you consider to be clearer and look at the following simple examples:

- `character`: this is not a literal; it’s probably a variable name; when you look at it, you cannot guess what value is currently assigned to that variable;
- `'A'`: this is a literal; when you look at it you can immediately guess its value; you even know that it’s a literal of the `char` type;
- `100`: this is a literal, too (of the `int` type);
- `100.0`: this is another literal, this time of a floating point type;
- `i + 100`: this is a combination of a variable and a literal joined together with the `+` operator; this structure is called an **expression.**

If you’re an inquisitive person, you probably want to ask a question: if a literal of type `char` is given as the character enclosed in apostrophes, how do we code the apostrophe itself?

The C++ language uses a special convention that also extends to other characters, not only to apostrophes. Let's start with an apostrophe anyway. An apostrophe looks like this:

`character = '\'';`

The `\` character (called *backslash*) acts as an **escape character**, because by using the `\` we can escape from the normal meaning of the character that follows the slash. In this example, we **escape** from the usual role of the apostrophe (i.e. delimiting the literals of type `char`).

You can also use the escape character to **escape from the escape character**. Yes, it does sound weird, but the example below should make it clear. This is how we put a backslash into a variable of type `char`.

`character = '\\';`

# **Escape characters**

The C++ language allows us to escape in other circumstances too. Let's start with those that denote literals representing white spaces.

`\n` – denotes a **transition to a new line** and is sometimes called an **LF** (**Line Feed**), as printers react to this character by pulling out the paper by one line of text.

`\r` – denotes the **return to the beginning of the line** and is sometimes called a **CR** (**Carriage Return** – “carriage” was the synonym of a “print head” in the typewriter era); printers respond to this character as if they are told to re-start printing from the left margin of the already printed line.

`\a` – (as in **alarm**) - is a relic of the past when teletypes were often used to communicate with computers (do you know what a [teletype](https://en.wikipedia.org/wiki/Teleprinter) is, are you old enough to remember them?); sending this character to a teletype turns on its ringer; hence, the character is officially called **BEL** (as in **bell**); interestingly, if you try to send the character to the screen, you’ll hear a sound – it won't be a real ringing but rather a short beep. The power of tradition works even in the IT world.

`\0` (*note: the character after the backslash is a zero, not the letter O*): called **nul** (from the Latin word **nullus** – none) is a character that **does not represent any character**; despite first impressions, it could be very useful, as we’ll show you in the lessons to come.

Now we’ll try to escape in a slightly different direction. The first example explains the variant when a backslash is followed by two or three **octal digits** (the digits from the range of 0 to 7). A number coded in this manner will be treated as an **ASCII value**. It may look like this:

`character = '\47';`

`047` octal is `39` decimal. Look at the ASCII code table and you'll find that this is the ASCII code of an apostrophe, so this is equivalent to the notation

`'\''`

(but only for computers implementing the ASCII code).

The second escape refers to the situation when a `\` is followed by the letter `X` (lower case or upper case – it doesn't matter). In this case there must be either one or two **hexadecimal digits**, which will be treated as ASCII code. Here's an example:

`character = '\x27';`

As you’ve probably guessed, `27` hexadecimal is `39` decimal.

![https://edube.org/uploads/media/default/0001/01/43f13e6c72898518ca337e623edadd16c1e9dcb6.png](https://edube.org/uploads/media/default/0001/01/43f13e6c72898518ca337e623edadd16c1e9dcb6.png)

# **char values are int values**

There’s an assumption in the C++ language that may seem surprising at first glance: the `char` type is treated as a special kind of `int` type. This means that:

- You can always **assign a `char` value** to an `int` variable;
- You can always assign an `int` value to a `char` variable, but if the value exceeds 255 (the top-most character code in ASCII), you must expect a loss of value;
- The value of the `char` type can be subject to the **same operators** as the data of type `int`.

We can check this using a simple example. We said earlier that in ASCII, the "distance" between upper and lower case letters is 32, and that 32 is the code of the space character. Look at this snippet:

```cpp
char character = 'A';
character += 32;
character -= ' ';
```

This sequence of subsequent addition and subtraction will bring the `character` value to its original value ("`A`"). You should be able to explain why, right?

All of these assignments are correct. Try to interpret their meanings – this should be a good exercise for you.

```cpp
char character = 'A' + 32;
character = 'A' + ' ' ;
character = 65 + ' ';
character = 97 - ' ';
character = 'a' - 32;
character = 'a' - ' ';
```

Check the answer

`97, 97, 97, 65, 65, 65`

**Well done! Here are the answers: 97, 97, 97, 65, 65, 65.**

![https://edube.org/uploads/media/default/0001/01/b3e12d56578c42f17fff54b89c9c67d19be8fb46.png](https://edube.org/uploads/media/default/0001/01/b3e12d56578c42f17fff54b89c9c67d19be8fb46.png)

# **One who asks does not err**

A programmer writes a program and the program **asks questions**. A computer executes the program and provides the answers. The program must be able to react according to the answers it receives. Fortunately, computers know only two kinds of answer: ***yes, this is true*** or ***no, this is false.*** You will never get a response like “I don’t know” or “Probably yes, but I don’t know for sure”.

To ask questions, the C++ language uses a set of very special operators. Let’s go through them one by one, illustrating their effects using some simple examples.

![https://edube.org/uploads/media/default/0001/01/190efb27cab87423779d415ae7f884c1c09abe54.png](https://edube.org/uploads/media/default/0001/01/190efb27cab87423779d415ae7f884c1c09abe54.png)

# **Question: is x equal to y?**

Question: are two values equal?

To ask this question you use the `==` (***equal equal***) operator.

Don't forget this important distinction:

- `=` is an **assignment operator**
- `==` is the **question “*are these values equal?”***

It’s **a binary operator with a left-side binding**. It needs two arguments and **checks if they’re equal**. Now let’s ask a few questions. Try to guess the answers.

# **Is x equal to y?**

1. `2 == 2`

Check

This question is simple. Of course `2` is equal to `2`. The computer will answer `true`.

2. `1 == 2`

Check

This one’s simple, too. The answer will be `false`.

3. `i == 0`

`**Check**`

Here we’re not able to find the answer if we do not know what value is currently stored in variable `i`. **If the variable has been changed many times during the execution of your program, the answer to this question can be given only by the computer and only at run time.**

# **Question: is x equal to y?**

There’s another developer who counts white and black sheep separately and falls asleep only when there are exactly twice as many black sheep as white ones. The question will be as follows:

`black_sheep_counter == 2 * white_sheep_counter`

Due to the low priority of the `==` operator, this question shall be treated as equivalent to this one:

`black_sheep_counter == (2 * white_sheep_counter)`

# **Question: is x not equal to y?**

To ask this question, we use the `!=` (**exclamation equal**). It’s a very close relative of the `==` operator. It’s also a binary operator and has the same low priority. Imagine that we want to ask whether the number of days left to the end of the world is currently not equal to zero:

`days_until_the_end_of_the_world != 0`

The answer `true` gives us the chance to go to the theater or to visit our friends.

# **Question: is x greater than y?**

You can ask this question by using the `>` (**greater than**) operator. If you want to know if there are more black sheep than white ones, you can write it as follows. The answer `true` confirms the statement; the answer `false` denies it.

`black_sheep > white_sheep`

# **Question: is x greater than or equal y?**

The “**greater than**” operator has another special, non-strict variant, but it’s denoted differently in classical arithmetic notation: `>=` (**greater than or equal**). There are two subsequent signs, not one. Both of these operators (strict and non-strict), as well as the other two that we discuss in the next section, are binary operators with left-side binding, and their priority is greater than the ones indicated by `==` and `!=`.

If we want to find out whether or not we have to wear a warm hat, we ask the following question:

`centigrade_outside >= 0.0`

# **Question: is x less than (or equal to) y?**

As you’ve probably already guessed, the operators we use in this case are: the `<` (**less than**) operator and its non-strict sibling `<=` (**less than or equal**). Look at this simple example: we’re going to check if there’s a risk that we’ll be fined by the highway police (the first question is strict, the second isn't).

```cpp
current_velocity < 110
current_velocity <= 110
```

# **How to use the answer we got?**

The C++ language defines a very special data type designed to store values resulting from any of the previously presented comparisons. The type is called:

```
bool
```

It's name come from the famous English mathematician, [George Bool](https://en.wikipedia.org/wiki/George_Boole) (1815 –1864), the creator of *Boolean algebra*, a branch of mathematics devoted to operations on *truth values*

The type itself shows many similarities to the previously presented `char` type. Here are some of them:

- it's actually an integer type using the minimal storage offered by a computer (it's one byte usually, just like in the `char` type);
- it can be assigned with integer values;
- it can participate in any integer evaluations and used in this way behaves like an ordinary `int`;

Along with the `bool` type there are two literals representing two possible **boolean** values - these are:

- `false` (a boolean equivalent of integer `0`);
- `true` (a boolean equivalent of integer `1` although is should be mentioned here that any non-zero integer value is interpreted as `true` by the C++ language).

Note that all the three presented words are **keywords** - don't forget about that and don't blame the compiler when it refuses a declaration of a variable named e.g. `true`.

How can we use the newly met type? The most obvious answers says that it's an ideal tool to **memorize** (store it in a variable) results of comparisons and make use of them later. How do we do that? Well, we would use an arbitrary variable of type `bool`, like this:

```cpp
int value1 = 0, value2 = 0;
bool answer = value1 >= value2;
```

If the answer is `true` because `value1` is greater than or equal to `value2`, the computer will assign `true` to `answer` (although if you take a look inside the variable, you'll find an integer `1`). If `value1` is less than `value2`, the variable `answer` will be assigned with `false` (actually `0`).

If you are unsatisfied with information about the logic of computers, we want to reassure you. We're going to discuss the issue soon. Stay tuned.

**TIME MACHINE**The `bool` type and its two literals are relatively new C++'s components. It's a common thing to find a code which uses an ordinary integers to achieve the same effects. Anyway, we prefer to uses `bool` out of respects for Mr. Bool's achievements and to increase readability of your code. Follow us, please!

# **The priority table – an update.**

The second possibility is more convenient and far more common: we can use the answer to make a decision about the future of our program. We use a special instruction for this purpose and we’ll tell you what that is very soon.

Now we need to update our priority table. It now looks as follows:

| operator         | unary / binary |
| ---------------- | -------------- |
| + -              | unary          |
| * / %            |                |
| + -              | binary         |
| < <= > >=        |                |
| == !=            |                |
| = += -= *= /= %= |                |

# **Conditions and conditional executions**

You already know how to ask, but you still don’t know how to make reasonable use of the answers. We must have a mechanism which allows us to do something if a condition is met (it evaluates to **true**) and not to do it if it isn’t (when its result is **false**. It's just like in life: we do certain things or we don’t when a specific condition is met or not, e.g. we go for a walk if the weather is good, or stay home if it’s wet and cold.

To make these decisions, the C++ language has a special instruction. Due to its nature and its application, it’s called a **conditional instruction** (or **conditional statement**).

There are several variants of the conditional instruction. We’ll start with the simplest, and slowly move on to the more difficult ones. The first form of a conditional statement, which you can see below, is written very informally but figuratively:

`if(true_or_not) do_this_if_true;`

This conditional statement consists of the following, strictly necessary, elements in this and this order only:

- **if** keyword;
- left (opening) parenthesis;
- an **expression** (a **question** or an **answer**) whose value will be interpreted solely in terms of `true` (when its value is non-zero) and `false` (when it is equal to zero);
- right (closing) parenthesis;
- an **instruction** (only **one**, but we’ll learn how to deal with that limitation).

How does this statement *work*?

- if the `true_or_not` expression enclosed inside the parentheses represents the truth (i.e. its *value is not equal to zero*), the statement behind this condition (`do_this_if_true`) will be executed;
- if the `true_or_not` expression represents a **falsehood** (its *value is equal to zero*), the statement behind this condition is **omitted** and the next executed instruction will be the one that lies after the conditional statement.

**Note:** the **true_or_not** expression is not required to be necessarily of type `int` or any of integer type's derivates. It may be of type `float` too and the general rule of the `if` statement's execution remains in force

In real life we often express a will:

*if the weather is good we will go for a walk next, we will have lunch*

As you can see, having lunch is not a conditional activity and doesn’t depend on the weather (what luck). Knowing what conditions influence our behavior and assuming that we have the parameterless functions `go_for_a_walk()` and `have_lunch()` we can write the following snippet:

`if(the_weather_is_good) go_for_a_walk();`

`have_lunch();`

As we already know, our friend the developer falls asleep when he counts 120 sheep. His sleep is implemented as a special function named `sleep_and_dream()`. This function does not require any arguments.

We can read it as: “***if** sheep_counter is greater **than** or equal **to** 120, then fall asleep and dream!*”

We’ve said that there may be only one statement after the `if` statement. When we have to **conditionally** execute more than one instruction, we need to use braces `{` and `}` which create a structure known as a **compound statement** or (much simpler) a **block**. The block is treated as a single instruction by the compiler.

This is how we can circumvent the `if` statement limitation.

Let’s treat our programmer a little nicer:

`if(sheep_counter >= 120){make_a_bed(); take_a_shower(); sleep_and_dream(); }`

`feed_the_sheepdogs();`

![https://edube.org/uploads/media/default/0001/01/8198e6bff17a60bf165d03e88496197e3c098619.png](https://edube.org/uploads/media/default/0001/01/8198e6bff17a60bf165d03e88496197e3c098619.png)

Now it’s time for some stylistic remarks. Writing blocks one after the other is, of course, syntactically correct, but very **inelegant**. It may cause the text of our program to run outside the right margin of the editor. There are a few styles of coding the blocks. We won't try to argue that some of them are better than others, but we will be follow the style being used by Bjarne Stroustrup in his book ["A Tour of C++"](https://www.stroustrup.com/Tour.html). It's likely that you may encounter code written according to different guidelines (as there are quite few of them in use worldwide) and it's also likely that after some time you'll elaborate your own coding style. Anyway, we prefer to follow in the footsteps of C++ creator.

The same snippet, written in accordance with the Bjarne's style, will look as follows:

`if (sheep_counter >= 120) {`

`make_a_bed();`

`take_a_shower();`

`sleep_and_dream();`

`}`

`feed_the_sheepdogs();`

**Note**:

- a conditionally executed block is **indented** – it improves the readability of the program and manifests its conditional nature;
- the opening brace is located in the **same line** as `if`;
- the closing brace occupies **separate line**.

In the next section, we’re going to discuss another variant of the conditional statement, which also allows you to perform an action only when the condition is not met.

Now feed your sheep dogs, please. They’ve been waiting ages for your attention.

# **Input and output**

Now we’re going to set aside conditional statements for a while and spend some time on two important and extremely useful features we use to provide connectivity between the computer and the **outside world**.

Sending data in the direction from human (user) to the computer program is called **input**. The stream of data transferred in the opposite direction, i.e. from the computer to the human, is called **output**.

We've already learned about one useful entity that serves to output data – can you remember its name? Yup, it’s the `cout` stream, and we used it along with the `<<` operator in the very first program we wrote in the C++ language, right at the beginning of this course.

The `<<` operator itself is sometimes referred to as an *insertion operator* as it inserts a string of characters into the character device (e.g. a console).

The actual `cout` capabilities are much more impressive: it’s capable of writing the data of virtually any type on a computer screen.

So what do we do if we want to output the value of type `int` or `float`, or `char`, not only a simple string?

# **Output**

To do this and other more complex tasks, we need to use any of the output streams associated with the screen (more formally: with the **console**) and send a value of a variable there.

`cout` is one of these streams and is ready to work without any special preparations – it only needs the header file name.

If you want to print the value of an integer variable to the screen, the only thing you have to do is send it to the cout stream through the `<<` operator, which indicates the desired direction of data transfer.

Both the `<<` operator and the `cout` stream are responsible for two important actions:

- **converting** the internal (machine) representation of the integer value into a form acceptable for humans
- **transferring** the converted form to the output device e.g. console

Streams are very powerful and convenient tools for both input and output. They can easily output several values of different types and mix them with the text. They can also easily input many values at once.

Let's look at streams in a few applications. The first one is trivial - we use `cout` to print a value of an `int` variable. We do it like this:

`int herd_size = 110;`

`cout << herd_size;`

We can expect that a string consisting of characters `1`, `1` and `0` will appear on the screen immediately.

You can also connect more than one `<<` operator in one `cout` statement and each of the printed elements may be of a different type and a different nature.

Take a look at the example on the right. We’re using **a string literal** (as the former element) and **an integer variable** (as the latter element) in one `cout` operation.

In this example:

`int herd_size = 123;`

`cout << "Sheep counted so far: " << herd_size;`

This snippet of code results in the string `Sheep counted so far: 123` printed on the screen.

An expression is a legal `cout` element too. The example below demonstrates one such case:

`int square_side = 12;`

`cout << "The square perimeter is: " << 4 * square_side;`

If you want a value of type `int` to be presented as a fixed-point hexadecimal number, you need to use the so-called **manipulator**. A manipulator is a special kind of entity that tells the stream that the data form has to be changed immediately. All elements outputted after the manipulator activation will be presented in the desired form.

A manipulator that is designed to switch the stream into a hexadecimal mode is called a `hex`. The snippet on the right will output a string consisting of characters 'F' and 'F'.

Technically, a manipulator is a function that changes one of the output stream’s properties, called `basefield`. The property is used to determine what number should be used as a base (as an mathematician would say: a **radix**) during the conversion of any `int` value into human readable text.

`int byte = 255;`

`cout << "Byte in hex: " << hex << byte;`

There are two important facts you need to understand here:

1. any manipulator starts its work from the point it was placed at and continues its work even after the end of the `cout` statement; it finishes working only when another manipulator cancels its action;
2. the name of the manipulator may be in conflict with any other name declared by the programmer; e.g. you can have your own variable named `hex` which could hide the manipulator’s name; such conflicts are resolved by a specialized mechanism called namespace; more on this later.

The example below demonstrates how manipulators begin and finish their work:

`int byte = 255;`

`cout << hex << byte;`

`cout << byte << dec << byte;`

Note: the `dec` manipulator switches the stream into a decimal form. We don’t have it explicitly in most cases, since **the decimal is the default** working mode for output streams.

The snippet will output the three specimens of the same value:

1. `FF` as a hexadecimal representation of 255 (as an effect of the `hex` manipulator)
2. `FF` again (the previous hex activation is still working here)
3. `255` (as a result of the `dec` manipulator activation)

The `oct` manipulator switches the stream into the **octal mode**.

The snippet below will output `377` to the screen. Can you guess why?

`int byte = 255;`

`cout << oct << byte;`

Yes, `255` in decimal is `377` in octal. Well done.

**Note**: unfortunately, there is no predefined **~~bin~~** manipulator so consequently there is no simple way to output binary image of an integer value although there are no obstacles to do the same thing in a different, user-defined way. However, we must admit it needs some more knowledge than you have in the moment.

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

int main()
{
    int byte = 255;
    cout << setbase(16) << byte << endl;
    cout << setbase(10) << byte << endl;
    cout << setbase(8) << byte;
}
```

**Console**

> `ff
> 255
> 377`

The three manipulators we showed you previously are only one of the methods (probably the simplest one) of accessing the basefield property. You can achieve the same effect by using the `setbase` manipulator, which directly instructs the stream on what base value it should use during conversion.

The **only acceptable** values for the `setbase` parameter are 8, 10 and 16 (note: 2 is not in this set so you still are not able to output integer values in the binary form). As you probably suspect, there is direct connection between these values and the previously discussed manipulators:

- `10` → `dec`
- `16` → `hex`
- `8` → `oct`

The program in the editor demonstrates the usage of the `setbase` manipulator.

Note: it requires a header file called `iomanip` (the three previous manipulators don’t).

```cpp
#include <iostream>

using namespace std;

int main()
{
    char character = 'X', minus = '-';
    float floating = 2.5;
    cout << character << minus << floating;
}
```

In general, output streams (including `cout`) are able **to recognize the type of the printed value** and act accordingly i.e. they’ll use a proper form of data presentation for char and float values.

The snippet in the editor will cause the stream to print the following text on the screen:

```
X-2.5
```

**output**

**Note:** there is one exception that should mentioned here - although `cout` stream is smart enough to recognize values of different types, it takes booleans as ordinary integers. In effect, the following snippet outputs `1`, not **true** (as you may expect):

```cpp
#include <iostream>

using namespace std;

int main()
{
    bool verdict = 1 > 0;
    cout << verdict;
}
```

```cpp
#include <iostream>

using namespace std;

int main()
{
    char character = 'X';
    int integer = character;
    cout << character << " " << static_cast<int>(character);
    cout << " " << integer << " " << static_cast<char>(integer);
}
```

`cout` is able to recognize the actual type of its element even when it is an effect of a **conversion** (an phenomenon which occurs when data is subject to type change).

We’ll discuss the conversions later, but for now we only want to mention that a phrase written as:

`static_cast<newtype>(expr)`

changes the type of the `expr` expression into the `newtype` type.

What it means is that we can see the ASCII code of any character stored within a `char` variable and vice versa, or see a character whose ASCII code is placed inside an `int` variable.

The snippet in the editor outputs the following text to the screen:

`X 88 88 X`

Sometimes we may want to (and sometimes we may have to) **break the line** being sent to the screen.

When we present many different results one by one in the same line of text, it doesn’t look nice and you won’t want to look at it. One line is okay, but a thousand lines written like that will make you go blind.

We can break the line in two ways. First, we can use one of the control characters called “newline” and coded as `\n` (note: we use two characters to write it down but the compiler sees it as one character - don’t let it fool you).

We can achieve exactly the same effect by using a manipulator called `endl` (as “end line”).

The snippet below:

`cout << "1\n2" << endl << "3\n";`

illustrates both methods and causes the console to display the following three lines of text:

```
1
2
3
```

# **Input**

Of course, equally important as data output is **data input**. Actually, it’s difficult to imagine any non-trivial program that doesn’t require any data from the user, although you can do the following:

- encode all the data needed inside the source code (which is sometimes called **hard coding**)
- when you need to repeat the execution of the program with other data, you just modify the program, compile it and run it again.

**This isn’t a particularly convenient solution**. It’s far better to get the information from the user, transfer it to the program, and then use it for calculations. So how does a C++ language program get data from a human and store it in variables?

The simplest way is to mentally reverse the direction of the transfer and to acknowledge that for the data input:

- we use `cin` stream instead of `cout`
- we use `>>` operator instead of `<<`.

By the way, the `>>` operator is often referred to as **an extraction operator**.

The `cin` stream, along with the extraction operator, is responsible for:

- transferring the human-readable form of the data from the input device e.g. a console;
- converting the data into the internal (machine) representation of the value being input.

Imagine that we need to ask the user about the maximum number of sheep we want to count before the programmer falls asleep.

The user enters the value from the keyboard and the program stores it in a specified variable (`max_sheep`). That statement looks like this:

`cin >> max_sheep;`

You probably see the similarity to emitting data using `cout`: we have a stream, we have an operator and we have a variable.

At this point the similarities end and the differences begin. First, the argument for cout may not be a variable. It can also be an expression.

Take a look:

`cout << 2 * i;`

Here we want the doubled value of `i` to be printed – and that’s feasible. Using an input stream, we need to **explicitly specify the variable** that can store the data entered by the user.

Now we’ll show you a simple but complete program that does the following:

- prompts the user to enter a single integer value,
- squares it,
- prints the result with an appropriate comment.

Analysing this program shouldn’t be a problem for you, should it?

```cpp
#include <iostream>

using namespace std;

int main() 
{
        int value;

        cout << "Give me a number and I will square it!\n";
        cin >> value;

        int square = value * value;
        cout << "You've given " << value << endl;
        cout << "The squared value is " << square << endl;
}
```

**console >_**

> Give me a number and I will square it!
> 16
> You've given 16
> The squared value is 256

So you prefer square roots to squares? No problem, but we need to remember two things: first, there’s **no such thing as a square root operator**; and second, that **square roots of negative numbers do not exist**.

We can solve the first issue by finding a function that knows how to compute the root. This type of function does exist and takes the argument of the `float` type.

The result is also a `float` (of course - the square of an integer is still an integer, but the root of any number is not always an integer, like the square root of 2).

The function we’re going to use is called `sqrtf` (square root float) and needs exactly one argument. Oh, one more thing - to use this function you need to include a header file named `cmath`.

We need to deal with negative numbers as well. If you’re careless and enter a negative number, the program will just ignore you and your input completely. It may not be polite, but at least it won’t attempt to bend the rules of mathematics. Whether we see the result or not will be decided by the conditional statement.

Now it’s time to focus on the use of floating point data and the `sqrtf` function.

Complete program is in the editor.

```cpp
#include <iostream>
#include <cmath>

using namespace std;

int main() 
{
    float value;

    cout << "Give me a number and I will find its square root:" << endl;
    cin >> value;
    if(value >= 0.0) {
        float squareroot = sqrtf(value);
        cout << "You have given: " << value << endl;
        cout << "The square root is: " << squareroot << endl;
    }
}
```

**console >_**

> Give me a number and I will find its square root:
> 26
> You have given: 26
> The square root is: 5.09902

# **Congratulations! You have completed Module 1.**

Well done! You've reached the end of Module 1 and completed a major milestone in your C++ programming education. Here's a short summary of the objectives you've covered and got familiar with in Module 1:

- the difference between machine and high-level languages;
- the machine code and compilation;
- variables, integers, floats, booleans, characters;
- comments;
- the basics of flow control;
- dealing with streams and basic I/O operations;
- writing simple programs.

You are now ready to take the module quiz and attempt the final challenge: Module 1 Test, which will help you gauge what you've learned so far.

![https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png](https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png)

---

<aside>
💡 **The End of Module I …..**

</aside>
