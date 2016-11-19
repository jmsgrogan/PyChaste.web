---
layout: page-full-width
title: Getting Started
---

## About 
Microvessel Chaste is a library for building simulations with discrete cells and vessels using either Python or C++. It is a plug-in for Chaste, which is a well-known library for agent based cell modelling. Microvessel Chaste comes with a Python interface, which is a low-level C++ wrapper, meaning the much of the functionality of the C++ interface is available and there is negligble performance loss. 

Microvessel Chaste allows detailed multi-scale simulations to be constructed using a friedndly scripting interface, which can be immediately combinded with existing Python software for image processing, data analysis and plotting.

This page gives an introduction to the Python interface, which is the recommended way to get started. If you just want a quick working demo you can jump to the [tutorials](), however you should check back here when troubleshooting.


## Getting Started With Python
Microvessel Chaste depends on PyChaste, which is a Python wrapper for the main Chaste library. The first thing to do when launching a Python session is to import the `chaste` module from PyChaste:

    import chaste

Sub-module naming follows the Chaste source directory layout, so you can use the [Chaste documentation](http://www.cs.ox.ac.uk/chaste/) for module name hints. We will mostly use the following modules:

    from chaste import core
    from chaste import mesh
    from chaste import pde
    from chaste import cell_based

Chaste is designed to work with distributed memory parallelism using MPI (and PETSc). Even when you are running on one processor with most Chaste solvers it is neccessary to do:

    chaste.init()

to initialize MPI. Once `chaste` has been imported and initialized you can import `microvessel_chaste`:

    import microvessel_chaste

Again, module naming follows the source code [directory structure](), the modules we will use the most are:

    import microvessel_chaste.geometry
    import microvessel_chaste.population.vessel
    import microvessel_chaste.pde
    import microvessel_chaste.mesh
    import microvessel_chaste.simulation







The best way to learn Scala depends on what you know already and the way you prefer to learn things. There is a variety of resources available including [books]({{ site.baseurl }}/documentation/books.html), tutorials, training courses, presentations, and of course the Scala compiler for practice. Many people find a good combination is to have one of the Scala books at hand and to start right away trying the examples with the Scala compiler. On the other hand, you may want to get started with a Scala training course or using the material available online.

As your knowledge of Scala grows, you will find there is more advanced material and a very friendly [Scala community]({{ site.baseurl }}/community/) at hand to help you. They all share a passion for Scala and welcome newcomers warmly. Many have written helpful material for programmers new to Scala, will respond to emails asking for help or are sharing neat new techniques, advanced concepts or tools in one of several Scala forums or personal blogs.


## Scala for Programming Beginners

If you are just starting to learn how to code, you will find that a large portion of the material about Scala assumes that you already have some programming experience. There are two valuable resources which we can recommend to programming beginners that will take you directly into the world of Scala:

* The online class [Functional Programming Principles in Scala](https://www.coursera.org/course/progfun), available on Coursera. Taught by the creator of Scala, Martin Odersky, this online class takes a somewhat academic approach to teach the fundamentals of functional programming. You will learn a lot of Scala by solving the programming assignments.
* [Kojo](http://www.kogics.net/sf:kojo) is an interactive learning environment that uses Scala programming to explore and play with math, art, music, animations and games.

## Your first lines of code

### The "Hello, world!" Program

As a first example, we use the standard "Hello, world!" program to demonstrate the use of the Scala tools without knowing too much about the language.

    object HelloWorld {
      def main(args: Array[String]): Unit = {
        println("Hello, world!")
      }
    }

The structure of this program should be familiar to Java programmers: it consists of the method `main` which prints out a friendly greeting to the standard output.

We assume that both the [Scala software]({{ site.baseurl }}/download) and the user environment are set up correctly. For example:

| Environment | Variable         | Value (example)
|:------------|:-----------------|:---------------
| Unix        | `$SCALA_HOME`    | `/usr/local/share/scala`
|             | `$PATH`          | `$PATH:$SCALA_HOME/bin`
| Windows     | `%SCALA_HOME%`   | `c:\Progra~1\Scala`
|             | `%PATH%`         | `%PATH%;%SCALA_HOME%\bin`


### Run it interactively!

The `scala` command starts an interactive shell where Scala expressions are interpreted interactively.

    > scala
    This is a Scala shell.
    Type in expressions to have them evaluated.
    Type :help for more information.

    scala> object HelloWorld {
        |   def main(args: Array[String]): Unit = {
        |     println("Hello, world!")
        |   }
        | }
    defined module HelloWorld

    scala> HelloWorld.main(Array())
    Hello, world!

    scala>:q
    >

The shortcut `:q` stands for the internal shell command `:quit` used to exit the interpreter.

### Compile it!

The `scalac` command compiles one (or more) Scala source file(s) and generates Java bytecode which can be executed on any [standard JVM](http://java.sun.com/docs/books/jvms/). The Scala compiler works similarly to `javac`, the Java compiler of the [Java SDK](http://java.sun.com/javase/).

    > scalac HelloWorld.scala

By default `scalac` generates the class files into the current working directory. You may specify a different output directory using the `-d` option.

    > scalac -d classes HelloWorld.scala


### Execute it!

The `scala` command executes the generated bytecode with the appropriate options:

    > scala HelloWorld

`scala` allows us to specify command options, such as the `-classpath` (alias `-cp`) option:

    > scala -cp classes HelloWorld

The argument of the `scala` command has to be a top-level object. If that object extends trait [`App`]({{page.docpath}}#scala.App), then all statements contained in that object will be executed; otherwise you have to add a method `main` which will act as the           entry point of your program.

Here is how the "Hello, world!" example looks like using the `App` trait:

    object HelloWorld extends App {
      println("Hello, world!")
    }

### Script it!

We may also run our example as a shell script or batch command (see the examples in the man pages of the `scala` command).

The [bash](http://www.gnu.org/software/bash/) shell script `script.sh` containing the following Scala code (and shell preamble):

    #!/usr/bin/env scala

    object HelloWorld extends App {
      println("Hello, world!")
    }
    HelloWorld.main(args)

can be run directly from the command shell:

    > ./script.sh

**Note**: We assume here that the file `script.sh` has execute permission and the search path for the `scala` command is specified in the `PATH` environment variable.
