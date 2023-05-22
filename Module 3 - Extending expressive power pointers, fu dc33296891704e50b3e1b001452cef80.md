# Module 3 - Extending expressive power: pointers, functions, and memory

Class: C++
Created: June 22, 2022 12:05 PM
Reviewed: No
Type: Section

# ****C++ Essentials: Module 3****

## **In this module, you will learn about:**

- designing, declaring, and invoking functions;
- pointers;
- different methods of passing parameters and their purpose;
- default parameters;
- inline functions;
- overloaded functions;
- sorting;
- memory on demand.

![https://edube.org/uploads/media/default/0001/01/7fa113f23a9307c667a6e631747d1afba20f6a82.png](https://edube.org/uploads/media/default/0001/01/7fa113f23a9307c667a6e631747d1afba20f6a82.png)

# **Pointers – the absolute basics**

**Pointers** are also **values**, but different from those we‘ve been using so far. The types we’ve been using are closely linked to computer data processing, but fully reflect our ideas and intuition. We use *floats* in everyday life when we pay for something and *ints* when we count something. Pointers have no simple and obvious analogy to our daily lives and their values are unreadable to humans and completely useless. Computers, however, can make great use of pointers, giving developers powerful options when designing algorithms and data structures.

Now, be prepared for the fact that not everything will be immediately obvious to you. This is normal – it’ll take some time before you can understand the pointers themselves and their specific traits.

![https://edube.org/uploads/media/default/0001/01/7a7aa5f9c967ceb485ed89eb7feda0401edf0e7a.png](https://edube.org/uploads/media/default/0001/01/7a7aa5f9c967ceb485ed89eb7feda0401edf0e7a.png)

Modern computer memories are large and fast. You probably already know that memory size is expressed in units called bytes. You probably also know that when you declare any variable, the variable occupies a small piece of the computer memory. So far, it’s been important for us to know what value is stored in the variable. From now on, we are also going to be interested in where this value is stored.

This trait of the data (to say it more formally, this **attribute**) is often called the **address**. We all live at certain addresses just like every variable “lives” at its address, too.

Try to see this important difference:

- the **value** of the variable is what the variable stores;
- the **address** of the variable is information about where this variable is placed (where it *lives*).

**Pointers are used to store information about the location (address) of any other data**. We can say that pointers are like **signposts**. They don’t say anything about the place itself, but they show us clearly how to reach it.

`int i;`

![https://edube.org/uploads/media/default/0001/01/d823427d8c111acb1a36971ff8ec08bed5bfa3b0.png](https://edube.org/uploads/media/default/0001/01/d823427d8c111acb1a36971ff8ec08bed5bfa3b0.png)

# **The first pointer**

Let's start off with a simple declaration and an equally simple operation. We’re going to encounter a few new operators, too. Already at the time of declaration, we can see the difference between regular data types and pointer types. Take a look:

`int *p;`

We use the asterisk (“`*`”) here in a completely new way. It has nothing to do with multiplication. You may be feeling a bit confused by this, but don’t worry.

This dual nature of asterisks will become clear soon enough. The C++ language syntax ensures that you'll always be able to figure out what meaning the asterisk is being used for in any particular context. This declaration sets up a variable named `p`. It isn't an `int` - the asterisk means that `p` is a **pointer** and will be used to **store information about the location** of the data of type `int`. The pointers are always used to point to the specific data referred to in the declaration. The C++ language may use so-called **amorphous pointers**, too, which can be used to point to any data of any type, but we’re going to discuss them at the very end of our story.

What is the type of variable `p`? There are a few answers, identical in meaning, but considerably different. First, we can say that `p` is a variable of type “*pointer to int*”. Secondly, it would be as follows: *p is a variable of type int ** where “`*`” reads simply as “*asterisk*”.

# **How do we assign a value?**

**How do we assign a value to the pointer variable?**

Can we assign a value to the pointer? Of course, in the same way that you can assign any value to any other variable: by using the `=` operator. A more important question is which values are we allowed to assign to the pointers?

Using a literal is **not an option**. The compiler won’t allow you to write something like this (look at the line of code below) because, firstly, the C++ language syntax doesn’t allow it and secondly, if you know what’s stored in the computer's memory at the address `148324`, then you’re a clairvoyant and computer programming is just a waste of your time.

`p = 148324;`

There’s one distinctive exception. You can assign **zero** to the pointer variable. Doing this doesn’t prompt any questions from the compiler.

`p = 0;`

A pointer which is assigned a value of zero is called a **null pointer** (as in Latin, *nullus* – none). It doesn’t point to anything. It's like a signpost with all the writing removed. It still exists, but with no purpose to the traveler. Despite appearances, this pointer can be very useful and sometimes even necessary.

Due to the fact that assigning a value of zero to a pointer variable sometimes causes misunderstandings and mistakes (some may confuse the pointer with a variable of type `int`), there’s an unwritten agreement that developers will avoid assigning null pointers. Instead, they should follow this next convention:

`p = nullptr;`

The `nullptr` symbol is actually an incarnation of empty (null) pointer. It looks like a variable but you cannot modify its value so it can be called a **constant**.

Don't forget `nullptr` must be assigned only to pointers. Compiler will be very strict with this.

**TIME MACHINE**

Older C++ standards used different (derived from the C language) way of notating null pointers - it was done by a word (actually a macro, i.e. a symbol implicitly replaced by the compiler to integer zero) `NULL`. You can find traces of this practice in older C++ code - don't imitate this manner! There is one more caveat also: using the `NULL` symbol requires **including the header file** named `cstring`, or any other header file which includes `cstring` itself (one of them is `iostream`).

How do we assign any meaningful value other than `nullptr` to a pointer variable? We may assign to the pointer a value which **points to any already existing variable**.

To do that, we need an `&` operator, called the **reference operator**. This is a unary prefix operator.

The operator simply finds the address of its argument. See the statement:

`p = &i;`

After completing the assignment, the `p` variable will point to the place where the `i` variable is stored in the memory.

This can be shown in the following way:

![https://edube.org/uploads/media/default/0001/01/ef4709f5e2ed673976663ab929b4e58eb561b639.png](https://edube.org/uploads/media/default/0001/01/ef4709f5e2ed673976663ab929b4e58eb561b639.png)

**UWAGA - tu brakuje obrazka, o którym mowa w tekście!**

If you assign `nullptr` to the pointer, it’ll look like this. From now on, the `p` pointer points to neither the `i` variable nor to any other variable.

We’ll use the following symbols to express this. As you can see, the `p` pointer is **grounded**.

What can we do with a pointer that is not null and points to a value? We can *dereference* it.

Dereferencing is an operation by which the pointer variable becomes **synonymous** with the value it points to. As we’ll see later, it can be not only a variable, but also an expression that yields a pointer).

Look at how we can declare a variable of type `int` (`ivar`) and a variable of type `int *` (`ptr`). We can do it within a single statement:

`int ivar, *ptr;`

Now let’s assign the value of 2 to the `ivar` variable – everything’s clear so far, right?

`ivar = 2;`

Now we make the `ptr` pointer point to the `ivar` variable.

`ptr = &ivar;`

How do we get a value pointed to by the pointer? We have to use a well-known operator (the asterisk: “`*`”) but in a completely new way – as a **dereferencer**.

If you place an asterisk in front of a pointer, you **get a value which is stored at the location pointed to by the pointer**.

- *`ptr`

The following invocation will display `2` on the screen, as the **dereferenced `ptr` value** is sent to `cout` (note: `ptr` points to `ivar` and `ivar` is equal to `2`).

`cout << *ptr;`

If you write a statement like the one here:

- *`ptr = 4`

you **won't change the pointer value**. You’ll instead change the value pointed to by the pointer. This is an important difference.

Don't forget that if you declare a pointer in the following way:

`ANY_TYPE *pointer;`

it means that:

- the `pointer` variable is of type `ANY_TYPE*`
- the *``pointer expression is of type `ANY_TYPE`

Notice the place the asterisk occupies in both cases.

Also, don't forget that **dereferencing `nullptr` pointers** is **strictly forbidden** and leads to serious problems very quickly.

# **sizeof operator**

The `sizeof` operator is distinguished by its appearance. The operators we’ve encountered so far are coded as single characters or digraphs. This new operator looks like a variable.

Don't be misled: this is a **unary prefix operator** and with the highest possible priority. There’s another difference too: a typical operator requires a value as its argument and usually changes the value in certain ways.

The new operator expects that its argument is a **literal**, or a **variable**, or an **expression** enclosed in parentheses, or the **type name**.

The operator provides information on **how many bytes of memory its argument occupies** (or may occupy). The name explains the purpose – here it is:

`sizeof`

Note: there’s no space between “*size*” and “*of*”.

The `sizeof` is not only an operator – it’s also a **keyword**.

`i = sizeof(char);`

Variable `i` will be assigned the value of `1`, because `char` values always occupy one byte. Note that we can achieve the same effect by writing:

`char c;`

`int i = sizeof c;`

You may not use parentheses when the argument is a literal or a value, but you must use them when the argument is a type.

Variable `i` will be set to the value of 8 if your platform uses 64-bit long addresses and 4 if it operates with 32-bit long addresses. It's unlikely that you encounter value less than 4 here although, of course, 16-bit long addresses were in common use not so long ago.

`int *ptr = nullptr;`

`int i = sizeof ptr;`

Variable `j` will be always set to the value of `8` as `double` values occupy 64 bits according to IEEE-754 rules.

`int j = sizeof 3.1415;`

The following example is not so obvious.

Values of the `int` type occupy 32 bits, i.e. 4 bytes in most modern compilers/computers, **but we cannot guarantee** that this is true in all cases.

`int k = sizeof k;`

We think it would be a good exercise for you to compile and run the following program on your computer. By doing this, you’ll learn **how your computer and compiler use the memory**.

The program is perhaps a bit simplistic, but its role is to identify interesting features of your environment, and it’s good enough for this.

```cpp
#include <iostream>

using namespace std;

int main() 
{
  cout << "This computing environment uses:" << endl;
  cout << sizeof(char) << " byte for chars" << endl;
  cout << sizeof(short int) << " bytes for shorts" << endl;
  cout << sizeof(int) << " bytes for ints" << endl;
  cout << sizeof(long int) << " bytes for longs" << endl;
  cout << sizeof(float) << " bytes for floats" << endl;
  cout << sizeof(double) << " bytes for doubles" << endl;
  cout << sizeof(bool) << " byte for bools" << endl;
  cout << sizeof(int *) << " bytes for pointers" << endl;
}
```

### console >_

> This computing environment uses:
> 1 byte for chars
> 2 bytes for shorts
> 4 bytes for ints
> 8 bytes for longs
> 4 bytes for floats
> 8 bytes for doubles
> 1 byte for bools
> 8 bytes for pointers

# **Pointers vs. vectors**

What do **pointers and vectors** have in common?

Well, a lot. Let's start with an important fact: a vector's method named `data()` returns a pointer pointing to the **first element of the vector**.

How does it work?

We’ve declared the three-element vector of type `int` (named `vect`) and a pointer to `int` (named `ptr`) initially set to a value associated with a very first element of the vector.

`vector<int> vect {1, 2, 3};`

`int *ptr = vect.data();`

The same effect can be achieved by applying the `&` operator to `vect[0]`.

`int *ptr = &vect[0];`

This figure illustrates the effect of the both assignments.

![https://edube.org/uploads/media/default/0001/01/30423016456448f240597045d501267700d3aa69.png](https://edube.org/uploads/media/default/0001/01/30423016456448f240597045d501267700d3aa69.png)

The following code outputs `1` proving the fact that `ptr` and `ptr2` point to the same location inside memory - the first vector's element:

```cpp
#include 

#include 

using namespace std;

int main() 
{
    std::vector vect {1, 2, 3};

    int *ptr = vect.data();
    int *ptr2 = &vect[0];
    cout << (ptr == ptr2) << endl;
}
```

# **The arithmetic of pointers**

TThe pointers' arithmetic is significantly different from the integers' arithmetic as it is relatively reduced and allows the following operations only:

- **adding an integer** value to a pointer, giving a pointer (*ptr + int → ptr*);
- **subtracting an integer** value from a pointer, giving a pointer (*ptr – int → ptr*);
- **subtracting a pointer from a pointer**, giving an integer (*ptr – ptr → int*);
- **comparing the two pointers** for equality or inequality (this gives a value of type `int` of either `true` or `false`) (*ptr == ptr → int; ptr != ptr → int*).

Any other operations are either prohibited or meaningless and only the ones mentioned above may be used.

Let’s discuss briefly what’s happening to a pointer subjected to these operations. We’ll do this by assuming the declarations and assignments shown in the editor.

At this point, `ptr1` points to the first element of `array`.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() 
{
    vector<int> array {1, 2, 3};
    int *ptr1 = array.data();
    int *ptr2;
    int i;

    // to be continued
}
```

After the following assignment, `ptr2` **points to the first element of `array`**, too – the figure shows the current state of the variables.

![https://edube.org/uploads/media/default/0001/01/a3346f0156f4b1dd04778eb8ab8fcad285794891.png](https://edube.org/uploads/media/default/0001/01/a3346f0156f4b1dd04778eb8ab8fcad285794891.png)

We can check if the two pointers are equal – yes, they are, as they point to the same element of the `array`.

`if(ptr2 == ptr1) {`

`:`

`:`

`}`

Let's check **how the addition works**. These statements do the same operation: they add `1` to `ptr2`.

We can interpret this operation as follows:

- it’s taken into account what type is pointed to by the pointer - in our example it’s `int`;
- it has determined **how many bytes of memory the type occupies** (the `sizeof` operator is used automatically for that purpose) – in our case it’s `sizeof` (`int`);
- the value we want to add to the pointer is multiplied by the given size;
- the address which is stored in the pointer is **increased** by the resulting product.

In effect, the pointer moves itself to the next `int` value in the memory.

The effect of this incrementation is shown in the figure.

![https://edube.org/uploads/media/default/0001/01/73f83a730d71635f80b6f85f2425566d1a67c96f.png](https://edube.org/uploads/media/default/0001/01/73f83a730d71635f80b6f85f2425566d1a67c96f.png)

What would happen if we added `2` instead of `1`?

In this case the `ptr2` would be increased by (`2 * sizeof (int)`) and thus `ptr2` would move through **two** `int` values and would point to the third element of the array (namely, `array[2]`).

The comparison

`ptr1 == ptr2`

is obviously false, while this one

`ptr1 != ptr2`

is true, as the addresses the pointers point to differ.

Now let's subtract the pointers in the following way:

We said earlier that subtraction gives a result of type `int`. How is it calculated?

- taken into account: the type to which the pointers point (`int`); this means that both pointers need to point to the same type; the compiler will check it;
- the addresses stored in the pointers are subtracted;
- the result of the subtraction is divided by the size of the type pointed to by the pointers.

The final result tells us how many variables of a given type (i.e. `int`) fit between the addresses stored in the pointers. In our case, it’s obviously `1`, and this value will be assigned to the `i` variable.

`i = ptr2 - ptr1;`

The result will be greater than `0` if `ptr2` points to the memory located after `ptr1`; otherwise, it’ll be less than `0`.

Try to guess the result of the following operation:

`ptr1 = ptr1 + 2;`

You can find the answer below:

![https://edube.org/uploads/media/default/0001/01/f8164d4fe4826806eaaa2210141e82d914450c1e.png](https://edube.org/uploads/media/default/0001/01/f8164d4fe4826806eaaa2210141e82d914450c1e.png)

Let’s assume that the following operation has been performed. Can you guess the effect?

`ptr2 = ptr2 - 1;`

Here’s the answer:

![https://edube.org/uploads/media/default/0001/01/c7c0a3e663d2b7a36d1d4037bcdf23dc577bb46b.png](https://edube.org/uploads/media/default/0001/01/c7c0a3e663d2b7a36d1d4037bcdf23dc577bb46b.png)

Try to determine the result of the following subtraction.

`ptr1 - ptr2`

Is it `2`?

Yes, it is.

Congratulations!

*OK*, you may say, *It's so thrilling what I'm reading, but where's the similarity between vectors and pointers?* That's very important question and we're in a hurry to explain this. The crux of the matter is that pointers can sometime behave like vectors and vice versa. Let's assume that the `ptr1` pointer points to the second element of the `array` vector. We want to dereference it and to fetch the value residing at address the pointer currently contains. We can do it in the following way:

`int value = *ptr1;`

It's clear, isn't it? So let us raise the bar a bit. We want to dereference the value located one element after the current pointer indication. **Note**: we don't want the pointer to be modified! How to do it? This is how:

`value = *(ptr1 + 1);`

The parentheses surrounding expression are obligatory and you must not omit them unless you want to get value pointed by `ptr1` increased by 1 - it's because the `*` working as dereferencer has higher priority that `+`.

What we are going to tell you now may surprise you. Are you ready?

**The C++ language assumes that the operation described as:**

- `*(pointer + offset)`

**is a synonym of:**

`pointer[offset]`

This means that our previous assignment can be rewritten as:

`value = ptr1[1];`

Can you see the similarity to vector's behavior now? To amaze you even more we'll tell you that using negative indices is also possible but only for pointers - vectors won't forgive you such an extravagance.

Take a look at the following code and try to predict its output:

```cpp
#include <vector>
#include <iostream>

using namespace std;

int main()
{
    vector<int> numbers {1, 2, 3};
    int *ptr = numbers.data() + 1;

    ptr[-1] = *ptr + ptr[1];

    cout << numbers[0] << endl;
}
```

### check

> It's 5. The result origins from the followings operations:
> initial ptr's value points to numbers[1];
> ptr[-1] points to numbers[0];
> ptr[1] points to numbers[2];
> As our crucial assignment can be rewritten as:
> *(ptr - 1) = *ptr + *(ptr + 1);
> and taking into consideration current ptr value we see that it's an equivalent of:
> numbers[0] = numbers[1] + numbers[2];

We hope that complicated relation between pointers and vectors looks clearer now, doesn't it?

# **What is a function?**

The word "**function**" is probably not so alien to you. Certainly, you’ll have heard it many times before, even in circumstances that had nothing to do with programming.

We can bet that you’ve met this word in a math class. Do you remember? Sine is just one of the many examples.

A function is a kind of box (not always black) that can do something useful for us, e.g. to evaluate a value or perform some actions. The former means that a function has (or may have) **a result**. The latter means that a function has (or may have) **an effect**.

In other words, a function is just a **separate part of a code** that can be used at (almost) any time to evaluate something, to do something, or both. **We identify a function by its name**.

The name of a function is subject to the same restrictions as a variable's name. Additionally, we can’t have a variable and a function of the same name.

![https://edube.org/uploads/media/default/0001/01/0077212ccd46919ef82b9a341e62847bda1a9fd7.png](https://edube.org/uploads/media/default/0001/01/0077212ccd46919ef82b9a341e62847bda1a9fd7.png)

Every function is able to modify its own behaviour using **parameters** (do you remember? The `sine` function has one parameter, too). Parameters may affect what is calculated or what is performed inside the function. Moreover, a function may modify its parameter's values if necessary.

When you want a particular function to perform its actions and/or evaluations, you need to **invoke** it.

The **function invocation** is a special instruction in the C++ language. The invocation has to specify the name of the function being invoked (always), the parameters that the function should use (if needed) and how to use the result evaluated by the function (if any).

There’s one catch: you shouldn't invoke a function that is unknown to the compiler. The compiler needs to be aware of the function's nature (name, parameters, result) and there are some ways to inform the compiler about all the functions you may want to use.

In general, we can divide functions into two groups:

- functions written by someone else (not you) which are made available by the environment, sometimes called **predefined** or **library functions**
- functions written by you

You can use both of them equally easily.

# **Why do we need functions?**

Functions facilitate the creation of programs in multiple ways. We can say that it’s nearly impossible to write a large, complex program without using functions. Even if it succeeds, it won’t be a piece of good software for many reasons.

Library functions are the first functions a novice developer uses, but it very soon becomes clear that they’re never sufficient for solving complicated problems. This is the moment when the developer decides to write his/her own functions.

Don't forget: it’s always better to ensure that the function you need is really worth being implemented from scratch. **It’s always a good idea to check if the function you want hasn’t already been written by someone else**, so as to avoid reinventing the wheel and to break wide open door.

Functions enable developers to divide a problem (and also a code) into smaller parts. A smaller code is easier to write, to test, to maintain and to understand.

Having a set of well written and well tested functions lets the developer construct the code in a way that’s similar to house building: using ready-made blocks. This method of dividing the problem is known as **decomposition**.

In general, there are two possible approaches you can use during decomposition:

- the **top-down** approach (when you try to define the most general functions first and then you divide them into simpler and more specialized ones);
- the **bottom-up** approach (when you start your work by creating a set of narrowly defined and highly specialized functions, and then assembling them into more complex structures).

Experienced developers know that creating functions is always a good idea even if the new function is invoked only once during the program's execution. If the code you’ve written is too long to fit on one screen, consider dividing it into functions.

It's easier to control a herd of small and well-defined functions than one large portion of code that you can't see at a glance.

# **Introduction to functions**

Each function is characterized by the following traits:

- name
- parameters
- type of result

The part of the code that specifies all these elements is known as the **function declaration**. The compiler must know the function declaration to enable it to properly interpret the invocations of the function. The function declaration is sometimes called the **function prototype**.

A function declaration says nothing about what the function does exactly. That information is provided by the function body, which is a separate part of the code, enclosed in brackets.

A function declaration enriched with a function body forms the so-called **function definition**.

Imagine that we need a function that can evaluate the second power of any `float` number.

We realize that:

- `square` would be quite a good name for the function; of course, we can call it in many different ways, e.g. `sqr`, `SecondPowerOf` or even `JohnDoe` (although it’s probably not a good idea, is it?)
- functions need one parameter: the value which will be raised to the power of 2; `x` will be a good name for the parameter, although not very original;
- the result type is `float` (like the parameter)

We can write the function declaration now. You can see it here:

`float square(float x);`

Note that the first `float` specifies the type of the result, while the second is the type of the parameter.

# **First function**

If we want to take advantage of this function, we need to **deliver its definition**. You can see it in the editor.

Note: transforming a declaration into a definition requires us to add a body, but the body also replaces the semicolon that ends the declaration (see previous slide). The function body doesn't end with a semicolon.

```cpp
float square(float x)
{
  float result = x * x;

  return result;
}
```

The body contains:

- a declaration of the `result` variable; the variable will be used **inside the function and only inside the function**; it’s neither visible nor accessible in any other part of your code;
- the `result` variable is initially assigned with the value of the `x` parameter multiplied by itself; this is the simplest and fastest method of raising a number to the power of 2;
- the last instruction of the `square` function is `return`; this instruction is responsible for two important actions:
  1. it indicates **which value is returned** (provided) as the function result
  2. it **terminates the execution** of the function

**Note**: we always try not to leave declarations without initializations inside out code. This is why we set the value to the `result` variable as quickly as possible i.e. in the moment of declaration.

We’re now going to make use of our first function and make it a part of a complete, runnable program. Here it is in the editor.

The parameters defined within the function are called **formal parameters**. The values actually transferred to the function (thus existing outside the function) are called **actual parameters** or **arguments**.

The function invocation is just the name of the function being invoked along with the values transferred (passed) into the function as arguments.

As you can see, we’ve declared a variable named `arg` and assigned it the value of 2.0. Next, we’ve invoked the `square()` function, delivering the `arg` variable as its argument (the actual parameter).

```cpp
#include <iostream>

using namespace std;

float square(float x) 
{
  float result = x * x;

  return result;
}

int main() 
{
  float arg = 2.0;

  cout << "The second power of " << arg << " is " << square(arg) << endl;
}
```

### Console >_

> `The second power of 2 is 4`

The result of the function is then sent to the screen and displayed as part of the message saying “`The second power of 2 is 4`”.

Is it possible to place the `square` function **after** the `main` function and not **before**? Yes, it is, but don't forget that the compiler must be aware of all the traits of the invoked function.

Therefore, you have to put the function declaration **before the first function invocation**.

Take a look at the modified code in the editor.

**Note**: you can omit the formal parameter's name in the function prototype.

You’re now ready to learn about some of the more advanced properties of functions.

```cpp
#include <iostream>

using namespace std;

float square(float);

int main() 
{
  float arg = 2.0;

  cout << "The second power of " << arg << " is " << square(arg) << endl;
}

float square(float x) 
{
  float result = x * x;

  return result;
}
```

### Console >_

> `The second power of 2 is 4`

# **Declaring functions**

A function declaration is intended to inform a compiler about the **function's name**, its **return type** and **type of the parameters** (if any). A general form of function declaration (or function prototype – we can use these terms interchangeably) is here:`return_type function_name(parameter_list);`

- `return_type` describes the **type of result returned (delivered) by the function** (e.g. we expect that the `sine` function will return a value of type `float` as `int` data is completely unusable in this context); you can use any of the C++ types as a `return_type`, including a very special type named `void`; a function of type `void` returns no result at all; we can say that such a function may have an effect but definitely has no result;
- `function_name` is an identifier which **names the function and distinguishes it from all other functions** (note: you can have more than one function of the same name, in contrast to variables; this is called **overloading** and we’re going to tell you about it soon);
- `parameters_list` (you have to enclose this one in parentheses!) is a comma-separated list of “type name” pairs, where each of the `names` may be omitted; the list may be empty (this means that the function accepts no arguments at all) but the parentheses must still be there.

**TIME MACHINE**

Older C++ standards used a special from of emphasizing the fact that the function has no parameters by putting the word `void` inside the parentheses, like this:

`void fun(void);`

This style of declaration is now considered obsolete and is not recommended but you can encounter such a phrase in older C++/C programs.

Assuming that we need a function named `fun` which return `int` as a result and has one parameter of type `int`, we can express it using two following equivalent declarations:

`int func(int number);`

`int func(int);`

- In this context, the name of the parameter (`number`) means nothing to the compiler and it completely ignores it; it's not an argument against specifying the parameter's name in the declarations as it could be very useful for people trying to understand your code;
- The declaration ends with a semicolon which must not be omitted.

Although each of the elements of the parameter list resembles the syntax of a variable declaration, **you're not allowed to declare more than one parameter name at the same time**. You can do this:

`int x, y;`

but you have to use the following verbose form if you declare two (or more) function parameters:

`void fun(int x, int y);`

# **Defining functions**

A function definition specifies the code to be executed on each function invocation. It differs from the declaration in the fact that a **semicolon is replaced by a body containing a sequence of declarations and/or instructions.**

A function definition specifies the code to be executed on each function invocation. It differs from the declaration in the fact that a **semicolon is replaced by a body containing a sequence of declarations and/or instructions.**

**If the `return_type` is void, the body may not contain the `return` instruction**, but if it’s used anyway, it has to have the following form:

`return;`

or (what may sound weird for you) the `return's` expression must be of type `void` (e.g. it may be a void function invocation).

It’s assumed that **the `return` statement is implicitly executed within the `void` function's body** just before the closing bracket. You don't have to write it there explicitly.

If the `return_type` is not `void`, the body must contain at least one `return` statement specifying the value of the function's result. You can’t leave a function's body without specifying the result's value.

Any value you intend the function body to return must have a type compatible with the type specified as the function type.

You can use **as many `return` statements as you need** to effectively implement your algorithm.

# **Example functions**

Let's assume that we need a highly specialized function to greet a user who’s dared to run our program.

We choose “Greet” as the name for that function, and decide that the new function should have no result and no parameters.

You can see the definition of the `greet()` function in the editor.

```cpp
void greet() 
{
  cout << "Ave user!" << endl;
}
```

# **Example functions**

Some users (those with very big egos) need to be greeted more than once. To avoid writing separate functions for different categories of users, we’ll write a universal function that can be instructed on **how many times the greetings should be shouted out**. We’ll use a parameter of type `int` for this purpose.

The function is ready. You can see it in the editor.

As you can see, we’ve made use of a previously defined function. In this way, if we changed the text of the greeting (e.g. to “`I'm ready to serve you, my Master`”), it would have an effect on both functions.

Now pay attention to what the function invocation looks like in the code. We’ve had to use a pair of parentheses, even though we haven’t specified an argument.

Also note how we named the function or, rather, how we glued all the words together using the underscore character (`_`) which mimics a space well enough and let us build complex and meaningful names.

```cpp
void greet_many_times(int how_many_times) 
{
    while (how_many_times > 0) {
        greet();
        how_many_times--;
    }
}
```

# **Example functions**

Now we’re going to show you a complete program demonstrating the functioning of our functions. The program asks a user for the size of his/her ego and responds with an adequate greeting. The size of the ego is measured in kilometers (apologies to all users of imperial units).

Look at how we send the argument value to the invoked function. Try to imagine how the argument replaces a parameter within a function.

The user gets one greet per kilometer and one extra greet (for those with no ego).

```cpp
#include <iostream>

using namespace std;

void greet() 
{
    cout << "Ave user!" << endl;
}

void greet_many_times(int how_many_times) 
{
    while (how_many_times > 0) {
        greet();
        how_many_times--;
    }
}

int main() 
{
    int size_of_ego;

    cout << "How big is your ego? [km]" << endl;
    cin >> size_of_ego;
    greet_many_times(1 + size_of_ego);
}
```

### Console >_

> `How big is your ego? [km]`

# **Example functions**

Let’s look at a more serious function now. Its task is to convert a temperature value expressed in Fahrenheit to Celsius.

As you might know, the formula says that:

`[°C] = ([°F] − 32) × 5 ⁄ 9`

We’ve embedded the formula inside the `fahrenheit_to_celsius()` function.

We are going to test our function by forcing it to evaluate results for some characteristic values. We’ll do this by using the `test_the_function()` function, which is designed to produce clear and legible output allowing testers (us) to check the correctness of the function.

The complete code is in the editor.

We expect the program to produce the following output:

```
Fahrenheit 32 corresponds to 0 Centigrade
Fahrenheit 212 corresponds to 100 Centigrade
Fahrenheit 451 corresponds to 232.778 Centigrade
```

                                                                                                                                                    **output**

```cpp
#include <iostream>

using namespace std;

float fahrenheit_to_celsius(float temp) 
{
      return ((temp - 32.0) * 5.0) / 9.0;
}

void test_the_function(float temp) 
{
      cout << "Fahrenheit " << temp << " corresponds to ";
      cout <<    fahrenheit_to_celsius(temp) << " Centigrade" << endl;
}

int main() 
{
    test_the_function(32.0);
    test_the_function(212.0);
    test_the_function(451.0);
}
```

### Console >_

> Fahrenheit 32 corresponds to 0 Centigrade
> Fahrenheit 212 corresponds to 100 Centigrade
> Fahrenheit 451 corresponds to 232.778 Centigrade

# **The invocation syntax - supplement**

As you already know, a function may:

- **return a value** when it has a **non-void** type name in front; such a function has a **result** and may have an **effect**, too;
- **return nothing** when the `void` keyword is in front of its name; such a function **doesn't have a result** and we can expect that it has an **effect**.

We've mentioned that these two kinds of functions differ in the way they use the `return` statement, but there is also another difference regarding invocations.

Let's assume that we have two functions, schematically shown below:

`void void_function(int par){...; return;}`

`int non_void_function(int par){...; return par * par;}`

Note that:

- the only acceptable form of the `void_function` invocation looks like this:`void_function(2);`
- the `non_void_function` can be invoked in the following two ways:`value = non_void_function(2);
  non_void_function(2);`

It means that any non-void function's result may be **honoured** by the invoker (the former) and assigned to a variable, or used in any other way, or may be **ignored** by the invoker (the latter) and just forgotten immediately after the return from the function.

# **Side effects**

Any function needs to have the ability to communicate with its environment. It must be able to receive data (numbers, texts, etc.), process it and share the results. We already know two kinds of communication like this:

- **transferring data to a function using arguments** whose values are assigned to function parameters;
- **transferring data from a function using the function's result**; note that only one value may be transferred by such means because the syntax of the `return` statement allows you to specify only one value; fortunately, this limitation can be easily bypassed e.g. when the function's result is a structure.

Any variable defined inside the function's body **can be neither used nor accessed from outside the function**. We can say that variables are **isolated from the outer world**. Moreover, such variables exist only when the function is executed and disappear when the function completes its execution. This means they cannot be used to store value between function invocations.

Variables of this kind are named **local variables**.

Furthermore, there is a special kind of variables called a **global variables**.

Global variables are declared **outside any function** and thus are accessible for all the functions declared in the same source file.

Note that the variable declaration has to **precede** the function definition in order to be recognizable by the function.

**Global variables allow functions to get and to provide data of any kind**. If a function modifies any global variable that isn’t using any other mechanism of transferring data, we say that this function has a **side effect**.

Side effects, although useful sometimes, are not recommended and are considered a sign of bad programming style because they make the code difficult to understand.

Take a look at the code in the editor.

The `globvar` is a global variable. Its declaration is not contained in any function. The `func()` function increments the `globvar` upon every invocation. We can say that `globvar` is used to count `func()`'s executions.

Note that the `main()` function makes use of this variable too, although it doesn't modify the variable's value. For this reason, we assume that the `main` function doesn't cause side effects.

We’ll avoid using side effects in future examples. Treat them only as a possibility, not a routine.

```cpp
#include <iostream>

using namespace std;

int globvar = 0;

void func() 
{
      cout << "Thank you for invoking me :)" << endl;
      globvar++;
}

int main() 
{
      for (int i = 0; i < 5; i++)
            func();
      cout << endl << "The function was happy " << globvar 
           << " times" << endl;
}
```

### Console >_

Thank you for invoking me :)
Thank you for invoking me :)
Thank you for invoking me :)
Thank you for invoking me :)
Thank you for invoking me :)

