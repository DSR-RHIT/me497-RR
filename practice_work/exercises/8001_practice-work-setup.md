
# practice work

The `practice_work` project is where we’ll put files for learning to use
R for data tidying, analysis, graphs, and reporting—skills you will use
in developing your project work.

We keep these files separate from the project work to reduce the file
clutter in the project folders.

## getting started

Launch your `practice_work` project

  - open a new R Markdown file
  - save it in the `exercises` folder, selecting a deliberate filename,
    for example, I’m using `8002_graphs_3-1-3-2.Rmd`. (All my exercises
    will be in the 8000 series. Your mileage may vary.)

At the top of the file is the YAML header. For exercises, the html
output is OK.

    ---
    title: "graphs 1"
    output: html_document
    ---

Add your name and date.

Add the following in a code chunk. The knitr options set here are to

  - set the knitr root directory one level up to match the project
    working directory
  - show the source code and output from a code chunk in a single block

<!-- end list -->

``` r
library(knitr)
opts_knit$set(root.dir = "../")
opts_chunk$set(echo=TRUE, collapse=TRUE)
```

Work through the examples in the book, duplicating the code from the
book in the Rmd file.

Knit the file regularly and compare your results to those shown in the
book.

The goal is to learn from the activity so you can work the exercises.

The goal of the exercises is learning R.
