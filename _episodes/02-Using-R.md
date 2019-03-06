---
title: Using R
teaching: 25
exercises: 10
questions:
- "What can R do?"
- "How can I install new packages?"
objectives:
- "Define a variable"
- "Assign data to a variable"
- "Manage a workspace in an interactive R session"
- "Use mathematical and comparison operators"
- "Call functions"
- "Manage packages"
keypoints:
- "R has the usual arithmetic operators and mathematical functions."
- "Use `<-` to assign values to variables."
- "Use `ls()` to list the variables in a program."
- "Use `rm()` to delete objects in a program."
- "Use `install.packages()` to install packages (libraries)."
source: Rmd
---



## Interactions
Sending code from script to console and repeating the previous lines from script

## Functions
R has many built in mathematical functions. To call a function,
we simply type its name, followed by  open and closing parentheses.
Anything we type inside the parentheses is called the function's
arguments:


~~~
function_name(args1 = val1, arg2 = val2, ...)  # functions  
~~~
{: .language-r}



~~~
Error in function_name(args1 = val1, arg2 = val2, ...): could not find function "function_name"
~~~
{: .error}

> ## TIP:  Getting Functions 
>
> The use a function, for example seq(), which makes regular 
> sequences of numbers, type se and hit TAB.  A popup shows you 
> possible completions.  Specify seq() by typing the next letter
> "q", or by using Up/Down arrows to select.  A floating tooltip 
> will be displayed, giving information about the functions's 
> arguments and purpose.  To display the details in the Help tab 
> in the lower right pane, press F1.
>
> When you have selected the function you want, press TAB once 
> more, and RStudio will add matching opening and closing 
> parenthese for you.  
{: .callout}


Type the arguments and hit return.


~~~
seq(1, 10)  # seq function
~~~
{: .language-r}



~~~
 [1]  1  2  3  4  5  6  7  8  9 10
~~~
{: .output}

Typing a `?` before the name of a command will open the help page
for that command. As well as providing a detailed description of
the command and how it works, scrolling to the bottom of the
help page will usually show a collection of code examples which
illustrate command usage.


## Mathematical functions

R has many built in mathematical functions. To call a function,
we simply type its name, followed by  open and closing parentheses.
Anything we type inside the parentheses is called the function's
arguments:


~~~
sin(1)  # trigonometry functions
~~~
{: .language-r}



~~~
[1] 0.841471
~~~
{: .output}


~~~
log10(10) # base-10 logarithm
~~~
{: .language-r}



~~~
[1] 1
~~~
{: .output}


~~~
exp(0.5) # e^(1/2)
~~~
{: .language-r}



~~~
[1] 1.648721
~~~
{: .output}



## Comparing things

We can also do comparison in R:


~~~
1 == 1  # equality (note two equals signs, read as "is equal to")
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 != 2  # inequality (read as "is not equal to")
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 < 2  # less than
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 <= 1  # less than or equal to
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


~~~
1 >= -9 # greater than or equal to
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}

