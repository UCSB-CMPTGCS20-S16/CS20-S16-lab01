# CS20-S16-lab01
UCSB-CMPTGCS20-S16, lab01 -- FtoC and CtoF with test cases

This lab is based on a session from the website http://cyber-dojo.org, created just for this course.T

Here's the session: http://cyber-dojo.org/enter/show/E5E50A0CDF

In this session, you have:
* a Python *module* called `tempConversions`
* a Python file with test cases called `tempConversions`

Briefly: your job is to fix the two functions defined in tempConversions so that they are correct.  Initially, it may appear that they *are* correct, because they are passing all of their test cases, as evidenced by the fact they when we click "test", the code appears "green".  However, we soon see that our tests are not complete enough.    So we first copy/paste two additional tests into the file `test_tempConversion.py`, and then the tests fail.   We then can correct the code and see that the functions are now correct.

Once you've tried the code in cyber-dojo.org, we'll go over how to do this in submit.cs as well.

# Step-by-Step

## Step 1: Start a new session

Navigate to  http://cyber-dojo.org/enter/show/E5E50A0CDF and click *start* to begin a new session.

You'll be assigned some "animal" as your avatar. Click OK to accept this animal.

Then you'll see some files listed on the left:

* instructions
* tempConversion.py
* test_tempConversion.py
* output
* cyber-dojo.sh

You can click each file's name to see and edit its code.

Take a moment, first to read the information below, as you click on each file and become familiar with the code inside.

Here is some more information about each of the files you'll find in this project.

### The file `tempConversions.py`

* `tempConversions.py` is a Python *module*, i.e. a file containing definitions
* a module can be imported for use into another file.
* Specfically, the module `tempConversions` contains two function definitions, for `ftoC(fTemp)` and `ctoF(cTemp)`
* The function definitions given here are not correct.  They work for some parameter values, but not for others.

### The file `test_tempConversions.py`

* This file starts with the line `from tempConversions import *`
* The `*` that ends this line is called a *wildcard*.  The meaning of this line of code is: "import everything you possibly can from tempConversions, and make it available for use".   Specifically, the function definitions for `ftoC(fTemp)` and `ctoF(cTemp)` are made available by this line of code.
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

### The file `instructions`

This file contains instructions, including two additional test cases to copy/paste into the file test_tempConversions.py

### The file `output`

This file shows the result of the last test that you have run.    If the previous test encountered any errors, they'll be shown in this file.   Unlike the other files, you don't have the capability to make changes here--you can only look at the file's contents.

### The file `cyber-dojo.sh`

This file contains the command that runs each time you click the test button.    You will not need to make any changes to this file.

Once you've looked over all of the code, you are ready to try running the code.

## Step 2: Click test--the tests will pass

Click test.  The tests will pass, and you'll see a green circle showing that they passed, and output that ends with this output (the `in 0.01 seconds` may be slightly different, but the `2 passed` should be there):

```
=========================== 2 passed in 0.01 seconds
===========================
```

So this seems fine.  But there's a problem: despite the two passing tests, the code is still incorrect!

The problem is that we haven't specified enough tests yet.

Look at the instructions file, and find two additional tests that look like this:

```Python
def test_temp_conversions_fToC_212_100():
    assert fToC(212.0) == 100.0

def test_temp_conversions_cToF_0_32():
    assert cToF(100.0) == 212.0
```

Copy/paste those into the `test_tempConversions.py` file.

Click test again.  The additional tests will fail.  You should see a red circle indicating the failures, and a message that 2 tests passed and two failed.   The failure output should look, more or less, like this (the formatting may be a bit off):

```
=================================== FAILURES ===================================
______________________ test_temp_conversions_fToC_212_100 ______________________

    def test_temp_conversions_fToC_212_100():
>       assert fToC(212.0) == 100.0
E       assert 180.0 == 100.0
E        +  where 180.0 = fToC(212.0)

test_tempConversion.py:11: AssertionError
_______________________ test_temp_conversions_cToF_0_32 ________________________

    def test_temp_conversions_cToF_0_32():
>       assert cToF(100.0) == 212.0
E       assert 132.0 == 212.0
E        +  where 132.0 = cToF(100.0)

test_tempConversion.py:14: AssertionError
====================== 2 failed, 1 passed in 0.02 seconds ======================
```

Look at the output above.  You'll see that the line `assert fToC(212.0) == 100.0` specifies that `fToC(212.0)` is supposed to evaluate to `100.0`.   (The `==` is the way we write *is equal to* in Python.)

However, this assertion failed.    Instead of `fToC(212.0)` evaluating to `212.0`, it evaluated to `180.0`, so something is awry.   There is a similar problem with the `cToF(100.0)` evaluating to `132.0` instead of `100.0`.

So, see if you can fix the code in `tempConversions.py` so that the tests pass.

This first involves changing the line in the definition of the `fToC(ftemp)` function that says:
```Python
  return ftemp - 32.0   # TODO: Fix this line of code
```

