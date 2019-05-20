# Lesson 4: Efficiency 

1. Efficiency

We said earlier that this Nanodegree program is about how to write code to **solve problems** and to do so **efficiently**.

Previously, we looked at some basic aspects of solving problems--but we didn't really think too much about whether our solutions were efficient. 

**Space and time**

When we refer to *efficiency* of a program, we aren't just thinking about its speed--we're considering both the **time** it will take to run the program *and* the amount of **space** the program will require in the computer's memory. Often there will be a trade-off between the two, where you can design a program that runs faster by slecting a data structure that takes up more space--or vice versa. 


--> Efficiency is perhaps the most important concept in this course. 

--> Efficiency a.k.a. complexity is how well you're using your computer's resources to get a particular job done. 

You can think of it as:

* How long does your code take to run? 
* How much storage space do you need?

**Algorithms**

An **algorithm** is essentially a *series of steps for solving a problem.* Usually, an algorithm takes some kind of input (such as an unsorted list) and then produces the desired output (such as a sorted list). 

For any given problem, there are usually many different algorithms that will get you to exactly the same end result. But some will be more efficient than others. To be an effective problem solver, you'll need to develop the ability too look at a problem and identify different algorithms that could be used--and then contrast those algorithms to consider which will be more or less efficient. 

**But Computers are so fast!**

Sometimes it seems like computers run programs so quickly that efficiency shouldn't really matter. And in some cases, this is true--one version of a program may take 10 times longer than another, but they both still run so quickly that it has no real impact. 

But in other  cases, a small difference in how your code is written--or a tiny change in the type of data structure you use--can mean the difference between a program that runs in a fraction of a millisecond and a program that takes hours (or even years!) to run. 


2. Quantifying Efficiency 

It's fine to say "this algorithm is more efficient than that algorithm", but can we be more specific than that? Can we quantify things and say *how much* more efficient the algorithm is?

Let's look at a simple example, so that we have something specific to consider. 

Question 1:

```Python 
def some_function(n):
	for i in range(2):
		n += 100
	return n
```
What does it do?

**Adds 200 to the given input**

Question 2:

```Python
def other_function(n):
	for i in range(100):
		n += 2
	return n
```
What does it do?

**Adds 200 to the given input.**

Question 3:

So these functions have exactly the same end result. But can you guess which one is more efficient?

Compare:

```Python 
def some_function(n):
	for i in range(2):
		n += 100
	return n

def other_function(n):
	for i in range(100):
		n += 2
	return n
```

**some_function is more efficient**


Although the two functions have the exact same end result, one of them iterates many times to get to that result, while the other iterates only a couple of times. 

THis was admittedly rather impractical example( you could sip the for loop althogether and just add 200 to the input), but it nevertheless demonstrates one way in which efficiency can come up. 

___

**Counting lines**

With the above examples, what we basically did was count the number of lines of code that were executed. Let's look again at the first function:

```Python
def some_function(n):
	for i in range(2):
		n += 100
	return n
```
There are four lines in total, but the line inside the for loop will get run twice. So running this code will involve running 5 lines. 

Now let's look at the second example:

```Python
def other_function(n):
	for i in range(100):
		n += 2
	return n
```

In this case, the code inside the loop runs 100 times. So running this code will involve running 103 lines!

Counting lines of code is not a perfect way to quantify efficiency, and we'll see that there's a lot more to it as we go throught the program. But in this case, it's an easy way for use to approximate the difference in efficiency between the two solutions. We can see that if Python has to perform an addition operation 100 times, this will certainly take longer than if it only has to perform an addition operation twice! 

___

3. Input size and efficiency 

**Question 1:**

```Python 
def some_function(n):
	for i in range(2):
		n += 100
	return n
```

Suppose we call this function and give it the value 1, like this:

```Python
some_function(1)
```
And then we call it again, but give it the imput 1000:

```Python 
some_function(1000)
```

Will this change the number of lines of code that get run?

**No- the same number of lines will get run in both cases.**

B/c this function just adds 200 to the input--it doesn't care what size the input is to start with. 

**Question 2:**

New function:

```Python 
def say_hello(n):
	for i in range(n):
		print("Hello!")
```
Suppose we call it like this:

say_hello(3)

And we call it like this 

```Python 
say_hello(100)
```

Will this change the number of lines of code that get run?

** Yes-- say_hello(1000) will involve running more lines of code.**

--> This highlights a key idea:
      As the input to an algorithm increases, the time required to run the alogrithm may also increase. 

Notice that we said *may* increase. As we saw with the above examples, input size sometimes affects the run-time of the program and sometimes doesn't--it depends on the program. 

** The rate of increase

**Question 3:**

```Python 
def say_hello(n):
	for i in range(n):
		print("hello!")
```

Below are some different function calls. Match one with the number of lines of code that will get run.

* say_hello(1)      3
* say_hello(2)      4 
* say_hello(3)      5
* say_hello(4)      6

**Question 4:**

Here's another question about that same function (from the above exercise). When we increase the size of the input n by 1, how many more lines of code get run?

**When n goes up by 1, the number of lines run also goes up by 1.**


So here's one thing that we know about this function: As the input increases, the number of lines executed also increases.

But we can go further than that! We can also say that as the input increases, the number of lines executed increases by a proportional amount. Increasing the input by 1 will cause 1 more line to get run. Increasing the input by 10 will cause 10 more lines to get run. Any change in the input is tied to a consistent, proportional change in the number of lines executed. This type of relationship is called a **linear relationship**, and we can see why if we graph it:

