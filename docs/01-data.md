

# Introduction to R







* R is the name of the programming language we will learn on this course. 

* RStudio is a convenient interface which we will be using throughout the course in order to learn how to organise data, produce accurate data analyses & data visualisations. 

* RStudio Cloud is a pay-to-use cloud software that means we can access R, RStudio and our projects through any browser with a username login. R and RStudio can be downloaded for free onto your personal computers, but for convenience we will use a classroom space on RStudio Cloud. 

Eventually we will also add extra tools like GitHub and RMarkdown for data reproducibility and collaborative programming, check out this short (and very cheesy) intro video.], which are collaboration and version control systems that we will be using throughout the course. More on this in future weeks.

By the end of this module I hope you will have the tools to confidently analyze real data, make informative and beautiful data visuals, and be able to analyse lots of different types of data.

## Getting around on RStudio

**VIDEO AND EXPLAINER**

## Using RStudio Cloud

All of our sessions will run on cloud-based software. All you have to do is make a free account, and join our Workspace BIO-5023Y the sharing link is here.

Once you are signed up - you will see that there are two spaces:

* Your workspace

* BIO-5023Y

Make sure you are working in the class workspace - there is a limit to the hours/month on your workspace, so all assigments and project work should take place in the BIO-5023Y space.

RStudio Cloud works in exactly the same way as RStudio, but means you don’t have to download any software. You can access the hosted cloud server and your projects through any browser connection (Chrome works best), from any computer.

Watch these short explainer videos to get used to navigating the environment.

**Video and explainer**

### Make RStudio your own

**PERSONALISE AND CUSTOMISE**

## Get Help!

There are a lot of sources of information about using R out there. Here are a few helpful places to get help when you have an issue, or just to learn more

* The R help system itself - type `help()` and put the name of the package or function you are querying inside the brackets

* Vignettes - type browseVignettes() into the console and hit Enter, a list of available vignettes for all the packages we have will be displayed

* Cheat Sheets - available at RStudio.com. Most common packages have an associate cheat sheet covering the basics of how to use them. Download/bookmark ones we will use commonly such as ggplot2, Data transformation with dplyr, Data tidying with tidyr & Data import.

* Google - I use Google constantly, because I continually forget how to do even basic tasks. If I want to remind myself how to round a number, I might type something like R round number - if I am using a particular package I should include that in the search term as well

* Ask for help - If you are stuck, getting an error message, can’t think what to do next, then ask someone. It could be me, it could be a classmate. When you do this it is very important that you show the code, include the error message. “This doesn’t work” is not helpful. “Here is my code, this is the data I am using, I want it to do X, and here’s the problem I get.”

<div class="info">
<p>It may be daunting to send your code to someone for help.</p>
<p>It is natural and common to feel apprehensive, or to think that your code is really bad. I still feel the same! But we learn when we share our mistakes, and eventually you will find it funny when you look back on your early mistakes, or laugh about the mistakes you still occasionally make!</p>
</div>

## Get Started

Go to RStudio Cloud and enter the Project labelled `Week One` - this will clone the project and provide you with your own workspace.

Follow the instructions below to get used to the R command line, and how R works as a language. 


## Your first R command

In the RStudio pane, navigate to the console (bottom left) and `type or copy` the below it should appear at the >

Hit Enter on your keyboard.


```r
10 + 20
```

* What answer did you get? 

<button id="displayTextunnamed-chunk-4" onclick="javascript:toggle('unnamed-chunk-4');">Show Solution</button>

