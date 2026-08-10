1. Build Q-network
2. Build replay buffer to store experiences
3. Implement policy to choose action
4. Piece together and train agent

Why does network does not learn +1 regardless of observation? - because there are negative rewards
--no not true, it will just learn actions that have more +1 rewards - we are calculating Q-values which are cumulative



t=0: eps = start
t=exploration_fraction \* total_timesteps: eps=end

m = dy/dx = (end-start) / (exploration_fraction * total_timesteps)

y = mx + c
eps = (end-start) / (exploration_fraction * total_timesteps) \* current_timestep + end_e


eps = start_e - 


What will happen to Q values when agent moves closer to solving cartpole environment? - The Q-values should start increasing, as the expected values of each state will start increasing (reward keeps going up). Not quite, $\lim_{n\to\infty} \frac 1 {1-\gamma}$ , values also spike every time Q-table is updated
# Policy Gradient
Learn the policy directly

Policy is parameterised $\pi_\theta(a|s)$ with parameters $\theta$

Choose $\theta$ to maximise expected return $J(\theta)=E_{\tau\sim\pi_\theta}[G(\tau)]$

Update policy directly with gradient ascent $\theta\leftarrow\theta+\alpha\nabla_\theta J(\theta)$

## Problem
Return $G$ is sum of rewards from trajectory $\tau$

$\tau$ is a result of sampling from policy and environmental distribution, which is inaccessible

This is circular
## Solution: Policy Gradient Theorem
Use the return weighted by gradient of log-prob as an unbiased estimator of the gradient of the return

? - this is a lot of words

$\nabla_\theta J(\theta)=E_{\tau\sim\pi_\theta}[\sum_tG_t\nabla_\theta\log\pi_\theta(a_t|s_t)]$
# This is the REINFORCE algorithm
