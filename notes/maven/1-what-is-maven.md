# What is Maven

> Apache Maven is a **software project management and comprehension tool**
> based on the concept of a **project object model(POM)**
> Maven can manage a project's build, reporting and documentation from a central piece of information

## Introduction
- Maven, a Yiddish word meaning **accumulator of knowledge**
- began as an attempt to **simplify** the **build processes** in the Jakarta Turbine project
- there were several projects, each with their own Ant build files, that were all slightly different.
- JARs were checked into CVS.
- we wanted a 
1. a standard way to build the project
2. a clear definition of what the project consists of
3. an easy way to publish project information
4. and a way to share JARs across several projects

## Maven's Objectives

> Maven's primary goal is to allow a developer to **comprehend the complete state of a development** effort in the shortest period of time.
> in order to attain this goal, Maven deals with several areas of concern:
1. Making the build process easy.
   : while using Maven doesn't eliminate the need to know about the underlying mechanisms
   : Maven does shield developers from many details.
   
2. Providing a uniform build system.
   : Maven builds a project using its POM and a set of plugin.
   : once you familiarize with a Maven project, you know how all Maven projects build.
   
3. providing quality project information.
   : Maven provides useful project information that is **in part** taken from your POM and in part generated from your project's sources.
   : 1. Change log created directly from source control
   : 2. cross referenceed sources
   : 3. Mailing lists managed by the project
   : 4. Dependencies used by the project
   : 5. Unit test reports including coverage
   : third party code analysis products also provide Maven plugins that add their reports to the standard information given by Maven

4. encouraging better development practices
   providing guidelines for best practices development
   1. keeping test source code in a separate, but parallel source tree.
   2. using test case naming conventions to locate and execute tests.
   3. having test cases setup their environment instead of customizing the build for test preparation.
   4. Maven also assists in project workflow such as releast and issue management
