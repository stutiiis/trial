Untitled
================
Stuti Subramani
2022-07-14

## TASK1- PREDICTION USING SUPERVISED ML

### Objective- To predict the marks obtained by the students based on the number of hours they study.

Dataset: <http://bit.ly/w-data>

#### IMPORTING REQUIRED LIBRARIES

``` r
library(readr)
library(ggplot2)
```

#### IMPORTING AND READING THE DATA

``` r
internship_data <- read_csv("https://raw.githubusercontent.com/AdiPersonalWorks/Random/master/student_scores%20-%20student_scores.csv")
```

    ## Rows: 25 Columns: 2
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (2): Hours, Scores
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
View(internship_data)
```

#### VISUALIZING THE DATA

``` r
ggplot(internship_data) + geom_point(mapping= aes(x=Hours,y=Scores)) +labs(title ="Number of hours studied vs percentage of marks", caption= "There is a positive linear relation between the number of hours studied and percentage of marks obtained by a student.")
```

![](s_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

#### APPLYING LINEAR REGRESSION

``` r
model= lm(internship_data$Scores~internship_data$Hours)
summary(model)
```

    ## 
    ## Call:
    ## lm(formula = internship_data$Scores ~ internship_data$Hours)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -10.578  -5.340   1.839   4.593   7.265 
    ## 
    ## Coefficients:
    ##                       Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)             2.4837     2.5317   0.981    0.337    
    ## internship_data$Hours   9.7758     0.4529  21.583   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 5.603 on 23 degrees of freedom
    ## Multiple R-squared:  0.9529, Adjusted R-squared:  0.9509 
    ## F-statistic: 465.8 on 1 and 23 DF,  p-value: < 2.2e-16

#### PLOTTING A REGRESSION LINE

``` r
ggplot(internship_data, aes(x=Hours,y=Scores)) + geom_point() +stat_smooth(method="lm",col="dodgerblue3") +labs(title= "Linear Model fitted tothe given data")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](s_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

#### PREDICTING THE SCORES

``` r
predicted_scores= predict(model,data.frame(internship_data$Hours))
```

#### COMPARING ACTUAL V/S PREDICTED

``` r
data.frame(predicted_scores,internship_data$Scores)
```

    ##    predicted_scores internship_data.Scores
    ## 1          26.92318                     21
    ## 2          52.34027                     47
    ## 3          33.76624                     27
    ## 4          85.57800                     75
    ## 5          36.69899                     30
    ## 6          17.14738                     20
    ## 7          92.42106                     88
    ## 8          56.25059                     60
    ## 9          83.62284                     81
    ## 10         28.87834                     25
    ## 11         77.75736                     85
    ## 12         60.16091                     62
    ## 13         46.47479                     41
    ## 14         34.74382                     42
    ## 15         13.23706                     17
    ## 16         89.48832                     95
    ## 17         26.92318                     30
    ## 18         21.05770                     24
    ## 19         62.11607                     67
    ## 20         74.82462                     69
    ## 21         28.87834                     30
    ## 22         49.40753                     54
    ## 23         39.63173                     35
    ## 24         69.93672                     76
    ## 25         78.73494                     86

#### WHAT WILL BE THE PREDICTED SCORE IF THE STUDENT STUDIES 9.25 HOURS A DAY?

``` r
    Hours=9.25
    Score= model$coefficients[1]+ model$coefficients[2]*Hours
    Score
```

    ## (Intercept) 
    ##    92.90985

According to the Regression model if the student studies for 9.25 hours
a day then he/she is likely to score 92.9 marks.

#### EVALUATING THE MODEL

``` r
    summary(model)$r.squared
```

    ## [1] 0.9529482

##### The R square value is 0.95. Therefore, the model has worked well for our data
