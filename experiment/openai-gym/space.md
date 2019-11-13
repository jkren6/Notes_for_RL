---
description: >-
  Every environment comes with an action_space and an observation_space. These
  attributes are of type Space, and they describe the format of valid actions
  and observations
---

# Space

{% tabs %}
{% tab title="Print the action\_space and observation\_space of \'CartPole-v0\'" %}
```python
import gym
env = gym.make('CartPole-v0')
print(env.action_space)
#> Discrete(2)
print(env.observation_space)
#> Box(4,) # [position of cart, velocity of cart, angle of pole, rotation rate of pole]
```
{% endtab %}
{% endtabs %}

The [`Discrete`](https://github.com/openai/gym/blob/master/gym/spaces/discrete.py) space allows a fixed range of non-negative numbers, so in this case valid `action`s are either 0 or 1. The [`Box`](https://github.com/openai/gym/blob/master/gym/spaces/box.py) space represents an `n`-dimensional box, so valid `observations` will be an array of 4 numbers. We can also check the `Box`’s bounds:

{% tabs %}
{% tab title="The Box\'s bounds of \'CartPole-v0\'" %}
```python
print(env.observation_space.high)
#> array([ 2.4       ,         inf,  0.20943951,         inf])
print(env.observation_space.low)
#> array([-2.4       ,        -inf, -0.20943951,        -inf])
```
{% endtab %}
{% endtabs %}

