# Framework

## Introduction

I have decided to introduce the R package framework before going through the set-up process because, quite frankly, I think this is more important. There are many sites that outline the steps of creating an R package (they likely do it better than I will next chapter), but the main point of this book is how to make the R package into a data analysis project. Therfore, understanding the use of the framework should be the reader's focus, here.

I try to address the following points for each peace of the framework:

1. What is it and what is its main role?
2. When does it need to be used or adjusted?
3. What is unique about its use for a data analysis project?



## Vignettes

Vignettes are the heart of the data analysis. Ironically, they are often covered last in tutorials on creating R packages, and rightly so! For an R package, the vignettes merely show a specific functionality or extension of the package. They are usually user guides or are attempts to inspire potential users.

However, in a data analysis, the vignettes *are* the analysis. They are where ideas are formed, discussed, tested, and validated. Everything is centered around a vignette. If you already use R markdown for data analysis, then this should be of little perturbance to your standard operating procedure. If you do not, though, this should be a welcomed change.


### Starting a Vignette

Ideally, each vignette will be a different step in the analysis. Alternatively, each vignette could be a different part of the project (e.g. analyzing the results of a screen in one vignette and analyzing the results of validation experiments in another). However you choose to divide up the analysis is your choice (though I have found R markdown files to slow down RStudio if they get too long or image intensive). To begin a vignette, use the 'usethis' function, passing the name of the vignette.


```r
usethis::use_vignette("a01_part1_firstvignette")
#> ✔ Setting active project to '/path/to/pkg/ExampleAnalysisPackage'
#> ✔ Adding 'knitr' to Suggests field in DESCRIPTION
#> ✔ Setting VignetteBuilder field in DESCRIPTION to 'knitr'
#> ✔ Adding 'rmarkdown' to Suggests field in DESCRIPTION
#> ✔ Creating 'vignettes/'
#> ✔ Adding '*.html', '*.R' to 'vignettes/.gitignore'
#> ✔ Adding 'inst/doc' to '.gitignore'
#> ✔ Creating 'vignettes/A01_part1_firstvignette.Rmd'
#> ● Modify 'vignettes/A01_part1_firstvignette.Rmd'
```

Notice that the ".Rmd" extension is ommited in the above function - 'usethis' adds the appropriate extension in many cases. 


### Naming system

It is important to deliberately decide on a naming scheme. I have opted for "(a-z)(##)_part_subpart" where the leading alpha-numeric index is made of two levels followed by the names of the two levels. The first letter is the highest level of orgnization and the second two digits are for the sublevel. For the naming, the first name ("part") is the name referring to the layer of organization dictated by the letter of the leading alpha-numeric index. The second name ("subpart") is referring to the layer of organization dictated by the second two digits of the leading alpha-numeric index

Therefore, the follow-up analysis that follows "A01_part1_firstvignette" could be "A02_part1_secondvignette". A vignette for another part of the project would alternatively be called "B01_part2_firstvignette". I now have two branches of analysis in my project, the first with two pages of analysis and the second with only one.

Of course, you should customize the naming scheme if this does not work for you, but it is definitely important to have one and to keep it ordered.

The only limit on the namining of a vignette is that it cannot start with a number.


### Formatting a vignette

I begin by loading the libraries in a single chunk *and leaving it visible* (i.e. `echo = TRUE` in the chunk's header). While it is tempting to hide this information to reduce clutter, this is obviously relevent information for anyone trying to replicate or adapt your analysis. 

Next, I declare the data directories in their own R chunk if I will be using them in the vignette. See below for more information on these. Again, leave them visible so others can track your work.

Finally, I begin writing the analysis with a section defining the purpose of the analysis to follow. Usually this section will be call **Purpose**, **Goal**, **Introduction**, etc. Whatever you choose, just make sure to clearly state the why the analysis is being done - focus on the "why", not the "how".

After this, it is up to you. The format of the analysis will obviously depend on the details of the work being done, but make sure to keep a logical flow and describe the purpose of each step. Also, it is helpful to include information on what is happening within the code. This will help both the reader and future you know what is being done in each chunk of code.



## Data management: "data", "data-raw", and "inst/extdata"

This topic is fully covered in [Chapter 2. Data Management][Data Management], though I breifly introduce the system here.

**#> TODO**: write the full chapter on data first before writing this subset of its information.



## The R/ Directory

The R directory will hold all R scripts (usually files ending with the ".R" extension). For a normal package, this is all of  the source code that builds the package.

For the purpose of a data analysis project, this will still hold R scripts (with the ".R" extension), but the organization of scripts is different.



## Other Languages

read ["Other languages"](https://r-pkgs.org/inst.html#inst-other-langs) section of Hadley's R Packages



## Metadata


### DESCRIPTION



### NAMESPACE

It is unlikely you will need to touch this file yourself. It is created by `usethis::create_package()` and updated by the functions used for documention and building the package. Briefly, the `NAMESPACE` file tells R what is being brought in by this package. If you really want to dive into the details, Wickham covers it is thoroughly in [*Advanced R: Chapter 9 Namespace*](https://r-pkgs.org/namespace.html). 

### NEWS.md

### LICENSE

### README

### .Rbuildignore



## Testing



