Mini Data Analysis Milestone 2
================

*To complete this milestone, you can edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to your second (and last) milestone in your mini data analysis project!

In Milestone 1, you explored your data, came up with research questions,
and obtained some results by making summary tables and graphs. This
time, we will first explore more in depth the concept of *tidy data.*
Then, you’ll be sharpening some of the results you obtained from your
previous milestone by:

-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 55 points (compared to the 45 points
of the Milestone 1): 45 for your analysis, and 10 for your entire
mini-analysis GitHub repository. Details follow.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

-   Understand what *tidy* data is, and how to create it using `tidyr`.
-   Generate a reproducible and clear report using R Markdown.
-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) # <- might contain the data you picked!
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.5 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.3      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

# Task 1: Tidy your data (15 points)

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

-   Each row is an **observation**
-   Each column is a **variable**
-   Each cell is a **value**

*Tidy’ing* data is sometimes necessary because it can simplify
computation. Other times it can be nice to organize data so that it can
be easier to understand when read manually.

### 2.1 (2.5 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

``` r
#reviewing what the vancouver_trees dataset contains
head(vancouver_trees)
```

    ## # A tibble: 6 × 20
    ##   tree_id civic_number std_str…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##     <dbl>        <dbl> <chr>     <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ## 1  149556          494 W 58TH AV ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ## 2  149563          450 W 58TH AV ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ## 3  149579         4994 WINDSOR … STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ## 4  149590          858 E 39TH AV FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ## 5  149604         5032 WINDSOR … ACER    CAMPES… <NA>    HEDGE … N       N      
    ## 6  149616          585 W 61ST AV PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ## # … with 11 more variables: plant_area <chr>, on_street_block <dbl>,
    ## #   on_street <chr>, neighbourhood_name <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, curb <chr>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​assigned, ⁷​root_barrier

``` r
glimpse(vancouver_trees)
```

    ## Rows: 146,611
    ## Columns: 20
    ## $ tree_id            <dbl> 149556, 149563, 149579, 149590, 149604, 149616, 149…
    ## $ civic_number       <dbl> 494, 450, 4994, 858, 5032, 585, 4909, 4925, 4969, 7…
    ## $ std_street         <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"…
    ## $ genus_name         <chr> "ULMUS", "ZELKOVA", "STYRAX", "FRAXINUS", "ACER", "…
    ## $ species_name       <chr> "AMERICANA", "SERRATA", "JAPONICA", "AMERICANA", "C…
    ## $ cultivar_name      <chr> "BRANDON", NA, NA, "AUTUMN APPLAUSE", NA, "CHANTICL…
    ## $ common_name        <chr> "BRANDON ELM", "JAPANESE ZELKOVA", "JAPANESE SNOWBE…
    ## $ assigned           <chr> "N", "N", "N", "Y", "N", "N", "N", "N", "N", "N", "…
    ## $ root_barrier       <chr> "N", "N", "N", "N", "N", "N", "N", "N", "N", "N", "…
    ## $ plant_area         <chr> "N", "N", "4", "4", "4", "B", "6", "6", "3", "3", "…
    ## $ on_street_block    <dbl> 400, 400, 4900, 800, 5000, 500, 4900, 4900, 4900, 7…
    ## $ on_street          <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"…
    ## $ neighbourhood_name <chr> "MARPOLE", "MARPOLE", "KENSINGTON-CEDAR COTTAGE", "…
    ## $ street_side_name   <chr> "EVEN", "EVEN", "EVEN", "EVEN", "EVEN", "ODD", "ODD…
    ## $ height_range_id    <dbl> 2, 4, 3, 4, 2, 2, 3, 3, 2, 2, 2, 5, 3, 2, 2, 2, 2, …
    ## $ diameter           <dbl> 10.00, 10.00, 4.00, 18.00, 9.00, 5.00, 15.00, 14.00…
    ## $ curb               <chr> "N", "N", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "…
    ## $ date_planted       <date> 1999-01-13, 1996-05-31, 1993-11-22, 1996-04-29, 19…
    ## $ longitude          <dbl> -123.1161, -123.1147, -123.0846, -123.0870, -123.08…
    ## $ latitude           <dbl> 49.21776, 49.21776, 49.23938, 49.23469, 49.23894, 4…

