---
title: "Exploring Elixir’s Advanced Features: Part 5 of the Elixir Series"
datePublished: Sat Nov 04 2023 15:40:41 GMT+0000 (Coordinated Universal Time)
cuid: clok7oevd000f09l21b4ub592
slug: exploring-elixirs-advanced-features-part-5-of-the-elixir-series
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/tArR7ys2F3Q/upload/b8519b7a1b2f05f413a44ea9b434ca02.jpeg
tags: phoenix, erlang, elixir, functional-programming, programming-languages

---

Welcome to the fifth part of our Elixir series, where we dive deeper into the advanced features and concepts that make Elixir a powerful and expressive language. In this part, we’ll explore modules, named functions, guard clauses, default parameters, private functions, the pipe operator, module creation and usage, attributes, module names, and more.

# **Structuring Code with Modules and Named Functions**

Elixir encourages structured code organization by breaking it into named functions grouped within modules. In Elixir, named functions must reside inside modules. Function names are identified by their arity, indicating the number of parameters they accept. For example, a function named double/1 accepts one parameter. If we had another version of double that took three parameters, it would be known as double/3. These functions are entirely separate in Elixir’s eyes.

```elixir
defmodule Times do
  def double(n) do
    n * 2
  end
end
```

# **Module Compilation**

## **1\. Compilation with** `.ex` Files

`.ex` files are used for production code. These files contain compiled bytecode and are typically part of your project's source code.

Here’s how you can compile a module from an `.ex` file:

```elixir
$ elixirc my_module.ex
```

This command compiles the module and creates a corresponding `.beam` file. You can then use this compiled module in your Elixir project.

## **2\. Scripting and Interactive Development with** `.exs` Files

`.exs` files, on the other hand, are intended for scripting, testing, and interactive development. These files do not produce compiled bytecode and are useful for quick experimentation and scripting tasks.

Here’s how you can run an `.exs` script:

```elixir
$ elixir my_script.exs
```

When using `.exs` files, there's no need for explicit compilation. Elixir interprets the code directly from the script.

Remember that if you want to use a module as part of your production application, it’s best to use `.ex` files. However, for quick scripts and interactive development, `.exs` files are more convenient.

These two file types provide flexibility in how you work with Elixir, allowing you to choose the best approach for your specific use case.

# **The Function’s Body Is a Block**

Elixir uses a `do...end` block to group expressions and pass them to other code. This construct is used in module and named function definitions, control structures, and anywhere code needs to be treated as an entity. The actual syntax for a function's body is as follows:

```elixir
def double(n), do: n * 2
```

You can pass multiple lines to `do:` by grouping them with parentheses.

# **Multiple Clauses in Named Functions**

Elixir allows named functions to have multiple clauses, each with specific patterns. When you call a named function, Elixir attempts to match your arguments with the parameter list of the first definition (clause). If there is no match, it tries the next definition of the same function, provided it has the same arity, continuing until it runs out of candidates.

Here’s an example with the factorial function:

```elixir
defmodule Factorial do
  def of(0), do: 1
  def of(n), do: n * of(n-1)
end
```

In this case, there are two definitions of the same function, and Elixir selects the appropriate one based on the provided argument.

One important point to note is that the order of function clauses can make a difference. Elixir tries functions from the top down, executing the first match.

```elixir
defmodule BadFactorial do
  def of(n), do: n * of(n-1)
  def of(0), do: 1
end
```

In this example, the order of the function clauses in the `BadFactorial` module matters. Elixir will try to match the clauses from top to bottom, executing the first one that matches. In this case, the first clause (`def of(n), do: n * of(n-1)`) will always match because it doesn't have any guard clause, resulting in an infinite loop when trying to calculate the factorial. The second clause (`def of(0), do: 1`) will never be reached.

This demonstrates how the order of function clauses can impact the behavior of your code in Elixir.

# **Guard Clauses**

Guard clauses are predicates attached to function definitions using the `when` keyword. They provide additional conditions for pattern matching. Here's an example:

```elixir
defmodule Guard do
  def what_is(x) when is_number(x) do
    IO.puts "#{x} is a number"
  end
  def what_is(x) when is_list(x) do
    IO.puts "#{inspect(x)} is a list"
  end
end
```

Guard clauses allow you to specify additional conditions for a function’s clauses, enabling more fine-grained pattern matching.

# **Default Parameters**

Elixir allows you to provide default values for function parameters. You use the `param \\ value` syntax to specify defaults. If a parameter isn't provided when calling the function, it defaults to the specified value. However, when defining multiple heads of a function with default parameters, there's a specific syntax:

```elixir
defmodule DefaultParams1 do
  def func(p1, p2 \\ 123) do
    IO.inspect [p1, p2]
  end
  def func(p1, 99) do
    IO.puts "you said 99"
  end
end
```

