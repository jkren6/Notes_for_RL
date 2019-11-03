---
description: An simple tutorial about using Gym
---

# OpenAI Gym

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

