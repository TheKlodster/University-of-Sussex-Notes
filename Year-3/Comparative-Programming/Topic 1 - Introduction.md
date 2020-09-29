# Introduction

### Programming Paradigms
- **Imperative Languages**: programs are decomposed into computation steps, and routines are used to modularise the program/ Such as:
	- variables, assignment, iteration and procedures.
	- E.g. Fortran, Pascal and C (Java has an imperative *subset*).
- **Functional Languages**: *what* is computed, rather than *how*. Emphasise the use of expressions evaluated by simplification.
	- E.g. Haskell, SML, Caml, Clean.
- **Object-oriented Languages**: emphasise the hierarchies of objects.
	- E.g. Java, Smalltalk.
- **Logic Languages**: programs describe a problem rather than defining an algorithmic implementation.
	- E.g. Prolog.

### Definition of a Programming Language
1. *Syntax* - defines the form of programs.
   - Concrete Syntax: describes which chains of characters are well-formed programs.
   - Abstract Syntax: descirbes the syntax trees, to which a semnatics is associated.
2. *Semantics* - gives the meaning of programs; two types: *static* (e.g. typing) and *dynamic* semantics.
	- Static Semantics: the goal is to detect programs that are syntatically correct but will give runtime errors, e.g. ```true && 37```.
3. *Implementation* - a software system that can read the program and execute it in a machine.