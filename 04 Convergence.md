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