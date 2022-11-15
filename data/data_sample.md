Data Sample
================
2022-11-03

-   <a href="#equaldex-data" id="toc-equaldex-data">Equaldex Data</a>
-   <a href="#map-data" id="toc-map-data">MAP Data</a>
-   <a href="#pdf" id="toc-pdf">PDF</a>

``` r
library(tidyverse)
library(rvest)
library(pdftools)
```

``` r
# build a simple tibble to connect state name and abbreviations, used for filtering
States <- tibble(State = state.name, Abbreviation = state.abb)
```

# Equaldex Data

Save the webpage html for easier access in following codes:

``` r
Equaldex <- read_html("https://www.equaldex.com/equality-index/united-states")
```

Scrape the table and save as a tibble.

``` r
Equaldex_raw <- Equaldex %>% 
  html_element(xpath ='//*[@id="content"]/div[3]/table') %>% 
  html_table()
head(Equaldex_raw)
```

    ## # A tibble: 6 × 4
    ##   `State and Territory` `Equality Index` `Legal Index` `Public Opinion Index`
    ##   <chr>                 <chr>            <chr>         <chr>                 
    ## 1 1. Vermont            86 / 100         98 / 100      74 / 100              
    ## 2 2. Massachusetts      86               98            74                    
    ## 3 3. Connecticut        85               98            71                    
    ## 4 4. New Hampshire      85               98            71                    
    ## 5 5. Rhode Island       84               98            70                    
    ## 6 6. Washington, D.C.   83               98            68

Tidy up the data.

``` r
Equaldex_df <- Equaldex %>% 
  html_element(xpath ='//*[@id="content"]/div[3]/table') %>% 
  html_table() %>% 
  # separating column data
  separate('State and Territory', into = c('Rank', 'State'), sep = "\\. ", convert = T) %>% 
  separate('Equality Index', into = c('Equality_Index', 'Max1'), convert = T) %>% 
  separate('Legal Index', into = c('Legal_Index', 'Max2'), convert = T) %>% 
  separate('Public Opinion Index', into = c('Public_Opinion_Index', 'Max3'), convert = T) %>% 
  select(-c(Max1, Max2, Max3)) %>%  #removing unnecessary columns 
  mutate('Total_Index'= (Equality_Index + Legal_Index + Public_Opinion_Index) / 3) %>% #making average colummn to compare to MAP data
  semi_join(States, by = 'State')
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 51 rows [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].
    ## Expected 2 pieces. Missing pieces filled with `NA` in 51 rows [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].
    ## Expected 2 pieces. Missing pieces filled with `NA` in 51 rows [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

``` r
head(Equaldex_df)
```

    ## # A tibble: 6 × 6
    ##    Rank State         Equality_Index Legal_Index Public_Opinion_Index Total_In…¹
    ##   <int> <chr>                  <int>       <int>                <int>      <dbl>
    ## 1     1 Vermont                   86          98                   74       86  
    ## 2     2 Massachusetts             86          98                   74       86  
    ## 3     3 Connecticut               85          98                   71       84.7
    ## 4     4 New Hampshire             85          98                   71       84.7
    ## 5     5 Rhode Island              84          98                   70       84  
    ## 6     7 New York                  82          98                   67       82.3
    ## # … with abbreviated variable name ¹​Total_Index

# MAP Data

Save the webpage html for easier access in following codes:

``` r
MAP <- read_html("https://www.lgbtmap.org/equality-maps")
```

Scrape the table and save as a tibble.

``` r
MAP_raw <- MAP %>% 
  html_element(xpath = '//*[@id="map-4"]/div/table') %>% 
  html_table()
