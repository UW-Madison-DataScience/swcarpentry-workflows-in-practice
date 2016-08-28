# Plan for Mistakes (or: Testing)
----

**Based on materials by Katy Huff, Rachel Slaybaugh, and Anthony
Scopatz, original document from [boot-camps](https://github.com/UW-Madison-ACI/boot-camps/blob/2015-06-03/python/testing/Readme.md)**

**NOTE: This lesson relies on the use of the `nose` testing framework for
  Python.  This testing framework is no longer supported.  The concepts
  introduced here are still relevant, but the specific syntax may not be.**

# What is testing?

Software testing is a process by which one or more expected behaviors
and results from a piece of software are exercised and confirmed. Well
chosen tests will confirm expected code behavior for the extreme
boundaries of the input domains, output ranges, parametric combinations,
and other behavioral **edge cases**.

# Why test software?

Unless you write flawless, bug-free, perfectly accurate, fully precise,
and predictable code **every time**, you must test your code in order to
trust it enough to answer in the affirmative to at least a few of the
following questions:

-   Does your code work?
-   **Always?**
-   Does it do what you think it does? ([Patriot Missile Failure](http://www.ima.umn.edu/~arnold/disasters/patriot.html))
-   Does it continue to work after changes are made?
-   Does it continue to work after system configurations or libraries
    are upgraded?
-   Does it respond properly for a full range of input parameters?
-   What about **edge and corner cases**?
-   What's the limit on that input parameter?
-   How will it affect your
    [publications](http://www.nature.com/news/2010/101013/full/467775a.html)?

## Verification

*Verification* is the process of asking, "Have we built the software
correctly?" That is, is the code bug free, precise, accurate, and
repeatable?

## Validation

*Validation* is the process of asking, "Have we built the right
software?" That is, is the code designed in such a way as to produce the
answers we are interested in, data we want, etc.

## Uncertainty Quantification

*Uncertainty Quantification* is the process of asking, "Given that our
algorithm may not be deterministic, was our execution within acceptable
error bounds?" This is particularly important for anything which uses
random numbers, eg Monte Carlo methods.

# Starting to test

## Our scenario

Suppose that we want to write our own set of Python functions to 
perform basic statistical tasks.  We want to develop them in a robust 
way, to make sure that when we use them in our analysis, our answers 
are correct.  Thus, we will be writing tests as part of our development 
process.  

## Getting started

We'll be creating our Python files inside a new directory.  Create a new 
directory on your Desktop called `simplestats`.  Open up a basic text editor. Also 
open a terminal window and `cd` to our new `simplestats` directory: 

```
cd Desktop/simplestats
```

Using your text editor, create a new file named `stats.py` and save it in 
the `simplestats` directory.  Then copy and paste the following 
function into the `stats.py` to get started.  

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    total = sum(vals)
    length = len(vals)
    return total/length
```

## Testing?  

The most naive test is simply printing out an example of our function, and 
checking ourselves whether the answer is correct.  

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    total = sum(vals)
    length = len(vals)
    return total/length
    
print(mean([2, 4]))
```

We can run this code using `python` from the command line: 

```bash
python stats.py
```

## First, version control

In your command line window, use `git add` and `git commit` to commit 
our new `stats.py` file.  Remember that we need to use `git init` once 
at the start to initialize the repository!  

```
git init
git add stats.py
git commit -m "starting to work on stats functions"
```

## Second, what could go wrong?  

We've include one very informal test in our program.  But this isn't 
enough to produce a bug-free piece of software.  What are some things 
we need to consider in advance?  

# Assertions

Assertions and exceptions are a way to test *within* the program, to make 
sure that the pieces of your function are behaving as you would expect.  
We'll start by covering assertions, and get to exceptions.  

An `assert` is like a specialized "if/then" statement for catching errors.  The 
`assert` command will make your program stop if the condition is not true
and is common when writing tests.

We want to catch the error that would happen if a string was passed instead of 
a list of values.  

First of all, Python will catch this on its own: 
```python
print(mean("hello"))
```

But we'd like to include a more descriptive message, and control how 
the assertion happens.  

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    assert type(vals) is list, 'Input format is incorrect'
    total = sum(vals)
    length = len(vals)
    return total/length
```

**Practice using git:** Commit this addition to the repository

    git add stats.py
    git commit -m "Adding assert to catch input errors" 

# Unit Tests

## Create Unit Test Functions

If we make the print statement we've been using so far into a function, using 
asserts, we can make these print 
statements more meaningful.  Let's make these changes to `stats.py`: 

```python
def test_mean():
	assert mean([2,4]) == 3.0, 'Simple mean test'
```

To make it even easier to test, we can add some lines at the bottom of
`stats.py` to run each of our tests:

```python
test_mean()
```

**Practice using git:** Commit this addition to the repository

    git add stats.py
    git commit -m "Adding real test function" 

## Edge Cases

One of the challenges of testing is 
to determine what the *edge cases* might
be.  Here are some cases that we might try for the mean function

* different lengths of lists:
    * [2, 4, 6]
    * [2, 4, 6, 8]
* negative numbers:
    * [-4, -2]
    * [-2, 2, 4]
* floating point numbers:
    * [2.0, 4.0, 6.0]
    * [2.5, 4.5, 6.0]

Edge cases are important because they may reveal important decisions you need 
to make about our software, and its design.  We will also be turning each 
edge case into something called a "unit test", where it tests one piece of 
our code - in this case, our `mean` function.  

The edge case we'll consider is an empty list - what should we do with that input?  

If we add the following statement to the bottom of `stats.py`, 

```python
def test_empty_list():
    assert mean([]) is None, 'Empty list test'```
```

What happens if we run `python stats.py`?  

### Short Exercise

Using an if/else statement, how can you adapt the current function to 
handle the empty list case?  

Commit this addition to the repository

    git add stats.py
    git commit -m "Handling example of empty list" 

### Short Exercise

1. Add one more test function, testing a set of values of your choice.   
2. **Practice using git:** Commit your changes to the repository

		git add test_stats.py
		git commit -m "Added more test functions"

Example test: 

```python
def test_float_mean():
    """Test some standard behavior when the result is not an integer."""
    assert(mean([1, .5, .5]) == .666)
```

# Test Organization

> "It’s not that we don’t test our code, it’s that we don’t store our tests so they can be re-run automatically."
> 
> -- [Hadley Wickham](https://journal.r-project.org/archive/2011-1/RJournal_2011-1_Wickham.pdf)

## Separating Tests

It is more common to place tests in a different file so that they don't
clutter the module that does the real work.  Let's move our tests to a new
file called `test_stats.py`.  Now, our `stats.py` file contains only:

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    assert type(vals) is list, 'Input format is incorrect'
    total = sum(vals)
    length = len(vals)
    if length == 0:
    	return None
    else
    	return total/length
```

and our `test_stats.py` file contains:

```python
from stats import mean

def test_mean():
	assert mean([2,4]) == 3.0, 'Simple mean test'

def test_empty_list():
    assert mean([]) is None, 'Empty list test'

def test_float_mean():
    """Test some standard behavior when the result is not an integer."""
    assert(mean([1, .5, .5]) == .666)
```

Commit your changes to the repository

	git add test_stats.py
	git commit -m "moving tests into a new file"

## Nose: A Python Testing Framework

We could start adding some lines to give us more information about each test
and why it might fail, but that could get tedious as we write basically the
same things over and over for each test.  Since we don't want to repeat
ourselves, we might write some functions to keep track of the expected result,
and report when it doesn't match the observed results.  However, that seems
like something that many people need, so maybe someone else did that already,
and we don't want to repeat others, either.

The testing framework we'll discuss today is called `nose`. However, there are
several other testing frameworks available in most languages. Most notably there
is [JUnit](http://www.junit.org/) in Java which can arguably attributed to
inventing the testing framework. Google also provides a [test
framework](http://code.google.com/p/googletest/) for C++ applications (note, there's
also [CTest](http://cmake.org/Wiki/CMake/Testing_With_CTest)).  There
is at least one testing framework for R:
[testthat](http://cran.r-project.org/web/packages/testthat/index.html).  

### Nosetests

Once `nose` is installed, you can run it in any directory and it will 
find files that begin with `Test-`, `Test_`, `test-`, or
`test_`. It will then run any functions it finds in these files (which 
it assumes to be all of your tests).  
<!-- Specifically, these satisfy the testMatch regular expression
`[Tt]est[-_]`. (You can also teach `nose` to find tests by declaring them
in the unittest.TestCase subclasses that you create in your code. You
can also create test functions which are not unittest.TestCase
subclasses if they are named with the configured testMatch regular
expression.) -->

Since the `nose` package finds the tests and runs them automatically, we don't
need to include lines that run the tests.  We can remove the lines that call
the tests and just use our existing `test_stat.py` file like this:

    nosetests test_stat.py

Commit your changes!  

### Nose Functions

`nose` also has a set of specific "assert-like" functions, that can be useful 
in writing tests.  The simplest case is the `assert_equal` function: 

```python
from nose.tools import assert_equal

def test_mean():
    """Test some standard behavior of the mean() function."""
    assert_equal(mean([2, 4]), 3, "Basic mean test fails")
```

### Short Exercise

Change our "empty list" test to use `assert_equal`.  Commit your changes.  

    git add test_stats.py
    git commit -m "Introduced nose functions"

`assert_equal` is not the only tool we can use.  `nose` defines many other 
convenient assert functions which can
be used to test more specific aspects of the code base.

```python
from nose.tools import assert_equal, assert_almost_equal, assert_true, \
    assert_false, assert_raises, assert_is_instance

assert_equal(a, b)
assert_almost_equal(a, b)
assert_true(a)
assert_false(a)
assert_raises(exception, func, *args, **kwargs)
assert_is_instance(a, b)
# and many more!
```

Let's add this to our code: 
```python
from nose.tools import assert_equal, assert_almost_equal

def test_float_mean():
    """Test some standard behavior when the result is not an integer."""
    assert_amost_equal(mean([1, .5, .5]) == .66, 1)
```

And commit changes.  

# A Testing Development Workflow

Maybe we want our function to be able to handle the following case: 

```python
mean(['1','2','3'])
```

(If you think this is farfetched, most scripting languages will read information 
from the command line and files as strings.  So this is more possible than you 
might think!)  

Let's add a test to our file and try to edit the function to handle this case.  

```python
def test_str_list_mean():
    """Create special list case"""
    assert_equal(mean(['1','2','3']), 2)
```

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    assert type(vals) is list, 'Input format is incorrect'
    
    new_vals = []
    for num in vals: 
    	new_vals.append(int(num))
	
    total = sum(new_vals)
    length = len(new_vals)
    if length == 0:
    	return None
    else
    	return total/length
```

Now run our tests again with `nosetests`.  It's broken!  What didn't work and 
how can we fix it?  

This shows the benefit of having a test suite to catch our mistakes as we edit 
our code and commit changes.  

# Exceptions

What happens if someone tries to use this function with real (non-numerical) strings?

```python
mean(['hello','world'])
```

Some mistakes don't just give a wrong answer, but fail to even finish.  Python
provides a mechanism to deal with this called **exceptions**.  

In this example, Python automatically *raises* a ValueError exception when we
try to take the sum of a string.

In this case, we can add a test for the expected behavior: raising a TypeError
exception, by using the nose tool `assert_raises`:

```python
def test_string_mean():
    assert_raises(ValueError, mean, ['hello','world'])
```

**Practice using git:** Commit this change to the repository

    git add test_stats.py
    git commit -m "Added a test for exceptions when passing in non-numeric results."

We can provide some extra information to the user by catching the TypeError exception:

```python
def mean(vals):
    """Calculate the arithmetic mean of a list of numbers in vals"""
    try:
        total = sum(vals)
        length = len(vals)
    except ValueError:
        raise ValueError("The list contains non-numeric elements")
    return total/length
```
**Practice using git:** Commit this change to the repository

    git add test_stats.py
    git commit -m "Added extra error message for TypeError."

# When should we test?

The three right answers are:

-   **ALWAYS!**
-   **EARLY!**
-   **OFTEN!**

The longer answer is that testing either before or after your software
is written will improve your code, but testing after your program is
used for something important is too late.

If we have a robust set of tests, we can run them before adding
something new and after adding something new. If the tests give the same
results (as appropriate), we can have some assurance that we didn't
wreck anything. The same idea applies to making changes in your system
configuration, updating support codes, etc.

Another important feature of testing is that it helps you remember what
all the parts of your code do. If you are working on a large project
over three years and you end up with 200 classes, it may be hard to
remember what the widget class does in detail. If you have a test that
checks all of the widget's functionality, you can look at the test to
remember what it's supposed to do.

# Who should test?

In a collaborative coding environment, where many developers contribute
to the same code base, developers should be responsible individually for
testing the functions they create and collectively for testing the code
as a whole.

Professionals often test their code, and take pride in test coverage,
the percent of their functions that they feel confident are
comprehensively tested.

* * * * *

# Test Driven Development

Test driven development (TDD) is a philosophy whereby the developer
creates code by **writing the tests first**. That is to say you write the
tests *before* writing the associated code!

This is an iterative process whereby you write a test then write the
minimum amount code to make the test pass. If a new feature is needed,
another test is written and the code is expanded to meet this new use
case. This continues until the code does what is needed.

TDD operates on the YAGNI principle (You Ain't Gonna Need It). People
who diligently follow TDD swear by its effectiveness. This development
style was put forth most strongly by [Kent Beck in
2002](http://www.amazon.com/Test-Driven-Development-By-Example/dp/0321146530).

## A TDD Example

Say you want to write a std() function which computes the
[Standard Deviation](http://en.wikipedia.org/wiki/Standard_deviation). You
would - of course - start by writing the test, possibly testing a single set
of numbers, by adding this to `test_stats.py`:

```python
from nose.tools import assert_equal, assert_almost_equal

def test_std1():
    obs = std([0.0, 2.0])
    exp = 1.0
    assert_equal(obs, exp)
```

You would *then* go ahead and write the actual function:

```python
def std(vals):
    # you snarky so-and-so
    return 1.0
```

**Practice using git:** Since this works, commit the change to the repository

    git add stats.py test_stats.py
    git commit -m "Added a test for std() and then a function that passes the test."

And that is it, right?! Well, not quite. This implementation fails for
most other values. Adding tests we see that:

```python
def test_std1():
    obs = std([0.0, 2.0])
    exp = 1.0
    assert_equal(obs, exp)

def test_std2():
    obs = std([])
    exp = 0.0
    assert_equal(obs, exp)

def test_std3():
    obs = std([0.0, 4.0])
    exp = 2.0
    assert_equal(obs, exp)
```

These extra tests now require that we bother to implement at least a slightly 
more reasonable function:

```python
def std(vals):
    # a little better
    if len(vals) == 0:
        return 0.0
    return vals[-1] / 2.0
```

**Practice using git:** Since this works again, commit the change to the repository

    git add stats.py test_stats.py
    git commit -m "Added moore tests for std() and updated function so that is passes all tests."

However, this function still fails whenever vals has more than two elements or
the first element is not zero. Time for more tests!

```python
def test_std1():
    obs = std([0.0, 2.0])
    exp = 1.0
    assert_equal(obs, exp)

def test_std2():
    obs = std([])
    exp = 0.0
    assert_equal(obs, exp)

def test_std3():
    obs = std([0.0, 4.0])
    exp = 2.0
    assert_equal(obs, exp)

def test_std4():
    obs = std([1.0, 3.0])
    exp = 1.0
    assert_equal(obs, exp)

def test_std5():
    obs = std([1.0, 1.0, 1.0])
    exp = 0.0
    assert_equal(obs, exp)
```

At this point, we had better go ahead and try do the right thing...

```python
def std(vals):
    # finally, some math
    n = len(vals)
    if n == 0:
        return 0.0
    mu = sum(vals) / n
    var = 0.0
    for val in vals:
        var = var + (val - mu)**2
    return (var / n)**0.5
```

**Practice using git:** Since this works again, commit the change to the repository

    git add stats.py test_stats.py
    git commit -m "Added more tests for std() and updated function so that is passes all tests."

Here it becomes very tempting to take an extended coffee break or
possibly a power lunch. But then you remember those pesky infinite values!
Perhaps the right thing to do here is to just be undefined.  Infinity in 
Python may be represented by any literal float greater than or equal to 1e309.

```python
def test_std1():
    obs = std([0.0, 2.0])
    exp = 1.0
    assert_equal(obs, exp)

def test_std2():
    obs = std([])
    exp = 0.0
    assert_equal(obs, exp)

def test_std3():
    obs = std([0.0, 4.0])
    exp = 2.0
    assert_equal(obs, exp)

def test_std4():
    obs = std([1.0, 3.0])
    exp = 1.0
    assert_equal(obs, exp)

def test_std5():
    obs = std([1.0, 1.0, 1.0])
    exp = 0.0
    assert_equal(obs, exp)

def test_std6():
    obs = std([1e500])
    exp = NotImplemented
    assert_equal(obs, exp)

def test_std7():
    obs = std([0.0, 1e4242])
    exp = NotImplemented
    assert_equal(obs, exp)
```

This means that it is time to add the appropriate case to the function
itself:

```python
def std(vals):
    # sequence and you shall find
    n = len(vals)
    if n == 0:
        return 0.0
    mu = sum(vals) / n
    if mu == 1e500:
        return NotImplemented
    var = 0.0
    for val in vals:
        var = var + (val - mu)**2
    return (var / n)**0.5
```

**Practice using git:** Since this works again, commit the change to the repository

    git add stats.py test_stats.py
    git commit -m "Added tests for infinity in std() and updated function so that is passes all tests."


## Quality Assurance Exercise

Can you think of other tests to make for the ``std()`` function? I promise there
are at least two.
<!---
	1. How about std(string) or std(array)?
	2. How about std(None)?
--->

Implement one new test in test_stats.py, run nosetests, and if it fails, implement
a more robust function for that case.

And thus - finally - we have a robust function together with working
tests!

## Exercise: A different function

Try your new test-driven development chops by implementing the ``var()``
function, noting that the variance is the square of the standard devation.

# How are tests written?

The type of tests that are written is determined by the testing
framework you adopt. Don't worry, there are a lot of choices.

## Types of Tests

**Exceptions:** Exceptions can be thought of as type of runtime test.
They alert the user to exceptional behavior in the code. Often,
exceptions are related to functions that depend on input that is unknown
at compile time. Checks that occur within the code to handle exceptional
behavior that results from this type of input are called Exceptions.

**Unit Tests:** Unit tests are a type of test which test the fundamental
units of a program's functionality. Often, this is on the class or
function level of detail. However what defines a *code unit* is not
formally defined.

To test functions and classes, the interfaces (API) - rather than the
implementation - should be tested. Treating the implementation as a
black box, we can probe the expected behavior with boundary cases for
the inputs.

**System Tests:** System level tests are intended to test the code as a
whole. As opposed to unit tests, system tests ask for the behavior as a
whole. This sort of testing involves comparison with other validated
codes, analytical solutions, etc.

**Regression Tests:** A regression test ensures that new code does
change anything. If you change the default answer, for example, or add a
new question, you'll need to make sure that missing entries are still
found and fixed.

**Integration Tests:** Integration tests query the ability of the code
to integrate well with the system configuration and third party
libraries and modules. This type of test is essential for codes that
depend on libraries which might be updated independently of your code or
when your code might be used by a number of users who may have various
versions of libraries.

**Test Suites:** Putting a series of unit tests into a collection of
modules creates a test suite. Typically the suite as a whole is
executed (rather than each test individually) when verifying that the
code base still functions after changes have been made.

# Elements of a Test

**Behavior:** The behavior you want to test. For example, you might want
to test the fun() function.

**Expected Result:** This might be a single number, a range of numbers,
a new fully defined object, a system state, an exception, etc. When we
run the fun() function, we expect to generate some fun. If we don't
generate any fun, the fun() function should fail its test.
Alternatively, if it does create some fun, the fun() function should
pass this test. The expected result should known *a priori*. For
numerical functions, this is result is ideally analytically determined
even if the function being tested isn't.

**Assertions:** Require that some conditional be true. If the
conditional is false, the test fails.

**Fixtures:** Sometimes you have to do some legwork to create the
objects that are necessary to run one or many tests. These objects are
called fixtures as they are not really part of the test themselves but
rather involve getting the computer into the appropriate state.

For example, since fun varies a lot between people, the fun() function
is a method of the Person class. In order to check the fun function,
then, we need to create an appropriate Person object on which to run
fun().

**Setup and teardown:** Creating fixtures is often done in a call to a
setup function. Deleting them and other cleanup is done in a teardown
function.

**The Big Picture:** Putting all this together, the testing algorithm is
often:

```python
setup()
test()
teardown()
```

But, sometimes it's the case that your tests change the fixtures. If so,
it's better for the setup() and teardown() functions to occur on either
side of each test. In that case, the testing algorithm should be:

```python
setup()
test1()
teardown()

setup()
test2()
teardown()

setup()
test3()
teardown()
```