<div id="toggleTextunnamed-chunk-4" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
30
```
</div></div></div>


The first line shows the request you made to R, the next line is R's response

You didn't type the `>` symbol: that's just the R command prompt and isn't part of the actual command. 

It's important to understand how the output is formatted. Obviously, the correct answer to the sum `10 + 20` is `30`, and not surprisingly R has printed that out as part of its response. But it's also printed out this `[1]` part, which probably doesn't make a lot of sense to you right now. You're going to see that a lot. You can think of `[1] 30` as if R were saying "the answer to the 1st question you asked is 30".


### Typos

Before we go on to talk about other types of calculations that we can do with R, there's a few other things I want to point out. The first thing is that, while R is good software, it's still software. It's pretty stupid, and because it's stupid it can't handle typos. It takes it on faith that you meant to type *exactly* what you did type. For example, suppose that you forgot to hit the shift key when trying to type `+`, and as a result your command ended up being `10 = 20` rather than `10 + 20`. Try it for yourself and replicate this error message:


```r
10 = 20
```

* What answer did you get?

<button id="displayTextunnamed-chunk-6" onclick="javascript:toggle('unnamed-chunk-6');">Show Solution</button>

<div id="toggleTextunnamed-chunk-6" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

Error in 10 = 20 : invalid (do_set) left-hand side to assignment
</div></div></div>


What's happened here is that R has attempted to interpret `10 = 20` as a command, and spits out an error message because the command doesn't make any sense to it. When a *human* looks at this, and then looks down at his or her keyboard and sees that `+` and `=` are on the same key, it's pretty obvious that the command was a typo. But R doesn't know this, so it gets upset. And, if you look at it from its perspective, this makes sense. All that R "knows" is that `10` is a legitimate number, `20` is a legitimate number, and `=` is a legitimate part of the language too. In other words, from its perspective this really does look like the user meant to type `10 = 20`, since all the individual parts of that statement are legitimate and it's too stupid to realise that this is probably a typo. Therefore, R takes it on faith that this is exactly what you meant... it only "discovers" that the command is nonsense when it tries to follow your instructions, typo and all. And then it whinges, and spits out an error.

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

```
> 10+
+ 
```

and there's a **blinking cursor** next to the plus sign. This means is that R is still waiting for you to finish. It "thinks" you're still typing your command, so it hasn't tried to execute it yet. In other words, this plus sign is actually another command prompt. It's different from the usual one (i.e., the `>` symbol) to remind you that R is going to "add" whatever you type now to what you typed last time. For example, type `20` and hit enter, then it finishes the command:

```
> 10 +
+ 20
[1] 30
```

*Alternatively* hit escape, and R will forget what you were trying to do and return to a blank line. 


### Try some maths


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
$$
5^4 = 5 \times 5 \times 5 \times 5 
$$

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


Similarly if we want to raise a number to a fraction, we need to surround the fraction with parentheses ()


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

Time to make a sidebar onto another kind of data. A key concept in that a lot of R relies on is the idea of a **_logical value_**. A logical value is an assertion about whether something is true or false. This is implemented in R in a pretty straightforward way. There are two logical values, namely `TRUE` and `FALSE`. Despite the simplicity, logical values are very useful things. Let's see how they work.

### Assessing mathematical truths

In George Orwell's classic book *1984*, one of the slogans used by the totalitarian Party was "two plus two equals five", the idea being that the political domination of human freedom becomes complete when it is possible to subvert even the most basic of truths. 

But they didn't have R! R will not be subverted. It has rather firm opinions on the topic of what is and isn't true, at least as regards basic mathematics. If I ask it to calculate `2 + 2`, it always gives the same answer, and it's **not** 5:


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

<button id="displayTextunnamed-chunk-20" onclick="javascript:toggle('unnamed-chunk-20');">Show Solution</button>

<div id="toggleTextunnamed-chunk-20" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

TRUE
</div></div></div>

What I've done here is use the **_equality operator_**, `==`, to force R to make a "true or false" judgement. 

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
Take that Big Brother! Anyway, it's worth having a look at what happens if I try to *force* R to believe that two plus two is five by making an assignment statement like  `2 + 2 = 5` or `2 + 2 <- 5`. When I do this, here's what happens:

```r
2 + 2 = 5
```
```
Error in 2 + 2 = 5 : target of assignment expands to non-language object
```
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

* You should be able to see that in the top right-hand pane in the **Environment** tab their is now an **object** called `a` with the value of `3`.

* You should be able to look at what a is by typing it into your Console and pressing Enter

* Note that you will not see the outcome of your functions *until* you type the object into the R console and hit Enter


```r
a
```

What output do you get when you type `a` into your console? 

<button id="displayTextunnamed-chunk-27" onclick="javascript:toggle('unnamed-chunk-27');">Show Solution</button>

<div id="toggleTextunnamed-chunk-27" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
3
```
</div></div></div>

You can now call this object at *any time* during your R session and perform calculations with it. 


```r
2 * a
```

<button id="displayTextunnamed-chunk-29" onclick="javascript:toggle('unnamed-chunk-29');">Show Solution</button>

