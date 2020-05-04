---
title: 'Class 10: Chapter 18: Inheritance / Unit Testing'
separator: '\-\-\-\-\-'
verticalSeparator: '\+\+\+\+\+'
theme: 'moon'
revealOptions:
    transition: 'fade'
---

### ITSE-1042 Intermediate Python
<span style="font-family:Helvetica Neue; font-weight:bold; color:#e49436">Class 10: Chapter 18: Inheritance / Unit Testing</span>
<br /><br />


-----

##### Chapter 18: Inheritance / Unit Testing

+++++

The language feature most often associated with object-oriented programming is inheritance. Inheritance is the ability to define a new class that is a modified version of an existing class.

Note:
In this chapter, we will be demonstrating inheritance using classes that represent playing cards, decks of cards, and poker hands.

+++++

parent class (superclass)


child class (parent)
Inherits all data and behaviors of parent class
Add additional info
Add additional behavior 
Override behavior

Note:
If you were to sum up your inheritance, this is what it would be. Before we hop into the book, let's summarize what inheritence looks like 

+++++

```python
class Vehicle(object):
	def __init__(self, year, make, model):
		self.year = year
		self.make = make
		self.model = model
	def __str__(self):
		return “This is a {} {} {}.”.format(year, make, model)
```

Note:
Last class we started looking classes. This should look very familiar with exception of the "(object)" at the end. This state is the same as what we wrote in the previous class. Today we are looking at inheritence which is defined between the parentheses.

+++++

```python
class Vehicle(object):
	def __init__(self, year, make, model):
		self.year = year
		self.make = make
		self.model = model
	def __str__(self):
		return “This is a {} {} {}.”.format(year, make, model)

class Car(Vehicle):
	def __str__(self):
		return “This car is a {} {} {}.”.format(year, make, model)
    def go(self):
		print(“vroom vroom. I’m a car.”)
```

Note:
This is an example of inheritance. As you can see, the class car inherits the vehicle class. To put it simply, this allows us the ability to not have to redefine the year, make and model. Looking at it more complexly, it allows us to establish a relationship between the two.

+++++

```python
class Vehicle(object):
	def __init__(self, year, make, model):
		 self.year = year
		 self.make = make
		 self.model = model
	def __str__(self):
		 return “This is a {} {} {}.”.format(year, make, model)

class Car(Vehicle):
	def __init__(self, year, make, model, mileage, body_type):
		 Vehicle.__init__(self, year, make, model)
		 self.body_type = body_type
	def __str__(self):
		 return “This car is a {} {} {}.”.format(year, make, model)
  def go(self):
		 print(“vroom vroom. I’m a car.”)
```

Note:
The previous slide didn't actually do anything with the inheritance. This class actually creates an instance of vehicle in the class.

+++++

```python
class Clock(object):
	def __init__(self, hour, minute, second):
         		self.hour = hour
		self.minute = minute
		self.second = second
		
class Calendar(object):
	def __init__(self, day, month, year):
         		self.day = day
		self.month = month
		self.year = year

class CalendarClock(Clock, Calendar):
	def __init__(self, day, month, year, hour, minute, second):
        Clock.__init__(self, hour, minute, second)
        Calendar.__init__(self, day, month, year)
```

Note:
We've seen single inheritance, but you can also have multiple inheritance and it works very similarly. 

+++++

##### 18.1 Card Objects

Open to page 171 (Chapter 18) covers the principles associated with objects and inheritance.   
Book Link (if needed): http://greenteapress.com/thinkpython2/thinkpython2.pdf  

+++++


- Chapter 18.3 (Homework) Add methods to PokerHand.py named has_pair, has_twopair, etc. 
  - This problem includes the following files from Chapter 18, which are also included with the Chapter 18 lab problems:
