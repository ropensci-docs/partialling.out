# partialling_out: partialling out variable of interest and main

Creates a data.frame of the residualised main explanatory variable and,
if wanted, variable of interest of a linear or fixed effects model

## Usage

``` r
partialling_out(model, data, weights, both, na.rm, ...)
```

## Arguments

- model:

  object for which we want to residualise variables

- data:

  data.frame used in the original model. Using different data will
  return unexpected results or an error.

- weights:

  a numeric vector for weighting the partial models. Length must be
  equal to number of rows of `data`

- both:

  if `TRUE` will residualise both the variable of interest and the first
  explanatory variable in the model. If `FALSE`, only the latter. Set to
  `TRUE` by default

- na.rm:

  if `TRUE` will remove observations with NA before any models are run.
  If `FALSE`, the underlying `lm`, `feols`, or `felm` will remove NA
  values but errors may arise if weights are used.

- ...:

  Any other lm, feols, or felm parameters that will be passed to the
  partial regressions

## Value

a data.frame with the (residualised) variable of interest and
residualised main explanatory variable

## Details

The function regresses the main (i.e. first in the model) explanatory
variable and the variable of interest (if parameter `both` is set to
`TRUE`) against all other control variables and fixed effects and
returns the residuals in a data.frame

Will accept lm, felm (lfe package), and feols (fixest package) objects

## Examples

``` r
library(palmerpenguins)
#> 
#> Attaching package: ‘palmerpenguins’
#> The following objects are masked from ‘package:datasets’:
#> 
#>     penguins, penguins_raw
library(fixest)
model <- feols(bill_length_mm ~ bill_depth_mm | species + island,
               data = penguins)
#> NOTE: 2 observations removed because of NA values (LHS: 2, RHS: 2).
partial_df <- partialling_out(model, penguins, both = TRUE)
```
