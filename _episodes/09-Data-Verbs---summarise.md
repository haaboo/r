---
# Please do not edit this file directly; it is auto generated.
# Instead, please edit 09-Data-Verbs---summarise.md in _episodes_rmd/
title: Summarise and Grouping
teaching: 20
exercises: 20
questions:
  - "How can I make summaries of groups of data?"
  - "How can I count the elements of groups in a dataset?"
objectives:
  - "Identify when grouping is necessary to make summaries"
  - "Be able to to usefully summarise variables in a dataframe"
keypoints:
  - "`summarise()` creates a new variable that provides a one row summary per group"
  - "`n()` is useful to count rows per group"
source: Rmd
---



The `summarise()` function lets us create new variables by collapsing a data frame into a single 
summary statistic. You can use `summarise()` with any function that takes a vector as input and 
returns a single value as output. For example, what is the average life expectance in the gapminder 
data?


~~~
summarise(gapminder, mean_life_exp = mean(lifeExp))
~~~
{: .language-r}



~~~
# A tibble: 1 x 1
  mean_life_exp
          <dbl>
1          59.5
~~~
{: .output}

On it's own, this may not seem that exciting. You could just as easily get the same result by using
`mean(gapminder$lifeExp)`. Where is becomes more useful however, is that you can use multiple 
summary functions at the same time.


~~~
summarise(
    gapminder,
    mean_life_exp = mean(lifeExp),
    sd_life_exp = sd(lifeExp),
    mean_gdp_per_cap = mean(gdpPercap),
    max_gdp_per_cap = max(gdpPercap)
)
~~~
{: .language-r}



~~~
# A tibble: 1 x 4
  mean_life_exp sd_life_exp mean_gdp_per_cap max_gdp_per_cap
          <dbl>       <dbl>            <dbl>           <dbl>
1          59.5        12.9            7215.         113523.
~~~
{: .output}

> ## Challenge 1
> Calculate the mean and median population for the gapminder data
> > ## Solution to Challenge 1
> > 
> > ~~~
> > summarise(gapminder, mean_pop = mean(pop), median_pop = median(pop))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 1 x 2
> >    mean_pop median_pop
> >       <dbl>      <dbl>
> > 1 29601212.   7023596.
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

and you can get summaries for different groups in conjunction with `group_by()`


~~~
gapminder_by_country <- group_by(gapminder, country)

summarise(gapminder_by_country, mean_life_exp = mean(lifeExp))
~~~
{: .language-r}



~~~
# A tibble: 142 x 2
   country     mean_life_exp
   <chr>               <dbl>
 1 Afghanistan          37.5
 2 Albania              68.4
 3 Algeria              59.0
 4 Angola               37.9
 5 Argentina            69.1
 6 Australia            74.7
 7 Austria              73.1
 8 Bahrain              65.6
 9 Bangladesh           49.8
10 Belgium              73.6
# … with 132 more rows
~~~
{: .output}

> ## Challenge 2
> Adjust your answer to Challenge 1 to show the mean and median population for each continent.
> > ## Solution to Challenge 2
> > 
> > ~~~
> > gapminder_by_country <- group_by(gapminder, country)
> > 
> > summarise(gapminder_by_country, mean_pop = mean(pop), median_pop = median(pop))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 142 x 3
> >    country      mean_pop median_pop
> >    <chr>           <dbl>      <dbl>
> >  1 Afghanistan 15823715.  13473708.
> >  2 Albania      2580249.   2644572.
> >  3 Algeria     19875406.  18593278.
> >  4 Angola       7309390.   6589530.
> >  5 Argentina   28602240.  28162601 
> >  6 Australia   14649312.  14629150 
> >  7 Austria      7583298.   7571522.
> >  8 Bahrain       373913.    337688.
> >  9 Bangladesh  90755395.  86751356 
> > 10 Belgium      9725119.   9839052.
> > # … with 132 more rows
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Sorting your results
If you need to sort your resulting data frame by a particular variable, use `arrange()`. This 
function takes a data frame and a set of column names and it rearranges the rows so that the 
specified columns are in order.


~~~
arrange(gapminder, gdpPercap)
~~~
{: .language-r}