<div id="toggleTextunnamed-chunk-29" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
6
```
</div></div></div>

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

* What is the value of `c`? 

<button id="displayTextunnamed-chunk-34" onclick="javascript:toggle('unnamed-chunk-34');">Show Solution</button>

<div id="toggleTextunnamed-chunk-34" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

[1] 15
</div></div></div>


Look at the environment tab again  - you should see it's starting to fill up now!

<div class="info">
<p>RStudio will by default save the objects in its memory when you close a session.</p>
<p>These will then be there the next time you logon. It might seem nice to be able to close things down and pick up where you left off, but its actually quite dangerous. It's messy, and can cause lots of problems when we work with scripts later, so don't do this!</p>
<p>To stop RStudio from saving objects by default go to the Preferences option and change "Save workspace to .RData on exit" to "Never".</p>
<p>Instead we are going to learn how to use scripts to quickly re-run analyses we have been working on.</p>
</div>

### Choosing names

- Use informative variable names. As a general rule, using meaningful names like `orange` and `apple` is preferred over arbitrary ones like `variable1` and `variable2`. Otherwise it's very hard to remember what the contents of different variables actually are.

- Use short variable names. Typing is a pain and no-one likes doing it. So we much prefer to use a name like `apple` over a name like `pink_lady_apple`.

- Use one of the conventional naming styles for multi-word variable names. R only lets you use certain things as **legal** names. Legal names must start with a letter **not** a number, which can then be followed by a sequence of letters, numbers, ., or _. R does not like using spaces. Upper and lower case names are allowed, but R is case sensitive so `Apple` and `apple` are different. 

- My favourite naming convention is `snake_case` short, lower case only, spaces between words are separated with a _. It's easy to read and easy to remember. 

<div class="figure" style="text-align: center">
<img src="images/snake_case.png" alt="snake_case" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-36)courtesy of Allison Horst</p>
</div>


## Error

Things will go wrong eventually, they always do... 

R is *very* pedantic, even the smallest typo can result in failure and typos are impossilbe to avoid. So we will make mistakes. One type of mistake we will make is an **error**. The code fails to run. The most common causes for an error are:

* typos

* missing commas

* missing brackets

There's nothing wrong with making *lots* of errors. The trick is not to panic or get frustrated, but to read the error message and our script carefully and start to *debug*...

... and sometimes we need to walk away and come back later!

Try typing the command `help()` into the R console, it should open a new tab on the bottom right. 


Put a function or package into the brackets to get help with a specific topic 

<div class="figure" style="text-align: center">
<img src="images/Error.jpg" alt="R Error" width="80%" />
<p class="caption">(\#fig:unnamed-chunk-37)courtesy of Allison Horst</p>
</div>


## Functions

Functions are the tools of R. Each one helps us to do a different task.

Take for example the function that we use to round a number to a certain number of digits - this function is called `round`

Here's an example:


```r
round(x  = 2.4326782647, digits = 2)
```

We start the command with the function name `round`. The name is followed by parentheses (). Within these we place the *arguments* for the function, each of which is separated by a comma. 

The arguments

* x = 2.4326782647 (the number we would like to round)

* digits = 2 (the number of decimal places we would like to round to)

**Arguments are the inputs we give to a function**. These arguments are in the form `name = value` the name specifies the argument, and the value is what we are providing to define the input. That is the first argument x is the number we would like to round, it has a value of 2.4326782647. The second argument digits is how we would like the number to be rounded and we specify 2. There is no limit to how many arguments a function *could* have. 

### Storing the output of functions

What if we need the answer from a function in a later calculation. The answer is to use the assignment operator again `<-`. 

In this example we assign values to two R objects that we can then call inside our R function **as though we were putting numbers in directly**.


```r
number_of_digits <- 2

my_number <- 2.4326782647

rounded_number <- round(x  = my_number, 
                        digits = number_of_digits)
```


### More fun with functions

Check this out:


```r
round(2.4326782647, 2)
```

We don't *have* to give the names of arguments for a function to still work. This works because the function `round` expects us to give the number value first, and the argument for rounding digits second. *But* this assumes we know the expected ordering within a function, this might be the case for functions we use a lot. If you give arguments their proper names *then* you can actually introduce them in any order you want.

Try this:


```r
round(digits = 2, x  = 2.4326782647)
```


But this gives a different answer


```r
round(2, 2.4326782647)
```


<div class="warning">
<p>Naming arguments overrides the position defaults</p>
</div>

Ok what about this?


```r
round(2.4326782647)
```

We didn't specify how many digits to round to, but we still got an answer. That's because in many functions arguments have **defaults** - the default argument here is digits = 0. So we don't have to specify the argument *if* we are happy for round to produce whole numbers. 

How do we know argument orders and defaults? Well we get to know how a lot of functions work through practice, but we can also use the inbuilt R help. This is a function - but now we specify the name of another function to provide a help menu. 

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Use R to bring up the help menu for the function `round` </div></div>

<button id="displayTextunnamed-chunk-46" onclick="javascript:toggle('unnamed-chunk-46');">Show Solution</button>

<div id="toggleTextunnamed-chunk-46" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
help(round)
```
</div></div></div>


