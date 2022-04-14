# modelarchive

## `brms`

```r
library("brms")

dat <- mtcars
dat$logic <- as.logical(dat$vs)
dat$cyl_fac <- as.factor(dat$cyl)
dat$cyl_cha <- as.character(dat$cyl)

brms_numeric <- brm(am ~ hp, data = dat, family = bernoulli(), backend = "cmdstanr",
               seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_numeric2 <- brm(am ~ mpg + hp, data = dat, family = bernoulli(), backend = "cmdstanr",
                     seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_character <- brm(am ~ mpg + cyl_cha, data = dat, family = bernoulli(), backend = "cmdstanr",
                      seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_factor <- brm(am ~ mpg + cyl_fac, data = dat, family = bernoulli(), backend = "cmdstanr",
                   seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_factor_formula <- brm(am ~ mpg + factor(cyl), data = dat, family = bernoulli(), backend = "cmdstanr",
                           seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_interaction <- brm(am ~ mpg * vs, data = dat, family = bernoulli(), backend = "cmdstanr",
                        seed = 1024, silent = 2, chains = 4, iter = 1000)

brms_logical <- brm(am ~ logic, data = dat, family = bernoulli(), backend = "cmdstanr",
                    seed = 1024, silent = 2, chains = 4, iter = 1000)


brms_cumulative_random <- brm(rating ~ treat + period + (1 | subject), family = cumulative(),
                              data = inhaler, backend = "cmdstanr", silent = 2)

brms_monotonic <- brm(mpg ~ hp + mo(carb), backend = "cmdstanr", data = mtcars, silent = 2)

brms_monotonic_factor <- brm(mpg ~ hp + factor(cyl) + mo(carb), backend = "cmdstanr", data = mtcars, silent = 2)

# epi
prior1 <- prior(normal(0, 10), class = b) + prior(cauchy(0, 2), class = sd)
brms_epi <- brm(count ~ zAge + zBase * Trt + (1 | patient), backend = "cmdstanr",
                data = epilepsy, family = poisson(), prior = prior1,
                seed = 1024, iter = 1000, silent = 2)

# vdem
vdem_2015 <- read.csv("https://github.com/vincentarelbundock/marginaleffects/raw/main/data-raw/vdem_2015.csv")
brms_vdem <- suppressWarnings(brm(
  bf(media_index ~ party_autonomy + civil_liberties + (1 | region),
     phi ~ (1 | region)),
  data = vdem_2015,
  family = Beta(),
  backend = "cmdstanr",
  control = list(adapt_delta = 0.9)))


# downloaded from the easystats circus and hosted here as stable duplicate
brms_mv_1 <- insight::download_model("brms_mv_1")
brms_categorical_1 <- insight::download_model("brms_categorical_1")
```