The function was happy 5 tim

# **Passing parameters by value**

So far, we’ve been assuming that the argument's values are sent to the function and we haven’t said a word about the way back. Our arguments travel to the function's body and we don't expect them to return from there.

Let's do a simple experiment showing if a function is able to change the value of its argument.

Now take a look at the code in the editor.

As you can see, the `can_i_change_my_argument()` function increments its argument's value. It also reports it to the user. The question is: is the modified value visible outside the function? In other words: **does the parameter's change reflect the argument's value?**

Let's compile the code and run it. It should produce the following output:

```
var = 1
----------
I've got: 1
I'm about to give back: 2
----------
var = 1
```

**output**

Analyse the example carefully and do the experiment yourself.

As you can see, **the parameter's value doesn't replace the argument's value upon return from the function**. We can say that the argument has a one-way ticket: it transports a value to the function and doesn't take it up to the invoker.

Don't forget that. This way of communication is based on transferring a value from the invoker to the function. And that’s why this method is called **passing parameters by value**.

```cpp
#include <iostream>

using namespace std;

void can_i_change_my_argument(int param)
{
    cout << "----------" << endl;
    cout << "I have got: " << param << endl;
    param++;
    cout << "I'm about to give back: " << param << endl;
    cout << "----------" << endl;
}

int main() 
{
    int var = 1;

    cout << "var = " << var << endl;
    can_i_change_my_argument(var);
    cout << "var = " << var << endl;
}
```

