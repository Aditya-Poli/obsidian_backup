
**Power Set:** Power set **P(S)** of a set **S** is the set of all subsets of **S**. For example S = {a, b, c} then P(s) = {{}, {a}, {b}, {c}, {a,b}, {a, c}, {b, c}, {a, b, c}}.  
If **S** has **n** elements in it then **P(s)** will have **2n** elements

**Example:** 

> Set  = [a,b,c]  
> power_set_size = pow(2, 3) = 8  
> Run for binary counter = 000 to 111
> 
> Value of Counter            Subset  
>    000                    -> Empty set  
>    001                    -> a  
>    010                    -> b  
>    011                    -> ab  
>    100                    -> c  
>    101                    -> ac  
>    110                    -> bc  
>    111                    -> abc

**Algorithm:** 

Input: Set[], set_size  
1. Get the size of power set  
      powet_set_size = pow(2, set_size)  
2  Loop for counter from 0 to pow_set_size  
    (a) Loop for i = 0 to set_size  
         (i) If ith bit in counter is set  
                Print ith element from set for this subset  
   (b) Print separator for subsets i.e., newline

**Method 1:**  
For a given set[] S, the power set can be found by generating all binary numbers between **0** and **2n-1**, where **n** is the size of the set.   
For example, for the set **S {**_**x**_**,** _**y**_**,** _**z**_**}**, generate all binary numbers from **0** to **23-1** and for each generated number, the corresponding set can be found by considering set bits in the number.

Below is the implementation of the above approach.

```java
// Java program for power set
import java .io.*;

public class GFG {
	
	static void printPowerSet(char []set,
							int set_size)
	{
		
		/*set_size of power set of a set
		with set_size n is (2**n -1)*/
		long pow_set_size =
			(long)Math.pow(2, set_size);
		int counter, j;
	
		/*Run from counter 000..0 to
		111..1*/
		for(counter = 0; counter <
				pow_set_size; counter++)
		{
			for(j = 0; j < set_size; j++)
			{
				/* Check if jth bit in the
				counter is set If set then
				print jth element from set */
				if((counter & (1 << j)) > 0)
					System.out.print(set[j]);
			}
			
			System.out.println();
		}
	}
	
	// Driver program to test printPowerSet
	public static void main (String[] args)
	{
		char []set = {'a', 'b', 'c'};
		printPowerSet(set, 3);
	}
}

// This code is contributed by anuj_67.

```

**Output**

a
b
ab
c
ac
bc
abc

**Time Complexity:** O(n2<sup>n</sup>)  
**Auxiliary Space:** O(1)

**Method 2: (sorted by cardinality)**

In auxiliary array of bool set all elements to 0. That represent an empty set. Set first element of auxiliary array to 1 and generate all permutations to produce all subsets with one element. Then set the second element to 1 which will produce all subsets with two elements, repeat until all elements are included.

Below is the implementation of the above approach.
```java
// Java program for the above approach

import java.util.*;

class GFG
{

// A function to reverse only the indices in the
// range [l, r]
static int[] reverse(int[] arr, int l, int r)
{
	int d = (r - l + 1) / 2;
	for (int i = 0; i < d; i++) {
	int t = arr[l + i];
	arr[l + i] = arr[r - i];
	arr[r - i] = t;
	}
	return arr;
}
// A function which gives previous
// permutation of the array
// and returns true if a permutation
// exists.
static boolean prev_permutation(int[] str)
{
	// Find index of the last
	// element of the string
	int n = str.length - 1;

	// Find largest index i such
	// that str[i - 1] > str[i]
	int i = n;
	while (i > 0 && str[i - 1] <= str[i]) {
	i--;
	}

	// If string is sorted in
	// ascending order we're
	// at the last permutation
	if (i <= 0) {
	return false;
	}

	// Note - str[i..n] is sorted
	// in ascending order Find
	// rightmost element's index
	// that is less than str[i - 1]
	int j = i - 1;
	while (j + 1 <= n && str[j + 1] < str[i - 1]) {
	j++;
	}

	// Swap character at i-1 with j
	int temper = str[i - 1];
	str[i - 1] = str[j];
	str[j] = temper;

	// Reverse the substring [i..n]
	str = reverse(str, i, str.length - 1);

	return true;
}

// Function to print all the power set
static void printPowerSet(char[] set, int n)
{

	int[] contain = new int[n];
	for (int i = 0; i < n; i++)
	contain[i] = 0;

	// Empty subset
	System.out.println();
	for (int i = 0; i < n; i++) {
	contain[i] = 1;

	// To avoid changing original 'contain'
	// array creating a copy of it i.e.
	// "Contain"
	int[] Contain = new int[n];
	for (int indx = 0; indx < n; indx++) {
		Contain[indx] = contain[indx];
	}

	// All permutation
	do {
		for (int j = 0; j < n; j++) {
		if (Contain[j] != 0) {
			System.out.print(set[j]);
		}
		}
		System.out.print("\n");

	} while (prev_permutation(Contain));
	}
}

/*Driver code*/
public static void main(String[] args)
{
	char[] set = { 'a', 'b', 'c' };
	printPowerSet(set, 3);
}
}

// This code is contributed by phasing17

```

