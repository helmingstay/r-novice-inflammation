
Novice R materials - following Python examples
--------------------------------------------------

* Draw concept map of where we are headed towards best scientific practices, and reproducibility.
* Its really important that you know what you did. More journals/grants/etc. are also making it important for them to know what you did.
* A lot of scientific code is NOT reproducible.
* If you keep a lab notebook, why are we not as careful with our code. 
* We edit each others manuscripts, but we don't edit each other's code. 
* If you write your code with "future you" in mind, you will save yourself and others a lot of time.

## Very basics of R

R is a versatile, open source programming/scripting language that's useful both for statistics but also data science. Inspired by the programming language S.  

* Open source software under GPL.  
* Superior (if not just comparable) to commercial alternatives. R has over 5,000 user contributed packages at this time. It's widely used both in academia and industry.  
* Available on all platforms.  
* Not just for statistics, but also general purpose programming.  
* Is object oriented and functional.  
* Large and growing community of peers.  

## Introduction to R and RStudio

Let's start by learning about our tool.  

_Point out the different windows in R._ 

Compare R in RStudio to R on the command line. Point out why it's nice to have all the extra views into what you're working on.

* Console, Scripts, Environments, Plots
* Avoid using shortcuts. 
* Code and workflow is more reproducible if we can document everything that we do.
* Our end goal is not just to "do stuff" but to do it in a way that anyone can easily and exactly replicate our workflow and results.
* Typing in console vs typing in text editor and sending to console. Always type in editor and send to console!
* Always add some comment lines to the top of your file with your name and date, and what the purpose of the script is

You can get output from R simply by typing in math
    

```r
3 + 5
12/7
```

or by typing words. Don't even have to type `print` like in python.


```r
"hello world"
```

We can annotate our code (take notes) by typing "#". Everything to the right of # is ignored by R

We can save our results to an object, if we give it a name


```r
a     <- 60 * 60
hours <- 365 * 24
```


Some of the same commands we will learn on the command line can be used in R.
List objects in your current environment


```r
ls()
```

Remove objects from your current environment.  


```r
x <- 5
rm(x)
```

Remove all objects from your current environment. Typing `x` on the console will give you an error.


```r
rm(list = ls())
```

Notice that we have _nested_ one function inside of another.  

Use # signs to comment. Comment liberally in your R scripts. Anything to the right of a # is ignored by R.  

__Assignment operator__

`<-` is the assignment operator. Assigns values on the right to objects on the left. Mostly similar to `=` but not always. Learn to use `<-` as it is good programming practice. Using `=` in place of `<-` can lead to issues down the line.

__Package management__

`install.packages("package-name")` will download a package from one of the CRAN mirrors assuming that a binary is available for your operating system. If you have not set a preferred CRAN mirror in your options(), then a menu will pop up asking you to choose a location.

Use `old.packages()` to list all your locally installed packages that are now out of date. `update.packages()` will update all packages in the known libraries interactively. This can take a while if you haven't done it recently. To update everything without any user intervention, use the `ask = FALSE` argument.


```r
update.packages(ask = FALSE)
```

The RStudio GUI option for updating packages is also quite useful, but it's good to know how to do it in a script so you can make sure it's done automatically.

## Data types

__Understanding basic data types in R__

To make the best of the R language, you'll need a strong understanding of the basic data types and data structures and how to operate on those.

Very Important to understand because these are the objects you will manipulate on a day-to-day basis in R. Dealing with object conversions is one of the most common sources of frustration for beginners.

Everything in R is an object.

R has 6 (although we will not discuss the raw class for this workshop) atomic classes.

* character
* numeric (real or decimal)
* integer
* logical
* complex

__Example Type__

* “a”, “swc”	character
* 2, 15.5	numeric
* 2 (Must add a L at end to denote integer)	integer
* TRUE, FALSE	logical
* 1+4i	complex

`typeof()` - what is it?  
`length()` - how long is it? What about two dimensional objects?  
`attributes()` - does it have any metadata?  


```r
# Example
x <- "dataset"
typeof(x)
attributes(x)

y <- 1:10
typeof(y)
length(y)
attributes(y)

z <- c(1L, 2L, 3L)
typeof(z)
```

## Data Structures

R has many different structures for storing the data you want to
analyze. The most commonly used are

- vectors,
- lists,
- matrices,
- arrays, and 
- data frames.

