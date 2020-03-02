# 前言
强化学习，作为一门由计算机科学、神经科学、数学、心理学等多领域融合而成的学科，现在已经被DeepMind认为是实现AI(Artificial Intelligence)的关键技术。最为世人熟知的AlphaGo也是基于强化学习的方法，才实现了在Game of Go上对于人类的彻底超越。作为机器学习的一个特殊分支，熟悉机器学习的人应该很容易发现他和传统监督学习、非监督学习的区别，DeepMind Thore Graepel甚至直接认为二者是强化学习的特殊情况。[（Material）](https://www.youtube.com/watch?v=iOh7QUZGyiU&list=PLqYmG7hTraZDNJre23vqCGIVpfZ_K2RZs&index=1) 我的理解是刻意去找他们之间的关联并没有太多意义，而是需要理解每一种学习方式所适合的场景。对于强化学习，他解决的就是带有目标的决策问题，我们希望训练一个智能体来代替人在某些可以交互的环境下执行一系列决策，以获得最大回报。

### 现实中的一些例子
- 直升飞机特技动作:考虑智能体控制直升机控制器的多个按钮组合来完成一些特技动作
- 在Atari游戏中取得更高分：Atari提供了一系列非常适合训练强化学习算法的环境,DeepMind公司在几十个不同游戏上都训练出“超级玩家”
- 自动驾驶、机器人控制：在自然环境下，控制机械设备执行正确的操作，是AI的一个热门领域
- ...

### 强化学习问题的基本概念
####  reward
关于概念本身无需多言，比较有意思的是这三点：
- Reward Hypothesis：所有的目标都可以通过最大化期望聚集回报来描述
- Reward Value：有的问题智能体在每一步时都会获得一个非零reward，比如说自动驾驶；有的可能在任务结束时才可以给出非零的reward，比如说围棋比赛。
- 无论如何，我们考虑的都不仅仅只是每一步的回报，而是最大化整个未来回报的期望。

#### Environment and State
在吵闹的教室里，我们可能很难集中注意力学习，而最终刷起了手机。此时，教室是我们所处的环境，吵闹是我们的感官系统对于教室状态的一个描述，刷手机就算我们在该状态下的一个决策。

**Environment State、Agent State、Observation**
如何理解这三个概念的区别？如果把环境理解为客观物质世界（或者一些规则设定的场景），那么我理解的Environment State指的就是当前时刻客观世界中那些与任务相关的信息；Observation指的就是
一个智能体在当前时刻观察环境能得到的信息，能得到通常意味着可能不能获得所有信息；Agent State我的理解是智能体基于他已有的信息来产生自己对环境状态的理解，当然这种理解可能与真实情况  
并不完全一致。

**Information State**
信息状态的定义实际上就是具备马尔可夫性质的状态，这种性质也是RL的基础，我们希望RL问题中状态要满足这个性质。

**Fully Observable Environments**
完全可观测指的就是智能体可以观测到环境中与任务相关的所有信息，那么
$$O_t=S_t^a=S_t^e$$
貌似我们学习的问题大部分背景都假设在这种性质的环境下

**Partially Observable Environments**
这种性质的环境我的理解就是$S_t^e$不能被智能体完全获得，智能体通过观察拿到的信息只是一部分信息。  
形式化来说，这是一个[POMDP](https://en.wikipedia.org/wiki/Partially_observable_Markov_decision_process)问题。
解决这种问题你就需要结合历史信息来定义智能体自己对于环境状态的理解，即$S_t^a$,然后训练的策略是从这种状态到动作的映射。
当然你所定义的智能体状态，也是要满足Markov Property的。

Silver强调了状态需要区分主观状态（智能体所理解的环境状态），客观状态（环境实际存在的状态），一般情况下我们不做区分，除非环境对于智能体来说给予的信息非常有限

#### An RL Agent
一个强化学习的智能体主要由以下三个部分组成：
- Policy：顾名思义，决策的依据，是一个（状态，动作）的分布函数
- Value function：预测了未来回报，给出了状态和动作好坏衡量的定量值
- Model：一个模型预测环境的动态，即下一个状态和立即回报值

智能体的分类
##### （1）
- Value Based：只依赖Value Function决策，不依赖具体的Policy
- Policy Based：依赖Policy决策
- Actor Critic：Policy+Value Function
##### （2）
- Model Free：正统的强化学习问题
- Model Based：一个动态规划解决的优化问题

# 总结
接下来



