# Topic 3: Foundations

## λ-Calculus
### Syntax
The following are all the same:
- <code>f x y = x + y</code>
- <code>f x = λy.x + y</code>
- <code>f = λx.λy.x + y</code>

### Conventions
Write as few parentheses as possible:
- <code>(λy.(λxy))</code> = <code>λy.xy</code>

**Application** associates to the left:
- <code>xyz</code> = <code>((xy)z))</code>

**Abstractions** bind as far right as possible:
- <code> λx.(λy.y)x</code> = <code>(λx.((λy.y)x))</code>

**Abstraction** can be abbreviated:
- <code>λx.λy.M</code> = <code>λxy.M</code>

<code>\x -> M</code> is the same as λx.M

### Variables
A variable is *free* in a λ-term if it is not bound by a lamda.
- <code>x</code> is a free variable.
- <code>λx.x</code> is *not* a free variable.

### Computation
<center>
**α-reduction**
</center>

λ-terms that differ only in the names of their bound variables will be equated. More precisely: if y is not free in M:

<center>
<code>λx.M = <sub>α</sub>λy.M{x -> y}</code>
</center>
where M{x -> y} is the term M where each occurence of x is replaced by y.

- λ-terms are defined modulo α-conversion, so λx.x and λy.y are the SAME term.
- α-equivalent terms represent the same computation.

<center>
**β-reduction**
</center>

Abstractions represent functions, which can be applied to arguments. The main computaation rule is β-reduction, which indicates how to find the result of the function for a given argument.

<center>
<code>(λx.M)N</code> -> <code><sub>β</sub>M{x -> N}</code> <br>
It reduces to the term <code>M{x -> N}</code> where it is the term obtained when we substitute <code>x</code> by <code>N</code> taking into account bound variables.
</center>