### Console >_

```cpp
var = 1
----------
I've got: 1
I'm about to give back: 2
----------
var = 1
```

# **Passing parameters by reference**

The C++ language doesn’t just offer one method for passing parameters. The second method is called **passing by reference** and allows functions to affect an actual parameter's values.

If you’re going to pass any parameters by reference, you need to **announce** it while declaring the function. See the example in the editor.

It looks very similar to the previous example, doesn't it? Look carefully and find one specific difference. This is a very important difference, one which radically changes the function's behaviour.

Yes, you're right. The difference is caused by the `&` sign being placed after the parameter's type name. Let’s clarify:

- type `name` – the `name` parameter is passed **by value**
- type`& name` – the `name` parameter is passed **by reference**

When a parameter is passed by reference it means that a **parameter is just a synonym of an argument**. Every modification made into a parameter immediately affects an associated argument. We can informally say that arguments passed by reference have return tickets and bring their modified values back to the invoker.

As you may suspect, the code will produce the following output:

```
var = 1
----------
I have got: 1
I'm about to give back: 2
----------
var = 2
```

                                                                                                                                                    **output**

```cpp
#include <iostream>

using namespace std;

void can_i_change_my_argument(int& param) 
{
    cout << "----------" << endl;
    cout << "I have got: " << param << endl;
    param++;
    cout << "I'm about to give back: " << param << endl;
    cout << "----------" << endl;
}

int main() 
{
    int
    var = 1;

    cout << "var = " << var << endl;
    can_i_change_my_argument(var);
    cout << "var = " << var << endl;
}
```

