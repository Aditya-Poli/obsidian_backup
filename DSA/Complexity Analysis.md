# Complexity Analysis

Ok so till now we have just learn some algorithm and tried to solve some problems based on them. Now an important question arise while programming is: How efficient is an algorithm or piece of code? How much time and space does it take to run?

## [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#what-is-complexity-analysis)_What is Complexity analysis_

It's really important to understand the real-world significance of **algorithms and its properties** because using different ideas one can design many algorithms for computing a solution to a given problem. Key important questions in algorithms are :

- How do we design **good** algorithms?
- How do we know that our algorithm is **efficient**?
- How to efficiently implement algorithms in a programming language?

> **Interviewer** _often checks your ideas and coding skills by asking you to write a code giving restrictions on its_ **time or space complexities.**

## [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#why-to-do-complexity-analysis)_Why to do Complexity analysis_

We already know there are tools to measure how fast a program runs. There are programs called _profilers_ which measure running time in milliseconds and can help us optimize our code by spotting bottlenecks. While this is a useful tool, it isn't really relevant to algorithm complexity. Algorithm complexity is something designed to compare two algorithms at the idea level — ignoring low-level details such as the implementation programming language, the hardware the algorithm runs on, or the instruction set of the given CPU. We want to compare algorithms in terms of just what they are: Ideas of how something is computed. Counting milliseconds won't help us in that. It's quite possible that a bad algorithm written in a low-level programming language such as [assembly](http://en.wikipedia.org/wiki/Assembly_language) runs much quicker than a good algorithm written in a high-level programming language such as [Python](http://www.python.org/) or [Ruby](http://www.ruby-lang.org/en/).

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#memory)_Memory_

Memory in a computer is just a sequential set of "buckets" that can contain numbers, characters, or Boolean values. By using several buckets in a row, we get arrays. By giving names to a set of contiguous buckets, we get a "structure". But at its core, a computer memory is a very simple list of numbers. Everything else must be built up upon this.

1. Memory is laid out in sequential order basically from 0 on up (one byte at a time). Each position in memory has a number (called its address!).
    
2. The compiler (or interpreter) associates your variable names with memory addresses.
    
3. In some languages like C, you can actually ask the computer for the address of a variable in memory. In C this is done using the ampersand &
    
    In many languages, the actual address is hidden from you and is of little use to you, as all the access methods "abstract" the details of the computer hardware away, allowing the programmer to concentrate on the algorithm, and not the details.
    
4. Arrays variables simply contain the address of the first element of the array. Arrays are zero based so the address simply becomes the base address plus the index.
    
5. Structure variables simply contain the address of the first element of the structure, and each "named" field of the structure forms an offset from the first bucket. The computer keeps track of this offset so that the programmer can use symbolic names instead of numbers.
    
6. Memory buckets are 8 bits long (or one byte). A character (char) is one byte. An integer is (usually) four bytes. A float is four bytes. A double is 8 bytes.
    

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#performance)**Performance**

It conclude on the basis of time/memory/disk/etc. usage when we run the code. It depends on the machine, compiler, OS, etc as well as the code itself.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#complexity)**Complexity**

We are typically interested in the execution time of large instances of a problem, e.g., when 𝑛 → ∞, (asymptotic complexity). _for this we introduce the big O notation._

**Big O notation** is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity. big O notation is used to classify algorithms according to how their run time or space requirements grow as the input size grows. In analytic number theory, big O notation is often used to express a bound on the difference between an arithmetical function and a better understood approximation. Big O notation characterizes functions according to their growth rates: different functions with the same growth rate may be represented using the same O notation. The letter O is used because the growth rate of a function is also referred to as the **order of the function**. A description of a function in terms of big O notation usually only provides an upper bound on the growth rate of the function.

|Function|common name|
|:-:|:-:|
|N!|factorial|
|2^n|exponential|
|n³|cubic|
|n²|quadratic|
|n log n|quasi-linear|
|n|linear|
|log n|logarithmic|
|1|constant|

