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

*Be descriptive: Use names that clearly describe what the object represents. For example, use <code>total_income</code> instead of <code>x</code> or <code>ti</code>.

*'''Use lowercase letters:''' Stick to lowercase letters and use underscores (_) to separate words. This style is consistent with tidyverse conventions and improves readability (household_id, not HouseholdID or houseHoldId).

*'''Avoid abbreviations:''' Unless widely recognized (e.g., GDP, ID, ISO), avoid abbreviations that may not be clear to others.

*'''Don't overwrite base functions:''' Avoid naming objects data, mean, sum, T, c, etc., which are already used by R and can lead to hard-to-spot bugs.

*'''Consistency is key:''' Pick a style and stick with it throughout your project (e.g., always use snake_case or always use dot.case, but don’t mix them).

#### For Example;
*<code>survey_data_2023</code>: Descriptive and specific

*<code>income_total</code>: Meaningful variable name 

*<code>calculate_growth</code>: Action-based function name 

*<code>beneficiary_status</code>: Clear and readable

## Style and white space
Following consistent style and white space conventions in R code improves readability, helps with debugging, and facilitates collaboration across teams. At DIME, we recommend adhering to the [https://style.tidyverse.org/ Tidyverse style guide] with some team-specific adjustments. Below are key points to follow:

### 1. Indentation:
*Use two spaces for indentation, not tabs.
*Nested structures (like if, for, or pipes) should be indented to reflect logical structure.

<code>if (condition) {
  do_something()
}</code>

### 2. Line Length

*Keep lines under 80 characters when possible.
*Break long lines logically, especially for pipes, put each step on a new line and indent.

 <code>data %>%
   filter(x > 0) %>%
   group_by(id) %>%
   summarise(mean_val = mean(value))</code>

### 3. Spaces:

*Add spaces around operators: <code>x <- 1</code>, not <code>x<-1</code>.
*No space before a comma; one space after a comma: <code>c(1, 2, 3)</code>.
*No space inside parentheses or square brackets: <code>mean(x)</code>, not <code>mean( x )</code>.

## Loops in R


## Tidyverse

## Version control

## RStudio projects

### Additional Resources
* [https://www.r-bloggers.com/r-code-best-practices/| R-bloggers post on best practices]
* DIME Analytics, World Bank [https://github.com/dime-wb-trainings/shiny-training?tab=readme-ov-file/ shiny training]
* Tidyverse Team, [https://style.tidyverse.org/ Tidyverse style guide]

==Related DIME Analytics Trainings==
* Training session recording on [https://osf.io/8sgrh/files/osfstorage/68387ddec1e467f319a4db5a/ Introduction to R Shiny]
* Training session recording on [https://osf.io/8sgrh/files/osfstorage/65ac8ac0b1f2b501d5b0ef7d/ Big data workflows with R <code>data.table</code>]
[[Category: Coding Practices]]
