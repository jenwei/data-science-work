Gapminder
================
Jen Wei
2020-07-24

  - [Grading Rubric](#grading-rubric)
      - [Individual](#individual)
      - [Team](#team)
      - [Due Date](#due-date)
  - [Guided EDA](#guided-eda)
  - [Your Own EDA](#your-own-eda)

*Purpose*: Learning to do EDA well takes practice\! In this challenge
you’ll further practice EDA by first completing a guided exploration,
then by conducting your own investigation. This challenge will also give
you a chance to use the wide variety of visual tools we’ve been
learning.

<!-- include-rubric -->

# Grading Rubric

<!-- -------------------------------------------------- -->

Unlike exercises, **challenges will be graded**. The following rubrics
define how you will be graded, both on an individual and team basis.

## Individual

<!-- ------------------------- -->

| Category    | Unsatisfactory                                                                   | Satisfactory                                                               |
| ----------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| Effort      | Some task **q**’s left unattempted                                               | All task **q**’s attempted                                                 |
| Observed    | Did not document observations                                                    | Documented observations based on analysis                                  |
| Supported   | Some observations not supported by analysis                                      | All observations supported by analysis (table, graph, etc.)                |
| Code Styled | Violations of the [style guide](https://style.tidyverse.org/) hinder readability | Code sufficiently close to the [style guide](https://style.tidyverse.org/) |

## Team

<!-- ------------------------- -->

| Category   | Unsatisfactory                                                                                   | Satisfactory                                       |
| ---------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| Documented | No team contributions to Wiki                                                                    | Team contributed to Wiki                           |
| Referenced | No team references in Wiki                                                                       | At least one reference in Wiki to member report(s) |
| Relevant   | References unrelated to assertion, or difficult to find related analysis based on reference text | Reference text clearly points to relevant analysis |

## Due Date

<!-- ------------------------- -->

All the deliverables stated in the rubrics above are due on the day of
the class discussion of that exercise. See the
[Syllabus](https://docs.google.com/document/d/1jJTh2DH8nVJd2eyMMoyNGroReo0BKcJrz1eONi3rPSc/edit?usp=sharing)
for more information.

``` r
library(tidyverse)
```

    ## ── Attaching packages ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.1     ✓ dplyr   1.0.0
    ## ✓ tidyr   1.1.0     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(gapminder)
```

*Background*: [Gapminder](https://www.gapminder.org/about-gapminder/) is
an independent organization that seeks to education people about the
state of the world. They promote a “fact-based worldview” by focusing on
data. The dataset we’ll study in this challenge is from Gapminder.

# Guided EDA

<!-- -------------------------------------------------- -->

First, we’ll go through a round of *guided EDA*. Try to pay attention to
the high-level process we’re going through—after this guided round
you’ll be responsible for doing another cycle of EDA on your own\!

**q0** Perform your “first checks” on the dataset. What variables are in
this dataset?

``` r
glimpse(gapminder)
```

    ## Rows: 1,704
    ## Columns: 6
    ## $ country   <fct> Afghanistan, Afghanistan, Afghanistan, Afghanistan, Afghani…
    ## $ continent <fct> Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia, Asia,…
    ## $ year      <int> 1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997,…
    ## $ lifeExp   <dbl> 28.801, 30.332, 31.997, 34.020, 36.088, 38.438, 39.854, 40.…
    ## $ pop       <int> 8425333, 9240934, 10267083, 11537966, 13079460, 14880372, 1…
    ## $ gdpPercap <dbl> 779.4453, 820.8530, 853.1007, 836.1971, 739.9811, 786.1134,…

``` r
summary(gapminder)
```

    ##         country        continent        year         lifeExp     
    ##  Afghanistan:  12   Africa  :624   Min.   :1952   Min.   :23.60  
    ##  Albania    :  12   Americas:300   1st Qu.:1966   1st Qu.:48.20  
    ##  Algeria    :  12   Asia    :396   Median :1980   Median :60.71  
    ##  Angola     :  12   Europe  :360   Mean   :1980   Mean   :59.47  
    ##  Argentina  :  12   Oceania : 24   3rd Qu.:1993   3rd Qu.:70.85  
    ##  Australia  :  12                  Max.   :2007   Max.   :82.60  
    ##  (Other)    :1632                                                
    ##       pop              gdpPercap       
    ##  Min.   :6.001e+04   Min.   :   241.2  
    ##  1st Qu.:2.794e+06   1st Qu.:  1202.1  
    ##  Median :7.024e+06   Median :  3531.8  
    ##  Mean   :2.960e+07   Mean   :  7215.3  
    ##  3rd Qu.:1.959e+07   3rd Qu.:  9325.5  
    ##  Max.   :1.319e+09   Max.   :113523.1  
    ## 

**Observations**:

  - The variables in the dataset include `country`, `continent`, `year`,
    `lifeExp`, `pop`, and `gdpPercap`

**q1** Determine the most and least recent years in the `gapminder`
dataset.

``` r
## TASK: Find the largest and smallest values of `year` in `gapminder`
year_max <- max(select(gapminder, year))
year_min <- min(select(gapminder, year))

year_max
```

    ## [1] 2007

``` r
year_min
```

    ## [1] 1952

Use the following test to check your work.

``` r
## NOTE: No need to change this
assertthat::assert_that(year_max %% 7 == 5)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_max %% 3 == 0)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_min %% 7 == 6)
```

    ## [1] TRUE

``` r
assertthat::assert_that(year_min %% 3 == 2)
```

    ## [1] TRUE

``` r
print("Nice!")
```

    ## [1] "Nice!"

**q2** Filter on years matching `year_min`, and make a plot of the GDE
per capita against continent. Choose an appropriate `geom_` to visualize
the data. What observations can you make?

You may encounter difficulties in visualizing these data; if so document
your challenges and attempt to produce the most informative visual you
can.

``` r
year_min_df <- filter(gapminder, year == year_min)
glimpse(year_min_df)
```

    ## Rows: 142
    ## Columns: 6
    ## $ country   <fct> Afghanistan, Albania, Algeria, Angola, Argentina, Australia…
    ## $ continent <fct> Asia, Europe, Africa, Africa, Americas, Oceania, Europe, As…
    ## $ year      <int> 1952, 1952, 1952, 1952, 1952, 1952, 1952, 1952, 1952, 1952,…
    ## $ lifeExp   <dbl> 28.801, 55.230, 43.077, 30.015, 62.485, 69.120, 66.800, 50.…
    ## $ pop       <int> 8425333, 1282697, 9279525, 4232095, 17876956, 8691212, 6927…
    ## $ gdpPercap <dbl> 779.4453, 1601.0561, 2449.0082, 3520.6103, 5911.3151, 10039…

``` r
year_min_df %>%
  ggplot(mapping = aes(y = gdpPercap, x = continent)) +
  geom_boxplot() +
  labs(title = "GDP per capita by continent in 1952") +
  scale_y_log10()
```

![](c04-gapminder-assignment_files/figure-gfm/q2-task-1.png)<!-- -->

**Observations**:

  - Asia has the largest range of GDP per capita
  - Oceania has the smallest range of GDP per capita
  - Asia has the country with the largest GDP per capita (though it’s an
    outlier)
      - Excluding the outliers, Europe has the country with the largest
        GDP per capita
  - Africa has the country with the lowest GDP per capita
  - Oceania has the largest median GDP per capita
  - Africa has the smallest median GDP per capita
  - There are three outliers identified in the dataset - two in Americas
    and one in Asia

**Difficulties & Approaches**:

  - For visualizing `gdpPercap` vs `continent`, I first tried a column
    plot, but it was a bit noisy (as there seemed to be a line per row
    in the filtered dataset), and the main takeaway from it was the
    total count per continent. Then, I decided to use a boxplot to see
    trends within each `continent`. This worked better, but the spread
    of data across countries and continents made certain boxplots
    squished. To stretch them out a bit, I log-scaled `gdpPercap`.

**q3** You should have found at least three outliers in q2. Identify
those outliers (figure out which countries they are).

``` r
americas_outliers_df <- filter(year_min_df, gdpPercap > 1.000e+04, continent == 'Americas')
glimpse(americas_outliers_df)
```

    ## Rows: 2
    ## Columns: 6
    ## $ country   <fct> Canada, United States
    ## $ continent <fct> Americas, Americas
    ## $ year      <int> 1952, 1952
    ## $ lifeExp   <dbl> 68.75, 68.44
    ## $ pop       <int> 14785584, 157553000
    ## $ gdpPercap <dbl> 11367.16, 13990.48

``` r
asia_outliers_df <- filter(year_min_df, gdpPercap > 1.000e+05, continent == 'Asia')
glimpse(asia_outliers_df)
```

    ## Rows: 1
    ## Columns: 6
    ## $ country   <fct> Kuwait
    ## $ continent <fct> Asia
    ## $ year      <int> 1952
    ## $ lifeExp   <dbl> 55.565
    ## $ pop       <int> 160000
    ## $ gdpPercap <dbl> 108382.4

**Observations**:

I initially thought of using the plot to identify the outliers via [this
StackOverflow
post](https://stackoverflow.com/questions/33524669/labeling-outliers-of-boxplots-in-r),
but then I realized I could just filter the data based on info from the
q2 plot of GDP per capita by continent in 1952.

  - The outliers are Canada, United States, and Kuwait

NOTE: This was done manually and could’ve been done in a smarter way,
but it works?

**q4** Create a plot similar to yours from q2 studying both `year_min`
and `year_max`. Find a way to highlight the outliers from q3 on your
plot. Compare the patterns between `year_min` and `year_max`.

*Hint*: We’ve learned a lot of different ways to show multiple
variables; think about using different aesthetics or facets.

``` r
year_extremes_df <- filter(gapminder, year == year_min | year == year_max)
glimpse(year_extremes_df)
```

    ## Rows: 284
    ## Columns: 6
    ## $ country   <fct> Afghanistan, Afghanistan, Albania, Albania, Algeria, Algeri…
    ## $ continent <fct> Asia, Asia, Europe, Europe, Africa, Africa, Africa, Africa,…
    ## $ year      <int> 1952, 2007, 1952, 2007, 1952, 2007, 1952, 2007, 1952, 2007,…
    ## $ lifeExp   <dbl> 28.801, 43.828, 55.230, 76.423, 43.077, 72.301, 30.015, 42.…
    ## $ pop       <int> 8425333, 31889923, 1282697, 3600523, 9279525, 33333216, 423…
    ## $ gdpPercap <dbl> 779.4453, 974.5803, 1601.0561, 5937.0295, 2449.0082, 6223.3…

``` r
year_extremes_df %>%
  ggplot(mapping = aes(y = gdpPercap, x = continent, color = factor(year))) +
  geom_boxplot() +
  facet_grid(~ year) +
  stat_summary(
    fun = median,
    geom = "line",
    aes(group = year, color = factor(year)),
    lwd = 1,
    position = position_dodge(width = .75)
  ) +
  scale_y_log10() +
  labs(title = "GDP per capita by continent")
```

![](c04-gapminder-assignment_files/figure-gfm/q4-task-1.png)<!-- -->

**Observations**: - GDP per capita by continent (from highest to lowest)
is the same for the earliest and latest years - Oceania, Europe,
Americas, Asia, Africa - The spread of GDP per capita across countries
for each continent has increased between 1952 and 2007 - Both years have
three outliers - 2007 outliers are all in Americas: Haiti, Canada, and
United States

``` r
americas_latest_outliers_df <- filter(year_extremes_df, gdpPercap > 2.000e+04 | gdpPercap < 2.500e+03 , continent == 'Americas', year == 2007)
glimpse(americas_latest_outliers_df)
```

    ## Rows: 3
    ## Columns: 6
    ## $ country   <fct> Canada, Haiti, United States
    ## $ continent <fct> Americas, Americas, Americas
    ## $ year      <int> 2007, 2007, 2007
    ## $ lifeExp   <dbl> 80.653, 60.916, 78.242
    ## $ pop       <int> 33390141, 8502814, 301139947
    ## $ gdpPercap <dbl> 36319.235, 1201.637, 42951.653

# Your Own EDA

<!-- -------------------------------------------------- -->

Now it’s your turn\! We just went through guided EDA considering the GDP
per capita at two time points. You can continue looking at outliers,
consider different years, repeat the exercise with `lifeExp`, consider
the relationship between variables, or something else entirely.

**q5** Create *at least* three new figures below. With each figure, try
to pose new questions about the data.

While going through EDA for GDP per capita, I was curious about how
other variables impact GDP per capita, so first, I’ll look into
population.

``` r
gapminder %>%
  ggplot(mapping = aes(x = pop, y = gdpPercap, color = year)) +
  geom_point() +
  facet_wrap(~ continent, nrow = 5) +
  scale_x_log10() +
  scale_y_log10() +
  labs(title = "GDP per capita by population per continent over time")
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task1-1.png)<!-- -->

**Observations:** - Seems like there are some groupings within the data
that show a linear, positive trend - Over time, both population and GDP
per capita increased for Oceania - There are two distinct groups, one
for each Oceanian country (New Zealand and Australia)

There’s a lot of data to digest here, so similar to the guided EDA, I’ll
now focus on the earliest and latest years, 1952 and 2007 and try to
familiarize myself with just population.

``` r
year_extremes_df %>%
  ggplot(mapping = aes(y = pop, x = continent, color = factor(year))) +
  geom_boxplot() +
  facet_grid(~ year) +
  stat_summary(
    fun = median,
    geom = "line",
    aes(group = year, color = factor(year)),
    lwd = 1,
    position = position_dodge(width = .75)
  ) +
  scale_y_log10() +
  labs(title = "Population by continent for the year-extremes")
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task2-1.png)<!-- -->

**Observations:**

  - The median population size increased for all continents between 1952
    and 2007
  - The largest median population size is associated with Asia in both
    years
  - There is only one outlier in 2007 compared to three in 1952
  - The median population sizes for Africa, Americas, Europe, and
    Oceania look similar on the log scale (or at least less distinct)
    for 2007 compared to 1952

The insights from the plot are expected as the world population is
consistently growing, and this served as a helpful check to ensure there
aren’t any abnormalities before looking at population AND GDP per
capita.

``` r
# Needed for geom_label_repel
library(ggrepel)

year_extremes_min_max_df <-
  year_extremes_df %>%
  group_by(continent, year) %>%
  filter(pop == min(pop) | pop == max(pop))

year_extremes_min_max_df
```

    ## # A tibble: 20 x 6
    ## # Groups:   continent, year [10]
    ##    country               continent  year lifeExp        pop gdpPercap
    ##    <fct>                 <fct>     <int>   <dbl>      <int>     <dbl>
    ##  1 Australia             Oceania    1952    69.1    8691212    10040.
    ##  2 Australia             Oceania    2007    81.2   20434176    34435.
    ##  3 Bahrain               Asia       1952    50.9     120447     9867.
    ##  4 Bahrain               Asia       2007    75.6     708573    29796.
    ##  5 China                 Asia       1952    44    556263527      400.
    ##  6 China                 Asia       2007    73.0 1318683096     4959.
    ##  7 Germany               Europe     1952    67.5   69145952     7144.
    ##  8 Germany               Europe     2007    79.4   82400996    32170.
    ##  9 Iceland               Europe     1952    72.5     147962     7268.
    ## 10 Iceland               Europe     2007    81.8     301931    36181.
    ## 11 New Zealand           Oceania    1952    69.4    1994794    10557.
    ## 12 New Zealand           Oceania    2007    80.2    4115771    25185.
    ## 13 Nigeria               Africa     1952    36.3   33119096     1077.
    ## 14 Nigeria               Africa     2007    46.9  135031164     2014.
    ## 15 Sao Tome and Principe Africa     1952    46.5      60011      880.
    ## 16 Sao Tome and Principe Africa     2007    65.5     199579     1598.
    ## 17 Trinidad and Tobago   Americas   1952    59.1     662850     3023.
    ## 18 Trinidad and Tobago   Americas   2007    69.8    1056608    18009.
    ## 19 United States         Americas   1952    68.4  157553000    13990.
    ## 20 United States         Americas   2007    78.2  301139947    42952.

``` r
year_extremes_df %>%
  ggplot(mapping = aes(x = pop, y = gdpPercap, color = continent)) +
  geom_point() +
  geom_label_repel(
    data = year_extremes_min_max_df,
    aes(label = gdpPercap)
  ) +
  facet_grid(~ year ~ .) +
  scale_x_log10() +
  scale_y_log10() +
  labs(title = "GDP per capita by population per continent for 1952 and 2007 (with first and last population counts annotated)")
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task3-1.png)<!-- -->

**Observations:**

Looking at the extremes of each continent in 1952, the smallest
populated countries in Africa and the Americas had lower GDP per capita
than that of the largest populated countries, while in Asia, Europe, and
Oceania, the opposite is true where the smallest populated countries had
higher GDP per capita than that of the largest populated countries.

  - In Africa, the smallest populated country had a *lower* GDP per
    capita than that of the largest populated country
  - In Americas, the smallest populated country had a *lower* GDP per
    capita than that of the largest populated country
  - In Asia, the smallest populated country had a *higher* GDP per
    capita than that of the largest populated country
  - In Europe, the smallest populated country had a *higher* GDP per
    capita than that of the largest populated country
  - In Oceania, the smallest populated country had a *higher* GDP per
    capita than that of the largest populated country

Looking at the extremes of each continent in 2007, all countries had the
same relations between the extremes aside from Oceania, where the
smallest populated country had a *lower* GDP per capita than that of the
largest populated country (which is different from 1952).

Both generally and by continent, there is no linear relationship between
population and GDP per capita. This is not totally unexpected though as
each point is a country, and each country has its own economy, and there
are other factors not represented in the dataset that likely more
directly and more greatly influenced GDP per capita.

**Bonus\!**

After chatting with the rest of Team Zeta, people were curious about
drilling into the second plot of GDP per capita and population per
continent. Thought about doing that earlier but ran out of time/energy.
However, I ended up circling back and figured I’d add it here.

``` r
gap_minder_mean_df <- gapminder %>%
  group_by(continent, year) %>%
  summarise(mean_gdpPercap = mean(gdpPercap), mean_pop = mean(pop))
```

    ## `summarise()` regrouping output by 'continent' (override with `.groups` argument)

``` r
gap_minder_mean_df
```

    ## # A tibble: 60 x 4
    ## # Groups:   continent [5]
    ##    continent  year mean_gdpPercap  mean_pop
    ##    <fct>     <int>          <dbl>     <dbl>
    ##  1 Africa     1952          1253.  4570010.
    ##  2 Africa     1957          1385.  5093033.
    ##  3 Africa     1962          1598.  5702247.
    ##  4 Africa     1967          2050.  6447875.
    ##  5 Africa     1972          2340.  7305376.
    ##  6 Africa     1977          2586.  8328097.
    ##  7 Africa     1982          2482.  9602857.
    ##  8 Africa     1987          2283. 11054502.
    ##  9 Africa     1992          2282. 12674645.
    ## 10 Africa     1997          2379. 14304480.
    ## # … with 50 more rows

``` r
gap_minder_mean_df %>%
  ggplot(mapping = aes(x = mean_pop, y = mean_gdpPercap, color = year)) +
  geom_point() +
  facet_wrap(~ continent, nrow = 5) +
  scale_x_log10() +
  scale_y_log10() +
  labs(title = "Mean GDP per capita by mean population per continent over time")
```

![](c04-gapminder-assignment_files/figure-gfm/q5-task4-1.png)<!-- -->
**Observations:**

When looking at the mean population and mean GDP per capita on a log-log
scale, we can see a somewhat linear trend of population and GDP per
capita both increasing over the years.

  - Europe has the smallest mean population range over time
  - Africa has the largest mean population range over time
  - Slope of the Europe datapoints is the sharpest across the five
    continents
