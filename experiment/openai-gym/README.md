---
description: An simple tutorial about using Gym.
---

# OpenAI Gym

> View the [full list of environments](https://gym.openai.com/envs) to get the birds-eye view.
>
> To list the environments available in your installation, just ask `gym.envs.registry`:

{% code-tabs %}
{% code-tabs-item title="gym.envs.registry" %}
```python
from gym import envs
print(envs.registry.all())
#> [EnvSpec(DoubleDunk-v0), EnvSpec(InvertedDoublePendulum-v0), EnvSpec(BeamRider-v0), EnvSpec(Phoenix-ram-v0), EnvSpec(Asterix-v0), EnvSpec(TimePilot-v0), EnvSpec(Alien-v0), EnvSpec(Robotank-ram-v0), EnvSpec(CartPole-v0), EnvSpec(Berzerk-v0), EnvSpec(Berzerk-ram-v0), EnvSpec(Gopher-ram-v0), ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Open source interface to reinforcement learning tasks.

```python
import gym
env = gym.make("CartPole-v1")
observation = env.reset()
for _ in range(1000):
  env.render()
  
  # when you use RL_Glue, we should use method 'rl_agent_step(self, reward, observation)'
  # to return an action by the agent.
  action = env.action_space.sample() # your agent here (this takes random actions)
 
  observation, reward, done, info = env.step(action)

  if done:
    observation  
  env.close()
```



> [A brief introduction video in madarian.](https://morvanzhou.github.io/tutorials/machine-learning/reinforcement-learning/4-4-gym/)
>
> [A bried introduction in Zhihu.](https://zhuanlan.zhihu.com/p/40673328)
>
> [A good introduction in Blog](https://www.meltycriss.com/2018/03/26/tech-gym/)
>
> [A detail introduction in Zhihu.](https://zhuanlan.zhihu.com/p/43109742)

