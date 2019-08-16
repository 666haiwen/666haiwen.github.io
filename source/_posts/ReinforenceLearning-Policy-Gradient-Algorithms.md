---
title: ReinforenceLearning--Policy Gradient Algorithms
date: 2019-08-16 14:33:32
tags:
- [Reinforcement Learning]
categories:
- [algorithm]
---
### Policy

Policy $\pi$,代表在状态$s$，会执行的动作$a$.(分为确定性和随机性)

- Deterministic: $\pi(s)=a.$
- Stochastic: $π(a|s)=\mathbb{P}_π[A=a|S=s]$

==> $π_\theta(a|s)=\mathbb{P}_π[A=a|S=s,\theta]$



#### Policy Gradient

**object function**:

**episodic environments:**

$J_1(\theta)=V^{\pi_\theta}(s_1)=\mathbb{E}_{\pi_\theta}[V_1]$

**continuing environments:**

*连续型环境就没有初始状态一说了，那么就取平均，考虑agent在某时刻处于某个状态下的概率，即状态分布*

**average value:**

$J_{avV}(\theta)=\sum_sd^{\pi_\theta}(s)V^{\pi_\theta}(s)$

对每个可能的状态计算从该时刻(该状态)开始于环境一直交互下去的奖励，然后对其概率分布求和.

**average reward per time-step:**

$J_{avR}(\theta)=\sum_sd^{\pi_\theta}(s)\sum_a\pi_\theta(s,a)\mathcal{R}_s^a$

其中,$d^{\pi_\theta}(s)$是马尔科夫链在$\pi_\theta$下的随机概率分布；即$d^π(s)=lim_{t→∞}P(s_t=s|s_0,π_θ)$就表示你从状态$s_0$开始，在策略$π_θ$下经过$t$个时间步后到达状态$s$的概率。

该式代表了到达某个状态$s$,并且采用动作$a$的情况下，获得的平均回报$\mathcal{R_s^a}$,概率化累加就是平均回报.

这个可以如下计算(以李宏毅教授PPT为例)，每条迹的概率*该条迹累计的期望即为平均

![](ReinforenceLearning-Policy-Gradient-Algorithms\ac-1.png)

目标是将目标函数最大化，可以用梯度下降法将其最大化

*注：用基于梯度的策略优化时，是基于序列结构片段，如果无穷地和环境交互，得到一个结果是没有意义的；就是和环境交互中的某一个序列，将其拿出来进行学习，然后优化策略*

**one-step MDP(per time-step):**
$$
\begin{split}
J(\theta)&=\sum_sd^{\pi_\theta}(s)\sum_a\pi_\theta(s,a)\mathcal{R}_s^a  
\\
\nabla_\theta J(\theta)&=\sum_sd^{\pi_\theta}(s)\sum_a\pi_\theta(s,a)\nabla_\theta log\pi_\theta(s,a)\mathcal{R}_s^a
\end{split}
$$


#### ==>policy gradient theorem

![](ReinforenceLearning-Policy-Gradient-Algorithms\ac-2.png)

#### ==>李宏毅教授PPT

![AC-3](ReinforenceLearning-Policy-Gradient-Algorithms\AC-3.png)

<br>

### Actor-Critic

AC是在基于Policy Gradient的基础上进行了变化，融合了Value based的方法.

Actor:就是把$J(\theta)$最大化，但是梯度里面的$Q^{\pi_\theta}(s,a)$用Value based的方法来计算，结果如下：

![AC-4](ReinforenceLearning-Policy-Gradient-Algorithms\AC-4.png)

### Reference

博客:

<https://lilianweng.github.io/lil-log/2018/02/19/a-long-peek-into-reinforcement-learning.html#deadly-triad-issue>

<https://lilianweng.github.io/lil-log/2018/04/08/policy-gradient-algorithms.html>

李宏毅教授：

[youtube]: https://www.youtube.com/playlist?list=PLJV_el3uVTsODxQFgzMzPLa16h6B8kWM_	"youtube"
[课程网站]: http://speech.ee.ntu.edu.tw/~tlkagk/courses_MLDS18.html	"课程网站"

David_Silver:

[视频]: https://www.bilibili.com/video/av45357759/?p=7	"视频"

配套PPT

Mnih, Volodymyr, et al. [“Asynchronous methods for deep reinforcement learning.”](https://arxiv.org/abs/1602.01783) ICML. 2016.

David Silver, et al. [“Deterministic policy gradient algorithms.”](https://hal.inria.fr/file/index/docid/938992/filename/dpg-icml2014.pdf) ICML. 2014.

Timothy P. Lillicrap, et al. [“Continuous control with deep reinforcement learning.”](https://arxiv.org/pdf/1509.02971.pdf) arXiv preprint arXiv:1509.02971 (2015).

