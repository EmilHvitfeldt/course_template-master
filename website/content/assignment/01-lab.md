---
title: "Lab 01 - Hello R!"
output: tufte::tufte_html
link-citations: yes
---

# Learning goals

- Get acquainted with R and RStudio, which we will be using throughout the course to analyze data as well as to learn the statistical concepts discussed in the course. 
- Appreciate the value of visualization in exploring the relationship between variables.
- Start using R for building plots and calculating summary statistics.

# Terminology

We've already thrown around a few new terms, so let's define them before we proceed.

- **R**: Name of the programming language we will be using throughout the course.
- **RStudio**: An integrated development environment for R. In other words, a convenient interface for writing and running R code.

I like to think of R as the engine of the car, and RStudio is the dashboard.

# Starting slow

As the labs progress, you are encouraged to explore beyond what the labs dictate; a willingness to experiment will make you a much better programmer. Before we get to that stage, however, you need to build some basic fluency in R. Today we begin with the fundamental building blocks of R and RStudio: the interface, reading in data, and basic commands.

And to make versioning simpler, this is a solo lab. Additionally, we want to make sure everyone gets a significant amount of time at the steering wheel.

# Getting started

## 1 Download project

Go the the the lab page for this week on the [website](/PM566/class/01-class/). You should see a "Download" button under the "Lab Exercise" section. Click it to download the template for your responses to this lab, `01-lab-hello-r.Rmd`.

## 2 Download R

### If you don't have R installed.

