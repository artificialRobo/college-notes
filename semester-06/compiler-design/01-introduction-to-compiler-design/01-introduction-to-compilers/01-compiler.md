# 1.1. Definition and Functions of a Compiler

## 1. What is a compiler?

A **compiler** is a system software program that translates a program written in a **source language** (usually a high-level programming language) into an equivalent program in a **target language**, while detecting and reporting errors in the source program.

A more formal view is:

$$
\text{Source Program} \xrightarrow{\text{Compiler}} \text{Target Program}
$$

For example:

```
Source program (C)
        |
        v
     Compiler
        |
        v
Assembly / machine-oriented target code
```

The source language is designed to be convenient for humans. The target language is designed to be executed by a particular machine or runtime system.

For example, a programmer may write:

```
int sum = a + b;
```

The compiler analyzes the meaning and structure of this statement and eventually produces lower-level instructions that the target machine can execute.

A compiler is therefore **not merely a translator of words**. It must understand the structure and meaning of the source program sufficiently to produce correct target code.

---

## 2. Why is a Compiler Needed?

Computers ultimately execute instructions in a form understood by their processor or execution environment. Human programmers, however, generally use languages such as C, C++, Java, or similar high-level languages because they provide abstraction and make programs easier to develop and maintain.

There is therefore a gap between:

* the language convenient for humans, and
* the language directly executable by a machine.

The compiler acts as the bridge between these two levels.

### Without a compiler

A programmer would have to write programs directly in machine language or another low-level representation. This would make programming:

* difficult,
* error-prone,
* machine-dependent,
* and difficult to maintain.

### With a compiler

The programmer can use abstractions such as:

```
variables
functions
loops
arrays
classes
expressions
```

and the compiler handles the translation into an appropriate lower-level representation.

Thus, the fundamental purpose of a compiler is **to automate the translation from a higher-level programming notation to a lower-level target representation**.


---

## 3. Main Functions of a Compiler

A compiler performs several related functions rather than one simple translation operation.

### 3.1 Translation

The primary function is to translate the source program into an equivalent target program.

The compiler should preserve the intended behavior of the source program. In other words, the generated program should perform the same computation, subject to the language and compiler's defined semantics.

### 3.2 Error Detection and Reporting

A compiler detects errors in the source program and reports them to the programmer.

Errors may occur at different levels. For example:

```
int x = ;
```

contains a syntactic problem because the statement is incomplete.

A compiler may also detect problems involving types, declarations, or other language rules.

Importantly, **error detection is not a separate unrelated activity**. It is integrated into the various stages of compilation because different stages have different kinds of information available to them.

For example:

* lexical analysis can detect invalid character sequences,
* syntax analysis can detect violations of grammatical structure,
* semantic analysis can detect certain meaning-related errors.

### 3.3 Checking the Correctness of Program Structure and Meaning

The compiler verifies that the program conforms to the rules of the source language.

* This includes checking things such as:
* whether tokens form valid language constructs,
* whether expressions and statements have valid structures,
* whether identifiers are used appropriately,
* whether operations are compatible with their operands,
* and whether declarations and uses are consistent.

This checking is essential because successful translation should not simply mean that the source text can be converted mechanically into machine instructions.

### 3.4 Optimization

A compiler may transform the program to produce more efficient target code without changing its intended behavior.

For example, suppose the source contains:

```
x = 10 * 20;
```

The compiler can recognize that the multiplication involves constants and may calculate the result during compilation:

```
x = 200;
```

This is an example of constant folding.

Optimization can target several properties, including:

* execution speed,
* memory usage,
* code size,
* and sometimes energy consumption.

Optimization is important, but it must preserve the observable meaning of the program.

### 3.5 Target Code Generation

After analyzing the source program, the compiler eventually generates code for the target machine or target environment.

The target may be:

* machine language,
* assembly language,
* an intermediate representation,
* bytecode,
* or another suitable target form, depending on the compiler architecture.

Thus, compilation can be viewed as a sequence of transformations rather than a single direct conversion.

---

## 4. Overall View of Compilation

A simplified conceptual representation is:

```
SOURCE PROGRAM
                     |
                     v
          +----------------------+
          |      COMPILER        |
          |                      |
          | Analysis + Synthesis |
          +----------------------+
                     |
                     v
              TARGET PROGRAM
```

The compiler must answer two broad questions:

1. **What does the source program mean?**
2. **How should that meaning be represented in the target language?**

This leads to an important distinction between the analysis and synthesis aspects of compilation.

---

## 5. Analysis and Synthesis

A compiler is often conceptually divided into two major parts:

```
Source Program
      |
      v
+-------------+
|   Analysis  |
+-------------+
      |
      v
Intermediate Representation
      |
      v
+-------------+
|  Synthesis  |
+-------------+
      |
      v
Target Program
```

### 5.1 Analysis

The **analysis phase** examines the source program and determines its structure and meaning.

It breaks the source program into meaningful components and checks whether those components satisfy the rules of the language.

Analysis commonly includes:

* lexical analysis,
* syntax analysis,
* semantic analysis,
* and related intermediate representation construction.

The analysis portion is sometimes called the front end of a compiler.

### 5.2 Synthesis

The **synthesis phase** uses the information obtained during analysis to construct the target program.

It commonly involves:

