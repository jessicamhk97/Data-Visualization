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

### Music Visualization - Stephen Malinowski

### Assignment 1: Leaf of Fall

```markdown
Install packages

install.packages("gsubfn")
install.packages("tidyverse")
library(gsubfn)
library(tidyverse)

Define elements in plant art
Each image corresponds to a different axiom, rules, angle and depth

Leaf of Fall

axiom="X"
rules=list("X"="F-[[X]+X]+F[+FX]-X", "F"="FF")
angle=22.5
depth=6

for (i in 1:depth) axiom=gsubfn(".", rules, axiom)
actions=str_extract_all(axiom, "\\d*\\+|\\d*\\-|F|L|R|\\[|\\]|\\|") %>% unlist
status=data.frame(x=numeric(0), y=numeric(0), alfa=numeric(0))
points=data.frame(x1 = 0, y1 = 0, x2 = NA, y2 = NA, alfa=90, depth=1)

Generating data
Note: may take a minute or two

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
               color="burlywood3", # Set Fall color?
               data=na.omit(points)) +
  coord_fixed(ratio = 1) +
  theme(legend.position="none",
        panel.background = element_rect(fill="white"),
        panel.grid=element_blank(),
        axis.ticks=element_blank(),
        axis.title=element_blank(),
        axis.text=element_blank())
```
        
### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/jessicamhk97/Data-visualization/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
