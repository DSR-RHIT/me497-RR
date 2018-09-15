
# centering figures and captions

R Markdown does not have a native method for centering figures and
captions in docx output. In this tutorial, I modify a predefined Word
*style* to center figures and captions.

## word styles

In R Markdown, you control the formatting of a Word document output by
modifying predefined Word styles. For more information on creating and
editing the reference styles file generally, see my article [Happy
collaboration with Rmd to
docx](http://rmarkdown.rstudio.com/articles_docx.html).

For centering figures and captions, I suggest modifying the rarely used,
predefined *Heading 6* style in the same way that Norbert Köhler, in his
article [R Markdown: How to insert page breaks in a MS Word
document](http://datascienceplus.com/r-markdown-how-to-insert-page-breaks-in-a-ms-word-document/),
suggests dedicating the rarely used, predefined *Heading 5* style for
inserting page breaks.

## getting started

Prepare the following files:

  - An image saved in PNG format or other docx-compatible format
  - A reference styles file, e.g., `my-styles.docx`
  - Your Rmd to docx script with the reference styles file specified in
    the YAML header, e.g.,

<!-- end list -->

``` 
    ---
    output:
      word_document:
         reference_docx: my-styles.docx
    ---
```

## modify heading 6

  - Open the Rmd script  
  - At the location where you wish to insert the image, type the 6
    hashtags that indicate a level-6 heading, and repeat on the next
    line.
  - Add some temporary text, for example,

<!-- end list -->

``` 
    ###### the figure will go here 
    ###### the caption will go here
```

  - Save and Knit
  - In the Word doc that appears, select the lines formatted with the
    Heading 6 style
  - Modify the style to be centered on the page
  - Modify the typeface as desired for figure captions
  - Save As the new version of the reference styles file,
    `my-styles.docx`
  - Close the docx file

## import the first image

In the Rmd script, replace the two temporary lines:

  - heading-6, line 1, import the image
  - heading-6, line 2, the figure caption

<!-- end list -->

``` 
    ###### ![](my-image.png) 
    ###### Figure 1: Caption for my image 
```

  - Save and Knit.

## subsequent images

For subsequent centered images, use the heading-6 markup again, e.g.,

``` 
    ###### ![](my-next-image.png) 
    ###### Figure 2: Caption for my next image 
```

-----

[main page](../README.md)