Go to the [CRAN](https://cran.r-project.org/) and download R, make sure you get the version that matches your operating system.

### If you have R installed

If you have R installed run the following code


```r
R.version
```

```
##                _                           
## platform       x86_64-apple-darwin20       
## arch           x86_64                      
## os             darwin20                    
## system         x86_64, darwin20            
## status                                     
## major          4                           
## minor          3.1                         
## year           2023                        
## month          06                          
## day            16                          
## svn rev        84548                       
## language       R                           
## version.string R version 4.3.1 (2023-06-16)
## nickname       Beagle Scouts
```

This should tell you what version of R you are currently using. If your R version is lower then 4.3.0 I would strongly recommend updating. In general it is a good idea to update your R version, unless you have a project right now that depend on a specific version of R.

## 2.2 Download RStudio

We recommend using RStudio as your IDE if you don't already have it installed. You can go to the [RStudio](https://rstudio.com/products/rstudio/download/) website to download and install the software.

## 2.3 Launch RStudio

You have 2 ways to open the lab project we will be working with. Inside the folder is a `pm566-01-lab.Rproj` file, opening this file should launch your RStudio project.

You can also open the RStudio application first and then open the project by going `file -> open project...`

## 3. Get working!

Open the R Markdown (Rmd) file called `lab-01-hello-r.Rmd`. It will likely ask you if you would like to install a package that is required, click Install.

# Hello RStudio!

RStudio is comprised of four panes.

![](/PM566/assignment-img/rstudio-anatomy.png)



- On the bottom left is the Console, this is where you can write code that will be evaluated. Try typing `2 + 2` here and hit enter, what do you get?

- On the bottom right is the Files pane, as well as other panes that will come handy as we start our analysis.

- If you click on a file, it will open in the editor, on the top left pane.

- Finally, the top right pane shows your Environment. If you define a variable it would show up there. Try typing `x <- 2` in the Console and hit enter, what do you get in the Environment pane?

# Packages

R is an open-source language, and developers contribute functionality to R via packages. In this lab we will work with three packages: `datasauRus` which contains the dataset, and `tidyverse` which is a collection of packages for doing data analysis in a "tidy" way.

Load these packages by running the following in the Console.


```r
library(tidyverse) 
library(datasauRus)
```

If you haven't installed these packages yet and R complains, then you can install these packages by running the following command. (Note that R package names are case-sensitive)


```r
install.packages(c("tidyverse", "datasauRus"))
```

Note that the packages are also loaded with the same commands in your R Markdown document.

# Warm up

Before we introduce the data, let's warm up with some simple exercises.

The top portion of your R Markdown file (between the three dashed lines) is called YAML. It stands for "YAML Ain't Markup Language". It is a human friendly data serialization standard for all programming languages. All you need to know is that this area is called the YAML (we will refer to it as such) and that it contains meta information about your document.

## YAML

Open the R Markdown (Rmd) file in your project, change the author name to your name, and knit the document.

![](../../static/assignment-img/yaml-raw-to-rendered.png)
# Data

The data frame we will be working with today is called `datasaurus_dozen` and it's in the `datasauRus` package. Actually, this single data frame contains 13 datasets, designed to show us  why data visualisation is important and how summary statistics alone can be misleading. The different datasets are marked by the `dataset` variable.

To find out more about the dataset, type the following in your Console: `?datasaurus_dozen`. A question mark before the name of an object will always bring up its help file. This command must be ran in the Console.

## Question 1
1. Based on the help file, how many rows and how many columns does the `datasaurus_dozen` file have? What are the variables included in the data frame? Add your responses to your lab report. 

Let's take a look at what these datasets are. To do so we can make a *frequency table* of the dataset variable:


```r
datasaurus_dozen %>%
  count(dataset)
```

```
## # A tibble: 13 × 2
##    dataset        n
##    <chr>      <int>
##  1 away         142
##  2 bullseye     142
##  3 circle       142
##  4 dino         142
##  5 dots         142
##  6 h_lines      142
##  7 high_lines   142
##  8 slant_down   142
##  9 slant_up     142
## 10 star         142
## 11 v_lines      142
## 12 wide_lines   142
## 13 x_shape      142
```

```r
# table(datasaurus_dozen$dataset)
```

The original Datasaurus (`dino`) was created by Alberto Cairo in [this great blog post](http://www.thefunctionalart.com/2016/08/download-datasaurus-never-trust-summary.html). The other Dozen were generated using simulated annealing and the process is described in the paper *Same Stats, Different Graphs: Generating Datasets with Varied Appearance and Identical Statistics* through Simulated Annealing by Justin Matejka and George Fitzmaurice. In the paper, the authors simulate a variety of datasets that the same summary statistics to the Datasaurus but have very different distributions.

# Data visualization and summary

## Question 2
2. Plot `y` vs. `x` for the `dino` dataset. Then, calculate the correlation coefficient between `x` and `y` for this dataset.

Below is the code you will need to complete this exercise. Basically, the answer is already given, but you need to include relevant bits in your Rmd document and successfully knit it and view the results.

Start with the `datasaurus_dozen` and pipe it into the `filter` function to filter for observations where `dataset == "dino"`. Store the resulting filtered data frame as a new data frame called `dino_data`.


```r
dino_data <- datasaurus_dozen %>%
  filter(dataset == "dino")
# dino_data <- datasaurus_dozen[datasaurus_dozen$dataset == 'dino', ]
```

There is a lot going on here, so let's slow down and unpack it a bit. 

First, the pipe operator: `%>%`, takes what comes before it and sends it as the first argument to what comes after it. So here, we're saying `filter` the `datasaurus_dozen` data frame for observations where `dataset == "dino"`.

Second, the assignment operator: `<-`, assigns the name `dino_data` to the filtered data frame.

Next, we need to visualize these data. We will use the `ggplot` function for this. Its first argument is the data you're visualizing. Next we define the `aes`thetic mappings. In other words, the columns of the data that get mapped to certain aesthetic features of the plot, e.g. the `x` axis will represent the variable called `x` and the `y` axis will represent the variable called `y`. Then, we add another layer to this plot where we define which `geom`etric shapes we want to use to represent each observation in the data. In this case we want these to be points,m hence `geom_point`.


```r
ggplot(data = dino_data, mapping = aes(x = x, y = y)) +
  geom_point()
```

<img src="/PM566/assignment/01-lab_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```r
# plot(dino_data$x, dino_data$y)
```

If this seems like a lot, it is. And you will learn about the philosophy of building data visualizations in layers in detail in the upcoming class. For now, follow along with the code that is provided.

For the second part of these exercises, we need to calculate a summary statistic: the correlation coefficient. Correlation coefficient, often referred to as `\(r\)` in statistics, measures the linear association between two variables. You will see that some of the pairs of variables we plot do not have a linear relationship between them. This is exactly why we want to visualize first: visualize to assess the form of the relationship, and calculate `\(r\)` only if relevant. In this case, calculating a correlation coefficient really doesn't make sense since the relationship between `x` and `y` is definitely not linear -- it's dinosaurial!

But, for illustrative purposes, let's calculate correlation coefficient between `x` and `y`.

Start with `dino_data` and calculate a summary statistic that we will call `r` as the `cor`relation between `x` and `y`.


```r
dino_data %>%
  summarize(r = cor(x, y))
# cor(dino_data$x, dino_data$y)
```

## Question 3
3. Plot `y` vs. `x` for the `star` dataset. You can (and should) reuse code we introduced above, just replace the dataset name with the desired dataset. Then, calculate the correlation coefficient between `x` and `y` for this dataset. How does this value compare to the `r` of `dino`?

## Question 4
4. Plot `y` vs. `x` for the `circle` dataset. You can (and should) reuse code we introduced above, just replace the dataset name with the desired dataset. Then, calculate the correlation coefficient between `x` and `y` for this dataset. How does this value compare to the `r` of `dino`?

Facet by the dataset variable, placing the plots in a 3 column grid, and don't add a legend.

## Question 5
5. Finally, let's plot all datasets at once. In order to do this we will make use of facetting.


```r
ggplot(datasaurus_dozen, aes(x = x, y = y, color = dataset))+
  geom_point()+
  facet_wrap(~ dataset, ncol = 3) +
  theme(legend.position = "none")
# layout(matrix(1:16, ncol=4))
# for(i in 1:length(unique(datasaurus_dozen$dataset))){
#   dset_name <- unique(datasaurus_dozen$dataset)[i]
#   subset <- datasaurus_dozen[datasaurus_dozen$dataset == dset_name, ]
#   plot(subset$x, subset$y, main = dset_name, col = i)
# }
# layout(1)
```

And we can use the `group_by` function to generate all correlation coefficients.


```r
datasaurus_dozen %>%
  group_by(dataset) %>%
  summarize(r = cor(x, y))
# sapply(unique(datasaurus_dozen$dataset), function(ds){
#     subset <- datasaurus_dozen[datasaurus_dozen$dataset == ds, ]
#     cor(subset$x, subset$y)
# })
```

You're done with the data analysis exercises, but we'd like you to do two more things:

![](../../static/assignment-img/fig-resize-global.png)

- **Resize your figures:** 

Click on the gear icon in on top of the R Markdown document, and select "Output Options..." in the dropdown menu. In the pop up dialogue box go to the Figures tab and change the height and width of the figures, and hit OK when done. Then, knit your document and see how you like the new sizes. Change and knit again and again until you're happy with the figure sizes. Note that these values get saved in the YAML.

![](../../static/assignment-img/fig-resize-local.png)

You can also use different figure sizes for different figures. To do so click on the gear icon within the chunk where you want to make a change. Changing the figure sizes added new options to these chunks: `fig.width` and `fig.height`. You can change them by defining different values directly in your R Markdown document as well.

![](../../static/assignment-img/theme-highlight.png)

- **Change the look of your report:** 

Once again click on the gear icon in on top of the R Markdown document, and select "Output Options..." in the dropdown menu. In the General tab of the pop up dialogue box try out different syntax highlighting and theme options. Hit OK and knit your document to see how it looks. Play around with these until you're happy with the look.


# Optional

If you have time you can explore the different ways you can add styling to your rmarkdown document.

Here is a [cheatsheet](https://rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)

and a [markdown cheatsheet](https://www.markdownguide.org/cheat-sheet/)

---

This set of lab exersixes have been adopted from [Mine Çetinkaya-Rundel](https://twitter.com/minebocek)'s class [Introduction to Data Science](https://github.com/ids-s1-19).
