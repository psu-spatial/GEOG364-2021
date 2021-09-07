---
title: "Tutorial 6: Input/Output"
subtitle: <h5 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
output: 
  html_document:
    toc: true
    toc_depth: 4
    toc_float: true
    theme: flatly
---


<style>
p.comment {
background-color: #DBDBDB;
padding: 10px;
border: 1px solid black;
margin-left: 0px;
border-radius: 5px;
font-style: normal;
}

h1.title {
  font-weight: bold;
  font-family: Arial;  
}

h2.title {
  font-family: Arial;  
}

</style>


<style type="text/css">
#TOC {
  font-size: 12px;
  font-family: Arial;
}
</style>

\



## Tutorial 6: Input/Output

This tutorial is all about reading in and saving files

 - [**Tutorial 6A: Reading in Excel Files**](#Tut6a_Excel)

<br>

 
## Tutorial 6A: Reading in Excel Files {#Tut6a_Excel}

R can easily read in Microsoft Excel spreadsheets using the `readxl` package:

<br>

### Basic approach

1. **Make sure the readxl package is loaded.**<br>E.g. is `library(readxl)` in your library code chunk?<br>Have you run the code chunk?

<br>

2. **Place your excel file in your project folder**.<br>E.g. for Lab 2, place *frostdays.xlsx* into your Lab 2 project folder.  

<br>

3. **Make a new code chunk and add the read_excel() command e.g.**<br>
   
   ```r
   frost <- read_excel("frostdays.xlsx")
   ```
   Here the command is `read_excel()`, you are applying this to "frostdays.xlsx" (e.g. reading in that file), then assigning the result to a variable called frost.

<br>

If this works, there should be no errors and nothing prints on the screen when you run the code chunk.  

In the environment tab, frost should have appeared with a description as a table with 76 rows (observations/obs), and 7 columns (variables).  In R, this type of table/spreadsheet is called a `data.frame`.

<br>

### Troubleshooting

**It says it can't find the file:**
 - Are you running the right project? e.g. does it say Lab 2 at the top of the screen?
 - Did you put the file into your Lab 2 folder?
 - Did you spell it right and include the full .xslx extension?
 - Did you use quote marks?
 
**It says read_excel doesn't exist**
 - Did you install the readxl package?
 - Did you load the readxl package? Go click the code chunk with the library command again!
 - Did you spell the command right? (case sensitive)
 - Did you use () afterwards so R understands that it's a command?

<br>

### Using the wizard.

Sometimes you just can't get it working.  In those cases, try the import wizard.

1. Go to the file menu at the very top of the screen. Click import dataset, then From Excel. Use the wizard to find your file and get it looking correct. It will show you the code you need in the code preview

<br>

2.  Because we want to include this file in the markdown, rather than pressing OK, copy the code preview text and put it in your code chunk.











<br>
<br>


***

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
