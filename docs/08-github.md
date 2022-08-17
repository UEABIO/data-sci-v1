
# Github

https://intro2r.com/use_git.html#undo

## Let's Git it started 

Git is a **version control system**. Originally built to help groups of developers work collaboratively on big software projects. It helps us manage our RStudio projects - with tracked changes. 

Git and GitHub are a big part of the data science community. We can use GitHub in a number of ways

1) To source code and repurpose analyses built by others for our own uses

2) Manage our analysis projects so that all parts of it: 

  * Data
  
  * Scripts
  
  * Figures
  
  * Reports
  
Are version controlled and open access

3) Version control lets you recover from any mistakes & your analysis is *backed up* externally

4) When you come to publish any reports - your analysis is accessible to others

5) Build up your own library of projects to show what you can do in Data Science


Watch [this video](https://www.youtube.com/watch?v=w3jLJU7DT5E) *before* or *after* today's session

### Will this be fun?

No.

Using GitHub and version control is a bit like cleaning your teeth. It's not exactly fun, but it's good for you and it promotes excellent hygiene. It also only takes about 2 minutes. 

When we talk a about projects on GitHub we refer to Repositories / repos.

Repos on GitHub are the same unit as an RStudio Project - it's a place where you can easily store all information/data/etc. related to whatever project you're working on.

The way in which we will set up our RStudio Projects will now have a few extra steps to it

* Make a new GitHub repository (or *fork* an existing one)

* Make a New project on RStudio Cloud - selecting the *from GitHub Repository* option 

* Clone your GitHub repo into an RStudio Project

* Make sure RStudio and Github can *talk* to each other

* Go about your normal business

* When it comes to *saving* your files, you will also periodically make a **commit** - this takes a multi-file *snapshot* of your *entire* project

* At the end of a session **push** your changes to GitHub.

These changes to working with RStudio will feel a little different at first, but will quickly become routine - and are a big step forward in your Data Science skills. 

### The Payoff

* **A portfolio** build up a library of data science projects you can show off

* **be keen** track the development of R packages on GitHUb

* **version control** keep a safe archive of all your edits and changes

* **play with others** easy ways to collaborate on data science projects

For the full rundown on how to use Git and R you can't go wrong with checking out [Happy Git](https://happygitwithr.com/)


## Set up GitHub

First things first you will need to set yourself up with a GitHub account. 

Head to [GitHub](https://github.com/) and sign up for a free account. 

<div class="warning">
<p>Make a careful note of</p>
<ul>
<li><p>The username you choose</p></li>
<li><p>Use the same email you have signed up to RStudio Cloud with</p></li>
<li><p>Note your password carefully!</p></li>
</ul>
</div>


## **Exercise 1.** Fork & clone an existing repo on GitHub, make edits, push back

**a.** Go to [github.com](https://github.com/) and log in (you need your own account - for sign up with your uea.ac.uk e-mail)

**b.** In the Search bar, look for repo **Philip-Leftwich/5023Y-Happy-Git**

**c.** Click on the repo name, and look at the existing repo structure

**d.** **FORK** the repo

### What the hell is a fork?

<img src="images/fork.png" width="100%" style="display: block; margin: auto;" />


A fork is when you generate a *personal* copy of another user's [repository](#glossary-github).

**e.** Press Clone/download and copy the URL, then create a **new** project in RStudio Cloud selecting the **New project from Git repository** option -  make sure you are in the 5023Y Workspace

<img src="images/new-project.png" width="100%" style="display: block; margin: auto;" />


**f.** Open the some_cool_animals.Rmd document, and the accompanying html 

**g.** Add *your name* to the top of the document

**h.** BUT WAIT. We have forgotten to add a great image and facts about a very important species - Baby Yoda, including an image (the file is in the repo, and the info to add is below).


**FACTS**

<img src="images/Grogu.png" width="100%" style="display: block; margin: auto;" />


- Also known as "The Child"

- likes unfertilised frog eggs & control knobs

- strong with the force

<p>&nbsp;</p>
<p>&nbsp;</p>


**i.** Once you’ve added Grogu, knit the Rmd document to update the html

**j.** Add your Git credentials go to section [talking to github](#talking-to-github)

**k.** Stage, Commit & Push all files [(glossary)](#glossary-github)

Staged - pick those files which you intend to bind to a commit

Commit - write a short descriptive message, binds changes to a single [commit](#commit)

Push - "Pushes" your changes from the local repo to the remote repo on GitHub, [(push)](#push)


**l.** On GitHub, refresh and see that files are updated. Cool! Now you’ve used something someone else has created, customized it, and saved your updated version. 

## Talking to GitHub

Getting set up to talk to GitHub can seem like a pain. Eventually when you work on your own computer - with a copy of R & RStudio installed - you will only have to do this once. For now when we use RStudio Cloud - it looks like we have to do this **once per project**. It only takes a few seconds and you should put these commands **directly into your console**. 

Run this first line **in your console** and put in your GitHub username and the e-mail connected to your GitHub account. 

<div class="warning">
<p>Make sure you go to your RStudio Cloud profile &gt; Authentication and select Github Enabled &amp; Private repo access also enabled</p>
</div>


```r
usethis::use_git_config(user.name = "Jane Doe", user.email = "jane@example.org")
```


Then you need to give RStudio Cloud your GitHub Personal Access Token, which you can retrieve by going to Settings > Developer Settings > Generate Token 

Select all the "scopes" and name your token. 

<img src="images/git-PAT.png" width="100%" style="display: block; margin: auto;" />

Make a note of this because you will need it whenever you set up a new project you want to talk to GitHub. GitHub recently removed password authentication in favour of PATs, but RStudio Cloud doesn't seem to have updated this yet - that's ok though - just enter this line of code - then copy+paste your PAT when prompted. - Option set/replace these credentials.


```r
gitcreds::gitcreds_set()
```


If you forget your PAT - that's ok - you can't retrieve it - but you can just generate a new one.

### See changes

The first and most immediate benefit of using GitHub with your RStudio Project is seeing the changes you have made since your last commit.

The RStudio Git pane lists every file that’s been added, modified or deleted. The icon describes the change:

* You've changed a file
<img src="images/git-modified.png" width="5%" style="display: block; margin: auto auto auto 0;" />

* You've added a new file Git hasn't seen before
<img src="images/git-unknown.png" width="5%" style="display: block; margin: auto auto auto 0;" />

* You've deleted a file
<img src="images/git-deleted.png" width="5%" style="display: block; margin: auto auto auto 0;" />

You can get more details on the changes that have been made to each file by right-clicking and selecting diff 

<img src="images/git-diff.png" width="15%" style="display: block; margin: auto auto auto 0;" />

This opens a new window highlighting the **diff**erences between your current file and the previous commit. 

<img src="images/git-diff-window.png" width="100%" style="display: block; margin: auto;" />
The background colours tells you whether the text has been added (green) or removed (red). (If you’re colourblind you can use the line numbers in the two columns at the far left as a guide). 


## How to use version control - when to commit, push and pull
 
Repositories (repos) on GitHub are the same unit as an RStudio Project - it's a place where you can easily store all information/data/etc. related to whatever project you're working on.
 
When we create a Repository in GitHub and have it communicating with a Project in RStudio, then we can get (**pull**) information from GitHub to RStudio, or **push** information from RStudio to GitHub where it is safely stored and/or our collaborators can access it. It also keeps a *complete history* of updated versions that can be accessed/reviewed by you and your collaborators at any time, from anywhere, as long as you have the internet.


I have mentioned the term **commit** a few times (\@ref(glossary-github)). The fundamental unit of work in Git is a commit. A commit takes a snapshot of your code at a specified point in time. 

You create a commit in two stages:

1. You **stage** files, telling Git which changes should be included in the next commit.

2. You **commit** the staged files, describing the changes with a message.

To create a new commit, **save** your files, then select files for inclusion by *staging* them, tick the checkbox and then select the commit box

<img src="images/stage_step_4.png" width="100%" style="display: block; margin: auto;" />

A new window will open - and you will see the diffs in the bottom pane, and all the files you have selected for the latest commit. 

### Commit

You now need to write a **commit message**. This should be short but meaningful

<img src="images/stage_step_5.png" width="100%" style="display: block; margin: auto;" />


Describe the **why**, not the what. Git stores all the associated differences between commits, the message doesn’t need to say exactly what changed. Instead it should provide a summary that focuses on the **reasons** for the change. Make this understandable for someone else!

Once you click commit a new window will open that summarises your commit - and you can close this

<img src="images/stage_step_6.png" width="100%" style="display: block; margin: auto;" />


### Push

At the moment, all of your commits are *local*, in order to send them to GitHub you have to select **Push** at this point your github credentials need to be in place - if you get prompted to provide these, close the windows and follow the steps [here](#talking-to-github) before trying again. 

Your git pane will be empty at this point - but there is a little message at the top detailing how many commits you are *ahead* of the master repo on GitHub. 

<img src="images/stage_step_7.png" width="100%" style="display: block; margin: auto;" />


### A couple of general tips:

<div class="note">
<ul>
<li><p>Pull at the start of <strong>every session</strong> this retrieves the master repo from GitHub - which you update at the end of every session. This helps prevent <em>conflicts</em></p></li>
<li><p><strong>Commit/push</strong> in small, meaningful increments and do this often. You can make <strong>multiple</strong> commits in a session - and <strong>always push at the end of the session</strong></p></li>
<li><p>In this way your GitHub Repo becomes the <strong>master copy</strong> of your project.</p></li>
</ul>
</div>


### Turn back time with Git

````md
"If I could turn back time,

If I could find a way,

I'd take back those commits that have hurt you,

And you'd stay" - Cher
````

Once you start using Git with RStudio - you get a whole bunch of different options for undoing changes, correcting mistakes and turning back time to previous versions! 

* To undo changes between commits you can select the diff option and remove lines one-by-one

* Right-click on a file in the Git pane and select the revert option will undo all changes between this and the previous commit **beware** cannot be undone.

If you don't catch a mistake right away you can select the history button and **pull** previous commits from GitHub.

<img src="images/git-history.png" width="5%" style="display: block; margin: auto auto auto 0;" />



## **Exercise 2.** GitHub Classrooms enabled R Projects with subfolders

GitHub Classrooms is a way for me to set repos as assigments - when you accept an assignment on GitHub Classroom it *automatically* forks a private repo for you. 

You should make regular commits and pushes to save your work as you go - and I will be grading your project repositories on GitHub classrooms when you do your assignment work. 

<div class="warning">
<p>When you accept an assignment on GitHub classrooms - the repo won't appear on your main profile, this is because it belongs to our class rather than you. You can always find it by searching through your Organisations - <strong>but</strong> it's probably easiest just to make a bookmark/make a note of your unique URL for each assignment.</p>
</div>

**a.** Follow this [invite link](https://classroom.github.com/a/QFt76-i2)

**b.** You will be invited to sign-in to Github (if not already) & to join the UEABIO organisation

**c.** Clone your assignment to work locally in RStudio Cloud - 5023Y Workspace

**d.** In your local project folder, create subfolders ‘data’ and ‘figures’, 'scripts', 'markdown' (**Note** use the dir.create commands in the console)

**e.** Drop the file disease_burden.csv into the ‘data’ subfolder

**f.** Open a new .R script

**g.** Attach the `tidyverse`, `janitor`, and optionally `here` packages

**h.** Read in the infant_mortality.csv data

This is a file look at the death rate for every country in the world across six decades. See the README for more information

**i.** Stage, commit & push at this point - notice that the empty folder ‘final_graphs’ doesn’t show up (won’t commit an empty folder) - **you will have to set up your git credentials again**

**j.** Back in the script, write a short script to read and clean the data. 

This script is pre-written, it puts the data in tidy format, cleans names, makes sure year is treated as date data and filters four countries of interest.

Assign this to a new object 



```r
library(tidyverse)
library(lubridate)
library(janitor)
library(plotly)

infant_mortality <- read_csv("data/infant_mortality.csv") 

subset_infant_mortality <- infant_mortality %>%
  pivot_longer(cols="1960":"2020", 
               names_to="year",               
               values_to="infant_mortality_rate") %>%
  mutate(year=lubridate::years(year)) %>% # set ymd format
  mutate(year=lubridate::year(year)) %>% # extract year
  janitor::clean_names() %>% # put names in snake case
  filter(country_name %in% 
           c("United States", 
             "Japan", 
             "Afghanistan", 
             "United Kingdom")) # extract four countries

# View(subset_infant_mortality)

# subset the date according to (US,UK, Japan = lowest infant death rates, Afghanistan = highest infant death rates)
```


**k.** Make a ggplot plotting the infant mortality rate by country

HINT - use `geom_line()` and remember to separate countries by colour



```r
ggplot(data = subset_infant_mortality) +
  geom_line(aes(x = year,
                 y = infant_mortality_rate,
                 color = country_name))
```


**l.** Update your graph with direct labels (using `annotate`) and vertical or horizontal lines with `geom_vline` or `geom_hline`. 



**m.** Use ggsave() to write your graph to a .png in the ‘final_graphs’ subfolder



```r
ggsave("figures/infant mortality graph.png", plot=mortality_figure, dpi=900, width = 7, height = 7)
```

**n.** Save, stage, commit

**o** Let's do one more cool and fun thing! And make an interactive version of our plot using plotly @R-plotly just for fun!


```r
ggplotly(mortality_figure, tooltip = c("infant_mortality_rate"))
## uses plotly package
```

**p** Now save, stage, commit & **push**

**q.** Check that changes are stored on GitHub


(**NOTE** this will be in your organisations rather than repos)



**Make sure you finish both exercises before next week to become a GitHub pro!!!!!!!!!**

## Find your classroom repos

When you work with GitHub classrooms your repos become part of our organisation UEABIO. 
If you want to find your repos on GitHub then you can use the direct URL (if you noted it), or head to (https://github.com/UEABIO) - you should only be able to see repos that belong to **you**. 

<img src="images/classroom-organisation.png" width="100%" style="display: block; margin: auto;" />

## Glossary-GitHub

<table>
 <thead>
  <tr>
   <th style="text-align:left;"> Terms </th>
   <th style="text-align:left;"> Description </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> clone </td>
   <td style="text-align:left;"> A clone is a copy of a repository that lives on your computer instead of on a website's server somewhere, or the act of making that copy. When you make a clone, you can edit the files in your preferred editor and use Git to keep track of your changes without having to be online. The repository you cloned is still connected to the remote version so that you can push your local changes to the remote to keep them synced when you're online. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> commit </td>
   <td style="text-align:left;"> A commit, or revision, is an individual change to a file (or set of files). When you make a commit to save your work, Git creates a unique ID that allows you to keep record of the specific changes committed along with who made them and when. Commits usually contain a commit message which is a brief description of what changes were made. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> commit message </td>
   <td style="text-align:left;"> Short, descriptive text that accompanies a commit and communicates the change the commit is introducing. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> fork </td>
   <td style="text-align:left;"> A fork is a personal copy of another user's repository that lives on your account. Forks allow you to freely make changes to a project without affecting the original upstream repository. You can also open a pull request in the upstream repository and keep your fork synced with the latest changes since both repositories are still connected. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Git </td>
   <td style="text-align:left;"> Git is an open source program for tracking changes in text files. It was written by the author of the Linux operating system, and is the core technology that GitHub, the social and user interface, is built on top of. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> GitHub Classroom </td>
   <td style="text-align:left;"> GitHub Classroom automates repository creation and access control, making it easy to distribute starter code and collect assignments on GitHub </td>
  </tr>
  <tr>
   <td style="text-align:left;"> Markdown </td>
   <td style="text-align:left;"> Markdown is an incredibly simple semantic file format, not too dissimilar from .doc, .rtf and .txt. Markdown makes it easy for even those without a web-publishing background to write prose (including with links, lists, bullets, etc.) and have it displayed like a website. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> pull </td>
   <td style="text-align:left;"> Pull refers to when you are fetching in changes and merging them. For instance, if someone has edited the remote file you're both working on, you'll want to pull in those changes to your local copy so that it's up to date </td>
  </tr>
  <tr>
   <td style="text-align:left;"> push </td>
   <td style="text-align:left;"> To push means to send your committed changes to a remote repository on GitHub.com. For instance, if you change something locally, you can push those changes so that others may access them. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> README </td>
   <td style="text-align:left;"> A text file containing information about the files in a repository that is typically the first file a visitor to your repository will see. A README file, along with a repository license, contribution guidelines, and a code of conduct, helps you share expectations and manage contributions to your project. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> repository </td>
   <td style="text-align:left;"> A repository (repo) is the most basic element of GitHub. They're easiest to imagine as a project's folder. A repository contains all of the project files (including documentation), and stores each file's revision history. Repositories can have multiple collaborators and can be either public or private. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> RMarkdown </td>
   <td style="text-align:left;"> Rmarkdown is a package and filetype that are deeply embedded with RStudio to allow the integration of Markdown and output chunks of programming code (such as R) to publish a variety of different file types </td>
  </tr>
  <tr>
   <td style="text-align:left;"> personal access token </td>
   <td style="text-align:left;"> A token that is used in place of a password when performing Git operations over HTTPS. Also called a PAT. </td>
  </tr>
</tbody>
</table>


## Summing up GitHub

### What we learned

You have learned

* How to fork and clone GitHub Projects

* How to use GitHub classrooms

* How to make RStudio and GitHub talk to each other

* How to use version control, with stage, commit and push

You have used

* `gitcreds` @R-gitcreds

* `usethis` @R-usethis




