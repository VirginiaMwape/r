---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 10-Data-Verbs---filter.md in _episodes_rmd/
title: Selecting rows
teaching: 15
exercises: 10
questions:
  - "How can I select rows from a data frame based on their values?"
objectives:
  - "Filter data frames using logical operators"
  - "Combine logical expressions in a filter"
keypoints:
  - "Use `filter()` to choose data based on values."
  - "The logical operator `%in%` can filter data from a list of possible values"
source: Rmd
---



If we are looking to subset the rows of our data (rather than the columns using `select()`) we can 
use `filter()`. This function takes a data frame as it's first argument, then a set of conditions to
check. Any row of the data frame that meets all the conditions is kept and any that fail are discarded.

For example, to get just the Australian data from the gapminder set:


~~~
filter(gapminder, country == "Australia")
~~~
{: .language-r}



~~~
# A tibble: 12 x 6
   country   continent  year lifeExp      pop gdpPercap
   <chr>     <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Australia Oceania    1952    69.1  8691212    10040.
 2 Australia Oceania    1957    70.3  9712569    10950.
 3 Australia Oceania    1962    70.9 10794968    12217.
 4 Australia Oceania    1967    71.1 11872264    14526.
 5 Australia Oceania    1972    71.9 13177000    16789.
 6 Australia Oceania    1977    73.5 14074100    18334.
 7 Australia Oceania    1982    74.7 15184200    19477.
 8 Australia Oceania    1987    76.3 16257249    21889.
 9 Australia Oceania    1992    77.6 17481977    23425.
10 Australia Oceania    1997    78.8 18565243    26998.
11 Australia Oceania    2002    80.4 19546792    30688.
12 Australia Oceania    2007    81.2 20434176    34435.
~~~
{: .output}

or to get only data from 1997 or later:


~~~
filter(gapminder, year >= 1997)
~~~
{: .language-r}



~~~
# A tibble: 426 x 6
   country     continent  year lifeExp      pop gdpPercap
   <chr>       <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Afghanistan Asia       1997    41.8 22227415      635.
 2 Afghanistan Asia       2002    42.1 25268405      727.
 3 Afghanistan Asia       2007    43.8 31889923      975.
 4 Albania     Europe     1997    73.0  3428038     3193.
 5 Albania     Europe     2002    75.7  3508512     4604.
 6 Albania     Europe     2007    76.4  3600523     5937.
 7 Algeria     Africa     1997    69.2 29072015     4797.
 8 Algeria     Africa     2002    71.0 31287142     5288.
 9 Algeria     Africa     2007    72.3 33333216     6223.
10 Angola      Africa     1997    41.0  9875024     2277.
# … with 416 more rows
~~~
{: .output}