head(MAP_raw)
```

    ## # A tibble: 6 × 13
    ##      X1 X2     X3    X4    X5    X6    X7    X8    X9    X10   X11   X12   X13  
    ##   <int> <chr>  <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr> <chr>
    ## 1    NA State  ""    Rela… Non–… Reli… LGBT… Heal… Crim… Iden… Sexu… Gend… Over…
    ## 2     1 Alaba… "SO"  1/6   0/4.5 -2.5… -1/5  0.5/2 0/3   --    -2.00 -6.50 -8.50
    ## 3     1 Alaba… "GI"  0/1   0/4.5 -2.5… -3/5  -1/4… 0/3   0/4   -2.00 -6.50 -8.50
    ## 4     2 Alaska "SO"  3/6   3.5/… 0/-3… 2/5   0.5/2 0.75… --    9.75  9.50  19.25
    ## 5     2 Alaska "GI"  1/1   3.5/… 0/-2… 2/5   1.5/… -0.2… 1.75… 9.75  9.50  19.25
    ## 6     3 Ameri… "SO"  1/6   0/4.5 0/-3… 0/5   0/2   0/3   --    1.00  -1.00 0.00

Tidy up the data.

``` r
MAP_df <- MAP %>% 
  html_element(xpath = '//*[@id="map-4"]/div/table') %>% 
  html_table(header = T) %>% # works to rename, how to make it proper titles, how to add missing titles?
  rename('Alpha_Rank' = 1, 'Measured_Category' = 3) %>%  #renaming empty columns
  select(-Alpha_Rank) %>% #removes unnecessary initial column that numbered state positions
  semi_join(States, by = 'State') %>% 
  #separating the score and the scale
  separate('Relationship andParental Recognition', into = c('Relationship_and_Parental_Recognition', 'Relationship_and_Parental_Recognition_Scale'), sep = '/', convert = T) %>% 
  separate('Non–Discrimination', into = c('Non-Discrimination', 'Non-Discrimination_Scale'), sep = '/', convert = T) %>% 
  separate('Religious Exemption Laws', into = c('Religious_Exemption_Laws', 'Religious_Exemption_Laws_Scale'), sep = '/', convert = T) %>% 
  separate('LGBT Youth', into = c('LGBT_Youth', 'LGBT_Youth_Scale'), sep = '/', convert = T) %>% 
  separate('Healthcare', into = c('Healthcare', 'Healthcare_Scale'), sep = '/', convert = T) %>% 
  separate('CriminalJustice', into = c('Criminal_Justice', 'Criminal_Justice_Scale'), sep = '/', convert = T) %>% 
  separate('IdentityDocuments', into = c('Identity_Documents', 'Identity_Documents_Scale'), sep = '/', convert = T)
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 50 rows [1, 3, 5,
    ## 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39, ...].

``` r
head(MAP_df)
```

    ## # A tibble: 6 × 19
    ##   State  Measu…¹ Relat…² Relat…³ Non-D…⁴ Non-D…⁵ Relig…⁶ Relig…⁷ LGBT_…⁸ LGBT_…⁹
    ##   <chr>  <chr>     <dbl>   <int>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <int>
    ## 1 Alaba… SO          1         6    0        4.5    -2.5    -3.5      -1       5
    ## 2 Alaba… GI          0         1    0        4.5    -2.5    -2.5      -3       5
    ## 3 Alaska SO          3         6    3.5      4.5     0      -3.5       2       5
    ## 4 Alaska GI          1         1    3.5      4.5     0      -2.5       2       5
    ## 5 Arizo… SO          2.5       6    1.75     4.5    -1.5    -3.5       0       5
    ## 6 Arizo… GI          0         1    1.75     4.5    -1.5    -2.5      -1       5
    ## # … with 9 more variables: Healthcare <dbl>, Healthcare_Scale <dbl>,
    ## #   Criminal_Justice <dbl>, Criminal_Justice_Scale <int>,
    ## #   Identity_Documents <chr>, Identity_Documents_Scale <int>,
    ## #   `Sexual Orientation Policy Tally` <dbl>,
    ## #   `Gender Identity Policy Tally` <dbl>, `Overall Tally` <dbl>, and
    ## #   abbreviated variable names ¹​Measured_Category,
    ## #   ²​Relationship_and_Parental_Recognition, …

# PDF

Instructions pulled from:
<https://data.library.virginia.edu/reading-pdf-files-into-r-for-text-mining/>

The output is rather long, so I will hide it from view, but the
following code is used to generate the object.

``` r
# pro legislation from nebraska
pdf_text('https://nebraskalegislature.gov/FloorDocs/107/PDF/Intro/LB120.pdf') %>% 
  str_split("[\\r\\n]+") %>% 
  map(~ .x %>% 
        str_trim() %>% # trims leading white space
        str_squish() %>% # removes inner white space
        str_remove("^\\d+ ")) # remove line numbers
```

``` r
# anti from nebraska
pdf_text('https://nebraskalegislature.gov/FloorDocs/107/PDF/Intro/LB1077.pdf') %>% 
  str_split("[\\r\\n]+") %>% 
  map(~ .x %>% 
        str_trim() %>% 
        str_squish() %>% 
        str_remove("^\\d+ "))
```
