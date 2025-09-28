# FRequent Calculi

This is a **fr**amework for developing and reasoning about s**equent** proof systems. Early development & WIP. This is intended as an experiment.

Built with [Athena](https://github.com/AthenaFoundation/athena/tree/master)


## Layout

- `/sequent-calculus.ath`: This file defines the sequent calculus abstract syntax. Proof objects are polymorphic over a rule datatype. The intention will be to define proof-theoretic properties in this module that an extending module can prove for a particular rule system.

- `/parser/`: Contains a lexer and parser. Likely, what will be generated is a proof object of sort `(Proof Ide)`, in which case the parser will come with a function along the lines of `(transform proof transformer)` where `proof` is of sort `(Proof Ide)` and transformer has the signature: `(Proof Ide) -> (Proof <SpecificRuleDatatype>)`.

- `/calculi`: This is intended to contain specific sequent systems.


## Syntax

Regardless of specific proof system, the base syntax is like the following example of a sequent proof in Gentzen's LK:

```
     p |- p     
   ------------ (rule-WR)  
     p |- p, q                   q |- q
   ----------- (rule-XR)       -----------      (rule-WL)
     p |- q, p                 p, q |- q
   ----------- (rule-NEG-L)    -----------      (rule-XL)
   ~p, p |- q            q, p |- q
    -----------------------------               (rule-OR-L)
        ~p or q, p |- q
        ---------------                         (rule-XR)
        p, ~p or q |- q
        -----------------------------           (rule-IMP-R)
            ~p or q |- p ---> q

```

The accepted `rule-` tags (and the syntactic transformations that they permit) are the primary distinction between different proof systems implemented in this framework.

