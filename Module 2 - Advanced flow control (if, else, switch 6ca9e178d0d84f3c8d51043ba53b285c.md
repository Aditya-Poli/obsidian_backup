# Module 2 - Advanced flow control (if, else, switch; loops) and data aggregates

Class: C++
Created: June 5, 2022 4:34 PM
Reviewed: No
Type: Section

# ****C++ Essentials: Module 2****

![https://edube.org/uploads/media/default/0001/01/e24ff993ca540f09993b3a042461c8b66be07eaa.png](https://edube.org/uploads/media/default/0001/01/e24ff993ca540f09993b3a042461c8b66be07eaa.png)

## **In this module, you will learn about:**

- how to control the flow of the program;
- more data types;
- conditional instructions: if, else, switch;
- loops and controlling the loop execution;
- logic, bitwise and arithmetic operators;
- vectors, multidimensional arrays;
- declaring and initializing structures.

# **The conditional statement – more conditional than before**

We concluded our last discussion on conditional statements with a promise that we would introduce a more complex and flexible form soon. We started our tale with a simple phrase which read: *If the weather is good, we will go for a walk*.

Note – there is not a word about what will happen if it rains cats and dogs. We only know that we certainly won’t go outdoors, but what we would do instead isn’t mentioned. We may want to plan something in case of bad weather, too.

We can say, for example: *If the weather is good we will go for a walk, otherwise we will go to a theater*. This sentence makes our plans more resistant to the whims of fate – we know what we’ll do if the conditions are met and we know what we we’ll do if not everything goes our way. In other words, we have a plan “B”.

Luckily, the C++ language allows us to express alternative plans. We do this with a second, slightly more complex form of the conditional statement – here it is:

```cpp
if(true_or_false_condition)
perform_if_condition_true;
else
perform_if_condition_false;
```

Thus, we have a new word: `else` – this is a keyword (*reserved word*). A statement which begins with `else` tells us what to do if the **condition specified for the `if` is not met**.

So the *if-else* execution goes as follows:

- if the condition is `true` (its value is not equal to zero) the `perform_if_condition_true` is executed and the conditional statement comes to an end;
- if the condition is `false` (its value is equal to zero) the `perform_if_condition_false` is executed and the conditional statement comes to an end;

```cpp
if(the_weather_is_good)
     go_for_a_walk();
else
     go_to_the_theater();
have_lunch();
```

By using this form of the conditional statement we can describe our plans as follows:

![https://edube.org/uploads/media/default/0001/01/45bf8ba2f5726ba10b3d5426b8e539bb78ee01d9.png](https://edube.org/uploads/media/default/0001/01/45bf8ba2f5726ba10b3d5426b8e539bb78ee01d9.png)

As well as in other simplified forms of this instruction, like the ones we’ve already encountered, both `if` and `else` may contain **only one statement**.

If you’re going to write more than one instruction, you have to use a **block**, as in the example below:

```cpp
if(the_weather_is_good){
    go_for_a_walk();
    have_fun();
} 
else {
    go_to_the_theater();
    enjoy_the_movie();
}
have_lunch();
```

Now it’s time to discuss two special cases of the conditional statement. First, think about when the instruction placed after `if` is another `if`.

Listen to what we have planned for this Sunday: *If the weather is fine, we’ll go for a walk. If we find a nice restaurant, we’ll have lunch there. Otherwise, we’ll eat a sandwich. If the weather is poor, we'll go to the theater. If there are no tickets, we’ll go shopping in the nearest mall.*

Complicated, right? Let’s write the same thing in C++ language. Consider the code below carefully:

```cpp
if(the_weather_is_good)
     if (nice_restaurant_is_found)
         have_lunch();
     else
         eat_a_sandwich();
else
     if(tickets_are_available)
         go_to_the_theater();
     else
         go_shopping();
```

Let’s examine two important points:

- such a use of the `if` statement is known as **nesting**; remember that every **`else` refers to the closest former `if`** which did not match any other `else`; we need to know this to determine how the `if`s and `else`s pair up;
- consider how the **indentation** improves readability and emphasizes the nesting of inner conditional statements; the depth of the indentation is in fact a matter of style but we prefer to use 4 spaces for each indentation level.

This second special case is somewhat similar to nesting, but with an important difference. Again, we’re going to change our plans and express them as follows: “If the weather is fine, we'll go for walk, otherwise if we get tickets, we’ll go to the theatre, otherwise if there are free tables at the restaurant, we’ll go for lunch. If everything fails, we’ll return home and play chess”.

Can you see how many alternatives we’ve listed here? Let’s write the same scenario in C++ language:

```cpp
if(the_weather_is_good)
    go_for_a_walk();
else if(tickets_are_available)
    go_to_the_theater();
else if(table_is_available)
    go_for_lunch();
else
    play_chess_at_home();
```

This way of assembling subsequent `if` statements is called a **cascade**. Notice how the **indentation** improves the readability of the code.

Now, let our minds work out all that we’ve told them about conditional statements, while we pay attention to our old friends: types `int`, `char` and `float`. We’re going to meet their siblings.

# **Not only the int is an int**

It would seem that the developer’s life would be organized well enough if they had type `int` to operate with integers, type `char` to manipulate characters and type `float` for floating-point calculations.

However, this practice has shown that such a narrow repertoire of types may raise some problems.

Most of the computers currently in use store `int`s using **32 bits** (4 bytes); this means that we can operate the `int`s within the range of [-2147483648 .. 2147483647]. It may happen that:

- we don’t need such big values; if we count sheep, it’s unlikely that we’ll need to count two billion of them, so why waste the majority of these 32 bits if we don’t need them;
- we need much larger values; for example, we intend to calculate the exact number of humans living on Earth; in this case we need more than 32 bits to represent that number;
- this brings us to another observation – after all, the number of inhabitants on Earth will never be a negative number; it seems like a real waste that up to half of the permissible range will never be used.

For these reasons, the C++ language provides some methods for defining precisely how we intend to store large/small numbers. This allows the compiler to allocate memory, either smaller than usual (e.g. 16 bits instead of 32) or larger than usual (e.g. 64 bits instead of 32). We can also declare that we guarantee that the value stored in the variable will be **non-negative**.

In this case the width of the variable’s **range does not change**, but is **shifted** toward the positive numbers. This means that instead of the range of [-2,147,483,648 .. 2,147,483,647] we get the range of [0 .. 4294967295].

![https://edube.org/uploads/media/default/0001/01/0e80652f8cd1866ec78933910dc107cb6aa2cb48.png](https://edube.org/uploads/media/default/0001/01/0e80652f8cd1866ec78933910dc107cb6aa2cb48.png)

To specify our memory requirements, we can use some additional keywords called *modifiers*:

- *long* – is used to declare that we need a wider range of `int`s than the standard one;
- *short* – is used to determine that we need a narrower range of `int`s than the standard one;
- *unsigned* – used to declare that a variable will be used only for non-negative numbers; this might surprise you, but we can use this modifier together with the type `char`; we’ll explain it soon.

Let’s look at some examples.

The `counter` variable will use fewer bits than the standard `int` (e.g., it could be 16 bits long – in this case, the range of the variable will be suppressed to the range of [-32768 to 32767]):

`short int counter;`

The word `int` may be **omitted** and the meaning of the declaration remains the same, like this:

`short counter;`

The `ants` variable will occupy more bits than the standard `int` (e.g. 64 bits, so it can be used to store numbers from the range of [-9223372036854775808 .. 9223372036854775807] – can you read such huge numbers?

`long int ants;`

Note – we can again **omit** the word `int`:

`long ants;`

If we come to the conclusion that a variable will **never be a negative value**, we can use the **unsigned** modifier:

`unsigned int positive;`

Of course, we can omit the `int` as usual:

`unsigned positive;`

We can also mix some of the modifiers together – take a look:

`unsigned long int big_number;`

We can remove the word `int` and the declaration will preserve its meaning:

`unsigned long big_number;`

A more modest example is here:

`unsigned short int lambs;`

Its equivalent form is:

`unsigned short lambs;`

The `long` and `short` modifiers **must not be used** in conjunction with the type `char` (which length is always the mininal possible) and (for obvious reasons) must not be used simultaneously in a single declaration.

You may ask (and it would be very reasonable question) whether `char` type is defaultly **signed** (like other integers) or **unsigned** (in contrast to other integers)?

The answer my surprise you: `char` is neither signed nor unsigned. We are serious. As its primary purpose is storing characters, not numbers, so we don't need to take care of the sign.

Anyway, if you really want to use an eight bit integer variable (that may be enough to store a small value such as the number of month or even the day of the month) and want it to behave as a signed/unsigned integer, you can express your need explicitly using either `signed` or `unsigned` modifier.

If we treat the `char` variable as a signed integer number, its range would be [-128 .. 127]. If we take it as a signed value, its range shifts to [0 .. 255]. This may be sufficient for many applications and may also result in significant savings in memory usage. The examples below presents both possible cases:

`unsigned char little_counter = 0;`

`signed char satisfaction_level = -1;`

**Note**:

- you’re not allowed to omit the word `char`;
- you can use the `signed` modifier in conjunction with `int`, `long` and `short` but it will change nothing in the variables' life (nothing unusual);
- don't try to put `signed` and `unsigned` side by side in the same declaration as the variable will suffer from split personality (it's a joke, of course - as compilers show no sense of humor at all, we have to make up this lack).

We need to add an important remark. So far we’ve used integer literals, assuming that all of them are of type `int`. This is generally the case, but there are some cases when the compiler recognizes literals of type `long`. This will happen if:

- a literal value goes **beyond the acceptable** range of type `int`;
- **letter L or l is appended** to the literal, such as `0L` or `1981l` – both of these literals are of type `long`.

# **Another float types**

The `short` and `long` modifiers cannot be used alongside the `float` but it doesn't mean that the `float` type has no floating point siblings. In fact, there are at least two of them: `double` and `long double`. The variables of types `double` and `long double` may differ from the variables of type `float`, not only in **range**, but also in **accuracy**.

What does this mean? The data stored in a floating-point variable has **finite precision** – in other words, only a certain number of digits are **precisely stored** in the variable.

For example, we expect that the value:

`1111111111111111111.111111111111111111111`

will be stored by a specific type of computer as:

`1111111131851653120.000000`

We say that the variable saves (only) **8 precise digits**. This is within the expected accuracy of 32-bit long (4 bytes)`float`s. Using a `double` (which is usually 64 bits/8 bytes long) guarantees that the variable will save a more significant number of digits – about **15-17**. This is where the name `double` comes from – its accuracy is **doubled** compared to `float`. In turn, the `long double` variable occupy 128 bit (16 bytes) bit and is able to store **33-36 significant digits**. This is why this type is sometimes called **quadruple**.

It's worth to mention that some hardware platforms my offer even longer floating point types like 256 bit long **octuple** - if a specific compiler is able to operate with data of this kind, it will accept `long long double` as a corresponding type specifier.

Now, when you're initiated to the details of floating point data life, it's time to tell you an important secret regarding literals. It may sound shocking - we are aware of it - an ordinary floating point literal like `3.1415` is recognized by a compiler as `double` and as a consequence occupies 64 bits of computer storage.

If you're determined to convince the compiler that any of your literals is actually an ordinary `float`, you should append suffix "f" or "F" to it. It means that `3.1515f` and `6.626E-34f` are of type `float`.

# **Floats and their traits**

We told you some time ago that computer addition is **not always commutative**. Do you know why? Imagine that you have to add a large number of floating-point values – some of them are very large, some very small (close to zero). If a very small float value is added to another that’s very large, the result can be quite surprising.

Take a look at the picture – we’ll assume that our computer only saves 8 precise digits of any `float`. If we add these two floats, we’ll probably get:

`11111110656.000000`

as the result. The lower value simply vanished without a trace.

We can’t avoid these effects when we add/subtract the numbers of type `float` (and of its cousins as well, because they’re also affected by this issue). The phenomenon described here is what we call a **numerical anomaly**.

![https://edube.org/uploads/media/default/0001/01/b091959aeea96769c6e29716785dbe56c93233c2.png](https://edube.org/uploads/media/default/0001/01/b091959aeea96769c6e29716785dbe56c93233c2.png)

# **Doubles and their traits**

Don't think that lenghtening the floating points data is a cure for numeric anomalies. It may mask some of them but creates new in the same time. One of the most famous innacuracies the doubles are burdened with is shown in the editor.

The code seems to be trivial. **It's obvious that 0.1 added to 0.2 is equal to 0.3**, isn't it?

Of course, it is. But not always. Run the code, please!

And what did you see?

Yes, your eyes don't deceive you. This is an effect of the fact that numbers stored as floating point data can be different from their real (precise) values. If you want to trace that phenomenon deeper, try to change type from `double` to `float` and check the result.

```cpp
#include <iostream>

using namespace std;

int main()
{
    double a = 0.1;
    double b = 0.2;
    double c = 0.3;

    if(a + b != c)
        cout << "Your computer is out of order";
}
```

**console >_**

> `Your computer is out of order`

# **Two simple programs**

Now we’re going to show you some simple but complete programs. We won’t explain them in detail, because we think the comments inside the code are sufficient guides.

All these programs solve the same problem – they find the largest of several numbers and print it out.

Let’s start with the simplest case – how to **identify the larger of two numbers**.

```cpp
/* finding the larger of two numbers */

#include <iostream>

using namespace std;

int main() 
{
  /* the two numbers */
  int number1, number2;

  /* read two numbers */
  cin >> number1;
  cin >> number2;

  /* we will save the larger number here */
  /* we temporarily assume that the former number is the larger one */
  /* we will check it soon */
  int max = number1;

  /* we check if the assumption was false */
  if (number2 > max)
      max = number2;

  /* we print the result */
  cout << "The larger number is " << max << endl;
}
```

**console >_**

> `5 3`

> `The larger number is 5`

Now let's try to find **the largest of three numbers**. We find the larger of the first two and compare it with the third one. Here we go.

```cpp
/* finding the largest of three numbers */

#include <iostream>
using namespace std;

int main() 
{
  /* the three numbers */
  int number1, number2, number3;

  /* read three numbers */
  cin >> number1;
  cin >> number2;
  cin >> number3;

  /* we will save the larger number here */
  /* we temporarily assume that the former number is the larger one */
  /* we will check it soon */
  int max = number1;

  /* we check if the second value is the largest */
  if (number2 > max)
      max = number2;

  /* we check if the third value is the largest */
  if (number3 > max)
      max = number3;

  /* we print the result */
  cout << "The largest number is " << max << endl;
}
```

**console >_**

> `5 3 10`

> `The largest number is 10`

# **Some simple programs**

By this point, you should be able to write a program that finds the largest of four, five, six or even ten numbers. You already know the scheme, so the extension of the program doesn’t need to be particularly complex.

But what happens if we ask you to write a program that finds the largest of a hundred of numbers? Can you imagine the code?

- You’d need hundreds of declarations of type `int` variables. If you think you can cope with that, then try to imagine searching for the greatest of a million numbers;
- Imagine the code that contains 99 conditional statements and a hundred `cin` statements.

![https://edube.org/uploads/media/default/0001/01/f6c756e81e56b3a54044cdeb7f1d127be472c42a.png](https://edube.org/uploads/media/default/0001/01/f6c756e81e56b3a54044cdeb7f1d127be472c42a.png)

# **Some simple programs**

Let’s ignore the C++ language for the moment and try to analyze the problem while not thinking about the programming. In other words, let’s try to write the **algorithm**, and when we’re happy with it, we'll try to implement it.

We’re going to use a kind of notation that is not a programming language at all (it could be neither compiled nor executed), but is formalized, concise and readable. We call this **pseudo-code**.

There is an example of pseudo-code below. Take a look at it. What’s going on?

`1. max = -999999999;
2. read number
3. if(number == -1) print max next stop;
4. if(number > max) max = number
5. go to step 2`

First, we can simplify our program if, at the very beginning of the code, we assign the variable max with a value which will be smaller than any of the numbers entered. We’ll use *-999999999* for this purpose.

Second, we assume that our algorithm doesn’t know in advance how many numbers will be delivered to the program. We expect that the user will enter as many numbers as she/he wants – the algorithm will work equally well with one hundred or one thousand numbers. How do we do that? Well, we make a deal with the user: when the value `-1` is entered, it will be a sign that there is no more data and the program should end its work. Otherwise, if the entered value is not equal to - 1, the program will read another number and so on.

The trick is based on the assumption that any part of the code **can be performed more than once** – in fact, as many times as you need.

Performing a certain part of the code more than once is called a loop. You probably already know what a loop is. See, steps 2 through 5 make a loop. Can we use a similar structure in the program written in the C++ language? Yes, we can. And we’re going to tell all you about it soon.

# **The “while” loop**

We want to ask you a strange question: how long do you usually take to wash your hands? Don’t think about it, just answer. Well, when your hands are very dirty, you wash them for a very long time. Otherwise it takes less time. Do you agree with this statement:

`while my hands are dirty`

`I am washing my hands;`

Note that this also implies that if our hands are clean, we won’t wash them at all.

So now you've learnt one of the **loops** available in the C++ language. In general, the loop manifests itself as follows:

`while(conditional_expression)`

`statement;`

If you think it looks similar to the `if` instruction, you’re quite right. Indeed, there’s only one syntactic difference: we replaced the word `if` with the word `while`.

The semantic difference is more important: when the condition is met, if performs its statements only once; `while` repeats the execution as long as the condition evaluates to `true`.

```cpp
while(conditional_expression) {
    statement_1;
    statement_2;
    :
    :
    statement_n;
}
```

Let’s make a few observations:

- if you want `while` to execute **more than one** statement, you must (like with the `if` statement) use a block – take a look at the code in the editor;
- an instruction or instructions executed inside the loop are called the **loop's body**;
- if the condition is `false` (equal to zero) as early as when it’s tested for the first time, the **body is not executed** even once (note the analogy of not having to wash your hands if they’re not dirty);
- the body should be able to change the condition value, because if the condition is true at the beginning, the body might **run continuously to infinity** (notice that washing changes the state of impurity).

```cpp
while(true) {
  cout << "I am stuck inside a loop" << endl;
}
```

Here is an example of a loop that is not able to finish its execution. This loop will infinitely print `I am stuck inside a loop` on the screen.

![https://edube.org/uploads/media/default/0001/01/d26f39e15dd1b5aa20366418cd5a4fadea5e46e4.png](https://edube.org/uploads/media/default/0001/01/d26f39e15dd1b5aa20366418cd5a4fadea5e46e4.png)

Analyze this program carefully. Locate the loop’s body and find out how the **body is exited**.

See how the above code implements the algorithm we made earlier.

```cpp
#include <iostream>

using namespace std;

int main()
{
    /* temporary storage for the incoming numbers */
    int number;
    /* get the first value */
    cin >> number;
    /* we will store the currently greatest number here */
    int max = number;
    /* if the number is not equal to -1 we will continue */
    while (number != -1) {
        /* is the number greater than max? */
        if (number > max)
            /* yes – update max */
            max = number;
        /* get next number */
        cin >> number;
    }
    /* print the largest number */
    cout << "The largest number is " << max << endl;
}
```

**console >_**

> 6

> 5

> 10

> -1

> `The largest number is 10`

This program counts odd and even numbers coming from the keyboard. Have a look at it.

Certain snippets can be simplified without changing the program’s behavior. Take a look at the next slide.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    /* we will count the numbers here */
    int evens = 0, odds = 0;

    /* we will store the incoming numbers here */
    int number;

    /* read first number */
    cin >> number;

    /* 0 terminates execution */
    while (number != 0) {
        /* check if the number is odd */
        if (number % 2 == 1)        
            /* increase „odd” counter */
            odds++;
        else
            /* increase „even” counter */
            evens++;
        /* read next number */
        cin >> number;
    }
    /* print results */
    cout << "Even numbers: " << evens << endl;
    cout << "Odd numbers: " << odds << endl;
}
```

**console >_**

> 5

> 6

> 2

> 1

> 9

> 4

> 0

> `Even numbers: 3`

> `Odd numbers: 3`

Try to recall how the C++ language interprets the truth of a condition and note that these two forms are equivalent.

```cpp
while(number != 0) {...}
while(number) {...}
```

The condition that checks if a number is odd can be coded in like this:

```cpp
if(number % 2 == 1)...
if(number % 2)...
```

We guess that nothing surprises you, right? But there are two things that we can write more compactly. First, the condition of the while loop.

```cpp
int main() 
{
      int counter = 5;

      while(counter != 0) {
               cout << "I am an awesome program" << endl;
               counter--;
      }
}
```

Another change requires us to have some knowledge of how the post-decrement works. We’ll use it to compact our program once again.

```cpp
int main() 
{
       int counter = 5;

       while(counter) {
                cout << "I am an awesome program" << endl;
                counter--;
       }
}
```

We’re convinced that this is the simplest form of this program, but you can challenge us if you dare.

```cpp
int main() 
{
       int counter = 5;

       while(counter--)
                cout << "I am an awesome program" << endl;
}
```

# **The “do” loop or do it at least once**

We already know that the `while` loop has two important features:

- it checks the condition **before** entering the body,
- the body will not be entered if the condition is false.

These two properties can often cause unnecessary complications. For this reason, there’s another loop in the C++ language which **acts like a mirror image of the while loop**.

We say this because in that loop:

- the condition is checked at the end of the body execution,
- the loop's body is executed at least once, even if the condition is not met.

This loop is called the `do` loop. Its simplified syntax is listed in the editor.

If you want to execute a body containing more than one statement, you need to use a block.

```cpp
do
    statement;
while(condition);

do {
    statement_1;
    statement_2;
    :
    :
    statement_n;
} while(condition);
```

Let’s return to the program that searches for the largest number. Firstly, we will use the “`do`” loop instead of “`while`” for teaching purposes. Secondly, we remove the vulnerability involved in the excessive trust in the user’s good will. Our new program won’t be misled by entering the value of `-1` as the first number. Look at the editor. Here's our code.

Take a look. We used the `counter` variable to count the numbers entered so we can instruct the user that we cannot search for the greatest number if no number is given.

As we have to **read at least one number**, it makes sense to use the `do` loop. We use this approach in the program.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int number;
    int max = -100000;
    int counter = 0;
    do {
        cin >> number;
        if (number != -1)
            counter++;
        if (number > max)
            max = number;
    } while (number != -1);
    if (counter)
        cout << "The largest number is " << max << endl;
    else
        cout << "Are you kidding? You haven't entered any number!" << endl;
}
```

**console >_**

> 6

> 7

> 10

> -1

> `The largest number is 10`

# **“for” - the last loop**

The last available kind of loop in C++ language comes from the fact that sometimes it’s more important to **count the “turns” of the loop** than to check the conditions.

Imagine that a loop's body needs to be executed exactly one hundred times. If you want to use the `while` loop for that purpose, it may look something like this:

```cpp
int i = 0;
while(i < 100) {
  /* the body goes here */
  i++;
}
```

We can distinguish three independent elements there:

- the initialization of the counter
- the checking of the condition
- the modification of the counter

It’s possible to create something like a generalized scheme for these kinds of loops, here it is:

```cpp
initialization;
while(checking) {
  /* the body goes here */
  modifying;
}
```

This way of coding the loop is very common, so there’s a special, brief way of writing it in the C++ language.

Below we’ve gathered all three decisive parts together. The loop is clear and easy to understand. Its name is `for`.

```cpp
for(initialization; checking; modifying) {
  /* the body goes here */
}
```

```cpp
for(int i = 0; i < 100; i++) {
  /* the body goes here */ 
}
```

The `for` loop can take the form shown in the editor.

The variable used for counting the loop's turns is often called a **control variable**.

Notice, that if a control variable is declared **within** the *initialization* clause (like in the example) the variable is available **only inside the loop's body**.

If it's not desirable and you want to use the same variable somewhere outside the loop's body you need to declare it outside the loop, like this:

```cpp
int i;

/*
some code
*/

for(i = 0; i < 100; i++) {
   // the body goes here 
}
```

```cpp
for(;;) {
  /* the body goes here */ 
}
```

The `for` loop has an interesting singularity. If we omit any of its three components, it is presumed that there is a `1` there instead.

One of the consequences of this is that a loop written in this way is an infinite loop (do you know why?).

- **`Check`**
  
    Well, the conditional expression is not there, so it is automatically assumed to be true. And because the condition never becomes false, the loop becomes infinite.

Let’s look at a short program whose task is to write some of the first powers of 2.

The `exp` variable is used as a control variable for the loop and indicates the current value of the exponent. The exponentiation itself is replaced by multiplying by 2. Since 2^0 is equal to 1, then 2 ∙ 1 is equal to 2^1, 2 ∙ 21 is equal to 2^2 and so on.

Answer this question: what is the greatest exponent for which our program still prints the result?

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int pow = 1;

    for(int exp = 0; exp < 16; exp++) {
        cout << "2 to the power of " << exp << " is " << pow << endl;
        pow *= 2;
    }
}
```

**console >_**

> 2 to the power of 0 is 1
> 2 to the power of 1 is 2
> 2 to the power of 2 is 4
> 2 to the power of 3 is 8
> 2 to the power of 4 is 16
> 2 to the power of 5 is 32
> 2 to the power of 6 is 64
> 2 to the power of 7 is 128
> 2 to the power of 8 is 256
> 2 to the power of 9 is 512
> 2 to the power of 10 is 1024
> 2 to the power of 11 is 2048
> 2 to the power of 12 is 4096
> 2 to the power of 13 is 8192
> 2 to the power of 14 is 16384
> 2 to the power of 15 is 32768

# **break and continue – the loop's spices**

So far, we’ve treated the body of the loop as an **indivisible and inseparable** sequence of instructions that are performed completely at every turn of the loop. However, as a developer, you could be faced with the following choices:

- it appears that it is unnecessary to continue the loop as a whole; we should stop executing the loop's body and go further;
- it appears that we need to start the condition testing without completing the execution of the current turn.

The C++ language provides us with two special instructions to implement both these tasks. Let's say for the sake of accuracy that their existence in the language is not necessary - an experienced programmer can code any algorithm without these instructions.

The famous Dutch computer scientist [Edsger Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra) proved it in 1965. These additions, which don't improve the language's expressive power but only simplify the developer's work, are sometimes called **syntactic sugar**.

These two instructions are:

- `break` - exits the loop immediately and unconditionally ends the loop’s operation; the program begins to execute the nearest instruction after the loop's body;
- `continue` – behaves as the program suddenly reached the end of the body; the end of the loop's body is reached and the condition expression is tested immediately.

Both these words are keywords.

Now let’s look at two simple examples. We’ll return to our program that recognizes the largest of the numbers entered. We’ll convert it twice, using both instructions. Analyze the code and judge whether and how you would use any of them.

You can see the `break` variant in the editor.

Note that the only way to exit the body is to perform the break, as the loop itself is infinite (`for (;;)`).

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int number;
    int max = -100000;
    int counter = 0;
    for (;;) {
        cin >> number;
        if (number == -1)
            break;
        counter++;
        if (number > max)
            max = number;
    }
    if (counter)
        cout << "The largest number is " << max << endl;
    else
        cout << "Are you kidding? You haven't entered any number!" << endl;
}
```

**console >_**

> 10
> 6
> 12
> 13
> 10
> -1
> The largest number is 13

# **break and continue – the loop's spices**

And now the `continue` variant.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int number;
    int max = -100000;
    int counter = 0;

    do {
        cin >> number;
        if(number == -1)
            continue;
        counter++;
        if(number > max)
            max = number;
    } while (number != -1);
    if(counter)
        cout << "The largest number is " << max << endl;
    else 
        cout << "Are you kidding? You haven't entered any number!" << endl;
}
```

**console >_**

> 6
> 12
> 13
> 10
> -1
> The largest number is 13

# **Computers and their logic**

Have you noticed that the conditions we’ve used so far are very simple, quite primitive, in fact? The conditions we use in real life are much more complex. Let's look at this following sentence:

*If we have some free time, and the weather is good, we will go for a walk.*

We have used the conjunction “and”, which means that going for a walk depends on the **simultaneous fulfillment of the two conditions**.

In the language of logic, connecting conditions like this is called a conjunction. And now another example:

*If you are in the mall or I am in the mall, one of us will buy a gift for Mom.*

The appearance of the word “or” means that the purchase depends on at least one of these conditions. In logic terms, this is called a **disjunction**.

So clearly, the C++ language needs to have operators to build conjunctions and disjunctions. Without them, the expressive power of the language would be substantially weakened. They are called **logical operators**.

![https://edube.org/uploads/media/default/0001/01/d2d0e1f5356591a298cfb916d6c585ff2839cba7.png](https://edube.org/uploads/media/default/0001/01/d2d0e1f5356591a298cfb916d6c585ff2839cba7.png)

# **Pride && Prejudice**

The logical conjunction operator in the C++ language is a digraph `&&` (*ampersand ampersand*).

This is a binary operator with a priority lower than the comparison operators. It allows us to code complex conditions without the use of parentheses like this one:

`counter > 0 && value == 100`

The result provided by the `&&` operator can be determined on the basis of the **truth table**. If we consider the conjunction of:

`left && right`

the set of possible values of arguments and corresponding values of the conjunction looks as follows:

| left  | right | left && right** |
| ----- | ----- | --------------- |
| false | false | false           |
| false | true  | false           |
| true  | false | false           |
| true  | true  | true            |

**TIME MACHINE:**

The `&&` operator derives directly from C++'s ancestor, the C language and in the opinion of many using it may be error prone for at least two reasons:

- it's very (too) similar to the `&` operator performing completely different operation;
- it's counter-intuitive.

Due to this reasons C++ introduced a more verbose and unequivocal synonym for the conjunction: it's a keyword `and`. Feel free to use one of them in your code - they work exactly the same.

# **To be || not to be**

The disjunction operator is the digraph `||` (*bar bar*). It’s a binary operator with a lower priority than `&&` (just like “`+`” compared to “`*`”). Its truth table looks as follows:

| left | right | left || right** |
| --- | --- | --- |
| false | false     | false |
| false | true | true |
| true | false | true |
| true  | true | true |

**TIME MACHINE**The `||` has its synonym too - it's a keyword `or`.

In addition, there’s another operator that can be used to construct conditions. It’s a unary operator performing a **logical negation**. Its operation is simple: it turns true into false and false into true. This operator is written as a single character `!` (*exclamation mark*) and its priority is very high: the same as the increment and decrement operators.

Its truth table is truly simple:

| arg   | !arg  |
| ----- | ----- |
| false | true  |
| true  | false |

**TIME MACHINE**Can you guess how to write `!`'s keyworded synonym? Yes, it's a keyword `not`. Note that the exclamation mark can be really dangerous - it can be confused with the digit `1` or even overlooked (it's tiny so you can miss it when the logical expression is long and complicated). `not` is definitely more eye-catching.

# **Some logical expressions**

Note that the following conditions are **equivalent, respectively**:

`variable > 0         !(variable <= 0)`

`variable != 0        !(variable == 0)`

You may remember [De Morgan's laws](https://en.wikipedia.org/wiki/De_Morgan's_laws) from school. They say that:

*The negation of a conjunction is the disjunction of the negations. The negation of a disjunction is the conjunction of the negations.*

Let's try to write the same thing using the “C” language:

`!(p && q) == !p || !q`

`!(p || q) == !p && !q`

Note how the parentheses have been used to code the expressions.

We should add that none of the previous two-argument operators can be used in the abbreviated form known as `op=`. This exception is worth remembering.

# **How to deal with single bits**

Logical operators take their arguments as a whole, **regardless of how many bits they contain**. The operators are aware only of the value: `0` (when all the bits are reset) means “`false`”; not `0` (when at least one bit is set) means “`true`”. The result of their operations is one of the values: `0` or `1`. This means that the following snippet:

`bool i = false;`

`bool j = !!i;`

will assign a value of `1` to the `j` variable if `i` is not zero; otherwise, it will be `0` (why?).

However, there are four operators that allow you to manipulate single bits of data. We call them **bitwise operators**. They cover all the operations we mentioned before in the logical context and one additional operator. This is the *xor (exclusive or)* and is denoted as `^` (caret). Here are all of them:

| & (ampersand) | bitwise              |
| ------------- | -------------------- |
| conjunction   |                      |
| (bar)         | bitwise disjunction  |
| ~ (tilde)     | bitwise negation     |
| ^ (caret)     | bitwise exclusive or |

**TIME MACHINE**All these single-character operators have they modern verbose synonyms - here they are:.

| &                 | bitand |
| ----------------- | ------ |
|                   |        |
| ~                 | compl  |
| (as in compliment |        |
| )                 |        |
| ^                 | xor    |

Let's make it easier:

- `&` requires exactly two “1s” to provide “1” as the result
- `|` requires at least one “1” to provide “1” as the result
- `^` requires only one “1” to provide “1” as the result
- `~` (is one argument and) requires “0” to provide “1” as the result

But take note: arguments of these operators **must be integers** (int as well as `long`, `short` or `char`); we must not use any of floats here.

The difference in the operation of the logical and bit operators is important: the logical operators do not penetrate into the bit level of its argument. They’re only interested in the final boolean value.

Bitwise operators are stricter: **they deal with every bit separately**. If we assume that the `int` variable occupies 32 bits, you can imagine the bitwise operation as a 32-fold evaluation of the logical operator for each pair of bits of the arguments. Obviously, this analogy is somewhat imperfect, as in the real world all these 32 operations are performed at the same time.

| left | right | left & right | left | right | left ^ right |
| --- | --- | --- | --- | --- |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 | 1 |
| 1 | 0 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 0 |

| arg | ~ arg |
| --- | ----- |
| 0   | 1     |
| 1   | 0     |

Let’s have a look at an example of the difference in operation between logical and bit operations. Let’s assume that the following declaration has been performed:

`int i = 15, j = 22;`

If we assume that the `int`s are stored with 32 bits, the bitwise image of the two variables will be as follows:

`i: 00000000000000000000000000001111
j: 00000000000000000000000000010110`

The declaration is given:

`int log = i && j;`

We’re dealing with a logical conjunction. Let’s trace the course of the calculations. Both variables `i` and `j` are not zeros so will be deemed to represent “`true`”.

If we look at the truth table for the && operator, we can see that the result will be “true” and that it’s an integer equal to 1. This means that the bitwise image of the log variable is as follows:

`log:00000000000000000000000000000001`

Now the bitwise operation – here it is:

`int bit = i & j;`

The & operator will operate with each pair of corresponding bits separately, producing the values of the relevant bits of the result. Therefore the result is this:

`bit:00000000000000000000000000000110`

These bits correspond to the integer value of 6.

Let's try the **negation operators** now. First the logical one:

`int i = 15; logneg = !i;`

The `logneg` variable will be set to `0`, so its image will consist of zeros only.

The result:

`logneg:00000000000000000000000000000000`

The bitwise negation goes here:

`int i = 15, bitneg = ~i;`

The result:

`bitneg:11111111111111111111111111110000`

It may surprise you to learn that the `bitneg` variable value is -16. Strange? No, not at all!

If it surprises you, try to spend some time looking into the secrets of the binary numeral system and the rules governing so-called **[two's complement numbers](https://en.wikipedia.org/wiki/Two%27s_complement)**. It makes for good bedtime reading.

We can use each of the previous two-argument operators in their abbreviated forms. These are the examples of equivalent notations:

| x = x & y; | x &= y; |
| ---------- | ------- |
| x = x      | y;      |
| x = x ˜ y; | x ~ = y |

**Note**
: keyworded bitwise operators cannot be used in shortcut forms. You may find it inconsistent (so do we).

We'll now show what you can use bitwise operators for.

Imagine that you have to write an important piece of an operating system. You’ve been told that you’re to use a variable declared in the following way:

`int flag_register;`

The variable stores the information about various aspects of system operation. Each bit of the variable stores one yes/no value.

You’ve also been told that only one of these bits is yours – bit number three (remember that bits are numbered from 0 and bit number 0 is the lowest one, while the highest is number 31).

The remaining bits are not allowed to change because they’re intended to store other data.

Here's your bit marked with the letter “x”:

`0000000000000000000000000000x000`

You may face the following tasks:

**#1:**

Check the state of your bit – you want to find out the value of your bit; comparing the whole variable to zero will not do anything, because the remaining bits can have completely unpredictable values, but we can use the following conjunction property:

`x & 1 = x
x & 0 = 0`

If we apply the `&` operation to the flag_register variable along with the following bit image:

`00000000000000000000000000001000`

(note the "1" at your bit's position) we obtain one of the following bit strings as a result

`00000000000000000000000000001000`

if your bit was set to “1”

`00000000000000000000000000000000`

if your bit was reset to “0”.

A sequence of zeros and ones whose task is to grab the value or to change the selected bits is called **a bitmask**. Let’s try to build a bitmask to **detect the state** of your bit. It should point to the **third** bit. That bit has the weight of 23 = 8. A suitable mask could be created by the following declaration:

`int the_mask = 8;`

or (in the more detailed way):

`int the_mask = 0b1000;`

We can also make a sequence of instructions depending on the state of your bit – here it is:

```cpp
if(flag_register & the_mask) {
    /* my bit is set */
} else {
    /* my bit is reset */
}
```

**#2:**

**Reset your bit** – you assign a zero to the bit while all other bits remain unchanged; we’ll use the same property of the conjunction as before, but we’ll use a slightly different mask – just like this:

`1111111111111111111111111111110111`

Note that the mask was created as a result of the negation of all bits of `the_mask` variable.

Resetting the bit is simple and looks like these (choose the one you like most):

`flag_register = flag_register & ~the_mask;

flag_register &= ~the_mask;`

**#3:**

**Set your bit** – you assign a “one” to your bit while all the remaining bits must remain unchanged; we’ll use the following disjunction's property:

`x | 1 = 1`

`x | 0 = x`

We’re ready to set your bit with one of the following instructions:

`flag_register = flag_register | the_mask;

flag_register |= the_mask;`

**#4:**

**Negate your bit** – you replace a “one” with a “zero” and a “zero” with a “one”. We’ll use an interesting property of the xor operator:

`x ^ 1 = !x`

`x ^ 0 = x`

Now let's negate your bit with one of the instructions:

`flag_register = flag_register ^ the_mask;

flag_register ^= the_mask;`

```cpp
value << bits
value >> bits
```

The C++ language offers us yet another operation relating to single bits: **shifting**. It applies only to integer values and you can’t use it with floats as arguments. You use this operation unconsciously all the time. How do you multiply any number by 10? Take a look:

12345 ∙ 10 = 123450

As you can see, multiplying by ten is in fact a shift of all the digits to the left and filling the resulting gap with a “0”. Division by 10? Let's look:

12340 ÷ 10 = 1234

Dividing by 10 is nothing more than shifting the digits to the right.

The same kind of operation is performed by the computer, but with one difference: as 2 is the base for binary numbers (not 10), shifting a value one bit to the left corresponds to multiplying it by 2; respectively, shifting one bit to the right is like dividing by 2 (notice that the right-most bit is lost).

Bit shifting can be:

- logical, if all the bits of the variable are shifted; shifting takes place when you apply it to the unsigned integers;
- arithmetic, if the shift omits the **sign bit** – in two's complement notation, the role of the **sign bit** is played by the **highest bit** of a variable; if it’s equal to "1", the value is treated as a negative; this means than the arithmetic shift cannot change the sign of the shifted value.

The shift operators in the C++ language are a pair of digraphs, `<<` and `>>`, clearly suggesting in which direction the shift will act. The left argument of these operators is the integer value whose bits are shifted. The right argument determines the size of the shift. This shows that this operation is certainly not commutative.

The priority of these operators is very high. You'll see them in the updated table of priorities which we’ll show you at the end of this section.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int w_sign = -8;
    unsigned wo_sign = 4;

    int var_s;
    unsigned var_u;

    /* equivalent to division by 2 –> var_s == -4 */
    var_s = w_sign >> 1;
    cout << var_s << endl;

    /* equivalent to multiplication by 4 –> var_s == -32 */
    var_s = w_sign << 2;
    cout << var_s << endl;

    /* equivalent to division by 4 –> var_u == 1 */
    var_u = wo_sign >> 2;
    cout << var_u << endl;

    /* equivalent to multiplication by 2 –> var_u == 2 */
    var_u = wo_sign << 1;
    cout << var_u << endl;
}
```

Let’s assume the following declarations exist:

```cpp
int w_sign = -8;
unsigned wo_sign = 4;
```

Take a look at the shifts in the editor. Run the code and make sure that you can explain each of the results.

**Note**: both operators can be used in the shortcut form as below:

```cpp
signed >>= 1; /* division by 2 */
unsigned <<= 1; /* multiplication by 2 */
```

And here’s the updated priority table, containing all the operators introduced in this section.

![Untitled](Module%202%20-%20Advanced%20flow%20control%20(if,%20else,%20switch%206ca9e178d0d84f3c8d51043ba53b285c/Untitled.png)

# **Case and switch vs. if**

As we already know, an *if-cascade* is a name for a construction of code where many if instructions are **placed consecutively one after another**, as in the example in the editor.

Of course, there are no obstacles to using and maintaining a code like this, but there are a few disadvantages that may be discouraging. The longer the cascade, the harder it is to read and understand what it’s indented for.

Amending the cascade is also hard: it's hard to add a new branch into it and it's hard to remove any previously created branch.

The C++ language offers us a way to make these selections easier. By the way, this is only more syntax candy. You can manage without it, but don't hesitate to use it when your `if`s start growing extensively.

```cpp
if(i == 1) 
      cout << "Only one?" << endl;
else if(i == 2)
      cout << "I want more" << endl;
else if(i == 3)
      cout << "Not bad" << endl;
else
      cout << "OK" << endl;
```

Let's take a look at the snippet in the editor. It's an example of how to replace an `if` cascade with a specialized instruction. Note that the words `switch` and `case` are keywords.

The new instruction is called `switch` and it is, in fact, a switch. So how does it work?

First, the value of the expression enclosed inside the parenthesis after the `switch` keyword is **evaluated** (this is sometimes called a *switching expression*).

Then the block is searched in order to **find a literal** preceded by the `case` keyword which is equal to the value of the expression. The pair consisting of the `case` keyword and the correspoding constant is sometimes calles **case label**.

When this case is found, the instructions behind the colon are **executed**. If there’s a `break` among them, the execution of the `switch` statement is terminated, otherwise, all instructions are executed until the end of the block is reached or another `break` is met.

What happens if the switching expression has a value that does not occur in any of the cases? The answer is simple: nothing will happen – none of the branches of the `switch` statement are executed.

Note the way we used to layout we used to encode the `switch`. Such a format increases legibility of the code and makes it elegant - do you agree?

```cpp
switch(i) {
case 1: 
    cout << "Only one?" << endl; 
    break;
case 2: 
    cout << "I want more" << endl; 
    break;
case 3: 
    cout << "Not bad" << endl; 
    break;
case 4: 
    cout << "OK"<< endl;
}
```

Let's modify the requirements. We’ll assume now that our program is satisfied (it says “OK”) if the `i` variable is equal to `4` or to `3`. Does this mean that we have to create two branches for both possibilities?

Fortunately not. We’re allowed to place more than one `case` in front of any branch, like the one in the editor.

```cpp
switch(i) {
case 1: 
    cout << "Only one?" << endl; 
    break;
case 2: 
    cout << "I want more" << endl; 
    break;
case 3: 
case 4: 
    cout << "OK" << endl;
}
```

We can also assume that our program does not have an opinion when `i` values are different from the ones specified so far and we want the program to express it in a clear form. Have we made a million new cases covering the entire `int` type's range?

No. We can use a generalized `case` that covers all these events which haven’t been enumerated in the previous cases. Take a look at the code in the editor.

Note that `default` is a keyword too.

Don't forget to use the break. Leaving out this keyword is one of **the most common mistakes** developers make (not only at the beginning of their careers).

Simple, right? And how elegant.

But now a few more important remarks to note:

- the value after the case **must not be an expression** containing variables or any other entities whose values aren't known at compilation time;
- the `default` can be located anywhere (even as the first switch's label) although putting it at the last position makes the code easier to analyze;
- all labels must be unique;
- `default` cannot be used more than once.

Now we say goodbye to our `switch` statement; it's time to take up an important challenge – we’re going to discuss **arrays**.

```cpp
switch(i) {
case 1: 
    cout << "Only one?" << endl; 
    break;
case 2: 
    cout << "I want more" << endl; 
    break;
case 3: 
case 4: 
    cout << "OK" << endl; 
    break;
default: 
    cout << "Don't care"  << endl;
}
```

# **Vectors – why?**

```cpp
int var1, var2, var3, var4, var5;
```

There may come a time when we have to read, store, process, and finally, print dozens, maybe hundreds, perhaps even thousands of numbers. What then? Must we declare a separate variable for each value? Will we have to spend long hours writing statements like the one in the editor.

If you think this is a simple task, then we suggest that you take a piece of paper and write a program that reads five numbers of type `int` and prints them in order from the smallest to the largest (NB this is called *sorting*). We don’t think your piece of paper will be big enough for the task.

So far, we’ve declared variables that can store exactly one given value at a time. These variables are called *scalars*, analogous to mathematical terms. All variables we’ve used so far have actually been scalars.

Think of how convenient it would be if we could declare a variable that can store more than one value. For example, `100` or `1000` or even `10,000` variables. It would still be one and the same variable, but very wide and extensive. Does that sound appealing? Perhaps, but how would it handle all these different values? How would it choose just the one we need?

Should we just number them? And we'll say: *give me the value number 2; assign the value number 15; increment the value number 10000.*

Maybe... what do you think?

We'll show you how to declare these **multi-value variables**. We’ll do this with the example that we suggested before. We’ll try to write a program that sorts a sequence of integers, but we won't be particularly ambitious right now – we’ll assume that there will be 5 numbers.

```cpp
#include <vector>

using namespace std;

vector<int> numbers(5);
```

We read this record as follows:

- as we're going to declare a vector we need to include a header file named `vector` (no suprise)
- as we prefer not to write `std::` in front of each `vector` declaration we instruct the compiler to use `std` namespace as the default one;
- we create a variable of type `vector`;
- the vector is intended to store `int` values (**note**: you specify the vector element's type putting its name between `<` and `>`);
- the newly declared variable is called `numbers`;
- it’s intended to store five values (note the number enclosed inside parentheses).

Let’s say the same thing using the appropriate terminology: `numbers` **is a vector consisting of 5 values of type `int`**.

All the elements of a vector **have the same type**. There are no exceptions to this rule. There are other programming languages which allow the use of vectors with elements of various types, but C++ is not one of them. It’s not, as you might think, a troublesome limitation and it can be effectively avoided, if necessary. However, this is a very complex subject and you have to wait some time for the solution to this puzzle.

It’s time for a bit of intrigue. The C++ language has a convention which says that the elements in a vector are numbered **starting from 0**. This means that the item stored at the beginning of the vector will have the number 0. Since there are 5 elements in our vector the last one will have the number 4. **Don't forget this**. However, you’ll soon get used to it and it’ll become second nature.

Before we go any further, we have to note the following: our vector is a **collection of elements**, but each **element is a scalar**.

**TIME MACHINE**The presented way of declaring vectors is the recommended and timely solution for creating new code but it doesn't meant that there are not other ways of achieving (nearly) the same effect. Don't be surprised seeing the following line in someone else's code:

```cpp
int numbers[5];
```

The above declaration doesn't need any additional header file to be included (what seems attractive) but the functionality offered by such a vector is significantly smaller. This is why we prefer the modern way although we reserve the right to use the older form as well.

How do we assign a value to the chosen element of the vector?

Let's assign the value of 111 to the **first** element of the vector. We do it this way:

`numbers[0] = 111;`

We need a value stored in the **third** element of the vector and we want to assign it to the integer variable `i`. This is how we can do it:

`int i = numbers[2];`

And now we want the value of the **fifth** element to be copied to the **second** element – can you guess how to do it?

`numbers[1] = numbers[4];`

The value inside the brackets, which selects one element of the vector, is called an **index**, while the operation of selecting an element from the vector is known as **indexing**.

**Note**: all the indices we’ve used so far are literals. Their values are fixed at run time, but any expression could be the index too. This opens up lots of opportunities.

```cpp
#include <vector>

using namespace std;

vector<int> numbers(5);
int sum = 0;

for(int i = 0; i < 5; i++)
    sum += numbers[i];
```

We want to calculate the **sum of all values** stored in the `numbers` vector. We declare a variable where the sum will be stored and initially assign a value of `0` to it – its name is `sum.`

Then we add to it all the elements of the vector using the `for` loop, which is a great tool for processing vectors. Take a look at the snippet in the editor.

Let’s talk about this example for a moment. The `i` variable will take the values `0`, `1`, `2`, `3`, and `4` subsequently and will index the `numbers` vector by selecting subsequent elements: the first, second, third, fourth and fifth. Each of these elements will be added by the `+=` operator to the `sum` variable, giving the final result at the end of the loop.

```cpp
#include <vector>

using namespace std;

vector<int> numbers(5);

for(int i = 0; i < 5; i++)
    numbers[i] = 2020;
```

The next task is to assign the same value (e.g. 2012) to all the elements of the vector.

Now let‘s try to rearrange the elements of the vector i.e. **reverse the order of the elements**: the first and the fifth as well as the second and fourth elements will be **swapped**. The third one will remain untouched.

**Question**: how can we swap the values of two variables? Let's look at the snippet in the editor - if we do something like this, we would lose the value we stored previously in `variable2`.

```cpp
int variable1 = 1, variable2 = 2;

variable2 = variable1;
variable1 = variable2;
```

Changing the order of the assignments won‘t help us either. Unfortunately, we need a third variable that serves as an auxiliary storage.

Look at the editor - this is how we do it.

```cpp
int variable1 = 1, variable2 = 2, auxiliary;

auxiliary = variable1;
variable1 = variable2; 
variable2 = auxiliary;
```

This is how we can utilize the presented receipt to reverse the whole 5 element vector. It works for sure, but we definitely do not like this (do you?). It’s acceptable with a vector of 5 elements, but try to image similar code operating on 99 elements - you wouldn't want to write it.

```cpp
/* swap elements #1 and #5 */
auxiliary  = numbers[0];
numbers[0] = numbers[4];
numbers[4] = auxiliary;

/* swap elements #2 and #4 */
auxiliary  = numbers[1];
numbers[1] = numbers[3];
numbers[3] = auxiliary;
```

```cpp
for(int i = 0; i < 2; i++) {
   auxiliary = numbers[i];
   numbers[i] = numbers[4 – i];
   numbers[4 – i] = auxiliary;
}
```

Let’s use the services of a `for` loop. Look carefully at how we manipulate the indices values.

During the first turn of the loop, the `i` variable will be equal to 0, so the instructions in the body will actually perform the following operations:

`auxiliary  = numbers[0];`

`numbers[0] = numbers[4];`

`numbers[4] = auxiliary;`

At the second turn, `i` will be equal to `1`, so:

`auxiliary  = numbers[1];`

`numbers[1] = numbers[3];`

`numbers[3] = auxiliary;`

As you can see, the loop does the same job by shortening the source code and making it more readable.

# **Vector initialization**

Defaultly, a newly created vector is filled with zeros. It's a good starting point for many of applications but sometimes you may want the vector to begin its live with a different set of values. Fortunately, you can initiate vectors, i.e. assign initial values to them at the time of declaration. We do this slightly differently than the initiation of scalars because we need to **specify more than one value**.

The syntax of a vector initiator is clear and legible. Imagine that we want to create an array where the value of any element is equal to its index. A suitable initiator would look like this:

`vector<int> int_vector = {0,1,2,3,4};`

As you can see, the vector initiator is simply a list of values enclosed inside **curly brackets**.

**Note**: using an initializer precludes the possibility of specifying the size of the vector as the compiler deduces vector's size from the initiator's length.

The equal sign (`=`) can be omitted so the following line is still valid and causes the same effect:

`vector<int> int_vector {0,1,2,3,4};`

If you provide neither the vector's size nor the initiator, the created vector will be of size `0`. Such a vector seems to be completely useless but it's only a guise - the vectors are able to change their size dynamically so there is no obstacle to make the vector more capacious in the future. This is how such a zero-length can be created:

`vector<int> int_vector;`

**TIME MACHINE** do końca!The old style vector declaration can use initiator too but its syntax is a bit different - look:

`int int_vector[5] = {0, 1, 2, 3, 4};`

If you provide fewer values than the size of a vector, like this, nothing bad will happen. The compiler determines that those elements you didn‘t specify any value to should be set to 0.

`int int_vector[5] = {0,1,2};`

If you provide more elements than can be stored in a vector, like this:

`int int_vector[5] = {0,1,2,3,4,5,6};`

it‘ll be an **error**. The compiler will be most dissatisfied.

One more example. Look at this:

`int int_vector[] = {0,1,2,3,4,5,6};`

We didn't specify the size of the vector but **provided an initiator**.

This is legal and it’ll force the compiler to assume that the size of the vector is the same as the length of the initiator.

# **Not only ints**

So far, we’ve discussed vectors whose elements are of type `int` only. Don't worry. You can also use **vectors of any other type**.

Let's assume that we've already included the `<vectors>` header file and the `using namespace` directive has been successfully issued. Having these two things done we can present you some examples.

This is an array in which you can store ten floating-point values.

`vector<float> float_vec(10);`

And you can store twenty characters here:

`vector<char> surname(20);`

...as well as the logical (Boolean) values:

`vector<bool> votes(100);`

Virtually every piece of data can be aggregated into a vector. Even a vector. We‘ll show you that soon.

**TIME MACHINE**The above declarations expressed in the older form would look like:

```cpp
float float_vec[10];
char surname[20];
bool votes[100];
```

We're sure that you're able to successfully switch between both forms of vector's declaration.

# **Not only vectors**

We’ve assumed thus far that vectors consist of scalars, but in fact, **vectors can contain elements of a much more complex structure**. Let’s consider the case when an **vector's elements are just vectors**. Such a construct isn't a vector any more - as it has more than one dimension (as vectors do) it becomes **an array**.

Surprising? Not at all! We often find arrays like this in our lives. Probably the best example of this is simply a chessboard.

What we’re going to say now will probably outrage experienced chess players, so we apologize in advance for all our simplifications and inaccuracies. If you’re a chess master... it’s nothing personal.

A chessboard is composed of **rows** and **columns**. There are 8 rows and 8 columns. Each column is marked with the letters **A** through **H**. Each row is marked with a number from **1** to **8**. The location of each square is identified by letter-digit pairs. Thus, we know that the bottom right corner of the board (the one with the white rook) is **A1**, while the opposite corner is **H8**

Let’s assume that we can use the selected integer values to represent any chess piece. We can also assume that every row on the chessboard is a... **vector**!

Let's try to declare it – here it is (assuming that we've already done what it takes):

`vector<int> row(8);`

Unfortunately, we have 8 of these rows. Does this mean that we have to declare 8 arrays like this?

`vector<int> row1(8), row2(8), row3(8), row4(8), row5(8), row6(8), row7(8), row8(8);`

Do you feel some sort of *déjà vu*? We’ve already gone through a similar dilemma, when we were trying to figure out the reason for using vectors.

A *chessboard* is in fact an 8-element array of elements as single rows. Let's summarize our observations:

- **elements of rows** are fields, 8 of them per row;
- **elements of the chessboard are rows**, 8 of them per chessboard.

We’re now ready to create an array for the chessboard – here’s the declaration:

`vector<vector<int>> chessboard(8, vector<int>(8));`

The chessboard variable is a **two dimensional array**. It’s also called, by analogy to algebraic terms, a **matrix**.

Let's analyze the declaration step-by-step:

- the declared variable is a **vector**;
- each of the vector's elements is another **vector** containing **integer values**;
- the declared variable's name is `chessboard`;
- the number `8` says that there is space for 8 vectors (but till now we know nothing about their sizes!);
- the inner declaration `vector<int>(8)` says that each of the inner vectors contains space for 8 integers.

**Note**: the matrix is initially filled with zeros (i.e. each of the 64 fields is set to zero during matrix creation).

To make the story more generic let us present the following case:

- we are going to declare a matrix consisting of ROWS rows;
- each of the rows contains COLS elementes of type TYPE.

The relevant declaration looks as follows:

```cpp
vector<vector<TYPE>> matrix(ROWS, vector<TYPE>(COLS));
```

**TIME MACHINE**Similar old-style declaration for the chessboard would look as follows:

```cpp
int chessboard[8][8];
```

Yes, it looks much, much simpler but the price we pay for the simplicity isn't worth the profits we can get from newer mechanisms.

A vector is one-dimensional structure so if you need to access any of its elements, you're obliged do provide exactly one index. A matrix (just like a chessboard) is a two-dimensional creation thus one index is not enough - you must use two indices to identify any of the elements:

- the first index selects the **row**;
- the second one selects the field number inside the row, which is *de facto* a **column number**.

Look at our chessboard. Every field contains a pair of indices which should be given in order to access the field's content.

Glancing at the figure here → we can set some chess pieces on our board. First, let's put all the rooks on the board:

`chessboard[0][0] = ROOK;`

`chessboard[0][7] = ROOK;`

`chessboard[7][0] = ROOK;`

`chessboard[7][7] = ROOK;`

If we wanted to place a knight on C4, we would do this as follows:

`chessboard[3][2] = KNIGHT;`

And now a pawn to E5:

`chessboard[4][4] = PAWN;`

As clear as check mate, right?

![https://edube.org/uploads/media/default/0001/01/3f7d44f733ea5ea6086466dcc26d3dc4f875206a.png](https://edube.org/uploads/media/default/0001/01/3f7d44f733ea5ea6086466dcc26d3dc4f875206a.png)

```cpp
vector<vector<float>> temp(31, vector<float>(24));
float sum = 0.0;

for (int day = 0; day < 31; day++)
  sum += temp[day][11];

float average = sum / 31;
cout << "Average temperature at noon: " << average << endl;
```

Now let's go deeper into the multi-dimensional nature of matrices. To find any element of a two-dimensional array, we have to use two “***coordinates***”: a vertical (row number) one and a **horizontal** (column number) one. Imagine that we develop a piece of software for an automatic weather station. The device records the air temperature on an hourly basis and does it throughout the month. This gives us a total of `24 * 31 = 744` values. Let's try to design an array capable of storing all these results.

First, we have to decide which data type would be adequate for this application. We think that a `float` would be the best, since our thermometer can measure the temperature with an accuracy of 0.1 degree Centigrade. Then we decide that the rows will record the readings every hour on the hour (so the row will have 24 elements) and each of the rows will be assigned to one day of the month (so we need 31 rows). Here’s the appropriate declaration:

`vector<vector<float>> temp(31, vector<float>(24));`

Now we’ll try to determine the monthly average noon temperature. We’ll add all 31 readings recorded at noon and divide the sum by 31. We assume that the midnight temperature is stored first. In the editor you can find the relevant code along with the necessary declarations.

**TIME MACHINE**

An old-style declaration causing the same effect looks as follows:

`float temp[31][24];`

Now let's find the highest temperature for the whole month – see the code in the editor.

```cpp
vector<vector<float>> temp(31, vector<float>(24));
float max = -100.0;

for (int day = 0; day < 31; day++)
  for (int hour = 0; hour < 24; hour++)
    if (temp[day][hour] > max)
      max = temp[day][hour];

cout << "The highest temperature was " << max << endl;
```

We want to count the days when the temperature at noon was at least 20C.

```cpp
vector<vector<float>> temp(31, vector<float>(24));
int hotdays = 0;

for (int day = 0; day < 31; day++)
  if (temp[day][11] >= 20.0)
    hotdays++;

cout << hotdays << " days were hot.";
```

We’re going to fill the entire array with zeros in order to prepare it for use in the coming month.

```cpp
vector<vector<float>> temp(31, vector<float>(24));

for (int d = 0; d < 31; d++)
  for (int h = 0; h < 24; h++)
    temp[d][h] = 0.0;
```

The C++ language **doesn’t limit the size of the array's dimensions**. Here we show an example of a 3-dimensional array (i.e. a vector of vectors of vectors).

Now imagine a hotel. It's a huge hotel consisting of three buildings, 15 floors each. There are 20 rooms on each floor. We need an array that can collect and process information on the number of guests registered in each room.

Step one – the type of the array's element. We think an `unsigned` would fit as there’s no such thing as a negative number of guests.

Step two – calm analysis of the situation. Summarize the available information: **3 towers, 15 floors, 20 rooms**.

Now we can write the declaration (look at the editor).

We agree that declarations like this need a lot of cold blood both to write and read (we're sure that the most cold blooded of the readers is the compiler). Don't panic, keep calm and let us to guide you through the dark sides of 3-dimensional declarations:

- let's start from the type: as it's a *"vector of vectors of vectors"* the corresponding part of the code seems to be obvious: it's `vector<vector<vector<int>>>`; (note how the nested parts of the clause reflects our verbally expressed idea);

- the right side of the declaration is a harder nut to crack but we aren't going to be intimidated (after all, we are no less smart than the compiler); let's start from the fact that the most nested element is a vector of 20 rooms - we marked in red; can you see it?
  
    vector<vector<vector<int>>> guests(3, vector<vector<int>>(15, vector<int>(20)));

- each of 20 room vectors is immersed inside a 15 floor tower - we marked the tower's part in blue:
  
    vector<vector<vector<int>>> guests(3, vector<vector<int>>(15, vector<int>(20)));

- as there are 3 towers the most outer part of the `guests` description looks like the fragment showed in green:
  
    vector<vector<vector<int>>> guests(3, vector<vector<int>>(15, vector<int>(20)));

The first index (0 through 2) selects one of the buildings; the second (0 through 14) selects the floor, the third (0 through 19) selects the room number.

Now we can book a room for two newlyweds: in the second building, on the tenth floor, room fourteen:

`guests[1][9][13] = 2;`

and release the second room on the fifth floor located in the first building:

`guests[0][4][1] = 0;`

Before we say goodbye and finish this part of our course, let's check if there are any vacancies on the fifteenth floor of the third building:

```cpp
int room;
int vacancy = 0;
for (room = 0; room < 20; room++)
  if (guests[2][14][room] == 0)
    vacancy++;
```

The `vacancy` variable contains `0` if all the rooms are occupied; otherwise it displays the number of available rooms.

**TIME MACHINE**

An equivalent old-style declaration would say:

```cpp
int guests[3][15][20];
```

```cpp
vector<vector<vector<int>>> guests(3, vector<vector<int>>(15, vector<int>(20)));
```

We have a feeling that you may want to ask us about a delicate issue: why we want you to use these complicated and winding vector declarations when the old-style vectors look so simple and tempting? How would you benefit from not to write something as simple as:

`int vect[10];`

but write that a bit mysterious phrase instead:

`vector<int> vect(10);`

which must be also accomplished with additional `#include <vector>` and `using namespace std;`? What's going on here? Where is the advantage of the new over the old?

The old-style vectors, matrices and arrays are stiff as a rock. Created once, they exist unchanged until the end of their existence. You can neither expand them to accommodate more data then you initially expected nor shrink them to release unneeded and wasted memory. If you're going to implement a vector with a variable content you have to do everything yourself: create a counter storing the actual number of elements (which has to be less than vector's size at every moment of the program execution), move some elements to the right when a new element is inserted into the vector and move them to the left when an existing element is removed from the vector (yes, we assume that vector's elements are deployed from left to right hence the direction of our moves).

Modern vector can do all these things for us themselves. Really.

But before we tell you about all these magical amenities he have to introduce you to the new world - world of methods. Not so far from here you will start your journey through the object oriented programming when you create your own classes equipped with properties and methods so we don't want to burden you with unnecessary (currently) details - there will be time for them soon. For now, we'll tell you that a **method** is a close relative of **function** but the way in which the method is invoked looks a bit different. Let's assume that there is a variable of type `float` and we want to find square root of the variable. This is how we do it:

```cpp
float value = 144;
float root = sqrt(value);  // 12.
```

Each vector has a method named `size` which provides you with current size of the subject vector. To obtain this information you need to invoke the method in the following way:

```cpp
vector<int> vect(10);
int current_size = vect.size(); // 10
```

Note: the method is invoked **from within** the vector! The vector (whose size is being determined by the invocation) is not **an argument** but a place where the method lives thus you have to invoke it in this distinctive way.

The power of the modern vectors (compared to old-style solutions) lies in the fact that they are equipped with a numerous methods what makes them elastic and flexible.

Let's take a look at some of these conveniences, but before we want you to analyze and run the code inside the editor. Thank you.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() 
{
    int elements = 10;
    vector<int> vect(elements);
    int current_size = vect.size();

    cout << current_size << endl;
}
```

### **console >_**

> 10

When a vector is brought to live using the old-fashioned declaration (like the one presented in the code window) there is no simple way to determine number of vector's elements - the `size()` method does not exist and cannot be invoked (try do it yourself!). One of possible tricks that can be used instead is to determine whole vector's size and to divide it by single element's size - this is how we do it!

Let's dive into more advanced modern vector's skills.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    int elements = 10;
    int vect[elements];
    int current_size = sizeof(vect) / sizeof(vect[0]);

    cout << current_size << endl;
}
```

### console>_

> `10`

Modern vectors can be freely expanded - the old ones can't. A method named `push_back(value)` is able to extend vector's size by one and to put a new value at vector's end. To make the sample more spectacular we set vector's initial size to zero and pushed back three values changing vector's size to 3.

**Note**: don't forget that the type of value being pushed back should be compatible with vector's elements type!

There are much more facilities that new style vectors provide and old one doesn't. We're not going to tell about them now as we prefer to do it later along with more advances topics. The more important factor is to convince you that modern vectors are worth using - their potential cannot be overrated.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() 
{
    vector<int> vect(0);

    vect.push_back(1);
    vect.push_back(-1);
    vect.push_back(0);
    cout << vect.size()  << endl;
    for(int i = 0; i < vect.size(); i++)
        cout << vect[i] << " ";
    cout << endl;
}
```

### console >_

> 3
> 1 -1 0

# **Structures – why do we need them?**

Before we start going on about structures, we need to tell you about a completely new type, named **string**. For now, we’re not going to tell you any more than what we use it for and how we operate on variables of this type. We promise we’ll give you more details in a separate section devoted exclusively to strings, and we’ll show you how to manipulate them and how to enjoy using them.

To be honest, a string is little more than a type, and all we want to tell you at this point is that variables of type `string` are able to store **strings of characters**, like surnames, family names, street names and all other names you can think of, including R2D2.

**Note**: if you want to utilize the `string` type in your code you've to ensure that:

- the `string` header file has been included i.e. your source file should contains directive: `#include <string>`
- the `using namespace std;` statement has been placed at the top of your code unless you agree to use prefix `std::` every time you make use of `string`.

Variables of type `string` may be assigned with the same operators as any other variable we’ve previously encountered. For example, if we want to store the name of our favourite dish in a string variable, we do it in the following way:

`string dish_to_order = "pizza";`

Imagine that we, the developers, have the following job to do: we’re obliged to design a data-base that can store information about students attending our course. It needs to store the name of each student, the time spent on studying the chapters and the number of the last completed chapter. We know that the total number of all students will not exceed 100,000. This leads us to write the following declaration:

`vector<string> student_name(100000);`

The array allows us to store up to 100,000 names.

Let's try to manipulate that array. For example, suppose that the first registered student was Mr. Bond (James Bond). Let’s store the information in our array:

`student_name[0] = "Bond";`

The time spent on the site will be stored as a float. This is not particularly convenient, but we can certainly handle it. The number of hours will be represented as a decimal fraction. This leads us directly to the following statement.

`vector<float> student_time_spent(100000);`

We know that Mr. Bond spent three hours and thirty minutes studying our course. We’ll denote it in the following way:

`student_time_spent[0] = 3.5;`

**Note**: 3h30m = three and a half hours, thus **3.5**.

The recent chapter number is obviously an `int`. This is the declaration we need:

`vector<int> student_recent_chapter(100000);`

Using some advances spying techniques we noticed that James finished his study at chapter number 7 (we don't write it as 007 as it would be an octal number what may introduce unnecessary confusion - sorry!). We record this fact using the following assignment:

`student_recent_chapter[0] = 7;`

```cpp
struct Student {
  string name;
  float time_spent;
  int recent_chapter;
};
```

The main issue here is that the data concerning the same object (a student) is **dispersed between three variables**, although it should logically exist as a consolidated unit. Handling multiple arrays is cumbersome and error-prone, and when life forces us to collect additional student's information (e.g. e-mail address) we’re going to need to declare another array and make a lot of other changes throughout the program. We don’t like it, and you can be sure you won't like it either.

We already know what a vector is. The vector is an aggregate of elements. The elements are numbered and are of the same type. Can we use **an aggregate whose elements could be of different types**? Could they be identified by names, not by numbers? And is it a good idea?

Yes, it's a great idea! This magical aggregate is called a **structure**.

A structure contains **any number of elements of any type**. Each of these elements is called a **field**. Each field is identified by its name, not by its number. Obviously, the field names must be **unique** and cannot be doubled within a single structure. We’ll show you how to declare a structure suitable for our needs and we’ll explain its meaning.

You can see the declaration of the structure in the editor.

- the declaration of the structure always starts with the keyword `struct`;
- there is a so-called struct tag after the keyword (`Student` in this case); it's the name of the structure itself; there is a widely accepted custom of composing structure tags starting with capital letter simply to distinguish them from ordinary variables;
- here comes the opening curly bracket – a sign that the field declaration begins at this point;
- our structure has three fields: the first is a `string` and is called `name`; the second is a `float` and is called `time_spent`; the third is an `int` and it’s called `recent_chapter`
- the declaration ends with the closing curly bracket followed by a semicolon.

We want to emphasize that the previous declaration doesn't create a variable, but only describes the structure we’re going to use in our program. If we want to declare a variable as a structure, we can do it in one of two possible ways:

`Student stdnt;`

`Student stdnt2;`

This declaration sets up two variables (**structured variables**) named `stdnt` and `stdnt2` respectively. The variables are of type `struct STUDENT` or just `STUDENT` (notice, that the structure declaration creates a new type name). We know that this variable consists of three named fields, but we don’t yet know how to access them.

As the C++ language offers a specialized indexing operator `[]` for arrays, it also gives us a so-called **selection operator** designed for structures and is denoted as a single character `.` (dot).

The priority of the selection operator is very high, equal to the priority of the `[]` operator.

This is a binary operator. Its left argument **must identify the structure** while the right argument must be the **name of the field** known in this structure.

The result of this operator is the selected field of structure, and therefore the expression containing this operator is sometimes called a **selector**.

This means that the selector here:

`stdnt.time_spent`

results in the selection of a field named `time_spent`. The type of this expression is the type of the selected field and this expression is an **l-value** (i.e. a value that can be put at the **left side of a assignment operator** `=`.

Consequently, you can use both of these selectors:

`stdnt.time_spent = 1.5;`

and

`float t = stdnt.time_spent;`

**TIME MACHINE**

Modern C++ treats structure's names in the same way as other types names (like the `Student` in our example) but there's also possibility (derived from C where it was the only method to name structured types) to use phrase `struct Student` as type's name. In effect, the following declaration is correct either, but - you will admit it, won't you? - definitely looks uglier:

`struct Student stdnt;`

Virtually any data could be used as a structure's field: scalars, vectors and other arrays and also almost all of the structures. We say “almost” because a **structure cannot be a field of itself**.

Structures can be aggregated inside a vector, so if we want to declare a vector consisting of `Student` structures, we do it in this way:

`vector<Student> stdnt(100000);`

Access to the selected fields requires two subsequent operations:

- in the first step, the `[]` operator indexes the vector in order to access the structure we need;
- in the second step, the selection operator selects the desired field.

This means that if we want to select the `time_spent` field of the fourth `stdnts`' element, we'll write it like this:

`stdnts[3].time_spent`

We’ve collected all these assignments which have been performed for the three separate arrays. Analyze them carefully:

`stndts[0].name = "Bond";`

`stndts[0].time_spent = 3.5;`

`stdnts[0].recent_chapter = 7;`

```cpp
struct Date {
    int year;
    int month;
    int day;
};
```

# **Declaring the structures**

For the purposes of further considerations we’ll use a simple structure designed to store the date. It’s equipped with three fields, each of type `int`, named `year`, `month` and `day`, which clearly denote their role and purpose.

The first possible way of declaring the structure is in the editor.

Of course, we can write this declaration much more compactly:

```cpp
struct Date {
    int year, month, day;
};
```

Both variants are equivalent.

That declaration doesn't create any new variables, but **only announces to the compiler** our intention to use this structure tag to declare new variables. The new variable would be declared, for example, in this way:

`Date DateOfBirth;`

We can use it to store Harry Potter's date of birth:

`DateOfBirth.year = 1980;`

`DateOfBirth.month = 7;`

`DateOfBirth.day = 31;`

We can also use the structure tag to declare an array of structures:

`vector<Date> visits(100);`

Accessing a single structure stored in the array is easy. If we want to modify the data of the first visit, we do this:

`Visits[0].year = 2020;`

`Visits[0].month = 1;`

`Visits[0].day =  1;`

It’s also possible to kill two birds with one stone by defining the structure tag and declaring any number of variables simultaneously in the same statement, like this:

```cpp
struct Date {
     int year, month, day;
} DateOfBirth, ExpirationDate, ETA;

Date current_date;
```

We can also omit the tag and declare the variables only:

```cpp
struct {
  int year, month, day;
}
the_date_of_the_end_of_the_world;
```

In this case, however, determining the type of the variable `the_date_of_the_end_of_the_world` becomes troublesome. To show you how it may reflect programmer's life let's take into consideration a very useful and meritorious operator named `sizeof()` (don't be misled - despite its appearance it's an operator, not a function!) which returns a number of bytes occupied by a variable or a type. E.g. the following line:

`cout << sizeof(char) << endl;`

will always print `1` - it's one fundamental axioms of both C and C++. If you want to get to know how many bytes you must to spend to store one date's data, you can obtain this information from the following expression:

`sizeof(Date)`

Without a struct you won't have such a possibility although you can use `the_date_of_the_end_of_the_world;` instead.

# **Structures – how do we use them?**

**A structure could be a field inside another structure**. Imagine that we have to extend our `Student` structure and add a field to save the date when a particular student last accessed the course. We can do it the way shown in the editor.

It means that we’ll have to use two subsequent selection operations to **go deeper** into the structure i.e. first we select a structure within the structure and then we select the desired field of the inner structure.

This is how it works:

`HarryPotter.last_visit.year = 2020;`

`HarryPotter.last_visit.month = 12;`

`HarryPotter.last_visit.day = 21;`

So now you should be able to answer the following question: when did Harry visit us recently?

```cpp
struct Student {
  string name;
  float time_spent;
  int recent_chapter;
  Date last_visit;
};

Student HarryPotter;
```

# **Structures – a few important rules**

A structure's field names may overlap with the tag names, and this is generally not considered a problem, although it may cause some difficulty in reading and understanding the program.

The snippet shown in the editor is completely correct.

```cpp
struct Struct {
  int Struct;
} Structure;

Structure.Struct = 0; // Struct is a field name here
```

It may be the case that the particular compiler you’re working with doesn't like it when a structure’s tag name overlaps with the variable's name (you know how those compilers are); – therefore, it's better to avoid tricks like the ones shown in the editor.

Alternatively, get yourself a new compiler – one that doesn’t complain so much. OK, just kidding.

```cpp
struct Str {
  int field;
} Structure;
int Str;

Structure.field = 0;
Str = 1; // works for us
```

Two structures **can contain fields with the same names** – the snippet in the editor is correct.

```cpp
struct S1 {
  int f1;
};

struct S2 {
  char f1;
};

S1 str1;
S2 str2;
str1.f1 = 32;
str2.f1 = str1.f1;
```

Structures can be initialized as early as **at the time of declaration**. The structure's initiator is enclosed in curly brackets and contains **a list of values assigned to the subsequent fields**, starting from the first.

The values listed in the initiator **must conform to the types** of the fields. If the initiator contains fewer elements than the number of the structure's fields, it’s presumed that the list is automatically extended with zeros. This also means that an empty structure initializer `{}` will zero all structure's fields. Keep in mind that zeroing may cause completely different effects depending on field's type - integers and floats will be actually zeroed while string fields will be assigned with an empty string (definitely not with a string `"0"`).

If the particular field is an array or a structure, it should have its own initiator, which is also subject to the rule of zero extension. If an “internal” initiator is complete, we can omit the surrounding curly parentheses.

Take a look at the example:

`struct Date moon_landing = { 1969, 7, 20 };`

This initiator is equivalent to the following sequence of assignments:

`date.year = 1969;`

`date.month = 7;`

`date.day = 20;`

And this is a sample initiator for the `Student` structure:

`Student he = { "Bond", 3.5, 4, {2020, 12, 21} };`

The initiator of this form is functionally equivalent to the following assignments:

`he.name = "Bond";`

`he.time_spent = 3.5;`

`he.recent_chapter = 4;`

`he.last_visit.year = 2012;`

`he.last_visit.month = 12;`

`he.last_visit.day = 21;`

Due to the completeness of the inner initializer, we can write the following, simplified form:

`Student he = { "Bond", 3.5, 4, 2012, 12, 21};`

This simplification (omitting the internal curly brackets) cannot be applied in the following case (although we must admin that such a way is not recommended and some compilers may emit a warning message here):

`Student she = { "Mata Hari", 12., 12, { 2012 }  };`

The internal initiator, referring to the `last_visit field`, doesn't cover all the fields. This means that it’ll be equivalent to the following sequence of assignments:

`she.name= "Mata Hari";`

`she.time_spent = 12.;`

`she.recent_chapter = 12;`

`she.last_visit.year = 2012;`

`she.last_visit.month = 0;`

`she.last_visit.day = 0;`

Let's see what happens when we apply an “empty” initializer:

`Student nobody = {};`

Here's the answer:

`nobody.name = "";`

`nobody.time = 0.0;`

`nobody.recent_chapter = 0;`

`nobody.last_visit.year = 0`

`nobody.last_visit.month = 0;`

`nobody.last_visit.day = 0;`

# **Congratulations! You have completed Module 2.**

Well done! You've reached the end of Module 2 and completed a major milestone in your C++ programming education. Here's a short summary of the objectives you've covered and got familiar with in Module 2:

- how to control the flow of the program;
- more data types;
- conditional instructions: if, else, switch;
- loops and controlling the loop execution;
- logic, bitwise and arithmetic operators;
- vectors, multidimensional arrays;
- declaring and initializing structures.

You are now ready to take the module quiz and attempt the final challenge: Module 2 Test, which will help you gauge what you've learned so far.

![https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png](https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png)