> ## Tip: Comparing Numbers
>
> A word of warning about comparing numbers: you should
> never use `==` to compare two numbers unless they are
> integers (a data type which can specifically represent
> only whole numbers).
>
> Computers may only represent decimal numbers with a
> certain degree of precision, so two numbers which look
> the same when printed out by R, may actually have
> different underlying representations and therefore be
> different by a small margin of error (called Machine
> numeric tolerance).
>
> Instead you should use the `all.equal` function.
>
> Further reading: [http://floating-point-gui.de/](http://floating-point-gui.de/)
>
{: .callout}


## Help


## Naming Conventions

Object names can contain letters, numbers, underscores and periods. They
cannot start with a number nor contain spaces at all. Different people use
different conventions for long variable names, these include


~~~
this_is_snake_case
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'this_is_snake_case' not found
~~~
{: .error}



~~~
otherPeopleUseCamelCase
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'otherPeopleUseCamelCase' not found
~~~
{: .error}



~~~
some.people.use.periods
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'some.people.use.periods' not found
~~~
{: .error}



~~~
And_aFew.People_RENOUNCEconvention
~~~
{: .language-r}



~~~
Error in eval(expr, envir, enclos): object 'And_aFew.People_RENOUNCEconvention' not found
~~~
{: .error}
HadleyWickham recommends <b>snake_case</b>.  However, what you use is up 
to you, but **be consistent**.


## Variables and assignment

We can store values in variables using the assignment operator `<-`, like this:


~~~
x <- 1/40
~~~
{: .language-r}

Notice that assignment does not print a value. Instead, we stored it for later
in something called a **variable**. `x` now contains the **value** `0.025`:


~~~
x
~~~
{: .language-r}



~~~
[1] 0.025
~~~
{: .output}

More precisely, the stored value is a *decimal approximation* of
this fraction called a [floating point number](http://en.wikipedia.org/wiki/Floating_point).

Look for the `Environment` tab in one of the panes of RStudio, and you will see that `x` and its value
have appeared. Our variable `x` can be used in place of a number in any calculation that expects a number:


~~~
log(x)
~~~
{: .language-r}



~~~
[1] -3.688879
~~~
{: .output}

Notice also that variables can be reassigned:


~~~
x <- 100
~~~
{: .language-r}

`x` used to contain the value 0.025 and and now it has the value 100.

Assignment values can contain the variable being assigned to:


~~~
x <- x + 1 #notice how RStudio updates its description of x on the top right tab
y <- x * 2
~~~
{: .language-r}

The right hand side of the assignment can be any valid R expression.
The right hand side is *fully evaluated* before the assignment occurs.


It is also possible to use the `=` operator for assignment:


~~~
x = 1/40
~~~
{: .language-r}

But this is much less common among R users.  The most important thing is to
**be consistent** with the operator you use. There are occasionally places
where it is less confusing to use `<-` than `=`, and it is the most common
symbol used in the community. So the recommendation is to use `<-`.

> ## Challenge 1
>
> Which of the following are valid R variable names?
> 
> ~~~
> min_height
> max.height
> _age
> .mass
> MaxLength
> min-length
> 2widths
> celsius2kelvin
> ~~~
> {: .language-r}
>
> > ## Solution to challenge 1
> >
> > The following can be used as R variables:
> > 
> > ~~~
> > min_height
> > max.height
> > MaxLength
> > celsius2kelvin
> > ~~~
> > {: .language-r}
> >
> > The following creates a hidden variable:
> > 
> > ~~~
> > .mass
> > ~~~
> > {: .language-r}
> >
> > The following will not be able to be used to create a variable
> > 
> > ~~~
> > _age
> > min-length
> > 2widths
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

## Vectorization

One final thing to be aware of is that R is *vectorized*, meaning that
variables and functions can have vectors as values. In contrast to physics and
mathematics, a vector in R describes a set of values in a certain order of the 
same data type. For example


~~~
1:5
~~~
{: .language-r}



~~~
[1] 1 2 3 4 5
~~~
{: .output}



~~~
2^(1:5)
~~~
{: .language-r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}



~~~
x <- 1:5
2^x
~~~
{: .language-r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}

This is incredibly powerful; we will discuss this further in an
upcoming lesson.


## Managing your environment

There are a few useful commands you can use to interact with the R session.

`ls` will list all of the variables and functions stored in the global environment
(your working R session):


~~~
ls()
~~~
{: .language-r}



~~~
[1] "args"          "dest_md"       "missing_pkgs"  "required_pkgs"
[5] "src_rmd"       "x"             "y"            
~~~
{: .output}

> ## Tip: hidden objects
>
> Like in the shell, `ls` will hide any variables or functions starting
> with a "." by default. To list all objects, type `ls(all.names=TRUE)`
> instead
>
{: .callout}

Note here that we didn't give any arguments to `ls`, but we still
needed to give the parentheses to tell R to call the function.

If we type `ls` by itself, R will print out the source code for that function!


~~~
ls
~~~
{: .language-r}



~~~
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern, sorted = TRUE) 
{
    if (!missing(name)) {
        pos <- tryCatch(name, error = function(e) e)
        if (inherits(pos, "error")) {
            name <- substitute(name)
            if (!is.character(name)) 
                name <- deparse(name)
            warning(gettextf("%s converted to character string", 
                sQuote(name)), domain = NA)
            pos <- name
        }
    }
    all.names <- .Internal(ls(envir, all.names, sorted))
    if (!missing(pattern)) {
        if ((ll <- length(grep("[", pattern, fixed = TRUE))) && 
            ll != length(grep("]", pattern, fixed = TRUE))) {
            if (pattern == "[") {
                pattern <- "\\["
                warning("replaced regular expression pattern '[' by  '\\\\['")
            }
            else if (length(grep("[^\\\\]\\[<-", pattern))) {
                pattern <- sub("\\[<-", "\\\\\\[<-", pattern)
                warning("replaced '[<-' by '\\\\[<-' in regular expression pattern")
            }
        }
        grep(pattern, all.names, value = TRUE)
    }
    else all.names
}
<bytecode: 0x7fd50c39ff88>
<environment: namespace:base>
~~~
{: .output}

You can use `rm` to delete objects you no longer need:


~~~
rm(x)
~~~
{: .language-r}

If you have lots of things in your environment and want to delete all of them,
you can pass the results of `ls` to the `rm` function:


~~~
rm(list = ls())
~~~
{: .language-r}

In this case we've combined the two. Like the order of operations, anything
inside the innermost parentheses is evaluated first, and so on.

In this case we've specified that the results of `ls` should be used for the
`list` argument in `rm`. When assigning values to arguments by name, you *must*
use the `=` operator!!

If instead we use `<-`, there will be unintended side effects, or you may get an error message:


~~~
rm(list <- ls())
~~~
{: .language-r}



~~~
Error in rm(list <- ls()): ... must contain names or character strings
~~~
{: .error}

> ## Tip: Warnings vs. Errors
>
> Pay attention when R does something unexpected! Errors, like above,
> are thrown when R cannot proceed with a calculation. Warnings on the
> other hand usually mean that the function has run, but it probably
> hasn't worked as expected.
>
> In both cases, the message that R prints out usually give you clues
> how to fix a problem.
>
{: .callout}


## Packages
## R Packages

It is possible to add functions to R by writing a package, or by
obtaining a package written by someone else. As of this writing, there
are over 10,000 packages available on CRAN (the comprehensive R archive
network). R and RStudio have functionality for managing packages:

* You can see what packages are installed by typing
  `installed.packages()`
* You can install packages by typing `install.packages("packagename")`,
  where `packagename` is the package name, in quotes.
* You can update installed packages by typing `update.packages()`
* You can remove a package with `remove.packages("packagename")`
* You can make a package available for use with `library(packagename)`

> ## Challenge 2
>
> What will be the value of each  variable  after each
> statement in the following program?
>
> 
> ~~~
> mass <- 47.5
> age <- 122
> mass <- mass * 2.3
> age <- age - 20
> ~~~
> {: .language-r}
>
> > ## Solution to challenge 2
> >
> > 
> > ~~~
> > mass <- 47.5
> > ~~~
> > {: .language-r}
> > This will give a value of 47.5 for the variable mass
> >
> > 
> > ~~~
> > age <- 122
> > ~~~
> > {: .language-r}
> > This will give a value of 122 for the variable age
> >
> > 
> > ~~~
> > mass <- mass * 2.3
> > ~~~
> > {: .language-r}
> > This will multiply the existing value of 47.5 by 2.3 to give a new value of
> > 109.25 to the variable mass.
> >
> > 
> > ~~~
> > age <- age - 20
> > ~~~
> > {: .language-r}
> > This will subtract 20 from the existing value of 122 to give a new value
> > of 102 to the variable age.
> {: .solution}
{: .challenge}


> ## Challenge 3
>
> Run the code from the previous challenge, and write a command to
> compare mass to age. Is mass larger than age?
>
> > ## Solution to challenge 3
> >
> > One way of answering this question in R is to use the `>` to set up the following:
> > 
> > ~~~
> > mass > age
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] TRUE
> > ~~~
> > {: .output}
> > This should yield a boolean value of TRUE since 109.25 is greater than 102.
> {: .solution}
{: .challenge}


> ## Challenge 4
>
> Clean up your working environment by deleting the mass and age
> variables.
>
> > ## Solution to challenge 4
> >
> > We can use the `rm` command to accomplish this task
> > 
> > ~~~
> > rm(age, mass)
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}


## Commenting

Comments are 'notes' that are added to your script to provide further details, 
but do not get processed when you run the code.  To add comments to you code,
just type a "#" before your note text.


~~~
# this is a comment line
~~~
{: .language-r}



