to fully understand Java, one must understand the reasons behind its creation, the forces that shaped it, and the legacy that it inherits.

like the successful computer languages that came before, Java is a blend of the best elements of its rich heritage combinded with the innovative concepts
required by its unique mission.

This Chapters talk about 
1. how and why Java came about.
2. why Java is so important.
3. how it has evovled over the years.

although Java has become inseparatly linked with the online environment of the Internet,
it is important to remember that Java is first and foremost a programming language.

computer languages innovation and development occurs for two fundamental reasons:
1. to adapt to changing environments and uses.
2. to implement refinements and imporvements in the art of programming.

## Java's Lineage
1. Java is related to C++, which is a direct descendant of C.
2. From C, Java derives the syntax.
3. Many of Java's object-oriented features were influenced by C++.
4. moreover, the creation of Java was deeply rooted in the process of refinement and adaptation that has been occuring in computer programming languages
   for the past serveral decades.
5. each innovation in language design was driven by the the need to solve a fundamental problem that the preceding languages could not solve.

## The birth of Modern Programming: C
> the creation of C was a direct result of the need for a structured, efficient, high-level language
> that could replace assembly code when creating system programs.

trade-offs are made during the language design:
1. easy-of-use vs power.
2. safety vs efficiency
3. rigidity vs extensibility

assembly language can be used to produce highly efficient programs, but it is not easy to learn or use efficiently.
further, debugging assembly code could be very difficult

early computer languages such as BASIC, FORTRAN were not designed around structured principles.
as a result, programs written using these languages tend to produce "spaghetti code**
a mass of tangled jumps and conditional branches that make a program virtually impossible to understand

C was started with a older language called BCPL which are called B
C was formally standardized in December 1989
C have marked the beginning of the modern age of computer languages.
**C was a programmer's language.**

## C++: The Next Step

since C is a successful and useful language, why a need for something else existed.
The answer is **complexity**, programs are larger and more complex
With structured language, once a project reaches a certain size, its complexity exceeds what a programmer can manage.
To solve this problem, **OOP (object-oriented programming)** was intruduced.
> OOP is a programming methdology that helps organize complex programs through the use of **inheritence**, **encapsulation**, **polymorphism**

> C++ was invented in 1979, first was called "C with Classes", then changed to "C++", extends C by adding object-oriented features.

## The Creation of Java
- Java was conceived in 1991, first was called 'Oak', renamed "Java" in 1995
- the public announcement of Java in the spring of 1995
> Java's creation was the need for a platform-independent (architecture-neutral) language

- the trouble with C and C++ is that they are desinged to be compiled for a specific target.
- to compile a C++ program for any type of CPU, requires a full C++ compiler targeted for that CPU.
- compilers are expensive and time-consuming to create.

> World Wide Web demand portable programs.

## How Java Impacted the Internet

### Java Applets
> An applet is special kind of Java program that is designed to be transimitted over the Internet and automatically executed inside a Java-compatible browser.
- applet will download and run in the browser
- applet support was removed by JDK 11.

Security
- a program that download and executes on client computer must be prevented from doing harm.
> Java enables you to confine an application to the Java execution environment and prevent it from accessing other parts of the computer.
> The ability to download programs with a degree of confidence that no harm will be done may have been the single most innovative aspect of Java.

Portability
> the same application code must work on all computers.
- some means of generating portable executable code was needed.
> the same mechanism that helps ensure security also helps create portability.

## Java's Magic: The ByteCode

> the key that Java to solve both the security and portability problems is that the output of a Java compiler is not executable code.
> Rather, it is bytecode.
> ByteCode is a highly optimized set of instructions designed to be executed by JVM, which is part of JRE (Java Runtime Environment)
- The original JVM was designed as an interpreter for bytecode
- many modern languages are designed to be compiled into executable code because of performance concerns.
- once a JRE exists for a given system, any Java program can run on it.
- If a Java program were compiled to native code, then different version of the same program would have to exist for each type of CPU.

> The fact that a Java program is executed by the JVM also helps to make it secure.
> because JVM is in control, it manages program execution.
> it is possible for the JVM to create a sandbox.

> because bytecode has been highly optimized, JVM could run the program much faster than you expected.

> JIT (Just-In-Time) compiler
- Hotspot provides a JIT compiler for bytecode.
- With JIT, selected portions of bytecode are compiled into executable code in real time.
- a JIT compiler compiles code as it is needed, during execution.
- even when dynamic compilation is applied to bytecode, the portability and safety features still apply
- because the JVM is still in charge of the execution environment.

> ahead-of-time compiler for Java
- such a compiler compile bytecode into native code prior to execution by the JVM, rather than **on-the-fly**

## Moving Beyond Applets.
However, applets rely on a Java browser plug-in. 
Thus, for an applet to work, the browser must support it. Over the past few years, support for the Java browser plug-in has been waning.
beginning with JDK 9, the phase-out of applets was begun, with support for applets being deprecated. 
In the language of Java, deprecated means that a feature is still available but flagged as obsolete. 
Beginning with JDK 17, the entire Applet API was deprecated for removal.

