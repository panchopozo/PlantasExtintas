Trabajo con plantas extintas
================

# Introducción

En este documento trabajaremos la identidad de plantas que se encuentrán
extintas en silvestría o totalmente extintas según la
[*IUCN*](https://www.iucnredlist.org/es)

## Trabajando con los datos

Vamos a partir por cargar los paquetes necesarios para trabajar

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.3.3

    ## Warning: package 'tidyr' was built under R version 4.3.3

    ## Warning: package 'dplyr' was built under R version 4.3.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

Ahora voy a leer los datos con los que voy a trabajar:

``` r
library(readr)

plants <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-08-18/plants.csv")
```

    ## Rows: 500 Columns: 24
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (6): binomial_name, country, continent, group, year_last_seen, red_list...
    ## dbl (18): threat_AA, threat_BRU, threat_RCD, threat_ISGD, threat_EPM, threat...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Filtrando los datos para resolver el ejemplo 1

El codigo que voy a hacer ahora es para resolver el problema en el
siguiente slide, para poner dentro de la base de datos todos los datos
de Chile y solo usar la columnas para pais(“country”), especies
(“binomial_name”) y la categoría del IUCN (red_list_category)

``` r
Chile <- plants %>% 
  dplyr::filter(country == "Chile") %>% 
  dplyr::select(binomial_name, country, red_list_category)
Chile
```

    ## # A tibble: 2 × 3
    ##   binomial_name           country red_list_category  
    ##   <chr>                   <chr>   <chr>              
    ## 1 Santalum fernandezianum Chile   Extinct            
    ## 2 Sophora toromiro        Chile   Extinct in the Wild

## Resumen de especies por pais

``` r
Resumen <- plants %>%
  dplyr::filter(continent == "South America") %>% 
  group_by(country) %>% 
  summarise(n_species = n ())
Resumen
```

    ## # A tibble: 9 × 2
    ##   country             n_species
    ##   <chr>                   <int>
    ## 1 Argentina                   1
    ## 2 Bolivia                     1
    ## 3 Brazil                     10
    ## 4 Chile                       2
    ## 5 Colombia                    6
    ## 6 Ecuador                    52
    ## 7 Peru                        4
    ## 8 Trinidad and Tobago         6
    ## 9 Venezuela                   1