## Packages

An R package is a container for various things including functions and data. These make it easy to do very complicated protocols by using custom-built functions. Later we will see how we can write our own simple functions. Packages are a lot like new apps extending the functionality of what your phone can do. 

On RStudio Cloud I have already installed several add-on packages, all we need to do is use a simple function `library()` to load these packages into our workspace. Once this is complete we will have access to all the custom functions they contain. 

Let's try that now: 


```r
library(ggplot2)
library(palmerpenguins)
```

* `ggplot2` - is one of the most popular packages to use in R. This "grammar of graphics" packages is dedicated to making data visualisations, and contains lots of dedicated functions for this.

* `palmerpenguins` - is a good example of a data-heavy package, it contains no functions, but instead datasets that we can use.

<div class="warning">
<p>A common source of errors is to call a function that is part of a package but forgetting to load the package.</p>
<p>If R says something like <code>Error in "function-name": could not find</code> then most likely the function was misspelled or the package containing the function hasn't been loaded.</p>
</div>

## My first data visualisation

Let's run our first data visualisation using the functions and data we have now loaded - this produces a plot using functions from the `ggplot2` package (@R-ggplot2) and data from the `palmerpenguins` (@R-palmerpenguins) package. 

Using these functions we can write a simple line of code to produce a figure. We specify the data source, the variables to be used for the x and y axis and then the type of visual object to produce, colouring them by the species.

Copy this into your console and hit Enter.


```r
ggplot(data = penguins,aes(x = bill_length_mm, y = bill_depth_mm)) + geom_point(aes(colour=species)) 
```

```
## Warning: Removed 2 rows containing missing values (geom_point).
```

<img src="01-data_files/figure-html/unnamed-chunk-49-1.png" width="100%" style="display: block; margin: auto;" />

<div class="information">
<p>You may have noticed R gave you a warning. Not the same as a big scary error, but R wants you to be aware of something.</p>
<p>In this case that two of the observations had missing data in them (either bill length or bill depth), so couldn't be plotted.</p>
</div>

The above command can also be written as below, its in a longer style with each new line for each argument in the function. This style can be easier to read, and makes it easier to write comments with `#`. Copy this longer command into your console then hit Enter. 

R ignores anything that comes after `#` on a line of code.


```r
ggplot(data = penguins, # calls ggplot function, data is penguins
       aes(x = bill_length_mm, # sets x axis as bill length
           y = bill_depth_mm)) + # sets y axis value as bill depth
    geom_point(aes(colour=species)) # plot points coloured by penguin species
```

## Writing scripts

Until now we have been typing words directly into the Console. This is fine for short/simple calculations - but as soon as we have a more complex, multi-step process this becomes time consuming, error-prone and *boring*. **Scripts** are a document containing all of your commands (in the order you want them to run), they are *repeatable, shareable, annotated records of what you have done*. In short they are incredibly useful - and a big step towards **open** and **reproducible** research. 

To create a script go to File > New File > R Script. 

This will open a pane in the top-left of RStudio with a tab name of `Untitled1`. In your new script, type some of the basic arithmetic and assignment commands you used previously. When you write a script, make sure it has all of the commands you need to complete your analysis, *in the order you want them to run*. 

### Commenting on scripts

Annotating your instructions provides yourself and others insights into why you are doing what you are doing. This is a vital aspect of a robust and reproducible workflow. And when you come back to a script, one week, one month or one year from now you will often wonder what a command was for. It is very, very useful to make notes for yourself, and its useful in case anyone else will ever read your script. Make these comments helpful they are for humans to read.

We have already seen how to signal a comment with the `#` key. Everything in the line after a # is ignored by R and won't be treated as a command. You should also see that it is marked in a different colour in your script. 

Put the following comment in your script on line 1.


