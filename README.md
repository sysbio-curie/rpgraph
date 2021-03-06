The package rpgraph allows constructing, manipulating and analysing principal graphs in R. The code is relies on the Java functions written by [Andrei Zynoviev](https://github.com/auranic) available in the java library [VDAOEngine](https://github.com/auranic/VDAOEngine). The R code interfaces with the java library via the [`rJava` package](https://www.rforge.net/rJava/). A MATLAB implementation of elastic principal graphs developed and mainteined by Andrei Zynoviev is available [here](https://github.com/auranic/Elastic-principal-graphs).

An essential overview of Pircipal elastic circles
-------------------------------------------------

For an overview of theory behind principal graphs see [description provided by Andrei](https://github.com/auranic/Elastic-principal-graphs/wiki). Further details will be presented here in a future update.

rpgraph prerequisite and installation
-------------------------------------

The package is currently under heavy development, non very well documented, and only available on GitHub. A functional Java Virtual machine for your system is necessary. **Before** installing the package, it is advisable to install `rJava` from sources by using

``` r
install.packages(pkgs = "rJava", repos="http://rforge.net", type = 'source')
```

Compiling from source requires the appropriate development tools, e.g., C/C++ compiler. The installation of the package requires the `devtools` package, which is available from CRAN. The `rpgraph` package can be installed using

``` r
install.packages("devtools")
library(devtools)
install_github("Albluca/rpgraph")
```

To take advantage of all the feature of the package, it is advisable to also install (not necessary from source in this case) `bigpca`, `flashpcaR`, `irlba`, `nsprcomp`, and `plotly`.

`flashpcaR` is available from GitHub

``` r
library(devtools)
install_github("gabraham/flashpca")
```

The other packages can be found on CRAN.

``` r
install.packages(c("bigpca", "flashpcaR", "irlba", "nsprcomp", "plotly")
```

Workaround for common problems
------------------------------

The installation and loading of `rJava` is known to be problematics under certain circumstances on MacOS. A number of workaround can be found on the [internet](http://conjugateprior.org/2014/12/r-java8-osx/). Possible solutions include recompiling the package, setting certain environment variables manually, ~ and changing the operating system~. Most of the times the problem is connected with the package struggling to find the appropriate information in the global environment.

If `rJava` fails to load try typing

``` r
options("java.home"="/Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/jre")
dyn.load('/Library/Java/JavaVirtualMachines/jdk1.7.0_79.jdk/Contents/Home/jre/lib/server/libjvm.dylib')
```

before loading the library. These lines may need to get adjusted depending on the version of the virtual machine that the user intendt to use.

Basic functionalities
---------------------

The basic functionality of rpgraph is provided by the `computeElasticPrincipalGraph` function, which can be used to cmpute a list of principal graphs. For each principal graph is then possible to obtain debug information (`plotMSDEnergyPlot` and `accuracyComplexityPlot`) and to plot the result in 2 and 3 dimensions (`plotData2D`, `plotPieNet`, `plotData3D`). The principal graph can also be converted into a igraph network (`ConstructGraph`).

The points a set of points can be projected on the principal graph with the same number of dimensions in two different ways. Using `TaxonList` it is possible to obtains a list of points associated with each node of the graph, while using `projectPoints` is it possible to project the points on the edges. Note that, expecially in high dimensional spaces, it is possible tha a point is projected on an nodes instead of an edge. More details on this will be available in future updates.

Once the points have been projected on the edges, it is possible to order them on a path using the fucntion `OrderOnPath`. This allows for the derivation of a *pseudo time* across the points.

Examples
--------

The package contains a few example datasets that can be used to test its functionalities.

Specific documents describe the derivation of [principal curves](doc/curve.md), [pringipal circles](doc/circle.md), and [principal trees](doc/tree.md).

Also available are a tutorial on the step-by-step derivation of a graph [available](doc/step.md), a few examples describing how the different topologies can be [combined](doc/mix.md), and a description of the [projection procedure](doc/proj.md).

While the default construction parameters are often ok, it is also possible to change the behaviour of the java functions as documented [here](doc/javapar.md).

Biological applications
-----------------------

The package will provide functions that can be used to study biological processes with principal graphs. An interface to study cell cycle is currently being tested and will be available soon.
