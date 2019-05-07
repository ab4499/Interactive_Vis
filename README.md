# Interactive_Visualization

Interactive visualization is becoming a more prominent feature of reporting. Business analytics packages tend to stress the ease eith which data can be played with by non-experts. Allowing students to explore aspects of complex data rather than simply telling them what you see can be a powerful tool for learning as explored in the readings. Within the RStudio universe this functionality is accomplished through the Shiny ecosystem. A web-app designing interface that allows web-apps to be built from within R with limited knowledge of javascript or html.

![int_vis](https://github.com/ab4499/Interactive_Vis/blob/master/graphs/Int_vis.png "github")

In this project, I will first practice and show some simple example of interactive visualizations, and then I will build one to show how students master different skills as tested.


## Random Histogram Generator

Now we will build another Shiny App one piece at a time (Only the code starting at line 97 will run). This app will generate a histogram based on random values drawn from a normal distribution, the user will be able to select the number of draws that generate the histogram by using a slider.

![gif1](https://github.com/ab4499/Interactive_Vis/blob/master/graphs/gif1.gif "github")

## Final Part

Build an interactive visualization using the data sets quiz-categories.csv and midterm-results.csv. These data represent midterm results from an open book test. The categories represent the skills required to answer each question:

wrangling - Question required data manipulations skills  
coding - Question required coding skills  
d.trees - Question invoilved decision trees  
sna - Question involved social network analysis  
nlp - Question involved natural language processing  
viz - Question involved visualization of data  
n.nets - Question involved neural nets  
googleable - Question could be answered by searching the internet  
non-googleable - Question could not be answered through simple searching of the internet  
jitl - Question involved learning somethimg new (just in time learning)  
substantive - Question involved wrestling with a complex idea that does not have a definitive answer

Here is what the app looks like: 
![App](http://recordit.co/I3DzLgE8Zj "github")

In this visualization, questions are clustered within skill categories. Some skill categories are more specific (such as wrangling, nlp, sna, d.trees), some are more general (such as coding, goolgeableable, non-googleable). We can see how many students get the questions related to specific skills right.

## Relevant Materials

[Shiny Apps Documentation](https://shiny.rstudio.com/)

[Shiny Gallery](https://shiny.rstudio.com/gallery/)

[Verbert, K., Duval, E., Klerkx, J., Govaerts, S., & Santos, J. L. (2013). Learning Analytics Dashboard Applications. American Behavioral Scientist, 57(10), 1500–1509.](https://journals.sagepub.com/doi/abs/10.1177/0002764213479363)


