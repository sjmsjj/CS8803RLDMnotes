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
