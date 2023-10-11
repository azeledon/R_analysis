# R_analysis

## Functions in R

```install.packages()```

```c()```

Regardless of where a function comes from, all R functions use the same basic syntax:

```
function_name <- function(arg1, arg2=T, …){

<BODY OF FUNCTION>

return <RETURN VALUE>
}
```

There are four components of an R function:

- The function name is the name of the function, which can be used in the R console to call the function itself.
- Just like Python methods, R functions can have any number of required or optional arguments, depending on the design of the function.
- The function body includes data structures, if-statements, and other logical statements that define what the function does.
- The return statement is the last evaluated statement before returning the resulting value out of the function.

If at any point you are unsure what an R function does or what it needs to execute, you can always type ```?<name of function>```  in the R console and it'll open the documentation in the Help pane. 

## Read and Write Using R

There are built-in R functions to import the most common data formats, such as comma-separated values (CSV) and JavaScript Object Notation (JSON)

- To read in a CSV file, we use R's ```read.csv()``` 

```?read.csv()```

- We can use ```read.csv()`` for comma-delimited files.
- ```read.delim()``` for tab-delimited files.
- ```read.table()```  if we need to manually tell the function what delimiter is used.

Although optional arguments are used to parse more complicated datasets, we'll only concentrate on the following arguments:

- file
- header
- sep
- check.names
- stringsAsFactors

To practice reading in a CSV file, first download our sample CSV file demo.csv

- After ```demo.csv``` has downloaded, place the data file into your active working directory.
- Next, we'll use ```read.csv()``` in our source RScript pane to read in the demo file into our R environment.
- Type the following code:

  ```demo_table <- read.csv(file='demo.csv',check.names=F,stringsAsFactors = F)```

- There are two ways to send RScript lines to our R console. We can either use the "Run" button in the top-right source pane or use the following shortcut:

**Command + Enter (Mac)**
**CTRL + Enter (Windows)**
