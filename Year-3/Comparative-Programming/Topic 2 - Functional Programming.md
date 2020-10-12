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

### Syntax of Function Definitions
Functions are defined in terms of equations. <br>
Example: <br>
<code>square x = x * x</code> <br>
<code>min x y = if x <= y then x else y</code>

We can also use *conditional equations* <br>
```
min x y
	| x <= y = x
	| x > y = y>
sign x
	| x < 0 = -1
	| x == 0 = 0
	| x > 0 = 1
```

This is equivalent to: <br>
<code>if x < 0 then -1 else if x == 0 then 0 else </code> ew not as clear.

Error is a predefined function that takes a string as argument. When evaluated it causes immediate termination of the evaluator and dispalys the string.

### Local Definitions
We can write:
<code>f x = a + 1 where a = x/2</code> which is the same as <code>f x = let a = x/2 in a + 1</code>

<code>let</code> and <code>where</code>  are used to introduce **local definitions**.

```
f x = square (successor x) where
	square z = z * z; successor x = x + 1
```

### Functional Composition
Combine functions through *composition*, denoted by <code>.</code> as in <code>f . g</code>. <br>
Composition is itself a function:
```
(.) :: (B -> r) -> (a -> B) -> (a -> r)
(f . g) x = f (g x)
```
Example:
```
square :: Integer -> Integer
quad = square . square
```

### Types: General Concepts
Predefined types:
- Basic data types: <code>Bool, Char, Int, Integer, Float</code>...
- Structured types: <code>[Integer]</code> is the type of *lists* of integers.
- Function types: <code>(Integer -> Integer) -> Integer</code> are *arrow types*

### Polymorphism
Type systems can be
- *monomorphic*: every expression has at most one type.
- *polymorphic*: some expressions have more than one type.

**Overloading** is the notion where several functions, with different types, share the same name.

### Disjoint Sums
We can define several constructors in a type. <br>
Example:
<code>data Nat = Zero | Succ Nat</code> <br>
<code>Zero</code> and <code>Succ</code> are *constructors*. In this case, they are not polymorphic, but we could define a type with polymorphic constructors.

### Constructing Data types: Pairs (x,y)

Components do not need to have the same type: <code>(2, True)</code>.
- extract 'c' from <code>((True, 'c'), 42)</code> &rarr; <code>snd (fst ( ))</code>.
- extract 'c' from <code>(True, 'c', 42, (3,4))</code> &rarr; <code>f x = a b c d</code>.

### Lists
Strings in Haskell are just: <code>Char</code>

<code>:,[],head,tail,null,length</code>

```
6:[7,8]				---> [6,7,8]
[1,2,3] ++ [4,5]	---> [1,2,3,4,5]
'h':"ello"			---> "hello"
"h" ++ "ello"		---> "hello"
[1..10]				---> [1,2,3,4,5,6,7,8,9,10]
head [3..]			---> [3]
[3..]				---> [3,4,5,6,7,...,...,...]
[x*x | x <- [1,2,3]]	---> [1*1, 2*2, 3*3]
```

Write a function to sum all the elements of a list.<br>
Example: <code>sum [1..10] = 55</code>

First attempt:<br>
<code>sum x = if null x then 0 else head x+sum (tail x)</code>

Guarded equations:
```
sum x
	| null x = 0
	| otherwise = head x + sum (tail x)
```

Pattern matching:
```
sum [] = 0
sum (h:t) = h+sum t
```

### Algebraic Data Types
We can define our own data types:
- <code>data Bool = True | False</code>
- <code>data Suit = Club | Diamond | Heart | Spade</code>
- <code> data List a = nil | Cons a (List a)</code>