```r
# I really love R
```

### Packages

To use the functions in a package they must be loaded *before* we call on the functions or data they contain. So the most sensible place to put library calls for packages is at the very **top** of our script. So let's do that now, 

<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Add the `library(ggplot2)` & `library(palmerpenguins)` on lines 2 & 3. 
Put a comment next to each line explaining what the package is for
"Hint use the help() function". </div></div>

<button id="displayTextunnamed-chunk-54" onclick="javascript:toggle('unnamed-chunk-54');">Show Solution</button>

<div id="toggleTextunnamed-chunk-54" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
# I really love R
library(ggplot2) # create elegant data visualisations
library (palmer penguins) # Palmer Archipelago Penguin Data
```
</div></div></div>


### Adding some code

Add the below code into your script, it is very similar to the code you ran earlier, but is preceded by `plot_1 <-`


```r
plot_1 <- ggplot(data = penguins, # calls ggplot function, data is penguins
       aes(x = bill_length_mm, # sets x axis as bill length
           y = bill_depth_mm)) + # sets y axis value as bill depth
    geom_point(aes(colour=species)) # plot points coloured by penguin species
```


### Running your script

To run the commands from your script, we need to get it *into* the Console. You could select and copy/paste this into the Console. But there are a couple of faster shortcuts.

* Hit the Run button in the top right of the script pane. Pressing this will run the line of code the cursor is sitting on. 

* Pressing Ctrl+Enter will do the same thing as hitting the Run button

* If you want to run the whole script in one go then press Ctrl+A then either click Run or press Ctrl+Enter

Try it now. 

You should notice that unlike when making previous data visuals, you do not immediately see your graph, this is because you assigned the output of your functions to an R object, instead of the default action where R would print the output. 

* To see the new plot you have made you should type `plot_1` into the R console. Or add it underneath the script and run it again! 

### Making an output

For our next trick we will make a script that outputs a file. Underneath the lines of code to generate the figure we will add a new function `ggsave()`. Then **re-run your script**.
To find out more about this function (and the arguments it contains), type `help(ggsave)` into the console. 


```r
ggsave(filename = "bill_scatterplot.png", 
       plot = plot_1, 
       dpi = 300, 
       width = 6, 
       height = 6)
```

Check the files tab on RStudio Cloud, there should now be a new file in your workspace. 
<div class="warning">
<p>It is very important to have naming conventions for all files.</p>
<p>Everything after the <code>.</code> is file extension information informing the computer how to process the contents of the file. <code>.png</code> stands for "Portable Graphics Format”, and it means the data is an uncompressed image format.</p>
<p>Everything before the <code>.</code> is for humans, it is a good idea to make sure these have a naming convention.</p>
<p>Avoid periods, spaces or slashes, instead use YYYYMMDD and underscores</p>
<p>e.g. YYYYMMDD_short_image_description.fileextension</p>
</div>


**FILE FORMAT PICTURE**

### Saving your script

Our script now contains code and comments from our first workshop. We need to save it. 

Alongside our data, our script is the most precious part of our analysis. We don't need to save anything else, any outputs etc. because our script can always be used to generate everything again. Note the colour of the script - the name changes colour when we have unsaved changes. Press the Save button or go to File > Save as. 
Give the File a sensible name like "YYYYMMDD_simple_commands" and in the bottom right pane under `Files` you should now be able to see your saved script, it should be saved with a `.R` file extension indicating this is an R Script.  

You could now safely quit R, and when you log on next time to this project, your script will be waiting for you.

## Quitting

* Make sure you have saved any changes to your R script - that's all you need to make sure you've done!

* If you want me to take a look at your script let me know

* If you spotted any mistakes or errors let me know

* Close your RStudio Cloud Browser

* Go to Blackboard to complete a short quiz! 


<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
Produce a scatterplot of longevity` against `thorax`. What does the relationship look like? </div></div>

<button id="displayTextunnamed-chunk-59" onclick="javascript:toggle('unnamed-chunk-59');">Show Solution</button>

<div id="toggleTextunnamed-chunk-59" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body"><div class="tab"><button class="tablinksunnamed-chunk-59 active" onclick="javascript:openCode(event, 'option1unnamed-chunk-59', 'unnamed-chunk-59');">Base R</button><button class="tablinksunnamed-chunk-59" onclick="javascript:openCode(event, 'option2unnamed-chunk-59', 'unnamed-chunk-59');"><tt>tidyverse</tt></button></div><div id="option1unnamed-chunk-59" class="tabcontentunnamed-chunk-59">

