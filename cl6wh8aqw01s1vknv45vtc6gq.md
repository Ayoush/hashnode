## Python Quick Interview Revision Notes - Part 1

# Introduction
Python is a:-
- **High-Level Language (HLL)**:- A high-level language has a higher level of abstraction from the computer and focuses more on the programming logic rather than the underlying hardware components such as memory addressing and register utilization. 

- ** Interpreted Language**:- An interpreted language is a language in which the implementations execute instructions directly without earlier compiling a program into machine language whereas a compiled language is converted into machine code so that the processor can execute it.

# Installation Tips
If you have installed a particular python version but after doing `python --version` you are still getting that old version then you have to simply run this command.

```
// Suppose you installed python 3.6
>>> python3.6 --version
Python 3.6.5
```
But if you want to use this as a default you have to alias the same in your bash profile file like this 
```
alias python=python3.6
```

# Strings and working with Textual Data
String or text can be defined in two ways either inside a single quote or a double quote. The only difference between the two is that within single quotes you don’t need to escape `"` (but you have to escape `'`) and vice versa. Example:-
```
>>> 'doesn\'t'  # use \' to escape the single quote...
"doesn't"
>>> "doesn't"  # ...or use double quotes instead
"doesn't"
>>> '"Yes," they said.'
'"Yes," they said.'
>>> "\"Yes,\" they said."
'"Yes," they said.'
>>> '"Isn\'t," they said.'
'"Isn\'t," they said.'
>>>""" Hello how are you ?
       ...This is a multiline string"""
>>> str[0]
P

+---+---+---+---+---+---+
 | P | y | t | h | o | n |
 +---+---+---+---+---+---+
 0   1   2   3   4   5   6
-6  -5  -4  -3  -2  -1
```

**String Replacement**

Now let's suppose you have a variable that contains some string and you want to form a sentence using that string.
Example:-
```
greetings = 'Hi'
designation = 'Mr'

message = designation + ' Ayoush said ' + greetings 
```
The same thing can be achieved using `format` function or `f` string. Example:-
```
greetings = 'Hi'
designation = 'Mr'

// Here the sequence is important

message = '{} Ayoush said {}'.format(designation, greetings)
// or
message = f'{designation} Ayoush said {greetings}'

// Using f string or format. You can do some advance formatting also.

message = f'{designation.upper()}' Ayoush said {greetings.lower()}'
```
*However there is one edge case between these two ways.* Let's take an example to explain further.
```
person = {'name': 'Ayoush', 'age': 27}
message = '{} + is + {} +  years old'.format(person['name'], person['age'])
```

This above statement will work fine but when we try to do the same with `f` string
```
message = f'{person['name']}  is {person['age']} years old'
```

**This statement will throw an error since as mentioned above we have to escape that single quote**. So if you wrap that thing in double quotes it will resolve
```
message = f"{person['name']}  is {person['age']} years old"
```

Some more advance examples:-
```
>>> n=1
>>> f'The two digit value for n is {n:02}'
01
>>> pi = 3.14567
>>> f'The two digit value for pi is {pi:.4f}'
3.1457
```

There are many things that you can do with a string. If you want to check that list of things that you can do, you can use the `dir` function. Example:-
```
>>> dir(greetings)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isascii', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'removeprefix', 'removesuffix', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
// Or you can use the help function
>>> help(str)
```
  ### Some points to remember:-
  - **Strings are immutable so if you try to replace any value in a string like `name='Ayoush'` and then      `name[0]='a'`, this will throw an error.**
  - **Since strings are immutable so in production, if you are doing string replacement, keep this in mind that every time you are adding a string to the same variable, it's not actually replacing the value but assigning a new address to the variable with an updated value. **


