# Introduction to Tidy Data in R

<a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license"><img style="border-width: 0;" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png" alt="Creative Commons License" /></a>
This tutorial is licensed under a <a href="http://creativecommons.org/licenses/by-nc/4.0/" rel="license">Creative Commons Attribution-NonCommercial 4.0 International License</a>.

## Lab Goals

Data sets are stored in tabular format and there are many possible ways to organize tabular data. Some organizational schemes are designed to be easily read on the page (or screen), while others are designed to be easily used in analysis. In this tutorial, we focus on best practices for how a data set should be formatted for analysis in `R`.

Lab overview videos (Panopto, ND users):
- [Tidy Data Principles](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=6a08f05f-a3d5-4567-83d8-acd1003f312b) (10 minutes)
- [RStudio Tidy Data Lab Overview](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=b0bc9f58-3cc4-4bb8-a8df-acd1003f30d1) (20 minutes)

## Acknowledgements

This lab procedure is adapted from and based on Ryan Miller's ["Introduction to Tidy Data in R"](https://remiller1450.github.io/s230f19/Tidy_Data.html) (Fall 2019, Intro to Data Science STA 230 course, Grinnell College).

Links to lab overview videos (Panopto, ND users):
- [Tidy data principles](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=10b00206-2811-4138-af9b-acd10034d5e1)
- [Tidy data in RStudio](https://notredame.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=4753c4a6-2c49-4a33-9edc-acd100389c55)

# Table of Contents

- [Overview](#overview)
  * [Tidy Data Principles](#tidy-data-principles)
  * [Common Spreadsheet Errors](#common-spreadsheet-errors)
- [Defining Tidy Data](#defining-tidy-data)
  * [Tidy Data Syntax](#tidy-data-syntax)
  * [Visualizing Tidy Data](#visualizing-tidy-data)
- [Data and Environment Setup](#data-and-environment-setup)
- [Case Studies](#case-studies)
  * [Tidying Longitudinal Data Using `gather`](#tidying-longitudinal-data-using-gather)
  * [Tidying Pollster Data Using `separate` and `gather`](#tidying-pollster-data-using-separate-and-gather)
  * [Tidying Crash Data Using `gather` + `separate` + `spread`](#tidying-crash-data-using-gather--separate--spread)
- [Additional Resources](#additional-resources)
- [Additional Questions](#additional-questions)
- [Lab Notebook Questions](#lab-notebook-questions)

[Click here](https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/tidy-data-r-intro-markdown.Rmd) and select the "Save As" option to download this lab as an RMarkdown file.

# Overview

1. Hadley Wickham's 2014 article in the *Journal of Statistical Software* outlines the foundations and principles of tidy data. 

2. Article abstract: "A huge amount of effort is spent cleaning data to get it ready for analysis, but there has been little research on how to make data cleaning as easy and effective as possible. This paper tackles a small, but important, component of data cleaning: data tidying. Tidy datasets are easy to manipulate, model and visualize, and have a specific structure: each variable is a column, each observation is a row, and each type of observational unit is a table. This framework makes it easy to tidy messy datasets because only a small set of tools are needed to deal with a wide range of un-tidy datasets. This structure also makes it easier to develop tidy tools for data analysis, tools that both input and output tidy datasets. The advantages of a consistent data structure and matching tools are demonstrated with a case study free from mundane data manipulation chores." (Hadley Wickham, Tidy Data, Vol. 59, Issue 10, Sep 2014, Journal of Statistical Software. http://www.jstatsoft.org/v59/i10.)

3. Wickham's tidy data principles have become widely used in data science and other statistical software applications. 

4. To prepare for this lab, we read Karl W. Broman and Kara H. Woo's 2018 "Data Organization in Spreadsheets" from *The American Statistician*. 

5. Article abstract: "Spreadsheets are widely used software tools for data entry, storage, analysis, and visualization. Focusing on the data entry and storage aspects, this article offers practical recommendations for organizing spreadsheet data to reduce errors and ease later analyses. The basic principles are: be consistent, write dates like YYYY-MM-DD, do not leave any cells empty, put just one thing in a cell, organize the data as a single rectangle (with subjects as rows and variables as columns, and with a single header row), create a data dictionary, do not include calculations in the raw data files, do not use font color or highlighting as data, choose good names for things, make backups, use data validation to avoid data entry errors, and save the data in plain text files." ( Karl W. Broman & Kara H. Woo (2018) Data Organization in Spreadsheets, The American Statistician, 72:1, 2-10, DOI: 10.1080/00031305.2017.1375989)

## Tidy Data Principles?

6. Designing spreadsheets that are “tidy, consistent, and as resistant to mistakes as possible” (2)

7. Be Consistent:
  * Use consistent codes for categorical variables
  * Use a consistent fixed code for any missing values
  * Use consistent variable names
  * Use consistent subject identifiers
  * Use a consistent data layout in multiple files
  * Use consistent file names
  * Use a consistent format for all dates
  * Use consistent phrases in your notes
  * Be careful about extra spaces within cells

8. Choose Good Names for Things:
  * Avoid spaces
  * Avoid special characters
  * Be short but meaningful

9. Write Dates as YYYY-MM-DD
  * Or have separate columns for YEAR, MONTH, DATE

10. No Empty Cells

11. Put Just One Thing in a Cell

12. Make it a Rectangle
  * Single first row with variable names

13.- Create a Data Dictionary
  * “This is part of the metadata that you will want to prepare: information about the data” (6)
  * You might also find this information in a codebook that goes with a dataset
  * Things to include:
    * The exact variable name as in the data file
    * A version of the variable name that might be used in data visualizations
    * A longer explanation of what the variable means
    * The measurement units
    * Expected minimum and maximum values

14. No Calculations in the Raw Data Files

15. Do Not Use Font Color or Highlighting as Data

16. Make Backups
  * Multiple locations (OneDrive, local computer, etc.)
  * Version control program (i.e. Git)
  * Write protect the file when not entering data

17. Use Data Validation to Avoid Errors

18. Save a Copy of the Data in Plain Text Files
  * File formats can include comma-separated values (CSV) or plain-text (TXT)
  
19. The principles are also available as a PDF in this repo.

## Common Spreadsheet Errors

20. As described in Library Carpentry's ["Tidy data for librarians" tutorial](https://librarycarpentry.org/lc-spreadsheets/02-common-mistakes/index.html), common formatting problems for data in spreadsheets include:

- Multiple tables
- Multiple tabs
- Not filling in zeros
- Using bad null values
- Using formatting to convey information
- Using formatting to make the data sheet look pretty
- Placing comments or units in cells
- More than one piece of information in a cell
- Field name problems
- Special characters in data
- Inclusion of metadata in data table
- Date formatting

<blockquote>Q1: What questions do you have about these principles? Which ones are unclear are confusing?</blockquote>

# Defining Tidy Data

21. `R` is best-suited to working with data that follows five core rules:
  * Every variable is stored in its own column
  * Every observation is stored in its own row--that is, every row corresponds to a single case
  * Each value of a variable is stored in a cell of the table
  * Values should not contain units. Rather, units should be specified in the supporting documentation forthe data set, often called a codebook
  * There should be no extraneous information in the table (footnotes, table title, etc.)

22. A dataset satisfying  these rules is said to be "tidy."

23. NOTE: Most of the time data that violate rules 4 and 5 are obviously not tidy, and there are easy ways to exclude footnotes and titles in spreadsheets by simply omitting the offending rows. 

24. This lab focuses on the first three rules.

##  Tidy Data Syntax

25. This lab will describe the following `tidyr` commands, which can be thought of as verbs for tidying data:

Command | Meaning
--- | ---
`gather` | collapses multiple columns into two columns
`spread` | creates multiple columns from two columns
`separate` | splits compound variables into individual columns

## Visualizing Tidy Data

<p align="center"><a href="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.1.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.1.png?raw=true" /></a></p>

Figure 12.1: Following three rules makes a dataset tidy: variables are in columns, observations are in rows, and values are in cells.
From: Garrett Grolemund and Hadley Wickham, [R for Data Science](https://r4ds.had.co.nz/tidy-data.html) (O’Reilly, 2017)

<p align="center"><a href="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.2.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.2.png?raw=true" /></a></p>

Figure 12.2. Garrett Grolemund and Hadley Wickham, [R for Data Science](https://r4ds.had.co.nz/tidy-data.html) (O’Reilly, 2017)

<p align="center"><a href="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.3.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.3.png?raw=true" /></a></p>

Figure 12.3. Garrett Grolemund and Hadley Wickham, [R for Data Science](https://r4ds.had.co.nz/tidy-data.html) (O’Reilly, 2017)

<p align="center"><a href="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.4.png?raw=true"><img class="aligncenter" src="https://github.com/kwaldenphd/tidy-data-r-intro/blob/main/figures/Figure_12.4.png?raw=true" /></a></p>

Figure 12.4. Garrett Grolemund and Hadley Wickham, [R for Data Science](https://r4ds.had.co.nz/tidy-data.html) (O’Reilly, 2017)

# Data and Environment Setup

26. Make sure that the following packages are installed and loaded:
```R
#install.packages("tidyr")
#install.packages("ggplot2")
#install.packages("readr")
library(tidyr)     # contains tools to tidy data
library(ggplot2)   # for plotting
library(readr)     # a package for parsing data
```

27. These packages are part of what is known as "the Tidyverse," in the RStudio user community.

28. According to https://www.tidyverse.org/, "the tidyverse is an opinionated collection of R packages designed for data science. All packages share an underlying design philosophy, grammar, and data structures."

29. To install and load all packages that are part of the `tidyverse` core, you can install the parent `tidyverse` package.
```R
install.packages("tidyverse")
library(tidyverse)
```
30. As of December 2020, the tidyverse core incldues the following packages: `ggplot2`, `dplyr`, `tidyr`, `readr`, `purrr`, `tibble`, `stringr`, `forcats`.

31. We are working with three tidyverse packages in this lab.

32. [`reader`](https://readr.tidyverse.org/) "provides a fast and friendly way to read rectangular data (like csv, tsv, and fwf). It is designed to flexibly parse many types of data found in the wild, while still cleanly failing when data unexpectedly changes"

33. [`tidyr`](https://tidyr.tidyverse.org/) "provides a set of functions that help you get to tidy data"

34. [`ggplot2`](https://ggplot2.tidyverse.org/) "is a system for declaratively creating graphics, based on The Grammar of Graphics. You provide the data, tell ggplot2 how to map variables to aesthetics, what graphical primitives to use, and it takes care of the details."

35. Load in the following datasets:
```R
UBSprices <- read.csv("https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/UBSprices.csv", as.is = TRUE)
polls <- read.csv("https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/rcp-polls.csv", na.strings = "--", as.is = TRUE)
airlines <- read.csv("https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/airline-safety.csv", as.is = TRUE)
```

36. [Google Drive link if needed (ND users only)](https://drive.google.com/drive/folders/1hOV-0vVsPbHs7RF9OJQzbFtSRy-wvYIs?usp=sharing)

# Case Studies

## Tidying Longitudinal Data Using `gather`

37. UBS is an international bank that reports prices of various staples in major cities every three years. 

38. The data set in UBSprices data set contains prices of a 1 kg bag of rice in the years 2003 and 2009 in major world cities. 

39. The data set was originally extracted from the `alr4` R package.

40. We can get header information about the `USBprices` dataset.
```R
head(USBprices)
```

41. This data set is not tidy because each row contains two cases: the city in 2003 and the city in 2009. 

42. Additionally, the column names `2003` and `2009` contain the year, which should be the value of a variable. 

43. In order to tidy these data, we need to:
  i. Reorganize the data so that each row corresponds to a city in a specific year
  ii. Create a single variable for the price of rice
  iii. Add a variable for year

44. To do this, we will use the `gather` function in the `tidyr` package. 

45. `gather` collapses multiple columns into two columns: a key column and a value column. 

46. The key will be the new variable containing the old column names and the value will contain the information recorded in the cells of the collapsed columns.

47. In our example, we want to collapse `rice2003` and `rice2009` into the key-value pair `year` and `price`. 

48. To do this, we use the following command:
```R
tidy_ubs <- gather(data = UBSprices, key = year, value = price, rice2003, rice2009)
head(tidy_ubs)
```

49. The first argument passed to `gather` should be the name of the data frame that is being tidied.

50. This syntax is true for all `tidyr` functions covered in this lab.

51. After specifying the data frame, the next two arguments specify the column names for the two new columns you are creating.

52. One column is called the key and the other is called the values.
- For those familiar with Python, this is similar to a dictionary's key-value pairs

53. After the first three arguments, specify the columns that you wish to collapse, separated by commas. 

54. Notice that the original column names are now listed in the key column and the original cell values are now all in one column.

<blockquote>Q2: Write code (with comments) that answers the following questions:
 <ul>
  <li>How are the number of rows adjusted by using the gather command? (Hint: Use dim(UBSprices) to determine how many rows are in the UBSprices data set and dim(tidy_ubs) to determine how many are in the tidy_ubs data set).</li>
  <li>How many rows would there be after using the gather command if the UBSprices data set had five columns of years: rice2003, rice2006, rice2009, rice2012, and rice2015?</li>
 </ul>
 </blockquote>

55. To finish tidying these data, we need to modify the year column by removing the word “rice” from each cell.

56. To do this, we can use the `parse_number` function in the readr package. 

57. This function drops any non-numeric characters in a character string.
```R
tidy_ubs$year <- parse_number(tidy_ubs$year)
head(tidy_ubs)
```

58. We now have a dataset that follows tidy data principles.

59. This data set started in a relatively tidy form, so why bother with tidying it?

60. Tidy data are typically required for summarizing and plotting data in `R`. 

61. For example, consider making a side-by-side boxplot using `ggplot` (we will learn more about `ggplot` in a future lab).
```R
qplot(data=tidy_ubs, x= factor(year), y=price, geom="boxplot")
```

62. This was straightforward since `tidy_ubs` was already tidy, but would have required extra manipulation in the original format.

## Tidying Pollster Data Using `separate` and `gather`

63. The polls data set contains the results of various presidential polls conducted during July 2016, and was scraped from [RealClear Politics](http://www.realclearpolitics.com/epolls/latest_polls/president/).

```R
polls
```

64. This dataset does not follow tidy data principles.

65. The `Date` column contains both the beginning and end dates. These should be stored in separate columns.

66. The `Sample` column contains two variables: the number of people in the sample and the population that was sampled (likely voters or registered voters). These should be stored in separate columns.

67. The last four column names are values of candidate and party variables, which should be stored in their own columns.

68. To break a single character column into multiple new columns we use the `separate` function in the `tidyr` package.

69. To begin, let’s break the `Date` column into `Begin` and `End` columns:

```R
tidy_polls <- separate(data = polls, col = Date, into = c("Begin", "End"), sep = " - ")
tidy_polls
```

70. The second argument `col` specifies the name of the column to be split.

71. The third argument `into` specifies the names of the new columns. Note that since these are specific column names we are creating, they should be given in quotes.

72. `R` will try to guess how the values should be separated by searching for non-alphanumeric values; however, if there are multiple non-alphanumeric values this may fail. 

73. In this example, if we did not specify that `sep = " - "`, then `R` would erroneously use `\` as the separator. 

74. To manually specify the separator between columns we can place the character(s) in quotes.

75. In `sep = " - "`, the spaces around `-` avoid excess whitespace in the resulting cell values.

76. We also need to separate the `Sample` column into `size` and `population` columns.
```R
tidy_polls <- separate(data = tidy_polls, col = Sample, into = c("size", "population"), sep = " ")
tidy_polls
```

77. Next, we need to gather the last four columns into a `candidate` variable.
```R
tidy_polls <- gather(data = tidy_polls, key = candidate, value = percentage, 7:10)
head(tidy_polls)
```

78. Notice that instead of writing out the column names (Clinton..D., Trump..R., etc.) we can simply specify the column numbers.

79. `7:10` specifies that we are gathering columns 7 through 10.

80. Finally, we need to separate the candidate names from the political party.
```R
tidy_polls <- separate(tidy_polls, candidate, into= c("candidate", "party"))
head(tidy_polls)
```

81. In the last command we let `R` guess which separator to use. 

82. This worked, but resulted in a warning message—we’re lucky that it worked! 

83. There are many situations where the separator is too complex for `R` to guess correctly and it cannot be specified using a simple character in quotes. 

84. In such cases we need to use regular expressions to aid our data tidying, but that’s a topic for another tutorial. 

85. The important thing to note here is that you should always check that `separate` worked as expected. 

86. When in doubt, check your output!

## Tidying Crash Data Using `gather` + `separate` + `spread`

87. The airlines data set contains the raw data behind the 2014 Nate Silver article ["Should Travelers Avoid Flying Airlines That Have Had Crashes in the Past?"](http://fivethirtyeight.com/features/should-travelers-avoid-flying-airlines-that-have-had-crashes-in-the-past/) that appeared on [fivethirtyeight.com](https://fivethirtyeight.com).

88. We can get some basic information about this dataset.
```R
head(airlines)
dim(airlines)
```

89. In this example, a `case` is best described as an airline in a specific time frame.

90. So these data are not tidy because each case is not its own row. 

91. Additionally, the last six column names contain the time frame, which is a value. 

92. To be tidy, this dataset needs to:
- have rows corresponding to airlines in a specific time frame
- create a `years` column to specify the time frame
- create columns for each type of accident: `incidents`, `fatal_accidents`, and `fatalities`

93. First, we gather the last six columns into a common accidents column. 

94. This will allow us to easily create the years column.
```R
tidy_airlines <- gather(airlines, key = accidents, value = count, 3:8)
head(tidy_airlines)
```

95. Next, we separate the values of the new accidents column into `var` (short for variable) and `years`. 

96. The default guessing scheme fails here, so we must specify `sep = "[.]"` to denote that the period is the separator. 

```R
tidy_airlines <- separate(tidy_airlines, accidents, into = c("var", "years"), sep = "[.]")
head(tidy_airlines)
```

97. To learn more about regular expressions in `RStudio`, check out [the RegEx Cheatsheet](https://github.com/rstudio/cheatsheets/blob/master/regex.pdf).

98. Finally, we need to ensure that each row corresponds to a case. (Don’t worry, this will also make each column a variable!) 

99. Currently, there are six rows for each airline: one for each var in each time frame. 

100. To solve this problem, we need to spread out the var column so that each variable has its own column.
```R
tidy_airlines <- spread(data = tidy_airlines, key = var, value = count)
head(tidy_airlines)
```

101. Notice that the first argument given to spread is the data frame, followed by the key-value pair. 

102. The key is the name of the column whose values will be used as column headings and the value is the name of the column whose values will populate the cells of the new columns. 

103. In this example, we use `var` as the key and populate the cells with the `count`.

# Additional Resources

104. [RStudio’s data wrangling cheat sheet](https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf) provides a nice summary of how to reshape data sets and a quick reminder of the definition of tidy data.

105. The [tidyr vignette](https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html) provides additional examples and elaborates on the capabilities of the tidyr package.

# Additional Questions

Q3: The file under5mortality.csv (available at https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/under5mortality.csv) contains the child mortality rate per 1,000 children born for each country from 1800 to 2015. (Source: https://www.gapminder.org/data/)
- Briefly describe why it is not considered to be tidy data and what changes need to be made to tidy it.
- Use `gather` to create a tidy data set with columns `country`, `year` and `mortality`. Use `parse_number` to ensure that the year column is numeric. 
  * Hint: you can change the column names of a data.frame object using the `colnames` function. 
  * For example, the code `colnames(mydata)[1] <- "newName"` will change the name of the first column to `“newName”`

Q4: The file HospitalAdmits.csv (available at https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/HospitalAdmits.csv) describes the general reasons for people being hospitalized in the financial years ranging from July 1993 to June 1998. The variable `Separations` describes how many patient discharges occured in that year, while the variable `PatientDays` describes how many days in total patients spent in the hospital for that reason.
- Briefly explain why it is not considered to be tidy data and what changes need to be made to tidy it.
- Use `gather` and `separate` to create a tidy data set with columns `IcdCode`, `IcdText`, `Year`, `Field`, and `Count`. 
- The `IcdCode` is the numeric component of `IcdChapter`
  * Hint: pay attention to variable types, you might need to coerce factor variables into character variables using the `as.character` function, and then convert the result to numeric using the `as.numeric` function

# Lab Notebook Questions

Q1: What questions do you have about these principles? Which ones are unclear are confusing?

Q2: Write code (with comments) that answers the following questions:
- How are the number of rows adjusted by using the gather command? (Hint: Use dim(UBSprices) to determine how many rows are in the UBSprices data set and dim(tidy_ubs) to determine how many are in the tidy_ubs data set).
- How many rows would there be after using the gather command if the UBSprices data set had five columns of years: rice2003, rice2006, rice2009, rice2012, and rice2015?

Q3: The file under5mortality.csv (available at https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/under5mortality.csv) contains the child mortality rate per 1,000 children born for each country from 1800 to 2015. (Source: https://www.gapminder.org/data/)
- Briefly describe why it is not considered to be tidy data and what changes need to be made to tidy it.
- Use `gather` to create a tidy data set with columns `country`, `year` and `mortality`. Use `parse_number` to ensure that the year column is numeric. 
  * Hint: you can change the column names of a data.frame object using the `colnames` function. 
  * For example, the code `colnames(mydata)[1] <- "newName"` will change the name of the first column to `“newName”`

Q4: The file HospitalAdmits.csv (available at https://raw.githubusercontent.com/kwaldenphd/tidy-data-r-intro/main/data/HospitalAdmits.csv) describes the general reasons for people being hospitalized in the financial years ranging from July 1993 to June 1998. The variable `Separations` describes how many patient discharges occured in that year, while the variable `PatientDays` describes how many days in total patients spent in the hospital for that reason.
- Briefly explain why it is not considered to be tidy data and what changes need to be made to tidy it.
- Use `gather` and `separate` to create a tidy data set with columns `IcdCode`, `IcdText`, `Year`, `Field`, and `Count`. 
- The `IcdCode` is the numeric component of `IcdChapter`
  * Hint: pay attention to variable types, you might need to coerce factor variables into character variables using the `as.character` function, and then convert the result to numeric using the `as.numeric` function
