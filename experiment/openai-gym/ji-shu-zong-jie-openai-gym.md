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

```text
$ give me super-powers
```

#### 我们先关注`env.reset()`和`env.step(a)`。这两个函数是超类`Env`的成员函数，`Env`的相关代码如下：

{% code-tabs %}
{% code-tabs-item title="gym/core.py" %}
```python
# gym/core.py
class Env(object):
	...
    # Override in ALL subclasses
    def _step(self, action): raise NotImplementedError
    def _reset(self): raise NotImplementedError
    ...
    def step(self, action):
        return self._step(action)
    def reset(self):
        return self._reset()
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

可以看到这两个函数依赖于子类的`_reset(self)`和`_step(self, action)`实现，子类`CartPoleEnv`的相关代码如下：

{% code-tabs %}
{% code-tabs-item title="gym/envs/classic\_control/CartPole.py" %}
```python
# gym/envs/classic_control/CartPole.py
class CartPoleEnv(gym.Env):
	...
    def _step(self, action):
        ...
    def _reset(self):
        ...
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

综上，`env.reset()`和`env.step(a)`实际上是调用子类的`_reset(self)`和`_step(self, action)`。

#### 下面我们关注`gym.make('CartPole-v0')`，它的实现如下：

{% code-tabs %}
{% code-tabs-item title="registration.py" %}
```python
# gym/envs/registration.py
# Have a global registry
registry = EnvRegistry()
...
def make(id):
    return registry.make(id)

```
{% endcode-tabs-item %}
{% endcode-tabs %}

可以看到`gym.make`依赖于类`EnvRegistry`的成员函数`make`，`EnvRegistry`的相关代码如下：

{% code-tabs %}
{% code-tabs-item title="registration.py" %}
```python
# gym/envs/registration.py
class EnvRegistry(object):
    def __init__(self):
    	# 注册表
    	# key:	环境名称（e.g., 'CartPole-v0'）
    	# value:类型为EnvSpec，可以暂时理解为环境
        self.env_specs = {}
    def make(self, id):
        ...
        # 根据环境名称，通过成员函数找到对应的环境
        spec = self.spec(id)
        # 实例化环境
        env = spec.make()
        ...
        return env
    ...
    def spec(self, id):
        ...
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

可见类`EnvRegistry`的成员函数`make`依赖于类`EnvSpec`的成员函数`make`，`EnvSpec`的相关代码如下：

{% code-tabs %}
{% code-tabs-item title="registration.py" %}
```python
# gym/envs/registration.py
def load(name):
    ...
# EnvSpec与Env之间的关系类似于说明商品规格的订单与商品之间的关系，
# 下面用一个例子来说明：
# 假设你网购看中了一款衣服，那么你会挑选该款衣服的颜色、码数，然后再下单。
# 在这个例子里面，那款衣服就是Env，而说明该款衣服颜色、码数的订单就是EnvSpec。
# 这就是为什么EnvRegistry.make(self, id)中，在得到spec之后还要再spec.make()，
# 因为EnvSpec并不是Env，正如订单不是衣服。
class EnvSpec(object):
    def __init__(self, id, entry_point=None, ...):
    	self.id = id
        ...
        self._entry_point = entry_point
        ...
    def make(self):
        ...
        # 动态加载环境类
        # 相当于以下代码
        # from self._entry_point import classA
        # cls = classA
        cls = load(self._entry_point)
        # 实例化环境
        env = cls(**self._kwargs)
        ...
        return env
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> 至此，我们对Gym的核心函数调用链有了一个基本的了解：
>
> * `gym.make(id)`：通过`EnvRegistry`中的注册表找到对应的`EnvSpec`，`EnvSpec`根据`entry_point`动态`import`对应的`Env`，并将其实例化；
> * `env.reset()`和`env.step(a)`：子类的`_reset(self)`和`_step(self, action)`。

