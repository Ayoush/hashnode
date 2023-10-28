---
title: "Elixir: Exploring Functional Concurrency - Part 1 of Our Elixir Series"
datePublished: Sat Oct 28 2023 03:37:36 GMT+0000 (Coordinated Universal Time)
cuid: clo9hrjn400040amlhrnndtjh
slug: elixir-exploring-functional-concurrency-part-1-of-our-elixir-series
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/2JIvboGLeho/upload/d94c2f89a3313845dc7d3b9430965dbb.jpeg
tags: software-development, learning, education

---

Welcome to the first installment of our Elixir blog series! In this series, we will delve deep into Elixir, a programming language renowned for its remarkable functional and concurrent programming capabilities. This introductory blog will serve as the foundation, covering the following topics in detail, with coding examples and visual aids for better understanding:

### Motivation for Elixir

Elixir was born out of a compelling need to address various challenges in modern software development. Its key motivations are:

1\. **Concurrency**: Elixir is designed to excel in handling massive concurrency. In an era of multi-core processors, it provides a solution for efficiently processing tasks concurrently.

2\. **Fault Tolerance**: Elixir is built to manage system failures gracefully, ensuring that a single fault does not lead to a catastrophic system failure.

3\. **Functional Elegance**: Elixir embraces functional programming principles, promoting immutability and pure functions, which lead to clean, maintainable code.

Let’s dive deeper into these motivations with practical examples:

Example — Concurrency:

```elixir
# Spawning lightweight processes
pid = spawn(fn -> IO.puts("Hello from process #{inspect(self())}!") end)
IO.puts("Spawned process with PID #{inspect(pid)}")
```

Example — Fault Tolerance:

```elixir
# Handling errors with supervision
defmodule MyApp.Worker do
  use Supervisor
  def start_link do
    Supervisor.start_link(__MODULE__, [], name: __MODULE__)
  end
  def init([]) do
    children = [
      worker(MyApp.Worker.Task, []),
      # Add more workers here
    ]
    supervise(children, strategy: :one_for_one)
  end
end
```

### Thinking in Functional

Functional programming is at the core of Elixir. It treats computation as the evaluation of mathematical functions and avoids mutable data and state changes. Let’s illustrate functional thinking with an example:

Example — Pure Function:

```elixir
# A function to calculate the square of a number
square = fn(x) -> x * x end
# Applying the function
result = square.(5) # This yields 25
```

In functional programming, functions are predictable, relying solely on inputs and outputs, making the code easier to reason about.

### Elixir’s Lightweight Processes and BEAM VM

Elixir’s unique power comes from its lightweight processes and the BEAM virtual machine. Elixir processes are incredibly lightweight, allowing you to spawn thousands of them without overloading system resources. These processes communicate through message passing, providing isolation.

The BEAM VM is optimized for concurrency and fault tolerance, making it the backbone of Elixir’s impressive performance. Let’s explore these concepts further:

Example — Lightweight Process:

```elixir
# Creating a process that sends and receives messages
send(self(), {:hello, "world"})
receive do
  {:hello, msg} -> IO.puts("Received: #{msg}")
end
```

### Installing and Running Elixir

To start your journey with Elixir, you’ll need to install it on your system. The installation process is straightforward and well-documented. Once installed, you can run Elixir code from the command line.

Example — Running Elixir Code:

```elixir
# Starting the Elixir interactive shell (iex)
iex
```

### iex and iex Helpers

Elixir offers an interactive shell known as `iex`, which is more than just a simple REPL. It's a powerful tool for experimenting with Elixir code.

Example — Using iex:

```elixir
# Example of using iex
iex(1)> IO.puts("Hello, Elixir!")
Hello, Elixir!
:ok
```

### Helper Keywords: ‘h’ and ‘i’

While working in `iex`, you have access to helpful keywords:

* The ‘h’ key followed by a module, function, or macro name provides detailed documentation and usage examples.
    

Example — Using ‘h’ for Help:

```elixir
iex(2)> h Enum.map

                            def map(enumerable, fun)                            

  @spec map(t(), (element() -> any())) :: list()

Returns a list where each element is the result of invoking fun on each
corresponding element of enumerable.

For maps, the function expects a key-value tuple.

## Examples

    iex> Enum.map([1, 2, 3], fn x -> x * 2 end)
    [2, 4, 6]
    
    iex> Enum.map([a: 1, b: 2], fn {k, v} -> {k, -v} end)
    [a: -1, b: -2]
```

* The ‘i’ key followed by a data structure or variable inspects and displays its contents.
    

Example — Using ‘i’ for Inspection:

```elixir
iex(3)> i [1, 2, 3]
Term
  [1, 2, 3]
Data type
  List
Reference modules
  List
Implemented protocols
  Collectable, Enumerable, IEx.Info, Inspect, List.Chars, String.Chars
```

### Customizing IEx Settings

You can customize the `iex` shell to match your preferences. Configure the prompt, add custom helper functions, and tailor it to enhance your workflow.

Example — Customizing the iex Prompt:

```elixir
iex(4)> h IEx.configure def configure(options)
Configures IEx.
The supported options are: :colors, :inspect, :default_prompt,
:alive_prompt and :history_size.
Colors
A keyword list that encapsulates all color settings used by the shell. See
documentation for the IO.ANSI module for the list of supported colors and
attributes.
The value is a keyword list. List of supported keys:
• :enabled      - boolean value that allows for switching the coloring
                  on and off
• :eval_result  - color for an expressions resulting value
• :eval_info.   - various informational messages
```

### Writing Elixir in Source Files: .ex vs. .exs

Understanding the difference between `.ex` and `.exs` files is crucial in Elixir:

* `.ex` files are compiled, typically used for modules and larger applications.
    
* `.exs` files are interpreted, ideal for scripts and quick experimentation.
    

Example — Running an .exs Script:

```elixir
# Example: Running an .exs script
IO.puts("Hello from script.exs")
```

### Why Functional Programming?

Functional programming is a cornerstone of Elixir’s design. It emphasizes immutability, pure functions, and predictable code, allowing for easier maintenance and debugging.

### The Limitations of Imperative Languages

Imperative languages often struggle with concurrency, fault tolerance, and scalability. Elixir’s functional approach addresses these limitations.

### Immutability

Immutability ensures that data does not change once it’s created, leading to more reliable and predictable code.

Example — Immutability in Elixir:

```elixir
# Immutable list
list = [1, 2, 3]
new_list = [0 | list]
# new_list is [0, 1, 2, 3], list remains [1, 2, 3]
```

### Advantages of Functional Programming

Elixir leverages functional programming’s strengths, offering code maintainability, reliability, and parallelism. These advantages are a significant driver behind Elixir’s growing popularity.

Example — Code Maintainability:

```elixir
# Functional code for finding the factorial of a number
factorial = fn
  0 -> 1
  n -> n * factorial.(n - 1)
end
```

### Functional vs. OOP

Let’s compare functional programming to object-oriented programming (OOP), highlighting the differences and discussing scenarios where each paradigm excels.

Example — Functional vs. OOP Comparison:

![](https://cdn-images-1.medium.com/max/1600/1*qebjM3acsaI6QgIMh7G9kw.png align="left")

In conclusion, we’ve explored the fundamental topics that set the stage for understanding Elixir and its functional and concurrent capabilities. In the upcoming parts of our Elixir series, we’ll delve deeper into these topics and explore Elixir’s features and capabilities in even greater detail. Whether you’re new to Elixir or looking to deepen your knowledge, this series has something for everyone.