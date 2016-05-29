# Temporal Difference Learning

## RL Context

[s, a, r]* -> RL algorithm -> pi (policy)

### Model-based

[s, a, r]* -> Model Learner -> learns T and R -> MDP-solver -> Q* -> argmax -> pi

Learning occurs in the Model Learner - T / R step

### Value-function based (model-free)

[s, a, r]* -> value update -> Q -> argmax -> pi

Learning occurs in value  update based on Q.

### Policy search

[s, a, r]* -> policy update -> pi

Learning occurs in the policy update - pi step. This is very direct but very difficult because the kind of feedback that you're getting isn't very useful in directly modifying the policy.

More supervised learning is inverse with how direct the learning is. Most research is in value based learning as it strikes a nice compromise.

## TD(lambda)

TD = Temporal Difference

Learning to predict over time. (Trying to learn V(s))

V(s) = 0, if s = s_F, E[r + gamma V(s')], otherwise

### Learning value

Given a model of a Markov Chain you can work backwards from the final state to calculate the value of proceeding states.

Given data you can estimate the value based on the average the reward between sequences. 

### Computing Estimates Incrementally

```
V_t-1 (s_1), R_t(s_1) V_t(s_1)

v_t(s_1) = ((t - 1) V_t-1(s_1) + R_t(s_1)) / t 
= (t - 1) / t * V_t-1 (s_1) + 1 / t * R_t(s_1)
= v_t-1(s_1) + alpha_t * (R_t(s_1) - v_t-1(s))
where alpha_T = 1 / T
```

Resembles perceptron update rule! R_t(s_1) - v_t-1(s) can be thought of as an error rate

### Properties of Learning Rates

V_t(s) = V_t-1(s_1) + alpha_t * (R_t(s_1) - V_t-1(s))

lim_T->inf V_t(s) = V(s) if:

1. sum_T alpha_T = inf
2. sum_T alpha_T ^2 < inf

### Selecting Learning Rates

1. Learning rate needs to relate to T and decrease over time.
2. 1/T^p converges if p > 1

## TD (1) Rule

```
For episode T:
For all s, e(s) = 0 at start of episode, V_T(s) = V_T-1(s)
After, s_t-1 ->^r_t s_t (step t)
e(s_t-1) = e(s_t) + 1
For all s, V_T (s) = V_T(s) + alpha_T(r_t + gamma V_T-1(s_t) - V_T-1(s_t-1)) e(s)
e(s) = gamma e(s)
```

e(s) is eligibility

### TD(1) Intuition

 The value that is propagated back from successive states cancel with each other. Thus TD(1) is the same as outcome based updates (if no repeated states).

 If there are repeated states than outcome based learning doesn't learn from them within the episode. However TD(1) will learn based on the value previously calculated earlier in the episode.

### TD(1) Flaws

Compared to Maximum Likelihood (which doesn't necessarily represent the model - it too can be subject to whims of the data), doesn't necessarily capture information from other states that were visited along the path in other learning episodes.

ML is better able to use all the data available

## TD(0) rule

Find the ML estimate! (if data repeated infinitely). This has the effect of a Maximum likelihood (ML) model even over finite data. It uses the intermediary node value estimates from other sequences that we've seen.

```
V_T (s_t-1) = V_T(s_t-1) + alpha_T(r_t + gamma V_T(s_t) - V_T(S_t-1)) e(s)
V_T (s_t-1) = E_s_t [r + gamma V_T(s_t)]
```

## TD(lambda)

Rule that encompases TD(0) and TD(1)! (when lambda = 0 or lambda = 1).

Both TD(0) and TD(1) have updated based on differences between temporally successive predictions. One algorithm covers both.

TD(1) is essentially equivalent to TD(0) except that there is no eligibility and instead of updating across all states, only update for the state s = s_t-1

In order to introduce a lambda so that when lambda = 0 the algorithm behaves like TD(0) and when lambda = 1 th algorithm behaves like TD(1) we simply change the eligibility update rule to be e(s) = lambda gamma e(s)

## K-step estimator

TD(0) is a 1 step estimator

```
E_1: V(s_t) = V(s_t) + alpha_T(r_t+1 + gamma V(s_t+1) - V(s_t))
E_2: V(s_t) = V(s_t) + alpha_T(r_t+1 + gamma r_t+2 + gamma^2 V(s_t+2) - V(s_t))
...
E_inf: V(s_t) = V(s_t) + alpha_T(r_t+1 + gamma r_t+2 + ... + gamma^k-1 r_t+k
```

## K-Step estimators and TD(lambda)

```
E_1: 1 - lambda
E_2: lambda (1 - lambda)
E_k: lambda ^ k (1 - lambda)
...
E_inf: lambda^inf
```

So this makes it so that lambda = 0 behaves like TD(0) and lambda = 1 behaves like TD(1) and values of lambda in between incorporate other estimators to a certain extent

## TD(lambda) empirically

TD(0) performs better than TD(1) typically however usually in between 0 and 1 it tends to bow downwards with the minimum typically being around lambda = 0.7

## Summary

- Temporal difference learning - difference reward and value estimates - at different time steps
- different ways to solve the Reinforcement learning problem:
    - model-based
    - value-based: where TD typically falls
    - policy-based
- Incremental estimates, outcome based
- Learning rate properties
- TD(1) - inefficient, high variance
- TD(0) - maximum likelihood estimate
- TD(lambda) - has the properties of TD(0) and TD(1) when lambda = 0, 1. interpolates and cleaner outputs.