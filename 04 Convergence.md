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