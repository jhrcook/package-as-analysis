# Getting Started

Setting up the package is mostly automated and is well documented in [R Packages](http://r-pkgs.had.co.nz/intro.html) by Hadley Wickham. If you are running the analysis on your local machine, I would recommend using [RStudio](https://www.rstudio.com) (which you likely already do), but this is possible to do on a remote computing cluster (which is how I work). I begin by going through the steps of setting up the basic package framework, which is the same for local or remote work. Following that, there is a section for how I work remotely. This can be skipped if you only work locally or if you already have a system you enjoy (though I highly recommend the system I currently use). I finish off with a few extras that I recommend using, but are not necessary.

## R Package Set Up

The set up process is rather simple. If using RStudio, you can start a new R project as a package. Otherwise, the following command will get the basic framework started. There is a lot of overlap between the devtools and usethis package. I believe that RStudio is trying to fade out devtools and instead have people use the various packages that were split from it, including usethis.

The advantage to using the usethis functions for seemingly simple tasks (such as making the "data-raw" directory) is that it will also add the necessary lines to ".RBuildignore," the "DESCRIPTION," and "NAMESPACE" if needed.

It's easy to create the package from the R console.


```r
usethis::create("path/to/package/pkgname")
```

You can then add a license as shown below. I generally use a GPL-3, though you can get a lot of information on the common licenses at [choosealicense.com](https://choosealicense.com).


```r
usethis::use_gpl3_license(name = "Your Name")
```

Prepare the project to use roxygen for documentation.


```r
usethis::use_roxygen_md()
```

Create a README file. You can also opt to use a normal Markdown file with `usethis::use_readme_md()`, though I would recommend to just go with an RMarkdown file.


```r
usethis::use_readme_rmd()
```

Create a "NEWS" file for announcing major changes to the project.


```r
usethis::use_news_md()
```

Create a "data-raw" directory.


```r
usethis::use_data_raw()
```

Finally, set up the use of testthat package for testing.


```r
usethis::use_testthat()
```

**Note:** If you are working remotely (ie. sshing to the computer running the code), many of the usethis functions will open the file that you just asked them to create (eg. open "NEWS.md" after using `use_news_md()`) in vim. To suppress this, just pass the paramter `open = FALSE`. Otherwise, it is set to `interactive()`.


### Git and GitHub

If you are programming, you should be using git. This is especially important in the sciences because git logs can be used to resolve legal conflicts and issues of data falsification. GitHub is not essential, though I would highly recommend you use it because it makes managing files and collaboration much easier. It is also essential for taking advantage of some of the best parts of an R package such as build checks and `pkgdown` (see Extras below)

To get started with git, there are *tons* of resources available, so I will not describe it here. If you are new to git and GitHub, here are a few good resources to get you started:

* [An introduction to Git: what it is, and how to use it](https://medium.freecodecamp.org/what-is-git-and-how-to-use-it-c341b049ae61)
* [How To Use Git: A Reference Guide](https://www.digitalocean.com/community/tutorials/how-to-use-git-a-reference-guide)
* [GitHub Guides: Hello World](https://guides.github.com/activities/hello-world/)

There is a usethis function to initiate git (`usethis::use_git()`) though I always prefer to set up myself.


## Remote

If you conduct work remotely, I'm going to assume that you have ssh set up and running. Otherwise, there are plenty of resources available, and you should review the material available by your system admin.

Though I prefer Rstudio for normal package development, I spare my computer the pain of performing complex and heavy computation, opting instead to off-load it to the [Harvard Medical School Research Computing Cluster](https://rc.hms.harvard.edu). Therefore, I use [SublimeText3](https://www.sublimetext.com) as by text editor and send code to the remote comuting node over ssh using [iTerm2](https://iterm2colorschemes.com) as my terrminal. Finally, I use SSH File System (SSHFS) to "mount" the remote directory to my local directory.


### SublimeText3 Set-Up

Here are the handful of SublimeText3 (ST3) packages I use for R coding, followed by any particular notes on their use:

* [LSP](https://packagecontrol.io/packages/LSP) - "Gives Sublime Text 3 rich editing features for languages with Language Server Protocol support"
* [MarkdownEditing](https://packagecontrol.io/packages/MarkdownEditing) - "Markdown plugin for Sublime Text. Provides... more robust syntax highlighting and useful Markdown editing features for Sublime Text."
* [R-IDE](https://packagecontrol.io/packages/R-IDE) - "[A]iming to utilize the use of language server + better support R Markdown + better support of R packaging + ..."
* [SendCode](https://packagecontrol.io/packages/SendCode) - "Send code and text to macOS and Linux Terminals, iTerm, ConEmu, Cmder, Tmux, Terminus; R (RStudio), Julia, IPython."

LSP and R-IDE handle syntax and completion in ST3. It isn't a great system, so if you know of a better set-up in ST3, [please let me know](https://github.com/jhrcook/package-as-analysis/issues). MarkdownEditing and R-IDE combine to make RMarkdown feasible. The SendCode package essentially copies, pastes, and runs my code written in ST3 to the terminal when I press `command` + `return`. This way, I can type in ST3 and run in the terminal without using the mouse.

Before moving on, I made this snippet to quickly add a code chunk.

````html
<snippet>
        <content><![CDATA[
```{r ${1:chunk_name}}
$0
```
]]></content>
        <!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
        <tabTrigger>rchunk</tabTrigger>
        <!-- Optional: Set a scope to limit where the snippet will trigger -->
        <scope>text.html.markdown.multimarkdown, text.html.markdown</scope>
        <description>create a Rmd code chunk</description>
</snippet>
````

### Using SSH File System

I use SSH File System (SSFHS) to "mount" my remote directory to my local directory. It is essentually SFTP and SSH combined (the details go right over my head) and it is fairly easy to get set-up. Here is a [link](https://github.com/osxfuse/osxfuse/wiki/SSHFS) to get everything going, and I have included the steps I used below.

To start I downloaded and installed [FUSE for macOS](https://osxfuse.github.io). Then I downloaded and installed the [latest build of SSHFS](https://github.com/osxfuse/sshfs/releases). Finally, I created an empty directory that will become the place that I mount the remote directory. Typically, I make the root of the package, though I could see instances where you would want the package in a subdirectory below it.

```bash
# on local
mkdir ~/Lab_Projects/pkgName
```

On the remote server, I make a directory with the same name

```bash
# on remote
/path/to/compute/directory/pkgName
```

Finally, to connect the two, I use the following command that is pretty much identical to initiating a normal ssh session.

```bash
# on local
sshfs username@remote.host.com:/path/to/compute/directory/pkgName ~/Lab_Projects/pkgName
```

Now, the computer will treat the mount just like a normal flash drive, and ST3 fully accepts it. The only change I made to ST3 was to map a key-binding to "Project/Refresh Folders". This way, if new files are created remotely, a quick key-stroke and everything is visible in the ST3 sidebar.


### Git and GitHub

If working remotely, I have found it much easier to handle everything git-related on the remote side. Therefore, I created  ssh RSA keys and shared the public one with the GitHub repo so I could push over ssh. Setting this up is pretty simple and well outlined in [Connecting to GitHub with SSH](https://help.github.com/en/articles/connecting-to-github-with-ssh).


## Extras

Though these next few items are not required, I *highly recommend* implementing them because they each take advantage of the fact that this project adheres to the standard R framework. Their different functions are all reasons to go through the trouble of mainting this framework.

### pkgdown

Pkgdown ties a bow around your package, slaps it on the bottom, and builds a gorgeous and professional website rich with useful features. It builds the documentation for easy reference, presents the vignettes, and organizes all of the package meta-data so it is easily viewable and understandable. Here are some packages that take advantage of pkgdown:

* [pkgdown](https://pkgdown.r-lib.org) (of course)
* [ggplot2](https://ggplot2.tidyverse.org)
* [ggsci](https://nanx.me/ggsci/)
* [ggasym](https://jhrcook.github.io/ggasym/index.html) (a shameless plug of my own lil' package)

The use of pkgdown obviously begins with a usethis function.


```r
usethis::use_pkgdown()
```

All that you have to do from there is use `pkgdown::build_site()` to build the site whenever the project is at a good stopping point for the day. (If working remotely, pass `preview = FALSE` to prevent pkgdown from searching for a browser to display in when completed.)

To show the website on GitHub, go to "Settings" in the repository, and select "master branch /docs folder" from the options in the "GitHub Pages" section. It should look something like this (another shameless plug for lil' ole' ggasym).



### Travis-CI, Appveyor, and Codecov

GitHub integration also opens up the use of continuous integration (CI) apps. [Travis-CI](https://travis-ci.org) and [Appveyor](https://www.appveyor.com) are useful for checking the build status of the package. I just use both because they each require so little effort to integrate and each provides their own suite of functions. Noteably, Appveyor build the package on Linux and Windows. To get started, just use usethis.

[Codecov](https://codecov.io) provides an indication as to how well the package's tests cover the code. Though not a perfect measure of test quality (nothing ever will be), I find this tool to be helpful for me to find which functions I have and have not created tests for.


```r
usethis::use_travis()
usethis::use_coverage("codecov")
usethis::use_appveyor()
```

You then just follow the instructions printed out to get everything set up. If this your first time useing any of the tools, then you will have to grant them access to your GitHub repositories, and they will do the rest.

The usethis command will also procuce the markdown code for showing the status badges for each tools. Placing these below the package name in the README.Rmd is sstandard practice and will tell pkgdown to put them in the side bar of the site.

On top of looking good and being informative for you during the development process, these badges will also provide visitors an indication as to the quality and maintaince of the package. A few good badges will likely make visitors more trusting of your results.


### Spelling

TODO
