# Reinforcement Learning Basics

RL takes place as a conversation between an agent and an environment.

The environment reveals itself to the agent as state s. The agent can impact the environment via some action a and receives a feedback r.

This is similar to MDP, however instead of having all of the knowledge and computation done over the environment, it's all occurring "in the head" of the agent. Furthermore details of the environment are only exposed to the agent. All of the possibilities aren't really known unless an action is taken.

## Behavior Structures

- Plan - fixed sequence of actions. 
    - This can't always be done! 
    - During learning you don't know outcomes so you can't execute a plan.
    - If the environment is stochastic than you need to react to the stochasticity
- Conditional plan - includes "if" statements. Normally this is thought of having a fixed plan for all of the possibilities. Contrasts with dynamic re-planning where a new plan is regenerated if a deviation is found 
- Stationary policy / universal plan - Mapping from state to action. 
    - It's a conditional plan with an if for every possible state. 
    - Very large!
    - Alway an optimal stationary policy for every MDP

## Evaluating a policy


## Evaluating a Learner


## Summary