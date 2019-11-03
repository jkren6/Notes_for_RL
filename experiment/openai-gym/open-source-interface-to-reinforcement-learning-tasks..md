# Open source interface to reinforcement learning tasks.

The [gym](https://github.com/openai/gym) library provides an easy-to-use suite of reinforcement learning tasks

```python
import gym
env = gym.make("CartPole-v1")
observation = env.reset()
for _ in range(1000):
  env.render()
  action = env.action_space.sample() # your agent here (this takes random actions)
  observation, reward, done, info = env.step(action)

  if done:
    observation
```

