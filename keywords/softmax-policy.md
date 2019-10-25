# Softmax Policy

## Advantage

One advantage of a softmax policy is that it explores according to the action-values, meaning that an action with a moderate value has a higher chance of getting selected compared to an action with a lower value. Contrast this with an 𝜖-greedy policy which does not consider the individual action values when choosing an exploratory action in a state and instead chooses randomly when doing so.

The probability of selecting each action according to the softmax policy is shown below:

$$
Pr{(A_t=a | S_t=s)} \hspace{0.1cm} \dot{=} \hspace{0.1cm} \frac{e^{Q(s, a)/\tau}}{\sum_{b \in A}e^{Q(s, b)/\tau}}
$$

where $$\tau$$ is the temperature parameter which controls how much the agent focuses on the highest valued actions. The smaller the termperature, the more the agent selects the greedy action. Conversely, when the temperature is high, the agent selects among actions more uniformly random.

## Problem

Given that a softmax policy exponentiates action values, if those values are large, exponentiating them could get very large. To implement the softmax policy in a numerically stable way, we often subtract the maximum action-value from the action-values. If we do so, the probability of selecting each action looks as follows:

$$
Pr{(A_t=a | S_t=s)} \hspace{0.1cm} \dot{=} \hspace{0.1cm} \frac{e^{Q(s, a)/\tau - max_{c}Q(s, c)/\tau}}{\sum_{b \in A}e^{Q(s, b)/\tau - max_{c}Q(s, c)}}
$$