![Derivative of Comparison of computational complexity, by Cmglee](01-n-comparison-computational-complexity.svg)

The horizontal axis, n, represents the size of the input (in this case, the number of times we want to print "Hello!").

The vertical axis, N, represents the number of operations that will be performed. In this case, we're thinking of an "operation" as a single line of Python code (which is not the most accurate, but it will do for now).

We can see that if we give the function a larger input, this will result in more operations. And we can see the rate at which this increase happens—the rate of increase is linear. Another way of saying this is that the number of operations increases at a constant rate.

If that doesn't quite seem clear yet, it may help to contrast it with an alternative possibility—a function where the operations increase at a rate that is not constant.

**Question 5:** 

Now here's a slightly modified version of the say_hello function:

```Python
def say_hello(n):
    for i in range(n):
        for i in range(n):
            print("Hello!")

Notice that it has a nested loop (a for loop inside another for loop!).

Below are some function calls. Match each one with the number of times "Hello!" will get printed.

```

**Question 6:**
```Python
Looking at the say_hello function from the above exercise, what can we say about the relationship between the input, n, and the number of times the function will print "Hello!"?
```

**The function will print "Hello!" exactly n-sqaured times (so say_hello(2) will print "Hello!" 2 * 2 or four times)**.


___

Notice that when the input goes up by a certain amount, the number of operations goes up by the square of that amount. If the input is 2, the number of operations is 2 to the second or 4. If the input is 3, the number of operations is 3 to the 2 or 9. 

To state this in general terms, if we have an input, n, then the number of operations will be n squared. This is what we would call a **quadractic** rate of increase. 
 

Let's graph both of these rates so we can see them together:


**Order**

We should note that when people refer to the rate of increase of an algorithm, they will sometimes instead use the term order. Or to put that another way:

The rate of increase of an algorithm is also referred to as the order of the algorithm.
For example, instead of saying "this relationship has a linear rate of increase", we could instead say, "the order of this relationship is linear".

On the next page, we'll introduce something called Big O Notation, and you'll see that the "O" in the name refers to the order of the rate of increase.

## 4. Big 0 Notation (1/2):


**Big O Notation**

When describing the efficiency of an algorithm, we could say something like "the run-time of the algorithm increases linearly with the input size". This can get wordy and it also lacks precision. So as an alternative, mathematicians developed a form of notation called big O notation.

The "O" in the name refers to the order of the function or algorithm in question. And that makes sense, because big O notation is used to describe the order—or rate of increase—in the run-time of an algorithm, in terms of the input size (n).

In this next video, Brynn will show some different examples of what the notation would actually look like in practice. This likely won't "click" for you right away, but don't worry—once you've gotten some experience applying it to real problems, it will be much more concrete.

___

The n in the Big O notation refers to the length of the input to your algorithm. 

```
O(0n + 1) == O(1)
```
**6. Worst Case and Approximation**


Suppose that we analyze an algorithm and decide that it has the following relationship between the input size, n, and the number of operations needed to carry out the algorithm:

N = $n^2$ + 5

Where n is the input size and N is the number of operations required.

For example, if we gave this algorithm an input of 2, the number of required operations would be $2^2+5$ or simply 9. 

___

The thing to notice in the above exercise, is this: In the $n^2+5$, 
5 has very little impact on the total efficiency—especially as the input size gets larger and larger. Asking the computer to do 10,005 operations vs. 10,000 operations makes little difference. Thus, it is the $n^2$ that we really care about the most, and the '+5' makes little difference.

Most of the time, when analyzing the efficiency of an algorithm, the most important thing to know is the order. In other words, we care a lot whether the algorithm's time-complexity has a linear order or a quadratic order (or some other order). This means that very often (in fact, most of the time) when you are asked to analyze an algorithm, you can do so by making an approximation that significantly simplifies things. In this next video, Brynn will discuss this concept and show how it's used with Big O Notation.


**Approximation**

Since, the amount of steps can vary widely based on the specific implementations, we normally use approximations when talking about efficiency in Big O notation. 
By approximating we are saying that "Some number of computations must be performed for each letter in the input."

**Worst Case**

When discussing efficiency, we often talk about it in terms of the worst-case scenario.

We focus on worst case because it puts a upper bound on the amount of time out code is going to take. 

You could aslo talk about efficiency in terms of the average case or even best case. 

*Make sure in your interview that you specify which case you are using: Best Case, Average Case, or Worst Case*

**7. Efficiency Practice**

```Python
def main(x,y):
    if True:
        z = x + y
    for i in range(10):
        z+=1
    return z

# The run time analysis is O(1): the function is constant because the run time # does not change as a function of the input.    
```


---

**8. Space Complexity**

You can also use the same notation that you use in time efficiency in space efficiency. 


When we refer to space complexity, we are talking about how efficient our algorithm is in terms of memory usage. This comes down to the datatypes of the variables we are using and their allocated space requirements. In Python, it's less clear how to do this due to the the underlying data structures using more memory for house keeping functions (as the language is actually written in C).

For example, in C/C++, an integer type takes up 4 bytes of memory to store the value, but in Python 3 an integer takes 14 bytes of space. Again, this extra space is used for housekeeping functions in the Python language.



