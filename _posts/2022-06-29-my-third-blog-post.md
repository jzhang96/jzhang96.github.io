My third blog
================
Jiyue Zhang
2022-06-29

# Feeling about R so far

I’m really impressed by how flexible the packages are, for example, the
ciTools that can add predict interval in plot.

Here is an example using ciTools package

``` r
library(ggplot2)
library(tidyr)
fit <- lm(dist ~ speed, data = cars)
cars <- cars %>% ciTools::add_pi(fit, names = c("lower", "upper"))
ggplot(cars, aes(x = speed, y = dist)) +
geom_point() +
geom_smooth(method = "lm", fill = "Blue") +
geom_ribbon(aes(ymin = lower, ymax = upper), alpha = 0.3, fill = "Red") +
ggtitle("Scatter Plot with 95% PI & 95% CI")
```

![](C:/Users/LAILA/Desktop/558/git/jzhang96.github.io/_posts/2022-06-29-my-third-blog-post_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->
