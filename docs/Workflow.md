

# Workflow

## Analysis




## Build and Check

Below is the workflow to use to build and check the package. The frequency of going thorugh this process needs to be calibrated such that it is done often enough to catch errors early on, but not too often to be disruptive to the analysis. I generally go through the process after each major chunk of work - such as a completing vignette - or at the end of the day (if I think it should build).

### Document

The first step is to uild the documentation using 'roxygen2'. In RStudio, the keyboard shortcut is cmd+shift+D. Otherwise, a 'devtools' function can be used from the console.


```r
devtools::document()
```


### Test

Then run the tests to make sure everything still works. Since the tests are written to check that the functions work as expected and not the test the efficiency of the functions, these should be quick tasks, and thus easy to perform often. In RStudio, the keyboard shortcut is cmd+shift+T. Otherwise, a 'devtools' function can be used from the console.


```r
devtools::test()
```


### Build and Install

The package must be built and installed (in the actual R library). This can be done in RStuido with the hot-keys XXX. Otherwise, there is the "Build" button in the "Build" pane. If not using RStudio, then 'devtools' or the command line can be used. the `install()` function *builds* and *installs* the package. In RStudio, the keyboard shortcut is cmd+shift+B. Otherwise, a 'devtools' function can be used from the console.


```r
devtools::install()
```

If (for some strange reason) only the build *or* install is desired, these two functionalities can be separated.
 

```r
devtools::build()
devtools::install(build = FALSE)
```


### Check

The final step is the check the package. In RStudio, the keyboard shortcut is cmd+shift+E. Otherwise, a 'devtools' function can be used from the console.


```r
devtools::check()
```


**Note:** I check the package after building and installing, though Wickham describes that the checking process should be first and only build and install the package after the check is successful. The difference arises because of the use of vignettes. In the vignettes, the package being developed is loaded from the library with `library(ExampleAnalysisPackage)`. Therefore, the version in the library needs to be updated every time. This is a bit annoying, but the build and installation really do not take very long (especially compared to the check) and catch the big errors, anyways.

