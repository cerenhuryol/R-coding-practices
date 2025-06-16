# R-coding-practices
Creating R page for DIME Wiki

<onlyinclude>
This article lays out some best practices for coding using R. Though it is possible to use R without it, the RStudio integrated development environment makes its use easier and is the standard among R users. There is not a single set of best practices and the guidelines below are suggestions that can and should be adapted the each project's needs, as well as users' preferences
</onlyinclude>

## Read First
* RStudio
* Comments
* Objects names

## Package installation
R packages are collections of functions, data, and documentation that extend the functionality of base R. They are essential for everything from data cleaning to statistical modeling and visualization.

## Installing CRAN Packages

CRAN (The Comprehensive R Archive Network) is the primary repository for R packages.

Here's an example to install a package from CRAN:

 <code>install.packages("tidyverse")</code>

To install multiple packages:

 <code>install.packages(c("tidyverse", "haven", "data.table"))</code>

To load the packages installed:

 <code>library(tidyverse)</code>

## Comments and script structure
Running code that returns the right result is only the first half of the job. The other half is making sure your code is easy to follow, test, and reuse. This helps teams catch mistakes, audit decisions, and collaborate more effectively. Poorly structured code increases the risk of errors.


#### 1. Use header comments to introduce each script:
 ```R
 ##################################################
 # Script: 01_clean_data.R
 # Purpose: Clean raw baseline data
 # Author: First Last
 # Date: 2025-05-30
 # Inputs: data/raw/baseline.csv
 # Outputs: data/clean/baseline_clean.rds
 ##################################################
```

#### 2. Use section headers to structure code within each script

 ```R
 # Load packages -------------------------------------------------------

 # Import data ---------------------------------------------------------

 # Clean variables -----------------------------------------------------

 # Save outputs --------------------------------------------------------
```

'''Good syntax''' makes it easy to understand what the code is doing and why. You should:

*Use clear, expressive names for variables and objects (e.g., baseline_data instead of bd).

*Avoid deeply nested code and one-liners that sacrifice clarity.

*Write logic in small chunks—long chains of operations should be broken down or commented carefully.

## Naming objects
In R, object names are one of the most fundamental tools for writing readable, maintainable, and collaborative code. This includes variable names, function names, data frame names, and any other user-defined object. Good naming helps future users (and your future self) quickly understand what your code is doing without constantly referring back to earlier lines.

### General Principles

* Be descriptive: Use names that clearly describe what the object represents. For example, use <code>total_income</code> instead of <code>x</code> or <code>ti</code>.

* Use lowercase letters: Stick to lowercase letters and use underscores (_) to separate words. This style is consistent with tidyverse conventions and improves readability (household_id, not HouseholdID or houseHoldId).

* Avoid abbreviations: Unless widely recognized (e.g., GDP, ID, ISO), avoid abbreviations that may not be clear to others.

* Don't overwrite base functions: Avoid naming objects data, mean, sum, T, c, etc., which are already used by R and can lead to hard-to-spot bugs.

* Consistency is key: Pick a style and stick with it throughout your project (e.g., always use snake_case or always use dot.case, but don’t mix them).

#### For Example;

* <code>survey_data_2023</code>: Descriptive and specific
* <code>income_total</code>: Meaningful variable name 
* <code>calculate_growth</code>: Action-based function name 
* <code>beneficiary_status</code>: Clear and readable

