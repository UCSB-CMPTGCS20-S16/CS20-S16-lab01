# CS20-S16-lab01
UCSB-CMPTGCS20-S16, lab01 -- FtoC and CtoF with test cases

This lab is based on a session from the website http://cyber-dojo.org, created just for this course.

Here's the session: http://cyber-dojo.org/enter/show/B2D1B6D3D0

In this session, you have:
* a Python *module* called `tempConversions`
* a Python file with test cases called `tempConversions`

Briefly: your job is to fix the two functions defined in tempConversions so that they are correct.  Initially, it may appear that they *are* correct, because they are passing all of their test cases, as evidenced by the fact they when we click "test", the code appears "green".  However, we soon see that our tests are not complete enough.    So we first copy/paste two additional tests into the file `test_tempConversion.py`, and then the tests fail.   We then can correct the code and see that the functions are now correct.

Here is some more information about each of these files:

## `tempConversions.py`

* `tempConversions.py` is a Python *module*, i.e. a file containing definitions
* a module can be imported for use into another file.
* Specfically, the module `tempConversions` contains two function definitions, for `ftoC(fTemp)` and `ctoF(cTemp)`
* The function definitions given here are not correct.  They work for some parameter values, but not for others.

## `test_tempConversions.py`

* This file starts with the line `from tempConversions import *`
* The `*` on the previous line is called a *wildcard*.  In this case, the line means "import everything you possibly can from tempConversions, and make it available for use".
* There are then two function definitions that have names starting with `test_`.  They look like this:

```Python
def test_temp_conversions_fToC_32_0():
    assert fToC(32.0) == 0.0

def test_temp_conversions_cToF_0_32():
    assert cToF(0.0) == 32.0
```

* Each of these functions takes no parameters (as seen by the fact that we have an empty set of parens `()` between the name of the function and the colon (`:`).    
* The function has a single line of code that starts with `assert`
* What follows `assert` is a statement that is either True or False
* If the statement is True, the test case passes.  If it is False, the test case fails.

So the statement `assert cToF(0.0) == 32.0` asks the question: "when we evaluate the function cToF with the parameter value 0.0, is the value that is returned equal to 32.0?"  If the answer is yes, then the statement is true, and the test case will pass.

Note that you test for equality in Python, you must use `==` rather than `=`.   

* The reason is that `=` is used for *assignment*, i.e. giving a value to a variable.
* It isn't important to go into more detail on that right now, since we don't need assignment in this lab.

An aside: testing numbers with decimals for exact equality is risky.  It isn't likely to be a problem in this exercise, and because this is a very introductory exercise, we are glossing over it.  But I want to acknowledge it as an issue.  The "For further exploration" section below has further information on this topic, which we'll revisit later in the course.

## instructions

This file contains instructions, including two additional test cases to copy/paste into the file test_tempConversions.py

# For further exploration

The information below is not necessarily required to do this lab, but you may find it helpful or interesting.   It contains the answers to some questions that may come up as you try to complete the lab.

## Rules for function definitions

* Every Python function definition must start with a line in this format:
** `def`, exactly like that, followed by at least one space (usually exactly one).
** the name of the function (there are certain rules for these names, including no spaces in the name).
** a list of parameters in parens.  This list my be empty.  If there is more than one parameter, params are separated with commas.


## An aside about working with real numbers

Real numbers are numbers on the number line other than integers, such as -2.5, square root of 2, pi, and so forth.  

Python treats integers such as 2, 4, 100, and -42 differently from real numbers.  This is even true when we write an integer with a decimal point; that is 100 and 100.0 are treated differently in terms of Python's "internal processing", even though they represent the same number.

Python will be precise and exact in representing integers.  However, when representing real numbers, even ones that correspond to integers such as 100.0, there is always the potential for some error.  This is a consequence of the fact that the number of bits used to represent a number is finite, but the number of real numbers in any range is infinite.  

Thati is:
* If we use 32 bits, or 64 bits, or 128 bits to represent an integer, we know precisely how many integers we can represent, and we can be sure each one has a unique, exact representation.    
* Between any two real numbers, there is an uncountably infinite number of additional real numbers.  So, no matter how many bits we use, and no matter what range of numbers we choose to represent, we cannot represent them all exactly and precisely.  Therefore representations of real numbers are always an approximation, and there is always the potential for some error.  
 
This error is usually small and insignificant--but not always.  It can cause at least two kinds of problems:
* In calculations involving many steps, small errors can accmuulate into larger, more significant errors.  Knowing about this problem and designing ways to predict and control the error is part of a topic in Computer Science and Applied Math known as "numerical analysis".   
* When we test for equality, i.e. is cToF(100.0) == 212.0, there is the possibility that the calculation on the left gives us 212.0000000001  instead of 212.0000000000.  That tiny difference could cause the test case to fail, even though the calculation is as close as we can get.

So, in general, it's risky to test for exact equality with floating point numbers. Since this is designed to be a very introductory exercise, we are glossing over that detail.    The calculations we are doing are on numbers small enough that the number of bits of precision we have is likely to give us answers precise enough that the problem will not arise.

Later on, we'll see problems where this problem *does* present itself.  We'll see that the correct practice, when working with any kind of calculation involving real numbers (as opposed to integer) is to check whether the returned value is *approximately equal* to the value expected, i.e. that the difference between the two values is less than some *tolerance*.  This *tolerance* is usually very small, for example, 0.000001, or ten to the minus 6 (which can be written in Python either as `0.000001` or in scientific notation like this: `1.0E-6`).