```r
plot(longevity ~ thorax, data = ff, 
     pch=19, col='darkgrey')
```


The plot suggests that a linear relationship might exist between the two variables. So we can proceed by fitting a linear model in R.
</div><div id="option2unnamed-chunk-59" class="tabcontentunnamed-chunk-59">

```r
ggplot(ff) +
    geom_point(aes(x = thorax, y = longevity))
```


The plot suggests that a linear relationship might exist between the two variables. So we can proceed by fitting a linear model in R.
</div><script> javascript:hide('option2unnamed-chunk-59') </script></div></div></div>





<div class="panel panel-default"><div class="panel-heading"> Task </div><div class="panel-body"> 
1. Fit a linear model with lifespan as response variable and thorax length as explanatory variable.
2. Display a summary of the fit, together with the 97% confidence interval for the estimated parameters.
3. Show the diagnostic plots for the model. </div></div>

<button id="displayTextunnamed-chunk-61" onclick="javascript:toggle('unnamed-chunk-61');">Show Solution</button>

<div id="toggleTextunnamed-chunk-61" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

```r
fit <- lm(longevity ~ thorax, ff)
summary(fit)
confint(fit, level=0.97)
par(mfrow=c(2, 2))
plot(fit, pch=19, col='darkgrey')
par(mfrow=c(1, 1))
```
</div></div></div>


## Activity 1 

When you get the correct answer, the answer box will turn green. Sometimes this doesn't work on Internet Explorer or Edge so be sure to use Chrome or Firefox.

1.  What is the output from 5^4

<input class='webex-solveme nospaces' size='3' data-answer='["625"]'/> 

2. Put the brackets in the correct place to make this equation correct `4+2*8 = 48`

<input class='webex-solveme nospaces' size='2' data-answer='["48"]'/>

3. What answer will you get when you type `2+2 = 4` into the R console?

<select class='webex-select'><option value='blank'></option><option value=''>TRUE</option><option value=''>FALSE</option><option value='answer'>Error</option></select>

<button id="displayTextunnamed-chunk-62" onclick="javascript:toggle('unnamed-chunk-62');">Show Solution</button>

<div id="toggleTextunnamed-chunk-62" style="display: none"><div class="panel panel-default"><div class="panel-heading panel-heading1"> Solution </div><div class="panel-body">

If we wanted R to make a judgement we must use == not = otherwise we will get an Error message
</div></div></div>

4. What symbol do I use if I want to **assign** a value or output of a function to an R object

<input class='webex-solveme nospaces' size='2' data-answer='["<-"]'/>

5. What is the value of `a` if I ran the following commands?


```r
a <-  12*2

a <- 5
```

 <input class='webex-solveme nospaces' size='1' data-answer='["5"]'/>

6. Which of these variable naming conventions is **not** written correctly?

<select class='webex-select'><option value='blank'></option><option value=''>snake_case</option><option value=''>camelCase</option><option value='answer'>Screaming_Snake_Case</option><option value=''>kebab-case</option></select>

7. What should I type into the R console if I want `help` with the `round()` function?

<input class='webex-solveme nospaces' size='11' data-answer='["help(round)"]'/>

8. Which of these statements about function arguments **is not true**

<select class='webex-select'><option value='blank'></option><option value=''>Arguments are the inputs we give to a function</option><option value='answer'>Values for R arguments must always be defined by the user</option><option value=''>Naming arguments supersedes position in a function</option><option value=''>There is no limit to the number of arguments a function could have</option></select>

9. Evaluate this statement "An R Package can contain code functions, data, or both."

<select class='webex-select'><option value='blank'></option><option value='answer'>TRUE</option><option value=''>FALSE</option></select>

### Head to Blackboard and submit your answers to the quiz to get your first Data Science Learning Badge. 

<h3 style = 'color:#003366;' id="webex-total_correct"></h3>




## Activity 2


```{=html}
<a href="https://raw.githubusercontent.com/UEABIO/5023Y_Workshop/main/data/Challenger.csv">
<button class="btn btn-success"><i class="fa fa-save"></i> Download as csv</button>
</a>
```

1. Download this R Script

2. Upload it to your workspace on RStudio Cloud

3. Rearrange the chunks of code to make a sensible pipeline

4. Save the file! 


