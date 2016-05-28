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

### TD (1) Rule

```
For episode T:
For all s, e(s) = 0 at start of episode, V_T(s) = V_T-1(s)
After, s_t-1 ->^r_t s_t (step t)
e(s_t-1) = e(s_t) + 1
For all s, V_T (s) = V_T(s) + alpha_T(r_T + gamma V_t-1(s_T) - V_t-1(S_t-1)) e(s)
e(s) = gamma e(s)
```

e(s) is eligibility

### TD(1) Intuition

 The value that is propagated back from successive states cancel with each other. Thus TD(1) is the same as outcome based updates (if no repeated states).

 If there are repeated states than outcome based learning doesn't learn from them within the episode. However TD(1) will learn based on the value previously calculated earlier in the episode.