It can be determined with the function `class()`.

The *type* or *mode* of an object defines how it is stored. It could
be

- a character,
- a numeric value,
- an integer,
- a complex number, or
- a logical value (Boolean value: TRUE/FALSE).

It can be determined with the function `mode()`.

Below is a short definition  and quick example of each of these data
structures which you can use to decide which is the best for
representing your data  in R.

## Vectors
It is the most basic data type. Vectors only have one dimension and
all their elements must be the same mode. There are various ways to
create vectors. The simplest one is with the `c` function.


```r
v1 <- c(1, 2, 5)
```

The `c` function allows to combine its arguments. If the arguments
are of various modes, they will be reduced to their lowest common
type:


```r
v2 <- c(1, 3, "a")
mode(v2)
```

Objects can be explicitly coerced with the `as.` function.


```r
as.character(v1)
```

You can also use the `:` operator or the `seq` function:


```r
1:10
seq(from = 5, to = 25, by = 5)
```

## Factors
Factor is a special type of vector to store categorical values.


```r
breed <- factor(c("Holstein", "Holstein", "Brown Swiss", "Holstein",
                  "Ayrshire", "Canadian", "Canadian", "Brown Swiss",
                  "Holstein", "Brown Swiss", "Holstein"))
```
It stores values as a set of labeled integers. Some functions treat
factors differently from numeric vectors.


```r
table(breed)
```

## Lists
A list is an ordered collection of objects where the objects can be of
different modes.


```r
l <- list("a", "b", "c")
```

Each element of a list can be given a name and referred to by that
name. Elements of a list can be accessed by their number or their name.


```r
cow <- list(breed = "Holstein", age = 3, last.prod = c(25, 35, 32))
cow$breed
cow[[1]]
```

Lists can be used to hold together multiple values returned from a
function. For example the elements used to create an histogram can be
saved and returned.  The `islands` data set is the area of major islands 
over 10,000 square miles (in thousands of square miles).


```r
h <- hist(islands)
```

![plot of chunk unnamed-chunk-18](figure/unnamed-chunk-18-1.png) 

```r
str(h)
```

The function `str` is used here. It stands for *structure* and shows
the internal structure of an R object.

## Matrices
A matrix is a rectangular array of numbers. Technically, it is a
vector with two additional attributes: number of rows and number of
columns. This is what you would use to analyze a spreadsheet full of
only numbers, or only words. You can create a matrix with the `matrix`
function:


```r
m <- rbind(c(1, 4), c(2, 2))
m <- matrix(data = 1:12, nrow = 4, ncol = 3,
            dimnames = list(c("cow1", "cow2", "cow3", "cow4"),
                c("milk", "fat", "prot")))
```

## Arrays
If a matrix is a two-dimensional data structure, we can add *layers*
to the data and have further dimensions in addition to rows and
columns. These datasets would be arrays. It can be
created with the `array` function:


```r
a <- array(data = 1:24, dim = c(3, 4, 2))
```

## Data frames
Data frames are used to store tabular data: multiple rows, columns and
format.


```r
df <- data.frame(cow = c("Moo-Moo", "Daisy", "Elsie"),
                 prod = c(35, 40, 28),
                 pregnant = c(TRUE, FALSE, TRUE))
```

### __Useful functions__

* `head()` - see first 6 rows
* `tail()` - see last 6 rows
* `dim()` - see dimensions
* `nrow()` - number of rows
* `ncol()` - number of columns
* `str()` - structure of each column
* `names()` - will list the names attribute for a data frame (or any object really), which gives the column names.
* A data frame is a special type of list where every element of the list has same length.

See that it is actually a special list:


```r
is.list(iris)
class(iris)
```

| Dimensions | Homogenous | Heterogeneous |
| ------- | ---- | ---- |
| 1-D | atomic vector | list |
| 2-D | matrix | data frame |

### __Indexing__

Vectors have positions, these positions are ordered and can be called using name_vector[index]


```r
letters[2]
```

### __Functions__

A function is a saved object that takes inputs to perform a task. 
Functions take in information and return desired outputs.

output = name_of_function(inputs)


```r
x <- 1:10
y <- sum(x)
```

### __Help__

All functions come with a help screen. 
It is critical that you learn to read the help screens since they provide important information on what the function does, 
how it works, and usually sample examples at the very bottom.

### __Install new functions__

To install any new package `install.packages('ggplot2')`