If you compile this module, you may encounter a warning:

```elixir
warning: definitions with multiple clauses and default values require a function head. Instead of this:
    def func(:first_clause, b \\ :default) do ... end
    def func(:second_clause, b) do ... end
one should write this:
    def func(a, b \\ :default)
    def func(:first_clause, b) do ... end
    def func(:second_clause, b) do ... end
```

The intent is to reduce confusion that can arise with defaults. Adding a function head with no body that contains the default parameters ensures the defaults apply to all calls to the function.

Example:

```elixir
defmodule Params do
  def func(p1, p2 \\ 123)
  def func(p1, p2) when is_list(p1) do
    "You said #{p2} with a list"
  end
  def func(p1, p2) do
    "You passed in #{p1} and #{p2}"
  end
end
```

# **Private Functions**

Elixir allows you to define private functions using the `defp` macro. Private functions are only accessible within the module that declares them, providing encapsulation and hiding internal implementation details. You can define private functions with multiple heads just like public functions. However, you cannot have some heads as private and others as public.

Example:

```elixir
defmodule MyModule do
  def my_function() do
    some_public_function()
    my_private_function()
  end
  defp my_private_function() do
    # Private logic
  end
  def some_public_function() do
    # Public logic
  end
end
```

Private functions are essential for maintaining code organization and protecting internal details from external code.

# **The Amazing Pipe Operator: |&gt;**

Elixir’s pipe operator, `|>`, simplifies code composition. It allows you to chain function calls, making your code more readable and expressive. Consider the following example:

```elixir
filing = DB.find_customers
         |> Orders.for_customers
         |> sales_tax(2018)
         |> prepare_filing
```

The pipe operator passes the result of each expression to the next function, enhancing code clarity and reducing nesting.

# **Module Nesting**

In Elixir, module nesting is a way to organize code logically, but it’s an organizational feature rather than a strict hierarchy. When you define a module inside another, Elixir simply prepends the outer module name to the inner module name, separating them with a dot. This approach allows you to create nested modules directly.

```elixir
defmodule Mix.Tasks.Doctest do
  def run do
    # Implementation
  end
end
```

Module nesting provides a convenient way to structure your code, but it’s important to note that there’s no inherent relationship between the outer and inner modules.

# **Importing Modules**

The `import` directive in Elixir allows you to bring a module's functions and macros into the current scope. This feature reduces clutter in your source files and eliminates the need to repeat the module name. Here's an example of how to use it:

```elixir
defmodule Example do
  def func1 do
    List.flatten([1, [2, 3], 4])
  end
  def func2 do
    import List, only: [flatten: 1]
    flatten([5, [6, 7], 8])
  end
end
```

By importing the `List` module, you can call its functions without specifying the module name repeatedly.

# **The Alias Directive**

Elixir’s `alias` directive creates an alias for a module, which is particularly useful for reducing typing effort. You can create aliases for modules to make your code more concise and readable.

```elixir
defmodule Example do
  def compile_and_go(source) do
    alias My.Other.Module.Parser, as: Parser
    alias My.Other.Module.Runner, as: Runner
    source
    |> Parser.parse()
    |> Runner.execute()
  end
end
```

Aliases enhance code readability and minimize the need for lengthy module references.

# **The Require Directive**

In Elixir, you use the `require` directive to include modules that define macros. This ensures that macro definitions are available during code compilation, enabling the use of macros in your code. The `require` directive is particularly relevant when working with macros.

# **Module Attributes**

Elixir modules can have attributes, which are metadata associated with the module and identified by a name. These attributes are accessed using the `@` symbol within a module. Attributes are often used for configuration and metadata purposes.

Example:

```elixir
defmodule Example do
  @author "Dave Thomas"
  def get_author do
    @author
  end
end
```

Attributes can be set multiple times within a module, and the value you see in a named function is based on the attribute’s definition at the time the function is defined.

Here’s an example demonstrating that attributes can be set multiple times within a module, and the value you see in a named function is based on the attribute’s definition at the time the function is defined:

```elixir
defmodule Example do
  @attr "one"
  
  def first, do: @attr
  
  @attr "two"
  def second, do: @attr
end
IO.puts "#{Example.second} #{Example.first}"
```

In this example, we define the `@attr` attribute twice within the `Example` module, first with the value "one" and later with the value "two." The two named functions, `first` and `second`, each access the `@attr` attribute. When we print the values of `Example.second` and `Example.first`, you'll see that the attribute's value is based on the definition at the time the function is defined. In this case, it will output "two one."

You now have a comprehensive guide to the advanced features of Elixir, including module compilation differences, function clauses, default parameters, private functions, module attributes, and more. These features are essential for writing efficient, well-structured, and expressive code in Elixir.