### Console >_

```cpp
var = 1
----------
I have got: 1
I'm about to give back: 2
----------
var = 2
```

We do **the selection of the passing method for each parameter individually**. You can mix parameters of both kinds if you find it useful. Use the “**passing by value**” if you don't need to share the function's results using the parameter's values, and use “**passing by reference**” in all other cases.

See the example in the editor.

The `mixed_styles` function assigns its second parameter with an incremented value of its first parameter. This means that the former parameter is passed by value, while the latter is passed by reference.

The program produces the following output:

```
var1 = 1, var2 = 2
```

                                                                                                                                                    **output**

```cpp
#include <iostream>

using namespace std;

void mixed_styles(int bval, int & bref) {
  bref = bval + 1;
}

int main(void) {
  int var1 = 1, var2;

  mixed_styles(var1, var2);
  cout << "var1 = " << var1 << ", var2 = " << var2 << endl;
  return 0;
}
```

### Console >_

> `var1 = 1, var2 = 2`

The “passing by reference” method has one important and obvious **limitation. If a parameter is declared as passed by reference (so it is preceded by the `&` sign) its corresponding argument must be a variable**.

An argument referring to a “passed by value” parameter may be an expression in general, so we can use not only a variable but also a literal, or even a function invocation's result.

We say this limitation is “obvious” because the function can’t place a value in something other than a variable. It cannot assign a new value to a literal, or force an expression to change its result. See the snippet in the editor.

