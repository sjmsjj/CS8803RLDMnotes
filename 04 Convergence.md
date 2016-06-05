# Convergence: TD with control

Not just learn values with TD but learn the values of different actions we might take in order to learn the right way to behave.

## Bellman's equations

no actions:

```
V(s) = R(s) + gamma sum_s' T(s, s') V(s')

[s_t-1, r_t, s_t]: V_t(s_t-1) = V_t-1(s_t-1) + alpha_t(r_t + gamma V_t-1(s_t) - V_t(s_t))
v_t(s) = v_t-1(s) otherwise
'''

TD(0)

## Bellman's equation with actions:

```
actions: Q(s, a) R(s, a) + gamma sum_s' T(s, a, s') max_a' Q(s', a')

[s_t-1, a_t-1, r_t, s_t]: Q_t(s_t-1, a_t-1) = Q_t-1(s_t-1, a_t-1) + alpha_t(r_t + gamma max_a' Q_t-1(s_t,a') - Q_t(s_t-1, a_t-1))
Q_t(s, a) = Q_T-1(s, a) otherwise
```

Same kind of update as for (but helps decide action based on highest value)

We can use it to create a TD(0)-esque reward

Approximations 1) If we knew the model synchronously update.

2) If we knew Q*, sampling asynchronously update.

## Bellman operator

Let B be an operator, or mapping of value functions to value functions (it is a mapping of Q functions to Q functions)

[BQ](s, a) = R(s, a) + gamma sum_s' T(s, a, s') max_a' Q(s', a')

Q* = BQ*: Bellman Equations

Q_t = BQ_t-1: Value Iteration

## Contraction Mapping

B is an operator

If, for all F, G and some 0 <= gamma <= 1

||BF - BG||_inf <= gamma ||F - G||_inf

then B is a contraction mapping

||Q||_inf = max_s,a ||Q(s, a)||: infinity norm, max norm (what's the largest state action pair that can be taken)

## Contraction properties

If B is a contraction mapping

1. F* = BF* (fixed star equation) has a solution and it is unique
2. F_t = BF_t-1 => F_t => F* (value iteration converges)

The first point (that it is unique) follow from the the contradiction if there were 2 fixed points F* and G* the difference wouldn't grow smaller but since it is contraction it must grow smaller.

The second point follows from ||F_t - F*||_inf = ||BF_t-q - BF*||_inf <= gamma ||F_t-1 -F*||_inf

## Bellman operator contractions

```
[BQ](s, a) = R(s, a) + gamma \sum_s' T(s, a, s') max_a' Q(s', a')

Given Q_1, Q_2:
||BQ_1 - BQ_2||_inf = max_a, s |[BQ_1](s, a) - [BQ_2](s, a)|