---
title: "Unlocking Elixir's Power: Mastering Variables, Pattern Matching, and Immutability - Part 2 of Our Elixir Series"
datePublished: Sat Oct 28 2023 10:09:34 GMT+0000 (Coordinated Universal Time)
cuid: clo9vrm8b000808lb8kosaoze
slug: unlocking-elixirs-power-mastering-variables-pattern-matching-and-immutability-part-2-of-our-elixir-series
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/rv3scW1xpaI/upload/8c6cb4e8d350a1a3b8135b8f045deb7e.jpeg
tags: interview, software-development, elixir, software-engineering

---

In the world of programming, Elixir stands out as a language that excels in functional programming paradigms. This blog is the second installment of our Elixir series, where we will explore three crucial aspects of Elixir - Working with Variables, Pattern Matching, and Immutability. Elixir's unique approach to these concepts offers clean, maintainable, and robust code. Let's dive right in and understand how Elixir conquers these essential topics.

## **Working with Variables**

### **Elixir Basics**

Elixir's syntax may initially seem familiar, but it holds some distinctive qualities that set it apart. The concept of variables in Elixir is where the journey begins.

In Elixir, a variable is nothing like a mutable storage container in other languages. Instead, it's like an assertion. It succeeds if Elixir can find a way of making the left-hand side equal the right-hand side. Elixir uses the `=` symbol, which it refers to as the match operator, to perform this operation. For example:

```elixir
a = 1
1 = a
2 = a
# (MatchError) no match of right-hand side value: 1
```

Elixir will only change the value of a variable on the left side of an equals sign, whereas on the right, a variable is replaced with its value. Elixir looks for a way to make the value on the left side the same as the value on the right side.

### **Some Types You'll Find in Elixir**

Elixir supports various data types, including integers, floats, booleans, atoms, tuples, and more. Understanding these data types is fundamental to working with Elixir variables. For example:

```elixir
number = 42
is_active = true
name = :john
details = {name, number, is_active}
```

Here, `number` is an integer, `is_active` is a boolean, `name` is an atom, and `details` is a tuple.

### **Operators with Examples**

Elixir uses a set of operators to manipulate data, just like other languages. Here are a few operators with examples:

* **Arithmetic Operators:**
    

```elixir
x = 10
y = 5
sum = x + y
difference = x - y
product = x * y
quotient = x / y
```

* **Comparison Operators:**
    

```elixir
age = 30
is_adult = age >= 18
is_teenager = age > 12 && age < 18
```

* **String Concatenation:**
    

```elixir
first_name = "John"
last_name = "Doe"
full_name = first_name <> " " <> last_name
```

### **Creating Logical Expressions**

Elixir allows you to create logical expressions using logical operators, which include `and`, `or`, and `not`. These operators are used to combine or negate conditions. Here's an example:

```elixir
is_student = true
has_homework = false
is_ready_for_exam = is_student and not has_homework
```

## **Pattern Matching**

Elixir's pattern matching is a powerful tool that shapes everything you program. It's useful for assigning variables, unpacking values, and making decisions such as which function to invoke.

### **Pattern Matching In-Depth Understanding**

Pattern matching in Elixir goes far beyond simple variable assignment. It allows you to destructure data, create complex conditions, and guide the flow of your program. Here are some in-depth examples:

```elixir
{status, message} = {:ok, "Success"}
[head | tail] = [1, 2, 3, 4, 5]
{a, b, a} = {1, 2, 1} # Error: a and b have conflicting values
```

### **Ignoring a Value with \_**

You can use an underscore (`_`) to ignore a value during pattern matching. This is handy when you want to focus on specific parts of a data structure:

```elixir
{result, _} = {:ok, "Data"}
```

### **Variables Bind Once (per Match)**

In Elixir, once a variable is bound to a value during pattern matching, it retains that value for the rest of the match:

```elixir
{a, a} = {1, 1}
# a is 1
{b, b} = {1, 2}
# Error: b cannot have conflicting values
```

### **The Pin Operator (^)**

If you want to force Elixir to use an existing value in the pattern, you can prefix the variable with a caret (^). It tells Elixir to keep the value as is:

```elixir
value = 42
^value = 42
# Successfully matches, value remains 42
```

Elixir's pattern matching empowers you to create structured, robust code that's easy to understand and maintain.

## **Immutability**

### **Coding with Immutable Data**

Immutability is a core principle in Elixir, and it plays a significant role in shaping the language's characteristics. In Elixir, any function that transforms data returns a new copy of it. You never modify data directly. Instead, you create new instances with the desired changes. For example:

```elixir
name = "elixir"
cap_name = String.capitalize(name)
# name remains "elixir"
# cap_name is "Elixir"
```

### **Immutable Data Is Known Data**

Elixir's immutable nature ensures that all values, whether simple or complex, are treated the same way. This uniformity simplifies your code and makes it easier to reason about. Whether you're dealing with integers or intricate data structures, you can rely on their immutability.

### **Performance Implications of Immutability**

Elixir handles immutability efficiently, ensuring your code remains performant. It does this through techniques like sharing existing data when constructing new structures. For instance:

```elixir
list1 = [3, 2, 1]
list2 = [4 | list1]
# list2 shares data with list1
```

Elixir's garbage collection process is also optimized, thanks to the isolation of data in separate processes.

### **Garbage Collection**

The other performance issue with transformational language is that you quite often end up leaving old values unused when you create new values from them. This leaves a bunch of things using up memory on the heap, so garbage collection has to reclaim them.

Most modern languages have a garbage collector, and developers have grown to be suspicious of them—they can impact performance quite badly.

But the cool thing about Elixir is that you write your code using lots and lots of processes, and each process has its own heap. The data in your application is divvied up between these processes, so each individual heap is much, much smaller than would have been the case if all the data had been in a single heap. As a result, garbage collection runs faster. If a process terminates before its heap becomes full, all its data is discarded—no garbage collection is required.

## **Conclusion**

Working with variables, pattern matching, and immutability are fundamental aspects of Elixir programming. Embracing Elixir's approach to these concepts can lead to cleaner, more maintainable, and scalable code. In this blog, we've explored the core principles and practices of each topic. These foundations are essential for your journey through Elixir's unique and powerful features.

Elixir's distinctive approach to variables, pattern matching, and immutability ensures a new way of thinking and coding. By following these principles, you'll be well-prepared to explore Elixir's concurrent and distributed capabilities in the next parts of our Elixir series.

Stay tuned for more insights into the world of Elixir, where we'll continue to unlock its potential in programming and problem-solving.

Don't hesitate to reach out if you have any questions or need further clarification on any of the topics discussed in this blog. Happy coding with Elixir!

*Remember to bookmark this page for future reference.*