# (PART\*) R Programming {.unnumbered}

# Introduction to R and RStudio




-   R is the name of the programming language we will learn on this course.

-   RStudio is a convenient interface which we will be using throughout the course in order to learn how to organise data, produce accurate data analyses & data visualisations.

R is a programming language that you will write code in, and RStudio is an Integrated Development Environment (IDE) which makes working with R easier. Think of it as knowing English and using a plain text editor like NotePad to write a book versus using a word processor like Microsoft Word. You could do it, but it wouldn't look as good and it would be much harder without things like spell-checking and formatting. In a similar way, you can use R without R Studio but we wouldn't recommend it. The key thing to remember is that although you will do all of your work using RStudio for this course, you are actually using **two** pieces of software which means that from time-to-time, both of them may have separate updates.

R and RStudio can be downloaded for free onto your [personal computers](https://www.rstudio.com/products/rstudio/)(see Appendices), but for convenience we will use a classroom space on **RStudio Cloud**.

[RStudio Cloud](https://rstudio.cloud/) is a cloud-based service where we can log into remotely hosted servers that host our data analysis projects.

The advantage of using RStudio Cloud is that all the extra packages and functions you need for this course will already be installed. You can log-in to your workspace from any computer as long as you have an internet connection and remember you username and password. I can also "visit" your projects and help out when you get stuck, if they are hosted on RStudio Cloud.

Eventually we will may also add extra tools like GitHub and RMarkdown for data reproducibility, literate and collaborative programming.

By the end of this course I hope you will have the tools to confidently analyze real data, make informative and beautiful data visuals, and be able to analyze lots of different types of data.

## Using RStudio Cloud

All of our sessions will run on cloud-based software. All you have to do is make a free account, and join our Workspace.

Once you are signed up - you will see that there are two spaces:

-   Your workspace - for personal use (20hrs/month)

-   Our shared classroom - educational licence (no limit)

Make sure you are working in the classroom workspace - so that I can distribute project work and 'visit' your projects if needed.

RStudio Cloud works in exactly the same way as RStudio, but means you don't have to download any software. You can access the hosted cloud server and your projects through any browser connection (Chrome works best), from any computer.

Here is a good reference guide to [RStudio Cloud](https://rstudio.cloud/learn/guide#projects)

## Getting to know RStudio

R Studio has a console that you can try out code in (appearing as the bottom left window), there is a script editor (top left), a window showing functions and objects you have created in the "Environment" tab (top right window in the figure), and a window that shows plots, files packages, and help documentation (bottom right).

<div class="figure" style="text-align: center">
<img src="images/rstudio.png" alt="RStudio interface" width="100%" />
<p class="caption">(\#fig:img-rstudio)RStudio interface</p>
</div>

You will learn more about how to use the features included in R Studio throughout this course, however, I highly recommend watching [RStudio Essentials 1](https://rstudio.com/resources/webinars/programming-part-1-writing-code-in-rstudio/) at some point. 

The video lasts \~30 minutes and gives a tour of the main parts of R Studio.

### Consoles vs. scripts

* The *script* window is the place to enter and run code so that it is easily edited and saved for future use. Usually the Script Window is shown at the top left in RStudio. If this window is not shown, it will be visible *if* you open a previously saved R script, *or* if you create a new R Script. You create new R Script by clicking on File > New File > R Script in the RStudio menu bar.

* To execute your code in the R script, you can either highlight the code and click on Run, or you can highlight the code and press CTRL + Enter on your keyboard.

* The *console*: you can enter code directly in the Console Window and click Enter. The commands that you run will be shown in the History Window on the top right of RStudio. Though it is much more difficult to keep track of your work this way.

### Environment

The Environment tab (top right) allows you to see what objects are in the workspace. If you create variables or data frames, you have a visual listing of everything in the current workspace. When you start a new project this should be completely empty.

### Plots, files, packages, help

1. Plots - The Plots panel, shows all your plots. There are buttons for opening the plot in a separate window and exporting the plot as a pdf or jpeg (though you can also do this with code.)

2. Files - The files panel gives you access to the file directory on your hard drive. 

3. Packages - Shows a list of all the R packages installed on your harddrive and indicates whether or not they are currently loaded. Packages that are loaded in the current session are checked while those that are installed but not yet loaded are unchecked. We will discuss packages more later.

4. Help - Help menu for R functions. You can either type the name of a function in the search window, or use the code to search for a function with the name


<div class="figure" style="text-align: center">
<img src="images/RStudio_Screenshot_Labels.png" alt="RStudio interface labelled" width="100%" />
<p class="caption">(\#fig:labelled)RStudio interface labelled</p>
</div>

### Make RStudio your own

You can [personalise the RStudio GUI](https://support.rstudio.com/hc/en-us/articles/115011846747-Using-Themes-in-the-RStudio-IDE) as much as you like. 

<img src="images/dark_mode.png" width="50%" style="display: block; margin: auto;" /><img src="images/classic_mode.png" width="50%" style="display: block; margin: auto;" />


## Get Help!

There are a lot of sources of information about using R out there. Here are a few helpful places to get help when you have an issue, or just to learn more

-   The R help system itself - type `help()` and put the name of the package or function you are querying inside the brackets

-   Vignettes - type `browseVignettes()` into the console and hit Enter, a list of available vignettes for all the packages we have will be displayed

-   Cheat Sheets - available at [RStudio.com.](https://www.rstudio.com/resources/cheatsheets/) Most common packages have an associate cheat sheet covering the basics of how to use them. Download/bookmark ones we will use commonly such as ggplot2, data transformation with dplyr, Data tidying with tidyr & Data import.

-   Google - I use Google constantly, because I continually forget how to do even basic tasks. If I want to remind myself how to round a number, I might type something like R round number - if I am using a particular package I should include that in the search term as well

-   Ask for help - If you are stuck, getting an error message, can't think what to do next, then ask someone. It could be me, it could be a classmate. When you do this it is very important that you show the code, include the error message. "This doesn't work" is not helpful. "Here is my code, this is the data I am using, I want it to do X, and here's the problem I get."

<div class="info">
<p>It may be daunting to send your code to someone for help.</p>
<p>It is natural and common to feel apprehensive, or to think that your code is really bad. I still feel the same! But we learn when we share our mistakes, and eventually you will find it funny when you look back on your early mistakes, or laugh about the mistakes you still occasionally make!</p>
</div>

## Get Started

Go to RStudio Cloud and enter the Project labelled `Day One` - this will clone the project and provide you with your own project workspace.

Follow the instructions below to get used to the R command line, and how R works as a language.

## Your first R command

In the RStudio pane, navigate to the **console** (bottom left) and `type or copy` the below it should appear at the \>

Hit Enter on your keyboard.


```r
10 + 20
```

-   What answer did you get?


<div class='webex-solution'><button>Solution</button>



```r
30
```


</div>


The first line shows the request you made to R, the next line is R's response

You didn't type the `>` symbol: that's just the R command prompt and isn't part of the actual command.

It's important to understand how the output is formatted. Obviously, the correct answer to the sum `10 + 20` is `30`, and not surprisingly R has printed that out as part of its response. But it's also printed out this `[1]` part, which probably doesn't make a lot of sense to you right now. You're going to see that a lot. You can think of `[1] 30` as if R were saying "the answer to the 1st question you asked is 30".

### Operators

There are two types of operators to consider

#### Arithmetic Operators

|Operator|Description
|-----|-----|
|+|	addition|
|-|	subtraction|
|*|	multiplication|
|/|	division|
|^|	exponentiation|

#### Logical Operators

|Operator|Description
|-----|-----|
|<|less than|
|<=|less than or equal to|
|>|	greater than|
|>=|greater than or equal to|
|==|exactly equal to|
|!=|not equal to|

### Typos

<div class="warning">
<p>Before we go on to talk about other types of calculations that we can do with R, there's a few other things I want to point out. The first thing is that, while R is good software, it's still software. It's pretty stupid, and because it's stupid it can't handle typos. It takes it on faith that you meant to type exactly what you did type.</p>
</div>

Suppose you forget to hit the shift key when trying to type `+`, and as a result your command ended up being `10 = 20` rather than `10 + 20`. Try it for yourself and replicate this error message:


```r
10 = 20
```


<div class='webex-solution'><button>What answer did you get?</button>

Error in 10 = 20 : invalid (do_set) left-hand side to assignment


</div>


What's happened here is that R has attempted to interpret `10 = 20` as a command, and spits out an error message because the command doesn't make any sense to it.

When a *human* looks at this, and then looks down at his or her keyboard and sees that `+` and `=` are on the same key, it's pretty obvious that the command was a typo. But R doesn't know this, so it gets upset.

Even more subtle is the fact that some typos won't produce errors at all, because they happen to correspond to "well-formed" R commands. For instance, suppose that not only did I forget to hit the shift key when trying to type `10 + 20`, I also managed to press the key next to one I meant do. The resulting typo would produce the command `10 - 20`. Clearly, R has no way of knowing that you meant to *add* 20 to 10, not *subtract* 20 from 10, so what happens this time is this:


```r
10 - 20
```

```
## [1] -10
```

In this case, R produces the right answer, but to the the wrong question.

### More simple arithmetic

One of the best ways to get to know R is to play with it, it's pretty difficult to break it so don't worry too much. Type whatever you want into to the console and see what happens.

If the last line of your console looks like this

    > 10+
    + 

and there's a **blinking cursor** next to the plus sign. This means is that R is still waiting for you to finish. It "thinks" you're still typing your command, so it hasn't tried to execute it yet. In other words, this plus sign is actually another command prompt. It's different from the usual one (i.e., the `>` symbol) to remind you that R is going to "add" whatever you type now to what you typed last time. For example, type `20` and hit enter, then it finishes the command:

    > 10 +
    + 20
    [1] 30

*Alternatively* hit the escape key, and R will forget what you were trying to do and return to a blank line.

### Try some simple maths


```r
1+7
```


```r
13-10
```


```r
4*6
```


```r
12/3
```

Raise a number to the power of another


```r
5^4
```

As I'm sure everyone will probably remember the moment they read this, the act of multiplying a number $x$ by itself $n$ times is called "raising $x$ to the $n$-th power". Mathematically, this is written as $x^n$. Some values of $n$ have special names: in particular $x^2$ is called $x$-squared, and $x^3$ is called $x$-cubed. So, the 4th power of 5 is calculated like this: 

$$5^4 = 5 \times 5 \times 5 \times 5 $$

### Perform some combos

Perform some mathematical combos, noting that the order in which R performs calculations is the standard one.

That is, first calculate things inside **B**rackets `()`, then calculate **O**rders of (exponents) `^`, then **D**ivision `/` and **M**ultiplication `*`, then **A**ddition `+` and **S**ubtraction `-`.

Notice the different outputs of these two commands.


```r
3^2-5/2
```


```r
(3^2-5)/2
```

Similarly if we want to raise a number to a fraction, we need to surround the fraction with parentheses `()`


```r
16^1/2
```


```r
16^(1/2)
```

The first one calculates 16 raised to the power of 1, then divided this answer by two. The second one raises 16 to the power of a half. A big difference in the output.

<div class="info">
<p>While the cursor is in the console, you can press the up arrow to see all your previous commands.</p>
<p>You can run them again, or edit them. Later on we will look at scripts, as an essential way to re-use, store and edit commands.</p>
</div>

## "TRUE or FALSE" data

Time to make a sidebar onto another kind of data. Many concepts in programming rely on the idea of a ***logical value***. A logical value is an assertion about whether something is true or false. This is implemented in R in a pretty straightforward way. There are two logical values, namely `TRUE` and `FALSE`. Despite the simplicity, logical values are very useful things. Let's see how they work.

### Assessing mathematical truths

In George Orwell's classic book *1984*, one of the slogans used by the totalitarian Party was "two plus two equals five", the idea being that the political domination of human freedom becomes complete when it is possible to subvert even the most basic of truths.

But they didn't have R!

R will not be subverted. It has rather firm opinions on the topic of what is and isn't true, at least as regards basic mathematics. If I ask it to calculate `2 + 2`, it always gives the same answer, and it's **not** 5:


```r
2 + 2
```

```
## [1] 4
```

Of course, so far R is just doing the calculations. I haven't asked it to explicitly assert that $2+2 = 4$ is a true statement. If I want R to make an explicit judgement, I can use a command like this:


```r
2 + 2 == 4
```


<div class='webex-solution'><button>Solution</button>

TRUE


</div>


What I've done here is use the ***equality operator***, `==`, to force R to make a "true or false" judgement.

<div class="info">
<p>This is a very different operator to the assignment operator <code>=</code> you saw previously.</p>
<p>A common typo that people make when trying to write logical commands in R (or other languages, since the "<code>=</code> versus <code>==</code>" distinction is important in most programming languages) is to accidentally type <code>=</code> when you really mean <code>==</code>.</p>
</div>

Okay, let's see what R thinks of the Party slogan:


```r
2+2 == 5
```

```
## [1] FALSE
```

Take that Big Brother! Anyway, it's worth having a look at what happens if I try to *force* R to believe that two plus two is five by making an assignment statement like `2 + 2 = 5` or `2 + 2 <- 5`. When I do this, here's what happens:


```r
2 + 2 = 5
```

    Error in 2 + 2 = 5 : target of assignment expands to non-language object

R doesn't like this very much. It recognises that `2 + 2` is *not* a variable (that's what the "non-language object" part is saying), and it won't let you try to "reassign" it. While R is pretty flexible, and actually does let you do some quite remarkable things to redefine parts of R itself, there are just some basic, primitive truths that it refuses to give up. It won't change the laws of addition, and it won't change the definition of the number `2`.

That's probably for the best.

## Storing outputs

With simple questions like the ones above we are happy to just see the answer, but our questions are often more complex than this. If we need to take multiple steps, we benefit from being able to store our answers and recall them for use in later steps. This is very simple to do we can *assign* outputs to a name:


```r
a <- 1+2
```

This literally means please *assign* the value of `1+2` to the name `a`. We use the **assignment operator** `<-` to make this assignment.

<div class="info">
<p>Note the shortcut key for &lt;- is Alt + - (Windows) or Option + - (Mac)</p>
</div>

If you perform this action you should be able to do two things

-   You should be able to see that in the top right-hand pane in the **Environment** tab their is now an **object** called `a` with the value of `3`.

<div class="figure" style="text-align: center">
<img src="images/environment.png" alt="object a is now visible withe a value of 3 in the Environment Pane" width="100%" />
<p class="caption">(\#fig:img-environment)object a is now visible withe a value of 3 in the Environment Pane</p>
</div>

-   You should be able to look at what a is by typing it into your Console and pressing Enter

-   Note that you will not see the outcome of your functions *until* you type the object into the R console and hit Enter


```r
a
```


<div class='webex-solution'><button>What output do you get when you type a into your console?</button>


```r
3
```


</div>


You can now call this object at *any time* during your R session and perform calculations with it.


```r
2 * a
```


<div class='webex-solution'><button>Solution</button>


```r
6
```


</div>



What happens if we assign a value to a named object that **already** exists in our R environment??? for example


```r
a <- 10
a
```

The value of `a` is now 10.

You should see that the previous assignment is lost, *gone forever* and has been replaced by the new value.

We can assign lots of things to objects, and use them in calculations to build more objects.


```r
b <- 5
c <- a + b
```

<div class="warning">
<p>Remember: If you now change the value of b, the value of c does <em>not</em> change.</p>
<p>Objects are totally <strong>independent</strong> from each other once they are made.</p>
<p>Overwriting objects with new values means the old value is lost.</p>
</div>


```r
b <- 7
b
c
```

-   What is the value of `c`?


<div class='webex-solution'><button>What is the value of c ?</button>

[1] 15

When `c` was created it was a product of `a` and `b` having values of 10 and 15 respectively. 
If we re-ran the command `c <- a + b` *after* changing the value of `b` **then** we would get a value of 17. 


</div>


Look at the environment tab again - you should see it's starting to fill up now!

<div class="info">
<p>RStudio will by default save the objects in its memory when you close a session.</p>
<p>These will then be there the next time you logon. It might seem nice to be able to close things down and pick up where you left off, but its actually quite dangerous. It's messy, and can cause lots of problems when we work with scripts later, so don't do this!</p>
<p>To stop RStudio from saving objects by default go to Tools &gt; Project Options option and change "Save workspace to .RData on exit" to "No" or "Never".</p>
<p>Instead we are going to learn how to use scripts to quickly re-run analyses we have been working on.</p>
</div>

### Choosing names

-   Use informative variable names. As a general rule, using meaningful names like `orange` and `apple` is preferred over arbitrary ones like `variable1` and `variable2`. Otherwise it's very hard to remember what the contents of different variables actually are.

-   Use short variable names. Typing is a pain and no-one likes doing it. So we much prefer to use a name like `apple` over a name like `pink_lady_apple`.

-   Use one of the conventional naming styles for multi-word variable names. R only lets you use certain things as **legal** names. Legal names must start with a letter **not** a number, which can then be followed by a sequence of letters, numbers, ., or \_. R does not like using spaces. Upper and lower case names are allowed, but R is case sensitive so `Apple` and `apple` are different.

-   My favourite naming convention is `snake_case` short, lower case only, spaces between words are separated with a \_. It's easy to read and easy to remember.

<div class="figure" style="text-align: center">
<img src="images/snake_case.png" alt="snake_case" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-37)courtesy of Allison Horst</p>
</div>

## Error

Things will go wrong eventually, they always do...

R is *very* pedantic, even the smallest typo can result in failure and typos are impossilbe to avoid. So we will make mistakes. One type of mistake we will make is an **error**. The code fails to run. The most common causes for an error are:

-   typos

-   missing commas

-   missing brackets

There's nothing wrong with making *lots* of errors. The trick is not to panic or get frustrated, but to read the error message and our script carefully and start to *debug*...

... and sometimes we need to walk away and come back later!

<div class="try">
<p>Try typing the command <code>help()</code> into the R console, it should open a new tab on the bottom right.</p>
<p>Put a function or package into the brackets to get help with a specific topic</p>
</div>

<div class="figure" style="text-align: center">
<img src="images/Error.jpg" alt="R Error" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-39)courtesy of Allison Horst</p>
</div>

## Functions

Functions are the tools of R. Each one helps us to do a different task.

Take for example the function that we use to round a number to a certain number of digits - this function is called `round`

Here's an example:


```r
round(x  = 2.4326782647, digits = 2)
```

We start the command with the function name `round`. The name is followed by parentheses `()`. Within these we place the *arguments* for the function, each of which is separated by a comma.

The arguments:

-   `x =` 2.4326782647 (the number we would like to round)

-   `digits =` 2 (the number of decimal places we would like to round to)

**Arguments are the inputs we give to a function**. These arguments are in the form `name = value` the name specifies the argument, and the value is what we are providing to define the input. That is the first argument `x` is the number we would like to round, it has a value of 2.4326782647. The second argument `digits` is how we would like the number to be rounded and we specify 2. There is no limit to how many arguments a function *could* have.

<div class="try">
<p>Copy and paste the following code into the console.</p>
</div>



```r
help(round)
```

The help documentation for `round()`should appear in the bottom right help panel. In the usage section, we see that `round()`takes the following form:


```r
round(x, digits = 0)
```

In the arguments section, there are explanations for each of the arguments. `x`is the number or vector where we wish to round values. `digits` is the number of decimal places to be used. In the description we can see that if no value is supplied for `digits` it will default to 0 or whole number rounding.

Read the 'Details' section to find out what happens when rounding when the last digit is a 5.

Let's try an example and just change the required argument `digits`

<div class="try">
<p>Copy and paste the following code into the console.</p>
</div>


```r
round(x  = 2.4326782647)
```

```
## [1] 2
```

Now we can change the additional arguments to produce a different set of numbers.


```r
round(x  = 2.4326782647, digits = 2)
```

```
## [1] 2.43
```

This time R has still rounded the number, but it has done so to a set number of 'decimal places'.

Always remember to use the help documentation to help you understand what arguments a function requires.

### Storing the output of functions

What if we need the answer from a function in a later calculation. The answer is to use the assignment operator again `<-`.

In this example we assign values to two R objects that we can then call inside our R function **as though we were putting numbers in directly**.

<div class="try">
<p>Copy and paste the following code into the console.</p>
</div>


```r
number_of_digits <- 3

my_number <- 2.4326782647

rounded_number <- round(x  = my_number, 
                        digits = number_of_digits)
```

**What value is assigned to the R object `rounded_number`** **?**


<div class='webex-solution'><button>Solution</button>


[1] 2.433


</div>


### More fun with functions

Copy and paste this:


```r
round(2.4326782647, 2)
```

Looks like we don't even *have* to give the names of arguments for a function to still work. This works because the function `round` expects us to give the number value first, and the argument for rounding digits second. *But* this assumes we know the expected ordering within a function, this might be the case for functions we use a lot. If you give arguments their proper names *then* you can actually introduce them in **any order you want**.

Try this:


```r
round(digits = 2, x  = 2.4326782647)
```

But this gives a different answer


```r
round(2, 2.4326782647)
```

<div class="warning">
<p>Remember naming arguments overrides the position defaults</p>
</div>

How do we **know** the argument orders and defaults? Well we get to know how a lot of functions work through practice, but we can also use `help()` .

## Packages

When you install R you will have access to a range of functions including options for data wrangling and statistical analysis. The functions that are included in the default installation are typically referred to as **Base R** and there is a useful cheat sheet that shows many Base R functions [here](%5Bhttps://www.rstudio.com/wp-content/uploads/2016/05/base-r.pdf)

However, the power of R is that it is extendable and open source - anyone can create a new **package** that extends the functions of R.

An R package is a container for various things including functions and data. These make it easy to do very complicated protocols by using custom-built functions. Later we will see how we can write our own simple functions. Packages are a lot like new apps extending the functionality of what your phone can do.

On RStudio Cloud I have already installed several add-on packages, all we need to do is use a simple function `library()` to load these packages into our workspace. Once this is complete we will have access to all the custom functions they contain.

<div class="try">
<p>Copy and paste the following code into the console.</p>
</div>


```r
library(ggplot2)
library(palmerpenguins)
```

-   `ggplot2` - is one of the most popular packages to use in R. This "grammar of graphics" packages is dedicated to making data visualisations, and contains lots of dedicated functions for this.

-   `palmerpenguins` - is a good example of a data-heavy package, it contains no functions, but instead datasets that we can use.

<div class="warning">
<p>A common source of errors is to call a function that is part of a package but forgetting to load the package.</p>
<p>If R says something like "Error in "function-name": could not find X" then most likely the function was misspelled or the package containing the function hasn't been loaded.</p>
</div>

## My first data visualisation

Let's run our first data visualisation using the functions and data we have now loaded - this produces a plot using functions from the `ggplot2` package and data from the `palmerpenguins` package.

Data visualisation is a core part of data science, and generating insights from your data - we will spend a lot of time on this course working on our data visualisations.

Today let's use some simple functions to produce a figure. We specify the data source, the variables to be used for the x and y axis and then the type of visual object to produce, colouring them by the species.

<div class="try">
<p>Copy and paste the following code into the console.</p>
</div>


```r
ggplot(data = penguins,aes(x = bill_length_mm, y = bill_depth_mm)) + geom_point(aes(colour=species)) 
```

<img src="01-intro-to-r_files/figure-html/unnamed-chunk-55-1.png" width="100%" style="display: block; margin: auto;" />

<div class="information">
<p>You may have noticed R gave you a warning. Not the same as a big scary error, but R wants you to be aware of something.</p>
<p>In this case that two of the observations had missing data in them (either bill length or bill depth), so couldn't be plotted.</p>
<p>It is a good thing to take note of all warnings and errors - they provide useful information.</p>
</div>

The above command can also be written as below, its in a longer style with each new line for each argument in the function. This style can be easier to read, and makes it easier to write comments with `#`. Copy this longer command into your console then hit Enter.

Note that R ignores anything that comes after `#` on a line of code - this means we can add notes to our work.


```r
ggplot(data = penguins, # calls ggplot function, data is penguins
       aes(x = bill_length_mm, # sets x axis as bill length
           y = bill_depth_mm)) + # sets y axis value as bill depth
    geom_point(aes(colour=species)) # plot points coloured by penguin species
```

## Writing scripts

Until now we have been typing words directly into the Console. This is fine for short/simple calculations - but as soon as we have a more complex, multi-step process this becomes time consuming, error-prone and *boring*. **Scripts** are a document containing all of your commands (in the order you want them to run), they are *repeatable, shareable, annotated records of what you have done*. In short they are incredibly useful - and a big step towards **open** and **reproducible** research.


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Create a script by going to File \> New File \> R Script. </div></div>


<div class="figure" style="text-align: center">
<img src="images/rstudio.png" alt="RStudio interface - top left script, botto  left console" width="100%" />
<p class="caption">(\#fig:script)RStudio interface - top left script, botto  left console</p>
</div>

This will open a pane in the top-left of RStudio with a tab name of `Untitled1`.

<div class="info">
<p>A script is a way of organising all your R commands, in a sequence, to produce a desired output.</p>
<p>When you write a script, nothing happens until you tell it to RUN, then you will see your commands appearing in the console.</p>
<p>Make sure you include all of the commands you need to complete your analysis, in the correct order.</p>
</div>

### Organising scripts

Scripts work best when they are well organised - and well documented. Simple tricks and consistent organisation can make your work easier to read and be reproduced by others.

You should bookmark the [Tidyverse Style Guide](https://style.tidyverse.org/files.html), it is an opinionated way of organising your scripts and code so that it has a consistent style, that maximises readability. Later in the course we will use this as a benchmark for assessing your code writing.

Annotating your instructions provides yourself and others insights into why you are doing what you are doing. This is a vital aspect of a robust and reproducible workflow. And when you come back to a script, one week, one month or one year from now you will often wonder what a command was for. It is very, very useful to make notes for yourself, and its useful in case anyone else will ever read your script. Make these comments helpful as they are for humans to read.

We have already seen how to signal a comment with the `#` key. Everything in the line after a `#` is ignored by R and won't be treated as a command. You should also see that it is marked in a different colour in your script.

<div class="try">
<p>Put the following comment in your script on line 1.</p>
</div>


```r
# I really love R
```

We can also use `#` to produce Headers of different levels, if we follow these with commented lines of `-` or `=` as shown in the figure below.

<div class="figure" style="text-align: center">
<img src="images/organised script.png" alt="R script document outline. Push the button with five horizontal lines to reveal how R recognises headers and subheaders" width="100%" />
<p class="caption">(\#fig:script outline)R script document outline. Push the button with five horizontal lines to reveal how R recognises headers and subheaders</p>
</div>

### Loading packages

To use the functions from a package in our script they must be loaded *before* we call on the functions or data they contain. So the most sensible place to put library calls for packages is at the very **top** of our script. So let's do that now,

<div class="try">
<p>Add the commands<code>library(ggplot2)</code> and <code>library(palmerpenguins)</code> to your script.</p>
<p>Think about how you would organise you script using the image above as a guide</p>
<p>Put a comment next to each package explaining what it is for "Hint use the help() function".</p>
<p>Use the document outline button to help organise your script.</p>
</div>


<div class='webex-solution'><button>Solution</button>



```r
# I really love R
# _______________----

# 📦 PACKAGES ----

library(ggplot2) # create elegant data visualisations
library(palmer penguins) # Palmer Archipelago Penguin Data

# ______________----
```


<div class="info">
<p>R Studio will interpret Unicode to present images that you can include in your scripts. It's not necessary, but a fun way to help organise your scripts.</p>
</div>

</div>


### Adding more code

<div class="try">
<p>Add the below code into your script, underneath the sections you already have</p>
</div>

It is very similar to the code you ran earlier, but is preceded by `plot_1 <-`


```r
# DATA VISUAL ----

plot_1 <- ggplot(data = penguins, # calls ggplot function, data is penguins
           aes(x = bill_length_mm, # sets x axis as bill length
               y = bill_depth_mm)) + # sets y axis value as bill depth
          geom_point(aes(colour=species)) # geometric to plot

# ______________----
```


### Running your script

To run the commands from your script, we need to get it *into* the Console. You could select and copy/paste this into the Console. But there are a couple of faster shortcuts.

-   Hit the Run button in the top right of the script pane. Pressing this will run the line of code the cursor is sitting on.

-   Pressing Ctrl+Enter will do the same thing as hitting the Run button

-   If you want to run the whole script in one go then press Ctrl+A then either click Run or press Ctrl+Enter

Try it now.

You should notice that unlike when making previous data visuals, you **do not** immediately see your graph, this is because you assigned the output of your functions to an **R object**, instead of the default action where R would print the output. Check the "Environment" tab - you should be able to see `plot_1` there.

-   To see the new plot you have made you should type `plot_1` into the R console. Or add it underneath the script and run it again!

### Making an output

For our next trick we will make a script that outputs a file. Underneath the lines of code to generate the figure we will add a new function `ggsave()`. Then **re-run your script**. To find out more about this function (and the arguments it contains), type `help(ggsave)` into the console.



```r
# OUTPUT TO FILE ----

ggsave(filename = "2022_10_01_5023Y_workshop_1_penguin_scatterplot.png", 
       plot = plot_1, 
       dpi = 300, 
       width = 6, 
       height = 6)
# _________________----
```


Check the Files tab on RStudio Cloud, there should now be a new file in your workspace called "2022_10_01_5023Y_workshop_1\_penguin_scatterplot.png".

Wow that is a mouthful! Why have we made such a long filename? Well it contains information that should help you know what it is for the future.

-   Date

-   Module code

-   Short description of the file contents

<div class="warning">
<p>It is very important to have naming conventions for all files.</p>
<p>Everything after the <code>.</code> is file extension information informing the computer how to process the contents of the file. <code>.png</code> stands for "Portable Graphics Format”, and it means the data is an uncompressed image format.</p>
<p>Everything before the <code>.</code> is for humans, it is a good idea to make sure these have a naming convention.</p>
<p>Avoid periods, spaces or slashes, instead use YYYYMMDD and underscores</p>
<p>e.g. YYYYMMDD_short_image_description.fileextension</p>
</div>

### Saving your script

Our script now contains code and comments from our first workshop. We need to save it.

Alongside our data, our script is the most precious part of our analysis. We don't need to save anything else, any outputs etc. because our script can always be used to generate everything again. Note the colour of the script - the name changes colour when we have unsaved changes. Press the Save button or go to File \> Save as. Give the File a sensible name like "YYYYMMDD_5023Y_workshop_1\_simple_commands" and in the bottom right pane under `Files` you should now be able to see your saved script, it should be saved with a `.R` file extension indicating this is an R Script.

You could now safely quit R, and when you log on next time to this project, your script will be waiting for you.



<div class='webex-solution'><button>Check your script</button>



```r
# I really love R
# _______________----

# 📦 PACKAGES ----

library(ggplot2) # create elegant data visualisations
library(palmer penguins) # Palmer Archipelago Penguin Data

# ________________----
# DATA VISUAL ----

plot_1 <- ggplot(data = penguins, # calls ggplot function, data is penguins
           aes(x = bill_length_mm, # sets x axis as bill length
               y = bill_depth_mm)) + # sets y axis value as bill depth
          geom_point(aes(colour=species)) # geometric to plot

# ______________----

# OUTPUT TO FILE ----

ggsave(filename = "2022_10_01_5023Y_workshop_1_penguin_scatterplot.png", 
       plot = plot_1, 
       dpi = 300, 
       width = 6, 
       height = 6)
# _________________----
```


</div>



## Quitting

-   Make sure you have saved any changes to your R script - that's all you need to make sure you've done!

-   If you want me to take a look at your script let me know

-   If you spotted any mistakes or errors let me know

-   Close your RStudio Cloud Browser

-   Complete this week's short quiz!

## Activity 1

### Complete this Quiz

When you get the correct answer, the answer box will turn green. Sometimes this doesn't work on Internet Explorer or Edge so be sure to use Chrome or Firefox.

**Question 1.**  What is the output from 5\^4

<input class='webex-solveme nospaces' size='3' data-answer='["625"]'/>



**Question 2.**  What answer will you get when you type `2+2 = 4` into the R console?

<select class='webex-select'><option value='blank'></option><option value=''>TRUE</option><option value=''>FALSE</option><option value='answer'>Error</option></select>


<div class='webex-solution'><button>Solution</button>


If we wanted R to make a judgement we must use == not = otherwise we will get an Error message


</div>


**Question 3.**  What symbol do I use if I want to **assign** a value or output of a function to an R object

<input class='webex-solveme nospaces' size='2' data-answer='["<-"]'/>

**Question 4.**  What is the value of `a` if I ran the following commands?


```r
a <-  12*2

a <- 5
```

<input class='webex-solveme nospaces' size='1' data-answer='["5"]'/>

**Question 5.**  Which of these variable naming conventions is **not** written correctly?

<select class='webex-select'><option value='blank'></option><option value=''>snake_case</option><option value=''>camelCase</option><option value='answer'>Screaming_Snake_Case</option><option value=''>kebab-case</option></select>

**Question 6.**  What should I type into the R console if I want `help` with the `round()` function?

<input class='webex-solveme nospaces' size='11' data-answer='["help(round)"]'/>

**Question 7.**  Which of these statements about function arguments **is not true**

<select class='webex-select'><option value='blank'></option><option value=''>Arguments are the inputs we give to a function</option><option value='answer'>Values for R arguments must always be defined by the user</option><option value=''>Naming arguments supersedes position in a function</option><option value=''>There is no limit to the number of arguments a function could have</option></select>

**Question 8.**  Evaluate this statement "An R Package can contain code functions, data, or both."

<select class='webex-select'><option value='blank'></option><option value='answer'>TRUE</option><option value=''>FALSE</option></select>
