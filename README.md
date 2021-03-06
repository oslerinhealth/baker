
<!-- README.md is generated from README.Rmd. Please edit that file -->

## **baker**: Bayesian Analysis Kit for Etiology Research

> An R Package for Fitting Bayesian [Nested Partially Latent Class
> Models](https://academic.oup.com/biostatistics/article/18/2/200/2555349/Nested-partially-latent-class-models-for-dependent)

[![Build
Status](https://travis-ci.org/zhenkewu/baker.svg?branch=master)](https://travis-ci.org/zhenkewu/baker)
[![AppVeyor build
status](https://ci.appveyor.com/api/projects/status/github/zhenkewu/baker?branch=master&svg=true)](https://ci.appveyor.com/project/zhenkewu/baker)
[![Coverage
status](https://codecov.io/gh/zhenkewu/baker/branch/master/graph/badge.svg)](https://codecov.io/github/zhenkewu/baker?branch=master)

**Maintainer**: Zhenke Wu, <zhenkewu@umich.edu>

**Issues** Please click [here](https://github.com/zhenkewu/baker/issues)
to report reproducible issues.

**References**: If you are using **baker** for population and individual
estimation from case-control data, please cite the following papers:

|                                      | Citation                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Paper Link                                                                                                                 |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| partially Latent Class Models (pLCM) | Wu, Z., Deloria-Knoll, M., Hammitt, L. L., Zeger, S. L. and the Pneumonia Etiology Research for Child Health Core Team (2016), Partially latent class models for case???control studies of childhood pneumonia aetiology. *J. R. Stat. Soc. C*, 65: 97???114. <doi:10.1111/rssc.12101>                                                                                                                                                                                                                                                                                                                         | [Link](http://onlinelibrary.wiley.com/doi/10.1111/rssc.12101/full)                                                         |
| nested pLCM                          | Wu, Z., Deloria-Knoll, M., Zeger, S.L.; Nested partially latent class models for dependent binary data; estimating disease etiology. *Biostatistics* 2017; 18 (2): 200-213. doi: 10.1093/biostatistics/kxw037                                                                                                                                                                                                                                                                                                                                                                                              | [Link](https://academic.oup.com/biostatistics/article/18/2/200/2555349/Nested-partially-latent-class-models-for-dependent) |
| nested pLCM regression               | Wu, Z., Chen, I (2020). Probabilistic Cause-of-disease Assignment using Case-control Diagnostic Tests: A Hierarchical Bayesian Approach. *Statistics in Medicine*. To Appear. <DOI:10.1002/sim.8804>.                                                                                                                                                                                                                                                                                                                                                                                                      | [Link](https://doi.org/10.1101/672808)                                                                                     |
| Application                          | Maria Deloria Knoll, Wei Fu, Qiyuan Shi, Christine Prosperi, Zhenke Wu, Laura L. Hammitt, Daniel R. Feikin, Henry C. Baggett, Stephen R.C. Howie, J. Anthony G. Scott, David R. Murdoch, Shabir A. Madhi, Donald M. Thea, W. Abdullah Brooks, Karen L. Kotloff, Mengying Li, Daniel E. Park, Wenyi Lin, Orin S. Levine, Katherine L. O???Brien, Scott L. Zeger; Bayesian Estimation of Pneumonia Etiology: Epidemiologic Considerations and Applications to the Pneumonia Etiology Research for Child Health Study, *Clinical Infectious Diseases*, Volume 64, Issue suppl\_3, 15 June 2017, Pages S213???S227 | [Link](https://academic.oup.com/cid/article/64/suppl_3/S213/3858226/Bayesian-Estimation-of-Pneumonia-Etiology)             |
| Primary PERCH Analysis               | The PERCH Study Group (2019). Aetiology of severe hospitalized pneumonia in HIV-uninfected children from Africa and Asia: the Pneumonia Aetiology Research for Child Health (PERCH) Case-Control Study. *The Lancet*, In press.                                                                                                                                                                                                                                                                                                                                                                            | [Link]()                                                                                                                   |

## Table of content

<div id='id-section1'/>

-   [1. Installation](#id-section1)
-   [2. Vignettes](#id-section2)
-   [3. Graphical User Interface (GUI)](#id-section3)
-   [4. Analytic Goal](#id-section4)
-   [5. Comparison to Other Existing Solutions](#id-section5)
-   [6. Details](#id-section6)
-   [7. Platform](#id-section7)
-   [8. Connect `R` to `JAGS` on Unix systems or OSX](#id-section8)
-   [9. Submit Jobs to Computing Cluster via a shell
    script](#id-section9)
-   [10. Connect `R` to `JAGS` on Windows](#id-section10)
-   [11. Example Datasets](#id-section11)

<div id='id-section1'/>

## Installation

``` r
# install.packages("devtools",repos="https://cloud.r-project.org")
devtools::install_github("zhenkewu/baker")
```

Note:

-   run `install.packages("pbkrtest")` for `R(>=3.2.3)` if this package
    is reported as missing.
-   Windows User: use
    `devtools::install_github("zhenkewu/baker",INSTALL_opts=c("--no-multiarch"))`
    instead if you see an error message
    `ERROR: loading failed for 'i386'` (Thanks Chrissy!).

<div id='id-section2'/>

## Vignettes

``` r
devtools::install_github("zhenkewu/baker", build_vignettes=TRUE) # will take extra time to run a few examples.
browseVignettes("baker")
```

<div id='id-section3'/>

## Graphical User Interface (GUI)

``` r
# install.packages("devtools",repos="http://watson.nci.nih.gov/cran_mirror/")
devtools::install_github("zhenkewu/baker")
shiny::runApp(system.file("shiny", package = "baker"))
```

For developers interested in low-level details, here is a pretty awesome
[visualization](https://stackoverflow.com/questions/44143110/visualizing-r-function-dependencies)
of the function dependencies within the package:

``` r
library(DependenciesGraphs) # if not installed, try this-- devtools::install_github("datastorm-open/DependenciesGraphs")
library(QualtricsTools) # devtools::install_github("emmamorgan-tufts/QualtricsTools")
dep <- funDependencies('package:baker','nplcm')
plot(dep)
```

You will get a dynamic figure. A snapshot is below:

![](inst/figs/nplcm_functional_dependence.png)

<div id='id-section4'/>

## Analytic Goal

-   To study disease etiology from case-control data from multiple
    sources that have measurement errors. If you are interested in
    estimating the population etiology pie (fraction), and the
    probability of each cause for individual case, try `baker`.

<div id='id-section5'/>

## Comparison to Other Existing Solutions

-   Acknowledges various levels of measurement errors and combines
    multiple sources of data for optimal disease diagnosis.
-   Main function: `nplcm()` that fits the model with or without
    covariates.

<div id='id-section6'/>

## Details

1.  Implements hierarchical Bayesian models to infer disease etiology
    for multivariate binary data. The package builds in functionalities
    for data cleaning, exploratory data analyses, model specification,
    model estimation, visualization and model diagnostics and
    comparisons, catalyzing vital effective communications between
    analysts and practicing clinicians.
2.  `baker` has implemented models for dependent measurements given
    disease status, regression analyses of etiology, multiple imperfect
    measurements, different priors for true positive rates among cases
    with differential measurement characteristics, and multiple-pathogen
    etiology.
3.  Scientists in [Pneumonia Etiology Research for Child
    Health](http://www.jhsph.edu/research/centers-and-institutes/ivac/projects/perch/)
    (PERCH) study usually refer to the etiology distribution as
    ???*population etiology pie*??? and ???*individual etiology pie*??? for
    their compositional nature, hence the name of the package.

<div id='id-section7'/>

## Platform

-   The `baker` package is compatible with OSX, Linux and Windows
    systems, each requiring a slightly different setup as described
    below. If you need to speed up the installation and analysis, please
    contact the maintainer or chat by clicking the `gitter` button at
    the top of this README file.

<div id='id-section8'/>

## Connect `R` to `JAGS`/`WinBUGS`

#### Mac OSX 10.11 El Capitan

1.  Use [Just Another Gibbs Sampler
    (JAGS)](http://mcmc-jags.sourceforge.net/)
2.  Install JAGS 4.2.0; Download
    [here](https://sourceforge.net/projects/mcmc-jags/files/JAGS/4.x/Mac%20OS%20X/)
3.  Install `R`; Download from [here](https://cran.r-project.org/)
4.  Fire up `R`, run `R` command `install.packages("rjags")`
5.  Run `R` command `library(rjags)` in R console; If the installations
    are successful, you???ll see some notes like this:

``` r
>library(rjags)
Loading required package: coda
Linked to JAGS 4.x.0
Loaded modules: basemod,bugs
```

-   Run `R` command `library(baker)`. If the package `ks` cannot be
    loaded due to failure of loading package `rgl`, first install X11 by
    going [here](https://www.xquartz.org/releases/XQuartz-2.7.11.html),
    followed by

``` r
install.packages("http://download.r-forge.r-project.org/src/contrib/rgl_0.95.1504.tar.gz",repo=NULL,type="source")
```

#### Unix (Build from source without administrative privilege)

Here we use [JHPCE](https://jhpce.jhu.edu/) as an example. [The complete
installation
guide](https://sourceforge.net/projects/mcmc-jags/files/Manuals/4.x/)
offers extra information.

1.  Download source code for [JAGS
    4.2.0](https://sourceforge.net/projects/mcmc-jags/files/JAGS/4.x/Source/JAGS-4.2.0.tar.gz/download);

2.  Suppose you???ve downloaded it in `~/local/jags/4.2.0`. Follow the
    bash commands below:

    ``` bash
    # change to the directory with the newly downloaded source files:
    cd ~/local/jags/4.2.0

    # create a new folder named "usr"
    mkdir usr

    # decompress files:
    tar zxvf JAGS-4.2.0.tar.gz

    # change to the directory with newly decompressed files:
    cd ~/local/jags/4.2.0/JAGS-4.2.0



    # specify new JAGS home:
    export JAGS_HOME=$HOME/local/jags/4.2.0/usr
    export PATH=$JAGS_HOME/bin:$PATH

    # link to BLAS and LAPACK:
    # Here I have used "/usr/lib64/atlas/" and "/usr/lib64/" on JHPCE that give me
    # access to libblas.so.3 and liblapack.so.3. Please modify to paths on your system.
    LDFLAGS="-L/usr/lib64/atlas/ -L/usr/lib64/" ./configure --prefix=$JAGS_HOME --libdir=$JAGS_HOME/lib64 

    # if you have 8 cores:
    make -j8
    make install

    # prepare to install R package, rjags:
    export PKG_CONFIG_PATH=$HOME/local/jags/4.2.0/usr/lib64/pkgconfig 

    module load R
    R> install.packages("rjags")
    # or if the above fails, try:
    R>install.packages("rjags", configure.args="--enable-rpath")
    ```

3.  Also check out the
    [INSTALLATION](https://CRAN.R-project.org/package=rjags/INSTALL)
    file for `rjags` package.

<div id='id-section9'/>

## Submitting Jobs to Computing Cluster via a shell script

Again, I use JHPCE as an example.

``` bash
#!/bin/bash
#$ -M zhenkewu@gmail.com
#$ -N baker_regression_perch
#$ -o /users/zhwu/baker_regression/data_analysis/baker_regression_test.txt
#$ -e /users/zhwu/baker_regression/data_analysis/baker_regression_test.txt

export JAGS_HOME=$HOME/local/jags/4.2.0/usr
export PATH=$JAGS_HOME/bin:$PATH

export LD_LIBRARY_PATH=$JAGS_HOME/lib64

cd /users/zhwu/baker_regression/data_analysis
#$ -cwd

echo "**** Job starts ****"
date
echo "**** JHPCE info ****"
echo "User: ${USER}"
echo "Job id: ${JOB_ID}"
echo "Job name: ${JOB_NAME}"
echo "Hostname: ${HOSTNAME}" 

Rscript real_regression_data_jhpce.R

echo "**** Job ends ****" 
date
```

<div id='id-section10'/>

#### Windows

-   JAGS 4.2.0

1.  Install `R`; Download from [here](https://cran.r-project.org/)
2.  Install [JAGS
    4.2.0](https://sourceforge.net/projects/mcmc-jags/files/JAGS/4.x/Windows/);
    Add the path to JAGS 4.2.0 into the environmental variable
    (essential for R to find the jags program). See
    [this](http://superuser.com/questions/949560/how-do-i-set-system-environment-variables-in-windows-10)
    for setting environmental variables;

-   alternatives are `brew install -v jags` for OSX,
    `sudo apt-get install jags` for Ubuntu/Debian

1.  Fire up `R`, run `R` command `install.packages("rjags")`
2.  Install [`Rtools`](https://cran.r-project.org/bin/windows/Rtools/)
    (for building and installing R pacakges from source); Add the path
    to `Rtools` (e.g.??`C:\Rtools\`) into your environmental variables so
    that R knows where to find it.

<!-- - [WinBUGS 1.4.3](http://www.mrc-bsu.cam.ac.uk/software/bugs/the-bugs-project-winbugs/) -->
<!--     1. Install the [patch](http://www.mrc-bsu.cam.ac.uk/software/bugs/the-bugs-project-winbugs/the-bugs-project-winbugs-patches/) -->
<!--     2. Install the WinBUGS 1.4.x [immortality key](http://www.mrc-bsu.cam.ac.uk/software/bugs/the-bugs-project-winbugs/) -->
<div id='id-section11'/>

#### Datasets

We provide two datasets for exploratory use with the `baker` package.

1.  `data_nplcm_reg`: a dataset containing BrS measurements,
    case-control status, and regression covariates (testing site and
    enrollment date). This dataset was generated using the
    `simulate_nplcm` function. We also provide the BrS measurements,
    case-control status, and regression covariates (testing site and
    enrollment date). Code to fit the NPLCM to this dataset is in the
    accompanying software paper and the full code used to produce this
    dataset is available upon request. Using this dataset and the
    functionality in `baker`, a user can reproduce Figures 7 and 8 in
    the accompanying software paper.

2.  `baker_posterior_samples_example`: a folder which contains the
    output of an NPLCM fitted to real data. We are not able to provide
    the real data due to privacy restrictions. Instead, we provide:

    -   1.  the posterior samples, which can be found in
            `CODAchain1.txt` and `CODAindex.txt`.

    -   1.  the covariates used in fitting the model (`ENRLDATE` and
            `AGE`), which can be found in `data_nplcm.txt`. Note that
            this folder can be found here [to be added]()

Using the posterior samples in this folder, Figure 10 of the software
paper can be replicated. If you would like to use `baker` visualization
functions on this data, please download the compressed folder directly
to your local drive, so that the path to the folder containing these
`.txt` files can be provided as an argument for the plotting functions.