( https://github.com/cliffjsgit/chapter-18  and  http://thinkpython2.com/code ):      
    - Card.py      
      - A complete version of the Card, Deck and Hand classes in this chapter.      
    - PokerHand.py      
      - An incomplete implementation of a class that represents a poker hand, and some code that tests it.   
   
   
-----

##### Unit Testing


+++++

![Image](./assets/tdd.png)

Note:
If you we are going to talk testing, we also need to talk about the methodology behind it. One of the favorite approaches to unit testing is test driven development. This image is a great summary of Test Driven Development.
Another competing methodology is Behavior Driven Development. We aren't going to go in depth to either of these, but BDD takes a similar approach to TDD with writing tests first as well... just gives greater value in bigger picture viewing.

+++++

Testing is not fun, but it's necessary.

Note:
Aside from those two methods, there are even more ways to approach it that take ideas from those two, but write tests later. For example, if you don't do TDD or BDD.. you are probably coding first and testing later. The point of this all is that you should test always and test often. 
We'll now be looking at some examples of unit testing and how they can be helpful. For ease of learning, we'll just be taking an approach of TDD.

+++++

### Example Story

We need to check whether a given input string is a palindrome. 

Note:
We've done this before, but maybe not as well as we could have.
A side note, for our testing purposes, we are going to use nose which is a python package you will have to install to use. We'll talk more about other options later.

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	pass
```

Note:
We start off with just a barebones function so that we can call it and get a failure.

+++++

##### test.py
```python
from palindrome import is_palindrome

def test_palindrome_words():
	input = "noon"
	assert is_palindrome(input) == True
```

Note:
We then create a function to test it. Note, you have to import the function in order to test it. 
You also may notice that the function is named test\_palindrome\_words. This can be anything you want it to be. I would recommend sticking to a standard of test\_[function-identifier]\_[descriptor(s)]

+++++

```
philipulrich:~/workspace/class10 (master) $ nosetests
F
======================================================================
FAIL: test.test_palindrome_words
......................................................................
Traceback (most recent call last):
  File "/usr/local/lib/python3.4/dist-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/ubuntu/workspace/class7/test.py", line 5, in test_palindrome_words
    assert is_palindrome(input) == True
AssertionError
......................................................................
Ran 1 test in 0.006s
FAILED (failures=1)
```

Note:
We then can run this test and see what happens. As you can see from the results, it fails with an assertion error (this is one place where assert comes in very handy).

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	return strin == strin[::-1]
```

Note:
Now that we have a test ready, we can finish coding it and run it to see what happens.

+++++

```
philipulrich:~/workspace/class10 (master) $ nosetests
.
......................................................................
Ran 1 test in 0.005s
OK
```

Note:
Great, it works.

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	return strin == strin[::-1]
```

Note:
Are we satisfied now? Will this work for anything that will be inputted to it?

+++++

##### test.py
```python
from palindrome import is_palindrome

def test_palindrome_words():
	input = "noon"
	assert is_palindrome(input) == True

def test_palindrome_case_independent():
	input = "Noon"
	assert is_palindrome(input) == True
```

Note:
Let's make sure that case isn't an issue when testing. (Hint: it is in our current solution)

+++++

```
philipulrich:~/workspace/class7 (master) $ nosetests
.F
======================================================================
FAIL: test.test_palindrome_case_independent
......................................................................
Traceback (most recent call last):
  File "/usr/local/lib/python3.4/dist-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/ubuntu/workspace/class7/test.py", line 9, in test_palindrome_case_independent
    assert is_palindrome(input) == True
AssertionError
......................................................................
Ran 2 tests in 0.005s
FAILED (failures=1)
```

Note:
Ouch! It is an issue!

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	lstrin = strin.lower()
	return lstrin == lstrin[::-1]
```

Note:
Easy enough fix, make it lower!

+++++

```
philipulrich:~/workspace/class10 (master) $ nosetests
..
......................................................................
Ran 2 tests in 0.005s
OK
```

Note:
Easy enough fix. Now let's go fix a space case.

+++++

##### test.py
```python
from palindrome import is_palindrome

def test_palindrome_words():
	input = "noon"
	assert is_palindrome(input) == True

def test_palindrome_case_independent():
	input = "Noon"
	assert is_palindrome(input) == True
	
def test_palindrome_with_spaces():
	input = "    Noon       "
	assert is_palindrome(input) == True
```

Note:
If we put equal spaces on both sides, it would work. So make sure to specify uneven spaces.

+++++

```
philipulrich:~/workspace/class10 (master) $ nosetests
..F
======================================================================
FAIL: test.test_palindrome_with_spaces
......................................................................
Traceback (most recent call last):
  File "/usr/local/lib/python3.4/dist-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/ubuntu/workspace/class7/test.py", line 13, in test_palindrome_with_spaces
    assert is_palindrome(input) == True
AssertionError
......................................................................
Ran 3 tests in 0.005s
FAILED (failures=1)
```

Note:
Failure! Let's fix that. 

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	cstrin = strin.strip().lower()
	return cstrin == cstrin[::-1]
```

Note:
Now we are removing whitespace and switching to lowercase.

+++++

```
philipulrich:~/workspace/class7 (master) $ nosetests
…
......................................................................
Ran 3 tests in 0.005s
OK
```

Note:
Test again... good!

+++++

##### test.py
```python
from palindrome import is_palindrome

def test_palindrome_words():
	input = "noon"
	assert is_palindrome(input) == True

def test_palindrome_case_independent():
	input = "Noon"
	assert is_palindrome(input) == True
	
def test_palindrome_with_spaces():
	input = "    Noon       "
	assert is_palindrome(input) == True
	
def test_palindrome_with_spaces_between():
	input = "A man a plan a caret a ban a myriad a sum a lac a liar a hoop a pint a catalpa a gas an oil a bird a yell a vat a caw a pax a wag a tax a nay a ram a cap a yam a gay a tsar a wall a car a luger a ward a bin a woman a vassal a wolf a tuna a nit a pall a fret a watt a bay a daub a tan a cab a datum a gall a hat a fag a zap a say a jaw a lay a wet a gallop a tug a trot a trap a tram a torr a caper a top a tonk a toll a ball a fair a sax a minim a tenor a bass a passer a capital a rut an amen a ted a cabal a tang a sun an ass a maw a sag a jam a dam a sub a salt an axon a sail an ad a wadi a radian a room a rood a rip a tad a pariah a revel a reel a reed a pool a plug a pin a peek a parabola a dog a pat a cud a nu a fan a pal a rum a nod an eta a lag an eel a batik a mug a mot a nap a maxim a mood a leek a grub a gob a gel a drab a citadel a total a cedar a tap a gag a rat a manor a bar a gal a cola a pap a yaw a tab a raj a gab a nag a pagan a bag a jar a bat a way a papa a local a gar a baron a mat a rag a gap a tar a decal a tot a led a tic a bard a leg a bog a burg a keel a doom a mix a map an atom a gum a kit a baleen a gala a ten a don a mural a pan a faun a ducat a pagoda a lob a rap a keep a nip a gulp a loop a deer a leer a lever a hair a pad a tapir a door a moor an aid a raid a wad an alias an ox an atlas a bus a madam a jag a saw a mass an anus a gnat a lab a cadet an em a natural a tip a caress a pass a baronet a minimax a sari a fall a ballot a knot a pot a rep a carrot a mart a part a tort a gut a poll a gateway a law a jay a sap a zag a fat a hall a gamut a dab a can a tabu a day a batt a waterfall a patina a nut a flow a lass a van a mow a nib a draw a regular a call a war a stay a gam a yap a cam a ray an ax a tag a wax a paw a cat a valley a drib a lion a saga a plat a catnip a pooh a rail a calamus a dairyman a bater a canal panama"
	assert is_palindrome(input) == True
```

Note:
Now we are testing with spaces between the words with a 540 word palindrome. A little, much, but why not?

+++++

```
philipulrich:~/workspace/class10 (master) $ nosetests
..F
======================================================================
FAIL: test.test_palindrome_with_spaces
......................................................................
Traceback (most recent call last):
  File "/usr/local/lib/python3.4/dist-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/ubuntu/workspace/class7/test.py", line 13, in test_palindrome_with_spaces
    assert is_palindrome(input) == True
AssertionError
......................................................................
Ran 4 tests in 0.005s
FAILED (failures=1)
```

Note:
Another failure. Let's fix it!

+++++

##### palindrome.py
```python
def is_palindrome(strin): 
	cstrin = strin.replace(" ", "").lower()
	return cstrin == cstrin[::-1]
```

Note:
We replaced strip with replace and opted to just remove all whitespace.

+++++

```
philipulrich:~/workspace/class7 (master) $ nosetests
….
......................................................................
Ran 4 tests in 0.005s
OK
```

Note:
Awesome! Fixed. 

+++++

Testing is important to ensure that your code is quality. As you can see though, it adds additional time to the development process. In this case, however, if we did not test… we would have missed quite a lot of potential problems. 

Note:
We obviously didn't fix all the issues yet, but you get the point. Let's move on and we can practice at the end.

+++++

In order for tests to be good, they must be:

- Consistent / Reliable
- Clear
- Quick
- Offer Full Coverage

Note:
Tests require four attributes to be good. Keep these in mind when coding and it will help you greatly.

+++++

We will be looking at three testing frameworks:

- nose 
- unittest
- py.test

Note:
Moving on to testing frameworks, we will be comparing 3. unittest is included in the python library. The other two are third party.

+++++

#### nose

##### Pros:
- works with unittest
- django (and others) support
- advanced features
- lots of plugins
- IDE support

##### Cons:
- not a standard

+++++

#### unittest

##### Pros:
- similar to other languages tests
- part of standard python library
- IDE support
- widely used

##### Cons:
- not pretty/pythonic
- lots of code
- no autodiscovery
- no advanced features

+++++

#### py.test

##### Pros:
- test autodiscovery 
- easy to write/run
- advanced features
- lots of plugins

##### Cons:
- not standard
- little IDE support

+++++

Tests compared!

Note:
Not sold on using something other than unittest? try these examples of our first test out for size.

+++++

##### nose

```python
def test_palindrome_words():
    input = "noon"
    assert is_palindrome(input) == True
```

##### py.test

```python
def test_palindrome_words():
    input = "noon"
    assert is_palindrome(input) == True
```

Note:
Nose and py.test are the same in this case (and in many ways)

+++++

##### unittest

```python
import unittest

class TestPalindrome(unittest.TestCase):
	def test_palindrome_words():
    		input = "noon"
    		self.assertTrue(is_palindrome(input))
```

Note:
and this is unittest... I'll pass on writing that...

+++++

We will now write some nose tests for the previous code we have written.

-----

Homework is 18.3

No homework on unit testing, but it wouldn't hurt to play around with it. 



