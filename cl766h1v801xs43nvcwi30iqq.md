## Python Quick Interview Revision Notes - Part 2

Hello everyone, welcome back to this 3 part series. [Part 1](https://thinkersclub.xyz/python-quick-interview-revision-notes-part-1) was lengthy but I swear this won't. There are a few specific topics that we will be targeting in this blog such as `generators`, `decorators`, `logging`. But out of all those topics, 3 topics that are very important are `context managers`, `threading` and `multiprocessing`. 

So without further a due, let's dive in. First, let's look into one topic which might have been skipped in Part 1 that is:-

## What is the difference between str() and repr() ?

Okay so the major difference between these two are the goals they serve. `repr` goal is to be unambiguous but the goal of `str` is to be readable.  Let's take a look at a simple example to check this:-

```
import datetime
a = datetime.date(2022, 8, 22)
b = '2022-08-22'
print(str(a))
print(str(b))
print(repr(a))
print(repr(b))

Output:-
2022-08-22
2022-08-22
datetime.date(2022, 8, 22)
'2022-08-22'
```

So if you see this both the output of str representation of a and b are giving the same result but the repr representation is giving you the unambiguous result which you according to the documentation you can directly pass to `eval()` function, so what does that mean. Simply it means you can copy and run this code directly on the shell or inside your script.

## Decorators

So from this section, some advanced Python concepts will kick in. Before discussing `decorators`, let me first discuss `closures`.

### Closures 
So to understand Closures we first look into `first class functions`
#### First-Class Functions
First-class functions are basically the functions that are treated the same as that of any common variable or object. It can be assigned or passed to other functions or returned from another function. Let's take a simple example to clear things out.
```
def square(x):
    return x*x

f = square
print(f(5))

Output:-
25
```

> As you can see here we assigned a function to another variable and then we used that variable as a reference to that function.

Let's see an example were we are passing a function to another function`(The function which takes or returns another function are called high order functions.)`:-
```
def square(x):
    return x*x

def my_map(func, arg_list):
    result = []
    for i in arg_list:
        result.append(func(i))
    return result

squares = my_map(square, [1, 2, 3, 4, 5])

print(squares)

def cube(x):
    return x*x*x

cubes = my_map(cube, [1, 2, 3, 4, 5])

print(cubes)

Output:-
[1, 4, 9, 16, 25]
[1, 8, 27, 64, 125]
```

> Here we passed a function to `my_map` function and return the results accordingly

Let's see an example where a function is being returned:-
```
def html_tab(tag):
    def wrapped_markup(msg):
        print('<{0}>{1}<{0}>'.format(tag, msg))
    
    return wrapped_markup

print_h1 = html_tab('h1')
print_h1("H1 tag")

Output:-
<h1>H1 tag<h1>
```

> Here a function is being returned which is being assigned and then called up by the same variable.

Now that we understand what `first class functions` are, let's understand `closures`.

> To put it simply a `closure` are these inner functions that are enclosed within the outer function. Closures can access variables present in the outer function scope. It can access these variables even after the outer function has completed its execution. 

Let's see an example for the above statement:-
```
def outer_function():
    message = 'Hi'
    def inner_function():
        print(message)
    return inner_function

my_function = outer_function()
my_function()
my_function()
my_function()

Output:-
Hi
Hi
Hi
```

> As you can see here, even after the outer_function is finished with its execution in line `my_function = outer_function()`, when we try to access a free variable `message`, it remembers the value through closures.

Lets see one last example of closure before we move on to `decorators`:-
```
import logging

logging.basicConfig(filename='example.log', level=logging.INFO)
def my_logger(func):
    def log_func(*args):
        logging.info('Running the {} with arguments'.format(func.__name__, args))
        print(func(*args))
    return log_func    

def add(x, y):
    return x+y

def subtract(x, y):
    return x-y

add_log = my_logger(add)
sub_log = my_logger(subtract)
add_log(3, 5)
add_log(4, 2)
sub_log(10, 5)
sub_log(5, 20)

Output:-
8
6
5
-15

# Output of example.log file:-
INFO:root:Running the add with arguments
INFO:root:Running the add with arguments
INFO:root:Running the subtract with arguments
INFO:root:Running the subtract with arguments
```

So what are `decorators`?
> Decorators are the functions that take another function as an argument, add some functionality, and return the function without altering the source code of originally passed functions.

Let's see a simple example to understand

```
def decorator_functions(original_function):
    def wrapped_function():
        return original_function()
    return wrapped_function

def display():
    print('Display Function Ran')
decorated_variable = decorator_functions(display)
decorated_variable()

Output:-
Display Function Ran
```

As you can see we passed the `display` function to our `dectorator_function` which calls this function inside `wrapped_function` and return it.

So why do we need decorator functions?
Decorator functions give us the ability to modify the functionality of the passed function inside `wrapped_function` without modifying the original function.

So most of the time we follow different syntax while passing a function in our decorator but that syntax is doing pretty much the same thing as we did in the above example.
```
def decorator_functions(original_function):
    def wrapped_function():
        return original_function()
    return wrapped_function

@decorator_functions
def display():
    print('Display Function Ran')

# The above code simply converts to this 
display = decorator_functions(display)

```

Now if you want the above decorator function to be accommodating any number of arguments then you can pass `(*args, **kwargs)`  in your wrapper function.

```
def decorator_functions(original_function):
    def wrapped_function(*args, **kwargs):
        return original_function(*args, **kwargs)
    return wrapped_function

@decorator_functions
def display():
    print('Display Function Ran')

@decorator_functions
def display_info(age, name):
    print('display_info Function Ran {} {}'.format(age, name))

display()
display_info(23, 'Ayoush')

Output:-
Display Function Ran
display_info Function Ran 23 Ayoush
```

Now let's see an example related to decorator classes.
```
class decorator_class():
    def __init__(self, original_function):
        self.original_function = original_function

    def __call__(self, *args, **kwds):
        print('call method inside decorator class is calling {}'.format(self.original_function.__name__))
        return self.original_function(*args, **kwds)

@decorator_class
def display():
    print('Display Function Ran')

@decorator_class
def display_info(age, name):
    print('display_info Function Ran {} {}'.format(age, name))

display()
display_info(23, 'Ayoush')

Output :-
call method inside decorator class is calling display
Display Function Ran
call method inside decorator class is calling display_info
display_info Function Ran 23 Ayoush
```

> Here is another practical example of how you can use a Decorator and some points to remember.

```
def my_logger(orig_func):
    import logging
    logging.basicConfig(filename='{}.log'.format(orig_func.__name__), level=logging.INFO)

    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        logging.info(
            'Ran with args: {}, and kwargs: {}'.format(args, kwargs))
        return orig_func(*args, **kwargs)

    return wrapper


def my_timer(orig_func):
    import time
    @wraps(orig_func)
    def wrapper(*args, **kwargs):
        t1 = time.time()
        result = orig_func(*args, **kwargs)
        t2 = time.time() - t1
        print('{} ran in: {} sec'.format(orig_func.__name__, t2))
        return result

    return wrapper

@my_logger
@my_timer
def display_info(age, name):
    print('display_info Function Ran {} {}'.format(age, name))

# The above code means:-

>>> display_info = my_logger(my_timer(display_info))

# If you try to find the name of the function being returned by this 

>>> my_timer(display_info).__name__
wrapper

# Hence we don't get any display_info.log file which according to my_logger we should. Instead we get wrapper.log file

# To solve this we have to decorate our wrapper functions with wraps
from functools import wraps

```

Some points to remember:-
- Here the sequence in which the decorators are being used is very important.
- Here if you observe closely an actual function that is being passed to `my_logger` is a `wrapper` function that is being returned from `my_timer`. So to maintain the originality of the function we can use wraps from `functools`.


## Generators

Okay so understand `generators` we will start with a simple example:-
```
def square_number(nums):
    result = []
    for i in nums:
        result.append(i*i)
    return result
nums = square_number([1, 2, 3, 4, 5])
print(nums)
# Output:-
[1, 4, 9, 16, 25]
```
Pretty straightforward script right? Now if I have to change the `square_number` function to the generator. I will do the following changes
```
def square_number(nums):
    for i in nums:
        yield(i*i)

nums = square_number([1, 2, 3, 4, 5])
print(nums)

# Output:-
<generator object square_number at 0x7f95d8112f90>
```
Now if you observe the output, you will see an object why is that? 
> The reason for that is that `generators` don't hold the entire result in the memory. It just yields one result at a time. It waits for the call of the next result and then computes and returns it.

> So initial yield just holds the object reference

> If you call next it will start giving you the result

```
print(next(nums))
print(next(nums))
print(next(nums))
print(next(nums))
print(next(nums))

#Output:-
1
4
9
16
25
```

> If you try to yield more than the actual loop length than it will throw an error.
> A more safer way to use it by using for iteration to access value.

Now you may ask that the same thing can be achieved using `List Comprehensions`. Absolutely, in-fact if you want to convert your list comprehension into generator its more easier than anything.

```
# List Comprehension
nums = [x*x for x in [1, ,2 ,3, 4]]

#Generator
nums = (x*x for x in [1, ,2 ,3, 4])

# Just replace square brackets
```

### Now whats the use of `Generators`.
Let's take an example to verify that:-
```
import mem_profile
import random
import time

names = ['John', 'Corey', 'Adam', 'Steve', 'Rick', 'Thomas']
majors = ['Math', 'Engineering', 'CompSci', 'Arts', 'Business']

print('Memory (Before): {}Mb'.format(mem_profile.memory_usage_psutil()))

def people_list(num_people):
    result = []
    for i in range(num_people):
        person = {
                    'id': i,
                    'name': random.choice(names),
                    'major': random.choice(majors)
                }
        result.append(person)
    return result

def people_generator(num_people):
    for i in range(num_people):
        person = {
                    'id': i,
                    'name': random.choice(names),
                    'major': random.choice(majors)
                }
        yield person

t1 = time.perf_counter()
people = people_list(1000000)
t2 = time.perf_counter()

# t1 = time.perf_counter()
# people = people_generator(1000000)
# t2 = time.perf_counter()

print('Memory (After) : {}Mb'.format(mem_profile.memory_usage_psutil()))
print('Took {} Seconds'.format(t2-t1))

# Output:-
Memory (Before): 33.94921875Mb
Memory (After) : 219.19140625Mb
Took 0.888026875 Seconds
```
Now if uncomment the generator call see, here is the output I get:-
```
Memory (Before): 33.8828125Mb
Memory (After) : 33.91015625Mb
Took 5.409999999927972e-07 Seconds
```
> Clearly you can see, there is a significant improvement in memory usage and time take.
 
**IMPORTANT**
If you try to convert the generator result into list like this `list(people_generator(1000000))`. You will loose all those improvements and it will work as a normal calling which will take same amount of memory and time



 


















 

