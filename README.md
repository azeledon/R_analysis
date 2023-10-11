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

 ### what if we want to bring in a dataset from an application programming interface (API) query?

 The JSON format is one of the most common data formats returned from a URL request. Although native JSON data can be easier to work with in Python, many data scientists still prefer to use R for their data analysis. To accommodate this need, R developers created the ```jsonlite``` library to read in JSON data structures and convert them to an R data frame. Because the ```jsonlite``` library was not built into R, we must import it into our R environment.
 To import a library into R, we'll use the ```library(package)``` function. Just like in Python, it's good practice to import any required libraries at the top of our RScript.
 Let's try loading in our installed ```jsonlite``` package using the ```library(jsonlite)``` function. Be sure to write the statement in your RScript and then send the statement to your R console (Command + Enter for Mac or CTRL + Enter for Windows).

- Now that we have successfully imported our ```jsonlite``` package, we can use the ```fromJSON()``` function to read in a JSON file into R.

- First, type the following code into the R console to look at the ```fromJSON()``` documentation in the Help pane:

```?fromJSON()```

As we can see, we only need to provide the txt argument to properly read in a JSON file into R because the other parameters have default values indicated with equations (e.g. simplifyVector=True). ```txt``` is the file path of the JSON file on our machine. Alternatively, we can provide the ```fromJSON()``` function a JSON URL directly. Now let's practice reading in our first JSON file.

Place the downloaded data file in your active working directory. Next, use ```fromJSON()``` in our source RScript pane to read in the used car data into our R environment, as follows:

```demo_table2 <- fromJSON(txt='demo.json')```

Now that we know how to create data structures and data frames in R, let's learn how to **slice and sample** our datasets.

## Select Data in R

There are many ways to select and subset data in R, depending on what data structure is being used. When it comes to vectors, the easiest way to select data is using the bracket ("[ ]") notation. For example, if we have a numeric vector x with 10 values and want to select the third value, we would use the following statements:

```x <- c(3, 3, 2, 2, 5, 5, 8, 8, 9)```

```> x[3]```

Unlike Python, R's index starts at 1. So, the third element would be ```index = 3```

You can also use bracket notation to select data from two-dimensional data structures, such as matrices, data frames, and tibbles. For example, let's look at our ```demo_table``` again:

![](demo_table.png)

If we want to select the third row of the Year column using bracket notation, our statement would appear as follows:

```demo_table[3,"Year"]```

Because R keeps track of both the row indices as well as the column indices as integers under the hood, we can also select the same data using just number indices:

```demo_table[3,3]```

There is a third way to select data from an R data frame that behaves very similarly to Pandas. By using the $ operator, we can select columns from any two-dimensional R data structure as a single vector, similar to selecting a series from a Pandas DataFrame. For example, if we want to select the vector of vehicle classes from demo_table, we would use the following statement:

```demo_table$"Vehicle_Class"```

Once we have selected the single vector, we can use bracket notation to select a single value.

```demo_table$"Vehicle_Class"[2]```

## Select Data with Logic

Just as it is for selecting single values, there are multiple ways to subset and filter data from our larger data frames. As with most programming languages, we use a combination of operators and logical statements to tell R what data to filter. Thankfully, most operators are the same between R and Python, as shown below:

Category	    R Operator    	Description	              Python Equivalent
Arithmetical	+	              Addition operator	        +
              -	              Subtraction operator	    -
              *	              Multiplication operator	   *
              /	              Division operator	         /
              ^ or **	        Exponent operator	         **
              %%	            Modulus operator (finds the remainder of the first element divided by the second)	%

![](Relational.png)
![](Logical.png)
![](Miscellany.png)


One of the most common ways to filter and subset a dataset in R is to use bracket notation. To use bracket notation to filter a data frame, we can supply a logical statement to assert our row and columns.

For example, if we want to filter our used car data demo_table2 so that we only have rows where the vehicle price is greater than $10,000, we would use the following statement:

```filter_table <- demo_table2[demo_table2$price > 10000,]```

This filter statement generates a view-only data frame tab listing vehicles priced greater than $10,000

When our logical statements are simple (using only one or two operators), bracket notation is easy to read and write. However, if we need to filter and subset our data using more complicated logic, bracket notation can become cumbersome. In these cases, we'll use an R function such as ```subset()``` to filter our data.

## Subset Data in R

The subset() function uses a few arguments to subset and filter a two-dimensional R data structure:

- x
- subset
- select

For example, if we want to create a more elaborate filtered dataset from our used car data demo_table2 where price > 10000, drive == 4wd, and "clean" %in% title_status, we would use the following statement:

```filter_table2 <- subset(demo_table2, price > 10000 & drive == "4wd" & "clean" %in% title_status) #filter by price and drivetrain```

## Sample Data in R

Often in data science, we need to generate a random sample of data points from a larger dataset. For example, some models might take too long to run on a massive dataset and require a smaller sample of the data.

Using filtering and subsetting methods may be appropriate for certain cases (such as looking at data within a specific timeframe), but usually we'll want to randomly sample our larger data to reduce bias. In these cases, we can use the built-in function sample(). Let's try it now.

The sample() function uses a few arguments to create a sampled vector from a larger vector:

- x
- size
- replace

If we want to sample a large vector and create a smaller vector, we can set the vector to "x":

```sample(c("cow", "deer", "pig", "chicken", "duck", "sheep", "dog"), 4)```

When it comes to sampling a two-dimensional data structure, we need to supply the index of each row we want to sample. This process can be completed in three steps:

1. Create a numerical vector that is the same length as the number of rows in the data frame using the colon (:) operator.
2. Use the sample() function to sample a list of indices from our first vector.
3. Use bracket notation to retrieve data frame rows from sample list.

So, first capture the number of rows in demo_table in a variable. The nrow() function counts the number of rows in a dataframe.

```num_rows <- 1:nrow(demo_table)```

Next, sample 3 of those rows, as shown in this code:

``` sample_rows <- sample(num_rows, 3)```

Finally, retrieve the requested data within the demo_table:

``` demo_table[sample_rows,]```

If we want to combine all three steps in a single R statement, our code would be as follows:

```demo_table[sample(1:nrow(demo_table), 3),]```


 
 

