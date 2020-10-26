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


### Substitution
Substitution is a special kind of replacement: M{x &rarr; N} means replace all *free* occurrences of x in M by the term in N.

Question: why only the free occurrences? <br>
In case there are occurrences of y in x, for instance.

Some examples (conversion, reduction, substitution).

α-converion:
- <code>λx.x = <sub>α</sub>λy.y</code>
- <code>λx.λy.xy = <sub>α</sub>λz<sub>1</sub>.λz<sub>2</sub>.z<sub>1</sub>z<sub>2</sub></code>

β-reduction:
- <code>(λx.λy.xy)(λx.x) &rarr; <sub>β</sub>λy.(λx.x)y &rarr; <sub>β</sub>λy.y</code>

## Normal Forms
**Normal forms** are terms that does not contain any redex, and cannot be reduced anymore.

A term that can be reduced to normal form is *normalisable*.

**Weak Head Normal Form (WHNF)**: Stop reducing when there are no redexes left, but without reducing under an abstraction.

<code>(λx.xx)(λx.xx)</code> does not have a normal form!!!

## Properties of Computations
- **Confluence**: If M &rarr; <sub>β</sub><sup>\*</sup>M<sub>1</sub>, and M &rarr; <sub>β</sub><sup>\*</sup>M<sub>2</sub>, then there exists a term M<sub>3</sub> such that M<sub>1</sub> &rarr; <sub>β</sub><sup>\*</sup>M<sub>3</sub> and M<sub>2</sub> &rarr; <sub>β</sub><sup>\*</sup>M<sub>3</sub>.
- **Normalisation**: exists a sequence of reductions which terminates.
- **Strong Normalisation (or Termination)**: all reduction sequences terminate.

The λ-calculus is confluent but not normalising (or strongly normalising). Confluence *implies* unicity of normal forms: each λ-term has at most one normal form.
