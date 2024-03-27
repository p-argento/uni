## chapter 1

```r
review_data %>% filter(product == "iRobot Roomba 650 for Pets") %>% summarize(stars_mean = mean(stars))

review_data %>% group_by(product) %>% summarize(stars_mean = mean(stars))


```