## [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#different-types-of-complexity)Different types of complexity

There are several different types of complexities , we will only be looking into the more popular and the most commonly used ones.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#constant-time-complexity-o1)Constant Time Complexity: O(1)

Complexity **O(1)** is the best, it’s not always achievable, but if it is, then your code is _independent_ of the input size.

Other operations that have complexity **O(1)** are the print function, simple arithmetic — addition, subtraction, and multiplication and division in the case of integers.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#linear-time-complexity-on)Linear Time Complexity: O(n)

When time complexity grows in direct proportion to the size of the input, you are facing Linear Time Complexity, or O(n). Algorithms with this time complexity will process the input (n) in “n” number of operations. This means that as the input grows, the algorithm takes proportionally longer to complete.

Linear running time algorithms are very common, and they relate to the fact that the algorithm visits every element from the input.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#logarithmic-time-complexity-olog-n)Logarithmic Time Complexity: O(log n)

Algorithms with this complexity make computation amazingly fast. An algorithm is said to run in logarithmic time if its time execution is proportional to the logarithm of the input size. This means that instead of increasing the time it takes to perform each subsequent step, the time is decreased at a magnitude that is inversely proportional to the input “n”.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#quadratic-time-complexity-on%C2%B2)Quadratic Time Complexity: O(n²)

In this type of algorithms, the time it takes to run grows directly proportional to the square of the size of the input (like linear, but squared).

Nested **For Loops** run on quadratic time, because you’re running a linear operation within another linear operation, or _n_ which equals _n²._

If you face these types of algorithms, you’ll either need a lot of resources and time, or you’ll need to come up with a better algorithm.

### [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#on-logn)O(n log(n))

If we have a code or an algorithm with complexity **O(log(n))** that gets repeated multiple times, then it becomes **O(n log(n))**. Famous examples of this are **merge sort and quicksort**.

# [](https://utkarsh1504.github.io/DSA-Java/intro-complexity#big-o-rules)Big O rules

Going through the above examples, you might have figured out some rules for calculating Big O, but let’s sum them up:

1. Reading, writing an item in a list or a dictionary has **O(1)**.
2. Going through an iterable is **O(n)**.
3. Nested loops lead to **O(n²)** complexity.
4. Any divide and concur approach or loops handling binary numbers have **O(n log(n))** complexity.
5. We sum up the complexity of sequential loops and multiply the complexity of nested loops.


# Time Complexity

Time Complexity is a function / relationship that tells us how the time increases as input size increases.

## [](https://utkarsh1504.github.io/DSA-Java/time-complexity#types-of-notations)Types of Notations:

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#big-o-notation-o-)Big O Notation, O :

- Word Definition - The notation Ο(n) is the formal way to express the strict upper bound of an algorithm's running time. It measures the worst case time complexity or the longest amount of time an algorithm can possibly take to complete.
- Mathematical Definition -

