# <U-Mich - Arranging and Visualizing Data in R>

Mini project: Visualising and arranging data to analyse bank account ownership with respect to average income per country.

## Results
- We find that as income increases more individuals hold bank accounts
- Notably, the upper and lower middle income countries share a similar range from ~20-90% ownership

## How to run
```r
install.packages("renv"); renv::restore()

# 1) Generate data - Output: data/Indicator_Table.csv
Rscript scripts/IndicatorTable.R

# 2) Make plot - Output: plot/Account_Ownership.png
Rscript script/Account_Ownership.R