All the following invocations are permitted:

- `by_val(var);`
- `by_val(var + 2);`
- `by_val(var * fun(1));`

If you want to modify the invocations to take advantage of the `by_ref()` function, you can only use the first one. **All the others will cause a compilation error**.

```cpp
#include <iostream>

using namespace std;

int fun(int n)
{
        return 2 * n;
}

void by_val(int parameter)
{
        parameter++;
}

void by_ref(int& parameter)
{
        parameter++;
}

int main()
{
        int var = 1;

        by_val(var);
        by_ref(var);
        cout << "var = " << var << endl;
}
```

### Console >_

> `var = 2`

# **Passing parameters by value**

Is it possible to utilize “passing by value” and be able to propagate the value outside the function despite the one-way nature of this method?

The answer is “yes”. We’re going to show you how to do that, but we want to emphasize that this is not the way we recommend doing it. This method is inherited from the C programming language, the C++ ancestor, and was the only available way of performing two-way parameter based communication. The C language offers nothing similar to the “passing by reference” mechanism, and therefore using other (we might even say slightly risky) methods is fully justified.

The idea is based on transferring a **pointer to a value**, not the value itself. If you declare a function with a prototype like this one:

`void by_ptr(int* ptr);`

you enable the function to deal with the addresses pointing to `int` values, and therefore you **give the function the chance to modify the values pointed to by the parameter**.

Now take a look at the code in the editor.

The `by_ptr` function takes one parameter, which is a **pointer**, and **accesses the value pointed to by the pointer** using the `*` (dereference) operator.

Reminder: if `p` is a pointer to a value, the `*p` represents the value itself.

In effect, the `by_ptr()` function modifies the variable without even knowing about its existence.

Some would say that this is the third method of passing parameters. We don't agree – it's still an old “passing by value” method. Only the values are different.

The example code produces the following output:

```
variable = 2
```

                                                                                                                                                    **output**

```cpp
#include <iostream>

using namespace std;

void by_ptr(int* ptr) 
{
    *ptr = *ptr + 1;
}

int main() 
{
    int variable = 1;
    int *pointer = &variable;

    by_ptr(pointer);
    cout << "variable = " << variable << endl;
}
```

### Console >_

> `variable = 2`

# **Parameters – continue**

We’re now going to rewrite our `Greet` function to make it more flexible. We want it to:

- be able to emit **any greeting**, not only the one predefined in the source code,
- be able to emit the greeting **more than once**, on the invoker's demand.

This means that our `new_greet` (this is how we name the new function) has to have two parameters intended to:

- store the greeting,
- store the number of greeting repetitions.

The complete function along with the short main function is here in the editor.

```cpp
#include <iostream>

using namespace std;

void new_greet(string greet, int repeats)
{
    for (int i = 0; i < repeats; i++)
        cout << greet << endl;
}

int main() 
{
  new_greet("Hi!", 5);
}
```

### Console >_

> Hi!
> Hi!
> Hi!
> Hi!
> Hi!

# **Default parameters – a simple example**

The new function makes our life easier, but we want more from it (isn’t that always the case?). We’ve learnt that most of our users require only one greeting at the same time, probably due to the average size of their egos. This may mean that we could use the following form of greeting more often than others:

`new_greet("Good morning", 1);`

We may just want to omit the “`1`”, hoping that the function will be smart enough to guess what we're going to do.

Is it reasonable to expect that any function will be able to behave in such a convenient way?

The answer is yes, but... But we have to inform it first that some of the invocations will not specify all the expected parameters, and indicate which values should be used instead of the absent ones. This mechanism is called “default parameters” and we’ll present its rules by modifying our previous function slightly.

We can modify the second formal parameter's declaration by using a phrase:

`= value`

to signal that we want the compiler to assume the default value for the parameter when we omit it during the invocation. If we declare the function in the following way:

`new_greet(string greet, int repeats = 1)`

the compiler will treat the one-parameter invocations like this one:

`new_greet("Hello");`

as if they were (explicitly) written as follows:

`new_greet("Hello", 1);`

Now look carefully at the example in the editor.

Note the different forms of invocation. The program will produce the following output:

```
Hello
Hello
Good morning
Hi
```

                                                                                                                                                     **output**

As you can see, the explicitly specified parameter value invalidates the default value.

```cpp
#include <iostream>

using namespace std;

void new_greet(string greet, int repeats = 1)
{
    for (int i = 0; i < repeats; i++)
        cout << greet << endl;
}

int main() 
{
    new_greet("Hello", 2);
    new_greet("Good morning");
    new_greet("Hi", 1);
}
```

### Console >_

> Hello
> Hello
> Good morning
> Hi

# **Default parameters – a more complex example**

You might want to ask now if it’s possible to have more than one default parameter in one function, i.e. if we may choose the default value not only for the `repeats` parameter but also for the `greet`.

Yes, it’s possible. Here’s an example of how to do it in the editor.

This mechanism is useful, but to take full advantage of it you mustn’t forget about the following limitations:

- the order of parameters is very important (in contrast to regular, non-default parameters which may be in virtually any order); intuitively, we can say that non-default parameters must be coded before the default ones; the compiler won't be able to identify the parameters otherwise;
- if more than one parameter is declared with a default value and at least one argument is specified in the invocation, the arguments are assigned to their parameter counterparts in the same order in which they are listed in the function declaration; this means that you are not allowed to use the default value for the first parameter and specify an explicit value for the second.

