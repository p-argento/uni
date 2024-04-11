## chapter 1

```r
review_data %>% filter(product == "iRobot Roomba 650 for Pets") %>% summarize(stars_mean = mean(stars))

review_data %>% group_by(product) %>% summarize(stars_mean = mean(stars))


```


### facet_wrap
In the code you provided, `facet_wrap` is a function used in the `ggplot2` package in R. It is used to create a multi-panel plot by wrapping the facets (subsets of the data) into multiple panels. This allows you to create separate plots for different subsets of your data.
In `facet_wrap(~ sentiment, scales = "free")`
- `~ sentiment` specifies that you want to create separate panels for each level of the "sentiment" variable.
- `scales = "free"` specifies that each panel should have its own scale. This means that the scales (e.g., axes) for each panel will be determined independently based on the data in that panel, rather than being fixed across all panels.

### fct_reorder
In the provided code snippet, the `fct_reorder()` function from the `forcats` package is used to reorder the levels of the "word" variable based on the counts of each word. This function is typically used to reorder factor levels based on some summary statistic, such as counts, means, or medians.

Here's an example
```r
word_probs <- lda_topics %>%
# Keep the top 10 highest word probabilities by topic
group_by(topic) %>%
slice_max(beta, n=10) %>%
ungroup() %>%

# Create term2, a factor ordered by word probability
mutate(term2 = fct_reorder(term, beta))
# Plot term2 and the word probabilities
ggplot(word_probs, aes(x=term2, y=beta, fill=topic)) +
geom_col() +
# Facet the bar plot by topic
facet_wrap(~ topic, scales = "free") +
coord_flip()
```

## chapter 4

LDA -> Latent Dirichlet Allocation

### Document Term Matrix
```r
# Start with the tidied Twitter data
tidy_twitter %>%
# Count each word used in each tweet
count(word, tweet_id) %>%
# Use the word counts by tweet to create a DTM
cast_dtm(tweet_id, word, n)
```