``` r
class(vancouver_trees)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

From what I can see, this dataset is relatively tidy. Every column
represents a different variable, every row is a specific observation
(individual tree id), and every cell is a single measurement. The one
variable/column that could potentially be considered as untidy is
“plant_area” where there are a mix of numerical and categorical data
within the column. A solution could be to split the column into 2
different columns, keeping the measurements in “plant_area” as the
categorical/letter based data, and then creating a new column to hold
all of the “continuous”/numerical data and call it something like
“width_of_blvrd”. However, a downside of this would be the relatively
large amount of “NA” cells in each of the columns.

<!----------------------------------------------------------------------------->

### 2.2 (5 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

``` r
# original vancouver_trees tibble before any alterations
head(vancouver_trees)
```

    ## # A tibble: 6 × 20
    ##   tree_id civic_number std_str…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##     <dbl>        <dbl> <chr>     <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ## 1  149556          494 W 58TH AV ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ## 2  149563          450 W 58TH AV ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ## 3  149579         4994 WINDSOR … STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ## 4  149590          858 E 39TH AV FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ## 5  149604         5032 WINDSOR … ACER    CAMPES… <NA>    HEDGE … N       N      
    ## 6  149616          585 W 61ST AV PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ## # … with 11 more variables: plant_area <chr>, on_street_block <dbl>,
    ## #   on_street <chr>, neighbourhood_name <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, curb <chr>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​assigned, ⁷​root_barrier

``` r
# putting the street block number and name together into one column, could potentially be useful but also runs the risk of being too coarse if certain street blocks within a neighbourhood need to be analyzed
vancouver_trees %>%
  unite(col = "street_block_info",
        c(on_street_block, on_street),
        sep = " ")
```

    ## # A tibble: 146,611 × 19
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1  149556          494 W 58TH … ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ##  2  149563          450 W 58TH … ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ##  3  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ##  4  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ##  5  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N       N      
    ##  6  149616          585 W 61ST … PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ##  7  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  8  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  9  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ## 10  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N       N      
    ## # … with 146,601 more rows, 10 more variables: plant_area <chr>,
    ## #   street_block_info <chr>, neighbourhood_name <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, curb <chr>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​assigned, ⁷​root_barrier

``` r
# combining the longitude and latitude together into a coordinates variable which shortens the tibbles number of columns as well - probably easier to compile the raw data in this separated form but could make sense to have these together
vancouver_trees %>%
  unite(col = "coordinates",
        c(longitude, latitude),
        sep = ", ")
```

    ## # A tibble: 146,611 × 19
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1  149556          494 W 58TH … ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ##  2  149563          450 W 58TH … ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ##  3  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ##  4  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ##  5  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N       N      
    ##  6  149616          585 W 61ST … PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ##  7  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  8  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  9  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ## 10  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N       N      
    ## # … with 146,601 more rows, 10 more variables: plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, neighbourhood_name <chr>,
    ## #   street_side_name <chr>, height_range_id <dbl>, diameter <dbl>, curb <chr>,
    ## #   date_planted <date>, coordinates <chr>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​assigned, ⁷​root_barrier

``` r
# making the dataset untidy by creating separate columns for each neighbourhood and placing the diameter value as the observaitonal value for each tree - this makes for an unreasonably "wide" dataset and results in a very large number of NA values scattered throughout the dataset
untidy_1 <- vancouver_trees %>%
  pivot_wider(names_from = neighbourhood_name,
              values_from = diameter)

untidy_1
```

    ## # A tibble: 146,611 × 40
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1  149556          494 W 58TH … ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ##  2  149563          450 W 58TH … ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ##  3  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ##  4  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ##  5  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N       N      
    ##  6  149616          585 W 61ST … PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ##  7  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  8  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  9  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ## 10  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N       N      
    ## # … with 146,601 more rows, 31 more variables: plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, curb <chr>, date_planted <date>, longitude <dbl>,
    ## #   latitude <dbl>, MARPOLE <dbl>, `KENSINGTON-CEDAR COTTAGE` <dbl>,
    ## #   OAKRIDGE <dbl>, `MOUNT PLEASANT` <dbl>, `RENFREW-COLLINGWOOD` <dbl>,
    ## #   `RILEY PARK` <dbl>, DOWNTOWN <dbl>, SUNSET <dbl>, `ARBUTUS-RIDGE` <dbl>,
    ## #   `GRANDVIEW-WOODLAND` <dbl>, KITSILANO <dbl>, `WEST END` <dbl>, …

``` r
# tidying the dataset back to its original state
van_trees_og <- untidy_1 %>%
  pivot_longer(cols = c(-tree_id, -civic_number, -std_street, -genus_name, -species_name, -cultivar_name, -common_name, -assigned, -root_barrier, -plant_area, -on_street_block, -on_street, -street_side_name, -height_range_id, -curb, -date_planted, -longitude, -latitude), 
               names_to = "neighbourhood_names", 
               values_to = "diameter",
               values_drop_na = TRUE)