[![BigOh](https://utkarsh1504.github.io/DSA-Java/static/51da309c9fcf1af1dbc8a1a66ba81e51/e33ef/BigOh.png "BigOh")](https://utkarsh1504.github.io/DSA-Java/static/51da309c9fcf1af1dbc8a1a66ba81e51/e33ef/BigOh.png)If f(n) = O(g(n)), then there exists positive constants c, n0 such that 0 ≤ f(n) ≤ c.g(n), for all n ≥ n0, where f(n) are g(n) are asymptotic functions.

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#big-omega-notation-%CF%89-)Big Omega Notation, Ω :

- Word Definition - The notation Ω(n) is the formal way to express the strict lower bound of an algorithm's running time. It is opposite of Big Oh notation.
- Mathematical Definition -

[![Big Omega](https://utkarsh1504.github.io/DSA-Java/static/80ed51c8dd947195b1f643b90a3fa89e/e33ef/BigOmega.png "Big Omega")](https://utkarsh1504.github.io/DSA-Java/static/80ed51c8dd947195b1f643b90a3fa89e/e33ef/BigOmega.png)If f(n) = Ω(g(n)), then there exists positive constants c, n0 such that 0 ≤ c.g(n) ≤ f(n), for all n ≥ n0

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#theta-notation-%CE%B8-)Theta Notation, θ :

- Word Definition - The notation θ(n) is the formal way to express both the lower bound and the upper bound of an algorithm's running time.
- Mathematical Definition -

[![Theta](https://utkarsh1504.github.io/DSA-Java/static/d8ebac5216e411b76b54f229bddf4250/e7c18/Theta.png "Theta")](https://utkarsh1504.github.io/DSA-Java/static/d8ebac5216e411b76b54f229bddf4250/e7c18/Theta.png)If f(n) = Θ(g(n)), then there exists positive constants c1, c2, n0 such that 0 ≤ c1.g(n) ≤ f(n) ≤ c2.g(n), for all n ≥ n0

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#little-o-notation-o-)Little O Notation, o :

- Word Definition - The notation o(n) is the formal way to express the loose upper bound of an algorithm's running time.
- Mathematical Definition -

[![LittleOh](https://utkarsh1504.github.io/DSA-Java/static/255d9b076ef8138c265a89dcbaee1297/39d76/LittleOh.png "LittleOh")](https://utkarsh1504.github.io/DSA-Java/static/255d9b076ef8138c265a89dcbaee1297/39d76/LittleOh.png)If f(n) = o(g(n)), then there exists positive constants c, n0 such that 0 ≤ f(n) < c.g(n), for all n ≥ n0

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#little-omega-notation-%CF%89-)Little Omega Notation, Ω :

- Word Definition - The notation Ω(n) is the formal way to express the loose lower bound of an algorithm's running time.
- Mathematical Definition -

[![LittleOmega](https://utkarsh1504.github.io/DSA-Java/static/61c833f0c1639a7b02cccd4dc5a65932/ba1c3/LittleOmega.png "LittleOmega")](https://utkarsh1504.github.io/DSA-Java/static/61c833f0c1639a7b02cccd4dc5a65932/ba1c3/LittleOmega.png)If f(n) = ω(g(n)), then there exists positive constants c, n0 such that 0 ≤ c.g(n) < f(n), for all n ≥ n0

NOTE : We use Big O and Big Omega notations mostly.

## [](https://utkarsh1504.github.io/DSA-Java/time-complexity#points-to-remember-while-calculating-time-complexity)Points to remember while calculating time complexity

- Consider larger inputs because relationship at this point persists.
- Constants are ignored since actual time even differs for the same relationship.
- Always ignore less dominating terms.
- Look for the worst case complexity - this will be what we consider the Big O of our algorithm/function

## [](https://utkarsh1504.github.io/DSA-Java/time-complexity#example)Example

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#1--fn--5nsup3sup--4n--3)1) f(n) = 5n3 + 4n + 3

Time Complexity - O(n3)

Explanation - Ignoring the less dominating terms we are left with 5n3. Now ignoring the constants, we get n3. And this is the time complexity.

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#2)2)

```java
int sum = 0;
for(int i = 0; i < n; i++){
    for(int j = 0; j < n; j++){
        sum += i;
    }
}
```

Time Complexity - O(n2)

Explanation - Adding i to sum is constant time operation. And if we fix the value of i, we are traversing the inner loop n times. So, that means for a particular value of i, inner loop has O(n) complexity. And if we notice the outer loop, it is also traversing n times. So, total = n * n times and that is the time complexity.

## [](https://utkarsh1504.github.io/DSA-Java/time-complexity#guidelines-for-asymptotic-notation)Guidelines for Asymptotic notation:

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#loops)Loops:

The running time of a loop is, at most, the running time of the statements inside the loop, multiplied number of iterations.

```java
for(int i = 0; i < n; i++){
    System.out.println(i);
}
```

Here, no of iterations are n and printing statement is a constant time operation. So, time complexity becomes O(n * 1) i.e. O(n).

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#nested-loops)Nested Loops:

The total running time is the product of the sizes of all the loops.

```java
for(int j = 0; j < n; j++){
    for(int i = 0; i < n; i++){
        System.out.println(i);
    }
}
```

Here, outer loop is traversing n times(each loop having complexity O(n) as explained earlier).So total becomes O(n * n).

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#consecutive-statements)Consecutive statements:

Add the time complexity of each statement.

```java
int x = 0;
x += 1;
for(int i = 0; i < n; i++){
    System.out.println(i);
}
for(int j = 0; j < n; j++){
    for(int i = 0; i < n; i++){
        System.out.println(i);
    }
}
```

Here, the topmost two lines of code take 2 units of time(each statement takes 1 unit of time). The loop next to them executes n times(as explained earlier). The nested loop takes n2 time. Hence,the total becomes n2 + n + 2. Ignoring less dominating terms and constants, final time complexity is O(n2).

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#if-then-else-statements)If-then-else statements:

The total running time is the the sum of time taken for checking the condition and the part(if or else) which takes the highest time.

```java
int val = 12;
if(val < 18){
    for(int i = 0; i < n; i++){
        System.out.println(i);
    }
}
else{
    System.out.println(val);
}
```

Here, the first statement takes 1 unit of time. Then checking takes 1 unit of time. "if" part takes n unit of time. "else" part takes 1 unit of time. Larger among "if" and "else" is "if" (i.e. n unit of time).

So total = 1 + 1 + n = O(n2)

### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#logarithmic-complexity)Logarithmic Complexity:

It is achieved when the problem size is cut down by a fraction.

```java
for(int i = 1; i <= n;){
    i *= 2;
}
```

Here, in the first iteration, i = 1(i.e. 20)  
second , i = 2(i.e. 21)  
third , i = 4(i.e. 22)  
fourth , i = 8(i.e. 23)  
...  
kth , i = n(i.e. 2k - 1)

So, we need to find the no of interations i.e. the value of k = log2n + 1. That means, time complexity will be O(log2n)

## [](https://utkarsh1504.github.io/DSA-Java/time-complexity#properties-of-asymptotic-notation)Properties of Asymptotic Notation:

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#1-reflexivity)1) Reflexivity:

If f(n) is given then, f(n) = O(f(n)).Example:If f(n) = n3 ⇒ O(n3)  
Similarly, f(n) = Ω(f(n)) and f(n) = Θ(f(n)).

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#2-symmetry)2) Symmetry:

f(n) = Θ(g(n)) if and only if g(n) = Θ(f(n)). Example: If f(n) = n3 and g(n) = n3 then f(n) = Θ(n3) and g(n) = Θ(n3)

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#3-transistivity)3) Transistivity:

f(n) = O(g(n)) and g(n) = O(h(n)) ⇒ f(n) = O(h(n)). Example: If f(n) = n, g(n) = n2 and h(n) = n3 ⇒ n is O(n2) and n2 is O(n3) then n is O(n3)

#### [](https://utkarsh1504.github.io/DSA-Java/time-complexity#4-transpose-symmetry)4) Transpose Symmetry:

f(n) = O(g(n)) if and only if g(n) = Ω(f(n)). Example: If f(n) = n and g(n) = n2 then n is O(n2) and n2 is Ω(n).

[  
](https://utkarsh1504.github.io/DSA-Java/intro-complexity)


# Space Complexity

Now that we have learned about the 'time' aspect of performance analysis of an algorithm, let's move on to memory aspect of the same.

_**Space complexity of an algorithm is basically the amount of memory it needs to run to completion, ie, to execute and produce the result.**_

Calculation of space complexity used to hold much more significance in early days of computing than it does now. This is because most machines today have large memories and the user does not need to worry about running out of memory for running a program or two. But it is a crucial estimate where the physical memory is limited or closely monitored.

_Above all, it’s necessary to mention that space complexity depends on a variety of things such as the programming language, the compiler, or even the machine running the algorithm._

## [](https://utkarsh1504.github.io/DSA-Java/space-complexity#memory-usage-while-execution)Memory Usage while Execution

While executing, an algorithm uses memory space for three reasons:

- **Instruction Space**

-- It's the amount of memory used to save the compiled version of instructions.

- **Environmental Stack**

-- Sometimes an algorithm(function) may be called inside another algorithm(function). In such a situation, the current variables are pushed onto the system stack, where they wait for further execution and then the call to the inside algorithm(function) is made.  
Ex. If a function A() calls function B() inside it, then all the variables of the function A() will get stored on the system stack temporarily, while the function B() is called and executed inside the function A().

- **Data Space**

-- Amount of space used by the variables and constants.

So in general for any algorithm, the memory may be used for the following: - `Variables (Data Space)`, `Program Instruction (Instruction Space)` and `Execution (Environmental Space)`. But while calculating the Space Complexity of any algorithm, we usually consider only Data Space and we neglect the Instruction Space and Environmental Stack.

## [](https://utkarsh1504.github.io/DSA-Java/space-complexity#calculation-of-space-complexity)Calculation of Space Complexity

An algorithm's space can be categorized into 2 parts:  
**1) Fixed Part** - It is independent of the characteristics of input and output.  
It includes instruction(code) space, space for simple variables, fixed-size component variables and constants.  
**2) Variable Part** - It depends on instance characteristics.  
It consists of the space needed by component variables whose size is dependent on the particular problem instance being solved, the space needed by referenced variables, and the recursion stack space.

Sometimes, _**Auxiliary Space**_ is confused with Space Complexity. The Auxiliary Space is the extra space or the temporary space used by the algorithm during it's execution.

`Space Complexity = Auxiliary Space + Input space`

> Thus, space requirement S(M) of any algorithm M is: S(M) = c + Sm (Instance characteristics), where c is constant

While analyzing space complexity, we primarily concentrate on estimating Sm. Consider the following algorithm:

```java
public int sum(int a, int b) {
    return a + b;
}
```

In this particular method, three variables are used and allocated in memory:

1. The first `int` argument, a
2. The second `int` argument, b
3. The returned sum result which is also an `int` like a and b

In Java, a single integer variable occupies `4` bytes of memory. In this example, we have three integer variables. Therefore, this algorithm always takes 12 bytes of memory to complete (3*4 bytes).

> We can clearly see that the space complexity is constant, so, it can be expressed in big-O notation as O(1).

Now let us see another example -

```java
public int sumArray(int[] array) {
    int size = array.length;
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += array[i];
    }
    return sum;
}
```

Again, let’s list all variables present in the above code:

1. Array – the function’s only argument – the space taken by the array is equal to 4n bytes where n is the length of the array
2. The `int` variable, size
3. The `int` variable, sum
4. The `int` iterator, i

The total space needed for this algorithm to complete is 4n + 4 + 4 + 4 (bytes). The highest order is of n in this equation. Thus, the space complexity of that code snippet is O(n). When the program consists of loops (In case of Iterative algorithms), it will have linear space complexity or O(n).

> While dealing with operations on data structures, we can say that space complexity depends on size of the data structure. Ex, if an array stores N elements, its space complexity is O(N). A program with an array of N arrays will have space complexity O(N^2) and so on.

Now, the space complexity analysis also takes into account the size of recursion stack in case of recursive algorithms. Consider the code below -

```java
Algorithm fact(n)
{
  if (n<=0) 
    return 1;
  else  
    return n * (n - 1);
}
```

In this case there are 3 statements ( an `if` statement & 2`return` statements). The depth of recursion is _n + 1_. Thus the recursion stack space needed is >=3(n+1). So we can say, space complexity is O(n) i.e. linear.

## [](https://utkarsh1504.github.io/DSA-Java/space-complexity#space-complexities-of-common-algorithms)Space Complexities of Common Algorithms

The space complexities of various algorithms is given below -

|Algorithm|Space Complexity|
|---|---|
|Linear Search|O(1)|
|Binary Search|O(1)|
|Bubble Sort|O(1)|
|Insertion Sort|O(1)|
|Selection Sort|O(1)|
|Heapsort|O(1)|
|Shell Sort|O(1)|
|Quicksort|O(log(n))|
|Mergesort|O(n)|
|Timsort|O(n)|
|Tree Sort|O(n)|
|Bucket Sort|O(n)|
|Radix Sort|O(n+k)|
|Counting Sort|O(k)|


# Time Space Tradeoff

# [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#time-space-trade-off-in-algorithms)**Time-Space Trade-Off in Algorithms**

Space-Time tradeoff in computer science is basically a problem solving technique in which we solve the problem:

- Either in less time and using more space, or
- In very little space by spending more time.

The best algorithm is the one which helps to solve a problem that requires less space in memory as well as takes less time to generate the output.But in general, it is not always possible to achieve both of these conditions at the same time.

If our problem is taking a long time but not much memory, a space-time trade-off would let us use more memory and solve the problem more quickly. Or, if it could be solved very quickly but requires more memory than we have, we can try to spend more time solving the problem in the limited memory.

## [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#types-of-time-space-trade-off)Types of Time-Space Trade-Off

- Lookup tables or Recalculation
- Compressed or Uncompressed data
- Re Rendering or Stored images
- Smaller code or loop unrolling

### [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#1-lookup-tables-or-recalculation)_1. Lookup tables or Recalculation:_

In a lookup table, an implementation can include the entire table which reduces computing time but increases the amount of memory required. It can recalculate i.e., compute table entries as needed, increasing computing time but reducing memory requirements.

### [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#2-compressed-or-uncompressed-data)_2. Compressed or Uncompressed data:_

A space-time trade-off can be applied to the problem of data storage. If data stored is uncompressed, it takes more space but less time. But if the data is stored compressed, it takes less space but more time to run the decompression algorithm. There are many instances where it is possible to directly work with compressed data. In that case of compressed bitmap indices, where it is faster to work with compression than without compression.

### [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#3-re-rendering-or-stored-images)_3. Re Rendering or Stored images:_

In this case, storing only the source and rendering it as an image would take more space but less time i.e., storing an image in the cache is faster than re-rendering but requires more space in memory.

### [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#4-smaller-code-or-loop-unrolling)_4. Smaller code or loop unrolling:_

Smaller code occupies less space in memory but it requires high computation time that is required for jumping back to the beginning of the loop at the end of each iteration. Loop unrolling can optimize execution speed at the cost of increased binary size. It occupies more space in memory but requires less computation time.

### [](https://utkarsh1504.github.io/DSA-Java/time_space_tradeoff#example)Example:

There are many algorithms that make use of time-space tradeoffs. Some of the algorithms are:

- In the field of cryptography, using space-time trade-off, the attacker is decreasing the exponential time required for a brute-force attack. **Rainbow tables** use partially precomputed values in the hash space of a cryptographic hash function to crack passwords in minutes instead of weeks. Decreasing the size of the rainbow table increases the time required to iterate over the hash space. The meet-in-the-middle attack uses a space-time trade-off to find the cryptographic key in only 2^{n+1} encryptions (and O(2^{n}) space) compared to the expected 2^{2n} encryptions (but only O(1) space) of the normal attack.
    
- **Dynamic programming** is another example where the time of solving problems can be decreased by using more memory. Fibonacci problem can be solved faster with DP.
    

[  
](https://utkarsh1504.github.io/DSA-Java/recurrence)(refer this website with good notes no need to take except the personal points.)
