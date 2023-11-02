---
title: "Demystifying Elixir Functions: A Comprehensive Guide — Part 4 -Subpart 2/3 of Our Elixir Series"
datePublished: Thu Nov 02 2023 11:56:07 GMT+0000 (Coordinated Universal Time)
cuid: cloh4rwtu000f09kze9n48o4r
slug: demystifying-elixir-functions-a-comprehensive-guide-part-4-subpart-23-of-our-elixir-series
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Pv5WeEyxMWU/upload/d52743c121d1919d87221f761ea896f5.jpeg
tags: phoenix, software-development, software-architecture, elixir, software-engineering

---

Continuing the series and subpart of part 4, we will look into some other functionality of functions.

### **6\. Parameterized Functions**

In Elixir, parameterized functions allow you to create flexible and reusable functions that take arguments. They are a fundamental part of functional programming. Here are a few coding examples to illustrate the concept:

**Example 1: Basic Parameterized Function**

```elixir
add_n = fn n -> fn other -> n + other end end
add_two = add_n.(2)
result = add_two.(3) # Returns 5
```

In this simple example, we define a parameterized function `add_n` that takes a value `n` and returns another function. We then create a specific function `add_two` by invoking `add_n` with `n` set to 2. Finally, we use `add_two` to add 3 to 2.

**Example 2: Complex Parameterized Function**

```elixir
divide_by = fn divisor ->
  fn dividend when dividend != 0 -> divisor / dividend
  dividend -> {:error, "Division by zero"}
end
end
```

```elixir
divide = divide_by.(10)
result1 = divide.(2) # Returns 5.0
result2 = divide.(0) # Returns {:error, "Division by zero"}
```

In this example, we create a more complex parameterised function, `divide_by`, which handles division while preventing division by zero. It returns either the result of division or an error tuple.

**Example 3: Advanced Parameterised Function**

```elixir
factorial = fn
  (0) -> 1
  (n) when n > 0 -> n * factorial.(n - 1)
  (n) when n < 0 -> {:error, "Factorial undefined for negative numbers"}
end
```

```elixir
result1 = factorial.(5) # Returns 120
result2 = factorial.(-2) # Returns {:error, "Factorial undefined for negative numbers"}
```

In this advanced example, we define a parameterized function `factorial` that calculates the factorial of a number. It includes pattern matching to handle various cases, even preventing factorial calculation for negative numbers.

These examples demonstrate the flexibility and power of parameterized functions in Elixir, from simple use cases to handling complex scenarios and errors.

### **7\. Passing Functions as Arguments**

**Example 1: Applying a Simple Operation**

```elixir
add_one = fn n -> n + 1 end
times_two = fn n -> n * 2 end
apply_operation = fn operation, a, b -> operation.(a, b) end
```

```elixir
result1 = apply_operation.(add_one, 5, 2) # Returns 7
result2 = apply_operation.(times_two, 4, 3) # Returns 24
```

In this example, we define two functions, `add_one` and `times_two`, each performing a specific mathematical operation. Then, we create an `apply_operation` function that takes an operation function and two values, applying the operation to those values. This demonstrates the ability to pass functions as arguments for various operations.

**Example 2: Dynamic Function Selection**

```elixir
calculate = fn operation, a, b -> operation.(a, b) end
```

```elixir
add = fn (a, b) -> a + b end
subtract = fn (a, b) -> a - b end
```

```elixir
result1 = calculate.(add, 10, 4) # Returns 14
result2 = calculate.(subtract, 8, 3) # Returns 5
```

In this example, the `calculate` function takes an operation function as an argument and applies it to two values. We define two operation functions, `add` and `subtract`, and use the `calculate` function to switch between these functions dynamically.

**Example 3: Custom Operations**

```elixir
custom_operation = fn n, operation -> operation.(n) end
square = fn n -> n * n end
cube = fn n -> n * n * n end
```

```elixir
result1 = custom_operation.(4, square) # Returns 16
result2 = custom_operation.(3, cube) # Returns 27
```

In this example, the `custom_operation` function takes a number `n` and an operation function. We define operation functions like `square` and `cube` to apply custom operations to the provided number `n`. This demonstrates the flexibility of passing functions to create custom operations.

**Example 4: Functional Composition**

```elixir
double = fn n -> n * 2 end
increment = fn n -> n + 1 end
composed_function = fn x -> double.(increment.(x)) end
```

```elixir
result1 = composed_function.(3) # Returns 8
result2 = composed_function.(7) # Returns 16
```

In this example, we compose functions `double` and `increment` into a new function `composed_function`. The composed function applies the `increment` function first and then doubles the result. This showcases the power of passing functions for functional composition.

### 8\. Pinned Values and Function Parameters

**Example 1: Customized Greetings**

```elixir
defmodule Greeter do
  def for(name, greeting) do
    fn (name_to_greet) when name == name_to_greet -> "#{greeting} #{name}"
       (_) -> "I don't know you"
    end
  end
end

greet_mr_valim = Greeter.for("José", "Oi!")
greet_dave = Greeter.for("Dave", "Hello")
result1 = greet_mr_valim.("José") # Returns "Oi! José"
result2 = greet_mr_valim.("Maria") # Returns "I don't know you"
result3 = greet_dave.("Dave") # Returns "Hello Dave"
result4 = greet_dave.("John") # Returns "I don't know you"
```

In this example, we define the `Greeter` module with a function `for` that accepts a name and a greeting message. We use a pinned value to customize greetings for specific names. The function matches the input name with the pinned value and generates a greeting accordingly.

**Example 2: Handling Different Data Types**