van_trees_og
```

    ## # A tibble: 146,611 × 20
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ assig…⁶ root_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1  149556          494 W 58TH … ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ##  2  149563          450 W 58TH … ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ##  3  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N       N      
    ##  4  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… Y       N      
    ##  5  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N       N      
    ##  6  149616          585 W 61ST … PYRUS   CALLER… CHANTI… CHANTI… N       N      
    ##  7  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  8  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  9  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ## 10  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N       N      
    ## # … with 146,601 more rows, 11 more variables: plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, street_side_name <chr>,
    ## #   height_range_id <dbl>, curb <chr>, date_planted <date>, longitude <dbl>,
    ## #   latitude <dbl>, neighbourhood_names <chr>, diameter <dbl>, and abbreviated
    ## #   variable names ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name,
    ## #   ⁵​common_name, ⁶​assigned, ⁷​root_barrier

<!----------------------------------------------------------------------------->

### 2.3 (7.5 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the next four tasks:

<!-------------------------- Start your work below ---------------------------->

1.  How does plant_area affect the diameter growth of trees? More
    specifically, are there neighbourhoods in which this is more or less
    impactful?
2.  How has the distribution of large trees vs small trees changed over
    time in each neighbourhood? And has there been a shift in the types
    of trees planted over time?

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

I decided to keep my research question related to plant_area and
diameter growth of trees because I was not able to parse the data as
effectively as I wanted to in the last mini data analysis project.
Determining this relationship seems like it could help make better
informed decisions when deciding where to plant further trees.

I added a new research question different from those in my first mini
data analysis assignment which is more focused on using the time data
included in the dataset. This data could help track trends in planting
efforts over the years and tell us whether planting has increased or
decreased in certain neighbourhoods over time.
<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

<!--------------------------- Start your work below --------------------------->

``` r
# getting rid of columns that are not of interest to me right now
van_trees_i <- vancouver_trees %>%
  select(c(-assigned, -on_street_block, -on_street, -street_side_name, -curb))

# new tibble where only trees with letter character inputs for plant_area are considered
pa_let <- van_trees_i %>%
  filter(plant_area %in% c("B", "C", "G", "L", "M", "N", "P", "Y"))

pa_let
```

    ## # A tibble: 33,864 × 15
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ root_…⁶ plant…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1  149556          494 W 58TH … ULMUS   AMERIC… BRANDON BRANDO… N       N      
    ##  2  149563          450 W 58TH … ZELKOVA SERRATA <NA>    JAPANE… N       N      
    ##  3  149616          585 W 61ST … PYRUS   CALLER… CHANTI… CHANTI… N       B      
    ##  4  149640         6968 SELKIRK… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  5  149683         7011 SELKIRK… ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  6  149684         1223 W 54TH … ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  7  149694         1292 W 49TH … ACER    PLATAN… COLUMN… COLUMN… N       N      
    ##  8  155226         4525 CLAREND… LIQUID… STYRAC… <NA>    AMERIC… N       N      
    ##  9  155317          316 CARRALL… ACER    RUBRUM  <NA>    RED MA… N       C      
    ## 10  155321          319 CARRALL… ACER    RUBRUM  <NA>    RED MA… N       C      
    ## # … with 33,854 more rows, 6 more variables: neighbourhood_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​root_barrier, ⁷​plant_area

``` r
# new tibble where only trees with number inputs for plant_area are considered
pa_num <- van_trees_i %>%
  filter(str_detect(plant_area, "\\d")) %>%
  rename(blvd_width = plant_area)

# converting the plant_area column to be numeric type  
pa_num$blvd_width = as.numeric(as.character(pa_num$blvd_width))

pa_num
```

    ## # A tibble: 110,833 × 15
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ root_…⁶ blvd_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>     <dbl>
    ##  1  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N             4
    ##  2  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N             4
    ##  3  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N             4
    ##  4  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             6
    ##  5  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             6
    ##  6  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             3
    ##  7  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N             3
    ##  8  149626          736 E 39TH … TILIA   EUCHLO… <NA>    CRIMEA… N             5
    ##  9  149636          812 E 39TH … TILIA   EUCHLO… <NA>    CRIMEA… N             3
    ## 10  149646          505 E 16TH … HIBISC… SYRIACA <NA>    ROSE O… N             3
    ## # … with 110,823 more rows, 6 more variables: neighbourhood_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, and abbreviated variable names
    ## #   ¹​std_street, ²​genus_name, ³​species_name, ⁴​cultivar_name, ⁵​common_name,
    ## #   ⁶​root_barrier, ⁷​blvd_width

``` r
# creating bins for the height ranges 
van_trees_bins <- pa_num %>%
  mutate(height_bins = cut(height_range_id, breaks = c(0,2,4,6,8,10), labels = c("xsmall", "small", "medium", "large", "xlarge")))