## Filter operators
Any of the standard (comparison operators)({{ page.root }}{% link _episodes/02-Using-R.md %}#comparing-things)
can be used in a filter

  * `==` equal to
  * `!=` not equal to
  * `<`/`>` less/greater than
  * `<=`/`>=` less/greater than or equal to

If you provide multiple filter conditions (separated by a comma) then only rows matching **all** of
the conditions will be kept.

> ## Challenge 1
> How would you extract just the Australian data from 1997 or later?
> > ## Solution to Challenge 1
> > 
> > ~~~
> > filter(gapminder, country == "Australia", year >= 1997)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 3 x 6
> >   country   continent  year lifeExp      pop gdpPercap
> >   <chr>     <chr>     <dbl>   <dbl>    <dbl>     <dbl>
> > 1 Australia Oceania    1997    78.8 18565243    26998.
> > 2 Australia Oceania    2002    80.4 19546792    30688.
> > 3 Australia Oceania    2007    81.2 20434176    34435.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

If you need to keep all rows that meet one or the other condition, use the logical OR operator (`|`)


~~~
# Tries to find data from Australia AND New Zealand (and returns an empty table)
filter(gapminder, country == "Australia", country == "New Zealand")
~~~
{: .language-r}



~~~
# A tibble: 0 x 6
# … with 6 variables: country <chr>, continent <chr>, year <dbl>,
#   lifeExp <dbl>, pop <dbl>, gdpPercap <dbl>
~~~
{: .output}



~~~
# Use | to look for data from Australia OR New Zealand
filter(gapminder, country == "Australia" | country == "New Zealand")
~~~
{: .language-r}



~~~
# A tibble: 24 x 6
   country   continent  year lifeExp      pop gdpPercap
   <chr>     <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Australia Oceania    1952    69.1  8691212    10040.
 2 Australia Oceania    1957    70.3  9712569    10950.
 3 Australia Oceania    1962    70.9 10794968    12217.
 4 Australia Oceania    1967    71.1 11872264    14526.
 5 Australia Oceania    1972    71.9 13177000    16789.
 6 Australia Oceania    1977    73.5 14074100    18334.
 7 Australia Oceania    1982    74.7 15184200    19477.
 8 Australia Oceania    1987    76.3 16257249    21889.
 9 Australia Oceania    1992    77.6 17481977    23425.
10 Australia Oceania    1997    78.8 18565243    26998.
# … with 14 more rows
~~~
{: .output}

> ## Challenge 2
> Modify your answer to Challenge 1 so that you extract all data from Australia, or from 1997 and 
> later.
> > ## Solution to Challenge 2
> > 
> > ~~~
> > filter(gapminder, country == "Australia" | year >= 1997)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 435 x 6
> >    country     continent  year lifeExp      pop gdpPercap
> >    <chr>       <chr>     <dbl>   <dbl>    <dbl>     <dbl>
> >  1 Afghanistan Asia       1997    41.8 22227415      635.
> >  2 Afghanistan Asia       2002    42.1 25268405      727.
> >  3 Afghanistan Asia       2007    43.8 31889923      975.
> >  4 Albania     Europe     1997    73.0  3428038     3193.
> >  5 Albania     Europe     2002    75.7  3508512     4604.
> >  6 Albania     Europe     2007    76.4  3600523     5937.
> >  7 Algeria     Africa     1997    69.2 29072015     4797.
> >  8 Algeria     Africa     2002    71.0 31287142     5288.
> >  9 Algeria     Africa     2007    72.3 33333216     6223.
> > 10 Angola      Africa     1997    41.0  9875024     2277.
> > # … with 425 more rows
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

It might seem natural to write `country == "Australia" | "New Zealand"` but try it and you will see
that you get an error. Each side of the `|` operator must result in a `TRUE` or `FALSE`, and "New
Zealand" is neither.

When you have many possible matches from a row that you want to keep, writing a long expression with 
many `|` can be time consuming and error prone. Instead, the `%in%` operator can be used to simplify
things. `%in%` returns `TRUE` if the left hand side is found somewhere in the right hand side and
`FALSE` otherwise.


~~~
filter(gapminder, country %in% c("Australia", "New Zealand"))
~~~
{: .language-r}



~~~
# A tibble: 24 x 6
   country   continent  year lifeExp      pop gdpPercap
   <chr>     <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Australia Oceania    1952    69.1  8691212    10040.
 2 Australia Oceania    1957    70.3  9712569    10950.
 3 Australia Oceania    1962    70.9 10794968    12217.
 4 Australia Oceania    1967    71.1 11872264    14526.
 5 Australia Oceania    1972    71.9 13177000    16789.
 6 Australia Oceania    1977    73.5 14074100    18334.
 7 Australia Oceania    1982    74.7 15184200    19477.
 8 Australia Oceania    1987    76.3 16257249    21889.
 9 Australia Oceania    1992    77.6 17481977    23425.
10 Australia Oceania    1997    78.8 18565243    26998.
# … with 14 more rows
~~~
{: .output}

> ## Challenge 3
> Extract the rows from all countries in Africa, Asia, or Europe. How many rows does your dataframe 
> have and why?
> > ## Solution to Challenge 3
> > 
> > ~~~
> > filter(gapminder, continent %in% c("Africa","Asia", "Europe"))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 1,380 x 6
> >    country     continent  year lifeExp      pop gdpPercap
> >    <chr>       <chr>     <dbl>   <dbl>    <dbl>     <dbl>
> >  1 Afghanistan Asia       1952    28.8  8425333      779.
> >  2 Afghanistan Asia       1957    30.3  9240934      821.
> >  3 Afghanistan Asia       1962    32.0 10267083      853.
> >  4 Afghanistan Asia       1967    34.0 11537966      836.
> >  5 Afghanistan Asia       1972    36.1 13079460      740.
> >  6 Afghanistan Asia       1977    38.4 14880372      786.
> >  7 Afghanistan Asia       1982    39.9 12881816      978.
> >  8 Afghanistan Asia       1987    40.8 13867957      852.
> >  9 Afghanistan Asia       1992    41.7 16317921      649.
> > 10 Afghanistan Asia       1997    41.8 22227415      635.
> > # … with 1,370 more rows
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

