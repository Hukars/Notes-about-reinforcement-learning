## Policy Gradient
Policy gradient是解决reinforcement learning问题的另一种思路，在上一个lecture中，我们采用的是value based的方法，我们优化的也是一个action-value function，实际上有了function approximation的技术，我们可以直接优化一个带参数的策略$\pi_\theta$，基于对标量性能衡量$J(\theta)$的梯度计算。

#### Introduction
考虑model-free的条件下，来优化：
$$\pi_{\theta}(s,a)=P[a\mid s,\theta]$$
这是**policy based**的方法；如果还是需要value function，那就是混合的**actor-critic**方法。
但是请注意，这两者和value based的本质区别是，在动作选择的时候不会再”**咨询**“value function了。


**Advantages of Policy-Based RL**
- 更好的收敛性质：参数化带来的随机性使得在一些特殊问题上可以避免振荡
- 在高维或者连续动作空间中很有效：避免了很难处理的$\mathop{\arg\max}_aq_\pi(s,a)$
- 可以学习到随机策略
- 可以引入有关策略形式的先验知识

**Disadvantages  of Policy-Based RL**
- 一般收敛到一个局部最优策略（这里soft-max可以解决嘛？）
- 评估一个策略一般来说很低效且方差大

**Policy Objective Functions**
- episodic environment：$J(\theta)=E_{S_0} [V^{\pi_{\theta}}(S_0)]$,在这种情况下一般 $\gamma=1$
- continuing environment:
$$J_{avV}(\theta)=\sum_s{d^{\pi_{\theta}}(s)V^{\pi_\theta}(s)}$$
$$J_{avR}(\theta)=\sum_s{d^{\pi_{\theta}}(s)\sum_a{\pi_\theta{(a \mid s)R_s^a}}}$$

	其中$d^{\pi_{\theta}}$指Markov chain的[stationary distribution](https://en.wikipedia.org/wiki/Stationary_distribution)（又称on-policy distribution），且$J_{avV}(\theta)=\frac{1}{1-\gamma}J_{avR}(\theta)$,所以两个目标式实际上是等价的。

我们的目标是找到最优$\theta$，使得$J(\theta)$最大


#### Monte-Carlo Policy Gradient

**Policy Gradient Theorem**
有关这个定理的详细推导可以参阅**An Introduction to Reinforcement Learning**，这个定理通过具体的数学推导向我们展示了$\nabla{J(\theta)}$的形式其实可以很简洁，
$$\nabla{J(\theta)}\varpropto \sum_s{\mu(s)\sum_a{q_{\pi_\theta}(s,a)\nabla\pi_\theta(a\mid{s})}}$$

其中$\mu(s)$是on-policy distribution，在episodic和continuing环境下二者定义略有区别，除此之外以上关系适用于$J(\theta),J_{avV}(\theta),J_{avR}(\theta)$
	