# making a new "year" date column  
van_trees_new <- van_trees_bins %>% 
    mutate(year = lubridate::floor_date(date_planted, "year"))

van_trees_new
```

    ## # A tibble: 110,833 × 17
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ root_…⁶ blvd_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>     <dbl>
    ##  1  149579         4994 WINDSOR… STYRAX  JAPONI… <NA>    JAPANE… N             4
    ##  2  149590          858 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N             4
    ##  3  149604         5032 WINDSOR… ACER    CAMPES… <NA>    HEDGE … N             4
    ##  4  149617         4909 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             6
    ##  5  149618         4925 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             6
    ##  6  149619         4969 SHERBRO… ACER    PLATAN… COLUMN… COLUMN… N             3
    ##  7  149625          720 E 39TH … FRAXIN… AMERIC… AUTUMN… AUTUMN… N             3
    ##  8  149626          736 E 39TH … TILIA   EUCHLO… <NA>    CRIMEA… N             5
    ##  9  149636          812 E 39TH … TILIA   EUCHLO… <NA>    CRIMEA… N             3
    ## 10  149646          505 E 16TH … HIBISC… SYRIACA <NA>    ROSE O… N             3
    ## # … with 110,823 more rows, 8 more variables: neighbourhood_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, height_bins <fct>, year <date>, and
    ## #   abbreviated variable names ¹​std_street, ²​genus_name, ³​species_name,
    ## #   ⁴​cultivar_name, ⁵​common_name, ⁶​root_barrier, ⁷​blvd_width

<!----------------------------------------------------------------------------->

# Task 2: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

<!-------------------------- Start your work below ---------------------------->

``` r
# graphing the change in frequency of trees in their respective height categories over time
van_trees_new %>%
  group_by(height_bins, year) %>%
  count(height_bins, year) %>%
  ggplot(aes(year, n)) +
  geom_line(aes(colour = height_bins)) +
  ylim(0,5000) +
  scale_y_continuous(trans='log10')
```

    ## Scale for 'y' is already present. Adding another scale for 'y', which will
    ## replace the existing scale.

    ## Warning: Removed 6 row(s) containing missing values (geom_path).

![](mini-project-2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->
<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)

        -   Note that you might first have to *make* a time-based column
            using a function like `ymd()`, but this doesn’t count.
        -   Examples of something you might do here: extract the day of
            the year from a date, or extract the weekday, or let 24
            hours elapse on your dates.

    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).

        -   For example, you could say something like “Investigating the
            day of the week might be insightful because penguins don’t
            work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number 3**

``` r
 # using the floor_date function in lubridate to create a new column indicating the month of the year each tree was planted, and then arranging this row in ascending order from the earliest recorded planting 

van_trees_monthly <- van_trees_new %>% 
    group_by(month = lubridate::floor_date(date_planted, "month")) %>%
  arrange(month)

van_trees_monthly
```

    ## # A tibble: 110,833 × 18
    ## # Groups:   month [293]
    ##    tree_id civic_number std_st…¹ genus…² speci…³ culti…⁴ commo…⁵ root_…⁶ blvd_…⁷
    ##      <dbl>        <dbl> <chr>    <chr>   <chr>   <chr>   <chr>   <chr>     <dbl>
    ##  1  122127          412 E 46TH … TILIA   CORDATA <NA>    LITTLE… N            10
    ##  2  122593         2211 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             9
    ##  3  122595         2221 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             9
    ##  4  122130          434 E 46TH … TILIA   CORDATA <NA>    LITTLE… N            10
    ##  5  122591         2185 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             9
    ##  6  122602         2244 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             9
    ##  7  122603         2232 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             9
    ##  8   31395         2105 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             4
    ##  9   31396         2105 W 32ND … TILIA   CORDATA <NA>    LITTLE… N             4
    ## 10   30343         3621 W 30TH … PRUNUS  CERASI… ATROPU… PISSAR… N            12
    ## # … with 110,823 more rows, 9 more variables: neighbourhood_name <chr>,
    ## #   height_range_id <dbl>, diameter <dbl>, date_planted <date>,
    ## #   longitude <dbl>, latitude <dbl>, height_bins <fct>, year <date>,
    ## #   month <date>, and abbreviated variable names ¹​std_street, ²​genus_name,
    ## #   ³​species_name, ⁴​cultivar_name, ⁵​common_name, ⁶​root_barrier, ⁷​blvd_width

Separating the date_planted column in the original dataset into specific
months could be of use when exploring what time of the year certain
species of trees are planted. This could help inform when and when not
to be planting certain species, along with informing what months out of
the year require the most amount of planting if taking advantage of
specific weather windows.
<!----------------------------------------------------------------------------->

<!-------------------------- Start your work below ---------------------------->

**Task Number 2**

``` r
# putting factor levels together for the height_bins variable if the frequency of the height_bin is less than 10.
van_trees_new %>%
  group_by(height_bins, year) %>%
  mutate(height_bins = fct_lump_min(height_bins, min = 10)) %>%
  count(height_bins, year) %>%
  ggplot(aes(year, n)) +
  geom_line(aes(colour = height_bins)) +
  ylim(0,5000) +
  scale_y_continuous(trans='log10')
