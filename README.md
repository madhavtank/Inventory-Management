# Inventory Management with Reinforcement Learning

## Project Description

This project addresses an **Inventory Management problem** where retail stores maintain a stock of products to meet random demand. Stock is replenished at regular intervals. Our objective is to develop a reinforcement learning model that determines the optimal procurement strategy to minimize costs over time.

### Problem Overview

At time step **t**, the amount of stock before procurement is denoted by $X_t$. The store can procure additional stock $U_t$ (with $0 \leq U_t \leq U$) at a cost of $p$ per unit, resulting in a total procurement cost of $pU_t$.

Demand, denoted $W_t$, is independent and identically distributed (i.i.d.) with distribution $P_W$, where $P_W \sim \text{Uniform}(0, 10)$. The stock available at the next time step is given by:

$$
X_{t+1} = X_t + U_t - W_t
$$

Negative stock indicates backlogged demand. The **holding cost** function $h(x)$ accounts for two types of costs:
- $a$ is the **per-unit storage cost**.
- $b$ is the **per-unit backlog cost**.

The **per-stage cost** is:

$$
c(X_{t+1}, U_t) = h(X_{t+1}) + pU_t
$$

Our goal is to minimize the **expected total cost** over a finite time horizon by determining an optimal inventory control strategy.

### Parameters:
- **Demand Distribution $P_W$**: $P_W \sim \text{Uniform}(0, 10)$
- **Holding cost function $h(x)$**:

$$
h(x) =
\begin{cases} 
    a \cdot x, & \text{if } x \geq 0 \\
    -b \cdot x, & \text{if } x < 0 
\end{cases}
$$

where $a$ is the cost for surplus stock and $b$ is the cost for backlogged demand.

### State Space
- The state $X_t$ represents the amount of inventory at time $t$.
- State space: $-10 \leq X_t \leq 10$.

### Action Space
- The action $U_t$ is the amount of additional inventory procured at time $t$.
- Action space: $0 \leq U_t \leq 10$.

---

## Algorithms Implemented

We implemented several reinforcement learning methods to solve this inventory management problem:

1. **Deep Q-Network (DQN)**:
   - A value-based method that uses a neural network to approximate the Q-function for optimal decision-making.

2. **Policy Gradient Methods**:
   - **REINFORCE Algorithm (Monte Carlo)**: 
     A policy-based method that updates the policy using complete episode returns.
   - **Actor-Critic**: 
     Combines value-based and policy-based methods by using an actor to suggest actions and a critic to evaluate them.

3. **Natural Actor-Critic**:
   - A variant of the Actor-Critic algorithm that uses natural gradients for more efficient learning.

4. **Natural Gradient with Fischer Projection Matrix**:
   - Incorporates Fischer information to adjust the gradients for better convergence properties.

5. **Sarsa(λ)**:
   - An on-policy temporal difference (TD) control algorithm that updates the value of state-action pairs using eligibility traces. This method balances exploration and exploitation while improving stability through the use of the trace-decay parameter, λ. Sarsa(λ) is particularly useful in continuous state and action spaces, making it a good fit for the inventory management problem.


## Contributors

- Madhav Tank
- Manav Shah
- Yash Kawade
- Yash Adivarekar
- Nikunj Garg
