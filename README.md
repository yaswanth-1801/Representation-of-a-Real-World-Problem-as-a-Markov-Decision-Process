# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process


## Aim
To identify a real-world public transport management problem and represent it as a Markov Decision Process (MDP) by defining its states, actions, transition probabilities, reward function, and discount factor using Python. The aim is to understand how Artificial Intelligence and Reinforcement Learning can improve public transport efficiency, reduce passenger waiting times, and manage buses effectively.



## Problem Statement


### Problem Description

Public transport systems often experience overcrowding during peak hours and underutilization during off-peak hours. Passengers may face long waiting times because of insufficient buses, traffic congestion, and improper scheduling.

An AI-Based Public Transport Management System monitors passenger demand and determines suitable actions to improve transport services. Depending on the current passenger demand, the intelligent agent can maintain the existing schedule, deploy an additional bus, or reallocate a bus from another route.

After an action is performed, the passenger demand may change according to the transition probabilities. The agent receives rewards or penalties based on the resulting demand and the operational cost of the selected action.

By applying Reinforcement Learning, the system can learn a suitable strategy to reduce overcrowding, minimize passenger waiting times, and improve bus utilization.

Note: The transition probabilities and rewards used in this experiment are illustrative assumptions, not measurements from an actual public transport network.


## MDP Components

A Markov Decision Process is represented as:
A Markov Decision Process is represented as:
\[
MDP=(S,A,P,R,\gamma)
\]
> S — States: Passenger demand conditions: Low, Medium, and High.
> A — Actions: Maintain Current Schedule, Deploy Extra Bus, and Reallocate Bus.
> P — Transition Probabilities: Probabilities of moving from the current passenger demand state to another state after an action.
> R — Reward Function: Feedback based on passenger demand and the operational cost of the selected action.
> γ — Discount Factor: 0.90, giving importance to future rewards as well as immediate rewards.

## State Space
The state space represents all possible passenger demand conditions.
\[
S=\{\text{Low, Medium, High}\}
\]
```
states = {
    "Low": "0-5 passengers waiting",
    "Medium": "6-15 passengers waiting",
    "High": "More than 15 passengers waiting"
}
```
1.Low: A small number of passengers are waiting. Available buses can handle the demand.
2.Medium: A moderate number of passengers are waiting. The system should monitor demand.
3.High: A large number of passengers are waiting. Additional transport resources may be required.


## Sample State
High is a sample state. It means more than 15 passengers are waiting at a bus stop. The AI agent may choose to deploy an additional bus to reduce passenger waiting time.





## Action Space

The action space represents all decisions available to the intelligent agent.
\[
A=\{\text{Maintain, Deploy Extra Bus, Reallocate Bus}\}
\]
```
actions = [
    "Maintain Current Schedule",
    "Deploy Extra Bus",
    "Reallocate Bus"
]
```
1.Maintain Current Schedule: Continue operating buses according to the existing timetable.
2.Deploy Extra Bus: Send an additional bus to a route experiencing high passenger demand.
3.Reallocate Bus: Transfer an available bus from a less crowded route to a route with greater demand.

## Sample Action
When the current state is High, the agent may select Deploy Extra Bus to increase transport capacity and reduce overcrowding.

## Transition Probability

