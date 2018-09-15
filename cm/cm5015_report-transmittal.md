
# preparing a report for transmittal

When sharing a report file with someone, the type of file I send them
depends on the circumstances.

  - collaborator using RR practices  
  - collaborator using Office software
  - client

## collaborator using RR practices

If my collaborator is using reproducible practices, I can simply invite
them to join my GitHub repo. They can suggest changes, make a pull
request that I can review, accept, or reject.

## collaborator using Office software

If my collaborator is a Word-Excel-PPT user, I send them the `.docx`
file. They will typically make revisions using the Word track changes
feature, send them back to me, and I have to take the time to
incorporate their changes in my “master” script. This adds time to the
my workflow, but keeps any document for which I’m responsible
reproducible.

## client

My usual practice is to make a copy of the `docx` file, rename it, then
manually convert it to a PDF file that I can send electronically to the
client. When creating the PDF, I add the transmittal date to the file
name.

``` r
# make a copy of the docx file
file.copy(from = "reports/06_calibr_report.docx", to = "reports/06_calibr_report_copy.docx"
)
```

Learn R

  - `file.copy()` is one of several file management functions in R
  - Type `?files` in the Console to browse other file manipulation
    functions in R
  - add `include = FALSE` to the code chunk header to prevent R from
    printing an output message from this code chunk

On my machine, to create the PDF,

  - Manually open the `06_calibr_report_copy.docx` file
  - Print to PDF and edit the file name, e.g.,
    `06_calibr_report_to-client_2016-09-09.pdf`

If later I should edit and knit the report again, the PDF remains
unchanged as a record of the report I sent the client on that date.
