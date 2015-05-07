---
layout: post
title: A tale of recursion
---
Factorial is 1 2 6 24 120......

Mathematical recursive function for the above is fact(n) = n * fact(n-1)

Doing this manually for large numbers will take a lot of time. So lets write a computer program to make computer do the manual work.

```scala
def fact(n : Int):Int = n match 
   {
	case 1 => 1
	case _ => n * fact(n-1)
   }
```

This works and here is how stack frame is going to look for fact(6)

###Calling Functions	
	fact(1)*2		
	fact(2)*3		
	fact(3)*4		
	fact(4)*5		
	fact(5)*6		
	fact(6) 		

###Returning Functions

	1*2		//This frame is  cleared once it returns 1*2 down.	
	1*2*3
	1*2*3*4
	1*2*3*4*5
	1*2*3*4*5*6
	1*2*3*4*5*6

Here we are using 6 stack frames. Stack fills up, reaches base case, i.e. fact(1) and comes back down returning values and releasing stack frames. 	

> Stack Overflow!

What if we have a holder which stores 6*5*4*3*2 and when reaches base case, returns its value. No need of previous stack frames, just require the holder value at every step.

###Calling function
	fact(1,1*6*5*4*3*2) // reached base case, return holder's value
	fact(2,1*6*5*4*3)
	fact(3,1*6*5*4)
	fact(4,1*6*5)
	fact(5,1*6)	
	fact(6,1) // 1 is the initial value of holder
```scala
def fact_tail(n:Int, holder:Int):Int = n match
    {
	case 1 => holder
	case _ => fact_tail(n-1, n*holder)	
    }
```

> The last call of a recursive function is called Tail Call. The above implementation of a recursive function is called Tail Recursion. Concept is called Tail Call Optimization, which states that the last expression of a recursive function should be function itself and not some computation.

Fibonacci is 0 1 1 2 3 5 8 13......

Mathematical recursive function for the above is fib(n) = fib(n-1) + fib(n-2)

I hope you understood the concept, try implementing fibonacci using tail recursion concept. Give it a try, you will be able to make it. You can look at my solution later, it will stay here only :)  

```scala
def fib(n : Int):Int = n match
    {
	case 0 => 0
	case 1 => 1
	case _ => fib(n-1) + fib(n-2)
    }
```
```scala
def fib_tail(n: Int, a: Int = 1, b: Int = 1):Int = n match 
    {
      case 0 => 0
      case 1 | 2 => b
      case _ => fib_tail(n - 1, b, (a + b))
    }
```
 
