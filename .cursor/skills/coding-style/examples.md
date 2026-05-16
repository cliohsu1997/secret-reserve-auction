# R and C++ Coding Style Examples

## General Rules

- **Break line for each argument** in function definitions and calls
- **Break line after arithmetic operations** (`+`, `-`, `*`, `/`, etc.)
- **Keep comments minimal** (only essential comments)
- **If statements**: condition on new line within parentheses

## For Loop

```r
for (
  variable in vector
) {
  # code
}
```

## Function Definition

```r
function_name <- 
  function(
    arg1,
    arg2 = default_value
  ) {
    # code
  }
```

## Function Call

Break line after the opening `(` and before the closing `)`; one argument or expression per line:

```r
do.call(
  rbind,
  cost_rows
)

matrix(
  nrow = 0L,
  ncol = 4L
)

rrsi_jt <-
  as.integer(
    nrow(matrix_sample_moment_rrsi[[j]][[t]]) > 0L
  )
crsi_jt <-
  as.integer(
    nrow(matrix_sample_moment_crsi[[j]][[t]]) > 0L
  )

compute_cutoff_purchase_jt(
  coverage_jt = coverage_jt,
  crsi_jt = 0,
  hassle_cost_jt = hassle_cost_jt,
  premium_crsi_jt = 0,
  price_jt = price_jt,
  rrsi_jt = 1,
  sigma_jt = sigma_jt
)
```

## Arithmetic Operations

Break line after arithmetic operators:

```r
# R
upper_bound <-
  (
    value_mean_jt +
    20.0 *
    value_sd_jt
  )

cs_ijt[
  1,
  1
] *
  dnorm(
    value_ijt,
    mean = value_mean_jt,
    sd = value_sd_jt
  )

# C++
double upper_bound =
  (
    value_mean_jt +
    20.0 *
    value_sd_jt
  );

return cs_ijt *
  density;
```

## Complex Expressions with Parentheses

Break line **after** the opening `(`, **after** each binary operator (e.g. `-`, `+`), and **before** the closing `)`:

```r
# R
result <-
  (
    value_mean_jt +
    20.0 *
    value_sd_jt
  )

production_cost_crsi_jt <-
  (
    RHS_c -
    handle_cost_normalized * dR_c_dp
  ) /
  dD_c_dp

# C++
Eigen::MatrixXd exp_uk =
  (
    sigma_jt *
    (
      realized_value_jt.array() -
      price_jt
    )
  ).exp();
```

## If Statements

Break line **after** the opening `(`, and **before** the closing `)`. When the condition uses `&&` or `||`, break line after each:

```r
# R
if (
  !check_integration_interval_valid(
    lower_bound = cutoff_purchase_jt,
    upper_bound = upper_bound,
    value_mean_jt = value_mean_jt,
    value_sd_jt = value_sd_jt
  )
) {
  result <- 0.0
} else if (
  a &&
  b
) {
  result <- 1.0
}

# C++
if (
  !check_integration_interval_valid_rcpp(
    cutoff_purchase_jt,
    upper_bound,
    value_mean_jt,
    value_sd_jt
  )
) {
  result = 0.0;
} else if (
  rrsi_jt == 1 &&
  crsi_jt == 0
) {
  result = production_cost_rrsi_jt;
} else {
  try {
    result = boost::math::quadrature::gauss_kronrod<double, 255>::integrate(
      integrand,
      cutoff_purchase_jt,
      upper_bound,
      max_iter,
      1e-6,
      &error
    );
  } catch (std::exception &ex) {
    std::cout << "Integration error: " << ex.what() << std::endl;
    result = std::numeric_limits<double>::quiet_NaN();
  }
}
```

## C++ Error Handling

Use `std::numeric_limits<double>::quiet_NaN()` for error handling in C++:

```cpp
catch (std::exception &ex) {
  std::cout << "Integration error: " << ex.what() << std::endl;
  result = std::numeric_limits<double>::quiet_NaN();
}
```

## Matrix Slicing

```r
matrix[
  ,
  spec_supply,
  drop = FALSE
]

cs_ijt[
  1,
  1
]
```
