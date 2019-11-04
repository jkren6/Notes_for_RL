---
description: >-
  cite from here:
  https://www.meltycriss.com/2018/03/18/paper-prioritized-experience-replay/
---

# 技术总结《OpenAI Gym》

## Gym核心函数调用链

一般来说，使用Gym的代码如下：

{% code-tabs %}
{% code-tabs-item title="main.py" %}
```python
# main.py
import gym
def choose_action(o):
	...
env = gym.make('CartPole-v0')
o = env.reset()
while True:
	a = choose_action(o)
	o_, r, done, info = env.step(a)
	o = o_
	if done:
		break
```
{% endcode-tabs-item %}
{% endcode-tabs %}

可见，关键的函数有：

* `env = gym.make('CartPole-v0')`
* `env.reset()`
* `env.step(a)`

\*\*\*





```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

```
// Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```



