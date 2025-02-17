---
title: "Tutorial 1: R, R-Studio & R-Studio Cloud"
subtitle: <h5 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
output: 
  html_document:
    toc: true
    toc_depth: 3
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


## Tutorial 1 Contents

This tutorial is all about the R and R-Studio programmes, along with the things you will need to complete your lab

 - [**Tutorial 1A: What are R and R studio?**](#Tut1A_WhatisR)

 - [**Tutorial 1B. Accessing R and R-studio**](#Tut1B_Install)
 
      a. [Installing R/R-studio on your computer](#Tut1Ba_Desktop)
      b. [Using R-studio cloud as an alternative](#Tut1Bb_Cloud)
      c. [Lab computers and the TLT server](#Tut1Bc_Campus)
      <br><br>

 - [**Tutorial 1C. Going between RStudio-Cloud and desktop**](#Tut1C_Transfer)
 
<br>
<br>

## Tutorial 1A: What are R and R studio? {#Tut1A_WhatisR}

There are two programmes needed to run R on your computer, "R" and "R-Studio".  R teaches the computer to "speak" in the language R.  R-studio is just a nicer place to edit code.

<br>

### What is R

**R** is a programming language commonly used by statisticians and scientists across the world.  By a "programming language", I mean it is a collection of commands that you can type into the computer in order to analyse and visualise data.  

As described by Noli Brazil:"R is a free, open source statistical programming language.  It is useful for data cleaning, analysis, and visualization. R is an interpreted language, not a compiled one. This means that you type something into R and it does it." 

The easiest way I find to think about R is that it is literally a language, like Spanish or Hindi, that is spoken by your computer. Learning R means learning vocabulary and grammar in order to communicate. It also means it will get easier with experience and practice..

<br>

##### **What happens when you install R?**

When you install R on your computer, you are essentially instantly teaching your computer to “speak in R” with some very basic Notepad-like software where you can enter commands."*

<div class="figure">
<img src="pg_Tut1_about_fig1.png" alt="*The basic R console. You write in blue, the computer replies in black. The &gt; means it is waiting for a command*" width="1686" />
<p class="caption">*The basic R console. You write in blue, the computer replies in black. The > means it is waiting for a command*</p>
</div>

<br>

### What is R-Studio?
 
More recently, **R-studio** has been designed as a piece of software to make it easier to programme in R. 

It’s Microsoft Word is compared to notepad; many more options and things to click. For example, you can easily see help files, run code, see your output and edit interactive visualisations.  R-Studio also allows us to make interactive documents called R-Markdown files.  


<div class="figure">
<img src="pg_Tut1_about_fig2.png" alt="*R-studio is much more sophisticated*" width="2848" />
<p class="caption">*R-studio is much more sophisticated*</p>
</div>

To learn more about R studio, see here: https://www.rstudio.com/products/rstudio/ (1 minute video), or a slightly longer one here:


```{=html}
<div class="vembedr">
<div>
<iframe src="https://www.youtube.com/embed/SdMPh5uphO0" width="533" height="300" frameborder="0" allowfullscreen="" data-external="1"></iframe>
</div>
</div>
```

You can also see more about the interactive R Markdown documents we will be making here:


```{=html}
<div class="vembedr">
<div>
<iframe class="vimeo-embed" src="https://player.vimeo.com/video/178485416" width="533" height="300" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="" data-external="1"></iframe>
</div>
</div>
```


<br>
<br>

<div style="margin-bottom:25px;">
</div>
## Tutorial 1B. Accessing R and R-studio {#Tut1B_Install}

For this course you will need BOTH R and R studio.  There are three ways we can access these

a. [Installing R/R-studio on your computer](#Tut1Ba_Desktop) (Recommended)
b. [Using R-studio cloud as an alternative](#Tut1Bb_Cloud) (Recommended)
c. [Lab computers and the TLT server](#Tut1Bc_Campus) (NOT recommended)

<br>

### 1B.a. Installing R/R-studio {#Tut1Ba_Desktop}

R is free and having it on your own computer will give you a lot more freedom to complete the labs, especially if there is social distancing later in the semester.

**If you already have R and/or R-Studio, it is very important you update both of them to the most recent version.**  The easiest way to do this is to first uninstall both programmes, then re-install fresh.  If you are worried this will affect another class, chat with Dr Greatrex before starting out..

<br> 

##### **To install R:**

  1. On a windows machine, go to: https://cloud.r-project.org/bin/windows/base/ , download R v 4.1.1 and double click to install (click next through all the options)
  
  2. On a Mac, go to: https://cloud.r-project.org/bin/macosx/ , download the R v 4.1.1 package and double click to install (click next through all the options)
  
  3. On anything else: https://cloud.r-project.org/bin

<br> 

<div style="margin-bottom:25px;">
</div> 
##### **To install R-Studio:**

1. Go to the website here: https://www.rstudio.com/products/rstudio/download/#download and download the version for your operating system.

   _**For Windows Users**: Sometimes R asks you to download something called RTools.  You can ignore this request as it is not relevant to our course.  If you really want the warning to go away, you can download Rtools here https://cran.r-project.org/bin/windows/Rtools/  Follow the instructions closely and ask if you need support._

<br>

<p class="comment">**Your R AND R-Studio MUST be up to date, or things wont' work**. R should be a minimum of 4.1.2 (2021-11-01) -- "Bird Hippie" and R-studio a minimum of Version 1.4.1717</p>


<div style="margin-bottom:25px;">
</div> 
### 1B.b. Using R-studio cloud {#Tut1Bb_Cloud}

You can access both R and R-studio online without installing anything.  

You can access R-studio Cloud anywhere and I believe is free for the first 25hrs each month, then $5 a month.  You also get a total of 50 projects which should be fine given we only have 8 labs and 1 project.

1. To do this, make an account at  https://rstudio.cloud/plans/free.  

You can also easily move files from the Cloud to your Desktop, so for example, you can work on the cloud during lab hours and on your desktop at home.  You can find instructions in [Tutorial A3. Transfer betweeen Cloud & Desktop](#TutA3_Transfer)

<br>

<div style="margin-bottom:25px;">
</div> 
### 1B.c. Lab computers and the TLT server {#Tut1Bc_Campus}

The geography lab computers should have the most up to date version of R, but sometimes the "packages" you will later install fill up your U-drive.  Equally, the version of R *outside* the geography lab room is going to be out of date and will likely cause issues. Saying that, R and R-Studio are R installed on them & we have made it work in the past.

There is also a free Penn State server called the TLT server (also a second called the science server).  In both cases R studio is out of date, which will likely cause issues.

*If you go down these routes, proceed with care and talk to Dr Greatrex first*

<br>
<br>

<div style="margin-bottom:25px;">
</div> 
## Tutorial 1C. Cloud - Desktop Transfers {#Tut1C_Transfer}

R-Projects mean you can complete your labs either on your laptops, or on R-Studio Cloud, then easily transfer between the two.

<br>

### To go from R-Studio Cloud to R-Desktop

1. On your computer, go to your GEOG364 folder (or make one!)
2. Make a subfolder named for that lab e.g. *Lab 1*
3. On your browser, open your project in R-studio cloud
4. In the files quadrant/tab, select the checkbox of all the files.
5. Click Export.  This will zip them into a folder.  Save that into your lab folder
6. Unzip. Double click the project.RProj file to reopen your lab on your computer

<img src="pg_Tut1_about_fig3.png" width="2716" />


<br>


### To go from R-Desktop to R-Studio Cloud

1. On your browser, in R studio cloud make a new project and name it something relevant
2. Click the upload button
3. Navigate to the lab folder on your computer.  Choose ONLY the .Rmd file(s) and any input data as appropriate (RStudio-Cloud will make the rest)
4. Click on the .Rmd file name in the files in RStudio and you're good to go


<br>



<img src="pg_Tut1_about_fig4.png" width="2906" />

<br>


<img src="pg_Tut1_about_fig5.png" width="70%" />


<br>


<img src="pg_Tut1_about_fig6.png" width="70%" />

<br>
<br>


***

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
