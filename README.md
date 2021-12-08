## DATA VISUALIZATION - FALL 2021


### _Journalism in Age of Data_ - Geoff McGhee (2011)

These two journalists use the principle that vision is the best way for individuals to assess the world around them. Capturing images of the surroundings allow the brain to actually know what is going and understand the information presented. The goal is to use the complicated data given and try to make it look like something the audience can easily relate to. It is more about how it looks like. Data in itself is raw and difficult to see or understand what is happening. Data visualization allows to put the raw data into context. By using graphics, art, charts, etc. the information found in the raw data appears to be easier to understand. 

In the recent years, more and more people give less time to reading long articles containing lots if information. People want to spend as less time as possible still wants to get the whole context of the article. That is why data visualization is being used more often in journalism. But when data visualization is done incorrectly, it can communicate wrong information and change the whole data in the wrong way. 

I personally think that data slideshow is a good way to capture people’s attention. It allows them to go straight to their element of interest on the slide show but at same time they have access to the rest. So maybe comparisons between data from two different years become a little bit easier for instance. Also, I think data visualization gives life to the data with all the sounds, movements, colors, pictures, graphs, etc. also, when data visualization is too hard to understand, it becomes frustrating to the reader, which is something that should be avoided. 

I think data visualization in journalism is the way to go because it is a way of telling a story to the reader that enables him to better understand complicated and/or sophisticated data easily and in a short period of time. It makes it more interesting, useful, and digestible to the readers.

### _The Future of data Analysis_ - Edward Tufte (2016)

Dr. Edward Tufte gives us 4 points on which to focus when it comes to the future of Data Analysis which are: future excellence, getting it right in data analysis, confirmatory-unhacked vs. exploratory-detective work, and the last interface: the thinking eye. According to him, data analysis is about making conclusions from information given and analytical thinking is about assessing and evaluating the relationship between the two. It is all about having all the information given displayed in one visual representation. With the example of the Swiss Alps given here, details, colors, fonts, etc. make it easier to understand visualize the visual representation displayed here.

Also, by thinking about the future of data analysis, 3D representations add movement to visual representations. Using stop actions, slow motions or videos help improve the displays of the information given. It gives a better understanding and different views of the overall data (soccer picture example). By using a map as a display, he is explaining how an important amount of data can be stored in the map display, regardless of language of place. 

Tufte is saying that what is important in analytical thinking is to admire excellence ask ourselves how did they do what they did? Understand excellence! Another point is to have an open mind, not an empty mind. It means that other ideas are always good to explore and entertain. The responsibility of data analysis is to make right conclusion; by torturing the data, it tells just about anything that we want, which is not necessarily right. 

### _Data Visualization and Data Science (EMBL)_ - Hadley Wickham

In this short video, Wickham introduced different technologies/techniques which are basically R packages and commands that allow the manipulation and analysis of data to be a little easier. Those techniques are: ggplot, gapminder, geom_point, scale_x_log10, group_split(year), gap_plot, animate, ggseq.

Hadley Wickham is using a visualization project and tries to explain how to use R commands to get to those results. He starts with the raw data. He uses different command to filter to the data to only one year (2015). He then uses ggplot2 to plot the data and see. He keeps going by rescaling, adding colors, placing smaller countries first so that they are not hidden by larger countries. The same commands can be used to look at other years individually. 

He goes further by combining all the graphs to show the changes over the years; instead of comparing them individually, he creates a type of slideshow that shows all the graphs from different years and that makes the comparison easier. He also put all the plots from different years on one graph. That method is not clear enough to analyze and compare according to me, but it might me efficient to do so for certain reasons.

Wickham goes ahead and gives us three reasons why people should code according to him. Those reasons are code is text, code is able to be read, and code is reproducible. When coding, we have the ability to copy and paste which makes it easier to communicate it and share it with others. Code can be criticized as well which leaves room for improvement. And thus, codes can be reproduced as many times as possible.

### Big Data Analytics Pitfall & Overfitting and Overparameterization

### Comparison of Different Styles of Data Visualization of Two Authors

### _How to Improve Your Relationship With Your Future Self_ - Jake Bowers (2016)

### Rachmaninoff, Prelude in C-sharp minor (opus 3 no. 2) [link](https://www.youtube.com/watch?v=Edg910m-3o8) - Stephen Malinowski

In this video, we can observe how the shapes move with every sound that we are hearing. Shapes are brightened when they get to the middle of the display and that is when we also hear the sound. We can observe different colors and different shapes and as they differ from each other, the sound that is heard is also different. 