```cpp
#include <iostream>

using namespace std;

void new_greet(string greet = "Good morning", int repeats = 1) 
{
    for (int i = 0; i < repeats; i++)
        cout << greet << endl;
}

int main(void) {
    new_greet("Hello", 2);
    new_greet("Hi");
    new_greet();
}
```

### Console >_

> Hello
> Hello
> Hi
> Good morning

# **Anatomy of a function invocation**

So far, we’ve been using the term “**function invocation**” without going into detail. We’ve simply assumed that the invocations do their job in an automatic or magical way (or as developers used to say, “automagically”). It's now time to fix this and to explain how this mechanism works.

There is a function that takes its argument, multiplies it by 2 and returns the result to the invoker. The function is invoked three times within the main function. Clear enough? Okay, let’s keep going.

We’re going to look at the code from the compiler' s perspective. It reads the `function` code, translates it into the machine code and stores the translated code in a separate place in the memory, but the code cannot be used “as is” with no extra steps. Each function's code has to be supplemented with two important elements: a **prologue** and an **epilogue**.

A **prologue is the part of the code implicitly executed before the function**. The prologue is responsible for transferring arguments from the invoker's code and for storing them in a special transient area called a “stack”.

The **epilogue is implicitly executed just after the function's code** and is responsible for transferring the result of the function and for clearing the stack of the values placed there by the prologue.

```cpp
#include <iostream>

using namespace std;

int function(int parameter)
{
    return parameter * 2;
}

int main() 
{
    int var = 1;
    var = function(var);
    var = function(var);
    var = function(var);
    cout << var << endl;
}
```

### Console >_

> `8`

# **Prologues and epilogues**

Take a look at the diagram below:

