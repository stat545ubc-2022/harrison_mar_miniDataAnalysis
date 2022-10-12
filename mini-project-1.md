Mini Data-Analysis Deliverable 1
================

# Welcome to your (maybe) first-ever data analysis project!

And hopefully the first of many. Let’s get started:

1.  Install the [`datateachr`](https://github.com/UBC-MDS/datateachr)
    package by typing the following into your **R terminal**:

<!-- -->

    install.packages("devtools")
    devtools::install_github("UBC-MDS/datateachr")

2.  Load the packages below.

``` r
library(datateachr)
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

3.  Make a repository in the <https://github.com/stat545ubc-2022>
    Organization. You will be working with this repository for the
    entire data analysis project. You can either make it public, or make
    it private and add the TA’s and Lucy as collaborators. A link to
    help you create a private repository is available on the
    \#collaborative-project Slack channel.

# Instructions

## For Both Milestones

-   Each milestone is worth 45 points. The number of points allocated to
    each task will be annotated within each deliverable. Tasks that are
    more challenging will often be allocated more points.

-   10 points will be allocated to the reproducibility, cleanliness, and
    coherence of the overall analysis. While the two milestones will be
    submitted as independent deliverables, the analysis itself is a
    continuum - think of it as two chapters to a story. Each chapter, or
    in this case, portion of your analysis, should be easily followed
    through by someone unfamiliar with the content.
    [Here](https://swcarpentry.github.io/r-novice-inflammation/06-best-practices-R/)
    is a good resource for what constitutes “good code”. Learning good
    coding practices early in your career will save you hassle later on!

## For Milestone 1

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-1.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work below --->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to the mini-analysis GitHub repository you made
earlier, and tag a release on GitHub. Then, submit a link to your tagged
release on canvas.

**Points**: This milestone is worth 45 points: 43 for your analysis, 1
point for having your Milestone 1 document knit error-free, and 1 point
for tagging your release on Github.

# Learning Objectives

By the end of this milestone, you should:

-   Become familiar with your dataset of choosing
-   Select 4 questions that you would like to answer with your data
-   Generate a reproducible and clear report using R Markdown
-   Become familiar with manipulating and summarizing your data in
    tibbles using `dplyr`, with a research question in mind.

# Task 1: Choose your favorite dataset (10 points)

The `datateachr` package by Hayley Boyce and Jordan Bourak currently
composed of 7 semi-tidy datasets for educational purposes. Here is a
brief description of each dataset:

-   *apt_buildings*: Acquired courtesy of The City of Toronto’s Open
    Data Portal. It currently has 3455 rows and 37 columns.

-   *building_permits*: Acquired courtesy of The City of Vancouver’s
    Open Data Portal. It currently has 20680 rows and 14 columns.

-   *cancer_sample*: Acquired courtesy of UCI Machine Learning
    Repository. It currently has 569 rows and 32 columns.

-   *flow_sample*: Acquired courtesy of The Government of Canada’s
    Historical Hydrometric Database. It currently has 218 rows and 7
    columns.

-   *parking_meters*: Acquired courtesy of The City of Vancouver’s Open
    Data Portal. It currently has 10032 rows and 22 columns.

-   *steam_games*: Acquired courtesy of Kaggle. It currently has 40833
    rows and 21 columns.

-   *vancouver_trees*: Acquired courtesy of The City of Vancouver’s Open
    Data Portal. It currently has 146611 rows and 20 columns.

**Things to keep in mind**

-   We hope that this project will serve as practice for carrying our
    your own *independent* data analysis. Remember to comment your code,
    be explicit about what you are doing, and write notes in this
    markdown document when you feel that context is required. As you
    advance in the project, prompts and hints to do this will be
    diminished - it’ll be up to you!

-   Before choosing a dataset, you should always keep in mind **your
    goal**, or in other ways, *what you wish to achieve with this data*.
    This mini data-analysis project focuses on *data wrangling*,
    *tidying*, and *visualization*. In short, it’s a way for you to get
    your feet wet with exploring data on your own.

And that is exactly the first thing that you will do!

1.1 Out of the 7 datasets available in the `datateachr` package, choose
**4** that appeal to you based on their description. Write your choices
below:

**Note**: We encourage you to use the ones in the `datateachr` package,
but if you have a dataset that you’d really like to use, you can include
it here. But, please check with a member of the teaching team to see
whether the dataset is of appropriate complexity. Also, include a
**brief** description of the dataset here to help the teaching team
understand your data.

<!-------------------------- Start your work below ---------------------------->

1: flow_sample 2: building_permits 3: steam_games 4: vancouver_trees

<!----------------------------------------------------------------------------->

1.2 One way to narrowing down your selection is to *explore* the
datasets. Use your knowledge of dplyr to find out at least *3*
attributes about each of these datasets (an attribute is something such
as number of rows, variables, class type…). The goal here is to have an
idea of *what the data looks like*.

*Hint:* This is one of those times when you should think about the
cleanliness of your analysis. I added a single code chunk for you below,
but do you want to use more than one? Would you like to write more
comments outside of the code chunk?

<!-------------------------- Start your work below ---------------------------->

Exploring the “steam_games” dataset:

``` r
head(steam_games)
```

    ## # A tibble: 6 × 21
    ##      id url          types name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶
    ##   <dbl> <chr>        <chr> <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ## 1     1 https://sto… app   DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ## 2     2 https://sto… app   PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ## 3     3 https://sto… app   BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado…
    ## 4     4 https://sto… app   DayZ  The po… Mixed,… Mixed,… Dec 13… Bohemi… Bohemi…
    ## 5     5 https://sto… app   EVE … EVE On… Mixed,… Mostly… May 6,… CCP     CCP,CCP
    ## 6     6 https://sto… bund… Gran… Grand … NaN     NaN     NaN     Rockst… Rockst…
    ## # … with 11 more variables: popular_tags <chr>, game_details <chr>,
    ## #   languages <chr>, achievements <dbl>, genre <chr>, game_description <chr>,
    ## #   mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>,
    ## #   and abbreviated variable names ¹​desc_snippet, ²​recent_reviews,
    ## #   ³​all_reviews, ⁴​release_date, ⁵​developer, ⁶​publisher

``` r
glimpse(steam_games)
```

    ## Rows: 40,833
    ## Columns: 21
    ## $ id                       <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14…
    ## $ url                      <chr> "https://store.steampowered.com/app/379720/DO…
    ## $ types                    <chr> "app", "app", "app", "app", "app", "bundle", …
    ## $ name                     <chr> "DOOM", "PLAYERUNKNOWN'S BATTLEGROUNDS", "BAT…
    ## $ desc_snippet             <chr> "Now includes all three premium DLC packs (Un…
    ## $ recent_reviews           <chr> "Very Positive,(554),- 89% of the 554 user re…
    ## $ all_reviews              <chr> "Very Positive,(42,550),- 92% of the 42,550 u…
    ## $ release_date             <chr> "May 12, 2016", "Dec 21, 2017", "Apr 24, 2018…
    ## $ developer                <chr> "id Software", "PUBG Corporation", "Harebrain…
    ## $ publisher                <chr> "Bethesda Softworks,Bethesda Softworks", "PUB…
    ## $ popular_tags             <chr> "FPS,Gore,Action,Demons,Shooter,First-Person,…
    ## $ game_details             <chr> "Single-player,Multi-player,Co-op,Steam Achie…
    ## $ languages                <chr> "English,French,Italian,German,Spanish - Spai…
    ## $ achievements             <dbl> 54, 37, 128, NA, NA, NA, 51, 55, 34, 43, 72, …
    ## $ genre                    <chr> "Action", "Action,Adventure,Massively Multipl…
    ## $ game_description         <chr> "About This Game Developed by id software, th…
    ## $ mature_content           <chr> NA, "Mature Content Description  The develope…
    ## $ minimum_requirements     <chr> "Minimum:,OS:,Windows 7/8.1/10 (64-bit versio…
    ## $ recommended_requirements <chr> "Recommended:,OS:,Windows 7/8.1/10 (64-bit ve…
    ## $ original_price           <dbl> 19.99, 29.99, 39.99, 44.99, 0.00, NA, 59.99, …
    ## $ discount_price           <dbl> 14.99, NA, NA, NA, NA, 35.18, 70.42, 17.58, N…

``` r
class(steam_games)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

Exploring the “flow_sample” dataset:

``` r
head(flow_sample)
```

    ## # A tibble: 6 × 7
    ##   station_id  year extreme_type month   day  flow sym  
    ##   <chr>      <dbl> <chr>        <dbl> <dbl> <dbl> <chr>
    ## 1 05BB001     1909 maximum          7     7   314 <NA> 
    ## 2 05BB001     1910 maximum          6    12   230 <NA> 
    ## 3 05BB001     1911 maximum          6    14   264 <NA> 
    ## 4 05BB001     1912 maximum          8    25   174 <NA> 
    ## 5 05BB001     1913 maximum          6    11   232 <NA> 
    ## 6 05BB001     1914 maximum          6    18   214 <NA>

``` r
glimpse(flow_sample)
```

    ## Rows: 218
    ## Columns: 7
    ## $ station_id   <chr> "05BB001", "05BB001", "05BB001", "05BB001", "05BB001", "0…
    ## $ year         <dbl> 1909, 1910, 1911, 1912, 1913, 1914, 1915, 1916, 1917, 191…
    ## $ extreme_type <chr> "maximum", "maximum", "maximum", "maximum", "maximum", "m…
    ## $ month        <dbl> 7, 6, 6, 8, 6, 6, 6, 6, 6, 6, 6, 7, 6, 6, 6, 7, 5, 7, 6, …
    ## $ day          <dbl> 7, 12, 14, 25, 11, 18, 27, 20, 17, 15, 22, 3, 9, 5, 14, 5…
    ## $ flow         <dbl> 314, 230, 264, 174, 232, 214, 236, 309, 174, 345, 185, 24…
    ## $ sym          <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…

``` r
class(flow_sample)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

Exploring the “building_permits” dataset:

``` r
head(building_permits)
```

    ## # A tibble: 6 × 14
    ##   permit_nu…¹ issue_date proje…² type_…³ address proje…⁴ build…⁵ build…⁶ appli…⁷
    ##   <chr>       <date>       <dbl> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ## 1 BP-2016-02… 2017-02-01       0 Salvag… 4378 W… <NA>    <NA>     <NA>   Raffae…
    ## 2 BU468090    2017-02-01       0 New Bu… 1111 R… <NA>    <NA>     <NA>   MAX KE…
    ## 3 DB-2016-04… 2017-02-01   35000 Additi… 3732 W… <NA>    <NA>     <NA>   Peter …
    ## 4 DB-2017-00… 2017-02-01   15000 Additi… 88 W P… <NA>    Mercur… "88 W … Aaron …
    ## 5 DB452250    2017-02-01  181178 New Bu… 492 E … <NA>    082016… "3559 … John H…
    ## 6 BP-2016-01… 2017-02-02       0 Salvag… 3332 W… <NA>    <NA>     <NA>   Shalin…
    ## # … with 5 more variables: applicant_address <chr>, property_use <chr>,
    ## #   specific_use_category <chr>, year <dbl>, bi_id <dbl>, and abbreviated
    ## #   variable names ¹​permit_number, ²​project_value, ³​type_of_work,
    ## #   ⁴​project_description, ⁵​building_contractor, ⁶​building_contractor_address,
    ## #   ⁷​applicant

``` r
glimpse(building_permits)
```

    ## Rows: 20,680
    ## Columns: 14
    ## $ permit_number               <chr> "BP-2016-02248", "BU468090", "DB-2016-0445…
    ## $ issue_date                  <date> 2017-02-01, 2017-02-01, 2017-02-01, 2017-…
    ## $ project_value               <dbl> 0, 0, 35000, 15000, 181178, 0, 15000, 0, 6…
    ## $ type_of_work                <chr> "Salvage and Abatement", "New Building", "…
    ## $ address                     <chr> "4378 W 9TH AVENUE, Vancouver, BC V6R 2C7"…
    ## $ project_description         <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
    ## $ building_contractor         <chr> NA, NA, NA, "Mercury Contracting Ltd", "08…
    ## $ building_contractor_address <chr> NA, NA, NA, "88 W PENDER ST  \r\nUnit 2069…
    ## $ applicant                   <chr> "Raffaele & Associates DBA: Raffaele and A…
    ## $ applicant_address           <chr> "2642 East Hastings\r\nVancouver, BC  V5K …
    ## $ property_use                <chr> "Dwelling Uses", "Dwelling Uses", "Dwellin…
    ## $ specific_use_category       <chr> "One-Family Dwelling", "Multiple Dwelling"…
    ## $ year                        <dbl> 2017, 2017, 2017, 2017, 2017, 2017, 2017, …
    ## $ bi_id                       <dbl> 524, 535, 539, 541, 543, 546, 547, 548, 54…

``` r
class(building_permits)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

Exploring the “vancouver_trees” dataset:

``` r
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

<!----------------------------------------------------------------------------->

1.3 Now that you’ve explored the 4 datasets that you were initially most
interested in, let’s narrow it down to 2. What lead you to choose these
2? Briefly explain your choices below, and feel free to include any code
in your explanation.

<!-------------------------- Start your work below ---------------------------->

I will work with either the “vancouver_trees” or “steam_games” datasets.
I chose these because they seem to contain the most amount of
information within their datasets, as well as missing and potentially
untidy data. By working with these datasets I am hoping to improve and
challenge myself with these aspects of data analysis.
<!----------------------------------------------------------------------------->

1.4 Time for the final decision! Going back to the beginning, it’s
important to have an *end goal* in mind. For example, if I had chosen
the `titanic` dataset for my project, I might’ve wanted to explore the
relationship between survival and other variables. Try to think of 1
research question that you would want to answer with each dataset. Note
them down below, and make your final choice based on what seems more
interesting to you!

<!-------------------------- Start your work below ---------------------------->

I think that trying to determine what the biggest influences are on
video game success would be an interesting question to try and answer. I
am initially unsure of how much what operating system the game runs on
impacts a users experience, whether the cost of the game is a large
factor, or if a certain time f year aligns with best sales and/or
reviews.

For the “vancouver_trees” dataset, I would be curious to explore what
species of trees do best in different parts of the city, and what impact
urbanization is having on specific species as well.

Between these two datasets, I think I am most interested in working with
“vancouver_trees” trying to determine how neighbourhood and plant area
affecting the health of trees in relation to height and diameter.
<!----------------------------------------------------------------------------->

# Important note

Read Tasks 2 and 3 *fully* before starting to complete either of them.
Probably also a good point to grab a coffee to get ready for the fun
part!

This project is semi-guided, but meant to be *independent*. For this
reason, you will complete tasks 2 and 3 below (under the **START HERE**
mark) as if you were writing your own exploratory data analysis report,
and this guidance never existed! Feel free to add a brief introduction
section to your project, format the document with markdown syntax as you
deem appropriate, and structure the analysis as you deem appropriate.
Remember, marks will be awarded for completion of the 4 tasks, but 10
points of the whole project are allocated to a reproducible and clean
analysis. If you feel lost, you can find a sample data analysis
[here](https://www.kaggle.com/headsortails/tidy-titarnic) to have a
better idea. However, bear in mind that it is **just an example** and
you will not be required to have that level of complexity in your
project.

# Task 2: Exploring your dataset (15 points)

If we rewind and go back to the learning objectives, you’ll see that by
the end of this deliverable, you should have formulated *4* research
questions about your data that you may want to answer during your
project. However, it may be handy to do some more exploration on your
dataset of choice before creating these questions - by looking at the
data, you may get more ideas. **Before you start this task, read all
instructions carefully until you reach START HERE under Task 3**.

2.1 Complete *4 out of the following 8 exercises* to dive deeper into
your data. All datasets are different and therefore, not all of these
tasks may make sense for your data - which is why you should only answer
*4*. Use *dplyr* and *ggplot*.

1.  Plot the distribution of a numeric variable. (DONE)
2.  Create a new variable based on other variables in your data (only if
    it makes sense)
3.  Investigate how many missing values there are per variable. Can you
    find a way to plot this? (DONE)
4.  Explore the relationship between 2 variables in a plot.
    “height_range_id” vs “plant_area”
5.  Filter observations in your data according to your own criteria.
    Think of what you’d like to explore - again, if this was the
    `titanic` dataset, I may want to narrow my search down to passengers
    born in a particular year… “filter into neightbourhoods”
6.  Use a boxplot to look at the frequency of different observations
    within a single variable. You can do this for more than one variable
    if you wish! “species”
7.  Make a new tibble with a subset of your data, with variables and
    observations that you are interested in exploring. (DONE)
8.  Use a density plot to explore any of your variables (that are
    suitable for this type of plot). (DONE)

2.2 For each of the 4 exercises that you complete, provide a *brief
explanation* of why you chose that exercise in relation to your data (in
other words, why does it make sense to do that?), and sufficient
comments for a reader to understand your reasoning and code.

<!-------------------------- Start your work below ---------------------------->

The first thing I want to do to this dataset is determine how many
missing values there are per variable. This will be valuable information
to have for numeric columns where I may want to take mean values (for
example diameter of trees), as well as knowing where I may need to
utilize “na.rm = TRUE” when manipulating certain variables.

``` r
na_vals <- vancouver_trees %>% 
  summarise(across(everything(), ~ sum(is.na(.x))))
```

``` r
#creating a dataframe that takes the sum of NA values in each column in vancouver_trees
null_values <- enframe(colSums(is.na(vancouver_trees)))


#plotting the count of NA values in each column
ggplot(null_values, aes(name, value)) +
  geom_col() +
  coord_flip()
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

From this we can see that 5 out of the 20 variables in this dataset
contain missing data.

Next, I want to explore the density distribution of height_range_id in
each neighborhood in Vancouver. This plot will allow me to quickly see
which neighbourhoods contain the largest distribution of tree heights
and could be used to further investigate what parts of the city are
better suited to growing taller trees.

``` r
#Plotting height_range_id versus neighbourhood in density ridges plot
ggplot(vancouver_trees, aes(height_range_id, neighbourhood_name)) +
  ggridges::geom_density_ridges()
```

    ## Picking joint bandwidth of 0.214

![](mini-project-1_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

The next thing I want to do is create a subset of my data that contains
the most relevant information related to the questions I want to answer
for the time being. If it turns out I change some of my research
questions or realize that I might need some of the data in the original
dataframe, then I can come back and edit this code chunk.At the time
being, data related to individual tree id, street name, street block,
and street number data are not that interesting to me.

``` r
#creating a new tibble where I am selecting all columns except for columns related to tree id, street name, street block, and street number

vancouver_trees_new <- select(vancouver_trees, -c(tree_id,civic_number,std_street,assigned,on_street_block,on_street,street_side_name))

glimpse(vancouver_trees_new)
```

    ## Rows: 146,611
    ## Columns: 13
    ## $ genus_name         <chr> "ULMUS", "ZELKOVA", "STYRAX", "FRAXINUS", "ACER", "…
    ## $ species_name       <chr> "AMERICANA", "SERRATA", "JAPONICA", "AMERICANA", "C…
    ## $ cultivar_name      <chr> "BRANDON", NA, NA, "AUTUMN APPLAUSE", NA, "CHANTICL…
    ## $ common_name        <chr> "BRANDON ELM", "JAPANESE ZELKOVA", "JAPANESE SNOWBE…
    ## $ root_barrier       <chr> "N", "N", "N", "N", "N", "N", "N", "N", "N", "N", "…
    ## $ plant_area         <chr> "N", "N", "4", "4", "4", "B", "6", "6", "3", "3", "…
    ## $ neighbourhood_name <chr> "MARPOLE", "MARPOLE", "KENSINGTON-CEDAR COTTAGE", "…
    ## $ height_range_id    <dbl> 2, 4, 3, 4, 2, 2, 3, 3, 2, 2, 2, 5, 3, 2, 2, 2, 2, …
    ## $ diameter           <dbl> 10.00, 10.00, 4.00, 18.00, 9.00, 5.00, 15.00, 14.00…
    ## $ curb               <chr> "N", "N", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "…
    ## $ date_planted       <date> 1999-01-13, 1996-05-31, 1993-11-22, 1996-04-29, 19…
    ## $ longitude          <dbl> -123.1161, -123.1147, -123.0846, -123.0870, -123.08…
    ## $ latitude           <dbl> 49.21776, 49.21776, 49.23938, 49.23469, 49.23894, 4…

Finally, I want to take a look at the distribution of height_range_id
since this is a variable that is of interest to me for some of my
potential research questions.

``` r
#using the new "vancouver_trees_new tibble and creating a histogram to look at distribution of height_range_id
vancouver_trees_new %>%
  ggplot(aes(height_range_id)) +
  geom_histogram(binwidth = 0.5)
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

<!----------------------------------------------------------------------------->

# Task 3: Write your research questions (5 points)

So far, you have chosen a dataset and gotten familiar with it through
exploring the data. Now it’s time to figure out 4 research questions
that you would like to answer with your data! Write the 4 questions and
any additional comments at the end of this deliverable. These questions
are not necessarily set in stone - TAs will review them and give you
feedback; therefore, you may choose to pursue them as they are for the
rest of the project, or make modifications!

<!--- *****START HERE***** --->

1.  How does plant_area affect the height of trees?

2.  What size (height) of trees is most common in Vancouver?

3.  What is the relationship between height_range_id and diameter?

4.  Are root barriers used more in certain neighbourhoods?

<!----------------------------------------------------------------------------->

# Task 4: Process and summarize your data (13 points)

From Task 2, you should have an idea of the basic structure of your
dataset (e.g. number of rows and columns, class types, etc.). Here, we
will start investigating your data more in-depth using various data
manipulation functions.

### 1.1 (10 points)

Now, for each of your four research questions, choose one task from
options 1-4 (summarizing), and one other task from 4-8 (graphing). You
should have 2 tasks done for each research question (8 total). Make sure
it makes sense to do them! (e.g. don’t use a numerical variables for a
task that needs a categorical variable.). Comment on why each task helps
(or doesn’t!) answer the corresponding research question.

Ensure that the output of each operation is printed!

**Summarizing:**

1.  Compute the *range*, *mean*, and *two other summary statistics* of
    **one numerical variable** across the groups of **one categorical
    variable** from your data.
2.  Compute the number of observations for at least one of your
    categorical variables. Do not use the function `table()`!
3.  Create a categorical variable with 3 or more groups from an existing
    numerical variable. You can use this new variable in the other
    tasks! *An example: age in years into “child, teen, adult, senior”.*
4.  Based on two categorical variables, calculate two summary statistics
    of your choosing.

**Graphing:**

5.  Create a graph out of summarized variables that has at least two
    geom layers.
6.  Create a graph of your choosing, make one of the axes logarithmic,
    and format the axes labels so that they are “pretty” or easier to
    read.
7.  Make a graph where it makes sense to customize the alpha
    transparency.
8.  Create 3 histograms out of summarized variables, with each histogram
    having different sized bins. Pick the “best” one and explain why it
    is the best.

Make sure it’s clear what research question you are doing each operation
for!

<!------------------------- Start your work below ----------------------------->

Investigating research question 1 by computing the number of
observations in the “plant_area” categorical variable. This can help
tell me what the distribution of each type of plant area is and can then
hopefully be used to answer how plant area type impacts the overall tree
height.

``` r
#First create a tibble which shows the count of each type of observation in the plant_area variable

df <- vancouver_trees %>%
  count(plant_area)

#There are duplicates of some observations in the form of the same letter representation in upper and lower case. In order to fix this start by making all characters upper case

pa_count <- mutate_all(df, .funs = toupper) 

#Now change the "n" column in this tibble to from character to numeric so we can apply the sum function to add up the rows which are identical

pa_count$n <- as.numeric(as.character(pa_count$n))

pa_count_clean <- pa_count %>%
  group_by(plant_area) %>%
  summarise(n = sum(n))

print(pa_count_clean)
```

    ## # A tibble: 45 × 2
    ##    plant_area     n
    ##    <chr>      <dbl>
    ##  1 0              3
    ##  2 1             33
    ##  3 10         20467
    ##  4 11          1235
    ##  5 12          9198
    ##  6 13           290
    ##  7 14           422
    ##  8 15          1617
    ##  9 16           215
    ## 10 17           102
    ## # … with 35 more rows

``` r
#further splitting up the plant_area variable fo further analysis and tidying - for later analysis
#char_plant_area <- df_2_clean %>%
#  arrange(desc(plant_area)) %>%
#  slice(1:8)

#numeric_plant_area <- df_2_clean %>%
#  arrange(desc(plant_area)) %>%
#  slice(9:45)

#numeric_plant_area$plant_area <- as.numeric(as.character(numeric_plant_area$plant_area))
```

To further address research question 1 I will plot the number of
observations of each plant area type against the height of each tree and
see what the relationship between the two variable is. Because of the
large counts for observations, I will use a log scale on the x-axis ().
This is a semi-useful graph but it could be better by grouping the plant
area into further categories so the y-axis isnt so cluttered.

``` r
ggplot(pa_count_clean, aes(n, plant_area)) +
  geom_col() +
  scale_x_log10()
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

I will now investigate research question 3. First I want to create
summary statistics for the numerical variable height_range_id for each
type of tree. This summary of height_range_id is helpful for being able
to glimpse at a variety of different summary statistics for tree species
heights, but ultimately I am only interested in the means for this
research question.

``` r
vancouver_trees %>%
  group_by(species_name) %>%
  summarise(mean = mean(height_range_id, na.rm = TRUE),
            sd = sd(height_range_id, na.rm = TRUE),
            range = max(height_range_id, na.rm = TRUE) - min(height_range_id, na.rm = TRUE),
            median = median(height_range_id, na.rm = TRUE))
```

    ## # A tibble: 283 × 5
    ##    species_name    mean     sd range median
    ##    <chr>          <dbl>  <dbl> <dbl>  <dbl>
    ##  1 ABIES           3.28  1.67      8    3  
    ##  2 ACERIFOLIA   X  4.63  1.92      8    4  
    ##  3 ACUMINATA       2.57  0.535     1    3  
    ##  4 ACUTISSIMA      2.76  1.06      6    3  
    ##  5 AILANTHIFOLIA   5     1         2    5  
    ##  6 ALBA            3.12  1.82      6    3.5
    ##  7 ALBA-SINENSIS   2.67  0.577     1    3  
    ##  8 ALNIFOLIA       1.77  0.706     6    2  
    ##  9 ALPINUM         2    NA         0    2  
    ## 10 ALTISSIMA       3.5   1.73      4    4  
    ## # … with 273 more rows

Next, I will find the means of both variables and plot them against one
another. This should help give me an answer as to whether there is a
relationship between tree height and tree diameter across all tree
species.

``` r
#Create a new tibble which holds the species names of trees and the means of their height and diameters
mean_tree_dims <- vancouver_trees %>%
  group_by(species_name) %>%
  summarise(mean_height = mean(height_range_id, na.rm = TRUE), 
            mean_diameter = mean(diameter, na.rm = TRUE))

#Plot the mean height vs the mean diameter - since there are a large amount of data points clustered in the lower mean diameter and height section of the chart, decreasing the alpha transparency can help visualize just how densly populated that area is
ggplot(mean_tree_dims, aes(mean_height, mean_diameter)) +
  geom_point(alpha = 0.4)
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

To investigate my research question 4 I will start by taking the
categorical variables of “neighbourhood_name” and “root_barrier” and
counting the number of trees per neighbourhood that have, and do not
have, root barriers. This will quickly let me know if certain
neighbourhoods have more trees with or without root barriers

``` r
count_rb_per_neighbourhood <- vancouver_trees %>%
  group_by(neighbourhood_name) %>%
  filter(root_barrier == 'Y') %>%
  summarise(n = n())

count_rb_per_neighbourhood
```

    ## # A tibble: 22 × 2
    ##    neighbourhood_name           n
    ##    <chr>                    <int>
    ##  1 ARBUTUS-RIDGE              201
    ##  2 DOWNTOWN                   326
    ##  3 DUNBAR-SOUTHLANDS          207
    ##  4 FAIRVIEW                   248
    ##  5 GRANDVIEW-WOODLAND         534
    ##  6 HASTINGS-SUNRISE          1055
    ##  7 KENSINGTON-CEDAR COTTAGE   597
    ##  8 KERRISDALE                 252
    ##  9 KILLARNEY                  495
    ## 10 KITSILANO                  442
    ## # … with 12 more rows

``` r
count_no_rb_per_neighbourhood <- vancouver_trees %>%
  group_by(neighbourhood_name) %>%
  filter(root_barrier == 'N') %>%
  summarise(n = n())

count_no_rb_per_neighbourhood
```

    ## # A tibble: 22 × 2
    ##    neighbourhood_name           n
    ##    <chr>                    <int>
    ##  1 ARBUTUS-RIDGE             4968
    ##  2 DOWNTOWN                  4833
    ##  3 DUNBAR-SOUTHLANDS         9208
    ##  4 FAIRVIEW                  3754
    ##  5 GRANDVIEW-WOODLAND        6169
    ##  6 HASTINGS-SUNRISE          9492
    ##  7 KENSINGTON-CEDAR COTTAGE 10445
    ##  8 KERRISDALE                6684
    ##  9 KILLARNEY                 5653
    ## 10 KITSILANO                 7673
    ## # … with 12 more rows

To address research question 2, I will create a new categorical variable
out of an existing numeric variable “height_range_id”. This can help
group the observations together and take the previous height range id’s
into categories that are more easily interpreted.

``` r
#Creating new categorical variable "height_bins" which groups together different tree heights into categories of xsmall, small, medium, large, and xlarge trees
height_cats <- vancouver_trees %>%
  mutate(height_bins = cut(height_range_id, breaks = c(0,2,4,6,8,10), labels = c("xsmall", "small", "medium", "large", "xlarge")))

height_cats
```

    ## # A tibble: 146,611 × 21
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
    ## # … with 146,601 more rows, 12 more variables: plant_area <chr>,
    ## #   on_street_block <dbl>, on_street <chr>, neighbourhood_name <chr>,
    ## #   street_side_name <chr>, height_range_id <dbl>, diameter <dbl>, curb <chr>,
    ## #   date_planted <date>, longitude <dbl>, latitude <dbl>, height_bins <fct>,
    ## #   and abbreviated variable names ¹​std_street, ²​genus_name, ³​species_name,
    ## #   ⁴​cultivar_name, ⁵​common_name, ⁶​assigned, ⁷​root_barrier

Next, I will create a histogram that groups together the count of each
unique observation in the new categorical variable “height_bins” so I
can see what category of tree height is most common in Vancouver.

``` r
#Creating 3 histograms from "counts" of new height_bins categorical variable (used geom_col to create histogram because variable is discrete) with different binwidths
height_cats %>%
  group_by(height_bins) %>%
  summarize(n = n(), na.rm = TRUE) %>%
  ggplot(aes(height_bins, n)) +
  geom_col(width = 2)
```

    ## Warning: position_stack requires non-overlapping x intervals

![](mini-project-1_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
height_cats %>%
  group_by(height_bins) %>%
  summarize(n = n(), na.rm = TRUE) %>%
  ggplot(aes(height_bins, n)) +
  geom_col(width = 0.5)
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-17-2.png)<!-- -->

``` r
height_cats %>%
  group_by(height_bins) %>%
  summarize(n = n(), na.rm = TRUE) %>%
  ggplot(aes(height_bins, n)) +
  geom_col(width = 0.1)
```

![](mini-project-1_files/figure-gfm/unnamed-chunk-17-3.png)<!-- -->

``` r
# Based on the resulting graphs, the binwidth of 0.5 seems like the best option to display this data. A binwidth of 2 is too wide and the columns overlap one another making it hard to distinguish between each bin, and the bunwidth of 0.1 is very narrow, leaving too much blank space on the graph.
```

<!----------------------------------------------------------------------------->

### 1.2 (3 points)

Based on the operations that you’ve completed, how much closer are you
to answering your research questions? Think about what aspects of your
research questions remain unclear. Can your research questions be
refined, now that you’ve investigated your data a bit more? Which
research questions are yielding interesting results?

<!-------------------------- Start your work below ---------------------------->

I am slightly closer to answering some of my research questions, however
I need to do some further tidying of my data to come to any conclusions.
My research questions 1 and 2 seem to be yeilding interesting results
and wit hmore tidying of this data I think I would be able to get closer
to answering these questions. Research questions 3 and 4 seem to be a
bit more straight forward in terms of finding answers to these questions
with less intensive manipulation of the dataset, so I might need to
revise these questions and think of some better research questions. One
avenue I could explore is looking at a subset of the data related to the
most common tree species, or the largest (in height or diameter) trees.
<!----------------------------------------------------------------------------->

### Attribution

Thanks to Icíar Fernández Boyano for mostly putting this together, and
Vincenzo Coia for launching.
