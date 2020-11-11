Data Transformation/Wrangling
================
Matthew Perez
8/21/2020

### 5.1 Introduction

##### 5.1.1 Prerequisites

``` r
library(nycflights13)
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(Lahman)
```

##### 5.1.2 nycflights13

``` r
flights
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

##### 5.1.3 dplyr basics

In this chapter you are going to learn the five key dplyr functions that
allow you to solve the vast majority of your data manipulation
challenges:

*Pick observations by their values (filter()). *Reorder the rows
(arrange()). *Pick variables by their names (select()). *Create new
variables with functions of existing variables (mutate()). \*Collapse
many values down to a single summary (summarize()).

These can all be used in conjunction with group\_by() which changes the
scope of each function from operating on the entire dataset to operating
on it group-by-group. These six functions provide the verbs for a
language of data manipulation.

All verbs work similarly:

  - 1.  The first argument is a data frame.

  - 2.  The subsequent arguments describe what to do with the data
        frame, using the variable names (without quotes).

  - 3.  The result is a new data frame.

Together these properties make it easy to chain together multiple simple
steps to achieve a complex result. Let’s dive in and see how these verbs
work.

### 5.2 Filter rows with filter()

filter() allows you to subset observations based on their values. The
first argument is the name of the data frame. The second and subsequent
arguments are the expressions that filter the data frame. For example,
we can select all flights on January 1st with:

``` r
filter(flights, month == 1, day == 1)
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 832 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
    ## #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
    ## #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
jan1 <- filter(flights, month == 1, day == 1)
```

``` r
jan1
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 832 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
    ## #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
    ## #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
(jan1 <- filter(flights, month == 1, day == 1))
```

    ## # A tibble: 842 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 832 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
    ## #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
    ## #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

##### 5.2.2 Comparisons

To use filtering effectively, you have to know how to select the
observations that you want using the comparison operators. R provides
the standard suite: \>, \>=, \<, \<=, \!= (not equal), and == (equal).

When you’re starting out with R, the easiest mistake to make is to use =
instead of == when testing for equality.

``` r
#filter(flights, month = 1)
```

There’s another common problem you might encounter when using ==:
floating point numbers. These results might surprise you\!

``` r
sqrt(2) ^ 2 == 2
```

    ## [1] FALSE

Computers use finite precision arithmetic (they obviously can’t store an
infinite number of digits\!) so remember that every number you see is an
approximation. Instead of relying on ==, use near():

##### 5.2.2 Logical operators

Multiple arguments to filter() are combined with “and”: every expression
must be true in order for a row to be included in the output. For other
types of combinations, you’ll need to use Boolean operators yourself: &
is “and”, | is “or”, and \! is “not”.

The following code finds all flights that departed in November or
December:

``` r
filter(flights, month == 11 | month == 12)
```

    ## # A tibble: 55,403 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    11     1        5           2359         6      352            345
    ##  2  2013    11     1       35           2250       105      123           2356
    ##  3  2013    11     1      455            500        -5      641            651
    ##  4  2013    11     1      539            545        -6      856            827
    ##  5  2013    11     1      542            545        -3      831            855
    ##  6  2013    11     1      549            600       -11      912            923
    ##  7  2013    11     1      550            600       -10      705            659
    ##  8  2013    11     1      554            600        -6      659            701
    ##  9  2013    11     1      554            600        -6      826            827
    ## 10  2013    11     1      554            600        -6      749            751
    ## # … with 55,393 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

The order of operations doesn’t work like English. You can’t write
filter(flights, month == (11 | 12)), which you might literally translate
into “finds all flights that departed in November or December”. Instead
it finds all months that equal 11 | 12, an expression that evaluates to
TRUE. In a numeric context (like here), TRUE becomes one, so this finds
all flights in January, not November or December. This is quite
confusing\!

A useful short-hand for this problem is x %in% y. This will select every
row where x is one of the values in y. We could use it to rewrite the
code above:

``` r
(nov_dec <- filter(flights, month %in% c(11, 12)))
```

    ## # A tibble: 55,403 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    11     1        5           2359         6      352            345
    ##  2  2013    11     1       35           2250       105      123           2356
    ##  3  2013    11     1      455            500        -5      641            651
    ##  4  2013    11     1      539            545        -6      856            827
    ##  5  2013    11     1      542            545        -3      831            855
    ##  6  2013    11     1      549            600       -11      912            923
    ##  7  2013    11     1      550            600       -10      705            659
    ##  8  2013    11     1      554            600        -6      659            701
    ##  9  2013    11     1      554            600        -6      826            827
    ## 10  2013    11     1      554            600        -6      749            751
    ## # … with 55,393 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Sometimes you can simplify complicated subsetting by remembering De
Morgan’s law: \!(x & y) is the same as \!x | \!y, and \!(x | y) is the
same as \!x & \!y. For example, if you wanted to find flights that
weren’t delayed (on arrival or departure) by more than two hours, you
could use either of the following four filters:

``` r
filter(flights, !(dep_delay > 120) & !(arr_delay > 120))
```

    ## # A tibble: 316,050 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 316,040 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
filter(flights, !(dep_delay > 120), !(arr_delay > 120)) #same as above, but with commas
```

    ## # A tibble: 316,050 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 316,040 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
filter(flights, !(arr_delay > 120 | dep_delay > 120)) #De Morgan's Law
```

    ## # A tibble: 316,050 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 316,040 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
filter(flights, arr_delay <= 120 & dep_delay <= 120)
```

    ## # A tibble: 316,050 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 316,040 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

##### 5.2.3 Missing values

One important feature of R that can make comparison tricky are missing
values, or NAs (“not availables”). NA represents an unknown value so
missing values are “contagious”: almost any operation involving an
unknown value will also be unknown.

``` r
100 == NA
```

    ## [1] NA

``` r
2 > NA
```

    ## [1] NA

``` r
x <- NA
is.na(x)
```

    ## [1] TRUE

How do I get rid of NA’s on my dataset?

``` r
(
withoutNA <- filter(flights, !is.na(dep_time))
)
```

    ## # A tibble: 328,521 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 328,511 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

##### 5.2.4 Exercises

> 1.  Find all flights that

Had an arrival delay of two or more hours

``` r
filter(flights, arr_delay >= 120)
```

    ## # A tibble: 10,200 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      811            630       101     1047            830
    ##  2  2013     1     1      848           1835       853     1001           1950
    ##  3  2013     1     1      957            733       144     1056            853
    ##  4  2013     1     1     1114            900       134     1447           1222
    ##  5  2013     1     1     1505           1310       115     1638           1431
    ##  6  2013     1     1     1525           1340       105     1831           1626
    ##  7  2013     1     1     1549           1445        64     1912           1656
    ##  8  2013     1     1     1558           1359       119     1718           1515
    ##  9  2013     1     1     1732           1630        62     2028           1825
    ## 10  2013     1     1     1803           1620       103     2008           1750
    ## # … with 10,190 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Flew to Houston (IAH or HOU)

``` r
filter(flights, dest == 'IAH' | dest == 'HOU')
```

    ## # A tibble: 9,313 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      623            627        -4      933            932
    ##  4  2013     1     1      728            732        -4     1041           1038
    ##  5  2013     1     1      739            739         0     1104           1038
    ##  6  2013     1     1      908            908         0     1228           1219
    ##  7  2013     1     1     1028           1026         2     1350           1339
    ##  8  2013     1     1     1044           1045        -1     1352           1351
    ##  9  2013     1     1     1114            900       134     1447           1222
    ## 10  2013     1     1     1205           1200         5     1503           1505
    ## # … with 9,303 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
filter(flights, dest %in% c('IAH', 'HOU'))
```

    ## # A tibble: 9,313 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      623            627        -4      933            932
    ##  4  2013     1     1      728            732        -4     1041           1038
    ##  5  2013     1     1      739            739         0     1104           1038
    ##  6  2013     1     1      908            908         0     1228           1219
    ##  7  2013     1     1     1028           1026         2     1350           1339
    ##  8  2013     1     1     1044           1045        -1     1352           1351
    ##  9  2013     1     1     1114            900       134     1447           1222
    ## 10  2013     1     1     1205           1200         5     1503           1505
    ## # … with 9,303 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Were operated by United (UA), American (AA), or Delta (DL)

``` r
filter(flights, carrier %in% c('UA', 'AA', 'DL'))
```

    ## # A tibble: 139,504 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      554            600        -6      812            837
    ##  5  2013     1     1      554            558        -4      740            728
    ##  6  2013     1     1      558            600        -2      753            745
    ##  7  2013     1     1      558            600        -2      924            917
    ##  8  2013     1     1      558            600        -2      923            937
    ##  9  2013     1     1      559            600        -1      941            910
    ## 10  2013     1     1      559            600        -1      854            902
    ## # … with 139,494 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Departed in summer (July, August, and September)

``` r
filter(flights, month %in% c(7, 8, 9))
```

    ## # A tibble: 86,326 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     7     1        1           2029       212      236           2359
    ##  2  2013     7     1        2           2359         3      344            344
    ##  3  2013     7     1       29           2245       104      151              1
    ##  4  2013     7     1       43           2130       193      322             14
    ##  5  2013     7     1       44           2150       174      300            100
    ##  6  2013     7     1       46           2051       235      304           2358
    ##  7  2013     7     1       48           2001       287      308           2305
    ##  8  2013     7     1       58           2155       183      335             43
    ##  9  2013     7     1      100           2146       194      327             30
    ## 10  2013     7     1      100           2245       135      337            135
    ## # … with 86,316 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Arrived more than two hours late, but (AND) didn’t leave late

``` r
filter(flights, arr_delay > 120 & dep_delay <= 0)
```

    ## # A tibble: 29 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1    27     1419           1420        -1     1754           1550
    ##  2  2013    10     7     1350           1350         0     1736           1526
    ##  3  2013    10     7     1357           1359        -2     1858           1654
    ##  4  2013    10    16      657            700        -3     1258           1056
    ##  5  2013    11     1      658            700        -2     1329           1015
    ##  6  2013     3    18     1844           1847        -3       39           2219
    ##  7  2013     4    17     1635           1640        -5     2049           1845
    ##  8  2013     4    18      558            600        -2     1149            850
    ##  9  2013     4    18      655            700        -5     1213            950
    ## 10  2013     5    22     1827           1830        -3     2217           2010
    ## # … with 19 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
    ## #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
    ## #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
filter(flights, arr_delay > 120, dep_delay <= 0)
```

    ## # A tibble: 29 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1    27     1419           1420        -1     1754           1550
    ##  2  2013    10     7     1350           1350         0     1736           1526
    ##  3  2013    10     7     1357           1359        -2     1858           1654
    ##  4  2013    10    16      657            700        -3     1258           1056
    ##  5  2013    11     1      658            700        -2     1329           1015
    ##  6  2013     3    18     1844           1847        -3       39           2219
    ##  7  2013     4    17     1635           1640        -5     2049           1845
    ##  8  2013     4    18      558            600        -2     1149            850
    ##  9  2013     4    18      655            700        -5     1213            950
    ## 10  2013     5    22     1827           1830        -3     2217           2010
    ## # … with 19 more rows, and 11 more variables: arr_delay <dbl>, carrier <chr>,
    ## #   flight <int>, tailnum <chr>, origin <chr>, dest <chr>, air_time <dbl>,
    ## #   distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Were delayed by at least an hour, but made up over 30 minutes in flight

``` r
filter(flights, dep_delay >= 60, dep_delay - arr_delay > 30)
```

    ## # A tibble: 1,844 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1     2205           1720       285       46           2040
    ##  2  2013     1     1     2326           2130       116      131             18
    ##  3  2013     1     3     1503           1221       162     1803           1555
    ##  4  2013     1     3     1839           1700        99     2056           1950
    ##  5  2013     1     3     1850           1745        65     2148           2120
    ##  6  2013     1     3     1941           1759       102     2246           2139
    ##  7  2013     1     3     1950           1845        65     2228           2227
    ##  8  2013     1     3     2015           1915        60     2135           2111
    ##  9  2013     1     3     2257           2000       177       45           2224
    ## 10  2013     1     4     1917           1700       137     2135           1950
    ## # … with 1,834 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Departed between midnight and 6am (inclusive)

``` r
filter(flights, between(dep_time, 00, 600))
```

    ## # A tibble: 9,344 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 9,334 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

> 2.  Another useful dplyr filtering helper is between(). What does it
>     do? Can you use it to simplify the code needed to answer the
>     previous challenges?

The expression between(x, left, right) is equivalent to x \>= left & x
\<= right.

Of the answers in the previous question, we could simplify the statement
of departed in summer (month \>= 7 & month \<= 9) using the between()
function.

``` r
filter(flights, between(dep_time, 00, 600))
```

    ## # A tibble: 9,344 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 9,334 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

> 3.  How many flights have a missing dep\_time? What other variables
>     are missing? What might these rows represent?

``` r
filter(flights, is.na(dep_time))
```

    ## # A tibble: 8,255 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1       NA           1630        NA       NA           1815
    ##  2  2013     1     1       NA           1935        NA       NA           2240
    ##  3  2013     1     1       NA           1500        NA       NA           1825
    ##  4  2013     1     1       NA            600        NA       NA            901
    ##  5  2013     1     2       NA           1540        NA       NA           1747
    ##  6  2013     1     2       NA           1620        NA       NA           1746
    ##  7  2013     1     2       NA           1355        NA       NA           1459
    ##  8  2013     1     2       NA           1420        NA       NA           1644
    ##  9  2013     1     2       NA           1321        NA       NA           1536
    ## 10  2013     1     2       NA           1545        NA       NA           1910
    ## # … with 8,245 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

### 5.3 Arrange rows with arrange()

arrange() works similarly to filter() except that instead of selecting
rows, it changes their order. It takes a data frame and a set of column
names (or more complicated expressions) to order by. If you provide more
than one column name, each additional column will be used to break ties
in the values of preceding columns:

``` r
arrange(flights, dep_delay)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    12     7     2040           2123       -43       40           2352
    ##  2  2013     2     3     2022           2055       -33     2240           2338
    ##  3  2013    11    10     1408           1440       -32     1549           1559
    ##  4  2013     1    11     1900           1930       -30     2233           2243
    ##  5  2013     1    29     1703           1730       -27     1947           1957
    ##  6  2013     8     9      729            755       -26     1002            955
    ##  7  2013    10    23     1907           1932       -25     2143           2143
    ##  8  2013     3    30     2030           2055       -25     2213           2250
    ##  9  2013     3     2     1431           1455       -24     1601           1631
    ## 10  2013     5     5      934            958       -24     1225           1309
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
arrange(flights, dep_delay, month)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013    12     7     2040           2123       -43       40           2352
    ##  2  2013     2     3     2022           2055       -33     2240           2338
    ##  3  2013    11    10     1408           1440       -32     1549           1559
    ##  4  2013     1    11     1900           1930       -30     2233           2243
    ##  5  2013     1    29     1703           1730       -27     1947           1957
    ##  6  2013     8     9      729            755       -26     1002            955
    ##  7  2013     3    30     2030           2055       -25     2213           2250
    ##  8  2013    10    23     1907           1932       -25     2143           2143
    ##  9  2013     3     2     1431           1455       -24     1601           1631
    ## 10  2013     5     5      934            958       -24     1225           1309
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Use desc() to re-order by a column in descending order:

``` r
arrange(flights, desc(dep_delay))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     9      641            900      1301     1242           1530
    ##  2  2013     6    15     1432           1935      1137     1607           2120
    ##  3  2013     1    10     1121           1635      1126     1239           1810
    ##  4  2013     9    20     1139           1845      1014     1457           2210
    ##  5  2013     7    22      845           1600      1005     1044           1815
    ##  6  2013     4    10     1100           1900       960     1342           2211
    ##  7  2013     3    17     2321            810       911      135           1020
    ##  8  2013     6    27      959           1900       899     1236           2226
    ##  9  2013     7    22     2257            759       898      121           1026
    ## 10  2013    12     5      756           1700       896     1058           2020
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

**Missing values are always sorted at the end**

##### 5.3.1 Exercises

> 3.  Sort flights to find the fastest (highest speed) flights.

``` r
arrange(flights, distance / air_time)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1    28     1917           1825        52     2118           1935
    ##  2  2013     6    29      755            800        -5     1035            909
    ##  3  2013     8    28      932            940        -8     1116           1051
    ##  4  2013     1    30     1037            955        42     1221           1100
    ##  5  2013    11    27      556            600        -4      727            658
    ##  6  2013     5    21      558            600        -2      721            657
    ##  7  2013    12     9     1540           1535         5     1720           1656
    ##  8  2013     6    10     1356           1300        56     1646           1414
    ##  9  2013     7    28     1322           1325        -3     1612           1432
    ## 10  2013     4    11     1349           1345         4     1542           1453
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

> 4.  Which flights travelled the farthest? Which travelled the
>     shortest?

``` r
arrange(flights, desc(distance))
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      857            900        -3     1516           1530
    ##  2  2013     1     2      909            900         9     1525           1530
    ##  3  2013     1     3      914            900        14     1504           1530
    ##  4  2013     1     4      900            900         0     1516           1530
    ##  5  2013     1     5      858            900        -2     1519           1530
    ##  6  2013     1     6     1019            900        79     1558           1530
    ##  7  2013     1     7     1042            900       102     1620           1530
    ##  8  2013     1     8      901            900         1     1504           1530
    ##  9  2013     1     9      641            900      1301     1242           1530
    ## 10  2013     1    10      859            900        -1     1449           1530
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
arrange(flights, distance)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     7    27       NA            106        NA       NA            245
    ##  2  2013     1     3     2127           2129        -2     2222           2224
    ##  3  2013     1     4     1240           1200        40     1333           1306
    ##  4  2013     1     4     1829           1615       134     1937           1721
    ##  5  2013     1     4     2128           2129        -1     2218           2224
    ##  6  2013     1     5     1155           1200        -5     1241           1306
    ##  7  2013     1     6     2125           2129        -4     2224           2224
    ##  8  2013     1     7     2124           2129        -5     2212           2224
    ##  9  2013     1     8     2127           2130        -3     2304           2225
    ## 10  2013     1     9     2126           2129        -3     2217           2224
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

### 3.4 Select columns with select()

It’s not uncommon to get datasets with hundreds or even thousands of
variables. In this case, the first challenge is often narrowing in on
the variables you’re actually interested in. select() allows you to
rapidly zoom in on a useful subset using operations based on the names
of the variables.

``` r
select(flights, year, month, day)
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # … with 336,766 more rows

``` r
select(flights, year:day) #same as above
```

    ## # A tibble: 336,776 x 3
    ##     year month   day
    ##    <int> <int> <int>
    ##  1  2013     1     1
    ##  2  2013     1     1
    ##  3  2013     1     1
    ##  4  2013     1     1
    ##  5  2013     1     1
    ##  6  2013     1     1
    ##  7  2013     1     1
    ##  8  2013     1     1
    ##  9  2013     1     1
    ## 10  2013     1     1
    ## # … with 336,766 more rows

``` r
select(flights, -(year:day)) #all except the ones above
```

    ## # A tibble: 336,776 x 16
    ##    dep_time sched_dep_time dep_delay arr_time sched_arr_time arr_delay carrier
    ##       <int>          <int>     <dbl>    <int>          <int>     <dbl> <chr>  
    ##  1      517            515         2      830            819        11 UA     
    ##  2      533            529         4      850            830        20 UA     
    ##  3      542            540         2      923            850        33 AA     
    ##  4      544            545        -1     1004           1022       -18 B6     
    ##  5      554            600        -6      812            837       -25 DL     
    ##  6      554            558        -4      740            728        12 UA     
    ##  7      555            600        -5      913            854        19 B6     
    ##  8      557            600        -3      709            723       -14 EV     
    ##  9      557            600        -3      838            846        -8 B6     
    ## 10      558            600        -2      753            745         8 AA     
    ## # … with 336,766 more rows, and 9 more variables: flight <int>, tailnum <chr>,
    ## #   origin <chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>,
    ## #   minute <dbl>, time_hour <dttm>

There are a number of helper functions you can use within select():

``` r
select(flights, starts_with('dep'))
```

    ## # A tibble: 336,776 x 2
    ##    dep_time dep_delay
    ##       <int>     <dbl>
    ##  1      517         2
    ##  2      533         4
    ##  3      542         2
    ##  4      544        -1
    ##  5      554        -6
    ##  6      554        -4
    ##  7      555        -5
    ##  8      557        -3
    ##  9      557        -3
    ## 10      558        -2
    ## # … with 336,766 more rows

``` r
select(flights, ends_with('delay'))
```

    ## # A tibble: 336,776 x 2
    ##    dep_delay arr_delay
    ##        <dbl>     <dbl>
    ##  1         2        11
    ##  2         4        20
    ##  3         2        33
    ##  4        -1       -18
    ##  5        -6       -25
    ##  6        -4        12
    ##  7        -5        19
    ##  8        -3       -14
    ##  9        -3        -8
    ## 10        -2         8
    ## # … with 336,766 more rows

``` r
select(flights, contains('_'))
```

    ## # A tibble: 336,776 x 8
    ##    dep_time sched_dep_time dep_delay arr_time sched_arr_time arr_delay air_time
    ##       <int>          <int>     <dbl>    <int>          <int>     <dbl>    <dbl>
    ##  1      517            515         2      830            819        11      227
    ##  2      533            529         4      850            830        20      227
    ##  3      542            540         2      923            850        33      160
    ##  4      544            545        -1     1004           1022       -18      183
    ##  5      554            600        -6      812            837       -25      116
    ##  6      554            558        -4      740            728        12      150
    ##  7      555            600        -5      913            854        19      158
    ##  8      557            600        -3      709            723       -14       53
    ##  9      557            600        -3      838            846        -8      140
    ## 10      558            600        -2      753            745         8      138
    ## # … with 336,766 more rows, and 1 more variable: time_hour <dttm>

select() can be used to rename variables, but it’s rarely useful because
it drops all of the variables not explicitly mentioned. Instead, use
rename(), which is a variant of select() that keeps all the variables
that aren’t explicitly mentioned:

``` r
#rename(dataset, new_name = old_name)
rename(flights, tail_num = tailnum)
```

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tail_num <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

Another option is to use select() in conjunction with the everything()
helper. This is useful if you have a handful of variables you’d like to
move to the start of the data frame.

``` r
select(flights, dep_delay, arr_delay, everything())
```

    ## # A tibble: 336,776 x 19
    ##    dep_delay arr_delay  year month   day dep_time sched_dep_time arr_time
    ##        <dbl>     <dbl> <int> <int> <int>    <int>          <int>    <int>
    ##  1         2        11  2013     1     1      517            515      830
    ##  2         4        20  2013     1     1      533            529      850
    ##  3         2        33  2013     1     1      542            540      923
    ##  4        -1       -18  2013     1     1      544            545     1004
    ##  5        -6       -25  2013     1     1      554            600      812
    ##  6        -4        12  2013     1     1      554            558      740
    ##  7        -5        19  2013     1     1      555            600      913
    ##  8        -3       -14  2013     1     1      557            600      709
    ##  9        -3        -8  2013     1     1      557            600      838
    ## 10        -2         8  2013     1     1      558            600      753
    ## # … with 336,766 more rows, and 11 more variables: sched_arr_time <int>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

### 5.5 Add new variables with mutate()

Besides selecting sets of existing columns, it’s often useful to add new
columns that are functions of existing columns. That’s the job of
mutate().

mutate() always adds new columns at the end of your dataset so we’ll
start by creating a narrower dataset so we can see the new variables.

Make a new dataset called “flights\_narrow” that includes only the
columns; year, month, day, dep\_delay, arr\_delay, distance, and
air\_time

``` r
flights_narrow <- select(flights, year:day, ends_with('delay'), distance, air_time)
```

Use the mutate() function to create two new columns; gain = dep\_delay -
arr\_delay, and speed = distance / air\_time \* 60

``` r
mutate(flights_narrow, gain = dep_delay - arr_delay, speed = distance / air_time * 60)
```

    ## # A tibble: 336,776 x 9
    ##     year month   day dep_delay arr_delay distance air_time  gain speed
    ##    <int> <int> <int>     <dbl>     <dbl>    <dbl>    <dbl> <dbl> <dbl>
    ##  1  2013     1     1         2        11     1400      227    -9  370.
    ##  2  2013     1     1         4        20     1416      227   -16  374.
    ##  3  2013     1     1         2        33     1089      160   -31  408.
    ##  4  2013     1     1        -1       -18     1576      183    17  517.
    ##  5  2013     1     1        -6       -25      762      116    19  394.
    ##  6  2013     1     1        -4        12      719      150   -16  288.
    ##  7  2013     1     1        -5        19     1065      158   -24  404.
    ##  8  2013     1     1        -3       -14      229       53    11  259.
    ##  9  2013     1     1        -3        -8      944      140     5  405.
    ## 10  2013     1     1        -2         8      733      138   -10  319.
    ## # … with 336,766 more rows

Note that you can refer to columns that you’ve just created:

``` r
mutate(
  flights_narrow, 
  gain = dep_delay - arr_delay, 
  hours = air_time / 60, 
  gain_per_hour = gain / hours
)
```

    ## # A tibble: 336,776 x 10
    ##     year month   day dep_delay arr_delay distance air_time  gain hours
    ##    <int> <int> <int>     <dbl>     <dbl>    <dbl>    <dbl> <dbl> <dbl>
    ##  1  2013     1     1         2        11     1400      227    -9 3.78 
    ##  2  2013     1     1         4        20     1416      227   -16 3.78 
    ##  3  2013     1     1         2        33     1089      160   -31 2.67 
    ##  4  2013     1     1        -1       -18     1576      183    17 3.05 
    ##  5  2013     1     1        -6       -25      762      116    19 1.93 
    ##  6  2013     1     1        -4        12      719      150   -16 2.5  
    ##  7  2013     1     1        -5        19     1065      158   -24 2.63 
    ##  8  2013     1     1        -3       -14      229       53    11 0.883
    ##  9  2013     1     1        -3        -8      944      140     5 2.33 
    ## 10  2013     1     1        -2         8      733      138   -10 2.3  
    ## # … with 336,766 more rows, and 1 more variable: gain_per_hour <dbl>

If you only want to keep the new variables, use transmute():

``` r
transmute(
  flights, 
  gain = dep_delay - arr_delay, 
  hours = air_time / 60, 
  gain_per_hour = gain / hours
)
```

    ## # A tibble: 336,776 x 3
    ##     gain hours gain_per_hour
    ##    <dbl> <dbl>         <dbl>
    ##  1    -9 3.78          -2.38
    ##  2   -16 3.78          -4.23
    ##  3   -31 2.67         -11.6 
    ##  4    17 3.05           5.57
    ##  5    19 1.93           9.83
    ##  6   -16 2.5           -6.4 
    ##  7   -24 2.63          -9.11
    ##  8    11 0.883         12.5 
    ##  9     5 2.33           2.14
    ## 10   -10 2.3           -4.35
    ## # … with 336,766 more rows

### 5.6 Grouped summaries with summarise()

The last key verb is summarize(). It collapses a data frame to a single
row:

``` r
summarize(
  flights, 
  delay = mean(dep_delay, na.rm = TRUE)
)
```

    ## # A tibble: 1 x 1
    ##   delay
    ##   <dbl>
    ## 1  12.6

summarise() is not terribly useful unless we pair it with group\_by().
This changes the unit of analysis from the complete dataset to
individual groups. Then, when you use the dplyr verbs on a grouped data
frame they’ll be automatically applied “by group”. For example, if we
applied exactly the same code to a data frame grouped by date, we get
the average delay per date:

``` r
by_day <- group_by(flights, year, month, day) #group by day

summarize(by_day, delay = mean(dep_delay, na.rm = TRUE)) #calculate average delay for each individual group
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day delay
    ##    <int> <int> <int> <dbl>
    ##  1  2013     1     1 11.5 
    ##  2  2013     1     2 13.9 
    ##  3  2013     1     3 11.0 
    ##  4  2013     1     4  8.95
    ##  5  2013     1     5  5.73
    ##  6  2013     1     6  7.15
    ##  7  2013     1     7  5.42
    ##  8  2013     1     8  2.55
    ##  9  2013     1     9  2.28
    ## 10  2013     1    10  2.84
    ## # … with 355 more rows

``` r
by_dest <- group_by(flights, dest) #group by destination

summarize(by_dest, delay = mean(dep_delay, na.rm = TRUE)) #calculate average delay for each individual group
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 105 x 2
    ##    dest  delay
    ##    <chr> <dbl>
    ##  1 ABQ   13.7 
    ##  2 ACK    6.46
    ##  3 ALB   23.6 
    ##  4 ANC   12.9 
    ##  5 ATL   12.5 
    ##  6 AUS   13.0 
    ##  7 AVL    8.19
    ##  8 BDL   17.7 
    ##  9 BGR   19.5 
    ## 10 BHM   29.7 
    ## # … with 95 more rows

Together group\_by() and summarise() provide one of the tools that
you’ll use most commonly when working with dplyr: grouped summaries.
But before we go any further with this, we need to introduce a powerful
new idea: the pipe.

##### 5.6.1 Combining multiple operations with the pipe

Imagine that we want to explore the relationship between the distance
and average delay for each location. Using what you know about dplyr,
you might write code like this.

Group flights by destination:

``` r
by_dest <- group_by(flights, dest)
```

Summarize the group, using average distance, average delay, and count.
Save this summary to a new data frame called “delays”:

``` r
(
delays <- summarize(by_dest, 
                    count = n(), 
                    dist = mean(distance, na.rm = TRUE), 
                    delay = mean(arr_delay, na.rm = TRUE)
                    )
)
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 105 x 4
    ##    dest  count  dist delay
    ##    <chr> <int> <dbl> <dbl>
    ##  1 ABQ     254 1826   4.38
    ##  2 ACK     265  199   4.85
    ##  3 ALB     439  143  14.4 
    ##  4 ANC       8 3370  -2.5 
    ##  5 ATL   17215  757. 11.3 
    ##  6 AUS    2439 1514.  6.02
    ##  7 AVL     275  584.  8.00
    ##  8 BDL     443  116   7.05
    ##  9 BGR     375  378   8.03
    ## 10 BHM     297  866. 16.9 
    ## # … with 95 more rows

Visualize your data: Make a plot of distance vs delay, with count mapped
to the size aesthetic. Improve if necessary

``` r
ggplot(data = delays) + 
  geom_point(mapping = aes(x = dist, y = delay, size = count))
```

    ## Warning: Removed 1 rows containing missing values (geom_point).

![](Data-Wrangling-_files/figure-gfm/step3-1.png)<!-- -->

Remove “noisy” points. Save to the “delays” data frame (over-write):

``` r
delays <- filter(delays, count > 20, dest != 'HNL')
```

Visualize data again:

``` r
ggplot(data = delays) +
  geom_point(mapping = aes(x = dist, y = delay, size = count))
```

![](Data-Wrangling-_files/figure-gfm/step%205-1.png)<!-- -->

Clean up your plot, and add trendline:

``` r
ggplot(data = delays, mapping = aes(x = dist, y = delay)) +
  geom_point(mapping = aes(size = count), alpha = 1/3) + 
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Wrangling-_files/figure-gfm/step%206-1.png)<!-- -->

``` r
delays <- flights %>% #delays gets flights, then
  group_by(dest) %>% #group by destination, then
  summarize( 
    count = n(),
    dist = mean(distance, na.rm = TRUE),
    delay = mean(arr_delay, na.rm = TRUE)
  ) %>% #summarize by count, distance and delay, then
  filter(count > 20, dest != 'HNL') #filter by...
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
ggplot(data = delays, mapping = aes(x = dist, y = delay)) + 
  geom_point(mapping = aes(size = count), alpha = 1/3) + 
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Wrangling-_files/figure-gfm/pipe-1.png)<!-- -->

##### 5.6.2 Missing values

You may have wondered about the na.rm argument we used above. What
happens if we don’t set it?

``` r
flights %>%
  group_by(year, month, day) %>%
  summarize(delay = mean(dep_delay))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day delay
    ##    <int> <int> <int> <dbl>
    ##  1  2013     1     1    NA
    ##  2  2013     1     2    NA
    ##  3  2013     1     3    NA
    ##  4  2013     1     4    NA
    ##  5  2013     1     5    NA
    ##  6  2013     1     6    NA
    ##  7  2013     1     7    NA
    ##  8  2013     1     8    NA
    ##  9  2013     1     9    NA
    ## 10  2013     1    10    NA
    ## # … with 355 more rows

We get a lot of missing values\! That’s because aggregation functions
obey the usual rule of missing values: if there’s any missing value in
the input, the output will be a missing value. Fortunately, all
aggregation functions have an na.rm argument which removes the missing
values prior to computation.

``` r
flights %>%
  group_by(year, month, day) %>%
  summarize(delay = mean(dep_delay, na.rm = TRUE))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day delay
    ##    <int> <int> <int> <dbl>
    ##  1  2013     1     1 11.5 
    ##  2  2013     1     2 13.9 
    ##  3  2013     1     3 11.0 
    ##  4  2013     1     4  8.95
    ##  5  2013     1     5  5.73
    ##  6  2013     1     6  7.15
    ##  7  2013     1     7  5.42
    ##  8  2013     1     8  2.55
    ##  9  2013     1     9  2.28
    ## 10  2013     1    10  2.84
    ## # … with 355 more rows

In this case, where missing values represent canceled flights, we could
also tackle the problem by first removing the canceled flights. We’ll
save this dataset so we can reuse it in the next few examples.

**What’s the difference between is.na and na.rm?**

is.na —– question (is it NA?) na.rm —– command (removes NA)

``` r
not_cancelled <- flights %>%
  filter(!is.na(dep_delay) & !is.na(arr_delay))
```

##### 5.6.3 Counts

Whenever you do any aggregation, it’s always a good idea to include
either a count (n()), or a count of non-missing values
(sum(\!is.na(x))). That way you can check that you’re not drawing
conclusions based on very small amounts of data. For example, let’s look
at the planes (identified by their tail number) that have the highest
average delays:

``` r
delays <- not_cancelled %>%
  group_by(tailnum) %>%
  summarize(delay = mean(arr_delay))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
delays
```

    ## # A tibble: 4,037 x 2
    ##    tailnum  delay
    ##    <chr>    <dbl>
    ##  1 D942DN  31.5  
    ##  2 N0EGMQ   9.98 
    ##  3 N10156  12.7  
    ##  4 N102UW   2.94 
    ##  5 N103US  -6.93 
    ##  6 N104UW   1.80 
    ##  7 N10575  20.7  
    ##  8 N105UW  -0.267
    ##  9 N107US  -5.73 
    ## 10 N108UW  -1.25 
    ## # … with 4,027 more rows

``` r
arrange(delays, desc(delay))
```

    ## # A tibble: 4,037 x 2
    ##    tailnum delay
    ##    <chr>   <dbl>
    ##  1 N844MH   320 
    ##  2 N911DA   294 
    ##  3 N922EV   276 
    ##  4 N587NW   264 
    ##  5 N851NW   219 
    ##  6 N928DN   201 
    ##  7 N7715E   188 
    ##  8 N654UA   185 
    ##  9 N665MQ   175.
    ## 10 N427SW   157 
    ## # … with 4,027 more rows

Wow, there are some planes that have an average delay of 5 hours (300
minutes)\!

The story is actually a little more nuanced. We can get more insight if
we draw a scatterplot of number of flights vs. average delay:

``` r
delays <- not_cancelled %>%
  group_by(tailnum) %>%
  summarize(
    delay = mean(arr_delay, na.rm = TRUE),
    count = n()
  )
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
arrange(delays, desc(delay))
```

    ## # A tibble: 4,037 x 3
    ##    tailnum delay count
    ##    <chr>   <dbl> <int>
    ##  1 N844MH   320      1
    ##  2 N911DA   294      1
    ##  3 N922EV   276      1
    ##  4 N587NW   264      1
    ##  5 N851NW   219      1
    ##  6 N928DN   201      1
    ##  7 N7715E   188      1
    ##  8 N654UA   185      1
    ##  9 N665MQ   175.     6
    ## 10 N427SW   157      1
    ## # … with 4,027 more rows

``` r
ggplot(data = delays, mapping = aes(x = count, y = delay)) + 
  geom_point(alpha = 1/3)
```

![](Data-Wrangling-_files/figure-gfm/example_29-1.png)<!-- -->

Not surprisingly, there is much greater variation in the average delay
when there are few flights. The shape of this plot is very
characteristic: **whenever you plot a mean (or other summary) vs. group
size, you’ll see that the variation decreases as the sample size
increases.**

When looking at this sort of plot, it’s often useful to filter out the
groups with the smallest numbers of observations, so you can see more of
the pattern and less of the extreme variation in the smallest groups.
This is what the following code does, as well as showing you a handy
pattern for integrating ggplot2 into dplyr flows. It’s a bit painful
that you have to switch from %\>% to +, but once you get the hang of it,
it’s quite convenient.

``` r
delays %>%
  filter(count > 25) %>%
  ggplot(mapping = aes(x = count, y = delay)) + 
    geom_point(alpha = 1/10)
```

![](Data-Wrangling-_files/figure-gfm/example_30-1.png)<!-- -->

There’s another common variation of this type of pattern. Let’s look at
how the average performance of batters in baseball is related to the
number of times they’re at bat. Here I use data from the Lahman package
to compute the batting average (number of hits / number of attempts) of
every major league baseball player.

``` r
Batting
```

    ##       playerID yearID stint teamID lgID   G  AB   R   H X2B X3B HR RBI  SB CS
    ## 1    abercda01   1871     1    TRO   NA   1   4   0   0   0   0  0   0   0  0
    ## 2     addybo01   1871     1    RC1   NA  25 118  30  32   6   0  0  13   8  1
    ## 3    allisar01   1871     1    CL1   NA  29 137  28  40   4   5  0  19   3  1
    ## 4    allisdo01   1871     1    WS3   NA  27 133  28  44  10   2  2  27   1  1
    ## 5    ansonca01   1871     1    RC1   NA  25 120  29  39  11   3  0  16   6  2
    ## 6    armstbo01   1871     1    FW1   NA  12  49   9  11   2   1  0   5   0  1
    ## 7    barkeal01   1871     1    RC1   NA   1   4   0   1   0   0  0   2   0  0
    ## 8    barnero01   1871     1    BS1   NA  31 157  66  63  10   9  0  34  11  6
    ## 9    barrebi01   1871     1    FW1   NA   1   5   1   1   1   0  0   1   0  0
    ## 10   barrofr01   1871     1    BS1   NA  18  86  13  13   2   1  0  11   1  0
    ## 11    bassjo01   1871     1    CL1   NA  22  89  18  27   1  10  3  18   0  1
    ## 12   battijo01   1871     1    CL1   NA   1   3   0   0   0   0  0   0   0  0
    ## 13   bealsto01   1871     1    WS3   NA  10  36   6   7   0   0  0   1   2  0
    ## 14   beaveed01   1871     1    TRO   NA   3  15   7   6   0   0  0   5   2  0
    ## 15   bechtge01   1871     1    PH1   NA  20  94  24  33   9   1  1  21   4  0
    ## 16   bellast01   1871     1    TRO   NA  29 128  26  32   3   3  0  23   4  4
    ## 17   berkena01   1871     1    PH1   NA   1   4   0   0   0   0  0   0   0  0
    ## 18   berryto01   1871     1    PH1   NA   1   4   0   1   0   0  0   0   0  0
    ## 19   berthha01   1871     1    WS3   NA  17  73  17  17   1   1  0   8   3  1
    ## 20   biermch01   1871     1    FW1   NA   1   2   0   0   0   0  0   0   0  0
    ## 21    birdge01   1871     1    RC1   NA  25 106  19  28   2   5  0  13   1  0
    ## 22   birdsda01   1871     1    BS1   NA  29 152  51  46   3   3  0  24   6  0
    ## 23   brainas01   1871     1    WS3   NA  30 134  24  30   4   0  0  21   4  0
    ## 24   brannmi01   1871     1    CH1   NA   3  14   2   1   0   0  0   0   0  0
    ## 25   burrohe01   1871     1    WS3   NA  12  63  11  15   2   3  1  14   0  0
    ## 26   careyto01   1871     1    FW1   NA  19  87  16  20   2   0  0  10   5  0
    ## 27   carleji01   1871     1    CL1   NA  29 127  31  32   8   1  0  18   2  1
    ## 28    conefr01   1871     1    BS1   NA  19  77  17  20   3   1  0  16  12  1
    ## 29   connone01   1871     1    TRO   NA   7  33   6   7   0   0  0   2   0  0
    ## 30   cravebi01   1871     1    TRO   NA  27 118  26  38   8   1  0  26   6  3
    ## 31   cuthbne01   1871     1    PH1   NA  28 150  47  37   7   5  3  30  16  2
    ## 32   deaneha01   1871     1    FW1   NA   6  22   3   4   0   1  0   2   0  0
    ## 33   donnepe01   1871     1    FW1   NA   9  34   7   7   1   1  0   3   0  0
    ## 34   duffyed01   1871     1    CH1   NA  26 121  30  28   5   0  0  15  11  4
    ## 35   eggleda01   1871     1    NY2   NA  33 147  37  47   7   3  0  18  14  3
    ## 36   ewellge01   1871     1    CL1   NA   1   3   0   0   0   0  0   0   0  0
    ## 37   fergubo01   1871     1    NY2   NA  33 158  30  38   6   1  0  25   4  4
    ## 38   fishech01   1871     1    RC1   NA  25 123  24  28   3   3  1  22   1  2
    ## 39   fislewe01   1871     1    PH1   NA  28 147  43  41   8   2  0  16   6  3
    ## 40   fleetfr01   1871     1    NY2   NA   1   6   1   2   0   0  0   1   0  0
    ## 41   flowedi01   1871     1    TRO   NA  21 105  39  33   5   4  0  18   8  2
    ## 42   flynncl01   1871     1    TRO   NA  29 142  43  48   6   1  0  27   3  3
    ## 43   foleyto01   1871     1    CH1   NA  18  84  18  22   3   1  0  13   1  4
    ## 44   foranji01   1871     1    FW1   NA  19  89  21  31   1   3  1  18   1  0
    ## 45   forceda01   1871     1    WS3   NA  32 162  45  45   9   4  0  29   8  0
    ## 46   fulmech01   1871     1    RC1   NA  16  63  11  17   1   3  0   3   0  0
    ## 47   glennjo01   1871     1    WS3   NA  26 120  25  37   3   2  0  21   1  1
    ## 48   goldswa01   1871     1    FW1   NA  19  88   8  18   1   0  0  12   0  0
    ## 49   gouldch01   1871     1    BS1   NA  31 151  38  43   9   2  2  32   6  2
    ## 50    hallge01   1871     1    WS3   NA  32 136  31  40   3   3  2  17   2  1
    ## 51   halliji01   1871     1    FW1   NA   5  25   7   5   0   0  0   2   1  1
    ## 52     hamra01   1871     1    RC1   NA  25 113  25  28   4   0  0  12   6  2
    ## 53   hastisc01   1871     1    RC1   NA  25 118  27  30   6   4  0  20  11  2
    ## 54   hatfijo01   1871     1    NY2   NA  33 168  41  43   3   2  0  22  10  3
    ## 55   heubege01   1871     1    PH1   NA  17  75  18  23   4   2  0  13   1  0
    ## 56   highadi01   1871     1    NY2   NA  21  94  21  34   3   1  0   9   3  2
    ## 57   hodesch01   1871     1    CH1   NA  28 130  32  36   4   1  2  25   3  0
    ## 58   jackssa01   1871     1    BS1   NA  16  76  17  17   5   3  0  11   0  1
    ## 59   johnsca01   1871     1    CL1   NA  16  67  10  15   1   0  0   7   1  0
    ## 60   kellybi01   1871     1    FW1   NA  18  67  16  15   1   1  0   7   0  0
    ## 61   kimbage01   1871     1    CL1   NA  29 131  18  25   1   0  0   9   5  1
    ## 62    kingma01   1871     1    CH1   NA  20 101  23  21   1   0  2  16   5  0
    ## 63    kingst01   1871     1    TRO   NA  29 144  45  57  10   6  0  34   3  3
    ## 64   kohlehe01   1871     1    FW1   NA   3  12   0   2   1   0  0   1   0  0
    ## 65   lennobi01   1871     1    FW1   NA  12  48   5  11   3   0  0   5   1  0
    ## 66   leonaan01   1871     1    WS3   NA  31 148  33  43   8   3  0  30  14  3
    ## 67    mackde01   1871     1    RC1   NA  25 122  34  30   7   1  0  17  12  0
    ## 68   malonfe01   1871     1    PH1   NA  27 134  33  46   7   1  1  33   9  3
    ## 69   mathebo01   1871     1    FW1   NA  19  89  15  24   3   1  0  10   2  1
    ## 70   mcatebu01   1871     1    CH1   NA  26 135  34  37   8   2  0  10   5  3
    ## 71   mcbridi01   1871     1    PH1   NA  25 132  36  31   3   0  0  17   4  0
    ## 72   mcderjo01   1871     1    FW1   NA   2   8   3   2   0   0  0   1   1  0
    ## 73   mcgeami01   1871     1    TRO   NA  29 148  42  39   4   0  0  12  20  4
    ## 74   mcmuljo01   1871     1    TRO   NA  29 136  38  38   0   5  0  32  11  1
    ## 75   mcveyca01   1871     1    BS1   NA  29 153  43  66   9   5  0  43   6  0
    ## 76   meyerle01   1871     1    PH1   NA  26 130  45  64   9   3  4  40   4  0
    ## 77   millsch01   1871     1    NY2   NA  32 146  27  36   4   3  0  22   2  0
    ## 78   millsev01   1871     1    WS3   NA  32 157  38  43   6   4  1  24   2  3
    ## 79   minched01   1871     1    FW1   NA   9  36   4   8   0   0  0   5   1  0
    ## 80   nortofr01   1871     1    WS3   NA   1   1   0   0   0   0  0   0   0  0
    ## 81   paborch01   1871     1    CL1   NA  29 142  24  42   2   4  0  18   1  0
    ## 82   patteda01   1871     1    NY2   NA  32 151  31  31   2   0  0  13   2  1
    ## 83   pearcdi01   1871     1    NY2   NA  33 163  31  44   5   0  0  20   0  0
    ## 84   phelpne01   1871     1    FW1   NA   1   3   0   0   0   0  0   0   0  0
    ## 85    pikeli01   1871     1    TRO   NA  28 130  43  49  10   7  4  39   3  2
    ## 86   pinkhed01   1871     1    CH1   NA  24  95  27  25   5   5  1  17   5  2
    ## 87   prattal01   1871     1    CL1   NA  29 130  31  34   6   8  0  20   1  0
    ## 88   prattto01   1871     1    PH1   NA   1   6   2   2   0   0  0   1   0  0
    ## 89   questjo01   1871     1    CL1   NA   3  13   1   3   1   0  0   2   0  0
    ## 90   quinnpa02   1871     1    FW1   NA   5  17   8   4   0   0  0   2   3  1
    ## 91   radcljo01   1871     1    PH1   NA  28 145  47  44   7   5  0  22   5  1
    ## 92   reachal01   1871     1    PH1   NA  26 133  43  47   7   6  0  34   2  0
    ## 93   sagerpo01   1871     1    RC1   NA   8  39   9  11   0   0  0   5   5  1
    ## 94   schafha01   1871     1    BS1   NA  31 149  38  42   7   5  0  28  13  4
    ## 95   selmafr01   1871     1    FW1   NA  14  65  14  15   3   0  1  10   1  0
    ## 96   senseco01   1871     1    PH1   NA  25 127  38  41   5   2  0  23   5  3
    ## 97   simmojo01   1871     1    CH1   NA  27 129  29  28   6   1  0  17   4  1
    ## 98   smithch01   1871     1    NY2   NA  14  72  15  19   2   1  0   5   6  0
    ## 99   spaldal01   1871     1    BS1   NA  31 144  43  39  10   1  1  31   2  0
    ## 100  startjo01   1871     1    NY2   NA  33 161  35  58   5   1  1  34   4  2
    ## 101  stearbi01   1871     1    WS3   NA   2   9   1   0   0   0  0   1   0  0
    ## 102  stirega01   1871     1    RC1   NA  25 110  23  30   4   6  2  24   3  0
    ## 103  suttoez01   1871     1    CL1   NA  29 128  35  45   3   7  3  23   3  1
    ## 104  sweasch01   1871     1    WS3   NA   5  19   5   4   1   0  0   4   0  0
    ## 105  treacfr01   1871     1    CH1   NA  25 124  39  42   7   5  4  33  13  5
    ## 106  waterfr01   1871     1    WS3   NA  32 158  46  50   7   4  0  17  11  3
    ## 107  whitede01   1871     1    CL1   NA  29 146  40  47   6   5  1  21   2  2
    ## 108  whiteel01   1871     1    CL1   NA  15  70  13  18   2   0  0   9   0  1
    ## 109  whitewa01   1871     1    WS3   NA   1   4   0   0   0   0  0   0   0  0
    ## 110  woltery01   1871     1    NY2   NA  32 138  33  51   6   9  0  44   1  0
    ## 111   woodji01   1871     1    CH1   NA  28 135  45  51  10   6  1  29  18  2
    ## 112  wrighge01   1871     1    BS1   NA  16  80  33  33   7   5  0  11   9  1
    ## 113  wrighha01   1871     1    BS1   NA  31 147  42  44   5   2  0  26   7  1
    ## 114   yorkto01   1871     1    TRO   NA  29 145  36  37   5   7  2  23   2  2
    ## 115  zettlge01   1871     1    CH1   NA  28 128  23  32   3   0  0  18   4  0
    ## 116  allenha01   1872     1    MID   NA  17  70   9  19   3   0  0  11   0  0
    ## 117  allisan01   1872     1    BR1   NA  22  92   9  15   2   0  0  10   0  0
    ## 118  allisar01   1872     1    CL1   NA  19  87  13  23   4   0  0   8   0  0
    ## 119  allisbi01   1872     1    BR1   NA   5  19   5   3   0   0  0   1   0  0
    ## 120  allisdo01   1872     1    TRO   NA  23 114  23  35   4   2  0  20   1  1
    ## 121  allisdo01   1872     2    BR1   NA  18  83  18  28   2   1  0   4   0  0
    ## 122  ansonca01   1872     1    PH1   NA  46 217  60  90  10   7  0  48   6  6
    ## 123  arnolbi01   1872     1    MID   NA   2   7   2   1   0   0  0   0   1  0
    ## 124  barloto01   1872     1    BR2   NA  37 171  34  54   1   0  0   8   7  5
    ## 125  barnero01   1872     1    BS1   NA  45 230  81  99  28   2  1  44  12  2
    ## 126    barre01   1872     1    BR2   NA   8  34   6   7   1   0  0   2   1  0
    ## 127  barrebi01   1872     1    WS3   NA   1   4   0   0   0   0  0   0   0  0
    ## 128   bassjo01   1872     1    BR2   NA   2   7   0   1   1   0  0   1   0  0
    ## 129  bealsto01   1872     1    WS3   NA   9  36   6  11   1   1  0   5   0  0
    ## 130  beaveed01   1872     1    BR2   NA  10  43   6   9   2   0  0   2   0  0
    ## 131  bechtge01   1872     1    NY2   NA  51 247  61  74  11   3  0  42   9  1
    ## 132  bellast01   1872     1    TRO   NA  23 115  22  30   4   0  0  17   1  0
    ## 133  bentlcy01   1872     1    MID   NA  23 114  23  25   3   4  1  11   1  2
    ## 134    besti01   1872     1    BR1   NA   4  14   0   4   0   0  0   0   0  0
    ## 135  bielaos01   1872     1    WS4   NA  10  46  13   8   0   0  0   3   0  0
    ## 136  birdsda01   1872     1    BS1   NA  16  76  11  16   3   0  0  15   0  2
    ## 137  boothed01   1872     1    MID   NA  24 116  25  37   5   2  0  15   0  2
    ## 138  boothed01   1872     2    BR2   NA  15  62  10  19   4   0  0   7   0  2
    ## 139   boydbi01   1872     1    NY2   NA  36 170  27  44   6   1  1  32   4  2
    ## 140  brainas01   1872     1    WS3   NA   9  43   8  16   3   0  0   6   0  0
    ## 141  brainas01   1872     2    MID   NA   6  25   2   5   0   0  0   1   0  0
    ## 142  brittji01   1872     1    BR2   NA  37 155  26  41   7   0  0  11   0  1
    ## 143  brownol01   1872     1    BR2   NA   4  15   0   2   0   0  0   0   0  0
    ## 144  burdoja01   1872     1    BR2   NA  37 174  27  47   3   0  0  14   0  1
    ## 145  burrohe01   1872     1    WS3   NA   2   7   1   1   0   0  0   0   0  0
    ## 146  buttefr01   1872     1    MID   NA  18  93  16  20   0   0  0   7   0  0
    ## 147  careyto01   1872     1    BL1   NA  42 196  42  57   7   0  2  27   4  1
    ## 148  carleji01   1872     1    CL1   NA   7  38   8  12   1   0  0   4   1  0
    ## 149  clappjo01   1872     1    MID   NA  19  97  30  27   7   1  1  16   2  1
    ## 150  clarede01   1872     1    BR2   NA   2   7   1   1   0   0  0   0   0  0
    ## 151  clintji01   1872     1    BR1   NA  25  98  11  24   4   1  0   6   0  1
    ## 152  coughde01   1872     1    WS4   NA   8  37   5  11   1   0  0   7   0  0
    ## 153  cravebi01   1872     1    BL1   NA  35 178  55  50   3   3  0  24   9  1
    ## 154  cummica01   1872     1    NY2   NA  55 249  37  52   9   3  0  26   0  1
    ## 155  cuthbne01   1872     1    PH1   NA  47 260  83  88  10   0  1  47  14  4
    ## 156  dehlmhe01   1872     1    BR2   NA  37 164  30  37   4   1  0  15   4  2
    ## 157  doschhe01   1872     1    BR2   NA   6  24   4   9   0   0  0   5   0  1
    ## 158  doylejo01   1872     1    WS4   NA   9  41   6  11   1   0  0   9   0  0
    ## 159  eggleda01   1872     1    NY2   NA  56 290  94  97  20   0  0  19  18  6
    ## 160  fergubo01   1872     1    BR2   NA  37 164  33  46   3   0  0  19   4  2
    ## 161  fieldge01   1872     1    MID   NA  18  86  17  19   3   1  0  14   0  0
    ## 162  fishech01   1872     1    BL1   NA  46 225  39  52  10   3  1  36   1  1
    ## 163  fislewe01   1872     1    PH1   NA  47 244  49  85  13   3  0  48   3  0
    ## 164  fleetfr01   1872     1    BR1   NA  13  53   9  12   1   0  0   6   1  0
    ## 165  fletcge01   1872     1    BR1   NA   2   8   1   2   0   0  0   1   0  0
    ## 166  flowedi01   1872     1    PH1   NA   3  15   1   4   0   0  0   4   0  0
    ## 167  flynncl01   1872     1    WS3   NA   9  40   4   9   1   0  0   2   0  0
    ## 168  forceda01   1872     1    TRO   NA  25 130  40  53  11   0  0  19   2  2
    ## 169  forceda01   1872     2    BL1   NA  19  95  29  41   2   2  0  14   5  0
    ## 170  fulmech01   1872     1    NY2   NA  36 165  29  50   1   1  1  15   1  1
    ## 171  galvijo01   1872     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 172  gedneco01   1872     1    TRO   NA   9  47  14  20   3   0  3  18   1  0
    ## 173  gedneco01   1872     2    BR1   NA  18  71   5  13   1   0  0   6   2  2
    ## 174  glennjo01   1872     1    WS3   NA   9  39   6   6   0   0  0   3   0  1
    ## 175  glennjo01   1872     2    WS4   NA   1   4   0   2   0   0  0   0   0  0
    ## 176  goldswa01   1872     1    WS3   NA   9  41   4  10   2   0  0   5   0  0
    ## 177  gouldch01   1872     1    BS1   NA  45 212  40  54   9   8  0  32   0  0
    ## 178   hallge01   1872     1    BL1   NA  53 250  69  84  17   6  1  37   8  1
    ## 179   hallji01   1872     1    BR2   NA  13  57   9  18   0   1  0   6   0  0
    ## 180  hastisc01   1872     1    CL1   NA  22 115  34  45   4   0  0  16   5  1
    ## 181  hastisc01   1872     2    BL1   NA  13  62  16  19   3   1  0   4   0  1
    ## 182  hatfijo01   1872     1    NY2   NA  56 288  76  93  15   2  1  47  12  5
    ## 183  heubege01   1872     1    WS3   NA   5  23   2   3   0   0  0   1   0  0
    ## 184  hicksna01   1872     1    NY2   NA  56 267  54  82  12   2  0  32   3  0
    ## 185    higby01   1872     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 186  highadi01   1872     1    BL1   NA  50 245  72  84  10   1  2  37   4  5
    ## 187  hinespa01   1872     1    WS4   NA  11  49   9  11   1   0  0   5   0  0
    ## 188  hodesch01   1872     1    TRO   NA  13  62  17  15   3   0  0  10   0  0
    ## 189  holdsji01   1872     1    CL1   NA  22 110  19  33   5   0  0  11   3  2
    ## 190  holdsji01   1872     2    BR1   NA   3  11   1   3   1   0  0   0   0  0
    ## 191  holliho01   1872     1    WS4   NA   9  44  12  14   1   1  0   6   0  0
    ## 192   huntdi01   1872     1    BR1   NA  11  46  10  15   1   1  0   4   0  1
    ## 193  hurledi01   1872     1    WS3   NA   2   7   0   0   0   0  0   0   0  0
    ## 194  jackssa01   1872     1    BR2   NA   4  12   0   2   0   0  0   0   0  0
    ## 195  jewetna01   1872     1    BR1   NA   2   8   1   1   0   0  0   0   0  0
    ## 196    kavan01   1872     1    BR1   NA   5  23   3   6   1   0  0   4   0  0
    ## 197  kennejo01   1872     1    BR2   NA   5  19   0   0   0   0  0   1   0  0
    ## 198   kingma01   1872     1    TRO   NA   3  11   0   0   0   0  0   1   0  0
    ## 199   kingst01   1872     1    TRO   NA  25 128  33  39   8   0  0  20   1  1
    ## 200  lennobi01   1872     1    WS4   NA  11  54  11  11   1   0  0   6   0  0
    ## 201  leonaan01   1872     1    BS1   NA  46 241  57  84   7   1  2  42   8  5
    ## 202    leutz01   1872     1    BR1   NA   4  12   2   1   0   0  0   0   0  0
    ## 203   lowech01   1872     1    BR2   NA   7  31   2   5   0   0  0   3   0  0
    ## 204   mackde01   1872     1    PH1   NA  47 205  68  59   9   1  0  34   9  5
    ## 205  malonfe01   1872     1    PH1   NA  41 213  46  60   5   3  0  39   3  0
    ## 206  malonma01   1872     1    BR1   NA   5  16   2   6   0   0  0   3   0  1
    ## 207  martial01   1872     1    BR1   NA   4  18   2   5   0   0  0   1   0  0
    ## 208  martiph01   1872     1    TRO   NA  25 119  27  36   2   1  0  14   0  0
    ## 209  martiph01   1872     2    BR1   NA  18  78  13  15   1   1  0   9   3  2
    ## 210  mathebo01   1872     1    BL1   NA  50 222  36  50   2   0  0  22   3  1
    ## 211  mcatebu01   1872     1    TRO   NA  25 126  30  28   3   1  0  15   0  2
    ## 212  mcbridi01   1872     1    PH1   NA  47 258  57  74   6   1  0  37   2  1
    ## 213  mccarfr01   1872     1    MID   NA  19  82  19  25   5   0  0  12   0  0
    ## 214  mcderjo01   1872     1    BR1   NA   7  32   3   9   3   0  0   3   0  0
    ## 215  mcdonja01   1872     1    BR2   NA   4  14   2   2   0   0  0   0   0  0
    ## 216  mcdonja01   1872     2    BR1   NA   1   4   0   0   0   0  0   0   0  0
    ## 217  mcdonja01   1872     3    BR2   NA  11  48   7  14   3   1  0   4   0  0
    ## 218  mcgeami01   1872     1    PH1   NA  47 225  68  81   9   2  0  35  13  8
    ## 219  mcmuljo01   1872     1    NY2   NA  54 236  47  60   6   1  0  24   8  2
    ## 220  mcveyca01   1872     1    BS1   NA  46 237  56  76  10   2  0  41   6  1
    ## 221  meyerle01   1872     1    PH1   NA  27 146  31  48  10   5  1  31   0  0
    ## 222  millejo01   1872     1    WS4   NA   1   4   0   1   0   0  0   0   0  0
    ## 223  millsch01   1872     1    NY2   NA   6  31   6   4   0   0  0   2   0  0
    ## 224  millsev01   1872     1    BL1   NA  55 266  55  79  14   2  0  34   0  2
    ## 225  minched01   1872     1    WS4   NA  11  53   5   5   0   0  0   4   0  0
    ## 226    mulle01   1872     1    CL1   NA   1   4   1   0   0   0  0   0   0  0
    ## 227  murnati01   1872     1    MID   NA  23 114  28  41   1   1  0  16   1  2
    ## 228  nelsoca01   1872     1    TRO   NA   4  20   2   7   0   0  0   4   0  0
    ## 229  nelsoca01   1872     2    BR1   NA  18  76  12  19   5   1  0   9   1  0
    ## 230    orour01   1872     1    BR1   NA   1   4   0   0   0   0  0   0   0  0
    ## 231  orourji01   1872     1    MID   NA  23  99  25  27   5   0  0  16   1  0
    ## 232  paborch01   1872     1    CL1   NA  21  92  12  19   0   0  0   7   0  0
    ## 233  patteda01   1872     1    BR1   NA  12  47   6  10   1   0  0   3   0  3
    ## 234  pearcdi01   1872     1    NY2   NA  44 206  32  39   2   1  1  22   1  1
    ## 235   pikeli01   1872     1    BL1   NA  56 285  68  85  15   5  7  60  10  1
    ## 236  prattal01   1872     1    CL1   NA  16  65  10  18   0   1  0  12   0  0
    ## 237  radcljo01   1872     1    BL1   NA  56 297  70  86  13   4  1  44   3  3
    ## 238  reachal01   1872     1    PH1   NA  24 118  21  23   0   0  0  10   1  1
    ## 239  reachbo01   1872     1    WS3   NA   2   8   1   2   0   0  0   0   0  0
    ## 240  remseja01   1872     1    BR2   NA  37 165  25  39   3   5  1  14   1  2
    ## 241  robinva01   1872     1    WS3   NA   7  30   6   6   0   0  0   4   0  0
    ## 242  rogerfr01   1872     1    BS1   NA  45 204  39  56   7   1  1  28   2  0
    ## 243  schafha01   1872     1    BS1   NA  48 226  51  65  10   4  1  35   3  0
    ## 244  selmafr01   1872     1    WS3   NA   9  42   3  10   2   0  0   1   0  2
    ## 245  senseco01   1872     1    PH1   NA   1   5   2   2   0   0  0   1   0  1
    ## 246  simmojo01   1872     1    CL1   NA  18  90  11  23   5   1  0   9   1  0
    ## 247  snydeji01   1872     1    BR1   NA  25 103  16  30   2   3  0  11   0  2
    ## 248  snydejo01   1872     1    BR1   NA   9  37   4   6   2   0  0   1   0  0
    ## 249  spaldal01   1872     1    BS1   NA  48 237  60  84  12   5  0  47   3  0
    ## 250    spenc01   1872     1    WS4   NA   1   4   1   0   0   0  0   0   0  0
    ## 251  startjo01   1872     1    NY2   NA  54 277  60  75   5   0  0  48   3  3
    ## 252  stearbi01   1872     1    WS4   NA  11  45   8  11   1   0  0   4   0  0
    ## 253  studlse01   1872     1    WS4   NA   5  21   3   2   0   0  0   2   0  0
    ## 254  suttoez01   1872     1    CL1   NA  22 107  30  30   6   1  0  10   1  0
    ## 255  swandma01   1872     1    BR1   NA  14  52   8  12   1   0  0   4   0  1
    ## 256  sweasch01   1872     1    CL1   NA  12  57   8  16   0   0  0   6   1  0
    ## 257  thakeal01   1872     1    BR2   NA  18  78  14  23   2   2  0  15   2  0
    ## 258  tippeji01   1872     1    MID   NA  24 110  24  29   4   0  0  18   0  0
    ## 259  treacfr01   1872     1    PH1   NA  47 236  53  65   7   3  2  31   7  5
    ## 260  waterfr01   1872     1    WS3   NA   9  45  13  17   1   2  0   6   0  0
    ## 261  whitede01   1872     1    CL1   NA  22 109  21  37   2   2  0  22   0  0
    ## 262  whitewa01   1872     1    WS4   NA  10  45   7  12   0   0  0   4   0  0
    ## 263  woltery01   1872     1    CL1   NA  16  69   7  16   1   0  0  11   0  0
    ## 264   woodji01   1872     1    TRO   NA  25 113  40  38  11   4  2  26   0  0
    ## 265   woodji01   1872     2    BR1   NA   7  31  10   6   1   1  0   0   1  0
    ## 266  worthhe01   1872     1    BR2   NA   1   5   1   1   1   0  0   1   0  0
    ## 267  wrighge01   1872     1    BS1   NA  48 255  87  86  16   6  2  35  14  4
    ## 268  wrighha01   1872     1    BS1   NA  48 208  39  53   5   1  0  24   0  0
    ## 269  yeatmbi01   1872     1    WS4   NA   1   4   0   0   0   0  0   0   0  0
    ## 270   yorkto01   1872     1    BL1   NA  51 250  66  66  10   4  0  40   6  1
    ## 271  zettlge01   1872     1    TRO   NA  25 114  25  29   9   0  0  21   0  1
    ## 272  zettlge01   1872     2    BR1   NA   9  34   1   3   0   0  0   1   0  0
    ## 273   addybo01   1873     1    PH2   NA  10  51  12  16   1   0  0  10   1  1
    ## 274   addybo01   1873     2    BS1   NA  31 152  37  54   6   3  1  32   6  5
    ## 275  allisar01   1873     1    ELI   NA  23 100  12  32   2   0  0  11   0  0
    ## 276  allisdo01   1873     1    ELI   NA  19  80  11  24   6   0  0   8   0  0
    ## 277  allisdo01   1873     2    NY2   NA  11  48   6  10   0   0  0   3   0  0
    ## 278  ansonca01   1873     1    PH1   NA  52 254  53 101   9   2  0  36   1  2
    ## 279  atkined01   1873     1    WS5   NA   2   8   2   0   0   0  0   0   0  0
    ## 280  austihe01   1873     1    ELI   NA  23 101  10  25   3   3  0  11   1  1
    ## 281  barloto01   1873     1    BR2   NA  55 269  48  74   0   2  1  12   3  4
    ## 282  barnero01   1873     1    BS1   NA  60 320 125 138  31  11  2  60  43  6
    ## 283  barrebi01   1873     1    BL1   NA   1   4   0   1   0   0  0   0   0  1
    ## 284  battijo01   1873     1    PH1   NA   1   5   4   3   0   0  0   2   0  0
    ## 285  bealsto01   1873     1    WS5   NA  37 169  35  46   9   5  0  22   3  0
    ## 286  bechtge01   1873     1    PH2   NA  53 258  53  63  12   1  1  39   2  1
    ## 287  bellast01   1873     1    NY2   NA   8  32   4   7   2   0  0   3   0  0
    ## 288  bielaos01   1873     1    WS5   NA  38 173  35  49   3   2  0  20   1  3
    ## 289  birdsda01   1873     1    BS1   NA   3  11   4   1   0   0  0   0   1  0
    ## 290  boothed01   1873     1    ELI   NA  18  74  11  21   5   2  0   6   0  0
    ## 291  boothed01   1873     2    BR2   NA  16  70   8  14   3   1  0   7   0  1
    ## 292   boydbi01   1873     1    BR2   NA  48 228  31  63   5   4  1  30   1  1
    ## 293  brainas01   1873     1    BL1   NA  16  69  18  18   1   0  0   9   0  0
    ## 294  brittji01   1873     1    BR2   NA  54 240  29  47   3   0  0  13   1  1
    ## 295  burdoja01   1873     1    BR2   NA  55 245  56  62   7   1  2  36   3  2
    ## 296  campbhu01   1873     1    ELI   NA  20  86   9  13   0   1  0   7   1  1
    ## 297  campbmi02   1873     1    ELI   NA  21  84   9  12   2   0  0   2   1  0
    ## 298  careyto01   1873     1    BL1   NA  56 291  76  98  18   3  1  55   2  3
    ## 299  clappjo01   1873     1    PH1   NA  45 204  36  62  10   2  1  27   4  5
    ## 300  clintji01   1873     1    ELI   NA   9  39   5   9   2   0  0   4   0  0
    ## 301  cranefr01   1873     1    ELI   NA   1   4   0   1   0   0  0   1   0  0
    ## 302  cravebi01   1873     1    BL1   NA  41 197  45  57   9   3  0  26   5  4
    ## 303  cummica01   1873     1    BL1   NA  42 192  30  48   5   0  0  36   1  0
    ## 304  cuthbne01   1873     1    PH2   NA  51 279  78  77   5   3  2  34  14  2
    ## 305  dehlmhe01   1873     1    BR2   NA  54 219  50  52   5   1  0  18   5  0
    ## 306  devliji01   1873     1    PH2   NA  23  99  18  24   4   4  0  10   0  0
    ## 307  donnejo01   1873     1    WS5   NA  30 137  15  35   2   0  0  19   0  0
    ## 308  doschhe01   1873     1    BR2   NA   1   6   1   1   0   0  0   1   0  0
    ## 309  eggleda01   1873     1    NY2   NA  53 266  82  90  13   4  0  35   3  2
    ## 310    eland01   1873     1    BL4   NA   1   3   0   0   0   0  0   0   0  0
    ## 311  farrojo01   1873     1    ELI   NA  12  48   2   8   1   0  0   3   0  0
    ## 312  fergubo01   1873     1    BR2   NA  51 228  36  59   3   5  0  25   1  2
    ## 313  fishech01   1873     1    PH1   NA  51 253  50  66   4   3  1  37   2  2
    ## 314  fislewe01   1873     1    PH1   NA  44 218  44  75  11   4  1  41   3  1
    ## 315  fleetfr01   1873     1    ELI   NA  22  89  11  23   3   0  0  10   0  2
    ## 316  forceda01   1873     1    BL1   NA  49 233  77  85  10   1  0  30   1  0
    ## 317  frencbi01   1873     1    BL4   NA   5  18   3   4   0   0  0   1   0  0
    ## 318  fulmech01   1873     1    PH2   NA  49 236  42  66  11   3  1  38   3  1
    ## 319  gedneco01   1873     1    NY2   NA  53 225  41  60   5   5  1  24   1  0
    ## 320  gerhajo01   1873     1    WS5   NA  13  57   6  12   3   0  0   9   0  1
    ## 321  glennjo01   1873     1    WS5   NA  39 186  39  49   9   2  1  22   3  1
    ## 322  goldswa01   1873     1    BL4   NA   1   4   0   0   0   0  0   0   0  0
    ## 323  greasjo01   1873     1    WS5   NA   7  27   4   4   0   0  0   1   1  0
    ## 324   hallge01   1873     1    BL1   NA  35 168  44  58   6   4  0  31   0  0
    ## 325  hastisc01   1873     1    BL1   NA  30 145  41  41   4   0  0  15   4  2
    ## 326  hatfijo01   1873     1    NY2   NA  52 255  54  78   5   6  2  46   2  0
    ## 327  hicksna01   1873     1    NY2   NA  28 120  12  29   1   2  1  14   2  1
    ## 328  highadi01   1873     1    NY2   NA  49 244  57  77   5   4  0  34   2  2
    ## 329  hinespa01   1873     1    WS5   NA  39 181  33  60   6   3  1  29   0  1
    ## 330  holdsji01   1873     1    NY2   NA  53 232  46  75   4   8  0  28   1  0
    ## 331  holliho01   1873     1    WS5   NA  30 136  25  35   2   2  0  22   0  0
    ## 332  hoopemi01   1873     1    BL4   NA   3  14   3   3   1   0  0   2   0  0
    ## 333  johnsto01   1873     1    BL4   NA   1   4   0   0   0   0  0   0   0  0
    ## 334    jones01   1873     1    BL4   NA   1   4   0   3   0   0  0   1   0  0
    ## 335  kernajo01   1873     1    BL4   NA   2   8   1   3   0   0  0   1   0  0
    ## 336  kesslhe01   1873     1    BR2   NA   1   5   0   1   0   0  0   1   0  0
    ## 337  kohlehe01   1873     1    BL4   NA   6  25   2   3   0   0  0   1   0  0
    ## 338  laughbe01   1873     1    ELI   NA  12  51   3  12   0   0  0   5   0  0
    ## 339  lennobi01   1873     1    BL4   NA   5  19   2   4   0   0  0   2   0  0
    ## 340  leonaan01   1873     1    BS1   NA  58 300  81  96  13   6  0  60  27  9
    ## 341  lovetle01   1873     1    ELI   NA   1   5   1   2   0   0  0   1   0  0
    ## 342   mackde01   1873     1    PH2   NA  48 205  55  60   5   0  0  19   6  2
    ## 343  malonfe01   1873     1    PH2   NA  53 259  59  75  11   2  0  41   6  1
    ## 344  mannija01   1873     1    BS1   NA  31 154  28  41   4   1  0  21   5  2
    ## 345  martiph01   1873     1    NY2   NA  31 140  12  31   1   0  0  14   1  1
    ## 346  mathebo01   1873     1    NY2   NA  52 223  40  43   3   3  0  14   1  1
    ## 347  mcbridi01   1873     1    PH1   NA  49 253  41  71   7   0  0  40   1  0
    ## 348    mcdoo01   1873     1    BL4   NA   1   4   1   0   0   0  0   0   0  0
    ## 349  mcgeami01   1873     1    PH1   NA  52 275  63  83   8   1  0  31   4  6
    ## 350  mcmuljo01   1873     1    PH1   NA  52 227  54  62   7   1  0  28   9  1
    ## 351  mcveyca01   1873     1    BL1   NA  38 192  49  73   5   5  2  35   2  1
    ## 352  meyerle01   1873     1    PH2   NA  48 238  53  83  14   4  3  59   5  0
    ## 353  millsev01   1873     1    BL1   NA  54 262  64  87  20   9  0  56   1  0
    ## 354  murnati01   1873     1    PH1   NA  41 176  53  39   2   1  1  10   8  2
    ## 355  nelsoca01   1873     1    NY2   NA  36 168  28  55   4   1  0  22   2  0
    ## 356  nevinal01   1873     1    ELI   NA  13  55   7  11   1   2  0   1   0  0
    ## 357  orourji01   1873     1    BS1   NA  57 280  79  98  21   2  1  49   9  5
    ## 358  paborch01   1873     1    BR2   NA  55 228  36  82   9   3  0  41   2  0
    ## 359  pearcdi01   1873     1    BR2   NA  55 262  42  72   6   0  1  23   3  0
    ## 360  phelpne01   1873     1    NY2   NA   1   6   0   0   0   0  0   0   0  0
    ## 361   pikeli01   1873     1    BL1   NA  56 285  71  90  15   8  4  51   8  1
    ## 362  popplge01   1873     1    BL4   NA   1   4   0   0   0   0  0   0   0  0
    ## 363  radcljo01   1873     1    BL1   NA  45 244  59  70   5   0  0  33   0  0
    ## 364  reachal01   1873     1    PH1   NA  16  73  13  16   5   1  0   9   2  0
    ## 365  reachbo01   1873     1    WS5   NA   1   5   1   1   0   0  0   0   0  0
    ## 366  remseja01   1873     1    BR2   NA  50 207  29  61   5   6  1  29   1  2
    ## 367  rogerfr01   1873     1    BS1   NA   2  11   2   4   1   0  0   3   0  0
    ## 368   ryanjo01   1873     1    PH2   NA   2   8   1   2   0   0  0   1   0  0
    ## 369    saylo01   1873     1    BL4   NA   3  12   1   2   0   0  0   2   0  0
    ## 370  schafha01   1873     1    BS1   NA  60 296  65  79  12   2  2  42  14  7
    ## 371  selmafr01   1873     1    BL4   NA   1   3   1   1   0   0  0   0   0  0
    ## 372  senseco01   1873     1    PH1   NA  20  86  12  24   1   0  0   8   0  2
    ## 373  sheppjo01   1873     1    BL4   NA   3  11   1   0   0   0  0   0   0  0
    ## 374  simpsma01   1873     1    BL4   NA   4  15   4   2   0   0  0   2   0  0
    ## 375  smithbi01   1873     1    BL4   NA   6  23   2   4   0   0  0   1   0  0
    ## 376  smithjo01   1873     1    BL4   NA   5  19   2   2   0   0  0   1   0  0
    ## 377  snydepo01   1873     1    WS5   NA  28 107  16  21   2   0  0   3   0  1
    ## 378  spaldal01   1873     1    BS1   NA  60 323  83 106  15   1  1  71   9  0
    ## 379  startjo01   1873     1    NY2   NA  53 252  42  67   8   3  1  29   1  0
    ## 380  stearbi01   1873     1    WS5   NA  32 133  22  24   0   0  0   8   1  0
    ## 381  strated01   1873     1    BL4   NA   4  16   2   2   0   0  0   0   0  0
    ## 382  suttoez01   1873     1    PH1   NA  51 243  51  81   7   6  0  34   2  3
    ## 383  swandma01   1873     1    ELI   NA   2   9   1   1   0   0  0   1   0  0
    ## 384  sweasch01   1873     1    BS1   NA   1   4   0   1   0   0  0   0   0  0
    ## 385  treacfr01   1873     1    PH2   NA  51 243  49  62   7   2  1  31   4  3
    ## 386   wallho01   1873     1    WS5   NA   1   3   1   1   0   0  0   0   0  0
    ## 387  waterfr01   1873     1    WS5   NA  15  80  20  28   1   1  0  12   0  0
    ## 388  whitede01   1873     1    BS1   NA  60 311  79 122  17   8  1  77  19  3
    ## 389  whitewa01   1873     1    WS5   NA  39 158  29  43   3   4  0  20   2  1
    ## 390  woltery01   1873     1    ELI   NA   1   4   1   0   0   0  0   0   0  0
    ## 391  woodhre01   1873     1    BL4   NA   1   5   1   0   0   0  0   0   0  0
    ## 392   woodji01   1873     1    PH2   NA  42 209  67  67  11   1  0  27   9  3
    ## 393  wordsfa01   1873     1    ELI   NA  12  40   5  10   0   0  0   3   1  0
    ## 394  wrighge01   1873     1    BS1   NA  59 323  99 125  17   7  3  43   9  9
    ## 395  wrighha01   1873     1    BS1   NA  58 263  57  68   7   3  2  36   3  2
    ## 396   yorkto01   1873     1    BL1   NA  57 278  70  84  11   7  2  50   4  1
    ## 397  zettlge01   1873     1    PH2   NA  51 241  39  50   2   0  0  21   4  0
    ## 398   addybo01   1874     1    HR1   NA  50 213  25  51   9   2  0  22   4  2
    ## 399  allisdo01   1874     1    NY2   NA  65 318  68  90   7   5  0  28   1  0
    ## 400  ansonca01   1874     1    PH1   NA  55 260  51  87   8   3  0  37   6  0
    ## 401  barloto01   1874     1    HR1   NA  32 155  37  46   5   1  0  12  17  4
    ## 402  barnero01   1874     1    BS1   NA  51 259  72  88  12   4  0  39   8  7
    ## 403  barnibi01   1874     1    HR1   NA  45 190  21  35   4   2  0  20   2  2
    ## 404  battijo01   1874     1    PH1   NA  51 226  40  52  11   1  0  27   3  2
    ## 405  bealsto01   1874     1    BS1   NA  19  97  20  19   3   4  0  17   0  1
    ## 406  bechtge01   1874     1    PH2   NA  32 151  29  42   4   5  1  34   0  0
    ## 407  bielaos01   1874     1    BL1   NA  43 187  24  45   0   0  0   8   3  1
    ## 408  boardfr01   1874     1    BL1   NA   1   4   0   1   0   0  0   0   0  0
    ## 409   bondto01   1874     1    BR2   NA  55 245  25  54  10   1  0  20   0  0
    ## 410  boothed01   1874     1    BR2   NA  44 185  24  47   4   3  1  16   0  0
    ## 411   boydbi01   1874     1    HR1   NA  26 117  22  41   8   4  0  19   1  0
    ## 412  bradyst01   1874     1    HR1   NA  27 118  19  37   5   1  0  14   1  2
    ## 413  brainas01   1874     1    BL1   NA  47 196  19  47   3   0  0   8   0  3
    ## 414    brown01   1874     1    BL1   NA   2   9   0   0   0   0  0   0   0  0
    ## 415  burdoja01   1874     1    NY2   NA  61 273  45  75  11   4  1  26   4  1
    ## 416  careyto01   1874     1    NY2   NA  64 287  56  82  10   3  1  38   3  0
    ## 417   carlle01   1874     1    BL1   NA   1   3   0   0   0   0  0   0   0  0
    ## 418  chapmja01   1874     1    BR2   NA  53 242  32  64  10   2  0  24   2  1
    ## 419  clackbo01   1874     1    BR2   NA  33 135  22  23   1   0  0  13   0  0
    ## 420  clappjo01   1874     1    PH1   NA  39 165  46  48   7   4  3  19   2  0
    ## 421  clintji01   1874     1    BR2   NA   2  11   3   2   1   0  0   2   0  0
    ## 422  collida01   1874     1    CH2   NA   3  12   1   1   1   0  0   0   1  0
    ## 423  connete01   1874     1    CH2   NA   1   4   0   0   0   0  0   0   0  0
    ## 424  cravebi01   1874     1    PH2   NA  55 265  68  91  19  11  0  56  11  3
    ## 425  cummica01   1874     1    PH2   NA  54 231  32  52   4   2  0  19   1  1
    ## 426  cuthbne01   1874     1    CH2   NA  58 295  65  79   6   1  2  24   8  0
    ## 427  deaneha01   1874     1    BL1   NA  47 203  29  50   8   1  0  13   2  1
    ## 428  dehlmhe01   1874     1    BR2   NA  53 218  40  49   3   1  0  18   2  0
    ## 429  devliji01   1874     1    CH2   NA  45 203  26  58   5   0  0  26   2  1
    ## 430  donnejo01   1874     1    PH2   NA   6  22   2   5   0   0  0   2   0  0
    ## 431  eggleda01   1874     1    PH2   NA  58 299  70  95  13   8  0  31   5  6
    ## 432  farreja01   1874     1    HR1   NA   3  13   3   5   0   0  0   0   0  0
    ## 433  farrojo01   1874     1    BR2   NA  27 122  16  26   3   0  0  10   0  0
    ## 434  fergubo01   1874     1    BR2   NA  56 245  34  64   4   0  0  19   5  3
    ## 435  fishech01   1874     1    HR1   NA  52 241  28  54   7   0  0  31   2  3
    ## 436  fislewe01   1874     1    PH1   NA  37 180  26  59  12   1  0  22   2  0
    ## 437  fleetfr01   1874     1    BR2   NA  22  97  18  22   0   0  0  10   1  0
    ## 438  forceda01   1874     1    CH2   NA  59 294  61  92   9   0  0  26   4  0
    ## 439  fulmech01   1874     1    PH2   NA  57 258  49  72   3   2  0  37   0  2
    ## 440    gaver01   1874     1    BR2   NA   1   4   1   0   0   0  0   0   0  0
    ## 441  gedneco01   1874     1    PH1   NA  54 222  49  61   4   1  1  34   2  2
    ## 442   geerbi01   1874     1    NY2   NA   2   8   0   2   0   0  0   1   0  0
    ## 443  gerhajo01   1874     1    BL1   NA  14  61  10  19   0   1  0   6   0  0
    ## 444    gilro01   1874     1    CH2   NA   8  38   4   8   1   0  0   7   0  0
    ## 445  glennjo01   1874     1    CH2   NA  55 237  33  67   9   0  0  32   2  2
    ## 446  gouldch01   1874     1    BL1   NA  33 143  19  32   6   0  0  14   1  0
    ## 447   hallge01   1874     1    BS1   NA  47 222  58  64  10   8  1  34   2  0
    ## 448   hallji01   1874     1    BR2   NA   2   9   0   1   0   0  0   0   0  0
    ## 449  hastisc01   1874     1    HR1   NA  52 247  60  80  11   2  0  30  10  5
    ## 450  hatfijo01   1874     1    NY2   NA  63 292  47  66  12   1  0  29   4  0
    ## 451  hicksna01   1874     1    PH2   NA  58 266  51  73   8   1  0  30   3  2
    ## 452  highadi01   1874     1    NY2   NA  65 333  58  87  14   3  1  38   5  3
    ## 453  hinespa01   1874     1    CH2   NA  59 271  47  80  10   2  0  34   4  1
    ## 454  hodesch01   1874     1    BR2   NA  21  81   8  12   3   0  0   7   0  0
    ## 455  holdsji01   1874     1    PH2   NA  57 285  60  97   8   9  0  37   1  2
    ## 456    jones01   1874     1    BL1   NA   2   7   0   1   0   0  0   1   0  0
    ## 457  kesslhe01   1874     1    BR2   NA  14  56   8  17   1   0  0   4   0  0
    ## 458  knowdja01   1874     1    BR2   NA  24  86   8  12   1   1  0   3   1  0
    ## 459  kohlehe01   1874     1    BL1   NA   2   4   0   0   0   0  0   0   0  0
    ## 460  ledwimi01   1874     1    BR2   NA   1   4   1   1   0   0  0   1   0  0
    ## 461  leonaan01   1874     1    BS1   NA  71 339  68 106  18   4  0  50  11  3
    ## 462   mackde01   1874     1    PH2   NA  56 246  48  51   8   4  0  22   4  0
    ## 463  malonfe01   1874     1    CH2   NA  47 223  33  56   5   0  0  28   2  1
    ## 464  mannija01   1874     1    BL1   NA  42 174  32  61   8   2  0  18   0  0
    ## 465  mannija01   1874     2    HR1   NA   1   5   1   1   0   0  0   0   0  0
    ## 466  martial01   1874     1    BR2   NA   7  29   1   4   0   0  0   1   0  0
    ## 467  mathebo01   1874     1    NY2   NA  65 298  46  72   6   1  0  30   2  0
    ## 468  mcbridi01   1874     1    PH1   NA  55 263  30  57   7   1  0  34   1  0
    ## 469  mcgeami01   1874     1    PH1   NA  54 271  61  87  10   2  0  22  10  2
    ## 470  mcgeepa01   1874     1    BR2   NA  16  65   4  11   1   0  0   6   0  0
    ## 471  mckenfr01   1874     1    PH2   NA   1   4   0   0   0   0  0   0   0  0
    ## 472  mcmuljo01   1874     1    PH1   NA  55 260  61  90  10   2  2  32   4  3
    ## 473  mcveyca01   1874     1    BS1   NA  70 343  91 123  21   6  3  71   5  0
    ## 474  meyerle01   1874     1    CH2   NA  53 254  65 100  19   1  1  45   3  1
    ## 475  milleto01   1874     1    PH1   NA   4  16   1   8   0   0  0   5   0  0
    ## 476  millsev01   1874     1    HR1   NA  53 244  39  69   6   1  0  19   1  1
    ## 477  murnati01   1874     1    PH1   NA  21  82  11  17   2   0  0  11   0  1
    ## 478  nelsoca01   1874     1    NY2   NA  65 297  55  73   7   5  0  31   6  0
    ## 479    oneal01   1874     1    HR1   NA   1   3   0   0   0   0  0   0   0  0
    ## 480  orourji01   1874     1    BS1   NA  70 331  82 104  15   8  5  61  11  2
    ## 481  paborch01   1874     1    PH2   NA  17  77  11  17   0   1  0   1   0  1
    ## 482  patteda01   1874     1    NY2   NA   1   5   1   2   0   0  0   2   0  0
    ## 483  pearcdi01   1874     1    BR2   NA  56 255  48  75   1   0  0  26   1  0
    ## 484  peterjo01   1874     1    CH2   NA  55 239  39  69  10   0  1  25   2  2
    ## 485  phelpne01   1874     1    NY2   NA   6  24   5   3   0   0  0   2   0  0
    ## 486   pikeli01   1874     1    HR1   NA  52 234  58  83  22   5  1  50   4  1
    ## 487    quinl01   1874     1    PH2   NA   1   4   0   1   0   0  0   1   0  0
    ## 488  radcljo01   1874     1    PH2   NA  23 103  20  25   7   0  1  14   1  1
    ## 489  reachal01   1874     1    PH1   NA  14  55   8   7   2   0  0   2   0  0
    ## 490   reedhu01   1874     1    BL1   NA   1   4   0   0   0   0  0   0   0  0
    ## 491  remseja01   1874     1    NY2   NA  64 284  52  65   9   3  2  38   6  0
    ## 492  revilhe01   1874     1    BL1   NA   1   4   0   0   0   0  0   0   0  0
    ## 493   ryanjo01   1874     1    BL1   NA  47 181  29  35   8   1  0  19   3  0
    ## 494    saylo01   1874     1    BL1   NA  18  66   4  14   3   0  0   5   0  0
    ## 495  schafha01   1874     1    BS1   NA  71 327  69  87  10   2  1  45   2  4
    ## 496  selmafr01   1874     1    BL1   NA  12  54   9  16   3   2  0   7   2  0
    ## 497  senseco01   1874     1    PH1   NA   5  16   3   3   0   0  0   2   0  0
    ## 498  shaffor01   1874     1    HR1   NA   9  35   6   8   0   0  1   3   0  0
    ## 499  shaffor01   1874     2    NY2   NA   1   5   1   1   0   0  0   0   0  0
    ## 500  smilebi01   1874     1    BL1   NA   2   7   0   0   0   0  0   0   0  0
    ## 501  smithjo01   1874     1    BL1   NA   6  21   2   4   1   0  0   1   0  0
    ## 502   snowch01   1874     1    BR2   NA   1   1   0   1   0   0  0   0   0  0
    ## 503  snydepo01   1874     1    BL1   NA  39 151  24  33   4   0  1  17   0  0
    ## 504  spaldal01   1874     1    BS1   NA  71 362  80 119  13   1  0  54   2  1
    ## 505  startjo01   1874     1    NY2   NA  63 306  67  96  13   3  2  46   5  0
    ## 506  stearbi01   1874     1    HR1   NA  33 132  16  21   1   0  0  11   0  0
    ## 507  suttoez01   1874     1    PH1   NA  55 243  54  71  10   3  0  28   6  4
    ## 508  sweasch01   1874     1    BL1   NA   8  33   2   8   0   0  0   4   0  0
    ## 509  sweasch01   1874     2    BR2   NA  10  44   4   5   1   0  0   3   0  0
    ## 510  tayloza01   1874     1    BL1   NA  13  48   3  12   0   0  0   3   0  0
    ## 511  tippeji01   1874     1    HR1   NA  45 197  36  60   8   0  0  19   0  1
    ## 512  treacfr01   1874     1    CH2   NA  35 148  18  28   5   0  0  12   4  4
    ## 513   westbi01   1874     1    BR2   NA   9  35   4   8   1   0  0   2   0  0
    ## 514  whitede01   1874     1    BS1   NA  70 352  75 106   5   7  3  52   1  1
    ## 515  whitewa01   1874     1    BL1   NA  45 211  21  57   1   0  0  17   1  0
    ## 516     wood01   1874     1    BL1   NA   1   5   0   0   0   0  0   0   0  0
    ## 517  wrighge01   1874     1    BS1   NA  60 313  76 103  10  15  2  44   2  0
    ## 518  wrighha01   1874     1    BS1   NA  40 184  44  58   4   2  2  27   1  0
    ## 519   yorkto01   1874     1    PH2   NA  50 224  36  56   4   7  0  37   1  0
    ## 520  zettlge01   1874     1    CH2   NA  57 244  26  47   7   0  0  18   0  0
    ## 521  abadijo01   1875     1    PH3   NA  11  45   3  10   0   0  0   4   1  0
    ## 522  abadijo01   1875     2    BR2   NA   1   4   1   1   0   0  0   1   0  0
    ## 523   addybo01   1875     1    PH2   NA  69 310  60  80   8   4  0  43  16  8
    ## 524  allisar01   1875     1    WS6   NA  26 112  18  24   3   1  0   3   6  0
    ## 525  allisar01   1875     2    HR1   NA  40 175  26  42   4   1  1  19   1  2
    ## 526  allisdo01   1875     1    HR1   NA  61 269  38  67   7   0  0  21   2  0
    ## 527  ansonca01   1875     1    PH1   NA  69 326  84 106  15   3  0  58  11  6
    ## 528  arundha01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 529  banckst01   1875     1    NH1   NA  19  72   3  11   0   0  0   2   1  0
    ## 530  barloto01   1875     1    NH1   NA   1   5   1   1   0   0  0   0   0  0
    ## 531  barloto01   1875     2    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 532  barnero01   1875     1    BS1   NA  78 393 115 143  20   4  1  58  29  6
    ## 533  barnibi01   1875     1    KEO   NA  10  36   3   4   1   0  0   2   0  0
    ## 534  barnibi01   1875     2    NY2   NA   9  34   1   5   0   0  0   1   0  0
    ## 535  battijo01   1875     1    SL2   NA  67 284  31  71   6   3  0  33  15  3
    ## 536  bealsto01   1875     1    BS1   NA  35 155  38  41   2   6  0  16   1  0
    ## 537  bechtge01   1875     1    PH3   NA  14  61  12  17   5   0  0   7   0  0
    ## 538  bechtge01   1875     2    PH1   NA  35 164  33  46   6   2  0  20   2  0
    ## 539  bielaos01   1875     1    CH2   NA  51 201  21  48   1   0  0  11   5  5
    ## 540  blongjo01   1875     1    SL1   NA  16  68   3  10   2   0  0   5   1  0
    ## 541    bolan01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 542   bondto01   1875     1    HR1   NA  72 289  32  77  11   3  0  33   5  1
    ## 543    booth01   1875     1    NH1   NA   1   2   0   0   0   0  0   0   0  0
    ## 544  boothed01   1875     1    NY2   NA  68 281  33  56   3   4  0  18   4  3
    ## 545  bordejo01   1875     1    PH2   NA   7  28   3   3   0   0  0   1   0  0
    ## 546   boydbi01   1875     1    BR2   NA  36 151  14  44  11   0  1  10   0  0
    ## 547  bradlge01   1875     1    SL2   NA  60 254  28  62   7   3  0  24   3  3
    ## 548    brady01   1875     1    CH2   NA   1   4   1   1   0   1  0   0   0  0
    ## 549  bradyst01   1875     1    WS6   NA  21  91   7  13   0   0  0   3   5  0
    ## 550  bradyst01   1875     2    HR1   NA   1   4   0   0   0   0  0   0   0  0
    ## 551  brannmi01   1875     1    CH2   NA   2   9   2   1   0   0  0   0   2  0
    ## 552  brownol01   1875     1    BR2   NA   3  10   0   0   0   0  0   0   0  0
    ## 553  burdoja01   1875     1    HR1   NA  74 350  72 103  12   5  0  35  20 11
    ## 554  bushodo01   1875     1    BR2   NA   1   5   0   3   0   1  0   0   0  0
    ## 555  carbijo01   1875     1    KEO   NA  10  36   0   3   0   0  0   2   0  0
    ## 556  careyto01   1875     1    HR1   NA  86 382  63 101   6   2  0  38  13  3
    ## 557  cassijo01   1875     1    BR2   NA  41 166  14  29   3   2  1   6   0  0
    ## 558  cassijo01   1875     2    NH1   NA   6  22   3   3   1   0  0   1   0  1
    ## 559  chapmja01   1875     1    SL2   NA  43 195  28  44   5   3  0  30   4  1
    ## 560  clackbo01   1875     1    BR2   NA  17  59   1   6   0   0  0   1   0  0
    ## 561  clappjo01   1875     1    PH1   NA  60 292  65  77   8   7  0  39   9  5
    ## 562  clintji01   1875     1    BR2   NA  22  81   3  10   0   0  0   0   0  0
    ## 563   coonwi01   1875     1    PH1   NA   4  12   1   2   0   0  0   1   1  0
    ## 564  cranefr01   1875     1    BR2   NA  21  81   7  17   1   0  0   4   0  0
    ## 565  cravebi01   1875     1    PH3   NA  14  65   8  18   4   2  0   5   1  0
    ## 566  cravebi01   1875     2    PH1   NA  54 260  71  83  11  11  2  40   8  4
    ## 567  croftar01   1875     1    SL1   NA  19  75   5  15   3   0  0   2   5  1
    ## 568  crowlbi01   1875     1    PH2   NA   9  37   4   3   0   0  0   3   0  0
    ## 569  cummica01   1875     1    HR1   NA  53 221  30  44   7   2  0  15   1  0
    ## 570  cuthbne01   1875     1    SL2   NA  68 319  68  78   9   2  0  17  18  1
    ## 571  dailejo01   1875     1    WS6   NA  27 110  16  20   5   4  0  13   3  2
    ## 572  dailejo01   1875     2    BR2   NA   2   8   3   1   0   0  0   0   0  0
    ## 573  dehlmhe01   1875     1    SL2   NA  67 254  42  57  12   2  0  14  23  9
    ## 574  devliji01   1875     1    CH2   NA  69 318  60  92  17   6  0  40   6  1
    ## 575  dillojo01   1875     1    SL1   NA   1   1   0   0   0   0  0   0   0  0
    ## 576  dillopa01   1875     1    SL1   NA   3  13   1   3   1   0  0   1   0  0
    ## 577   dolele01   1875     1    NH1   NA   1   4   1   2   0   0  0   0   0  0
    ## 578  doschhe01   1875     1    WS6   NA  22  81   5  15   4   0  0   5   1  0
    ## 579    edwar01   1875     1    BR2   NA   1   5   1   1   0   0  0   0   0  0
    ## 580  eggleda01   1875     1    PH1   NA  66 295  66  89  13   7  0  33   6  5
    ## 581  ellicjo01   1875     1    SL1   NA   7  27   1   6   1   0  0   1   1  0
    ## 582    evans01   1875     1    NH1   NA   1   4   1   2   0   0  0   1   0  0
    ## 583  fergubo01   1875     1    HR1   NA  85 366  65  88  10   4  0  43   2  1
    ## 584  fieldsa01   1875     1    PH3   NA   3  11   2   1   0   0  0   0   0  0
    ## 585  fieldsa01   1875     2    WS6   NA   5  16   0   5   0   0  0   1   1  0
    ## 586  fishech01   1875     1    PH2   NA  41 177  26  41   3   1  0  11   4  3
    ## 587  fislewe01   1875     1    PH1   NA  58 268  54  74  13   3  0  31   1  4
    ## 588  fleetfr01   1875     1    SL2   NA   4  16   1   1   0   0  0   1   0  0
    ## 589  fleetfr01   1875     2    BR2   NA  26 111  13  25   2   0  0   9   0  0
    ## 590  flintsi01   1875     1    SL1   NA  17  61   4   5   0   0  0   1   2  0
    ## 591  foleywi01   1875     1    CH2   NA   3  12   0   3   1   0  0   1   0  0
    ## 592  forceda01   1875     1    PH1   NA  77 386  78 120  22   5  0  49   6  3
    ## 593  fulmech01   1875     1    PH2   NA  69 295  50  65   6   1  0  24  10  4
    ## 594  fulmewa01   1875     1    BR2   NA   1   4   1   2   0   0  0   1   0  0
    ## 595  galvipu01   1875     1    SL2   NA  13  46   8   6   2   1  0   2   3  0
    ## 596  gedneco01   1875     1    NY2   NA  68 267  30  55  12   2  0  17   2  3
    ## 597   geerbi01   1875     1    NH1   NA  37 164  20  40   4   1  0   9   2  2
    ## 598  gerhajo01   1875     1    NY2   NA  58 252  29  54   7   3  0  20   0  5
    ## 599  gilgahu01   1875     1    BR2   NA   2   8   2   2   0   0  0   0   0  0
    ## 600  gilmoji01   1875     1    WS6   NA   3  12   2   3   0   0  0   0   0  0
    ## 601    gilro01   1875     1    PH1   NA   2   6   0   1   0   0  0   0   0  0
    ## 602  glennjo01   1875     1    CH2   NA  69 308  46  75   8   0  0  27  10  2
    ## 603  goldemi01   1875     1    KEO   NA  13  46   6   6   0   0  0   1   0  0
    ## 604  goldemi01   1875     2    CH2   NA  39 155  16  40   3   0  0  14   3  2
    ## 605  goldsfr01   1875     1    NH1   NA   1   4   0   2   0   0  0   1   0  0
    ## 606  goldswa01   1875     1    KEO   NA  13  51   3   6   0   0  0   1   0  0
    ## 607  gouldch01   1875     1    NH1   NA  27 109   9  29   4   1  0   8   0  1
    ## 608  haguebi01   1875     1    SL2   NA  62 260  24  57   2   0  0  22   3  4
    ## 609   hallge01   1875     1    PH1   NA  77 358  71 107  10  12  4  62   8  5
    ## 610  halliji01   1875     1    KEO   NA  13  51  12  14   2   1  0   3   2  2
    ## 611  halliji01   1875     2    NY2   NA  44 203  29  58   6   3  3  21   2  2
    ## 612   hallji01   1875     1    KEO   NA   1   3   0   1   0   1  0   1   0  0
    ## 613  harbibi01   1875     1    HR1   NA  53 208  32  50   3   3  0  26   2  4
    ## 614  harriri01   1875     1    NH1   NA   1   4   0   2   1   0  0   1   0  1
    ## 615  hastisc01   1875     1    CH2   NA  65 287  43  73   9   0  0  30  13 11
    ## 616  hatfijo01   1875     1    NY2   NA   1   4   1   2   1   0  0   1   0  0
    ## 617  hautzch01   1875     1    SL1   NA  19  83   5  25   3   0  0   4   5  1
    ## 618  heifefr01   1875     1    BS1   NA  11  50  11  14   0   3  0   5   0  0
    ## 619    helli01   1875     1    BR2   NA   1   4   0   1   0   0  0   0   0  0
    ## 620  hicksna01   1875     1    NY2   NA  62 269  32  67  10   0  0  22   1  0
    ## 621  highadi01   1875     1    CH2   NA  42 208  44  49   5   3  0  12   6  2
    ## 622  highadi01   1875     2    NY2   NA  15  64  12  25   5   0  0  10   0  0
    ## 623  hinespa01   1875     1    CH2   NA  68 308  45 101  14   4  0  36   6  9
    ## 624  holdsji01   1875     1    NY2   NA  71 324  45  92  12   1  0  23   3  3
    ## 625  holliho01   1875     1    WS6   NA  19  81   8  20   1   1  0   5   2  1
    ## 626  jonesch01   1875     1    KEO   NA  12  47   4  13   2   4  0  10   1  1
    ## 627  jonesch01   1875     2    HR1   NA   1   4   1   0   0   0  0   0   0  0
    ## 628  keenaji01   1875     1    NH1   NA   5  13   1   1   0   0  0   0   0  0
    ## 629  keerlge01   1875     1    CH2   NA   6  23   2   3   0   0  0   3   0  0
    ## 630  kesslhe01   1875     1    BR2   NA  25 105  17  26   2   0  0   7   0  2
    ## 631  knighge01   1875     1    NH1   NA   1   4   0   0   0   0  0   0   0  0
    ## 632  knighlo01   1875     1    PH1   NA  13  47   5   6   2   0  0   2   2  0
    ## 633  knowdja01   1875     1    BR2   NA  43 163  17  32   2   0  0   9   0  1
    ## 634  lathaju01   1875     1    BS1   NA  16  78  23  21   4   0  0  13   0  0
    ## 635  lathaju01   1875     2    NH1   NA  20  76   6  15   1   0  0   5   6  0
    ## 636  leonaan01   1875     1    BS1   NA  80 396  87 127  14   6  1  74  14  8
    ## 637  lovetle01   1875     1    PH3   NA   6  21   2   5   1   0  0   2   0  0
    ## 638  lowryjo01   1875     1    WS6   NA   6  22   2   3   0   0  0   0   0  1
    ## 639   luffhe01   1875     1    NH1   NA  38 166  15  45  10   3  2  18   3  3
    ## 640  malonfe01   1875     1    PH2   NA  29 123  15  28   2   1  0  10   1  0
    ## 641  mannija01   1875     1    BS1   NA  77 348  71  94  11   3  1  46   5  5
    ## 642  martial01   1875     1    BR2   NA   6  26   1   3   0   0  0   1   0  0
    ## 643  masonch01   1875     1    PH3   NA  12  47   5  11   0   0  0   3   0  0
    ## 644  masonch01   1875     2    WS6   NA   8  33   2   3   0   0  0   1   0  0
    ## 645  mathebo01   1875     1    NY2   NA  70 264  23  48   6   2  0  15   1  2
    ## 646  mcbridi01   1875     1    PH1   NA  60 270  42  73   9   0  0  45   2  1
    ## 647  mcclobi01   1875     1    WS6   NA  11  40   1   7   0   0  0   4   0  1
    ## 648  mcgeami01   1875     1    PH2   NA  68 310  71  90   6   2  0  37  19  4
    ## 649  mcgeepa01   1875     1    NY2   NA  25  95   4  17   2   0  0   9   0  0
    ## 650  mcgeepa01   1875     2    BR2   NA  18  65   3  10   3   1  0   5   0  0
    ## 651  mcginti01   1875     1    PH3   NA  13  52   5  12   0   1  0   5   0  0
    ## 652  mcginti01   1875     2    NH1   NA  32 131  13  36   3   1  0  10   1  1
    ## 653  mckeljo01   1875     1    NH1   NA  43 188  26  43   3   1  0  10   3  1
    ## 654  mcmuljo01   1875     1    PH2   NA  54 222  33  57   9   4  2  19   6 10
    ## 655  mcsortr01   1875     1    SL1   NA  15  52   4  11   0   0  0   2   3  0
    ## 656  mcveyca01   1875     1    BS1   NA  82 389  89 138  36   9  3  87   7  0
    ## 657  metcaal01   1875     1    NY2   NA   8  32   2   7   0   0  0   1   2  0
    ## 658  meyerle01   1875     1    PH2   NA  68 301  55  95  14   8  1  54   7  2
    ## 659  millejo01   1875     1    KEO   NA  13  50   4   6   1   0  0   0   0  0
    ## 660  millejo01   1875     2    CH2   NA  15  54   1   8   0   0  0   1   0  0
    ## 661  milleto01   1875     1    SL2   NA  56 214  18  35   2   0  0  12   2  0
    ## 662  millsev01   1875     1    HR1   NA  80 342  59  89   8   4  1  48   6  4
    ## 663  mooremo01   1875     1    BR2   NA  21  86   5  19   4   0  0   5   0  1
    ## 664  morgapi01   1875     1    SL1   NA  19  69  11  18   4   0  0   1   2  1
    ## 665   munnho01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 666  murnati01   1875     1    PH2   NA  69 313  71  85   5   0  1  30  30  9
    ## 667  nelsoca01   1875     1    NY2   NA  70 276  28  55   7   1  0  23   4  2
    ## 668  nichoal01   1875     1    BR2   NA  32 131   4  20   2   0  0   9   0  0
    ## 669  nichotr01   1875     1    NH1   NA  34 119  12  23   0   2  0   5   5  0
    ## 670   oneilj01   1875     1    BR2   NA   7  26   3   2   0   0  0   1   0  1
    ## 671   oranto01   1875     1    SL1   NA  19  81   7  15   3   1  0  10   3  2
    ## 672  orourji01   1875     1    BS1   NA  75 358  97 106  13   7  6  72  17  5
    ## 673  paborch01   1875     1    BR2   NA  42 153  14  36   2   2  0  11   0  0
    ## 674  paborch01   1875     2    NH1   NA   6  23   4   8   0   2  0   2   0  0
    ## 675  parksbi01   1875     1    WS6   NA  27 111  13  20   0   0  0   6   1  1
    ## 676  parksbi01   1875     2    PH2   NA   2   6   0   1   0   0  0   0   0  0
    ## 677  patteda01   1875     1    BR2   NA  12  45   4   9   0   0  0   4   1  0
    ## 678  pearcdi01   1875     1    SL2   NA  70 311  51  77   6   3  0  29   8  3
    ## 679  peterjo01   1875     1    CH2   NA  69 297  40  85  16   2  0  34  12  6
    ## 680  phelpne01   1875     1    NY2   NA   2   6   1   2   1   0  0   0   0  0
    ## 681   pikeli01   1875     1    SL2   NA  70 312  61 108  22  12  0  44  25 10
    ## 682  quinnpa01   1875     1    BR2   NA   2   8   2   1   0   0  0   0   0  0
    ## 683  quinnpa02   1875     1    KEO   NA  11  43   4  14   1   0  0   5   0  1
    ## 684  quinnpa02   1875     2    HR1   NA   5  13   1   3   0   0  0   1   0  1
    ## 685  quinnpa02   1875     3    CH2   NA  17  61  12  14   0   0  0   1   1  1
    ## 686  radcljo01   1875     1    PH3   NA   5  23   2   4   0   0  0   0   0  0
    ## 687  reachal01   1875     1    PH1   NA   3  14   4   4   1   0  0   1   2  1
    ## 688  redmobi01   1875     1    SL1   NA  19  82  12  16   2   0  0   1   3  0
    ## 689  remseja01   1875     1    HR1   NA  86 358  70  96  10   4  0  34   6  3
    ## 690  resslla01   1875     1    WS6   NA  27 108  17  21   1   0  0   5   4  0
    ## 691  rextewi01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 692  richmjo01   1875     1    PH1   NA  29 125  29  25   2   0  0  12   1  0
    ## 693  rileybi01   1875     1    KEO   NA   8  33   4   5   1   0  0   1   0  0
    ## 694  rocapad01   1875     1    PH1   NA  16  69  13  12   1   0  0   4   3  2
    ## 695   ryanjo01   1875     1    NH1   NA  37 146  17  23   2   2  0   8  10  4
    ## 696    saylo01   1875     1    WS6   NA  11  38   4  10   0   0  0   2   0  0
    ## 697  schafha01   1875     1    BS1   NA  52 222  49  64   9   0  0  17   3  2
    ## 698  selmafr01   1875     1    WS6   NA   1   3   0   1   0   0  0   0   0  0
    ## 699  sewarge01   1875     1    SL2   NA  25  96  12  24   2   0  0   8   1  0
    ## 700    shaff01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 701  shaffor01   1875     1    PH2   NA  19  70  10  17   2   1  0   6   2  0
    ## 702    sheri01   1875     1    BR2   NA   1   4   0   0   0   0  0   0   0  0
    ## 703  simmojo01   1875     1    KEO   NA  13  53   5   9   1   0  0   4   1  2
    ## 704  smithjo01   1875     1    NH1   NA   1   3   0   0   0   0  0   0   0  0
    ## 705  smithto01   1875     1    BR2   NA   3  13   0   1   0   0  0   1   0  0
    ## 706  snydepo01   1875     1    PH2   NA  66 263  38  64   8   2  1  25   3  8
    ## 707  somered01   1875     1    PH3   NA  14  57   6  13   3   0  0   6   1  0
    ## 708  somered01   1875     2    NH1   NA  33 136  14  29   5   0  0   7   1  2
    ## 709  spaldal01   1875     1    BS1   NA  74 343  68 107  15   3  0  56   2  2
    ## 710  startjo01   1875     1    NY2   NA  69 314  58  90  10   5  4  30   1  4
    ## 711  stearbi01   1875     1    WS6   NA  21  78   9  20   0   0  0   7   0  1
    ## 712  stevero01   1875     1    WS6   NA   1   4   0   1   0   0  0   0   0  0
    ## 713    stodd01   1875     1    BR2   NA   2   9   1   1   1   0  0   0   0  0
    ## 714    sulli01   1875     1    NH1   NA   2   8   3   3   0   0  0   2   1  0
    ## 715  suttoez01   1875     1    PH1   NA  75 358  83 116  11   7  1  59  13 10
    ## 716  sweasch01   1875     1    SL1   NA  19  76   7  13   1   0  0   4   2  4
    ## 717    terry01   1875     1    WS6   NA   6  22   0   4   0   1  0   2   0  0
    ## 718  thompfr01   1875     1    BR2   NA   1   5   1   2   0   0  0   1   0  0
    ## 719  thompfr01   1875     2    WS6   NA  11  41   3   4   0   1  0   3   0  0
    ## 720  tippeji01   1875     1    NH1   NA  41 159  10  25   1   0  0   4   1  0
    ## 721  treacfr01   1875     1    PH3   NA  11  46   9  12   3   0  0   2   1  0
    ## 722  treacfr01   1875     2    PH2   NA  43 179  23  38   3   3  0  15   6  3
    ## 723  trenwge01   1875     1    PH3   NA  10  45   5   8   2   0  0   4   0  0
    ## 724  trenwge01   1875     2    NH1   NA   6  25   1   6   2   0  0   3   0  0
    ## 725  waittch01   1875     1    SL2   NA  30 113  14  23  10   0  0  12   3  2
    ## 726  walkeos01   1875     1    BR2   NA   1   2   0   0   0   0  0   0   0  0
    ## 727  warnefr01   1875     1    PH3   NA  14  57  11  14   4   0  0   2   0  0
    ## 728  waterfr01   1875     1    CH2   NA   5  20   2   6   0   0  0   3   0  1
    ## 729  weavesa01   1875     1    PH2   NA   1   4   1   1   1   0  0   1   0  0
    ## 730  whitede01   1875     1    BS1   NA  80 371  76 136  23   3  1  60   2  3
    ## 731  whitewa01   1875     1    CH2   NA  69 287  37  71   9   0  0  23   5 10
    ## 732  withech01   1875     1    WS6   NA   1   1   0   0   0   0  0   0   0  0
    ## 733  wrighge01   1875     1    BS1   NA  79 408 106 136  20   7  2  61  13  6
    ## 734  wrighha01   1875     1    BS1   NA   1   4   1   1   0   0  0   0   0  0
    ## 735  wrighsa01   1875     1    NH1   NA  33 127  10  24   4   0  0   5   1  0
    ## 736   yorkto01   1875     1    HR1   NA  86 375  68 111  14   7  0  37   7  3
    ## 737  zettlge01   1875     1    CH2   NA  32 133   7  29   0   0  0   9   0  0
    ## 738  zettlge01   1875     2    PH2   NA  21  83  10  15   0   0  0   6   1  0
    ## 739   addybo01   1876     1    CHN   NL  32 142  36  40   4   1  0  16  NA NA
    ## 740  allisar01   1876     1    LS1   NL  31 130   9  27   2   1  0  10  NA NA
    ## 741  allisdo01   1876     1    HAR   NL  44 163  19  43   4   0  0  15  NA NA
    ## 742  andrufr01   1876     1    CHN   NL   8  36   6  11   3   0  0   2  NA NA
    ## 743  ansonca01   1876     1    CHN   NL  66 309  63 110   9   7  2  59  NA NA
    ## 744  barnero01   1876     1    CHN   NL  66 322 126 138  21  14  1  59  NA NA
    ## 745  battijo01   1876     1    SL3   NL  64 283  34  85  11   4  0  46  NA NA
    ## 746  bechtge01   1876     1    LS1   NL  14  55   2  10   1   0  0   2  NA NA
    ## 747  bechtge01   1876     2    NY3   NL   2  10   2   3   0   0  0   0  NA NA
    ## 748  berghjo01   1876     1    PHN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 749  bielaos01   1876     1    CHN   NL  32 139  24  29   3   0  0  10  NA NA
    ## 750  blongjo01   1876     1    SL3   NL  62 264  30  62   7   4  0  30  NA NA
    ## 751   bondto01   1876     1    HAR   NL  45 182  18  50   8   0  0  21  NA NA
    ## 752  bootham01   1876     1    CN1   NL  63 272  31  71   3   0  0  14  NA NA
    ## 753  boothed01   1876     1    NY3   NL  57 228  17  49   2   1  0   7  NA NA
    ## 754  bordejo01   1876     1    BSN   NL  32 121  19  25   3   0  0   7  NA NA
    ## 755  bradlfo01   1876     1    BSN   NL  22  82  12  19   2   1  0   8  NA NA
    ## 756  bradlge01   1876     1    SL3   NL  64 265  29  66   7   6  0  28  NA NA
    ## 757  brownle01   1876     1    BSN   NL  45 195  23  41   6   6  2  21  NA NA
    ## 758  burdoja01   1876     1    HAR   NL  69 309  66  80   9   1  0  23  NA NA
    ## 759  bushodo01   1876     1    PHN   NL   5  21   4   1   0   0  0   1  NA NA
    ## 760  carbijo01   1876     1    LS1   NL   7  25   3   4   0   0  0   1  NA NA
    ## 761  careyto01   1876     1    HAR   NL  68 289  51  78   7   0  0  26  NA NA
    ## 762  cassijo01   1876     1    HAR   NL  12  47   6  13   2   0  0   8  NA NA
    ## 763  chapmja01   1876     1    LS1   NL  17  67   4  16   1   0  0   5  NA NA
    ## 764  clackbo01   1876     1    CN1   NL  32 118  10  19   0   1  0   5  NA NA
    ## 765  clappjo01   1876     1    SL3   NL  64 298  60  91   4   2  0  29  NA NA
    ## 766  clintji01   1876     1    LS1   NL  16  65   8  22   2   0  0   0  NA NA
    ## 767  collida01   1876     1    LS1   NL   7  28   3   4   1   0  0   9  NA NA
    ## 768   coonwi01   1876     1    PHN   NL  54 220  30  50   5   1  0  22  NA NA
    ## 769  cravebi01   1876     1    NY3   NL  56 246  24  55   4   0  0  22  NA NA
    ## 770  cummica01   1876     1    HAR   NL  24 105  14  17   3   0  0   7  NA NA
    ## 771  currepe01   1876     1    PHN   NL   3  12   5   4   1   0  0   2  NA NA
    ## 772  cuthbne01   1876     1    SL3   NL  63 283  46  70  10   1  0  25  NA NA
    ## 773   deando01   1876     1    CN1   NL  34 138   9  36   3   1  0   4  NA NA
    ## 774  dehlmhe01   1876     1    SL3   NL  64 245  40  45   6   0  0   9  NA NA
    ## 775  devliji01   1876     1    LS1   NL  68 298  38  94  14   1  0  28  NA NA
    ## 776  eggleda01   1876     1    PHN   NL  39 174  28  52   4   0  0  19  NA NA
    ## 777   fairge01   1876     1    NY3   NL   1   4   0   0   0   0  0   0  NA NA
    ## 778  fergubo01   1876     1    HAR   NL  69 310  48  82   8   5  0  32  NA NA
    ## 779  fieldsa01   1876     1    CN1   NL   4  14   2   0   0   0  0   0  NA NA
    ## 780  fishech01   1876     1    CN1   NL  35 129  12  32   1   0  0   4  NA NA
    ## 781  fislewe01   1876     1    PHN   NL  59 278  42  80  15   1  1  30  NA NA
    ## 782  foleywi01   1876     1    CN1   NL  58 221  19  50   3   2  0   9  NA NA
    ## 783  forceda01   1876     1    PHN   NL  60 284  48  66   6   0  0  17  NA NA
    ## 784  forceda01   1876     2    NY3   NL   1   3   0   0   0   0  0   0  NA NA
    ## 785  fousebi01   1876     1    PHN   NL  21  89  11  12   0   1  0   2  NA NA
    ## 786  fulmech01   1876     1    LS1   NL  66 267  28  73   9   5  1  29  NA NA
    ## 787  gerhajo01   1876     1    LS1   NL  65 292  33  76  10   3  2  18  NA NA
    ## 788  glennjo01   1876     1    CHN   NL  66 276  55  84   9   2  0  32  NA NA
    ## 789  gouldch01   1876     1    CN1   NL  61 258  27  65   7   0  0  11  NA NA
    ## 790  haguebi01   1876     1    LS1   NL  67 294  31  78   8   0  1  22  NA NA
    ## 791   hallge01   1876     1    PHN   NL  60 268  51  98   7  13  5  45  NA NA
    ## 792  halliji01   1876     1    NY3   NL  54 240  45  67   7   6  2  36  NA NA
    ## 793  harbibi01   1876     1    HAR   NL  30 106  11  23   2   1  0   6  NA NA
    ## 794  hastisc01   1876     1    LS1   NL  67 283  36  73   6   1  0  21  NA NA
    ## 795  hatfijo01   1876     1    NY3   NL   1   4   0   1   0   0  0   1  NA NA
    ## 796  hayesmi01   1876     1    NY3   NL   5  21   1   3   0   2  0   2  NA NA
    ## 797  heubege01   1876     1    NY3   NL   1   4   0   0   0   0  0   0  NA NA
    ## 798  hicksna01   1876     1    NY3   NL  45 188  20  44   4   1  0  15  NA NA
    ## 799  highadi01   1876     1    HAR   NL  67 312  59 102  21   2  0  35  NA NA
    ## 800  hinespa01   1876     1    CHN   NL  64 305  62 101  21   3  2  59  NA NA
    ## 801  holbebi01   1876     1    LS1   NL  12  43   3  11   0   0  0   5  NA NA
    ## 802  holdsji01   1876     1    NY3   NL  52 241  23  64   3   2  0  19  NA NA
    ## 803  jonesch01   1876     1    CN1   NL  64 276  40  79  17   4  4  38  NA NA
    ## 804  kesslhe01   1876     1    CN1   NL  59 248  26  64   5   0  0  11  NA NA
    ## 805  knighlo01   1876     1    PHN   NL  55 240  32  60   9   3  0  24  NA NA
    ## 806  laffefl01   1876     1    PHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 807  larkite01   1876     1    NY3   NL   1   4   0   0   0   0  0   0  NA NA
    ## 808  leonaan01   1876     1    BSN   NL  64 303  53  85  10   2  0  27  NA NA
    ## 809   mackde01   1876     1    SL3   NL  48 180  32  39   5   0  1   7  NA NA
    ## 810  malonfe01   1876     1    PHN   NL  22  96  14  22   2   0  0   6  NA NA
    ## 811  malonjo01   1876     1    NY3   NL   2   7   1   2   0   1  0   2  NA NA
    ## 812  mannija01   1876     1    BSN   NL  70 288  52  76  13   0  2  25  NA NA
    ## 813  mathebo01   1876     1    NY3   NL  56 218  19  40   4   1  0   9  NA NA
    ## 814  mcbridi01   1876     1    BSN   NL   4  16   2   3   0   0  0   4  NA NA
    ## 815  mcgeami01   1876     1    SL3   NL  61 276  48  72   3   0  0  30  NA NA
    ## 816  mcginti01   1876     1    BSN   NL   9  40   5   6   0   0  0   2  NA NA
    ## 817  mcguijo01   1876     1    NY3   NL   1   4   0   0   0   0  0   0  NA NA
    ## 818  mcveyca01   1876     1    CHN   NL  63 308  62 107  15   0  1  53  NA NA
    ## 819  meyerle01   1876     1    PHN   NL  55 256  46  87  12   8  0  34  NA NA
    ## 820  millsev01   1876     1    HAR   NL  63 254  28  66   8   1  0  23  NA NA
    ## 821  morrijo01   1876     1    BSN   NL  66 278  38  73   5   2  0  26  NA NA
    ## 822  mullejo01   1876     1    PHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 823  murnati01   1876     1    BSN   NL  69 308  60  87   4   3  2  34  NA NA
    ## 824  nichoal01   1876     1    NY3   NL  57 212  20  38   4   0  0   9  NA NA
    ## 825  nichotr01   1876     1    BSN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 826  orourji01   1876     1    BSN   NL  70 312  61 102  17   3  2  43  NA NA
    ## 827  parksbi01   1876     1    BSN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 828   paullo01   1876     1    PHN   NL   3  12   2   2   1   0  0   0  NA NA
    ## 829  pearcdi01   1876     1    SL3   NL  25 102  12  21   1   0  0  10  NA NA
    ## 830  pearcfr01   1876     1    LS1   NL   1   2   0   0   0   0  0   0  NA NA
    ## 831  peterjo01   1876     1    CHN   NL  66 316  70 111  14   2  1  47  NA NA
    ## 832  phelpne01   1876     1    NY3   NL   1   3   0   0   0   0  0   0  NA NA
    ## 833  phelpne01   1876     2    PHN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 834  piersda01   1876     1    CN1   NL  57 233  33  55   4   1  0  13  NA NA
    ## 835   pikeli01   1876     1    SL3   NL  63 282  55  91  19  10  1  50  NA NA
    ## 836  remseja01   1876     1    HAR   NL  69 324  62  89  12   5  1  30  NA NA
    ## 837  rittewh01   1876     1    PHN   NL  16  52   8  13   3   0  0   4  NA NA
    ## 838   ryanjo01   1876     1    LS1   NL  64 241  32  61   5   1  1  18  NA NA
    ## 839  schafha01   1876     1    BSN   NL  70 286  47  72  11   0  0  35  NA NA
    ## 840  sewarge01   1876     1    NY3   NL   1   3   0   0   0   0  0   0  NA NA
    ## 841  shandji01   1876     1    NY3   NL   2   8   0   1   0   0  0   0  NA NA
    ## 842  snydepo01   1876     1    LS1   NL  56 224  21  44   4   1  1   9  NA NA
    ## 843  snydere01   1876     1    CN1   NL  55 205  10  31   3   1  0  12  NA NA
    ## 844  somered01   1876     1    LS1   NL  64 256  29  48   5   1  0  14  NA NA
    ## 845  spaldal01   1876     1    CHN   NL  66 292  54  91  14   2  0  44  NA NA
    ## 846  startjo01   1876     1    NY3   NL  56 264  40  73   6   0  0  21  NA NA
    ## 847  suttoez01   1876     1    PHN   NL  54 236  45  70  12   7  1  31  NA NA
    ## 848  sweasch01   1876     1    CN1   NL  56 225  18  46   5   2  0  10  NA NA
    ## 849  treacfr01   1876     1    NY3   NL  57 256  47  54   5   1  0  18  NA NA
    ## 850  treacpe01   1876     1    NY3   NL   2   5   1   0   0   0  0   0  NA NA
    ## 851  valenbo01   1876     1    NY3   NL   1   3   0   0   0   0  0   0  NA NA
    ## 852   wardji01   1876     1    PHN   NL   1   4   1   2   0   0  0   1  NA NA
    ## 853  warnefr01   1876     1    PHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 854   westbi01   1876     1    NY3   NL   1   4   0   0   0   0  0   0  NA NA
    ## 855  whitede01   1876     1    CHN   NL  66 303  66 104  18   1  1  60  NA NA
    ## 856  whitnfr01   1876     1    BSN   NL  34 139  27  33   7   1  0  15  NA NA
    ## 857  willida01   1876     1    CN1   NL   9  35   1   7   0   0  0   1  NA NA
    ## 858  wrighge01   1876     1    BSN   NL  70 335  72 100  18   6  1  34  NA NA
    ## 859  wrighha01   1876     1    BSN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 860  wrighsa01   1876     1    BSN   NL   2   8   0   1   0   0  0   0  NA NA
    ## 861   yorkto01   1876     1    HAR   NL  67 263  47  68  12   7  1  39  NA NA
    ## 862  zettlge01   1876     1    PHN   NL  32 128  11  27   2   1  0  11  NA NA
    ## 863   addybo01   1877     1    CN1   NL  57 245  27  68   2   3  0  31  NA NA
    ## 864  allisdo01   1877     1    HAR   NL  29 115  14  17   2   0  0   6  NA NA
    ## 865  ansonca01   1877     1    CHN   NL  59 255  52  86  19   1  0  32  NA NA
    ## 866  barnero01   1877     1    CHN   NL  22  92  16  25   1   0  0   5  NA NA
    ## 867   bassjo01   1877     1    HAR   NL   1   4   1   1   0   0  0   0  NA NA
    ## 868  battijo01   1877     1    SL3   NL  57 226  28  45   3   7  1  22  NA NA
    ## 869  blongjo01   1877     1    SL3   NL  58 218  17  47   8   3  0  13  NA NA
    ## 870   bondto01   1877     1    BSN   NL  61 259  32  59   4   3  0  30  NA NA
    ## 871  bootham01   1877     1    CN1   NL  44 157  16  27   2   1  0  13  NA NA
    ## 872  bradlge01   1877     1    CHN   NL  55 214  31  52   7   3  0  12  NA NA
    ## 873  brownle01   1877     1    BSN   NL  58 221  27  56  12   8  1  31  NA NA
    ## 874  buncejo01   1877     1    HAR   NL   1   4   0   0   0   0  0   0  NA NA
    ## 875  burdoja01   1877     1    HAR   NL  58 277  35  72   6   0  0   9  NA NA
    ## 876  careyto01   1877     1    HAR   NL  60 274  38  70   3   2  1  20  NA NA
    ## 877  cassijo01   1877     1    HAR   NL  60 251  43  95  10   5  0  27  NA NA
    ## 878  clappjo01   1877     1    SL3   NL  60 255  47  81   6   6  0  34  NA NA
    ## 879  cravebi01   1877     1    LS1   NL  57 238  33  63   5   2  0  29  NA NA
    ## 880  croftar01   1877     1    SL3   NL  54 220  23  51   5   2  0  27  NA NA
    ## 881  crowlbi01   1877     1    LS1   NL  61 238  30  67   9   3  1  23  NA NA
    ## 882  cummica01   1877     1    CN1   NL  19  70   6  14   1   2  0   4  NA NA
    ## 883  cuthbne01   1877     1    CN1   NL  12  56   6  10   5   0  0   2  NA NA
    ## 884  dehlmhe01   1877     1    SL3   NL  32 119  24  22   4   0  0  11  NA NA
    ## 885  devliji01   1877     1    LS1   NL  61 268  38  72   6   3  1  27  NA NA
    ## 886  dorgami01   1877     1    SL3   NL  60 266  45  82   9   7  0  23  NA NA
    ## 887   edench01   1877     1    CHN   NL  15  55   9  12   0   1  0   5  NA NA
    ## 888  eggleda01   1877     1    CHN   NL  33 136  20  36   3   0  0  20  NA NA
    ## 889  fergubo01   1877     1    HAR   NL  58 254  40  65   7   2  0  35  NA NA
    ## 890  fishech01   1877     1    CHN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 891  foleywi01   1877     1    CN1   NL  56 216  23  41   5   1  0  18  NA NA
    ## 892  forceda01   1877     1    SL3   NL  58 225  24  59   5   3  0  22  NA NA
    ## 893  gerhajo01   1877     1    LS1   NL  59 250  41  76   6   5  1  35  NA NA
    ## 894  gleasja01   1877     1    SL3   NL   1   4   0   1   0   0  0   0  NA NA
    ## 895  glennjo01   1877     1    CHN   NL  50 202  31  46   6   1  0  20  NA NA
    ## 896  gouldch01   1877     1    CN1   NL  24  91   5  25   2   1  0  13  NA NA
    ## 897  haguebi01   1877     1    LS1   NL  59 263  38  70   7   1  1  24  NA NA
    ## 898  haldejo01   1877     1    LS1   NL   1   4   0   0   0   0  0   0  NA NA
    ## 899   hallge01   1877     1    LS1   NL  61 269  53  87  15   8  0  26  NA NA
    ## 900  halliji01   1877     1    CN1   NL  16  73  18  27   1   1  0   7  NA NA
    ## 901  halliji01   1877     2    CHN   NL  19  89  17  25   4   1  0  11  NA NA
    ## 902  harbibi01   1877     1    HAR   NL  41 167  18  37   5   2  0   8  NA NA
    ## 903  hastisc01   1877     1    CN1   NL  20  71   7  10   1   0  0   3  NA NA
    ## 904  hicksna01   1877     1    CN1   NL   8  32   3   6   0   0  0   3  NA NA
    ## 905  hinespa01   1877     1    CHN   NL  60 261  44  73  11   7  0  23  NA NA
    ## 906  holdsji01   1877     1    HAR   NL  55 260  26  66   5   2  0  20  NA NA
    ## 907  jonesch01   1877     1    CN1   NL  17  69  16  21   3   3  1  10  NA NA
    ## 908  jonesch01   1877     2    CHN   NL   2   8   1   3   1   0  0   2  NA NA
    ## 909  jonesch01   1877     3    CN1   NL  38 163  36  51   8   7  1  26  NA NA
    ## 910  kesslhe01   1877     1    CN1   NL   6  20   0   2   0   0  0   0  NA NA
    ## 911  laffefl01   1877     1    LS1   NL   4  17   2   1   1   0  0   0  NA NA
    ## 912  larkite01   1877     1    HAR   NL  58 228  28  52   6   5  1  18  NA NA
    ## 913  lathaju01   1877     1    LS1   NL  59 278  42  81  10   6  0  22  NA NA
    ## 914    leele01   1877     1    SL3   NL   4  18   0   5   1   0  0   0  NA NA
    ## 915  leonaan01   1877     1    BSN   NL  58 272  46  78   5   0  0  27  NA NA
    ## 916  littlha01   1877     1    SL3   NL   1   5   0   1   0   0  0   0  NA NA
    ## 917  littlha01   1877     2    LS1   NL   1   3   0   0   0   0  0   0  NA NA
    ## 918  littlha01   1877     3    SL3   NL   2   7   2   1   0   0  0   0  NA NA
    ## 919  loftuto01   1877     1    SL3   NL   3  11   2   2   0   0  0   0  NA NA
    ## 920  malonjo01   1877     1    HAR   NL   1   4   0   1   0   0  0   0  NA NA
    ## 921  mannija01   1877     1    CN1   NL  57 252  47  80  16   7  0  36  NA NA
    ## 922  mathebo01   1877     1    CN1   NL  15  59   5  10   0   0  0   0  NA NA
    ## 923  mcgeami01   1877     1    SL3   NL  57 258  35  65   3   2  0  20  NA NA
    ## 924  mckenpa01   1877     1    SL3   NL   1   5   0   1   0   0  0   0  NA NA
    ## 925  mcveyca01   1877     1    CHN   NL  60 266  58  98   9   7  0  36  NA NA
    ## 926  meyerle01   1877     1    CN1   NL  27 107  11  35   7   2  0  15  NA NA
    ## 927  millege01   1877     1    CN1   NL  11  37   4   6   1   0  0   3  NA NA
    ## 928  mitchbo01   1877     1    CN1   NL  13  49   5  10   3   0  0   5  NA NA
    ## 929  morrijo01   1877     1    BSN   NL  61 242  47  73   5   1  0  28  NA NA
    ## 930  murnati01   1877     1    BSN   NL  35 140  23  39   7   1  1  15  NA NA
    ## 931  newelte01   1877     1    SL3   NL   1   3   0   0   0   0  0   0  NA NA
    ## 932  nichoal01   1877     1    LS1   NL   6  19   1   4   0   1  0   0  NA NA
    ## 933  nichotr01   1877     1    SL3   NL  51 186  22  31   4   2  0   9  NA NA
    ## 934  orourji01   1877     1    BSN   NL  61 265  68  96  14   4  0  23  NA NA
    ## 935  pearcdi01   1877     1    SL3   NL   8  29   1   5   0   0  0   4  NA NA
    ## 936  peterjo01   1877     1    CHN   NL  60 265  45  84  10   3  0  41  NA NA
    ## 937   pikeja01   1877     1    HAR   NL   1   4   0   1   0   0  0   0  NA NA
    ## 938   pikeli01   1877     1    CN1   NL  58 262  45  78  12   4  4  23  NA NA
    ## 939  quinnpa02   1877     1    CHN   NL   4  14   1   1   0   0  0   0  NA NA
    ## 940  redmobi01   1877     1    CN1   NL   3  12   1   3   1   0  0   3  NA NA
    ## 941   reisla01   1877     1    CHN   NL   4  16   3   2   0   0  0   1  NA NA
    ## 942  remseja01   1877     1    SL3   NL  33 123  14  32   3   4  0  13  NA NA
    ## 943   roweda01   1877     1    CHN   NL   2   7   0   2   0   0  0   0  NA NA
    ## 944   ryanjo01   1877     1    CN1   NL   6  26   2   4   0   1  0   2  NA NA
    ## 945  schafha01   1877     1    BSN   NL  33 141  20  39   5   2  0  13  NA NA
    ## 946  shaffor01   1877     1    LS1   NL  61 260  38  74   9   5  3  34  NA NA
    ## 947  smithha01   1877     1    CHN   NL  24  94   7  19   1   0  0   3  NA NA
    ## 948  smithha01   1877     2    CN1   NL  10  36   4   9   2   1  0   3  NA NA
    ## 949  snydepo01   1877     1    LS1   NL  61 248  23  64   7   2  2  28  NA NA
    ## 950  spaldal01   1877     1    CHN   NL  60 254  29  65   7   6  0  35  NA NA
    ## 951  startjo01   1877     1    HAR   NL  60 271  55  90   3   6  1  21  NA NA
    ## 952  sullich01   1877     1    CN1   NL   8  32   4   8   0   0  0   4  NA NA
    ## 953  suttoez01   1877     1    BSN   NL  58 253  43  74  10   6  0  39  NA NA
    ## 954  tayloli01   1877     1    HAR   NL   2   8   0   3   0   0  0   0  NA NA
    ## 955  waittch01   1877     1    CHN   NL  10  41   2   4   0   0  0   2  NA NA
    ## 956  whitede01   1877     1    BSN   NL  59 266  51 103  14  11  2  49  NA NA
    ## 957  whitewi01   1877     1    BSN   NL   3  15   4   3   0   0  0   1  NA NA
    ## 958  wrighge01   1877     1    BSN   NL  61 290  58  80  15   1  0  35  NA NA
    ## 959  wrighha01   1877     1    BSN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 960   yorkto01   1877     1    HAR   NL  56 237  43  67  16   7  1  37  NA NA
    ## 961  allisdo01   1878     1    PRO   NL  19  76   9  22   2   0  0   7  NA NA
    ## 962  ansonca01   1878     1    CHN   NL  60 261  55  89  12   2  0  40  NA NA
    ## 963  bennech01   1878     1    ML2   NL  49 184  16  45   9   0  1  12  NA NA
    ## 964  blissfr01   1878     1    ML2   NL   2   8   1   1   0   0  0   0  NA NA
    ## 965   bondto01   1878     1    BSN   NL  59 236  22  50   4   1  0  23  NA NA
    ## 966  brownle01   1878     1    PRO   NL  58 243  44  74  21   6  1  43  NA NA
    ## 967  burdoja01   1878     1    BSN   NL  60 246  37  64  12   6  0  25  NA NA
    ## 968  careyto01   1878     1    PRO   NL  61 253  33  60  10   3  0  24  NA NA
    ## 969  cassijo01   1878     1    CHN   NL  60 256  33  68   7   1  0  29  NA NA
    ## 970  clappjo01   1878     1    IN1   NL  63 263  42  80  10   2  0  29  NA NA
    ## 971  coreyfr01   1878     1    PRO   NL   7  21   3   3   0   0  0   1  NA NA
    ## 972  creamge01   1878     1    ML2   NL  50 193  30  41   7   3  0  15  NA NA
    ## 973  croftar01   1878     1    IN1   NL  60 222  22  35   6   0  0  16  NA NA
    ## 974  dalryab01   1878     1    ML2   NL  61 271  52  96  10   4  0  15  NA NA
    ## 975  dickebu01   1878     1    CN1   NL  29 123  17  38   5   1  0   9  NA NA
    ## 976  ellicjo01   1878     1    ML2   NL   3  13   2   2   0   0  0   1  NA NA
    ## 977  fergubo01   1878     1    CHN   NL  61 259  44  91  10   2  0  39  NA NA
    ## 978  fishech01   1878     1    PRO   NL   1   3   0   0   0   0  0   0  NA NA
    ## 979  flintsi01   1878     1    IN1   NL  63 254  23  57   7   0  0  18  NA NA
    ## 980  foleywi01   1878     1    ML2   NL  56 229  33  62   8   5  0  22  NA NA
    ## 981   geerbi01   1878     1    CN1   NL  61 237  31  52  13   2  0  20  NA NA
    ## 982  gerhajo01   1878     1    CN1   NL  60 259  46  77   7   2  0  28  NA NA
    ## 983  goldemi01   1878     1    ML2   NL  55 214  16  44   6   3  0  20  NA NA
    ## 984  goodmja01   1878     1    ML2   NL  60 252  28  62   4   3  1  27  NA NA
    ## 985  haguebi01   1878     1    PRO   NL  62 250  21  51   3   0  0  25  NA NA
    ## 986  halliji01   1878     1    CHN   NL  16  67  14  19   3   0  0   2  NA NA
    ## 987  halliji01   1878     2    IN1   NL   3  12   0   3   2   0  0   1  NA NA
    ## 988  hankifr01   1878     1    CHN   NL  58 240  38  64   8   3  1  27  NA NA
    ## 989  harbibi01   1878     1    CHN   NL  54 240  32  71  12   0  0  37  NA NA
    ## 990  healeto01   1878     1    PRO   NL   3   9   0   2   1   0  0   2  NA NA
    ## 991  healeto01   1878     2    IN1   NL  12  45   2   8   1   0  0   4  NA NA
    ## 992  highadi01   1878     1    PRO   NL  62 281  60  90  22   1  1  29  NA NA
    ## 993  hinespa01   1878     1    PRO   NL  62 257  42  92  13   4  4  50  NA NA
    ## 994  holbebi01   1878     1    ML2   NL  45 173  10  32   2   0  0  12  NA NA
    ## 995  jennial01   1878     1    ML2   NL   1   2   0   0   0   0  0   0  NA NA
    ## 996  jonesch01   1878     1    CN1   NL  61 261  50  81  11   7  3  39  NA NA
    ## 997  kellyki01   1878     1    CN1   NL  60 237  29  67   7   1  0  27  NA NA
    ## 998  knowdja01   1878     1    ML2   NL   4  14   2   3   1   0  0   2  NA NA
    ## 999  larkite01   1878     1    CHN   NL  58 226  33  65   9   4  0  32  NA NA
    ## 1000 leonaan01   1878     1    BSN   NL  60 262  41  68   8   5  0  16  NA NA
    ## 1001 mannija01   1878     1    BSN   NL  60 248  41  63  10   1  0  23  NA NA
    ## 1002 mcclebi01   1878     1    CHN   NL  48 205  26  46   6   1  0  29  NA NA
    ## 1003 mccorji01   1878     1    IN1   NL  15  56   5   8   1   0  0   0  NA NA
    ## 1004 mckelru01   1878     1    IN1   NL  63 253  33  57   4   3  2  36  NA NA
    ## 1005 mcveyca01   1878     1    CN1   NL  61 271  43  83  10   4  2  28  NA NA
    ## 1006 mitchbo01   1878     1    CN1   NL  13  49   4  12   0   0  0   8  NA NA
    ## 1007 morgapi01   1878     1    ML2   NL  14  56   2  11   0   0  0   5  NA NA
    ## 1008 morrijo01   1878     1    BSN   NL  60 233  26  56   5   1  0  23  NA NA
    ## 1009 murnati01   1878     1    PRO   NL  49 188  35  45   6   1  0  14  NA NA
    ## 1010 nelsoca01   1878     1    IN1   NL  19  84  12  11   1   0  0   5  NA NA
    ## 1011 nichotr01   1878     1    PRO   NL  11  49   2   9   2   0  0   2  NA NA
    ## 1012 nolanth01   1878     1    IN1   NL  38 152  11  37   8   0  0  16  NA NA
    ## 1013 orourji01   1878     1    BSN   NL  60 255  44  71  17   7  1  29  NA NA
    ## 1014 peterjo01   1878     1    ML2   NL  55 246  33  76   6   1  0  22  NA NA
    ## 1015  pikeli01   1878     1    CN1   NL  31 145  28  47   5   1  0  11  NA NA
    ## 1016  pikeli01   1878     2    PRO   NL   5  22   4   5   0   1  0   4  NA NA
    ## 1017 powerph01   1878     1    CHN   NL   8  31   2   5   1   1  0   2  NA NA
    ## 1018 questjo01   1878     1    IN1   NL  62 278  45  57   3   2  0  13  NA NA
    ## 1019 redmobi01   1878     1    ML2   NL  48 187  16  43   8   0  0  21  NA NA
    ## 1020  reisla01   1878     1    CHN   NL   5  20   2   3   0   0  0   0  NA NA
    ## 1021 remseja01   1878     1    CHN   NL  56 224  32  52  11   1  1  19  NA NA
    ## 1022 schafha01   1878     1    BSN   NL   2   8   0   1   0   0  0   0  NA NA
    ## 1023 shaffor01   1878     1    IN1   NL  63 266  48  90  19   6  0  30  NA NA
    ## 1024 snydepo01   1878     1    BSN   NL  60 226  21  48   5   0  0  14  NA NA
    ## 1025 spaldal01   1878     1    CHN   NL   1   4   0   2   0   0  0   0  NA NA
    ## 1026 startjo01   1878     1    CHN   NL  61 285  58 100  12   5  1  27  NA NA
    ## 1027 sullibi01   1878     1    CHN   NL   2   6   1   1   0   0  0   0  NA NA
    ## 1028 sullich01   1878     1    CN1   NL  61 244  29  63   4   2  0  20  NA NA
    ## 1029 suttoez01   1878     1    BSN   NL  60 239  31  54   9   3  1  29  NA NA
    ## 1030 sweasch01   1878     1    PRO   NL  55 212  23  37   3   0  0   8  NA NA
    ## 1031 traffbi01   1878     1    CHN   NL   2   9   1   1   0   0  0   1  NA NA
    ## 1032  wardjo01   1878     1    PRO   NL  37 138  14  27   5   4  1  15  NA NA
    ## 1033 warnefr01   1878     1    IN1   NL  43 165  19  41   4   0  0  10  NA NA
    ## 1034 weavesa01   1878     1    ML2   NL  48 170  15  34   4   1  0   3  NA NA
    ## 1035 wheelha01   1878     1    PRO   NL   7  27   7   4   0   0  0   1  NA NA
    ## 1036 whitede01   1878     1    CN1   NL  61 258  41  81   4   1  0  29  NA NA
    ## 1037 whitewi01   1878     1    CN1   NL  52 197  15  28   1   1  0   9  NA NA
    ## 1038 willine01   1878     1    IN1   NL  63 250  31  58  10   2  1  19  NA NA
    ## 1039 wrighge01   1878     1    BSN   NL  59 267  35  60   5   1  0  12  NA NA
    ## 1040  yorkto01   1878     1    PRO   NL  62 269  56  83  19  10  1  26  NA NA
    ## 1041 adamsge01   1879     1    SR1   NL   4  13   0   3   0   0  0   0  NA NA
    ## 1042 allenja01   1879     1    SR1   NL  11  48   7   9   2   1  0   3  NA NA
    ## 1043 allenja01   1879     2    CL2   NL  16  60   7   7   1   1  0   4  NA NA
    ## 1044 allisdo01   1879     1    PRO   NL   1   5   0   0   0   0  0   0  NA NA
    ## 1045 ansonca01   1879     1    CHN   NL  51 227  40  72  20   1  0  34  NA NA
    ## 1046 barnero01   1879     1    CN1   NL  77 323  55  86   9   2  1  30  NA NA
    ## 1047  bondto01   1879     1    BSN   NL  65 257  35  62   3   1  0  21  NA NA
    ## 1048 bradlge01   1879     1    TRN   NL  63 251  36  62   9   5  0  23  NA NA
    ## 1049 broutda01   1879     1    TRN   NL  39 168  17  46  12   1  4  17  NA NA
    ## 1050 brownle01   1879     1    PRO   NL  53 229  23  59  13   4  2  38  NA NA
    ## 1051 brownle01   1879     2    CHN   NL   6  21   2   6   1   0  0   3  NA NA
    ## 1052 burdoja01   1879     1    BSN   NL  84 359  64  86  10   3  0  36  NA NA
    ## 1053 burkemi01   1879     1    CN1   NL  28 117  13  26   3   0  0   8  NA NA
    ## 1054 careyto01   1879     1    CL2   NL  80 335  30  80  14   1  0  32  NA NA
    ## 1055 carpehi01   1879     1    SR1   NL  65 261  30  53   6   0  0  20  NA NA
    ## 1056 caskied01   1879     1    TRN   NL  70 304  32  78  13   2  0  21  NA NA
    ## 1057 cassijo01   1879     1    TRN   NL   9  37   4   7   1   0  0   1  NA NA
    ## 1058 clappaa01   1879     1    TRN   NL  36 146  24  39   9   3  0  18  NA NA
    ## 1059 clappjo01   1879     1    BFN   NL  70 292  47  77  12   5  1  36  NA NA
    ## 1060 cogswed01   1879     1    BSN   NL  49 236  51  76   8   1  1  18  NA NA
    ## 1061 creamge01   1879     1    SR1   NL  15  60   3  13   2   0  0   3  NA NA
    ## 1062 crowlbi01   1879     1    BFN   NL  60 261  41  75   9   5  0  30  NA NA
    ## 1063 dalryab01   1879     1    CHN   NL  71 333  47  97  25   1  0  23  NA NA
    ## 1064 deckefr01   1879     1    SR1   NL   3  10   0   1   0   0  0   0  NA NA
    ## 1065 dickebu01   1879     1    CN1   NL  81 350  73 102  18  14  2  57  NA NA
    ## 1066 dolanto01   1879     1    CHN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1067 dorgami01   1879     1    SR1   NL  59 270  38  72  11   5  1  17  NA NA
    ## 1068 doschhe01   1879     1    TRN   NL  47 191  16  42   8   0  0  18  NA NA
    ## 1069 doschhe01   1879     2    CHN   NL   3  11   1   2   0   0  0   1  NA NA
    ## 1070  edench01   1879     1    CL2   NL  81 353  40  96  31   7  3  34  NA NA
    ## 1071 eggleda01   1879     1    BFN   NL  78 317  41  66   5   7  0  27  NA NA
    ## 1072 evansja01   1879     1    TRN   NL  72 280  30  65   9   5  0  17  NA NA
    ## 1073 farreja02   1879     1    SR1   NL  54 241  40  73   6   2  1  21  NA NA
    ## 1074 farreja02   1879     2    PRO   NL  12  51   5  13   2   0  0   5  NA NA
    ## 1075 fergubo01   1879     1    TRN   NL  30 123  18  31   5   2  0   4  NA NA
    ## 1076 flintsi01   1879     1    CHN   NL  79 324  46  92  22   6  1  41  NA NA
    ## 1077 foleycu01   1879     1    BSN   NL  35 146  16  46   3   1  0  17  NA NA
    ## 1078 foleywi01   1879     1    CN1   NL  56 218  22  46   5   1  0  25  NA NA
    ## 1079 forceda01   1879     1    BFN   NL  79 316  36  66   5   2  0   8  NA NA
    ## 1080 fulmech01   1879     1    BFN   NL  76 306  30  82  11   5  0  28  NA NA
    ## 1081 galvipu01   1879     1    BFN   NL  67 265  34  66  11   6  0  27  NA NA
    ## 1082 gardngi01   1879     1    TRN   NL   2   6   1   1   0   0  0   0  NA NA
    ## 1083 gerhajo01   1879     1    CN1   NL  79 313  22  62  12   3  1  39  NA NA
    ## 1084 gilliba01   1879     1    CL2   NL  52 205  20  35   6   2  0  11  NA NA
    ## 1085 glassja01   1879     1    CL2   NL  80 325  31  68   9   3  0  29  NA NA
    ## 1086 goldsfr01   1879     1    TRN   NL   9  38   6   9   1   0  0   2  NA NA
    ## 1087  gorege01   1879     1    CHN   NL  63 266  43  70  17   4  0  32  NA NA
    ## 1088 grossem01   1879     1    PRO   NL  30 132  31  46   9   5  0  24  NA NA
    ## 1089 gunklfr01   1879     1    CL2   NL   1   3   1   0   0   0  0   0  NA NA
    ## 1090 haguebi01   1879     1    PRO   NL  51 209  20  47   3   1  0  21  NA NA
    ## 1091  hallal01   1879     1    TRN   NL  67 306  30  79   7   3  0  14  NA NA
    ## 1092 hankifr01   1879     1    CHN   NL  44 171  14  31   4   0  0   8  NA NA
    ## 1093 harbibi01   1879     1    CHN   NL   4  18   2   2   0   0  0   1  NA NA
    ## 1094 hawesbi01   1879     1    BSN   NL  38 155  19  31   3   3  0   9  NA NA
    ## 1095 hawketh01   1879     1    TRN   NL  64 250  24  52   6   1  0  20  NA NA
    ## 1096 hinespa01   1879     1    PRO   NL  85 409  81 146  25  10  2  52  NA NA
    ## 1097 hoffmhi01   1879     1    CL2   NL   2   6   0   0   0   0  0   0  NA NA
    ## 1098 holbebi01   1879     1    SR1   NL  59 229  11  46   0   0  0  21  NA NA
    ## 1099 holbebi01   1879     2    TRN   NL   4  15   1   4   0   0  0   2  NA NA
    ## 1100 hornujo01   1879     1    BFN   NL  78 319  46  85  18   7  0  38  NA NA
    ## 1101 hotalpe01   1879     1    CN1   NL  81 369  64 103  20   9  1  27  NA NA
    ## 1102 houcksa01   1879     1    BSN   NL  80 356  69  95  24   9  2  49  NA NA
    ## 1103 jonesch01   1879     1    BSN   NL  83 355  85 112  22  10  9  62  NA NA
    ## 1104 kellyjo01   1879     1    CL2   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1105 kellyki01   1879     1    CN1   NL  77 345  78 120  20  12  2  47  NA NA
    ## 1106 kellyki02   1879     1    SR1   NL  10  36   4   4   1   0  0   2  NA NA
    ## 1107 kellyki02   1879     2    TRN   NL   6  22   1   5   0   0  0   0  NA NA
    ## 1108 kemmlru01   1879     1    PRO   NL   2   7   0   1   0   0  0   0  NA NA
    ## 1109 kennedo01   1879     1    CL2   NL  49 193  19  56   8   2  1  18  NA NA
    ## 1110 larkite01   1879     1    CHN   NL  60 228  26  50  12   2  0  18  NA NA
    ## 1111 libbyst01   1879     1    BFN   NL   1   2   0   0   0   0  0   0  NA NA
    ## 1112 maculji01   1879     1    SR1   NL  64 246  24  52   9   0  0  13  NA NA
    ## 1113 magnejo01   1879     1    CN1   NL   1   4   0   0   0   0  0   1  NA NA
    ## 1114 mansemi01   1879     1    SR1   NL  67 242  24  52   4   2  1  13  NA NA
    ## 1115 manseto01   1879     1    TRN   NL  40 177  29  43   6   0  0  11  NA NA
    ## 1116 manseto01   1879     2    SR1   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1117 mathebo01   1879     1    PRO   NL  43 173  25  35   2   0  1  10  NA NA
    ## 1118 mccorha01   1879     1    SR1   NL  57 230  21  51   4   1  1  21  NA NA
    ## 1119 mccorji01   1879     1    CL2   NL  75 282  35  62  10   2  0  20  NA NA
    ## 1120 mcgeami01   1879     1    PRO   NL  85 374  62 103   7   2  0  35  NA NA
    ## 1121 mcguijo01   1879     1    SR1   NL  12  51   7  15   1   1  0   4  NA NA
    ## 1122 mcgunbi01   1879     1    BFN   NL  47 171  22  30   0   1  0   5  NA NA
    ## 1123 mcmanpa01   1879     1    TRN   NL   2   8   0   1   0   0  0   0  NA NA
    ## 1124 mcveyca01   1879     1    CN1   NL  81 354  64 105  18   6  0  55  NA NA
    ## 1125 mitchbo01   1879     1    CL2   NL  30 109  11  16   2   2  0   6  NA NA
    ## 1126 morrijo01   1879     1    BSN   NL  84 348  56  98  18   5  0  49  NA NA
    ## 1127 neaglja01   1879     1    CN1   NL   3  12   1   2   0   0  0   2  NA NA
    ## 1128 nelsoca01   1879     1    TRN   NL  28 106  17  28   7   1  0  10  NA NA
    ## 1129 olearda01   1879     1    PRO   NL   2   7   1   3   0   0  0   2  NA NA
    ## 1130 orourji01   1879     1    PRO   NL  81 362  69 126  19   9  1  46  NA NA
    ## 1131 orourjo01   1879     1    BSN   NL  72 317  69 108  17  11  6  62  NA NA
    ## 1132 osterch01   1879     1    SR1   NL   2   8   0   0   0   0  0   0  NA NA
    ## 1133 peterjo01   1879     1    CHN   NL  83 379  45  93  13   2  1  31  NA NA
    ## 1134 phillbi01   1879     1    CL2   NL  81 365  58  99  15   4  0  29  NA NA
    ## 1135 purcebl01   1879     1    SR1   NL  63 277  32  72   6   3  0  25  NA NA
    ## 1136 purcebl01   1879     2    CN1   NL  12  50  10  11   0   0  0   4  NA NA
    ## 1137 questjo01   1879     1    CHN   NL  83 334  38  69  16   1  0  22  NA NA
    ## 1138 reillch01   1879     1    TRN   NL  62 236  17  54   5   1  0  19  NA NA
    ## 1139 remseja01   1879     1    CHN   NL  42 152  14  33   4   2  0   8  NA NA
    ## 1140 richaha01   1879     1    BFN   NL  79 336  54  95  18  10  0  37  NA NA
    ## 1141 richmjo01   1879     1    SR1   NL  62 254  31  54   8   4  1  23  NA NA
    ## 1142 richmle01   1879     1    BSN   NL   1   6   0   2   0   0  0   1  NA NA
    ## 1143 rileybi01   1879     1    CL2   NL  43 161  14  23   2   0  0   9  NA NA
    ## 1144  roweja01   1879     1    BFN   NL   8  34   8  12   1   0  0   8  NA NA
    ## 1145 salisha01   1879     1    TRN   NL  10  36   3   2   0   0  0   0  NA NA
    ## 1146 shaffor01   1879     1    CHN   NL  73 316  53  96  13   0  0  35  NA NA
    ## 1147 shoupjo01   1879     1    TRN   NL  11  44   5   4   0   0  0   1  NA NA
    ## 1148 snydepo01   1879     1    BSN   NL  81 329  42  78  16   3  2  35  NA NA
    ## 1149 startjo01   1879     1    PRO   NL  66 317  70 101  11   5  2  37  NA NA
    ## 1150 stedrjo01   1879     1    CHN   NL   4  12   0   1   0   0  0   0  NA NA
    ## 1151 stockle01   1879     1    CL2   NL   2   6   0   0   0   0  0   0  NA NA
    ## 1152 striege01   1879     1    CL2   NL  71 264  24  46   7   1  0  15  NA NA
    ## 1153 sullide01   1879     1    PRO   NL   5  19   5   5   2   0  0   2  NA NA
    ## 1154 suttoez01   1879     1    BSN   NL  84 339  54  84  13   4  0  34  NA NA
    ## 1155 tayloli01   1879     1    TRN   NL  24  97  10  21   4   0  0   8  NA NA
    ## 1156  tyngji01   1879     1    BSN   NL   3  14   2   5   1   0  0   0  NA NA
    ## 1157 walkeos01   1879     1    BFN   NL  72 287  35  79  15   6  1  35  NA NA
    ## 1158  wardjo01   1879     1    PRO   NL  83 364  71 104   9   4  2  41  NA NA
    ## 1159 warnefr01   1879     1    CL2   NL  76 316  32  77  11   4  0  22  NA NA
    ## 1160 wheelha01   1879     1    CN1   NL   1   3   0   0   0   0  0   0  NA NA
    ## 1161 whitebi01   1879     1    PRO   NL   1   4   1   1   0   0  0   0  NA NA
    ## 1162 whitede01   1879     1    CN1   NL  78 333  55 110  16   6  1  52  NA NA
    ## 1163 whitewi01   1879     1    CN1   NL  76 294  28  40   6   0  0  17  NA NA
    ## 1164 willine01   1879     1    CHN   NL  80 320  66  94  20  13  1  36  NA NA
    ## 1165 woodhre01   1879     1    SR1   NL  34 131   4  21   1   0  0   2  NA NA
    ## 1166 wrighge01   1879     1    PRO   NL  85 388  79 107  15  10  1  42  NA NA
    ## 1167  yorkto01   1879     1    PRO   NL  81 342  69 106  25   5  1  50  NA NA
    ## 1168 ahearch01   1880     1    TRN   NL   1   4   1   1   0   0  0   0  NA NA
    ## 1169 ansonca01   1880     1    CHN   NL  86 356  54 120  24   1  1  74  NA NA
    ## 1170 bealsto01   1880     1    CHN   NL  13  46   4   7   0   0  0   3  NA NA
    ## 1171 bennech01   1880     1    WOR   NL  51 193  20  44   9   3  0  18  NA NA
    ## 1172 berghjo01   1880     1    BSN   NL  11  40   2   8   3   0  0   0  NA NA
    ## 1173  bondto01   1880     1    BSN   NL  76 282  27  62   4   1  0  24  NA NA
    ## 1174 bootham01   1880     1    CN1   NL   1   2   0   0   0   0  0   0  NA NA
    ## 1175 bradlge01   1880     1    PRO   NL  82 309  32  70   7   6  0  23  NA NA
    ## 1176 briodfa01   1880     1    TRN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1177 broutda01   1880     1    TRN   NL   3  12   0   2   0   0  0   1  NA NA
    ## 1178 burdoja01   1880     1    BSN   NL  86 356  58  90  17   4  2  35  NA NA
    ## 1179 burnsto01   1880     1    CHN   NL  85 333  47 103  17   3  0  43  NA NA
    ## 1180 bushodo01   1880     1    WOR   NL  41 146  13  25   3   0  0  19  NA NA
    ## 1181 carpehi01   1880     1    CN1   NL  77 300  32  72   6   4  0  23  NA NA
    ## 1182 caskied01   1880     1    TRN   NL  82 333  36  75   5   4  0  28  NA NA
    ## 1183 cassijo01   1880     1    TRN   NL  83 352  40  89  14   8  0  29  NA NA
    ## 1184 clappjo01   1880     1    CN1   NL  80 323  33  91  16   4  1  20  NA NA
    ## 1185 cogswed01   1880     1    TRN   NL  47 209  41  63   7   3  0  13  NA NA
    ## 1186 connoro01   1880     1    TRN   NL  83 340  53 113  18   8  3  47  NA NA
    ## 1187 corcola01   1880     1    CHN   NL  72 286  41  66  11   1  0  25  NA NA
    ## 1188 coreyfr01   1880     1    WOR   NL  41 138  11  24   8   1  0   6  NA NA
    ## 1189 cranesa01   1880     1    BFN   NL  10  31   4   4   0   0  0   2  NA NA
    ## 1190 creamge01   1880     1    WOR   NL  85 306  40  61   6   3  0  27  NA NA
    ## 1191 crowlbi01   1880     1    BFN   NL  85 354  57  95  16   4  0  20  NA NA
    ## 1192 dalryab01   1880     1    CHN   NL  86 382  91 126  25  12  0  36  NA NA
    ## 1193 dickebu01   1880     1    TRN   NL  30 119  15  23   2   2  0  10  NA NA
    ## 1194 dickebu01   1880     2    WOR   NL  31 133  22  39   8   6  0  20  NA NA
    ## 1195 dignast01   1880     1    BSN   NL   8  34   4  11   1   0  0   4  NA NA
    ## 1196 dignast01   1880     2    WOR   NL   3  10   1   3   0   1  0   2  NA NA
    ## 1197 dorgaje01   1880     1    WOR   NL  10  35   2   7   1   0  0   1  NA NA
    ## 1198 dorgami01   1880     1    PRO   NL  79 321  45  79  10   1  0  31  NA NA
    ## 1199 driscde01   1880     1    BFN   NL  18  65   1  10   1   0  0   4  NA NA
    ## 1200 dunlafr01   1880     1    CL2   NL  85 373  61 103  27   9  4  30  NA NA
    ## 1201 ellicjo01   1880     1    WOR   NL   5  18   1   1   0   0  0   0  NA NA
    ## 1202 esterdu01   1880     1    BFN   NL  64 253  20  61  12   1  0  35  NA NA
    ## 1203 evansja01   1880     1    TRN   NL  47 180  31  46   8   1  0  22  NA NA
    ## 1204 ewingbu01   1880     1    TRN   NL  13  45   1   8   1   0  0   5  NA NA
    ## 1205 farreja02   1880     1    PRO   NL  80 339  46  92  12   5  3  36  NA NA
    ## 1206 fergubo01   1880     1    TRN   NL  82 332  55  87   9   0  0  22  NA NA
    ## 1207 flintsi01   1880     1    CHN   NL  74 284  30  46  10   4  0  17  NA NA
    ## 1208 foleycu01   1880     1    BSN   NL  80 332  44  97  13   2  2  31  NA NA
    ## 1209 forceda01   1880     1    BFN   NL  81 290  22  49  10   0  0  17  NA NA
    ## 1210 fulmech01   1880     1    BFN   NL  11  44   3   7   0   0  0   1  NA NA
    ## 1211 galvipu01   1880     1    BFN   NL  66 241  25  51   9   2  0  12  NA NA
    ## 1212 gardngi01   1880     1    CL2   NL  10  32   0   6   1   1  0   4  NA NA
    ## 1213  geerbi01   1880     1    WOR   NL   2   6   0   0   0   0  0   0  NA NA
    ## 1214 gillepe01   1880     1    TRN   NL  82 346  50  84  20   5  2  24  NA NA
    ## 1215 gilliba01   1880     1    CL2   NL  30  99   9  17   4   3  1  13  NA NA
    ## 1216 glassja01   1880     1    CL2   NL  77 296  37  72  13   3  0  27  NA NA
    ## 1217 goldsfr01   1880     1    CHN   NL  35 142  24  37   4   2  0  15  NA NA
    ## 1218  gorege01   1880     1    CHN   NL  77 322  70 116  23   2  2  47  NA NA
    ## 1219 grossem01   1880     1    PRO   NL  87 347  43  90  18   3  1  34  NA NA
    ## 1220  guthch01   1880     1    CHN   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1221 haleyfr01   1880     1    TRN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 1222  hallal01   1880     1    CL2   NL   3   8   1   1   0   0  0   0  NA NA
    ## 1223 hankifr01   1880     1    CL2   NL  69 263  32  55   7   4  1  19  NA NA
    ## 1224 hanlone01   1880     1    CL2   NL  73 280  30  69  10   3  0  32  NA NA
    ## 1225 harbibi01   1880     1    TRN   NL   9  27   3  10   0   1  0   2  NA NA
    ## 1226 highadi01   1880     1    TRN   NL   1   5   1   1   0   0  0   0  NA NA
    ## 1227 hinespa01   1880     1    PRO   NL  85 374  64 115  20   2  3  35  NA NA
    ## 1228 holbebi01   1880     1    TRN   NL  60 212  18  40   5   1  0   8  NA NA
    ## 1229 hornujo01   1880     1    BFN   NL  85 342  47  91   8  11  1  42  NA NA
    ## 1230 hotalpe01   1880     1    CL2   NL  78 325  40  78  17   8  0  41  NA NA
    ## 1231 houcksa01   1880     1    BSN   NL  12  47   2   7   0   0  0   2  NA NA
    ## 1232 houcksa01   1880     2    PRO   NL  49 184  27  37   7   7  1  22  NA NA
    ## 1233 irwinar01   1880     1    WOR   NL  85 352  53  91  19   4  1  35  NA NA
    ## 1234 jonesch01   1880     1    BSN   NL  66 280  44  84  15   3  5  37  NA NA
    ## 1235 kearnto01   1880     1    BFN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 1236 keefeti01   1880     1    TRN   NL  12  43   4  10   3   0  0   3  NA NA
    ## 1237 keenaji01   1880     1    BFN   NL   2   7   1   1   0   0  0   0  NA NA
    ## 1238 kellyki01   1880     1    CHN   NL  84 344  72 100  17   9  1  60  NA NA
    ## 1239 kennedo01   1880     1    CL2   NL  66 250  26  50  10   1  0  18  NA NA
    ## 1240 knighlo01   1880     1    WOR   NL  49 201  31  48  11   3  0  21  NA NA
    ## 1241 larkite01   1880     1    TRN   NL   6  20   1   3   1   0  0   1  NA NA
    ## 1242 lathaar01   1880     1    BFN   NL  22  79   9  10   3   1  0   3  NA NA
    ## 1243 lawlomi01   1880     1    TRN   NL   4   9   1   1   0   0  0   0  NA NA
    ## 1244 learyja01   1880     1    BSN   NL   1   3   1   0   0   0  0   0  NA NA
    ## 1245 leonaan01   1880     1    CN1   NL  33 133  15  28   3   0  1  17  NA NA
    ## 1246  mackde01   1880     1    BFN   NL  17  59   5  12   0   0  0   3  NA NA
    ## 1247 mannija01   1880     1    CN1   NL  48 190  20  41   6   3  2  17  NA NA
    ## 1248 mansemi01   1880     1    CN1   NL  53 187  22  36   6   2  2  12  NA NA
    ## 1249 mccorji01   1880     1    CL2   NL  78 289  34  71  11   0  0  26  NA NA
    ## 1250 mcgeami01   1880     1    PRO   NL  18  59   5   8   0   0  0   1  NA NA
    ## 1251 mcgeami01   1880     2    CL2   NL  31 111  14  28   2   1  0   6  NA NA
    ## 1252 mcgunbi01   1880     1    BFN   NL   7  22   0   4   0   0  0   1  NA NA
    ## 1253 mcgunbi01   1880     2    WOR   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1254 morrijo01   1880     1    BSN   NL  86 342  51  81  16   8  2  44  NA NA
    ## 1255 mountfr01   1880     1    TRN   NL   2   9   1   2   0   0  0   0  NA NA
    ## 1256 moynami01   1880     1    BFN   NL  27 100  12  33   5   1  0  14  NA NA
    ## 1257 nichotr01   1880     1    WOR   NL   2   7   0   0   0   0  0   0  NA NA
    ## 1258 olearda01   1880     1    BSN   NL   3  12   1   3   2   0  0   1  NA NA
    ## 1259 orourji01   1880     1    BSN   NL  86 363  71 100  20  11  6  45  NA NA
    ## 1260 orourjo01   1880     1    BSN   NL  81 313  30  86  22   8  3  36  NA NA
    ## 1261 peterjo01   1880     1    PRO   NL  86 359  30  82   5   0  0  24  NA NA
    ## 1262 phillbi01   1880     1    CL2   NL  85 334  41  85  14  10  1  36  NA NA
    ## 1263 poormto01   1880     1    BFN   NL  19  70   5  11   1   0  0   1  NA NA
    ## 1264 poormto01   1880     2    CHN   NL   7  25   3   5   1   2  0   0  NA NA
    ## 1265 powerph01   1880     1    BSN   NL  37 126  11  18   5   0  0  10  NA NA
    ## 1266 purcebl01   1880     1    CN1   NL  77 325  48  95  13   6  1  24  NA NA
    ## 1267 questjo01   1880     1    CHN   NL  82 300  37  71  12   1  0  27  NA NA
    ## 1268 radboch01   1880     1    BFN   NL   6  21   1   3   0   0  0   1  NA NA
    ## 1269 reillch01   1880     1    CN1   NL  30 103   8  21   1   0  0   9  NA NA
    ## 1270 reilljo01   1880     1    CN1   NL  73 272  21  56   8   4  0  16  NA NA
    ## 1271 richaha01   1880     1    BFN   NL  83 343  48  89  18   8  0  17  NA NA
    ## 1272 richmjo01   1880     1    BSN   NL  32 129  12  32   3   1  0   9  NA NA
    ## 1273 richmle01   1880     1    WOR   NL  77 309  44  70   8   4  0  34  NA NA
    ## 1274  roweja01   1880     1    BFN   NL  79 326  43  82  10   6  1  36  NA NA
    ## 1275   saylo01   1880     1    CN1   NL  48 191  14  38   8   1  0  15  NA NA
    ## 1276 shaffor01   1880     1    CL2   NL  83 338  62  90  14   9  0  21  NA NA
    ## 1277 smithpo01   1880     1    CN1   NL  83 334  35  69  10   9  0  27  NA NA
    ## 1278 sommejo01   1880     1    CN1   NL  24  88  10  16   1   0  0   6  NA NA
    ## 1279 startjo01   1880     1    PRO   NL  82 345  53  96  14   6  0  27  NA NA
    ## 1280 stearec01   1880     1    BFN   NL  28 104   8  19   6   1  0  13  NA NA
    ## 1281 stoveha01   1880     1    WOR   NL  83 355  76  94  21  14  6  28  NA NA
    ## 1282 straujo01   1880     1    TRN   NL   3  12   1   3   0   0  0   3  NA NA
    ## 1283 sullich01   1880     1    WOR   NL  43 166  22  43   6   3  0   0  NA NA
    ## 1284 sullide01   1880     1    BSN   NL   1   4   1   1   0   0  0   2  NA NA
    ## 1285 suttoez01   1880     1    BSN   NL  76 288  41  72   9   2  0  25  NA NA
    ## 1286 tobinbi01   1880     1    WOR   NL   5  16   1   2   0   0  0   3  NA NA
    ## 1287 tobinbi01   1880     2    TRN   NL  33 136  14  22   1   1  0   8  NA NA
    ## 1288 trottsa01   1880     1    BSN   NL  39 125  14  26   4   1  0   9  NA NA
    ## 1289 walkeos01   1880     1    BFN   NL  34 126  12  29   4   2  1  15  NA NA
    ## 1290  wardjo01   1880     1    PRO   NL  86 356  53  81  12   2  0  27  NA NA
    ## 1291 welchmi01   1880     1    TRN   NL  66 251  25  72  20   3  0  27  NA NA
    ## 1292 wheelha01   1880     1    CL2   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1293 wheelha01   1880     2    CN1   NL  17  65   1   6   2   0  0   2  NA NA
    ## 1294 whitede01   1880     1    CN1   NL  35 141  21  42   4   2  0   7  NA NA
    ## 1295 whitewi01   1880     1    CN1   NL  62 207  16  35   7   1  0  14  NA NA
    ## 1296 whitnar01   1880     1    WOR   NL  76 302  38  67  13   5  1  36  NA NA
    ## 1297 wiedmst01   1880     1    BFN   NL  23  78   8   8   1   0  0   3  NA NA
    ## 1298 willine01   1880     1    CHN   NL  75 311  65  78  20   2  0  31  NA NA
    ## 1299  woodge01   1880     1    WOR   NL  81 327  37  80  16   5  0  28  NA NA
    ## 1300 wrighge01   1880     1    BSN   NL   1   4   2   1   0   0  0   0  NA NA
    ## 1301 wrighsa01   1880     1    CN1   NL   9  34   0   3   0   0  0   0  NA NA
    ## 1302  yorkto01   1880     1    PRO   NL  53 203  21  43   9   2  0  18  NA NA
    ## 1303 ansonca01   1881     1    CHN   NL  84 343  67 137  21   7  1  82  NA NA
    ## 1304 barnero01   1881     1    BSN   NL  69 295  42  80  14   1  0  17  NA NA
    ## 1305 bennech01   1881     1    DTN   NL  76 299  44  90  18   7  7  64  NA NA
    ## 1306  bondto01   1881     1    BSN   NL   3  10   0   2   0   0  0   0  NA NA
    ## 1307 bradlge01   1881     1    DTN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1308 bradlge01   1881     2    CL2   NL  60 241  21  60  10   1  2  18  NA NA
    ## 1309 broutda01   1881     1    BFN   NL  65 270  60  86  18   9  8  45  NA NA
    ## 1310 brownle01   1881     1    DTN   NL  27 108  16  26   3   1  3  14  NA NA
    ## 1311 brownle01   1881     2    PRO   NL  18  75   9  18   3   1  0  10  NA NA
    ## 1312 burdoja01   1881     1    BSN   NL  73 282  36  67  12   4  1  24  NA NA
    ## 1313 burnsto01   1881     1    CHN   NL  84 342  41  95  20   3  4  42  NA NA
    ## 1314 bushodo01   1881     1    WOR   NL  76 275  35  64   7   4  0  21  NA NA
    ## 1315 carpehi01   1881     1    WOR   NL  83 347  40  75  12   2  2  31  NA NA
    ## 1316 caskied01   1881     1    TRN   NL  63 234  33  53   7   1  0  21  NA NA
    ## 1317 cassijo01   1881     1    TRN   NL  85 370  57  82  13   3  1  11  NA NA
    ## 1318 clappjo01   1881     1    CL2   NL  68 261  47  66  12   2  0  25  NA NA
    ## 1319 connoro01   1881     1    TRN   NL  85 367  55 107  17   6  2  31  NA NA
    ## 1320 corcola01   1881     1    CHN   NL  47 189  25  42   8   0  0   9  NA NA
    ## 1321 coreyfr01   1881     1    WOR   NL  51 203  22  45   8   4  0  10  NA NA
    ## 1322 creamge01   1881     1    WOR   NL  80 309  42  64   9   2  0  25  NA NA
    ## 1323 crowlbi01   1881     1    BSN   NL  72 279  33  71  12   0  0  31  NA NA
    ## 1324 dalryab01   1881     1    CHN   NL  82 362  72 117  22   4  1  37  NA NA
    ## 1325 deaslpa01   1881     1    BSN   NL  43 147  13  35   5   2  0   8  NA NA
    ## 1326 dennyje01   1881     1    PRO   NL  85 320  38  77  16   2  1  24  NA NA
    ## 1327 derbyge01   1881     1    DTN   NL  59 236  17  44   3   1  0  12  NA NA
    ## 1328 dickebu01   1881     1    WOR   NL  80 367  48 116  18   6  1  31  NA NA
    ## 1329 dorgami01   1881     1    WOR   NL  51 220  36  61   5   0  0  18  NA NA
    ## 1330 dorgami01   1881     2    DTN   NL   8  34   5   8   1   0  0   5  NA NA
    ## 1331 doschhe01   1881     1    CL2   NL   5  19   2   4   0   0  0   0  NA NA
    ## 1332 dunlafr01   1881     1    CL2   NL  80 351  60 114  25   4  3  24  NA NA
    ## 1333 evansja01   1881     1    TRN   NL  83 315  35  76  11   5  0  28  NA NA
    ## 1334 ewingbu01   1881     1    TRN   NL  67 272  40  68  14   7  0  25  NA NA
    ## 1335 farreja02   1881     1    PRO   NL  84 345  69  82  16   5  5  36  NA NA
    ## 1336 fergubo01   1881     1    TRN   NL  85 339  56  96  13   5  1  35  NA NA
    ## 1337 flahema01   1881     1    WOR   NL   1   2   0   0   0   0  0   0  NA NA
    ## 1338 flintsi01   1881     1    CHN   NL  80 306  46  95  18   0  1  34  NA NA
    ## 1339 foleycu01   1881     1    BFN   NL  83 375  58  96  20   2  1  25  NA NA
    ## 1340 foleywi01   1881     1    DTN   NL   5  15   0   2   0   0  0   1  NA NA
    ## 1341 forceda01   1881     1    BFN   NL  75 278  21  50   9   1  0  15  NA NA
    ## 1342   foxjo01   1881     1    BSN   NL  30 118   8  21   0   0  0   4  NA NA
    ## 1343 galvipu01   1881     1    BFN   NL  62 236  19  50  12   4  0  21  NA NA
    ## 1344 gerhajo01   1881     1    DTN   NL  80 297  35  72  13   6  0  36  NA NA
    ## 1345 gillepe01   1881     1    TRN   NL  84 348  43  96  14   3  0  41  NA NA
    ## 1346 gilliba01   1881     1    PRO   NL  46 183  19  40   7   2  0  20  NA NA
    ## 1347 glassja01   1881     1    CL2   NL  85 335  49  86   9   5  0  33  NA NA
    ## 1348 goldsfr01   1881     1    CHN   NL  42 158  24  38   3   4  0  16  NA NA
    ## 1349  gorege01   1881     1    CHN   NL  73 309  86  92  18   9  1  44  NA NA
    ## 1350 grossem01   1881     1    PRO   NL  51 182  15  50   9   4  1  24  NA NA
    ## 1351 hankifr01   1881     1    TRN   NL  85 321  34  62  15   0  1  19  NA NA
    ## 1352 hanlone01   1881     1    DTN   NL  76 305  63  85  14   8  2  28  NA NA
    ## 1353 hinespa01   1881     1    PRO   NL  80 361  65 103  27   5  2  31  NA NA
    ## 1354 holbebi01   1881     1    TRN   NL  46 180  16  49   3   0  0  14  NA NA
    ## 1355 hornujo01   1881     1    BSN   NL  83 324  39  78  12   8  2  25  NA NA
    ## 1356 hotalpe01   1881     1    WOR   NL  77 317  51  98  15   3  1  35  NA NA
    ## 1357 houcksa01   1881     1    DTN   NL  75 308  43  86  16   6  1  36  NA NA
    ## 1358 irwinar01   1881     1    WOR   NL  50 206  27  55   8   2  0  24  NA NA
    ## 1359 keefeti01   1881     1    TRN   NL  46 152  18  35   7   1  0  19  NA NA
    ## 1360 kellyki01   1881     1    CHN   NL  82 353  84 114  27   3  2  55  NA NA
    ## 1361 kemmlru01   1881     1    CL2   NL   1   3   0   0   0   0  0   0  NA NA
    ## 1362 kennedo01   1881     1    CL2   NL  39 150  19  47   7   1  0  15  NA NA
    ## 1363 knighlo01   1881     1    DTN   NL  83 340  67  92  16   3  1  52  NA NA
    ## 1364 learyja01   1881     1    DTN   NL   3  11   2   3   1   1  0   4  NA NA
    ## 1365 lewisfr01   1881     1    BSN   NL  27 114  17  25   6   0  0   9  NA NA
    ## 1366 lynchja01   1881     1    BFN   NL  23  78   6  13   3   0  0   3  NA NA
    ## 1367 mannija01   1881     1    BFN   NL   1   1   0   0   0   0  0   0  NA NA
    ## 1368 mathebo01   1881     1    PRO   NL  16  57   6  11   1   0  0   4  NA NA
    ## 1369 mathebo01   1881     2    BSN   NL  19  71   2  12   2   0  0   4  NA NA
    ## 1370 mcclebi01   1881     1    PRO   NL  68 259  30  43   3   1  0  16  NA NA
    ## 1371 mccorha01   1881     1    WOR   NL  12  45   1   6   0   0  0   3  NA NA
    ## 1372 mccorji01   1881     1    CL2   NL  70 309  45  79   9   4  0  26  NA NA
    ## 1373 mcgeami01   1881     1    CL2   NL  11  41   1   9   0   0  0   5  NA NA
    ## 1374 morrijo01   1881     1    BSN   NL  81 311  47  90  19   3  1  39  NA NA
    ## 1375 morrijo02   1881     1    BFN   NL  12  47   3  10   2   0  0   3  NA NA
    ## 1376 mountfr01   1881     1    DTN   NL   7  25   0   4   1   1  0   4  NA NA
    ## 1377 moynami01   1881     1    CL2   NL  33 135  12  31   5   1  0   8  NA NA
    ## 1378 moynami01   1881     2    DTN   NL   1   4   1   1   0   0  0   0  NA NA
    ## 1379 mullato01   1881     1    DTN   NL   5  19   0   5   0   0  0   1  NA NA
    ## 1380 myershe01   1881     1    PRO   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1381 nelsoca01   1881     1    WOR   NL  24 103  13  29   1   0  1  15  NA NA
    ## 1382 nicolhu01   1881     1    CHN   NL  26 108  13  22   2   0  0   7  NA NA
    ## 1383 nolanth01   1881     1    CL2   NL  41 168  12  41   5   1  0  18  NA NA
    ## 1384 olearda01   1881     1    DTN   NL   2   8   0   0   0   0  0   0  NA NA
    ## 1385 orourji01   1881     1    BFN   NL  83 348  71 105  21   7  0  30  NA NA
    ## 1386 peterjo01   1881     1    BFN   NL  54 229  21  49   8   1  0  25  NA NA
    ## 1387 phillbi01   1881     1    CL2   NL  85 357  51  97  18  10  1  44  NA NA
    ## 1388 piercan01   1881     1    CHN   NL   2   8   1   2   0   0  0   0  NA NA
    ## 1389  pikeli01   1881     1    WOR   NL   5  18   1   2   0   0  0   0  NA NA
    ## 1390 powelma01   1881     1    DTN   NL  55 219  47  74   9   4  1  38  NA NA
    ## 1391 powerph01   1881     1    CL2   NL   5  15   1   1   0   0  0   0  NA NA
    ## 1392 purcebl01   1881     1    CL2   NL  20  80   3  14   2   1  0   4  NA NA
    ## 1393 purcebl01   1881     2    BFN   NL  30 113  15  33   7   2  0  17  NA NA
    ## 1394 questjo01   1881     1    CHN   NL  78 293  35  72   6   0  1  26  NA NA
    ## 1395 quinnjo01   1881     1    BSN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1396 quinnjo01   1881     2    WOR   NL   2   7   0   1   0   0  0   1  NA NA
    ## 1397 radboch01   1881     1    PRO   NL  72 270  27  59   9   0  0  28  NA NA
    ## 1398 reillch01   1881     1    DTN   NL  19  70   8  12   2   0  0   3  NA NA
    ## 1399 reillch01   1881     2    WOR   NL   2   8   2   3   0   0  0   1  NA NA
    ## 1400 remseja01   1881     1    CL2   NL  48 172  14  30   4   3  0  13  NA NA
    ## 1401 richaha01   1881     1    BFN   NL  83 344  62 100  18   9  2  53  NA NA
    ## 1402 richmjo01   1881     1    BSN   NL  27  98  13  27   2   2  1  12  NA NA
    ## 1403 richmle01   1881     1    WOR   NL  61 252  31  63   5   1  0  28  NA NA
    ## 1404  roweja01   1881     1    BFN   NL  64 246  30  82  11  11  1  43  NA NA
    ## 1405 shaffor01   1881     1    CL2   NL  85 343  48  88  13   6  1  34  NA NA
    ## 1406 smithpo01   1881     1    CL2   NL  10  34   1   4   0   0  0   3  NA NA
    ## 1407 smithpo01   1881     2    BFN   NL   3  11   3   0   0   0  0   1  NA NA
    ## 1408 smithpo01   1881     3    WOR   NL  11  41   1   3   0   0  0   2  NA NA
    ## 1409 snydepo01   1881     1    BSN   NL  62 219  14  50   8   0  0  16  NA NA
    ## 1410 startjo01   1881     1    PRO   NL  79 348  56 114  12   6  0  29  NA NA
    ## 1411 stearec01   1881     1    DTN   NL   3  11   1   1   1   0  0   0  NA NA
    ## 1412 stoveha01   1881     1    WOR   NL  75 341  57  92  25   7  2  30  NA NA
    ## 1413 stratas01   1881     1    WOR   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1414 sullisl01   1881     1    BFN   NL  35 121  13  23   4   0  0  15  NA NA
    ## 1415 suttoez01   1881     1    BSN   NL  83 333  42  97  12   4  0  31  NA NA
    ## 1416 swarted01   1881     1    BFN   NL   1   3   0   1   0   0  0   0  NA NA
    ## 1417 taylobi01   1881     1    WOR   NL   6  28   3   3   1   0  0   2  NA NA
    ## 1418 taylobi01   1881     2    DTN   NL   1   4   0   2   2   0  0   1  NA NA
    ## 1419 taylobi01   1881     3    CL2   NL  24 103   6  25   1   0  0  12  NA NA
    ## 1420 trottsa01   1881     1    DTN   NL   6  25   3   5   2   1  0   2  NA NA
    ## 1421  troyda01   1881     1    DTN   NL  11  44   2  15   3   0  0   4  NA NA
    ## 1422  wardjo01   1881     1    PRO   NL  85 357  56  87  18   6  0  53  NA NA
    ## 1423 welchmi01   1881     1    TRN   NL  40 148  12  30  10   0  0  11  NA NA
    ## 1424 whitede01   1881     1    BFN   NL  78 319  58  99  24   4  0  53  NA NA
    ## 1425 whitewi01   1881     1    DTN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 1426 whitnar01   1881     1    DTN   NL  58 214  23  39   7   5  0   9  NA NA
    ## 1427 whitnji01   1881     1    BSN   NL  75 282  37  72  17   3  0  32  NA NA
    ## 1428 wiedmst01   1881     1    DTN   NL  13  47   9  12   1   0  0   5  NA NA
    ## 1429 willine01   1881     1    CHN   NL  82 343  56  92  12   6  1  48  NA NA
    ## 1430  wisesa01   1881     1    DTN   NL   1   4   0   2   0   0  0   0  NA NA
    ## 1431  woodge01   1881     1    DTN   NL  80 337  54 100  18   9  2  32  NA NA
    ## 1432 wrighge01   1881     1    BSN   NL   7  25   4   5   0   0  0   0  NA NA
    ## 1433 wrighsa01   1881     1    BSN   NL   1   4   0   1   0   0  0   0  NA NA
    ## 1434  yorkto01   1881     1    PRO   NL  85 316  57  96  23   5  2  47  NA NA
    ## 1435 ansonca01   1882     1    CHN   NL  82 348  69 126  29   8  1  83  NA NA
    ## 1436 arundha01   1882     1    PT1   AA  14  52   6  10   0   0  0  NA  NA NA
    ## 1437 arundtu01   1882     1    PH4   AA   1   5   0   0   0   0  0  NA  NA NA
    ## 1438 battijo01   1882     1    PT1   AA  34 133  13  28   5   1  1  NA  NA NA
    ## 1439 bennech01   1882     1    DTN   NL  84 342  43 103  16  10  5  51  NA NA
    ## 1440 birchju01   1882     1    PH4   AA  75 338  65  89  12   1  0  27  NA NA
    ## 1441 blakibo01   1882     1    PH4   AA  72 281  40  64   4   1  0  20  NA NA
    ## 1442  bohnch01   1882     1    LS2   AA   4  13   0   2   0   0  0  NA  NA NA
    ## 1443  bondto01   1882     1    WOR   NL   8  30   1   4   0   0  0   2  NA NA
    ## 1444 bootham01   1882     1    BL2   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 1445 bootham01   1882     2    LS2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1446 bradlge01   1882     1    CL2   NL  30 115  16  21   5   0  0   6  NA NA
    ## 1447 briodfa01   1882     1    CL2   NL  53 194  30  50  13   0  0  13  NA NA
    ## 1448 broutda01   1882     1    BFN   NL  84 351  71 129  23  11  6  63  NA NA
    ## 1449 browned01   1882     1    SL4   AA  17  60   4  11   0   0  0  NA  NA NA
    ## 1450 brownpe01   1882     1    LS2   AA  69 288  67 109  17   3  5  NA  NA NA
    ## 1451 brownto01   1882     1    BL2   AA  45 180  28  52   4   2  1  23  NA NA
    ## 1452 buffich01   1882     1    BSN   NL  15  50   5  13   1   0  0   4  NA NA
    ## 1453 burdoja01   1882     1    BSN   NL  83 319  36  76   6   7  0  27  NA NA
    ## 1454 burkeja01   1882     1    BFN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1455 burnsto01   1882     1    CHN   NL  84 355  55  88  23   6  0  48  NA NA
    ## 1456  burtfr01   1882     1    BL2   AA  10  36   2   4   2   1  0  NA  NA NA
    ## 1457 bushodo01   1882     1    WOR   NL  69 253  20  40   4   1  1  15  NA NA
    ## 1458 carpehi01   1882     1    CN2   AA  80 351  78 120  15   5  1  67  NA NA
    ## 1459 carrocl01   1882     1    PRO   NL  10  41   4   5   0   0  0   2  NA NA
    ## 1460 caseybo01   1882     1    DTN   NL   9  39   5   9   2   1  1   7  NA NA
    ## 1461 cassijo01   1882     1    TRN   NL  29 121  14  21   3   1  0   9  NA NA
    ## 1462 clarkjo01   1882     1    WOR   NL   3  11   0   4   2   0  0   2  NA NA
    ## 1463 clinemo01   1882     1    BL2   AA  44 172  18  38   6   2  0  NA  NA NA
    ## 1464 clintji01   1882     1    WOR   NL  26  98   9  16   2   0  0   3  NA NA
    ## 1465 cogswed01   1882     1    WOR   NL  13  51  10   7   1   0  0   1  NA NA
    ## 1466 comisch01   1882     1    SL4   AA  78 329  58  80   9   5  1  45  NA NA
    ## 1467 connoro01   1882     1    TRN   NL  81 349  65 115  22  18  4  42  NA NA
    ## 1468 corcola01   1882     1    CHN   NL  40 169  23  35  10   2  1  24  NA NA
    ## 1469 coreyfr01   1882     1    WOR   NL  64 255  33  63   7  12  0  29  NA NA
    ## 1470 creamge01   1882     1    WOR   NL  81 286  27  65  16   6  1  29  NA NA
    ## 1471 critcmo01   1882     1    PT1   AA   1   5   0   0   0   0  0  NA  NA NA
    ## 1472 critcmo01   1882     2    SL4   AA   4  14   0   3   0   0  0  NA  NA NA
    ## 1473 crottjo01   1882     1    LS2   AA   5  20   1   2   0   0  0  NA  NA NA
    ## 1474 crottjo01   1882     2    SL4   AA   8  28   2   4   1   0  0  NA  NA NA
    ## 1475 cuthbne01   1882     1    SL4   AA  60 233  28  52  16   5  0  NA  NA NA
    ## 1476 dailyhu01   1882     1    BFN   NL  29 110  10  18   6   1  0   9  NA NA
    ## 1477 dalryab01   1882     1    CHN   NL  84 397  96 117  25  11  1  36  NA NA
    ## 1478 deaslpa01   1882     1    BSN   NL  67 264  36  70   8   0  0  29  NA NA
    ## 1479 deckefr01   1882     1    SL4   AA   2   8   0   2   0   0  0   1  NA NA
    ## 1480 dennyje01   1882     1    PRO   NL  84 329  54  81  10   9  2  42  NA NA
    ## 1481 derbyge01   1882     1    DTN   NL  40 149  13  29   2   1  0   8  NA NA
    ## 1482 dolanto01   1882     1    BFN   NL  22  89  12  14   0   1  0   8  NA NA
    ## 1483 dorgaje01   1882     1    PH4   AA  44 181  25  51   9   1  0  24  NA NA
    ## 1484  dorrbe01   1882     1    SL4   AA   8  26   2   4   0   0  0  NA  NA NA
    ## 1485 doschhe01   1882     1    CL2   NL  25 104   7  25   2   0  0  10  NA NA
    ## 1486 doylejo02   1882     1    SL4   AA   3  11   0   2   0   0  0  NA  NA NA
    ## 1487 driscde01   1882     1    PT1   AA  23  80  12  11   2   0  1  NA  NA NA
    ## 1488 dunlafr01   1882     1    CL2   NL  84 364  68 102  19   4  0  28  NA NA
    ## 1489 dwyerjo01   1882     1    CL2   NL   1   3   0   0   0   0  0   1  NA NA
    ## 1490 dylerjo01   1882     1    LS2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1491  eastha01   1882     1    BL2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1492  eganji01   1882     1    TRN   NL  30 115  15  23   3   2  0  10  NA NA
    ## 1493 esterdu01   1882     1    CL2   NL  45 179  13  44   4   3  0  19  NA NA
    ## 1494 evansja01   1882     1    WOR   NL  80 334  33  71  10   4  0  25  NA NA
    ## 1495 eversto01   1882     1    BL2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1496 ewingbu01   1882     1    TRN   NL  74 328  67  89  16  11  2  29  NA NA
    ## 1497 farrebi01   1882     1    PH4   AA   2   7   2   2   1   0  0   1  NA NA
    ## 1498 farreja02   1882     1    PRO   NL  84 366  67  93  21   6  2  31  NA NA
    ## 1499 farrejo01   1882     1    DTN   NL  69 283  34  70  12   2  1  24  NA NA
    ## 1500 fergubo01   1882     1    TRN   NL  81 319  44  82  15   2  0  32  NA NA
    ## 1501 flintsi01   1882     1    CHN   NL  81 331  48  83  18   8  4  44  NA NA
    ## 1502 foleycu01   1882     1    BFN   NL  84 341  51 104  16   4  3  49  NA NA
    ## 1503 forceda01   1882     1    BFN   NL  73 278  39  67  10   1  1  28  NA NA
    ## 1504 forstto01   1882     1    DTN   NL  21  76   5   7   0   0  0   2  NA NA
    ## 1505 fulmech01   1882     1    CN2   AA  79 324  54  91  13   4  0  27  NA NA
    ## 1506 fusseed01   1882     1    SL4   AA  35 136  13  31   2   0  0  NA  NA NA
    ## 1507 galvipu01   1882     1    BFN   NL  54 206  21  44   7   4  0  17  NA NA
    ## 1508  geisbi01   1882     1    BL2   AA  13  41   2   6   0   1  0   2  NA NA
    ## 1509 gillepe01   1882     1    TRN   NL  74 298  46  82   5   4  2  33  NA NA
    ## 1510 gilliba01   1882     1    PRO   NL  56 201  32  45   7   6  0  26  NA NA
    ## 1511 glassja01   1882     1    CL2   NL  84 358  66 104  27   9  4  46  NA NA
    ## 1512 gleasbi01   1882     1    SL4   AA  79 347  63 100  11   6  1  NA  NA NA
    ## 1513 gleasja01   1882     1    SL4   AA  78 331  53  84  10   1  2  NA  NA NA
    ## 1514 goldsfr01   1882     1    CHN   NL  46 183  23  42  11   1  0  19  NA NA
    ## 1515 goodmja01   1882     1    PT1   AA  10  41   5  13   2   2  0  NA  NA NA
    ## 1516  gorege01   1882     1    CHN   NL  84 367  99 117  15   7  3  51  NA NA
    ## 1517 greenbi01   1882     1    PH4   AA   7  30   8   9   1   0  0   1  NA NA
    ## 1518 halbred01   1882     1    PH4   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1519 halpiji01   1882     1    WOR   NL   2   8   0   0   0   0  0   0  NA NA
    ## 1520 hanlone01   1882     1    DTN   NL  82 347  68  80  18   6  5  38  NA NA
    ## 1521 harbibi01   1882     1    TRN   NL  32 123  11  23   1   1  0  13  NA NA
    ## 1522 hayesja01   1882     1    WOR   NL  78 326  27  88  22   4  4  54  NA NA
    ## 1523 heckegu01   1882     1    LS2   AA  78 340  62  94  14   4  3  NA  NA NA
    ## 1524 hinespa01   1882     1    PRO   NL  84 379  73 117  28  10  4  34  NA NA
    ## 1525 hoganed01   1882     1    SL4   AA   1   3   1   1   0   0  0  NA  NA NA
    ## 1526 holbebi01   1882     1    TRN   NL  71 251  24  46   5   0  0  23  NA NA
    ## 1527 holdsji01   1882     1    TRN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 1528 hornujo01   1882     1    BSN   NL  85 388  67 117  14  11  1  50  NA NA
    ## 1529 hotalpe01   1882     1    BSN   NL  84 378  64  98  16   5  0  28  NA NA
    ## 1530 housech02   1882     1    BL2   AA  74 306  40  79  10   7  1  NA  NA NA
    ## 1531 irwinar01   1882     1    WOR   NL  84 333  30  73  12   4  0  30  NA NA
    ## 1532 irwinjo01   1882     1    WOR   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1533 jacobha01   1882     1    BL2   AA  31 121  19  24   1   1  1  NA  NA NA
    ## 1534 jonesda06   1882     1    BL2   AA   4  15   1   1   0   0  0  NA  NA NA
    ## 1535 kearnto01   1882     1    DTN   NL   4  13   2   4   2   0  0   1  NA NA
    ## 1536 keefeti01   1882     1    TRN   NL  53 189  24  43   8   7  1  19  NA NA
    ## 1537 keenaji01   1882     1    PT1   AA  24  91   9  19   6   0  1  NA  NA NA
    ## 1538 kellyjo01   1882     1    CL2   NL  30 104   6  14   2   0  0   5  NA NA
    ## 1539 kellyki01   1882     1    CHN   NL  84 377  81 115  37   4  1  55  NA NA
    ## 1540 kemmlru01   1882     1    CN2   AA   3  11   0   1   1   0  0  NA  NA NA
    ## 1541 kemmlru01   1882     2    PT1   AA  24  97   8  23   4   0  0  NA  NA NA
    ## 1542 kennedo01   1882     1    CL2   NL   1   3   0   1   0   0  0   0  NA NA
    ## 1543 kienzbi01   1882     1    PH4   AA   9  33   8  11   3   2  0   9  NA NA
    ## 1544 kinziwa01   1882     1    DTN   NL  13  53   5   5   0   1  0   2  NA NA
    ## 1545 knighlo01   1882     1    DTN   NL  86 347  39  72  12   6  0  24  NA NA
    ## 1546 landido01   1882     1    PH4   AA   3  12   1   2   0   0  0  NA  NA NA
    ## 1547 landido01   1882     2    BL2   AA  50 175  10  30   1   0  0  NA  NA NA
    ## 1548  lanech01   1882     1    PT1   AA  57 211  26  37   7   2  3  NA  NA NA
    ## 1549 lathaju01   1882     1    PH4   AA  74 323  47  92  10   2  0  38  NA NA
    ## 1550 learyja01   1882     1    PT1   AA  60 255  31  73   7   3  1  NA  NA NA
    ## 1551 learyja01   1882     2    BL2   AA   4  18   3   4   1   0  0  NA  NA NA
    ## 1552  luffhe01   1882     1    DTN   NL   3  11   1   3   2   0  0   1  NA NA
    ## 1553  luffhe01   1882     2    CN2   AA  28 120  16  28   2   2  0   6  NA NA
    ## 1554  mackde01   1882     1    LS2   AA  72 264  41  48   3   1  0  NA  NA NA
    ## 1555 maculji01   1882     1    CN2   AA  79 299  44  70   6   6  0  22  NA NA
    ## 1556  mannfr01   1882     1    WOR   NL  19  77  12  18   5   0  0   7  NA NA
    ## 1557  mannfr01   1882     2    PH4   AA  29 121  13  28   7   4  0  NA  NA NA
    ## 1558 manniti01   1882     1    PRO   NL  21  76   7   8   0   0  0   8  NA NA
    ## 1559 mansejo01   1882     1    PH4   AA  31 126  17  30   3   1  0  17  NA NA
    ## 1560 mansemi01   1882     1    PT1   AA  79 346  59  95  16  16  2  NA  NA NA
    ## 1561 maskrha01   1882     1    LS2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1562 maskrle01   1882     1    LS2   AA  76 288  30  65  14   2  0  NA  NA NA
    ## 1563 mathebo01   1882     1    BSN   NL  45 169  17  38   6   0  0  13  NA NA
    ## 1564 mccafha01   1882     1    SL4   AA  38 153  23  42   8   6  0  NA  NA NA
    ## 1565 mccafha01   1882     2    LS2   AA   1   4   1   1   0   0  0  NA  NA NA
    ## 1566 mccluha01   1882     1    BSN   NL   2   6   1   2   0   0  0   0  NA NA
    ## 1567 mccorha01   1882     1    CN2   AA  26  93   3  12   0   1  0   3  NA NA
    ## 1568 mccorji01   1882     1    CL2   NL  70 262  35  57   7   3  2  15  NA NA
    ## 1569 mcgeami01   1882     1    DTN   NL  34 133  14  19   4   1  0   2  NA NA
    ## 1570 mcginju01   1882     1    SL4   AA  51 203  17  44   6   4  0  NA  NA NA
    ## 1571 mcgunbi01   1882     1    CL2   NL   1   5   2   1   0   0  0   0  NA NA
    ## 1572 mckelru01   1882     1    PT1   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1573 mclaufr01   1882     1    WOR   NL  15  55   7  12   0   2  1   4  NA NA
    ## 1574 mcphebi01   1882     1    CN2   AA  78 311  43  71   8   7  1  31  NA NA
    ## 1575 merried01   1882     1    LS2   AA   1   0   0   0   0   0  0  NA  NA NA
    ## 1576 merried01   1882     2    WOR   NL   2   8   0   1   0   0  0   0  NA NA
    ## 1577 mitchbo01   1882     1    SL4   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1578 morgabi02   1882     1    PT1   AA  17  66  10  17   2   1  0  NA  NA NA
    ## 1579 morrijo01   1882     1    BSN   NL  83 349  73 101  19  11  2  54  NA NA
    ## 1580 morrito01   1882     1    DTN   NL   2   7   1   2   0   0  0   0  NA NA
    ## 1581 mortoch01   1882     1    PT1   AA  24  98  12  29   0   3  0  NA  NA NA
    ## 1582 mortoch01   1882     2    SL4   AA   9  32   2   2   0   1  0  NA  NA NA
    ## 1583 mountfr01   1882     1    WOR   NL   5  16   1   1   0   0  0   1  NA NA
    ## 1584 mountfr01   1882     2    PH4   AA   9  36   5  12   3   0  0  NA  NA NA
    ## 1585 mountfr01   1882     3    WOR   NL  20  70   8  19   2   2  2   5  NA NA
    ## 1586 muldomi01   1882     1    CL2   NL  84 341  50  84  17   5  6  45  NA NA
    ## 1587 mullato01   1882     1    LS2   AA  77 303  46  78  13   1  0  NA  NA NA
    ## 1588 myershe01   1882     1    BL2   AA  69 294  41  53   3   0  0  NA  NA NA
    ## 1589  navasa01   1882     1    PRO   NL  28  97  15  20   2   0  0   7  NA NA
    ## 1590 nichotr01   1882     1    BL2   AA  26  95   4  15   1   0  0  NA  NA NA
    ## 1591 nicolhu01   1882     1    CHN   NL  47 186  19  37   9   1  1  16  NA NA
    ## 1592 obrieja01   1882     1    PH4   AA  62 241  44  73  13   3  3  37  NA NA
    ## 1593 obrieto01   1882     1    WOR   NL  22  89   9  18   1   1  0   7  NA NA
    ## 1594 olearda01   1882     1    WOR   NL   6  22   2   4   1   0  0   2  NA NA
    ## 1595 orourji01   1882     1    BFN   NL  84 370  62 104  15   6  2  37  NA NA
    ## 1596 peterjo01   1882     1    PT1   AA  78 331  47  96  10   1  0  NA  NA NA
    ## 1597 pfefffr01   1882     1    TRN   NL  85 330  26  72   7   4  1  43  NA NA
    ## 1598 phillbi01   1882     1    CL2   NL  78 335  40  87  17   7  4  47  NA NA
    ## 1599 piercgr01   1882     1    LS2   AA   9  33   3  10   1   0  0  NA  NA NA
    ## 1600 piercgr01   1882     2    BL2   AA  41 151  10  32   2   1  0  NA  NA NA
    ## 1601 powelma01   1882     1    DTN   NL  80 338  44  81  13   0  0  29  NA NA
    ## 1602 powerph01   1882     1    CN2   AA  16  60   4  13   1   1  0   5  NA NA
    ## 1603 purcebl01   1882     1    BFN   NL  84 380  79 105  18   6  2  40  NA NA
    ## 1604 questjo01   1882     1    CHN   NL  42 159  24  32   5   2  0  15  NA NA
    ## 1605 radboch01   1882     1    PRO   NL  83 326  30  78  11   0  1  32  NA NA
    ## 1606 reccijo01   1882     1    LS2   AA  74 266  46  63  12   3  1  NA  NA NA
    ## 1607 recciph01   1882     1    LS2   AA   4  15   0   2   0   0  0  NA  NA NA
    ## 1608 reillch01   1882     1    PRO   NL   3  11   0   2   0   0  0   2  NA NA
    ## 1609 reynoch01   1882     1    PH4   AA   2   8   1   1   0   0  0  NA  NA NA
    ## 1610 richaha01   1882     1    BFN   NL  83 354  61  96  20   8  2  57  NA NA
    ## 1611 richmjo01   1882     1    CL2   NL  41 140  12  24   6   2  0  11  NA NA
    ## 1612 richmjo01   1882     2    PH4   AA  18  65   8  12   2   2  0   4  NA NA
    ## 1613 richmle01   1882     1    WOR   NL  55 228  50  64   8   9  2  28  NA NA
    ## 1614 robinya01   1882     1    DTN   NL  11  39   1   7   1   0  0   2  NA NA
    ## 1615 rosemch01   1882     1    TRN   NL  82 331  41  78  21   6  1  29  NA NA
    ## 1616  roweda01   1882     1    CL2   NL  24  97  13  25   4   3  1  17  NA NA
    ## 1617  roweja01   1882     1    BFN   NL  75 308  43  82  14   5  1  42  NA NA
    ## 1618 rowened01   1882     1    BSN   NL  83 327  36  81   7   4  1  43  NA NA
    ## 1619  russjo01   1882     1    BL2   AA   1   3   0   1   0   0  0  NA  NA NA
    ## 1620 salisha01   1882     1    PT1   AA  39 145  17  22   2   0  0  NA  NA NA
    ## 1621   sayji01   1882     1    PH4   AA  12  48   8   9   1   0  0  NA  NA NA
    ## 1622   sayji01   1882     2    LS2   AA   1   4   1   1   0   0  0  NA  NA NA
    ## 1623   sayji01   1882     3    PH4   AA  10  34   4   8   1   0  1  NA  NA NA
    ## 1624   saylo01   1882     1    PH4   AA  49 199  35  45   4   3  1  28  NA NA
    ## 1625 schapjo01   1882     1    SL4   AA  15  50   7   9   1   0  0  NA  NA NA
    ## 1626 scharni01   1882     1    BL2   AA  10  39   4   8   1   1  1  NA  NA NA
    ## 1627 schenbi01   1882     1    LS2   AA  60 231  37  60  11   3  0  NA  NA NA
    ## 1628 scottmi01   1882     1    CHN   NL   1   5   1   2   0   0  0   0  NA NA
    ## 1629 sewarge01   1882     1    SL4   AA  38 144  23  31   1   1  0  NA  NA NA
    ## 1630 seymoja01   1882     1    PT1   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1631 shaffor01   1882     1    CL2   NL  84 313  37  67  14   2  3  28  NA NA
    ## 1632 shetzjo01   1882     1    BL2   AA  73 281  22  60   8   2  0  NA  NA NA
    ## 1633 shoupjo01   1882     1    SL4   AA   2   7   1   0   0   0  0  NA  NA NA
    ## 1634 smilebi01   1882     1    SL4   AA  59 240  30  51   4   2  0  NA  NA NA
    ## 1635 smilebi01   1882     2    BL2   AA  16  61   3   9   0   0  0  NA  NA NA
    ## 1636 smithjo02   1882     1    TRN   NL  35 149  27  36   4   3  0  14  NA NA
    ## 1637 smithjo02   1882     2    WOR   NL  19  70  10  17   3   2  0   5  NA NA
    ## 1638  smithl01   1882     1    BL2   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 1639 smithpo01   1882     1    PH4   AA  20  65  10   6   0   0  0   2  NA NA
    ## 1640 smithpo01   1882     2    LS2   AA   3  11   1   2   0   0  0  NA  NA NA
    ## 1641 snydege01   1882     1    PH4   AA   1   3   2   1   0   0  0  NA  NA NA
    ## 1642 snydepo01   1882     1    CN2   AA  72 309  49  90  12   2  1  50  NA NA
    ## 1643 sommejo01   1882     1    CN2   AA  80 354  82 102  12   6  1  29  NA NA
    ## 1644 startjo01   1882     1    PRO   NL  82 356  58 117   8  10  0  48  NA NA
    ## 1645 stearec01   1882     1    CN2   AA  49 214  28  55  10   2  0  35  NA NA
    ## 1646 stoveha01   1882     1    WOR   NL  84 360  90 104  13  10  5  26  NA NA
    ## 1647 straujo01   1882     1    PH4   AA   8  32   2   6   2   0  0   1  NA NA
    ## 1648 striccu01   1882     1    PH4   AA  72 272  34  59   6   1  0  18  NA NA
    ## 1649 stricjo01   1882     1    LS2   AA  32 110  17  18   6   1  0  NA  NA NA
    ## 1650 striege01   1882     1    PT1   AA  79 296  44  59   9   6  2  NA  NA NA
    ## 1651 sullida01   1882     1    LS2   AA  67 286  44  78   8   2  0  NA  NA NA
    ## 1652 sullisl01   1882     1    SL4   AA  51 188  24  34   3   3  0  NA  NA NA
    ## 1653 suttoez01   1882     1    BSN   NL  81 319  44  80   8   1  2  38  NA NA
    ## 1654 swarted01   1882     1    PT1   AA  77 329  87 109  18  11  4  NA  NA NA
    ## 1655 sweenbi01   1882     1    PH4   AA  23  88   8  14   4   0  0   6  NA NA
    ## 1656 sweench01   1882     1    PRO   NL   1   4   0   0   0   0  0   0  NA NA
    ## 1657 taylobi01   1882     1    PT1   AA  71 302  40  84  16  13  3  NA  NA NA
    ## 1658 thomptu01   1882     1    CN2   AA   1   5   0   1   0   0  0  NA  NA NA
    ## 1659 tiernbi01   1882     1    CN2   AA   1   5   1   0   0   0  0  NA  NA NA
    ## 1660 tillejo01   1882     1    CL2   NL  15  56   2   5   1   1  0   4  NA NA
    ## 1661 trottsa01   1882     1    DTN   NL  32 129  11  31   7   1  0  12  NA NA
    ## 1662  troyda01   1882     1    DTN   NL  40 152  22  37   7   2  0  14  NA NA
    ## 1663  troyda01   1882     2    PRO   NL   4  17   1   4   0   0  0   1  NA NA
    ## 1664 waittch01   1882     1    BL2   AA  72 249  20  39   4   0  0  NA  NA NA
    ## 1665 walkeos01   1882     1    SL4   AA  76 318  48  76  15   7  7  NA  NA NA
    ## 1666  wardjo01   1882     1    PRO   NL  83 355  58  87  10   3  1  39  NA NA
    ## 1667 weavesa01   1882     1    PH4   AA  43 155  19  36   3   0  0   8  NA NA
    ## 1668 welchmi01   1882     1    TRN   NL  38 151  26  37   6   0  1  17  NA NA
    ## 1669 wheelha01   1882     1    CN2   AA  76 344  59  86  11  11  1  29  NA NA
    ## 1670 whitede01   1882     1    BFN   NL  83 337  51  95  17   0  1  33  NA NA
    ## 1671 whitewi01   1882     1    CN2   AA  54 207  28  55   4   0  0  25  NA NA
    ## 1672 whitied01   1882     1    BL2   AA  74 308  43  80  13   5  0  NA  NA NA
    ## 1673 whitnar01   1882     1    PRO   NL  11  40   2   3   0   0  0   1  NA NA
    ## 1674 whitnar01   1882     2    DTN   NL  31 115  10  21   0   0  0   4  NA NA
    ## 1675 whitnji01   1882     1    BSN   NL  61 251  49  81  18   7  5  48  NA NA
    ## 1676 wiedmst01   1882     1    DTN   NL  50 193  20  42   7   1  0  20  NA NA
    ## 1677 williju01   1882     1    DTN   NL   1   3   0   1   0   0  0   0  NA NA
    ## 1678 williju01   1882     2    CL2   NL   9  36   5   5   1   1  0   2  NA NA
    ## 1679 willine01   1882     1    CHN   NL  83 348  66  98  27   4  3  60  NA NA
    ## 1680  wisebi01   1882     1    BL2   AA   5  20   2   2   1   0  0   1  NA NA
    ## 1681  wisesa01   1882     1    BSN   NL  78 298  44  66  11   4  4  34  NA NA
    ## 1682  wolfji01   1882     1    LS2   AA  78 318  46  95  11   8  0  NA  NA NA
    ## 1683  woodge01   1882     1    DTN   NL  84 375  69 101  12  12  7  29  NA NA
    ## 1684 wrighge01   1882     1    PRO   NL  46 185  14  30   1   2  0   9  NA NA
    ## 1685 wyliere01   1882     1    PT1   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 1686  yorkto01   1882     1    PRO   NL  81 321  48  86  23   7  1  40  NA NA
    ## 1687 allenmy01   1883     1    NY1   NL   1   4   0   0   0   0  0   1  NA NA
    ## 1688 allisdo01   1883     1    BL2   AA   1   3   2   2   0   0  0  NA  NA NA
    ## 1689 ansonca01   1883     1    CHN   NL  98 413  70 127  36   5  0  68  NA NA
    ## 1690 bakelje01   1883     1    PH4   AA   8  26   4   5   1   0  0   2  NA NA
    ## 1691 bakerge01   1883     1    BL2   AA   7  22   0   5   0   0  0  NA  NA NA
    ## 1692 bakerno01   1883     1    PT1   AA   4  12   1   0   0   0  0   1  NA NA
    ## 1693 bakerph01   1883     1    BL2   AA  28 121  22  33   2   1  1  NA  NA NA
    ## 1694 barnibi01   1883     1    BL2   AA  17  55   7  11   0   0  0  NA  NA NA
    ## 1695  barrbo01   1883     1    PT1   AA  37 142  12  35   4   3  0  NA  NA NA
    ## 1696 battijo01   1883     1    PT1   AA  98 388  42  83   9   6  1  NA  NA NA
    ## 1697 benedar01   1883     1    PHI   NL   3  15   3   4   1   0  0   4  NA NA
    ## 1698 bennech01   1883     1    DTN   NL  92 371  56 113  34   7  5  55  NA NA
    ## 1699 birchju01   1883     1    PH4   AA  96 448  95 108  10   1  1  24  NA NA
    ## 1700 blakibo01   1883     1    PH4   AA  44 167  26  41   3   3  0  26  NA NA
    ## 1701 bloggwe01   1883     1    PT1   AA   9  34   0   5   0   0  0  NA  NA NA
    ## 1702 bradlge01   1883     1    CL2   NL   4  16   0   5   0   1  0   1  NA NA
    ## 1703 bradlge01   1883     2    PH4   AA  76 312  47  73   8   5  1  36  NA NA
    ## 1704 bradyst01   1883     1    NY4   AA  97 432  69 117  12   6  0  NA  NA NA
    ## 1705 breital01   1883     1    PHI   NL   1   2   0   0   0   0  0   0  NA NA
    ## 1706 briodfa01   1883     1    CL2   NL  40 145  23  34   5   1  0  10  NA NA
    ## 1707 brougca01   1883     1    CL2   NL   4  10   2   2   0   0  0   1  NA NA
    ## 1708 brougca01   1883     2    BL2   AA   9  32   1   6   0   0  0  NA  NA NA
    ## 1709 broutda01   1883     1    BFN   NL  98 425  85 159  41  17  3  97  NA NA
    ## 1710 brownle01   1883     1    BSN   NL  14  54   5  13   4   1  0   9  NA NA
    ## 1711 brownle01   1883     2    LS2   AA  14  60   6  11   2   1  0  NA  NA NA
    ## 1712 brownpe01   1883     1    LS2   AA  84 358  95 121  15   9  4  NA  NA NA
    ## 1713 brownto01   1883     1    CL5   AA  97 420  69 115  12   7  5  32  NA NA
    ## 1714 buffich01   1883     1    BSN   NL  86 341  28  81   8   3  1  26  NA NA
    ## 1715 burdoja01   1883     1    BSN   NL  96 400  80 132  27   8  5  88  NA NA
    ## 1716 burkeja01   1883     1    BFN   NL   1   5   0   1   0   0  0   1  NA NA
    ## 1717 burnsdi01   1883     1    DTN   NL  37 140  11  26   7   1  0   5  NA NA
    ## 1718 burnsto01   1883     1    CHN   NL  97 405  69 119  37   7  2  67  NA NA
    ## 1719 bushodo01   1883     1    CL2   NL  63 215  15  37   5   0  0   9  NA NA
    ## 1720  cadych01   1883     1    CL2   NL   3  11   0   0   0   0  0   0  NA NA
    ## 1721 carpehi01   1883     1    CN2   AA  95 435  99 130  18   4  3  40  NA NA
    ## 1722 carrocl01   1883     1    PRO   NL  58 238  37  63  12   3  1  20  NA NA
    ## 1723 caskied01   1883     1    NY1   NL  95 383  47  91  11   2  1  40  NA NA
    ## 1724 cassijo01   1883     1    PRO   NL  89 366  46  87  16   5  0  42  NA NA
    ## 1725 childsa01   1883     1    CL5   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1726 clappjo01   1883     1    NY1   NL  20  73   6  13   0   0  0   5  NA NA
    ## 1727 clintji01   1883     1    BL2   AA  94 399  69 125  16   8  0  NA  NA NA
    ## 1728 colemjo01   1883     1    PHI   NL  90 354  33  83  12   8  0  32  NA NA
    ## 1729 comisch01   1883     1    SL4   AA  96 401  87 118  17   9  2  64  NA NA
    ## 1730 connoro01   1883     1    NY1   NL  98 409  80 146  28  15  1  50  NA NA
    ## 1731 corcola01   1883     1    CHN   NL  68 263  40  55  12   7  0  25  NA NA
    ## 1732 coreyfr01   1883     1    PH4   AA  71 298  45  77  16   2  1  40  NA NA
    ## 1733 corkhpo01   1883     1    CN2   AA  88 375  53  81  10   8  2  46  NA NA
    ## 1734 cramedi01   1883     1    NY1   NL   2   6   0   0   0   0  0   0  NA NA
    ## 1735 cranesa01   1883     1    NY4   AA  96 349  57  82   8   5  0  NA  NA NA
    ## 1736 creamge01   1883     1    PT1   AA  91 369  54  94   7   9  0  NA  NA NA
    ## 1737 crowlbi01   1883     1    PH4   AA  23  96  16  24   4   3  0  16  NA NA
    ## 1738 crowlbi01   1883     2    CL2   NL  11  41   3  12   5   0  0   5  NA NA
    ## 1739 cushmed01   1883     1    BFN   NL   7  23   3   5   0   0  0   1  NA NA
    ## 1740 cuthbne01   1883     1    SL4   AA  21  71   3  12   1   0  0   3  NA NA
    ## 1741 dailyhu01   1883     1    CL2   NL  45 142  18  18   1   0  0   5  NA NA
    ## 1742 dalryab01   1883     1    CHN   NL  80 363  78 108  24   4  2  37  NA NA
    ## 1743 darlide01   1883     1    BFN   NL   6  18   1   3   0   0  0   1  NA NA
    ## 1744 deaglre01   1883     1    CN2   AA  19  70   9   9   2   0  0   5  NA NA
    ## 1745 deaslpa01   1883     1    SL4   AA  58 206  27  53   2   1  0  15  NA NA
    ## 1746 dennyje01   1883     1    PRO   NL  98 393  73 108  26   8  8  55  NA NA
    ## 1747 derbyge01   1883     1    BFN   NL  16  59  10  14   1   0  0   3  NA NA
    ## 1748 devinji01   1883     1    BL2   AA   2   9   4   2   0   0  0  NA  NA NA
    ## 1749 dickebu01   1883     1    PT1   AA  85 354  62  88  15   1  0  NA  NA NA
    ## 1750 dolanto01   1883     1    SL4   AA  81 295  32  63   9   2  1  18  NA NA
    ## 1751 dorgami01   1883     1    NY1   NL  64 261  32  61  11   3  0  27  NA NA
    ## 1752 doyleco01   1883     1    PHI   NL  16  68   3  15   3   2  0   3  NA NA
    ## 1753 driscde01   1883     1    PT1   AA  41 148  19  27   2   1  0  NA  NA NA
    ## 1754 dundoed01   1883     1    CL5   AA  26  93   8  15   1   0  0  NA  NA NA
    ## 1755 dunlafr01   1883     1    CL2   NL  93 396  81 129  34   2  4  37  NA NA
    ## 1756 eggleda01   1883     1    BL2   AA  53 202  15  38   2   0  0   7  NA NA
    ## 1757 eggleda01   1883     2    BFN   NL  38 153  13  38   2   1  0  13  NA NA
    ## 1758 emslibo01   1883     1    BL2   AA  27  97  14  16   1   2  0  NA  NA NA
    ## 1759 esterdu01   1883     1    NY4   AA  97 407  55 103   9   7  0  NA  NA NA
    ## 1760 evansja01   1883     1    CL2   NL  90 332  36  79  13   2  0  31  NA NA
    ## 1761 ewingbu01   1883     1    NY1   NL  88 376  90 114  11  13 10  41  NA NA
    ## 1762 ewingjo01   1883     1    SL4   AA   1   5   0   0   0   0  0  NA  NA NA
    ## 1763 farrasi01   1883     1    PHI   NL  99 377  41  88  19   8  0  29  NA NA
    ## 1764 farrebi01   1883     1    BL2   AA   2   7   0   0   0   0  0  NA  NA NA
    ## 1765 farreja02   1883     1    PRO   NL  95 420  92 128  24  11  3  61  NA NA
    ## 1766 farrejo01   1883     1    DTN   NL 101 444  58 108  13   5  0  36  NA NA
    ## 1767 fergubo01   1883     1    PHI   NL  86 329  39  85   9   2  0  27  NA NA
    ## 1768 fieldji01   1883     1    CL5   AA  75 291  31  75  10   6  1  NA  NA NA
    ## 1769 flintsi01   1883     1    CHN   NL  85 332  57  88  23   4  0  32  NA NA
    ## 1770 foleycu01   1883     1    BFN   NL  23 111  23  30   5   3  0   6  NA NA
    ## 1771 forceda01   1883     1    BFN   NL  96 378  40  82  11   3  0  35  NA NA
    ## 1772   foxjo01   1883     1    BL2   AA  23  92  12  14   3   0  0  NA  NA NA
    ## 1773 friespe01   1883     1    CL5   AA   3  10   1   3   1   0  0  NA  NA NA
    ## 1774 fulmech01   1883     1    CN2   AA  92 362  52  92  13   5  5  52  NA NA
    ## 1775 gallabi01   1883     1    BL2   AA  16  61   9  10   3   1  0  NA  NA NA
    ## 1776 gallabi01   1883     2    PHI   NL   2   8   1   0   0   0  0   0  NA NA
    ## 1777 galvipu01   1883     1    BFN   NL  80 322  41  71  11   2  1  19  NA NA
    ## 1778 gardngi01   1883     1    BL2   AA  42 161  28  44  10   3  1  NA  NA NA
    ## 1779 gerhajo01   1883     1    LS2   AA  78 319  56  84  11   9  0  NA  NA NA
    ## 1780 gillepe01   1883     1    NY1   NL  98 411  64 129  23  12  1  62  NA NA
    ## 1781 gilliba01   1883     1    PRO   NL  74 263  34  52  13   3  0  24  NA NA
    ## 1782 gladmbu01   1883     1    PHI   NL   1   4   1   0   0   0  0   0  NA NA
    ## 1783 glassja01   1883     1    CL2   NL  96 383  67 110  19   6  0  46  NA NA
    ## 1784 gleasbi01   1883     1    SL4   AA  98 425  81 122  21   9  2  42  NA NA
    ## 1785 gleasja01   1883     1    SL4   AA   9  34   2   8   0   0  0  NA  NA NA
    ## 1786 gleasja01   1883     2    LS2   AA  84 355  69 106  11   4  2  NA  NA NA
    ## 1787 goldsfr01   1883     1    CHN   NL  60 235  38  52  12   3  1  16  NA NA
    ## 1788  gorege01   1883     1    CHN   NL  92 392 105 131  30   9  2  52  NA NA
    ## 1789 gormaja01   1883     1    SL4   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1790 grossem01   1883     1    PHI   NL  57 231  39  71  25   7  1  25  NA NA
    ## 1791 guinebe01   1883     1    DTN   NL   1   5   1   1   0   0  0   0  NA NA
    ## 1792 hackeme01   1883     1    BSN   NL  46 179  20  42   8   6  2  24  NA NA
    ## 1793 haganar01   1883     1    PHI   NL  17  59   3   6   1   1  0   3  NA NA
    ## 1794 haganar01   1883     2    BFN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 1795 hankifr01   1883     1    NY1   NL  94 337  40  74  13   6  2  30  NA NA
    ## 1796 hanlone01   1883     1    DTN   NL 100 413  65 100  13   2  1  40  NA NA
    ## 1797 harbibi01   1883     1    PHI   NL  73 280  32  62  12   3  0  21  NA NA
    ## 1798 hayesja01   1883     1    PT1   AA  85 351  41  92  23   5  3  NA  NA NA
    ## 1799 heckegu01   1883     1    LS2   AA  81 332  59  90   6   6  1  NA  NA NA
    ## 1800 hendeha01   1883     1    PHI   NL   2   8   1   2   1   0  0   1  NA NA
    ## 1801 hendeha01   1883     2    BL2   AA  51 191  13  31   5   1  1  NA  NA NA
    ## 1802 hilsech01   1883     1    PHI   NL   3  10   0   1   0   0  0   1  NA NA
    ## 1803 hinesmi01   1883     1    BSN   NL  63 231  38  52  13   1  0  16  NA NA
    ## 1804 hinespa01   1883     1    PRO   NL  97 442  94 132  32   4  4  45  NA NA
    ## 1805 hodnech01   1883     1    SL4   AA   4  11   3   2   0   0  0  NA  NA NA
    ## 1806 holbebi01   1883     1    NY4   AA  73 299  26  71   9   1  0  NA  NA NA
    ## 1807 hornujo01   1883     1    BSN   NL  98 446 107 124  25  13  8  66  NA NA
    ## 1808 hotalpe01   1883     1    CL2   NL 100 417  54 108  20   8  0  30  NA NA
    ## 1809 houcksa01   1883     1    DTN   NL 101 416  52 105  18  12  0  40  NA NA
    ## 1810 hubbaal01   1883     1    PH4   AA   2   6   2   2   0   0  0   2  NA NA
    ## 1811 humphjo01   1883     1    NY1   NL  29 107   5  12   1   0  0   4  NA NA
    ## 1812 huntele01   1883     1    CL2   NL   1   4   1   1   0   0  0   0  NA NA
    ## 1813 ingrach01   1883     1    BL2   AA   1   4   0   1   0   0  0  NA  NA NA
    ## 1814 irwinar01   1883     1    PRO   NL  98 406  67 116  22   7  0  44  NA NA
    ## 1815 jonesch01   1883     1    CN2   AA  90 391  84 115  15  12 10  80  NA NA
    ## 1816 jonesja01   1883     1    LS2   AA   2   7   1   0   0   0  0  NA  NA NA
    ## 1817 jonesja02   1883     1    DTN   NL  12  42   3   8   1   0  0   3  NA NA
    ## 1818 jonesja02   1883     2    PH4   AA   7  25   3   6   1   0  0   1  NA NA
    ## 1819 keefeti01   1883     1    NY4   AA  70 259  39  57   6   9  0  NA  NA NA
    ## 1820 kellych01   1883     1    PHI   NL   2   7   1   1   0   1  0   0  NA NA
    ## 1821 kellyjo01   1883     1    BL2   AA  48 202  18  46   9   2  0  NA  NA NA
    ## 1822 kellyjo01   1883     2    PHI   NL   1   3   0   0   0   0  0   0  NA NA
    ## 1823 kellyki01   1883     1    CHN   NL  98 428  92 109  28  10  3  61  NA NA
    ## 1824 kemmlru01   1883     1    CL5   AA  84 318  27  66   6   2  0  NA  NA NA
    ## 1825 kennedo01   1883     1    BFN   NL   5  19   3   6   0   0  0   2  NA NA
    ## 1826 kenneed01   1883     1    NY4   AA  94 356  57  78   6   7  2  NA  NA NA
    ## 1827 knighlo01   1883     1    PH4   AA  97 429  98 108  23   9  1  53  NA NA
    ## 1828 kuehnbi01   1883     1    CL5   AA  95 374  38  85   8  14  1  NA  NA NA
    ## 1829 lathaar01   1883     1    SL4   AA  98 406  86  96  12   7  0  NA  NA NA
    ## 1830 lathaju01   1883     1    LS2   AA  88 368  60  92   7   6  0  NA  NA NA
    ## 1831 learyja01   1883     1    LS2   AA  40 165  16  31   1   3  3  NA  NA NA
    ## 1832 learyja01   1883     2    BL2   AA   3  11   1   2   0   2  0  NA  NA NA
    ## 1833 lewisfr01   1883     1    PHI   NL  38 160  21  40   7   0  0  18  NA NA
    ## 1834 lewisfr01   1883     2    SL4   AA  49 209  37  63   8   4  1  33  NA NA
    ## 1835 lilliji01   1883     1    BFN   NL  50 201  25  47   7   3  1  29  NA NA
    ## 1836 loftuto01   1883     1    SL4   AA   6  22   1   4   0   0  0  NA  NA NA
    ## 1837   lough01   1883     1    BL2   AA   1   5   0   2   0   0  0  NA  NA NA
    ## 1838  luffhe01   1883     1    LS2   AA   6  23   1   4   0   0  0   2  NA NA
    ## 1839 lynchja01   1883     1    NY4   AA  29 107   9  20   2   1  0  NA  NA NA
    ## 1840  mackde01   1883     1    PT1   AA  60 224  26  44   5   3  0  NA  NA NA
    ## 1841 maculji01   1883     1    CN2   AA  14  48   4   8   2   0  0   4  NA NA
    ## 1842  mannfr01   1883     1    CL5   AA  96 394  61  98  18  13  1  NA  NA NA
    ## 1843 mannija01   1883     1    PHI   NL  98 420  60 112  31   5  0  37  NA NA
    ## 1844 manniti01   1883     1    BL2   AA  35 121  23  26   5   0  0  NA  NA NA
    ## 1845 mansemi01   1883     1    PT1   AA  96 412  90 106  12  13  3  NA  NA NA
    ## 1846 manseto01   1883     1    DTN   NL  34 131  22  29   4   1  0  10  NA NA
    ## 1847 manseto01   1883     2    SL4   AA  28 112  23  45   8   1  0  24  NA NA
    ## 1848 maskrle01   1883     1    LS2   AA  96 361  50  73  13   8  1  NA  NA NA
    ## 1849 masonch01   1883     1    PH4   AA   1   2   0   1   0   0  0   1  NA NA
    ## 1850 mathebo01   1883     1    PH4   AA  45 167  15  31   2   0  0  11  NA NA
    ## 1851 mccafha01   1883     1    SL4   AA   5  18   0   1   0   0  0   1  NA NA
    ## 1852 mcclebi01   1883     1    PHI   NL  80 326  42  75  21   4  1  33  NA NA
    ## 1853 mccorha01   1883     1    CN2   AA  15  55   8  17   2   1  0  11  NA NA
    ## 1854 mccorje01   1883     1    BL2   AA  93 389  40 102  16   6  0  NA  NA NA
    ## 1855 mccorji01   1883     1    CL2   NL  43 157  21  37   2   2  0  13  NA NA
    ## 1856 mcginju01   1883     1    SL4   AA  45 180  20  36   4   2  0  14  NA NA
    ## 1857 mcintfr01   1883     1    DTN   NL   1   4   1   0   0   0  0   0  NA NA
    ## 1858 mcintfr01   1883     2    CL5   AA   2   7   0   0   0   0  0  NA  NA NA
    ## 1859 mclaufr01   1883     1    PT1   AA  29 114  15  25   2   0  1  NA  NA NA
    ## 1860 mclauto01   1883     1    LS2   AA  42 146  16  28   1   2  0  NA  NA NA
    ## 1861 mcphebi01   1883     1    CN2   AA  96 367  61  90  10  10  2  42  NA NA
    ## 1862 morgabi02   1883     1    PT1   AA  32 114  12  18   2   1  0  NA  NA NA
    ## 1863 morrijo01   1883     1    BSN   NL  97 404  83 129  33  16  6  68  NA NA
    ## 1864 mountbi01   1883     1    CN2   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 1865 mountfr01   1883     1    CL5   AA  70 276  36  60  14   5  3  NA  NA NA
    ## 1866 moynami01   1883     1    PH4   AA  95 400  90 124  18  10  1  67  NA NA
    ## 1867 muldomi01   1883     1    CL2   NL  98 378  54  86  22   3  0  29  NA NA
    ## 1868 mullato01   1883     1    SL4   AA  83 307  38  69  11   6  0  33  NA NA
    ## 1869 mulvejo01   1883     1    PRO   NL   4  16   1   2   1   0  0   2  NA NA
    ## 1870 mulvejo01   1883     2    PHI   NL   3  12   2   6   1   0  0   3  NA NA
    ## 1871  navasa01   1883     1    PRO   NL  29 100  18  24   4   2  0  16  NA NA
    ## 1872 neaglja01   1883     1    PHI   NL  18  73   6  12   1   0  0   4  NA NA
    ## 1873 neaglja01   1883     2    BL2   AA   9  35   3  10   4   0  0  NA  NA NA
    ## 1874 neaglja01   1883     3    PT1   AA  27 101  14  19   0   1  0  NA  NA NA
    ## 1875 nelsoca01   1883     1    NY4   AA  97 417  75 127  19   6  0  NA  NA NA
    ## 1876 nicolhu01   1883     1    SL4   AA  94 368  73 105  13   3  0  39  NA NA
    ## 1877 nolanth01   1883     1    PT1   AA   7  26   4   8   1   0  0  NA  NA NA
    ## 1878 oberbhe01   1883     1    PT1   AA   2   9   1   2   1   0  0  NA  NA NA
    ## 1879 oberbhe01   1883     2    SL4   AA   4  14   0   0   0   0  0  NA  NA NA
    ## 1880 obrieja01   1883     1    PH4   AA  94 390  74 113  14  10  0  70  NA NA
    ## 1881 obrieto01   1883     1    BL2   AA  33 138  16  37   6   4  0  NA  NA NA
    ## 1882 oldfida01   1883     1    BL2   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1883 oneilti01   1883     1    NY1   NL  23  76   8  15   3   0  0   5  NA NA
    ## 1884 orourji01   1883     1    BFN   NL  94 436 102 143  29   8  1  38  NA NA
    ## 1885 orourjo01   1883     1    NY4   AA  77 315  49  85  19   5  2  NA  NA NA
    ## 1886   orrda01   1883     1    NY4   AA   1   4   1   1   1   0  0  NA  NA NA
    ## 1887   orrda01   1883     2    NY1   NL   1   3   0   0   0   0  0   0  NA NA
    ## 1888   orrda01   1883     3    NY4   AA  12  46   5  15   3   3  2  11  NA NA
    ## 1889 peterjo01   1883     1    PT1   AA   8  28   3   3   0   0  0  NA  NA NA
    ## 1890 pfefffr01   1883     1    CHN   NL  96 371  41  87  22   7  1  45  NA NA
    ## 1891 phillbi01   1883     1    CL2   NL  97 382  42  94  29   8  2  40  NA NA
    ## 1892 piercgr01   1883     1    CL5   AA  11  41   5   7   0   0  0  NA  NA NA
    ## 1893 piercgr01   1883     2    NY1   NL  18  62   3   5   0   1  0   2  NA NA
    ## 1894 pirieji01   1883     1    PHI   NL   5  19   1   3   0   0  0   0  NA NA
    ## 1895 powelma01   1883     1    DTN   NL 101 421  76 115  17   5  1  48  NA NA
    ## 1896 powerph01   1883     1    CN2   AA  30 114  16  28   1   4  0   8  NA NA
    ## 1897 princwa01   1883     1    LS2   AA   4  11   1   2   0   0  0  NA  NA NA
    ## 1898 purcebl01   1883     1    PHI   NL  97 425  70 114  20   5  1  32  NA NA
    ## 1899 questjo01   1883     1    DTN   NL  37 137  22  32   8   2  0  15  NA NA
    ## 1900 questjo01   1883     2    SL4   AA  19  78  12  20   3   1  0  10  NA NA
    ## 1901 radboch01   1883     1    PRO   NL  89 381  59 108  11   3  3  48  NA NA
    ## 1902 radboge01   1883     1    DTN   NL   3  12   2   2   0   0  0   0  NA NA
    ## 1903 radfopa01   1883     1    BSN   NL  72 258  46  53   6   3  0  14  NA NA
    ## 1904 reccijo01   1883     1    LS2   AA  18  63  10   9   2   0  0   3  NA NA
    ## 1905 recciph01   1883     1    LS2   AA   1   3   1   1   1   0  0  NA  NA NA
    ## 1906  reidbi01   1883     1    BL2   AA  24  97  14  27   3   0  0  NA  NA NA
    ## 1907 reilljo01   1883     1    CN2   AA  98 437 103 136  21  14  9  79  NA NA
    ## 1908 reipsch01   1883     1    NY4   AA  37 145   8  27   4   2  0  NA  NA NA
    ## 1909 richaha01   1883     1    BFN   NL  92 399  73 124  34   7  1  56  NA NA
    ## 1910 richmjo01   1883     1    CL5   AA  92 385  63 109   7   8  0  NA  NA NA
    ## 1911 richmle01   1883     1    PRO   NL  49 194  41  55   8   6  1  19  NA NA
    ## 1912 ringofr01   1883     1    PHI   NL  60 221  24  42  10   1  0  12  NA NA
    ## 1913 rosemch01   1883     1    NY4   AA  93 398  48 100  13   6  0  NA  NA NA
    ## 1914  roweda01   1883     1    BL2   AA  59 256  40  80  11   6  0  NA  NA NA
    ## 1915  roweja01   1883     1    BFN   NL  87 374  65 104  18   7  1  38  NA NA
    ## 1916 rowened01   1883     1    PH4   AA  49 196  28  43  10   1  0  21  NA NA
    ## 1917 sawyewi01   1883     1    CL2   NL  17  47   3   1   0   0  0   0  NA NA
    ## 1918   saylo01   1883     1    BL2   AA  74 324  52  83  13   2  1  NA  NA NA
    ## 1919 scharni01   1883     1    BL2   AA   3  13   1   2   1   0  0  NA  NA NA
    ## 1920 schwabi01   1883     1    CL5   AA   2   4   0   1   0   0  0  NA  NA NA
    ## 1921 shaffor01   1883     1    BFN   NL  95 401  67 117  11   3  0  41  NA NA
    ## 1922  shawdu01   1883     1    DTN   NL  38 141  13  29   3   0  0   5  NA NA
    ## 1923 smithed01   1883     1    PRO   NL   2   9   2   2   1   0  0   1  NA NA
    ## 1924 smithed01   1883     2    PHI   NL   1   4   1   3   0   0  0   1  NA NA
    ## 1925 smithed02   1883     1    BSN   NL  30 115  10  25   5   3  0  16  NA NA
    ## 1926 smithpo01   1883     1    CL5   AA  97 405  82 106  14  17  4  NA  NA NA
    ## 1927 snydepo01   1883     1    CN2   AA  58 250  38  64  14   6  0  34  NA NA
    ## 1928 sommejo01   1883     1    CN2   AA  97 413  79 115   5   7  3  52  NA NA
    ## 1929 startjo01   1883     1    PRO   NL  87 370  63 105  16   7  1  57  NA NA
    ## 1930 stearec01   1883     1    BL2   AA  93 382  54  94  10   9  1  NA  NA NA
    ## 1931 stoveha01   1883     1    PH4   AA  94 421 110 128  31   6 14  66  NA NA
    ## 1932 straujo01   1883     1    CL5   AA  27 100   4  13   0   0  0  NA  NA NA
    ## 1933 striccu01   1883     1    PH4   AA  89 330  67  90   8   0  1  40  NA NA
    ## 1934 striege01   1883     1    SL4   AA  82 302  22  68   9   0  1  22  NA NA
    ## 1935  suckto01   1883     1    BFN   NL   2   7   1   0   0   0  0   0  NA NA
    ## 1936 sullida01   1883     1    LS2   AA  36 145   8  31   5   2  0  NA  NA NA
    ## 1937 sullisl01   1883     1    SL4   AA   8  27   2   6   0   1  0  NA  NA NA
    ## 1938 sullisl01   1883     2    LS2   AA   1   2   0   0   0   0  0  NA  NA NA
    ## 1939 sundabi01   1883     1    CHN   NL  14  54   6  13   4   0  0   5  NA NA
    ## 1940 suttoez01   1883     1    BSN   NL  94 414 101 134  28  15  3  73  NA NA
    ## 1941 swarted01   1883     1    PT1   AA  94 412  86 147  24   8  3  NA  NA NA
    ## 1942 sweench01   1883     1    PRO   NL  22  87   9  19   3   0  0  15  NA NA
    ## 1943 sweenro01   1883     1    BL2   AA  25 101  13  21   5   2  0  NA  NA NA
    ## 1944 taylobi01   1883     1    PT1   AA  83 369  43  96  13   7  2  NA  NA NA
    ## 1945 traffbi01   1883     1    CN2   AA  30 105  17  21   5   0  0   8  NA NA
    ## 1946 trottsa01   1883     1    DTN   NL  75 295  27  72  14   1  0  29  NA NA
    ## 1947  troyda01   1883     1    NY1   NL  85 316  37  68   7   5  0  20  NA NA
    ## 1948 valenjo01   1883     1    CL5   AA  16  60   9  17   4   0  0  NA  NA NA
    ## 1949 waittch01   1883     1    PHI   NL   1   3   0   1   0   0  0   0  NA NA
    ## 1950  wardjo01   1883     1    NY1   NL  88 380  76  97  18   7  7  54  NA NA
    ## 1951  wardpi01   1883     1    PHI   NL   1   5   0   0   0   0  0   0  NA NA
    ## 1952 warnefr01   1883     1    PHI   NL  39 141  13  32   6   1  0  13  NA NA
    ## 1953 weavesa01   1883     1    LS2   AA  53 193  19  37   6   1  0  NA  NA NA
    ## 1954 weihepo01   1883     1    CN2   AA   1   4   1   1   0   0  0  NA  NA NA
    ## 1955 welchmi01   1883     1    NY1   NL  84 320  42  75  13   5  2  30  NA NA
    ## 1956 wheelha01   1883     1    CL5   AA  82 371  42  84   6   7  0  NA  NA NA
    ## 1957 whitebi02   1883     1    PHI   NL   1   1   0   0   0   0  0   0  NA NA
    ## 1958 whitede01   1883     1    BFN   NL  94 391  62 114  14   5  0  47  NA NA
    ## 1959 whitewi01   1883     1    CN2   AA  65 240  38  54   4   3  0  23  NA NA
    ## 1960 whitied01   1883     1    LS2   AA  58 240  35  70  16   4  2  NA  NA NA
    ## 1961 whitnji01   1883     1    BSN   NL  96 409  78 115  27  10  5  57  NA NA
    ## 1962 wiedmst01   1883     1    DTN   NL  79 313  34  58   6   1  1  24  NA NA
    ## 1963 willine01   1883     1    CHN   NL  98 402  83 111  49   5  2  59  NA NA
    ## 1964 winklge01   1883     1    LS2   AA   4  13   2   0   0   0  0  NA  NA NA
    ## 1965  wisesa01   1883     1    BSN   NL  96 406  73 110  25   7  4  58  NA NA
    ## 1966  wolfji01   1883     1    LS2   AA  98 389  59 102  17   9  1  NA  NA NA
    ## 1967 wolstab01   1883     1    PHI   NL   3  11   0   1   1   0  0   0  NA NA
    ## 1968  woodge01   1883     1    DTN   NL  99 441  81 133  26  11  5  47  NA NA
    ## 1969  yorkto01   1883     1    CL2   NL 100 381  56  99  29   5  2  46  NA NA
    ## 1970   akejo01   1884     1    BL2   AA  13  52   1  10   0   1  0   2  NA NA
    ## 1971 albergu01   1884     1    PT1   AA   2   5   1   1   0   0  0  NA  NA NA
    ## 1972 albergu01   1884     2    WSU   UA   4  16   4   4   0   0  0  NA  NA NA
    ## 1973 alexani01   1884     1    KCU   UA  19  65   2   9   0   0  0  NA  NA NA
    ## 1974 alexani01   1884     2    SL4   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 1975 allenhe01   1884     1    PHI   NL   1   3   0   2   0   0  0   0  NA NA
    ## 1976 andreed01   1884     1    PHI   NL 109 420  74  93  21   2  0  23  NA NA
    ## 1977 andrewa01   1884     1    LS2   AA  14  49  10  10   5   1  0   8  NA NA
    ## 1978 andrufr01   1884     1    CHN   NL   1   5   3   1   0   0  0   0  NA NA
    ## 1979 annisbi01   1884     1    BSN   NL  27  96  17  17   2   0  0   3  NA NA
    ## 1980 ansonca01   1884     1    CHN   NL 112 475 108 159  30   3 21 102  NA NA
    ## 1981 ardnejo01   1884     1    CL2   NL  26  92   6  16   1   1  0   4  NA NA
    ## 1982 arundha01   1884     1    PRO   NL   1   3   2   1   0   0  0   1  NA NA
    ## 1983 arundtu01   1884     1    TL1   AA  15  47   6   4   0   0  0  NA  NA NA
    ## 1984 atkinal01   1884     1    PH4   AA  22  83  13  16   3   1  0  NA  NA NA
    ## 1985 atkinal01   1884     2    CHU   UA  19  68   4  14   0   0  0  NA  NA NA
    ## 1986 atkinal01   1884     3    BLU   UA   8  29   3   4   1   0  0  NA  NA NA
    ## 1987 aydelja01   1884     1    IN2   AA  12  44   1   5   1   0  0  NA  NA NA
    ## 1988 bahrefr01   1884     1    BLU   UA   2   8   0   0   0   0  0  NA  NA NA
    ## 1989 bakelje01   1884     1    PHU   UA  45 167  21  22   4   2  0  NA  NA NA
    ## 1990 bakelje01   1884     2    WIL   UA   2   5   0   0   0   0  0  NA  NA NA
    ## 1991 bakelje01   1884     3    KCU   UA   6  20   3   3   1   0  0  NA  NA NA
    ## 1992 bakerch01   1884     1    CHU   UA  15  57   5   8   2   0  1  NA  NA NA
    ## 1993 bakerge01   1884     1    SLU   UA  80 317  39  52   6   0  0  NA  NA NA
    ## 1994 bakerph01   1884     1    WSU   UA  86 371  75 107  12   5  1  NA  NA NA
    ## 1995 baldwki01   1884     1    KCU   UA  50 191  19  37   6   3  0  NA  NA NA
    ## 1996 baldwki01   1884     2    CHU   UA   1   1   0   1   0   0  0  NA  NA NA
    ## 1997 baldwla01   1884     1    MLU   UA   7  27   6   6   3   0  0  NA  NA NA
    ## 1998 barbech01   1884     1    CNU   UA  55 204  38  41   1   4  0  NA  NA NA
    ## 1999 barklsa01   1884     1    TL1   AA 104 435  71 133  39   9  1  NA  NA NA
    ## 2000 barnebi01   1884     1    SPU   UA   8  30   2   6   1   0  0  NA  NA NA
    ## 2001  barrbo01   1884     1    WS7   AA  39 135  15  20   3   1  2  NA  NA NA
    ## 2002  barrbo01   1884     2    IN2   AA  18  65   6  12   3   2  0  NA  NA NA
    ## 2003 barrema01   1884     1    BSN   NL   3   6   0   0   0   0  0   0  NA NA
    ## 2004 barrema01   1884     2    IN2   AA   5  13   1   1   1   0  0  NA  NA NA
    ## 2005 bassech01   1884     1    PRO   NL  27  79  10  11   2   1  0   6  NA NA
    ## 2006 bastich01   1884     1    WIL   UA  17  60   6  12   1   3  2  NA  NA NA
    ## 2007 bastich01   1884     2    KCU   UA  11  46   6   9   3   0  1  NA  NA NA
    ## 2008 battijo01   1884     1    PT1   AA  43 158  10  28   1   2  0  NA  NA NA
    ## 2009 battijo01   1884     2    CHU   UA  18  69   8  13   2   0  0  NA  NA NA
    ## 2010 battijo01   1884     3    BLU   UA  17  59   3   6   1   0  0  NA  NA NA
    ## 2011 baueral01   1884     1    CL5   AA   3  11   2   3   0   0  0  NA  NA NA
    ## 2012 beachja01   1884     1    WS7   AA   8  31   3   3   2   0  0  NA  NA NA
    ## 2013 beatlda01   1884     1    DTN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2014 becanbu01   1884     1    NY4   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 2015  beckfr01   1884     1    PT1   AA   3  12   1   4   1   0  0  NA  NA NA
    ## 2016  beckfr01   1884     2    BLU   UA   5  20   1   2   1   0  0  NA  NA NA
    ## 2017 begleed01   1884     1    NY1   NL  33 121  12  22   4   0  0   8  NA NA
    ## 2018 behelst01   1884     1    MLU   UA   9  33   5   8   1   0  0  NA  NA NA
    ## 2019 bennech01   1884     1    DTN   NL  90 341  37  90  18   6  3  40  NA NA
    ## 2020 benneik01   1884     1    BR3   AA  49 189  25  38  11   5  1  NA  NA NA
    ## 2021 benneik01   1884     2    WIL   UA   6  22   0   1   0   0  0  NA  NA NA
    ## 2022 berkefr01   1884     1    CN2   AA   6  25   3   6   0   1  0   3  NA NA
    ## 2023 berrych01   1884     1    ALT   UA   7  25   2   6   0   0  0  NA  NA NA
    ## 2024 berrych01   1884     2    KCU   UA  29 118  15  29   6   1  1  NA  NA NA
    ## 2025 berrych01   1884     3    CHU   UA   7  27   4   3   2   0  0  NA  NA NA
    ## 2026 bignege01   1884     1    MLU   UA   4   9   4   2   0   0  0  NA  NA NA
    ## 2027 birchju01   1884     1    PH4   AA  54 221  36  57   2   2  0  NA  NA NA
    ## 2028 bishofr01   1884     1    CHU   UA   4  16   1   3   1   0  0  NA  NA NA
    ## 2029 blackbo01   1884     1    KCU   UA  38 146  25  36  14   2  1  NA  NA NA
    ## 2030 blaisdi01   1884     1    KCU   UA   4  16   1   5   1   0  0  NA  NA NA
    ## 2031 blakibo01   1884     1    PH4   AA  32 128  21  33   6   0  0  NA  NA NA
    ## 2032 blakibo01   1884     2    IN2   AA   6  18   0   4   1   0  0  NA  NA NA
    ## 2033  bondto01   1884     1    BSU   UA  37 162  21  48   8   0  0  NA  NA NA
    ## 2034  bondto01   1884     2    IN2   AA   7  23   0   3   1   1  0  NA  NA NA
    ## 2035 boylehe01   1884     1    SLU   UA  65 262  41  68  10   3  4  NA  NA NA
    ## 2036 bradlal01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2037 bradlge01   1884     1    CNU   UA  58 226  31  43   4   7  0  NA  NA NA
    ## 2038 bradyst01   1884     1    NY4   AA 112 485 102 122  11   3  1  NA  NA NA
    ## 2039 brennji01   1884     1    SLU   UA  56 231  38  50   6   1  0  NA  NA NA
    ## 2040 briggch01   1884     1    CHU   UA  49 182  29  31   8   2  1  NA  NA NA
    ## 2041 brillfr01   1884     1    DTN   NL  13  44   5   6   0   0  0   2  NA NA
    ## 2042 briodfa01   1884     1    CL2   NL  43 148  17  25   6   0  1  12  NA NA
    ## 2043 briodfa01   1884     2    CNU   UA  22  89  11  30   2   2  0  NA  NA NA
    ## 2044 brougca01   1884     1    MLU   UA  11  39   5  12   5   0  0  NA  NA NA
    ## 2045 broutda01   1884     1    BFN   NL  94 398  82 130  22  15 14  79  NA NA
    ## 2046 browned01   1884     1    TL1   AA  42 153  13  27   3   0  0  NA  NA NA
    ## 2047 brownji01   1884     1    ALT   UA  21  88  12  22   2   2  1  NA  NA NA
    ## 2048 brownji01   1884     2    NY1   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2049 brownji01   1884     3    SPU   UA   6  16   5   5   4   0  0  NA  NA NA
    ## 2050 brownjo01   1884     1    CHN   NL  15  61   6  13   1   0  0   3  NA NA
    ## 2051 brownle01   1884     1    BSU   UA  85 325  50  75  18   3  1  NA  NA NA
    ## 2052 brownpe01   1884     1    LS2   AA 103 447 101 150  33   8  4  47  NA NA
    ## 2053 brownto01   1884     1    CL5   AA 107 451  93 123   9  11  5  32  NA NA
    ## 2054 buffich01   1884     1    BSN   NL  87 352  48  94  18   3  1  39  NA NA
    ## 2055 bukerha01   1884     1    DTN   NL  30 111   5  15   1   0  0   3  NA NA
    ## 2056 bullasi01   1884     1    TL1   AA  13  45   4   4   0   1  0  NA  NA NA
    ## 2057 burcher01   1884     1    CL2   NL  32 124   9  26   4   0  0   7  NA NA
    ## 2058 burdoja01   1884     1    BSN   NL  87 361  65  97  14   4  6  49  NA NA
    ## 2059 burkeja01   1884     1    BSU   UA  47 184  21  41   8   3  0  NA  NA NA
    ## 2060 burnsdi01   1884     1    CNU   UA  79 350  84 107  17  12  4  NA  NA NA
    ## 2061 burnsoy01   1884     1    WIL   UA   2   7   0   1   0   1  0  NA  NA NA
    ## 2062 burnsoy01   1884     2    BL2   AA  35 131  34  39   2   6  6  23  NA NA
    ## 2063 burnspa01   1884     1    BL2   AA   6  25   3   5   2   1  0  NA  NA NA
    ## 2064 burnspa01   1884     2    BLU   UA   1   4   0   2   0   0  0  NA  NA NA
    ## 2065 burnsto01   1884     1    CHN   NL  83 343  54  84  14   2  7  44  NA NA
    ## 2066 bushodo01   1884     1    CL2   NL  62 203  24  48   6   1  0  10  NA NA
    ## 2067 butlebi01   1884     1    IN2   AA   9  31   7   7   3   2  0  NA  NA NA
    ## 2068 butleki01   1884     1    BSU   UA  71 255  36  43  15   0  0  NA  NA NA
    ## 2069  cadych01   1884     1    CHU   UA   6  20   4   2   1   1  0  NA  NA NA
    ## 2070  cadych01   1884     2    KCU   UA   2   3   0   0   0   0  0  NA  NA NA
    ## 2071 cahiljo01   1884     1    CL5   AA  59 210  28  46   3   3  0  NA  NA NA
    ## 2072 callaed01   1884     1    SLU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2073 callaed01   1884     2    KCU   UA   3  11   0   4   0   0  0  NA  NA NA
    ## 2074 callaed01   1884     3    BSU   UA   4  13   2   5   0   0  0  NA  NA NA
    ## 2075 callapa01   1884     1    IN2   AA  61 258  38  67   8   5  2  NA  NA NA
    ## 2076 carpehi01   1884     1    CN2   AA 108 474  80 121  16   2  4  60  NA NA
    ## 2077 carroch01   1884     1    WSU   UA   4  16   1   4   0   0  0  NA  NA NA
    ## 2078 carrocl01   1884     1    PRO   NL 113 452  90 118  16   4  3  54  NA NA
    ## 2079 carrofr01   1884     1    CL5   AA  69 252  46  70  13   5  6  NA  NA NA
    ## 2080 carropa01   1884     1    ALT   UA  11  49   4  13   1   0  0  NA  NA NA
    ## 2081 carropa01   1884     2    PHU   UA   5  19   1   3   1   0  0  NA  NA NA
    ## 2082 carrosc01   1884     1    SPU   UA   9  31   3   3   1   0  0  NA  NA NA
    ## 2083 carutbo01   1884     1    SL4   AA  23  82  15  22   2   0  2  NA  NA NA
    ## 2084 caseyda01   1884     1    WIL   UA   2   6   0   1   0   0  0  NA  NA NA
    ## 2085 caseyde01   1884     1    WIL   UA   2   8   1   2   1   0  0  NA  NA NA
    ## 2086 caseyde01   1884     2    BL2   AA  37 149  20  37   7   4  3  NA  NA NA
    ## 2087 caskied01   1884     1    NY1   NL 100 351  49  81  11   1  1  40  NA NA
    ## 2088 cassijo01   1884     1    BR3   AA 106 433  57 109  11   6  2  NA  NA NA
    ## 2089 cattajo01   1884     1    PRO   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2090 cattajo01   1884     2    SLU   UA   2   7   0   0   0   0  0  NA  NA NA
    ## 2091 chattji01   1884     1    KCU   UA   4  15   4   2   1   0  0  NA  NA NA
    ## 2092 clarkjo01   1884     1    CHN   NL  21  84  16  22   6   2  3  17  NA NA
    ## 2093 clemeja01   1884     1    PHU   UA  41 177  37  50  13   2  3  NA  NA NA
    ## 2094 clemeja01   1884     2    PHI   NL   9  30   3   7   0   0  0   0  NA NA
    ## 2095 cleveel01   1884     1    CNU   UA  29 115  24  37   9   2  0  NA  NA NA
    ## 2096 clinemo01   1884     1    LS2   AA  94 396  91 115  16   7  2  39  NA NA
    ## 2097 clintji01   1884     1    BL2   AA 104 437  82 118  12   6  4  NA  NA NA
    ## 2098 colemjo01   1884     1    PHI   NL  43 171  16  42   7   2  0  22  NA NA
    ## 2099 colemjo01   1884     2    PH4   AA  28 107  16  22   2   3  2  NA  NA NA
    ## 2100 colgaed01   1884     1    PT1   AA  48 161  10  25   4   1  0  NA  NA NA
    ## 2101 collich01   1884     1    BFN   NL  45 169  24  30   6   0  0  20  NA NA
    ## 2102 collich01   1884     2    IN2   AA  38 138  18  31   3   1  0  NA  NA NA
    ## 2103 comisch01   1884     1    SL4   AA 108 460  76 109  17   6  2  84  NA NA
    ## 2104 conleed01   1884     1    PRO   NL   8  28   0   4   0   0  0   0  NA NA
    ## 2105 connojo01   1884     1    ALT   UA   3  11   0   1   0   0  0  NA  NA NA
    ## 2106 connojo01   1884     2    KCU   UA   3  11   2   1   0   0  0  NA  NA NA
    ## 2107 connojo02   1884     1    BSN   NL   7  25   1   2   0   0  0   1  NA NA
    ## 2108 connoro01   1884     1    NY1   NL 116 477  98 151  28   4  4  82  NA NA
    ## 2109 conwabi01   1884     1    PHI   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2110 conwaji01   1884     1    BR3   AA  14  47   1   6   0   0  0  NA  NA NA
    ## 2111  cookpa01   1884     1    PHI   NL   3  12   0   1   0   0  0   0  NA NA
    ## 2112 corcoja01   1884     1    BR3   AA  52 185  17  39   4   3  0  NA  NA NA
    ## 2113 corcola01   1884     1    CHN   NL  64 251  43  61   3   4  1  19  NA NA
    ## 2114 corcomi01   1884     1    CHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2115 coreyfr01   1884     1    PH4   AA 104 439  64 121  17  16  5  NA  NA NA
    ## 2116 corkhpo01   1884     1    CN2   AA 110 452  85 124  13  11  4  70  NA NA
    ## 2117 corriph01   1884     1    CHU   UA   2   7   1   1   0   0  0  NA  NA NA
    ## 2118 coughed01   1884     1    BFN   NL   1   4   0   1   0   0  0   1  NA NA
    ## 2119   coxfr01   1884     1    DTN   NL  27 102   6  13   3   1  0   4  NA NA
    ## 2120 craneed01   1884     1    BSU   UA 101 428  83 122  23   6 12  NA  NA NA
    ## 2121 cranesa01   1884     1    CNU   UA  80 309  56  72   9   3  1  NA  NA NA
    ## 2122 creamge01   1884     1    PT1   AA  98 339  38  62   8   5  0  NA  NA NA
    ## 2123 creegma01   1884     1    WSU   UA   9  33   4   5   0   0  0  NA  NA NA
    ## 2124 cronida01   1884     1    CHU   UA   1   4   1   1   0   0  0  NA  NA NA
    ## 2125 cronida01   1884     2    SLU   UA   1   5   0   0   0   0  0  NA  NA NA
    ## 2126 crosbge01   1884     1    CHN   NL   3  13   1   4   0   0  1   1  NA NA
    ## 2127 crosscl01   1884     1    ALT   UA   2   7   1   4   1   0  0  NA  NA NA
    ## 2128 crosscl01   1884     2    PHU   UA   2   9   0   2   0   0  0  NA  NA NA
    ## 2129 crosscl01   1884     3    KCU   UA  25  93  13  20   1   0  0  NA  NA NA
    ## 2130 crothdo01   1884     1    KCU   UA   4  15   2   2   0   0  0  NA  NA NA
    ## 2131 crottjo01   1884     1    CNU   UA  21  84  11  22   4   2  1  NA  NA NA
    ## 2132 crowlbi01   1884     1    BSN   NL 108 407  50 110  14   6  6  61  NA NA
    ## 2133 crowljo01   1884     1    PHI   NL  48 168  26  41   7   3  0  19  NA NA
    ## 2134 cudwoji01   1884     1    KCU   UA  32 116   7  17   3   1  0  NA  NA NA
    ## 2135  cuffjo01   1884     1    BLU   UA   3  11   1   1   1   0  0  NA  NA NA
    ## 2136 cullejo01   1884     1    WIL   UA   9  31   2   6   0   0  0  NA  NA NA
    ## 2137 currywe01   1884     1    RIC   AA   2   8   1   2   0   0  0  NA  NA NA
    ## 2138 cushmed01   1884     1    MLU   UA   4  11   1   1   0   0  0  NA  NA NA
    ## 2139 cusicto01   1884     1    WIL   UA  11  34   0   5   0   0  0  NA  NA NA
    ## 2140 cusicto01   1884     2    PHI   NL   9  29   2   4   0   0  0   1  NA NA
    ## 2141 cuthbne01   1884     1    BLU   UA  44 168  29  34   5   0  0  NA  NA NA
    ## 2142 dailyhu01   1884     1    CHU   UA  58 196  21  43   6   1  0  NA  NA NA
    ## 2143 dailyhu01   1884     2    WSU   UA   2   5   0   0   0   0  0  NA  NA NA
    ## 2144 daisege01   1884     1    ALT   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2145 dalryab01   1884     1    CHN   NL 111 521 111 161  18   9 22  69  NA NA
    ## 2146  dalyto01   1884     1    PHU   UA   2   8   0   0   0   0  0  NA  NA NA
    ## 2147 daniech01   1884     1    BSU   UA   3  11   1   3   0   0  0  NA  NA NA
    ## 2148 davisda01   1884     1    SL4   AA  25  87   5  15   0   1  0  NA  NA NA
    ## 2149 davisda01   1884     2    BSN   NL   4  16   0   0   0   0  0   0  NA NA
    ## 2150 davisju01   1884     1    KCU   UA   7  29   3   6   0   0  0  NA  NA NA
    ## 2151 deaglre01   1884     1    CN2   AA   4  13   1   0   0   0  0  NA  NA NA
    ## 2152 deaglre01   1884     2    LS2   AA  12  45   2   6   1   0  0   3  NA NA
    ## 2153 dealypa01   1884     1    SPU   UA   5  15   2   2   0   0  0  NA  NA NA
    ## 2154 deasljo01   1884     1    WSU   UA  31 134  20  29   1   1  0  NA  NA NA
    ## 2155 deasljo01   1884     2    KCU   UA  13  40   3   7   2   0  0  NA  NA NA
    ## 2156 deaslpa01   1884     1    SL4   AA  75 254  27  52   5   4  0  NA  NA NA
    ## 2157 deckeha01   1884     1    IN2   AA   4  15   1   4   1   0  0  NA  NA NA
    ## 2158 deckeha01   1884     2    KCU   UA  23  75   8  10   2   0  0  NA  NA NA
    ## 2159   deeji01   1884     1    PT1   AA  12  40   0   5   0   0  0  NA  NA NA
    ## 2160 dennyje01   1884     1    PRO   NL 110 439  57 109  22   9  6  59  NA NA
    ## 2161 depanmi01   1884     1    PHI   NL   4  10   0   2   0   0  0   0  NA NA
    ## 2162 dickebu01   1884     1    SLU   UA  46 211  49  77  15   1  0  NA  NA NA
    ## 2163 dickebu01   1884     2    BL2   AA  13  56   9  12   2   1  0  NA  NA NA
    ## 2164 dickebu01   1884     3    LS2   AA   8  28   6   4   0   2  1  NA  NA NA
    ## 2165 dolanto01   1884     1    SL4   AA  35 137  19  36   6   2  0  NA  NA NA
    ## 2166 dolanto01   1884     2    SLU   UA  19  69   9  13   3   0  0  NA  NA NA
    ## 2167 donneji01   1884     1    IN2   AA  40 134  22  34   2   2  0  NA  NA NA
    ## 2168 donneji02   1884     1    KCU   UA   6  23   2   3   1   0  0  NA  NA NA
    ## 2169 dorgaje01   1884     1    IN2   AA  34 141  22  42   6   1  0  NA  NA NA
    ## 2170 dorgaje01   1884     2    BR3   AA   4  13   2   4   0   0  0  NA  NA NA
    ## 2171 dorgami01   1884     1    NY1   NL  83 341  61  94  11   6  1  48  NA NA
    ## 2172 dorseje01   1884     1    BLU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2173 doughch01   1884     1    ALT   UA  23  85   6  22   5   0  0  NA  NA NA
    ## 2174   dowcl01   1884     1    BSU   UA   1   6   1   2   0   0  0  NA  NA NA
    ## 2175 doyleco01   1884     1    PT1   AA  15  58   8  17   3   2  0  NA  NA NA
    ## 2176 drakely01   1884     1    WS7   AA   2   7   0   2   1   0  0   2  NA NA
    ## 2177  drewda01   1884     1    PHU   UA   2   9   1   4   0   0  0  NA  NA NA
    ## 2178  drewda01   1884     2    WSU   UA  13  53   8  16   1   2  0  NA  NA NA
    ## 2179 driscde01   1884     1    LS2   AA  13  48   5   9   1   0  0   1  NA NA
    ## 2180 duganbi01   1884     1    RIC   AA   9  28   4   3   1   0  0  NA  NA NA
    ## 2181 duganbi01   1884     2    KCU   UA   3   6   0   0   0   0  0  NA  NA NA
    ## 2182 duganed01   1884     1    RIC   AA  22  70   4   8   0   0  0  NA  NA NA
    ## 2183 dundoed01   1884     1    CL5   AA  26  86   6  12   2   2  0  NA  NA NA
    ## 2184 dunlafr01   1884     1    SLU   UA 101 449 160 185  39   8 13  NA  NA NA
    ## 2185  dunnst01   1884     1    SPU   UA   9  32   2   8   2   0  0  NA  NA NA
    ## 2186 dwighal01   1884     1    KCU   UA  12  43   8  10   2   0  0  NA  NA NA
    ## 2187 eastehe01   1884     1    PHU   UA  28 115  12  28   5   0  0  NA  NA NA
    ## 2188  edench01   1884     1    PT1   AA  32 122  12  33   7   4  1  NA  NA NA
    ## 2189 eggleda01   1884     1    BFN   NL  63 241  25  47   3   1  0  20  NA NA
    ## 2190 ellicjo01   1884     1    CHU   UA  92 394  71  93  11   0  0  NA  NA NA
    ## 2191 ellicjo01   1884     2    KCU   UA   2   8   0   0   0   0  0  NA  NA NA
    ## 2192 ellicjo01   1884     3    BLU   UA   7  27   2   4   0   0  0  NA  NA NA
    ## 2193   elybo01   1884     1    BFN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2194 emslibo01   1884     1    BL2   AA  51 195  21  37   6   3  0  NA  NA NA
    ## 2195 esterdu01   1884     1    NY4   AA 112 477 110 150  29  11  1  NA  NA NA
    ## 2196 evansja01   1884     1    CL2   NL  80 313  32  81  18   3  1  38  NA NA
    ## 2197 eversto01   1884     1    WSU   UA 109 427  54  99   6   1  0  NA  NA NA
    ## 2198 ewingbu01   1884     1    NY1   NL  94 382  90 106  15  20  3  41  NA NA
    ## 2199 ewingjo01   1884     1    CNU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2200 ewingjo01   1884     2    WSU   UA   1   5   1   1   0   1  0  NA  NA NA
    ## 2201 faatzja01   1884     1    PT1   AA  29 112  18  27   2   3  0  NA  NA NA
    ## 2202 falchan01   1884     1    MLU   UA   5  18   0   2   0   0  0  NA  NA NA
    ## 2203 farleto01   1884     1    WS7   AA  14  52   5  11   4   0  0  NA  NA NA
    ## 2204 farrasi01   1884     1    PHI   NL 111 428  62 105  16   6  1  45  NA NA
    ## 2205 farreja02   1884     1    PRO   NL 111 469  70 102  13   6  1  37  NA NA
    ## 2206 farrejo01   1884     1    DTN   NL 110 461  59 104  10   5  3  41  NA NA
    ## 2207 farrojo01   1884     1    BR3   AA  16  58   7  11   2   0  0  NA  NA NA
    ## 2208 fennefr01   1884     1    WS7   AA  62 257  52  75  17   7  2  NA  NA NA
    ## 2209 fennefr01   1884     2    CN2   AA  28 122  42  43   5   8  2  NA  NA NA
    ## 2210 fergubo01   1884     1    PT1   AA  10  41   2   6   0   0  0  NA  NA NA
    ## 2211 ferguch01   1884     1    PHI   NL  52 203  26  50   6   3  0  20  NA NA
    ## 2212 fieldji01   1884     1    CL5   AA 105 417  74  97   9   7  4  NA  NA NA
    ## 2213 firthte01   1884     1    RIC   AA   1   3   0   1   0   0  0  NA  NA NA
    ## 2214   fishe01   1884     1    PHU   UA  10  36   7   8   2   0  0  NA  NA NA
    ## 2215 fishech02   1884     1    KCU   UA  10  40   3   8   2   0  0  NA  NA NA
    ## 2216 fishech02   1884     2    CHU   UA   1   3   1   2   0   0  0  NA  NA NA
    ## 2217 fishege01   1884     1    CL2   NL   6  24   2   3   0   0  0   0  NA NA
    ## 2218 fishege01   1884     2    WIL   UA   8  29   0   2   0   0  0  NA  NA NA
    ## 2219 flintsi01   1884     1    CHN   NL  73 279  35  57   5   2  9  45  NA NA
    ## 2220 flynnjo01   1884     1    PHU   UA  52 209  38  52   9   4  4  NA  NA NA
    ## 2221 flynnjo01   1884     2    BSU   UA   9  31   4   7   2   0  0  NA  NA NA
    ## 2222 fogarji01   1884     1    PHI   NL  97 378  42  80  12   6  1  37  NA NA
    ## 2223 foleywi01   1884     1    CHU   UA  19  71  15  20   1   1  0  NA  NA NA
    ## 2224 forceda01   1884     1    BFN   NL 106 403  47  83  13   3  0  36  NA NA
    ## 2225  forded01   1884     1    RIC   AA   2   5   0   0   0   0  0  NA  NA NA
    ## 2226 foremfr01   1884     1    CHU   UA   3  11   0   1   0   0  0  NA  NA NA
    ## 2227 foremfr01   1884     2    KCU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2228 forstto01   1884     1    PT1   AA  35 126  10  28   5   0  0  NA  NA NA
    ## 2229 fostero02   1884     1    PHU   UA   1   3   0   1   0   1  0  NA  NA NA
    ## 2230 fostero02   1884     2    PH4   AA   4  11   4   2   0   0  0  NA  NA NA
    ## 2231 foutzda01   1884     1    SL4   AA  33 119  17  27   4   0  0  NA  NA NA
    ## 2232   foxjo01   1884     1    PT1   AA   8  25   4   6   2   0  0  NA  NA NA
    ## 2233   frank01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2234 friespe01   1884     1    IN2   AA   1   3   0   1   1   0  0  NA  NA NA
    ## 2235 fulmech01   1884     1    CN2   AA  31 114  13  20   2   1  0   8  NA NA
    ## 2236 fulmech01   1884     2    SL4   AA   1   5   0   0   0   0  0  NA  NA NA
    ## 2237 fulmech02   1884     1    WSU   UA  48 181  39  50   9   0  0  NA  NA NA
    ## 2238 fusseed01   1884     1    BLU   UA  68 303  60  86  16   3  1  NA  NA NA
    ## 2239 gagusch01   1884     1    WSU   UA  44 154  14  38   7   1  0  NA  NA NA
    ## 2240 gallabi01   1884     1    PHU   UA   3  11   1   1   0   0  0  NA  NA NA
    ## 2241 galvilo01   1884     1    SPU   UA   3   9   0   2   0   0  0  NA  NA NA
    ## 2242 galvipu01   1884     1    BFN   NL  72 274  34  49   6   1  0  24  NA NA
    ## 2243 ganzech01   1884     1    SPU   UA   7  23   2   5   0   0  0  NA  NA NA
    ## 2244 gardnal01   1884     1    WS7   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 2245 gardngi01   1884     1    BL2   AA  41 173  32  37   6   8  2  NA  NA NA
    ## 2246 gardngi01   1884     2    CHU   UA  38 149  22  38  10   2  0  NA  NA NA
    ## 2247 gardngi01   1884     3    BLU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2248 gastfed01   1884     1    DTN   NL  23  82   6   6   1   0  0   2  NA NA
    ## 2249  geerbi01   1884     1    PHU   UA   9  36   7   9   2   1  0  NA  NA NA
    ## 2250  geerbi01   1884     2    BR3   AA 107 391  68  82  15   7  0  NA  NA NA
    ## 2251  geisbi01   1884     1    DTN   NL  75 283  22  50  11   4  2  16  NA NA
    ## 2252 gerhajo01   1884     1    LS2   AA 106 404  39  89   7   8  0  40  NA NA
    ## 2253 getzich01   1884     1    DTN   NL  17  55   4   6   0   0  0   1  NA NA
    ## 2254 gillepe01   1884     1    NY1   NL 101 413  75 109   7   4  2  44  NA NA
    ## 2255 gilleto01   1884     1    PHU   UA  29 116   5  18   2   0  0  NA  NA NA
    ## 2256 gilliba01   1884     1    PRO   NL  82 294  47  72  13   2  1  38  NA NA
    ## 2257 gilmapi01   1884     1    CL2   NL   2  10   0   1   0   0  0   0  NA NA
    ## 2258 gladmbu01   1884     1    WS7   AA  56 224  17  35   5   3  1  NA  NA NA
    ## 2259 glassja01   1884     1    CL2   NL  72 281  45  70   4   4  1  22  NA NA
    ## 2260 glassja01   1884     2    CNU   UA  38 172  48  72   9   5  2  NA  NA NA
    ## 2261 gleasbi01   1884     1    SL4   AA 110 472  97 127  21   7  1  NA  NA NA
    ## 2262 gleasja01   1884     1    SLU   UA  92 395  90 128  30   2  4  NA  NA NA
    ## 2263 glenned01   1884     1    RIC   AA  43 175  26  43   2   4  1  NA  NA NA
    ## 2264 goldsfr01   1884     1    CHN   NL  22  81  11  11   2   0  2   6  NA NA
    ## 2265 goldsfr01   1884     2    BL2   AA   4  14   2   2   0   0  0  NA  NA NA
    ## 2266 goldswa02   1884     1    SL4   AA   5  20   2   4   0   0  0   1  NA NA
    ## 2267 goldswa02   1884     2    WS7   AA   6  24   4   9   0   0  0   3  NA NA
    ## 2268 goldswa02   1884     3    RIC   AA  11  40   4   9   1   0  0   4  NA NA
    ## 2269  gorege01   1884     1    CHN   NL 103 422 104 134  18   4  5  34  NA NA
    ## 2270 gormaja01   1884     1    KCU   UA   8  31   3   4   1   0  0  NA  NA NA
    ## 2271 gormaja01   1884     2    PT1   AA   8  27   3   4   0   1  0  NA  NA NA
    ## 2272 gormato04   1884     1    KCU   UA  25 106  22  34   4   2  0  NA  NA NA
    ## 2273 gradyjo01   1884     1    ALT   UA   9  36   5  11   3   0  0  NA  NA NA
    ## 2274 grahabe01   1884     1    CHU   UA   1   5   2   1   0   0  0  NA  NA NA
    ## 2275 grahabe01   1884     2    BLU   UA  41 167  21  45  11   0  0  NA  NA NA
    ## 2276  grayji01   1884     1    PT1   AA   1   2   0   1   0   0  0  NA  NA NA
    ## 2277 greenbi01   1884     1    BR3   AA  92 385  52  83   8   3  3  NA  NA NA
    ## 2278 greenji01   1884     1    WSU   UA  10  36   4   5   1   0  0  NA  NA NA
    ## 2279 griffsa01   1884     1    NY1   NL  16  62   7  11   2   0  0   6  NA NA
    ## 2280 griffth01   1884     1    MLU   UA  11  41   5   9   2   0  0  NA  NA NA
    ## 2281 grossem01   1884     1    CHU   UA  23  95  13  34   6   2  4  NA  NA NA
    ## 2282 guinebe01   1884     1    DTN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 2283 gunnito01   1884     1    BSN   NL  12  45   4   5   1   1  0   2  NA NA
    ## 2284 gunsojo01   1884     1    WSU   UA  45 166  15  23   2   0  0  NA  NA NA
    ## 2285 hackeme01   1884     1    BSN   NL  72 268  28  55  13   2  1  20  NA NA
    ## 2286 hackewa01   1884     1    BSU   UA 103 415  71 101  19   0  1  NA  NA NA
    ## 2287 haganar01   1884     1    BFN   NL   3  13   3   4   0   0  0   1  NA NA
    ## 2288 halpiji01   1884     1    WSU   UA  46 168  24  31   3   0  0  NA  NA NA
    ## 2289 hamiljo01   1884     1    WS7   AA  21  71   5   7   0   2  0  NA  NA NA
    ## 2290 hankifr01   1884     1    NY1   NL 105 389  44  90  16   7  2  43  NA NA
    ## 2291 hanlone01   1884     1    DTN   NL 114 450  86 119  18   6  5  39  NA NA
    ## 2292 hannajo01   1884     1    WS7   AA  23  76   8   5   0   0  0  NA  NA NA
    ## 2293 hannajo01   1884     2    RIC   AA  22  67   6  13   2   1  0  NA  NA NA
    ## 2294 harbibi01   1884     1    CNU   UA  82 341  59  95  12   5  2  NA  NA NA
    ## 2295 hardilo01   1884     1    PHI   NL   3   8   0   3   2   0  0   0  NA NA
    ## 2296 harkijo01   1884     1    CL2   NL  61 229  24  47   4   2  0  20  NA NA
    ## 2297 harrifr01   1884     1    ALT   UA  24  95  10  25   2   1  0  NA  NA NA
    ## 2298 hautzch01   1884     1    PT1   AA   7  24   0   5   0   0  0  NA  NA NA
    ## 2299 hawesbi01   1884     1    CNU   UA  79 349  80  97   7   4  4  NA  NA NA
    ## 2300 hawketh01   1884     1    WS7   AA  38 151  16  42   4   2  0  NA  NA NA
    ## 2301 hayesja01   1884     1    PT1   AA  33 124  11  28   6   1  0  NA  NA NA
    ## 2302 hayesja01   1884     2    BR3   AA  16  51   4  12   3   0  0  NA  NA NA
    ## 2303 heckegu01   1884     1    LS2   AA  78 316  53  94  14   8  4  42  NA NA
    ## 2304 hendeha01   1884     1    BL2   AA  53 203  24  46   7   7  0  NA  NA NA
    ## 2305 henglmo01   1884     1    CHU   UA  19  74   9  15   2   1  0  NA  NA NA
    ## 2306 henglmo01   1884     2    SPU   UA   9  33   2   5   1   1  0  NA  NA NA
    ## 2307 henryjo01   1884     1    CL2   NL   9  26   2   4   0   0  0   0  NA NA
    ## 2308 hibbajo01   1884     1    CHN   NL   2   7   0   0   0   0  0   0  NA NA
    ## 2309 hickmer01   1884     1    KCU   UA  19  72   4  12   1   0  0  NA  NA NA
    ## 2310 hilsech01   1884     1    PH4   AA   6  24   5   5   1   1  0  NA  NA NA
    ## 2311 hinesmi01   1884     1    BSN   NL  35 132  16  23   3   0  0   3  NA NA
    ## 2312 hinespa01   1884     1    PRO   NL 114 490  94 148  36  10  3  41  NA NA
    ## 2313 hodnech01   1884     1    SLU   UA  18  58   9  12   1   0  0  NA  NA NA
    ## 2314 hoganed02   1884     1    MLU   UA  11  37   6   3   1   0  0  NA  NA NA
    ## 2315 holbebi01   1884     1    NY4   AA  65 255  28  53   5   0  0  NA  NA NA
    ## 2316 holdsji01   1884     1    IN2   AA   5  18   1   2   0   0  0  NA  NA NA
    ## 2317 hoovebu01   1884     1    PHU   UA  63 275  76 100  20   8  0  NA  NA NA
    ## 2318 hoovebu01   1884     2    PHI   NL  10  42   6   8   1   0  1   4  NA NA
    ## 2319 horanjo01   1884     1    CHU   UA  20  68   3   6   0   0  0  NA  NA NA
    ## 2320 hornujo01   1884     1    BSN   NL 115 518 119 139  27  10  7  51  NA NA
    ## 2321 hotalpe01   1884     1    CL2   NL 102 408  69  99  16   6  3  27  NA NA
    ## 2322 houcksa01   1884     1    PH4   AA 108 472  93 140  19  14  0  NA  NA NA
    ## 2323 housech01   1884     1    CHU   UA  83 310  32  74  12   5  1  NA  NA NA
    ## 2324 housech02   1884     1    BR3   AA  76 273  28  66  15   3  3  NA  NA NA
    ## 2325 hughebi01   1884     1    WSU   UA  14  49   5   6   0   0  0  NA  NA NA
    ## 2326 humphjo01   1884     1    WS7   AA  49 193  23  34   2   0  0  NA  NA NA
    ## 2327 humphjo01   1884     2    NY1   NL  20  64   6   6   0   0  0   2  NA NA
    ## 2328 huntebi01   1884     1    LS2   AA   2   7   1   1   0   0  0  NA  NA NA
    ## 2329 hutchbi01   1884     1    KCU   UA   2   8   1   2   0   0  0  NA  NA NA
    ## 2330 irwinar01   1884     1    PRO   NL 102 404  73  97  14   3  2  44  NA NA
    ## 2331 irwinjo01   1884     1    BSU   UA 105 432  81 101  22   6  1  NA  NA NA
    ## 2332 johnsbi01   1884     1    PHU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2333 johnsdi01   1884     1    RIC   AA  39 146  23  41   5   5  2  NA  NA NA
    ## 2334   jones02   1884     1    WS7   AA   4  17   2   5   0   0  0  NA  NA NA
    ## 2335 jonesbi01   1884     1    PHU   UA   4  14   2   2   0   0  0  NA  NA NA
    ## 2336 jonesch01   1884     1    CN2   AA 112 472 117 148  19  17  7  71  NA NA
    ## 2337 jonesch02   1884     1    BR3   AA  25  90  10  16   1   0  0  NA  NA NA
    ## 2338 jonesfr01   1884     1    DTN   NL   2   8   0   1   0   0  0   0  NA NA
    ## 2339 joneshe01   1884     1    DTN   NL  34 127  24  28   3   1  0   3  NA NA
    ## 2340 jonesja01   1884     1    CNU   UA  69 272  36  71   5   1  2  NA  NA NA
    ## 2341   joypo01   1884     1    WSU   UA  36 130  12  28   0   0  0  NA  NA NA
    ## 2342 kalbfch01   1884     1    WSU   UA   1   5   1   1   0   0  0  NA  NA NA
    ## 2343 kappejo01   1884     1    PHI   NL   4  15   1   1   0   0  0   0  NA NA
    ## 2344 kearnto01   1884     1    DTN   NL  21  79   9  16   0   1  0   7  NA NA
    ## 2345 keefeti01   1884     1    NY4   AA  62 210  27  50   3   6  3  NA  NA NA
    ## 2346 keenaji01   1884     1    IN2   AA  68 249  36  73  14   4  3  NA  NA NA
    ## 2347 kellyjo01   1884     1    CNU   UA  38 142  23  40   5   1  1  NA  NA NA
    ## 2348 kellyjo01   1884     2    WSU   UA   4  14   1   5   1   0  0  NA  NA NA
    ## 2349 kellyki01   1884     1    CHN   NL 108 452 120 160  28   5 13  95  NA NA
    ## 2350 kemmlru01   1884     1    CL5   AA  61 211  28  42   3   3  0  NA  NA NA
    ## 2351 kenneed01   1884     1    NY4   AA 103 378  49  72   6   2  1  NA  NA NA
    ## 2352 kenneed02   1884     1    CNU   UA  13  48   6  10   1   1  0  NA  NA NA
    ## 2353  kented01   1884     1    TL1   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 2354 kerinjo01   1884     1    IN2   AA  94 364  58  78  10   3  6  NA  NA NA
    ## 2355 kienzbi01   1884     1    PHU   UA  67 299  76  76  13   8  0  NA  NA NA
    ## 2356 kileyjo01   1884     1    WS7   AA  14  56   9  12   2   2  0  NA  NA NA
    ## 2357 kimbesa01   1884     1    BR3   AA  41 142  14  21   1   2  0  NA  NA NA
    ## 2358  kingsa01   1884     1    WS7   AA  12  45   3   8   2   0  0  NA  NA NA
    ## 2359 kinziwa01   1884     1    CHN   NL  19  82   4  13   3   0  2   8  NA NA
    ## 2360 kinziwa01   1884     2    SL4   AA   2   9   0   1   0   0  0  NA  NA NA
    ## 2361 kirbyjo01   1884     1    KCU   UA   2   7   1   1   0   0  0  NA  NA NA
    ## 2362 knighjo01   1884     1    PHI   NL   6  24   2   6   3   0  0   2  NA NA
    ## 2363 knighlo01   1884     1    PH4   AA 108 484  94 131  18  12  1  NA  NA NA
    ## 2364 knowlji01   1884     1    PT1   AA  46 182  19  42   5   7  0  NA  NA NA
    ## 2365 knowlji01   1884     2    BR3   AA  41 153  19  36   5   1  1  NA  NA NA
    ## 2366 koonsha01   1884     1    ALT   UA  21  78   8  18   2   1  0  NA  NA NA
    ## 2367 koonsha01   1884     2    CHU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2368 kreegfr01   1884     1    KCU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2369 krehmch01   1884     1    SL4   AA  21  70   3  16   0   1  0   5  NA NA
    ## 2370 kriegbi01   1884     1    CHU   UA  71 279  35  69  15   4  0  NA  NA NA
    ## 2371 kuehnbi01   1884     1    CL5   AA 110 415  48  98  13  16  5  NA  NA NA
    ## 2372  lanech01   1884     1    TL1   AA  57 215  26  49   9   5  1  NA  NA NA
    ## 2373   larki01   1884     1    WSU   UA  17  70  11  17   0   0  0  NA  NA NA
    ## 2374 larkihe01   1884     1    PH4   AA  85 326  59  90  21   9  3  37  NA NA
    ## 2375 larkite01   1884     1    RIC   AA  40 139  17  28   1   4  0  NA  NA NA
    ## 2376 lathaar01   1884     1    SL4   AA 110 474 115 130  17  12  1  NA  NA NA
    ## 2377 lathaju01   1884     1    LS2   AA  77 308  31  52   3   3  0  23  NA NA
    ## 2378 lauerch01   1884     1    PT1   AA  13  44   5   5   0   0  0  NA  NA NA
    ## 2379 lavinjo01   1884     1    SL4   AA  16  52   9  11   2   0  0  NA  NA NA
    ## 2380 lawlomi01   1884     1    WSU   UA   2   7   0   0   0   0  0  NA  NA NA
    ## 2381 learyja01   1884     1    ALT   UA   8  33   1   3   0   0  0  NA  NA NA
    ## 2382 learyja01   1884     2    CHU   UA  10  40   0   7   1   0  0  NA  NA NA
    ## 2383   leeto01   1884     1    CHN   NL   6  24   0   3   1   0  0   1  NA NA
    ## 2384   leeto01   1884     2    BLU   UA  21  82  11  23   1   0  0  NA  NA NA
    ## 2385 lehanja01   1884     1    WSU   UA   3  12   1   4   2   0  0  NA  NA NA
    ## 2386 levisch01   1884     1    BLU   UA  87 373  59  85  11   4  5  NA  NA NA
    ## 2387 levisch01   1884     2    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2388 levisch01   1884     3    IN2   AA   3  10   0   2   0   0  0  NA  NA NA
    ## 2389 lewisfr01   1884     1    SL4   AA  73 300  59  97  25   3  0  NA  NA NA
    ## 2390 lewisfr01   1884     2    SLU   UA   8  30   6   9   1   0  0  NA  NA NA
    ## 2391 lilliji01   1884     1    BFN   NL 114 471  68 105  12   5  3  53  NA NA
    ## 2392 lockema01   1884     1    IN2   AA   7  29   5   7   0   1  0   5  NA NA
    ## 2393 lockwmi01   1884     1    WSU   UA  20  67   9  14   1   0  0  NA  NA NA
    ## 2394 loughbi01   1884     1    NY1   NL   9  29   4   3   1   1  0   3  NA NA
    ## 2395  lowedi01   1884     1    DTN   NL   1   3   0   1   0   0  0   0  NA NA
    ## 2396  luffhe01   1884     1    PHU   UA  26 111   9  30   4   2  0  NA  NA NA
    ## 2397  luffhe01   1884     2    KCU   UA   5  19   0   1   0   0  0  NA  NA NA
    ## 2398 lynchja01   1884     1    NY4   AA  55 198  21  30   2   3  0  NA  NA NA
    ## 2399 lynchto01   1884     1    WIL   UA  16  58   6  16   3   1  0  NA  NA NA
    ## 2400 lynchto01   1884     2    PHI   NL  13  48   7  15   4   2  0   3  NA NA
    ## 2401 lynchto02   1884     1    CHN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2402 macarma01   1884     1    IN2   AA   6  21   1   2   0   0  0  NA  NA NA
    ## 2403 maculji01   1884     1    BL2   AA 107 360  73  73  16   6  4  NA  NA NA
    ## 2404 malonfe01   1884     1    PHU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2405 manloch01   1884     1    ALT   UA   2   7   1   3   0   0  0  NA  NA NA
    ## 2406 manloch01   1884     2    NY1   NL   3  10   0   0   0   0  0   0  NA NA
    ## 2407  mannfr01   1884     1    CL5   AA  99 366  70 101  12  18  7  NA  NA NA
    ## 2408 mannija01   1884     1    PHI   NL 104 424  71 115  29   4  5  52  NA NA
    ## 2409 manniji01   1884     1    BSN   NL  89 345  52  83   8   6  2  35  NA NA
    ## 2410 manniti01   1884     1    BL2   AA  91 341  49  70  14   5  2  NA  NA NA
    ## 2411 mansemi01   1884     1    PT1   AA  27 100  15  14   0   3  1  NA  NA NA
    ## 2412 mansemi01   1884     2    PH4   AA  20  70   6  14   1   1  0  NA  NA NA
    ## 2413 mansemi01   1884     3    RIC   AA  29 113  21  34   2   5  0  NA  NA NA
    ## 2414 manseto01   1884     1    CN2   AA  65 266  49  66   4   6  0  23  NA NA
    ## 2415 manseto01   1884     2    CL5   AA  23  77   9  15   1   3  0   6  NA NA
    ## 2416 maskrle01   1884     1    LS2   AA 105 412  48 103  13   4  0  36  NA NA
    ## 2417 mathebo01   1884     1    PH4   AA  49 184  26  34   5   1  0  NA  NA NA
    ## 2418 mattecv01   1884     1    SLU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2419 matthst01   1884     1    CHU   UA  37 142  24  39   7   1  0  NA  NA NA
    ## 2420  maulal01   1884     1    PHU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2421 mccarto01   1884     1    BSU   UA  53 209  37  45   2   2  0  NA  NA NA
    ## 2422 mccaual01   1884     1    IN2   AA  17  53   7  10   0   1  0   5  NA NA
    ## 2423 mccauji01   1884     1    SL4   AA   1   2   0   0   0   0  0  NA  NA NA
    ## 2424 mcclebi01   1884     1    PHI   NL 111 450  71 116  13   2  3  33  NA NA
    ## 2425 mcclobi01   1884     1    WIL   UA   9  30   0   3   0   0  0  NA  NA NA
    ## 2426 mccorje01   1884     1    PHU   UA  67 295  41  84  12   2  0  NA  NA NA
    ## 2427 mccorje01   1884     2    WSU   UA  42 157  23  34   8   2  0  NA  NA NA
    ## 2428 mccorji01   1884     1    CL2   NL  49 190  15  50   5   4  0  23  NA NA
    ## 2429 mccorji01   1884     2    CNU   UA  27 110  12  27   3   1  0  NA  NA NA
    ## 2430 mcdonji01   1884     1    WSU   UA   2   6   0   1   0   0  0  NA  NA NA
    ## 2431 mcdonji01   1884     2    PT1   AA  38 145  11  23   3   0  0  NA  NA NA
    ## 2432 mcelrji01   1884     1    PHI   NL  14  48   3   7   0   0  0   3  NA NA
    ## 2433 mcelrji01   1884     2    WIL   UA   1   2   0   0   0   0  0  NA  NA NA
    ## 2434 mcfarch01   1884     1    BLU   UA   3  14   2   3   1   0  0  NA  NA NA
    ## 2435 mcgarch01   1884     1    CHU   UA  19  70  10  11   2   0  0  NA  NA NA
    ## 2436 mcginju01   1884     1    SL4   AA  40 146  16  34   9   1  0  NA  NA NA
    ## 2437 mcguide01   1884     1    TL1   AA  45 151  12  28   7   0  1  NA  NA NA
    ## 2438 mcguijo01   1884     1    PHU   UA  53 220  25  52   8   1  0  NA  NA NA
    ## 2439 mckeefr01   1884     1    WSU   UA   4  17   2   3   0   0  0  NA  NA NA
    ## 2440 mckeeji01   1884     1    BSU   UA  16  66  13   9   0   0  0  NA  NA NA
    ## 2441 mckened01   1884     1    WSU   UA  32 117  19  22   1   0  0  NA  NA NA
    ## 2442 mckeola01   1884     1    IN2   AA  70 250  29  53   8   1  0  NA  NA NA
    ## 2443 mckinal01   1884     1    NY1   NL 116 470  66 128  21  13  3  73  NA NA
    ## 2444 mclauba01   1884     1    KCU   UA  42 162  15  37   7   3  0  NA  NA NA
    ## 2445 mclaufr01   1884     1    CNU   UA  16  67  10  16   4   1  2  NA  NA NA
    ## 2446 mclaufr01   1884     2    CHU   UA  15  67  11  16   4   1  0  NA  NA NA
    ## 2447 mclaufr01   1884     3    KCU   UA  32 123  17  28  11   0  1  NA  NA NA
    ## 2448 mclauja01   1884     1    WSU   UA  10  37   3   7   3   0  0  NA  NA NA
    ## 2449 mclauji01   1884     1    BL2   AA   5  22   3   5   1   1  0  NA  NA NA
    ## 2450 mclauto01   1884     1    LS2   AA  98 335  41  67  11   6  0  21  NA NA
    ## 2451 mcphebi01   1884     1    CN2   AA 112 450 107 125   8   7  5  64  NA NA
    ## 2452 mcquemo01   1884     1    CNU   UA  35 132  31  37   5   0  2  NA  NA NA
    ## 2453   mcrem01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2454 mcsortr01   1884     1    TL1   AA  21  68  12  17   1   0  0  NA  NA NA
    ## 2455 meegape01   1884     1    RIC   AA  23  75   6  12   1   2  0   2  NA NA
    ## 2456 meinkfr01   1884     1    DTN   NL  92 341  28  56   5   7  6  24  NA NA
    ## 2457 meistge01   1884     1    TL1   AA  34 119   9  23   6   0  0  NA  NA NA
    ## 2458 merried01   1884     1    IN2   AA  55 196  14  35   3   1  0  NA  NA NA
    ## 2459 meyerle01   1884     1    PHU   UA   3  11   0   1   1   0  0  NA  NA NA
    ## 2460 meyerlo01   1884     1    CNU   UA   2   3   1   0   0   0  0  NA  NA NA
    ## 2461 millecy01   1884     1    CHU   UA   1   4   1   1   0   0  0  NA  NA NA
    ## 2462 millecy01   1884     2    PRO   NL   6  23   3   1   0   0  0   0  NA NA
    ## 2463 millecy01   1884     3    PHI   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2464 milledo01   1884     1    PT1   AA  89 347  46  78  10   2  0  NA  NA NA
    ## 2465 milleed01   1884     1    TL1   AA   8  24   2   6   0   0  0   1  NA NA
    ## 2466 millege01   1884     1    CN2   AA   6  20   6   5   1   1  0   3  NA NA
    ## 2467 millejo02   1884     1    TL1   AA 105 423  46 101  12   8  1  NA  NA NA
    ## 2468 millijo01   1884     1    PH4   AA  66 268  39  77  20   3  3  NA  NA NA
    ## 2469 moffejo01   1884     1    TL1   AA  56 204  17  41   5   3  0  NA  NA NA
    ## 2470 moffesa01   1884     1    CL2   NL  67 256  26  47  12   2  0  15  NA NA
    ## 2471 monrofr01   1884     1    IN2   AA   2   8   1   0   0   0  0  NA  NA NA
    ## 2472 mooreha01   1884     1    WSU   UA 111 461  77 155  23   5  1  NA  NA NA
    ## 2473 mooreje01   1884     1    ALT   UA  20  80  10  25   3   1  1  NA  NA NA
    ## 2474 mooreje01   1884     2    CL2   NL   9  30   1   6   0   0  0  10  NA NA
    ## 2475 morgabi01   1884     1    RIC   AA   6  20   0   2   0   0  0  NA  NA NA
    ## 2476 morgabi01   1884     2    BLU   UA   2   9   1   2   0   0  0  NA  NA NA
    ## 2477 morgabi02   1884     1    WS7   AA  45 162   8  28   1   1  0  NA  NA NA
    ## 2478 moriage01   1884     1    BSN   NL   4  16   1   1   0   0  0   0  NA NA
    ## 2479 moriage01   1884     2    IN2   AA  10  37   4   8   0   2  0   4  NA NA
    ## 2480  morrie01   1884     1    BLU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2481 morried01   1884     1    CL5   AA  57 199  19  37   4   8  0  NA  NA NA
    ## 2482 morrijo01   1884     1    BSN   NL 111 438  80 114  19   7  3  61  NA NA
    ## 2483 morrijo03   1884     1    IN2   AA  44 182  26  48   6   8  1  NA  NA NA
    ## 2484  morrip01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2485 morrito01   1884     1    MLU   UA  12  47   3   8   2   0  0  NA  NA NA
    ## 2486 mortoch01   1884     1    TL1   AA  32 111  11  18   6   2  0  NA  NA NA
    ## 2487 mortosp01   1884     1    PHI   NL   2   8   0   3   1   0  0   0  NA NA
    ## 2488 mountbi01   1884     1    CN2   AA  34 119  13  18   2   1  0   8  NA NA
    ## 2489 mountfr01   1884     1    CL5   AA  58 210  26  50   7   3  4  NA  NA NA
    ## 2490 moynami01   1884     1    PH4   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 2491 moynami01   1884     2    CL2   NL  12  45   9  13   2   1  0   6  NA NA
    ## 2492 muldomi01   1884     1    CL2   NL 110 422  46 101  16   6  2  38  NA NA
    ## 2493 mullato01   1884     1    TL1   AA  95 352  49  97  19   3  3  NA  NA NA
    ## 2494 mullihe01   1884     1    WS7   AA  34 120  13  17   3   1  0  NA  NA NA
    ## 2495 mullihe01   1884     2    BSU   UA   2   8   1   0   0   0  0  NA  NA NA
    ## 2496 mullijo01   1884     1    WSU   UA   1   4   2   1   0   0  0  NA  NA NA
    ## 2497 mulvejo01   1884     1    PHI   NL 100 401  47  92  11   2  2  32  NA NA
    ## 2498 muncejo01   1884     1    WIL   UA   7  21   1   4   0   0  0  NA  NA NA
    ## 2499 mundige01   1884     1    IN2   AA   3   8   1   2   0   0  0   3  NA NA
    ## 2500 murnati01   1884     1    BSU   UA  76 311  55  73   5   2  0  NA  NA NA
    ## 2501   murph01   1884     1    BSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2502 murphco01   1884     1    PHI   NL   3  10   0   0   0   0  0   0  NA NA
    ## 2503 murphjo01   1884     1    ALT   UA  23  94  10  14   1   0  0  NA  NA NA
    ## 2504 murphjo01   1884     2    WIL   UA  10  31   4   2   0   0  0  NA  NA NA
    ## 2505 murphto01   1884     1    NY4   AA   1   3   1   1   0   0  0  NA  NA NA
    ## 2506 murphwi01   1884     1    CL2   NL  42 168  18  38   3   3  1   9  NA NA
    ## 2507 murphwi01   1884     2    WS7   AA   5  21   3  10   0   0  0  NA  NA NA
    ## 2508 murrami01   1884     1    PRO   NL   8  27   1   5   0   0  0   1  NA NA
    ## 2509 myersal01   1884     1    MLU   UA  12  46   6  15   6   0  0  NA  NA NA
    ## 2510 myersge01   1884     1    BFN   NL  78 325  34  59   9   2  2  32  NA NA
    ## 2511 myershe01   1884     1    WIL   UA   6  24   3   3   0   0  0  NA  NA NA
    ## 2512  nashbi01   1884     1    RIC   AA  45 166  31  33   8   8  1  NA  NA NA
    ## 2513  navasa01   1884     1    PRO   NL  34 116  10  11   0   0  0   6  NA NA
    ## 2514 neaglja01   1884     1    PT1   AA  43 148  13  22   6   0  0  NA  NA NA
    ## 2515 nelsobi01   1884     1    PT1   AA   3  12   1   2   0   0  0  NA  NA NA
    ## 2516 nelsoca01   1884     1    NY4   AA 111 432 114 110  15   3  1  NA  NA NA
    ## 2517 nicolhu01   1884     1    SL4   AA 110 442  79 116  14   5  0  NA  NA NA
    ## 2518 noftsge01   1884     1    ALT   UA   7  25   0   1   0   0  0  NA  NA NA
    ## 2519 nolanth01   1884     1    WIL   UA   9  33   5   9   2   1  0  NA  NA NA
    ## 2520  nuszem01   1884     1    WSU   UA   1   4   1   0   0   0  0  NA  NA NA
    ## 2521 oberbhe01   1884     1    BLU   UA  33 125  19  23   4   0  0  NA  NA NA
    ## 2522 oberbhe01   1884     2    KCU   UA  27  90   7  17   3   0  0  NA  NA NA
    ## 2523 obriebi01   1884     1    SPU   UA   8  30   1   7   3   0  0  NA  NA NA
    ## 2524 obriebi01   1884     2    KCU   UA   4  17   2   4   0   0  0  NA  NA NA
    ## 2525 obrieja01   1884     1    PH4   AA  36 138  25  39   6   1  1  NA  NA NA
    ## 2526 obriejo01   1884     1    BLU   UA  18  77   7  19   1   1  0  NA  NA NA
    ## 2527 obrieto01   1884     1    BSU   UA 103 449  80 118  31   8  4  NA  NA NA
    ## 2528  odayha01   1884     1    TL1   AA  64 242  23  51   9   1  0  NA  NA NA
    ## 2529 odonnjo01   1884     1    PHU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2530 olearda01   1884     1    CNU   UA  32 132  14  34   0   2  1  NA  NA NA
    ## 2531  olinfr01   1884     1    WS7   AA  21  83  12  32   4   1  0  NA  NA NA
    ## 2532  olinfr01   1884     2    WSU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2533  olinfr01   1884     3    TL1   AA  26  86  16  22   0   1  1  NA  NA NA
    ## 2534 oneilti01   1884     1    SL4   AA  78 297  49  82  13  11  3  54  NA NA
    ## 2535 orourji01   1884     1    BFN   NL 108 467 119 162  33   7  5  63  NA NA
    ## 2536   orrda01   1884     1    NY4   AA 110 458  82 162  32  13  9 112  NA NA
    ## 2537 oxleyhe01   1884     1    NY1   NL   2   4   0   0   0   0  0   0  NA NA
    ## 2538 oxleyhe01   1884     2    NY4   AA   1   3   0   0   0   0  0  NA  NA NA
    ## 2539 pattige01   1884     1    PHU   UA   2   7   0   1   0   0  0  NA  NA NA
    ## 2540  peakel01   1884     1    BSU   UA   1   3   2   2   0   0  0  NA  NA NA
    ## 2541  peakel01   1884     2    PHU   UA  54 215  35  42   6   4  0  NA  NA NA
    ## 2542 peltzjo01   1884     1    IN2   AA 106 393  40  86  13  17  3  NA  NA NA
    ## 2543 peoplji01   1884     1    CN2   AA  69 267  28  45   2   2  1  16  NA NA
    ## 2544 peterjo01   1884     1    PT1   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 2545 pfefffr01   1884     1    CHN   NL 112 467 105 135  10  10 25 101  NA NA
    ## 2546 pheladi01   1884     1    BLU   UA 101 402  63  99  13   3  3  NA  NA NA
    ## 2547 phillbi01   1884     1    CL2   NL 111 464  58 128  25  12  3  46  NA NA
    ## 2548 phillma01   1884     1    IN2   AA  97 413  41 111  18   8  0  NA  NA NA
    ## 2549 piercgr01   1884     1    NY4   AA   5  20   2   5   1   0  0  NA  NA NA
    ## 2550 piercma01   1884     1    WSU   UA   2   7   0   1   0   0  0  NA  NA NA
    ## 2551 pinknge01   1884     1    CL2   NL  36 144  18  45   9   0  0  16  NA NA
    ## 2552 poormto01   1884     1    TL1   AA  94 382  56  89   8   7  0  NA  NA NA
    ## 2553 portehe01   1884     1    MLU   UA  11  40   3  11   3   0  0  NA  NA NA
    ## 2554 portema01   1884     1    KCU   UA   3  12   1   1   1   0  0  NA  NA NA
    ## 2555 powelab01   1884     1    WSU   UA  48 191  36  54  10   5  0  NA  NA NA
    ## 2556 powelji01   1884     1    RIC   AA  41 151  23  37   8   4  0  NA  NA NA
    ## 2557 powelma01   1884     1    CNU   UA  43 185  46  59   4   2  1  NA  NA NA
    ## 2558 powerph01   1884     1    CN2   AA  35 133  10  18   1   0  0   8  NA NA
    ## 2559 princwa01   1884     1    DTN   NL   7  21   0   3   0   0  0   1  NA NA
    ## 2560 princwa01   1884     2    WS7   AA  43 166  22  36   3   2  1  NA  NA NA
    ## 2561 princwa01   1884     3    WSU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2562 purcebl01   1884     1    PHI   NL 103 428  67 108  11   7  1  31  NA NA
    ## 2563  pylesh01   1884     1    PHI   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2564 questjo01   1884     1    SL4   AA  81 310  46  64   9   5  0  NA  NA NA
    ## 2565 questjo01   1884     2    PT1   AA  12  43   2   9   3   0  0  NA  NA NA
    ## 2566 quinnjo02   1884     1    SLU   UA 103 429  74 116  21   1  0  NA  NA NA
    ## 2567 quintma01   1884     1    RIC   AA  26  94  12  22   5   0  0  NA  NA NA
    ## 2568 radboch01   1884     1    PRO   NL  87 361  48  83   7   1  1  37  NA NA
    ## 2569 radfopa01   1884     1    PRO   NL  97 355  56  70  11   2  1  29  NA NA
    ## 2570 recciph01   1884     1    LS2   AA  73 263  23  63   9   2  3  21  NA NA
    ## 2571 reedeic01   1884     1    CN2   AA   3  14   0   2   0   0  0  NA  NA NA
    ## 2572 reedeic01   1884     2    WSU   UA   3  12   0   2   0   0  0  NA  NA NA
    ## 2573  reidbi01   1884     1    PT1   AA  19  70  11  17   2   0  0  NA  NA NA
    ## 2574 reillch01   1884     1    BSU   UA   3  11   1   0   0   0  0  NA  NA NA
    ## 2575 reilljo01   1884     1    CN2   AA 105 448 114 152  24  19 11  91  NA NA
    ## 2576 reipsch01   1884     1    NY4   AA  59 233  21  56  13   2  0  NA  NA NA
    ## 2577 reisich01   1884     1    IN2   AA   2   8   0   0   0   0  0  NA  NA NA
    ## 2578 remseja01   1884     1    PHI   NL  12  43   9   9   2   0  0   3  NA NA
    ## 2579 remseja01   1884     2    BR3   AA  81 301  45  67   6   6  3  NA  NA NA
    ## 2580   richa01   1884     1    CHU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2581 richada01   1884     1    NY1   NL  74 277  36  70   8   1  1  27  NA NA
    ## 2582 richaha01   1884     1    BFN   NL 102 439  85 132  27   9  6  60  NA NA
    ## 2583 richmjo01   1884     1    CL5   AA 105 398  57 100  13   7  3  NA  NA NA
    ## 2584 ricklch01   1884     1    PHU   UA   6  25   5   5   2   0  0  NA  NA NA
    ## 2585 ringofr01   1884     1    PHI   NL  26  91   4  12   2   0  0   6  NA NA
    ## 2586 ringofr01   1884     2    PH4   AA   2   6   0   0   0   0  0  NA  NA NA
    ## 2587 robinch01   1884     1    IN2   AA  20  80  11  23   2   0  0  NA  NA NA
    ## 2588 robinfr01   1884     1    CNU   UA   3  13   1   3   0   0  0  NA  NA NA
    ## 2589 robinya01   1884     1    BLU   UA 102 415 101 111  24   4  3  NA  NA NA
    ## 2590 rollibi01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2591 rosemch01   1884     1    NY4   AA 107 436  97 130  16  11  4  NA  NA NA
    ## 2592  roweda01   1884     1    SLU   UA 109 485  95 142  32  11  4  NA  NA NA
    ## 2593  roweja01   1884     1    BFN   NL  93 400  85 126  14  14  4  61  NA NA
    ## 2594 rowened01   1884     1    PH4   AA   4  15   4   6   1   0  0   1  NA NA
    ## 2595 roxbuji01   1884     1    BL2   AA   2   4   1   2   0   0  0  NA  NA NA
    ## 2596 ruddejo01   1884     1    BSU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2597  ryanjo02   1884     1    BLU   UA   7  25   2   2   0   0  0  NA  NA NA
    ## 2598  ryanjo03   1884     1    WSU   UA   7  28   2   4   0   1  0  NA  NA NA
    ## 2599  ryanjo03   1884     2    WIL   UA   2   6   0   1   0   0  0  NA  NA NA
    ## 2600 ryderto01   1884     1    SLU   UA   8  28   4   7   1   0  0  NA  NA NA
    ## 2601 santred01   1884     1    DTN   NL   6  22   1   4   0   0  0   0  NA NA
    ## 2602   sayji01   1884     1    WIL   UA  16  59   3  13   1   2  0  NA  NA NA
    ## 2603   sayji01   1884     2    KCU   UA   2   8   0   2   0   0  0  NA  NA NA
    ## 2604   saylo01   1884     1    BLU   UA  78 339  65  81  14   2  2  NA  NA NA
    ## 2605   saylo01   1884     2    KCU   UA  17  70   6  14   2   0  1  NA  NA NA
    ## 2606 scanlpa01   1884     1    BSU   UA   6  24   2   7   1   0  0  NA  NA NA
    ## 2607 schenbi01   1884     1    RIC   AA  42 151  14  31   4   0  3  NA  NA NA
    ## 2608 schoeju01   1884     1    CHU   UA  90 366  56 116  22   2  2  NA  NA NA
    ## 2609 schoeju01   1884     2    BLU   UA  16  60   5  15   2   0  0  NA  NA NA
    ## 2610 schwabi01   1884     1    CNU   UA  29 106  14  25   4   0  1  NA  NA NA
    ## 2611   scott01   1884     1    BLU   UA  13  53  10  12   1   1  1  NA  NA NA
    ## 2612 scottmi01   1884     1    DTN   NL 110 438  29 108  17   5  3  50  NA NA
    ## 2613 seeryem01   1884     1    BLU   UA 105 463 113 144  25   7  2  NA  NA NA
    ## 2614 seeryem01   1884     2    KCU   UA   1   4   2   2   1   0  0  NA  NA NA
    ## 2615 seradbi01   1884     1    BFN   NL  37 137  12  24   2   1  0   9  NA NA
    ## 2616 sextoto01   1884     1    MLU   UA  12  47   9  11   2   0  0  NA  NA NA
    ## 2617  shafff01   1884     1    ALT   UA   6  19   1   3   0   0  0  NA  NA NA
    ## 2618 shaffor01   1884     1    SLU   UA 106 467 130 168  40  10  2  NA  NA NA
    ## 2619 shaffta01   1884     1    ALT   UA  13  55  10  18   2   0  0  NA  NA NA
    ## 2620 shaffta01   1884     2    KCU   UA  44 164  18  28   3   2  0  NA  NA NA
    ## 2621 shaffta01   1884     3    BLU   UA   3  13   1   1   0   0  0  NA  NA NA
    ## 2622 shallgu01   1884     1    CN2   AA  23  84   3   3   0   0  0   3  NA NA
    ## 2623  shawdu01   1884     1    DTN   NL  36 136  16  26   4   1  1   8  NA NA
    ## 2624  shawdu01   1884     2    BSU   UA  44 153  13  37   8   0  0  NA  NA NA
    ## 2625 shoupjo01   1884     1    WSU   UA   1   4   1   3   0   0  0  NA  NA NA
    ## 2626 siegejo01   1884     1    PHU   UA   8  31   4   7   2   0  0  NA  NA NA
    ## 2627 siffefr01   1884     1    PH4   AA   7  17   3   3   1   0  0   3  NA NA
    ## 2628 sixsmed01   1884     1    PHI   NL   1   2   0   0   0   0  0   0  NA NA
    ## 2629 skinnal01   1884     1    BLU   UA   1   3   0   1   0   0  0  NA  NA NA
    ## 2630 skinnal01   1884     2    CHU   UA   1   3   1   1   0   0  0  NA  NA NA
    ## 2631 sladear01   1884     1    BSU   UA   2   7   0   0   0   0  0  NA  NA NA
    ## 2632 slattmi01   1884     1    BSU   UA 106 413  60  86   6   2  0  NA  NA NA
    ## 2633   smith01   1884     1    BLU   UA   1   5   1   1   0   0  0  NA  NA NA
    ## 2634 smithbi02   1884     1    CL2   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2635 smithed01   1884     1    WS7   AA  14  57   5   5   0   1  0  NA  NA NA
    ## 2636 smithed05   1884     1    BLU   UA   9  34   2   5   0   0  0  NA  NA NA
    ## 2637 smithfr01   1884     1    PT1   AA  10  36   3   9   0   1  0  NA  NA NA
    ## 2638 smithge01   1884     1    ALT   UA  25 108   9  34   8   1  0  NA  NA NA
    ## 2639 smithge01   1884     2    CL2   NL  72 291  31  74  14   4  4  26  NA NA
    ## 2640 smithph01   1884     1    PH4   AA   1   4   1   1   0   0  0  NA  NA NA
    ## 2641 smithph01   1884     2    PT1   AA   1   4   0   0   0   0  0  NA  NA NA
    ## 2642 smithpo01   1884     1    CL5   AA 108 445  78 106  18  10  6  NA  NA NA
    ## 2643 sneedjo01   1884     1    IN2   AA  27 102  14  22   4   0  1  NA  NA NA
    ## 2644 snydepo01   1884     1    CN2   AA  67 268  32  69   9   9  0  39  NA NA
    ## 2645 snydere01   1884     1    WIL   UA  17  52   4  10   0   0  0  NA  NA NA
    ## 2646 sommejo01   1884     1    BL2   AA 107 479  96 129  11  10  4  NA  NA NA
    ## 2647 stanljo01   1884     1    BLU   UA   6  21   3   5   1   0  0  NA  NA NA
    ## 2648 startjo01   1884     1    PRO   NL  93 381  80 105  10   5  2  32  NA NA
    ## 2649 stearec01   1884     1    BL2   AA 100 396  61  94  12   3  3  NA  NA NA
    ## 2650 stockle01   1884     1    LS2   AA   2   9   0   1   0   0  0  NA  NA NA
    ## 2651 stoveha01   1884     1    PH4   AA 104 448 124 146  22  23 10  83  NA NA
    ## 2652 straujo02   1884     1    KCU   UA  16  60   4  12   3   0  0  NA  NA NA
    ## 2653 striccu01   1884     1    PH4   AA 107 399  59  92  16  11  1  NA  NA NA
    ## 2654 striege01   1884     1    SL4   AA  48 184  22  37   5   2  2  NA  NA NA
    ## 2655 striege01   1884     2    KCU   UA  15  56   5   6   5   0  0  NA  NA NA
    ## 2656 striege01   1884     3    CHU   UA  15  53   6  11   5   0  0  NA  NA NA
    ## 2657 striege01   1884     4    CL2   NL   8  29   2   7   2   0  0   0  NA NA
    ## 2658 struval01   1884     1    SL4   AA   2   7   2   2   0   0  0  NA  NA NA
    ## 2659  suckto01   1884     1    CHU   UA  53 188  18  28   2   0  0  NA  NA NA
    ## 2660  suckto01   1884     2    BLU   UA   3  10   2   3   0   0  0  NA  NA NA
    ## 2661 sullida01   1884     1    LS2   AA  63 247  27  59   8   6  0  26  NA NA
    ## 2662 sullifl01   1884     1    PT1   AA  54 189  14  29   2   1  0  NA  NA NA
    ## 2663 sullipa01   1884     1    KCU   UA  31 114  15  22   3   1  0  NA  NA NA
    ## 2664 sullisl01   1884     1    SLU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2665 sullite01   1884     1    KCU   UA   3   9   0   3   0   0  0  NA  NA NA
    ## 2666 sullito01   1884     1    CL5   AA   4  11   1   1   0   0  0  NA  NA NA
    ## 2667 sulliwi01   1884     1    SLU   UA   1   5   0   1   0   0  0  NA  NA NA
    ## 2668 sundabi01   1884     1    CHN   NL  43 176  25  39   4   1  4  28  NA NA
    ## 2669 sutclsy01   1884     1    CHN   NL   4  15   4   3   1   0  0   2  NA NA
    ## 2670 suttoez01   1884     1    BSN   NL 110 468 102 162  28   7  3  61  NA NA
    ## 2671  swanan01   1884     1    WS7   AA   5  21   3   3   1   0  0  NA  NA NA
    ## 2672  swanan01   1884     2    RIC   AA   3  10   2   5   0   0  0  NA  NA NA
    ## 2673 swarted01   1884     1    PT1   AA 102 399  74 115  19   6  0  NA  NA NA
    ## 2674 sweenbi01   1884     1    BLU   UA  74 296  35  71   7   0  0  NA  NA NA
    ## 2675 sweench01   1884     1    PRO   NL  41 168  24  50   9   0  1  19  NA NA
    ## 2676 sweench01   1884     2    SLU   UA  45 171  31  54  14   2  1  NA  NA NA
    ## 2677 sweenje01   1884     1    KCU   UA  31 129  16  34   3   0  0  NA  NA NA
    ## 2678 sweenro01   1884     1    BLU   UA  48 186  37  42   7   1  0  NA  NA NA
    ## 2679 sylvelo01   1884     1    CNU   UA  82 333  67  89  13   8  2  NA  NA NA
    ## 2680 taylobi01   1884     1    SLU   UA  43 186  44  68  23   1  3  NA  NA NA
    ## 2681 taylobi01   1884     2    PH4   AA  30 111   8  28   6   2  0  NA  NA NA
    ## 2682 tayloli01   1884     1    PT1   AA  41 152  22  32   4   1  0  NA  NA NA
    ## 2683 tennefr01   1884     1    WSU   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2684 tennefr01   1884     2    BSU   UA   4  17   1   2   0   0  0  NA  NA NA
    ## 2685 tennefr01   1884     3    WIL   UA   1   3   0   0   0   0  0  NA  NA NA
    ## 2686 terryad01   1884     1    BR3   AA  67 236  15  55  10   3  0  NA  NA NA
    ## 2687 thomptu01   1884     1    IN2   AA  24  97  10  20   3   0  0  NA  NA NA
    ## 2688 tiernbi01   1884     1    BLU   UA   1   3   0   1   0   0  0  NA  NA NA
    ## 2689 tillejo01   1884     1    TL1   AA  17  56   5  10   2   0  0  NA  NA NA
    ## 2690 tillejo01   1884     2    SPU   UA   9  26   2   4   1   0  0  NA  NA NA
    ## 2691 tinneth01   1884     1    WSU   UA  32 119  17  28   3   1  0  NA  NA NA
    ## 2692 traffbi01   1884     1    BL2   AA  53 210  25  37   4   6  0  NA  NA NA
    ## 2693  trayji01   1884     1    IN2   AA   6  21   2   6   0   0  0  NA  NA NA
    ## 2694 trottsa01   1884     1    BL2   AA  71 284  36  73  17   9  3  NA  NA NA
    ## 2695  troyda01   1884     1    NY4   AA 107 421  80 111  22  10  2  NA  NA NA
    ## 2696 trumbed01   1884     1    WS7   AA  25  86   5  10   2   0  0  NA  NA NA
    ## 2697 turbije01   1884     1    KCU   UA  13  49   5  11   4   0  0  NA  NA NA
    ## 2698 vadebge01   1884     1    PHI   NL   4  14   1   3   0   0  0   3  NA NA
    ## 2699 veachpe01   1884     1    KCU   UA  27  82   9  11   1   0  1  NA  NA NA
    ## 2700 vintobi01   1884     1    PHI   NL  21  78   9   9   1   0  0   4  NA NA
    ## 2701  vossal01   1884     1    WSU   UA  63 245  33  47   9   0  0  NA  NA NA
    ## 2702  vossal01   1884     2    KCU   UA  14  45   1   4   0   0  0  NA  NA NA
    ## 2703 walkefl01   1884     1    TL1   AA  42 152  23  40   2   3  0  NA  NA NA
    ## 2704 walkeos01   1884     1    BR3   AA  95 382  59 103  12   8  2  NA  NA NA
    ## 2705 walkewa01   1884     1    DTN   NL   1   4   1   1   0   0  0   0  NA NA
    ## 2706 walkewe01   1884     1    TL1   AA   5  18   1   4   1   0  0   2  NA NA
    ## 2707  wardjo01   1884     1    NY1   NL 113 482  98 122  11   8  2  51  NA NA
    ## 2708  wardjo02   1884     1    WSU   UA   1   4   0   1   0   0  0  NA  NA NA
    ## 2709 warnefr01   1884     1    BR3   AA  84 352  40  78   4   0  1  NA  NA NA
    ## 2710 watkibi01   1884     1    IN2   AA  35 127  16  26   4   0  0  NA  NA NA
    ## 2711 weavesa01   1884     1    PHU   UA  20  84  11  18   2   0  0  NA  NA NA
    ## 2712 weberha01   1884     1    IN2   AA   3   8   0   0   0   0  0  NA  NA NA
    ## 2713 weberjo01   1884     1    DTN   NL   2   8   0   0   0   0  0   0  NA NA
    ## 2714 weihepo01   1884     1    IN2   AA  63 256  29  65  13   2  4  NA  NA NA
    ## 2715 welchcu01   1884     1    TL1   AA 109 425  61  95  24   5  0  NA  NA NA
    ## 2716 welchmi01   1884     1    NY1   NL  71 249  47  60  14   3  3  29  NA NA
    ## 2717 werdepe01   1884     1    SLU   UA  18  76   7  18   2   0  0  NA  NA NA
    ## 2718 werrijo01   1884     1    SPU   UA   9  27   3   2   0   0  0  NA  NA NA
    ## 2719  westbu01   1884     1    CN2   AA  33 131  20  32   2   8  1  15  NA NA
    ## 2720 wheelha01   1884     1    SL4   AA   5  19   0   5   2   0  0  NA  NA NA
    ## 2721 wheelha01   1884     2    KCU   UA  14  62  11  16   1   0  0  NA  NA NA
    ## 2722 wheelha01   1884     3    CHU   UA  37 158  29  36   5   3  1  NA  NA NA
    ## 2723 wheelha01   1884     4    BLU   UA  17  69   3  18   2   0  0  NA  NA NA
    ## 2724 whitebi02   1884     1    PT1   AA  74 291  25  66   7  10  0  NA  NA NA
    ## 2725 whitede01   1884     1    BFN   NL 110 452  82 147  16  11  5  74  NA NA
    ## 2726 whitegu01   1884     1    CL2   NL   8  34   4   5   0   0  0   0  NA NA
    ## 2727 whitemi01   1884     1    SLU   UA  99 393  61  83  15   1  1  NA  NA NA
    ## 2728 whitemi01   1884     2    KCU   UA   5  22   2   3   0   0  0  NA  NA NA
    ## 2729 whitewa01   1884     1    WSU   UA   4  18   2   1   0   0  0  NA  NA NA
    ## 2730 whitewi01   1884     1    CN2   AA  52 184  28  35   1   2  1  11  NA NA
    ## 2731 whitied01   1884     1    LS2   AA  42 157  16  35   7   3  0  18  NA NA
    ## 2732 whitnar01   1884     1    PT1   AA  23  94  10  28   4   0  0  NA  NA NA
    ## 2733 whitnji01   1884     1    BSN   NL  66 270  41  70  17   5  3  40  NA NA
    ## 2734 wiedmst01   1884     1    DTN   NL  81 300  24  49   6   0  0  26  NA NA
    ## 2735   wiley01   1884     1    WSU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2736 willine01   1884     1    CHN   NL 107 417  84 116  18   8 27  84  NA NA
    ## 2737 williwa01   1884     1    RIC   AA   2   8   0   2   0   0  0  NA  NA NA
    ## 2738   wills01   1884     1    WS7   AA   4  15   1   2   2   0  0  NA  NA NA
    ## 2739   wills01   1884     2    KCU   UA   5  21   2   3   1   0  0  NA  NA NA
    ## 2740 wilsotu01   1884     1    BR3   AA  24  82  13  19   4   0  0  NA  NA NA
    ## 2741  wisebi01   1884     1    WSU   UA  85 339  51  79  17   1  2  NA  NA NA
    ## 2742  wisesa01   1884     1    BSN   NL 114 426  60  91  15   9  4  41  NA NA
    ## 2743  wolfji01   1884     1    LS2   AA 110 486  79 146  24  11  3  73  NA NA
    ## 2744  woodfr01   1884     1    DTN   NL  12  42   4   2   0   0  0   1  NA NA
    ## 2745  woodge01   1884     1    DTN   NL 114 473  79 119  16  10  8  29  NA NA
    ## 2746 woulfji01   1884     1    CN2   AA   8  34   3   5   0   1  0   2  NA NA
    ## 2747 woulfji01   1884     2    PT1   AA  15  53   7   6   1   0  0   1  NA NA
    ## 2748 wymanfr01   1884     1    KCU   UA  30 124  16  27   4   0  0  NA  NA NA
    ## 2749 wymanfr01   1884     2    CHU   UA   2   8   1   3   0   0  0  NA  NA NA
    ## 2750 yeweled01   1884     1    WS7   AA  27  93  14  23   3   1  0  NA  NA NA
    ## 2751 yeweled01   1884     2    WSU   UA   1   4   0   0   0   0  0  NA  NA NA
    ## 2752  yorkto01   1884     1    BL2   AA  83 314  64  70  14   7  1  NA  NA NA
    ## 2753 zimmech01   1884     1    DTN   NL   8  29   0   2   1   0  0   0  NA NA
    ## 2754 alvorbi01   1885     1    SL5   NL   2   5   0   0   0   0  0   0  NA NA
    ## 2755 andreed01   1885     1    PHI   NL 103 421  77 112  15   3  0  23  NA NA
    ## 2756 andruwi01   1885     1    PRO   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2757 ansonca01   1885     1    CHN   NL 112 464 100 144  35   7  7 108  NA NA
    ## 2758 bakerge01   1885     1    SL5   NL  38 131   5  16   0   0  0   5  NA NA
    ## 2759 bakerno01   1885     1    LS2   AA  25  87  15  18   2   0  0   5  NA NA
    ## 2760 baldwki01   1885     1    CN2   AA  34 126   9  17   1   0  1   8  NA NA
    ## 2761 baldwla01   1885     1    DTN   NL  31 124  12  30   6   3  0  18  NA NA
    ## 2762 barklsa01   1885     1    SL4   AA 106 418  67 112  18  10  3  53  NA NA
    ## 2763 bassech01   1885     1    PRO   NL  82 285  21  41   8   2  0  16  NA NA
    ## 2764 bastich01   1885     1    PHI   NL 103 389  63  65  11   5  4  29  NA NA
    ## 2765 becanbu01   1885     1    NY4   AA  10  33   3  10   0   0  0   2  NA NA
    ## 2766 begleed01   1885     1    NY4   AA  15  52   5   9   1   0  1   3  NA NA
    ## 2767  bellfr01   1885     1    BR3   AA  10  29   5   5   0   1  0   2  NA NA
    ## 2768 bennech01   1885     1    DTN   NL  91 349  49  94  24  13  5  60  NA NA
    ## 2769 boylehe01   1885     1    SL5   NL  72 258  24  52   9   1  1  21  NA NA
    ## 2770 bradyst01   1885     1    NY4   AA 108 434  60 128  14   5  3  58  NA NA
    ## 2771 brennji01   1885     1    SL5   NL   3  10   0   1   0   0  0   1  NA NA
    ## 2772 briodfa01   1885     1    SL5   NL  62 215  14  42   9   0  1  17  NA NA
    ## 2773 brougca01   1885     1    SL4   AA   4  17   1   1   0   0  0   1  NA NA
    ## 2774 brougca01   1885     2    NY4   AA  11  41   1   6   1   0  0   1  NA NA
    ## 2775 broutda01   1885     1    BFN   NL  98 407  87 146  32  11  7  59  NA NA
    ## 2776 brownjo01   1885     1    BL2   AA   5  19   2   3   0   0  0   0  NA NA
    ## 2777 brownpe01   1885     1    LS2   AA 112 481  98 174  34  10  9  73  NA NA
    ## 2778 brownto01   1885     1    PT1   AA 108 437  81 134  16  12  4  68  NA NA
    ## 2779 bryange01   1885     1    DTN   NL   1   4   0   0   0   0  0   1  NA NA
    ## 2780 buffich01   1885     1    BSN   NL  82 338  26  81  12   3  1  33  NA NA
    ## 2781 burdoja01   1885     1    BSN   NL  45 169  18  24   5   0  0   7  NA NA
    ## 2782 burnsdi01   1885     1    SL5   NL  14  54   2  12   2   1  0   4  NA NA
    ## 2783 burnsoy01   1885     1    BL2   AA  78 321  47  74  11   6  5  37  NA NA
    ## 2784 burnsto01   1885     1    CHN   NL 111 445  82 121  23   9  7  71  NA NA
    ## 2785 bushodo01   1885     1    SL4   AA  85 300  42  80  13   5  0  21  NA NA
    ## 2786 carpehi01   1885     1    CN2   AA 112 473  89 131  12   8  2  61  NA NA
    ## 2787 carrocl01   1885     1    PRO   NL 104 426  62  99  12   3  1  40  NA NA
    ## 2788 carrofr01   1885     1    PT1   AA  71 280  45  75  13   8  0  30  NA NA
    ## 2789 carrosc01   1885     1    BFN   NL  13  40   1   3   0   0  0   1  NA NA
    ## 2790 carutbo01   1885     1    SL4   AA  60 222  37  50  10   2  1  12  NA NA
    ## 2791 caseyda01   1885     1    DTN   NL  12  43   3   5   0   1  0   1  NA NA
    ## 2792 caseyde01   1885     1    BL2   AA  63 264  50  76  10   5  3  29  NA NA
    ## 2793 caskied01   1885     1    SL5   NL  71 262  31  47   3   0  0  12  NA NA
    ## 2794 cassijo01   1885     1    BR3   AA  54 221  36  47   6   2  1  28  NA NA
    ## 2795 clarkjo01   1885     1    CHN   NL  72 283  34  61  11   5  4  32  NA NA
    ## 2796 clemeja01   1885     1    PHI   NL  52 188  14  36  11   3  1  14  NA NA
    ## 2797 clinemo01   1885     1    LS2   AA   2   9   0   2   1   0  0   2  NA NA
    ## 2798 clintji01   1885     1    CN2   AA 105 408  48  97   5   5  0  34  NA NA
    ## 2799 colemjo01   1885     1    PH4   AA  96 398  71 119  15  11  3  70  NA NA
    ## 2800 collich01   1885     1    DTN   NL  14  55   8  10   0   2  0   6  NA NA
    ## 2801 collvbi01   1885     1    BSN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2802 comisch01   1885     1    SL4   AA  83 340  68  87  15   7  2  44  NA NA
    ## 2803 connojo02   1885     1    BFN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2804 connojo02   1885     2    LS2   AA   4  14   0   2   0   0  0   1  NA NA
    ## 2805 connoro01   1885     1    NY1   NL 110 455 102 169  23  15  1  65  NA NA
    ## 2806 conwaji01   1885     1    PH4   AA   2   6   2   0   0   0  0   0  NA NA
    ## 2807 conwape01   1885     1    BFN   NL  29  90   7  10   5   0  1   7  NA NA
    ## 2808 corcola01   1885     1    CHN   NL   7  22   6   6   1   0  0   4  NA NA
    ## 2809 corcola01   1885     2    NY1   NL   3  14   3   5   0   0  0   2  NA NA
    ## 2810 coreyfr01   1885     1    PH4   AA  94 384  61  94  14   8  1  38  NA NA
    ## 2811 corkhpo01   1885     1    CN2   AA 112 440  64 111  10   8  1  53  NA NA
    ## 2812 craneed01   1885     1    PRO   NL   1   2   0   0   0   0  0   0  NA NA
    ## 2813 craneed01   1885     2    BFN   NL  13  51   5  14   0   1  2   9  NA NA
    ## 2814 cranesa01   1885     1    DTN   NL  68 245  23  47   4   6  1  20  NA NA
    ## 2815 crossam01   1885     1    LS2   AA  35 130  11  37   2   1  0  14  NA NA
    ## 2816 crothdo01   1885     1    NY4   AA  18  51  11   8   0   0  0   0  NA NA
    ## 2817 crottjo01   1885     1    LS2   AA  39 129  14  20   2   0  0   7  NA NA
    ## 2818 crowlbi01   1885     1    BFN   NL  92 344  29  83  14   1  1  36  NA NA
    ## 2819 cushmed01   1885     1    PH4   AA  10  37   5   7   1   0  0   2  NA NA
    ## 2820 cushmed01   1885     2    NY4   AA  22  69   5  10   1   0  0   3  NA NA
    ## 2821 cusicto01   1885     1    PHI   NL  39 141  12  25   1   0  0   5  NA NA
    ## 2822 dailyco01   1885     1    PRO   NL  60 223  20  58   6   1  0  19  NA NA
    ## 2823 dailyed01   1885     1    PHI   NL  50 184  22  38   8   2  1  13  NA NA
    ## 2824 dailyhu01   1885     1    SL5   NL  11  35   1   3   0   0  0   1  NA NA
    ## 2825 dalryab01   1885     1    CHN   NL 113 492 109 135  27  12 11  61  NA NA
    ## 2826 davisda01   1885     1    BSN   NL  11  37   4   7   2   0  0   3  NA NA
    ## 2827 dealypa01   1885     1    BSN   NL  35 130  18  29   4   1  1   9  NA NA
    ## 2828 deaslpa01   1885     1    NY1   NL  54 207  22  53   5   1  0  24  NA NA
    ## 2829 dennyje01   1885     1    PRO   NL  83 318  40  71  14   4  3  24  NA NA
    ## 2830 derbyge02   1885     1    BL2   AA  10  31   4   4   0   0  0   2  NA NA
    ## 2831 dickebu01   1885     1    BFN   NL   5  21   1   1   1   0  0   0  NA NA
    ## 2832 dolanto01   1885     1    SL5   NL   3   9   1   2   0   0  0   0  NA NA
    ## 2833 donneji01   1885     1    DTN   NL  56 211  24  49   4   3  1  22  NA NA
    ## 2834 dorgaje01   1885     1    DTN   NL  39 161  23  46   6   2  0  24  NA NA
    ## 2835 dorgami01   1885     1    NY1   NL  89 347  60 113  17   8  0  46  NA NA
    ## 2836 driscde02   1885     1    BFN   NL   7  19   2   3   0   0  0   0  NA NA
    ## 2837 drissmi01   1885     1    SL4   AA   6  20   0   1   0   0  0   0  NA NA
    ## 2838 dunlafr01   1885     1    SL5   NL 106 423  70 114  11   5  2  25  NA NA
    ## 2839  edench01   1885     1    PT1   AA  98 405  57 103  18   6  0  38  NA NA
    ## 2840 eggleda01   1885     1    BFN   NL   6  24   0   2   0   0  0   0  NA NA
    ## 2841 emslibo01   1885     1    BL2   AA  13  51   6  12   1   1  0   4  NA NA
    ## 2842 emslibo01   1885     2    PH4   AA   4  12   1   1   0   0  0   0  NA NA
    ## 2843 esterdu01   1885     1    NY1   NL  88 359  48  92  14   5  2  44  NA NA
    ## 2844 evansja01   1885     1    BL2   AA  20  77  18  17   1   1  0   7  NA NA
    ## 2845 ewingbu01   1885     1    NY1   NL  81 342  81 104  15  12  6  63  NA NA
    ## 2846 farrasi01   1885     1    PHI   NL 111 420  49 103  20   3  3  36  NA NA
    ## 2847 farreja02   1885     1    PRO   NL  68 257  27  53   7   1  1  19  NA NA
    ## 2848 fennefr01   1885     1    CN2   AA 112 454  82 124  14  17 10  89  NA NA
    ## 2849 ferguch01   1885     1    PHI   NL  61 235  42  72   8   3  1  27  NA NA
    ## 2850 fieldji01   1885     1    PT1   AA  56 209  28  50   9   1  1  15  NA NA
    ## 2851 fieldji01   1885     2    BL2   AA  38 144  16  30   3   2  0  10  NA NA
    ## 2852   fishe01   1885     1    BFN   NL   1   4   0   0   0   0  0   0  NA NA
    ## 2853 flintsi01   1885     1    CHN   NL  68 249  27  52   8   2  1  17  NA NA
    ## 2854 fogarji01   1885     1    PHI   NL 111 427  49  99  13   3  0  39  NA NA
    ## 2855 fogarjo01   1885     1    SL5   NL   2   8   1   1   0   0  0   0  NA NA
    ## 2856 foleyjo01   1885     1    PRO   NL   1   2   0   0   0   0  0   0  NA NA
    ## 2857 forceda01   1885     1    BFN   NL  71 253  20  57   6   1  0  15  NA NA
    ## 2858 foremfr01   1885     1    BL2   AA   3  14   4   4   0   1  0   2  NA NA
    ## 2859 forstto01   1885     1    NY4   AA  57 213  28  47   7   2  0  18  NA NA
    ## 2860 foutzda01   1885     1    SL4   AA  65 238  42  59   6   4  0  34  NA NA
    ## 2861 fusseed01   1885     1    PH4   AA   5  19   2   6   1   0  0   2  NA NA
    ## 2862 galvipu01   1885     1    BFN   NL  33 122  14  23   4   2  1  10  NA NA
    ## 2863 galvipu01   1885     2    PT1   AA  11  38   2   4   0   0  0   2  NA NA
    ## 2864 ganzech01   1885     1    PHI   NL  34 125  15  21   3   1  0   6  NA NA
    ## 2865 gardngi01   1885     1    BL2   AA  44 170  22  37   5   4  0  17  NA NA
    ## 2866 gastfed01   1885     1    DTN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2867 gastfed01   1885     2    CHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2868  geerbi01   1885     1    LS2   AA  14  51   2   6   2   0  0   3  NA NA
    ## 2869 gerhajo01   1885     1    NY1   NL 112 399  43  62  12   2  0  33  NA NA
    ## 2870 getzich01   1885     1    DTN   NL  40 137   9  29   3   0  0  16  NA NA
    ## 2871 gillepe01   1885     1    NY1   NL 102 420  67 123  17   6  0  52  NA NA
    ## 2872 gilliba01   1885     1    PRO   NL  71 252  23  54   7   3  0  12  NA NA
    ## 2873 glassja01   1885     1    SL5   NL 111 446  66 125  18   3  1  40  NA NA
    ## 2874 gleasbi01   1885     1    SL4   AA 112 472  79 119   9   5  3  53  NA NA
    ## 2875 gleasja01   1885     1    SL5   NL   2   7   0   1   0   0  0   0  NA NA
    ## 2876  gorege01   1885     1    CHN   NL 109 441 115 138  21  13  5  57  NA NA
    ## 2877 greered01   1885     1    BL2   AA  56 211  32  42   7   0  0  21  NA NA
    ## 2878 gunnito01   1885     1    BSN   NL  48 174  17  32   3   0  0  15  NA NA
    ## 2879 hackeme01   1885     1    BSN   NL  34 115   9  21   7   1  0   4  NA NA
    ## 2880 hackewa01   1885     1    BSN   NL  35 125   8  23   3   0  0   9  NA NA
    ## 2881 hallsch01   1885     1    PRO   NL   1   4   1   0   0   0  0   0  NA NA
    ## 2882 halpiji01   1885     1    DTN   NL  15  54   3   7   2   0  0   1  NA NA
    ## 2883 hankifr01   1885     1    NY4   AA  94 362  43  81  12   2  2  44  NA NA
    ## 2884 hanlone01   1885     1    DTN   NL 105 424  93 128  18   8  1  29  NA NA
    ## 2885 harkijo01   1885     1    BR3   AA  43 159  20  42   4   2  1  15  NA NA
    ## 2886 hatfigi01   1885     1    BFN   NL  11  30   1   4   0   1  0   0  NA NA
    ## 2887 hayesja01   1885     1    BR3   AA  42 137  10  18   3   0  0  10  NA NA
    ## 2888 healyjo01   1885     1    SL5   NL   8  24   0   1   0   0  0   0  NA NA
    ## 2889 heckegu01   1885     1    LS2   AA  70 297  48  81   9   2  2  35  NA NA
    ## 2890 hendeha01   1885     1    BL2   AA  61 229  23  51   5   2  1  21  NA NA
    ## 2891 henglmo01   1885     1    BFN   NL   7  26   2   4   0   0  0   0  NA NA
    ## 2892 henryjo01   1885     1    BL2   AA  10  34   4   9   3   0  0   3  NA NA
    ## 2893 hilanjo01   1885     1    PHI   NL   3   9   0   0   0   0  0   0  NA NA
    ## 2894 hinesmi01   1885     1    BSN   NL  14  56  11  13   4   0  0   4  NA NA
    ## 2895 hinesmi01   1885     2    BR3   AA   3  13   1   1   0   1  0   1  NA NA
    ## 2896 hinesmi01   1885     3    PRO   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2897 hinespa01   1885     1    PRO   NL  98 411  63 111  20   4  1  35  NA NA
    ## 2898 hoffojo01   1885     1    PT1   AA   3   8   1   1   0   0  0   0  NA NA
    ## 2899 holbebi01   1885     1    NY4   AA  56 202  13  35   3   0  0  13  NA NA
    ## 2900 hornujo01   1885     1    BSN   NL  25 109  14  22   4   1  1   7  NA NA
    ## 2901 hotalpe01   1885     1    BR3   AA  94 370  73  95   9   5  1  34  NA NA
    ## 2902 houcksa01   1885     1    PH4   AA  93 388  74  99  10   9  0  54  NA NA
    ## 2903 hughebi01   1885     1    PH4   AA   4  16   3   3   1   1  0   1  NA NA
    ## 2904 irwinar01   1885     1    PRO   NL  59 218  16  39   2   1  0  14  NA NA
    ## 2905 jacobha01   1885     1    BL2   AA  11  43   4   6   2   0  0   1  NA NA
    ## 2906 johnsdi01   1885     1    BSN   NL  26 111  17  26   6   3  1  23  NA NA
    ## 2907   jones03   1885     1    NY4   AA   1   4   0   1   0   0  0   0  NA NA
    ## 2908 jonesch01   1885     1    CN2   AA 112 487 108 157  19  17  5  35  NA NA
    ## 2909 keefeti01   1885     1    NY1   NL  47 166  20  27   1   5  0  12  NA NA
    ## 2910 keenaji01   1885     1    CN2   AA  36 132  16  35   2   2  1  15  NA NA
    ## 2911 kellona01   1885     1    DTN   NL   5  17   4   2   1   0  0   0  NA NA
    ## 2912 kellyki01   1885     1    CHN   NL 107 438 124 126  24   7  9  75  NA NA
    ## 2913 kemmlru01   1885     1    PT1   AA  18  64   2  13   2   1  0   5  NA NA
    ## 2914 kenneed01   1885     1    NY4   AA  96 349  35  71   8   4  2  21  NA NA
    ## 2915 kennete01   1885     1    CHN   NL   9  36   3   3   0   0  0   1  NA NA
    ## 2916 kerinjo01   1885     1    LS2   AA 112 456  65 111   9  16  3  51  NA NA
    ## 2917 kimbesa01   1885     1    PRO   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2918 kirbyjo01   1885     1    SL5   NL  14  50   2   3   0   0  0   0  NA NA
    ## 2919 knighlo01   1885     1    PH4   AA  29 119  17  25   1   1  0  14  NA NA
    ## 2920 knighlo01   1885     2    PRO   NL  25  81   8  13   1   0  0   8  NA NA
    ## 2921 knoufed01   1885     1    PH4   AA  14  48   5   9   0   0  0   2  NA NA
    ## 2922 krehmch01   1885     1    LS2   AA   7  31   4   7   1   1  0   5  NA NA
    ## 2923 krehmch01   1885     2    SL5   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2924 kriegbi01   1885     1    BR3   AA  17  60   7   9   4   0  1   5  NA NA
    ## 2925 kriegbi01   1885     2    CHN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2926 kuehnbi01   1885     1    PT1   AA 104 411  54  93   9  19  0  43  NA NA
    ## 2927 larkihe01   1885     1    PH4   AA 108 453 114 149  37  14  8  88  NA NA
    ## 2928 lathaar01   1885     1    SL4   AA 110 485  84 100  15   3  1  35  NA NA
    ## 2929 levisch01   1885     1    BL2   AA   1   4   2   1   0   0  0   0  NA NA
    ## 2930 lewisfr01   1885     1    SL5   NL  45 181  12  53   9   0  1  27  NA NA
    ## 2931 lilliji01   1885     1    BFN   NL 112 430  49 107  13   3  2  30  NA NA
    ## 2932 lovetto01   1885     1    PH4   AA  16  58   9  13   0   1  0   3  NA NA
    ## 2933 lynchja01   1885     1    NY4   AA  44 153  16  30   5   1  0  10  NA NA
    ## 2934 lynchto01   1885     1    PHI   NL  13  53   7  10   3   0  0   1  NA NA
    ## 2935 lyonsde01   1885     1    PRO   NL   4  16   3   2   1   0  0   1  NA NA
    ## 2936  mackre01   1885     1    LS2   AA  11  41   7  10   1   0  0   5  NA NA
    ## 2937 maculji01   1885     1    BL2   AA 100 320  52  61   7   6  3  26  NA NA
    ## 2938  mannfr01   1885     1    PT1   AA  99 391  60  99  17   6  0  41  NA NA
    ## 2939 mannija01   1885     1    PHI   NL 107 445  61 114  24   4  3  40  NA NA
    ## 2940 manniji01   1885     1    BSN   NL  84 306  34  63   8   9  2  27  NA NA
    ## 2941 manniji01   1885     2    DTN   NL  20  78  15  21   4   0  1   9  NA NA
    ## 2942 manniti01   1885     1    BL2   AA  43 157  17  32   8   1  0  16  NA NA
    ## 2943 manniti01   1885     2    PRO   NL  10  35   3   2   1   0  0   0  NA NA
    ## 2944 mappege01   1885     1    BL2   AA   6  19   2   4   0   1  0   0  NA NA
    ## 2945 maskrle01   1885     1    LS2   AA 109 423  54  97   8  11  1  46  NA NA
    ## 2946 mathebo01   1885     1    PH4   AA  48 179  22  30   3   0  0  12  NA NA
    ## 2947  maysal01   1885     1    LS2   AA  17  61   8  13   1   1  0   4  NA NA
    ## 2948   mccaf01   1885     1    CN2   AA   1   5   0   0   0   0  0   0  NA NA
    ## 2949 mccarto01   1885     1    BSN   NL  40 148  16  27   2   0  0  11  NA NA
    ## 2950 mccauji01   1885     1    BFN   NL  24  84   4  15   2   1  0   7  NA NA
    ## 2951 mccauji01   1885     2    CHN   NL   3   6   1   1   0   0  0   0  NA NA
    ## 2952 mcclebi01   1885     1    BR3   AA 112 464  85 124  22   7  0  46  NA NA
    ## 2953 mccorji01   1885     1    PRO   NL   4  14   2   3   1   0  0   0  NA NA
    ## 2954 mccorji01   1885     2    CHN   NL  25 103  13  23   1   4  0  16  NA NA
    ## 2955 mcdersa01   1885     1    BL2   AA   1   0   0   0   0   0  0   0  NA NA
    ## 2956 mcdonji01   1885     1    BFN   NL   5  14   0   0   0   0  0   0  NA NA
    ## 2957 mcginju01   1885     1    SL4   AA  13  50   3  11   0   0  1   7  NA NA
    ## 2958 mcguide01   1885     1    DTN   NL  34 121  11  23   4   2  0   9  NA NA
    ## 2959 mckeola01   1885     1    CN2   AA  33 121  14  20   3   1  0   8  NA NA
    ## 2960 mckinal01   1885     1    SL5   NL 100 411  42 121  21   6  1  44  NA NA
    ## 2961 mclauto01   1885     1    LS2   AA 112 411  49  87  13   9  2  41  NA NA
    ## 2962 mcphebi01   1885     1    CN2   AA 110 431  78 114  12   4  0  46  NA NA
    ## 2963 mcquemo01   1885     1    DTN   NL  70 278  34  76  15   4  3  30  NA NA
    ## 2964 mcsortr01   1885     1    SL5   NL   2   6   2   3   1   0  0   1  NA NA
    ## 2965 mctamji01   1885     1    BR3   AA  35 131  21  36   7   2  1  13  NA NA
    ## 2966 mcveyge01   1885     1    BR3   AA   6  21   2   3   0   0  0   1  NA NA
    ## 2967 meegape01   1885     1    PT1   AA  19  67   3  13   1   0  0   3  NA NA
    ## 2968 meinkfr01   1885     1    DTN   NL   1   3   0   0   0   0  0   0  NA NA
    ## 2969 milledo01   1885     1    PT1   AA  42 166  19  27   3   1  0  13  NA NA
    ## 2970 millejo02   1885     1    LS2   AA  98 339  44  62   9   5  0  24  NA NA
    ## 2971 millijo01   1885     1    PH4   AA  67 265  35  71  15   4  2  39  NA NA
    ## 2972 mooreje01   1885     1    DTN   NL   6  23   2   4   1   0  0   0  NA NA
    ## 2973 moriage01   1885     1    DTN   NL  11  39   1   1   1   0  0   0  NA NA
    ## 2974 morried01   1885     1    PT1   AA  64 237  19  44   3   3  0  14  NA NA
    ## 2975 morrijo01   1885     1    BSN   NL 111 394  74  89  20   7  4  44  NA NA
    ## 2976 mortoch01   1885     1    DTN   NL  22  79   9  14   1   2  0   3  NA NA
    ## 2977 mountbi01   1885     1    CN2   AA  17  60   7  10   0   0  0   2  NA NA
    ## 2978 mountbi01   1885     2    BL2   AA   7  18   5   1   0   0  0   0  NA NA
    ## 2979 mountfr01   1885     1    PT1   AA   5  20   1   2   0   1  0   1  NA NA
    ## 2980 muldomi01   1885     1    BL2   AA 102 410  47 103  20   6  2  52  NA NA
    ## 2981 mulvejo01   1885     1    PHI   NL 107 443  74 119  25   6  6  64  NA NA
    ## 2982 murrami01   1885     1    LS2   AA  12  43   4   8   0   0  0   3  NA NA
    ## 2983 myersal01   1885     1    PHI   NL  93 357  25  73  13   2  1  28  NA NA
    ## 2984 myersge01   1885     1    BFN   NL  89 326  40  67   7   2  0  19  NA NA
    ## 2985  nashbi01   1885     1    BSN   NL  26  94   9  24   4   0  0  11  NA NA
    ## 2986  navasa01   1885     1    BL2   AA   8  27   2   5   1   0  0   4  NA NA
    ## 2987 nelsoca01   1885     1    NY4   AA 107 420  98 107  12   4  1  30  NA NA
    ## 2988 nicolhu01   1885     1    SL4   AA 112 425  59  88  11   1  0  45  NA NA
    ## 2989 nolanth01   1885     1    PHI   NL   7  26   1   2   1   0  0   1  NA NA
    ## 2990 obrieja01   1885     1    PH4   AA  62 225  35  60   9   1  2  30  NA NA
    ## 2991 obrieto01   1885     1    BL2   AA   8  33   4   7   3   0  0   5  NA NA
    ## 2992  odayha01   1885     1    PT1   AA  13  49   7  12   2   1  0   3  NA NA
    ## 2993 oldfida01   1885     1    BR3   AA  10  25   2   8   1   0  0   2  NA NA
    ## 2994  olinfr01   1885     1    DTN   NL   1   4   1   2   0   0  0   0  NA NA
    ## 2995 oneilti01   1885     1    SL4   AA  52 206  44  72   7   4  3  38  NA NA
    ## 2996 orourji01   1885     1    NY1   NL 112 477 119 143  21  16  5  42  NA NA
    ## 2997   orrda01   1885     1    NY4   AA 107 444  76 152  29  21  6  77  NA NA
    ## 2998   palme01   1885     1    SL5   NL   4  11   1   1   0   0  0   1  NA NA
    ## 2999 pechige01   1885     1    CN2   AA  11  40   3   6   1   1  0   1  NA NA
    ## 3000 peoplji01   1885     1    CN2   AA   7  22   1   4   0   0  0   1  NA NA
    ## 3001 peoplji01   1885     2    BR3   AA  41 151  21  30   4   1  1  15  NA NA
    ## 3002 pfefffr01   1885     1    CHN   NL 112 469  90 113  12   7  5  73  NA NA
    ## 3003 pheladi01   1885     1    BFN   NL   4  16   2   2   0   0  1   3  NA NA
    ## 3004 pheladi01   1885     2    SL5   NL   2   4   1   1   1   0  0   1  NA NA
    ## 3005 phillbi01   1885     1    BR3   AA  99 391  65 118  16  11  3  63  NA NA
    ## 3006 phillma01   1885     1    DTN   NL  33 139  13  29   5   0  0  17  NA NA
    ## 3007 phillma01   1885     2    PT1   AA   4  15   1   4   0   0  0   2  NA NA
    ## 3008 piersdi01   1885     1    NY4   AA   3   9   1   1   0   0  0   0  NA NA
    ## 3009 pinknge01   1885     1    BR3   AA 110 447  77 124  16   5  0  42  NA NA
    ## 3010 poormto01   1885     1    BSN   NL  56 227  44  54   5   3  3  25  NA NA
    ## 3011 portehe01   1885     1    BR3   AA  54 195  28  40   1   4  0  16  NA NA
    ## 3012 powelji01   1885     1    PH4   AA  19  75   5  12   0   3  0   5  NA NA
    ## 3013 powerph01   1885     1    CN2   AA  15  60   6  16   2   0  0   7  NA NA
    ## 3014 powerph01   1885     2    BL2   AA   9  34   6   4   1   0  0   2  NA NA
    ## 3015 purcebl01   1885     1    PH4   AA  66 304  71  90  15   5  0  22  NA NA
    ## 3016 purcebl01   1885     2    BSN   NL  21  87   9  19   1   1  0   3  NA NA
    ## 3017 questjo01   1885     1    DTN   NL  55 200  24  39   8   2  0  21  NA NA
    ## 3018 quinnjo02   1885     1    SL5   NL  97 343  27  73   8   2  0  15  NA NA
    ## 3019 quintma01   1885     1    PH4   AA   7  29   6   6   1   0  0   4  NA NA
    ## 3020 radboch01   1885     1    PRO   NL  66 249  34  58   9   2  0  22  NA NA
    ## 3021 radfopa01   1885     1    PRO   NL 105 371  55  90  12   5  0  32  NA NA
    ## 3022 ramseto01   1885     1    LS2   AA   9  31   2   4   0   0  0   3  NA NA
    ## 3023 recciph01   1885     1    LS2   AA 102 402  57  97   8  10  1  38  NA NA
    ## 3024 reilljo01   1885     1    CN2   AA 111 482  92 143  18  11  5  60  NA NA
    ## 3025 reilljo02   1885     1    NY4   AA  10  40   6   7   3   0  0   3  NA NA
    ## 3026 reipsch01   1885     1    NY4   AA  72 268  29  65  11   1  0  21  NA NA
    ## 3027 richada01   1885     1    NY1   NL  49 198  26  52   9   3  0  25  NA NA
    ## 3028 richaha01   1885     1    BFN   NL  96 426  90 136  19  11  6  44  NA NA
    ## 3029 richmjo01   1885     1    PT1   AA  34 131  14  27   2   2  0  12  NA NA
    ## 3030 ringofr01   1885     1    DTN   NL  17  65  12  16   3   0  0   2  NA NA
    ## 3031 ringofr01   1885     2    PT1   AA   3  11   0   2   0   0  0   0  NA NA
    ## 3032 rittech01   1885     1    BFN   NL   2   6   0   1   0   0  0   0  NA NA
    ## 3033 robinch01   1885     1    BR3   AA  11  40   5   6   2   1  0   4  NA NA
    ## 3034 robinya01   1885     1    SL4   AA  78 287  63  75   8   8  0  35  NA NA
    ## 3035 rosemch01   1885     1    NY4   AA 101 410  72 114  13  14  4  46  NA NA
    ## 3036  roweda01   1885     1    SL5   NL  16  62   8  10   3   0  0   3  NA NA
    ## 3037  roweja01   1885     1    BFN   NL  98 421  62 122  28   8  2  51  NA NA
    ## 3038  ryanji01   1885     1    CHN   NL   3  13   2   6   1   0  0   2  NA NA
    ## 3039 schenbi01   1885     1    BR3   AA   1   4   0   0   0   0  0   0  NA NA
    ## 3040 scottmi01   1885     1    DTN   NL  38 148  14  39   7   0  0  12  NA NA
    ## 3041 scottmi01   1885     2    PT1   AA  55 210  15  52   7   1  0  18  NA NA
    ## 3042 seeryem01   1885     1    SL5   NL  59 216  20  35   7   0  1  14  NA NA
    ## 3043 seradbi01   1885     1    BFN   NL  30 104   8  16   3   0  0   3  NA NA
    ## 3044 sewared01   1885     1    PRO   NL   1   3   0   0   0   0  0   0  NA NA
    ## 3045 shaffor01   1885     1    SL5   NL  69 257  30  50  11   2  0  18  NA NA
    ## 3046 shaffor01   1885     2    PH4   AA   2   9   1   2   0   1  0   1  NA NA
    ## 3047 shallgu01   1885     1    CN2   AA  13  39   3   5   0   0  0   2  NA NA
    ## 3048  shawdu01   1885     1    PRO   NL  49 165  17  22   2   0  0   9  NA NA
    ## 3049 siffefr01   1885     1    PH4   AA   3  10   0   1   0   0  0   0  NA NA
    ## 3050 smithed01   1885     1    PRO   NL   1   4   0   1   0   0  0   0  NA NA
    ## 3051 smithge01   1885     1    BR3   AA 108 419  63 108  17  11  4  62  NA NA
    ## 3052 smithph01   1885     1    BR3   AA   1   3   0   1   0   0  0   0  NA NA
    ## 3053 smithph01   1885     2    PH4   AA   1   2   0   0   0   0  0   0  NA NA
    ## 3054 smithpo01   1885     1    PT1   AA 106 453  85 113  11  13  0  35  NA NA
    ## 3055 snydepo01   1885     1    CN2   AA  39 152  13  36   4   3  1  19  NA NA
    ## 3056 sommejo01   1885     1    BL2   AA 110 471  84 118  23   6  1  44  NA NA
    ## 3057 stapljo01   1885     1    BFN   NL   7  22   0   1   0   0  0   0  NA NA
    ## 3058 startjo01   1885     1    PRO   NL 101 374  47 103  11   4  0  41  NA NA
    ## 3059 stearec01   1885     1    BL2   AA  67 253  40  47   3   8  1  29  NA NA
    ## 3060 stearec01   1885     2    BFN   NL  30 105   7  21   6   1  0   9  NA NA
    ## 3061 stellbi01   1885     1    PRO   NL   1   4   0   0   0   0  0   0  NA NA
    ## 3062 stemmbi01   1885     1    BSN   NL   2   7   1   3   1   0  0   2  NA NA
    ## 3063 stoveha01   1885     1    PH4   AA 112 486 130 153  27   9 13  75  NA NA
    ## 3064 straujo02   1885     1    LS2   AA   2   6   0   1   0   0  0   0  NA NA
    ## 3065 striccu01   1885     1    PH4   AA 106 398  71  93   9   3  1  41  NA NA
    ## 3066 striege01   1885     1    PH4   AA  44 175  19  48   8   5  0  27  NA NA
    ## 3067 sullida01   1885     1    LS2   AA  13  44   3   8   1   0  0   4  NA NA
    ## 3068 sullida01   1885     2    SL4   AA  17  60   4   7   2   0  0   3  NA NA
    ## 3069 sundabi01   1885     1    CHN   NL  46 172  36  44   3   3  2  20  NA NA
    ## 3070 sutclsy01   1885     1    CHN   NL  11  43   5   8   1   1  0   4  NA NA
    ## 3071 sutclsy01   1885     2    SL5   NL  16  49   2   6   1   0  0   4  NA NA
    ## 3072 suttoez01   1885     1    BSN   NL 110 457  78 143  23   8  4  47  NA NA
    ## 3073 swarted01   1885     1    BR3   AA  99 399  80 106   8   9  0  49  NA NA
    ## 3074 sweench01   1885     1    SL5   NL  71 267  27  55   7   1  0  24  NA NA
    ## 3075 sweenro01   1885     1    SL5   NL   3  11   1   1   0   0  0   0  NA NA
    ## 3076  tatepo01   1885     1    BSN   NL   4  13   1   2   0   0  0   2  NA NA
    ## 3077 taylobi01   1885     1    PH4   AA   6  21   0   4   0   0  0   2  NA NA
    ## 3078 tenerjo01   1885     1    BL2   AA   1   4   0   0   0   0  0   0  NA NA
    ## 3079 terryad01   1885     1    BR3   AA  71 264  23  45   1   3  1  20  NA NA
    ## 3080 thompsa01   1885     1    DTN   NL  63 254  58  77  11   9  7  44  NA NA
    ## 3081 traffbi01   1885     1    BL2   AA  69 254  27  39   4   5  1  20  NA NA
    ## 3082 trottsa01   1885     1    BL2   AA  21  88  12  24   2   2  0  12  NA NA
    ## 3083  troyda01   1885     1    NY4   AA  45 177  24  39   3   3  2  12  NA NA
    ## 3084 vintobi01   1885     1    PHI   NL   9  30   2   2   0   0  0   1  NA NA
    ## 3085 vintobi01   1885     2    PH4   AA   7  26   5   4   2   0  0   4  NA NA
    ## 3086 visnejo01   1885     1    BL2   AA   4  13   2   3   0   0  0   2  NA NA
    ## 3087 walkeos01   1885     1    BL2   AA   4  13   1   0   0   0  0   1  NA NA
    ## 3088  wardjo01   1885     1    NY1   NL 111 446  72 101   8   9  0  37  NA NA
    ## 3089  wardjo03   1885     1    PRO   NL   1   3   0   0   0   0  0   0  NA NA
    ## 3090 welchcu01   1885     1    SL4   AA 112 432  84 117  18   8  3  69  NA NA
    ## 3091 welchmi01   1885     1    NY1   NL  56 199  28  41   8   0  2  19  NA NA
    ## 3092 wetzesh01   1885     1    BL2   AA   2   7   0   0   0   0  0   1  NA NA
    ## 3093 whitede01   1885     1    BFN   NL  98 404  54 118   6   6  0  57  NA NA
    ## 3094 whitegu01   1885     1    BSN   NL  33 135  14  25   2   2  1   7  NA NA
    ## 3095 whitewi01   1885     1    CN2   AA  34 118   9  20   5   0  0  10  NA NA
    ## 3096 whitnar01   1885     1    PT1   AA  90 373  53  87  10   4  0  28  NA NA
    ## 3097 whitnji01   1885     1    BSN   NL  72 290  35  68   8   4  0  36  NA NA
    ## 3098 wiedmst01   1885     1    DTN   NL  44 153   7  24   2   1  1  14  NA NA
    ## 3099 willine01   1885     1    CHN   NL 113 407  87  97  16   5  3  65  NA NA
    ## 3100 williwa01   1885     1    CHN   NL   1   4   0   1   0   0  0   0  NA NA
    ## 3101  wisesa01   1885     1    BSN   NL 107 424  71 120  20  10  4  46  NA NA
    ## 3102  wolfji01   1885     1    LS2   AA 112 483  79 141  23  17  1  52  NA NA
    ## 3103  woodfr01   1885     1    BFN   NL   1   4   0   1   0   0  0   0  NA NA
    ## 3104  woodge01   1885     1    DTN   NL  82 362  62 105  19   8  5  28  NA NA
    ## 3105  woodpe01   1885     1    BFN   NL  28 104  10  23   3   1  0   5  NA NA
    ## 3106  yorkto01   1885     1    BL2   AA  22  87   6  23   4   2  0  12  NA NA
    ## 3107 allenmy01   1886     1    BSN   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3108 andreed01   1886     1    PHI   NL 107 437  93 109  15   4  2  28  56 NA
    ## 3109 ansonca01   1886     1    CHN   NL 125 504 117 187  35  11 10 147  29 NA
    ## 3110 atkinal01   1886     1    PH4   AA  45 148  27  18   1   1  0   9   4 NA
    ## 3111 aydelja01   1886     1    PH4   AA   2   6   0   0   0   0  0   0   0 NA
    ## 3112 bakerge01   1886     1    KCN   NL   1   4   1   1   0   0  0   0   0 NA
    ## 3113 bakerph01   1886     1    WS8   NL  81 325  37  72   6   5  1  34  16 NA
    ## 3114 baldwki01   1886     1    CN2   AA  87 315  41  72   8   7  3  32  12 NA
    ## 3115 baldwla01   1886     1    DTN   NL  57 204  25  41   6   3  0  25   3 NA
    ## 3116 barklsa01   1886     1    PT1   AA 122 478  77 127  31   8  1  69  22 NA
    ## 3117 barnibi01   1886     1    BL2   AA   2   6   0   0   0   0  0   0   0 NA
    ## 3118  barrbo01   1886     1    WS8   NL  23  79   6  13   2   0  0   2   0 NA
    ## 3119 bassech01   1886     1    KCN   NL  90 342  41  89  19   8  2  32   6 NA
    ## 3120 bastich01   1886     1    PHI   NL 105 373  46  81   9  11  2  38  29 NA
    ## 3121 baueral01   1886     1    SL5   NL   4  12   1   2   0   0  0   0   0 NA
    ## 3122 beglege01   1886     1    NY1   NL   5  16   1   2   0   0  0   1   1 NA
    ## 3123 behelst01   1886     1    NY4   AA  59 224  32  46   5   2  0  17  16 NA
    ## 3124 bennech01   1886     1    DTN   NL  72 235  37  57  13   5  4  34   4 NA
    ## 3125 bickhda01   1886     1    CN2   AA   1   3   2   1   0   0  0   0   0 NA
    ## 3126 bierblo01   1886     1    PH4   AA 137 522  56 118  17   5  2  47  19 NA
    ## 3127 bishobi01   1886     1    PT1   AA   2   7   0   1   0   0  0   0   0 NA
    ## 3128 blighne01   1886     1    BL2   AA   3   9   0   0   0   0  0   0   0 NA
    ## 3129 boylehe01   1886     1    SL5   NL  30 108   8  27   2   2  1  13   0 NA
    ## 3130 boyleja01   1886     1    CN2   AA   1   5   0   1   0   0  0   0   0 NA
    ## 3131 bradlge01   1886     1    PH4   AA  13  48   1   4   0   1  0   1   2 NA
    ## 3132 bradyst01   1886     1    NY4   AA 124 466  56 112   8   5  0  39  16 NA
    ## 3133 briodfa01   1886     1    KCN   NL  56 215  14  51  10   3  0  29   0 NA
    ## 3134 brookha01   1886     1    NY4   AA   1   1   0   0   0   0  0   0   0 NA
    ## 3135 broutda01   1886     1    DTN   NL 121 489 139 181  40  15 11  72  21 NA
    ## 3136 brownji01   1886     1    PH4   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3137 brownpe01   1886     1    LS2   AA 112 467  86 159  29   6  2  68  26 NA
    ## 3138 brownto01   1886     1    PT1   AA 115 460 106 131  11  11  1  51  30 NA
    ## 3139 buffich01   1886     1    BSN   NL  44 176  27  51   4   1  1  30   3 NA
    ## 3140 burcher01   1886     1    BR3   AA 113 456  78 119  22   6  2  72  16 NA
    ## 3141 burdoja01   1886     1    BSN   NL  59 221  26  48   6   1  0  25   3 NA
    ## 3142 burnsto01   1886     1    CHN   NL 112 445  64 123  18  10  3  65  15 NA
    ## 3143 bushodo01   1886     1    SL4   AA 107 386  56  86   8   0  1  31  12 NA
    ## 3144 cahiljo01   1886     1    SL5   NL 125 463  43  92  17   6  1  32  16 NA
    ## 3145 carpehi01   1886     1    CN2   AA 111 458  67 101   8   5  2  61   8 NA
    ## 3146 carrocl01   1886     1    WS8   NL 111 433  73  99  11   6  2  22  31 NA
    ## 3147 carrofr01   1886     1    PT1   AA 122 486  92 140  28  11  5  64  20 NA
    ## 3148 carutbo01   1886     1    SL4   AA  87 317  91 106  21  14  4  61  26 NA
    ## 3149 caseyda01   1886     1    PHI   NL  44 151  11  23   4   1  0   9   0 NA
    ## 3150 caskied01   1886     1    NY1   NL   1   4   1   2   0   0  0   1   0 NA
    ## 3151 chambel01   1886     1    LS2   AA   6  19   2   3   0   0  0   1   0 NA
    ## 3152 clarkbo01   1886     1    BR3   AA  71 269  37  58   8   2  0  26  14 NA
    ## 3153 clarked01   1886     1    PH4   AA   1   2   0   0   0   0  0   0   0 NA
    ## 3154 clarkjo01   1886     1    CHN   NL  55 210  21  49   9   1  3  23   2 NA
    ## 3155 clemeja01   1886     1    PHI   NL  54 185  15  38   5   1  0  11   4 NA
    ## 3156 clintji01   1886     1    BL2   AA  23  83   8  15   1   0  0   6   3 NA
    ## 3157 colemjo01   1886     1    PH4   AA 121 492  67 121  18  16  0  65  28 NA
    ## 3158 colemjo01   1886     2    PT1   AA  11  43   3  15   2   1  0   9   1 NA
    ## 3159 collihu01   1886     1    LS2   AA  27 101  12  29   3   2  0  10   7 NA
    ## 3160 comisch01   1886     1    SL4   AA 131 578  95 147  15   9  3  76  41 NA
    ## 3161 connepe01   1886     1    NY4   AA   1   5   0   0   0   0  0   0   0 NA
    ## 3162 connore01   1886     1    SL5   NL   2   7   0   0   0   0  0   0   0 NA
    ## 3163 connoro01   1886     1    NY1   NL 118 485 105 172  29  20  7  71  17 NA
    ## 3164 conwabi01   1886     1    BL2   AA   7  14   4   2   0   0  0   3   0 NA
    ## 3165 conwadi01   1886     1    BL2   AA   9  34   5   7   2   0  0   3   1 NA
    ## 3166 conwape01   1886     1    KCN   NL  51 194  22  47   8   2  1  18   3 NA
    ## 3167 conwape01   1886     2    DTN   NL  12  43  10   8   1   0  2   3   0 NA
    ## 3168  cookpa01   1886     1    LS2   AA  66 262  28  54   5   2  0  14   6 NA
    ## 3169 corcola01   1886     1    NY1   NL   1   4   0   0   0   0  0   0   0 NA
    ## 3170 corcola01   1886     2    WS8   NL  21  81   9  15   2   1  0   3   3 NA
    ## 3171 corkhpo01   1886     1    CN2   AA 129 540  81 143   9   7  5  97  24 NA
    ## 3172 craneed01   1886     1    WS8   NL  80 292  20  50  11   3  0  20   8 NA
    ## 3173 cranesa01   1886     1    DTN   NL  47 185  24  26   2   2  1  12   8 NA
    ## 3174 cranesa01   1886     2    SL5   NL  39 116  10  20   3   1  0   7   6 NA
    ## 3175 crossam01   1886     1    LS2   AA  74 283  51  78  14   6  1  42  13 NA
    ## 3176 crottjo01   1886     1    NY4   AA  14  47   6   8   0   1  0   2   3 NA
    ## 3177 cushmed01   1886     1    NY4   AA  38 126  10  19   1   0  0   5   0 NA
    ## 3178 cusicto01   1886     1    PHI   NL  29 104  10  23   5   1  0   4   1 NA
    ## 3179 dailyco01   1886     1    BSN   NL  50 180  25  43   4   2  0  21   2 NA
    ## 3180 dailyed01   1886     1    PHI   NL  79 309  40  70  17   1  4  50  23 NA
    ## 3181 dailyhu01   1886     1    WS8   NL   6  16   2   2   0   0  0   1   0 NA
    ## 3182 dalryab01   1886     1    CHN   NL  82 331  62  77   7  12  3  26  16 NA
    ## 3183 davisju01   1886     1    BL2   AA  60 216  23  42   5   2  1  20  12 NA
    ## 3184 dealypa01   1886     1    BSN   NL  15  46   9  15   1   1  0   3   5 NA
    ## 3185 deaslpa01   1886     1    NY1   NL  41 143  18  38   6   1  0  17   2 NA
    ## 3186 deckeha01   1886     1    DTN   NL  14  54   2  12   1   0  0   6   0 NA
    ## 3187 deckeha01   1886     2    WS8   NL   7  23   0   5   1   1  0   1   0 NA
    ## 3188 dennyje01   1886     1    SL5   NL 119 475  58 122  24   6  9  62  16 NA
    ## 3189 devinji01   1886     1    NY1   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3190 devliji02   1886     1    NY1   NL   1   1   0   0   0   0  0   1   0 NA
    ## 3191 dolanto01   1886     1    SL5   NL  15  44   8  11   3   0  0   1   2 NA
    ## 3192 dolanto01   1886     2    BL2   AA  38 125  13  19   3   2  0  12   8 NA
    ## 3193 donahji01   1886     1    NY4   AA  49 186  14  37   0   0  0   9   1 NA
    ## 3194 donneji01   1886     1    KCN   NL 113 438  51  88  11   3  0  38  16 NA
    ## 3195 dorgami01   1886     1    NY1   NL 118 442  61 129  19   4  2  79   9 NA
    ## 3196 dugdada01   1886     1    KCN   NL  12  40   4   7   0   0  0   2   1 NA
    ## 3197 dunlafr01   1886     1    SL5   NL  71 285  53  76  15   2  3  32   7 NA
    ## 3198 dunlafr01   1886     2    DTN   NL  51 196  32  56   8   3  4  37  13 NA
    ## 3199   elybo01   1886     1    LS2   AA  10  32   5   5   0   0  0   6   1 NA
    ## 3200 esterdu01   1886     1    NY1   NL 123 473  62 125  20   6  3  43  13 NA
    ## 3201 ewingbu01   1886     1    NY1   NL  73 275  59  85  11   7  4  31  18 NA
    ## 3202 farrasi01   1886     1    PHI   NL 118 439  55 109  19   7  5  50  10 NA
    ## 3203 farreja02   1886     1    PHI   NL  17  60   7  11   0   1  0   3   1 NA
    ## 3204 farreja02   1886     2    WS8   NL  47 171  24  41  11   4  2  18  12 NA
    ## 3205 farrejo01   1886     1    BL2   AA  73 301  36  63   8   3  1  31   5 NA
    ## 3206 fennefr01   1886     1    CN2   AA 132 497 113 124  13  17  6  72  32 NA
    ## 3207 ferguch01   1886     1    PHI   NL  72 261  56  66   9   1  2  25   9 NA
    ## 3208 finlebi01   1886     1    NY1   NL  13  44   2   8   0   0  0   5   2 NA
    ## 3209 flintsi01   1886     1    CHN   NL  54 173  30  35   6   2  1  13   1 NA
    ## 3210 flynnjo02   1886     1    CHN   NL  57 205  40  41   6   2  4  19   9 NA
    ## 3211 fogarji01   1886     1    PHI   NL  77 280  54  82  13   5  3  47  30 NA
    ## 3212 forceda01   1886     1    WS8   NL  68 242  26  44   5   1  0  16   9 NA
    ## 3213 forstto01   1886     1    NY4   AA  67 251  33  49   3   2  1  20   9 NA
    ## 3214 fosteel01   1886     1    NY4   AA  35 125  16  23   0   1  0   7   3 NA
    ## 3215 foutzda01   1886     1    SL4   AA 102 414  66 116  18   9  3  59  17 NA
    ## 3216   foxjo01   1886     1    WS8   NL   1   3   0   1   0   0  0   0   0 NA
    ## 3217 fulleed01   1886     1    WS8   NL   2   7   0   1   0   0  0   0   0 NA
    ## 3218 fulmech02   1886     1    BL2   AA  80 270  54  66   9   3  1  30  29 NA
    ## 3219 gallaji01   1886     1    WS8   NL   1   5   1   1   0   0  0   0   0 NA
    ## 3220 galvipu01   1886     1    PT1   AA  50 194  24  49   7   2  0  21   8 NA
    ## 3221 ganzech01   1886     1    PHI   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3222 ganzech01   1886     2    DTN   NL  57 213  28  58   7   2  1  31   5 NA
    ## 3223 gerhajo01   1886     1    NY1   NL 123 426  44  81  11   7  0  40   8 NA
    ## 3224 gessnch01   1886     1    PH4   AA   1   4   1   1   0   0  0   0   0 NA
    ## 3225 getzich01   1886     1    DTN   NL  43 165  14  29   3   3  0  19   3 NA
    ## 3226 gillepe01   1886     1    NY1   NL  97 396  65 108  13   8  0  58  17 NA
    ## 3227 gilleto01   1886     1    DTN   NL   2  10   2   4   0   0  0   4   0 NA
    ## 3228 gilliba01   1886     1    WS8   NL  81 273  23  52   9   2  0  17   6 NA
    ## 3229 gilmofr01   1886     1    WS8   NL   9  29   2   0   0   0  0   0   0 NA
    ## 3230 gladmbu01   1886     1    WS8   NL  44 152  17  21   5   3  1  15   5 NA
    ## 3231 glassja01   1886     1    SL5   NL 121 486  96 158  29   7  3  40  38 NA
    ## 3232 gleasbi01   1886     1    SL4   AA 125 524  97 141  18   5  0  61  19 NA
    ## 3233 gleasja01   1886     1    PH4   AA  77 299  39  56   8   7  1  31   8 NA
    ## 3234 glenned01   1886     1    PT1   AA  71 277  32  53   6   5  0  26  19 NA
    ## 3235 goldswa02   1886     1    WS8   NL   6  18   0   4   1   0  0   1   0 NA
    ## 3236  gorege01   1886     1    CHN   NL 118 444 150 135  20  12  6  63  23 NA
    ## 3237 gravefr01   1886     1    SL5   NL  43 138   7  21   2   0  0   9  11 NA
    ## 3238 greered01   1886     1    BL2   AA  11  38   2   5   1   0  0   4   4 NA
    ## 3239 greered01   1886     2    PH4   AA  71 264  33  51   5   3  1  20  12 NA
    ## 3240 gunnito01   1886     1    BSN   NL  27  98  15  22   2   1  0   7   3 NA
    ## 3241 hackeme01   1886     1    KCN   NL  62 230  18  50   8   3  3  25   1 NA
    ## 3242 handiji01   1886     1    PT1   AA  14  44  10   5   1   0  0   2   1 NA
    ## 3243 hankifr01   1886     1    NY4   AA 136 522  66 126  14   5  2  63  10 NA
    ## 3244 hanlone01   1886     1    DTN   NL 126 494 105 116   6   6  4  60  50 NA
    ## 3245 hardilo01   1886     1    CHN   NL  16  51   4   9   0   0  0   3   1 NA
    ## 3246 hardilo02   1886     1    SL4   AA   1   3   0   1   1   0  0   1   0 NA
    ## 3247 harkijo01   1886     1    BR3   AA  41 142  18  32   4   2  1  15   2 NA
    ## 3248  hartbi01   1886     1    PH4   AA  22  73   3  10   1   1  0   1   1 NA
    ## 3249 hayesja01   1886     1    WS8   NL  26  89   8  17   3   0  3   9   0 NA
    ## 3250 healyjo01   1886     1    SL5   NL  43 145  10  14   5   0  0   5   0 NA
    ## 3251 heckegu01   1886     1    LS2   AA  84 343  76 117  14   5  4  48  25 NA
    ## 3252 heinzja01   1886     1    LS2   AA   1   5   1   0   0   0  0   0   0 NA
    ## 3253 hellmto01   1886     1    BL2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3254 hendeha01   1886     1    BL2   AA  19  68   5  16   2   2  0  14   0 NA
    ## 3255 hendeha01   1886     2    BR3   AA  14  50   9   9   2   0  0   6   0 NA
    ## 3256 henryjo01   1886     1    WS8   NL   4  14   3   5   0   0  0   0   0 NA
    ## 3257 hinespa01   1886     1    WS8   NL 121 487  80 152  30   8  9  56  21 NA
    ## 3258 hoffojo01   1886     1    PT1   AA   9  34   4  10   3   1  0   5   2 NA
    ## 3259 holbebi01   1886     1    NY4   AA  48 171   8  35   4   2  0  13   4 NA
    ## 3260 hoovebu01   1886     1    BL2   AA  40 157  25  34   2   6  0  10  15 NA
    ## 3261 hornujo01   1886     1    BSN   NL  94 424  67 109  12   2  2  40  16 NA
    ## 3262 houcksa01   1886     1    BL2   AA  61 260  29  50   8   1  0  17  25 NA
    ## 3263 houcksa01   1886     2    WS8   NL  52 195  14  42   3   0  0  14   4 NA
    ## 3264 housefr01   1886     1    BL2   AA   1   4   0   1   0   0  0   0   0 NA
    ## 3265 hudsona01   1886     1    SL4   AA  43 150  16  35   4   1  0  17   2 NA
    ## 3266 hyndmji01   1886     1    PH4   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3267 irwinar01   1886     1    PHI   NL 101 373  51  87   6   6  0  34  24 NA
    ## 3268 irwinbi01   1886     1    CN2   AA   2   6   0   0   0   0  0   0   0 NA
    ## 3269 irwinjo01   1886     1    PH4   AA   3  13   4   3   1   0  0   1   0 NA
    ## 3270 johnsdi01   1886     1    BSN   NL 109 413  48  99  18   9  1  57  11 NA
    ## 3271 jonesch01   1886     1    CN2   AA 127 500  87 135  22  10  6  68   3 NA
    ## 3272   joyce01   1886     1    WS8   NL   1   0   0   0   0   0  0   0   0 NA
    ## 3273 keefege01   1886     1    WS8   NL   4  14   1   0   0   0  0   0   0 NA
    ## 3274 keefeti01   1886     1    NY1   NL  64 205  26  35  10   1  1  20   3 NA
    ## 3275 keenaji01   1886     1    CN2   AA  44 148  31  40   4   3  3  24   0 NA
    ## 3276 kellych01   1886     1    PH4   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3277 kellyki01   1886     1    CHN   NL 118 451 155 175  32  11  4  79  53 NA
    ## 3278 kemmlru01   1886     1    SL4   AA  35 123  13  17   2   0  0   6   0 NA
    ## 3279 kenneed01   1886     1    BR3   AA   6  22   1   4   0   0  0   2   1 NA
    ## 3280 kennete01   1886     1    PH4   AA  20  68   3   3   0   0  0   0   0 NA
    ## 3281 kennete01   1886     2    LS2   AA   4  13   1   1   1   0  0   0   0 NA
    ## 3282 kerinjo01   1886     1    LS2   AA 120 487 113 131  19   9  4  50  26 NA
    ## 3283 kilroma01   1886     1    BL2   AA  68 218  33  38   3   1  0  11  20 NA
    ## 3284  kingsi01   1886     1    KCN   NL   7  22   0   1   0   0  0   1   0 NA
    ## 3285 kinslto01   1886     1    WS8   NL   3   8   1   2   0   0  0   1   0 NA
    ## 3286 kirbyjo01   1886     1    SL5   NL  42 136  10  15   4   0  0   5   0 NA
    ## 3287 knoufed01   1886     1    BL2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3288 knowlji01   1886     1    WS8   NL 115 443  43  94  16  11  3  35  20 NA
    ## 3289 kriegbi01   1886     1    WS8   NL  27  98  11  25   6   3  1  15   2 NA
    ## 3290 kuehnbi01   1886     1    PT1   AA 117 481  73  98  16  17  1  48  26 NA
    ## 3291 larkihe01   1886     1    PH4   AA 139 565 133 180  36  16  2  74  32 NA
    ## 3292 lathaar01   1886     1    SL4   AA 134 578 152 174  23   8  1  47  60 NA
    ## 3293 lewisfr01   1886     1    CN2   AA  77 324  72 103  14   6  2  32   8 NA
    ## 3294 lilliji01   1886     1    KCN   NL 114 416  37  73   9   0  0  22  13 NA
    ## 3295 lynchja01   1886     1    NY4   AA  51 169  17  27   5   0  0   9   4 NA
    ## 3296 lyonsde01   1886     1    PH4   AA  32 123  22  26   3   1  0  11   7 NA
    ## 3297  mackco01   1886     1    WS8   NL  10  36   4  13   2   1  0   5   0 NA
    ## 3298  mackre01   1886     1    LS2   AA 137 483  82 118  23  11  1  56  13 NA
    ## 3299 maculji01   1886     1    BL2   AA  85 268  49  55   7   1  0  26  23 NA
    ## 3300 madigto01   1886     1    WS8   NL  14  48   2   4   1   0  0   2   0 NA
    ## 3301  mannfr01   1886     1    PT1   AA 116 440  85 110  16  14  2  60  26 NA
    ## 3302 mannija01   1886     1    BL2   AA 137 556  78 124  18   7  1  45  24 NA
    ## 3303 manniji01   1886     1    DTN   NL  26  97  14  18   2   3  0   7   7 NA
    ## 3304 mappege01   1886     1    SL5   NL   6  14   1   2   0   0  0   0   0 NA
    ## 3305  marrle01   1886     1    CN2   AA   8  29   2   8   1   1  0   2   1 NA
    ## 3306 maskrle01   1886     1    LS2   AA   5  19   1   3   1   0  0   2   0 NA
    ## 3307 maskrle01   1886     2    CN2   AA  27  98   7  19   3   1  0  10   4 NA
    ## 3308 mathebo01   1886     1    PH4   AA  24  88  16  21   3   0  0  10   1 NA
    ## 3309  maysal01   1886     1    NY4   AA  41 135  11  16   3   1  1  10   2 NA
    ## 3310 mccarto01   1886     1    PHI   NL   8  27   6   5   2   1  0   3   1 NA
    ## 3311 mccauji01   1886     1    BR3   AA  11  30   5   7   1   0  0   3   2 NA
    ## 3312 mcclebi01   1886     1    BR3   AA 141 595 131 152  33   9  1  68  43 NA
    ## 3313 mccorji01   1886     1    CHN   NL  42 174  17  41   9   2  2  21   1 NA
    ## 3314 mcgarch01   1886     1    PH4   AA  71 267  41  71   9   3  2  31  17 NA
    ## 3315 mcgeaja01   1886     1    DTN   NL   6  27   3   9   0   1  0   4   2 NA
    ## 3316 mcgeaja01   1886     2    SL5   NL  59 226  31  46  12   3  2  24   8 NA
    ## 3317 mcginju01   1886     1    SL4   AA  10  37   4   7   2   0  0   4   1 NA
    ## 3318 mcginju01   1886     2    BL2   AA  26  85   7  16   5   0  1   6   3 NA
    ## 3319 mcglojo01   1886     1    WS8   NL   4  15   2   1   0   0  0   1   0 NA
    ## 3320 mcguide01   1886     1    PHI   NL  50 167  25  33   7   1  2  18   2 NA
    ## 3321 mckeola01   1886     1    CN2   AA  19  75   9  19   2   3  0   9   0 NA
    ## 3322 mckeola01   1886     2    KCN   NL   3   9   0   0   0   0  0   0   0 NA
    ## 3323 mckinal01   1886     1    SL5   NL 122 491  75 148  24   7  8  72  10 NA
    ## 3324 mclauto01   1886     1    NY4   AA  74 250  27  34   3   1  0  16  13 NA
    ## 3325 mcphebi01   1886     1    CN2   AA 140 560 139 150  23  12  8  70  40 NA
    ## 3326 mcquemo01   1886     1    KCN   NL 122 449  62 111  27   4  4  38   4 NA
    ## 3327 mcsortr01   1886     1    SL4   AA   5  20   1   3   3   0  0   0   0 NA
    ## 3328 mctamji01   1886     1    BR3   AA 111 418  86 106  23  10  2  56  18 NA
    ## 3329 meistjo01   1886     1    NY4   AA  45 186  35  44   7   3  2  21   1 NA
    ## 3330 millecy01   1886     1    PH4   AA  21  66   8   9   2   0  0   1   3 NA
    ## 3331 milledo01   1886     1    PT1   AA  83 317  70  80  15   1  2  36  35 NA
    ## 3332 millijo01   1886     1    PH4   AA  75 301  52  76  17   3  5  45  18 NA
    ## 3333 moolige01   1886     1    CHN   NL  16  56   9   8   3   0  0   2   0 NA
    ## 3334 morried01   1886     1    PT1   AA  64 227  26  38   8   3  1  24   6 NA
    ## 3335 morrijo01   1886     1    BSN   NL 117 430  86 106  25   6  7  69   9 NA
    ## 3336 mountfr01   1886     1    PT1   AA  18  55   6   8   1   1  0   2   3 NA
    ## 3337 muldomi01   1886     1    BL2   AA 101 381  57  76  13   8  0  23  12 NA
    ## 3338 mullato01   1886     1    CN2   AA  91 324  59  73  12   5  0  39  20 NA
    ## 3339 mulvejo01   1886     1    PHI   NL 107 430  71 115  16  10  2  53  27 NA
    ## 3340 murphcl01   1886     1    LS2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3341 murphjo02   1886     1    CN2   AA   5  18   0   0   0   0  0   0   0 NA
    ## 3342 murphjo02   1886     2    SL5   NL   4  14   0   3   1   0  0   1   0 NA
    ## 3343 murphjo02   1886     3    SL4   AA   1   3   0   0   0   0  0   0   1 NA
    ## 3344 myersal01   1886     1    KCN   NL 118 473  69 131  22   9  4  51   3 NA
    ## 3345 myersge01   1886     1    SL5   NL  79 295  26  56   7   3  0  27   6 NA
    ## 3346  nashbi01   1886     1    BSN   NL 109 417  61 117  11   8  1  45  16 NA
    ## 3347  navasa01   1886     1    BL2   AA   2   5   0   1   0   0  0   0   1 NA
    ## 3348 nealejo01   1886     1    LS2   AA   2   5   0   0   0   0  0   0   0 NA
    ## 3349 nelsoca01   1886     1    NY4   AA 109 413  89  93   7   2  0  23  14 NA
    ## 3350 nicolhu01   1886     1    SL4   AA  67 253  44  52   6   3  0  19  38 NA
    ## 3351 obrieja01   1886     1    PH4   AA 105 423  65 107  25   7  0  56  23 NA
    ## 3352 oconnpa01   1886     1    BL2   AA  42 166  20  30   3   2  0   8  10 NA
    ## 3353  odayha01   1886     1    WS8   NL   6  19   0   1   0   0  0   0   0 NA
    ## 3354 oldfida01   1886     1    BR3   AA  14  55   7  13   1   0  0   5   1 NA
    ## 3355 oldfida01   1886     2    WS8   NL  21  71   2  10   2   0  0   2   0 NA
    ## 3356 oneilti01   1886     1    SL4   AA 138 579 106 190  28  14  3 107   9 NA
    ## 3357 orourji01   1886     1    NY1   NL 105 440 106 136  26   6  1  34  14 NA
    ## 3358   orrda01   1886     1    NY4   AA 136 571  93 193  25  31  7  91  16 NA
    ## 3359 parsoch01   1886     1    BSN   NL   2   8   0   3   1   0  0   0   0 NA
    ## 3360 pechige01   1886     1    CN2   AA  41 144  14  30   4   2  1  21   1 NA
    ## 3361 peloulo01   1886     1    SL5   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3362 peoplji01   1886     1    BR3   AA  93 340  43  74   7   3  3  38  20 NA
    ## 3363 pfefffr01   1886     1    CHN   NL 118 474  88 125  17   8  7  95  30 NA
    ## 3364 phillbi01   1886     1    BR3   AA 141 585  68 160  26  15  0  72  13 NA
    ## 3365 pinknge01   1886     1    BR3   AA 141 597 119 156  22   7  0  37  32 NA
    ## 3366 poormto01   1886     1    BSN   NL  88 371  72  97  16   6  3  41  31 NA
    ## 3367 portehe01   1886     1    BR3   AA  48 184  20  33   4   0  0  13   3 NA
    ## 3368 powelab01   1886     1    BL2   AA  11  39   4   7   2   1  0   7   4 NA
    ## 3369 powelab01   1886     2    CN2   AA  19  74  13  17   1   1  0   8   0 NA
    ## 3370 purcebl01   1886     1    BL2   AA  26  85  17  19   0   1  0   8  13 NA
    ## 3371 questjo01   1886     1    PH4   AA  42 150  14  31   4   1  0  10   5 NA
    ## 3372 quinnjo02   1886     1    SL5   NL  75 271  33  63  11   3  1  21  12 NA
    ## 3373 quinnto01   1886     1    PT1   AA   3  11   1   0   0   0  0   0   1 NA
    ## 3374 radboch01   1886     1    BSN   NL  66 253  30  60   5   1  2  22   5 NA
    ## 3375 radfopa01   1886     1    KCN   NL 122 493  78 113  17   5  0  20  39 NA
    ## 3376 ramseto01   1886     1    LS2   AA  67 241  29  58   8   1  0  28   1 NA
    ## 3377 reardje02   1886     1    SL5   NL   1   4   0   1   0   0  0   0   0 NA
    ## 3378 reardje02   1886     2    CN2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3379 recciph01   1886     1    LS2   AA   5  13   4   4   1   1  0   2   0 NA
    ## 3380 reilljo01   1886     1    CN2   AA 115 441  92 117  12  11  6  79  19 NA
    ## 3381 reipsch01   1886     1    NY4   AA  65 232  21  49   4   6  0  25   2 NA
    ## 3382 richada01   1886     1    NY1   NL  68 237  43  55   9   1  1  27  12 NA
    ## 3383 richaha01   1886     1    DTN   NL 125 538 125 189  27  11 11  61  42 NA
    ## 3384 richmle01   1886     1    CN2   AA   8  29   3   8   0   0  0   3   0 NA
    ## 3385 ringofr01   1886     1    PT1   AA  15  56   3  12   2   2  0   5   0 NA
    ## 3386 ringofr01   1886     2    KCN   NL  16  56   6  13   7   0  0   7   0 NA
    ## 3387 robinwi01   1886     1    PH4   AA  87 342  57  69  11   3  1  30  33 NA
    ## 3388 robinya01   1886     1    SL4   AA 133 481  89 132  26   9  3  71  51 NA
    ## 3389 rosemch01   1886     1    NY4   AA 134 559  90 127  19  10  5  53   6 NA
    ## 3390  roweda01   1886     1    KCN   NL 105 429  53 103  24   8  3  57   2 NA
    ## 3391  roweja01   1886     1    DTN   NL 111 468  97 142  21   9  6  87  12 NA
    ## 3392  ryanji01   1886     1    CHN   NL  84 327  58 100  17   6  4  53  10 NA
    ## 3393 schomot01   1886     1    PT1   AA  72 246  53  67   6   6  1  29   7 NA
    ## 3394 schripo01   1886     1    BR3   AA   8  21   2   1   0   0  0   0   0 NA
    ## 3395 scottmi01   1886     1    BL2   AA 137 484  48  92  11   4  2  52  11 NA
    ## 3396 seeryem01   1886     1    SL5   NL 126 453  73 108  22   6  2  48  24 NA
    ## 3397 shaffjo01   1886     1    NY4   AA   8  25   3   6   0   0  0   1   0 NA
    ## 3398 shaffor01   1886     1    PH4   AA  21  82  15  22   3   3  0   8   3 NA
    ## 3399  shawdu01   1886     1    WS8   NL  45 148  13  13   2   0  0   6   0 NA
    ## 3400 shindbi01   1886     1    DTN   NL   7  26   4   7   0   0  0   4   2 NA
    ## 3401 shochge01   1886     1    WS8   NL  26  95  11  28   2   1  1  18   2 NA
    ## 3402 smithbi03   1886     1    DTN   NL  10  38   2   7   2   0  0   4   0 NA
    ## 3403 smithel01   1886     1    CN2   AA   9  28   6   8   1   1  0   2   0 NA
    ## 3404 smithge01   1886     1    BR3   AA 105 426  66 105  17   6  2  45  22 NA
    ## 3405 smithph01   1886     1    DTN   NL   3   9   0   1   0   0  0   1   0 NA
    ## 3406 smithpo01   1886     1    PT1   AA 126 483  75 105  20   9  2  57  38 NA
    ## 3407 smithre01   1886     1    CN2   AA   1   4   1   1   0   0  0   0   0 NA
    ## 3408 smithre01   1886     2    PH4   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3409 snydepo01   1886     1    CN2   AA  60 220  33  41   8   3  0  28  11 NA
    ## 3410 sommejo01   1886     1    BL2   AA 139 560  79 117  18   4  1  52  31 NA
    ## 3411 sowdele01   1886     1    BL2   AA  23  76  10  20   3   1  0  14   6 NA
    ## 3412 startjo01   1886     1    WS8   NL  31 122  10  27   4   1  0  17   4 NA
    ## 3413 stemmbi01   1886     1    BSN   NL  41 148  24  41   3   2  0  20   3 NA
    ## 3414 stephcl01   1886     1    CN2   AA   1   5   0   3   0   0  0   0   0 NA
    ## 3415 stoveha01   1886     1    PH4   AA 123 489 115 144  28  11  7  59  68 NA
    ## 3416 straujo02   1886     1    LS2   AA  74 297  36  64   5   6  1  31  25 NA
    ## 3417 straujo02   1886     2    BR3   AA   9  36   6   9   1   1  0   5   4 NA
    ## 3418 strikjo01   1886     1    PHI   NL   2   7   0   0   0   0  0   0   0 NA
    ## 3419 sullida01   1886     1    PT1   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3420 sullito01   1886     1    LS2   AA   9  27   1   3   0   0  0   0   0 NA
    ## 3421 sundabi01   1886     1    CHN   NL  28 103  16  25   2   2  0   6  10 NA
    ## 3422 suttoez01   1886     1    BSN   NL 116 499  83 138  21   6  3  48  18 NA
    ## 3423 swarted01   1886     1    BR3   AA 122 471  95 132  13  10  3  58  37 NA
    ## 3424 sweench01   1886     1    SL5   NL  17  64   4  16   2   0  0   7   0 NA
    ## 3425 sylvelo01   1886     1    LS2   AA  45 154  41  35   5   3  0  17   3 NA
    ## 3426 sylvelo01   1886     2    CN2   AA  17  55  10  10   0   0  3   8   2 NA
    ## 3427  tatepo01   1886     1    BSN   NL  31 106  13  24   3   1  0   3   0 NA
    ## 3428 taylobi01   1886     1    BL2   AA  10  39   4  12   0   1  0   8   1 NA
    ## 3429 terreto01   1886     1    LS2   AA   1   4   0   1   0   0  0   0   0 NA
    ## 3430 terryad01   1886     1    BR3   AA  75 299  34  71   8   9  2  39  17 NA
    ## 3431 thompsa01   1886     1    DTN   NL 122 503 101 156  18  13  8  89  13 NA
    ## 3432 titcoca01   1886     1    PHI   NL   5  16   0   1   0   0  0   1   0 NA
    ## 3433 toolest01   1886     1    BR3   AA  14  57   7  20   4   0  0   9   3 NA
    ## 3434 traffbi01   1886     1    BL2   AA  25  85  15  18   0   1  0   7   8 NA
    ## 3435 twitcla01   1886     1    DTN   NL   4  16   0   1   0   0  0   0   0 NA
    ## 3436 vaughfa01   1886     1    CN2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3437  wardjo01   1886     1    NY1   NL 122 491  82 134  17   5  2  81  36 NA
    ## 3438 weavesa01   1886     1    PH4   AA   2   7   0   1   0   0  0   0   0 NA
    ## 3439 welchcu01   1886     1    SL4   AA 138 563 114 158  31  13  2  95  59 NA
    ## 3440 welchmi01   1886     1    NY1   NL  59 213  17  46   4   2  0  18   3 NA
    ## 3441 werrijo01   1886     1    LS2   AA 136 561  75 140  20  14  3  62  19 NA
    ## 3442 whitebi02   1886     1    LS2   AA 135 557  96 143  17  10  1  66  14 NA
    ## 3443 whitede01   1886     1    DTN   NL 124 491  65 142  19   5  1  76   9 NA
    ## 3444 whitewi01   1886     1    CN2   AA   3   9   1   1   0   0  0   1   0 NA
    ## 3445 whitnar01   1886     1    PT1   AA 136 511  70 122  13   4  0  55  15 NA
    ## 3446 whitnji01   1886     1    KCN   NL  67 247  25  59  13   3  2  23   5 NA
    ## 3447 wiedmst01   1886     1    KCN   NL  51 179  13  30   2   0  0   7   3 NA
    ## 3448 willine01   1886     1    CHN   NL 121 430  69  93  17   8  6  58  13 NA
    ## 3449 winkege01   1886     1    WS8   NL   1   5   0   1   0   0  0   0   0 NA
    ## 3450  wisebi01   1886     1    WS8   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3451  wisesa01   1886     1    BSN   NL  96 387  71 112  19  12  4  72  31 NA
    ## 3452  wolfji01   1886     1    LS2   AA 130 545  93 148  17  12  3  61  23 NA
    ## 3453  woodge01   1886     1    PHI   NL 106 450  81 123  18  15  4  50   9 NA
    ## 3454 yingljo01   1886     1    WS8   NL   1   2   0   0   0   0  0   0   0 NA
    ## 3455     zay01   1886     1    BL2   AA   1   1   0   0   0   0  0   0   0 NA
    ## 3456 zeihehe01   1886     1    WS8   NL   6  21   0   0   0   0  0   0   0 NA
    ## 3457 zimmech01   1886     1    NY4   AA   6  19   1   3   0   0  0   1   0 NA
    ## 3458 allenmy01   1887     1    CL3   AA 117 463  66 128  22  10  4  77  26 NA
    ## 3459 andreed01   1887     1    PHI   NL 104 464 110 151  19   7  4  67  57 NA
    ## 3460 ansonca01   1887     1    CHN   NL 122 472 107 164  33  13  7 102  27 NA
    ## 3461 arundtu01   1887     1    IN3   NL  43 157  13  31   4   0  0  13   8 NA
    ## 3462 atkinal01   1887     1    PH4   AA  16  59   8  12   2   0  1   5   3 NA
    ## 3463 baldwki01   1887     1    CN2   AA  96 388  46  98  15  10  1  57  13 NA
    ## 3464 baldwla01   1887     1    DTN   NL  24  85  15  23   0   1  0   7   4 NA
    ## 3465 baldwma01   1887     1    CHN   NL  41 139  18  26   1   1  4  17   4 NA
    ## 3466 barklsa01   1887     1    PIT   NL  89 340  44  76  10   4  1  35   6 NA
    ## 3467 bassech01   1887     1    IN3   NL 119 452  41 104  14   6  1  47  25 NA
    ## 3468 bastich01   1887     1    PHI   NL  60 221  33  47  11   1  1  21  11 NA
    ## 3469 beatied01   1887     1    DTN   NL   2   7   0   0   0   0  0   0   0 NA
    ## 3470 becanbu01   1887     1    NY1   NL   1   5   0   0   0   0  0   0   0 NA
    ## 3471 beeched01   1887     1    PIT   NL  41 169  15  41   8   0  2  22   8 NA
    ## 3472 bennech01   1887     1    DTN   NL  46 160  26  39   6   5  3  20   7 NA
    ## 3473 bierblo01   1887     1    PH4   AA 126 530  74 144  19   7  1  82  40 NA
    ## 3474 bishobi01   1887     1    PIT   NL   3   9   0   0   0   0  0   0   0 NA
    ## 3475 boylehe01   1887     1    IN3   NL  41 141  17  27   9   1  2  13   2 NA
    ## 3476 boyleja01   1887     1    SL4   AA  88 350  48  66   3   1  2  41   7 NA
    ## 3477 briodfa01   1887     1    DTN   NL  33 128  24  29   6   1  1  26   6 NA
    ## 3478 broutda01   1887     1    DTN   NL 123 500 153 169  36  20 12 101  34 NA
    ## 3479 brownpe01   1887     1    LS2   AA 134 547 137 220  35  16  4 118 103 NA
    ## 3480 brownto01   1887     1    PIT   NL  47 192  30  47   3   4  0   6  12 NA
    ## 3481 brownto01   1887     2    IN3   NL  36 140  20  25   3   0  2   9  13 NA
    ## 3482 brownwi01   1887     1    NY1   NL  49 170  17  37   3   2  0  25  10 NA
    ## 3483 buffich01   1887     1    PHI   NL  66 269  34  72  12   1  1  46   8 NA
    ## 3484 burcher01   1887     1    BR3   AA  49 188  47  55   4   4  2  26  15 NA
    ## 3485 burdoja01   1887     1    BSN   NL  65 237  36  61   6   0  0  29  19 NA
    ## 3486 burkebi01   1887     1    DTN   NL   2   8   1   2   0   0  0   1   0 NA
    ## 3487 burnsoy01   1887     1    BL2   AA 140 551 122 188  33  19  9  99  58 NA
    ## 3488 burnsto01   1887     1    CHN   NL 115 424  57 112  20  10  3  60  32 NA
    ## 3489 bushodo01   1887     1    SL4   AA  53 201  35  51   4   0  0  26  14 NA
    ## 3490 cahiljo01   1887     1    IN3   NL  68 263  22  54   4   3  0  26  34 NA
    ## 3491 careyro01   1887     1    NY1   NL   1   4   0   0   0   0  0   2   0 NA
    ## 3492 carpehi01   1887     1    CN2   AA 127 498  70 124  12   6  1  50  44 NA
    ## 3493 carrocl01   1887     1    WS8   NL 103 420  79 104  17   4  4  37  40 NA
    ## 3494 carrofr01   1887     1    PIT   NL 102 421  71 138  24  15  6  54  23 NA
    ## 3495 carrosc01   1887     1    CL3   AA  57 216  30  43   5   1  0  19  19 NA
    ## 3496 carutbo01   1887     1    SL4   AA  98 364 102 130  23  11  8  73  49 NA
    ## 3497 caseybi01   1887     1    PH4   AA   1   0   0   0   0   0  0   0   0 NA
    ## 3498 caseyda01   1887     1    PHI   NL  45 164  22  27   3   0  1  17   1 NA
    ## 3499 chambel01   1887     1    LS2   AA  37 131  14  26   1   1  1  16   2 NA
    ## 3500 chapmfr01   1887     1    PH4   AA   1   2   0   0   0   0  0   0   0 NA
    ## 3501 clarkbo01   1887     1    BR3   AA  48 177  24  47   3   1  0  18  15 NA
    ## 3502 clarkjo01   1887     1    CHN   NL  63 215  40  52   5   5  6  25   6 NA
    ## 3503 clemeja01   1887     1    PHI   NL  66 246  48  69  13   7  1  47   7 NA
    ## 3504 colemjo01   1887     1    PIT   NL 115 475  75 139  21  11  2  54  25 NA
    ## 3505 collibi01   1887     1    NY4   AA   1   4   0   1   0   0  0   0   0 NA
    ## 3506 collihu01   1887     1    LS2   AA 130 559 122 162  22   8  1  66  71 NA
    ## 3507 comisch01   1887     1    SL4   AA 125 538 139 180  22   5  4 103 117 NA
    ## 3508 connoro01   1887     1    NY1   NL 127 471 113 134  26  22 17 104  43 NA
    ## 3509 conwadi01   1887     1    BSN   NL  42 145  20  36   4   1  0  10   5 NA
    ## 3510 conwape01   1887     1    DTN   NL  24  95  16  22   5   1  1   7   0 NA
    ## 3511  cookpa01   1887     1    LS2   AA  61 223  34  55   4   2  0  17  15 NA
    ## 3512 corcola01   1887     1    IN3   NL   3  10   2   2   0   0  0   0   2 NA
    ## 3513 corkhpo01   1887     1    CN2   AA 128 541  79 168  19  11  5  97  30 NA
    ## 3514 cranesa01   1887     1    WS8   NL   7  30   6   9   1   1  0   1   5 NA
    ## 3515 crossam01   1887     1    LS2   AA   8  28   0   3   0   0  0   0   0 NA
    ## 3516 crosscl01   1887     1    NY4   AA  16  55   9  11   2   1  0   5   0 NA
    ## 3517 crossla01   1887     1    LS2   AA  54 203  32  54   8   3  0  26  15 NA
    ## 3518 crowebi01   1887     1    CL3   AA  45 156  15  22   1   0  0   6   5 NA
    ## 3519 cunnibe01   1887     1    BR3   AA   3   8   3   0   0   0  0   0   0 NA
    ## 3520 cushmed01   1887     1    NY4   AA  26  93  14  23   4   2  0   9   2 NA
    ## 3521 cusicto01   1887     1    PHI   NL   7  24   3   7   1   0  0   5   0 NA
    ## 3522 dailyco01   1887     1    BSN   NL  36 120  12  19   5   0  0  13   7 NA
    ## 3523 dailyed01   1887     1    PHI   NL  26 106  18  30  11   1  1  17   8 NA
    ## 3524 dailyed01   1887     2    WS8   NL  78 311  39  78   6  10  2  36  26 NA
    ## 3525 dailyhu01   1887     1    CL3   AA  16  58   1   4   0   0  0   1   0 NA
    ## 3526 dalryab01   1887     1    PIT   NL  92 358  45  76  18   5  2  31  29 NA
    ## 3527  dalyto01   1887     1    CHN   NL  74 256  45  53  10   4  2  17  29 NA
    ## 3528 daniela01   1887     1    BL2   AA  48 165  23  41   5   1  0  32   7 NA
    ## 3529 darlide01   1887     1    CHN   NL  38 141  28  45   7   4  3  20  19 NA
    ## 3530 davisju01   1887     1    BL2   AA 130 485  81 150  23  19  8 109  49 NA
    ## 3531 dealypa01   1887     1    WS8   NL  58 212  33  55   8   2  1  18  36 NA
    ## 3532 deaslpa01   1887     1    NY1   NL  30 118  12  37   5   0  0  23   3 NA
    ## 3533 dennyje01   1887     1    IN3   NL 122 510  86 165  34  12 11  97  29 NA
    ## 3534 devliji02   1887     1    PHI   NL   2   6   2   2   0   0  0   0   0 NA
    ## 3535 donahji01   1887     1    NY4   AA  60 220  33  62   4   1  1  29   6 NA
    ## 3536 donneji01   1887     1    WS8   NL 117 425  51  85   9   6  1  46  42 NA
    ## 3537 dorgami01   1887     1    NY1   NL  71 283  41  73  10   0  0  34  22 NA
    ## 3538 dunlafr01   1887     1    DTN   NL  65 272  60  72  13  10  5  45  15 NA
    ## 3539 esterdu01   1887     1    NY4   AA  26 101  11  17   1   0  0   7   8 NA
    ## 3540 ewingbu01   1887     1    NY1   NL  77 318  83  97  17  13  6  44  26 NA
    ## 3541 faganbi01   1887     1    NY4   AA   6  21   0   3   0   0  0   0   0 NA
    ## 3542 farrasi01   1887     1    PHI   NL 116 443  83 125  20   9  4  72  24 NA
    ## 3543 farreja02   1887     1    WS8   NL  87 339  40  75  14   9  0  41  31 NA
    ## 3544    fast01   1887     1    IN3   NL   4  11   1   2   0   0  0   0   1 NA
    ## 3545 fennefr01   1887     1    CN2   AA 134 526 133 140  15  16  8  97  74 NA
    ## 3546 ferguch01   1887     1    PHI   NL  72 264  67  89  14   6  3  85  13 NA
    ## 3547 fieldjo01   1887     1    PIT   NL  43 164  26  44   9   2  0  17   7 NA
    ## 3548 flanaed01   1887     1    PH4   AA  19  80  12  20   5   0  1  10   3 NA
    ## 3549 flintsi01   1887     1    CHN   NL  49 187  22  50   8   6  3  21   7 NA
    ## 3550 flynned01   1887     1    CL3   AA   7  27   0   5   1   0  0   4   3 NA
    ## 3551 flynnjo02   1887     1    CHN   NL   1   0   0   0   0   0  0   0   0 NA
    ## 3552 fogarji01   1887     1    PHI   NL 126 495 113 129  26  12  8  50 102 NA
    ## 3553 foutzda01   1887     1    SL4   AA 102 423  79 151  26  13  4 108  22 NA
    ## 3554 fulmech02   1887     1    BL2   AA  56 201  52  54  11   4  0  32  35 NA
    ## 3555 galvipu01   1887     1    PIT   NL  49 193  10  41   7   3  2  22   5 NA
    ## 3556 ganzech01   1887     1    DTN   NL  57 227  40  59   6   5  0  20   3 NA
    ## 3557 gardnbi01   1887     1    BL2   AA   4  11   2   3   0   0  0   1   0 NA
    ## 3558 gardngi01   1887     1    IN3   NL  18  63   8  11   1   0  1   8   7 NA
    ## 3559 geissem01   1887     1    CHN   NL   3  12   0   1   0   0  0   0   0 NA
    ## 3560 georgbi01   1887     1    NY1   NL  13  53   6   9   0   0  0   5   2 NA
    ## 3561 gerhajo01   1887     1    NY1   NL   1   4   0   0   0   0  0   0   0 NA
    ## 3562 gerhajo01   1887     2    NY4   AA  85 307  40  68  13   2  0  27  15 NA
    ## 3563 getzich01   1887     1    DTN   NL  43 156  19  29   4   5  1  14   2 NA
    ## 3564 gilksbo01   1887     1    CL3   AA  22  83  12  26   2   0  0  13   5 NA
    ## 3565 gillepe01   1887     1    NY1   NL  76 295  40  78   9   3  3  37  37 NA
    ## 3566 gilliba01   1887     1    WS8   NL  28  90   7  18   2   0  1   6   2 NA
    ## 3567 gilmofr01   1887     1    WS8   NL  28  93   4   6   0   0  0   1   2 NA
    ## 3568 glassja01   1887     1    IN3   NL 122 483  91 142  18   7  0  40  62 NA
    ## 3569 gleasbi01   1887     1    SL4   AA 135 598 135 172  19   1  0  76  23 NA
    ## 3570 goodfmi01   1887     1    SL4   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3571  gorege01   1887     1    NY1   NL 111 459  95 133  16   5  1  49  39 NA
    ## 3572 greenbi01   1887     1    BL2   AA 118 495 114 130  16   6  0  65  71 NA
    ## 3573 greered01   1887     1    PH4   AA   3  11   1   2   0   0  0   0   2 NA
    ## 3574 greered01   1887     2    BR3   AA  91 327  49  83  13   2  2  48  33 NA
    ## 3575 griffmi01   1887     1    BL2   AA 136 532 142 160  32  13  3  94  94 NA
    ## 3576 grubehe01   1887     1    DTN   NL   7  24   3   4   0   1  0   0   0 NA
    ## 3577 gunnito01   1887     1    PHI   NL  28 104  22  27   6   1  1  16  18 NA
    ## 3578 hackeme01   1887     1    IN3   NL  42 147  12  35   6   3  2  10   4 NA
    ## 3579  hallch01   1887     1    NY4   AA   3  12   1   1   0   0  0   0   1 NA
    ## 3580 hankifr01   1887     1    NY4   AA 127 512  79 137  29  11  1  71  19 NA
    ## 3581 hanlone01   1887     1    DTN   NL 118 471  79 129  13   7  4  69  69 NA
    ## 3582 harkijo01   1887     1    BR3   AA  27  98  10  23   5   0  0  16   4 NA
    ## 3583  hartbi01   1887     1    PH4   AA   3  13   0   1   0   0  0   0   0 NA
    ## 3584 hatfigi01   1887     1    NY1   NL   2   7   2   3   1   0  0   3   0 NA
    ## 3585 hayesja01   1887     1    BL2   AA   8  28   2   4   3   0  0   3   0 NA
    ## 3586 healyjo01   1887     1    IN3   NL  41 138  14  24   4   2  3  14   7 NA
    ## 3587 heckegu01   1887     1    LS2   AA  91 370  89 118  21   6  4  50  48 NA
    ## 3588  hempdu01   1887     1    LS2   AA   1   3   1   1   1   0  0   0   0 NA
    ## 3589 hendeha01   1887     1    BR3   AA  13  41  10   5   0   0  0   3   1 NA
    ## 3590  herred01   1887     1    CL3   AA  11  44   6  12   2   0  0   6   2 NA
    ## 3591 hinespa01   1887     1    WS8   NL 123 478  83 147  32   5 10  72  46 NA
    ## 3592 hoganed02   1887     1    NY4   AA  32 120  22  24   6   1  0   5  12 NA
    ## 3593 holbebi01   1887     1    NY4   AA  69 255  20  58   4   3  0  32  12 NA
    ## 3594 hornujo01   1887     1    BSN   NL  98 437  85 118  10   6  5  49  41 NA
    ## 3595 hotalpe01   1887     1    CL3   AA 126 505 108 151  28  13  3  94  43 NA
    ## 3596 houcksa01   1887     1    NY4   AA  10  33   3   5   1   0  0   0   2 NA
    ## 3597 hudsona01   1887     1    SL4   AA  13  48   7  12   2   1  0   3   0 NA
    ## 3598 irwinar01   1887     1    PHI   NL 100 374  65  95  14   8  2  56  19 NA
    ## 3599 irwinjo01   1887     1    WS8   NL   8  31   6  11   2   0  2   3   6 NA
    ## 3600 jackshe01   1887     1    IN3   NL  10  38   1  10   1   0  0   3   2 NA
    ## 3601 johnsbi01   1887     1    IN3   NL  11  42   3   8   0   0  0   3   5 NA
    ## 3602 johnsdi01   1887     1    BSN   NL 127 507  87 131  13  20  5  77  52 NA
    ## 3603 jonesch01   1887     1    CN2   AA  41 153  28  48   7   4  2  40   7 NA
    ## 3604 jonesch01   1887     2    NY4   AA  62 247  30  63  11   3  3  29   8 NA
    ## 3605 kappehe01   1887     1    CN2   AA  23  78  11  22   3   2  0  15   3 NA
    ## 3606 keatibo01   1887     1    BL2   AA   1   4   0   1   0   0  0   0   0 NA
    ## 3607 keefege01   1887     1    WS8   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3608 keefeti01   1887     1    NY1   NL  56 191  27  42   7   6  2  23   2 NA
    ## 3609 keenaji01   1887     1    CN2   AA  47 174  19  44   4   1  0  17   7 NA
    ## 3610 kellyki01   1887     1    BSN   NL 116 484 120 156  34  11  8  63  84 NA
    ## 3611 kerinjo01   1887     1    LS2   AA 112 476 101 140  18  19  5  57  49 NA
    ## 3612 kilroma01   1887     1    BL2   AA  72 239  46  59   5   6  0  25  12 NA
    ## 3613  kingsi01   1887     1    SL4   AA  62 222  28  46   6   1  0  19  10 NA
    ## 3614 kinslto01   1887     1    NY4   AA   2   6   0   0   0   0  0   0   0 NA
    ## 3615 kirbyjo01   1887     1    IN3   NL   8  29   3   4   0   1  0   2   0 NA
    ## 3616 kirbyjo01   1887     2    CL3   AA   5  18   0   3   0   1  0   0   0 NA
    ## 3617 knoufed01   1887     1    BL2   AA   9  31   4   9   0   0  0   3   1 NA
    ## 3618 knoufed01   1887     2    SL4   AA  15  56   4  10   1   2  0   6   1 NA
    ## 3619 knowlji01   1887     1    NY4   AA  16  60  12  15   1   1  0   6   6 NA
    ## 3620 kriegbi01   1887     1    WS8   NL  25  95   9  24   4   1  2  17   2 NA
    ## 3621 kuehnbi01   1887     1    PIT   NL 102 402  68 120  18  15  1  41  17 NA
    ## 3622 larkihe01   1887     1    PH4   AA 126 497 105 154  22  12  3  88  37 NA
    ## 3623 lathaar01   1887     1    SL4   AA 136 627 163 198  35  10  2  83 129 NA
    ## 3624 leitndo01   1887     1    IN3   NL   8  27   3   4   0   0  0   0   1 NA
    ## 3625 lynchja01   1887     1    NY4   AA  23  83   4  14   1   0  0   6   3 NA
    ## 3626 lyonsde01   1887     1    PH4   AA 137 570 128 209  43  14  6 102  73 NA
    ## 3627 lyonsha01   1887     1    PHI   NL   1   4   0   0   0   0  0   0   0 NA
    ## 3628 lyonsha01   1887     2    SL4   AA   2   8   2   1   0   0  0   1   2 NA
    ## 3629  mackco01   1887     1    WS8   NL  82 314  35  63   6   1  0  20  26 NA
    ## 3630  mackre01   1887     1    LS2   AA 128 478 117 147  23   8  1  69  22 NA
    ## 3631 maddeki01   1887     1    BSN   NL  37 132  23  32   2   3  1  10   6 NA
    ## 3632  mannfr01   1887     1    CL3   AA  64 259  45  80  15   7  2  41  25 NA
    ## 3633  mannfr01   1887     2    PH4   AA  55 229  42  63  14   6  0  32  16 NA
    ## 3634 manniji01   1887     1    DTN   NL  13  52   5  10   1   0  0   3   3 NA
    ## 3635 mathebo01   1887     1    PH4   AA   7  25   5   5   0   0  0   0   0 NA
    ## 3636 mattimi01   1887     1    NY1   NL   8  32   5   8   1   0  0   4   1 NA
    ## 3637  maulal01   1887     1    PHI   NL  16  56  15  17   2   2  1   4   5 NA
    ## 3638  maysal01   1887     1    NY4   AA  62 221  23  45  15   4  2  23   7 NA
    ## 3639 mccarto01   1887     1    PHI   NL  18  70   7  13   4   0  0   6  15 NA
    ## 3640 mcclebi01   1887     1    BR3   AA 136 548 109 144  24   6  1  53  70 NA
    ## 3641 mccorji01   1887     1    PIT   NL  36 136  12  33   7   0  0  18   9 NA
    ## 3642 mcgarch01   1887     1    PH4   AA 137 536  93 158  23   6  1  63  84 NA
    ## 3643 mcgeaja01   1887     1    IN3   NL  99 405  49 109  17   3  1  56  27 NA
    ## 3644 mcginju01   1887     1    CN2   AA   8  31   8   6   2   1  0   2   1 NA
    ## 3645 mcglojo01   1887     1    CL3   AA  21  79  14  20   2   1  0  10  15 NA
    ## 3646 mcguide01   1887     1    PHI   NL  41 150  22  46   6   6  2  23   3 NA
    ## 3647 mckeaed01   1887     1    CL3   AA 132 539  97 154  16  13  2  54  76 NA
    ## 3648 mckinal01   1887     1    PIT   NL  48 200  26  68  16   4  1  30   6 NA
    ## 3649 mclauba01   1887     1    PHI   NL  50 205  26  45   8   3  1  26   2 NA
    ## 3650 mcmulge01   1887     1    NY4   AA   3  12   2   1   0   0  0   1   0 NA
    ## 3651 mcphebi01   1887     1    CN2   AA 129 540 137 156  20  19  2  87  95 NA
    ## 3652 mctamji01   1887     1    BR3   AA 134 520 123 134  22  10  1  68  66 NA
    ## 3653 meistjo01   1887     1    NY4   AA  39 158  24  35   6   2  1  21   9 NA
    ## 3654 milledo01   1887     1    PIT   NL  87 342  58  83  17   4  1  34  33 NA
    ## 3655 millijo01   1887     1    PH4   AA  95 377  54 114  27   4  2  50   8 NA
    ## 3656 moffesa01   1887     1    IN3   NL  11  41   6   5   1   0  0   1   2 NA
    ## 3657 morried01   1887     1    PIT   NL  38 126  15  25   2   0  0  10   1 NA
    ## 3658 morriha01   1887     1    IN3   NL   7  26   4   3   0   0  0   3   2 NA
    ## 3659 morrijo01   1887     1    BSN   NL 127 504  79 141  32   6 12  81  19 NA
    ## 3660 morrijo03   1887     1    NY4   AA   9  34   7   4   0   0  0   3   0 NA
    ## 3661 morrimi01   1887     1    CL3   AA  41 141  23  27   3   2  0  12   5 NA
    ## 3662 mullato01   1887     1    CN2   AA  56 199  35  44   6   3  3  23  20 NA
    ## 3663 mulvejo01   1887     1    PHI   NL 111 474  93 136  21   6  2  78  43 NA
    ## 3664 munyajo01   1887     1    CL3   AA  16  58   9  14   1   1  0   6   4 NA
    ## 3665 murphjo02   1887     1    SL4   AA   1   6   2   1   0   0  0   0   0 NA
    ## 3666 murphpa01   1887     1    NY1   NL  17  56   4  12   2   0  0   4   1 NA
    ## 3667 myersal01   1887     1    WS8   NL 105 362  45  84   9   5  2  36  18 NA
    ## 3668 myersge01   1887     1    IN3   NL  69 235  25  51   8   1  1  20  26 NA
    ## 3669  nashbi01   1887     1    BSN   NL 121 475 100 140  24  12  6  94  43 NA
    ## 3670 nealejo01   1887     1    LS2   AA   5  19   3   1   0   0  0   1   1 NA
    ## 3671 nelsoca01   1887     1    NY4   AA  68 257  61  63   5   1  0  24  29 NA
    ## 3672 nelsoca01   1887     2    NY1   NL   1   2   0   0   0   0  0   0   0 NA
    ## 3673 nicolhu01   1887     1    CN2   AA 125 475 122 102  18   2  1  34 138 NA
    ## 3674 obriebi01   1887     1    WS8   NL 113 453  71 126  16  12 19  73  11 NA
    ## 3675 obrieda01   1887     1    NY4   AA 127 522  97 157  30  13  5  73  49 NA
    ## 3676 obrieja01   1887     1    BR3   AA  30 123  18  28   4   1  1  17   8 NA
    ## 3677 obriepe01   1887     1    WS8   NL   1   4   0   0   0   0  0   0   0 NA
    ## 3678 obrieto01   1887     1    NY4   AA  31 129  13  25   3   2  0  18  10 NA
    ## 3679 oconnja01   1887     1    CN2   AA  12  40   4   4   0   0  0   1   3 NA
    ## 3680  odayha01   1887     1    WS8   NL  36 116  10  23   3   0  0   7   1 NA
    ## 3681 oneilfr01   1887     1    NY4   AA   6  26   4   8   1   1  0   3   3 NA
    ## 3682 oneilti01   1887     1    SL4   AA 124 517 167 225  52  19 14 123  30 NA
    ## 3683 orourji01   1887     1    NY1   NL 103 397  73 113  15  13  3  88  46 NA
    ## 3684 orourto01   1887     1    BSN   NL  22  78  12  12   3   0  0  10   4 NA
    ## 3685   orrda01   1887     1    NY4   AA  84 345  63 127  25  10  2  66  17 NA
    ## 3686 otterbi01   1887     1    BR3   AA  30 100  16  20   4   1  2  15   8 NA
    ## 3687 parsoch01   1887     1    NY4   AA   4  15   3   3   0   0  0   0   1 NA
    ## 3688 pechige01   1887     1    CL3   AA  10  36   6   9   1   0  0   2   0 NA
    ## 3689 peoplji01   1887     1    BR3   AA  73 268  36  68  14   2  1  38  22 NA
    ## 3690 pettibo01   1887     1    CHN   NL  32 138  29  36   3   3  2  12  16 NA
    ## 3691 pfefffr01   1887     1    CHN   NL 123 479  95 133  21   6 16  89  57 NA
    ## 3692 phillbi01   1887     1    BR3   AA 132 533  82 142  34  11  2 101  16 NA
    ## 3693  pikeli01   1887     1    NY4   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3694 pinknge01   1887     1    BR3   AA 138 580 133 155  26   6  3  69  59 NA
    ## 3695 polhema01   1887     1    IN3   NL  20  75   6  18   1   0  0   8   4 NA
    ## 3696 poormto01   1887     1    PH4   AA 135 585 140 155  18  19  4  61  88 NA
    ## 3697 portehe01   1887     1    BR3   AA  40 146  16  29   2   4  1  12   6 NA
    ## 3698 purcebl01   1887     1    BL2   AA 140 567 101 142  25   8  4  96  88 NA
    ## 3699  pylesh01   1887     1    CHN   NL   4  16   1   3   1   0  1   4   1 NA
    ## 3700 radboch01   1887     1    BSN   NL  51 175  25  40   2   2  1  24   6 NA
    ## 3701 radfopa01   1887     1    NY4   AA 128 486 127 129  15   5  4  45  73 NA
    ## 3702 rainejo01   1887     1    NY1   NL  17  58   6  17   3   0  0  12   0 NA
    ## 3703 ramseto01   1887     1    LS2   AA  65 225  19  43   4   0  0  24   2 NA
    ## 3704 recciph01   1887     1    LS2   AA  11  37   9   9   2   0  0   4   3 NA
    ## 3705 recciph01   1887     2    CL3   AA  62 229  23  47   6   3  0  29   9 NA
    ## 3706 reilljo01   1887     1    CN2   AA 134 551 106 170  35  14 10  96  50 NA
    ## 3707 reipsch01   1887     1    CL3   AA  63 231  20  49   8   3  0  17   7 NA
    ## 3708 richada01   1887     1    NY1   NL 122 450  79 125  19  10  3  62  41 NA
    ## 3709 richaha01   1887     1    DTN   NL 120 543 131 178  25  18  8  94  29 NA
    ## 3710 roachjo01   1887     1    NY1   NL   1   4   0   1   0   0  0   1   0 NA
    ## 3711 robinwi01   1887     1    PH4   AA  68 264  28  60   6   2  1  24  15 NA
    ## 3712 robinya01   1887     1    SL4   AA 125 430 102 131  32   4  1  74  75 NA
    ## 3713 rosemch01   1887     1    PH4   AA  21  73  16  16   2   1  0   8   3 NA
    ## 3714 rosemch01   1887     2    NY4   AA  60 241  30  55  10   1  1  27   3 NA
    ## 3715 rosemch01   1887     3    BR3   AA   1   3   2   1   0   0  0   1   0 NA
    ## 3716  roweja01   1887     1    DTN   NL 124 537 135 171  30  10  6  96  22 NA
    ## 3717 roxbuji01   1887     1    PH4   AA   2   8   0   1   0   0  0   0   0 NA
    ## 3718  ryancy01   1887     1    NY4   AA   8  32   4   7   1   0  0   3   1 NA
    ## 3719  ryanji01   1887     1    CHN   NL 126 508 117 145  23  10 11  74  50 NA
    ## 3720   sayji01   1887     1    CL3   AA  16  64   9  24   5   3  0  12   0 NA
    ## 3721 scheifr01   1887     1    CL3   AA   3   9   2   2   0   0  0   0   0 NA
    ## 3722 schomot01   1887     1    IN3   NL 112 419  91 129  18  16  5  83  21 NA
    ## 3723 seeryem01   1887     1    IN3   NL 122 465 104 104  18  15  4  28  48 NA
    ## 3724 seradbi01   1887     1    CN2   AA  22  79   9  14   1   2  0   5   0 NA
    ## 3725 sewared01   1887     1    PH4   AA  74 266  31  50  10   0  5  28  14 NA
    ## 3726 shaffjo01   1887     1    NY4   AA  13  48   4   8   1   1  0   3   1 NA
    ## 3727  shawdu01   1887     1    WS8   NL  21  70   7  13   2   0  0   3   1 NA
    ## 3728  sheami01   1887     1    CN2   AA   2   8   1   2   0   0  0   0   0 NA
    ## 3729 shindbi01   1887     1    DTN   NL  22  84  17  24   3   2  0  12  13 NA
    ## 3730 shochge01   1887     1    WS8   NL  70 264  47  63   9   1  1  18  29 NA
    ## 3731 shrevle01   1887     1    BL2   AA   6  24   3   4   0   1  0   2   1 NA
    ## 3732 shrevle01   1887     2    IN3   NL  14  49   6  13   1   0  0   4   2 NA
    ## 3733 simonha01   1887     1    CL3   AA   3  10   1   1   0   0  0   0   0 NA
    ## 3734 smithel01   1887     1    CN2   AA  52 186  26  47  10   6  0  23   5 NA
    ## 3735 smithge01   1887     1    BR3   AA 103 435  79 128  19  16  4  72  26 NA
    ## 3736 smithph01   1887     1    BL2   AA  64 205  37  48   7   6  1  18   7 NA
    ## 3737 smithpo01   1887     1    PIT   NL 122 456  69  98  12   7  2  54  30 NA
    ## 3738 snydepo01   1887     1    CL3   AA  74 282  33  72  12   6  0  27   5 NA
    ## 3739 sommejo01   1887     1    BL2   AA 131 463  88 123  11   5  0  65  29 NA
    ## 3740 sommepe01   1887     1    NY4   AA  33 116   9  21   3   0  1  12   6 NA
    ## 3741 sowdejo01   1887     1    IN3   NL   1   2   0   0   0   0  0   0   0 NA
    ## 3742 spragch01   1887     1    CHN   NL   3  13   0   2   0   0  0   0   0 NA
    ## 3743 stemmbi01   1887     1    BSN   NL  15  47   5  12   0   2  1   9   0 NA
    ## 3744 stoveha01   1887     1    PH4   AA 124 497 125 142  31  12  4  77  74 NA
    ## 3745 striccu01   1887     1    CL3   AA 131 534 122 141  19   4  2  53  86 NA
    ## 3746 sullima01   1887     1    CHN   NL 115 472  98 134  13  16  7  77  35 NA
    ## 3747 sundabi01   1887     1    CHN   NL  50 199  41  58   6   6  3  32  34 NA
    ## 3748 suttoez01   1887     1    BSN   NL  77 326  61  99  14   9  3  46  17 NA
    ## 3749 swababi01   1887     1    NY1   NL   2   7   0   0   0   0  0   0   0 NA
    ## 3750 swarted01   1887     1    BR3   AA  91 363  72  92  14   8  1  54  29 NA
    ## 3751 sweench01   1887     1    CL3   AA  36 133  22  30   4   4  0  19  11 NA
    ## 3752 sylvelo01   1887     1    SL4   AA  29 112  20  25   4   3  1  18  13 NA
    ## 3753  tatepo01   1887     1    BSN   NL  60 231  34  60   5   3  0  27   7 NA
    ## 3754 taylobi01   1887     1    PH4   AA   1   4   0   1   0   0  0   1   0 NA
    ## 3755 tebeage01   1887     1    CN2   AA  85 318  57  94  12   5  4  33  37 NA
    ## 3756 tebeapa01   1887     1    CHN   NL  20  68   8  11   3   0  0  10   8 NA
    ## 3757 terryad01   1887     1    BR3   AA  86 352  56 103   6  10  3  65  27 NA
    ## 3758 thompsa01   1887     1    DTN   NL 127 545 118 203  29  23 10 166  22 NA
    ## 3759 tiernmi01   1887     1    NY1   NL 103 407  82 117  13  12 10  62  28 NA
    ## 3760 titcoca01   1887     1    PH4   AA   3  10   0   0   0   0  0   0   0 NA
    ## 3761 titcoca01   1887     2    NY1   NL   9  29   1   2   0   0  0   1   1 NA
    ## 3762 toolest01   1887     1    BR3   AA  26 103  19  24   6   0  1  13   4 NA
    ## 3763 townsge01   1887     1    PH4   AA  31 109  12  21   3   0  0  14   8 NA
    ## 3764   toyji01   1887     1    CL3   AA 109 423  56  94  20   5  1  56   8 NA
    ## 3765 trottsa01   1887     1    BL2   AA  85 300  44  77  16   3  0  37   8 NA
    ## 3766 tucketo01   1887     1    BL2   AA 136 524 114 144  15   9  6  84  85 NA
    ## 3767 twitcla01   1887     1    DTN   NL  65 264  44  88  14   6  0  51  12 NA
    ## 3768 vanhage01   1887     1    CHN   NL  45 172  30  35   4   0  3  17  12 NA
    ## 3769 veachpe01   1887     1    LS2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3770  wardjo01   1887     1    NY1   NL 129 545 114 184  16   5  1  53 111 NA
    ## 3771 watsomo01   1887     1    CN2   AA   2   8   1   1   0   0  0   0   0 NA
    ## 3772 welchcu01   1887     1    SL4   AA 131 544  98 151  32   7  3 108  89 NA
    ## 3773 welchmi01   1887     1    NY1   NL  41 148  16  36   4   2  2  15   2 NA
    ## 3774 werrijo01   1887     1    LS2   AA 136 533  90 152  21  13  7  99  49 NA
    ## 3775 weyhigu01   1887     1    PH4   AA  57 209  19  42   6   1  0  16   8 NA
    ## 3776 wheelbo01   1887     1    BSN   NL  48 166  32  42   4   2  2  15  20 NA
    ## 3777 whitebi02   1887     1    LS2   AA 132 512  85 129   7   9  2  79  41 NA
    ## 3778 whitede01   1887     1    DTN   NL 111 449  71 136  20  11  3  75  20 NA
    ## 3779 whitnar01   1887     1    PIT   NL 119 431  57 112  11   4  0  51  10 NA
    ## 3780 whitnji01   1887     1    WS8   NL  54 201  29  53   9   6  2  22  10 NA
    ## 3781 widnewi01   1887     1    CN2   AA   1   4   0   1   0   0  0   1   0 NA
    ## 3782 wiedmst01   1887     1    DTN   NL  21  82  12  17   2   0  1  11   6 NA
    ## 3783 wiedmst01   1887     2    NY4   AA  14  46   5   7   1   1  0   1   2 NA
    ## 3784 wiedmst01   1887     3    NY1   NL   1   3   0   1   0   0  0   0   0 NA
    ## 3785 willine01   1887     1    CHN   NL 127 439  77 117  20  14  9  78  45 NA
    ## 3786  wisesa01   1887     1    BSN   NL 113 467 103 156  27  17  9  92  43 NA
    ## 3787  wolfji01   1887     1    LS2   AA 137 569 103 160  27  13  2 102  45 NA
    ## 3788  woodge01   1887     1    PHI   NL 113 491 118 142  22  19 14  66  19 NA
    ## 3789 wrighbi01   1887     1    WS8   NL   1   3   0   2   0   0  0   0   0 NA
    ## 3790 zimmech01   1887     1    CL3   AA  14  52   9  12   5   0  0   4   1 NA
    ## 3791 albergu01   1888     1    CL3   AA 102 364  51  75  10   6  1  48  26 NA
    ## 3792 allenmy01   1888     1    KC2   AA  37 136  23  29   6   4  0  10   4 NA
    ## 3793 andreed01   1888     1    PHI   NL 124 528  75 126  14   4  3  44  35 NA
    ## 3794 andrewa01   1888     1    LS2   AA  26  93  12  18   6   3  0   6   5 NA
    ## 3795 ansonca01   1888     1    CHN   NL 134 515 101 177  20  12 12  84  28 NA
    ## 3796 arundtu01   1888     1    WS8   NL  17  51   2  10   0   1  0   3   1 NA
    ## 3797 bakelje01   1888     1    CL3   AA  61 194  19  26   0   1  1   9   1 NA
    ## 3798 baldwki01   1888     1    CN2   AA  67 271  27  59  11   3  1  25   4 NA
    ## 3799 baldwla01   1888     1    DTN   NL   6  23   5   6   0   0  0   3   0 NA
    ## 3800 baldwma01   1888     1    CHN   NL  30 106  11  16   1   2  1   5   4 NA
    ## 3801 banniji01   1888     1    WS8   NL   1   0   0   0   0   0  0   0   0 NA
    ## 3802 barklsa01   1888     1    KC2   AA 116 482  67 104  21   6  4  51  15 NA
    ## 3803 bassech01   1888     1    IN3   NL 128 481  58 116  20   3  2  60  24 NA
    ## 3804 bastich01   1888     1    PHI   NL  80 275  30  53   4   1  1  17  12 NA
    ## 3805 beatied01   1888     1    DTN   NL  16  56   8  14   1   2  2   9   1 NA
    ## 3806 becklja01   1888     1    PIT   NL  71 283  35  97  15   3  0  27  20 NA
    ## 3807 bennech01   1888     1    DTN   NL  74 258  32  68  12   4  5  29   4 NA
    ## 3808 bierblo01   1888     1    PH4   AA 134 535  83 143  20   9  0  80  34 NA
    ## 3809 blairbi01   1888     1    PH4   AA   4  13   1   4   1   0  0   1   0 NA
    ## 3810 blighne01   1888     1    CN2   AA   3   5   0   0   0   0  0   0   0 NA
    ## 3811 borchge01   1888     1    CHN   NL  10  33   3   2   2   0  0   2   1 NA
    ## 3812 boylehe01   1888     1    IN3   NL  37 125  13  18   2   0  1   6   1 NA
    ## 3813 boyleja01   1888     1    SL4   AA  71 257  33  62   8   1  1  23  11 NA
    ## 3814 bradlge01   1888     1    BL2   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3815 brennji01   1888     1    KC2   AA  34 118   5  20   2   0  0   6   3 NA
    ## 3816 briodfa01   1888     1    KC2   AA  13  48   1  10   1   0  0   8   0 NA
    ## 3817 brougca01   1888     1    DTN   NL   1   4   0   0   0   0  0   0   0 NA
    ## 3818 broutda01   1888     1    DTN   NL 129 522 118 160  33  11  9  66  34 NA
    ## 3819 brownpe01   1888     1    LS2   AA  99 383  58 120  22   8  3  72  36 NA
    ## 3820 brownto01   1888     1    BSN   NL 107 420  62 104  10   7  9  49  46 NA
    ## 3821 brownwi01   1888     1    NY1   NL  20  59   4  16   1   0  0   6   1 NA
    ## 3822 brynato01   1888     1    CHN   NL   3  11   1   2   0   1  0   1   0 NA
    ## 3823 buckldi01   1888     1    IN3   NL  71 260  28  71   9   3  5  22   4 NA
    ## 3824 buffich01   1888     1    PHI   NL  46 160  14  29   4   1  0  12   1 NA
    ## 3825 burdibi01   1888     1    IN3   NL  21  68   6  10   0   0  0   1   0 NA
    ## 3826 burdoja01   1888     1    BSN   NL  22  79   5  16   0   0  0   4   1 NA
    ## 3827 burdoja01   1888     2    BR3   AA  70 246  15  30   1   2  1   8   9 NA
    ## 3828 burnehe01   1888     1    LS2   AA   1   4   1   0   0   0  0   0   1 NA
    ## 3829 burnsji01   1888     1    KC2   AA  15  66  13  20   0   0  0   4   6 NA
    ## 3830 burnsoy01   1888     1    BL2   AA  79 325  54  97  18   9  4  42  23 NA
    ## 3831 burnsoy01   1888     2    BR3   AA  52 204  40  58   9   6  2  25  21 NA
    ## 3832 burnsto01   1888     1    CHN   NL 134 483  60 115  12   6  3  70  34 NA
    ## 3833 bushodo01   1888     1    BR3   AA  69 253  23  53   5   1  0  16   9 NA
    ## 3834 campaco01   1888     1    DTN   NL  70 251  28  51   5   3  1  18  27 NA
    ## 3835 cantzba01   1888     1    BL2   AA  37 126   7  21   2   1  0   9   0 NA
    ## 3836 carpehi01   1888     1    CN2   AA 136 551  68 147  14   5  3  67  59 NA
    ## 3837 carrocl01   1888     1    PIT   NL   5  20   1   0   0   0  0   0   2 NA
    ## 3838 carrofr01   1888     1    PIT   NL  97 366  62  91  14   5  2  48  18 NA
    ## 3839 carutbo01   1888     1    BR3   AA  94 335  58  77  10   5  5  53  23 NA
    ## 3840 caseyda01   1888     1    PHI   NL  33 118  11  18   2   1  0   5   2 NA
    ## 3841 chambel01   1888     1    LS2   AA  26  94  11  18   4   2  0   3   8 NA
    ## 3842 chambel01   1888     2    SL4   AA  14  50   6   5   0   0  1   2   3 NA
    ## 3843 childcu01   1888     1    PHI   NL   2   4   0   0   0   0  0   0   0 NA
    ## 3844 clarkbo01   1888     1    BR3   AA  45 150  23  36   5   3  1  20  11 NA
    ## 3845 clarkda01   1888     1    CHN   NL   2   7   4   2   0   1  1   2   0 NA
    ## 3846 clarkjo01   1888     1    BSN   NL  55 205  20  40   9   1  1  17   5 NA
    ## 3847 clemeja01   1888     1    PHI   NL  86 326  26  80   8   4  1  32   3 NA
    ## 3848 cleveel01   1888     1    NY1   NL   9  34   6   8   0   2  2   7   1 NA
    ## 3849 cleveel01   1888     2    PIT   NL  30 108  10  24   2   1  2   9   3 NA
    ## 3850 clinemo01   1888     1    KC2   AA  73 293  45  69  13   2  0  19  29 NA
    ## 3851 colemjo01   1888     1    PIT   NL 116 438  49 101  11   4  0  26  15 NA
    ## 3852 collihu01   1888     1    LS2   AA 116 485 117 149  26  11  2  50  62 NA
    ## 3853 collihu01   1888     2    BR3   AA  12  42  16  13   5   1  0   3   9 NA
    ## 3854 comisch01   1888     1    SL4   AA 137 576 102 157  22   5  6  83  72 NA
    ## 3855 connoro01   1888     1    NY1   NL 134 481  98 140  15  17 14  71  27 NA
    ## 3856 conwadi01   1888     1    BSN   NL   7  25   2   4   0   0  0   1   0 NA
    ## 3857 conwape01   1888     1    DTN   NL  45 167  28  46   4   2  3  23   1 NA
    ## 3858  cookpa01   1888     1    LS2   AA  57 185  20  34   2   0  0  13   9 NA
    ## 3859 corkhpo01   1888     1    CN2   AA 118 490  68 133  11   9  1  74  27 NA
    ## 3860 corkhpo01   1888     2    BR3   AA  19  71  17  27   4   3  1  19   3 NA
    ## 3861 craneed01   1888     1    NY1   NL  12  37   3   6   2   0  1   2   1 NA
    ## 3862 crossjo01   1888     1    LS2   AA   1   1   0   0   0   0  0   0   0 NA
    ## 3863 crossla01   1888     1    LS2   AA  46 180  20  41   3   0  0  15  10 NA
    ## 3864 crowebi01   1888     1    CL3   AA  18  58   5   5   2   0  0   3   1 NA
    ## 3865 crowebi01   1888     2    LS2   AA   1   3   0   0   0   0  0   0   1 NA
    ## 3866 cunnibe01   1888     1    BL2   AA  51 177  17  33   3   2  1   9   2 NA
    ## 3867 dailyco01   1888     1    IN3   NL  57 202  14  44   6   1  0  14  15 NA
    ## 3868 dailyed01   1888     1    WS8   NL 110 453  56 102   8   4  7  39  44 NA
    ## 3869 dalryab01   1888     1    PIT   NL  57 227  19  50   9   2  0  14   7 NA
    ## 3870  dalyto01   1888     1    CHN   NL  65 219  34  42   2   6  0  29  10 NA
    ## 3871 daniela01   1888     1    KC2   AA  61 218  32  45   2   0  2  28  20 NA
    ## 3872 darlide01   1888     1    CHN   NL  20  75  12  16   3   1  2   7   0 NA
    ## 3873 davisju01   1888     1    KC2   AA 121 491  70 131  22   8  3  61  42 NA
    ## 3874 deaslpa01   1888     1    WS8   NL  34 127   6  20   1   0  0   4   2 NA
    ## 3875 delahed01   1888     1    PHI   NL  74 290  40  66  12   2  1  31  38 NA
    ## 3876 dennyje01   1888     1    IN3   NL 126 524  92 137  27   7 12  63  32 NA
    ## 3877 devliji02   1888     1    SL4   AA  11  37   7  11   1   0  0   3   2 NA
    ## 3878 dolanto01   1888     1    SL4   AA  11  36   1   7   1   0  0   1   1 NA
    ## 3879 donahji01   1888     1    KC2   AA  88 337  29  79  11   3  1  28  12 NA
    ## 3880 donneji01   1888     1    WS8   NL 122 428  43  86   9   4  0  23  44 NA
    ## 3881 duffyhu01   1888     1    CHN   NL  71 298  60  84  10   4  7  41  13 NA
    ## 3882 dunlafr01   1888     1    PIT   NL  82 321  41  84  12   4  1  36  24 NA
    ## 3883 dwyerfr01   1888     1    CHN   NL   5  21   2   4   1   0  0   2   0 NA
    ## 3884 eastehe01   1888     1    KC2   AA 115 401  42  76   7   6  3  37  23 NA
    ## 3885 ehretre01   1888     1    KC2   AA  17  63   4  12   4   0  0   4   1 NA
    ## 3886 esterdu01   1888     1    IN3   NL  64 246  21  54   8   0  0  17  11 NA
    ## 3887 esterdu01   1888     2    LS2   AA  23  93   9  21   6   0  0   7   5 NA
    ## 3888 ewingbu01   1888     1    NY1   NL 103 415  83 127  18  15  6  58  53 NA
    ## 3889 ewingjo01   1888     1    LS2   AA  21  79   6  16   1   1  0   5   7 NA
    ## 3890 faatzja01   1888     1    CL3   AA 120 470  73 124  10   2  0  51  64 NA
    ## 3891 faganbi01   1888     1    KC2   AA  18  65   5  14   3   0  0   4   0 NA
    ## 3892 farmebi01   1888     1    PIT   NL   2   4   0   0   0   0  0   0   0 NA
    ## 3893 farmebi01   1888     2    PH4   AA   3  12   0   2   0   0  0   1   0 NA
    ## 3894 farrasi01   1888     1    PHI   NL 131 508  53 124  24   7  1  53  21 NA
    ## 3895 farredu01   1888     1    CHN   NL  64 241  34  56   6   3  3  19   8 NA
    ## 3896 farreja02   1888     1    BL2   AA 103 398  72  81  19   5  4  36  29 NA
    ## 3897 fennefr01   1888     1    CN2   AA 120 448  64  88   8   7  2  56  43 NA
    ## 3898 fennefr01   1888     2    PH4   AA  15  47  13  11   2   2  1  12   5 NA
    ## 3899 fieldjo01   1888     1    PIT   NL  45 169  22  33   7   2  1  15   9 NA
    ## 3900 flintsi01   1888     1    CHN   NL  22  77   6  14   3   0  0   3   1 NA
    ## 3901 fogarji01   1888     1    PHI   NL 121 454  72 107  14   6  1  35  58 NA
    ## 3902 fosteel01   1888     1    NY1   NL  37 136  15  20   3   2  0  10  13 NA
    ## 3903 foutzda01   1888     1    BR3   AA 140 563  91 156  20  13  3  99  35 NA
    ## 3904 freemju01   1888     1    SL4   AA   1   3   0   1   0   0  0   0   0 NA
    ## 3905 fullesh01   1888     1    WS8   NL  49 170  11  31   5   2  0  12   6 NA
    ## 3906 fulmech02   1888     1    BL2   AA  52 166  20  31   5   1  0  10  10 NA
    ## 3907 fusseed01   1888     1    LS2   AA   1   4   0   1   0   0  0   1   0 NA
    ## 3908 galvipu01   1888     1    PIT   NL  50 175   6  25   1   1  1   3   4 NA
    ## 3909 gamblbo01   1888     1    PH4   AA   1   3   0   1   0   0  0   0   0 NA
    ## 3910 ganzech01   1888     1    DTN   NL  95 386  45  96  13   5  1  46  12 NA
    ## 3911 gardngi01   1888     1    WS8   NL   1   3   0   1   0   0  0   0   0 NA
    ## 3912 gardngi01   1888     2    PHI   NL   1   3   0   2   0   0  0   1   0 NA
    ## 3913 gardngi01   1888     3    WS8   NL   1   1   0   0   0   0  0   0   0 NA
    ## 3914 georgbi01   1888     1    NY1   NL   9  39   7   9   1   0  1   6   1 NA
    ## 3915 getzich01   1888     1    DTN   NL  46 167  14  41   2   2  1  10   6 NA
    ## 3916 gibsowh01   1888     1    PH4   AA   1   3   0   0   0   0  0   0   0 NA
    ## 3917 gilksbo01   1888     1    CL3   AA 119 484  59 111  14   4  1  63  16 NA
    ## 3918 gilliba01   1888     1    DTN   NL   1   5   1   1   0   0  0   0   0 NA
    ## 3919 gilmofr01   1888     1    WS8   NL  13  41   0   1   0   0  0   2   0 NA
    ## 3920 glassja01   1888     1    IN3   NL 113 442  63 119  17   3  1  45  48 NA
    ## 3921 gleasbi01   1888     1    PH4   AA 123 499  55 112  10   2  0  61  27 NA
    ## 3922 gleaski01   1888     1    PHI   NL  24  83   4  17   2   0  0   5   3 NA
    ## 3923 glenned01   1888     1    KC2   AA   3   8   0   0   0   0  0   0   1 NA
    ## 3924 glenned01   1888     2    BSN   NL  20  65   8  10   0   2  0   3   0 NA
    ## 3925 goldswa02   1888     1    BL2   AA  45 165  13  39   1   1  0  14  17 NA
    ## 3926 goodfmi01   1888     1    CL3   AA  68 269  24  66   7   0  0  29   7 NA
    ## 3927  gorege01   1888     1    NY1   NL  64 254  37  56   4   4  2  17  11 NA
    ## 3928 greenbi01   1888     1    BL2   AA 115 409  69  78  13   1  0  29  46 NA
    ## 3929 greenjo01   1888     1    WS8   NL   1   3   0   0   0   0  0   0   0 NA
    ## 3930 griffmi01   1888     1    BL2   AA 137 542 103 139  21  11  0  46  46 NA
    ## 3931  grimjo01   1888     1    PHI   NL   2   7   0   1   0   0  0   0   0 NA
    ## 3932 grubehe01   1888     1    DTN   NL  27  92   8  13   2   1  0   4   0 NA
    ## 3933 gumbead01   1888     1    CHN   NL   7  24   3   8   0   1  0   2   0 NA
    ## 3934 gunnito01   1888     1    PH4   AA  23  92  18  18   0   0  0   5  14 NA
    ## 3935 haddoge01   1888     1    WS8   NL   2   5   0   1   0   0  0   0   0 NA
    ## 3936 hafnefr01   1888     1    KC2   AA   2   6   0   0   0   0  0   0   0 NA
    ## 3937 hallmbi01   1888     1    PHI   NL  18  63   5  13   4   1  0   6   1 NA
    ## 3938 hamilbi01   1888     1    KC2   AA  35 129  21  34   4   4  0  11  19 NA
    ## 3939 hankifr01   1888     1    KC2   AA  37 155  20  27   4   1  1  20   2 NA
    ## 3940 hanlone01   1888     1    DTN   NL 109 459  64 122   6   8  5  39  38 NA
    ## 3941 harkijo01   1888     1    BL2   AA   1   3   1   0   0   0  0   0   0 NA
    ## 3942 hatfigi01   1888     1    NY1   NL  28 105   7  19   1   0  0   9   8 NA
    ## 3943 healyjo01   1888     1    IN3   NL  37 131  14  30   9   0  1  13   5 NA
    ## 3944 heckegu01   1888     1    LS2   AA  56 211  32  48   9   2  0  29  20 NA
    ## 3945 hendeha01   1888     1    PIT   NL   5  18   2   5   0   0  0   3   0 NA
    ## 3946  herred01   1888     1    SL4   AA  43 172  21  46   7   1  3  43   9 NA
    ## 3947 higgibi01   1888     1    BSN   NL  14  54   5  10   1   0  0   4   1 NA
    ## 3948 hinesmi01   1888     1    BSN   NL   4  16   3   2   0   1  0   2   0 NA
    ## 3949 hinespa01   1888     1    IN3   NL 133 513  84 144  26   3  4  58  31 NA
    ## 3950 hoffmfr01   1888     1    KC2   AA  12  39   6   6   1   0  0   2   2 NA
    ## 3951 hoganed02   1888     1    CL3   AA  78 269  60  61  16   6  0  24  30 NA
    ## 3952 holbebi01   1888     1    BR3   AA  15  50   4   6   1   0  0   1   0 NA
    ## 3953 hoovech01   1888     1    KC2   AA   3  10   0   3   0   0  0   1   0 NA
    ## 3954 hornujo01   1888     1    BSN   NL 107 431  61 103  11   7  3  53  29 NA
    ## 3955 hotalpe01   1888     1    CL3   AA  98 403  67 101   7   6  0  55  35 NA
    ## 3956   hoydu01   1888     1    WS8   NL 136 503  77 138  10   8  2  29  82 NA
    ## 3957 hudsona01   1888     1    SL4   AA  56 196  27  50   7   0  2  28   9 NA
    ## 3958 hughemi01   1888     1    BR3   AA  40 139  10  19   5   0  0  10   1 NA
    ## 3959 irwinar01   1888     1    PHI   NL 125 448  51  98  12   4  0  28  19 NA
    ## 3960 irwinjo01   1888     1    WS8   NL  37 126  14  28   5   2  0   8  15 NA
    ## 3961 johnsdi01   1888     1    BSN   NL 135 585 102 173  31  18 12  68  35 NA
    ## 3962 jonesch01   1888     1    KC2   AA   6  25   2   4   0   1  0   5   1 NA
    ## 3963 kappehe01   1888     1    CN2   AA  36 143  18  37   4   4  1  15  20 NA
    ## 3964  keased01   1888     1    CL3   AA   6  23   1   2   0   0  0   0   0 NA
    ## 3965 keefege01   1888     1    WS8   NL  13  42   2   9   3   0  0   6   0 NA
    ## 3966 keefeti01   1888     1    NY1   NL  51 181  10  23   3   0  2   8   3 NA
    ## 3967 keenaji01   1888     1    CN2   AA  85 313  38  73   9   8  1  40   9 NA
    ## 3968 kellyki01   1888     1    BSN   NL 107 440  85 140  22  11  9  71  56 NA
    ## 3969 kerinjo01   1888     1    LS2   AA  83 319  38  75  11   4  2  41  16 NA
    ## 3970 kilroma01   1888     1    BL2   AA  43 145  13  26   5   2  0  19  10 NA
    ## 3971 kilromi01   1888     1    BL2   AA   1   4   0   0   0   0  0   0   0 NA
    ## 3972  kingsi01   1888     1    SL4   AA  66 207  25  43   4   6  1  14   6 NA
    ## 3973 kirbyjo01   1888     1    KC2   AA   5  16   1   1   0   0  0   0   0 NA
    ## 3974 klusmbi01   1888     1    BSN   NL  28 107   9  18   4   0  2  11   3 NA
    ## 3975 knellph01   1888     1    PIT   NL   3  11   0   1   0   0  0   0   0 NA
    ## 3976 knoufed01   1888     1    SL4   AA   9  31   1   3   0   0  0   1   1 NA
    ## 3977 knoufed01   1888     2    CL3   AA   2   6   0   1   1   0  0   0   0 NA
    ## 3978 krockgu01   1888     1    CHN   NL  39 134   9  22   0   0  1  11   1 NA
    ## 3979 kuehnbi01   1888     1    PIT   NL 138 524  60 123  22  11  3  62  34 NA
    ## 3980 larkihe01   1888     1    PH4   AA 135 546  92 147  28  12  7 101  20 NA
    ## 3981 laroqsa01   1888     1    DTN   NL   2   9   1   4   0   0  0   2   0 NA
    ## 3982 lathaar01   1888     1    SL4   AA 133 570 119 151  19   5  2  31 109 NA
    ## 3983    long01   1888     1    LS2   AA   1   2   0   0   0   0  0   0   0 NA
    ## 3984 lyonsde01   1888     1    PH4   AA 111 456  93 135  22   5  6  83  39 NA
    ## 3985 lyonsha01   1888     1    SL4   AA 123 499  66  97  10   5  4  63  36 NA
    ## 3986  mackco01   1888     1    WS8   NL  85 300  49  56   5   6  3  29  31 NA
    ## 3987  mackre01   1888     1    LS2   AA 112 446  77  97  13   5  3  34  18 NA
    ## 3988 maddeki01   1888     1    BSN   NL  20  67   7  11   0   0  0   5   4 NA
    ## 3989 mainswi01   1888     1    CHN   NL   2   7   1   1   0   0  0   0   0 NA
    ## 3990 mattimi01   1888     1    PH4   AA  41 142  22  38   6   5  0  12  16 NA
    ## 3991  maulal01   1888     1    PIT   NL  74 259  21  54   9   4  0  31   9 NA
    ## 3992  maysal01   1888     1    BR3   AA  18  63   4   5   1   1  0   5   2 NA
    ## 3993 mccarto01   1888     1    SL4   AA 131 511 107 140  20   3  1  68  93 NA
    ## 3994 mcclebi01   1888     1    BR3   AA  74 278  33  57   7   3  0  21  13 NA
    ## 3995 mcclebi01   1888     2    CL3   AA  22  72   6  16   0   0  0   5   6 NA
    ## 3996 mcgarch01   1888     1    SL4   AA  34 132  17  31   1   0  0  13  25 NA
    ## 3997 mcgeaja01   1888     1    IN3   NL 118 452  45  99  15   2  0  30  49 NA
    ## 3998 mcglojo01   1888     1    CL3   AA  55 203  22  37   1   3  1  22  26 NA
    ## 3999 mcguide01   1888     1    PHI   NL  12  51   7  17   4   2  0  11   0 NA
    ## 4000 mcguide01   1888     2    DTN   NL   3  13   0   0   0   0  0   0   0 NA
    ## 4001 mcguide01   1888     3    CL3   AA  26  94  15  24   1   3  1  13   2 NA
    ## 4002 mckeaed01   1888     1    CL3   AA 131 548  94 164  21  15  6  68  52 NA
    ## 4003 mcphebi01   1888     1    CN2   AA 111 458  88 110  12  10  4  51  54 NA
    ## 4004 mcshape01   1888     1    PIT   NL  26  98   5  19   1   0  0   5   3 NA
    ## 4005 mctamji01   1888     1    KC2   AA 130 516  94 127  12  10  4  41  55 NA
    ## 4006 milledo01   1888     1    PIT   NL 103 404  50 112  17   5  0  36  27 NA
    ## 4007 millijo01   1888     1    SL4   AA  63 219  19  55   6   2  5  37   3 NA
    ## 4008 moffesa01   1888     1    IN3   NL  10  35   6   4   0   0  0   0   0 NA
    ## 4009 morried01   1888     1    PIT   NL  55 189  12  19   0   2  0   6   2 NA
    ## 4010 morrijo01   1888     1    BSN   NL 135 486  60  96  18   7  4  39  21 NA
    ## 4011 morrimi01   1888     1    CL3   AA   4  17   2   4   0   0  0   0   0 NA
    ## 4012 mullato01   1888     1    CN2   AA  51 175  27  44   4   4  1  16  12 NA
    ## 4013 mulvejo01   1888     1    PHI   NL 100 398  37  86  12   3  0  39  18 NA
    ## 4014 murphpa01   1888     1    NY1   NL  28 106  11  18   1   0  0   4   3 NA
    ## 4015 murrami01   1888     1    WS8   NL  12  42   1   4   1   0  0   3   0 NA
    ## 4016 myersal01   1888     1    WS8   NL 132 502  46 104  12   7  2  46  20 NA
    ## 4017 myersge01   1888     1    IN3   NL  66 248  36  59   9   0  2  16  28 NA
    ## 4018  nashbi01   1888     1    BSN   NL 135 526  71 149  18  15  4  75  20 NA
    ## 4019 nichopa01   1888     1    DTN   NL  24  85  11  22   2   3  1   9   6 NA
    ## 4020 nichosa01   1888     1    PIT   NL   8  22   3   1   0   0  0   0   0 NA
    ## 4021 nicolhu01   1888     1    CN2   AA 135 548 112 131  10   2  1  35 103 NA
    ## 4022 oberldo01   1888     1    CL3   AA   3  14   3   3   2   0  0   4   0 NA
    ## 4023 obriebi01   1888     1    WS8   NL 133 528  42 119  15   2  9  66  10 NA
    ## 4024 obrieda01   1888     1    BR3   AA 136 532 105 149  27   6  2  65  55 NA
    ## 4025 obrieda02   1888     1    CL3   AA  32 109  13  20   1   0  0   9   2 NA
    ## 4026 obrieja01   1888     1    BL2   AA  57 196  25  44  11   5  0  18  14 NA
    ## 4027 oconnja01   1888     1    CN2   AA  36 137  14  28   3   1  1  17  12 NA
    ## 4028  odayha01   1888     1    WS8   NL  47 166   6  23   2   0  0   6   3 NA
    ## 4029 oneilti01   1888     1    SL4   AA 130 529  96 177  24  10  5  98  26 NA
    ## 4030 orourji01   1888     1    NY1   NL 107 409  50 112  16   6  4  50  25 NA
    ## 4031 orourto01   1888     1    BSN   NL  20  74   3  13   0   0  0   4   2 NA
    ## 4032   orrda01   1888     1    BR3   AA  99 394  57 120  20   5  1  59  11 NA
    ## 4033 peltzjo01   1888     1    BL2   AA   1   4   1   1   0   0  0   0   1 NA
    ## 4034 peoplji01   1888     1    BR3   AA  32 103  15  20   5   3  0  17  10 NA
    ## 4035 pettibo01   1888     1    CHN   NL  43 169  23  43   1   4  4  23   7 NA
    ## 4036 pfefffr01   1888     1    CHN   NL 135 517  90 129  22  10  8  57  64 NA
    ## 4037 phillbi01   1888     1    KC2   AA 129 509  57 120  20  10  1  56  10 NA
    ## 4038 pinknge01   1888     1    BR3   AA 143 575 134 156  18   8  4  52  51 NA
    ## 4039 poormto01   1888     1    PH4   AA  97 383  76  87  16   6  2  44  46 NA
    ## 4040 portehe01   1888     1    KC2   AA  55 195  12  28   3   0  0  10   1 NA
    ## 4041 proesge01   1888     1    CL3   AA   7  23   5   7   2   0  0   1   0 NA
    ## 4042 purcebl01   1888     1    BL2   AA 101 406  53  96   9   4  2  39  16 NA
    ## 4043 purcebl01   1888     2    PH4   AA  18  66  10  11   3   1  0   6  10 NA
    ## 4044 quinnjo02   1888     1    BSN   NL  38 156  19  47   8   3  4  29  12 NA
    ## 4045 radboch01   1888     1    BSN   NL  24  79   6  17   1   0  0   6   4 NA
    ## 4046 radfopa01   1888     1    BR3   AA  90 308  48  67   9   3  2  29  33 NA
    ## 4047 ramseto01   1888     1    LS2   AA  42 142  12  17   6   0  0   9   0 NA
    ## 4048   rayir01   1888     1    BSN   NL  50 206  26  51   2   3  2  26   7 NA
    ## 4049 raymoha01   1888     1    LS2   AA  32 123   8  26   2   0  0  13   7 NA
    ## 4050 recciph01   1888     1    LS2   AA   2   9   0   2   1   0  0   4   0 NA
    ## 4051 reilljo01   1888     1    CN2   AA 127 527 112 169  28  14 13 103  82 NA
    ## 4052 richada01   1888     1    NY1   NL 135 561  82 127  16   7  8  61  35 NA
    ## 4053 richaha01   1888     1    DTN   NL  58 266  60  77  18   2  6  32  13 NA
    ## 4054 robinwi01   1888     1    PH4   AA  66 254  32  62   7   2  1  31  11 NA
    ## 4055 robinya01   1888     1    SL4   AA 134 455 111 105  17   6  3  53  56 NA
    ## 4056  roweda01   1888     1    KC2   AA  32 122  14  21   3   4  0  13   2 NA
    ## 4057  roweja01   1888     1    DTN   NL 105 451  62 125  19   8  2  74  10 NA
    ## 4058  ryanji01   1888     1    CHN   NL 129 549 115 182  33  10 16  64  60 NA
    ## 4059 sandebe01   1888     1    PHI   NL  57 236  26  58  11   2  1  25  13 NA
    ## 4060 schefte01   1888     1    DTN   NL  27  94  17  19   3   1  0   4   4 NA
    ## 4061 scheifr01   1888     1    DTN   NL   1   4   0   0   0   0  0   0   0 NA
    ## 4062 schoeju01   1888     1    IN3   NL  48 169  15  40   4   0  0  20  11 NA
    ## 4063 schomot01   1888     1    IN3   NL  30 112  11  24   5   1  1  10   6 NA
    ## 4064 schripo01   1888     1    PHI   NL  40 134  15  26   5   2  1  23   2 NA
    ## 4065 seeryem01   1888     1    IN3   NL 133 500  87 110  20  10  5  50  80 NA
    ## 4066 seradbi01   1888     1    CN2   AA   6  23   4   3   1   0  0   4   0 NA
    ## 4067 sewared01   1888     1    PH4   AA  64 225  27  32   3   3  2  14  12 NA
    ## 4068  shawdu01   1888     1    WS8   NL   3  10   0   0   0   0  0   0   0 NA
    ## 4069  shawsa01   1888     1    BL2   AA   6  20   3   3   0   0  0   0   1 NA
    ## 4070 shindbi01   1888     1    BL2   AA 135 514  61 107  14   8  1  53  52 NA
    ## 4071 shochge01   1888     1    WS8   NL  90 317  46  58   6   3  2  24  23 NA
    ## 4072 shrevle01   1888     1    IN3   NL  36 115  10  21   3   0  0   2   5 NA
    ## 4073 silched01   1888     1    BR3   AA  14  48   5  13   4   0  0   3   4 NA
    ## 4074 slattmi01   1888     1    NY1   NL 103 391  50  96  12   6  1  35  26 NA
    ## 4075 smithel01   1888     1    CN2   AA  40 129  15  29   4   1  0   9   2 NA
    ## 4076 smithge01   1888     1    BR3   AA 103 402  47  86  10   7  3  61  27 NA
    ## 4077 smithph01   1888     1    BL2   AA  35 109  16  27   3   4  1  12   2 NA
    ## 4078 smithph01   1888     2    PH4   AA   3   9   1   3   1   0  0   2   1 NA
    ## 4079 smithpo01   1888     1    PIT   NL 131 481  61  99  15   2  4  52  37 NA
    ## 4080 smithsk01   1888     1    LS2   AA  58 206  27  49   9   4  1  31   5 NA
    ## 4081 snydepo01   1888     1    CL3   AA  64 237  22  51   7   3  0  14   9 NA
    ## 4082 sommejo01   1888     1    BL2   AA  79 297  31  65  10   0  0  35  13 NA
    ## 4083 sommepe01   1888     1    BSN   NL   4  13   1   3   1   0  0   0   0 NA
    ## 4084 sowdebi01   1888     1    BSN   NL  36 122  14  18   2   0  0   6   1 NA
    ## 4085 staleha01   1888     1    PIT   NL  25  85   6  11   1   0  0   1   2 NA
    ## 4086 stemmbi01   1888     1    CL3   AA   3  10   2   4   1   0  0   1   0 NA
    ## 4087 stoveha01   1888     1    PH4   AA 130 530 127 152  25  20  9  65  87 NA
    ## 4088 stratsc01   1888     1    LS2   AA  67 249  35  64   8   1  1  29  10 NA
    ## 4089 striccu01   1888     1    CL3   AA 127 493  80 115  13   6  1  33  60 NA
    ## 4090 sullima01   1888     1    CHN   NL  75 314  40  74  12   6  7  39   9 NA
    ## 4091 sullimi01   1888     1    PH4   AA  28 112  20  31   5   6  1  19  10 NA
    ## 4092 sullito01   1888     1    KC2   AA  28  92  10  10   1   0  0   5   7 NA
    ## 4093 sundabi01   1888     1    PIT   NL 120 505  69 119  14   3  0  15  71 NA
    ## 4094 sutclsy01   1888     1    DTN   NL  49 191  17  49   5   3  0  23   6 NA
    ## 4095 suttoez01   1888     1    BSN   NL  28 110  16  24   3   1  1  16  10 NA
    ## 4096 sweenpe01   1888     1    WS8   NL  11  44   3   8   0   1  0   5   0 NA
    ## 4097  tatepo01   1888     1    BSN   NL  41 148  18  34   7   1  1   6   3 NA
    ## 4098 tebeage01   1888     1    CN2   AA 121 411  72  94  12  12  3  51  37 NA
    ## 4099 tenerjo01   1888     1    CHN   NL  12  46   4   9   1   0  0   1   1 NA
    ## 4100 terryad01   1888     1    BR3   AA  30 115  13  29   6   0  0   8   7 NA
    ## 4101 thompsa01   1888     1    DTN   NL  56 238  51  67  10   8  6  40   5 NA
    ## 4102 tiernmi01   1888     1    NY1   NL 113 443  75 130  16   8  9  52  52 NA
    ## 4103 titcoca01   1888     1    NY1   NL  23  82   6  10   1   0  0   5   5 NA
    ## 4104 tomneph01   1888     1    LS2   AA  34 120  15  18   3   0  0   4  11 NA
    ## 4105 toolest01   1888     1    KC2   AA  13  48   6  10   2   2  0   7   2 NA
    ## 4106 townsge01   1888     1    PH4   AA  42 161  13  25   6   0  0  12   2 NA
    ## 4107 trottsa01   1888     1    BL2   AA  31 108  19  30  11   4  0  22   1 NA
    ## 4108 tucketo01   1888     1    BL2   AA 136 520  74 149  17  12  6  61  43 NA
    ## 4109 twitcla01   1888     1    DTN   NL 131 524  71 128  19   4  5  67  14 NA
    ## 4110  tyngji01   1888     1    PHI   NL   1   1   0   0   0   0  0   0   0 NA
    ## 4111 vanhage01   1888     1    CHN   NL  81 318  46  90   9  14  4  34  21 NA
    ## 4112 vanzadi01   1888     1    CL3   AA  10  31   1   8   1   0  0   1   1 NA
    ## 4113 vaughfa01   1888     1    LS2   AA  51 189  15  37   4   2  1  21   4 NA
    ## 4114  viaule01   1888     1    CN2   AA  43 149  16  13   1   2  0   8   5 NA
    ## 4115 wagenwo01   1888     1    PHI   NL   2   8   2   1   0   0  0   0   0 NA
    ## 4116 walkege01   1888     1    BL2   AA   4  13   1   1   0   0  0   1   0 NA
    ## 4117  wardjo01   1888     1    NY1   NL 122 510  70 128  14   5  2  49  38 NA
    ## 4118 weavefa01   1888     1    LS2   AA  26 112  12  28   1   1  0   8  12 NA
    ## 4119 welchcu01   1888     1    PH4   AA 136 549 125 155  22   8  1  61  95 NA
    ## 4120 welchmi01   1888     1    NY1   NL  47 169  16  32   5   0  2  10   4 NA
    ## 4121 wellsja01   1888     1    DTN   NL  16  57   5   9   1   0  0   2   0 NA
    ## 4122 werdepe01   1888     1    WS8   NL   3  10   0   3   0   0  0   2   0 NA
    ## 4123 werrijo01   1888     1    LS2   AA 111 413  49  89  12   7  0  51  15 NA
    ## 4124 weyhigu01   1888     1    PH4   AA  48 184  19  40   6   8  1  14   5 NA
    ## 4125 weyhijo01   1888     1    CN2   AA   8  23   2   3   0   0  0   0   0 NA
    ## 4126 whitapa01   1888     1    BL2   AA   2   6   0   0   0   0  0   0   0 NA
    ## 4127 whitebi02   1888     1    LS2   AA  49 198  35  55   6   5  1  30  15 NA
    ## 4128 whitebi02   1888     2    SL4   AA  76 275  31  48   2   3  2  30   6 NA
    ## 4129 whitede01   1888     1    DTN   NL 125 527  75 157  22   5  4  71  12 NA
    ## 4130 whitnar01   1888     1    NY1   NL  90 328  28  72   1   4  1  28   7 NA
    ## 4131 whitnji01   1888     1    WS8   NL  42 141  13  24   0   0  1  17   3 NA
    ## 4132 widnewi01   1888     1    WS8   NL  15  60   4  12   0   0  0   6   1 NA
    ## 4133 wiedmst01   1888     1    NY1   NL   2   7   1   0   0   0  0   1   0 NA
    ## 4134 willine01   1888     1    CHN   NL 132 452  75 113   9  14  8  73  25 NA
    ## 4135 wilmowa01   1888     1    WS8   NL 119 473  61 106  16   9  4  43  46 NA
    ## 4136  wiseni01   1888     1    BSN   NL   1   3   0   0   0   0  0   0   0 NA
    ## 4137  wisesa01   1888     1    BSN   NL 105 417  66 100  19  12  4  40  33 NA
    ## 4138  wolfji01   1888     1    LS2   AA 128 538  80 154  28  11  0  67  41 NA
    ## 4139  woodge01   1888     1    PHI   NL 106 433  67  99  19   6  6  51  20 NA
    ## 4140  yaikhe01   1888     1    PIT   NL   2   6   0   2   0   0  0   1   0 NA
    ## 4141 zimmech01   1888     1    CL3   AA  65 212  27  51  11   4  0  22  15 NA
    ## 4142  zinnfr01   1888     1    PH4   AA   2   7   0   0   0   0  0   0   0 NA
    ## 4143 alvorbi01   1889     1    KC2   AA  50 186  23  43   8   9  0  18   3 NA
    ## 4144 anderda01   1889     1    PHI   NL   5  11   1   2   1   0  0   0   0 NA
    ## 4145 anderva01   1889     1    IN3   NL   2   5   0   0   0   0  0   0   0 NA
    ## 4146 andreed01   1889     1    PHI   NL  10  39  10  11   1   0  0   7   7 NA
    ## 4147 andreed01   1889     2    IN3   NL  40 173  32  53  11   0  0  22   7 NA
    ## 4148 ansonca01   1889     1    CHN   NL 134 518 100 177  32   7  7 117  27 NA
    ## 4149 bakelje01   1889     1    CL4   NL  36 111   9  15   1   1  1   8   1 NA
    ## 4150 baldwki01   1889     1    CN2   AA  60 223  34  55  14   2  1  34   7 NA
    ## 4151 baldwma01   1889     1    CL6   AA  64 208  19  39   6   5  2  25   2 NA
    ## 4152 banniji01   1889     1    WS8   NL   2   1   0   0   0   0  0   0   0 NA
    ## 4153 barklsa01   1889     1    KC2   AA  45 176  36  50   6   2  0  23   8 NA
    ## 4154 bassech01   1889     1    IN3   NL 127 477  64 117  12   5  4  68  15 NA
    ## 4155 bastich01   1889     1    CHN   NL  46 155  19  21   0   0  0  10   1 NA
    ## 4156 batesjo01   1889     1    KC2   AA   1   4   0   0   0   0  0   0   0 NA
    ## 4157 bausege01   1889     1    PH4   AA   7  21   1   1   0   0  0   0   2 NA
    ## 4158  beamal01   1889     1    PIT   NL   2   6   0   1   1   0  0   0   0 NA
    ## 4159 beardol01   1889     1    CN2   AA 141 558  96 159  13  14  1  77  36 NA
    ## 4160 beatied01   1889     1    CL4   NL  37 121  13  14   0   0  1   8   0 NA
    ## 4161 becklja01   1889     1    PIT   NL 123 522  91 157  24  10  9  97  11 NA
    ## 4162 beeched01   1889     1    WS8   NL  42 179  20  53   9   0  0  30   3 NA
    ## 4163  bellch01   1889     1    KC2   AA   2   6   1   1   1   0  0   3   0 NA
    ## 4164 bellmja01   1889     1    SL4   AA   1   2   1   1   0   0  0   0   0 NA
    ## 4165 bennech01   1889     1    BSN   NL  82 247  42  57   8   2  4  28   7 NA
    ## 4166 bierblo01   1889     1    PH4   AA 130 549  80 167  27   7  7 105  17 NA
    ## 4167 bishobi01   1889     1    CHN   NL   2   1   0   0   0   0  0   0   0 NA
    ## 4168 bittmre01   1889     1    KC2   AA   4  14   2   4   0   0  0   2   1 NA
    ## 4169 blighne01   1889     1    CL6   AA  28  93   6  13   1   1  0   5   2 NA
    ## 4170 boylehe01   1889     1    IN3   NL  46 155  17  38  10   0  1  17   4 NA
    ## 4171 boyleja01   1889     1    SL4   AA  99 347  54  85  11   5  3  42   5 NA
    ## 4172 brennji01   1889     1    PH4   AA  31 113  12  25   4   0  0  15   1 NA
    ## 4173 broutda01   1889     1    BSN   NL 126 485 105 181  26   9  7 118  22 NA
    ## 4174 brownpe01   1889     1    LS2   AA  83 324  39  83  19   5  2  32  21 NA
    ## 4175 brownto01   1889     1    BSN   NL  90 362  93  84  10   5  2  24  63 NA
    ## 4176 brownwi01   1889     1    NY1   NL  40 139  16  36  10   0  1  29   6 NA
    ## 4177 buckldi01   1889     1    IN3   NL  68 260  35  67  11   0  8  41   5 NA
    ## 4178 buffich01   1889     1    PHI   NL  47 154  16  32   2   0  0  21   0 NA
    ## 4179 burdibi01   1889     1    IN3   NL  10  17   1   2   0   0  0   1   0 NA
    ## 4180 burnsji01   1889     1    KC2   AA 134 579 103 176  23  11  5  97  56 NA
    ## 4181 burnsoy01   1889     1    BR3   AA 131 504 105 153  19  13  5 100  32 NA
    ## 4182 burnsto01   1889     1    CHN   NL 136 525  64 135  27   6  4  66  18 NA
    ## 4183 bushodo01   1889     1    BR3   AA  25  84  15  13   1   0  0   8   2 NA
    ## 4184 cantzba01   1889     1    BL2   AA  20  69   6  12   2   0  0   8   2 NA
    ## 4185  carlfr01   1889     1    LS2   AA  25  99  13  20   2   2  0  13   0 NA
    ## 4186 carnejo01   1889     1    WS8   NL  69 273  25  63   7   0  1  29  12 NA
    ## 4187 carpehi01   1889     1    CN2   AA 123 486  67 127  23   6  0  63  47 NA
    ## 4188 carrofr01   1889     1    PIT   NL  91 318  80 105  21  11  2  51  19 NA
    ## 4189 carutbo01   1889     1    BR3   AA  59 172  45  43   8   3  2  31   9 NA
    ## 4190 caseyda01   1889     1    PHI   NL  20  68   5  15   2   0  0   8   0 NA
    ## 4191 chambel01   1889     1    SL4   AA  53 171  18  34   8   3  2  31   3 NA
    ## 4192 clarkbo01   1889     1    BR3   AA  53 182  32  50   5   2  0  22  18 NA
    ## 4193 clarkha01   1889     1    WS8   NL   1   3   0   0   0   0  0   0   0 NA
    ## 4194 clarkjo01   1889     1    BSN   NL  73 262  36  54   9   3  2  23   8 NA
    ## 4195 clarksp01   1889     1    WS8   NL  38 145  19  37   7   2  3  22   8 NA
    ## 4196 clemeja01   1889     1    PHI   NL  78 310  51  88  17   1  4  35   3 NA
    ## 4197 colemjo01   1889     1    PH4   AA   6  19   1   1   0   0  0   1   1 NA
    ## 4198 collibi01   1889     1    PH4   AA   1   4   0   1   0   0  0   1   1 NA
    ## 4199 collihu01   1889     1    BR3   AA 138 560 139 149  18   3  2  73  65 NA
    ## 4200 comisch01   1889     1    SL4   AA 137 587 105 168  28  10  3 102  65 NA
    ## 4201 connoro01   1889     1    NY1   NL 131 496 117 157  32  17 13 130  21 NA
    ## 4202 conovte01   1889     1    CN2   AA   1   0   0   0   0   0  0   0   0 NA
    ## 4203 conwaji01   1889     1    KC2   AA  41 149  14  31   2   2  0  12   1 NA
    ## 4204 conwape01   1889     1    PIT   NL   3  10   2   1   0   0  1   2   1 NA
    ## 4205  cookpa01   1889     1    LS2   AA  81 286  34  65  10   1  0  15  11 NA
    ## 4206 corkhpo01   1889     1    BR3   AA 138 537  91 134  21   9  8  78  22 NA
    ## 4207 craneed01   1889     1    NY1   NL  29 103  16  21   1   0  2  11   6 NA
    ## 4208 crookja01   1889     1    CL6   AA  12  43  13  14   2   3  0   7  10 NA
    ## 4209 crossla01   1889     1    PH4   AA  55 199  22  44   8   2  0  23  11 NA
    ## 4210 cunnibe01   1889     1    BL2   AA  41 131  10  27   4   2  0  18   3 NA
    ## 4211 dailyco01   1889     1    IN3   NL  62 219  35  55   6   2  0  26  14 NA
    ## 4212 dailyed01   1889     1    CL6   AA 136 578 105 148  22   8  3  70  60 NA
    ## 4213 daleybi01   1889     1    BSN   NL   9  20   2   3   1   0  0   0   0 NA
    ## 4214  dalyto01   1889     1    WS8   NL  71 250  39  75  13   5  1  40  18 NA
    ## 4215 darlide01   1889     1    CHN   NL  36 120  14  23   1   1  0   7   5 NA
    ## 4216 davisju01   1889     1    KC2   AA  62 241  40  64   4   3  0  30  25 NA
    ## 4217 davisju01   1889     2    SL4   AA   2   4   1   0   0   0  0   0   0 NA
    ## 4218   daybi01   1889     1    PHI   NL   4  10   0   0   0   0  0   0   0 NA
    ## 4219 deckeha01   1889     1    PHI   NL  11  30   4   3   0   0  0   2   1 NA
    ## 4220 delahed01   1889     1    PHI   NL  56 246  37  72  13   3  0  27  19 NA
    ## 4221 dennyje01   1889     1    IN3   NL 133 578  96 163  24   0 18 112  22 NA
    ## 4222 devliji02   1889     1    SL4   AA   9  26   4   5   0   0  0   0   1 NA
    ## 4223 donahji01   1889     1    KC2   AA  67 252  30  59   5   4  0  32  12 NA
    ## 4224 donneji01   1889     1    WS8   NL   4  13   3   2   0   0  0   0   1 NA
    ## 4225 dowiejo01   1889     1    BL2   AA  20  75  12  17   5   0  0   8   5 NA
    ## 4226 doyleja01   1889     1    CL6   AA  11  36   6  10   1   1  0   3   9 NA
    ## 4227 duffech01   1889     1    SL4   AA 137 509  93 124  15  11 16  86  21 NA
    ## 4228 duffyhu01   1889     1    CHN   NL 136 584 144 182  21   7 12  89  52 NA
    ## 4229 dunlafr01   1889     1    PIT   NL 121 451  59 106  19   0  2  65  21 NA
    ## 4230 dunnian01   1889     1    PIT   NL   2   7   0   0   0   0  0   0   0 NA
    ## 4231 duryeje01   1889     1    CN2   AA  54 162  37  44   6   3  0  17   5 NA
    ## 4232 dwyerfr01   1889     1    CHN   NL  36 135  14  27   1   1  1   6   0 NA
    ## 4233 earlebi01   1889     1    CN2   AA  53 169  37  45   4   7  4  31  26 NA
    ## 4234 eastehe01   1889     1    CL6   AA  95 324  43  56   5   8  4  34  10 NA
    ## 4235 eastoja01   1889     1    CL6   AA   4   7   0   0   0   0  0   0   2 NA
    ## 4236 ebrighi01   1889     1    WS8   NL  16  59   7  15   2   2  1   6   1 NA
    ## 4237 ehretre01   1889     1    LS2   AA  67 258  27  65   6   6  1  31   4 NA
    ## 4238 esterdu01   1889     1    LS2   AA  11  44   8  14   3   0  0   9   6 NA
    ## 4239 ewingbu01   1889     1    NY1   NL  99 407  91 133  23  13  4  87  34 NA
    ## 4240 ewingjo01   1889     1    LS2   AA  41 134  12  23   2   0  0   6   5 NA
    ## 4241 faatzja01   1889     1    CL4   NL 117 442  50 102  12   5  2  38  27 NA
    ## 4242 fannija01   1889     1    IN3   NL   1   1   0   0   0   0  0   0   0 NA
    ## 4243 farrasi01   1889     1    PHI   NL 130 477  70 128  22   2  3  58  28 NA
    ## 4244 farredu01   1889     1    CHN   NL 101 407  66 107  19   7 11  75  13 NA
    ## 4245 farreja02   1889     1    BL2   AA  42 157  25  33   3   0  1  26  14 NA
    ## 4246   feeja01   1889     1    IN3   NL   7  21   2   3   0   0  0   0   0 NA
    ## 4247 fennefr01   1889     1    PH4   AA 138 513  70 132  20   5  1  64  15 NA
    ## 4248 fersoal01   1889     1    WS8   NL  36 114   6  13   3   1  0   3   1 NA
    ## 4249 fieldjo01   1889     1    PIT   NL  75 289  41  90  22   5  2  43   7 NA
    ## 4250 fishech03   1889     1    LS2   AA   1   2   0   1   0   0  0   0   0 NA
    ## 4251 flanaed01   1889     1    LS2   AA  23  88  11  22   7   3  0   8   1 NA
    ## 4252 flintsi01   1889     1    CHN   NL  15  56   6  13   1   0  1   9   1 NA
    ## 4253 fogarji01   1889     1    PHI   NL 128 499 107 129  15  17  3  54  99 NA
    ## 4254 foremfr01   1889     1    BL2   AA  54 181  18  26   2   1  1  11   7 NA
    ## 4255 fosteel01   1889     1    NY1   NL   2   4   2   0   0   0  0   0   2 NA
    ## 4256 foutzda01   1889     1    BR3   AA 138 553 118 152  19   8  6 113  43 NA
    ## 4257 fullesh01   1889     1    SL4   AA 140 517  91 117  18   6  0  51  38 NA
    ## 4258 fulmech02   1889     1    BL2   AA  16  58  11  15   3   1  0  13   2 NA
    ## 4259 galliji01   1889     1    LS2   AA  31 120   6  20   0   2  0   7   1 NA
    ## 4260 galvipu01   1889     1    PIT   NL  41 150  15  28   7   2  0  16   2 NA
    ## 4261 ganzech01   1889     1    BSN   NL  73 275  30  73   3   5  1  43  13 NA
    ## 4262 garfibi01   1889     1    PIT   NL   4  13   0   0   0   0  0   0   0 NA
    ## 4263 gastrha01   1889     1    CL6   AA  32  94   5  17   0   1  0  11   2 NA
    ## 4264 gaulemi01   1889     1    LS2   AA   1   2   0   0   0   0  0   0   0 NA
    ## 4265 georgbi01   1889     1    NY1   NL   3  15   1   4   0   0  0   0   1 NA
    ## 4266 georgbi01   1889     2    CL6   AA   5  17   1   4   0   0  0   3   1 NA
    ## 4267 gettito01   1889     1    SL4   AA   4  16   2   7   0   0  1   2   0 NA
    ## 4268 getzich01   1889     1    IN3   NL  45 139  20  25   4   2  2  14   2 NA
    ## 4269 gilksbo01   1889     1    CL4   NL  53 210  17  50   5   2  0  18   6 NA
    ## 4270  gillji01   1889     1    SL4   AA   2   8   2   2   1   0  0   1   1 NA
    ## 4271 glassja01   1889     1    IN3   NL 134 582 128 205  40   3  7  85  57 NA
    ## 4272 gleasbi01   1889     1    LS2   AA  16  58   6  14   2   0  0   5   1 NA
    ## 4273 gleaski01   1889     1    PHI   NL  30  99  11  25   5   0  0   8   4 NA
    ## 4274 goetzge01   1889     1    BL2   AA   1   4   0   0   0   0  0   0   0 NA
    ## 4275  gorege01   1889     1    NY1   NL 120 488 132 149  21   7  7  54  28 NA
    ## 4276 grahaba01   1889     1    PH4   AA   4  18   0   3   0   0  0   0   0 NA
    ## 4277 greenbi01   1889     1    CL6   AA 118 414  62  93   7  10  3  49  37 NA
    ## 4278 griffmi01   1889     1    BL2   AA 137 531 152 148  21  14  4  48  39 NA
    ## 4279 grubehe01   1889     1    CL4   NL  25  69   7   7   2   0  0   4   0 NA
    ## 4280 gumbead01   1889     1    CHN   NL  41 153  30  44   3   2  7  29   2 NA
    ## 4281 gunnito01   1889     1    PH4   AA   8  24   3   6   0   1  1   1   3 NA
    ## 4282 gunsojo01   1889     1    KC2   AA  34 122  15  24   3   1  0  12   2 NA
    ## 4283 haddoge01   1889     1    WS8   NL  34 112  13  25   3   0  2  14   3 NA
    ## 4284 hallmbi01   1889     1    PHI   NL 119 462  67 117  21   8  2  60  20 NA
    ## 4285 hamilbi01   1889     1    KC2   AA 137 534 144 161  17  12  3  77 111 NA
    ## 4286 hanlone01   1889     1    PIT   NL 116 461  81 110  14  10  2  37  53 NA
    ## 4287 hatfigi01   1889     1    NY1   NL  32 125  21  23   2   0  1  12   9 NA
    ## 4288 healyjo01   1889     1    WS8   NL  13  45   7  10   2   0  1   4   0 NA
    ## 4289 healyjo01   1889     2    CHN   NL   5  20   2   2   0   0  0   1   0 NA
    ## 4290 heckegu01   1889     1    LS2   AA  81 327  42  93  17   5  1  36  17 NA
    ## 4291 hinespa01   1889     1    IN3   NL 121 486  77 148  27   1  6  72  34 NA
    ## 4292 hollawi01   1889     1    BL2   AA  40 143  13  27   1   2  0  16   4 NA
    ## 4293 hollibu01   1889     1    CN2   AA 135 563 107 181  28   7 19 104  46 NA
    ## 4294 hoovech01   1889     1    KC2   AA  71 258  44  64   2   5  1  25   9 NA
    ## 4295 hornujo01   1889     1    BL2   AA 135 533  73 122  13   9  1  78  34 NA
    ## 4296   hoydu01   1889     1    WS8   NL 127 507  98 139  11   6  0  39  35 NA
    ## 4297 hudsona01   1889     1    SL4   AA  13  52   6  13   1   1  1  10   1 NA
    ## 4298 hughemi01   1889     1    BR3   AA  20  68   4  12   0   0  0   5   0 NA
    ## 4299 hurleje01   1889     1    BSN   NL   1   4   0   0   0   0  0   0   0 NA
    ## 4300 hutchbi01   1889     1    CHN   NL  37 133  14  21   1   1  1   7   2 NA
    ## 4301 irwinar01   1889     1    PHI   NL  18  73   9  16   5   0  0  10   6 NA
    ## 4302 irwinar01   1889     2    WS8   NL  85 313  49  73  10   5  0  32   9 NA
    ## 4303 irwinjo01   1889     1    WS8   NL  58 228  42  66  11   4  0  25  10 NA
    ## 4304 johnsdi01   1889     1    BSN   NL 132 539  80 123  16   4  5  67  34 NA
    ## 4305 johnssp01   1889     1    CL6   AA 116 459  91 130  14  10  2  79  34 NA
    ## 4306 jonesal01   1889     1    PIT   NL   1   5   1   1   1   0  0   1   0 NA
    ## 4307 kappehe01   1889     1    CL6   AA  46 173  25  47   7   5  3  21  10 NA
    ## 4308 keefege01   1889     1    WS8   NL  30  98   7  16   2   1  0   1   2 NA
    ## 4309 keefeti01   1889     1    NY1   NL  47 149  17  23   5   2  0   8   2 NA
    ## 4310 keenaji01   1889     1    CN2   AA  87 300  52  86  10  11  6  60  18 NA
    ## 4311 kellyki01   1889     1    BSN   NL 125 507 120 149  41   5  9  78  68 NA
    ## 4312 kemmlru01   1889     1    CL6   AA   8  26   2   3   0   0  0   0   0 NA
    ## 4313 kerinjo01   1889     1    LS2   AA   2   9   2   3   1   0  0   3   0 NA
    ## 4314 kerinjo01   1889     2    BL2   AA  16  53   7  15   2   0  0  12   2 NA
    ## 4315 kilroma01   1889     1    BL2   AA  65 208  32  57   3   6  1  26  13 NA
    ## 4316  kingsi01   1889     1    SL4   AA  56 189  37  43   7   3  0  30   3 NA
    ## 4317 knoufed01   1889     1    PH4   AA   3  12   2   3   1   0  0   2   1 NA
    ## 4318 krockgu01   1889     1    CHN   NL   7  24   4   4   0   0  0   2   0 NA
    ## 4319 krockgu01   1889     2    IN3   NL   4  14   2   5   0   0  0   5   1 NA
    ## 4320 krockgu01   1889     3    WS8   NL   6  23   3   2   0   0  0   2   0 NA
    ## 4321 krummal01   1889     1    PIT   NL   1   4   0   0   0   0  0   0   0 NA
    ## 4322 kuehnbi01   1889     1    PIT   NL  97 390  43  96  20   5  5  57  15 NA
    ## 4323 ladewst01   1889     1    KC2   AA   2   4   0   0   0   0  0   0   0 NA
    ## 4324 larkihe01   1889     1    PH4   AA 133 516 105 164  23  12  3  74  11 NA
    ## 4325 lathaar01   1889     1    SL4   AA 118 512 110 126  13   3  4  49  69 NA
    ## 4326 lauerch01   1889     1    PIT   NL   4  16   2   3   0   0  0   1   0 NA
    ## 4327  longhe01   1889     1    KC2   AA 136 574 137 158  32   6  3  60  89 NA
    ## 4328 lovetto01   1889     1    BR3   AA  29 100  18  19   1   3  2  19   2 NA
    ## 4329 lyonsde01   1889     1    PH4   AA 131 510 135 168  36   4  9  82  10 NA
    ## 4330 lyonsha01   1889     1    NY1   NL   5  20   1   2   0   1  0   2   0 NA
    ## 4331  mackco01   1889     1    WS8   NL  98 386  51 113  16   1  0  42  26 NA
    ## 4332  mackre01   1889     1    BL2   AA 136 519  84 125  24   7  1  87  23 NA
    ## 4333 maddeki01   1889     1    BSN   NL  24  86   7  25   1   0  0  14   4 NA
    ## 4334 manniji01   1889     1    KC2   AA 132 506  68 103  16   7  3  68  58 NA
    ## 4335  marrle01   1889     1    CL6   AA 139 546 110 167  26  15  1  75  29 NA
    ## 4336 mattimi01   1889     1    PH4   AA  23  73  10  17   1   2  1   8   6 NA
    ## 4337 mattimi01   1889     2    KC2   AA  19  75   6  12   1   1  0   5   0 NA
    ## 4338  maulal01   1889     1    PIT   NL  68 257  37  71   6   6  4  44  18 NA
    ## 4339  maysal01   1889     1    CL6   AA  21  54   4   7   1   0  0   4   1 NA
    ## 4340 mcaleji01   1889     1    CL4   NL 110 447  66 105   6   6  0  35  37 NA
    ## 4341 mccafsp01   1889     1    CL6   AA   2   1   1   1   0   0  0   0   0 NA
    ## 4342 mccarjo01   1889     1    KC2   AA  20  79  12  18   0   1  0  12   3 NA
    ## 4343 mccarto01   1889     1    SL4   AA 140 604 136 176  24   7  2  63  57 NA
    ## 4344 mccoyar01   1889     1    WS8   NL   2   6   0   0   0   0  0   0   0 NA
    ## 4345 mcdermi01   1889     1    LS2   AA   9  33   7   6   2   0  0   3   0 NA
    ## 4346 mcgarch01   1889     1    KC2   AA  25 108  22  31   3   0  0  16  12 NA
    ## 4347 mcgarch01   1889     2    BL2   AA   3   7   1   1   0   0  0   0   0 NA
    ## 4348 mcgeaja01   1889     1    IN3   NL 131 532  83 142  32   1  2  63  37 NA
    ## 4349 mckeaed01   1889     1    CL4   NL 123 500  88 159  22   8  5  75  35 NA
    ## 4350 mcmahsa01   1889     1    PH4   AA  30 104   9  16   2   1  0   4   3 NA
    ## 4351 mcphebi01   1889     1    CN2   AA 135 540 109 145  25   7  5  57  63 NA
    ## 4352 mctamji01   1889     1    CL6   AA 139 529 113 146  21   7  4  52  40 NA
    ## 4353  meekda01   1889     1    SL4   AA   2   2   2   1   0   0  0   1   1 NA
    ## 4354 milledo01   1889     1    PIT   NL 104 422  77 113  25   3  6  56  16 NA
    ## 4355 milledu01   1889     1    BL2   AA  11  40   4   6   1   1  0   6   3 NA
    ## 4356 millijo01   1889     1    SL4   AA  72 273  53 100  30   2 12  76   2 NA
    ## 4357 morried01   1889     1    PIT   NL  21  72   2   7   1   0  0   4   1 NA
    ## 4358 morrijo01   1889     1    WS8   NL  44 146  20  27   5   0  2  16  12 NA
    ## 4359 mullato01   1889     1    CN2   AA  63 196  53  58  16   4  0  29  24 NA
    ## 4360 mulvejo01   1889     1    PHI   NL 129 544  77 157  21   9  6  77  23 NA
    ## 4361 murphpa01   1889     1    NY1   NL   9  28   5  10   1   1  1   4   0 NA
    ## 4362 myersal01   1889     1    WS8   NL  46 176  24  46   3   0  0  20  10 NA
    ## 4363 myersal01   1889     2    PHI   NL  75 305  52  82  14   2  0  28   8 NA
    ## 4364 myersge01   1889     1    IN3   NL  43 149  22  29   3   0  0  12  12 NA
    ## 4365  nashbi01   1889     1    BSN   NL 128 481  84 132  20   2  3  76  26 NA
    ## 4366 nicolhu01   1889     1    CN2   AA 122 474  82 121   7   8  2  58  80 NA
    ## 4367 obriebi01   1889     1    WS8   NL   2   8   1   0   0   0  0   0   0 NA
    ## 4368 obrieda01   1889     1    BR3   AA 136 567 146 170  30  11  5  80  91 NA
    ## 4369 obrieda02   1889     1    CL4   NL  41 140  13  35   1   0  0  18   2 NA
    ## 4370 oconnja01   1889     1    CL6   AA 107 398  69 107  17   7  4  60  26 NA
    ## 4371  odayha01   1889     1    WS8   NL  13  44   1   8   1   0  0   4   0 NA
    ## 4372  odayha01   1889     2    NY1   NL  10  31   5   3   0   0  0   3   2 NA
    ## 4373 oneilti01   1889     1    SL4   AA 134 534 123 179  33   8  9 110  28 NA
    ## 4374 orourji01   1889     1    NY1   NL 128 502  89 161  36   7  3  81  33 NA
    ## 4375   orrda01   1889     1    CL6   AA 134 560  70 183  31  12  4  87  12 NA
    ## 4376 pearsfr01   1889     1    KC2   AA   3  11   0   1   0   0  0   1   0 NA
    ## 4377 peoplji01   1889     1    CL6   AA  29 100  13  23   6   2  1  16   3 NA
    ## 4378 pettych01   1889     1    CN2   AA   5  20   3   6   1   1  0   4   1 NA
    ## 4379 pfefffr01   1889     1    CHN   NL 134 531  85 128  15   7  7  77  45 NA
    ## 4380 pickejo01   1889     1    KC2   AA  53 201  20  45   7   0  0  12   7 NA
    ## 4381 pinknge01   1889     1    BR3   AA 138 545 103 134  25   7  4  82  47 NA
    ## 4382 portehe01   1889     1    KC2   AA   4  10   0   1   0   0  0   1   0 NA
    ## 4383 purcebl01   1889     1    PH4   AA 129 507  72 160  19   7  0  85  22 NA
    ## 4384 quinnjo02   1889     1    BSN   NL 112 444  57 116  13   5  2  69  24 NA
    ## 4385 quinnto01   1889     1    BL2   AA  55 194  18  34   2   1  1  15   6 NA
    ## 4386 radboch01   1889     1    BSN   NL  35 122  17  23   1   0  1  13   3 NA
    ## 4387 radfopa01   1889     1    CL4   NL 136 487  94 116  21   5  1  46  30 NA
    ## 4388 ramseto01   1889     1    LS2   AA  18  57   3  15   1   0  0   3   1 NA
    ## 4389 ramseto01   1889     2    SL4   AA   5  17   2   5   1   0  0   4   0 NA
    ## 4390   rayir01   1889     1    BSN   NL   9  33   8  10   1   0  0   2   1 NA
    ## 4391   rayir01   1889     2    BL2   AA  26 106  20  36   4   1  0  17  12 NA
    ## 4392 raymoha01   1889     1    LS2   AA 130 515  58 123  12   9  0  47  19 NA
    ## 4393 reillch02   1889     1    CL6   AA   6  23   5  11   1   0  3   6   9 NA
    ## 4394 reilljo01   1889     1    CN2   AA 111 427  84 111  24  13  5  66  43 NA
    ## 4395 reynoch02   1889     1    KC2   AA   1   4   1   1   0   0  0   1   0 NA
    ## 4396 reynoch02   1889     2    BR3   AA  12  42   5   9   1   1  0   3   2 NA
    ## 4397 richada01   1889     1    NY1   NL 125 497  88 139  22   8  7 100  32 NA
    ## 4398 richaha01   1889     1    BSN   NL 132 536 122 163  33  10  6  79  47 NA
    ## 4399 riddljo01   1889     1    WS8   NL  11  37   3   8   3   0  0   3   0 NA
    ## 4400 robinbi01   1889     1    LS2   AA   1   3   2   1   0   0  0   0   0 NA
    ## 4401 robinwi01   1889     1    PH4   AA  69 264  31  61  13   2  0  28   9 NA
    ## 4402 robinya01   1889     1    SL4   AA 132 452  97  94  17   3  5  70  39 NA
    ## 4403  roweja01   1889     1    PIT   NL  75 317  57  82  14   3  2  32   5 NA
    ## 4404 rusieam01   1889     1    IN3   NL  33 103  15  18   3   1  0   4   3 NA
    ## 4405  ryanja01   1889     1    LS2   AA  21  79   8  14   1   0  0   2   2 NA
    ## 4406  ryanji01   1889     1    CHN   NL 135 576 140 187  31  14 17  72  45 NA
    ## 4407 sandebe01   1889     1    PHI   NL  44 169  21  47   8   2  0  21   4 NA
    ## 4408 scherha01   1889     1    LS2   AA   1   3   0   1   0   0  0   0   0 NA
    ## 4409 schoeju01   1889     1    IN3   NL  16  62   3  15   2   2  0   8   1 NA
    ## 4410 schripo01   1889     1    PHI   NL  55 211  24  56  10   0  1  19   5 NA
    ## 4411 seeryem01   1889     1    IN3   NL 127 526 123 165  26  12  8  59  19 NA
    ## 4412 sewared01   1889     1    PH4   AA  46 143  22  31   5   3  2  17   6 NA
    ## 4413 shannda01   1889     1    LS2   AA 121 498  90 128  22  12  4  48  26 NA
    ## 4414 shindbi01   1889     1    BL2   AA 138 567 122 178  24   7  3  64  56 NA
    ## 4415 shochge01   1889     1    WS8   NL  30 109  12  26   2   0  0  11   9 NA
    ## 4416 shrevle01   1889     1    IN3   NL   3   7   1   0   0   0  0   0   0 NA
    ## 4417 slattmi01   1889     1    NY1   NL  12  48   7  14   2   0  1  12   2 NA
    ## 4418 smithel01   1889     1    CN2   AA  29  83  12  23   3   1  2  17   1 NA
    ## 4419 smithge01   1889     1    BR3   AA 121 446  89 103  22   3  3  53  35 NA
    ## 4420 smithha01   1889     1    LS2   AA   1   2   0   1   0   0  0   1   0 NA
    ## 4421 smithph01   1889     1    PH4   AA   5  16   3   3   1   0  0   0   0 NA
    ## 4422 smithpo01   1889     1    PIT   NL  72 258  26  54  10   2  5  27  12 NA
    ## 4423 smithpo01   1889     2    BSN   NL  59 208  21  54  13   4  0  32  11 NA
    ## 4424 snydepo01   1889     1    CL4   NL  22  83   5  16   3   0  0  12   4 NA
    ## 4425 sommejo01   1889     1    BL2   AA 106 386  51  85  13   2  1  36  18 NA
    ## 4426 sommepe01   1889     1    CHN   NL  12  45   5  10   5   0  0   8   0 NA
    ## 4427 sommepe01   1889     2    IN3   NL  23  84  12  21   2   2  2  14   2 NA
    ## 4428 sowdebi01   1889     1    BSN   NL   7  17   2   4   0   0  0   0   0 NA
    ## 4429 sowdebi01   1889     2    PIT   NL  15  48   4  13   1   0  0   5   0 NA
    ## 4430 sowdejo01   1889     1    KC2   AA  28  87  11  19   3   0  0   6   1 NA
    ## 4431 spragch01   1889     1    CL4   NL   2   7   2   1   0   0  0   1   1 NA
    ## 4432 sprined01   1889     1    LS2   AA   1   2   0   0   0   0  0   0   0 NA
    ## 4433 staleha01   1889     1    PIT   NL  51 186  11  30   3   1  0   8   1 NA
    ## 4434 stearec01   1889     1    KC2   AA 139 560  96 160  24  12  3  87  67 NA
    ## 4435 stiveja01   1889     1    SL4   AA  27  79  12  18   2   2  0   7   0 NA
    ## 4436 stoveha01   1889     1    PH4   AA 137 556 152 171  38  13 19 119  63 NA
    ## 4437 stratsc01   1889     1    LS2   AA  62 229  30  66   7   5  4  34  10 NA
    ## 4438 striccu01   1889     1    CL4   NL 136 566  83 142  10   4  1  47  32 NA
    ## 4439 sullima01   1889     1    IN3   NL  69 256  45  73  11   3  4  35  15 NA
    ## 4440 sullimi02   1889     1    WS8   NL   9  19   2   1   0   0  0   0   0 NA
    ## 4441 sullito01   1889     1    KC2   AA  10  33   8   5   1   0  0   1   0 NA
    ## 4442 sundabi01   1889     1    PIT   NL  81 321  62  77  10   6  2  25  47 NA
    ## 4443 sutclsy01   1889     1    CL4   NL  46 161  17  40   3   2  1  21   5 NA
    ## 4444 swartpa01   1889     1    KC2   AA  51 174  19  25   4   0  0  20   7 NA
    ## 4445 sweenpe01   1889     1    WS8   NL  49 193  13  44   7   3  1  23   8 NA
    ## 4446 sweenpe01   1889     2    SL4   AA   9  38   8  14   2   0  0   8   2 NA
    ## 4447  tatepo01   1889     1    BL2   AA  72 253  28  46   6   3  1  27   4 NA
    ## 4448 tebeage01   1889     1    CN2   AA 135 496 110 125  21  11  7  70  61 NA
    ## 4449 tebeapa01   1889     1    CL4   NL 136 521  72 147  20   6  8  76  26 NA
    ## 4450 tenerjo01   1889     1    CHN   NL  42 150  18  41   4   2  1  19   2 NA
    ## 4451 terryad01   1889     1    BR3   AA  49 160  29  48   6   6  2  26   8 NA
    ## 4452 thompsa01   1889     1    PHI   NL 128 533 103 158  36   4 20 111  24 NA
    ## 4453 thornjo01   1889     1    WS8   NL   1   4   0   0   0   0  0   1   0 NA
    ## 4454 tiernmi01   1889     1    NY1   NL 122 499 147 167  23  14 10  73  33 NA
    ## 4455 titcoca01   1889     1    NY1   NL   3  12   2   1   0   0  0   0   0 NA
    ## 4456 tomneph01   1889     1    LS2   AA 112 376  61  80   8   5  4  38  26 NA
    ## 4457 traffjo01   1889     1    LS2   AA   1   2   0   1   0   0  0   0   0 NA
    ## 4458 tucketo01   1889     1    BL2   AA 134 527 103 196  22  11  5  99  63 NA
    ## 4459 twitcla01   1889     1    CL4   NL 134 549  73 151  16  11  4  95  17 NA
    ## 4460 vanhage01   1889     1    CHN   NL 134 543 126 175  20  10  9  81  28 NA
    ## 4461 vaughfa01   1889     1    LS2   AA  90 360  39  86  11   5  3  45  13 NA
    ## 4462  viaule01   1889     1    CN2   AA  47 147  14  21   2   1  0   9   4 NA
    ## 4463 visnejo01   1889     1    BR3   AA  80 295  56  76  12  10  8  68  13 NA
    ## 4464  wardjo01   1889     1    NY1   NL 114 479  87 143  13   4  1  67  62 NA
    ## 4465  wardpi01   1889     1    PHI   NL   7  25   0   4   1   0  0   4   1 NA
    ## 4466 weavefa01   1889     1    LS2   AA 124 499  62 145  17   6  0  60  21 NA
    ## 4467 weckbpe01   1889     1    IN3   NL   1   1   0   0   0   0  0   0   0 NA
    ## 4468 welchcu01   1889     1    PH4   AA 125 516 134 140  39   6  0  39  66 NA
    ## 4469 welchmi01   1889     1    NY1   NL  45 156  20  30   5   1  0  12   0 NA
    ## 4470 weyhigu01   1889     1    PH4   AA  54 191  16  25   2   0  0  12   4 NA
    ## 4471 weyhijo01   1889     1    CL6   AA   1   0   0   0   0   0  0   0   0 NA
    ## 4472 whitapa01   1889     1    BL2   AA   1   4   0   1   0   0  0   2   0 NA
    ## 4473 whitede01   1889     1    PIT   NL  55 225  35  57  10   1  0  26   2 NA
    ## 4474 whitnar01   1889     1    NY1   NL 129 473  71 103  12   2  1  59  19 NA
    ## 4475 whitnji01   1889     1    IN3   NL  10  32   6  12   4   1  0   4   2 NA
    ## 4476 widnewi01   1889     1    CL6   AA  41 133  16  28   3   0  2  10   5 NA
    ## 4477 willine01   1889     1    CHN   NL  47 173  16  41   3   1  1  30   2 NA
    ## 4478 wilmowa01   1889     1    WS8   NL 108 432  88 125  19  19  9  57  40 NA
    ## 4479  wisesa01   1889     1    WS8   NL 121 472  79 118  15   8  4  62  24 NA
    ## 4480  wolfji01   1889     1    LS2   AA 130 546  72 159  20   9  3  57  18 NA
    ## 4481  woodge01   1889     1    PHI   NL  97 422  77 106  21   4  5  53  17 NA
    ## 4482  woodge01   1889     2    BL2   AA   3  10   1   2   0   0  0   1   1 NA
    ## 4483  woodpe01   1889     1    PHI   NL   3   8   0   0   0   0  0   2   0 NA
    ## 4484 zimmech01   1889     1    CL4   NL  84 259  47  67   9   9  1  21  14 NA
    ## 4485 abbotda01   1890     1    TL2   AA   3   7   0   1   0   1  0   1   1 NA
    ## 4486 adamsji01   1890     1    SL4   AA   1   4   0   1   0   0  0   0   0 NA
    ## 4487 allenbo01   1890     1    PHI   NL 133 456  69 103  15  11  2  57  13 NA
    ## 4488 alvorbi01   1890     1    TL2   AA 116 495  69 135  13  16  2  52  21 NA
    ## 4489 anderda01   1890     1    PHI   NL   3   9   1   1   0   0  0   0   0 NA
    ## 4490 anderda01   1890     2    PIT   NL  13  42   4   3   0   0  0   0   0 NA
    ## 4491 andreed01   1890     1    BRP   PL  94 395  84 100  14   2  3  38  21 NA
    ## 4492 andreji01   1890     1    CHN   NL  53 202  32  38   4   2  3  17  11 NA
    ## 4493 ansonca01   1890     1    CHN   NL 139 504  95 157  14   5  7 107  29 NA
    ## 4494 ardnejo01   1890     1    CL4   NL  84 323  28  72  13   1  0  35   9 NA
    ## 4495 bakelje01   1890     1    CLP   PL  43 138  10  28   3   0  0   9   0 NA
    ## 4496 bakerki01   1890     1    PIT   NL  26  68   6  10   0   0  0   0   1 NA
    ## 4497 bakerno01   1890     1    BL3   AA   2   7   0   0   0   0  0   0   0 NA
    ## 4498 baldwki01   1890     1    CIN   NL  22  72   5  11   0   0  0  10   2 NA
    ## 4499 baldwki01   1890     2    PH4   AA  24  90   5  21   1   2  0  12   2 NA
    ## 4500 baldwla01   1890     1    BRO   NL   2   3   1   0   0   0  0   0   0 NA
    ## 4501 baldwla01   1890     2    BFP   PL   7  28   4   8   1   0  0   2   0 NA
    ## 4502 baldwma01   1890     1    CHP   PL  58 212  27  45   4   6  1  25   4 NA
    ## 4503  barrbo01   1890     1    RC2   AA  57 201  22  36   2   0  2  15   1 NA
    ## 4504 bartsch01   1890     1    CHP   PL  26  78   7  13   1   0  0   6   2 NA
    ## 4505 bassech01   1890     1    NY1   NL 100 410  52  98  13   8  0  54  14 NA
    ## 4506 bastich01   1890     1    CHP   PL  80 283  38  54  10   5  0  29   4 NA
    ## 4507 battijo01   1890     1    SR2   AA  29 119  15  25   2   1  0  13   8 NA
    ## 4508 beardol01   1890     1    CIN   NL 122 492  64 132  17  15  3  72  30 NA
    ## 4509 beatied01   1890     1    CL4   NL  54 191  25  27   4   3  1  21   2 NA
    ## 4510 becklja01   1890     1    PTP   PL 124 529 110 171  38  22  9 123  18 NA
    ## 4511 beeched01   1890     1    BFP   PL 126 536  69 159  22  10  3  90  14 NA
    ## 4512 bennech01   1890     1    BSN   NL  85 281  59  60  17   2  3  40   6 NA
    ## 4513 bergetu01   1890     1    PIT   NL 104 391  64 104  18   4  0  40  11 NA
    ## 4514 bierblo01   1890     1    BRP   PL 133 589 128 180  31  11  7  99  16 NA
    ## 4515 blauvhe01   1890     1    RC2   AA   2   6   3   3   0   0  0   1   3 NA
    ## 4516 blighne01   1890     1    CL6   AA   8  29   2   6   2   0  0   5   0 NA
    ## 4517 blighne01   1890     2    LS2   AA  24  73   9  15   0   0  1   9   1 NA
    ## 4518 bowesfr01   1890     1    BR4   AA  61 232  28  51   5   2  0  24  11 NA
    ## 4519 bowmasu01   1890     1    PHI   NL   1   4   0   2   0   0  0   1   0 NA
    ## 4520 bowmasu01   1890     2    PIT   NL  10  36   7  10   1   0  0   3   0 NA
    ## 4521 boyleja01   1890     1    CHP   PL 100 369  56  96   9   5  1  49  11 NA
    ## 4522 brennji01   1890     1    CLP   PL  59 233  32  59   3   7  0  26   8 NA
    ## 4523 brigggr01   1890     1    SR2   AA  86 316  44  57   6   5  0  21   7 NA
    ## 4524 brodist01   1890     1    BSN   NL 132 514  77 152  19   9  0  67  29 NA
    ## 4525 broutda01   1890     1    BSP   PL 126 475 123 159  38  10  2 102  29 NA
    ## 4526 brownpe01   1890     1    CLP   PL 118 493 112 184  40   8  5  93  35 NA
    ## 4527 brownto01   1890     1    BSP   PL 131 558 149 156  25  14  4  67  80 NA
    ## 4528 brownwi01   1890     1    NYP   PL  60 230  47  64   8   4  4  43   5 NA
    ## 4529 buckldi01   1890     1    NY1   NL  70 266  39  68  11   0  2  26   3 NA
    ## 4530 buckljo01   1890     1    BFP   PL   4  15   1   0   0   0  0   0   0 NA
    ## 4531    budd01   1890     1    CLP   PL   1   4   0   0   0   0  0   0   0 NA
    ## 4532 buffich01   1890     1    PHP   PL  42 150  24  41   3   2  1  24   1 NA
    ## 4533 burkeda01   1890     1    RC2   AA  32 102  14  22   1   0  0   9   2 NA
    ## 4534 burkeda01   1890     2    SR2   AA   9  20   1   0   0   0  0   0   0 NA
    ## 4535 burkeed01   1890     1    PHI   NL 100 430  85 113  16  11  4  50  38 NA
    ## 4536 burkeed01   1890     2    PIT   NL  31 124  17  26   5   2  1   7   6 NA
    ## 4537 burkeje01   1890     1    NY1   NL 101 401  67 124  23  13  4  60  14 NA
    ## 4538 burkejo01   1890     1    SL4   AA   2   6   3   4   0   0  0   2   0 NA
    ## 4539 burnsoy01   1890     1    BRO   NL 119 472 102 134  22  12 13 128  21 NA
    ## 4540 burnsto01   1890     1    CHN   NL 139 538  86 149  17   6  5  86  44 NA
    ## 4541 bushodo01   1890     1    BRO   NL  16  55   5  13   2   0  0   7   2 NA
    ## 4542 calihwi01   1890     1    RC2   AA  48 159  16  23   4   2  1  14   2 NA
    ## 4543 campaco01   1890     1    SL4   AA  75 314  68 101   9  12  9  75  36 NA
    ## 4544 campbsa01   1890     1    PH4   AA   2   5   0   0   0   0  0   0   0 NA
    ## 4545 cantzba01   1890     1    PH4   AA   5  22   1   1   0   0  0   1   0 NA
    ##       BB  SO IBB HBP SH SF GIDP
    ## 1      0   0  NA  NA NA NA    0
    ## 2      4   0  NA  NA NA NA    0
    ## 3      2   5  NA  NA NA NA    1
    ## 4      0   2  NA  NA NA NA    0
    ## 5      2   1  NA  NA NA NA    0
    ## 6      0   1  NA  NA NA NA    0
    ## 7      1   0  NA  NA NA NA    0
    ## 8     13   1  NA  NA NA NA    1
    ## 9      0   0  NA  NA NA NA    0
    ## 10     0   0  NA  NA NA NA    0
    ## 11     3   4  NA  NA NA NA    0
    ## 12     1   0  NA  NA NA NA    0
    ## 13     2   0  NA  NA NA NA    2
    ## 14     0   0  NA  NA NA NA    0
    ## 15     2   2  NA  NA NA NA    1
    ## 16     9   2  NA  NA NA NA    2
    ## 17     0   3  NA  NA NA NA    0
    ## 18     0   0  NA  NA NA NA    0
    ## 19     4   2  NA  NA NA NA    0
    ## 20     1   0  NA  NA NA NA    0
    ## 21     3   2  NA  NA NA NA    3
    ## 22     4   4  NA  NA NA NA    1
    ## 23     7   2  NA  NA NA NA    1
    ## 24     0   0  NA  NA NA NA    0
    ## 25     1   1  NA  NA NA NA    0
    ## 26     2   1  NA  NA NA NA    0
    ## 27     8   3  NA  NA NA NA    3
    ## 28     8   2  NA  NA NA NA    1
    ## 29     0   0  NA  NA NA NA    0
    ## 30     3   0  NA  NA NA NA    3
    ## 31    10   2  NA  NA NA NA    1
    ## 32     2   0  NA  NA NA NA    0
    ## 33     1   2  NA  NA NA NA    0
    ## 34     3   2  NA  NA NA NA    0
    ## 35     4   3  NA  NA NA NA    0
    ## 36     0   0  NA  NA NA NA    0
    ## 37     3   2  NA  NA NA NA    0
    ## 38     3   1  NA  NA NA NA    2
    ## 39     3   2  NA  NA NA NA    1
    ## 40     0   0  NA  NA NA NA    0
    ## 41     4   0  NA  NA NA NA    0
    ## 42     4   2  NA  NA NA NA    1
    ## 43     3   2  NA  NA NA NA    0
    ## 44     2   1  NA  NA NA NA    2
    ## 45     4   0  NA  NA NA NA    1
    ## 46     5   1  NA  NA NA NA    0
    ## 47     3   1  NA  NA NA NA    2
    ## 48     4   2  NA  NA NA NA    0
    ## 49     3   1  NA  NA NA NA    1
    ## 50     8   0  NA  NA NA NA    0
    ## 51     2   0  NA  NA NA NA    0
    ## 52     1   7  NA  NA NA NA    0
    ## 53     2   4  NA  NA NA NA    0
    ## 54     4   0  NA  NA NA NA    0
    ## 55     2   0  NA  NA NA NA    0
    ## 56     2   0  NA  NA NA NA    0
    ## 57     7   0  NA  NA NA NA    0
    ## 58     1   4  NA  NA NA NA    1
    ## 59     0   1  NA  NA NA NA    0
    ## 60     6   1  NA  NA NA NA    0
    ## 61     3   2  NA  NA NA NA    2
    ## 62     8   1  NA  NA NA NA    0
    ## 63     1   1  NA  NA NA NA    0
    ## 64     0   0  NA  NA NA NA    0
    ## 65     1   0  NA  NA NA NA    1
    ## 66     3   1  NA  NA NA NA    2
    ## 67     8   7  NA  NA NA NA    0
    ## 68     9   4  NA  NA NA NA    1
    ## 69     2   0  NA  NA NA NA    1
    ## 70     5   2  NA  NA NA NA    2
    ## 71     7   1  NA  NA NA NA    1
    ## 72     1   1  NA  NA NA NA    0
    ## 73     6   0  NA  NA NA NA    0
    ## 74     8   6  NA  NA NA NA    2
    ## 75     1   2  NA  NA NA NA    0
    ## 76     2   1  NA  NA NA NA    0
    ## 77     1   0  NA  NA NA NA    3
    ## 78     3   1  NA  NA NA NA    2
    ## 79     0   0  NA  NA NA NA    0
    ## 80     0   1  NA  NA NA NA    0
    ## 81     1   3  NA  NA NA NA    2
    ## 82     1   0  NA  NA NA NA    3
    ## 83     4   1  NA  NA NA NA    1
    ## 84     1   0  NA  NA NA NA    0
    ## 85     5   7  NA  NA NA NA    2
    ## 86    18   3  NA  NA NA NA    1
    ## 87     1   0  NA  NA NA NA    2
    ## 88     0   0  NA  NA NA NA    0
    ## 89     1   0  NA  NA NA NA    0
    ## 90     4   0  NA  NA NA NA    0
    ## 91     6   1  NA  NA NA NA    3
    ## 92     5   6  NA  NA NA NA    0
    ## 93     2   2  NA  NA NA NA    1
    ## 94     3   1  NA  NA NA NA    2
    ## 95     4   0  NA  NA NA NA    0
    ## 96     0   1  NA  NA NA NA    0
    ## 97     1   0  NA  NA NA NA    2
    ## 98     1   1  NA  NA NA NA    0
    ## 99     8   1  NA  NA NA NA    0
    ## 100    3   0  NA  NA NA NA    0
    ## 101    2   2  NA  NA NA NA    0
    ## 102    7   5  NA  NA NA NA    2
    ## 103    1   0  NA  NA NA NA    1
    ## 104    1   0  NA  NA NA NA    0
    ## 105    2   5  NA  NA NA NA    1
    ## 106   10   0  NA  NA NA NA    1
    ## 107    4   1  NA  NA NA NA    0
    ## 108    1   6  NA  NA NA NA    1
    ## 109    0   0  NA  NA NA NA    0
    ## 110   10   8  NA  NA NA NA    0
    ## 111   11   3  NA  NA NA NA    0
    ## 112    6   1  NA  NA NA NA    1
    ## 113   13   2  NA  NA NA NA    0
    ## 114    9   1  NA  NA NA NA    0
    ## 115    2   4  NA  NA NA NA    0
    ## 116    0   1  NA  NA NA NA    0
    ## 117    1   2  NA  NA NA NA    0
    ## 118    0   2  NA  NA NA NA    1
    ## 119    0   1  NA  NA NA NA    1
    ## 120    1   3  NA  NA NA NA    2
    ## 121    1   5  NA  NA NA NA    0
    ## 122   16   3  NA  NA NA NA    2
    ## 123    0   0  NA  NA NA NA    0
    ## 124    3   2  NA  NA NA NA    0
    ## 125    9   4  NA  NA NA NA    3
    ## 126    0   1  NA  NA NA NA    0
    ## 127    0   0  NA  NA NA NA    0
    ## 128    0   0  NA  NA NA NA    0
    ## 129    1   1  NA  NA NA NA    0
    ## 130    1   0  NA  NA NA NA    0
    ## 131    7   3  NA  NA NA NA    2
    ## 132    0   0  NA  NA NA NA    2
    ## 133    1   2  NA  NA NA NA    2
    ## 134    0   0  NA  NA NA NA    0
    ## 135    0   0  NA  NA NA NA    0
    ## 136    1   0  NA  NA NA NA    0
    ## 137    0   1  NA  NA NA NA    0
    ## 138    0   0  NA  NA NA NA    1
    ## 139    6   7  NA  NA NA NA    1
    ## 140    0   0  NA  NA NA NA    0
    ## 141    1   0  NA  NA NA NA    0
    ## 142    5   5  NA  NA NA NA    0
    ## 143    0   1  NA  NA NA NA    0
    ## 144    1   1  NA  NA NA NA    1
    ## 145    1   0  NA  NA NA NA    0
    ## 146    0   2  NA  NA NA NA    1
    ## 147    2   2  NA  NA NA NA    1
    ## 148    1   0  NA  NA NA NA    0
    ## 149    1   0  NA  NA NA NA    0
    ## 150    0   0  NA  NA NA NA    0
    ## 151    0   3  NA  NA NA NA    1
    ## 152    0   0  NA  NA NA NA    0
    ## 153    5   2  NA  NA NA NA    3
    ## 154    4  14  NA  NA NA NA    2
    ## 155    6  10  NA  NA NA NA    2
    ## 156    3   1  NA  NA NA NA    0
    ## 157    0   1  NA  NA NA NA    1
    ## 158    0   0  NA  NA NA NA    0
    ## 159    8   9  NA  NA NA NA    0
    ## 160    3   0  NA  NA NA NA    1
    ## 161    0   2  NA  NA NA NA    1
    ## 162    2   5  NA  NA NA NA    1
    ## 163    4   4  NA  NA NA NA    2
    ## 164    0   2  NA  NA NA NA    0
    ## 165    0   1  NA  NA NA NA    0
    ## 166    2   2  NA  NA NA NA    0
    ## 167    0   0  NA  NA NA NA    0
    ## 168    1   0  NA  NA NA NA    1
    ## 169    1   0  NA  NA NA NA    0
    ## 170    3   3  NA  NA NA NA    1
    ## 171    0   0  NA  NA NA NA    0
    ## 172    0   0  NA  NA NA NA    0
    ## 173    0   3  NA  NA NA NA    0
    ## 174    1   0  NA  NA NA NA    1
    ## 175    0   0  NA  NA NA NA    0
    ## 176    0   0  NA  NA NA NA    0
    ## 177    2   3  NA  NA NA NA    1
    ## 178    3   1  NA  NA NA NA    0
    ## 179    1   1  NA  NA NA NA    1
    ## 180    3   2  NA  NA NA NA    0
    ## 181    1   2  NA  NA NA NA    0
    ## 182    9   6  NA  NA NA NA    3
    ## 183    0   0  NA  NA NA NA    1
    ## 184    6   3  NA  NA NA NA    7
    ## 185    0   0  NA  NA NA NA    0
    ## 186    2   3  NA  NA NA NA    2
    ## 187    0   0  NA  NA NA NA    0
    ## 188    1   0  NA  NA NA NA    1
    ## 189    1   2  NA  NA NA NA    2
    ## 190    0   0  NA  NA NA NA    0
    ## 191    1   0  NA  NA NA NA    0
    ## 192    1   0  NA  NA NA NA    1
    ## 193    0   1  NA  NA NA NA    0
    ## 194    0   0  NA  NA NA NA    0
    ## 195    0   0  NA  NA NA NA    0
    ## 196    0   0  NA  NA NA NA    0
    ## 197    0   1  NA  NA NA NA    0
    ## 198    0   1  NA  NA NA NA    0
    ## 199    1   2  NA  NA NA NA    1
    ## 200    0   0  NA  NA NA NA    0
    ## 201    0   2  NA  NA NA NA    1
    ## 202    0   0  NA  NA NA NA    0
    ## 203    0   2  NA  NA NA NA    0
    ## 204   23   9  NA  NA NA NA    1
    ## 205    4   5  NA  NA NA NA    1
    ## 206    1   3  NA  NA NA NA    0
    ## 207    0   0  NA  NA NA NA    0
    ## 208    0   1  NA  NA NA NA    0
    ## 209    2   3  NA  NA NA NA    0
    ## 210    3   2  NA  NA NA NA    2
    ## 211    3   2  NA  NA NA NA    2
    ## 212    3   2  NA  NA NA NA    2
    ## 213    3   4  NA  NA NA NA    0
    ## 214    1   3  NA  NA NA NA    1
    ## 215    0   0  NA  NA NA NA    0
    ## 216    0   0  NA  NA NA NA    1
    ## 217    0   1  NA  NA NA NA    0
    ## 218    2   1  NA  NA NA NA    0
    ## 219   11   6  NA  NA NA NA    4
    ## 220    1   1  NA  NA NA NA    0
    ## 221    0   1  NA  NA NA NA    3
    ## 222    0   0  NA  NA NA NA    0
    ## 223    0   0  NA  NA NA NA    0
    ## 224    3   2  NA  NA NA NA    1
    ## 225    0   1  NA  NA NA NA    0
    ## 226    0   0  NA  NA NA NA    0
    ## 227    0   0  NA  NA NA NA    0
    ## 228    0   2  NA  NA NA NA    0
    ## 229    2   3  NA  NA NA NA    0
    ## 230    0   0  NA  NA NA NA    0
    ## 231    4   0  NA  NA NA NA    1
    ## 232    0   0  NA  NA NA NA    0
    ## 233    0   2  NA  NA NA NA    2
    ## 234    4   1  NA  NA NA NA    2
    ## 235    4   6  NA  NA NA NA    0
    ## 236    0   1  NA  NA NA NA    0
    ## 237    0   2  NA  NA NA NA    0
    ## 238    4   0  NA  NA NA NA    0
    ## 239    0   0  NA  NA NA NA    0
    ## 240    2   6  NA  NA NA NA    1
    ## 241    1   1  NA  NA NA NA    1
    ## 242    1   4  NA  NA NA NA    2
    ## 243    0   8  NA  NA NA NA    1
    ## 244    0   1  NA  NA NA NA    1
    ## 245    0   0  NA  NA NA NA    0
    ## 246    1   2  NA  NA NA NA    1
    ## 247    0   1  NA  NA NA NA    1
    ## 248    1   3  NA  NA NA NA    0
    ## 249    3   1  NA  NA NA NA    1
    ## 250    0   0  NA  NA NA NA    0
    ## 251    0   0  NA  NA NA NA    0
    ## 252    0   0  NA  NA NA NA    0
    ## 253    0   1  NA  NA NA NA    0
    ## 254    1   1  NA  NA NA NA    1
    ## 255    4   1  NA  NA NA NA    1
    ## 256    2   1  NA  NA NA NA    0
    ## 257    0   2  NA  NA NA NA    1
    ## 258    0   1  NA  NA NA NA    1
    ## 259    5  10  NA  NA NA NA    0
    ## 260    0   0  NA  NA NA NA    0
    ## 261    4   1  NA  NA NA NA    0
    ## 262    0   0  NA  NA NA NA    0
    ## 263    4   1  NA  NA NA NA    2
    ## 264    2   1  NA  NA NA NA    0
    ## 265    4   1  NA  NA NA NA    0
    ## 266    0   0  NA  NA NA NA    0
    ## 267    3   1  NA  NA NA NA    0
    ## 268    9   2  NA  NA NA NA    0
    ## 269    0   1  NA  NA NA NA    0
    ## 270    3   1  NA  NA NA NA    0
    ## 271    0   2  NA  NA NA NA    1
    ## 272    0   2  NA  NA NA NA    0
    ## 273    2   0  NA  NA NA NA    0
    ## 274    2   1  NA  NA NA NA    0
    ## 275    0   2  NA  NA NA NA    0
    ## 276    2   1  NA  NA NA NA    1
    ## 277    1   0  NA  NA NA NA    1
    ## 278    5   2  NA  NA NA NA    2
    ## 279    0   0  NA  NA NA NA    0
    ## 280    0   5  NA  NA NA NA    3
    ## 281    5   1  NA  NA NA NA    2
    ## 282   20   2  NA  NA NA NA    1
    ## 283    0   0  NA  NA NA NA    0
    ## 284    1   0  NA  NA NA NA    0
    ## 285    1   1  NA  NA NA NA    0
    ## 286    9   1  NA  NA NA NA    3
    ## 287    2   0  NA  NA NA NA    0
    ## 288    4   6  NA  NA NA NA    0
    ## 289    2   0  NA  NA NA NA    0
    ## 290    0   1  NA  NA NA NA    0
    ## 291    2   0  NA  NA NA NA    0
    ## 292    2   4  NA  NA NA NA    1
    ## 293    0   2  NA  NA NA NA    0
    ## 294    8  14  NA  NA NA NA    0
    ## 295    7   4  NA  NA NA NA    2
    ## 296    1   1  NA  NA NA NA    0
    ## 297    2   6  NA  NA NA NA    0
    ## 298    1   4  NA  NA NA NA    2
    ## 299    2   2  NA  NA NA NA    2
    ## 300    0   2  NA  NA NA NA    0
    ## 301    0   0  NA  NA NA NA    0
    ## 302    2   3  NA  NA NA NA    1
    ## 303    5   5  NA  NA NA NA    1
    ## 304    2   4  NA  NA NA NA    0
    ## 305   11   9  NA  NA NA NA    1
    ## 306    2   4  NA  NA NA NA    1
    ## 307    1   0  NA  NA NA NA    1
    ## 308    0   0  NA  NA NA NA    0
    ## 309    6   2  NA  NA NA NA    1
    ## 310    0   0  NA  NA NA NA    0
    ## 311    0   3  NA  NA NA NA    1
    ## 312    4   8  NA  NA NA NA    3
    ## 313    4   5  NA  NA NA NA    3
    ## 314    2   2  NA  NA NA NA    2
    ## 315    1   3  NA  NA NA NA    0
    ## 316    9   1  NA  NA NA NA    0
    ## 317    0   0  NA  NA NA NA    0
    ## 318    2   4  NA  NA NA NA    3
    ## 319    6   4  NA  NA NA NA    3
    ## 320    0   6  NA  NA NA NA    0
    ## 321    3   0  NA  NA NA NA    4
    ## 322    0   0  NA  NA NA NA    0
    ## 323    1   1  NA  NA NA NA    0
    ## 324    2   1  NA  NA NA NA    1
    ## 325    4   1  NA  NA NA NA    1
    ## 326    3   2  NA  NA NA NA    2
    ## 327    8   0  NA  NA NA NA    0
    ## 328    2   1  NA  NA NA NA    1
    ## 329    1   2  NA  NA NA NA    1
    ## 330    0   4  NA  NA NA NA    3
    ## 331    0   5  NA  NA NA NA    1
    ## 332    0   0  NA  NA NA NA    0
    ## 333    0   0  NA  NA NA NA    1
    ## 334    0   0  NA  NA NA NA    0
    ## 335    0   0  NA  NA NA NA    0
    ## 336    0   0  NA  NA NA NA    0
    ## 337    0   1  NA  NA NA NA    0
    ## 338    0   1  NA  NA NA NA    1
    ## 339    0   0  NA  NA NA NA    0
    ## 340    2   0  NA  NA NA NA    4
    ## 341    0   0  NA  NA NA NA    0
    ## 342   15   9  NA  NA NA NA    0
    ## 343   14   7  NA  NA NA NA    2
    ## 344    1  14  NA  NA NA NA    3
    ## 345    0   4  NA  NA NA NA    3
    ## 346   10   3  NA  NA NA NA    2
    ## 347    2   0  NA  NA NA NA    4
    ## 348    0   0  NA  NA NA NA    0
    ## 349    1   1  NA  NA NA NA    0
    ## 350    8   4  NA  NA NA NA    2
    ## 351    3   2  NA  NA NA NA    1
    ## 352    2   0  NA  NA NA NA    3
    ## 353    2   1  NA  NA NA NA    2
    ## 354    8  13  NA  NA NA NA    1
    ## 355    1   2  NA  NA NA NA    1
    ## 356    1   4  NA  NA NA NA    1
    ## 357   15   3  NA  NA NA NA    1
    ## 358    6   3  NA  NA NA NA    1
    ## 359    8   2  NA  NA NA NA    7
    ## 360    0   0  NA  NA NA NA    0
    ## 361    8   4  NA  NA NA NA    0
    ## 362    0   0  NA  NA NA NA    0
    ## 363    4   2  NA  NA NA NA    2
    ## 364    0   0  NA  NA NA NA    0
    ## 365    0   0  NA  NA NA NA    0
    ## 366    2   2  NA  NA NA NA    0
    ## 367    0   2  NA  NA NA NA    0
    ## 368    0   0  NA  NA NA NA    0
    ## 369    0   0  NA  NA NA NA    0
    ## 370    3   4  NA  NA NA NA    3
    ## 371    0   0  NA  NA NA NA    0
    ## 372    0   2  NA  NA NA NA    0
    ## 373    0   1  NA  NA NA NA    0
    ## 374    0   0  NA  NA NA NA    0
    ## 375    0   0  NA  NA NA NA    0
    ## 376    0   1  NA  NA NA NA    0
    ## 377    3   4  NA  NA NA NA    3
    ## 378    3   2  NA  NA NA NA    3
    ## 379    4   0  NA  NA NA NA    1
    ## 380    4   9  NA  NA NA NA    0
    ## 381    0   0  NA  NA NA NA    0
    ## 382    2   2  NA  NA NA NA    4
    ## 383    0   0  NA  NA NA NA    0
    ## 384    0   0  NA  NA NA NA    0
    ## 385    5   7  NA  NA NA NA    2
    ## 386    1   0  NA  NA NA NA    0
    ## 387    1   1  NA  NA NA NA    0
    ## 388    0   2  NA  NA NA NA    1
    ## 389    0   1  NA  NA NA NA    0
    ## 390    0   0  NA  NA NA NA    0
    ## 391    0   0  NA  NA NA NA    0
    ## 392    8   1  NA  NA NA NA    2
    ## 393    2   1  NA  NA NA NA    0
    ## 394    9   2  NA  NA NA NA    0
    ## 395   11   4  NA  NA NA NA    3
    ## 396    3   4  NA  NA NA NA    0
    ## 397    1   4  NA  NA NA NA    3
    ## 398    1   1  NA  NA NA NA    0
    ## 399    6   5  NA  NA NA NA    1
    ## 400    4   1  NA  NA NA NA    1
    ## 401    2   2  NA  NA NA NA    0
    ## 402    8   2  NA  NA NA NA    1
    ## 403    1  13  NA  NA NA NA    2
    ## 404    1   7  NA  NA NA NA    1
    ## 405    0   2  NA  NA NA NA    0
    ## 406    2   1  NA  NA NA NA    0
    ## 407    2   4  NA  NA NA NA    2
    ## 408    0   0  NA  NA NA NA    0
    ## 409    1   5  NA  NA NA NA    1
    ## 410    3   3  NA  NA NA NA    2
    ## 411    1   2  NA  NA NA NA    0
    ## 412    2  10  NA  NA NA NA    2
    ## 413    2   3  NA  NA NA NA    3
    ## 414    0   0  NA  NA NA NA    0
    ## 415    1   5  NA  NA NA NA    0
    ## 416    2   4  NA  NA NA NA    1
    ## 417    0   0  NA  NA NA NA    0
    ## 418    4  11  NA  NA NA NA    2
    ## 419    4   2  NA  NA NA NA    0
    ## 420    1   1  NA  NA NA NA    1
    ## 421    0   2  NA  NA NA NA    0
    ## 422    0   2  NA  NA NA NA    0
    ## 423    0   0  NA  NA NA NA    0
    ## 424    4   2  NA  NA NA NA    2
    ## 425    0  12  NA  NA NA NA    1
    ## 426    5   5  NA  NA NA NA    3
    ## 427    4   3  NA  NA NA NA    1
    ## 428    7   5  NA  NA NA NA    0
    ## 429    2   9  NA  NA NA NA    1
    ## 430    0   0  NA  NA NA NA    0
    ## 431    5   1  NA  NA NA NA    2
    ## 432    1   0  NA  NA NA NA    0
    ## 433    1   1  NA  NA NA NA    2
    ## 434    2   7  NA  NA NA NA    2
    ## 435    2   7  NA  NA NA NA    2
    ## 436    0   1  NA  NA NA NA    2
    ## 437    1   1  NA  NA NA NA    0
    ## 438    3   1  NA  NA NA NA    2
    ## 439    2   5  NA  NA NA NA    1
    ## 440    0   0  NA  NA NA NA    0
    ## 441    7  11  NA  NA NA NA    2
    ## 442    0   0  NA  NA NA NA    0
    ## 443    0   0  NA  NA NA NA    0
    ## 444    1   3  NA  NA NA NA    0
    ## 445    5   4  NA  NA NA NA    0
    ## 446    2   2  NA  NA NA NA    3
    ## 447    1   0  NA  NA NA NA    0
    ## 448    0   0  NA  NA NA NA    0
    ## 449    4   3  NA  NA NA NA    1
    ## 450    7  12  NA  NA NA NA    0
    ## 451    5   4  NA  NA NA NA    3
    ## 452    4   0  NA  NA NA NA    0
    ## 453    4   4  NA  NA NA NA    1
    ## 454    0   2  NA  NA NA NA    2
    ## 455    1   0  NA  NA NA NA    2
    ## 456    0   0  NA  NA NA NA    0
    ## 457    0   2  NA  NA NA NA    0
    ## 458    1   3  NA  NA NA NA    0
    ## 459    0   0  NA  NA NA NA    0
    ## 460    0   0  NA  NA NA NA    0
    ## 461    2   2  NA  NA NA NA    3
    ## 462    2   3  NA  NA NA NA    2
    ## 463    4   0  NA  NA NA NA    1
    ## 464    2   2  NA  NA NA NA    0
    ## 465    0   0  NA  NA NA NA    0
    ## 466    0   1  NA  NA NA NA    1
    ## 467    3   4  NA  NA NA NA    0
    ## 468    1   6  NA  NA NA NA    3
    ## 469    1   2  NA  NA NA NA    0
    ## 470    0   3  NA  NA NA NA    0
    ## 471    0   1  NA  NA NA NA    0
    ## 472    8  13  NA  NA NA NA    2
    ## 473    1   3  NA  NA NA NA    1
    ## 474    3   4  NA  NA NA NA    2
    ## 475    0   0  NA  NA NA NA    0
    ## 476    4   2  NA  NA NA NA    4
    ## 477    1   3  NA  NA NA NA    0
    ## 478    9   5  NA  NA NA NA    0
    ## 479    0   1  NA  NA NA NA    0
    ## 480    4   5  NA  NA NA NA    2
    ## 481    0   0  NA  NA NA NA    1
    ## 482    0   0  NA  NA NA NA    0
    ## 483    6   1  NA  NA NA NA    2
    ## 484    2  11  NA  NA NA NA    3
    ## 485    0   0  NA  NA NA NA    0
    ## 486    5   1  NA  NA NA NA    1
    ## 487    0   0  NA  NA NA NA    0
    ## 488    2   0  NA  NA NA NA    0
    ## 489    0   4  NA  NA NA NA    0
    ## 490    0   0  NA  NA NA NA    0
    ## 491    0   5  NA  NA NA NA    0
    ## 492    0   0  NA  NA NA NA    0
    ## 493    5  13  NA  NA NA NA    2
    ## 494    0   1  NA  NA NA NA    1
    ## 495    1   5  NA  NA NA NA    1
    ## 496    0   2  NA  NA NA NA    1
    ## 497    0   0  NA  NA NA NA    0
    ## 498    0   4  NA  NA NA NA    0
    ## 499    0   0  NA  NA NA NA    0
    ## 500    0   0  NA  NA NA NA    0
    ## 501    0   1  NA  NA NA NA    0
    ## 502    0   0  NA  NA NA NA    0
    ## 503    1   2  NA  NA NA NA    1
    ## 504    3   0  NA  NA NA NA    1
    ## 505    4   0  NA  NA NA NA    1
    ## 506    7  10  NA  NA NA NA    2
    ## 507    0   2  NA  NA NA NA    1
    ## 508    2   0  NA  NA NA NA    0
    ## 509    0   0  NA  NA NA NA    0
    ## 510    0   1  NA  NA NA NA    0
    ## 511    1   7  NA  NA NA NA    0
    ## 512    2   6  NA  NA NA NA    2
    ## 513    1   2  NA  NA NA NA    0
    ## 514    5   0  NA  NA NA NA    5
    ## 515    2   2  NA  NA NA NA    0
    ## 516    0   1  NA  NA NA NA    0
    ## 517    5   6  NA  NA NA NA    1
    ## 518    4   3  NA  NA NA NA    0
    ## 519    5   4  NA  NA NA NA    1
    ## 520    1   5  NA  NA NA NA    4
    ## 521    0   3  NA  NA NA NA    0
    ## 522    0   0  NA  NA NA NA    0
    ## 523    0   2  NA  NA NA NA    0
    ## 524    1   2  NA  NA NA NA    2
    ## 525    0   3  NA  NA NA NA    0
    ## 526    6   3  NA  NA NA NA    1
    ## 527    4   2  NA  NA NA NA    1
    ## 528    0   0  NA  NA NA NA    0
    ## 529    0   3  NA  NA NA NA    0
    ## 530    0   0  NA  NA NA NA    0
    ## 531    0   0  NA  NA NA NA    0
    ## 532    7   3  NA  NA NA NA    0
    ## 533    0   3  NA  NA NA NA    0
    ## 534    1   0  NA  NA NA NA    0
    ## 535    0   6  NA  NA NA NA    3
    ## 536    3   1  NA  NA NA NA    1
    ## 537    1   1  NA  NA NA NA    0
    ## 538    1   3  NA  NA NA NA    1
    ## 539    2   5  NA  NA NA NA    0
    ## 540    0   7  NA  NA NA NA    1
    ## 541    0   0  NA  NA NA NA    0
    ## 542    0   5  NA  NA NA NA    6
    ## 543    0   1  NA  NA NA NA    0
    ## 544    0   2  NA  NA NA NA    3
    ## 545    0   1  NA  NA NA NA    0
    ## 546    1   0  NA  NA NA NA    0
    ## 547    1  19  NA  NA NA NA    2
    ## 548    0   0  NA  NA NA NA    0
    ## 549    0   4  NA  NA NA NA    1
    ## 550    0   1  NA  NA NA NA    0
    ## 551    0   0  NA  NA NA NA    0
    ## 552    0   0  NA  NA NA NA    0
    ## 553    3  13  NA  NA NA NA    4
    ## 554    0   0  NA  NA NA NA    0
    ## 555    0   1  NA  NA NA NA    3
    ## 556    1   3  NA  NA NA NA    1
    ## 557    0   4  NA  NA NA NA    1
    ## 558    0   1  NA  NA NA NA    1
    ## 559    1   7  NA  NA NA NA    3
    ## 560    0   3  NA  NA NA NA    0
    ## 561    7   1  NA  NA NA NA    2
    ## 562    0   0  NA  NA NA NA    1
    ## 563    0   0  NA  NA NA NA    0
    ## 564    0   4  NA  NA NA NA    1
    ## 565    2   4  NA  NA NA NA    1
    ## 566    4   5  NA  NA NA NA    0
    ## 567    0   2  NA  NA NA NA    0
    ## 568    1   0  NA  NA NA NA    0
    ## 569    3  11  NA  NA NA NA    0
    ## 570    3   8  NA  NA NA NA    1
    ## 571    0   1  NA  NA NA NA    0
    ## 572    0   1  NA  NA NA NA    0
    ## 573   11  21  NA  NA NA NA    1
    ## 574    4   4  NA  NA NA NA    1
    ## 575    0   0  NA  NA NA NA    0
    ## 576    0   0  NA  NA NA NA    0
    ## 577    0   0  NA  NA NA NA    0
    ## 578    0   6  NA  NA NA NA    1
    ## 579    0   0  NA  NA NA NA    0
    ## 580    1  10  NA  NA NA NA    0
    ## 581    0   1  NA  NA NA NA    0
    ## 582    0   0  NA  NA NA NA    0
    ## 583    3   5  NA  NA NA NA    3
    ## 584    0   0  NA  NA NA NA    0
    ## 585    0   1  NA  NA NA NA    0
    ## 586    1   6  NA  NA NA NA    3
    ## 587    4   4  NA  NA NA NA    0
    ## 588    0   0  NA  NA NA NA    1
    ## 589    1   1  NA  NA NA NA    1
    ## 590    1  10  NA  NA NA NA    0
    ## 591    0   2  NA  NA NA NA    0
    ## 592    7   5  NA  NA NA NA    4
    ## 593    0   6  NA  NA NA NA    5
    ## 594    0   0  NA  NA NA NA    0
    ## 595    0   1  NA  NA NA NA    1
    ## 596    0   8  NA  NA NA NA    0
    ## 597    1   4  NA  NA NA NA    2
    ## 598    0   2  NA  NA NA NA    1
    ## 599    0   0  NA  NA NA NA    0
    ## 600    0   3  NA  NA NA NA    0
    ## 601    0   0  NA  NA NA NA    0
    ## 602    3   6  NA  NA NA NA    2
    ## 603    0   3  NA  NA NA NA    0
    ## 604    2  10  NA  NA NA NA    0
    ## 605    0   0  NA  NA NA NA    0
    ## 606    0   2  NA  NA NA NA    1
    ## 607    1   2  NA  NA NA NA    1
    ## 608    2   9  NA  NA NA NA    2
    ## 609    3   4  NA  NA NA NA    1
    ## 610    0   1  NA  NA NA NA    0
    ## 611    1   2  NA  NA NA NA    1
    ## 612    0   0  NA  NA NA NA    0
    ## 613    9   3  NA  NA NA NA    1
    ## 614    0   0  NA  NA NA NA    0
    ## 615    9  14  NA  NA NA NA    1
    ## 616    0   0  NA  NA NA NA    0
    ## 617    0   9  NA  NA NA NA    0
    ## 618    0   0  NA  NA NA NA    0
    ## 619    0   0  NA  NA NA NA    0
    ## 620    2  10  NA  NA NA NA    2
    ## 621    0   0  NA  NA NA NA    3
    ## 622    0   1  NA  NA NA NA    0
    ## 623    1   0  NA  NA NA NA    1
    ## 624    1   3  NA  NA NA NA    1
    ## 625    1   2  NA  NA NA NA    0
    ## 626    0   5  NA  NA NA NA    0
    ## 627    0   1  NA  NA NA NA    0
    ## 628    0   0  NA  NA NA NA    0
    ## 629    0   2  NA  NA NA NA    0
    ## 630    1   2  NA  NA NA NA    0
    ## 631    0   0  NA  NA NA NA    0
    ## 632    0   2  NA  NA NA NA    0
    ## 633    1   3  NA  NA NA NA    0
    ## 634    0   2  NA  NA NA NA    0
    ## 635    0   4  NA  NA NA NA    0
    ## 636    2   6  NA  NA NA NA    1
    ## 637    1   5  NA  NA NA NA    0
    ## 638    1   0  NA  NA NA NA    0
    ## 639    0   5  NA  NA NA NA    3
    ## 640    1   2  NA  NA NA NA    0
    ## 641    2   9  NA  NA NA NA    3
    ## 642    0   0  NA  NA NA NA    0
    ## 643    0   1  NA  NA NA NA    0
    ## 644    0   3  NA  NA NA NA    0
    ## 645    2   5  NA  NA NA NA    4
    ## 646    4   5  NA  NA NA NA    2
    ## 647    1   2  NA  NA NA NA    0
    ## 648    1   1  NA  NA NA NA    0
    ## 649    0  10  NA  NA NA NA    1
    ## 650    1   4  NA  NA NA NA    1
    ## 651    0   4  NA  NA NA NA    0
    ## 652    0   7  NA  NA NA NA    0
    ## 653    5   8  NA  NA NA NA    1
    ## 654    5  12  NA  NA NA NA    0
    ## 655    0   3  NA  NA NA NA    1
    ## 656    1   5  NA  NA NA NA    0
    ## 657    0   3  NA  NA NA NA    0
    ## 658    0   2  NA  NA NA NA    0
    ## 659    0   3  NA  NA NA NA    2
    ## 660    0   7  NA  NA NA NA    0
    ## 661    1   8  NA  NA NA NA    2
    ## 662    0   3  NA  NA NA NA    3
    ## 663    0   4  NA  NA NA NA    1
    ## 664    5   4  NA  NA NA NA    0
    ## 665    0   0  NA  NA NA NA    0
    ## 666    7   7  NA  NA NA NA    0
    ## 667    9   0  NA  NA NA NA    2
    ## 668    0   6  NA  NA NA NA    0
    ## 669    0   2  NA  NA NA NA    0
    ## 670    1   1  NA  NA NA NA    0
    ## 671    1   1  NA  NA NA NA    0
    ## 672    9   6  NA  NA NA NA    2
    ## 673    1   1  NA  NA NA NA    2
    ## 674    0   1  NA  NA NA NA    0
    ## 675    1   1  NA  NA NA NA    0
    ## 676    0   1  NA  NA NA NA    0
    ## 677    0   0  NA  NA NA NA    0
    ## 678    7   7  NA  NA NA NA    0
    ## 679    0   3  NA  NA NA NA    0
    ## 680    0   1  NA  NA NA NA    0
    ## 681    3   8  NA  NA NA NA    1
    ## 682    0   0  NA  NA NA NA    0
    ## 683    0   1  NA  NA NA NA    0
    ## 684    1   3  NA  NA NA NA    0
    ## 685    0   2  NA  NA NA NA    0
    ## 686    1   0  NA  NA NA NA    0
    ## 687    0   0  NA  NA NA NA    0
    ## 688    2   7  NA  NA NA NA    0
    ## 689    5   4  NA  NA NA NA    2
    ## 690    0   4  NA  NA NA NA    0
    ## 691    0   0  NA  NA NA NA    0
    ## 692    1   4  NA  NA NA NA    0
    ## 693    1   1  NA  NA NA NA    0
    ## 694    1   7  NA  NA NA NA    0
    ## 695    3  12  NA  NA NA NA    0
    ## 696    0   7  NA  NA NA NA    0
    ## 697    1   8  NA  NA NA NA    2
    ## 698    0   0  NA  NA NA NA    0
    ## 699    1   1  NA  NA NA NA    0
    ## 700    0   0  NA  NA NA NA    0
    ## 701    0   4  NA  NA NA NA    0
    ## 702    0   1  NA  NA NA NA    0
    ## 703    0   2  NA  NA NA NA    0
    ## 704    1   0  NA  NA NA NA    0
    ## 705    0   0  NA  NA NA NA    0
    ## 706    4   4  NA  NA NA NA    2
    ## 707    1   3  NA  NA NA NA    1
    ## 708    1   3  NA  NA NA NA    0
    ## 709    3   3  NA  NA NA NA    0
    ## 710    3   0  NA  NA NA NA    0
    ## 711    1   4  NA  NA NA NA    0
    ## 712    0   0  NA  NA NA NA    0
    ## 713    0   1  NA  NA NA NA    0
    ## 714    0   1  NA  NA NA NA    0
    ## 715    1   3  NA  NA NA NA    3
    ## 716    3   1  NA  NA NA NA    1
    ## 717    0   1  NA  NA NA NA    0
    ## 718    0   0  NA  NA NA NA    0
    ## 719    0   1  NA  NA NA NA    0
    ## 720    1   6  NA  NA NA NA    2
    ## 721    2   0  NA  NA NA NA    0
    ## 722    1   3  NA  NA NA NA    3
    ## 723    1   2  NA  NA NA NA    0
    ## 724    0   1  NA  NA NA NA    0
    ## 725    2   7  NA  NA NA NA    1
    ## 726    1   0  NA  NA NA NA    1
    ## 727    1   2  NA  NA NA NA    0
    ## 728    0   2  NA  NA NA NA    0
    ## 729    0   0  NA  NA NA NA    0
    ## 730    3   2  NA  NA NA NA    2
    ## 731    0   3  NA  NA NA NA    3
    ## 732    0   0  NA  NA NA NA    0
    ## 733    2   6  NA  NA NA NA    0
    ## 734    0   1  NA  NA NA NA    0
    ## 735    1   1  NA  NA NA NA    0
    ## 736    3   6  NA  NA NA NA    1
    ## 737    0   5  NA  NA NA NA    2
    ## 738    0   7  NA  NA NA NA    2
    ## 739    5   0  NA  NA NA NA   NA
    ## 740    2   6  NA  NA NA NA   NA
    ## 741    3   9  NA  NA NA NA   NA
    ## 742    0   5  NA  NA NA NA   NA
    ## 743   12   8  NA  NA NA NA   NA
    ## 744   20   8  NA  NA NA NA   NA
    ## 745    6   6  NA  NA NA NA   NA
    ## 746    0   1  NA  NA NA NA   NA
    ## 747    0   0  NA  NA NA NA   NA
    ## 748    0   2  NA  NA NA NA   NA
    ## 749    2   3  NA  NA NA NA   NA
    ## 750    2   9  NA  NA NA NA   NA
    ## 751    0   4  NA  NA NA NA   NA
    ## 752    9  11  NA  NA NA NA   NA
    ## 753    2   4  NA  NA NA NA   NA
    ## 754    3   3  NA  NA NA NA   NA
    ## 755    2   3  NA  NA NA NA   NA
    ## 756    3  12  NA  NA NA NA   NA
    ## 757    3  22  NA  NA NA NA   NA
    ## 758   13  16  NA  NA NA NA   NA
    ## 759    0   0  NA  NA NA NA   NA
    ## 760    0   0  NA  NA NA NA   NA
    ## 761    3   4  NA  NA NA NA   NA
    ## 762    1   0  NA  NA NA NA   NA
    ## 763    1   3  NA  NA NA NA   NA
    ## 764    5  12  NA  NA NA NA   NA
    ## 765    8   2  NA  NA NA NA   NA
    ## 766    0   0  NA  NA NA NA   NA
    ## 767    0   2  NA  NA NA NA   NA
    ## 768    2   4  NA  NA NA NA   NA
    ## 769    2   7  NA  NA NA NA   NA
    ## 770    0   3  NA  NA NA NA   NA
    ## 771    0   0  NA  NA NA NA   NA
    ## 772    7   4  NA  NA NA NA   NA
    ## 773    2  13  NA  NA NA NA   NA
    ## 774    9  10  NA  NA NA NA   NA
    ## 775    1  11  NA  NA NA NA   NA
    ## 776    2   4  NA  NA NA NA   NA
    ## 777    0   0  NA  NA NA NA   NA
    ## 778    2  11  NA  NA NA NA   NA
    ## 779    1   3  NA  NA NA NA   NA
    ## 780    0   8  NA  NA NA NA   NA
    ## 781    2   4  NA  NA NA NA   NA
    ## 782    0  14  NA  NA NA NA   NA
    ## 783    5   3  NA  NA NA NA   NA
    ## 784    0   0  NA  NA NA NA   NA
    ## 785    0   0  NA  NA NA NA   NA
    ## 786    1  10  NA  NA NA NA   NA
    ## 787    3   5  NA  NA NA NA   NA
    ## 788   12   6  NA  NA NA NA   NA
    ## 789    6  11  NA  NA NA NA   NA
    ## 790    2  10  NA  NA NA NA   NA
    ## 791    8   4  NA  NA NA NA   NA
    ## 792    2   4  NA  NA NA NA   NA
    ## 793    3   2  NA  NA NA NA   NA
    ## 794    5  11  NA  NA NA NA   NA
    ## 795    0   0  NA  NA NA NA   NA
    ## 796    0   0  NA  NA NA NA   NA
    ## 797    0   0  NA  NA NA NA   NA
    ## 798    3   4  NA  NA NA NA   NA
    ## 799    2   7  NA  NA NA NA   NA
    ## 800    1   3  NA  NA NA NA   NA
    ## 801    0   3  NA  NA NA NA   NA
    ## 802    1   2  NA  NA NA NA   NA
    ## 803    7  17  NA  NA NA NA   NA
    ## 804    7  10  NA  NA NA NA   NA
    ## 805    2   2  NA  NA NA NA   NA
    ## 806    0   0  NA  NA NA NA   NA
    ## 807    0   0  NA  NA NA NA   NA
    ## 808    4   6  NA  NA NA NA   NA
    ## 809   11   5  NA  NA NA NA   NA
    ## 810    0   1  NA  NA NA NA   NA
    ## 811    0   1  NA  NA NA NA   NA
    ## 812    7   5  NA  NA NA NA   NA
    ## 813    3   2  NA  NA NA NA   NA
    ## 814    0   0  NA  NA NA NA   NA
    ## 815    2   1  NA  NA NA NA   NA
    ## 816    0   1  NA  NA NA NA   NA
    ## 817    0   0  NA  NA NA NA   NA
    ## 818    2   4  NA  NA NA NA   NA
    ## 819    3   2  NA  NA NA NA   NA
    ## 820    1   3  NA  NA NA NA   NA
    ## 821    3   5  NA  NA NA NA   NA
    ## 822    0   0  NA  NA NA NA   NA
    ## 823    8  12  NA  NA NA NA   NA
    ## 824    2   3  NA  NA NA NA   NA
    ## 825    0   0  NA  NA NA NA   NA
    ## 826   15  17  NA  NA NA NA   NA
    ## 827    0   0  NA  NA NA NA   NA
    ## 828    0   0  NA  NA NA NA   NA
    ## 829    3   5  NA  NA NA NA   NA
    ## 830    0   0  NA  NA NA NA   NA
    ## 831    3   2  NA  NA NA NA   NA
    ## 832    0   1  NA  NA NA NA   NA
    ## 833    0   0  NA  NA NA NA   NA
    ## 834    1   9  NA  NA NA NA   NA
    ## 835    8   9  NA  NA NA NA   NA
    ## 836    1  15  NA  NA NA NA   NA
    ## 837    0   2  NA  NA NA NA   NA
    ## 838    6  23  NA  NA NA NA   NA
    ## 839    4  11  NA  NA NA NA   NA
    ## 840    0   0  NA  NA NA NA   NA
    ## 841    0   0  NA  NA NA NA   NA
    ## 842    2   7  NA  NA NA NA   NA
    ## 843    1  19  NA  NA NA NA   NA
    ## 844    1   6  NA  NA NA NA   NA
    ## 845    6   3  NA  NA NA NA   NA
    ## 846    1   2  NA  NA NA NA   NA
    ## 847    3   2  NA  NA NA NA   NA
    ## 848    2   5  NA  NA NA NA   NA
    ## 849    1   5  NA  NA NA NA   NA
    ## 850    1   0  NA  NA NA NA   NA
    ## 851    0   0  NA  NA NA NA   NA
    ## 852    0   1  NA  NA NA NA   NA
    ## 853    0   0  NA  NA NA NA   NA
    ## 854    0   0  NA  NA NA NA   NA
    ## 855    7   3  NA  NA NA NA   NA
    ## 856    1   3  NA  NA NA NA   NA
    ## 857    0   4  NA  NA NA NA   NA
    ## 858    8   9  NA  NA NA NA   NA
    ## 859    0   1  NA  NA NA NA   NA
    ## 860    0   0  NA  NA NA NA   NA
    ## 861   10   4  NA  NA NA NA   NA
    ## 862    0   5  NA  NA NA NA   NA
    ## 863    6   5  NA  NA NA NA   NA
    ## 864    3   7  NA  NA NA NA   NA
    ## 865    9   3  NA  NA NA NA   NA
    ## 866    7   4  NA  NA NA NA   NA
    ## 867    0   0  NA  NA NA NA   NA
    ## 868    6  17  NA  NA NA NA   NA
    ## 869    4  22  NA  NA NA NA   NA
    ## 870    1  15  NA  NA NA NA   NA
    ## 871   12  10  NA  NA NA NA   NA
    ## 872    6  19  NA  NA NA NA   NA
    ## 873    6  33  NA  NA NA NA   NA
    ## 874    0   0  NA  NA NA NA   NA
    ## 875    2  16  NA  NA NA NA   NA
    ## 876    0   9  NA  NA NA NA   NA
    ## 877    3   3  NA  NA NA NA   NA
    ## 878    8   6  NA  NA NA NA   NA
    ## 879    5  11  NA  NA NA NA   NA
    ## 880    1  15  NA  NA NA NA   NA
    ## 881    4  13  NA  NA NA NA   NA
    ## 882    4   6  NA  NA NA NA   NA
    ## 883    1   2  NA  NA NA NA   NA
    ## 884    7  21  NA  NA NA NA   NA
    ## 885    7  27  NA  NA NA NA   NA
    ## 886    9  13  NA  NA NA NA   NA
    ## 887    3   6  NA  NA NA NA   NA
    ## 888    1   5  NA  NA NA NA   NA
    ## 889    3  10  NA  NA NA NA   NA
    ## 890    0   2  NA  NA NA NA   NA
    ## 891    4  13  NA  NA NA NA   NA
    ## 892   11  15  NA  NA NA NA   NA
    ## 893    5   8  NA  NA NA NA   NA
    ## 894    0   1  NA  NA NA NA   NA
    ## 895    8  16  NA  NA NA NA   NA
    ## 896    5   5  NA  NA NA NA   NA
    ## 897    7  18  NA  NA NA NA   NA
    ## 898    0   0  NA  NA NA NA   NA
    ## 899   12  19  NA  NA NA NA   NA
    ## 900    1   1  NA  NA NA NA   NA
    ## 901    4   2  NA  NA NA NA   NA
    ## 902    3   6  NA  NA NA NA   NA
    ## 903    3   6  NA  NA NA NA   NA
    ## 904    1   2  NA  NA NA NA   NA
    ## 905    1   8  NA  NA NA NA   NA
    ## 906    2   8  NA  NA NA NA   NA
    ## 907    4   8  NA  NA NA NA   NA
    ## 908    1   0  NA  NA NA NA   NA
    ## 909   10  17  NA  NA NA NA   NA
    ## 910    2   1  NA  NA NA NA   NA
    ## 911    0   4  NA  NA NA NA   NA
    ## 912    5  23  NA  NA NA NA   NA
    ## 913    5   6  NA  NA NA NA   NA
    ## 914    0   1  NA  NA NA NA   NA
    ## 915    5   5  NA  NA NA NA   NA
    ## 916    0   3  NA  NA NA NA   NA
    ## 917    1   1  NA  NA NA NA   NA
    ## 918    1   3  NA  NA NA NA   NA
    ## 919    0   1  NA  NA NA NA   NA
    ## 920    0   0  NA  NA NA NA   NA
    ## 921    5   6  NA  NA NA NA   NA
    ## 922    1   2  NA  NA NA NA   NA
    ## 923    2   6  NA  NA NA NA   NA
    ## 924    0   1  NA  NA NA NA   NA
    ## 925    8  11  NA  NA NA NA   NA
    ## 926    0   4  NA  NA NA NA   NA
    ## 927    5   2  NA  NA NA NA   NA
    ## 928    1   2  NA  NA NA NA   NA
    ## 929    6  15  NA  NA NA NA   NA
    ## 930    6   7  NA  NA NA NA   NA
    ## 931    0   0  NA  NA NA NA   NA
    ## 932    0   2  NA  NA NA NA   NA
    ## 933    3  15  NA  NA NA NA   NA
    ## 934   20   9  NA  NA NA NA   NA
    ## 935    1   4  NA  NA NA NA   NA
    ## 936    1   7  NA  NA NA NA   NA
    ## 937    0   0  NA  NA NA NA   NA
    ## 938    9   7  NA  NA NA NA   NA
    ## 939    1   0  NA  NA NA NA   NA
    ## 940    1   1  NA  NA NA NA   NA
    ## 941    0   0  NA  NA NA NA   NA
    ## 942    4   3  NA  NA NA NA   NA
    ## 943    0   3  NA  NA NA NA   NA
    ## 944    1   5  NA  NA NA NA   NA
    ## 945    0   7  NA  NA NA NA   NA
    ## 946    9  17  NA  NA NA NA   NA
    ## 947    4   6  NA  NA NA NA   NA
    ## 948    1   5  NA  NA NA NA   NA
    ## 949    3  14  NA  NA NA NA   NA
    ## 950    3  16  NA  NA NA NA   NA
    ## 951    6   2  NA  NA NA NA   NA
    ## 952    1   0  NA  NA NA NA   NA
    ## 953    4  10  NA  NA NA NA   NA
    ## 954    0   2  NA  NA NA NA   NA
    ## 955    0   3  NA  NA NA NA   NA
    ## 956    8   3  NA  NA NA NA   NA
    ## 957    0   1  NA  NA NA NA   NA
    ## 958    9  15  NA  NA NA NA   NA
    ## 959    0   1  NA  NA NA NA   NA
    ## 960    3  11  NA  NA NA NA   NA
    ## 961    1   8  NA  NA NA NA   NA
    ## 962   13   1  NA  NA NA NA   NA
    ## 963   10  26  NA  NA NA NA   NA
    ## 964    0   0  NA  NA NA NA   NA
    ## 965    0   9  NA  NA NA NA   NA
    ## 966    7  37  NA  NA NA NA   NA
    ## 967    3  17  NA  NA NA NA   NA
    ## 968    0  14  NA  NA NA NA   NA
    ## 969    9  11  NA  NA NA NA   NA
    ## 970   13   8  NA  NA NA NA   NA
    ## 971    0   2  NA  NA NA NA   NA
    ## 972    5  15  NA  NA NA NA   NA
    ## 973    5  23  NA  NA NA NA   NA
    ## 974    6  29  NA  NA NA NA   NA
    ## 975    0   7  NA  NA NA NA   NA
    ## 976    0   1  NA  NA NA NA   NA
    ## 977   10  12  NA  NA NA NA   NA
    ## 978    0   0  NA  NA NA NA   NA
    ## 979    2  15  NA  NA NA NA   NA
    ## 980    7  14  NA  NA NA NA   NA
    ## 981   10  18  NA  NA NA NA   NA
    ## 982    7  14  NA  NA NA NA   NA
    ## 983    3  35  NA  NA NA NA   NA
    ## 984    7  33  NA  NA NA NA   NA
    ## 985    5  34  NA  NA NA NA   NA
    ## 986    5   6  NA  NA NA NA   NA
    ## 987    0   2  NA  NA NA NA   NA
    ## 988    5  36  NA  NA NA NA   NA
    ## 989    6  13  NA  NA NA NA   NA
    ## 990    0   4  NA  NA NA NA   NA
    ## 991    0  14  NA  NA NA NA   NA
    ## 992    5  16  NA  NA NA NA   NA
    ## 993    2  10  NA  NA NA NA   NA
    ## 994    3  14  NA  NA NA NA   NA
    ## 995    1   0  NA  NA NA NA   NA
    ## 996    4  17  NA  NA NA NA   NA
    ## 997    7   7  NA  NA NA NA   NA
    ## 998    0   3  NA  NA NA NA   NA
    ## 999   17  17  NA  NA NA NA   NA
    ## 1000   3  19  NA  NA NA NA   NA
    ## 1001  10  16  NA  NA NA NA   NA
    ## 1002   2  13  NA  NA NA NA   NA
    ## 1003   0   2  NA  NA NA NA   NA
    ## 1004   5  38  NA  NA NA NA   NA
    ## 1005   5  10  NA  NA NA NA   NA
    ## 1006   1   4  NA  NA NA NA   NA
    ## 1007   3   9  NA  NA NA NA   NA
    ## 1008   5  16  NA  NA NA NA   NA
    ## 1009   8  12  NA  NA NA NA   NA
    ## 1010   5  11  NA  NA NA NA   NA
    ## 1011   2  10  NA  NA NA NA   NA
    ## 1012   2  10  NA  NA NA NA   NA
    ## 1013   5  21  NA  NA NA NA   NA
    ## 1014   5   8  NA  NA NA NA   NA
    ## 1015   4   9  NA  NA NA NA   NA
    ## 1016   1   1  NA  NA NA NA   NA
    ## 1017   1   5  NA  NA NA NA   NA
    ## 1018  12  24  NA  NA NA NA   NA
    ## 1019   8  13  NA  NA NA NA   NA
    ## 1020   1   6  NA  NA NA NA   NA
    ## 1021  17  33  NA  NA NA NA   NA
    ## 1022   0   1  NA  NA NA NA   NA
    ## 1023  13  20  NA  NA NA NA   NA
    ## 1024   1  19  NA  NA NA NA   NA
    ## 1025   0   0  NA  NA NA NA   NA
    ## 1026   2   3  NA  NA NA NA   NA
    ## 1027   0   0  NA  NA NA NA   NA
    ## 1028   2   9  NA  NA NA NA   NA
    ## 1029   2  14  NA  NA NA NA   NA
    ## 1030   7  23  NA  NA NA NA   NA
    ## 1031   0   1  NA  NA NA NA   NA
    ## 1032   2  13  NA  NA NA NA   NA
    ## 1033   2  15  NA  NA NA NA   NA
    ## 1034  11  14  NA  NA NA NA   NA
    ## 1035   2  15  NA  NA NA NA   NA
    ## 1036  10   5  NA  NA NA NA   NA
    ## 1037   8  41  NA  NA NA NA   NA
    ## 1038   5  15  NA  NA NA NA   NA
    ## 1039   6  22  NA  NA NA NA   NA
    ## 1040   8  19  NA  NA NA NA   NA
    ## 1041   1   1  NA  NA NA NA   NA
    ## 1042   1   5  NA  NA NA NA   NA
    ## 1043   1   9  NA  NA NA NA   NA
    ## 1044   0   1  NA  NA NA NA   NA
    ## 1045   2   2  NA  NA NA NA   NA
    ## 1046  16  25  NA  NA NA NA   NA
    ## 1047   6   8  NA  NA NA NA   NA
    ## 1048   1  20  NA  NA NA NA   NA
    ## 1049   1  18  NA  NA NA NA   NA
    ## 1050   4  24  NA  NA NA NA   NA
    ## 1051   1   4  NA  NA NA NA   NA
    ## 1052   9  28  NA  NA NA NA   NA
    ## 1053   2   5  NA  NA NA NA   NA
    ## 1054   5  20  NA  NA NA NA   NA
    ## 1055   2  15  NA  NA NA NA   NA
    ## 1056   2  14  NA  NA NA NA   NA
    ## 1057   2   4  NA  NA NA NA   NA
    ## 1058   6  10  NA  NA NA NA   NA
    ## 1059  11  11  NA  NA NA NA   NA
    ## 1060   8   5  NA  NA NA NA   NA
    ## 1061   1   2  NA  NA NA NA   NA
    ## 1062   6  14  NA  NA NA NA   NA
    ## 1063   4  29  NA  NA NA NA   NA
    ## 1064   0   3  NA  NA NA NA   NA
    ## 1065   3  27  NA  NA NA NA   NA
    ## 1066   0   2  NA  NA NA NA   NA
    ## 1067   4  13  NA  NA NA NA   NA
    ## 1068   2  10  NA  NA NA NA   NA
    ## 1069   0   3  NA  NA NA NA   NA
    ## 1070   6  20  NA  NA NA NA   NA
    ## 1071  11  41  NA  NA NA NA   NA
    ## 1072   5  18  NA  NA NA NA   NA
    ## 1073   3  13  NA  NA NA NA   NA
    ## 1074   0   0  NA  NA NA NA   NA
    ## 1075   4   3  NA  NA NA NA   NA
    ## 1076   6  44  NA  NA NA NA   NA
    ## 1077   3   4  NA  NA NA NA   NA
    ## 1078   2  16  NA  NA NA NA   NA
    ## 1079  13  37  NA  NA NA NA   NA
    ## 1080   5  34  NA  NA NA NA   NA
    ## 1081   1  56  NA  NA NA NA   NA
    ## 1082   0   0  NA  NA NA NA   NA
    ## 1083   3  19  NA  NA NA NA   NA
    ## 1084   0  13  NA  NA NA NA   NA
    ## 1085   6  24  NA  NA NA NA   NA
    ## 1086   1   3  NA  NA NA NA   NA
    ## 1087   8  30  NA  NA NA NA   NA
    ## 1088   4   8  NA  NA NA NA   NA
    ## 1089   0   1  NA  NA NA NA   NA
    ## 1090   3  19  NA  NA NA NA   NA
    ## 1091   3  13  NA  NA NA NA   NA
    ## 1092   2  14  NA  NA NA NA   NA
    ## 1093   0   5  NA  NA NA NA   NA
    ## 1094   2  13  NA  NA NA NA   NA
    ## 1095   4  14  NA  NA NA NA   NA
    ## 1096   8  16  NA  NA NA NA   NA
    ## 1097   0   3  NA  NA NA NA   NA
    ## 1098   1  20  NA  NA NA NA   NA
    ## 1099   0   1  NA  NA NA NA   NA
    ## 1100   2  27  NA  NA NA NA   NA
    ## 1101  12  17  NA  NA NA NA   NA
    ## 1102   4  11  NA  NA NA NA   NA
    ## 1103  29  38  NA  NA NA NA   NA
    ## 1104   0   0  NA  NA NA NA   NA
    ## 1105   8  14  NA  NA NA NA   NA
    ## 1106   0   6  NA  NA NA NA   NA
    ## 1107   0   1  NA  NA NA NA   NA
    ## 1108   0   1  NA  NA NA NA   NA
    ## 1109   2  10  NA  NA NA NA   NA
    ## 1110   8  24  NA  NA NA NA   NA
    ## 1111   0   1  NA  NA NA NA   NA
    ## 1112   3  27  NA  NA NA NA   NA
    ## 1113   0   1  NA  NA NA NA   NA
    ## 1114   5  45  NA  NA NA NA   NA
    ## 1115   3   9  NA  NA NA NA   NA
    ## 1116   0   0  NA  NA NA NA   NA
    ## 1117   7  12  NA  NA NA NA   NA
    ## 1118   0  22  NA  NA NA NA   NA
    ## 1119   1   9  NA  NA NA NA   NA
    ## 1120   5  13  NA  NA NA NA   NA
    ## 1121   0   6  NA  NA NA NA   NA
    ## 1122   5  24  NA  NA NA NA   NA
    ## 1123   0   2  NA  NA NA NA   NA
    ## 1124   8  13  NA  NA NA NA   NA
    ## 1125   0  14  NA  NA NA NA   NA
    ## 1126  14  32  NA  NA NA NA   NA
    ## 1127   0   0  NA  NA NA NA   NA
    ## 1128   8   4  NA  NA NA NA   NA
    ## 1129   0   0  NA  NA NA NA   NA
    ## 1130  13  10  NA  NA NA NA   NA
    ## 1131   8  32  NA  NA NA NA   NA
    ## 1132   0   0  NA  NA NA NA   NA
    ## 1133   1  19  NA  NA NA NA   NA
    ## 1134   2  20  NA  NA NA NA   NA
    ## 1135   3  13  NA  NA NA NA   NA
    ## 1136   0   3  NA  NA NA NA   NA
    ## 1137   9  33  NA  NA NA NA   NA
    ## 1138   1  20  NA  NA NA NA   NA
    ## 1139   2  23  NA  NA NA NA   NA
    ## 1140  16  30  NA  NA NA NA   NA
    ## 1141   4  24  NA  NA NA NA   NA
    ## 1142   0   1  NA  NA NA NA   NA
    ## 1143   2  26  NA  NA NA NA   NA
    ## 1144   0   1  NA  NA NA NA   NA
    ## 1145   1   7  NA  NA NA NA   NA
    ## 1146   6  28  NA  NA NA NA   NA
    ## 1147   0   3  NA  NA NA NA   NA
    ## 1148   5  31  NA  NA NA NA   NA
    ## 1149   7   4  NA  NA NA NA   NA
    ## 1150   0   3  NA  NA NA NA   NA
    ## 1151   0   2  NA  NA NA NA   NA
    ## 1152  10  23  NA  NA NA NA   NA
    ## 1153   1   1  NA  NA NA NA   NA
    ## 1154   2  18  NA  NA NA NA   NA
    ## 1155   1   8  NA  NA NA NA   NA
    ## 1156   0   1  NA  NA NA NA   NA
    ## 1157   8  38  NA  NA NA NA   NA
    ## 1158   7  14  NA  NA NA NA   NA
    ## 1159   2  20  NA  NA NA NA   NA
    ## 1160   0   2  NA  NA NA NA   NA
    ## 1161   0   1  NA  NA NA NA   NA
    ## 1162   6   9  NA  NA NA NA   NA
    ## 1163   6  56  NA  NA NA NA   NA
    ## 1164  24  31  NA  NA NA NA   NA
    ## 1165   0  23  NA  NA NA NA   NA
    ## 1166  13  20  NA  NA NA NA   NA
    ## 1167  19  28  NA  NA NA NA   NA
    ## 1168   0   0  NA  NA NA NA   NA
    ## 1169  14  12  NA  NA NA NA   NA
    ## 1170   1   6  NA  NA NA NA   NA
    ## 1171  10  30  NA  NA NA NA   NA
    ## 1172   2   5  NA  NA NA NA   NA
    ## 1173   8  14  NA  NA NA NA   NA
    ## 1174   0   0  NA  NA NA NA   NA
    ## 1175   5  38  NA  NA NA NA   NA
    ## 1176   0   0  NA  NA NA NA   NA
    ## 1177   1   0  NA  NA NA NA   NA
    ## 1178   8  26  NA  NA NA NA   NA
    ## 1179  12  23  NA  NA NA NA   NA
    ## 1180   1  16  NA  NA NA NA   NA
    ## 1181   2  15  NA  NA NA NA   NA
    ## 1182   7  24  NA  NA NA NA   NA
    ## 1183  12  34  NA  NA NA NA   NA
    ## 1184  21  10  NA  NA NA NA   NA
    ## 1185  11  10  NA  NA NA NA   NA
    ## 1186  13  21  NA  NA NA NA   NA
    ## 1187  10  33  NA  NA NA NA   NA
    ## 1188   4  27  NA  NA NA NA   NA
    ## 1189   1   8  NA  NA NA NA   NA
    ## 1190   4  21  NA  NA NA NA   NA
    ## 1191  19  23  NA  NA NA NA   NA
    ## 1192   3  18  NA  NA NA NA   NA
    ## 1193   2   3  NA  NA NA NA   NA
    ## 1194   1   2  NA  NA NA NA   NA
    ## 1195   0   3  NA  NA NA NA   NA
    ## 1196   0   1  NA  NA NA NA   NA
    ## 1197   0   1  NA  NA NA NA   NA
    ## 1198  10  18  NA  NA NA NA   NA
    ## 1199   1   7  NA  NA NA NA   NA
    ## 1200   7  32  NA  NA NA NA   NA
    ## 1201   1   2  NA  NA NA NA   NA
    ## 1202   0  15  NA  NA NA NA   NA
    ## 1203   7  15  NA  NA NA NA   NA
    ## 1204   1   3  NA  NA NA NA   NA
    ## 1205  10   6  NA  NA NA NA   NA
    ## 1206  24  24  NA  NA NA NA   NA
    ## 1207   5  32  NA  NA NA NA   NA
    ## 1208   8  14  NA  NA NA NA   NA
    ## 1209  10  35  NA  NA NA NA   NA
    ## 1210   2   4  NA  NA NA NA   NA
    ## 1211   5  57  NA  NA NA NA   NA
    ## 1212   2   4  NA  NA NA NA   NA
    ## 1213   0   0  NA  NA NA NA   NA
    ## 1214  17  35  NA  NA NA NA   NA
    ## 1215   6  12  NA  NA NA NA   NA
    ## 1216   2  21  NA  NA NA NA   NA
    ## 1217   2  15  NA  NA NA NA   NA
    ## 1218  21  10  NA  NA NA NA   NA
    ## 1219  16  15  NA  NA NA NA   NA
    ## 1220   1   2  NA  NA NA NA   NA
    ## 1221   1   2  NA  NA NA NA   NA
    ## 1222   0   0  NA  NA NA NA   NA
    ## 1223   1  23  NA  NA NA NA   NA
    ## 1224  11  30  NA  NA NA NA   NA
    ## 1225   0   3  NA  NA NA NA   NA
    ## 1226   0   0  NA  NA NA NA   NA
    ## 1227  13  17  NA  NA NA NA   NA
    ## 1228   9  18  NA  NA NA NA   NA
    ## 1229   8  29  NA  NA NA NA   NA
    ## 1230  10  30  NA  NA NA NA   NA
    ## 1231   0   6  NA  NA NA NA   NA
    ## 1232   3   6  NA  NA NA NA   NA
    ## 1233  11  27  NA  NA NA NA   NA
    ## 1234  11  27  NA  NA NA NA   NA
    ## 1235   0   0  NA  NA NA NA   NA
    ## 1236   1  12  NA  NA NA NA   NA
    ## 1237   1   1  NA  NA NA NA   NA
    ## 1238  12  22  NA  NA NA NA   NA
    ## 1239   5  12  NA  NA NA NA   NA
    ## 1240   5   8  NA  NA NA NA   NA
    ## 1241   3   4  NA  NA NA NA   NA
    ## 1242   1   8  NA  NA NA NA   NA
    ## 1243   1   1  NA  NA NA NA   NA
    ## 1244   1   0  NA  NA NA NA   NA
    ## 1245   8  11  NA  NA NA NA   NA
    ## 1246   5   7  NA  NA NA NA   NA
    ## 1247   7  15  NA  NA NA NA   NA
    ## 1248   4  37  NA  NA NA NA   NA
    ## 1249   5   5  NA  NA NA NA   NA
    ## 1250   0   6  NA  NA NA NA   NA
    ## 1251   4   3  NA  NA NA NA   NA
    ## 1252   0   4  NA  NA NA NA   NA
    ## 1253   0   2  NA  NA NA NA   NA
    ## 1254  11  37  NA  NA NA NA   NA
    ## 1255   0   4  NA  NA NA NA   NA
    ## 1256   6   9  NA  NA NA NA   NA
    ## 1257   0   0  NA  NA NA NA   NA
    ## 1258   0   3  NA  NA NA NA   NA
    ## 1259  21   8  NA  NA NA NA   NA
    ## 1260  18  32  NA  NA NA NA   NA
    ## 1261   5  15  NA  NA NA NA   NA
    ## 1262   6  29  NA  NA NA NA   NA
    ## 1263   0  13  NA  NA NA NA   NA
    ## 1264   0   2  NA  NA NA NA   NA
    ## 1265   5  15  NA  NA NA NA   NA
    ## 1266   5  13  NA  NA NA NA   NA
    ## 1267   8  16  NA  NA NA NA   NA
    ## 1268   0   1  NA  NA NA NA   NA
    ## 1269   0   5  NA  NA NA NA   NA
    ## 1270   3  36  NA  NA NA NA   NA
    ## 1271  14  37  NA  NA NA NA   NA
    ## 1272   2  18  NA  NA NA NA   NA
    ## 1273   9  32  NA  NA NA NA   NA
    ## 1274   6  17  NA  NA NA NA   NA
    ## 1275   4  31  NA  NA NA NA   NA
    ## 1276  17  36  NA  NA NA NA   NA
    ## 1277   6  36  NA  NA NA NA   NA
    ## 1278   0   2  NA  NA NA NA   NA
    ## 1279  13  20  NA  NA NA NA   NA
    ## 1280   3  23  NA  NA NA NA   NA
    ## 1281  12  46  NA  NA NA NA   NA
    ## 1282   1   3  NA  NA NA NA   NA
    ## 1283   4   6  NA  NA NA NA   NA
    ## 1284   0   1  NA  NA NA NA   NA
    ## 1285   7   7  NA  NA NA NA   NA
    ## 1286   0   5  NA  NA NA NA   NA
    ## 1287   4  20  NA  NA NA NA   NA
    ## 1288   3   5  NA  NA NA NA   NA
    ## 1289   6  18  NA  NA NA NA   NA
    ## 1290   6  16  NA  NA NA NA   NA
    ## 1291   5  24  NA  NA NA NA   NA
    ## 1292   0   0  NA  NA NA NA   NA
    ## 1293   0  15  NA  NA NA NA   NA
    ## 1294   9   7  NA  NA NA NA   NA
    ## 1295   6  29  NA  NA NA NA   NA
    ## 1296   9  15  NA  NA NA NA   NA
    ## 1297   2  11  NA  NA NA NA   NA
    ## 1298  15  26  NA  NA NA NA   NA
    ## 1299  10  37  NA  NA NA NA   NA
    ## 1300   0   0  NA  NA NA NA   NA
    ## 1301   0   5  NA  NA NA NA   NA
    ## 1302   8  29  NA  NA NA NA   NA
    ## 1303  26   4  NA  NA NA NA   NA
    ## 1304  16  16  NA  NA NA NA   NA
    ## 1305  18  37  NA  NA NA NA   NA
    ## 1306   0   0  NA  NA NA NA   NA
    ## 1307   0   0  NA  NA NA NA   NA
    ## 1308   4  25  NA  NA NA NA   NA
    ## 1309  18  22  NA  NA NA NA   NA
    ## 1310   3  16  NA  NA NA NA   NA
    ## 1311   4  13  NA  NA NA NA   NA
    ## 1312   7  18  NA  NA NA NA   NA
    ## 1313  14  22  NA  NA NA NA   NA
    ## 1314  21  23  NA  NA NA NA   NA
    ## 1315   3  19  NA  NA NA NA   NA
    ## 1316  13  29  NA  NA NA NA   NA
    ## 1317  18  21  NA  NA NA NA   NA
    ## 1318  35   6  NA  NA NA NA   NA
    ## 1319  15  20  NA  NA NA NA   NA
    ## 1320   5  22  NA  NA NA NA   NA
    ## 1321   5  10  NA  NA NA NA   NA
    ## 1322  11  27  NA  NA NA NA   NA
    ## 1323  14  15  NA  NA NA NA   NA
    ## 1324  15  22  NA  NA NA NA   NA
    ## 1325   5  10  NA  NA NA NA   NA
    ## 1326   5  44  NA  NA NA NA   NA
    ## 1327   4  29  NA  NA NA NA   NA
    ## 1328   8   8  NA  NA NA NA   NA
    ## 1329   8   4  NA  NA NA NA   NA
    ## 1330   1   0  NA  NA NA NA   NA
    ## 1331   0   2  NA  NA NA NA   NA
    ## 1332  18  24  NA  NA NA NA   NA
    ## 1333  14  30  NA  NA NA NA   NA
    ## 1334   7   8  NA  NA NA NA   NA
    ## 1335  29  23  NA  NA NA NA   NA
    ## 1336  29  12  NA  NA NA NA   NA
    ## 1337   0   2  NA  NA NA NA   NA
    ## 1338   6  39  NA  NA NA NA   NA
    ## 1339   7  27  NA  NA NA NA   NA
    ## 1340   2   3  NA  NA NA NA   NA
    ## 1341  11  29  NA  NA NA NA   NA
    ## 1342   0  11  NA  NA NA NA   NA
    ## 1343   3  70  NA  NA NA NA   NA
    ## 1344   7  31  NA  NA NA NA   NA
    ## 1345   9  24  NA  NA NA NA   NA
    ## 1346   9  24  NA  NA NA NA   NA
    ## 1347  15   8  NA  NA NA NA   NA
    ## 1348   6  17  NA  NA NA NA   NA
    ## 1349  27  23  NA  NA NA NA   NA
    ## 1350  13  11  NA  NA NA NA   NA
    ## 1351  10  41  NA  NA NA NA   NA
    ## 1352  22  11  NA  NA NA NA   NA
    ## 1353  13  12  NA  NA NA NA   NA
    ## 1354   3  13  NA  NA NA NA   NA
    ## 1355   5  25  NA  NA NA NA   NA
    ## 1356  18  12  NA  NA NA NA   NA
    ## 1357   6   6  NA  NA NA NA   NA
    ## 1358   7   4  NA  NA NA NA   NA
    ## 1359  21  26  NA  NA NA NA   NA
    ## 1360  16  14  NA  NA NA NA   NA
    ## 1361   0   1  NA  NA NA NA   NA
    ## 1362   5  13  NA  NA NA NA   NA
    ## 1363  23  21  NA  NA NA NA   NA
    ## 1364   1   1  NA  NA NA NA   NA
    ## 1365   7   5  NA  NA NA NA   NA
    ## 1366   4   8  NA  NA NA NA   NA
    ## 1367   0   0  NA  NA NA NA   NA
    ## 1368   5   6  NA  NA NA NA   NA
    ## 1369   0   5  NA  NA NA NA   NA
    ## 1370  15  21  NA  NA NA NA   NA
    ## 1371   5   6  NA  NA NA NA   NA
    ## 1372   5  16  NA  NA NA NA   NA
    ## 1373   0   6  NA  NA NA NA   NA
    ## 1374  12  30  NA  NA NA NA   NA
    ## 1375   0   3  NA  NA NA NA   NA
    ## 1376   2   8  NA  NA NA NA   NA
    ## 1377   3  14  NA  NA NA NA   NA
    ## 1378   0   1  NA  NA NA NA   NA
    ## 1379   0   0  NA  NA NA NA   NA
    ## 1380   0   2  NA  NA NA NA   NA
    ## 1381   5   6  NA  NA NA NA   NA
    ## 1382   4  12  NA  NA NA NA   NA
    ## 1383   4  13  NA  NA NA NA   NA
    ## 1384   0   2  NA  NA NA NA   NA
    ## 1385  27  18  NA  NA NA NA   NA
    ## 1386   3  12  NA  NA NA NA   NA
    ## 1387   5  19  NA  NA NA NA   NA
    ## 1388   0   1  NA  NA NA NA   NA
    ## 1389   4   3  NA  NA NA NA   NA
    ## 1390  15   9  NA  NA NA NA   NA
    ## 1391   1   2  NA  NA NA NA   NA
    ## 1392   5   8  NA  NA NA NA   NA
    ## 1393   8   8  NA  NA NA NA   NA
    ## 1394   2  29  NA  NA NA NA   NA
    ## 1395   0   0  NA  NA NA NA   NA
    ## 1396   1   2  NA  NA NA NA   NA
    ## 1397  10  15  NA  NA NA NA   NA
    ## 1398   0  10  NA  NA NA NA   NA
    ## 1399   0   1  NA  NA NA NA   NA
    ## 1400   9  31  NA  NA NA NA   NA
    ## 1401  12  27  NA  NA NA NA   NA
    ## 1402   6   7  NA  NA NA NA   NA
    ## 1403  10  10  NA  NA NA NA   NA
    ## 1404   1  12  NA  NA NA NA   NA
    ## 1405  23  20  NA  NA NA NA   NA
    ## 1406   0   8  NA  NA NA NA   NA
    ## 1407   3   5  NA  NA NA NA   NA
    ## 1408   3   5  NA  NA NA NA   NA
    ## 1409   3  23  NA  NA NA NA   NA
    ## 1410   9   7  NA  NA NA NA   NA
    ## 1411   0   2  NA  NA NA NA   NA
    ## 1412  12  23  NA  NA NA NA   NA
    ## 1413   0   2  NA  NA NA NA   NA
    ## 1414   1  21  NA  NA NA NA   NA
    ## 1415  13   9  NA  NA NA NA   NA
    ## 1416   1   0  NA  NA NA NA   NA
    ## 1417   0   2  NA  NA NA NA   NA
    ## 1418   0   0  NA  NA NA NA   NA
    ## 1419   0   8  NA  NA NA NA   NA
    ## 1420   1   3  NA  NA NA NA   NA
    ## 1421   3   8  NA  NA NA NA   NA
    ## 1422   5  10  NA  NA NA NA   NA
    ## 1423   1  16  NA  NA NA NA   NA
    ## 1424   9   8  NA  NA NA NA   NA
    ## 1425   0   1  NA  NA NA NA   NA
    ## 1426   7  15  NA  NA NA NA   NA
    ## 1427  19  18  NA  NA NA NA   NA
    ## 1428   2   2  NA  NA NA NA   NA
    ## 1429  19  19  NA  NA NA NA   NA
    ## 1430   0   2  NA  NA NA NA   NA
    ## 1431  19  32  NA  NA NA NA   NA
    ## 1432   3   1  NA  NA NA NA   NA
    ## 1433   0   0  NA  NA NA NA   NA
    ## 1434  29  26  NA  NA NA NA   NA
    ## 1435  20   7  NA  NA NA NA   NA
    ## 1436   5  NA  NA  NA NA NA   NA
    ## 1437   0  NA  NA  NA NA NA   NA
    ## 1438   3  NA  NA  NA NA NA   NA
    ## 1439  20  33  NA  NA NA NA   NA
    ## 1440   8  NA  NA  NA NA NA   NA
    ## 1441   9  NA  NA  NA NA NA   NA
    ## 1442   0  NA  NA  NA NA NA   NA
    ## 1443   2   3  NA  NA NA NA   NA
    ## 1444   0  NA  NA  NA NA NA   NA
    ## 1445   0  NA  NA  NA NA NA   NA
    ## 1446   4  16  NA  NA NA NA   NA
    ## 1447   9  13  NA  NA NA NA   NA
    ## 1448  21   7  NA  NA NA NA   NA
    ## 1449   4  NA  NA  NA NA NA   NA
    ## 1450  26  NA  NA  NA NA NA   NA
    ## 1451   6  NA  NA  NA NA NA   NA
    ## 1452   2   3  NA  NA NA NA   NA
    ## 1453   9  24  NA  NA NA NA   NA
    ## 1454   0   1  NA  NA NA NA   NA
    ## 1455  15  28  NA  NA NA NA   NA
    ## 1456   1  NA  NA  NA NA NA   NA
    ## 1457   5  17  NA  NA NA NA   NA
    ## 1458  10  NA  NA  NA NA NA   NA
    ## 1459   0   4  NA  NA NA NA   NA
    ## 1460   0  15  NA  NA NA NA   NA
    ## 1461   3  16  NA  NA NA NA   NA
    ## 1462   0   3  NA  NA NA NA   NA
    ## 1463   3  NA  NA  NA NA NA   NA
    ## 1464   7  13  NA  NA NA NA   NA
    ## 1465   6   6  NA  NA NA NA   NA
    ## 1466   4  NA  NA  NA NA NA   NA
    ## 1467  13  20  NA  NA NA NA   NA
    ## 1468   6  18  NA  NA NA NA   NA
    ## 1469   5  31  NA  NA NA NA   NA
    ## 1470  14  24  NA  NA NA NA   NA
    ## 1471   0  NA  NA  NA NA NA   NA
    ## 1472   0  NA  NA  NA NA NA   NA
    ## 1473   0  NA  NA  NA NA NA   NA
    ## 1474   3  NA  NA  NA NA NA   NA
    ## 1475  17  NA  NA  NA NA NA   NA
    ## 1476   2  28  NA  NA NA NA   NA
    ## 1477  14  18  NA  NA NA NA   NA
    ## 1478   7  22  NA  NA NA NA   NA
    ## 1479   0  NA  NA  NA NA NA   NA
    ## 1480   4  46  NA  NA NA NA   NA
    ## 1481   7  23  NA  NA NA NA   NA
    ## 1482   2  11  NA  NA NA NA   NA
    ## 1483   4  NA  NA  NA NA NA   NA
    ## 1484   0  NA  NA  NA NA NA   NA
    ## 1485   0  11  NA  NA NA NA   NA
    ## 1486   0  NA  NA  NA NA NA   NA
    ## 1487   3  NA  NA  NA NA NA   NA
    ## 1488  23  26  NA  NA NA NA   NA
    ## 1489   0   0  NA  NA NA NA   NA
    ## 1490   0  NA  NA  NA NA NA   NA
    ## 1491   0  NA  NA  NA NA NA   NA
    ## 1492   1  21  NA  NA NA NA   NA
    ## 1493   5  12  NA  NA NA NA   NA
    ## 1494   7  22  NA  NA NA NA   NA
    ## 1495   0  NA  NA  NA NA NA   NA
    ## 1496  10  15  NA  NA NA NA   NA
    ## 1497   1  NA  NA  NA NA NA   NA
    ## 1498  16  23  NA  NA NA NA   NA
    ## 1499   4  20  NA  NA NA NA   NA
    ## 1500  23  21  NA  NA NA NA   NA
    ## 1501   2  50  NA  NA NA NA   NA
    ## 1502  12  26  NA  NA NA NA   NA
    ## 1503  12  17  NA  NA NA NA   NA
    ## 1504   5  12  NA  NA NA NA   NA
    ## 1505  10  NA  NA  NA NA NA   NA
    ## 1506   5  NA  NA  NA NA NA   NA
    ## 1507   2  49  NA  NA NA NA   NA
    ## 1508   1  NA  NA  NA NA NA   NA
    ## 1509   9  14  NA  NA NA NA   NA
    ## 1510   4  26  NA  NA NA NA   NA
    ## 1511  13   9  NA  NA NA NA   NA
    ## 1512   6  NA  NA  NA NA NA   NA
    ## 1513  27  NA  NA  NA NA NA   NA
    ## 1514   4  29  NA  NA NA NA   NA
    ## 1515   2  NA  NA  NA NA NA   NA
    ## 1516  29  19  NA  NA NA NA   NA
    ## 1517   1  NA  NA  NA NA NA   NA
    ## 1518   0  NA  NA  NA NA NA   NA
    ## 1519   0   2  NA  NA NA NA   NA
    ## 1520  26  25  NA  NA NA NA   NA
    ## 1521  10  17  NA  NA NA NA   NA
    ## 1522   6  26  NA  NA NA NA   NA
    ## 1523   5  NA  NA  NA NA NA   NA
    ## 1524  10  14  NA  NA NA NA   NA
    ## 1525   0  NA  NA  NA NA NA   NA
    ## 1526  11  22  NA  NA NA NA   NA
    ## 1527   0   1  NA  NA NA NA   NA
    ## 1528   2  25  NA  NA NA NA   NA
    ## 1529  16  21  NA  NA NA NA   NA
    ## 1530   4  NA  NA  NA NA NA   NA
    ## 1531  14  34  NA  NA NA NA   NA
    ## 1532   0   2  NA  NA NA NA   NA
    ## 1533   7  NA  NA  NA NA NA   NA
    ## 1534   0  NA  NA  NA NA NA   NA
    ## 1535   0   4  NA  NA NA NA   NA
    ## 1536  17  46  NA  NA NA NA   NA
    ## 1537   1  NA  NA  NA NA NA   NA
    ## 1538   1  24  NA  NA NA NA   NA
    ## 1539  10  27  NA  NA NA NA   NA
    ## 1540   0  NA  NA  NA NA NA   NA
    ## 1541   1  NA  NA  NA NA NA   NA
    ## 1542   1   0  NA  NA NA NA   NA
    ## 1543   5  NA  NA  NA NA NA   NA
    ## 1544   0   8  NA  NA NA NA   NA
    ## 1545  16  21  NA  NA NA NA   NA
    ## 1546   0  NA  NA  NA NA NA   NA
    ## 1547   3  NA  NA  NA NA NA   NA
    ## 1548   6  NA  NA  NA NA NA   NA
    ## 1549  10  NA  NA  NA NA NA   NA
    ## 1550   5  NA  NA  NA NA NA   NA
    ## 1551   0  NA  NA  NA NA NA   NA
    ## 1552   0   0  NA  NA NA NA   NA
    ## 1553   2  NA  NA  NA NA NA   NA
    ## 1554  16  NA  NA  NA NA NA   NA
    ## 1555  14  NA  NA  NA NA NA   NA
    ## 1556   2  15  NA  NA NA NA   NA
    ## 1557   4  NA  NA  NA NA NA   NA
    ## 1558   5  13  NA  NA NA NA   NA
    ## 1559   4  NA  NA  NA NA NA   NA
    ## 1560   7  NA  NA  NA NA NA   NA
    ## 1561   0  NA  NA  NA NA NA   NA
    ## 1562   9  NA  NA  NA NA NA   NA
    ## 1563   8  18  NA  NA NA NA   NA
    ## 1564   3  NA  NA  NA NA NA   NA
    ## 1565   0  NA  NA  NA NA NA   NA
    ## 1566   0   1  NA  NA NA NA   NA
    ## 1567   1  NA  NA  NA NA NA   NA
    ## 1568   2  22  NA  NA NA NA   NA
    ## 1569   2  20  NA  NA NA NA   NA
    ## 1570   3  NA  NA  NA NA NA   NA
    ## 1571   0   1  NA  NA NA NA   NA
    ## 1572   0  NA  NA  NA NA NA   NA
    ## 1573   0  11  NA  NA NA NA   NA
    ## 1574  11  NA  NA  NA NA NA   NA
    ## 1575   0  NA  NA  NA NA NA   NA
    ## 1576   0   1  NA  NA NA NA   NA
    ## 1577   0  NA  NA  NA NA NA   NA
    ## 1578   4  NA  NA  NA NA NA   NA
    ## 1579  18  29  NA  NA NA NA   NA
    ## 1580   0   2  NA  NA NA NA   NA
    ## 1581   4  NA  NA  NA NA NA   NA
    ## 1582   2  NA  NA  NA NA NA   NA
    ## 1583   0   5  NA  NA NA NA   NA
    ## 1584   2  NA  NA  NA NA NA   NA
    ## 1585   3  18  NA  NA NA NA   NA
    ## 1586  10  28  NA  NA NA NA   NA
    ## 1587  13  NA  NA  NA NA NA   NA
    ## 1588  12  NA  NA  NA NA NA   NA
    ## 1589   1  13  NA  NA NA NA   NA
    ## 1590   7  NA  NA  NA NA NA   NA
    ## 1591   7  29  NA  NA NA NA   NA
    ## 1592  13  NA  NA  NA NA NA   NA
    ## 1593   1  10  NA  NA NA NA   NA
    ## 1594   5   5  NA  NA NA NA   NA
    ## 1595  13  13  NA  NA NA NA   NA
    ## 1596   5  NA  NA  NA NA NA   NA
    ## 1597   1  24  NA  NA NA NA   NA
    ## 1598   7  18  NA  NA NA NA   NA
    ## 1599   1  NA  NA  NA NA NA   NA
    ## 1600   3  NA  NA  NA NA NA   NA
    ## 1601  19  27  NA  NA NA NA   NA
    ## 1602   3  NA  NA  NA NA NA   NA
    ## 1603  14  27  NA  NA NA NA   NA
    ## 1604   8  16  NA  NA NA NA   NA
    ## 1605  12  22  NA  NA NA NA   NA
    ## 1606  23  NA  NA  NA NA NA   NA
    ## 1607   0  NA  NA  NA NA NA   NA
    ## 1608   1   2  NA  NA NA NA   NA
    ## 1609   0  NA  NA  NA NA NA   NA
    ## 1610  11  33  NA  NA NA NA   NA
    ## 1611  11  27  NA  NA NA NA   NA
    ## 1612  11  NA  NA  NA NA NA   NA
    ## 1613   9  11  NA  NA NA NA   NA
    ## 1614   1  13  NA  NA NA NA   NA
    ## 1615   3  41  NA  NA NA NA   NA
    ## 1616   4   9  NA  NA NA NA   NA
    ## 1617  12   0  NA  NA NA NA   NA
    ## 1618  19  18  NA  NA NA NA   NA
    ## 1619   0  NA  NA  NA NA NA   NA
    ## 1620   4  NA  NA  NA NA NA   NA
    ## 1621   0  NA  NA  NA NA NA   NA
    ## 1622   0  NA  NA  NA NA NA   NA
    ## 1623   1  NA  NA  NA NA NA   NA
    ## 1624   8  NA  NA  NA NA NA   NA
    ## 1625   7  NA  NA  NA NA NA   NA
    ## 1626   0  NA  NA  NA NA NA   NA
    ## 1627   8  NA  NA  NA NA NA   NA
    ## 1628   0   0  NA  NA NA NA   NA
    ## 1629  12  NA  NA  NA NA NA   NA
    ## 1630   0  NA  NA  NA NA NA   NA
    ## 1631  27  27  NA  NA NA NA   NA
    ## 1632   5  NA  NA  NA NA NA   NA
    ## 1633   0  NA  NA  NA NA NA   NA
    ## 1634   6  NA  NA  NA NA NA   NA
    ## 1635   0  NA  NA  NA NA NA   NA
    ## 1636   3  24  NA  NA NA NA   NA
    ## 1637   5  10  NA  NA NA NA   NA
    ## 1638   0  NA  NA  NA NA NA   NA
    ## 1639  12  NA  NA  NA NA NA   NA
    ## 1640   0  NA  NA  NA NA NA   NA
    ## 1641   0  NA  NA  NA NA NA   NA
    ## 1642   9  NA  NA  NA NA NA   NA
    ## 1643  24  NA  NA  NA NA NA   NA
    ## 1644  11   7  NA  NA NA NA   NA
    ## 1645   6  NA  NA  NA NA NA   NA
    ## 1646  22  34  NA  NA NA NA   NA
    ## 1647   1  NA  NA  NA NA NA   NA
    ## 1648  15  NA  NA  NA NA NA   NA
    ## 1649   9  NA  NA  NA NA NA   NA
    ## 1650  13  NA  NA  NA NA NA   NA
    ## 1651   9  NA  NA  NA NA NA   NA
    ## 1652   3  NA  NA  NA NA NA   NA
    ## 1653  24  25  NA  NA NA NA   NA
    ## 1654  21  NA  NA  NA NA NA   NA
    ## 1655   4  NA  NA  NA NA NA   NA
    ## 1656   0   1  NA  NA NA NA   NA
    ## 1657   8  NA  NA  NA NA NA   NA
    ## 1658   0  NA  NA  NA NA NA   NA
    ## 1659   0  NA  NA  NA NA NA   NA
    ## 1660   2  11  NA  NA NA NA   NA
    ## 1661   0  13  NA  NA NA NA   NA
    ## 1662   5  10  NA  NA NA NA   NA
    ## 1663   0   1  NA  NA NA NA   NA
    ## 1664  14  NA  NA  NA NA NA   NA
    ## 1665  10  NA  NA  NA NA NA   NA
    ## 1666  13  22  NA  NA NA NA   NA
    ## 1667  12  NA  NA  NA NA NA   NA
    ## 1668   5  16  NA  NA NA NA   NA
    ## 1669   7  NA  NA  NA NA NA   NA
    ## 1670  15  16  NA  NA NA NA   NA
    ## 1671   5  NA  NA  NA NA NA   NA
    ## 1672   7  NA  NA  NA NA NA   NA
    ## 1673   2  11  NA  NA NA NA   NA
    ## 1674   1  12  NA  NA NA NA   NA
    ## 1675  24  13  NA  NA NA NA   NA
    ## 1676   2  19  NA  NA NA NA   NA
    ## 1677   0   1  NA  NA NA NA   NA
    ## 1678   3   7  NA  NA NA NA   NA
    ## 1679  27  21  NA  NA NA NA   NA
    ## 1680   0  NA  NA  NA NA NA   NA
    ## 1681   5  45  NA  NA NA NA   NA
    ## 1682   9  NA  NA  NA NA NA   NA
    ## 1683  14  30  NA  NA NA NA   NA
    ## 1684   4  36  NA  NA NA NA   NA
    ## 1685   0  NA  NA  NA NA NA   NA
    ## 1686  19  14  NA  NA NA NA   NA
    ## 1687   0   2  NA  NA NA NA   NA
    ## 1688   0  NA  NA  NA NA NA   NA
    ## 1689  18   9  NA  NA NA NA   NA
    ## 1690   6  NA  NA  NA NA NA   NA
    ## 1691   0  NA  NA  NA NA NA   NA
    ## 1692   0  NA  NA  NA NA NA   NA
    ## 1693   8  NA  NA  NA NA NA   NA
    ## 1694   2  NA  NA  NA NA NA   NA
    ## 1695   5  NA  NA  NA NA NA   NA
    ## 1696  11  NA  NA  NA NA NA   NA
    ## 1697   0   4  NA  NA NA NA   NA
    ## 1698  26  59  NA  NA NA NA   NA
    ## 1699  20  NA  NA  NA NA NA   NA
    ## 1700   9  NA  NA  NA NA NA   NA
    ## 1701   0  NA  NA  NA NA NA   NA
    ## 1702   0   1  NA  NA NA NA   NA
    ## 1703   8  NA  NA  NA NA NA   NA
    ## 1704  11  NA  NA  NA NA NA   NA
    ## 1705   0   1  NA  NA NA NA   NA
    ## 1706   3  13  NA  NA NA NA   NA
    ## 1707   2   2  NA  NA NA NA   NA
    ## 1708   1  NA  NA  NA NA NA   NA
    ## 1709  16  17  NA  NA NA NA   NA
    ## 1710   3   6  NA  NA NA NA   NA
    ## 1711   1  NA  NA  NA NA NA   NA
    ## 1712  23  NA  NA  NA NA NA   NA
    ## 1713  20  NA  NA  NA NA NA   NA
    ## 1714   6  24  NA  NA NA NA   NA
    ## 1715  14  35  NA  NA NA NA   NA
    ## 1716   0   3  NA  NA NA NA   NA
    ## 1717   2  22  NA  NA NA NA   NA
    ## 1718  13  31  NA  NA NA NA   NA
    ## 1719   7  19  NA  NA NA NA   NA
    ## 1720   1   5  NA  NA NA NA   NA
    ## 1721  19  NA  NA  NA NA NA   NA
    ## 1722   4  28  NA  NA NA NA   NA
    ## 1723  14  25  NA  NA NA NA   NA
    ## 1724   9  38  NA  NA NA NA   NA
    ## 1725   0  NA  NA  NA NA NA   NA
    ## 1726   5   4  NA  NA NA NA   NA
    ## 1727  27  NA  NA  NA NA NA   NA
    ## 1728  15  39  NA  NA NA NA   NA
    ## 1729  11  NA  NA  NA NA NA   NA
    ## 1730  25  16  NA  NA NA NA   NA
    ## 1731   6  62  NA  NA NA NA   NA
    ## 1732  12  NA  NA  NA NA NA   NA
    ## 1733   3  NA  NA  NA NA NA   NA
    ## 1734   1   5  NA  NA NA NA   NA
    ## 1735  13  NA  NA  NA NA NA   NA
    ## 1736  20  NA  NA  NA NA NA   NA
    ## 1737   3  NA  NA  NA NA NA   NA
    ## 1738   1   7  NA  NA NA NA   NA
    ## 1739   2   7  NA  NA NA NA   NA
    ## 1740   4  NA  NA  NA NA NA   NA
    ## 1741  10  36  NA  NA NA NA   NA
    ## 1742  11  29  NA  NA NA NA   NA
    ## 1743   2   5  NA  NA NA NA   NA
    ## 1744   1  NA  NA  NA NA NA   NA
    ## 1745   6  NA  NA  NA NA NA   NA
    ## 1746   9  48  NA  NA NA NA   NA
    ## 1747   0   7  NA  NA NA NA   NA
    ## 1748   0  NA  NA  NA NA NA   NA
    ## 1749  18  NA  NA  NA NA NA   NA
    ## 1750   9  NA  NA  NA NA NA   NA
    ## 1751   2  23  NA  NA NA NA   NA
    ## 1752   0  15  NA  NA NA NA   NA
    ## 1753   4  NA  NA  NA NA NA   NA
    ## 1754   3  NA  NA  NA NA NA   NA
    ## 1755  22  21  NA  NA NA NA   NA
    ## 1756   1  NA  NA  NA NA NA   NA
    ## 1757   2  29  NA  NA NA NA   NA
    ## 1758   6  NA  NA  NA NA NA   NA
    ## 1759  15  NA  NA  NA NA NA   NA
    ## 1760   8  38  NA  NA NA NA   NA
    ## 1761  20  14  NA  NA NA NA   NA
    ## 1762   0  NA  NA  NA NA NA   NA
    ## 1763   4  37  NA  NA NA NA   NA
    ## 1764   1  NA  NA  NA NA NA   NA
    ## 1765  15  21  NA  NA NA NA   NA
    ## 1766   5  29  NA  NA NA NA   NA
    ## 1767  18  21  NA  NA NA NA   NA
    ## 1768   7  NA  NA  NA NA NA   NA
    ## 1769   3  69  NA  NA NA NA   NA
    ## 1770   4  12  NA  NA NA NA   NA
    ## 1771  12  39  NA  NA NA NA   NA
    ## 1772   4  NA  NA  NA NA NA   NA
    ## 1773   1  NA  NA  NA NA NA   NA
    ## 1774  12  NA  NA  NA NA NA   NA
    ## 1775   3  NA  NA  NA NA NA   NA
    ## 1776   0   4  NA  NA NA NA   NA
    ## 1777   3  79  NA  NA NA NA   NA
    ## 1778  18  NA  NA  NA NA NA   NA
    ## 1779  14  NA  NA  NA NA NA   NA
    ## 1780   9  27  NA  NA NA NA   NA
    ## 1781  26  32  NA  NA NA NA   NA
    ## 1782   0   2  NA  NA NA NA   NA
    ## 1783  13  23  NA  NA NA NA   NA
    ## 1784  15  NA  NA  NA NA NA   NA
    ## 1785   4  NA  NA  NA NA NA   NA
    ## 1786  25  NA  NA  NA NA NA   NA
    ## 1787   4  35  NA  NA NA NA   NA
    ## 1788  27  13  NA  NA NA NA   NA
    ## 1789   0  NA  NA  NA NA NA   NA
    ## 1790  12  18  NA  NA NA NA   NA
    ## 1791   0   1  NA  NA NA NA   NA
    ## 1792   1  48  NA  NA NA NA   NA
    ## 1793   0  20  NA  NA NA NA   NA
    ## 1794   0   3  NA  NA NA NA   NA
    ## 1795  19  38  NA  NA NA NA   NA
    ## 1796  34  44  NA  NA NA NA   NA
    ## 1797  24  20  NA  NA NA NA   NA
    ## 1798  15  NA  NA  NA NA NA   NA
    ## 1799  12  NA  NA  NA NA NA   NA
    ## 1800   0   1  NA  NA NA NA   NA
    ## 1801  10  NA  NA  NA NA NA   NA
    ## 1802   0   4  NA  NA NA NA   NA
    ## 1803   7  36  NA  NA NA NA   NA
    ## 1804  18  23  NA  NA NA NA   NA
    ## 1805   2  NA  NA  NA NA NA   NA
    ## 1806   1  NA  NA  NA NA NA   NA
    ## 1807   8  54  NA  NA NA NA   NA
    ## 1808  12  31  NA  NA NA NA   NA
    ## 1809   9  18  NA  NA NA NA   NA
    ## 1810   1  NA  NA  NA NA NA   NA
    ## 1811   1  22  NA  NA NA NA   NA
    ## 1812   0   2  NA  NA NA NA   NA
    ## 1813   0  NA  NA  NA NA NA   NA
    ## 1814  12  38  NA  NA NA NA   NA
    ## 1815  20  NA  NA  NA NA NA   NA
    ## 1816   0  NA  NA  NA NA NA   NA
    ## 1817   1  11  NA  NA NA NA   NA
    ## 1818   1  NA  NA  NA NA NA   NA
    ## 1819  14  NA  NA  NA NA NA   NA
    ## 1820   0   3  NA  NA NA NA   NA
    ## 1821   3  NA  NA  NA NA NA   NA
    ## 1822   0   2  NA  NA NA NA   NA
    ## 1823  16  35  NA  NA NA NA   NA
    ## 1824  13  NA  NA  NA NA NA   NA
    ## 1825   2   2  NA  NA NA NA   NA
    ## 1826  17  NA  NA  NA NA NA   NA
    ## 1827  21  NA  NA  NA NA NA   NA
    ## 1828   2  NA  NA  NA NA NA   NA
    ## 1829  18  NA  NA  NA NA NA   NA
    ## 1830  12  NA  NA  NA NA NA   NA
    ## 1831   2  NA  NA  NA NA NA   NA
    ## 1832   0  NA  NA  NA NA NA   NA
    ## 1833   4  13  NA  NA NA NA   NA
    ## 1834   1  NA  NA  NA NA NA   NA
    ## 1835   1  31  NA  NA NA NA   NA
    ## 1836   2  NA  NA  NA NA NA   NA
    ## 1837   0  NA  NA  NA NA NA   NA
    ## 1838   0  NA  NA  NA NA NA   NA
    ## 1839   4  NA  NA  NA NA NA   NA
    ## 1840  13  NA  NA  NA NA NA   NA
    ## 1841   4  NA  NA  NA NA NA   NA
    ## 1842  18  NA  NA  NA NA NA   NA
    ## 1843  20  37  NA  NA NA NA   NA
    ## 1844  14  NA  NA  NA NA NA   NA
    ## 1845  25  NA  NA  NA NA NA   NA
    ## 1846   8  13  NA  NA NA NA   NA
    ## 1847   7  NA  NA  NA NA NA   NA
    ## 1848  10  NA  NA  NA NA NA   NA
    ## 1849   0  NA  NA  NA NA NA   NA
    ## 1850   5  NA  NA  NA NA NA   NA
    ## 1851   1  NA  NA  NA NA NA   NA
    ## 1852  19  18  NA  NA NA NA   NA
    ## 1853   2  NA  NA  NA NA NA   NA
    ## 1854   2  NA  NA  NA NA NA   NA
    ## 1855   2  14  NA  NA NA NA   NA
    ## 1856   0  NA  NA  NA NA NA   NA
    ## 1857   1   1  NA  NA NA NA   NA
    ## 1858   2  NA  NA  NA NA NA   NA
    ## 1859   6  NA  NA  NA NA NA   NA
    ## 1860   5  NA  NA  NA NA NA   NA
    ## 1861  18  NA  NA  NA NA NA   NA
    ## 1862   7  NA  NA  NA NA NA   NA
    ## 1863  15  68  NA  NA NA NA   NA
    ## 1864   0  NA  NA  NA NA NA   NA
    ## 1865   9  NA  NA  NA NA NA   NA
    ## 1866  31  NA  NA  NA NA NA   NA
    ## 1867  10  39  NA  NA NA NA   NA
    ## 1868  13  NA  NA  NA NA NA   NA
    ## 1869   0   1  NA  NA NA NA   NA
    ## 1870   0   1  NA  NA NA NA   NA
    ## 1871   3  17  NA  NA NA NA   NA
    ## 1872   1   9  NA  NA NA NA   NA
    ## 1873   2  NA  NA  NA NA NA   NA
    ## 1874   5  NA  NA  NA NA NA   NA
    ## 1875  31  NA  NA  NA NA NA   NA
    ## 1876  18  NA  NA  NA NA NA   NA
    ## 1877   1  NA  NA  NA NA NA   NA
    ## 1878   0  NA  NA  NA NA NA   NA
    ## 1879   0  NA  NA  NA NA NA   NA
    ## 1880  25  NA  NA  NA NA NA   NA
    ## 1881   5  NA  NA  NA NA NA   NA
    ## 1882   0  NA  NA  NA NA NA   NA
    ## 1883   3  15  NA  NA NA NA   NA
    ## 1884  15  13  NA  NA NA NA   NA
    ## 1885  21  NA  NA  NA NA NA   NA
    ## 1886   0  NA  NA  NA NA NA   NA
    ## 1887   0   1  NA  NA NA NA   NA
    ## 1888   0  NA  NA  NA NA NA   NA
    ## 1889   0  NA  NA  NA NA NA   NA
    ## 1890   8  50  NA  NA NA NA   NA
    ## 1891   8  49  NA  NA NA NA   NA
    ## 1892   0  NA  NA  NA NA NA   NA
    ## 1893   1   9  NA  NA NA NA   NA
    ## 1894   0   2  NA  NA NA NA   NA
    ## 1895  28  23  NA  NA NA NA   NA
    ## 1896   3  NA  NA  NA NA NA   NA
    ## 1897   0  NA  NA  NA NA NA   NA
    ## 1898  13  26  NA  NA NA NA   NA
    ## 1899  10  18  NA  NA NA NA   NA
    ## 1900   1  NA  NA  NA NA NA   NA
    ## 1901  14  16  NA  NA NA NA   NA
    ## 1902   0   5  NA  NA NA NA   NA
    ## 1903   9  26  NA  NA NA NA   NA
    ## 1904   7  NA  NA  NA NA NA   NA
    ## 1905   0  NA  NA  NA NA NA   NA
    ## 1906   4  NA  NA  NA NA NA   NA
    ## 1907   9  NA  NA  NA NA NA   NA
    ## 1908   4  NA  NA  NA NA NA   NA
    ## 1909  22  20  NA  NA NA NA   NA
    ## 1910  25  NA  NA  NA NA NA   NA
    ## 1911  15  19  NA  NA NA NA   NA
    ## 1912   6  34  NA  NA NA NA   NA
    ## 1913  11  NA  NA  NA NA NA   NA
    ## 1914   2  NA  NA  NA NA NA   NA
    ## 1915  15  14  NA  NA NA NA   NA
    ## 1916  11  NA  NA  NA NA NA   NA
    ## 1917   3  19  NA  NA NA NA   NA
    ## 1918  10  NA  NA  NA NA NA   NA
    ## 1919   1  NA  NA  NA NA NA   NA
    ## 1920   0  NA  NA  NA NA NA   NA
    ## 1921  27  39  NA  NA NA NA   NA
    ## 1922   3  36  NA  NA NA NA   NA
    ## 1923   0   2  NA  NA NA NA   NA
    ## 1924   0   0  NA  NA NA NA   NA
    ## 1925   5  11  NA  NA NA NA   NA
    ## 1926  22  NA  NA  NA NA NA   NA
    ## 1927   8  NA  NA  NA NA NA   NA
    ## 1928  20  NA  NA  NA NA NA   NA
    ## 1929  22  16  NA  NA NA NA   NA
    ## 1930  34  NA  NA  NA NA NA   NA
    ## 1931  27  NA  NA  NA NA NA   NA
    ## 1932   4  NA  NA  NA NA NA   NA
    ## 1933  19  NA  NA  NA NA NA   NA
    ## 1934  12  NA  NA  NA NA NA   NA
    ## 1935   1   4  NA  NA NA NA   NA
    ## 1936   3  NA  NA  NA NA NA   NA
    ## 1937   0  NA  NA  NA NA NA   NA
    ## 1938   0  NA  NA  NA NA NA   NA
    ## 1939   1  18  NA  NA NA NA   NA
    ## 1940  17  12  NA  NA NA NA   NA
    ## 1941  25  NA  NA  NA NA NA   NA
    ## 1942   2  10  NA  NA NA NA   NA
    ## 1943   4  NA  NA  NA NA NA   NA
    ## 1944   9  NA  NA  NA NA NA   NA
    ## 1945   4  NA  NA  NA NA NA   NA
    ## 1946  10  23  NA  NA NA NA   NA
    ## 1947   9  33  NA  NA NA NA   NA
    ## 1948   2  NA  NA  NA NA NA   NA
    ## 1949   0   1  NA  NA NA NA   NA
    ## 1950   8  25  NA  NA NA NA   NA
    ## 1951   0   2  NA  NA NA NA   NA
    ## 1952   5  21  NA  NA NA NA   NA
    ## 1953  12  NA  NA  NA NA NA   NA
    ## 1954   0  NA  NA  NA NA NA   NA
    ## 1955  10  38  NA  NA NA NA   NA
    ## 1956   6  NA  NA  NA NA NA   NA
    ## 1957   0   0  NA  NA NA NA   NA
    ## 1958  23  18  NA  NA NA NA   NA
    ## 1959  16  NA  NA  NA NA NA   NA
    ## 1960   9  NA  NA  NA NA NA   NA
    ## 1961  25  29  NA  NA NA NA   NA
    ## 1962   4  38  NA  NA NA NA   NA
    ## 1963  22  48  NA  NA NA NA   NA
    ## 1964   1  NA  NA  NA NA NA   NA
    ## 1965  13  74  NA  NA NA NA   NA
    ## 1966   5  NA  NA  NA NA NA   NA
    ## 1967   0   0  NA  NA NA NA   NA
    ## 1968  25  37  NA  NA NA NA   NA
    ## 1969  37  55  NA  NA NA NA   NA
    ## 1970   0  NA  NA   1 NA NA   NA
    ## 1971   0  NA  NA   0 NA NA   NA
    ## 1972   4  NA  NA  NA NA NA   NA
    ## 1973   1  NA  NA  NA NA NA   NA
    ## 1974   0  NA  NA   0 NA NA   NA
    ## 1975   0   0  NA  NA NA NA   NA
    ## 1976   9  42  NA  NA NA NA   NA
    ## 1977   4  NA  NA   0 NA NA   NA
    ## 1978   1   0  NA  NA NA NA   NA
    ## 1979   0   8  NA  NA NA NA   NA
    ## 1980  29  13  NA  NA NA NA   NA
    ## 1981   1  24  NA  NA NA NA   NA
    ## 1982   1   1  NA  NA NA NA   NA
    ## 1983   3  NA  NA   0 NA NA   NA
    ## 1984   4  NA  NA   1 NA NA   NA
    ## 1985   0  NA  NA  NA NA NA   NA
    ## 1986   1  NA  NA  NA NA NA   NA
    ## 1987   2  NA  NA   0 NA NA   NA
    ## 1988   0  NA  NA  NA NA NA   NA
    ## 1989  11  NA  NA  NA NA NA   NA
    ## 1990   1  NA  NA  NA NA NA   NA
    ## 1991   1  NA  NA  NA NA NA   NA
    ## 1992   0  NA  NA  NA NA NA   NA
    ## 1993   5  NA  NA  NA NA NA   NA
    ## 1994  11  NA  NA  NA NA NA   NA
    ## 1995   4  NA  NA  NA NA NA   NA
    ## 1996   0  NA  NA  NA NA NA   NA
    ## 1997   0  NA  NA  NA NA NA   NA
    ## 1998  11  NA  NA  NA NA NA   NA
    ## 1999  22  NA  NA   2 NA NA   NA
    ## 2000   0  NA  NA  NA NA NA   NA
    ## 2001   4  NA  NA   2 NA NA   NA
    ## 2002   3  NA  NA   0 NA NA   NA
    ## 2003   0   4  NA  NA NA NA   NA
    ## 2004   1  NA  NA   0 NA NA   NA
    ## 2005   4  15  NA  NA NA NA   NA
    ## 2006   3  NA  NA  NA NA NA   NA
    ## 2007   4  NA  NA  NA NA NA   NA
    ## 2008   3  NA  NA   1 NA NA   NA
    ## 2009   0  NA  NA  NA NA NA   NA
    ## 2010   0  NA  NA  NA NA NA   NA
    ## 2011   0  NA  NA   0 NA NA   NA
    ## 2012   0  NA  NA   0 NA NA   NA
    ## 2013   0   2  NA  NA NA NA   NA
    ## 2014   0  NA  NA   0 NA NA   NA
    ## 2015   0  NA  NA   0 NA NA   NA
    ## 2016   0  NA  NA  NA NA NA   NA
    ## 2017   8  31  NA  NA NA NA   NA
    ## 2018   3  NA  NA  NA NA NA   NA
    ## 2019  36  40  NA  NA NA NA   NA
    ## 2020   7  NA  NA   2 NA NA   NA
    ## 2021   1  NA  NA  NA NA NA   NA
    ## 2022   0  NA  NA   2 NA NA   NA
    ## 2023   0  NA  NA  NA NA NA   NA
    ## 2024   1  NA  NA  NA NA NA   NA
    ## 2025   0  NA  NA  NA NA NA   NA
    ## 2026   1  NA  NA  NA NA NA   NA
    ## 2027   4  NA  NA   5 NA NA   NA
    ## 2028   0  NA  NA  NA NA NA   NA
    ## 2029  10  NA  NA  NA NA NA   NA
    ## 2030   0  NA  NA  NA NA NA   NA
    ## 2031  11  NA  NA   4 NA NA   NA
    ## 2032   1  NA  NA   0 NA NA   NA
    ## 2033   4  NA  NA  NA NA NA   NA
    ## 2034   0  NA  NA   0 NA NA   NA
    ## 2035   9  NA  NA  NA NA NA   NA
    ## 2036   2  NA  NA  NA NA NA   NA
    ## 2037   7  NA  NA  NA NA NA   NA
    ## 2038  21  NA  NA   0 NA NA   NA
    ## 2039  12  NA  NA  NA NA NA   NA
    ## 2040  11  NA  NA  NA NA NA   NA
    ## 2041   1  13  NA  NA NA NA   NA
    ## 2042   6  19  NA  NA NA NA   NA
    ## 2043   1  NA  NA  NA NA NA   NA
    ## 2044   0  NA  NA  NA NA NA   NA
    ## 2045  33  20  NA  NA NA NA   NA
    ## 2046   2  NA  NA   0 NA NA   NA
    ## 2047   1  NA  NA  NA NA NA   NA
    ## 2048   0   1  NA  NA NA NA   NA
    ## 2049   1  NA  NA  NA NA NA   NA
    ## 2050   0  15  NA  NA NA NA   NA
    ## 2051  13  NA  NA  NA NA NA   NA
    ## 2052  13  NA  NA   2 NA NA   NA
    ## 2053  24  NA  NA   4 NA NA   NA
    ## 2054  16  12  NA  NA NA NA   NA
    ## 2055   4  15  NA  NA NA NA   NA
    ## 2056   1  NA  NA   0 NA NA   NA
    ## 2057   5  24  NA  NA NA NA   NA
    ## 2058  15  52  NA  NA NA NA   NA
    ## 2059   6  NA  NA  NA NA NA   NA
    ## 2060   5  NA  NA  NA NA NA   NA
    ## 2061   1  NA  NA  NA NA NA   NA
    ## 2062   7  NA  NA   3 NA NA   NA
    ## 2063   3  NA  NA   0 NA NA   NA
    ## 2064   0  NA  NA  NA NA NA   NA
    ## 2065  13  50  NA  NA NA NA   NA
    ## 2066  17  11  NA  NA NA NA   NA
    ## 2067   1  NA  NA   0 NA NA   NA
    ## 2068  12  NA  NA  NA NA NA   NA
    ## 2069   1  NA  NA  NA NA NA   NA
    ## 2070   0  NA  NA  NA NA NA   NA
    ## 2071   6  NA  NA   2 NA NA   NA
    ## 2072   0  NA  NA  NA NA NA   NA
    ## 2073   0  NA  NA  NA NA NA   NA
    ## 2074   1  NA  NA  NA NA NA   NA
    ## 2075   8  NA  NA   0 NA NA   NA
    ## 2076   6  NA  NA   4 NA NA   NA
    ## 2077   0  NA  NA  NA NA NA   NA
    ## 2078  29  39  NA  NA NA NA   NA
    ## 2079  13  NA  NA   5 NA NA   NA
    ## 2080   1  NA  NA  NA NA NA   NA
    ## 2081   0  NA  NA  NA NA NA   NA
    ## 2082   2  NA  NA  NA NA NA   NA
    ## 2083   4  NA  NA   0 NA NA   NA
    ## 2084   0  NA  NA  NA NA NA   NA
    ## 2085   0  NA  NA  NA NA NA   NA
    ## 2086   5  NA  NA   0 NA NA   NA
    ## 2087  34  55  NA  NA NA NA   NA
    ## 2088  19  NA  NA   2 NA NA   NA
    ## 2089   0   2  NA  NA NA NA   NA
    ## 2090   0  NA  NA  NA NA NA   NA
    ## 2091   2  NA  NA  NA NA NA   NA
    ## 2092   2  16  NA  NA NA NA   NA
    ## 2093   9  NA  NA  NA NA NA   NA
    ## 2094   4   8  NA  NA NA NA   NA
    ## 2095   4  NA  NA  NA NA NA   NA
    ## 2096  27  NA  NA   4 NA NA   NA
    ## 2097  29  NA  NA  13 NA NA   NA
    ## 2098   8  20  NA  NA NA NA   NA
    ## 2099   5  NA  NA   0 NA NA   NA
    ## 2100   3  NA  NA   0 NA NA   NA
    ## 2101  14  36  NA  NA NA NA   NA
    ## 2102   9  NA  NA   0 NA NA   NA
    ## 2103   5  NA  NA   5 NA NA   NA
    ## 2104   0   9  NA  NA NA NA   NA
    ## 2105   0  NA  NA  NA NA NA   NA
    ## 2106   1  NA  NA  NA NA NA   NA
    ## 2107   1  13  NA  NA NA NA   NA
    ## 2108  38  32  NA  NA NA NA   NA
    ## 2109   0   1  NA  NA NA NA   NA
    ## 2110   0  NA  NA   0 NA NA   NA
    ## 2111   0   2  NA  NA NA NA   NA
    ## 2112   8  NA  NA   2 NA NA   NA
    ## 2113  10  33  NA  NA NA NA   NA
    ## 2114   1   1  NA  NA NA NA   NA
    ## 2115  17  NA  NA   2 NA NA   NA
    ## 2116   6  NA  NA   4 NA NA   NA
    ## 2117   0  NA  NA  NA NA NA   NA
    ## 2118   0   2  NA  NA NA NA   NA
    ## 2119   2  36  NA  NA NA NA   NA
    ## 2120  14  NA  NA  NA NA NA   NA
    ## 2121  11  NA  NA  NA NA NA   NA
    ## 2122  16  NA  NA   2 NA NA   NA
    ## 2123   1  NA  NA  NA NA NA   NA
    ## 2124   0  NA  NA  NA NA NA   NA
    ## 2125   0  NA  NA  NA NA NA   NA
    ## 2126   0   1  NA  NA NA NA   NA
    ## 2127   2  NA  NA  NA NA NA   NA
    ## 2128   0  NA  NA  NA NA NA   NA
    ## 2129   6  NA  NA  NA NA NA   NA
    ## 2130   0  NA  NA  NA NA NA   NA
    ## 2131   1  NA  NA  NA NA NA   NA
    ## 2132  33  74  NA  NA NA NA   NA
    ## 2133  15  21  NA  NA NA NA   NA
    ## 2134   2  NA  NA  NA NA NA   NA
    ## 2135   1  NA  NA  NA NA NA   NA
    ## 2136   1  NA  NA  NA NA NA   NA
    ## 2137   0  NA  NA   0 NA NA   NA
    ## 2138   2  NA  NA  NA NA NA   NA
    ## 2139   1  NA  NA  NA NA NA   NA
    ## 2140   0   3  NA  NA NA NA   NA
    ## 2141  10  NA  NA  NA NA NA   NA
    ## 2142   8  NA  NA  NA NA NA   NA
    ## 2143   1  NA  NA  NA NA NA   NA
    ## 2144   0  NA  NA  NA NA NA   NA
    ## 2145  14  39  NA  NA NA NA   NA
    ## 2146   0  NA  NA  NA NA NA   NA
    ## 2147   2  NA  NA  NA NA NA   NA
    ## 2148   5  NA  NA   0 NA NA   NA
    ## 2149   0   9  NA  NA NA NA   NA
    ## 2150   0  NA  NA  NA NA NA   NA
    ## 2151   1  NA  NA   0 NA NA   NA
    ## 2152   0  NA  NA   0 NA NA   NA
    ## 2153   0  NA  NA  NA NA NA   NA
    ## 2154   3  NA  NA  NA NA NA   NA
    ## 2155   2  NA  NA  NA NA NA   NA
    ## 2156   7  NA  NA   3 NA NA   NA
    ## 2157   1  NA  NA   0 NA NA   NA
    ## 2158   5  NA  NA  NA NA NA   NA
    ## 2159   1  NA  NA   0 NA NA   NA
    ## 2160  14  58  NA  NA NA NA   NA
    ## 2161   1   3  NA  NA NA NA   NA
    ## 2162   8  NA  NA  NA NA NA   NA
    ## 2163   4  NA  NA   2 NA NA   NA
    ## 2164   3  NA  NA   0 NA NA   NA
    ## 2165   6  NA  NA   1 NA NA   NA
    ## 2166   4  NA  NA  NA NA NA   NA
    ## 2167   5  NA  NA   4 NA NA   NA
    ## 2168   1  NA  NA  NA NA NA   NA
    ## 2169   2  NA  NA   2 NA NA   NA
    ## 2170   0  NA  NA   0 NA NA   NA
    ## 2171  13  27  NA  NA NA NA   NA
    ## 2172   0  NA  NA  NA NA NA   NA
    ## 2173   2  NA  NA  NA NA NA   NA
    ## 2174   0  NA  NA  NA NA NA   NA
    ## 2175   2  NA  NA   0 NA NA   NA
    ## 2176   0  NA  NA   0 NA NA   NA
    ## 2177   0  NA  NA  NA NA NA   NA
    ## 2178   1  NA  NA  NA NA NA   NA
    ## 2179   2  NA  NA   0 NA NA   NA
    ## 2180   0  NA  NA   1 NA NA   NA
    ## 2181   0  NA  NA  NA NA NA   NA
    ## 2182   5  NA  NA   1 NA NA   NA
    ## 2183   5  NA  NA   1 NA NA   NA
    ## 2184  29  NA  NA  NA NA NA   NA
    ## 2185   0  NA  NA  NA NA NA   NA
    ## 2186   2  NA  NA  NA NA NA   NA
    ## 2187   5  NA  NA  NA NA NA   NA
    ## 2188   7  NA  NA   6 NA NA   NA
    ## 2189   6  54  NA  NA NA NA   NA
    ## 2190  16  NA  NA  NA NA NA   NA
    ## 2191   0  NA  NA  NA NA NA   NA
    ## 2192   2  NA  NA  NA NA NA   NA
    ## 2193   0   2  NA  NA NA NA   NA
    ## 2194   2  NA  NA   0 NA NA   NA
    ## 2195  12  NA  NA  10 NA NA   NA
    ## 2196  15  49  NA  NA NA NA   NA
    ## 2197   7  NA  NA  NA NA NA   NA
    ## 2198  28  22  NA  NA NA NA   NA
    ## 2199   0  NA  NA  NA NA NA   NA
    ## 2200   0  NA  NA  NA NA NA   NA
    ## 2201   1  NA  NA   4 NA NA   NA
    ## 2202   0  NA  NA  NA NA NA   NA
    ## 2203   1  NA  NA   1 NA NA   NA
    ## 2204   9  25  NA  NA NA NA   NA
    ## 2205  35  44  NA  NA NA NA   NA
    ## 2206  14  66  NA  NA NA NA   NA
    ## 2207   3  NA  NA   0 NA NA   NA
    ## 2208  20  NA  NA   0 NA NA   NA
    ## 2209  11  NA  NA   2 NA NA   NA
    ## 2210   0  NA  NA   0 NA NA   NA
    ## 2211  19  54  NA  NA NA NA   NA
    ## 2212  23  NA  NA  12 NA NA   NA
    ## 2213   0  NA  NA   0 NA NA   NA
    ## 2214   3  NA  NA  NA NA NA   NA
    ## 2215   0  NA  NA  NA NA NA   NA
    ## 2216   1  NA  NA  NA NA NA   NA
    ## 2217   0   3  NA  NA NA NA   NA
    ## 2218   0  NA  NA  NA NA NA   NA
    ## 2219   7  57  NA  NA NA NA   NA
    ## 2220  11  NA  NA  NA NA NA   NA
    ## 2221   2  NA  NA  NA NA NA   NA
    ## 2222  20  54  NA  NA NA NA   NA
    ## 2223   5  NA  NA  NA NA NA   NA
    ## 2224  27  41  NA  NA NA NA   NA
    ## 2225   0  NA  NA   0 NA NA   NA
    ## 2226   0  NA  NA  NA NA NA   NA
    ## 2227   0  NA  NA  NA NA NA   NA
    ## 2228   7  NA  NA   0 NA NA   NA
    ## 2229   0  NA  NA  NA NA NA   NA
    ## 2230   3  NA  NA   0 NA NA   NA
    ## 2231   8  NA  NA   0 NA NA   NA
    ## 2232   0  NA  NA   0 NA NA   NA
    ## 2233   0  NA  NA  NA NA NA   NA
    ## 2234   1  NA  NA   0 NA NA   NA
    ## 2235   1  NA  NA   0 NA NA   NA
    ## 2236   0  NA  NA   0 NA NA   NA
    ## 2237  11  NA  NA  NA NA NA   NA
    ## 2238   3  NA  NA  NA NA NA   NA
    ## 2239   4  NA  NA  NA NA NA   NA
    ## 2240   0  NA  NA  NA NA NA   NA
    ## 2241   0  NA  NA  NA NA NA   NA
    ## 2242   2  80  NA  NA NA NA   NA
    ## 2243   0  NA  NA  NA NA NA   NA
    ## 2244   0  NA  NA   0 NA NA   NA
    ## 2245  14  NA  NA   2 NA NA   NA
    ## 2246  10  NA  NA  NA NA NA   NA
    ## 2247   0  NA  NA  NA NA NA   NA
    ## 2248   2  34  NA  NA NA NA   NA
    ## 2249   4  NA  NA  NA NA NA   NA
    ## 2250  38  NA  NA   1 NA NA   NA
    ## 2251   6  60  NA  NA NA NA   NA
    ## 2252  13  NA  NA   5 NA NA   NA
    ## 2253   5  20  NA  NA NA NA   NA
    ## 2254  19  35  NA  NA NA NA   NA
    ## 2255   1  NA  NA  NA NA NA   NA
    ## 2256  35  41  NA  NA NA NA   NA
    ## 2257   0   3  NA  NA NA NA   NA
    ## 2258   3  NA  NA   3 NA NA   NA
    ## 2259  25  16  NA  NA NA NA   NA
    ## 2260   8  NA  NA  NA NA NA   NA
    ## 2261  27  NA  NA  12 NA NA   NA
    ## 2262  23  NA  NA  NA NA NA   NA
    ## 2263   5  NA  NA   1 NA NA   NA
    ## 2264   7  26  NA  NA NA NA   NA
    ## 2265   2  NA  NA   0 NA NA   NA
    ## 2266   0  NA  NA   0 NA NA   NA
    ## 2267   1  NA  NA   0 NA NA   NA
    ## 2268   1  NA  NA   1 NA NA   NA
    ## 2269  61  26  NA  NA NA NA   NA
    ## 2270   0  NA  NA  NA NA NA   NA
    ## 2271   1  NA  NA   0 NA NA   NA
    ## 2272   4  NA  NA  NA NA NA   NA
    ## 2273   2  NA  NA  NA NA NA   NA
    ## 2274   0  NA  NA  NA NA NA   NA
    ## 2275   2  NA  NA  NA NA NA   NA
    ## 2276   0  NA  NA   0 NA NA   NA
    ## 2277  10  NA  NA   1 NA NA   NA
    ## 2278   0  NA  NA  NA NA NA   NA
    ## 2279   1  19  NA  NA NA NA   NA
    ## 2280   3  NA  NA  NA NA NA   NA
    ## 2281   6  NA  NA  NA NA NA   NA
    ## 2282   0   3  NA  NA NA NA   NA
    ## 2283   1  12  NA  NA NA NA   NA
    ## 2284   3  NA  NA  NA NA NA   NA
    ## 2285   2  66  NA  NA NA NA   NA
    ## 2286   7  NA  NA  NA NA NA   NA
    ## 2287   0   1  NA  NA NA NA   NA
    ## 2288   2  NA  NA  NA NA NA   NA
    ## 2289   6  NA  NA   0 NA NA   NA
    ## 2290  23  59  NA  NA NA NA   NA
    ## 2291  40  52  NA  NA NA NA   NA
    ## 2292   6  NA  NA   0 NA NA   NA
    ## 2293   0  NA  NA   1 NA NA   NA
    ## 2294  25  NA  NA  NA NA NA   NA
    ## 2295   0   2  NA  NA NA NA   NA
    ## 2296   7  45  NA  NA NA NA   NA
    ## 2297   3  NA  NA  NA NA NA   NA
    ## 2298   3  NA  NA   0 NA NA   NA
    ## 2299   5  NA  NA  NA NA NA   NA
    ## 2300   4  NA  NA   0 NA NA   NA
    ## 2301   4  NA  NA   1 NA NA   NA
    ## 2302   3  NA  NA   0 NA NA   NA
    ## 2303  10  NA  NA   2 NA NA   NA
    ## 2304   5  NA  NA   0 NA NA   NA
    ## 2305   3  NA  NA  NA NA NA   NA
    ## 2306   0  NA  NA  NA NA NA   NA
    ## 2307   0  12  NA  NA NA NA   NA
    ## 2308   0   4  NA  NA NA NA   NA
    ## 2309   1  NA  NA  NA NA NA   NA
    ## 2310   0  NA  NA   0 NA NA   NA
    ## 2311   3  24  NA  NA NA NA   NA
    ## 2312  44  28  NA  NA NA NA   NA
    ## 2313  10  NA  NA  NA NA NA   NA
    ## 2314   7  NA  NA  NA NA NA   NA
    ## 2315   7  NA  NA   2 NA NA   NA
    ## 2316   2  NA  NA   0 NA NA   NA
    ## 2317  12  NA  NA  NA NA NA   NA
    ## 2318   4   9  NA  NA NA NA   NA
    ## 2319   1  NA  NA  NA NA NA   NA
    ## 2320  17  80  NA  NA NA NA   NA
    ## 2321  28  50  NA  NA NA NA   NA
    ## 2322   7  NA  NA   8 NA NA   NA
    ## 2323  12  NA  NA  NA NA NA   NA
    ## 2324  12  NA  NA   2 NA NA   NA
    ## 2325   2  NA  NA  NA NA NA   NA
    ## 2326   9  NA  NA   1 NA NA   NA
    ## 2327   9  19  NA  NA NA NA   NA
    ## 2328   0  NA  NA   0 NA NA   NA
    ## 2329   0  NA  NA  NA NA NA   NA
    ## 2330  28  52  NA  NA NA NA   NA
    ## 2331  15  NA  NA  NA NA NA   NA
    ## 2332   0  NA  NA  NA NA NA   NA
    ## 2333   2  NA  NA   0 NA NA   NA
    ## 2334   1  NA  NA   0 NA NA   NA
    ## 2335   1  NA  NA  NA NA NA   NA
    ## 2336  37  NA  NA  10 NA NA   NA
    ## 2337   5  NA  NA   0 NA NA   NA
    ## 2338   0   1  NA  NA NA NA   NA
    ## 2339  16  18  NA  NA NA NA   NA
    ## 2340  12  NA  NA  NA NA NA   NA
    ## 2341   2  NA  NA  NA NA NA   NA
    ## 2342   0  NA  NA  NA NA NA   NA
    ## 2343   0   2  NA  NA NA NA   NA
    ## 2344   2  10  NA  NA NA NA   NA
    ## 2345  18  NA  NA   1 NA NA   NA
    ## 2346  16  NA  NA   3 NA NA   NA
    ## 2347   6  NA  NA  NA NA NA   NA
    ## 2348   0  NA  NA  NA NA NA   NA
    ## 2349  46  24  NA  NA NA NA   NA
    ## 2350  15  NA  NA   0 NA NA   NA
    ## 2351  16  NA  NA   1 NA NA   NA
    ## 2352   1  NA  NA  NA NA NA   NA
    ## 2353   0  NA  NA   0 NA NA   NA
    ## 2354   6  NA  NA   1 NA NA   NA
    ## 2355  21  NA  NA  NA NA NA   NA
    ## 2356   3  NA  NA   1 NA NA   NA
    ## 2357   9  NA  NA   1 NA NA   NA
    ## 2358   1  NA  NA   1 NA NA   NA
    ## 2359   0  13  NA  NA NA NA   NA
    ## 2360   0  NA  NA   0 NA NA   NA
    ## 2361   0  NA  NA  NA NA NA   NA
    ## 2362   0   2  NA  NA NA NA   NA
    ## 2363  10  NA  NA   1 NA NA   NA
    ## 2364   5  NA  NA   2 NA NA   NA
    ## 2365   3  NA  NA   1 NA NA   NA
    ## 2366   2  NA  NA  NA NA NA   NA
    ## 2367   0  NA  NA  NA NA NA   NA
    ## 2368   0  NA  NA  NA NA NA   NA
    ## 2369   2  NA  NA   0 NA NA   NA
    ## 2370  11  NA  NA  NA NA NA   NA
    ## 2371   9  NA  NA   1 NA NA   NA
    ## 2372   2  NA  NA   2 NA NA   NA
    ## 2373   4  NA  NA  NA NA NA   NA
    ## 2374  15  NA  NA   8 NA NA   NA
    ## 2375   9  NA  NA   3 NA NA   NA
    ## 2376  18  NA  NA   6 NA NA   NA
    ## 2377   8  NA  NA   3 NA NA   NA
    ## 2378   0  NA  NA   0 NA NA   NA
    ## 2379   3  NA  NA   1 NA NA   NA
    ## 2380   0  NA  NA  NA NA NA   NA
    ## 2381   1  NA  NA  NA NA NA   NA
    ## 2382   0  NA  NA  NA NA NA   NA
    ## 2383   0   6  NA  NA NA NA   NA
    ## 2384   5  NA  NA  NA NA NA   NA
    ## 2385   0  NA  NA  NA NA NA   NA
    ## 2386   3  NA  NA  NA NA NA   NA
    ## 2387   0  NA  NA  NA NA NA   NA
    ## 2388   0  NA  NA   0 NA NA   NA
    ## 2389  16  NA  NA   4 NA NA   NA
    ## 2390   3  NA  NA  NA NA NA   NA
    ## 2391   5  71  NA  NA NA NA   NA
    ## 2392   0  NA  NA   0 NA NA   NA
    ## 2393   8  NA  NA  NA NA NA   NA
    ## 2394   7  11  NA  NA NA NA   NA
    ## 2395   0   1  NA  NA NA NA   NA
    ## 2396   4  NA  NA  NA NA NA   NA
    ## 2397   1  NA  NA  NA NA NA   NA
    ## 2398   9  NA  NA   0 NA NA   NA
    ## 2399   5  NA  NA  NA NA NA   NA
    ## 2400   4   5  NA  NA NA NA   NA
    ## 2401   0   2  NA  NA NA NA   NA
    ## 2402   1  NA  NA   0 NA NA   NA
    ## 2403  36  NA  NA   8 NA NA   NA
    ## 2404   0  NA  NA  NA NA NA   NA
    ## 2405   0  NA  NA  NA NA NA   NA
    ## 2406   0   4  NA  NA NA NA   NA
    ## 2407  25  NA  NA  11 NA NA   NA
    ## 2408  40  67  NA  NA NA NA   NA
    ## 2409  19  47  NA  NA NA NA   NA
    ## 2410  26  NA  NA   7 NA NA   NA
    ## 2411   7  NA  NA   1 NA NA   NA
    ## 2412   5  NA  NA   0 NA NA   NA
    ## 2413   8  NA  NA   3 NA NA   NA
    ## 2414  15  NA  NA   5 NA NA   NA
    ## 2415   6  NA  NA   1 NA NA   NA
    ## 2416  17  NA  NA   1 NA NA   NA
    ## 2417   7  NA  NA   0 NA NA   NA
    ## 2418   0  NA  NA  NA NA NA   NA
    ## 2419   5  NA  NA  NA NA NA   NA
    ## 2420   0  NA  NA  NA NA NA   NA
    ## 2421   6  NA  NA  NA NA NA   NA
    ## 2422  12  NA  NA   2 NA NA   NA
    ## 2423   0  NA  NA   0 NA NA   NA
    ## 2424  28  43  NA  NA NA NA   NA
    ## 2425   0  NA  NA  NA NA NA   NA
    ## 2426   4  NA  NA  NA NA NA   NA
    ## 2427   1  NA  NA  NA NA NA   NA
    ## 2428   1  11  NA  NA NA NA   NA
    ## 2429   0  NA  NA  NA NA NA   NA
    ## 2430   0  NA  NA  NA NA NA   NA
    ## 2431   2  NA  NA   0 NA NA   NA
    ## 2432   1  12  NA  NA NA NA   NA
    ## 2433   0  NA  NA  NA NA NA   NA
    ## 2434   0  NA  NA  NA NA NA   NA
    ## 2435   0  NA  NA  NA NA NA   NA
    ## 2436   4  NA  NA   0 NA NA   NA
    ## 2437   5  NA  NA   1 NA NA   NA
    ## 2438   5  NA  NA  NA NA NA   NA
    ## 2439   1  NA  NA  NA NA NA   NA
    ## 2440   0  NA  NA  NA NA NA   NA
    ## 2441   4  NA  NA  NA NA NA   NA
    ## 2442   1  NA  NA   0 NA NA   NA
    ## 2443   8  62  NA  NA NA NA   NA
    ## 2444   9  NA  NA  NA NA NA   NA
    ## 2445   2  NA  NA  NA NA NA   NA
    ## 2446   1  NA  NA  NA NA NA   NA
    ## 2447   9  NA  NA  NA NA NA   NA
    ## 2448   0  NA  NA  NA NA NA   NA
    ## 2449   0  NA  NA   0 NA NA   NA
    ## 2450  22  NA  NA   6 NA NA   NA
    ## 2451  27  NA  NA   6 NA NA   NA
    ## 2452   8  NA  NA  NA NA NA   NA
    ## 2453   0  NA  NA  NA NA NA   NA
    ## 2454   3  NA  NA   0 NA NA   NA
    ## 2455   2  NA  NA   0 NA NA   NA
    ## 2456   6  89  NA  NA NA NA   NA
    ## 2457   3  NA  NA   5 NA NA   NA
    ## 2458   6  NA  NA   1 NA NA   NA
    ## 2459   0  NA  NA  NA NA NA   NA
    ## 2460   1  NA  NA  NA NA NA   NA
    ## 2461   0  NA  NA  NA NA NA   NA
    ## 2462   1  10  NA  NA NA NA   NA
    ## 2463   0   3  NA  NA NA NA   NA
    ## 2464  13  NA  NA   2 NA NA   NA
    ## 2465   1  NA  NA   0 NA NA   NA
    ## 2466   1  NA  NA   1 NA NA   NA
    ## 2467  26  NA  NA   1 NA NA   NA
    ## 2468   8  NA  NA   0 NA NA   NA
    ## 2469   2  NA  NA   0 NA NA   NA
    ## 2470   8  56  NA  NA NA NA   NA
    ## 2471   0  NA  NA   0 NA NA   NA
    ## 2472  19  NA  NA  NA NA NA   NA
    ## 2473   0  NA  NA  NA NA NA   NA
    ## 2474   0   5  NA  NA NA NA   NA
    ## 2475   1  NA  NA   0 NA NA   NA
    ## 2476   1  NA  NA  NA NA NA   NA
    ## 2477   8  NA  NA   1 NA NA   NA
    ## 2478   0   8  NA  NA NA NA   NA
    ## 2479   0  NA  NA   0 NA NA   NA
    ## 2480   0  NA  NA  NA NA NA   NA
    ## 2481   5  NA  NA   3 NA NA   NA
    ## 2482  30  87  NA  NA NA NA   NA
    ## 2483   7  NA  NA   4 NA NA   NA
    ## 2484   0  NA  NA  NA NA NA   NA
    ## 2485   0  NA  NA  NA NA NA   NA
    ## 2486   7  NA  NA   0 NA NA   NA
    ## 2487   0   3  NA  NA NA NA   NA
    ## 2488   9  NA  NA   3 NA NA   NA
    ## 2489   9  NA  NA   4 NA NA   NA
    ## 2490   0  NA  NA   0 NA NA   NA
    ## 2491   7  11  NA  NA NA NA   NA
    ## 2492  18  67  NA  NA NA NA   NA
    ## 2493  33  NA  NA   1 NA NA   NA
    ## 2494   8  NA  NA   0 NA NA   NA
    ## 2495   0  NA  NA  NA NA NA   NA
    ## 2496   0  NA  NA  NA NA NA   NA
    ## 2497   4  49  NA  NA NA NA   NA
    ## 2498   1  NA  NA  NA NA NA   NA
    ## 2499   0  NA  NA   0 NA NA   NA
    ## 2500  22  NA  NA  NA NA NA   NA
    ## 2501   1  NA  NA  NA NA NA   NA
    ## 2502   1   1  NA  NA NA NA   NA
    ## 2503   4  NA  NA  NA NA NA   NA
    ## 2504   3  NA  NA  NA NA NA   NA
    ## 2505   0  NA  NA   0 NA NA   NA
    ## 2506   1  23  NA  NA NA NA   NA
    ## 2507   1  NA  NA   2 NA NA   NA
    ## 2508   1   8  NA  NA NA NA   NA
    ## 2509   0  NA  NA  NA NA NA   NA
    ## 2510  13  33  NA  NA NA NA   NA
    ## 2511   0  NA  NA  NA NA NA   NA
    ## 2512  12  NA  NA   7 NA NA   NA
    ## 2513  11  35  NA  NA NA NA   NA
    ## 2514   6  NA  NA   1 NA NA   NA
    ## 2515   0  NA  NA   0 NA NA   NA
    ## 2516  74  NA  NA   9 NA NA   NA
    ## 2517  22  NA  NA   3 NA NA   NA
    ## 2518   0  NA  NA  NA NA NA   NA
    ## 2519   2  NA  NA  NA NA NA   NA
    ## 2520   0  NA  NA  NA NA NA   NA
    ## 2521   3  NA  NA  NA NA NA   NA
    ## 2522   7  NA  NA  NA NA NA   NA
    ## 2523   0  NA  NA  NA NA NA   NA
    ## 2524   0  NA  NA  NA NA NA   NA
    ## 2525   9  NA  NA   3 NA NA   NA
    ## 2526   2  NA  NA  NA NA NA   NA
    ## 2527  12  NA  NA  NA NA NA   NA
    ## 2528  10  NA  NA   1 NA NA   NA
    ## 2529   0  NA  NA  NA NA NA   NA
    ## 2530   5  NA  NA  NA NA NA   NA
    ## 2531   7  NA  NA   0 NA NA   NA
    ## 2532   0  NA  NA  NA NA NA   NA
    ## 2533   5  NA  NA   1 NA NA   NA
    ## 2534  12  NA  NA   2 NA NA   NA
    ## 2535  35  17  NA  NA NA NA   NA
    ## 2536   5  NA  NA   1 NA NA   NA
    ## 2537   1   2  NA  NA NA NA   NA
    ## 2538   0  NA  NA   0 NA NA   NA
    ## 2539   0  NA  NA  NA NA NA   NA
    ## 2540   1  NA  NA  NA NA NA   NA
    ## 2541   7  NA  NA  NA NA NA   NA
    ## 2542   7  NA  NA   2 NA NA   NA
    ## 2543   6  NA  NA   0 NA NA   NA
    ## 2544   0  NA  NA   0 NA NA   NA
    ## 2545  25  47  NA  NA NA NA   NA
    ## 2546  12  NA  NA  NA NA NA   NA
    ## 2547  18  80  NA  NA NA NA   NA
    ## 2548   5  NA  NA   1 NA NA   NA
    ## 2549   0  NA  NA   0 NA NA   NA
    ## 2550   0  NA  NA  NA NA NA   NA
    ## 2551  10   7  NA  NA NA NA   NA
    ## 2552  10  NA  NA   1 NA NA   NA
    ## 2553   0  NA  NA  NA NA NA   NA
    ## 2554   0  NA  NA  NA NA NA   NA
    ## 2555   3  NA  NA  NA NA NA   NA
    ## 2556   7  NA  NA   4 NA NA   NA
    ## 2557  13  NA  NA  NA NA NA   NA
    ## 2558   5  NA  NA   0 NA NA   NA
    ## 2559   3   4  NA  NA NA NA   NA
    ## 2560  13  NA  NA   3 NA NA   NA
    ## 2561   0  NA  NA  NA NA NA   NA
    ## 2562  29  30  NA  NA NA NA   NA
    ## 2563   0   0  NA  NA NA NA   NA
    ## 2564  19  NA  NA   2 NA NA   NA
    ## 2565   0  NA  NA   1 NA NA   NA
    ## 2566   9  NA  NA  NA NA NA   NA
    ## 2567   0  NA  NA   1 NA NA   NA
    ## 2568  26  42  NA  NA NA NA   NA
    ## 2569  25  43  NA  NA NA NA   NA
    ## 2570   5  NA  NA   5 NA NA   NA
    ## 2571   0  NA  NA   0 NA NA   NA
    ## 2572   0  NA  NA  NA NA NA   NA
    ## 2573   4  NA  NA   1 NA NA   NA
    ## 2574   1  NA  NA  NA NA NA   NA
    ## 2575   5  NA  NA  14 NA NA   NA
    ## 2576   1  NA  NA   2 NA NA   NA
    ## 2577   1  NA  NA   0 NA NA   NA
    ## 2578   6   9  NA  NA NA NA   NA
    ## 2579  23  NA  NA   0 NA NA   NA
    ## 2580   0  NA  NA  NA NA NA   NA
    ## 2581  16  17  NA  NA NA NA   NA
    ## 2582  22  41  NA  NA NA NA   NA
    ## 2583  35  NA  NA   3 NA NA   NA
    ## 2584   2  NA  NA  NA NA NA   NA
    ## 2585   3  19  NA  NA NA NA   NA
    ## 2586   0  NA  NA   0 NA NA   NA
    ## 2587   3  NA  NA   0 NA NA   NA
    ## 2588   0  NA  NA  NA NA NA   NA
    ## 2589  37  NA  NA  NA NA NA   NA
    ## 2590   0  NA  NA  NA NA NA   NA
    ## 2591  21  NA  NA   6 NA NA   NA
    ## 2592  10  NA  NA  NA NA NA   NA
    ## 2593  23  14  NA  NA NA NA   NA
    ## 2594   1  NA  NA   1 NA NA   NA
    ## 2595   1  NA  NA   1 NA NA   NA
    ## 2596   0  NA  NA  NA NA NA   NA
    ## 2597   2  NA  NA  NA NA NA   NA
    ## 2598   1  NA  NA  NA NA NA   NA
    ## 2599   1  NA  NA  NA NA NA   NA
    ## 2600   2  NA  NA  NA NA NA   NA
    ## 2601   1   2  NA  NA NA NA   NA
    ## 2602   1  NA  NA  NA NA NA   NA
    ## 2603   0  NA  NA  NA NA NA   NA
    ## 2604  11  NA  NA  NA NA NA   NA
    ## 2605   2  NA  NA  NA NA NA   NA
    ## 2606   0  NA  NA  NA NA NA   NA
    ## 2607   1  NA  NA   1 NA NA   NA
    ## 2608   8  NA  NA  NA NA NA   NA
    ## 2609   0  NA  NA  NA NA NA   NA
    ## 2610   3  NA  NA  NA NA NA   NA
    ## 2611   2  NA  NA  NA NA NA   NA
    ## 2612   9  62  NA  NA NA NA   NA
    ## 2613  20  NA  NA  NA NA NA   NA
    ## 2614   1  NA  NA  NA NA NA   NA
    ## 2615   3  33  NA  NA NA NA   NA
    ## 2616   4  NA  NA  NA NA NA   NA
    ## 2617   0  NA  NA  NA NA NA   NA
    ## 2618  30  NA  NA  NA NA NA   NA
    ## 2619   3  NA  NA  NA NA NA   NA
    ## 2620  15  NA  NA  NA NA NA   NA
    ## 2621   0  NA  NA  NA NA NA   NA
    ## 2622   4  NA  NA   0 NA NA   NA
    ## 2623   4  21  NA  NA NA NA   NA
    ## 2624   5  NA  NA  NA NA NA   NA
    ## 2625   0  NA  NA  NA NA NA   NA
    ## 2626   1  NA  NA  NA NA NA   NA
    ## 2627   0  NA  NA   1 NA NA   NA
    ## 2628   0   0  NA  NA NA NA   NA
    ## 2629   0  NA  NA  NA NA NA   NA
    ## 2630   0  NA  NA  NA NA NA   NA
    ## 2631   0  NA  NA  NA NA NA   NA
    ## 2632   4  NA  NA  NA NA NA   NA
    ## 2633   0  NA  NA  NA NA NA   NA
    ## 2634   0   2  NA  NA NA NA   NA
    ## 2635   1  NA  NA   0 NA NA   NA
    ## 2636   2  NA  NA  NA NA NA   NA
    ## 2637   0  NA  NA   0 NA NA   NA
    ## 2638   1  NA  NA  NA NA NA   NA
    ## 2639   2  45  NA  NA NA NA   NA
    ## 2640   0  NA  NA   0 NA NA   NA
    ## 2641   0  NA  NA   0 NA NA   NA
    ## 2642  20  NA  NA  12 NA NA   NA
    ## 2643   6  NA  NA   0 NA NA   NA
    ## 2644   7  NA  NA   0 NA NA   NA
    ## 2645   1  NA  NA  NA NA NA   NA
    ## 2646   8  NA  NA   8 NA NA   NA
    ## 2647   0  NA  NA  NA NA NA   NA
    ## 2648  35  25  NA  NA NA NA   NA
    ## 2649  28  NA  NA   6 NA NA   NA
    ## 2650   0  NA  NA   0 NA NA   NA
    ## 2651  26  NA  NA   4 NA NA   NA
    ## 2652   1  NA  NA  NA NA NA   NA
    ## 2653  19  NA  NA   1 NA NA   NA
    ## 2654  13  NA  NA   0 NA NA   NA
    ## 2655   4  NA  NA  NA NA NA   NA
    ## 2656   3  NA  NA  NA NA NA   NA
    ## 2657   0   5  NA  NA NA NA   NA
    ## 2658   0  NA  NA   0 NA NA   NA
    ## 2659  13  NA  NA  NA NA NA   NA
    ## 2660   0  NA  NA  NA NA NA   NA
    ## 2661   9  NA  NA   1 NA NA   NA
    ## 2662   5  NA  NA   0 NA NA   NA
    ## 2663   4  NA  NA  NA NA NA   NA
    ## 2664   0  NA  NA  NA NA NA   NA
    ## 2665   1  NA  NA  NA NA NA   NA
    ## 2666   1  NA  NA   0 NA NA   NA
    ## 2667   0  NA  NA  NA NA NA   NA
    ## 2668   4  36  NA  NA NA NA   NA
    ## 2669   2   4  NA  NA NA NA   NA
    ## 2670  29  22  NA  NA NA NA   NA
    ## 2671   0  NA  NA   0 NA NA   NA
    ## 2672   0  NA  NA   0 NA NA   NA
    ## 2673  33  NA  NA  15 NA NA   NA
    ## 2674   9  NA  NA  NA NA NA   NA
    ## 2675  11  17  NA  NA NA NA   NA
    ## 2676  10  NA  NA  NA NA NA   NA
    ## 2677   4  NA  NA  NA NA NA   NA
    ## 2678  15  NA  NA  NA NA NA   NA
    ## 2679  18  NA  NA  NA NA NA   NA
    ## 2680   7  NA  NA  NA NA NA   NA
    ## 2681   2  NA  NA   1 NA NA   NA
    ## 2682   6  NA  NA   3 NA NA   NA
    ## 2683   0  NA  NA  NA NA NA   NA
    ## 2684   0  NA  NA  NA NA NA   NA
    ## 2685   0  NA  NA  NA NA NA   NA
    ## 2686   8  NA  NA   0 NA NA   NA
    ## 2687   2  NA  NA   0 NA NA   NA
    ## 2688   1  NA  NA  NA NA NA   NA
    ## 2689   4  NA  NA   1 NA NA   NA
    ## 2690   3  NA  NA  NA NA NA   NA
    ## 2691   6  NA  NA  NA NA NA   NA
    ## 2692   3  NA  NA   1 NA NA   NA
    ## 2693   2  NA  NA   0 NA NA   NA
    ## 2694   4  NA  NA   2 NA NA   NA
    ## 2695  19  NA  NA   3 NA NA   NA
    ## 2696   2  NA  NA   0 NA NA   NA
    ## 2697   3  NA  NA  NA NA NA   NA
    ## 2698   1   2  NA  NA NA NA   NA
    ## 2699   9  NA  NA  NA NA NA   NA
    ## 2700   3  21  NA  NA NA NA   NA
    ## 2701   5  NA  NA  NA NA NA   NA
    ## 2702   0  NA  NA  NA NA NA   NA
    ## 2703   8  NA  NA   6 NA NA   NA
    ## 2704   9  NA  NA   3 NA NA   NA
    ## 2705   0   0  NA  NA NA NA   NA
    ## 2706   0  NA  NA   0 NA NA   NA
    ## 2707  28  47  NA  NA NA NA   NA
    ## 2708   0  NA  NA  NA NA NA   NA
    ## 2709  17  NA  NA   1 NA NA   NA
    ## 2710   5  NA  NA   1 NA NA   NA
    ## 2711   2  NA  NA  NA NA NA   NA
    ## 2712   0  NA  NA   1 NA NA   NA
    ## 2713   0   2  NA  NA NA NA   NA
    ## 2714   9  NA  NA   0 NA NA   NA
    ## 2715  10  NA  NA   4 NA NA   NA
    ## 2716  16  49  NA  NA NA NA   NA
    ## 2717   2  NA  NA  NA NA NA   NA
    ## 2718   1  NA  NA  NA NA NA   NA
    ## 2719   2  NA  NA   0 NA NA   NA
    ## 2720   1  NA  NA   0 NA NA   NA
    ## 2721   3  NA  NA  NA NA NA   NA
    ## 2722   4  NA  NA  NA NA NA   NA
    ## 2723   0  NA  NA  NA NA NA   NA
    ## 2724  13  NA  NA   1 NA NA   NA
    ## 2725  32  13  NA  NA NA NA   NA
    ## 2726   1   8  NA  NA NA NA   NA
    ## 2727   8  NA  NA  NA NA NA   NA
    ## 2728   0  NA  NA  NA NA NA   NA
    ## 2729   0  NA  NA  NA NA NA   NA
    ## 2730  10  NA  NA   1 NA NA   NA
    ## 2731   9  NA  NA   2 NA NA   NA
    ## 2732   1  NA  NA   0 NA NA   NA
    ## 2733  16  38  NA  NA NA NA   NA
    ## 2734  13  41  NA  NA NA NA   NA
    ## 2735   0  NA  NA  NA NA NA   NA
    ## 2736  42  56  NA  NA NA NA   NA
    ## 2737   0  NA  NA   0 NA NA   NA
    ## 2738   0  NA  NA   0 NA NA   NA
    ## 2739   0  NA  NA  NA NA NA   NA
    ## 2740   5  NA  NA   0 NA NA   NA
    ## 2741  12  NA  NA  NA NA NA   NA
    ## 2742  25 104  NA  NA NA NA   NA
    ## 2743   4  NA  NA   3 NA NA   NA
    ## 2744   3  18  NA  NA NA NA   NA
    ## 2745  39  75  NA  NA NA NA   NA
    ## 2746   1  NA  NA   0 NA NA   NA
    ## 2747   0  NA  NA   0 NA NA   NA
    ## 2748   3  NA  NA  NA NA NA   NA
    ## 2749   0  NA  NA  NA NA NA   NA
    ## 2750   1  NA  NA   1 NA NA   NA
    ## 2751   0  NA  NA  NA NA NA   NA
    ## 2752  34  NA  NA  10 NA NA   NA
    ## 2753   1  14  NA  NA NA NA   NA
    ## 2754   1   2  NA  NA NA NA   NA
    ## 2755  32  25  NA  NA NA NA   NA
    ## 2756   0   1  NA  NA NA NA   NA
    ## 2757  34  13  NA  NA NA NA   NA
    ## 2758   9  28  NA  NA NA NA   NA
    ## 2759   2  NA  NA   1 NA NA   NA
    ## 2760   3  NA  NA   0 NA NA   NA
    ## 2761   6  22  NA  NA NA NA   NA
    ## 2762  25  NA  NA   2 NA NA   NA
    ## 2763  19  60  NA  NA NA NA   NA
    ## 2764  35  82  NA  NA NA NA   NA
    ## 2765   1  NA  NA   1 NA NA   NA
    ## 2766   1  NA  NA   0 NA NA   NA
    ## 2767   0  NA  NA   1 NA NA   NA
    ## 2768  47  37  NA  NA NA NA   NA
    ## 2769  13  38  NA  NA NA NA   NA
    ## 2770  25  NA  NA   6 NA NA   NA
    ## 2771   1   1  NA  NA NA NA   NA
    ## 2772  12  23  NA  NA NA NA   NA
    ## 2773   0  NA  NA   0 NA NA   NA
    ## 2774   1  NA  NA   0 NA NA   NA
    ## 2775  34  10  NA  NA NA NA   NA
    ## 2776   0  NA  NA   0 NA NA   NA
    ## 2777  25  NA  NA   0 NA NA   NA
    ## 2778  34  NA  NA   7 NA NA   NA
    ## 2779   0   2  NA  NA NA NA   NA
    ## 2780   3  26  NA  NA NA NA   NA
    ## 2781   8  18  NA  NA NA NA   NA
    ## 2782   3   8  NA  NA NA NA   NA
    ## 2783  16  NA  NA   6 NA NA   NA
    ## 2784  16  48  NA  NA NA NA   NA
    ## 2785  11  NA  NA   2 NA NA   NA
    ## 2786   9  NA  NA   3 NA NA   NA
    ## 2787  29  29  NA  NA NA NA   NA
    ## 2788   7  NA  NA   5 NA NA   NA
    ## 2789   2   8  NA  NA NA NA   NA
    ## 2790  20  NA  NA   0 NA NA   NA
    ## 2791   1  11  NA  NA NA NA   NA
    ## 2792  21  NA  NA   3 NA NA   NA
    ## 2793  12  22  NA  NA NA NA   NA
    ## 2794   8  NA  NA   3 NA NA   NA
    ## 2795   3  44  NA  NA NA NA   NA
    ## 2796   2  30  NA  NA NA NA   NA
    ## 2797   0  NA  NA   0 NA NA   NA
    ## 2798  15  NA  NA   7 NA NA   NA
    ## 2799  25  NA  NA   3 NA NA   NA
    ## 2800   0  11  NA  NA NA NA   NA
    ## 2801   0   1  NA  NA NA NA   NA
    ## 2802  14  NA  NA   4 NA NA   NA
    ## 2803   0   1  NA  NA NA NA   NA
    ## 2804   0  NA  NA   0 NA NA   NA
    ## 2805  51   8  NA  NA NA NA   NA
    ## 2806   1  NA  NA   1 NA NA   NA
    ## 2807   5  28  NA  NA NA NA   NA
    ## 2808   6   1  NA  NA NA NA   NA
    ## 2809   0   1  NA  NA NA NA   NA
    ## 2810  17  NA  NA   3 NA NA   NA
    ## 2811   7  NA  NA   7 NA NA   NA
    ## 2812   1   1  NA  NA NA NA   NA
    ## 2813   3   8  NA  NA NA NA   NA
    ## 2814  13  45  NA  NA NA NA   NA
    ## 2815   0  NA  NA   1 NA NA   NA
    ## 2816   8  NA  NA   1 NA NA   NA
    ## 2817   3  NA  NA   3 NA NA   NA
    ## 2818  21  32  NA  NA NA NA   NA
    ## 2819   1  NA  NA   0 NA NA   NA
    ## 2820   9  NA  NA   0 NA NA   NA
    ## 2821   1  24  NA  NA NA NA   NA
    ## 2822  12  20  NA  NA NA NA   NA
    ## 2823   0  25  NA  NA NA NA   NA
    ## 2824   2  10  NA  NA NA NA   NA
    ## 2825  46  42  NA  NA NA NA   NA
    ## 2826   1  11  NA  NA NA NA   NA
    ## 2827   2  14  NA  NA NA NA   NA
    ## 2828   9  20  NA  NA NA NA   NA
    ## 2829  12  53  NA  NA NA NA   NA
    ## 2830   1  NA  NA   1 NA NA   NA
    ## 2831   1   4  NA  NA NA NA   NA
    ## 2832   2   1  NA  NA NA NA   NA
    ## 2833  10  29  NA  NA NA NA   NA
    ## 2834   8  10  NA  NA NA NA   NA
    ## 2835  11  24  NA  NA NA NA   NA
    ## 2836   2   5  NA  NA NA NA   NA
    ## 2837   0  NA  NA   0 NA NA   NA
    ## 2838  41  24  NA  NA NA NA   NA
    ## 2839  17  NA  NA   8 NA NA   NA
    ## 2840   2   4  NA  NA NA NA   NA
    ## 2841   0  NA  NA   0 NA NA   NA
    ## 2842   0  NA  NA   0 NA NA   NA
    ## 2843   4  28  NA  NA NA NA   NA
    ## 2844   7  NA  NA   4 NA NA   NA
    ## 2845  13  17  NA  NA NA NA   NA
    ## 2846  28  34  NA  NA NA NA   NA
    ## 2847  10  25  NA  NA NA NA   NA
    ## 2848  38  NA  NA   3 NA NA   NA
    ## 2849  23  18  NA  NA NA NA   NA
    ## 2850  13  NA  NA   7 NA NA   NA
    ## 2851  13  NA  NA   1 NA NA   NA
    ## 2852   0   0  NA  NA NA NA   NA
    ## 2853   2  52  NA  NA NA NA   NA
    ## 2854  30  37  NA  NA NA NA   NA
    ## 2855   0   1  NA  NA NA NA   NA
    ## 2856   1   0  NA  NA NA NA   NA
    ## 2857  13  19  NA  NA NA NA   NA
    ## 2858   0  NA  NA   0 NA NA   NA
    ## 2859  17  NA  NA   1 NA NA   NA
    ## 2860  11  NA  NA   0 NA NA   NA
    ## 2861   0  NA  NA   0 NA NA   NA
    ## 2862   1  27  NA  NA NA NA   NA
    ## 2863   0  NA  NA   0 NA NA   NA
    ## 2864   4  13  NA  NA NA NA   NA
    ## 2865  12  NA  NA   0 NA NA   NA
    ## 2866   0   2  NA  NA NA NA   NA
    ## 2867   0   1  NA  NA NA NA   NA
    ## 2868   2  NA  NA   1 NA NA   NA
    ## 2869  24  47  NA  NA NA NA   NA
    ## 2870   4  27  NA  NA NA NA   NA
    ## 2871  15  32  NA  NA NA NA   NA
    ## 2872  23  33  NA  NA NA NA   NA
    ## 2873  29  10  NA  NA NA NA   NA
    ## 2874  29  NA  NA  15 NA NA   NA
    ## 2875   0   1  NA  NA NA NA   NA
    ## 2876  68  25  NA  NA NA NA   NA
    ## 2877   8  NA  NA   2 NA NA   NA
    ## 2878   5  29  NA  NA NA NA   NA
    ## 2879   2  28  NA  NA NA NA   NA
    ## 2880   3  22  NA  NA NA NA   NA
    ## 2881   0   2  NA  NA NA NA   NA
    ## 2882   1  12  NA  NA NA NA   NA
    ## 2883  12  NA  NA   1 NA NA   NA
    ## 2884  47  18  NA  NA NA NA   NA
    ## 2885   9  NA  NA   0 NA NA   NA
    ## 2886   0  11  NA  NA NA NA   NA
    ## 2887   5  NA  NA   3 NA NA   NA
    ## 2888   0  12  NA  NA NA NA   NA
    ## 2889   5  NA  NA   1 NA NA   NA
    ## 2890  12  NA  NA   1 NA NA   NA
    ## 2891   1   2  NA  NA NA NA   NA
    ## 2892   1  NA  NA   0 NA NA   NA
    ## 2893   0   4  NA  NA NA NA   NA
    ## 2894   4   5  NA  NA NA NA   NA
    ## 2895   0  NA  NA   0 NA NA   NA
    ## 2896   0   2  NA  NA NA NA   NA
    ## 2897  19  18  NA  NA NA NA   NA
    ## 2898   0  NA  NA   0 NA NA   NA
    ## 2899   8  NA  NA   0 NA NA   NA
    ## 2900   1  20  NA  NA NA NA   NA
    ## 2901  49  NA  NA   4 NA NA   NA
    ## 2902  10  NA  NA   7 NA NA   NA
    ## 2903   1  NA  NA   1 NA NA   NA
    ## 2904  14  29  NA  NA NA NA   NA
    ## 2905   2  NA  NA   0 NA NA   NA
    ## 2906   0  15  NA  NA NA NA   NA
    ## 2907   0  NA  NA   0 NA NA   NA
    ## 2908  21  NA  NA   9 NA NA   NA
    ## 2909  13  22  NA  NA NA NA   NA
    ## 2910   8  NA  NA   0 NA NA   NA
    ## 2911   1   5  NA  NA NA NA   NA
    ## 2912  46  24  NA  NA NA NA   NA
    ## 2913   2  NA  NA   1 NA NA   NA
    ## 2914  12  NA  NA   4 NA NA   NA
    ## 2915   0  10  NA  NA NA NA   NA
    ## 2916  20  NA  NA   4 NA NA   NA
    ## 2917   0   2  NA  NA NA NA   NA
    ## 2918   1  17  NA  NA NA NA   NA
    ## 2919   9  NA  NA   1 NA NA   NA
    ## 2920  11  17  NA  NA NA NA   NA
    ## 2921   2  NA  NA   0 NA NA   NA
    ## 2922   1  NA  NA   0 NA NA   NA
    ## 2923   0   2  NA  NA NA NA   NA
    ## 2924   2  NA  NA   0 NA NA   NA
    ## 2925   0   2  NA  NA NA NA   NA
    ## 2926  15  NA  NA   2 NA NA   NA
    ## 2927  26  NA  NA   6 NA NA   NA
    ## 2928  18  NA  NA   5 NA NA   NA
    ## 2929   0  NA  NA   1 NA NA   NA
    ## 2930   9  10  NA  NA NA NA   NA
    ## 2931   6  39  NA  NA NA NA   NA
    ## 2932   3  NA  NA   0 NA NA   NA
    ## 2933  11  NA  NA   0 NA NA   NA
    ## 2934  10   3  NA  NA NA NA   NA
    ## 2935   0   3  NA  NA NA NA   NA
    ## 2936   2  NA  NA   1 NA NA   NA
    ## 2937  49  NA  NA   4 NA NA   NA
    ## 2938  31  NA  NA   6 NA NA   NA
    ## 2939  37  27  NA  NA NA NA   NA
    ## 2940  19  36  NA  NA NA NA   NA
    ## 2941   4  10  NA  NA NA NA   NA
    ## 2942  10  NA  NA   3 NA NA   NA
    ## 2943   1  11  NA  NA NA NA   NA
    ## 2944   1  NA  NA   0 NA NA   NA
    ## 2945  19  NA  NA   4 NA NA   NA
    ## 2946  10  NA  NA   0 NA NA   NA
    ## 2947   2  NA  NA   0 NA NA   NA
    ## 2948   0  NA  NA   0 NA NA   NA
    ## 2949   5  25  NA  NA NA NA   NA
    ## 2950  11  12  NA  NA NA NA   NA
    ## 2951   2   3  NA  NA NA NA   NA
    ## 2952  28  NA  NA   6 NA NA   NA
    ## 2953   1   0  NA  NA NA NA   NA
    ## 2954   1  18  NA  NA NA NA   NA
    ## 2955   0  NA  NA   0 NA NA   NA
    ## 2956   0   4  NA  NA NA NA   NA
    ## 2957   1  NA  NA   0 NA NA   NA
    ## 2958   5  23  NA  NA NA NA   NA
    ## 2959   0  NA  NA   0 NA NA   NA
    ## 2960   8  31  NA  NA NA NA   NA
    ## 2961  15  NA  NA   3 NA NA   NA
    ## 2962  19  NA  NA   7 NA NA   NA
    ## 2963   8  29  NA  NA NA NA   NA
    ## 2964   2   1  NA  NA NA NA   NA
    ## 2965   9  NA  NA   0 NA NA   NA
    ## 2966   2  NA  NA   0 NA NA   NA
    ## 2967   3  NA  NA   0 NA NA   NA
    ## 2968   0   1  NA  NA NA NA   NA
    ## 2969   4  NA  NA   0 NA NA   NA
    ## 2970  28  NA  NA   2 NA NA   NA
    ## 2971   7  NA  NA   1 NA NA   NA
    ## 2972   1   3  NA  NA NA NA   NA
    ## 2973   0  10  NA  NA NA NA   NA
    ## 2974   5  NA  NA   0 NA NA   NA
    ## 2975  64  78  NA  NA NA NA   NA
    ## 2976   5  10  NA  NA NA NA   NA
    ## 2977   8  NA  NA   3 NA NA   NA
    ## 2978   7  NA  NA   0 NA NA   NA
    ## 2979   1  NA  NA   0 NA NA   NA
    ## 2980  20  NA  NA   4 NA NA   NA
    ## 2981   3  18  NA  NA NA NA   NA
    ## 2982   2  NA  NA   1 NA NA   NA
    ## 2983  11  41  NA  NA NA NA   NA
    ## 2984  23  40  NA  NA NA NA   NA
    ## 2985   2   9  NA  NA NA NA   NA
    ## 2986   1  NA  NA   0 NA NA   NA
    ## 2987  61  NA  NA   3 NA NA   NA
    ## 2988  34  NA  NA   3 NA NA   NA
    ## 2989   3   8  NA  NA NA NA   NA
    ## 2990  20  NA  NA   5 NA NA   NA
    ## 2991   2  NA  NA   0 NA NA   NA
    ## 2992   1  NA  NA   0 NA NA   NA
    ## 2993   3  NA  NA   1 NA NA   NA
    ## 2994   0   0  NA  NA NA NA   NA
    ## 2995  13  NA  NA   4 NA NA   NA
    ## 2996  40  21  NA  NA NA NA   NA
    ## 2997   8  NA  NA   3 NA NA   NA
    ## 2998   3   7  NA  NA NA NA   NA
    ## 2999   0  NA  NA   0 NA NA   NA
    ## 3000   1  NA  NA   0 NA NA   NA
    ## 3001   5  NA  NA   1 NA NA   NA
    ## 3002  26  47  NA  NA NA NA   NA
    ## 3003   0   3  NA  NA NA NA   NA
    ## 3004   0   2  NA  NA NA NA   NA
    ## 3005  27  NA  NA  11 NA NA   NA
    ## 3006   0  13  NA  NA NA NA   NA
    ## 3007   2  NA  NA   0 NA NA   NA
    ## 3008   2  NA  NA   0 NA NA   NA
    ## 3009  27  NA  NA   7 NA NA   NA
    ## 3010   7  32  NA  NA NA NA   NA
    ## 3011   5  NA  NA   0 NA NA   NA
    ## 3012   1  NA  NA   2 NA NA   NA
    ## 3013   0  NA  NA   0 NA NA   NA
    ## 3014   1  NA  NA   0 NA NA   NA
    ## 3015  16  NA  NA   3 NA NA   NA
    ## 3016   3  15  NA  NA NA NA   NA
    ## 3017  14  25  NA  NA NA NA   NA
    ## 3018   9  38  NA  NA NA NA   NA
    ## 3019   1  NA  NA   1 NA NA   NA
    ## 3020  36  27  NA  NA NA NA   NA
    ## 3021  33  43  NA  NA NA NA   NA
    ## 3022   0  NA  NA   0 NA NA   NA
    ## 3023  13  NA  NA   1 NA NA   NA
    ## 3024  11  NA  NA   7 NA NA   NA
    ## 3025   2  NA  NA   0 NA NA   NA
    ## 3026   9  NA  NA   1 NA NA   NA
    ## 3027  10  14  NA  NA NA NA   NA
    ## 3028  20  22  NA  NA NA NA   NA
    ## 3029   8  NA  NA   2 NA NA   NA
    ## 3030   0   7  NA  NA NA NA   NA
    ## 3031   0  NA  NA   0 NA NA   NA
    ## 3032   0   2  NA  NA NA NA   NA
    ## 3033   3  NA  NA   0 NA NA   NA
    ## 3034  29  NA  NA   7 NA NA   NA
    ## 3035  25  NA  NA  10 NA NA   NA
    ## 3036   5   8  NA  NA NA NA   NA
    ## 3037  13  19  NA  NA NA NA   NA
    ## 3038   1   1  NA  NA NA NA   NA
    ## 3039   0  NA  NA   0 NA NA   NA
    ## 3040   4  16  NA  NA NA NA   NA
    ## 3041   5  NA  NA   2 NA NA   NA
    ## 3042  16  37  NA  NA NA NA   NA
    ## 3043   1  19  NA  NA NA NA   NA
    ## 3044   0   2  NA  NA NA NA   NA
    ## 3045  19  31  NA  NA NA NA   NA
    ## 3046   1  NA  NA   0 NA NA   NA
    ## 3047   3  NA  NA   2 NA NA   NA
    ## 3048   4  38  NA  NA NA NA   NA
    ## 3049   0  NA  NA   0 NA NA   NA
    ## 3050   0   0  NA  NA NA NA   NA
    ## 3051  10  NA  NA   0 NA NA   NA
    ## 3052   0  NA  NA   0 NA NA   NA
    ## 3053   0  NA  NA   0 NA NA   NA
    ## 3054  25  NA  NA   3 NA NA   NA
    ## 3055   6  NA  NA   1 NA NA   NA
    ## 3056  24  NA  NA   3 NA NA   NA
    ## 3057   0   9  NA  NA NA NA   NA
    ## 3058  39  10  NA  NA NA NA   NA
    ## 3059  38  NA  NA   6 NA NA   NA
    ## 3060   8  23  NA  NA NA NA   NA
    ## 3061   0   2  NA  NA NA NA   NA
    ## 3062   0   0  NA  NA NA NA   NA
    ## 3063  39  NA  NA   4 NA NA   NA
    ## 3064   0  NA  NA   0 NA NA   NA
    ## 3065  21  NA  NA   7 NA NA   NA
    ## 3066   9  NA  NA   0 NA NA   NA
    ## 3067   2  NA  NA   1 NA NA   NA
    ## 3068   6  NA  NA   0 NA NA   NA
    ## 3069  12  33  NA  NA NA NA   NA
    ## 3070   2   5  NA  NA NA NA   NA
    ## 3071   5  10  NA  NA NA NA   NA
    ## 3072  17  25  NA  NA NA NA   NA
    ## 3073  36  NA  NA   5 NA NA   NA
    ## 3074  12  33  NA  NA NA NA   NA
    ## 3075   0   4  NA  NA NA NA   NA
    ## 3076   1   3  NA  NA NA NA   NA
    ## 3077   0  NA  NA   0 NA NA   NA
    ## 3078   0  NA  NA   0 NA NA   NA
    ## 3079  10  NA  NA   0 NA NA   NA
    ## 3080  16  22  NA  NA NA NA   NA
    ## 3081  17  NA  NA   3 NA NA   NA
    ## 3082   5  NA  NA   0 NA NA   NA
    ## 3083   5  NA  NA   4 NA NA   NA
    ## 3084   1  12  NA  NA NA NA   NA
    ## 3085   3  NA  NA   0 NA NA   NA
    ## 3086   2  NA  NA   0 NA NA   NA
    ## 3087   0  NA  NA   0 NA NA   NA
    ## 3088  17  39  NA  NA NA NA   NA
    ## 3089   0   2  NA  NA NA NA   NA
    ## 3090  23  NA  NA   7 NA NA   NA
    ## 3091  14  39  NA  NA NA NA   NA
    ## 3092   1  NA  NA   0 NA NA   NA
    ## 3093  12  11  NA  NA NA NA   NA
    ## 3094   1  25  NA  NA NA NA   NA
    ## 3095   4  NA  NA   2 NA NA   NA
    ## 3096  16  NA  NA   1 NA NA   NA
    ## 3097  17  24  NA  NA NA NA   NA
    ## 3098   8  32  NA  NA NA NA   NA
    ## 3099  75  60  NA  NA NA NA   NA
    ## 3100   0   0  NA  NA NA NA   NA
    ## 3101  25  61  NA  NA NA NA   NA
    ## 3102  11  NA  NA   1 NA NA   NA
    ## 3103   0   0  NA  NA NA NA   NA
    ## 3104  13  19  NA  NA NA NA   NA
    ## 3105   0  18  NA  NA NA NA   NA
    ## 3106   8  NA  NA   0 NA NA   NA
    ## 3107   0   1  NA  NA NA NA   NA
    ## 3108  31  35  NA  NA NA NA   NA
    ## 3109  55  19  NA  NA NA NA   NA
    ## 3110  26  NA  NA   0 NA NA   NA
    ## 3111   1  NA  NA   0 NA NA   NA
    ## 3112   0   1  NA  NA NA NA   NA
    ## 3113  20  32  NA  NA NA NA   NA
    ## 3114   8  NA  NA   2 NA NA   NA
    ## 3115  18  44  NA  NA NA NA   NA
    ## 3116  58  NA  NA   0 NA NA   NA
    ## 3117   1  NA  NA   0 NA NA   NA
    ## 3118   4  23  NA  NA NA NA   NA
    ## 3119  36  43  NA  NA NA NA   NA
    ## 3120  33  73  NA  NA NA NA   NA
    ## 3121   0   4  NA  NA NA NA   NA
    ## 3122   1   3  NA  NA NA NA   NA
    ## 3123  22  NA  NA   1 NA NA   NA
    ## 3124  48  29  NA  NA NA NA   NA
    ## 3125   1  NA  NA   0 NA NA   NA
    ## 3126  21  NA  NA   0 NA NA   NA
    ## 3127   0  NA  NA   0 NA NA   NA
    ## 3128   1  NA  NA   0 NA NA   NA
    ## 3129   5  19  NA  NA NA NA   NA
    ## 3130   0  NA  NA   0 NA NA   NA
    ## 3131   1  NA  NA   0 NA NA   NA
    ## 3132  35  NA  NA   3 NA NA   NA
    ## 3133   3  35  NA  NA NA NA   NA
    ## 3134   0  NA  NA   0 NA NA   NA
    ## 3135  66  16  NA  NA NA NA   NA
    ## 3136   0  NA  NA   0 NA NA   NA
    ## 3137  30  NA  NA   7 NA NA   NA
    ## 3138  56  NA  NA   2 NA NA   NA
    ## 3139   6  12  NA  NA NA NA   NA
    ## 3140  39  NA  NA   1 NA NA   NA
    ## 3141  11  27  NA  NA NA NA   NA
    ## 3142  14  40  NA  NA NA NA   NA
    ## 3143  31  NA  NA   0 NA NA   NA
    ## 3144   9  79  NA  NA NA NA   NA
    ## 3145  18  NA  NA   8 NA NA   NA
    ## 3146  44  26  NA  NA NA NA   NA
    ## 3147  52  NA  NA   4 NA NA   NA
    ## 3148  64  NA  NA   1 NA NA   NA
    ## 3149   9  41  NA  NA NA NA   NA
    ## 3150   0   1  NA  NA NA NA   NA
    ## 3151   4  NA  NA   0 NA NA   NA
    ## 3152  17  NA  NA   0 NA NA   NA
    ## 3153   1  NA  NA   0 NA NA   NA
    ## 3154   0  38  NA  NA NA NA   NA
    ## 3155   7  34  NA  NA NA NA   NA
    ## 3156   4  NA  NA   1 NA NA   NA
    ## 3157  33  NA  NA   2 NA NA   NA
    ## 3158   2  NA  NA   0 NA NA   NA
    ## 3159   5  NA  NA   0 NA NA   NA
    ## 3160  10  NA  NA   0 NA NA   NA
    ## 3161   0  NA  NA   0 NA NA   NA
    ## 3162   0   3  NA  NA NA NA   NA
    ## 3163  41  15  NA  NA NA NA   NA
    ## 3164   7  NA  NA   0 NA NA   NA
    ## 3165   3  NA  NA   0 NA NA   NA
    ## 3166   5  34  NA  NA NA NA   NA
    ## 3167   1   8  NA  NA NA NA   NA
    ## 3168  10  NA  NA   0 NA NA   NA
    ## 3169   0   2  NA  NA NA NA   NA
    ## 3170   7  14  NA  NA NA NA   NA
    ## 3171  23  NA  NA   6 NA NA   NA
    ## 3172  13  54  NA  NA NA NA   NA
    ## 3173   8  34  NA  NA NA NA   NA
    ## 3174  13  27  NA  NA NA NA   NA
    ## 3175  44  NA  NA   1 NA NA   NA
    ## 3176   4  NA  NA   1 NA NA   NA
    ## 3177   9  NA  NA   0 NA NA   NA
    ## 3178   3  14  NA  NA NA NA   NA
    ## 3179  19  29  NA  NA NA NA   NA
    ## 3180   7  34  NA  NA NA NA   NA
    ## 3181   2   5  NA  NA NA NA   NA
    ## 3182  33  44  NA  NA NA NA   NA
    ## 3183  11  NA  NA   2 NA NA   NA
    ## 3184   4   4  NA  NA NA NA   NA
    ## 3185   4  12  NA  NA NA NA   NA
    ## 3186   2   9  NA  NA NA NA   NA
    ## 3187   1   5  NA  NA NA NA   NA
    ## 3188  14  68  NA  NA NA NA   NA
    ## 3189   0   1  NA  NA NA NA   NA
    ## 3190   0   1  NA  NA NA NA   NA
    ## 3191   7   9  NA  NA NA NA   NA
    ## 3192   8  NA  NA   0 NA NA   NA
    ## 3193  10  NA  NA   3 NA NA   NA
    ## 3194  36  57  NA  NA NA NA   NA
    ## 3195  29  37  NA  NA NA NA   NA
    ## 3196   2  13  NA  NA NA NA   NA
    ## 3197  28  30  NA  NA NA NA   NA
    ## 3198  16  21  NA  NA NA NA   NA
    ## 3199   2  NA  NA   0 NA NA   NA
    ## 3200   8  43  NA  NA NA NA   NA
    ## 3201  16  17  NA  NA NA NA   NA
    ## 3202  16  47  NA  NA NA NA   NA
    ## 3203   3  11  NA  NA NA NA   NA
    ## 3204  15  12  NA  NA NA NA   NA
    ## 3205  12  NA  NA   0 NA NA   NA
    ## 3206  60  NA  NA  18 NA NA   NA
    ## 3207  37  28  NA  NA NA NA   NA
    ## 3208   1   8  NA  NA NA NA   NA
    ## 3209  12  36  NA  NA NA NA   NA
    ## 3210  18  45  NA  NA NA NA   NA
    ## 3211  42  16  NA  NA NA NA   NA
    ## 3212  17  26  NA  NA NA NA   NA
    ## 3213  20  NA  NA   3 NA NA   NA
    ## 3214   7  NA  NA   2 NA NA   NA
    ## 3215   9  NA  NA   1 NA NA   NA
    ## 3216   0   0  NA  NA NA NA   NA
    ## 3217   0   3  NA  NA NA NA   NA
    ## 3218  48  NA  NA   2 NA NA   NA
    ## 3219   0   2  NA  NA NA NA   NA
    ## 3220   3  NA  NA   0 NA NA   NA
    ## 3221   0   1  NA  NA NA NA   NA
    ## 3222   7  22  NA  NA NA NA   NA
    ## 3223  22  63  NA  NA NA NA   NA
    ## 3224   0  NA  NA   0 NA NA   NA
    ## 3225   6  46  NA  NA NA NA   NA
    ## 3226  16  30  NA  NA NA NA   NA
    ## 3227   0   1  NA  NA NA NA   NA
    ## 3228  39  35  NA  NA NA NA   NA
    ## 3229   2  12  NA  NA NA NA   NA
    ## 3230  12  30  NA  NA NA NA   NA
    ## 3231  38  13  NA  NA NA NA   NA
    ## 3232  43  NA  NA   7 NA NA   NA
    ## 3233  16  NA  NA  11 NA NA   NA
    ## 3234  17  NA  NA   1 NA NA   NA
    ## 3235   2   3  NA  NA NA NA   NA
    ## 3236 102  30  NA  NA NA NA   NA
    ## 3237   7  48  NA  NA NA NA   NA
    ## 3238   2  NA  NA   0 NA NA   NA
    ## 3239   8  NA  NA   2 NA NA   NA
    ## 3240   3  19  NA  NA NA NA   NA
    ## 3241   4  59  NA  NA NA NA   NA
    ## 3242   6  NA  NA   0 NA NA   NA
    ## 3243  49  NA  NA   0 NA NA   NA
    ## 3244  57  39  NA  NA NA NA   NA
    ## 3245   4  10  NA  NA NA NA   NA
    ## 3246   0  NA  NA   0 NA NA   NA
    ## 3247  17  NA  NA   0 NA NA   NA
    ## 3248   3  NA  NA   0 NA NA   NA
    ## 3249   4  23  NA  NA NA NA   NA
    ## 3250   2  67  NA  NA NA NA   NA
    ## 3251  32  NA  NA   3 NA NA   NA
    ## 3252   0  NA  NA   0 NA NA   NA
    ## 3253   0  NA  NA   0 NA NA   NA
    ## 3254   6  NA  NA   0 NA NA   NA
    ## 3255   5  NA  NA   0 NA NA   NA
    ## 3256   0   3  NA  NA NA NA   NA
    ## 3257  35  21  NA  NA NA NA   NA
    ## 3258   3  NA  NA   0 NA NA   NA
    ## 3259   6  NA  NA   0 NA NA   NA
    ## 3260  16  NA  NA   2 NA NA   NA
    ## 3261  10  62  NA  NA NA NA   NA
    ## 3262   4  NA  NA   4 NA NA   NA
    ## 3263   2  28  NA  NA NA NA   NA
    ## 3264   0  NA  NA   0 NA NA   NA
    ## 3265  11  NA  NA   0 NA NA   NA
    ## 3266   0  NA  NA   0 NA NA   NA
    ## 3267  35  39  NA  NA NA NA   NA
    ## 3268   1  NA  NA   1 NA NA   NA
    ## 3269   0  NA  NA   0 NA NA   NA
    ## 3270   3  70  NA  NA NA NA   NA
    ## 3271  61  NA  NA   6 NA NA   NA
    ## 3272   0   0  NA  NA NA NA   NA
    ## 3273   0   5  NA  NA NA NA   NA
    ## 3274  17  42  NA  NA NA NA   NA
    ## 3275  18  NA  NA   2 NA NA   NA
    ## 3276   0  NA  NA   0 NA NA   NA
    ## 3277  83  33  NA  NA NA NA   NA
    ## 3278   8  NA  NA   1 NA NA   NA
    ## 3279   2  NA  NA   0 NA NA   NA
    ## 3280   3  NA  NA   1 NA NA   NA
    ## 3281   1  NA  NA   0 NA NA   NA
    ## 3282  66  NA  NA   3 NA NA   NA
    ## 3283  21  NA  NA   2 NA NA   NA
    ## 3284   2  12  NA  NA NA NA   NA
    ## 3285   0   1  NA  NA NA NA   NA
    ## 3286   3  47  NA  NA NA NA   NA
    ## 3287   0  NA  NA   1 NA NA   NA
    ## 3288  15  73  NA  NA NA NA   NA
    ## 3289   3  12  NA  NA NA NA   NA
    ## 3290  19  NA  NA   2 NA NA   NA
    ## 3291  59  NA  NA   7 NA NA   NA
    ## 3292  55  NA  NA   6 NA NA   NA
    ## 3293  20  NA  NA   4 NA NA   NA
    ## 3294  11  80  NA  NA NA NA   NA
    ## 3295  15  NA  NA   0 NA NA   NA
    ## 3296   8  NA  NA   4 NA NA   NA
    ## 3297   0   2  NA  NA NA NA   NA
    ## 3298  68  NA  NA   4 NA NA   NA
    ## 3299  49  NA  NA   2 NA NA   NA
    ## 3300   1  20  NA  NA NA NA   NA
    ## 3301  45  NA  NA  11 NA NA   NA
    ## 3302  50  NA  NA   3 NA NA   NA
    ## 3303   6  10  NA  NA NA NA   NA
    ## 3304   1   5  NA  NA NA NA   NA
    ## 3305   1  NA  NA   1 NA NA   NA
    ## 3306   1  NA  NA   0 NA NA   NA
    ## 3307   5  NA  NA   1 NA NA   NA
    ## 3308   3  NA  NA   0 NA NA   NA
    ## 3309   4  NA  NA   2 NA NA   NA
    ## 3310   2   3  NA  NA NA NA   NA
    ## 3311  11  NA  NA   0 NA NA   NA
    ## 3312  56  NA  NA   2 NA NA   NA
    ## 3313   2  30  NA  NA NA NA   NA
    ## 3314   9  NA  NA   2 NA NA   NA
    ## 3315   0   3  NA  NA NA NA   NA
    ## 3316   1  37  NA  NA NA NA   NA
    ## 3317   3  NA  NA   0 NA NA   NA
    ## 3318   4  NA  NA   0 NA NA   NA
    ## 3319   0   3  NA  NA NA NA   NA
    ## 3320  19  25  NA  NA NA NA   NA
    ## 3321   0  NA  NA   0 NA NA   NA
    ## 3322   0   2  NA  NA NA NA   NA
    ## 3323  21  23  NA  NA NA NA   NA
    ## 3324  26  NA  NA   1 NA NA   NA
    ## 3325  59  NA  NA   5 NA NA   NA
    ## 3326  36  44  NA  NA NA NA   NA
    ## 3327   0  NA  NA   0 NA NA   NA
    ## 3328  54  NA  NA  10 NA NA   NA
    ## 3329   4  NA  NA   0 NA NA   NA
    ## 3330  14  NA  NA   1 NA NA   NA
    ## 3331  43  NA  NA   1 NA NA   NA
    ## 3332  21  NA  NA   0 NA NA   NA
    ## 3333   2  17  NA  NA NA NA   NA
    ## 3334  10  NA  NA   0 NA NA   NA
    ## 3335  56  81  NA  NA NA NA   NA
    ## 3336  13  NA  NA   1 NA NA   NA
    ## 3337  34  NA  NA   2 NA NA   NA
    ## 3338  25  NA  NA   1 NA NA   NA
    ## 3339  15  31  NA  NA NA NA   NA
    ## 3340   0  NA  NA   0 NA NA   NA
    ## 3341   0  NA  NA   0 NA NA   NA
    ## 3342   0   8  NA  NA NA NA   NA
    ## 3343   0  NA  NA   0 NA NA   NA
    ## 3344  22  42  NA  NA NA NA   NA
    ## 3345  18  42  NA  NA NA NA   NA
    ## 3346  24  28  NA  NA NA NA   NA
    ## 3347   0  NA  NA   0 NA NA   NA
    ## 3348   0  NA  NA   0 NA NA   NA
    ## 3349  64  NA  NA   2 NA NA   NA
    ## 3350  26  NA  NA   0 NA NA   NA
    ## 3351  38  NA  NA   7 NA NA   NA
    ## 3352  11  NA  NA   1 NA NA   NA
    ## 3353   0   9  NA  NA NA NA   NA
    ## 3354   2  NA  NA   0 NA NA   NA
    ## 3355   5  15  NA  NA NA NA   NA
    ## 3356  47  NA  NA   7 NA NA   NA
    ## 3357  39  21  NA  NA NA NA   NA
    ## 3358  17  NA  NA   5 NA NA   NA
    ## 3359   0   0  NA  NA NA NA   NA
    ## 3360   6  NA  NA   0 NA NA   NA
    ## 3361   0   2  NA  NA NA NA   NA
    ## 3362  20  NA  NA   0 NA NA   NA
    ## 3363  36  46  NA  NA NA NA   NA
    ## 3364  33  NA  NA   1 NA NA   NA
    ## 3365  70  NA  NA   0 NA NA   NA
    ## 3366  19  52  NA  NA NA NA   NA
    ## 3367   4  NA  NA   0 NA NA   NA
    ## 3368   1  NA  NA   0 NA NA   NA
    ## 3369   4  NA  NA   0 NA NA   NA
    ## 3370  17  NA  NA   2 NA NA   NA
    ## 3371  20  NA  NA   0 NA NA   NA
    ## 3372   8  31  NA  NA NA NA   NA
    ## 3373   0  NA  NA   0 NA NA   NA
    ## 3374  17  36  NA  NA NA NA   NA
    ## 3375  58  48  NA  NA NA NA   NA
    ## 3376   6  NA  NA   0 NA NA   NA
    ## 3377   0   2  NA  NA NA NA   NA
    ## 3378   0  NA  NA   0 NA NA   NA
    ## 3379   3  NA  NA   1 NA NA   NA
    ## 3380  31  NA  NA   5 NA NA   NA
    ## 3381   9  NA  NA   1 NA NA   NA
    ## 3382  17  21  NA  NA NA NA   NA
    ## 3383  46  27  NA  NA NA NA   NA
    ## 3384   3  NA  NA   0 NA NA   NA
    ## 3385   1  NA  NA   0 NA NA   NA
    ## 3386   5  10  NA  NA NA NA   NA
    ## 3387  21  NA  NA   3 NA NA   NA
    ## 3388  64  NA  NA  15 NA NA   NA
    ## 3389  24  NA  NA   8 NA NA   NA
    ## 3390  15  43  NA  NA NA NA   NA
    ## 3391  26  27  NA  NA NA NA   NA
    ## 3392  12  28  NA  NA NA NA   NA
    ## 3393  57  NA  NA   4 NA NA   NA
    ## 3394   2  NA  NA   0 NA NA   NA
    ## 3395  22  NA  NA   9 NA NA   NA
    ## 3396  57  82  NA  NA NA NA   NA
    ## 3397   4  NA  NA   0 NA NA   NA
    ## 3398   8  NA  NA   0 NA NA   NA
    ## 3399  14  44  NA  NA NA NA   NA
    ## 3400   0   5  NA  NA NA NA   NA
    ## 3401   2  13  NA  NA NA NA   NA
    ## 3402   1  14  NA  NA NA NA   NA
    ## 3403   9  NA  NA   0 NA NA   NA
    ## 3404  19  NA  NA   0 NA NA   NA
    ## 3405   0   3  NA  NA NA NA   NA
    ## 3406  42  NA  NA   6 NA NA   NA
    ## 3407   0  NA  NA   0 NA NA   NA
    ## 3408   0  NA  NA   0 NA NA   NA
    ## 3409  13  NA  NA   3 NA NA   NA
    ## 3410  24  NA  NA   3 NA NA   NA
    ## 3411  12  NA  NA   0 NA NA   NA
    ## 3412   5  13  NA  NA NA NA   NA
    ## 3413  12  17  NA  NA NA NA   NA
    ## 3414   0  NA  NA   0 NA NA   NA
    ## 3415  64  NA  NA   1 NA NA   NA
    ## 3416   8  NA  NA   1 NA NA   NA
    ## 3417   1  NA  NA   0 NA NA   NA
    ## 3418   0   4  NA  NA NA NA   NA
    ## 3419   0  NA  NA   0 NA NA   NA
    ## 3420   4  NA  NA   0 NA NA   NA
    ## 3421   7  26  NA  NA NA NA   NA
    ## 3422  26  21  NA  NA NA NA   NA
    ## 3423  70  NA  NA   3 NA NA   NA
    ## 3424   3  10  NA  NA NA NA   NA
    ## 3425  29  NA  NA   0 NA NA   NA
    ## 3426   7  NA  NA   1 NA NA   NA
    ## 3427   7  17  NA  NA NA NA   NA
    ## 3428   1  NA  NA   0 NA NA   NA
    ## 3429   0  NA  NA   0 NA NA   NA
    ## 3430  10  NA  NA   1 NA NA   NA
    ## 3431  35  31  NA  NA NA NA   NA
    ## 3432   0   5  NA  NA NA NA   NA
    ## 3433   1  NA  NA   0 NA NA   NA
    ## 3434  10  NA  NA   0 NA NA   NA
    ## 3435   0   2  NA  NA NA NA   NA
    ## 3436   0  NA  NA   1 NA NA   NA
    ## 3437  19  46  NA  NA NA NA   NA
    ## 3438   0  NA  NA   0 NA NA   NA
    ## 3439  29  NA  NA  14 NA NA   NA
    ## 3440   7  47  NA  NA NA NA   NA
    ## 3441  33  NA  NA   2 NA NA   NA
    ## 3442  37  NA  NA   1 NA NA   NA
    ## 3443  31  35  NA  NA NA NA   NA
    ## 3444   1  NA  NA   0 NA NA   NA
    ## 3445  51  NA  NA   6 NA NA   NA
    ## 3446  29  39  NA  NA NA NA   NA
    ## 3447   5  46  NA  NA NA NA   NA
    ## 3448  80  71  NA  NA NA NA   NA
    ## 3449   0   1  NA  NA NA NA   NA
    ## 3450   0   1  NA  NA NA NA   NA
    ## 3451  33  61  NA  NA NA NA   NA
    ## 3452  27  NA  NA   3 NA NA   NA
    ## 3453  23  75  NA  NA NA NA   NA
    ## 3454   0   1  NA  NA NA NA   NA
    ## 3455   0  NA  NA   0 NA NA   NA
    ## 3456   1  12  NA  NA NA NA   NA
    ## 3457   1  NA  NA   1 NA NA   NA
    ## 3458  36  40  NA   5 NA NA   NA
    ## 3459  21  21  NA   3 NA NA   NA
    ## 3460  60  18  NA   1 NA NA   NA
    ## 3461   8  12  NA   1 NA NA   NA
    ## 3462   5  12  NA   0 NA NA   NA
    ## 3463   6  19  NA   4 NA NA   NA
    ## 3464  10   6  NA   1 NA NA   NA
    ## 3465  10  42  NA   0 NA NA   NA
    ## 3466  30  24  NA   4 NA NA   NA
    ## 3467  25  31  NA   5 NA NA   NA
    ## 3468  19  29  NA   3 NA NA   NA
    ## 3469   0   4  NA   0 NA NA   NA
    ## 3470   0   2  NA   0 NA NA   NA
    ## 3471   7   8  NA   2 NA NA   NA
    ## 3472  30  22  NA   0 NA NA   NA
    ## 3473  13  12  NA   0 NA NA   NA
    ## 3474   1   2  NA   0 NA NA   NA
    ## 3475   9  18  NA   2 NA NA   NA
    ## 3476  20  51  NA   2 NA NA   NA
    ## 3477   9  10  NA   1 NA NA   NA
    ## 3478  71   9  NA   6 NA NA   NA
    ## 3479  55  39  NA   8 NA NA   NA
    ## 3480  11  40  NA   1 NA NA   NA
    ## 3481   8  25  NA   1 NA NA   NA
    ## 3482  10  15  NA   3 NA NA   NA
    ## 3483  11   3  NA   1 NA NA   NA
    ## 3484  29  14  NA   3 NA NA   NA
    ## 3485  18  22  NA   4 NA NA   NA
    ## 3486   0   1  NA   0 NA NA   NA
    ## 3487  63  47  NA   5 NA NA   NA
    ## 3488  34  32  NA   1 NA NA   NA
    ## 3489  11  10  NA   2 NA NA   NA
    ## 3490   9   5  NA   1 NA NA   NA
    ## 3491   0   1  NA   0 NA NA   NA
    ## 3492  19  32  NA   4 NA NA   NA
    ## 3493  17  30  NA   9 NA NA   NA
    ## 3494  36  21  NA   2 NA NA   NA
    ## 3495  15  27  NA   4 NA NA   NA
    ## 3496  66  21  NA   6 NA NA   NA
    ## 3497   0   0  NA   0 NA NA   NA
    ## 3498   6  20  NA   0 NA NA   NA
    ## 3499  12  13  NA   0 NA NA   NA
    ## 3500   0   0  NA   0 NA NA   NA
    ## 3501   7  11  NA   1 NA NA   NA
    ## 3502  11  25  NA   0 NA NA   NA
    ## 3503   9  24  NA   4 NA NA   NA
    ## 3504  31  40  NA   1 NA NA   NA
    ## 3505   0   0  NA   0 NA NA   NA
    ## 3506  39  33  NA   2 NA NA   NA
    ## 3507  27  11  NA   7 NA NA   NA
    ## 3508  75  50  NA   8 NA NA   NA
    ## 3509  16  16  NA   1 NA NA   NA
    ## 3510   2   9  NA   0 NA NA   NA
    ## 3511  11  25  NA   4 NA NA   NA
    ## 3512   2   1  NA   0 NA NA   NA
    ## 3513  14  10  NA   4 NA NA   NA
    ## 3514   1   6  NA   0 NA NA   NA
    ## 3515   1   0  NA   0 NA NA   NA
    ## 3516   2   3  NA   3 NA NA   NA
    ## 3517  15  14  NA   1 NA NA   NA
    ## 3518  10  43  NA   1 NA NA   NA
    ## 3519   2   2  NA   0 NA NA   NA
    ## 3520  10  20  NA   2 NA NA   NA
    ## 3521   3   1  NA   1 NA NA   NA
    ## 3522   9   8  NA   2 NA NA   NA
    ## 3523   3   9  NA   0 NA NA   NA
    ## 3524  14  27  NA   1 NA NA   NA
    ## 3525   3  30  NA   0 NA NA   NA
    ## 3526  45  43  NA   6 NA NA   NA
    ## 3527  22  25  NA   0 NA NA   NA
    ## 3528   8  18  NA   1 NA NA   NA
    ## 3529  22  18  NA   0 NA NA   NA
    ## 3530  28  27  NA   5 NA NA   NA
    ## 3531   8   8  NA   2 NA NA   NA
    ## 3532   9   7  NA   1 NA NA   NA
    ## 3533  13  22  NA   3 NA NA   NA
    ## 3534   1   0  NA   0 NA NA   NA
    ## 3535  21  16  NA   2 NA NA   NA
    ## 3536  16  26  NA   3 NA NA   NA
    ## 3537  15  20  NA   3 NA NA   NA
    ## 3538  25  12  NA   0 NA NA   NA
    ## 3539   6   2  NA   1 NA NA   NA
    ## 3540  30  33  NA   3 NA NA   NA
    ## 3541   0   7  NA   0 NA NA   NA
    ## 3542  42  29  NA  10 NA NA   NA
    ## 3543  20  12  NA   1 NA NA   NA
    ## 3544   0   3  NA   0 NA NA   NA
    ## 3545  82  81  NA   4 NA NA   NA
    ## 3546  34  19  NA   2 NA NA   NA
    ## 3547   7  13  NA   2 NA NA   NA
    ## 3548   3  11  NA   1 NA NA   NA
    ## 3549   4  28  NA   0 NA NA   NA
    ## 3550   1   7  NA   0 NA NA   NA
    ## 3551   0   0  NA   0 NA NA   NA
    ## 3552  82  44  NA  10 NA NA   NA
    ## 3553  23  20  NA   2 NA NA   NA
    ## 3554  36  21  NA   1 NA NA   NA
    ## 3555   2  47  NA   0 NA NA   NA
    ## 3556   8   2  NA   1 NA NA   NA
    ## 3557   1   4  NA   0 NA NA   NA
    ## 3558  12  11  NA   0 NA NA   NA
    ## 3559   0   7  NA   0 NA NA   NA
    ## 3560   1   6  NA   0 NA NA   NA
    ## 3561   0   0  NA   0 NA NA   NA
    ## 3562  24  43  NA   1 NA NA   NA
    ## 3563  10  32  NA   1 NA NA   NA
    ## 3564   3   7  NA   2 NA NA   NA
    ## 3565  12  21  NA   5 NA NA   NA
    ## 3566   5  18  NA   0 NA NA   NA
    ## 3567   7  46  NA   1 NA NA   NA
    ## 3568  41   8  NA  10 NA NA   NA
    ## 3569  41  23  NA   8 NA NA   NA
    ## 3570   0   0  NA   0 NA NA   NA
    ## 3571  42  18  NA   7 NA NA   NA
    ## 3572  54  25  NA   1 NA NA   NA
    ## 3573   0   3  NA   0 NA NA   NA
    ## 3574  25  31  NA   6 NA NA   NA
    ## 3575  55  17  NA   8 NA NA   NA
    ## 3576   6   6  NA   0 NA NA   NA
    ## 3577   5   6  NA   2 NA NA   NA
    ## 3578   7  24  NA   2 NA NA   NA
    ## 3579   2   3  NA   0 NA NA   NA
    ## 3580  38  43  NA   0 NA NA   NA
    ## 3581  30  24  NA   2 NA NA   NA
    ## 3582   7  11  NA   1 NA NA   NA
    ## 3583   0   2  NA   0 NA NA   NA
    ## 3584   0   1  NA   0 NA NA   NA
    ## 3585   0   4  NA   0 NA NA   NA
    ## 3586   4  42  NA   2 NA NA   NA
    ## 3587  31  38  NA   6 NA NA   NA
    ## 3588   1   0  NA   0 NA NA   NA
    ## 3589   6   6  NA   1 NA NA   NA
    ## 3590   6   5  NA   0 NA NA   NA
    ## 3591  48  24  NA   8 NA NA   NA
    ## 3592  30  26  NA   3 NA NA   NA
    ## 3593   7  23  NA   0 NA NA   NA
    ## 3594  17  28  NA   3 NA NA   NA
    ## 3595  53  46  NA   7 NA NA   NA
    ## 3596   3   2  NA   1 NA NA   NA
    ## 3597   4   6  NA   0 NA NA   NA
    ## 3598  48  26  NA   3 NA NA   NA
    ## 3599   3   6  NA   1 NA NA   NA
    ## 3600   0  12  NA   0 NA NA   NA
    ## 3601   0   6  NA   1 NA NA   NA
    ## 3602  16  35  NA   0 NA NA   NA
    ## 3603  19  12  NA   3 NA NA   NA
    ## 3604  12  15  NA   6 NA NA   NA
    ## 3605   2  16  NA   1 NA NA   NA
    ## 3606   0   3  NA   0 NA NA   NA
    ## 3607   0   0  NA   0 NA NA   NA
    ## 3608  20  41  NA   0 NA NA   NA
    ## 3609  11  17  NA   1 NA NA   NA
    ## 3610  55  40  NA   1 NA NA   NA
    ## 3611  38  26  NA   2 NA NA   NA
    ## 3612  31  19  NA   1 NA NA   NA
    ## 3613  24  42  NA   0 NA NA   NA
    ## 3614   0   3  NA   0 NA NA   NA
    ## 3615   0   7  NA   0 NA NA   NA
    ## 3616   0   5  NA   0 NA NA   NA
    ## 3617   1   9  NA   0 NA NA   NA
    ## 3618   1  14  NA   1 NA NA   NA
    ## 3619   1   2  NA   0 NA NA   NA
    ## 3620   7   5  NA   1 NA NA   NA
    ## 3621  14  39  NA   1 NA NA   NA
    ## 3622  48  13  NA   8 NA NA   NA
    ## 3623  45  29  NA   5 NA NA   NA
    ## 3624   0   5  NA   0 NA NA   NA
    ## 3625   7  18  NA   2 NA NA   NA
    ## 3626  47  16  NA   6 NA NA   NA
    ## 3627   1   0  NA   0 NA NA   NA
    ## 3628   0   1  NA   0 NA NA   NA
    ## 3629   8  17  NA   3 NA NA   NA
    ## 3630  83  63  NA   5 NA NA   NA
    ## 3631  12  17  NA   2 NA NA   NA
    ## 3632  23  24  NA   9 NA NA   NA
    ## 3633  15  18  NA   6 NA NA   NA
    ## 3634   5   4  NA   1 NA NA   NA
    ## 3635   4   3  NA   0 NA NA   NA
    ## 3636   0   6  NA   0 NA NA   NA
    ## 3637  15  10  NA   0 NA NA   NA
    ## 3638  10  25  NA   1 NA NA   NA
    ## 3639   2   5  NA   1 NA NA   NA
    ## 3640  80  45  NA   6 NA NA   NA
    ## 3641   2   0  NA   0 NA NA   NA
    ## 3642  23  67  NA   2 NA NA   NA
    ## 3643   5  16  NA   1 NA NA   NA
    ## 3644   1   1  NA   1 NA NA   NA
    ## 3645   7   6  NA   3 NA NA   NA
    ## 3646  11   8  NA   2 NA NA   NA
    ## 3647  60  32  NA   1 NA NA   NA
    ## 3648   8   9  NA   0 NA NA   NA
    ## 3649  11  27  NA   1 NA NA   NA
    ## 3650   0   1  NA   0 NA NA   NA
    ## 3651  55  30  NA   5 NA NA   NA
    ## 3652  76  34  NA  12 NA NA   NA
    ## 3653  16  12  NA   2 NA NA   NA
    ## 3654  35  13  NA   2 NA NA   NA
    ## 3655  21  30  NA   3 NA NA   NA
    ## 3656   1   6  NA   0 NA NA   NA
    ## 3657   5  16  NA   2 NA NA   NA
    ## 3658   2   4  NA   0 NA NA   NA
    ## 3659  37  86  NA   1 NA NA   NA
    ## 3660   6   4  NA   1 NA NA   NA
    ## 3661  11  32  NA   1 NA NA   NA
    ## 3662  16  24  NA   4 NA NA   NA
    ## 3663  21  14  NA   3 NA NA   NA
    ## 3664   3  18  NA   0 NA NA   NA
    ## 3665   0   0  NA   0 NA NA   NA
    ## 3666   2   4  NA   0 NA NA   NA
    ## 3667  40  26  NA   2 NA NA   NA
    ## 3668  22   7  NA   5 NA NA   NA
    ## 3669  60  30  NA   2 NA NA   NA
    ## 3670   3   1  NA   0 NA NA   NA
    ## 3671  48  11  NA   8 NA NA   NA
    ## 3672   0   1  NA   0 NA NA   NA
    ## 3673  86  47  NA   5 NA NA   NA
    ## 3674  21  17  NA   5 NA NA   NA
    ## 3675  40  42  NA   4 NA NA   NA
    ## 3676   6   7  NA   0 NA NA   NA
    ## 3677   0   2  NA   0 NA NA   NA
    ## 3678   2  14  NA   1 NA NA   NA
    ## 3679   2   0  NA   0 NA NA   NA
    ## 3680   7  15  NA   0 NA NA   NA
    ## 3681   1   4  NA   1 NA NA   NA
    ## 3682  50  20  NA   5 NA NA   NA
    ## 3683  36  11  NA   5 NA NA   NA
    ## 3684   7   6  NA   1 NA NA   NA
    ## 3685  22  21  NA   1 NA NA   NA
    ## 3686   8  17  NA   0 NA NA   NA
    ## 3687   1   0  NA   0 NA NA   NA
    ## 3688   2   6  NA   0 NA NA   NA
    ## 3689  16  19  NA   4 NA NA   NA
    ## 3690   8  15  NA   0 NA NA   NA
    ## 3691  34  20  NA   1 NA NA   NA
    ## 3692  45  30  NA   6 NA NA   NA
    ## 3693   0   2  NA   0 NA NA   NA
    ## 3694  61  20  NA   6 NA NA   NA
    ## 3695   2   9  NA   0 NA NA   NA
    ## 3696  35  46  NA  10 NA NA   NA
    ## 3697  10  21  NA   0 NA NA   NA
    ## 3698  46  38  NA  10 NA NA   NA
    ## 3699   0   0  NA   0 NA NA   NA
    ## 3700  18  21  NA   2 NA NA   NA
    ## 3701 106  40  NA   6 NA NA   NA
    ## 3702   5   6  NA   0 NA NA   NA
    ## 3703  19   9  NA   0 NA NA   NA
    ## 3704   8   2  NA   1 NA NA   NA
    ## 3705  24  24  NA   5 NA NA   NA
    ## 3706  22  29  NA  15 NA NA   NA
    ## 3707  11   7  NA   1 NA NA   NA
    ## 3708  36  25  NA   4 NA NA   NA
    ## 3709  31  40  NA   2 NA NA   NA
    ## 3710   0   1  NA   0 NA NA   NA
    ## 3711  14  15  NA   1 NA NA   NA
    ## 3712  92  49  NA  17 NA NA   NA
    ## 3713  10   9  NA   5 NA NA   NA
    ## 3714   9  18  NA   3 NA NA   NA
    ## 3715   0   0  NA   1 NA NA   NA
    ## 3716  39  11  NA   3 NA NA   NA
    ## 3717   0   1  NA   0 NA NA   NA
    ## 3718   3   2  NA   0 NA NA   NA
    ## 3719  53  19  NA   6 NA NA   NA
    ## 3720   1   9  NA   0 NA NA   NA
    ## 3721   2   1  NA   0 NA NA   NA
    ## 3722  56  32  NA   6 NA NA   NA
    ## 3723  71  68  NA   4 NA NA   NA
    ## 3724   3  10  NA   0 NA NA   NA
    ## 3725  16  36  NA   2 NA NA   NA
    ## 3726   1  13  NA   0 NA NA   NA
    ## 3727   8  14  NA   0 NA NA   NA
    ## 3728   1   0  NA   0 NA NA   NA
    ## 3729   7  10  NA   0 NA NA   NA
    ## 3730  21  16  NA   4 NA NA   NA
    ## 3731   1   3  NA   0 NA NA   NA
    ## 3732   3   4  NA   0 NA NA   NA
    ## 3733   0   3  NA   0 NA NA   NA
    ## 3734  11  16  NA   1 NA NA   NA
    ## 3735  13  18  NA   1 NA NA   NA
    ## 3736  26  11  NA   1 NA NA   NA
    ## 3737  30  48  NA  13 NA NA   NA
    ## 3738   9  38  NA   1 NA NA   NA
    ## 3739  63  36  NA   4 NA NA   NA
    ## 3740   7  19  NA   1 NA NA   NA
    ## 3741   0   1  NA   0 NA NA   NA
    ## 3742   0   2  NA   0 NA NA   NA
    ## 3743   3   9  NA   1 NA NA   NA
    ## 3744  56  38  NA   7 NA NA   NA
    ## 3745  53  16  NA   3 NA NA   NA
    ## 3746  36  53  NA   4 NA NA   NA
    ## 3747  21  20  NA   1 NA NA   NA
    ## 3748  13   6  NA   6 NA NA   NA
    ## 3749   0   4  NA   0 NA NA   NA
    ## 3750  46  41  NA   3 NA NA   NA
    ## 3751  21  16  NA   0 NA NA   NA
    ## 3752  13  24  NA   1 NA NA   NA
    ## 3753   8   9  NA   4 NA NA   NA
    ## 3754   0   0  NA   0 NA NA   NA
    ## 3755  31  31  NA   3 NA NA   NA
    ## 3756   4   4  NA   0 NA NA   NA
    ## 3757  16  19  NA   0 NA NA   NA
    ## 3758  32  19  NA   9 NA NA   NA
    ## 3759  32  31  NA   3 NA NA   NA
    ## 3760   2   7  NA   0 NA NA   NA
    ## 3761   1   9  NA   0 NA NA   NA
    ## 3762   3  11  NA   0 NA NA   NA
    ## 3763   3   1  NA   0 NA NA   NA
    ## 3764  17  40  NA   2 NA NA   NA
    ## 3765  27  10  NA   2 NA NA   NA
    ## 3766  29  45  NA  29 NA NA   NA
    ## 3767   8  19  NA   2 NA NA   NA
    ## 3768  15  15  NA   1 NA NA   NA
    ## 3769   1   0  NA   0 NA NA   NA
    ## 3770  29  12  NA   4 NA NA   NA
    ## 3771   1   2  NA   1 NA NA   NA
    ## 3772  25  21  NA  11 NA NA   NA
    ## 3773   6   1  NA   1 NA NA   NA
    ## 3774  38  49  NA   3 NA NA   NA
    ## 3775   6  39  NA   0 NA NA   NA
    ## 3776  15  15  NA   0 NA NA   NA
    ## 3777  47  36  NA   0 NA NA   NA
    ## 3778  26  15  NA   9 NA NA   NA
    ## 3779  55  18  NA   2 NA NA   NA
    ## 3780  18  24  NA   0 NA NA   NA
    ## 3781   0   2  NA   0 NA NA   NA
    ## 3782   3   3  NA   0 NA NA   NA
    ## 3783   4   2  NA   0 NA NA   NA
    ## 3784   0   0  NA   0 NA NA   NA
    ## 3785  73  57  NA   5 NA NA   NA
    ## 3786  36  44  NA   7 NA NA   NA
    ## 3787  34  19  NA   8 NA NA   NA
    ## 3788  40  51  NA   6 NA NA   NA
    ## 3789   0   0  NA   0 NA NA   NA
    ## 3790   4   4  NA   1 NA NA   NA
    ## 3791  41  56  NA   7 NA NA   NA
    ## 3792   9  14  NA   1 NA NA   NA
    ## 3793  21  41  NA   3 NA NA   NA
    ## 3794  13  25  NA   0 NA NA   NA
    ## 3795  47  24  NA   1 NA NA   NA
    ## 3796   5  10  NA   0 NA NA   NA
    ## 3797  26  68  NA   1 NA NA   NA
    ## 3798   3  33  NA   3 NA NA   NA
    ## 3799   3   3  NA   0 NA NA   NA
    ## 3800   5  47  NA   1 NA NA   NA
    ## 3801   0   0  NA   0 NA NA   NA
    ## 3802  26  51  NA   4 NA NA   NA
    ## 3803  32  41  NA   6 NA NA   NA
    ## 3804  27  41  NA   7 NA NA   NA
    ## 3805   6   8  NA   0 NA NA   NA
    ## 3806   7  22  NA   2 NA NA   NA
    ## 3807  31  40  NA   2 NA NA   NA
    ## 3808  25  13  NA   1 NA NA   NA
    ## 3809   1   4  NA   0 NA NA   NA
    ## 3810   0   1  NA   0 NA NA   NA
    ## 3811   1  13  NA   0 NA NA   NA
    ## 3812   6  31  NA   1 NA NA   NA
    ## 3813  13  40  NA   3 NA NA   NA
    ## 3814   0   2  NA   0 NA NA   NA
    ## 3815   3   9  NA   2 NA NA   NA
    ## 3816   1   6  NA   0 NA NA   NA
    ## 3817   0   0  NA   0 NA NA   NA
    ## 3818  68  13  NA  12 NA NA   NA
    ## 3819  37  38  NA   4 NA NA   NA
    ## 3820  30  68  NA   1 NA NA   NA
    ## 3821   1   8  NA   0 NA NA   NA
    ## 3822   0   3  NA   0 NA NA   NA
    ## 3823   6  24  NA   0 NA NA   NA
    ## 3824   7   5  NA   0 NA NA   NA
    ## 3825   2  11  NA   2 NA NA   NA
    ## 3826   2   5  NA   1 NA NA   NA
    ## 3827   8  39  NA   5 NA NA   NA
    ## 3828   1   4  NA   0 NA NA   NA
    ## 3829   1   3  NA   3 NA NA   NA
    ## 3830  24  13  NA   1 NA NA   NA
    ## 3831  14   7  NA   3 NA NA   NA
    ## 3832  26  49  NA   3 NA NA   NA
    ## 3833   5  18  NA   2 NA NA   NA
    ## 3834  19  36  NA   0 NA NA   NA
    ## 3835   2  18  NA   0 NA NA   NA
    ## 3836   5  51  NA   5 NA NA   NA
    ## 3837   0   8  NA   0 NA NA   NA
    ## 3838  32  31  NA  10 NA NA   NA
    ## 3839  45  40  NA   4 NA NA   NA
    ## 3840   3  28  NA   0 NA NA   NA
    ## 3841   6   7  NA   0 NA NA   NA
    ## 3842   3   7  NA   2 NA NA   NA
    ## 3843   0   0  NA   0 NA NA   NA
    ## 3844   9   8  NA   2 NA NA   NA
    ## 3845   1   2  NA   0 NA NA   NA
    ## 3846   7  48  NA   0 NA NA   NA
    ## 3847  10  36  NA   4 NA NA   NA
    ## 3848   3   1  NA   0 NA NA   NA
    ## 3849   5  23  NA   2 NA NA   NA
    ## 3850  20  27  NA   2 NA NA   NA
    ## 3851  29  52  NA   4 NA NA   NA
    ## 3852  41  48  NA   4 NA NA   NA
    ## 3853   9   7  NA   1 NA NA   NA
    ## 3854  12  37  NA   4 NA NA   NA
    ## 3855  73  44  NA   4 NA NA   NA
    ## 3856   1   6  NA   0 NA NA   NA
    ## 3857   8  25  NA   3 NA NA   NA
    ## 3858   5  33  NA   4 NA NA   NA
    ## 3859  15  14  NA   4 NA NA   NA
    ## 3860   4   5  NA   2 NA NA   NA
    ## 3861   3  11  NA   0 NA NA   NA
    ## 3862   0   1  NA   0 NA NA   NA
    ## 3863   2  10  NA   1 NA NA   NA
    ## 3864   3  24  NA   0 NA NA   NA
    ## 3865   1   0  NA   0 NA NA   NA
    ## 3866   5  39  NA   2 NA NA   NA
    ## 3867  10  28  NA   0 NA NA   NA
    ## 3868   7  42  NA   1 NA NA   NA
    ## 3869   6  28  NA   2 NA NA   NA
    ## 3870  10  26  NA   1 NA NA   NA
    ## 3871  14  23  NA   3 NA NA   NA
    ## 3872   3  12  NA   1 NA NA   NA
    ## 3873  20  56  NA   6 NA NA   NA
    ## 3874   2  18  NA   0 NA NA   NA
    ## 3875  12  26  NA   1 NA NA   NA
    ## 3876   9  79  NA   2 NA NA   NA
    ## 3877   4   3  NA   0 NA NA   NA
    ## 3878   1   3  NA   0 NA NA   NA
    ## 3879  21  26  NA   1 NA NA   NA
    ## 3880  20  16  NA   3 NA NA   NA
    ## 3881   9  32  NA   1 NA NA   NA
    ## 3882  16  30  NA   3 NA NA   NA
    ## 3883   0   5  NA   0 NA NA   NA
    ## 3884  31  70  NA   5 NA NA   NA
    ## 3885   1   6  NA   0 NA NA   NA
    ## 3886   2  20  NA   2 NA NA   NA
    ## 3887   3  10  NA   2 NA NA   NA
    ## 3888  24  28  NA   3 NA NA   NA
    ## 3889   1  15  NA   0 NA NA   NA
    ## 3890  12  34  NA  21 NA NA   NA
    ## 3891   2  15  NA   2 NA NA   NA
    ## 3892   0   1  NA   0 NA NA   NA
    ## 3893   0   3  NA   0 NA NA   NA
    ## 3894  31  38  NA  13 NA NA   NA
    ## 3895   4  41  NA   0 NA NA   NA
    ## 3896  26  49  NA   2 NA NA   NA
    ## 3897  63  76  NA   1 NA NA   NA
    ## 3898   9   7  NA   0 NA NA   NA
    ## 3899   8  19  NA   0 NA NA   NA
    ## 3900   1  21  NA   1 NA NA   NA
    ## 3901  53  66  NA   7 NA NA   NA
    ## 3902   9  20  NA   3 NA NA   NA
    ## 3903  28  27  NA   2 NA NA   NA
    ## 3904   0   0  NA   0 NA NA   NA
    ## 3905  10  14  NA   1 NA NA   NA
    ## 3906  21  32  NA   2 NA NA   NA
    ## 3907   0   1  NA   0 NA NA   NA
    ## 3908   1  51  NA   0 NA NA   NA
    ## 3909   0   0  NA   0 NA NA   NA
    ## 3910  14  15  NA   1 NA NA   NA
    ## 3911   1   1  NA   0 NA NA   NA
    ## 3912   0   0  NA   0 NA NA   NA
    ## 3913   0   0  NA   0 NA NA   NA
    ## 3914   0   2  NA   0 NA NA   NA
    ## 3915  12  30  NA   1 NA NA   NA
    ## 3916   0   0  NA   0 NA NA   NA
    ## 3917   7  36  NA   3 NA NA   NA
    ## 3918   0   1  NA   0 NA NA   NA
    ## 3919   0  20  NA   0 NA NA   NA
    ## 3920  14  17  NA   7 NA NA   NA
    ## 3921  12  27  NA   9 NA NA   NA
    ## 3922   3  16  NA   0 NA NA   NA
    ## 3923   0   4  NA   2 NA NA   NA
    ## 3924   2   8  NA   2 NA NA   NA
    ## 3925   8  14  NA   4 NA NA   NA
    ## 3926  11  24  NA   3 NA NA   NA
    ## 3927  30  31  NA   2 NA NA   NA
    ## 3928  30  51  NA   6 NA NA   NA
    ## 3929   0   2  NA   0 NA NA   NA
    ## 3930  55  34  NA   5 NA NA   NA
    ## 3931   0   0  NA   0 NA NA   NA
    ## 3932   6  23  NA   1 NA NA   NA
    ## 3933   0   2  NA   1 NA NA   NA
    ## 3934   2  14  NA   3 NA NA   NA
    ## 3935   1   2  NA   0 NA NA   NA
    ## 3936   1   4  NA   0 NA NA   NA
    ## 3937   1  12  NA   0 NA NA   NA
    ## 3938   4  13  NA   4 NA NA   NA
    ## 3939  11  12  NA   0 NA NA   NA
    ## 3940  15  32  NA   4 NA NA   NA
    ## 3941   1   1  NA   0 NA NA   NA
    ## 3942   2  18  NA   2 NA NA   NA
    ## 3943   1  39  NA   0 NA NA   NA
    ## 3944  11  16  NA   6 NA NA   NA
    ## 3945   0   2  NA   0 NA NA   NA
    ## 3946  11  28  NA   3 NA NA   NA
    ## 3947   1   3  NA   0 NA NA   NA
    ## 3948   2   0  NA   0 NA NA   NA
    ## 3949  41  45  NA   8 NA NA   NA
    ## 3950   4  16  NA   2 NA NA   NA
    ## 3951  50  47  NA  10 NA NA   NA
    ## 3952   2   8  NA   1 NA NA   NA
    ## 3953   0   1  NA   0 NA NA   NA
    ## 3954  16  39  NA   2 NA NA   NA
    ## 3955  26  44  NA   7 NA NA   NA
    ## 3956  69  48  NA  11 NA NA   NA
    ## 3957  18  34  NA   2 NA NA   NA
    ## 3958   7  28  NA   0 NA NA   NA
    ## 3959  33  56  NA   3 NA NA   NA
    ## 3960   5  18  NA   2 NA NA   NA
    ## 3961  15  33  NA   1 NA NA   NA
    ## 3962   1   5  NA   0 NA NA   NA
    ## 3963   2  34  NA   1 NA NA   NA
    ## 3964   0   4  NA   1 NA NA   NA
    ## 3965   2  10  NA   0 NA NA   NA
    ## 3966   4  56  NA   0 NA NA   NA
    ## 3967  22  51  NA   5 NA NA   NA
    ## 3968  31  39  NA   4 NA NA   NA
    ## 3969  25  34  NA   3 NA NA   NA
    ## 3970  11  16  NA   1 NA NA   NA
    ## 3971   0   1  NA   0 NA NA   NA
    ## 3972  40  64  NA   1 NA NA   NA
    ## 3973   0   5  NA   1 NA NA   NA
    ## 3974   5  13  NA   0 NA NA   NA
    ## 3975   0   0  NA   0 NA NA   NA
    ## 3976   3  15  NA   1 NA NA   NA
    ## 3977   1   2  NA   0 NA NA   NA
    ## 3978   5  34  NA   1 NA NA   NA
    ## 3979   9  68  NA   2 NA NA   NA
    ## 3980  33  28  NA  13 NA NA   NA
    ## 3981   1   1  NA   0 NA NA   NA
    ## 3982  43  35  NA   8 NA NA   NA
    ## 3983   1   1  NA   0 NA NA   NA
    ## 3984  41  43  NA   7 NA NA   NA
    ## 3985  20  47  NA   3 NA NA   NA
    ## 3986  17  18  NA   8 NA NA   NA
    ## 3987  52  75  NA  15 NA NA   NA
    ## 3988   1   6  NA   2 NA NA   NA
    ## 3989   1   3  NA   0 NA NA   NA
    ## 3990  12  23  NA   2 NA NA   NA
    ## 3991  21  45  NA   3 NA NA   NA
    ## 3992   5  14  NA   1 NA NA   NA
    ## 3993  38  22  NA   3 NA NA   NA
    ## 3994  40  40  NA   1 NA NA   NA
    ## 3995   6   5  NA   0 NA NA   NA
    ## 3996   6  15  NA   0 NA NA   NA
    ## 3997   5  21  NA   2 NA NA   NA
    ## 3998  16  26  NA   2 NA NA   NA
    ## 3999   4   9  NA   0 NA NA   NA
    ## 4000   0   4  NA   0 NA NA   NA
    ## 4001   7  16  NA   4 NA NA   NA
    ## 4002  28  30  NA   6 NA NA   NA
    ## 4003  43  32  NA   5 NA NA   NA
    ## 4004   1   9  NA   2 NA NA   NA
    ## 4005  67  72  NA  11 NA NA   NA
    ## 4006  18  16  NA   7 NA NA   NA
    ## 4007  17  26  NA   2 NA NA   NA
    ## 4008   5   4  NA   0 NA NA   NA
    ## 4009   3  44  NA   1 NA NA   NA
    ## 4010  55  68  NA   2 NA NA   NA
    ## 4011   0   4  NA   0 NA NA   NA
    ## 4012   8  21  NA   3 NA NA   NA
    ## 4013   9  33  NA   1 NA NA   NA
    ## 4014   6  11  NA   0 NA NA   NA
    ## 4015   1   7  NA   0 NA NA   NA
    ## 4016  37  46  NA   6 NA NA   NA
    ## 4017  16  14  NA   3 NA NA   NA
    ## 4018  50  46  NA   4 NA NA   NA
    ## 4019   2   7  NA   1 NA NA   NA
    ## 4020   2   2  NA   0 NA NA   NA
    ## 4021  67  23  NA   7 NA NA   NA
    ## 4022   0   1  NA   0 NA NA   NA
    ## 4023   9  70  NA   0 NA NA   NA
    ## 4024  30  61  NA   7 NA NA   NA
    ## 4025   4  21  NA   1 NA NA   NA
    ## 4026  17  24  NA   4 NA NA   NA
    ## 4027   6  10  NA   1 NA NA   NA
    ## 4028   4  41  NA   0 NA NA   NA
    ## 4029  44  28  NA   4 NA NA   NA
    ## 4030  24  30  NA   3 NA NA   NA
    ## 4031   1   9  NA   0 NA NA   NA
    ## 4032   7  15  NA   8 NA NA   NA
    ## 4033   0   0  NA   0 NA NA   NA
    ## 4034   8  14  NA   1 NA NA   NA
    ## 4035   7   9  NA   1 NA NA   NA
    ## 4036  32  38  NA   3 NA NA   NA
    ## 4037  27  50  NA   7 NA NA   NA
    ## 4038  66  22  NA  12 NA NA   NA
    ## 4039  31  46  NA   5 NA NA   NA
    ## 4040   8  39  NA   0 NA NA   NA
    ## 4041   1   5  NA   0 NA NA   NA
    ## 4042  27  34  NA   3 NA NA   NA
    ## 4043   5   6  NA   1 NA NA   NA
    ## 4044   2   5  NA   0 NA NA   NA
    ## 4045   3  14  NA   2 NA NA   NA
    ## 4046  35  36  NA   4 NA NA   NA
    ## 4047   9  18  NA   2 NA NA   NA
    ## 4048   6  11  NA   1 NA NA   NA
    ## 4049   1  18  NA   0 NA NA   NA
    ## 4050   1   0  NA   0 NA NA   NA
    ## 4051  17  56  NA  18 NA NA   NA
    ## 4052  15  35  NA   1 NA NA   NA
    ## 4053  17  23  NA   1 NA NA   NA
    ## 4054   9  26  NA   0 NA NA   NA
    ## 4055 116  78  NA  12 NA NA   NA
    ## 4056   6  28  NA   1 NA NA   NA
    ## 4057  19  28  NA   3 NA NA   NA
    ## 4058  35  50  NA   5 NA NA   NA
    ## 4059   8  12  NA   2 NA NA   NA
    ## 4060   9   9  NA   2 NA NA   NA
    ## 4061   0   0  NA   0 NA NA   NA
    ## 4062   9  24  NA   2 NA NA   NA
    ## 4063  10  12  NA   2 NA NA   NA
    ## 4064   7  21  NA   3 NA NA   NA
    ## 4065  64  73  NA   6 NA NA   NA
    ## 4066   1   3  NA   0 NA NA   NA
    ## 4067  18  34  NA   3 NA NA   NA
    ## 4068   0   3  NA   0 NA NA   NA
    ## 4069   2   3  NA   0 NA NA   NA
    ## 4070  20  47  NA   8 NA NA   NA
    ## 4071  25  22  NA   9 NA NA   NA
    ## 4072   4   9  NA   0 NA NA   NA
    ## 4073   4   8  NA   0 NA NA   NA
    ## 4074  13  28  NA   1 NA NA   NA
    ## 4075  20  22  NA   0 NA NA   NA
    ## 4076  22  39  NA   0 NA NA   NA
    ## 4077  11   7  NA   1 NA NA   NA
    ## 4078   1   1  NA   0 NA NA   NA
    ## 4079  22  78  NA   5 NA NA   NA
    ## 4080  24  32  NA  11 NA NA   NA
    ## 4081   6  37  NA   1 NA NA   NA
    ## 4082  18  29  NA   1 NA NA   NA
    ## 4083   0   3  NA   0 NA NA   NA
    ## 4084   3  24  NA   0 NA NA   NA
    ## 4085   1  18  NA   1 NA NA   NA
    ## 4086   1   1  NA   1 NA NA   NA
    ## 4087  62  69  NA   3 NA NA   NA
    ## 4088  12  49  NA   7 NA NA   NA
    ## 4089  50  31  NA   6 NA NA   NA
    ## 4090  15  32  NA   1 NA NA   NA
    ## 4091   3  25  NA   0 NA NA   NA
    ## 4092   9  34  NA   0 NA NA   NA
    ## 4093  12  36  NA   2 NA NA   NA
    ## 4094   5  14  NA   0 NA NA   NA
    ## 4095   7   3  NA   2 NA NA   NA
    ## 4096   0   4  NA   0 NA NA   NA
    ## 4097   8   7  NA   2 NA NA   NA
    ## 4098  61  75  NA   7 NA NA   NA
    ## 4099   1  15  NA   1 NA NA   NA
    ## 4100   5   8  NA   0 NA NA   NA
    ## 4101  23  10  NA   3 NA NA   NA
    ## 4102  42  42  NA   7 NA NA   NA
    ## 4103   1  22  NA   0 NA NA   NA
    ## 4104   7  22  NA   0 NA NA   NA
    ## 4105   1   9  NA   0 NA NA   NA
    ## 4106   4  13  NA   1 NA NA   NA
    ## 4107   4   9  NA   0 NA NA   NA
    ## 4108  16  52  NA  18 NA NA   NA
    ## 4109  28  45  NA   3 NA NA   NA
    ## 4110   0   0  NA   0 NA NA   NA
    ## 4111  22  34  NA   0 NA NA   NA
    ## 4112   1   6  NA   1 NA NA   NA
    ## 4113   4  26  NA   1 NA NA   NA
    ## 4114  11  46  NA   0 NA NA   NA
    ## 4115   0   1  NA   0 NA NA   NA
    ## 4116   0   3  NA   0 NA NA   NA
    ## 4117   9  13  NA   1 NA NA   NA
    ## 4118   3   6  NA   1 NA NA   NA
    ## 4119  33  37  NA  29 NA NA   NA
    ## 4120   1  33  NA   1 NA NA   NA
    ## 4121   0   5  NA   0 NA NA   NA
    ## 4122   1   4  NA   0 NA NA   NA
    ## 4123  30  49  NA   3 NA NA   NA
    ## 4124   1  45  NA   0 NA NA   NA
    ## 4125   1  11  NA   0 NA NA   NA
    ## 4126   0   0  NA   0 NA NA   NA
    ## 4127   7  23  NA   3 NA NA   NA
    ## 4128  21  38  NA   2 NA NA   NA
    ## 4129  21  24  NA   9 NA NA   NA
    ## 4130   8  22  NA   1 NA NA   NA
    ## 4131   7  20  NA   0 NA NA   NA
    ## 4132   0   8  NA   0 NA NA   NA
    ## 4133   2   1  NA   0 NA NA   NA
    ## 4134  65  71  NA   6 NA NA   NA
    ## 4135  23  55  NA   2 NA NA   NA
    ## 4136   0   0  NA   0 NA NA   NA
    ## 4137  34  66  NA   6 NA NA   NA
    ## 4138  25  30  NA   2 NA NA   NA
    ## 4139  39  44  NA   7 NA NA   NA
    ## 4140   1   0  NA   0 NA NA   NA
    ## 4141  18  39  NA   4 NA NA   NA
    ## 4142   1   0  NA   0 NA NA   NA
    ## 4143  10  35  NA   0 NA NA   NA
    ## 4144   0   2  NA   0 NA NA   NA
    ## 4145   0   0  NA   0 NA NA   NA
    ## 4146   2   4  NA   0 NA NA   NA
    ## 4147   5  10  NA   1 NA NA   NA
    ## 4148  86  19  NA   5 NA NA   NA
    ## 4149  17  40  NA   0 NA NA   NA
    ## 4150   5  32  NA   3 NA NA   NA
    ## 4151  16  63  NA   0 NA NA   NA
    ## 4152   0   0  NA   0 NA NA   NA
    ## 4153  15  20  NA   0 NA NA   NA
    ## 4154  37  38  NA   3 NA NA   NA
    ## 4155  25  46  NA   0 NA NA   NA
    ## 4156   0   2  NA   0 NA NA   NA
    ## 4157   4   8  NA   0 NA NA   NA
    ## 4158   0   2  NA   0 NA NA   NA
    ## 4159  35  39  NA   1 NA NA   NA
    ## 4160  14  33  NA   0 NA NA   NA
    ## 4161  29  29  NA   6 NA NA   NA
    ## 4162   5   4  NA   1 NA NA   NA
    ## 4163   2   2  NA   0 NA NA   NA
    ## 4164   1   0  NA   0 NA NA   NA
    ## 4165  21  43  NA   2 NA NA   NA
    ## 4166  29  30  NA   4 NA NA   NA
    ## 4167   1   1  NA   0 NA NA   NA
    ## 4168   1   1  NA   0 NA NA   NA
    ## 4169   4  14  NA   3 NA NA   NA
    ## 4170   9  23  NA   1 NA NA   NA
    ## 4171  21  42  NA   7 NA NA   NA
    ## 4172  10  15  NA   0 NA NA   NA
    ## 4173  66   6  NA  14 NA NA   NA
    ## 4174  34  30  NA   0 NA NA   NA
    ## 4175  59  56  NA   1 NA NA   NA
    ## 4176   9   9  NA   3 NA NA   NA
    ## 4177  15  32  NA   1 NA NA   NA
    ## 4178   9   5  NA   1 NA NA   NA
    ## 4179   4   1  NA   0 NA NA   NA
    ## 4180  20  68  NA   7 NA NA   NA
    ## 4181  68  26  NA   4 NA NA   NA
    ## 4182  32  57  NA   2 NA NA   NA
    ## 4183   9   7  NA   0 NA NA   NA
    ## 4184   4  14  NA   0 NA NA   NA
    ## 4185  16  22  NA   0 NA NA   NA
    ## 4186  14  14  NA   1 NA NA   NA
    ## 4187  18  41  NA   4 NA NA   NA
    ## 4188  85  26  NA  11 NA NA   NA
    ## 4189  44  17  NA   2 NA NA   NA
    ## 4190   0  12  NA   0 NA NA   NA
    ## 4191  12  32  NA   2 NA NA   NA
    ## 4192  26   7  NA   1 NA NA   NA
    ## 4193   0   1  NA   0 NA NA   NA
    ## 4194  11  59  NA   0 NA NA   NA
    ## 4195   6  18  NA   0 NA NA   NA
    ## 4196  29  21  NA   1 NA NA   NA
    ## 4197   1   3  NA   0 NA NA   NA
    ## 4198   1   0  NA   0 NA NA   NA
    ## 4199  80  41  NA   7 NA NA   NA
    ## 4200  19  19  NA   3 NA NA   NA
    ## 4201  93  46  NA   2 NA NA   NA
    ## 4202   0   0  NA   0 NA NA   NA
    ## 4203   2  26  NA   2 NA NA   NA
    ## 4204   1   3  NA   0 NA NA   NA
    ## 4205  15  48  NA   9 NA NA   NA
    ## 4206  42  24  NA   3 NA NA   NA
    ## 4207  13  21  NA   0 NA NA   NA
    ## 4208  10   4  NA   1 NA NA   NA
    ## 4209  14   9  NA   0 NA NA   NA
    ## 4210   4  25  NA   2 NA NA   NA
    ## 4211  28  21  NA   4 NA NA   NA
    ## 4212  38  65  NA   1 NA NA   NA
    ## 4213   1   8  NA   0 NA NA   NA
    ## 4214  38  28  NA   1 NA NA   NA
    ## 4215  25  22  NA   0 NA NA   NA
    ## 4216  17  35  NA   2 NA NA   NA
    ## 4217   1   1  NA   0 NA NA   NA
    ## 4218   0   3  NA   0 NA NA   NA
    ## 4219   2   5  NA   0 NA NA   NA
    ## 4220  14  17  NA   1 NA NA   NA
    ## 4221  27  63  NA   0 NA NA   NA
    ## 4222   1   4  NA   0 NA NA   NA
    ## 4223  21  20  NA   0 NA NA   NA
    ## 4224   2   0  NA   0 NA NA   NA
    ## 4225   2  10  NA   2 NA NA   NA
    ## 4226   6   6  NA   0 NA NA   NA
    ## 4227  60  81  NA   3 NA NA   NA
    ## 4228  46  30  NA   2 NA NA   NA
    ## 4229  46  33  NA   2 NA NA   NA
    ## 4230   0   2  NA   0 NA NA   NA
    ## 4231  11  30  NA   3 NA NA   NA
    ## 4232   4   8  NA   0 NA NA   NA
    ## 4233  30  24  NA   3 NA NA   NA
    ## 4234  41  57  NA   2 NA NA   NA
    ## 4235   0   2  NA   1 NA NA   NA
    ## 4236   3   8  NA   1 NA NA   NA
    ## 4237   4  23  NA   0 NA NA   NA
    ## 4238   5   2  NA   1 NA NA   NA
    ## 4239  37  32  NA   0 NA NA   NA
    ## 4240   9  30  NA   2 NA NA   NA
    ## 4241  17  28  NA  10 NA NA   NA
    ## 4242   0   0  NA   0 NA NA   NA
    ## 4243  52  36  NA   6 NA NA   NA
    ## 4244  41  21  NA   1 NA NA   NA
    ## 4245  15  15  NA   2 NA NA   NA
    ## 4246   0   1  NA   0 NA NA   NA
    ## 4247  65  78  NA   3 NA NA   NA
    ## 4248  10  47  NA   0 NA NA   NA
    ## 4249  29  30  NA   1 NA NA   NA
    ## 4250   0   0  NA   0 NA NA   NA
    ## 4251   7  11  NA   0 NA NA   NA
    ## 4252   3  18  NA   0 NA NA   NA
    ## 4253  65  60  NA   7 NA NA   NA
    ## 4254  12  35  NA   1 NA NA   NA
    ## 4255   3   1  NA   0 NA NA   NA
    ## 4256  64  23  NA   3 NA NA   NA
    ## 4257  52  56  NA   5 NA NA   NA
    ## 4258   6  12  NA   1 NA NA   NA
    ## 4259   6  17  NA   1 NA NA   NA
    ## 4260   3  46  NA   0 NA NA   NA
    ## 4261  15  11  NA   2 NA NA   NA
    ## 4262   0   4  NA   0 NA NA   NA
    ## 4263   3  24  NA   1 NA NA   NA
    ## 4264   0   1  NA   0 NA NA   NA
    ## 4265   0   3  NA   0 NA NA   NA
    ## 4266   1   1  NA   0 NA NA   NA
    ## 4267   2   1  NA   0 NA NA   NA
    ## 4268  15  38  NA   2 NA NA   NA
    ## 4269   7  20  NA   3 NA NA   NA
    ## 4270   1   2  NA   0 NA NA   NA
    ## 4271  31  10  NA   5 NA NA   NA
    ## 4272   4   1  NA   1 NA NA   NA
    ## 4273   8  12  NA   0 NA NA   NA
    ## 4274   0   4  NA   0 NA NA   NA
    ## 4275  84  28  NA   8 NA NA   NA
    ## 4276   0   0  NA   0 NA NA   NA
    ## 4277  58  71  NA   5 NA NA   NA
    ## 4278  91  29  NA   3 NA NA   NA
    ## 4279  14  18  NA   1 NA NA   NA
    ## 4280  11  36  NA   1 NA NA   NA
    ## 4281   0   4  NA   0 NA NA   NA
    ## 4282   3  17  NA   2 NA NA   NA
    ## 4283  19  27  NA   0 NA NA   NA
    ## 4284  36  54  NA   4 NA NA   NA
    ## 4285  87  41  NA  14 NA NA   NA
    ## 4286  58  25  NA   2 NA NA   NA
    ## 4287   9  15  NA   2 NA NA   NA
    ## 4288   0  10  NA   1 NA NA   NA
    ## 4289   0   6  NA   0 NA NA   NA
    ## 4290  18  27  NA   6 NA NA   NA
    ## 4291  49  22  NA   5 NA NA   NA
    ## 4292   9  28  NA   2 NA NA   NA
    ## 4293  43  59  NA   2 NA NA   NA
    ## 4294  29  38  NA   2 NA NA   NA
    ## 4295  22  72  NA   7 NA NA   NA
    ## 4296  75  30  NA   6 NA NA   NA
    ## 4297   2  11  NA   0 NA NA   NA
    ## 4298   4  15  NA   0 NA NA   NA
    ## 4299   0   0  NA   0 NA NA   NA
    ## 4300   7  40  NA   0 NA NA   NA
    ## 4301   6   6  NA   0 NA NA   NA
    ## 4302  42  37  NA   1 NA NA   NA
    ## 4303  25  14  NA   4 NA NA   NA
    ## 4304  41  60  NA   2 NA NA   NA
    ## 4305  39  47  NA  12 NA NA   NA
    ## 4306   0   0  NA   0 NA NA   NA
    ## 4307  21  28  NA   1 NA NA   NA
    ## 4308   8  29  NA   0 NA NA   NA
    ## 4309   8  40  NA   0 NA NA   NA
    ## 4310  48  35  NA   6 NA NA   NA
    ## 4311  65  40  NA   2 NA NA   NA
    ## 4312   3   3  NA   0 NA NA   NA
    ## 4313   0   1  NA   0 NA NA   NA
    ## 4314   2   4  NA   1 NA NA   NA
    ## 4315  23  26  NA   2 NA NA   NA
    ## 4316  22  40  NA   1 NA NA   NA
    ## 4317   1   1  NA   0 NA NA   NA
    ## 4318   0   6  NA   0 NA NA   NA
    ## 4319   2   1  NA   0 NA NA   NA
    ## 4320   0   2  NA   0 NA NA   NA
    ## 4321   0   2  NA   0 NA NA   NA
    ## 4322   9  36  NA   0 NA NA   NA
    ## 4323   0   3  NA   0 NA NA   NA
    ## 4324  83  41  NA  16 NA NA   NA
    ## 4325  42  30  NA  11 NA NA   NA
    ## 4326   0   5  NA   0 NA NA   NA
    ## 4327  64  63  NA  10 NA NA   NA
    ## 4328   2  24  NA   1 NA NA   NA
    ## 4329  79  44  NA   7 NA NA   NA
    ## 4330   2   0  NA   0 NA NA   NA
    ## 4331  15  12  NA   8 NA NA   NA
    ## 4332  60  69  NA   8 NA NA   NA
    ## 4333   3   7  NA   0 NA NA   NA
    ## 4334  54  61  NA  13 NA NA   NA
    ## 4335  87  32  NA   6 NA NA   NA
    ## 4336   9   7  NA   2 NA NA   NA
    ## 4337   3  16  NA   0 NA NA   NA
    ## 4338  29  41  NA   3 NA NA   NA
    ## 4339  11  10  NA   0 NA NA   NA
    ## 4340  30  49  NA   4 NA NA   NA
    ## 4341   1   0  NA   0 NA NA   NA
    ## 4342   1   9  NA   1 NA NA   NA
    ## 4343  46  26  NA   6 NA NA   NA
    ## 4344   2   1  NA   0 NA NA   NA
    ## 4345   2   3  NA   0 NA NA   NA
    ## 4346   6  11  NA   1 NA NA   NA
    ## 4347   1   1  NA   0 NA NA   NA
    ## 4348   9  39  NA   2 NA NA   NA
    ## 4349  42  25  NA   4 NA NA   NA
    ## 4350   4  16  NA   0 NA NA   NA
    ## 4351  60  29  NA   4 NA NA   NA
    ## 4352 116  66  NA   1 NA NA   NA
    ## 4353   0   0  NA   0 NA NA   NA
    ## 4354  31  11  NA   2 NA NA   NA
    ## 4355   2  11  NA   1 NA NA   NA
    ## 4356  16  19  NA   3 NA NA   NA
    ## 4357   4  17  NA   0 NA NA   NA
    ## 4358  30  23  NA   1 NA NA   NA
    ## 4359  27  21  NA   2 NA NA   NA
    ## 4360  23  25  NA   1 NA NA   NA
    ## 4361   2   0  NA   0 NA NA   NA
    ## 4362  22   7  NA   1 NA NA   NA
    ## 4363  36   9  NA   4 NA NA   NA
    ## 4364  17  13  NA   4 NA NA   NA
    ## 4365  79  44  NA   2 NA NA   NA
    ## 4366  54  35  NA   5 NA NA   NA
    ## 4367   1   1  NA   0 NA NA   NA
    ## 4368  61  76  NA  16 NA NA   NA
    ## 4369  12  18  NA   1 NA NA   NA
    ## 4370  33  37  NA   4 NA NA   NA
    ## 4371   3   7  NA   0 NA NA   NA
    ## 4372   4  10  NA   1 NA NA   NA
    ## 4373  72  37  NA   5 NA NA   NA
    ## 4374  40  34  NA   1 NA NA   NA
    ## 4375   9  38  NA   2 NA NA   NA
    ## 4376   0   3  NA   0 NA NA   NA
    ## 4377   6   8  NA   0 NA NA   NA
    ## 4378   0   2  NA   0 NA NA   NA
    ## 4379  53  51  NA   3 NA NA   NA
    ## 4380  11  21  NA   2 NA NA   NA
    ## 4381  59  43  NA   7 NA NA   NA
    ## 4382   1   3  NA   0 NA NA   NA
    ## 4383  50  27  NA   5 NA NA   NA
    ## 4384  25  21  NA   5 NA NA   NA
    ## 4385  19  22  NA   1 NA NA   NA
    ## 4386   9  19  NA   2 NA NA   NA
    ## 4387  91  37  NA   6 NA NA   NA
    ## 4388   1   8  NA   1 NA NA   NA
    ## 4389   1   3  NA   0 NA NA   NA
    ## 4390   4   0  NA   0 NA NA   NA
    ## 4391   7   6  NA   3 NA NA   NA
    ## 4392  19  45  NA   3 NA NA   NA
    ## 4393   2   2  NA   1 NA NA   NA
    ## 4394  34  37  NA  18 NA NA   NA
    ## 4395   0   1  NA   0 NA NA   NA
    ## 4396   1   6  NA   0 NA NA   NA
    ## 4397  46  37  NA   1 NA NA   NA
    ## 4398  48  44  NA   5 NA NA   NA
    ## 4399   2   8  NA   0 NA NA   NA
    ## 4400   0   1  NA   0 NA NA   NA
    ## 4401   6  34  NA   1 NA NA   NA
    ## 4402 118  55  NA   6 NA NA   NA
    ## 4403  22  16  NA   3 NA NA   NA
    ## 4404   2  19  NA   1 NA NA   NA
    ## 4405   3  17  NA   0 NA NA   NA
    ## 4406  70  62  NA   6 NA NA   NA
    ## 4407   6  11  NA   1 NA NA   NA
    ## 4408   0   0  NA   0 NA NA   NA
    ## 4409   3   3  NA   2 NA NA   NA
    ## 4410  16   8  NA   2 NA NA   NA
    ## 4411  67  59  NA  10 NA NA   NA
    ## 4412  22  19  NA   3 NA NA   NA
    ## 4413  42  52  NA   0 NA NA   NA
    ## 4414  42  37  NA   7 NA NA   NA
    ## 4415  20   5  NA   6 NA NA   NA
    ## 4416   1   1  NA   0 NA NA   NA
    ## 4417   4   3  NA   0 NA NA   NA
    ## 4418   7  18  NA   2 NA NA   NA
    ## 4419  40  42  NA   1 NA NA   NA
    ## 4420   0   1  NA   0 NA NA   NA
    ## 4421   3   3  NA   0 NA NA   NA
    ## 4422  24  38  NA   6 NA NA   NA
    ## 4423  23  30  NA   4 NA NA   NA
    ## 4424   2  12  NA   1 NA NA   NA
    ## 4425  42  49  NA   1 NA NA   NA
    ## 4426   2   8  NA   1 NA NA   NA
    ## 4427   1  16  NA   1 NA NA   NA
    ## 4428   1   2  NA   0 NA NA   NA
    ## 4429   3  10  NA   0 NA NA   NA
    ## 4430   4  20  NA   2 NA NA   NA
    ## 4431   1   0  NA   0 NA NA   NA
    ## 4432   0   1  NA   0 NA NA   NA
    ## 4433   4  40  NA   0 NA NA   NA
    ## 4434  56  69  NA   0 NA NA   NA
    ## 4435   3  13  NA   1 NA NA   NA
    ## 4436  77  68  NA   1 NA NA   NA
    ## 4437  13  36  NA   2 NA NA   NA
    ## 4438  58  18  NA   2 NA NA   NA
    ## 4439  50  31  NA   1 NA NA   NA
    ## 4440   1   2  NA   1 NA NA   NA
    ## 4441   5   8  NA   2 NA NA   NA
    ## 4442  27  33  NA   4 NA NA   NA
    ## 4443  14   6  NA   0 NA NA   NA
    ## 4444  18  33  NA   6 NA NA   NA
    ## 4445  11  26  NA   4 NA NA   NA
    ## 4446   1   5  NA   2 NA NA   NA
    ## 4447  13  37  NA   5 NA NA   NA
    ## 4448  69  62  NA   6 NA NA   NA
    ## 4449  37  41  NA   2 NA NA   NA
    ## 4450   7  22  NA   0 NA NA   NA
    ## 4451  14  14  NA   0 NA NA   NA
    ## 4452  36  22  NA   6 NA NA   NA
    ## 4453   0   1  NA   0 NA NA   NA
    ## 4454  96  32  NA   5 NA NA   NA
    ## 4455   0   2  NA   0 NA NA   NA
    ## 4456  46  47  NA   3 NA NA   NA
    ## 4457   0   0  NA   0 NA NA   NA
    ## 4458  42  26  NA  33 NA NA   NA
    ## 4459  29  37  NA   3 NA NA   NA
    ## 4460  82  41  NA   5 NA NA   NA
    ## 4461   7  41  NA   0 NA NA   NA
    ## 4462  11  47  NA   1 NA NA   NA
    ## 4463  36  36  NA   4 NA NA   NA
    ## 4464  27   7  NA   2 NA NA   NA
    ## 4465   0   7  NA   0 NA NA   NA
    ## 4466  40  22  NA   7 NA NA   NA
    ## 4467   0   0  NA   0 NA NA   NA
    ## 4468  67  30  NA  19 NA NA   NA
    ## 4469   5  27  NA   0 NA NA   NA
    ## 4470   9  59  NA   1 NA NA   NA
    ## 4471   0   0  NA   0 NA NA   NA
    ## 4472   0   2  NA   0 NA NA   NA
    ## 4473  16  18  NA   4 NA NA   NA
    ## 4474  56  39  NA   2 NA NA   NA
    ## 4475   5   6  NA   1 NA NA   NA
    ## 4476   2  31  NA   1 NA NA   NA
    ## 4477  23  22  NA   4 NA NA   NA
    ## 4478  51  32  NA   2 NA NA   NA
    ## 4479  61  62  NA   4 NA NA   NA
    ## 4480  29  34  NA   5 NA NA   NA
    ## 4481  53  33  NA   1 NA NA   NA
    ## 4482   0   2  NA   0 NA NA   NA
    ## 4483   0   1  NA   0 NA NA   NA
    ## 4484  44  35  NA   1 NA NA   NA
    ## 4485   0  NA  NA   0 NA NA   NA
    ## 4486   0  NA  NA   0 NA NA   NA
    ## 4487  87  54  NA   5 NA NA   NA
    ## 4488  22  NA  NA   0 NA NA   NA
    ## 4489   0   3  NA   0 NA NA   NA
    ## 4490   1  10  NA   2 NA NA   NA
    ## 4491  40  32  NA   1 NA NA   NA
    ## 4492  23  41  NA   2 NA NA   NA
    ## 4493 113  23  NA   6 NA NA   NA
    ## 4494  17  40  NA   2 NA NA   NA
    ## 4495  11  28  NA   1 NA NA   NA
    ## 4496  10   6  NA   2 NA NA   NA
    ## 4497   0  NA  NA   1 NA NA   NA
    ## 4498   3   6  NA   0 NA NA   NA
    ## 4499   4  NA  NA   1 NA NA   NA
    ## 4500   1   1  NA   0 NA NA   NA
    ## 4501   2   1  NA   0 NA NA   NA
    ## 4502  15  50  NA   0 NA NA   NA
    ## 4503  13  NA  NA   4 NA NA   NA
    ## 4504  11  12  NA   1 NA NA   NA
    ## 4505  29  25  NA   7 NA NA   NA
    ## 4506  33  37  NA   5 NA NA   NA
    ## 4507   8  NA  NA   0 NA NA   NA
    ## 4508  44  13  NA   2 NA NA   NA
    ## 4509  12  43  NA   0 NA NA   NA
    ## 4510  42  33  NA   6 NA NA   NA
    ## 4511  29  23  NA   7 NA NA   NA
    ## 4512  72  56  NA   2 NA NA   NA
    ## 4513  35  23  NA   7 NA NA   NA
    ## 4514  40  15  NA   0 NA NA   NA
    ## 4515   0  NA  NA   0 NA NA   NA
    ## 4516   2  NA  NA   0 NA NA   NA
    ## 4517   9  NA  NA   0 NA NA   NA
    ## 4518   7  NA  NA   1 NA NA   NA
    ## 4519   0   0  NA   0 NA NA   NA
    ## 4520   4   5  NA   0 NA NA   NA
    ## 4521  44  29  NA   5 NA NA   NA
    ## 4522  13  29  NA   4 NA NA   NA
    ## 4523  16  NA  NA   1 NA NA   NA
    ## 4524  66  20  NA  11 NA NA   NA
    ## 4525  99  17  NA  18 NA NA   NA
    ## 4526  75  36  NA   3 NA NA   NA
    ## 4527  87  87  NA   3 NA NA   NA
    ## 4528  13  13  NA   1 NA NA   NA
    ## 4529  23  35  NA   4 NA NA   NA
    ## 4530   2  10  NA   0 NA NA   NA
    ## 4531   0   3  NA   0 NA NA   NA
    ## 4532   9   3  NA   1 NA NA   NA
    ## 4533  17  NA  NA   1 NA NA   NA
    ## 4534   5  NA  NA   1 NA NA   NA
    ## 4535  49  40  NA   8 NA NA   NA
    ## 4536  14   9  NA   1 NA NA   NA
    ## 4537  33  52  NA   3 NA NA   NA
    ## 4538   1  NA  NA   1 NA NA   NA
    ## 4539  51  42  NA   4 NA NA   NA
    ## 4540  57  45  NA   2 NA NA   NA
    ## 4541   6   4  NA   0 NA NA   NA
    ## 4542   8  NA  NA   1 NA NA   NA
    ## 4543  26  NA  NA   0 NA NA   NA
    ## 4544   1  NA  NA   0 NA NA   NA
    ## 4545   0  NA  NA   0 NA NA   NA
    ##  [ reached 'max' / getOption("max.print") -- omitted 102884 rows ]

``` r
batting <- Batting

batters <- batting %>%
  group_by(playerID) %>%
  summarize(
    ba = sum(H, na.rm = TRUE) / sum(AB, na.rm = TRUE), #batting average
    ab = sum(AB, na.rm = TRUE) #at bats
  )
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
batters %>%
  filter(ab > 100) %>%
  ggplot(mapping = aes(x = ab, y = ba)) + 
    geom_point() +
    geom_smooth(se = FALSE) #turn off the standard error band
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

![](Data-Wrangling-_files/figure-gfm/example_31-1.png)<!-- -->

When I plot the skill of the batter (measured by the batting average,
ba) against the number of opportunities to hit the ball (measured by at
bat, ab), you see two patterns:

1.  As above, the variation in our aggregate decreases as we get more
    data points.

2.  There’s a positive correlation between skill (ba) and opportunities
    to hit the ball (ab). This is because teams control who gets to
    play, and obviously they’ll pick their best players.

This also has important implications for ranking. If you naively sort on
desc(ba), the people with the best batting averages are clearly lucky,
not skilled:

``` r
batters %>%
  arrange(desc(ba))
```

    ## # A tibble: 19,689 x 3
    ##    playerID     ba    ab
    ##    <chr>     <dbl> <int>
    ##  1 abramge01     1     1
    ##  2 alanirj01     1     1
    ##  3 alberan01     1     1
    ##  4 banisje01     1     1
    ##  5 bartocl01     1     1
    ##  6 bassdo01      1     1
    ##  7 birasst01     1     2
    ##  8 bruneju01     1     1
    ##  9 burnscb01     1     1
    ## 10 cammaer01     1     1
    ## # … with 19,679 more rows

##### 5.6.4 Useful summary functions

Just using means, counts, and sum can get you a long way, but R provides
many other useful summary functions:

Measures of location: we’ve used mean(x), but median(x) is also useful.
The mean is the sum divided by the length; the median is a value where
50% of x is above it, and 50% is below it.

``` r
not_cancelled %>%
  group_by(year, month, day) %>%
  summarize(median = median(arr_delay))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day median
    ##    <int> <int> <int>  <dbl>
    ##  1  2013     1     1      3
    ##  2  2013     1     2      4
    ##  3  2013     1     3      1
    ##  4  2013     1     4     -8
    ##  5  2013     1     5     -7
    ##  6  2013     1     6     -1
    ##  7  2013     1     7    -10
    ##  8  2013     1     8     -7
    ##  9  2013     1     9     -6
    ## 10  2013     1    10    -11
    ## # … with 355 more rows

It’s sometimes useful to combine aggregation with logical subsetting. We
haven’t talked about this sort of subsetting yet, but you’ll learn more
about it in subsetting.

``` r
not_cancelled %>%
  group_by(year, month, day) %>%
  summarize(
    avg_delay1 = mean(arr_delay),
    avg_delay2 = mean(arr_delay[arr_delay > 0]), #the average positive delay
    avg_delay3 = mean(arr_delay[arr_delay < 0]) #the average negative delay
  )
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 6
    ## # Groups:   year, month [12]
    ##     year month   day avg_delay1 avg_delay2 avg_delay3
    ##    <int> <int> <int>      <dbl>      <dbl>      <dbl>
    ##  1  2013     1     1     12.7         32.5      -12.5
    ##  2  2013     1     2     12.7         32.0      -14.3
    ##  3  2013     1     3      5.73        27.7      -18.2
    ##  4  2013     1     4     -1.93        28.3      -17.0
    ##  5  2013     1     5     -1.53        22.6      -14.0
    ##  6  2013     1     6      4.24        24.4      -13.6
    ##  7  2013     1     7     -4.95        27.8      -17.0
    ##  8  2013     1     8     -3.23        20.8      -14.3
    ##  9  2013     1     9     -0.264       25.6      -13.0
    ## 10  2013     1    10     -5.90        27.3      -16.4
    ## # … with 355 more rows

Measures of spread: sd(x), IQR(x), mad(x). The root mean squared
deviation, or standard deviation sd(x), is the standard measure of
spread. The interquartile range IQR(x) and median absolute deviation
mad(x) are robust equivalents that may be more useful if you have
outliers.

``` r
not_cancelled %>%
  group_by(dest) %>%
  summarize(distance_sd = sd(distance)) %>%
  arrange(desc(distance_sd))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 104 x 2
    ##    dest  distance_sd
    ##    <chr>       <dbl>
    ##  1 EGE         10.5 
    ##  2 SAN         10.4 
    ##  3 SFO         10.2 
    ##  4 HNL         10.0 
    ##  5 SEA          9.98
    ##  6 LAS          9.91
    ##  7 PDX          9.87
    ##  8 PHX          9.86
    ##  9 LAX          9.66
    ## 10 IND          9.46
    ## # … with 94 more rows

Measures of rank: min(x), quantile(x, 0.25), max(x). Quantiles are a
generalisation of the median. For example, quantile(x, 0.25) will find a
value of x that is greater than 25% of the values, and less than the
remaining 75%.

``` r
not_cancelled %>%
  group_by(year, month, day) %>%
  summarize(
    first = min(dep_time),
    last = max(dep_time)
  )
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 5
    ## # Groups:   year, month [12]
    ##     year month   day first  last
    ##    <int> <int> <int> <int> <int>
    ##  1  2013     1     1   517  2356
    ##  2  2013     1     2    42  2354
    ##  3  2013     1     3    32  2349
    ##  4  2013     1     4    25  2358
    ##  5  2013     1     5    14  2357
    ##  6  2013     1     6    16  2355
    ##  7  2013     1     7    49  2359
    ##  8  2013     1     8   454  2351
    ##  9  2013     1     9     2  2252
    ## 10  2013     1    10     3  2320
    ## # … with 355 more rows

Measures of position: first(x), nth(x, 2), last(x). These work similarly
to x\[1\], x\[2\], and x\[length(x)\] but let you set a default value if
that position does not exist (i.e. you’re trying to get the 3rd element
from a group that only has two elements). For example, we can find the
first and last departure for each day:

``` r
not_cancelled %>%
  group_by(year, month, day) %>%
  summarize(
    first_dep = first(dep_time),
    last_dep = last(dep_time)
  )
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 5
    ## # Groups:   year, month [12]
    ##     year month   day first_dep last_dep
    ##    <int> <int> <int>     <int>    <int>
    ##  1  2013     1     1       517     2356
    ##  2  2013     1     2        42     2354
    ##  3  2013     1     3        32     2349
    ##  4  2013     1     4        25     2358
    ##  5  2013     1     5        14     2357
    ##  6  2013     1     6        16     2355
    ##  7  2013     1     7        49     2359
    ##  8  2013     1     8       454     2351
    ##  9  2013     1     9         2     2252
    ## 10  2013     1    10         3     2320
    ## # … with 355 more rows

Counts: You’ve seen n(), which takes no arguments, and returns the size
of the current group. To count the number of non-missing values, use
sum(\!is.na(x)). To count the number of distinct (unique) values, use
n\_distinct(x).

``` r
# Which destinations have the most carriers?
not_cancelled %>%
  group_by(dest) %>%
  summarize(carriers = n_distinct(carrier)) %>%
  arrange(desc(carriers))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 104 x 2
    ##    dest  carriers
    ##    <chr>    <int>
    ##  1 ATL          7
    ##  2 BOS          7
    ##  3 CLT          7
    ##  4 ORD          7
    ##  5 TPA          7
    ##  6 AUS          6
    ##  7 DCA          6
    ##  8 DTW          6
    ##  9 IAD          6
    ## 10 MSP          6
    ## # … with 94 more rows

Counts are so useful that dplyr provides a simple helper if all you want
is a count:

``` r
not_cancelled %>%
  count(dest)
```

    ## # A tibble: 104 x 2
    ##    dest      n
    ##    <chr> <int>
    ##  1 ABQ     254
    ##  2 ACK     264
    ##  3 ALB     418
    ##  4 ANC       8
    ##  5 ATL   16837
    ##  6 AUS    2411
    ##  7 AVL     261
    ##  8 BDL     412
    ##  9 BGR     358
    ## 10 BHM     269
    ## # … with 94 more rows

You can optionally provide a weight variable. For example, you could use
this to “count” (sum) the total number of miles a plane flew:

``` r
not_cancelled %>%
  count(tailnum, wt = distance) %>%
  arrange(desc(n))
```

    ## # A tibble: 4,037 x 2
    ##    tailnum      n
    ##    <chr>    <dbl>
    ##  1 N328AA  929090
    ##  2 N338AA  921172
    ##  3 N335AA  902271
    ##  4 N327AA  900482
    ##  5 N323AA  839468
    ##  6 N319AA  837924
    ##  7 N336AA  833136
    ##  8 N329AA  825826
    ##  9 N324AA  786159
    ## 10 N339AA  783648
    ## # … with 4,027 more rows

Counts and proportions of logical values: sum(x \> 10), mean(y == 0).
When used with numeric functions, TRUE is converted to 1 and FALSE to 0.
This makes sum() and mean() very useful: sum(x) gives the number of
TRUEs in x, and mean(x) gives the proportion.

``` r
# How many flights left before 5am? (these usually indicate delayed flights from the previous day)
not_cancelled %>% 
  group_by(year, month, day) %>% 
  summarise(n_early = sum(dep_time < 500))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day n_early
    ##    <int> <int> <int>   <int>
    ##  1  2013     1     1       0
    ##  2  2013     1     2       3
    ##  3  2013     1     3       4
    ##  4  2013     1     4       3
    ##  5  2013     1     5       3
    ##  6  2013     1     6       2
    ##  7  2013     1     7       2
    ##  8  2013     1     8       1
    ##  9  2013     1     9       3
    ## 10  2013     1    10       3
    ## # … with 355 more rows

``` r
# What proportion of flights are delayed by more than an hour?
not_cancelled %>% 
  group_by(year, month, day) %>% 
  summarise(hour_prop = mean(arr_delay > 60))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day hour_prop
    ##    <int> <int> <int>     <dbl>
    ##  1  2013     1     1    0.0722
    ##  2  2013     1     2    0.0851
    ##  3  2013     1     3    0.0567
    ##  4  2013     1     4    0.0396
    ##  5  2013     1     5    0.0349
    ##  6  2013     1     6    0.0470
    ##  7  2013     1     7    0.0333
    ##  8  2013     1     8    0.0213
    ##  9  2013     1     9    0.0202
    ## 10  2013     1    10    0.0183
    ## # … with 355 more rows

##### 5.6.5 Grouping by multiple variables

When you group by multiple variables, each summary peels off one level
of the grouping. That makes it easy to progressively roll up a dataset:

``` r
daily <- group_by(flights, year, month, day)
(per_day   <- summarise(daily, flights = n()))
```

    ## `summarise()` regrouping output by 'year', 'month' (override with `.groups` argument)

    ## # A tibble: 365 x 4
    ## # Groups:   year, month [12]
    ##     year month   day flights
    ##    <int> <int> <int>   <int>
    ##  1  2013     1     1     842
    ##  2  2013     1     2     943
    ##  3  2013     1     3     914
    ##  4  2013     1     4     915
    ##  5  2013     1     5     720
    ##  6  2013     1     6     832
    ##  7  2013     1     7     933
    ##  8  2013     1     8     899
    ##  9  2013     1     9     902
    ## 10  2013     1    10     932
    ## # … with 355 more rows

``` r
(per_month <- summarise(per_day, flights = sum(flights)))
```

    ## `summarise()` regrouping output by 'year' (override with `.groups` argument)

    ## # A tibble: 12 x 3
    ## # Groups:   year [1]
    ##     year month flights
    ##    <int> <int>   <int>
    ##  1  2013     1   27004
    ##  2  2013     2   24951
    ##  3  2013     3   28834
    ##  4  2013     4   28330
    ##  5  2013     5   28796
    ##  6  2013     6   28243
    ##  7  2013     7   29425
    ##  8  2013     8   29327
    ##  9  2013     9   27574
    ## 10  2013    10   28889
    ## 11  2013    11   27268
    ## 12  2013    12   28135

``` r
(per_year  <- summarise(per_month, flights = sum(flights)))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 1 x 2
    ##    year flights
    ##   <int>   <int>
    ## 1  2013  336776

Be careful when progressively rolling up summaries: it’s OK for sums and
counts, but you need to think about weighting means and variances, and
it’s not possible to do it exactly for rank-based statistics like the
median. In other words, the sum of groupwise sums is the overall sum,
but the median of groupwise medians is not the overall median.

##### 5.6.6 Ungrouping

If you need to remove grouping, and return to operations on ungrouped
data, use ungroup().

``` r
daily %>% 
  ungroup() %>%             # no longer grouped by date
  summarise(flights = n())  # all flights
```

    ## # A tibble: 1 x 1
    ##   flights
    ##     <int>
    ## 1  336776

\#\#3 5.7 Grouped mutates (and filters)

Grouping is most useful in conjunction with summarise(), but you can
also do convenient operations with mutate() and filter():

``` r
#Find the worst members of each group
flights_narrow %>% 
  group_by(year, month, day) %>%
  filter(rank(desc(arr_delay)) < 10)
```

    ## # A tibble: 3,306 x 7
    ## # Groups:   year, month, day [365]
    ##     year month   day dep_delay arr_delay distance air_time
    ##    <int> <int> <int>     <dbl>     <dbl>    <dbl>    <dbl>
    ##  1  2013     1     1       853       851      184       41
    ##  2  2013     1     1       290       338     1134      213
    ##  3  2013     1     1       260       263      266       46
    ##  4  2013     1     1       157       174      213       60
    ##  5  2013     1     1       216       222      708      121
    ##  6  2013     1     1       255       250      589      115
    ##  7  2013     1     1       285       246     1085      146
    ##  8  2013     1     1       192       191      199       44
    ##  9  2013     1     1       379       456     1092      222
    ## 10  2013     1     2       224       207      550       94
    ## # … with 3,296 more rows

``` r
#Find all groups bigger than a treshold
popular_dests <- flights %>% 
  group_by(dest) %>% 
  filter(n() > 365)
popular_dests
```

    ## # A tibble: 332,577 x 19
    ## # Groups:   dest [77]
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # … with 332,567 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

``` r
#Standardise to compute per group metrics:
popular_dests %>% 
  filter(arr_delay > 0) %>% 
  mutate(prop_delay = arr_delay / sum(arr_delay)) %>% 
  select(year:day, dest, arr_delay, prop_delay)
```

    ## # A tibble: 131,106 x 6
    ## # Groups:   dest [77]
    ##     year month   day dest  arr_delay prop_delay
    ##    <int> <int> <int> <chr>     <dbl>      <dbl>
    ##  1  2013     1     1 IAH          11  0.000111 
    ##  2  2013     1     1 IAH          20  0.000201 
    ##  3  2013     1     1 MIA          33  0.000235 
    ##  4  2013     1     1 ORD          12  0.0000424
    ##  5  2013     1     1 FLL          19  0.0000938
    ##  6  2013     1     1 ORD           8  0.0000283
    ##  7  2013     1     1 LAX           7  0.0000344
    ##  8  2013     1     1 DFW          31  0.000282 
    ##  9  2013     1     1 ATL          12  0.0000400
    ## 10  2013     1     1 DTW          16  0.000116 
    ## # … with 131,096 more rows
