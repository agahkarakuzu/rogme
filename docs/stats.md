Statistical tests and measures of effect sizes in `rogme`
================
Guillaume A. Rousselet
2020-07-10

| Function                                                  | Description                                                                                |
| :-------------------------------------------------------- | :----------------------------------------------------------------------------------------- |
| `hd(x,q=.5)`                                              | Harrell-Davis quantile estimator                                                           |
| `hdseq(x, qseq=seq(0.1,0.9,0.1))`                         | Compute a sequence of quantiles                                                            |
| `allpdiff(x,y)`                                           | Calculate all pairwise differences between 2 vectors                                       |
| `allpdiff_hdpbci(x,y,alpha=.05,q=.5,nboot=600)`           | Compute percentile bootstrap confidence interval of the median of all pairwise differences |
| `pb2gen(x,y,alpha=.05, nboot=2000, est=hd)`               | Compare two independent groups using the percentile bootstrap - default estimator = `hd`   |
| `hdpbci(x,q=.5)`                                          | Compute percentile bootstrap confidence interval of the qth quantile                       |
| `quantiles_pbci(x,q=seq(.1,.9,.1),nboot=2000,alpha=0.05)` | Compute percentile bootstrap confidence intervals of a sequence of quantiles               |
| `ks(x,y)`                                                 | Kolmogorov-Smirnov test statistic                                                          |
| `cid(x,y)`                                                | Cliff’s delta test                                                                         |
| `pxgta(x,a=0)`                                            | Proportion of observations greater than a specified value                                  |
| `pxgty(x,y)`                                              | Proportion of observations in x greater than observations in y                             |