* optimization,
* target-code generation,
* and machine-dependent transformations.

This part is often associated with the back end of a compiler.

The distinction is useful because it separates:
> understanding the source program

from
> constructing an appropriate target program.

---

## 6. Compiler as a Language Translator

It is useful to understand a compiler in the broader context of language processing systems.

Suppose:

```
Source Language
      |
      |  translation
      v
Target Language
```

The compiler must understand the rules of both languages sufficiently to perform the translation correctly.

The source language has:

* **syntax** - rules describing how valid programs are formed,
* **semantics** - rules describing what valid programs mean.

The compiler therefore needs mechanisms for both structural analysis and meaning-related analysis.

This is why compiler design involves concepts from:

* formal languages,
* automata theory,
* algorithms,
* data structures,
* computer architecture,
* and programming language theory.

---

## 7. Important Terminology

Several terms are closely related and should not be confused.

### Source Program

The program written by the programmer in the source language.

Example:

```
int x = a + b;
```

### Source Language

The language in which the source program is written, such as C.

### Target Program

The program produced by the compiler in the target language.

### Target Language

The language into which the source program is translated.

### Compiler

The system that performs the translation together with associated analysis, error detection, and possibly optimization.

### Translation

The general process of converting a program from one language or representation to another.

A compiler is therefore a specialized and sophisticated **language translator**.


---

## 8. A Small Conceptual Example

Consider:

```python
x = a + b * 2;
```

A compiler cannot simply translate the characters from left to right without understanding their relationships.

It needs to determine, among other things, that:

1. `x`, `a`, and `b` are identifiers.
2. `=` is an assignment operator.
3. `+` and `*` are arithmetic operators.
4. `2` is a numeric constant.
5. `b * 2` is grouped before addition because multiplication has higher precedence.
6. The complete expression is assigned to `x`.



Conceptually, the compiler therefore discovers a structure similar to:

```
          =
        /   \
       x     +
            / \
           a   *
              / \
             b   2
```

This illustrates an important idea:

> Compilation is fundamentally an analysis-and-transformation process, not merely character-by-character translation.

The later compiler phases use structures such as this to generate appropriate target code.

---

## 9. Characteristics of a Good Compiler

A well-designed compiler should satisfy several important requirements.

### Correctness

The most important requirement is that the generated program should correctly implement the intended semantics of the source program.

### Efficient target code

The compiler should ideally generate code that uses machine resources effectively.

### Efficient compilation

The compiler itself should not take an unreasonable amount of time or memory.

### Good error reporting

Errors should be detected and reported in a way that helps the programmer locate and correct them.

### Portability

A compiler may be designed so that much of its source-language processing can be reused across different target machines.

### Maintainability

A compiler is a large software system. Its components should therefore be organized so that they can be modified, extended, and tested effectively.

There is often a trade-off between these goals. For example, sophisticated optimization can improve target-code performance but may increase compilation time and compiler complexity.


---

## 10. Compiler vs Interpreter

A common distinction in programming-language processing is between a **compiler** and an **interpreter**.

A compiler generally translates a source program into a target representation before execution.

An interpreter, in contrast, directly performs the operations specified by the source program or an intermediate representation during execution.

A simplified comparison is:

| Aspect | Compiler | Interpreter |
| --- | --- | ---|
| Basic operation | Translates source into target form | Executes/interprets the program |
| Target code | Usually produced | May not produce a permanent machine-code program |
| Execution | Generated target code is executed | Interpretation occurs during execution |
| Error reporting | Often reports errors during compilation | Many errors may appear during execution |
| Optimization | Can perform substantial compile-time optimization | Usually has a different optimization model |


However, modern language implementations often combine the two approaches. For example, a system may compile source code into an intermediate form and then interpret or further compile that representation.

Therefore, **"compiled" and "interpreted" are not always completely exclusive categories in modern systems**.

---

## 11. Compiler and Assembler: An Important Distinction

A **compiler** translates a high-level language into a lower-level target language.

An **assembler**, by contrast, translates an **assembly language program** into machine code.

For example:

```
High-level language
        |
     Compiler
        |
   Assembly language
        |
     Assembler
        |
    Machine code
```

The assembler therefore operates at a lower level than a typical high-level-language compiler.

This distinction becomes particularly important when studying the complete program-processing system surrounding a compiler.

---

## Revision Focus

Remember these points particularly well:

* A **compiler** is a system software program that translates a source program into an equivalent target program while performing analysis and reporting errors.

* The fundamental purpose of a compiler is to bridge the gap between a **human-oriented source language** and a **machine-oriented target representation**.

* Major compiler functions include:

  * translation,
  * error detection and reporting,
  * program analysis,
  * optimization,
  * and target-code generation.

* Compilation can be understood broadly as:

$$
  \text{Source Program} \rightarrow \text{Analysis} \rightarrow \text{Intermediate Representation} \rightarrow \text{Synthesis} \rightarrow \text{Target Program}
$$

* A compiler is more than a simple text translator because it must understand the **syntax and semantics** of the source program.

* Do not confuse:

  * compiler with interpreter,
  * compiler with assembler,
  * source program with target program,
  * source language with target language.

* **Correctness is the primary requirement** of a compiler; optimization and efficiency are important but must not change the intended program behavior.
