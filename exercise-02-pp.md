# Pair Programming

In pair programming exercises learners work in pairs to solve exercises
together.

# Task 0: Load R packages

R Packages are typically loaded at the beginning of the document.

``` r
library(readr)
library(dplyr)
library(ggplot2)
```

# Task 1: Data import

**Fill in the blanks**

1.  A code-chunk has already been created.
2.  Import the CSV file titled ‘country_level_data_0.csv’, contained in
    the ‘raw_data’ directory with help of the `read_csv()` function.
3.  Use the assignment operator (`<-`) to assign the data to an object
    named `global_waste_data`.
4.  **Render:** Render this file to HTML
5.  **Add:** Open the Git pane and add all files to the staging area
    (*Tip: Tick off all checkboxes under column ‘Staged’*)
6.  **Commit:** Commit pending changes, add a meaningful commit message
7.  **Push:** Push changes to the remote repository (i.e. GitHub)

``` r
global_waste_data <- read_csv("data/raw_data/country_level_data_0.csv")
```

# Task 2: Data tidying (and some transformation)

**Fill in the blanks**

1.  A code-chunk has already been created.
2.  Start with the `global_waste_data` object
3.  Add the pipe operator (`%>%`) and on a new line use the `select()`
    function.
4.  Inside the parantheses write the names of the following variables:

-   country_name
-   iso3c
-   income_id
-   total_msw_total_msw_generated_tons_year
-   population_population_number_of_people

5.  Add the pipe operator (`%>%`) and on a new line use the `rename()`
    function.
6.  Rename two variables:

-   1)  from ‘total_msw_total_msw_generated_tons_year’ to
        ‘msw_tons_year’

-   2)  from ‘population_population_number_of_people’ to ‘population’

7.  Use the assignment operator (`<-`) to assign the data to an object
    named `global_waste_data_small`.
8.  Run the code contained in the code-chunk.
9.  Render
10. Add, Commit, Push

``` r
global_waste_data_small <- global_waste_data %>% 
  select(country_name, 
         iso3c, 
         income_id, 
         total_msw_total_msw_generated_tons_year, 
         population_population_number_of_people) %>% 
  rename(msw_tons_year = total_msw_total_msw_generated_tons_year,
         population = population_population_number_of_people) 
```

# Task 3: Data transformation

**Fill in the blanks**

1.  A code-chunk has already been created.
2.  Start with the `global_waste_data_small` object.
3.  Add the pipe operator (`%>%`) and on a new line use the `mutate()`
    function.
4.  Create a new variable named ‘capita_kg_year’ by dividing
    ‘msw_tons_year’ by ‘population’ and multiplied by \[?\].
5.  Run the code contained in the code-chunk.
6.  Render
7.  Add, Commit, Push

``` r
global_waste_data_kg_year <- global_waste_data_small %>% 
  mutate(capita_kg_year = msw_tons_year / population * 1000) %>% 
  mutate(income_id = factor(income_id, 
                            levels = c("HIC", "UMC", "LMC", "LIC")))
```

**Fill in the blanks**

# Task 4: Data visualisation

1.  A code-chunk has already been created.
2.  Use the `global_waste_data_kg_year` object
3.  Use aesthetic mappings to plot the income category on the x-axis and
    MSW generation per capita on the y-axis.
4.  Run the code contained in the code-chunk.
5.  Use a search engine of your choice to figure out how to remove the
    legend from the plot (**Tipp:** Add the name of the ggplot2 package
    to your query and focus on results from StackOverflow).
6.  Run the code contained in the code-chunk.
7.  Render
8.  Add, Commit, Push

``` r
ggplot(data = global_waste_data_kg_year,
       mapping = aes(x = income_id, 
                     y = capita_kg_year,
                     color = income_id)) +
  geom_boxplot(outlier.shape = NA) +
  geom_jitter(position = position_jitter(width = 0.1, height = 0),
              alpha = 1/4, size = 3) +
  labs(x = "income category",
       y = "MSW generation per capita [kg/yr]") +
  theme_minimal(base_size = 14) +
  theme(legend.position = "none")
```

![](exercise-02-pp_files/figure-gfm/unnamed-chunk-10-1.png)

# Task 5: Data communication

1.  In the YAML header, replace ‘html’ with ‘gfm’ (GitHub Flavoured
    Markdown)
2.  Render, and close the pop-up window that opens.
3.  Add, Commit, Push
4.  Open your GitHub repository for this exercise, and click on the file
    with the ‘.md’ ending (‘02-pp-data-science-lifecycle-solutions.md’)

# References