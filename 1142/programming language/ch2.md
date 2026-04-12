# Evolution of the Major Programming Languages
## The First High-Level Language: Zuse's Plankalkül (1945)
- **<big>Historical Background</big>**:Designed in 1945, **its description was not published until 1972, and it was never implemented**. It was the first high-level programming language designed for a computer
- **<big>Language Features</big>**:It was complete, featuring advanced data structures like floating point, arrays, and records (similar to structs in C)
- **<big>Syntax Characteristics</big>**: A (Fin) command for loop. And selection statement with no (else)
## Overcoming Hardware Limitations: Pseudocodes
- **<big>Development Environment</big>**:These were developed in the late 1940s and early 1950s. Computers of that time were slow, unreliable, expensive, had extremely small memories, and lacked supporting software.
- **<big>Deficiencies of Machine Code(機器碼的缺陷)</big>**: **Machine code had poor readability ,It also had poor modifiability due to absolute addressing**.
- **<big>Short Code (1949)</big>**: Developed by Mauchly for BINAC computers. Expressions were coded from left to right and interpreted by software.
- **<big>Speedcoding (1954)</big>**:Developed by Backus for the IBM 701. It featured pseudo-ops for **floating-point arithmetic and auto-increment registers for array access**, both simulated by software.
## Pioneer of Compiled Languages: IBM 704 and Fortran
 - **<big>Hardware Breakthrough</big>**: The new IBM 704 included floating-point hardware, which meant **floating-point operations no longer had to be simulated in software**. This hardware advancement led to **the end of the interpretive era and the beginning of compiled programming languages**
 - **<big>Design goal</big>**: The primary use of computers was for scientific computations. Because computers had small memory and were slow, machine efficiency was the most important concern.
 - **<big>Fortran I (1957)</big>**: It was the first widely accepted compiled high-level language. No data typing. Cant independent compilation, any change need recompiling the entire program
 - **<big>Fortran II (1958)</big>**:Introduced independent compilation, making it access to develop much larger programs
 - **<big>Fortran IV (1960-62)</big>**: Add type declare for variable and logical IF. Become ANSI standard in 1966
 - **<big>Later Versions</big>**:Fortran 77 introduced character string handling and logical loop control statements. Fortran 90 introduced dynamic arrays and recursion
 
## Moving Toward Modernization and Universality(邁向現代化與通用化): ALGOL 5
- **<big>Motivation</big>**: Other languages were machine-dependent.  ALGOL 58 is a universal programming language for scientific applications
- **<big>Design Goals</big>**:language needed to be close to mathematical notation, good for describing algorithms, and translatable to machine code
- **<big>Key Innovation(重要革新與突破)</big>**:  
    1. Formalized Types(確立型態概念) only variables that were not floating-point required declaration.
    2. Flexible Naming: Names could be of any length,
    3. Advanced Arrays: It allowed any number of array dimensions the programmer could specify the lower bound of arrays
    4. Statement Structures(引入了複合敘述): It introduced compound statements (e.g., begin ... end) and nested selection statements with else-if clauses
- **<big>Feature Compromise</big>**:To prevent the language from becoming machine-dependent, ALGOL 58 included no I/O features