```

    ## Scale for 'y' is already present. Adding another scale for 'y', which will
    ## replace the existing scale.

    ## Warning: Removed 6 row(s) containing missing values (geom_path).

![](mini-project-2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

We can see in this plot that the large and extra large height_bins have
been grouped together in the “Other” category. I chose this grouping
because the frequency of large and extra large trees over time was
generally quite low (below 10) in comparison to the extra small to
medium sized trees whose frequency is generally one to two orders of
magnitude larger. It may not be as important to know how the large and
extra large trees are doing year to year as the smaller trees as the
smaller trees are most likely the ones which are planted and we will
want to know if their frequency is increasing (more planting over time)
or decreasing (less planting over time).

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: 1. How does plant_area (particularily the width
of the boulevard) affect the diameter growth of trees? More
specifically, are there neighbourhoods in which this is more or less
impactful?

**Variable of interest**: diameter

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.

    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

``` r
# running a linear regression model to determine the relationship between diameter a
diameter_lm <- lm(diameter ~ blvd_width, van_trees_new, na.action = na.exclude)

diameter_lm
```

    ## 
    ## Call:
    ## lm(formula = diameter ~ blvd_width, data = van_trees_new, na.action = na.exclude)
    ## 
    ## Coefficients:
    ## (Intercept)   blvd_width  
    ##     11.1079       0.1037

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

I would like to know what the impact of very large boulevards (at some
very large blvd_width one could imagine it becomes a green space such as
a park as opposed to a boulevard) is on diameter of trees. For this I
will use the broom::augment function to predict how these large values
of blvd_width which are not in th dataset would impact tree diameter

``` r
# using broom:augment to predict diameter sizes of trees when boulevard width ranges from 75ft to 250ft in steps of 25ft
broom::augment(diameter_lm, newdata = tibble(blvd_width = seq(75,250,by=25)))
```

    ## # A tibble: 8 × 2
    ##   blvd_width .fitted
    ##        <dbl>   <dbl>
    ## 1         75    18.9
    ## 2        100    21.5
    ## 3        125    24.1
    ## 4        150    26.7
    ## 5        175    29.3
    ## 6        200    31.9
    ## 7        225    34.5
    ## 8        250    37.0

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 1 (Task 4.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

``` r
# summary table from milestone 1
sum_table_milestone_1 <- vancouver_trees %>%
  group_by(species_name) %>%
  summarise(mean = mean(height_range_id, na.rm = TRUE),
            sd = sd(height_range_id, na.rm = TRUE),
            range = max(height_range_id, na.rm = TRUE) - min(height_range_id, na.rm = TRUE),
            median = median(height_range_id, na.rm = TRUE))

# creating directory in this filepath called output
dir.create(here::here("output"))
```

    ## Warning in dir.create(here::here("output")): '/Users/harrisonmar/repos/stat545/
    ## harrison_mar_miniDataAnalysis/output' already exists

``` r
# writing a CSV file of summary table to output folder
write.csv(sum_table_milestone_1, here::here("output", "summary_table_milestone_1"))
```

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 3.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

``` r
saveRDS(diameter_lm, here::here("output", "diameter_lm.rds"))

diameter_lm <- readRDS(here::here("output", "diameter_lm.rds"))
```

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

-   In a sentence or two, explains what this repository is, so that
    future-you or someone else stumbling on your repository can be
    oriented to the repository.
-   In a sentence or two (or more??), briefly explains how to engage
    with the repository. You can assume the person reading knows the
    material from STAT 545A. Basically, if a visitor to your repository
    wants to explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least four folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output, and all data
    files saved from Task 4 above appear in the `output` folder.
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 1 document knits error-free, and the Milestone 2 document
knits error-free.

## Tagged release (1 point)

You’ve tagged a release for Milestone 1, and you’ve tagged a release for
Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
