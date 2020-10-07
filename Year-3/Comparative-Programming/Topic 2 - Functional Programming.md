# Topic 2: Functional Programming

Programming that consists entirely of functions. The focus is *what* is to be computed, not *how* it should be computed.

| Advantages | Disadvantages |
| ---------- | ------------- |
| - Shorter Programs | - Often slower than imperative programs. |
| - Easier to understand | |
| - Easier to design & maintain than imperative programs. | |


### Syntax of Functional Programs

We can compute the square of a number using a function *square* define by the equation:

<code>square x = x * x</code>

**Execution of Programs** <br>
The role of the computer is to evaluate and display the results of the expressions that the programmer writes, using the available functions.

The process of evaluating an expression is a *simplification process*, also called *reduction* or *evaluation*.

Examples:

<code>square 6 -> 6 * 6 -> 36</code>

### Properties
1. **Unicity of normal forms**: in functional languages, the value of an expression is uniquely determined by its components, and is independent of the order of reduction.
	- Advantage: readability of programs.
2. **Non-termination**: not all reduction sequences lead to a value, some *do not terminate*.

**Example**

Let us define the constant function <br>
<code>fortytwo x = 42</code>

and the function *infinity* <br>
<code>infinity = infinity + 1</code>

The evaluation of <code>infinity</code> never reaches a normal form. For the expression <code>fortytwo infinity</code> some reduction sequences do not terminate, but those which terminate give the value of <code>42</code> (unicity of normal forms).

### Strategies
Most popular strategies:
- *Call-by-name* (normal order): reduce first the application using the definition of the funtion, then the argument.
- *Call-by-value* (applicative order): evaluate first the argument and then the application using the definition of the function.

<center>
An example reduction graph for the expression: <code>square (3+4)</code>

<img src=https://i.gyazo.com/0e569dbfd5be2cb9d9df306c3d92d0b2.png>

This has the shortest path for *call-by-value*.

Note: we underline each **reducible expression** (*redex*), all reductions lead to the same answer, and some reductions are longer than others.
</center>

<center>

<img src=https://i.gyazo.com/f76bc32e9506e86e3195612963fbfd31.png>

In this case, call-by-value gives the longest reduction path.

</center>

(fortytwo infinity, callbyname finds value, gets fortytwo, callbyvalue will not terminate.)

Call-by-name always finds the value, if there is one. <br>
Call-by-value is in general more efficient, but may fail to find a value.

Haskell uses *lazy evaluation*, which guarantees that if an expression has a normal form, the evaluator will find it: <br>
<code>lazy evaluation = call-by-name + sharing</code>