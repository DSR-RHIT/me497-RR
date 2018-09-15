
# Rmd to docx: numbering tables and figures

As Norbert Köhler says, “R Markdown has no native method to number and
reference table and figure captions”. The `captioner` packages gives us
a method for auto-numbering figures and tables and automatically
updating the in-text reference numbers as well.

This tutorial is adapted from Norbert Köhler’s [blog
post](http://datascienceplus.com/r-markdown-how-to-number-and-reference-tables/)
plus Andrew Dolman’s
[comments](https://onedrive.live.com/?authkey=%21AApYWBGHNR06Y5I&cid=FCFCD3FD042AF7F1&id=FCFCD3FD042AF7F1%2118306&parId=FCFCD3FD042AF7F1%21322&action=locate)
on that post.

When complete, your output document should be a 2-page docx file with
two tables and two figures with automatically-generated table and figure
numbers.

## install

  - Install the `captioner` package
  - Install the `devtools` package
  - In your Console: `devtools::install_github('yihui/knitr',
    build_vignettes = TRUE)`

The purpose of last line above is to install the latest development
version of `knitr` so we can take advantage of the knitr option
`row.names = FALSE` when using `kable()` to print a table. Plus we get
recent bug fixes.

## getting started

  - Launch your `practiceR` project
  - Open a new Rmd file. Mine is called `test-captioner.Rmd`.
  - Both `word_document` and `html_document` can be used in the YAML
    header.  
  - For `pdf_document`, see the references for additional lines needed.

The YAML header.

    ---
    title: "Testing *captioner*"
    output:
      word_document:
        fig_caption: yes
    ---

The usual setup.

``` r
# the usual setup
library(knitr)
opts_knit$set(root.dir = "../")
opts_chunk$set(echo = TRUE)
```

Load packages.

``` r
# packages  
library(captioner)
library(ggplot2)
library(splines)
```

## assign prefixes

Use `captioner()` to set the prefixes we want to use for our tables and
figures. Here, I’m using the full words. Some folks prefer to use
abbreviations, “Fig.” and “Tab.”.

``` r
# assign the prefixes
auto_tab_ID <- captioner(prefix = "Table")
auto_fig_ID <- captioner(prefix = "Figure")
```

The function names on the left, `auto_tab_ID` and `auto_fig_ID`, are
arbitrary.

## create a table caption

Begin the report. Start with a level 1 heading.

    # Tables 

We create *table captions* using `auto_tab_ID()`. The `name` argument is
a unique string to identify the table prefix and `caption` string.

``` r
# assign the table prefix, number, and caption 
auto_tab_ID(name = "a_table", caption = "A descriptive caption for the table.")
```

The table number (in this case, Table 1) is determined by the order of
appearance of the `auto_tab_ID()` function in the script. This is its
first use, so the table number is “1”.

## refer to the table inline

In a typical technical report, the paragraph just before a table
includes an inline reference to the table. For example:

> An excerpt of data from our fabulous experiment is shown in Table 1.

To construct this sentence, we an inline code chunk and the function
`auto_tab_ID()` with an added argument `display = "cite"` to print the
table number but not the caption.

<pre><code>An excerpt of data from our fabulous experiment is shown in 
<code>`</code>r auto_tab_ID("a_table", display = "cite")<code>`</code>. 
</code></pre>

## kable() the table

Keeping things simple, I’ll use `knitr::kable()` to print data from the
`cars` data set.

The `kable()` function has a `caption` argument we use to invoke the
`auto_tab_ID()` function.

``` r
# get some data
df <- head(cars, n = 5L)

# print the table with caption
kable(df, caption = auto_tab_ID("a_table"), row.names = FALSE)
```

I haven’t printed the table here, but it should appear in your docx
output.

In docx output, table captions are formatted with the *Table Caption*
style. The style can be edited using methods described in [Controlling
Word
Styles](https://github.com/DSR-RHIT/me497-RR/blob/master/cm/cm041_word-styles.md).

## make a second table

I’m going to create another table to demonstrate that the next table is
indeed assigned the number “2”.

``` r
# create a caption for a second table 
auto_tab_ID("another_table", "A boring table.")
```

Having created another caption, I can make an inline reference to the
next table.

> More amazing results are shown in Table 2.

Created using this Rmd script:

<pre><code>More amazing results are shown in 
<code>`</code>r auto_tab_ID("another_table", display = "cite")<code>`</code>. 
</code></pre>

New table:

``` r
# get some data
df <- tail(cars, n = 5L)

# print the table with caption
kable(df, caption = auto_tab_ID("another_table"), row.names = FALSE)
```

All tables are automatically renumbered if tables are added or deleted.

## create a figure caption

Create another level 1 heading.

    # Figures 

Create my first figure caption using
`auto_fig_ID()`.

``` r
auto_fig_ID(name = "one_figure", caption = "An auto-numbered figure caption.")
```

The figure number (in this case, Figure 1) is determined by the order of
appearance of the `auto_fig_ID()` function in the script. This is its
first use, so the figure number is “1”.

## refer to the figure inline

Inline references are typical.

> More amazing results are shown in Figure 1.

Created using this Rmd script:

<pre><code>More amazing results are shown in 
<code>`</code>r auto_fig_ID("one_figure", display = "cite")<code>`</code>. 
</code></pre>

## make a figure

In contrast to table captions, we create *figure captions* using the
`fig.cap` argument inside `{r }` header that starts a code chunk

For example, create a code chunk with these arguments:

<pre><code>```{r fig.cap = auto_fig_ID("one_figure"), fig.height = 3}

<code>```</code></code></pre>

and with this graph code:

``` r
ggplot(data = cars, aes(x = speed, y = dist)) + 
    geom_point() + 
    geom_smooth(method = "lm", formula = y ~ bs(x, 3), se = FALSE)
```

Just for fun, I’ve included a spline fit:

  - `bs()` is a polynomial B-spline from the `splines` package
  - For a complete list of spline functions, use `library(help =
    "splines")`

## make a second figure

Demonstrate the next figure is auto-numbered “2”.

New caption:

``` r
# create a caption for a second figure 
auto_fig_ID("another_figure", "Same data with a linear fit.")
```

New inline reference:

> If we do the same graph with a linear fit, we get Figure 2.

Created using this Rmd script:

<pre><code>If we do the same graph with a linear fit, we get 
<code>`</code>r auto_fig_ID("another_figure", display = "cite")<code>`</code>. 
</code></pre>

New code
chunk:

<pre><code>```{r fig.cap = auto_fig_ID("another_figure"), fig.height = 3}

<code>```</code></code></pre>

with this graph code, using a linear regression instead of a spline.

``` r
ggplot(data = cars, aes(x = speed, y = dist)) + 
    geom_point() + 
    geom_smooth(method = "lm", se = FALSE)
```

That’s all folks\!

## references

1.  Norbert Köhler (2016-10-22) [R Markdown: How to number and reference
    tables](http://datascienceplus.com/r-markdown-how-to-number-and-reference-tables/)
2.  Andrew Dolman (2016) [Testing
    captioner](https://onedrive.live.com/?authkey=%21AApYWBGHNR06Y5I&cid=FCFCD3FD042AF7F1&id=FCFCD3FD042AF7F1%2118306&parId=FCFCD3FD042AF7F1%21322&action=locate)
    from the comments section of Norbert’s blog post.

-----

[main page](../README.md)