```elixir
defmodule TypeHandler do
  def for(:int, action) do
    fn (value) when is_integer(value) -> action.(value)
       (_) -> "Invalid data type"
    end
  end
end

int_handler = TypeHandler.for(:int, fn n -> "Received an integer: #{n}" end)
string_handler = TypeHandler.for(:string, fn s -> "Received a string: #{s}" end)
result1 = int_handler.(42) # Returns "Received an integer: 42"
result2 = int_handler.("text") # Returns "Invalid data type"
result3 = string_handler.("Elixir") # Returns "Received a string: Elixir"
result4 = string_handler.(42) # Returns "Invalid data type"
```

In this example, we create a `TypeHandler` module to handle different data types using pinned values. The `for` function can customize behavior for specific data types, ensuring that the right action is taken for each input.

**Example 3: Restricted Access**

```elixir
defmodule AccessControl do
  def for(:admin, action) do
    fn (user_type) when user_type == :admin -> action.()
       (_) -> "Access denied"
    end
  end
end

admin_action = AccessControl.for(:admin, fn -> "Admin access granted" end)
guest_action = AccessControl.for(:guest, fn -> "Guest access granted" end)
result1 = admin_action.(:admin) # Returns "Admin access granted"
result2 = admin_action.(:user) # Returns "Access denied"
result3 = guest_action.(:guest) # Returns "Guest access granted"
result4 = guest_action.(:admin) # Returns "Access denied"
```

In this example, the `AccessControl` module allows customized access control based on user types. We use pinned values to handle access rights, ensuring that the appropriate access is granted or denied.

These examples demonstrate how pinned values in function parameters enable the creation of customized functions with different behaviors based on input patterns.

### 9\. The & Notation

**Example 1: Simple Arithmetic**

```elixir
add_one = &(&1 + 1)
result1 = add_one.(44) # Returns 45
square = &(&1 * &1)
result2 = square.(8) # Returns 64
```

In this example, we use the `&` operator to create two concise functions. `add_one` takes a number and returns the result of adding 1, while `square` squares the input number. These compact functions make common arithmetic operations more concise.

**Example 2: List Transformation**

```elixir
double_list = &Enum.map(&1, fn x -> x * 2 end)
list = [1, 2, 3, 4]
result3 = double_list.(list) # Returns [2, 4, 6, 8]
capitalize_words = &String.capitalize/1
words = ["elixir", "programming"]
result4 = Enum.map(words, capitalize_words.(&1)) # Returns ["Elixir", "Programming"]
```

In this example, we demonstrate the use of `&` notation for more complex functions. `double_list` doubles each element in a list, and `capitalize_words` capitalizes a list of words. The concise notation simplifies list transformations and string operations.

**Example 3: Custom Function Composition**

```elixir
add_three = &(&1 + 3)
multiply_by_five = &(&1 * 5)
compose = &(&1 |> add_three.() |> multiply_by_five.())
result5 = compose.(7) # Returns 50
```

Here, we illustrate how the `&` operator can be used to compose custom functions. The `compose` function combines the `add_three` and `multiply_by_five` functions to create a custom composition. It applies multiple operations in a single function call.

These examples showcase the versatility of the `&` notation for creating concise and custom functions in Elixir.

### 10\. Higher-Order Functions

**Example 1: Processing a List**

```elixir
enchanted_items = [
  %{title: "Edwin's Longsword", price: 150},
  %{title: "Healing Potion", price: 60},
  %{title: "Edwin's Rope", price: 30},
  %{title: "Dragon's Spear", price: 100}
]
defmodule MyList do
  def each([], _function), do: nil
  def each([head | tail], function) do
    function.(head)
    each(tail, function)
  end
end
MyList.each(enchanted_items, fn item ->
  IO.puts(item.title)
end)
```

In this example, we have a list of enchanted items, and we define a custom module `MyList`. The `each/2` function takes a list and a function as arguments. It processes each item in the list by invoking the provided function. In this case, we print the title of each enchanted item. This demonstrates the power of higher-order functions for processing collections in Elixir.

**Example 2: Custom Transformation**

```elixir
prices = [150, 60, 30, 100]
double = fn x -> x * 2 end
triple = fn x -> x * 3 end
double_prices = Enum.map(prices, double)
triple_prices = Enum.map(prices, triple)
```

In this example, we work with a list of prices and create two higher-order functions, `double` and `triple`, which double and triple a given value, respectively. We use [`Enum.map/2`](http://Enum.map/2) to transform the list of prices using these functions. This demonstrates the flexibility of higher-order functions for custom data transformations.

**Example 3: Function Composition**

```elixir
add_five = fn x -> x + 5 end
square = fn x -> x * x end
transform = fn f1, f2 -> fn x -> f2.(f1.(x)) end end
add_five_and_square = transform.(add_five, square)
result = add_five_and_square.(3) # Returns 64
```

In this example, we explore function composition using higher-order functions. We define two functions, `add_five` and `square`, and create a `transform` function that takes two functions and returns their composition. We then compose `add_five` and `square` into a new function, `add_five_and_square`, which applies both operations. This demonstrates the versatility of higher-order functions for building complex functions.

**Example 4: Filtering a List**

```elixir
numbers = [1, 2, 3, 4, 5, 6]
is_even = fn x -> rem(x, 2) == 0 end
is_odd = fn x -> rem(x, 2) != 0 end
even_numbers = Enum.filter(numbers, is_even)
odd_numbers = Enum.filter(numbers, is_odd)
```

In this example, we use higher-order functions to filter a list of numbers. We define `is_even` and `is_odd` functions to check if a number is even or odd. We then use `Enum.filter/2` to create new lists containing only even or odd numbers. This demonstrates how higher-order functions can simplify the process of filtering data.

---

That’s it for Subpart 2 of 3 subparts of part 4 of this series. Please follow for the last Subpart of this Part 4.