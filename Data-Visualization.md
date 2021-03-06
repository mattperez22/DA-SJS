Data Visualization
================
Matthew Perez
8/21/2020

# Data Visualization

### 3.1 Introduction

``` r
# we must load the tidyverse library every session
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ───────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### 3.2 First Steps

QUESTION: Do cars with big engines use more gas than cars with small
engines?

##### 3.2.1 The mpg data frame

A data frame is a rectangular collection of variables (in the columns)
and observations (in the rows). mpg contains observations collected by
the US Environmental Protection Agency on 38 models of car.

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

##### 3.2.2 Creating a ggplot

With ggplot2, you begin a plot with the function ggplot(). ggplot()
creates a coordinate system that you can add layers to. The first
argument of ggplot() is the dataset to use in the graph.

You complete your graph by adding one or more layers to ggplot(). The
function geom\_point() adds a layer of points to your plot, which
creates a scatterplot.

Each geom function in ggplot2 takes a mapping argument. This defines how
variables in your dataset are mapped to visual properties. The mapping
argument is always paired with aes(), and the x and y arguments of aes()
specify which variables to map to the x and y axes. ggplot2 looks for
the mapped variables in the data argument, in this case, mpg.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

The plot shows a negative relationship between engine size (displ) and
fuel efficiency (hwy). In other words, cars with big engines use more
fuel. Does this confirm or refute your hypothesis about fuel efficiency
and engine size?

##### Exercises

> 1.  Run ggplot(data = mpg). What do you see?

This code creates an empty plot. The ggplot() function creates the
background of the plot, but since no layers were specified with geom
function, nothing is drawn.

``` r
ggplot(data = mpg)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

> 2.  How many rows are in mpg? How many columns?

There are 234 rows and 11 columns in the mpg data frame.

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

> 3.  What does the drv variable describe? Read the help for ?mpg to
>     find out.

The drv variable is a categorical variable which categorizes cars into
front-wheels, rear-wheels, or four-wheel drive.

``` r
?mpg
```

> 4.  Make a scatterplot of hwy vs cyl.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = cyl, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

> 5.  What happens if you make a scatterplot of class vs drv? Why is the
>     plot not useful?

A scatter plot is not useful in this case because both variables are
CATEGORICAL, it doesn’t show us how many observations there are of each
variable. Scatter plots are better suited for plotting continuous
variables.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = class, y = drv))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### 3.3 Aesthetic mappings

You can convey information about your data by mapping the aesthetics in
your plot to the variables in your dataset. For example, you can map the
colors of your points to the class variable to reveal the class of each
car.

To map an aesthetic to a variable, associate the name of the aesthetic
to the name of the variable inside aes(). ggplot2 will automatically
assign a unique level of the aesthetic (here a unique color) to each
unique value of the variable, a process known as scaling. ggplot2 will
also add a legend that explains which levels correspond to which values.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

In the above example, we mapped class to the color aesthetic, but we
could have mapped class to the size aesthetic in the same way. In this
case, the exact size of each point would reveal its class affiliation.
We get a warning here, because mapping an unordered variable (class) to
an ordered aesthetic (size) is not a good idea.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

    ## Warning: Using size for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

Or we could have mapped class to the alpha aesthetic, which controls the
transparency of the points, or to the shape aesthetic, which controls
the shape of the points.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

What happened to the SUVs? ggplot2 will only use six shapes at a time.
By default, additional groups will go unplotted when you use the shape
aesthetic.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data-Visualization_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

For each aesthetic, you use aes() to associate the name of the aesthetic
with a variable to display. The aes() function gathers together each of
the aesthetic mappings used by a layer and passes them to the layer’s
mapping argument. The syntax highlights a useful insight about x and y:
the x and y locations of a point are themselves aesthetics, visual
properties that you can map to variables to display information about
the data.

Once you map an aesthetic, ggplot2 takes care of the rest. It selects a
reasonable scale to use with the aesthetic, and it constructs a legend
that explains the mapping between levels and values. For x and y
aesthetics, ggplot2 does not create a legend, but it creates an axis
line with tick marks and a label. The axis line acts as a legend; it
explains the mapping between locations and values.

