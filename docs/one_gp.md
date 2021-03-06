Quantify a single distribution
================
Guillaume A. Rousselet
2020-07-10

  - [References](#references)

``` r
library(cowplot)
library(ggplot2)
```

Given a sufficiently large sample size, a single distribution can be
quantified in more details, by including confidence intervals of the
quantiles. The figure below illustrates such detailed representation
using event-related potential onsets from 120 participants (Bieniek et
al., 2016). In that case, the earliest latencies are particularly
interesting, so it is useful to quantify the first deciles in addition
to the median.

``` r
#> --------------------------------------
#> Inference on the deciles of ERP onsets
#> --------------------------------------
#> load data:
load("./data/onsets.RData") # onsets

#> -----------------------------------
#> Panel A: scatterplot + deciles
#> -----------------------------------

df <- mkt1(onsets) # make data frame

#> scatterplot
p <- plot_scat2(df,
  xlabel = "",
  ylabel = "ERP onsets in ms",
  alpha = 1,
  shape = 21,
  colour = "grey10",
  fill = "grey90",
  size = 3) + 
  theme(axis.text.y = element_blank(),
        axis.title.y = element_blank(),
        axis.ticks.y = element_blank())
 
#> add vertical lines marking the deciles
p <- plot_hd_bars(p, 
                  q_seq = seq(.1,.9,.1),
                  col = "black",
                  q_size = 0.5,
                  md_size = 1.5,
                  alpha = 1) 

#> flip axes
#> one ERP onsets at 284 ms is masked
p <- p + coord_flip(ylim = c(50,200)) 
# p

#> ---------------------------------------
#> Panel B: deciles + confidence intervals
#> ---------------------------------------

#> compute deciles + confidence intervals
set.seed(7)
out <- quantiles_pbci(onsets,q=seq(1,9)/10,nboot=2000,alpha=0.05)

#> decile plot
decile_plot <- plot_hd_ci(data=out,plotzero=TRUE,label.x="ERP onsets in ms",
                           hjust=-.05,vjust=.5,size_text=5,
                           colour_q = "grey10",fill_q = "grey90",
                           colour_line = "grey10", linetype_line = 1, size_line = 1) +
                scale_y_continuous(limits=c(50, 140),breaks=seq(50,140,10))
# decile_plot

#> combine scatterplots + decile plot
cowplot::plot_grid(p, decile_plot,
                             labels=c("A", "B"),
                             ncol = 1,
                             nrow = 2,
                             rel_heights = c(1, 1.5),
                             label_size = 20,
                             hjust = -0.5,
                             scale=.95,
                             align = "v")
```

![](one_gp_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

**(A)** The scatterplot illustrates the distribution of event-related
potential (ERP) onsets in ms. Points were scattered along the y-axis to
avoid overlap. Vertical lines indicate the deciles, with the median
shown with a thicker line. One outlier (\> 200 ms) is not shown.

**(B)** Deciles and their 95% percentile bootstrap confidence intervals.
The vertical black line marks the median.

We can also answer useful questions, such as the proportion of onsets
less than 100 ms, which is 0.61.

# References

Bieniek, M.M., Bennett, P.J., Sekuler, A.B. & Rousselet, G.A. (2016) **A
robust and representative lower bound on object processing speed in
humans.** The European journal of neuroscience, 44, 1804-1814.
\[[article](https://www.ncbi.nlm.nih.gov/pubmed/26469359)\]
\[[reproducibility
package](https://figshare.com/articles/Face_noise_ERP_onsets_from_194_recording_sessions/1588513)\]

Rousselet, G.A., Pernet, C.R. & Wilcox, R.R. (2017) **Beyond differences
in means: robust graphical methods to compare two groups in
neuroscience.** The European journal of neuroscience, 46, 1738-1748.
\[[article](https://onlinelibrary.wiley.com/doi/abs/10.1111/ejn.13610)\]
\[[preprint](https://www.biorxiv.org/content/early/2017/05/16/121079)\]
\[[reproducibility
package](https://figshare.com/articles/Modern_graphical_methods_to_compare_two_groups_of_observations/4055970)\]
