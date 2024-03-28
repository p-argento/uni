## chapter 1

```r
review_data %>% filter(product == "iRobot Roomba 650 for Pets") %>% summarize(stars_mean = mean(stars))

review_data %>% group_by(product) %>% summarize(stars_mean = mean(stars))


```


  
In the provided code snippet, the `fct_reorder()` function from the `forcats` package is used to reorder the levels of the "word" variable based on the counts of each word. This function is typically used to reorder factor levels based on some summary statistic, such as counts, means, or medians.

## chapter 4

LDA -> Latent Dirichlet Allocation