The transition probability is represented as:
\[
P(s' \mid s,a)
\]
It represents the probability of reaching the next state \(s'\) after taking action \(a\) in the current state \(s\).

The following transition probabilities are illustrative.

| Current State | Action | Next Low | Next Medium | Next High |
|---|---|---:|---:|---:|
| Low | Maintain Current Schedule | 0.80 | 0.20 | 0.00 |
| Low | Deploy Extra Bus | 0.95 | 0.05 | 0.00 |
| Low | Reallocate Bus | 0.90 | 0.10 | 0.00 |
| Medium | Maintain Current Schedule | 0.30 | 0.50 | 0.20 |
| Medium | Deploy Extra Bus | 0.60 | 0.35 | 0.05 |
| Medium | Reallocate Bus | 0.50 | 0.40 | 0.10 |
| High | Maintain Current Schedule | 0.10 | 0.40 | 0.50 |
| High | Deploy Extra Bus | 0.35 | 0.55 | 0.10 |
| High | Reallocate Bus | 0.30 | 0.55 | 0.15 |

Each row sums to 1.0, representing all possible next passenger demand states for that state-action pair.

Example: If the current state is High and the agent selects Deploy Extra Bus, there is a 35% probability of reaching Low, a 55% probability of reaching Medium, and a 10% probability of remaining in High.


## Reward Function

The reward function is represented as:
\[
R(s,a,s')
\]
The reward depends on the next passenger demand state and the operational cost of the selected action.

State Rewards
| Next Passenger Demand State | Reward |
|---|---:|
| Low | +10 |
| Medium | +3 |
| High | -10 |

Action Rewards
| Action | Additional Reward |
|---|---:|
| Maintain Current Schedule | 0 |
| Deploy Extra Bus | -2 |
| Reallocate Bus | -1 |

The total reward is calculated by adding the state reward to the action reward:
\[
R(s,a,s')=R_{\text{state}}(s')+R_{\text{action}}(a)
\]
Example: If the agent deploys an extra bus and the next state becomes Low:
\[
R=10+(-2)=+8
\]
Positive rewards encourage lower passenger demand and shorter waiting times, while negative rewards discourage overcrowding and unnecessary operating costs.

Discount Factor
\[
\gamma=0.90
\]
The discount factor encourages the agent to consider future passenger demand and rewards in addition to immediate rewards.

## Graphical Representation

The following diagram illustrates the MDP states and example transitions.

       +----------------------+
       |      LOW DEMAND      |
       |  0-5 waiting people  |
       +----------------------+
                 |
                 | Demand increases
                 v
       +----------------------+
       |    MEDIUM DEMAND     |
       |  6-15 waiting people |
       +----------------------+
                 |
                 | Demand increases
                 v
       +----------------------+
       |      HIGH DEMAND     |
       | More than 15 waiting |
       +----------------------+
                 |
                 | Deploy Extra Bus
                 v
          LOW / MEDIUM DEMAND

The transition probabilities determine the likelihood of reaching each next state. The rewards evaluate the effectiveness of the selected action.

## Python Representation

The complete implementation uses Python dictionaries to represent states, actions, transition probabilities, rewards, and the discount factor. The program validates the transition probabilities and calculates the expected immediate reward for a sample decision.
Main.py
```

# AI-Based Public Transport Management System
# Representation of a Real-World Problem as an MDP

print("Name: Yaswanth R")
print("Register Number: 212225040499")

# State Space
states = ["Low", "Medium", "High"]

# Action Space
actions = [
    "Maintain Current Schedule",
    "Deploy Extra Bus",
    "Reallocate Bus"
]

# Transition Probabilities
transitions = {
    "Low": {
        "Maintain Current Schedule":
            {"Low": 0.80, "Medium": 0.20, "High": 0.00},
        "Deploy Extra Bus":
            {"Low": 0.95, "Medium": 0.05, "High": 0.00},
        "Reallocate Bus":
            {"Low": 0.90, "Medium": 0.10, "High": 0.00}
    },

    "Medium": {
        "Maintain Current Schedule":
            {"Low": 0.30, "Medium": 0.50, "High": 0.20},
        "Deploy Extra Bus":
            {"Low": 0.60, "Medium": 0.35, "High": 0.05},
        "Reallocate Bus":
            {"Low": 0.50, "Medium": 0.40, "High": 0.10}
    },

    "High": {
        "Maintain Current Schedule":
            {"Low": 0.10, "Medium": 0.40, "High": 0.50},
        "Deploy Extra Bus":
            {"Low": 0.35, "Medium": 0.55, "High": 0.10},
        "Reallocate Bus":
            {"Low": 0.30, "Medium": 0.55, "High": 0.15}
    }
}

# State Rewards
state_rewards = {
    "Low": 10,
    "Medium": 3,
    "High": -10
}

# Action Rewards
action_rewards = {
    "Maintain Current Schedule": 0,
    "Deploy Extra Bus": -2,
    "Reallocate Bus": -1
}

# Discount Factor
gamma = 0.90

print("\nStates:", states)
print("Actions:", actions)
print("Discount Factor:", gamma)

# Validate Transition Probabilities
print("\nTransition Probability Validation:")

for state in states:
    for action in actions:
        total = sum(transitions[state][action].values())

        print(state, "-", action, "=", round(total, 2))

        assert abs(total - 1.0) < 1e-9

print("All transition probabilities are valid.")

# Sample Decision
current_state = "High"
selected_action = "Deploy Extra Bus"

print("\nSample Decision")
print("Current State:", current_state)
print("Selected Action:", selected_action)

print(
    "Next State Probabilities:",
    transitions[current_state][selected_action]
)

# Calculate Expected Immediate Reward
expected_reward = 0

for next_state, probability in (
    transitions[current_state][selected_action].items()
):
    reward = (
        state_rewards[next_state]
        + action_rewards[selected_action]
    )

    expected_reward += probability * reward

print("Expected Immediate Reward:", round(expected_reward, 2))
```

## Output
```
<img width="907" height="597" alt="image" src="https://github.com/user-attachments/assets/84d0c53b-5146-473a-9945-6b954f8de872" />

```
Calculation of Expected Immediate Reward
For the current state High and the action Deploy Extra Bus:
| Next State | Probability | Total Reward | Weighted Reward |
|---|---:|---:|---:|
| Low | 0.35 | \(10-2=8\) | 2.80 |
| Medium | 0.55 | \(3-2=1\) | 0.55 |
| High | 0.10 | \(-10-2=-12\) | -1.20 |

Therefore,
\[
\begin{aligned}
E[R] &= 0.35(8)+0.55(1)+0.10(-12)\\
&=2.80+0.55-1.20\\
&=\boxed{2.15}
\end{aligned}
\]
The expected immediate reward is 2.15.

## Result
The real-world problem of an AI-Based Public Transport Management System was successfully represented as a Markov Decision Process using Python. The state space, action space, transition probabilities, reward function, and discount factor were defined.

The program validated all transition probabilities and calculated an expected immediate reward of 2.15 when passenger demand was high and the agent selected the Deploy Extra Bus action.

This experiment demonstrates how Reinforcement Learning can be applied to reduce passenger waiting times, manage bus schedules, reduce overcrowding, and improve public transport efficiency. Further algorithms, such as Q-learning, can be implemented to help the agent learn an effective transport management policy through repeated interactions.


---

