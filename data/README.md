# Data

Every file the notebook reads is here, so it runs offline. The source files are unchanged apart from reshaping and trimming to the columns used. All cleaning happens in the notebook.

## `un_cpi_syb65.csv`

Consumer price indices from the **UN Statistical Yearbook, 65th issue** (table SYB65_128, September 2022), downloaded from [UNdata](https://data.un.org/).

| Column | Meaning |
| --- | --- |
| `Area Code` | UN M49 country code |
| `Country` | Country or area name |
| `Year` | 2000, 2005, 2010, 2015, 2019, 2020 or 2021 |
| `Series` | `Consumer price index: General` or `Consumer price index: Food` |
| `Value` | Index value, usually 2010 = 100 |
| `Footnotes` | Notes on the value, including base-year changes and unit changes |
| `Source` | Where UNSD took the value from |

2,049 rows covering 202 countries and areas. The footnotes matter: some values are given in millions or billions, and some series change index base partway through. See section 1.2 of the notebook.

UNdata allows its data to be copied and redistributed free of charge, as long as UNdata is cited as the source.

## `wb_*.csv`

**World Bank World Development Indicators**, downloaded through the [World Bank API](https://datahelpdesk.worldbank.org/knowledgebase/articles/889392) (v2). The data was last updated on 11 November 2026. Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

| File | Indicator | Code |
| --- | --- | --- |
| `wb_inflation.csv` | Inflation, consumer prices (annual %) | `FP.CPI.TOTL.ZG` |
| `wb_unemployment.csv` | Unemployment, total (% of total labour force) (modelled ILO estimate) | `SL.UEM.TOTL.ZS` |
| `wb_gdp_growth.csv` | GDP growth (annual %) | `NY.GDP.MKTP.KD.ZG` |
| `wb_gdp_per_capita.csv` | GDP per capita (current US$) | `NY.GDP.PCAP.CD` |
| `wb_income_groups.csv` | Income group and region | — |

The four indicator files are wide tables: one row per country (`iso3`), one column per year from 2000 to 2023. Empty cells are missing values. Only countries are included; regional and income-group aggregates are left out.

`wb_income_groups.csv` has the World Bank's current classification of each country: `income_group` is `LIC` (low), `LMC` (lower-middle), `UMC` (upper-middle) or `HIC` (high), and `wb_region` is the World Bank region code.

## `country_codes.csv`

Country codes and regions from the [Datahub country-codes](https://github.com/datasets/country-codes) dataset, trimmed to the columns used:

| Column | Meaning | Original source |
| --- | --- | --- |
| `iso3` | ISO 3166-1 alpha-3 code | UN Statistics Division, M49 |
| `m49` | UN M49 numeric code | UN Statistics Division, M49 |
| `continent_code` | `AF`, `AS`, `EU`, `NA`, `SA`, `OC` or `AN` | [GeoNames](https://www.geonames.org/), CC BY 4.0 |
| `un_region`, `un_subregion`, `un_intermediate_region` | UN M49 regions | UN Statistics Division, M49 |

The notebook uses `m49` to link the UN data to ISO codes, `continent_code` for continents, and `un_subregion` to find Southern Asia. Continent data © GeoNames, used under CC BY 4.0. The UN Statistics Division doesn't publish an explicit licence for the M49 tables.

## `naturalearth_lowres/`

Low-resolution country boundaries from [Natural Earth](https://www.naturalearthdata.com/) (public domain), as previously shipped with geopandas. Used only to draw the world map.