~~~
# A tibble: 1,704 x 6
   country          continent  year lifeExp      pop gdpPercap
   <chr>            <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Congo, Dem. Rep. Africa     2002    45.0 55379852      241.
 2 Congo, Dem. Rep. Africa     2007    46.5 64606759      278.
 3 Lesotho          Africa     1952    42.1   748747      299.
 4 Guinea-Bissau    Africa     1952    32.5   580653      300.
 5 Congo, Dem. Rep. Africa     1997    42.6 47798986      312.
 6 Eritrea          Africa     1952    35.9  1438760      329.
 7 Myanmar          Asia       1952    36.3 20092996      331 
 8 Lesotho          Africa     1957    45.0   813338      336.
 9 Burundi          Africa     1952    39.0  2445618      339.
10 Eritrea          Africa     1957    38.0  1542611      344.
# … with 1,694 more rows
~~~
{: .output}



~~~
# Use desc() to sort from highest to lowest
arrange(gapminder, desc(gdpPercap))
~~~
{: .language-r}



~~~
# A tibble: 1,704 x 6
   country   continent  year lifeExp     pop gdpPercap
   <chr>     <chr>     <dbl>   <dbl>   <dbl>     <dbl>
 1 Kuwait    Asia       1957    58.0  212846   113523.
 2 Kuwait    Asia       1972    67.7  841934   109348.
 3 Kuwait    Asia       1952    55.6  160000   108382.
 4 Kuwait    Asia       1962    60.5  358266    95458.
 5 Kuwait    Asia       1967    64.6  575003    80895.
 6 Kuwait    Asia       1977    69.3 1140357    59265.
 7 Norway    Europe     2007    80.2 4627926    49357.
 8 Kuwait    Asia       2007    77.6 2505559    47307.
 9 Singapore Asia       2007    80.0 4553009    47143.
10 Norway    Europe     2002    79.0 4535591    44684.
# … with 1,694 more rows
~~~
{: .output}

> ## Challenge 3
> Calculate the average life expectancy per country. Which has the shortest average life expectancy 
> and which has the longest average life expectancy?
> > ## Solution to Challenge 3
> > 
> > ~~~
> > summarised_life_exp <- summarise(gapminder_by_country, mean_life_exp = mean(lifeExp))
> > 
> > arrange(summarised_life_exp, mean_life_exp)
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 142 x 2
> >    country           mean_life_exp
> >    <chr>                     <dbl>
> >  1 Sierra Leone               36.8
> >  2 Afghanistan                37.5
> >  3 Angola                     37.9
> >  4 Guinea-Bissau              39.2
> >  5 Mozambique                 40.4
> >  6 Somalia                    41.0
> >  7 Rwanda                     41.5
> >  8 Liberia                    42.5
> >  9 Equatorial Guinea          43.0
> > 10 Guinea                     43.2
> > # … with 132 more rows
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > arrange(summarised_life_exp, desc(mean_life_exp))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 142 x 2
> >    country     mean_life_exp
> >    <chr>               <dbl>
> >  1 Iceland              76.5
> >  2 Sweden               76.2
> >  3 Norway               75.8
> >  4 Netherlands          75.6
> >  5 Switzerland          75.6
> >  6 Canada               74.9
> >  7 Japan                74.8
> >  8 Australia            74.7
> >  9 Denmark              74.4
> > 10 France               74.3
> > # … with 132 more rows
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

If you provide multiple variables to sort by, `arrange()` will initially sort by the first variable,
with any ties broken by the next variable and so on.