Another observation from this video is that the oval shapes open up when the sound comes out and when a new sound, different and loud comes, there are different shapes that come together and create a rectangle. 

Colors are different when the sound is either strong or light. There is  a combination of green, bleu, violet for stronger sounds and a combination of orange, pink and light bleu for lighter sounds. Those color combinations are only for oval shapes. For lines and rectangles, the colors are slightly different but still have a similar tone. 

At some point, the sound is accelarated and the shapes change at the same time. Now, there are lines with different colors and sizes that appear as the sound goes on. Also, a different movement can be observed, different from what we have seen so far. The sizes of the rectangles are bigger as well. 

### Assignment 1: Leaf of Fall

```markdown
# Install packages

install.packages("gsubfn")
install.packages("tidyverse")
library(gsubfn)
library(tidyverse)

# Define elements in plant art
# Each image corresponds to a different axiom, rules, angle and depth

## Leaf of Fall

axiom="X"
rules=list("X"="F-[[X]+X]+F[+FX]-X", "F"="FF")
angle=22.5
depth=6

for (i in 1:depth) axiom=gsubfn(".", rules, axiom)
actions=str_extract_all(axiom, "\\d*\\+|\\d*\\-|F|L|R|\\[|\\]|\\|") %>% unlist
status=data.frame(x=numeric(0), y=numeric(0), alfa=numeric(0))
points=data.frame(x1 = 0, y1 = 0, x2 = NA, y2 = NA, alfa=90, depth=1)

# Generating data
# Note: may take a minute or two

for (action in actions)
{
  if (action=="F")
  {
    x=points[1, "x1"]+cos(points[1, "alfa"]*(pi/180))
    y=points[1, "y1"]+sin(points[1, "alfa"]*(pi/180))
    points[1,"x2"]=x
    points[1,"y2"]=y
    data.frame(x1 = x, y1 = y, x2 = NA, y2 = NA,
               alfa=points[1, "alfa"],
               depth=points[1,"depth"]) %>% rbind(points)->points
  }
  if (action %in% c("+", "-")){
    alfa=points[1, "alfa"]
    points[1, "alfa"]=eval(parse(text=paste0("alfa",action, angle)))
  }
  if(action=="["){
    data.frame(x=points[1, "x1"], y=points[1, "y1"], alfa=points[1, "alfa"]) %>%
      rbind(status) -> status
    points[1, "depth"]=points[1, "depth"]+1
  }

  if(action=="]"){
    depth=points[1, "depth"]
    points[-1,]->points
    data.frame(x1=status[1, "x"], y1=status[1, "y"], x2=NA, y2=NA,
               alfa=status[1, "alfa"],
               depth=depth-1) %>%
      rbind(points) -> points
    status[-1,]->status
  }
}

ggplot() +
  geom_segment(aes(x = x1, y = y1, xend = x2, yend = y2),
               lineend = "round",
               color="red", # Set Fall color?
               data=na.omit(points)) +
  coord_fixed(ratio = 1) +
  theme(legend.position="none",
        panel.background = element_rect(fill="white"),
        panel.grid=element_blank(),
        axis.ticks=element_blank(),
        axis.title=element_blank(),
        axis.text=element_blank())
```
 ![image](https://user-images.githubusercontent.com/81389378/136884889-0556d144-f3f7-41b2-9acd-37e61c6a2bb9.png)
 
### Assignment 2: Paul Murrell"s RGraphics basic R programs

```markdown
### Paul Murrell's R examples (selected)

## Start plotting from basics 
plot(pressure, pch=16)  # Can you change pch?
text(150, 600, 
     "Pressure (mm Hg)\nversus\nTemperature (Celsius)")

#  Examples of standard high-level plots 
#  In each case, extra output is also added using low-level 
#  plotting functions.
# 

# Setting the parameter (3 rows by 2 cols)
par(mfrow=c(3, 2))

# Scatterplot
# Note the incremental additions

x <- c(0.5, 2, 4, 8, 12, 16)
y1 <- c(1, 1.3, 1.9, 3.4, 3.9, 4.8)
y2 <- c(4, .8, .5, .45, .4, .3)

# Setting label orientation, margins c(bottom, left, top, right) & text size
par(las=1, mar=c(4, 4, 2, 4), cex=.7) 
plot.new()
plot.window(range(x), c(0, 6))
lines(x, y1)
lines(x, y2)
points(x, y1, pch=16, cex=2) # Try different cex value?  
points(x, y2, pch=21, bg="white", cex=2)  # Different background color
par(col="gray50", fg="gray50", col.axis="gray50")
axis(1, at=seq(0, 16, 4))
axis(2, at=seq(0, 6, 2))
axis(4, at=seq(0, 6, 2))
box(bty="u")
mtext("Travel Time (s)", side=1, line=2, cex=0.8)
mtext("Responses per Travel", side=2, line=2, las=0, cex=0.8)
mtext("Responses per Second", side=4, line=2, las=0, cex=0.8)
text(4, 5, "Bird 131")
par(mar=c(5.1, 4.1, 4.1, 2.1), col="black", fg="black", col.axis="black")

# Histogram
# Random data
Y <- rnorm(50)
# Make sure no Y exceed [-3.5, 3.5]
Y[Y < -3.5 | Y > 3.5] <- NA # Selection
x <- seq(-3.5, 3.5, .1)
dn <- dnorm(x)
par(mar=c(4.5, 4.1, 3.1, 0))
hist(Y, breaks=seq(-3.5, 3.5), ylim=c(0, 0.5), 
     col="gray80", freq=FALSE)
lines(x, dnorm(x), lwd=2)
par(mar=c(5.1, 4.1, 4.1, 2.1))

# Barplot
par(mar=c(2, 3.1, 2, 2.1)) 
midpts <- barplot(VADeaths, 
                  col=gray(0.1 + seq(1, 9, 2)/11), 
                  names=rep("", 4))
mtext(sub(" ", "\n", colnames(VADeaths)),
      at=midpts, side=1, line=0.5, cex=0.5)
text(rep(midpts, each=5), apply(VADeaths, 2, cumsum) - VADeaths/2,
     VADeaths, 
     col=rep(c("white", "black"), times=3:2), 
     cex=0.8)
par(mar=c(5.1, 4.1, 4.1, 2.1))  

# Boxplot
par(mar=c(3, 4.1, 2, 0))
boxplot(len ~ dose, data = ToothGrowth,
        boxwex = 0.25, at = 1:3 - 0.2,
        subset= supp == "VC", col="white",
        xlab="",
        ylab="tooth length", ylim=c(0,35))
mtext("Vitamin C dose (mg)", side=1, line=2.5, cex=0.8)
boxplot(len ~ dose, data = ToothGrowth, add = TRUE,
        boxwex = 0.25, at = 1:3 + 0.2,
        
        subset= supp == "OJ")
legend(1.5, 9, c("Ascorbic acid", "Orange juice"), 
       fill = c("white", "gray"), 
       bty="n")
par(mar=c(5.1, 4.1, 4.1, 2.1))

# Persp
x <- seq(-10, 10, length= 30)
y <- x
f <- function(x,y) { r <- sqrt(x^2+y^2); 10 * sin(r)/r }
z <- outer(x, y, f)
z[is.na(z)] <- 1
# 0.5 to include z axis label
par(mar=c(0, 0.5, 0, 0), lwd=0.5)
persp(x, y, z, theta = 30, phi = 30, 
      expand = 0.5)
par(mar=c(5.1, 4.1, 4.1, 2.1), lwd=1)

# Piechart
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=0.5)
pie.sales <- c(0.12, 0.3, 0.26, 0.16, 0.04, 0.12)
names(pie.sales) <- c("Blueberry", "Cherry",
                      "Apple", "Boston Cream", "Other", "Vanilla")
pie(pie.sales, col = gray(seq(0.3,1.0,length=6))) 

# Exercise: Can you generate these charts individually?  Be sure to 
# work on the layout and margins
```
![image](https://user-images.githubusercontent.com/81389378/136886542-d1e76e56-b27d-4b19-a3e5-c9223ee8b290.png) ![image](https://user-images.githubusercontent.com/81389378/136886573-cfd2b5e0-c626-45f2-93fa-42f562eed8bf.png)

### Assignment 3: Anscombe01

```markdown
## Anscombe (1973) Quartlet

data(anscombe)  # Load Anscombe's data
View(anscombe) # View the data
summary(anscombe)

## Simple version
plot(anscombe$x1,anscombe$y1)
summary(anscombe)

# Create four model objects
lm1 <- lm(y1 ~ x1, data=anscombe)
summary(lm1)
lm2 <- lm(y2 ~ x2, data=anscombe)
summary(lm2)
lm3 <- lm(y3 ~ x3, data=anscombe)
summary(lm3)
lm4 <- lm(y4 ~ x4, data=anscombe)
summary(lm4)
plot(anscombe$x1,anscombe$y1)
abline(coefficients(lm1))
plot(anscombe$x2,anscombe$y2)
abline(coefficients(lm2))
plot(anscombe$x3,anscombe$y3)
abline(coefficients(lm3))
plot(anscombe$x4,anscombe$y4)
abline(coefficients(lm4))


## Fancy version (per help file)

ff <- y ~ x
mods <- setNames(as.list(1:4), paste0("lm", 1:4))

# Plot using for loop
for(i in 1:4) {
  ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
  ## or   ff[[2]] <- as.name(paste0("y", i))
  ##      ff[[3]] <- as.name(paste0("x", i))
  mods[[i]] <- lmi <- lm(ff, data = anscombe)
  print(anova(lmi))
}

sapply(mods, coef)  # Note the use of this function
lapply(mods, function(fm) coef(summary(fm)))

# Preparing for the plots
op <- par(mfrow = c(2, 2), mar = 0.1+c(4,4,1,1), oma =  c(0, 0, 2, 0))

# Plot charts using for loop
for(i in 1:4) {
  ff[2:3] <- lapply(paste0(c("y","x"), i), as.name)
  plot(ff, data = anscombe, col = "red", pch = 21, bg = "orange", cex = 1.2,
       xlim = c(3, 19), ylim = c(3, 13))
  abline(mods[[i]], col = "blue")
}
mtext("Anscombe's 4 Regression data sets", outer = TRUE, cex = 1.5)
par(op)
```
![image](https://user-images.githubusercontent.com/81389378/136887232-8a13ef8c-9446-4da2-b4a7-7efd0aee277d.png)

### Codes used for Final project

```markdown

## Recoding the Likert scale
library("likert")
library("dplyr")
library("tidyverse")
library("magrittr")

project_data3 <- project_data %>% mutate_at(c((9:26)), 
funs(recode(., "Strongly agree" = 1, "Agree" = 2, 
"Uncertain" = 3, "Disagree" = 4, "Strongly disagree" =5)))

## pie chart
# gender pie chart
project.data4 <- project_data3 %>% group_by(GENDER) %>% 
summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=0.5)
GENDERS <- c(25, 15)
names(GENDERS) <- c("Female", "Male")
pct = round(GENDERS/sum(GENDERS)*100)
new_labels = paste(names(GENDERS), "-", pct, "%", sep = "")
pie(GENDERS, labels = new_labels, col = rainbow(2), main = "GENDER PROPORTION")

# age pie chart
project.data5 <- project_data3 %>% group_by(AGE.RANGE) %>% 
summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
AGE <- c(20, 18, 2)
names(AGE) <- c("17-24", "25-29", "30+")
pct1 = round(AGE/sum(AGE)*100)
new_labels1 = paste(names(AGE), "=", pct1, "%", sep = "")
pie(AGE, labels = new_labels1, col = rainbow(3), main = "AGE RANGE")

# education level pie chart
project.data6 <- project_data3 %>% group_by(LEVEL.EDUCATION) %>% 
summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
EDUCATION.LEVEL <- c(3, 19, 18)
names(EDUCATION.LEVEL) <- c("Associate", "Graduate", "Undergraduate")
pct2 = round(EDUCATION.LEVEL/sum(EDUCATION.LEVEL)*100)
new_labels2 = paste(names(EDUCATION.LEVEL), "=", pct2, "%", sep = "")
pie(EDUCATION.LEVEL, labels = new_labels2, col = rainbow(3), main = "EDUCATIONAL LEVEL")

# Digital tools BC19
project.data7 <- project_data3 %>% group_by(DIGITAL.TOOLS.BC19) %>% summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
TOOLS.BC19 <- c(21, 19, 0)
names(TOOLS.BC19) <- c("Laptop","Mobile Phone", "IPad")
pct2 = round(TOOLS.BC19/sum(TOOLS.BC19)*100)
new_labels2 = paste(names(TOOLS.BC19), "-", pct2, "%", sep = "")
pie(TOOLS.BC19, labels = new_labels2, col = rainbow(3), main = "DIGITAL TOOLS USED BEFORE COVID-19"

# Digital tools AC19
project.data7 <- project_data3 %>% group_by(DIGITAL.TOOLS.AC19) %>% summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
TOOLS.AC19 <- c(28, 11, 1)
names(TOOLS.AC19) <- c("Laptop","Mobile Phone", "IPad")
pct2 = round(TOOLS.AC19/sum(TOOLS.AC19)*100)
new_labels2 = paste(names(TOOLS.AC19), "-", pct2, "%", sep = "")
pie(TOOLS.AC19, labels = new_labels2, col = rainbow(3), main = "DIGITAL TOOLS USED AFTER COVID-19"

# Time Spent on Digital tools BC19
project.data7 <- project_data3 %>% group_by(HOURS.ON.TOOLS.BC19) %>% summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
TIME.BC19 <- c(3, 8, 15, 14)
names(TIME.BC19) <- c("1 TO 3","10+", "4 TO 6", "7 TO 9")
pct2 = round(TIME.BC19/sum(TIME.BC19)*100)
new_labels2 = paste(names(TIME.BC19), "-", pct2, "%", sep = "")
pie(TIME.BC19, labels = new_labels2, col = rainbow(4), main = "TIME SPENT ON DIGITAL TOOLS BEFORE COVID-19"

# Time spent on Digital tools AC19
project.data7 <- project_data3 %>% group_by(HOURS.ON.TOOLS.AC19) %>% summarise(counts = n(), percentage = n()/nrow(project_data3))
par(mar=c(0, 2, 1, 2), xpd=FALSE, cex=1)
TIME.AC19 <- c(3, 8, 15, 14)
names(TIME.AC19) <- c("1 TO 3","10+", "4 TO 6", "7 TO 9")
pct2 = round(TIME.AC19/sum(TIME.AC19)*100)
new_labels2 = paste(names(TIME.AC19), "-", pct2, "%", sep = "")
pie(TIME.AC19, labels = new_labels2, col = rainbow(4), main = "TIME SPENT ON DIGITAL TOOLS AFTER COVID-19"

# Students' Concentration BC19
project_data3 %>% 
  ggplot(aes(QUESTION.10))+
           geom_bar(fill = "#97B3C6")+ 
           coord_flip()+
           theme_bw()+
           labs(title = "Concentration when using digital tools before Covid=19", x = "scale", y = "Number of students")

# Students' Concentration AC19
project_data3 %>% 
  ggplot(aes(QUESTION.11))+
           geom_bar(fill = "#97B3C6")+ 
           coord_flip()+
           theme_bw()+
           labs(title = "Concentration when using digital tools after Covid=19", x = "scale", y = "Number of students")

# Sleeping Habits BC19
project_data3 %>% 
  ggplot(aes(QUESTION.12))+
           geom_bar(fill = "#97B3C6")+ 
           coord_flip()+
           theme_bw()+
           labs(title = "Sleeping habits before Covid-19", x = "scale", y = "Number of students")

# Sleeping Habits AC19
project_data3 %>% 
  ggplot(aes(QUESTION.13))+
           geom_bar(fill = "#97B3C6")+ 
           coord_flip()+
           theme_bw()+
           labs(title = "Sleeping habits after Covid-19", x = "scale", y = "Number of students")

# Importance of Face-to-Face
project_data3 %>% 
  ggplot(aes(QUESTION.18))+
           geom_bar(fill = "#546B3C99")+
           theme_bw()+
           labs(title = "Face-to-Face learning strengthens the social personality of students", x = "scale", y = "Number of students")

# Exams and Assignments online
project_data3 %>% 
  ggplot(aes(QUESTION.23))+
           geom_bar(fill = "#546B3C99")+
           theme_bw()+
           labs(title = "Online exams and quizzes are not comfortable and make students nervous", x = "scale", y = "Number of students")

# Academic Performance
project_data3 %>% 
  ggplot(aes(QUESTION.24))+
           geom_bar(fill = "#546B3C99")+
           theme_bw()+
           labs(title = "Academic performance took a hit with the online learning system", x = "scale", y = "Number of students")

# Social Distancing and Isolation
project_data3 %>% filter(QUESTION.16 == "1" |
                           QUESTION.16 == "2" |
                           QUESTION.16 == "3" |
                           QUESTION.16 == "4" |
                           QUESTION.16 == "5") %>%
  ggplot(aes(QUESTION.16, fill = GENDER)+
  geom_bar(position = "dodge", alpha = 2)+
  theme_bw()+
  theme(panel.grid.major = element_blank(),
        panel.grid.minor = element_blank())+
  labs(title = "Social Distancing and Isolation", x = "Scale", y = "Number of Students")
  
  # Continuing with the Online Learning System
  project_data3 %>% filter(QUESTION.25 == "1" |
                           QUESTION.25 == "2" |
                           QUESTION.25 == "3" |
                           QUESTION.25 == "4" |
                           QUESTION.25 == "5") %>%
  ggplot(aes(QUESTION.25, fill = GENDER)+
  geom_bar(position = "dodge", alpha = 2)+
  theme_bw()+
  theme(panel.grid.major = element_blank(),
        panel.grid.minor = element_blank())+
  labs(title = "Social Distancing and Isolation", x = "Scale", y = "Number of Students")
  
```

