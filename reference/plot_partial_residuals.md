# plot_partial_residuals: scatterplot of partial residuals

Function for plotting partial residuals Uses `tinyplot` as backend

## Usage

``` r
plot_partial_residuals(x, add_lm = TRUE, quantile = FALSE, probs = 0.02, ...)
```

## Arguments

- x:

  a partial_residuals objects from
  [`partialling_out()`](https://docs.ropensci.org/partialling.out/reference/partialling_out.md)

- add_lm:

  if TRUE, a `lm` will be plotted

- quantile:

  if TRUE, will plot only the mean values of the quantiles of the mean
  explanatory variable specified by `probs`

- probs:

  numeric vector of length one that specifies the number of quantiles to
  be computed if `quantile` is TRUE. by default, 0.02, which will give
  50 quantiles.

- ...:

  Any other
  [`tinyplot::plt()`](https://grantmcdermott.com/tinyplot/man/tinyplot.html)
  params

## Value

invisibly, x

## Examples

``` r
library(palmerpenguins)
library(fixest)
model <- feols(bill_length_mm ~ bill_depth_mm | species + island,
               data = penguins)
#> NOTE: 2 observations removed because of NA values (LHS: 2, RHS: 2).
partial_df <- partialling_out(model, penguins, both = TRUE)
plot_partial_residuals(partial_df)

```
