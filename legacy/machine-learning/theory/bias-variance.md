# Bias-variance trade-off

## Mathematical explanation

For any approximator `f'` for the function `f`, we can write MSE as

MSE = E[ (f'(x) - f(x))^2 ] + err(noise in f)

Remember variance formula
var(X) = E[X^2] - E[X]^2

Hence,
E[X^2] = var(X) + E[X]^2

Then, MSE formula becomes

MSE = var(f'(x) - f(x)) + E[f'(x) - f(x)]^2

Variance of a non-random variable is zero; hence, shifting a random variable doesn't change its variance. Since, f(x) is a fixed variable, the first term simplifies to

MSE = var(f'(x)) + E[f'(x) - f(x)]^2

The second term is denoted as square of bias of approximator.

MSE = var(f'(x)) + bias(f'(x))^2

Hence,
error = bias^2 + variance