> ## Challenge 4
> Create a new data frame called `summarised_gdp` which calculates the `mean_gdp_per_cap` per 
> continent for each year. Remember that `group_by()` can be given multiple grouping variables.
>
> Observe the result when you run each of the following two lines. What are the differences and 
> when might you use one over the other?
> ~~~~
> arrange(summarised_gdp, desc(year), desc(mean_gdp_per_cap))
> ~~~~
> {: .language-r}
> ~~~~
> arrange(summarised_gdp, desc(mean_gdp_per_cap), desc(year))
> ~~~~
> {: .language-r}
> > ## Solution to Challenge 4
> > 
> > ~~~
> > gap_by_cont_year <- group_by(gapminder, continent, year)
> > 
> > summarised_gdp <- summarise(gap_by_cont_year, mean_gdp_per_cap = mean(gdpPercap))
> > 
> > arrange(summarised_gdp, desc(year), desc(mean_gdp_per_cap))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 60 x 3
> > # Groups:   continent [5]
> >    continent  year mean_gdp_per_cap
> >    <chr>     <dbl>            <dbl>
> >  1 Oceania    2007           29810.
> >  2 Europe     2007           25054.
> >  3 Asia       2007           12473.
> >  4 Americas   2007           11003.
> >  5 Africa     2007            3089.
> >  6 Oceania    2002           26939.
> >  7 Europe     2002           21712.
> >  8 Asia       2002           10174.
> >  9 Americas   2002            9288.
> > 10 Africa     2002            2599.
> > # … with 50 more rows
> > ~~~
> > {: .output}
> > 
> > 
> > 
> > ~~~
> > arrange(summarised_gdp, desc(mean_gdp_per_cap), desc(year))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 60 x 3
> > # Groups:   continent [5]
> >    continent  year mean_gdp_per_cap
> >    <chr>     <dbl>            <dbl>
> >  1 Oceania    2007           29810.
> >  2 Oceania    2002           26939.
> >  3 Europe     2007           25054.
> >  4 Oceania    1997           24024.
> >  5 Europe     2002           21712.
> >  6 Oceania    1992           20894.
> >  7 Oceania    1987           20448.
> >  8 Europe     1997           19077.
> >  9 Oceania    1982           18555.
> > 10 Oceania    1977           17284.
> > # … with 50 more rows
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

## Counting things
A very common summary operation is to count the number of observations. The `n()`
function will help simplify this process. `n()` will return the number of rows in the data frame (or
in the group if the data frame is grouped).


~~~
summarise(gapminder, num_rows = n())
~~~
{: .language-r}



~~~
# A tibble: 1 x 1
  num_rows
     <int>
1     1704
~~~
{: .output}



~~~
summarise(gapminder_by_country, num_rows = n())
~~~
{: .language-r}



~~~
# A tibble: 142 x 2
   country     num_rows
   <chr>          <int>
 1 Afghanistan       12
 2 Albania           12
 3 Algeria           12
 4 Angola            12
 5 Argentina         12
 6 Australia         12
 7 Austria           12
 8 Bahrain           12
 9 Bangladesh        12
10 Belgium           12
# … with 132 more rows
~~~
{: .output}

The `n()` function can be very useful if we need to use the number of observations in calculations.
For instance, if we wanted to get the standard error of the population per country:


~~~
#standard error = standard deviation / square root of the number of samples
summarise(gapminder_by_country, se_pop = sd(pop) / sqrt(n()) )
~~~
{: .language-r}



~~~
# A tibble: 142 x 2
   country        se_pop
   <chr>           <dbl>
 1 Afghanistan  2053803.
 2 Albania       239192.
 3 Algeria      2486462.
 4 Angola        771421.
 5 Argentina    2178518.
 6 Australia    1130222.
 7 Austria       126342.
 8 Bahrain        60880.
 9 Bangladesh  10020393.
10 Belgium       150295.
# … with 132 more rows
~~~
{: .output}

> ## Challenge 5
> Let's try to put together all three functions introduced here. Produce a data frame that summarises
> the number of rows for each continent, sorted from highest to lowest. Use 
> `group_by()`, `summarise()`, and `arrange()` in that order to achieve it.
> > ## Solution to Challenge 5
> > 
> > ~~~
> > gap_by_cont <- group_by(gapminder, continent) 
> > 
> > count_by_cont <- summarise(gap_by_cont, num_rows = n())
> > 
> > arrange(count_by_cont, desc(num_rows))
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > # A tibble: 5 x 2
> >   continent num_rows
> >   <chr>        <int>
> > 1 Africa         624
> > 2 Asia           396
> > 3 Europe         360
> > 4 Americas       300
> > 5 Oceania         24
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}