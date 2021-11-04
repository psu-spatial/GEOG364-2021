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

 - Descriptive statistics
 - Density based spatial statistics (Kernel smoothing, quadrat analysis)
 - Distance based spatial statistics ( nearest neighbour analysis and the F, G, K and L functions.)
 - We will also work on downloading raster elevation and population density data

I will run my tutorials on a built in dataset inside R.   You will be conducting your analysis on a large (real) dataset on fossils and dinosaurs in Pennsylvania.  

Now you are getting more experienced in R, I will provide a worked example then get you to do something similar on your own data. As much as possible I will refer to the tutorials, but remember they are there and remember that you also have your previous labs.  I am purposefully not showing the code for the parts that you have done before, so this lab will be much harder if you have not finished Lab 6.

**This is a longer lab. You have until the start of the Thanksgiving break**

<br>

See [**your canvas assignment here**](https://psu.instructure.com/courses/2120046/assignments/13274841).

<p class="comment">**Need help?** Add a screenshot/question to the discussion board here: [**LAB 7 DISCUSSION BOARD**](https://psu.instructure.com/courses/2120046/discussion_topics/14125719)</p>

<br><br>

## A: Set up the lab **NEW**

<br>




## F. Submitting your Lab

Remember to save your work throughout and to spell check your writing (left of the knit button). Now, press the knit button again. If you have not made any mistakes in the code then R should create a html file in your lab 6 folder which includes your answers. If you look at your lab 6 folder, you should see this there - complete with a very recent time-stamp.

In that folder, double click on the html file. This will open it in your browser. CHECK THAT THIS IS WHAT YOU WANT TO SUBMIT

Now go to Canvas and submit BOTH your html and your .Rmd file in Lab 6.

<br><br>

## Lab 6 submission check-list

**For all answers: Full marks = everything down at a high standard, in full sentences as appropriate with no parts of your answer missing. Imagine it as an example I use in class**

**HTML FILE SUBMISSION - 5 marks**

**RMD CODE SUBMISSION - 5 marks**

**MARKDOWN STYLE - 10 MARKS**

We will start by awarding full marks and dock marks for mistakes.LOOK AT YOUR HTML FILE IN YOUR WEB-BROWSER BEFORE YOU SUBMIT 

TO GET 13/13 : All the below PLUS your equations use the equation format & you use subscripts/superscript as appropriate

TO GET 12/13 - all the below:

  - Your document is neat and easy to read. 
  - Answers are easy to find and paragraphs are clear (e.g. you left spaces between lines) 
  - You have written in full sentences, it is clear what your answers are referring to. 
  - You have used the spell check. 
  - You have used YAML code to make your work look professional (themes, tables of contents etc) 





**Above and beyond: 4 MARKS**

-   You get 2/4 for doing something new in any way 
-   You get 4/4 for something really impressive

An easy example, try conducting a Moran's analysis for your census data. Bonus marks if you can convert a column to TRUE/FALSE and do a join counts analysis on it!
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


::: {style="margin-bottom:25px;"}
:::


------------------------------------------------------------------------

Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