You can also set the aesthetic properties of your geom manually. For
example, we can make all of the points in our plot blue:

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

##### 3.3.1 Exercises

> 1.  What’s gone wrong with this code? Why are the points not blue?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

The argument color = “blue” is included within the mapping argument, and
as such, it is treated as an aesthetic, which is a mapping between a
variable and a value.

The following code does produces the expected result.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), colour = "blue")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

> 2.  Which variables in mpg are categorical? Which variables are
>     continuous? (Hint: type ?mpg to read the documentation for the
>     dataset). How can you see this information when you run mpg?

``` r
?mpg
```

> 3.  Map a continuous variable to color, size, and shape. How do these
>     aesthetics behave differently for categorical vs. continuous
>     variables?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
# THIS CODE WON'T WORK
# ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = cty))
```

> 4.  What happens if you map the same variable to multiple aesthetics?

REDUNDANT

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

> 6.  What happens if you map an aesthetic to something other than a
>     variable name, like aes(colour = displ \< 5)? Note, you’ll also
>     need to specify x and y.

Aesthetics can also be mapped to expressions like displ \< 5. The
ggplot() function behaves as if a temporary variable was added to the
data with values equal to the result of the expression. In this case,
the result of displ \< 5 is a logical variable which takes values of
TRUE or FALSE.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

### 3.5 Facets

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

##### 3.5.1 Exercises

> 1.  What happens if you facet on a continuous variable?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ cty, nrow = 1)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

> 2.  What do the empty cells in plot with facet\_grid(drv \~ cyl) mean?
>     How do they relate to this plot?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = drv, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

> 3.  What plots does the following code make? What does . do?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ .)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(. ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

> 4.  Take the first faceted plot in this section: What are the
>     advantages to using faceting instead of the colour aesthetic? What
>     are the disadvantages? How might the balance change if you had a
>     larger dataset?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

Advantages of encoding class with facets instead of color include the
ability to encode more distinct categories. For me, it is difficult to
distinguish between the colors of “midsize” and “minivan”.

Given human visual perception, the max number of colors to use when
encoding unordered categorical (qualitative) data is nine, and in
practice, often much less than that. Displaying observations from
different categories on different scales makes it difficult to directly
compare values of observations across categories. However, it can make
it easier to compare the shape of the relationship between the x and y
variables across categories.

Disadvantages of encoding the class variable with facets instead of the
color aesthetic include the difficulty of comparing the values of
observations between categories since the observations for each category
are on different plots. Using the same x- and y-scales for all facets
makes it easier to compare values of observations across categories, but
it is still more difficult than if they had been displayed on the same
plot. Since encoding class within color also places all points on the
same plot, it visualizes the unconditional relationship between the x
and y variables; with facets, the unconditional relationship is no
longer visualized since the points are spread across multiple plots.

The benefit of encoding a variable with facetting over encoding it with
color increase in both the number of points and the number of
categories. With a large number of points, there is often overlap. It is
difficult to handle overlapping points with different colors color.
Jittering will still work with color. But jittering will only work well
if there are few points and the classes do not overlap much, otherwise,
the colors of areas will no longer be distinct, and it will be hard to
pick out the patterns of different categories visually. Transparency
(alpha) does not work well with colors since the mixing of overlapping
transparent colors will no longer represent the colors of the
categories. Binning methods already use color to encode the density of
points in the bin, so color cannot be used to encode categories.

As the number of categories increases, the difference between colors
decreases, to the point that the color of categories will no longer be
visually distinct.

> 5.  Read ?facet\_wrap. What does nrow do? What does ncol do? What
>     other options control the layout of the individual panels? Why
>     doesn’t facet\_grid() have nrow and ncol arguments?

> 6.  When using facet\_grid() you should usually put the variable with
>     more unique levels in the columns. Why?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(cyl ~ cty)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->
