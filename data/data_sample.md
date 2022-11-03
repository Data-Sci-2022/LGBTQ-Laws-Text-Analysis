Data Sample
================
2022-11-03

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
    ## ✔ tibble  3.1.8     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.1
    ## ✔ readr   2.1.2     ✔ forcats 0.5.2
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

Save the webpage html for easier access in following codes:

``` r
Equaldex <- read_html("https://www.equaldex.com/equality-index/united-states")
```

Scrape the table and save as a tibble.

``` r
Equaldex_df <- Equaldex %>% 
  html_element(xpath ='//*[@id="content"]/div[3]/table') %>% 
  html_table()
head(Equaldex_df)
```

    ## # A tibble: 6 × 4
    ##   `State and Territory` `Equality Index` `Legal Index` `Public Opinion Index`
    ##   <chr>                 <chr>            <chr>         <chr>                 
    ## 1 1. Vermont            86 / 100         98 / 100      74 / 100              
    ## 2 2. Massachusetts      86               98            74                    
    ## 3 3. Connecticut        85               98            71                    
    ## 4 4. Rhode Island       84               98            70                    
    ## 5 5. New Hampshire      83               96            71                    
    ## 6 6. Washington, D.C.   83               98            68

Save the webpage html for easier access in following codes:

``` r
MAP <- read_html("https://www.lgbtmap.org/equality-maps")
```

Scrape the table and save as a tibble.

``` r
MAP_df <- MAP %>% 
  html_element(xpath = '//*[@id="map-4"]/div/table') %>% 
  html_table()
head(MAP_df)
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
