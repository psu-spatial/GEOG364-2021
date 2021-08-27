---
title: "Tutorial 1c: Getting Started"
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

Everything in this tutorial is a one-off to get R and R-studio set up.

<br>

<div style="margin-bottom:25px;">
</div> 
### Getting started

First, in an easy to access place on your computer, make a folder called GEOG-364.  This is where all your labs and projects are going to live.

**Now everything is installed, open R-studio** (NOT R!).  

<img src="Tutorial1c_fig1_RRstudiologos.png" width="2097" />

<br>

You will be greeted by three panels:

 - The interactive R console (entire left)
 - Environment/History (tabbed in upper right)
 - Files/Plots/Packages/Help/Viewer (tabbed in lower right)

If you click on the *View/Panes/Pane* Layout menu item, you can move these quadrants around.  I tend to like the console to be top left and scripts to be top right, with the plots and environment on the bottom - but this is  personal choice. 

<img src="Tutorial1c_fig2Rstudio.png" width="1778" />

<br> 

If you wish to learn more about what these windows do, have a look at this resource, from the Pirates Guide to R: https://bookdown.org/ndphillips/YaRrr/the-four-rstudio-windows.html.  

**If you have used R before, you might see that there are variables and plots etc already loaded**.  It is always good to clear these before you start a new analysis.  To do this, click the little broom symbol in your environment tab.

<br>

<div style="margin-bottom:25px;">
</div> 
### Change a few settings

R-studio wants to be helpful and will try to re-load exactly where you were in a project when you log back in.  This can get really confusing, so we are going to turn this off.

ON A MAC: Click on the R-studio menu button on the top left of the screen, then click Preferences. 

ON A PC: Click on Tools-> Global Options -> Preferences

Now:

 - UNCLICK "Restore most recently opened project at startup"
 - Set "Save workspace to .RData on" exit to Never

***

<a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/">Creative Commons Attribution-NonCommercial 4.0 International License</a>.


Website created and maintained by [Helen Greatrex](https://www.geog.psu.edu/directory/helen-greatrex). Website template by [Noli Brazil](https://nbrazil.faculty.ucdavis.edu/)
