# Introduction
## Programming Domains
- **<big>Scientific applications</big>**: Need array and floating point **e.g Fortran**
- **<big>Business applications</big>**: Produce reports, use decimal numbers and characters **e.g COBOL**
- **<big>Artificial intelligence</big>**:  Symbols rather than numbers manipulated; use of linked lists**e.g LISP(early),Python**
- **<big>Systems programming</big>**:Need efficiency because of continuous use **e.g C**
- **<big>Web Software</big>**:collection of languages **markup (e.g., HTML), scripting (e.g., PHP), general-purpose (e.g., Java)**
## Language evaluation criteria
- **<big>Readability(可讀性)</big>**:How easy programs can be **read and understood**.Depends on simplicity of language.
We **need well-defined APIs ,Minimizing feature multiplicity**. **Avoiding having count = count + 1, count += 1, and count++** . And restrict operator overloading(運算子過載) both help improve readability
- **<big>Writability(可寫性)</big>**: The key is language simplicity and orthogonality(正交性). Meaning small number instruction can create rich functionality. Support for abstraction, provides convenient syntax for specifying operations (e.g., count++ in C).
- **<big>Reliability(可靠性)</big>**: Whether a program can run sucess under all condition. **Type checking** is important factor in ensuring reliability , and  **compile time checking** better than run time checking. Languages with poor readability and writability are often difficult to maintain, which decrease reliability.
## Influences on Language Design
- **<big>Computer Architecture</big>**:The development of programming languages is heavily influenced by the prevalent von Neumann architecture
- **<big>Imperative Languages(指令式語言)</big>**:Most dominant languages are imperative because their design foundation perfectly matches how von Neumann computers operate. In this architecture, data and programs are stored separately in memory and then piped to the CPU for processing.
- **<big>Von Neumann Bottleneck(馮·紐曼瓶頸)</big>**: This is an inherent performance limitation of this hardware architecture.

## Language Design Trade-Offs
- **<big>Reliability vs Cost of Execution</big>**:Java enforces array index range checking to improve reliability, while C lacks this mechanism. Therefore, a C program will typically execute faster than a semantically equivalent Java program, meaning a lower execution cost.
- **<big>Reliability vs. Writability (Flexibility)</big>**: C++ provides powerful and highly flexible pointers (improving writability), but this can also easily lead to unreliable code.

## Implementation Methods
- **<big>Compilation</big>**:Translating **high-level source code into machine language**. The translation process is slow, but the execution is very fast. The entire process includes **lexical analysis, syntax analysis, semantics analysis, and code generation**. The generated machine code must also be linked with system programs and user programs to form an executable load module **e.g C++ C**  

- **<big>Pure Interpretation</big>**:the source code is executed directly by an interpreter.
Execution speed is slow
 **e.g., JavaScript, PHP**  
 - **<big>Hybrid Implementation </big>**:Between compilers and pure interpreters. Source code is first translated into an intermediate language that is easy to interpret, making execution faster than pure interpretation. **e.g., Java, Perl**  