## Style and white space
Following consistent style and white space conventions in R code improves readability, helps with debugging, and facilitates collaboration across teams. At DIME, we recommend adhering to the [tidyverse style guide](https://style.tidyverse.org/) with some team-specific adjustments. Below are key points to follow:

### 1. Indentation:
* Use two spaces for indentation, not tabs.
* Nested structures (like if, for, or pipes) should be indented to reflect logical structure.
```R
if (condition) {
  do_something()
}
```
### 2. Line Length

* Keep lines under 80 characters when possible.
* Break long lines logically, especially for pipes, put each step on a new line and indent.
  
```R
 data %>%
   filter(x > 0) %>%
   group_by(id) %>%
   summarise(mean_val = mean(value))
```

### 3. Spaces:

* Add spaces around operators: <code>x <- 1</code>, not <code>x<-1</code>.
* No space before a comma; one space after a comma: <code>c(1, 2, 3)</code>.
* No space inside parentheses or square brackets: <code>mean(x)</code>, not <code>mean( x )</code>.

## Functions and Piping
In R, you can define one function inside another, a concept related to metaprogramming. However, nesting multiple functions can become complex and error-prone. Using pipes helps break down operations into readable steps, improving both clarity and maintainability. Pipes take the output of the function at the left and pass it as the first argument of the function at the right. For example:

```R
  df$income_total %>% 
  log() %>% 
  mean()
```
Note that;
<code>x %>% f()</code> is the same as <code>f(x)</code> and 
<code>x %>% f() %>% g()</code> is the same as <code>g(f(x))</code>

## Loops in R

In Stata, we use <code>for</code> loops very frequently. In R, the syntax of <code>for</code> loop is this:

```R
for (number in 1:3) {
        print(number)
}
```
While R supports traditional loops like <code>for</code>, <code>while</code>, and <code>repeat</code>, since R is vectorized, you can avoid explicit loops in most cases and use vectorized functions or functional programming tools like <code>purrr::map()</code> or <code>lapply()</code> instead. These approaches are usually more concise, readable, and efficient.

### Installation 

To use <code>map</code> you need to load the package <code>purrr</code>. 
The syntax for <code>map()</code> is:

```R
map(X, function, ...) #Applies function to each of elements of X. If X is a data frame then function is applied column-wise, while if it's a vector or a list, it is applied item wise. The output of map is always a list. 
```


## Tidyverse

Tidyverse includes very useful packages that you will need frequently in your analysis. The functions include data transformation, tidying, filtering data and many more. 

To install all the packages in Tidyverse:
```R
install.packages("tidyverse")
```
When you load the <code>tidyverse</code>, you’re loading these core packages:

| Package   | Use                                         |
| --------- | ------------------------------------------- |
| `ggplot2` | Data visualization                          |
| `dplyr`   | Data manipulation (filter, mutate, etc.)    |
| `tidyr`   | Data reshaping (pivoting, nesting)          |
| `readr`   | Reading CSVs and flat files efficiently     |
| `tibble`  | Tidyverse's version of `data.frame`         |
| `purrr`   | Functional programming (e.g. map functions) |
| `stringr` | String manipulation                         |
| `forcats` | Working with categorical/factor variables   |

You can find more information on each package [here](https://www.tidyverse.org/)

## Useful Functions 
Cleaning and tidying data is a crucial step before starting your analysis. R has many functionalities to make this easier. 

* <code>clean_names()</code> function from <code>Janitor</code> package helps us to fix messy variable names. 
* <code>View()</code> to open the dataset.
* <code>class</code> reports object type of type of data stored.
* <code>dim</code> reports the size of each one of an object's dimension.
* <code>names()</code> returns the names of variables in a dataset.
* <code>str()</code> general information on a R object.
* <code>summary</code> summary information about the variables in data frame.
* <code>head()</code> shows the first few observations in a dataset.
* <code>tail</code> shows the last few observations in a dataset.
  
## Version control

Version control is essential for collaborative and reproducible research in R. It allows researchers to track changes to scripts, collaborate effectively across teams, and maintain a clear history of edits over time.

### Recommended Tools:

* Git: The most widely used version control system. It tracks changes in R scripts, RMarkdown files, and data analysis projects.

* GitHub / GitLab / Bitbucket: Platforms for hosting Git repositories. These tools facilitate collaboration, code review, and project management.
  
### Integration with R:

RStudio has built-in Git support, allowing users to commit changes, push/pull from repositories, and view change history directly within the RStudio interface.

To enable Git in RStudio, install Git on your computer and configure Git with your user name and email. Link your RStudio project to a Git repository (via "New Project" > "Version Control" or by initializing Git in an existing project).

## RStudio projects

To set working directories on R, <code>setwd</code> is the direct equivalent of <code>cd</code> on Stata. However, we don't recommend using this. 
Instead, you should use RStudio projects and <code>here</code> library. <code>here</code> locates files relative to your project root. 
It uses the root project directory to build paths to files easily and allows for interoperability between different computers where the absolute path to the same file is not the same.  


### Additional Resources
* [R-bloggers post on best practices](https://www.r-bloggers.com/r-code-best-practices/)
* DIME Analytics, World Bank [R shiny training](https://github.com/dime-wb-trainings/shiny-training?tab=readme-ov-file/)
* Tidyverse Team, [Tidyverse style guide](https://style.tidyverse.org/)

### Related DIME Analytics Training
* Training session recording on [Introduction to R Shiny](https://osf.io/8sgrh/files/osfstorage/68387ddec1e467f319a4db5a/)
* Training session recording on [Big data workflows with R <code>data.table</code>](https://osf.io/8sgrh/files/osfstorage/65ac8ac0b1f2b501d5b0ef7d/)
  
[[Category: Coding Practices]]
