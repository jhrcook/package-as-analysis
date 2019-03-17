


# Workflow

### Document


```r
devtools::document()
```


### Test


```r
devtools::test()
```


### Build and Install

Step one is to build and install the package. This can be done in RStuido with the hot-keys XXX. Otherwise, there is the "Build" button in the "Build" pane. If not using RStudio, then 'devtools' or the command line can be used. the `install()` function *builds* and *installs* the package.


```r
devtools::install()
```

 If (for some strange reason) only the build *or* install is desired, these two functionalities can be separated.
 

```r
devtools::build()
devtools::install(build = FALSE)
```
 

At the command line.

```bash
R CMD build ExampleAnalysisPackage



R CMD INSTALL ExampleAnalysisPackage_0.0.0.9000.tar.gz



```


### Check


```r
devtools::check()
```

```bash
R CMD check ExampleAnalysisPackage_0.0.0.9000.tar.gz
```