![https://edube.org/uploads/media/default/0001/01/c9774e05b931318adf4d597a16c5162488f711d1.png](https://edube.org/uploads/media/default/0001/01/c9774e05b931318adf4d597a16c5162488f711d1.png)

This diagram illustrates the flow of control during one function invocation from the previous example. All the other invocations will be carried out in the same way.

This approach has some obvious **advantages**. The **function code, the prologue and the epilogue occupy the same memory space** regardless of how many times the function is invoked. It means that invoking it in this way saves memory and makes your program more compact.

But...

One of the most interesting **paradoxes** of computer programming says that **when a code is compact, it cannot be fast** at the same time; and vice versa, when the code is fast, it cannot be compact. Of course, it's more of a joke rather than a scientific law, but in this case the rule works very well.

The phenomenon described above even has its name and traces of it can be found in many IT disciplines. If you want to know more of the **Space–time tradeoff** take a look here: [https://en.wikipedia.org/wiki/Space%E2%80%93time_tradeoff](https://en.wikipedia.org/wiki/Space%E2%80%93time_tradeoff).

Try to imagine that our program is going to invoke the function many times (e.g. hundreds or thousands of times). It may mean that you’ll have to pay a high price (in the sense of time) for all those transfers of control and prologue/epilogue executions. The price is higher when the function is short (i.e. shorter than the the prologue and epilogue).

This example shows that sometimes, in well-defined cases, it would be better to avoid the prologue-function-epilogue chain and to **insert the function's code directly into to the invoker's code**.

# **Function inlining**

Take a look at the modified diagram:

![https://edube.org/uploads/media/default/0001/01/695cee433ff7223cca987b17e217f7e956be007e.png](https://edube.org/uploads/media/default/0001/01/695cee433ff7223cca987b17e217f7e956be007e.png)

This diagram illustrates another approach to the problem of function invocation. When the function is short and fast, and when **we expect the function to be invoked very often**, it’s better (and more time effective) to write the function code at each invocation.

Of course, we’ll have to pay for that. Don't be surprised by the fact that the total code size will be significantly larger than previously.

The tactic of compiling function invocations is called **function inlining**. A function compiled like this is called an **inline function**.

# **Inline functions**

If you want a certain function to be compiled and invoked as an inline function, you have to mark it in a special way.

You need to precede the function declaration with the inline keyword. Look at the example in the editor.

Luckily for us, the syntax of this construction has some flexibility:

- **it doesn't matter whether the inline keyword is placed** before or after the name of the type; both of the following lines are syntactically correct:`inline int function(int parameter)
  int inline function(int parameter)`
- if you need to use both the declaration and the definition for the same function, it doesn't matter where you put the `inline` keyword; it’s correct to use it in the declaration and omit it in the definition; it’s also equally valid to use it in the definition and omit it in the declaration; of course, using the keyword in both places is also valid.

```cpp
#include <iostream>

using namespace std;

inline int function(int parameter) 
{
    return parameter * 2;
}

int main()
{
    int var = 1;
    var = function(var);
    var = function(var);
    var = function(var);
    cout << var << endl;
}
```

### Console >_

> `8`

# **Different tools for different tasks**

Different tasks require different tools, although these tools may have exactly the same name. For example, the tool named “knife” looks very different when it’s used by a surgeon, a cook or a serial killer. We said before that we’re not allowed to have a variable and a function of the same name. It's time to ask if we can have more than one function of the same name.

Yes, we can. It’s natural that we may want to have **different tools of the same name used for different purposes**. For example, we need a function to find the larger of two float numbers. It doesn’t look difficult, right?

Well, we've written this function for you. Take a look at the snippet in the editor.

You might argue that we could have written the function in a more compact way. We agree with you. It’s way too verbose. Feel free to rewrite it in a smarter fashion.

```cpp
float max(float a, float b) 
{
    if (a > b)
        return a;
    else
        return b;
}
```

# **Max – extended version**

Imagine that one day our needs increased and we suddenly wanted to have a very similar function that was able to find the largest of three values. What could we do?

Of course, we can make use of the previous function and, assuming that we want to find the largest of the a, b and c variables, do something like this:

`x = max(max(a, b), c);`

What, you don’t like it? We don't like it, either. It’s neither nice nor effective. It would be better to forget our old function and write a snazzy new one that was much more tailored to what we want.

It would also be a good idea to name it like the old one: `max`. This name perfectly illustrates the function's role and purpose.

Take a look at the snippet in the editor.

```cpp
float max(float a, float b, float c)
{
    int m = a;

    if (b > m)
        m = b;
    if (c > m)
        m = c;
    return m;
}
```

# **How it works?**

The mechanism that allows us to have more than one function of a certain name is called **overloading** (since the one and the same name is *overloaded* with different meanings).

There is one, important limitation: all the **overloaded functions must be clearly distinguishable to the compiler**. The compiler cannot hesitate over which of the overloaded variants need to be used in a particular part of the code.

Our examples leave no doubt. The choice is simple: if the invocation contains three arguments, the second variant is chosen. If there are two arguments, the compiler uses the first variant. Any other variant of the invocation is considered an error.

What circumstances does the compiler take into consideration when choosing the one target function (one of the few available)?

- **the number of arguments**: for example, if there are three overloaded functions with (respectively) two, three and four parameters, and the invocation specifies two arguments, only the first of the functions may be used as a target (this function is called '**the best candidate**')
- **the arguments' types**: if there’s more than one function with the same number of parameters, the target function is selected on the basis of the **parameters' type conformity**

Note: **the `return` type is not taken into consideration** when the compiler is looking for the best candidate for a certain invocation. This should be obvious to you if you remember that the return value of any typed function may be ignored.

In this sense, two functions which differ only in the return type are indistinguishable to the compiler. This means that the following snippet is wrong:

```cpp
int fnc(int a)
{
    return a;
}

void fnc(int a) {}
```

```cpp
float max(float a, float b, float c)
{
    int m = a;

    if (b > m)
        m = b;
    if (c > m)
        m = c;
    return m;
}
```

# **How to find the best candidate?**

The number of different data types in the C++ language is significant, so the mechanism responsible for finding the best candidate has to use some simplifications so as not to force developers to create a separate function for each different data type. Take a look at the following example in the editor.

Try to answer this question: which of these two overloaded functions is the best candidate for the invocation?

Yes, you're absolutely right (we hope) – it’s the first one, with the `int x` parameter declaration.

```cpp
void play_with_number(int x)
{
    ...
}

void play_with_number(float x)
{
    ...
}

play_with_number(1);
```

We've changed our example a bit. Can you see the difference?

Which of the functions is the best candidate now? You want to say that it’s the second one, don’t you? Sorry, you're wrong.

**There is no good candidate for the invocation** – why?

**The literal `1.` is not of type `float`!** It's of type `double` (really!). The C++ language compiler tries to promote the types if there is no exact fit (as in our example: obviously a `float` is not a `double`).

Unfortunately (to be honest, fortunately) the direction of this type of promotion goes from less precise to more precise, not vice versa. It means, that any `float` can be promoted to `double`, but no `double` can be promoted (or rather degraded) to `float`.

In this situation, the compiler will inform you that it is unable to find the best candidate and the compilations will fail.

You have two choices:

- you can write the third instance of the `play_with_number()` with one parameter of type `double`;
- you can convince the compiler that your literal is of type `float`; you can do that just by adding the suffix `f` to the number, like this:`play_with_number(1.f);`

The compiler will be satisfied.

```cpp
void play_with_number(int x)
{
    ...
}
void play_with_number(float x)
{
    ...
}

play_with_number(1.);
```

# **A new operator: a three-argument one**

Now's a good time to show you another C++ language operator: `?:`. This operator is very original because it requires three arguments. This is how we use it:

`expression1 ? expression2 : expression3`

This operator works as follows:

- **calculates** the value of the `expression1`;
- if the calculated value is **non-zero** (note: it includes `true` either), the operator returns the value of `expression2`, completely neglecting `expression3`;
- if the value calculated in step 1 is **zero**, the operator returns the value of expression3, omitting `expression2`.

This means that the result of the following expression:

`i = i > 0 ? 1 : 0;`

will be calculated in the following way:

- variable `i` will be assigned with a `1` if its previous value was greater than zero, and `0` otherwise. Note that we can achieve the same effect using a conditional statement:`if(i > 0)
  i = 1;
  else
  i = 0`

This form is somewhat more extensive, although we can’t deny that it’s more readable at the same time.

# **A new operator: an example**

We can use the new ternary operator (it’s worth mentioning that this is the only ternary operator in the “C++” language) to implement our two-argument max function in a more compact way. Here it is:

```cpp
float max(float a, float b)
{
    return a > b ? a : b;
}
```

# **A new operator: an example number 2**

The three-argument variant can make use of the ternary operator too, although we have to admit that the code below is not the most readable:

```cpp
float max(float a, float b, float c) 
{
    return a > b ? (a > c ? a : c) : (b > c ? b : c);
}
```

Please use the `?:` operator with caution. It doesn’t offer much expressivity, but does destroy a lot of clarity. But it’s up to you what you decide to do.

# **Sorting a vector**

Think of this chapter as a digression, but a very useful digression. We’re going to tell you about **sorting**. Sorting is very serious and many sorting algorithms have been invented so far which differ a lot in speed as well as in complexity.

We’re going to show you a very simple algorithm, easy to understand, but also not too efficient. It’s used very rarely, and certainly not for large and extensive vectors.

We can say that the vector can be sorted in two ways:

- **increasing** (or more precisely – **non-decreasing**) if, in every pair of adjacent elements, the former element is not greater than the latter;
- **decreasing** (or more precisely – **non-increasing**) if, in every pair of adjacent elements, the former element is not less than the latter.

In the following sections, we’re going to sort the vector in increasing order, so the numbers will be ordered from the smallest to the largest.

Here’s our vector:

![https://edube.org/uploads/media/default/0001/01/e96457693d479dc9691e3b0d21d1ebaec3cffd7e.png](https://edube.org/uploads/media/default/0001/01/e96457693d479dc9691e3b0d21d1ebaec3cffd7e.png)

We’ll try to use the following approach: we’ll take the first and second elements and compare them; if we determine that they’re in the **wrong order** (the first is greater than the second), we’ll **swap** them around; if they’re in the right order, we’ll do nothing. A glance at our vector confirms the second condition – the elements #1 and #2 are in the proper order, as *8 < 10*.

Now look at the second and third elements. They’re in the wrong positions. We have to swap them around. Let's do it.

We can go further and look at the third and fourth elements. Again, this is not what it’s supposed to be like.

We have to swap them around:

![https://edube.org/uploads/media/default/0001/01/8802b581254ca06fddbd6330367dba5c24f5cd8a.png](https://edube.org/uploads/media/default/0001/01/8802b581254ca06fddbd6330367dba5c24f5cd8a.png)

Now we check the fourth and fifth elements. Well, yes, they too are in the wrong positions. Another swap.

![https://edube.org/uploads/media/default/0001/01/c486f7798620cac1c352fc1bc72f66662feeb310.png](https://edube.org/uploads/media/default/0001/01/c486f7798620cac1c352fc1bc72f66662feeb310.png)

The first pass through the vector is complete. We’re still far from finishing our job, but something curious has happened in the meantime. The largest element (10) has gone to the end of the vector. Note that this is where we want it. All the remaining elements form a picturesque mess, but this one is already home.

![https://edube.org/uploads/media/default/0001/01/aeb8343102e95b3f9bd47a73ebbcd09a944a9359.png](https://edube.org/uploads/media/default/0001/01/aeb8343102e95b3f9bd47a73ebbcd09a944a9359.png)

Now, for a moment, try to imagine this vector in a slightly different way – namely, this

![https://edube.org/uploads/media/default/0001/01/e0d23ca025d03fe3f11be01aeae7e20e4273eab2.png](https://edube.org/uploads/media/default/0001/01/e0d23ca025d03fe3f11be01aeae7e20e4273eab2.png)

Look – 10 is at the top. We could say that it floated up from the bottom to the surface, just like the bubbles in a glass of champagne. The sorting method derives its name from this same observation – it's called a **bubble sort**.

We had a quick break with a glass of champagne, but it’s time to get back to sorting. We do it with pleasure, starting with the second pass through the vector. We look at the first and second elements – uh oh, a swap is necessary!

![https://edube.org/uploads/media/default/0001/01/72fd06a7aa8657844da624955a57fa30951afc53.png](https://edube.org/uploads/media/default/0001/01/72fd06a7aa8657844da624955a57fa30951afc53.png)

Now the second and third elements: yep, 8 is a bubble and goes up to the surface:

![https://edube.org/uploads/media/default/0001/01/c5e75ed4d7857de19b057b9a37f948c9c5f7b07e.png](https://edube.org/uploads/media/default/0001/01/c5e75ed4d7857de19b057b9a37f948c9c5f7b07e.png)

Time for the third and fourth elements: we have to swap them too:

![https://edube.org/uploads/media/default/0001/01/1aaedc29937f156bcd6988ad6d1cba62fe44574d.png](https://edube.org/uploads/media/default/0001/01/1aaedc29937f156bcd6988ad6d1cba62fe44574d.png)

The second pass is finished and 8 is already in place. We start the next pass immediately. Watch the first and second elements carefully - yes, it's time for a swap:

![https://edube.org/uploads/media/default/0001/01/528a345baa73ce8dc06b9d8b7638e90c1c1efee1.png](https://edube.org/uploads/media/default/0001/01/528a345baa73ce8dc06b9d8b7638e90c1c1efee1.png)

Now 6 wants to find its place. We’ll help it and swap the second and third elements.

![https://edube.org/uploads/media/default/0001/01/e3bf33ec6a49f602b9a9e86364832cc720e0bee8.png](https://edube.org/uploads/media/default/0001/01/e3bf33ec6a49f602b9a9e86364832cc720e0bee8.png)

Hey! Look! The vector is already sorted! We have nothing more to do! This is exactly what we wanted!

As you can see, this algorithm is simple: we compare the adjacent elements and by swapping some of them we achieve our goal.

We’ll try to code in the C++ language all the actions performed during a single pass through the vector, and then we’ll think about how many passes we actually need. We haven't analysed this so far, and we will discuss this more a little later.

![https://edube.org/uploads/media/default/0001/01/9bb11a4d140eeddd9c8516f337729f2fcd37aa9b.png](https://edube.org/uploads/media/default/0001/01/9bb11a4d140eeddd9c8516f337729f2fcd37aa9b.png)

How many passes do we need to sort the entire vector?

Take a look at the code in the editor - the snippet presented here shows actions needed to perform one pass of the sorting. The first pass must carry out 4 comparisons - do you know why?

### **`Check`**

If there are *n* elements inside the vector, there are *n-1* adjacent pairs of elements thus 5 elements require 4 comparisons.

There is a question worth to ask - how many such passes do we have to perform to be absolutely sure that our vector is fully sorted?

We answer this by doing the following: we introduce another variable; its task is to observe if any swap was done during the pass or not; if there was no swap, then the vector is already sorted and nothing more has to be done.

We declare a variable named `swapped` and we assign a value of `false` to it to indicate that there were no swaps. Otherwise, it will be assigned `true`.

```cpp
vector<int> numbers {8, 10, 6 , 2, 4}; // vector to be sorted 

// we need 5 – 1 comparisons – why? 
for(int i = 0; i < 4; i++) {
    // compare adjacent elements
    if(numbers[i] > numbers[i + 1]) {
    /* if we went here it means that we have to swap the elements */
        int aux = numbers[i]; // auxiliary variable for swaps
        numbers[i] = numbers[i + 1];
        numbers[i + 1] = aux;
    }
}
```

You shouldn’t have any problem reading or understanding the program. On the next slide you can see a complete program, enriched by a conversation with the user and allowing the user to enter and print elements of the array.

```cpp
vector<int> numbers {8, 10, 6 , 2, 4}; // vector to be sorted 
bool swapped;

do { // we will decide if we need to continue this loop 
  swapped = false; // no swap occured yet

  for(int i = 0; i < 4; i++)
    if(numbers[i] > numbers[i + 1]) {
      swapped = true;
      int aux = numbers[i];
      numbers[i] = numbers[i + 1];
      numbers[i + 1] = aux;
    }
} while(swapped);
```

The bubble sort – final version.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() 
{
  vector<int> numbers(5);

  // ask the user to enter 5 values 
  for (int i = 0; i < 5; i++) {
    cout << endl << "Enter value #" << i + 1 << ": ";
    cin >> numbers[i];
  }

  // sort them 
  bool swapped;
  do {
    swapped = false;
    for (int i = 0; i < 4; i++) {
      if (numbers[i] > numbers[i + 1]) {
        swapped = true;
        int aux = numbers[i];
        numbers[i] = numbers[i + 1];
        numbers[i + 1] = aux;
      }
    }
  } while (swapped);

  // print results 
  cout << endl << "Sorted vector: " << endl;
  for (int i = 0; i < 5; i++)
    cout << numbers[i] << " ";
  cout << endl;
}
```

### Console >_

Enter value #1: 7

Enter value #2: 6

Enter value #3: 2

Enter value #4: 3

Enter value #5: 4

Sorted vector:
2 3 4 6 7

# **void – the very exceptional type**

We've seen the unusual type called `void` in our examples a few times. We’ve used it to indicate that a function either doesn't return a result, or (which is currently obsoleted) doesn't expect any parameters.

According to the following function prototype (written in a bit vintage style):

`void nothing_at_all(void);`

The same declaration but coded in modern style looks as follows:

`void nothing_at_all();`

The function demands to be invoked without parameters and returns no result. This is how the invocation should look like:

`nothing_at_all();`

Despite the fact that the `void` type doesn't represent any useful value, it’s possible to declare pointers to this type, as in the following example:

`void *ptr;`

You may ask how to use **a pointer that points at nothing**, and then ask why have such a pointer at all. This kind of pointer, which is of the type `void *`, is called an **amorphous pointer** to emphasize the fact that it can point to **any value of any type**. This means that the pointer of type `void *` cannot be subject to the dereference operator, so you must not write anything like this:

- *`ptr;`

If `ptr` was of type `void *`, `*ptr` would be of type `void` and the assignment of a value of type `int` would be prohibited by the compiler.

However, pointers of type `void *` are very useful when you need to have a pointer, but don’t know what it may be used for in the future.

As soon as it becomes clear, the pointer can easily be converted into another pointer of the desired type (of course, a pointer type) which is always possible, and doesn’t cause any loss of accuracy.

# **Memory on demand**

In the examples we’ve seen so far, memory management has taken place outside of our consciousness. The parts of memory we’ve used to store values were hidden behind the names of scalars, vectors and arrays. They appeared as soon as they had been declared and disappeared when our program ended its operation. All work associated with memory allocation was organized by the compiler and we didn't care how it worked. And this is exactly how it should be – high level languages and their compilers are designed to exonerate the developers' minds of such responsibilities.

It frequently happens that the developer wants to have full control over how much memory is used and when exactly it’s used. This is especially important when you don’t know in advance what the size of the data to be processed is. To manage the allocating and freeing up of memory, the “C++” language gives us two specialized keywords. Here are both of them for you:

- `new`
- `delete`

# **The *new* keyword**

The `new` keyword is used to **request the creation of a new memory block**. When the allocated memory is no longer needed and/or utilized, it would be a good idea to return it to the operating system. We do this with the **delete** keyword.

`float *array = new float[20];`

`int count = new int;`

- it needs precise specifications regarding the entity being created; it must be expressed as a type description and if the created entity is a one dimensional array (in fact a vector), the size of the array must be given too (as in the first example);
- the **`new` returns a pointer** of type conforming to the newly created entity;
- the newly allocated memory area **is not filled (initiated)** in any way, so you should expect it to just contain **garbage**.

**Note**: the arrays we are dealing with using the `new` keyword have nothing to do with these brought to life as objects of `vector<type_name>` type. The former are managed by the low-level code generated by the compiler, the latter are high-level creations managed by library code.

# **The *delete* keyword**

When we no longer need the memory, we can release it (free it) using the `delete` keyword in the following way:

`delete [] array;`

`delete count;`

What happens here is the following:

- we use the `delete []` form if we want to free up the memory allocated for an array, otherwise we use `delete`;
- you can only release the entire allocated block, not a part of it;
- after performing the `delete` function, all the pointers that point to the data inside the freed area become illegal; attempting to use them may result in an abnormal program termination.

Now we’re going to show you a complete, albeit not very useful, program that demonstrates the use of both keywords.

- We declare a variable called `arr` which will point to the data of type `float` (the pointer's type is `float *`); no value is initially assigned to this variable;
- We use **the `new` keyword** to allocate a block of memory sufficient to store a float array consisting of 5 elements;
- We make use of the newly allocated array (to be precise, a vector) and next we release it using the `delete` keyword

Pay attention to the fact that the pointer returned by new is treated as if it’s an array. Surprising?

The handling of the **dynamic arrays** (created during the run of the program) is no different than using regular arrays/vectors declared in the usual way using `vector` template.

We owe it to the `[]` operator. Regardless of the nature of the array, we can access its elements in the same way.

```cpp
#include <iostream>

using namespace std;

int main() 
{
    float *arr = new float[5];

    for (int i = 0; i < 5; i++)
        arr[i] = i * i;

    for (int i = 0; i < 5; i++)
        cout << arr[i] << endl;

    delete[] arr;
}
```

### Console >_

> 0
> 1
> 4
> 9
> 16

Being able to allocate the amount of memory that’s really needed lets us write programs that can **adapt** themselves to the size of the data currently being processed. Let's go back to the bubble sort algorithm that we showed you earlier. This program assumed that there were exactly 5 numbers to sort. This is obviously a serious inconvenience.

It may happen one day that we want to sort 10,000 numbers or possibly even hundreds of thousands. You can, of course, declare an array of the maximum predictable size, but it would be unreasonable. A much better way is to ask the user how many numbers will be sorted and then allocate an array of the appropriate size.

Let's try to start with a simpler example. In the following program, we allocate an array containing 5 elements of type `int`, set their values, sum them up and, finally, release the previously allocated memory.

```cpp
#include <iostream>

using namespace std;

int main()
{
    int *tabptr = new int[5], sum = 0;

    for (int i = 0; i < 5; i++)
        tabptr[i] = i;
    for (int i = 0; i < 5; i++)
        sum += tabptr[i];
    delete [] tabptr;
    cout << "sum=" << sum << endl;
}
```

### Console >_

> `sum=10`

The bubble sort program adopted to use `new` and `delete` mechanisms is in the editor.

We encourage you to compile and run the program yourself.

```cpp
#include <iostream>

using namespace std;

int main() 
{
  cout << "How many numbers are you going to sort? ";
  int how_many_numbers;
  cin >> how_many_numbers;
  if(how_many_numbers <= 0 || how_many_numbers > 1000000) {
    cout << "Are you kidding?" << endl;
    return 1;
  }
  int *numbers = new int[how_many_numbers];
  for(int i = 0; i < how_many_numbers; i++) {
    cout << "\nEnter the number #" << i + 1 << ": ";
    cin >> numbers[i];
  }
  bool swapped;
  do {
    swapped = false;
    for (int i = 0; i < how_many_numbers - 1; i++)
      if (numbers[i] > numbers[i + 1]) {
        swapped = true;
        int aux = numbers[i];
        numbers[i] = numbers[i + 1];
        numbers[i + 1] = aux;
      }
  } while (swapped);
  cout << endl << "The sorted array:" << endl;
  for (int i = 0; i < how_many_numbers; i++)
    cout << numbers[i] << " ";
  cout << endl;
  delete[] numbers;
}
```

### Console >_

How many numbers are you going to sort? 6

Enter the number #1: 9

Enter the number #2: 0

Enter the number #3: 1

Enter the number #4: 4

Enter the number #5: 0

Enter the number #6: 9

The sorted array:
0 0 1 4 9 9

# **Congratulations! You have completed Module 3.**

Well done! You've reached the end of Module 3 and completed a major milestone in your C++ programming education. Here's a short summary of the objectives you've covered and got familiar with in Module 3:

- designing, declaring, and invoking functions;
- pointers;
- different methods of passing parameters and their purpose;
- default parameters;
- inline functions;
- overloaded functions;
- sorting;
- memory on demand.

You are now ready to take the module quiz and attempt the final challenge: Module 3 Test, which will help you gauge what you've learned so far.

![https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png](https://edube.org/uploads/media/default/0001/02/e6a200098d7994c2bb62c07d76e524e41ffadb67.png)