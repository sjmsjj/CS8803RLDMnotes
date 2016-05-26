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

Learning to predict over time