# Integer and Float
Some of the basic operations that we can perform are mentioned in the [Python Docs](https://docs.python.org/3/tutorial/introduction.html#numbers). There is no edge case that I encountered till now, if you have one, drop a comment and I will add it.


# List, Tuples, and Sets
 List and Tuples help us work with ordered data; sets are an unordered collection of data with no duplicates.
## Lists
```
>>> courses = ['Math', 'Japanese', 'History', 'CompSci']
>>> courses[0] 
'Math'
>>> courses[:2]
['Math', 'Japanese']
// Similar to string you can access a negative index starting from -1
// If you want to add something at the end just use the append() method
>>> courses.append('Art')
['Math', 'Japanese', 'History', 'CompSci', 'Art']
// If you want to add to a specific index, you can use insert()
>>> courses.insert(0, 'Art')
['Art', 'Math', 'Japanese', 'History', 'CompSci']
>>> courses = ['Math', 'Japanese', 'History', 'CompSci']
>>> courses_2 = ['Art', 'Hindi']
// Now if we insert and append the entire list will be inserted as a sub list
>>> courses.insert(0, courses_2)
[['Art', 'Hindi'], 'Math', 'Japanese', 'History', 'CompSci']
>>> courses.append(courses_2)
['Math', 'Japanese', 'History', 'CompSci', ['Art', 'Hindi']]
// for this we use the extend() method
>>> courses.extend(courses_2)
['Math', 'Japanese', 'History', 'CompSci', 'Art', 'Hindi']
// Some of the other functions that you should take care of are
// pop(), reverse(), sort(), sort(reverse=True), min(), max(), sum(), index()
>>> for index, course in enumerate(courses):
...     print(index, course)
0 Math
1 Japanese
2 History
3 CompSci
4 Art
5 Hindi
// if you want the index to start with 1 you can mention it like this in enumerate(courses, start=1)

// Now lets see slicing 
>>> num = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> num[2:-1]
[3, 4, 5, 6, 7, 8]
>>> num[2:-1:2]
[3, 5, 7]
// One more way to reverse a list
>>> num[::-1]
[9, 8, 7, 6, 5, 4, 3, 2, 1]
>>> num[2:-1:-1]
[]
>>> num[-1:2:-1]
[9, 8, 7, 6, 5, 4]
```

## Tuples
**`One major difference between List and Tuples are that lists are mutable(you can modify a list as we have seen with functions like insert, append, etc) but on the other hand tuples are immutable(can't be modified once assigned)`**
To explain this further here is an example for you:-
```
# Mutable
list1 = [1, 2, 3, 4, 5]
list2 = list1

print(list1)
print(list2)

list1[0] = 6

print(list1)
print(list2)

# Immutable
tuple1 = (1, 2, 3, 4, 5)
tuple2 = tuple1

print(tuple1)
print(tuple2)

tuple1[0] = 6

print(tuple1)
print(tuple2)

Output:-
[1, 2, 3, 4, 5]
[1, 2, 3, 4, 5]
[6, 2, 3, 4, 5]
[6, 2, 3, 4, 5]
(1, 2, 3, 4, 5)
(1, 2, 3, 4, 5)
Traceback (most recent call last):
  File "/Users/ayoushchourasia/Work/Interview/Python/list-tupes-sets.py", line 20, in <module>
    tuple1[0] = 6
TypeError: 'tuple' object does not support item assignment
```
## Sets
The sets as mentioned above are simply unordered collections that don't contain duplicates. `It is more optimized to find a value than list`
```
// Some of the major functions that sets are used for are intersections, difference, union and some more
set1 = {1, 2, 3, 4, 5}
set2 = {3, 4, 5, 6, 7}
print(set1.intersection(set2))
print(set1.difference(set2))
print(set1.union(set2))
print(set1.issuperset(set2))

Output:-
{3, 4, 5}
{1, 2}
{1, 2, 3, 4, 5, 6, 7}
False
```

## Dictionaries 
Dictionaries are the key-value pair.
```
\\ To get value for a key in a safer way by using the get method.
student = {'name': 'Ayoush', 'age': 27}
student.get('phone', 'Not Found')

\\ There are many other functions like pop, items, values etc.
\\ If you run a list command over dict, only its keys will be taken inside list
>>> student = {'name': 'Ayoush', 'age': 27}
>>> list(student)
['name', 'age']
>>> list(student.values())
['Ayoush', 27]
```

# List Comprehensions, Named-tuples
## List Comprehensions 
 It's a short way of creating a list.
```
nums = [1, 2, 3, 4, 5, 6, 7]
new_list = []
for n in nums:
    new_list.append(n)
print(new_list)

list_comprehended = [n for n in nums]
print(list_comprehended)

new_list = []
for n in nums:
    new_list.append(n*n)
print(new_list)

list_comprehended = [n*n for n in nums]
print(list_comprehended)

# Now if we want to add only even number
new_list = []
for n in nums:
    if n%2==0:
        new_list.append(n)
print(new_list)

list_comprehended = [n for n in nums if n%2==0]
print(list_comprehended)

# A little complicated one
new_list = []
for letter in 'abcd':
    for num in range(4):
        new_list.append((letter, num))
print(new_list)

list_comprehended = [(letter, num) for letter in 'abcd' for num in range(4)]
print(list_comprehended)

# The Same thing can be done with functions, these are a short form of `generator functions`
list_comprehended = (n*n for n in nums)
for i in list_comprehended:
    print(i)

Output:-
[1, 2, 3, 4, 5, 6, 7]
[1, 2, 3, 4, 5, 6, 7]
[1, 4, 9, 16, 25, 36, 49]
[1, 4, 9, 16, 25, 36, 49]
[2, 4, 6]
[2, 4, 6]
[('a', 0), ('a', 1), ('a', 2), ('a', 3), ('b', 0), ('b', 1), ('b', 2), ('b', 3), ('c', 0), ('c', 1), ('c', 2), ('c', 3), ('d', 0), ('d', 1), ('d', 2), ('d', 3)]
[('a', 0), ('a', 1), ('a', 2), ('a', 3), ('b', 0), ('b', 1), ('b', 2), ('b', 3), ('c', 0), ('c', 1), ('c', 2), ('c', 3), ('d', 0), ('d', 1), ('d', 2), ('d', 3)]
1
4
9
16
25
36
49
```

## NamedTupels
So one of the properties of tuples is that they are immutable. So sometimes we need to use that property to define some constants which are combination of couple of values.
Example:-
```
color = (55, 111, 123)
```
But this is not informative. Here I want to convey that my color comprises of  RGB values but someone can read it as sharpness, hue etc. So you might think we can use `Dictionary` for this but then we will loose our immutability part. Here comes the use of named-tuple. Example:-
```
from collections import namedtuple
Color = namedtuple('Color', ['red', 'green', 'blue'])
color = Color(55, 123, 111)
print(color.red)
print(color[0])
```

# Conditional Statements, and Loops
Some of the conditions that are allowed are:-
```
# Comparisons:
# Equal:            ==
# Not Equal:        !=
# Greater Than:     >
# Less Than:        <
# Greater or Equal: >=
# Less or Equal:    <=
# Object Identity:  is // This here is for matching their ids or if they are the same object and residing at the same address


# False Values:
    # False
    # None
    # Zero of any numeric type
    # Any empty sequence. For example, '', (), [].
    # Any empty mapping. For example, {}.

// For loops there is no specific edge cases.
```

# Functions
Functions are basically set of instructions package together to perform specific tasks.Example:-

```
month_days = [0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
def is_leap(year):
    """Return True for leap years, False for non-leap years."""
    return year % 4 == 0 and (year % 100 != 0 or year % 400 == 0)

>>> def student_info(*args, **kwargs):
...      print(args)
...      print(kwargs)
>>> student_info('a', 'b', name = 'a', age = '22', id=1)
('a', 'b')
{'name': 'a', 'age': '22', 'id': 1}
// If you try to wrap the thing into variables and then pass it, then it will create a issue like this
>>> co = ['mat', 'cat']
>>> lo = {'a': 1, 'b': 2}
>>> student_info(co, lo)
(['mat', 'cat'], {'a': 1, 'b': 2})
{}
// See here it didn't get expanded.Hence we use to send like this
>>> student_info(*co, **lo)
('mat', 'cat')
{'a': 1, 'b': 2}
```

# Error Handling
try, except, else and finally are some of the blocks that we use for handling exceptions. A quick example to understand this:-
```
try:
  file = open('testing.txt') // Trying to open this file
  raise Exception // manually raising exception
except FileNotFoundError as e:
  print(e) // will catch if the file is not there
except Exception as e:
  print(e) // Will catch any another exception apart from FileNotFoundError
else:
  file.read() // Will run if no exception is found
finally:
  file.close() // Will run no matter what. If try is successful then both the try and this command and if not then only this command
```
# `if __name__ == '__main__'`
So this is a very common conventional code that you will see in many python files here and there. So what exactly this means.
So if you simply do `print(__name__)` and run that file it will return `__main__`. So python assigns few special variables some values even before running any code. `__name__` is one such variable. It sets it to `__main__`.  So when ever you run any python file, for that specific file the `__name__` variable will always be `__main__` but if you import a module and try to access there `__name__`, `then python assigns the name of that module to that modules __name__  variable`. 
Example :- 
```
# File Name:- file1.py
print('This is the __name__ variable: {}'.format(__name__))
# Output:-
(base) ➜  Python python file1.py
This is the __name__ variable: __main__
```
```
# File Name:- file2.py
import file1
print('This is the __name__ variable: {}'.format(__name__))
# Output:-
(base) ➜  Python python file2.py
This is the __name__ variable: file1
This is the __name__ variable: __main__
```

As you can see in second code snippet that when we import file1 from file2 then for file1 `__name__` variable, the module name is assigned. And this is why we use `if __name__ == '__main__'` to differentiate if the file is being running directly or being imported. Example:-
```
def main():
    print('This is the __name__ variable: {}'.format(__name__))    
if __name__ == '__main__':
    main()

# Output:- 
(base) ➜  Python python file1.py
This is the __name__ variable: __main__
```
`And now the output for running file2.py this time is`
```
(base) ➜  Python python file2.py
This is the __name__ variable: __main__
```


## Unit-Testing
Testing your code is very important since it helps in covering the edge cases which might come while your code is in production. It's a very important skill a good developer has. Here we will be using `unittest` module.Let see some code snippets to understand this better. Here is a `calc.py` file which contains following functions.
```
def hello():
    return 'Hello'

def return_text(a):
    return a

def divide(x, y):
    if y == 0:
        raise ValueError('Can not divide by zero!')
    return x / y
```
`By convention we will create another file called test_calc.py and the code for that is this`.
```
import unittest
import calc

class TestCalc(unittest.TestCase):
    def test_hello(self):
        text = calc.hello()
        self.assertEqual(text, 'Hello')
```
Now if you try to run this file directly it will not run the test-cases. To run the test case you have to run it like this `python -m unittest test_calc.py` and it will give the following output.
```
(base) ➜  Python python -m unittest test_calc.py
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

But as studied in previous topic we can modify the calling of function when you call a specific file inside our `if __name__=='__main__'` statement. So now when you modify you test_calc.py file and run it directly it will run successfully like this:-
```
import unittest
import calc

class TestCalc(unittest.TestCase):
    def test_hello(self):
        text = calc.hello()
        self.assertEqual(text, 'Hello')

if __name__=='__main__':
    unittest.main()        
```
### Some quick pointers
- Do remember to define your function starting with test(here:- test_hello) or else the unittest module will not recognise it as a function that needs testing.
- If you want a piece of code or some variable initialisation to take place before every test-case you can use `setUp` function and to delete or free some memory or if you want to perform something after a test-case ends then in that case use `tearDown` function. But remember these two will always run before every test-case.
- Now if you want to perform some initial setups only once and wanted to run some process at the end when all the test cases successfully ran. You can do the same with classmethods called `setUpClass` and `tearDownClass`.

#### This brings us to the end of `Part 1` of this blog. Stay tuned for `Part 2` and `Part 3`. Incase of any typo or any wrong information do comment out and I will get it correct. I am planning to do such series on SQL, Elixir, Phoenix, ElasticSearch and etc. I am not well versed in frontend tech but I am quite good at backend. If you have any suggestions or want me to explore something new which is recently launched in the market, I am all ears. Do like, comment and share, it will motivate me to bring such thing more frequently. And lastly, the above content is completely inspired by the hard-work done by [Corey Schafer ](https://www.youtube.com/c/Coreyms).


#### Thanks ,
#### Regards
### Ayoush Chourasia






