You'll need to correct the formula.  Keep in mind that in Python:
* The `*` symbol is used for multiplication.  In algebra, we can write `1.8x` to mean `1.8` multiplied by `x`, however, this does not work in Python.  In Python you must write `1.8 * x` if you want to multiply the variable `x` by 1.8.
* The `+` and `-` symbols are used for addition and subtraction
* The `/` symbol is used for division, e.g '9.0/5.0' means nine divided by five.  Note that if both numerator and denominator are integers, in Python 2, the result will be an integer.   In this case, the result is 1 (the 0.8 part is thrown away, not rounded up to 2).

Also, the order of operations in Python is that multiplication and division are done before addition and subtraction. Some examples: 
* If `x` is 5, then `x + 2 * 3` gives us 11, not 21.  The multiplication is perfomed before the addition.
* If `x` is 16, then `x - 6 / 2` gives us 13, not 5.   The division is performed before the subtraction.
* If you want to force the addition or subtraction to be done first, you must use parentheses, e. g. `(x + 2) * 3` or `(x - 6) / 2`

When you replace `return ftemp - 32.0` with the correct formula for converting a Fahrenheit temperature to Celsius, you should leave out the comment that says `# TODO: Fix this line of code `.

You'll also want to replace the similar line in the cToF function.

Each time you add some code, try clicking the test button again.  When you've fixed the formulas so that all four tests pass, you are ready to move on to the next step.

That will look like this:

```
=========================== 4 passed in 0.01 seconds
===========================
```

## Step 3: Prepare submission for submit.cs

Now that we've practiced this on the cyber-dojo.org site, let's do the same thing again, but this time, building our code in IDLE, and submitting to submit.cs.

As we do this, you may want to keep your cyber-dojo.org session open (unless you want to just do the entire process over again from scratch.)

There are a few steps involved:

* First, we'll check whether you have `pip` on your computer.  The `pip` program is the <b>P</b>ackage <b>I</b>nstaller for <b>P</b>ython, and with any luck, when you installed Python 2.7.11, `pip` came along for the ride.
* Second, we'll use `pip` to install `pytest` which is the testing package that the cyber-dojo.org site uses to run test cases on code.
* Third, we'll open up IDLE, and set up the same files that were in the cyber-dojo.org session.

### Step 3a: Checking whether you have pip

First, open up a command line on your computer, in whatever way is appropriate to your operating system:
* Mac OS X: Open a Terminal window (here's [how] (http://blog.teamtreehouse.com/introduction-to-the-mac-os-x-command-line))
* Windows: Open a Command Prompt window (here's [how](http://www.digitalcitizen.life/7-ways-launch-command-prompt-windows-7-windows-8))
* Linux: Open a shell prompt (If you need to ask how, I wonder: should you really be using Linux?)

The reason we need a command prompt is that we are going to install a Python module using the `pip` command.

The `pip` command allows us to extend the capabilities of Python with "add-ons". The add-on we going to add is one that helps us do testing.

First, make sure that the `pip` command works on your system.  Try typing `pip --version` and pressing enter
* That's two hyphens, i.e. `--` in front of the word `version`
* Here's an example of what that might look like:

```
Phills-MacBook-Pro:~ pconrad$ pip --version
pip 7.1.2 from /Library/Frameworks/Python.framework/Versions/2.7/lib/python2.7/site-packages (python 2.7)
Phills-MacBook-Pro:~ pconrad$ 
```

If you get output such as this, that's a good sign.

If instead, you get something like this, it's a bad sign: it means that `pip` is not installed on your system. In that case, post to Piazza, or ask for help during class or the instructor's office hours.

```
Phills-MacBook-Pro:~ pconrad$ pip --version
-bash: pip: command not found
Phills-MacBook-Pro:~ pconrad$ 
```

### Step 3b: Installing pytest


Assuming, though, that the `pip --version` command worked for you, try this: `pip install -U pytest`

If it works properly, you'll get some output that ends with `Successfully installed pytest-2.9.1`, such as this:

```
Phills-MacBook-Pro:~ pconrad$ pip install -U pytest
Collecting pytest
...
Successfully installed pytest-2.9.1
Phills-MacBook-Pro:~ pconrad$ 
```

### Step 3c: Make a cs20/lab01 folder


Somewhere on your computer's disk space (i.e. on your computer's hard drive), create a folder called cs20.  Inside that folder, create another folder called lab01.  

In general, its probably a good idea to keep your work for this class all in the same folder, and within that folder, create a separate folder for each lab.   This isn't exactly *required* (no-one is going to check), but it's probably a good habit to develop.   Also, the rest of the instructions will be written based on the assumption that you did things this way.  So, I'd strongly encourage you to do it. 

### Step 3d: Set up the files `tempConversions.py` and `test_tempConversions.py` in IDLE

Open IDLE.  You'll see the Python prompt `>>>` in the window that opens up automatically.

In IDLE, go to the File menu, and select New.   An empty window should pop up where you can type in code.

In that window, put the code from the `tempConversions.py` file that you were working with in the cyber-dojo.org session.   Save the file under the name `tempConversions.py`, inside the cs20/lab01 folder that you created earlier.

Now, do the same thing with a file called `test_tempConversions.py`&mdash;put the contents of `test_tempConversions.py` fron your cyber-dojo.org session into a file called `test_tempConversions.py` and then save it in the cs20/lab01 folder that you created.



TODO: CONTINUE FROM HERE




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


