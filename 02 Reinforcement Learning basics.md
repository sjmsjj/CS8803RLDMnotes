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

focusing on stationary plans because they allow agents to handle all possibilities.

## Evaluating a policy

Discussed in the case of MDPs but re-visiting for RL!

Given stochasticity and other factors the same policy can produce different sequences of states and actions. We need a way to condense this into a signle value to measure how good a policy is.

4 steps to come up with a single measurement:

1. State transitions to immediate rewards - R(s, a)
2. Truncate according to horizon - T can be finite or infinite
3. Summarize sequence - sum_{i = 1}^T gamma^i r_i
4. Summarize over sequences - average expectation

## Evaluating a Learner

But in RL we worry about the learner not just the policy and the policy is just the output of a learner

Things to evaluate on:

- Value of returned policy
- Computational complexity (time) - how much cpu time is needed
- Sample complexity (time) - how much date is needed
- Space complexity ??? - generally not that interesting, generally not limited

## Summary