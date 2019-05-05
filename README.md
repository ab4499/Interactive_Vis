# Interactive_Visualization

Interactive visualization is becoming a more prominent feature of reporting. Business analytics packages tend to stress the ease eith which data can be played with by non-experts. Allowing students to explore aspects of complex data rather than simply telling them what you see can be a powerful tool for learning as explored in the readings. Within the RStudio universe this functionality is accomplished through the Shiny ecosystem. A web-app designing interface that allows web-apps to be built from within R with limited knowledge of javascript or html.

![int_vis](https://github.com/ab4499/Interactive_Vis/blob/master/graphs/Int_vis.png "github")

In this project, I will first practice and show some simple example of interactive visualizations, and then I will build one to show how students master different skills as tested.


## Basic Button

```{r}
ui <- fluidPage(actionButton("goButton", "Wake up!"),
                textOutput("reply"))
server <- function(input, output){
  observeEvent(input, output)
  output$reply<-renderText({"5 more minutes..."})
}

shinyApp(ui=ui, server=server)
```


## Random Histogram Generator

Now we will build another Shiny App one piece at a time (Only the code starting at line 97 will run). This app will generate a histogram based on random values drawn from a normal distribution, the user will be able to select the number of draws that generate the histogram by using a slider.

```{r}
ui <- fluidPage(
  sliderInput(inputId = "num", label = "Choose a number", 
    value = 1, min = 1, max = 100), plotOutput("hist"))

server <- function(input, output) {
  output$hist <- renderPlot({
    hist(rnorm(input$num))
  })
}

shinyApp(ui = ui, server = server)
```

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


```{r}
midterm<-read.csv("midterm-results.csv", header = TRUE)
categories<-read.csv("quiz-categories.csv", header = TRUE)
```

```{r}
library(dplyr)
library(tidyr)
library(ggplot2)
df1<-gather(categories, Skill, Count, -Question)
df2<-df1[which(df1$Count==1),]
df2<-df2[,c(2,1)]
df2$Question<-as.factor(gsub("_c", "", df2$Question))

correct<-unlist(lapply(midterm[,3:32], sum))
nameCorrect<-paste("Q", seq(1:30), sep="")
correct_df<-data.frame(x=nameCorrect, y=correct)
colnames(correct_df)<-c("Question", "Correct_Number")

df3<-left_join(df2, correct_df, by="Question")

df4<-df3[,c(2,1,3)]
df5<-spread(df4, Skill, Correct_Number)
df5<-df5%>%arrange(as.factor(Question))

```


```{r}
ui<-fluidPage(
  titlePanel("Skills"),
  sidebarLayout(
    sidebarPanel(
      radioButtons("p", "Select a Skill: ",
                   list("wrangling"='k', "coding"='a', "d.trees"='b', "sna"='h',
                        "nlp"='f', "viz"='j', "n.nets"='e', "googleable"='c',
                        "non-googleable"='g', "jitl"='d', "substantive"='i'))
    ),
    mainPanel(plotOutput("distPlot"))
  )
)

server<-function(input, output){
  output$distPlot<-renderPlot({
    if(input$p=="a"){
      i<-1
    }
    if(input$p=="b"){
      i<-2
    }
    if(input$p=="c"){
      i<-3
    }
    if(input$p=="d"){
      i<-4
    }
    if(input$p=="e"){
      i<-5
    }
    if(input$p=="f"){
      i<-6
    }
    if(input$p=="g"){
      i<-7
    }
    if(input$p=="h"){
      i<-8
    }
    if(input$p=="i"){
      i<-9
    }
    if(input$p=="j"){
      i<-10
    }
    if(input$p=="k"){
      i<-11
    }
    x<-df5%>%filter(!is.na(df5[,i+1]))%>%select(Question, i+1)
    colnames(x)<-c("Question", "Number")
    ggplot(x, aes(Question, Number))+
      geom_col(color="pink", fill="blue")
  })
}

shinyApp(ui=ui, server=server)
```

In this visualization, questions are clustered within skill categories. Some skill categories are more specific (such as wrangling, nlp, sna, d.trees), some are more general (such as coding, goolgeableable, non-googleable). We can see how many students get the questions related to specific skills right.