> jlink
- added by JDK9
- It can create a complete run-time image that includes all necessary support for your program, including the JRE

> jpackage
- added by JDK16
- can be used to create a ready-to-install application

## A Faster Release Schedule
- in the past, major Java releases were separated by two or more years.
- after realease of JDK9, just six months.

> feature release
- each six-month release, now called a **feature release**, will include those features ready at the time of the release.

> LTS (long-term support) release
- three-year intervals, will have a LTS release
- An LTS release will be supported (and thus remain viable) for a period of time longer than six months.
- The first LTS release was JDK 11.
- The second LTS release was JDK 17.
- Currently, feature releases are scheduled for March and September of each year.

## Servlets: Java on the Server Side

> a servlet is a small program that executes on the server.
> servlet are used to create dynamically generated content to client.
> the only requirements to run a servlet are that the server support the **JVM and a servlet container**.

## The Java Buzzwords

> the invention of Java are portability and security.
1. Simple
2. Secure
3. Portable
4. Object-oriented
5. Robust
6. Multithreaded
7. architecture-netural
8. Interpreted
9. High performance
10. Distributed
11. Dynamic

### Object-Oriented
- Java managed to strike a balance between the purist’s “everything is an object” paradigm and the pragmatist’s “stay out of my way” model.
- In Java, The Object model is simple and easy to extend
- while primitive types such as Integers were kept as high-performance

### Robust
- in Java, a program must execute well in a variety of systems.
- Java helps you to write a robust program.
- Java is strictly type language, checks your code at compile time.
- Java also checks your code at run time.
- Java let you write programe in a predictable way.

- two main reasons for program failure:
1. memory management mistakes.
   > Java manage memory for you
2. mishanlded exceptional conditions (run-time errors)
   > Java providing object-oriented exception handling
   > all run-time errors can-and-should be managed by your program.

### Architecture-Neutral
> write once, run anywhere, any time, forever.
> no matter about how the architecture are changed or upgrade, your program will work well all the time.

### Distributed
- handle TCP/IP protocols.
- accessing a URL is not much different from accessing a file.
- Java also support **RMI(remote method invocation)**

### Dynamic
> Java programs carry with them substantial amounts of run-time type information that is used to verify and resolve access to objects at run time.
> it makes it possible to dynamically link code in a safe and expedient manner.
> small fragments of bytecode may be dynamically updated on a running system which is crucial to the robustness of Java.

## The Evolution of Java.

- Java2
: first release of Java 2 used the 1.2 version number. 
: mark the beginning of Java's modern age
: With Java 2 , Sun repackaged the Java product as J2SE (Java 2 Platform Standard Edition)

- J2SE 1.3
: J2SE 1.3 was the first major upgrade to the original Java 2 release. 

- J2SE 1.4 The release of J2SE 1.4 further enhanced Java. 

- J2SE 5
: it was revolutionary.
: Generics
: Generics
: Autoboxing and auto-unboxing
: Enumerations
: Enhanced, for-each style for loop
: Variable-length arguments (varargs)
: Static import
: Formatted I/O
: Concurrency utilities
: the developer’s kit was called JDK 5
> in order to maintain consistency, Sun decided to use 1.5 as its internal version number, as **developer version number**
> The “5” in J2SE 5 is called the **product version number**.

- Java SE 6 ( Java Platform, Standard Edition 6.)
: JDK 6
: As with J2SE 5, the 6 in Java SE 6 is the product version number. The internal, developer version number is 1.6.

- Java SE 7
: A String can now control a switch statement.
: Binary integer literals
: Underscores in numeric literals.
: An expanded try statement, called try-with-resources, that supports automatic resource management.
: Type inference (via the diamond operator)
: Java SE 7 made several additions to the Java API library. 
  1. enhancements to the NIO Framework
  2. the addition of the Fork/Join Framework

- Java SE 8
: the lambda expression, add functional programming features to Java.
: new stream API, which is packaged in java.util.stream
: java.util.function. It defines a number of functional interfaces
: define a default implementation for a method specified by an interface.

- Java SE 9
: modules
: a tool called jlink was added to the JDK
: A new file type, called JMOD, was created
: JShell
: support for private interface methods.

- Java SE 10 (JDK 10)
: local variable type inference. 
: sensitive keyword var

-  Java SE 11 (JDK 11)
: was an LTS release. 
: HTTP Client API - provides enhanced, updated, and improved networking support for HTTP clients

- JDK 12 and JDK 13 did not add any new language features.

- JDK 14
: switch that produces a value 

- JDK 15
: Text blocks, which are essentially string literals that can span more than one line,

- JDK 16
: enhanced instanceof with pattern matching
: added a new type of class called a record 
: A record provides a convenient means of aggregating data
: jpackage - a new application packaging tool

- Java SE 17 (JDK 17)
: second LTS Java release
: seal classes and interfaces.





