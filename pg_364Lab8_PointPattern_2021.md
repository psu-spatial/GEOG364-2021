---
title: "Lab 8: Point Pattern"
subtitle: <h4 style="font-style:normal">GEOG-364 - Spatial Analysis</h4>
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
  font-size: 11px;
  font-family: Arial;
}
</style>





## Welcome to Lab 8!

<br>

Welcome to your final lab, where we are going to focus on Point Pattern Analysis, a specific set of spatial statistics tools we are can use for point datasets. A point dataset can be anything with a specific location, from stars, to greenhouses.

We will be focusing on:

-   Descriptive statistics
-   Density based spatial statistics (Kernel smoothing, quadrat analysis)
-   Distance based spatial statistics ( nearest neighbour analysis and the F, G, K and L functions.)
-   We will also work on downloading raster elevation and population density data

Uniquely for this lab, I am providing most of the code!  Your job is to get it running for a new dataset on fossils and dinosaurs in Pennsylvania.

<br>

See [**your canvas assignment here**](https://psu.instructure.com/courses/2120046/assignments/13274843).

<p class="comment">**Need help?** Add a screenshot/question to the discussion board here: [**LAB 7 DISCUSSION BOARD**](https://psu.instructure.com/courses/2120046/discussion_topics/14125721)</p>

<br><br>

## PART 1: Lab Set-Up & Tutorial

<br>

**YOU WILL NOT BE GRADED ON ANYTHING IN THIS TUTORIAL.<br>THERE SHOULD BE NO CODE/TEXT IN YOUR FINAL REPORT ABOUT IOWAN FARMERS MARKETS!**

<br>

1. Set up your lab 8 project.  If you can't remember, instructions are in [Tutorial 2c](https://psu-spatial.github.io/Geog364-2021/pg_Tut2_startup.html#Tutorial_2C:_Create_an_R-Project) or previous labs.<br><br>

2. Go to Canvas and download the .Rmd with the code, the data file on fossils and the worked example data file on farmers markets in Iowa. Put them in your project folder.<br><br>

3. Use the code provided to work through [Tutorial 12](https://psu-spatial.github.io/Geog364-2021/pg_Tut12_pointpattern.html).  Make sure all the libraries are installed, all the code chunks run, that it knits, and that there are no errors.  <br><br>

   +  This is an excellent time to comment the code and write notes to yourself about what the code does! <br>You will need to understand what is going on for part 2...<br><br>
   
   
4. If there are any issues here, make sure to ask for help ASAP.   

<br><br>

## PART 2: Your analysis

You will be conducting your analysis on a dataset on fossils in Pennsylvania. The data comes from a Paleobiology database that is maintained by an international non-governmental group of paleontologists. 

<br>

**Step 1: Original Data**<br>The data is stored here: https://paleobiodb.org/#/, with a nice interface.  Explore the data and any patterns. Also note how the data was collected and who by. You will need this for step 2..

<br>

**Step 1b: Clear your workspace**<br> You don't want Iowa stuff hanging around. Either click the broom in environment or run this command in the console:


```r
rm(list=ls())
```

<br>

**Step 2: Set up your report**<br>Edit the YAML code in the script so that it looks professional when knitted. At the top (under an appropriate heading), write a brief description of the data, including the scale/unit of analysis, how the data was collected and who by. (remember you can read the data into R and come back to this.. ).  

<br>


**Step 3: Read the data into R**<br>Edit the code so that it reads the fossil data into R, converts it to sf format and sets an appropriate UTM map projection `(remember to look at the column names for the coordinates in the st_as_sf command..)`

<br>

**Step 4: Initial patterns**<br>Make some good looking plots of the points (feel free to change my code).  Write a paragraph on what you might think causes this pattern of dinosaur fossils.  This is a real life example, so feel free to google if you are new to dinosaurs.....

<br>

<p class="comment">**Troubleshooting**. You can run each individual line of code in turn by clicking on it and pressing command-enter / ctrl-enter.<br>If it turns out that you are still seeing Iowa stuff, go back to step 1b, then very slowly run the code from the top, line by line until you discover the error.</p>

<br>

**Step 5: Read in secondary data into R**<br> I wish to know what the pattern of fossils looks like and whether it is determined by elevation (maybe the mountains have different rocks) or population density (more people digging..)<br>

   + Edit the code so that it reads in ACS data for Pennsylvania (your choice if county or census tract) and elevation data.<br>Merge that data with your fossil data. Make some plots of your own (e.g. yours could have different colour scales, better titles, plot different variables) <br><br>
   + If you have other ideas on what causes the pattern, feel free to read in other variables/datasets too (this could count as part of your show me something new..)
   + In the text, comment on whether the secondary data supports your hypotheses/theories about fossil patterns. 
   
   
<p class="comment">**Hint**. If you decide on census tract data, you will need to deal with empty geometries AKA Lab 7.</p>   

<br>


**Step 6:Convert your data to ppp**<br> Keep following the tutorial code to convert your data to ppp.  YOUR CODE SHOULD SUCCESSULLY KNIT AT THIS POINT.  If there are errors, fix them before moving forward <br>In the text explain if your data is marked and what that means.  Also, in your own words, describe the spatstat package itself (you can get the show me something new marks for properly referencing it, see the end for more)


<br>


**Step 7:Conduct a density based analysis** <br> Your analysis should include:

 a. The global point density, written up in the text<br><br>
 b. A quadrat analyses<br><br>
 c. An explanation in the text of why changing the grid size alters the results (e.g. what fallacy are we seeing here?)<br><br>
 d. A hypothesis test of whether the data is unusually distributed compared to one caused by an IRP.<br>*(You have done similar to this before, we will cover in the lecture and a lot of help in the quadrat.test helpfile and online*<br><br>
 e. A Kernel smoothing assessment at a few spatial scales, alongside description in the text that links different spatial scales to the pattern of fossils or things in Pennsylvania. (see my tutorial for Iowa)
 f. A rhohat analysis between the point density, log.population.density and Elevation.  A description in the text of what you found out.
 
 
<p class="comment">You DO NOT have to complete a regression analysis. The code is simply here for those with point projects</p>

 
<br>

**Step 8:Conduct a distance based analysis** <br> Your analysis should include:

 a. A professional histogram of the nearest neighbour distances<br><br>
 b. The global nearest neighbour statistic<br><br>
 c. An L analysis, where you clearly explain in the text what a Monte Carlo process is, and you fully explain the results<br><br>
 

<br>

**Step 9:Show me something new** <br> 

-   You get 2/4 for doing something new in any way
-   You get 4/4 for something really impressive

For example, you could add contours to plots, use different plotting commands than tmap, really improve some tmap plots. You could find out how to reference things properly in R markdown or include a relevant quote (using R markdown quote format) to your fossil analysis.

You could also look at some other point pattern tutorials because they are all linked into spatstat. There are loads of things you could do to build your knowledge of point pattern analysis

 - http://spatstat.org/Melb2018/solutions/solution03.html (density)
 - http://spatstat.org/Melb2018/solutions/solution04.html (poisson)
 - http://spatstat.org/Melb2018/solutions/solution05.html (marked)
 - http://spatstat.org/Melb2018/solutions/solution06.html (K and L functions)
 - https://mgimond.github.io/Spatial/point-pattern-analysis-in-r.html
 - https://bhaskarvk.github.io/user2017.geodataviz/notebooks/02-Static-Maps.nb.html  
 - https://bookdown.org/yihui/rmarkdown-cookbook/bibliography.html
 - https://www.r-bloggers.com/2018/08/how-to-cite-packages/
 
 Remember to say what you did in the report.
 

## F. Submitting your Lab

Remember to save your work throughout and to spell check your writing (left of the knit button). Now, press the knit button again. If you have not made any mistakes in the code then R should create a html file in your lab 8 folder which includes your answers. If you look at your lab 8 folder, you should see this there - complete with a very recent time-stamp.

In that folder, double click on the html file. This will open it in your browser. CHECK THAT THIS IS WHAT YOU WANT TO SUBMIT

Now go to Canvas and submit BOTH your html and your .Rmd file in Lab 8.

<br><br>

## Lab 8 submission check-list

**For all answers: Full marks = everything down at a high standard, in full sentences as appropriate with no parts of your answer missing. Imagine it as an example I use in class**

**HTML FILE SUBMISSION - 5 marks**

**RMD CODE SUBMISSION - 5 marks**

**MARKDOWN STYLE - 10 MARKS**

We will start by awarding full marks and dock marks for mistakes.LOOK AT YOUR HTML FILE IN YOUR WEB-BROWSER BEFORE YOU SUBMIT

TO GET 13/13 : All the below PLUS you use subscripts/superscript as appropriate

TO GET 12/13 - all the below:

-   Your document is neat and easy to read.
-   Answers are easy to find and paragraphs are clear (e.g. you left spaces between lines)
-   You have written in full sentences, it is clear what your answers are referring to.
-   You have used the spell check.
-   You have used YAML code to make your work look professional (themes, tables of contents etc)

**Step 2: Your description of the data: 8 MARKS**

You have thoughtfully described the data and included all the information expected in previous labs, or to allow someone to reproduce it.

**Step 3, 4, 5: Excellent maps: 10 MARKS**

You have made excellent maps and described the spatial patterns in the data and your expectations/theories about what causes the pattern. <br> 
6/8 max for simply getting my maps to run. More marks for making them your own

**Step 6 ppp 8 MARKS**

You have made excellent maps and described the spatial patterns in the data and your expectations/theories about what causes the pattern. <br> 
6/8 max for simply getting my maps to run. More marks for making them your own

**Step 7 density analysis 25 MARKS**

You did all that was requested


**Step 8 distance analysis 25 MARKS**

You did all that was requested


**Above and beyond: 4 MARKS**

-   You get 2/4 for doing something new in any way
-   You get 4/4 for something really impressive


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

::: {style="margin-bottom:25px;"}
:::

------------------------------------------------------------------------

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