**Output**

a
b
c
ab
ac
bc
abc

**Time Complexity:** O(n2<sup>n</sup>)  
**Auxiliary Space:** O(n)

**Method 3:**   
This method is specific to the python programming language. We can iterate a loop over 0 to the length of the set to obtain and generate all possible combinations of that string with the iterable length. The program below will give the implementation of the above idea.   
 

Below is the implementation of the above approach.
```java
import java.util.*;

class GFG {

// Function to generate all possible combinations of
// elements from an array
public static List<List<Character> >
	combinations(char[] arr, int len)
{
	List<List<Character> > a = new ArrayList<>();
	fn(new ArrayList<>(), arr, a, 0, len);
	return a;
}

// Helper function to generate the combinations
private static void fn(List<Character> active,
						char[] rest,
						List<List<Character> > a,
						int start, int len)
{
	if (active.size() == len) {
	a.add(new ArrayList<>(active));
	}
	else {
	for (int i = start; i < rest.length; i++) {
		active.add(rest[i]);
		fn(active, rest, a, i + 1, len);
		active.remove(active.size() - 1);
	}
	}
}

// Function to print all possible subsets of a given set
// (string)
public static void printPowerset(char[] string)
{
	for (int i = 0; i <= string.length; i++) {

	// Displaying all the combinations
	for (List<Character> combination :
		combinations(string, i)) {
		for (var letter : combination)
		System.out.print(letter);
		System.out.print("\n");
	}
	}
}

// Driver code
public static void main(String[] args)
{
	char[] string = { 'a', 'b', 'c' };
	printPowerset(string);
}
}

// This code is contributed by phasing17

```

**Output**

a
b
c
ab
ac
bc
abc

**Time Complexity: O((2<sup>n</sup> * n<sup>2</sup>)**  
**Auxiliary Space: O(n2<sup>n</sup>)**

**Method 4:**

We can use backtrack here, we have two choices first consider that element then don’t consider that element. 

Below is the implementation of the above approach.

```java
import java.util.*;

class Main
{
	public static void findPowerSet(char []s, Deque<Character> res,int n){
		if (n == 0){
		for (Character element : res)
			System.out.print(element);
		System.out.println();
			return;
		}
		res.addLast(s[n - 1]);
		findPowerSet(s, res, n - 1);
		res.removeLast();				
		findPowerSet(s, res, n - 1);
	}

	public static void main(String[] args)
	{
		char []set = {'a', 'b', 'c'};
		Deque<Character> res = new ArrayDeque<>();
		findPowerSet(set, res, 3);
	}
}

```

**Output**

cba
cb
ca
c
ba
b
a

**Time Complexity:** O(2^n)

**Space Complexity:** O(n)

[**Recursive program to generate power set**](https://www.geeksforgeeks.org/recursive-program-to-generate-power-set/)  
Refer [Power Set in Java](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/) for implementation in Java and more methods to print power set.  
**References:**   
[http://en.wikipedia.org/wiki/Power_set](http://en.wikipedia.org/wiki/Power_set)  
