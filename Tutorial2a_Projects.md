---
title: "Tutorial 2: Create your R project"
subtitle: <h4 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
output: 
  html_document:
    toc: true
    toc_depth: 3
    toc_float: true
    theme: flatly
    code_folding: show
---

<style>
p.comment {
background-color: #DBDBDB;
padding: 10px;
border: 1px solid black;
margin-left: 25px;
border-radius: 5px;
font-style: normal;
}


</style>

<style type="text/css">
#TOC {
  font-size: 13px;
  font-family: Arial;
}
</style>


\

Our first job is to create an R-project for your lab. YOU WILL DO THIS EVERY LAB.

### What are projects?

An R project is a special folder that will store everything to do with each lab in one place on your computer.  This is incredibly useful - it means that if you switch from R-Cloud, to the lab computers, to your laptop, all you have to do is to move the folder and everything will just work. Learn more here. 

[![Rproject](Tutorial2_VIDEO1_Projects.png)](https://www.linkedin.com/learning/learning-the-r-tidyverse/why-should-you-use-projects-in-rstudio?u=76811570 "Why use R Projects")

<br>

<div style="margin-bottom:25px;">
</div> 
### Creating your first lab project

<img src="Tutorial1c_fig1_RRstudiologos.png" width="2097" />

<br>

1. If it's not already open, open **R-Studio** 
2. Go to the file menu at the very top and click `New Project` 
3. Select `New Directory`, then `New Project`
4. Name your project *GEOG364-Lab1-Project* 
5. Under "create project as a subdirectory of", hit the browse button and go inside your GEOG-364 main folder (you just need to be in the folder, you don't need to have selected anything). Press open
6. Finally, press `Create Project`

<img src="Tutorial2a_fig2_projectmethod.png" width="1320" />

<br>

<div style="margin-bottom:25px;">
</div> 
#### How do I know it's worked?

R will change slightly.  If you look at the top of the screen in the title bar, it should say *GEOG364-Lab1-Project R Studio*.  

The Files tab should have gone to your project folder.  

<img src="Tutorial2a_fig3_projectcheck.png" width="1690" />

<br>

Essentially, R-Studio is now "looking" inside your Lab 1 folder, making it easier to find your data and output your results.  

If you want one, final check, try typing this into the console (INCLUDING THE EMPTY PARANTHESES/BRACKETS), press enter and see if it prints out the location of Lab 1 on your computer. If not, talk to an instructor.


```r
getwd()
```

<br>

<div style="margin-bottom:25px;">
</div> 
### Returning to your lab project

OK, let's imagine that you get halfway through your lab and your computer dies.  How do you get back to your Lab work?  Try this now.  Close down R-Studio.

To reopen a lab:

1. **DO NOT RE-OPEN R-STUDIO!**
2. Instead navigate on your computer to your *GEOG-364/GEOG364-Lab1-Project* folder.   
3. Double click on the GEOG364-Lab1-Project.RProj file.

This will reopen R for that specific lab, so you can continue where you left off.

It means you can also open several versions of R studio for multiple projects, which can be very useful in keeping labs separate and staying sane.


<img src="Tutorial2a_fig4_reopenproject.png" width="1922" />

<br>

***



Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
