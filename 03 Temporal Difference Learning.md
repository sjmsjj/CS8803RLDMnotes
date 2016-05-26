# Temporal Difference Learning

## RL Context

[s, a, r]* -> RL algorithm -> pi (policy)

### Model-based

[s, a, r]* -> Model Learner -> learns T and R -> MDP-solver -> Q* -> argmax -> pi

Learning occurs in the Model Learner - T / R step

### Value-function based (model-free)

[s, a, r]* -> value update -> Q -> argmax -> pi

Learning occurs in value  update based on Q.
