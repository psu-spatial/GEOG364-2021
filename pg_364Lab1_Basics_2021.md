---
title: "Lab 1: Introduction to R"
subtitle: <h5 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
author: <h5 style="font-style:normal">Dr Helen Greatrex</h4>
date: <h5 style="font-style:normal">Aug 16, 2021</h4>
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






## Welcome to Lab 1!

There are 8 labs in this course. Each one will build on the last one, with support provided in a series of tutorials (see the tutorials tab).  You should NOT submit the tutorial work. We will work through the tutorials together and then your job is to submit the requirements on this page.

By the end of this week's lab, you will be able to:

1. Get comfortable with the lab format & how to work through them
2. Know how to get help
2. Get familiar with the RStudio interface
3. Run your first programming commands
4. Put everything together into an interactive markdown website (like this guide)
5. Understand the process for submitting assignments

<p class="comment">**Assignment 1 is due by midnight the night before your next lab on Canvas.**  See [here](https://psu.instructure.com/courses/2120046/assignments/13274833) for assignment guidelines & we will cover them in detail here.</p>

<br>  

## Step A: Tutorials

### 1. Set up R and R-Studio

 - Covered during homework 1:  Read [Tutorial 1A](https://psu-spatial.github.io/Geog364-2021/pg_Tut1_about.html).
 - Covered during homework 1:  Install BOTH R and R-Studio, or create an R-Studio Cloud account. This is covered in  [Tutorial 1B](https://psu-spatial.github.io/Geog364-2021/pg_Tut1_about.html).
 - Set up your R and R studio. Work through [Tutorial 2A](https://psu-spatial.github.io/Geog364-2021/pg_Tut2_startup.html) and change your settings.
 
<br>  

### 2. Getting started

 - Use [Tutorial 2B](https://psu-spatial.github.io/Geog364-2021/pg_Tut2_startup.html) to understand what an R-Package is and to install all the code packages/libraries we will need for this course.
 - Use [Tutorial 2C](https://psu-spatial.github.io/Geog364-2021/pg_Tut2_startup.html) to make your first R-project called GEOG364-Lab1-Project
 - Now work through [Tutorial 3](https://psu-spatial.github.io/Geog364-2021/pg_Tut3_basics.html) to get used to the console
 
<br>  
  
### 3. Packages & Markdown basics

 - Work through [Tutorial 4A,4B and 4C](https://psu-spatial.github.io/Geog364-2021/pg_Tut4_markdown.html) to make your first Markdown document

<br>
<br>

## Step B: Actual lab

Everything above was for your own learning.  Now we will start the actual lab you will submit:

<br>  

### 1. Set up
 
 - Inside your R project, create a new RMarkdown document called `GEOG-364-Lab1.Rmd`.


 - Delete all the text below line 11 (e.g. everything from R Markdown onwards)

<br>  

### 2. Adding text

- In the white text area, create a level 1 heading called *"Introduction to GEOG-364"*.  For a cheat sheet to help with this, move your mouse to the top of the page, click the help menu, then click Markdown Quick reference (spaces and whitespace are important!).  If you want to add sub-headings etc, go for it!

 - Leave a blank line, then use the GEOG-364 syllabus to describe the course late policy in your own words (e.g. you're writing about this in the white space).
 
 - Leave a blank line, then write how to contact Dr Greatrex and Susan (e.g. e-mails vs canvas message? office hours?) 

 -  Press "knit" at the top of the screen.  If you haven't made a mistake a pop up should appear with a html file and your edits.

<br>  


### 3. Adding maths and functions


 - Leave another blank line and add a new heading called *"Code Showcase"*.  Add a blank line afterwards too.


 - Create a code chunk.  Inside use R code to calculate the following (Hint, you can put these all in one code chunk, or have separate code chunks with them in.  Just remember to leave blank lines between them)

    + 103^3^  (e.g `103*103*103`, or `103^3`)
  
    + The co-sine of your age (google is your friend, google R function for cosine)
  
    + Use R code to work out how many characters are in [the longest town name in Wales](https://www.bbcamerica.com/anglophenia/2015/09/how-to-pronounce-the-longest-place-name-in-the-u-k) *Llanfairpwllgwyngyllgogerychwyrndrobwllllantysiliogogogoch*.(Hint, remember you can copy paste this into your code. Hint 2.. your tutorials and quote marks!)
  
    + Create a sequence from 1000 to 2000, incrementing by 100 (e.g. 1000,1100,1200...).  Hint, see what google says for R and sequences, or see [here](http://www.simonqueenborough.info/R/basic/lessons/Sequences_of_Numbers.html). 
  
  
 - Press "knit" at the top of the screen.  If you haven't made a mistake a pop up should appear with a html file and your edits.

<br>

### 4. Packages

If you have run through the tutorials, you should have installed all the packages you need for this course.

**IF NOT GO AND DO [Tutorial 2B](https://psu-spatial.github.io/Geog364-2021/pg_Tut2_startup.html)]**

You only need to _download_ the packages once, but we still need to load them every time we need a command in that package (in the same way you only download your banking app once from the app store but need to press the icon every time you want to use it).

WE ALSO NEED TO LOAD THE PACKAGES IN A CODE CHUNK RATHER THAN IN THE CONSOLE.

When you press knit, in the background, your computer makes a new version of R where nothing is loaded, then processes your code.

Today we will be using commands from the skimr package, the ggplot2 package and the plotly package.

Somewhere near the topc of your script, make a new code chunk and add this code. Remember to run the code chunk! (pressing the green arrow, or go to the run button on the top right and press Run All)


```r
library(skimr)
library(ggplot2)
library(plotly)
```

### 5. Data analysis

Part 5 is taken from this tutorial (https://r4ds.had.co.nz/data-visualisation.html). 

Leave a blank line, and create a new heading called *Car Analysis*.  Leave a blank line afterwards too.  

We’re going to work with a table of data that’s already pre-loaded into R inside the ggplot2 package. Make sure you have run the library code chunk.  Now, type the `?mpg` command in the console. This will bring up the help file. If it can't find the dataset, you need to load the ggplot2 package using the library command or install ggplot2.


Read the background of the dataset and briefly summarise it in your file (in the white space).

Now look at the data itself.  In the console, type `View(mpg)`.  This will open a new tab with the spreadsheet itself.  

Let's look at the summary statistics. Leave a blank line and create a new code chunk containing the following code


```r
# mpg comes from the ggplot2 package
# skim comes from the skimr package
skim(mpg)
```


and finally, let's make your first plot.

Among the variables in the mpg dataset are:

 - `displ`, a car’s engine size, in litres.

 - `hwy`, a car’s fuel efficiency on the highway, in miles per gallon (mpg). A car with a low fuel efficiency consumes more fuel than a car with a high fuel efficiency when they travel the same distance.

 - `class`, the class of car e.g. mini, SUV, pick up..
 
To make a nice looking plot, let's use the ggplot package rather than the basic r commands.  Create a code chunk


```r
# ggplotly comes from the plotly package
# Choose the dataset and tell R the columns to plot
p <- ggplot(data = mpg) +                  
     geom_point(mapping = aes(x = displ, y = hwy, color = class)) 

ggplotly(p)  # Plot interactively
```

Now below your code, answer the following questions.

1. What's the unit of observation? (e.g. what does one row in the MPG SPREADSHEET/TABLE correspond to)
2. What is the mean/average manufacturing year of the car models in the dataset?
3. As fully as possible, describe the relationship between car’s engine size and its fuel efficiency on the highway 

If you want to make it neat, you can use sub headings, or bold/italic text (see that R cheatsheet).  Press knit a lot!  Check you haven't made a mistake, check it all works.

<br>


### 6. Above and beyond

Remember that an A is 93%, so you can ignore this section and still easily get an A.

But here is your time to shine. Also, if you are struggling in another part of the lab, you can use this to gain back points.

**To get the final 4 marks in the lab, you need to show me someting new, e.g. you need to go above and beyond the lab questions in some way.** 

 - You get 2/4 for doing something new in any way
 - You get 4/4 for something really impressive or multiple small things.
 
Please tell us in your R script what you did!

Here in lab 1, maybe you added in different text formats to make your lab script more clear (bold/italic etc).  Maybe you worked out how to add axis labels to ggplot (note, it's a pain), maybe you used nested headings or sub-headings, or worked out how to add a table of contents.  

You get 2/4 for doing something new in any way and 4/4 for something really impressive or multiple small things.

<br>
<br>

## C. Submitting your Lab

Remember to save your work throughout and to spell check your writing (next to the save button). Now, press the knit button again. If you have not made any mistakes in the code then R should create a html file in your lab 1 folder which includes your answers. If you look at your lab 1 folder, you should see this there - complete with a very recent time-stamp.

In that folder, double click on the html file.  This will open it in your browser. CHECK THAT THIS IS WHAT YOU WANT TO SUBMIT

Now go to Canvas and submit BOTH your html and your .Rmd file in Lab 1.

<img src="pg_364Lab1_Basics_2021_fig1.png" width="3346" />

<br>

## Lab 1 submission check-list

**HTML FILE SUBMISSION - 8 marks**

**RMD CODE SUBMISSION - 8 marks**

**MARKDOWN/CODE STYLE - 20 MARKS**

Your code and document is neat and easy to read. LOOK AT YOUR HTML FILE IN YOUR WEB-BROWSER BEFORE YOU SUBMIT.  There is also a spell check next to the save button.  You have written your answers below the relevant code chunk in full sentences in a way that is easy to find and grade. For example, you have written in full sentences, it is clear what your answers are referring to. 
    
**Introduction to GEOG-364: 10 MARKS** 

You have described the lab late policy clearly in a way I could share with a new student.

**Code Showcase: 20 MARKS** 

You have managed to successfully complete all the code challenges
 
**Car analysis: 30 MARKS** 

You included all the code and successfully answered the questions, providing reasoning where appropriate

**Above and beyond: 4 MARKS**
 
Here you need to go above and beyond the lab questions in some way.  Here in lab 1, maybe you added in different text formats to make your lab script more clear (bold/italic etc).  Maybe you worked out how to add axis labels to ggplot (note, it's a pain), maybe you used nested headings or sub-headings, or worked out how to add a table of contents.  

You get 2/4 for doing something new in any way and 4/4 for something really impressive or multiple small things.


[100 marks total]


Overall, here is what your lab should correspond to:

<table class=" lightable-classic-2 table table-striped table-hover table-responsive" style='font-family: "Arial Narrow", "Source Sans Pro", sans-serif; margin-left: auto; margin-right: auto; margin-left: auto; margin-right: auto;'>
 <thead>
  <tr>
   <th style="text-align:left;"> Grade </th>
   <th style="text-align:left;"> % Mark </th>
   <th style="text-align:left;"> Rubric </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> A* </td>
   <td style="text-align:left;"> 98-100 </td>
   <td style="text-align:left;"> Exceptional.  Not only was it near perfect, but the graders learned something.  THIS IS HARD TO GET. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> NA </td>
   <td style="text-align:left;"> 96+ </td>
   <td style="text-align:left;"> You went above and beyond </td>
  </tr>
  <tr>
   <td style="text-align:left;"> A </td>
   <td style="text-align:left;"> 93+: </td>
   <td style="text-align:left;"> Everything asked for with high quality.   Class example </td>
  </tr>
  <tr>
   <td style="text-align:left;"> A- </td>
   <td style="text-align:left;"> 90+ </td>
   <td style="text-align:left;"> The odd minor mistake, All code done but not written up in full sentences etc. A little less care </td>
  </tr>
  <tr>
   <td style="text-align:left;"> B+ </td>
   <td style="text-align:left;"> 87+ </td>
   <td style="text-align:left;"> More minor mistakes.  Things like missing units, getting the odd question wrong, no workings shown </td>
  </tr>
  <tr>
   <td style="text-align:left;"> B </td>
   <td style="text-align:left;"> 83+ </td>
   <td style="text-align:left;"> Solid work but the odd larger mistake or missing answer.  Completely misinterpreted something, that type of thing </td>
  </tr>
  <tr>
   <td style="text-align:left;"> B- </td>
   <td style="text-align:left;"> 80+ </td>
   <td style="text-align:left;"> Starting to miss entire/questions sections, or multiple larger mistakes. Still a solid attempt.  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> C+ </td>
   <td style="text-align:left;"> 77+ </td>
   <td style="text-align:left;"> You made a good effort and did some things well, but there were a lot of problems. (e.g. you wrote up the text well, but messed up the code) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> C </td>
   <td style="text-align:left;"> 70+ </td>
   <td style="text-align:left;"> It’s clear you tried and learned something.  Just attending labs will get you this much as we can help you get to this stage </td>
  </tr>
  <tr>
   <td style="text-align:left;"> D </td>
   <td style="text-align:left;"> 60+ </td>
   <td style="text-align:left;"> You attempt the lab and submit something. Not clear you put in much effort or you had real issues </td>
  </tr>
  <tr>
   <td style="text-align:left;"> F </td>
   <td style="text-align:left;"> 0+ </td>
   <td style="text-align:left;"> Didn’t submit, or incredibly limited attempt.  </td>
  </tr>
</tbody>
</table>


***


Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)

