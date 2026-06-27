---
title: "Markov decision process"
source: "https://en.wikipedia.org/wiki/Markov_decision_process"
author:
  - "[[Wikipedia]]"
published: 2004-11-01
created: 2026-06-26
description:
tags:
  - "clippings"
---
A **Markov decision process** (**MDP**) is a mathematical model for [sequential decision making](https://en.wikipedia.org/wiki/Sequential_decision_making "Sequential decision making") when [outcomes](https://en.wikipedia.org/wiki/Outcome_\(probability\) "Outcome (probability)") are uncertain.[^1] It is a type of stochastic decision process [^2], and is often solved using the methods of [stochastic dynamic programming](https://en.wikipedia.org/wiki/Stochastic_dynamic_programming "Stochastic dynamic programming").

Originating from [operations research](https://en.wikipedia.org/wiki/Operations_research "Operations research") in the 1950s,[^3] [^4] MDPs have since gained recognition in a variety of fields, including [ecology](https://en.wikipedia.org/wiki/Ecology "Ecology"), [economics](https://en.wikipedia.org/wiki/Economics "Economics"), [healthcare](https://en.wikipedia.org/wiki/Health_care "Health care"), [telecommunications](https://en.wikipedia.org/wiki/Telecommunications "Telecommunications") and [reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning "Reinforcement learning").[^5] Reinforcement learning utilizes the MDP framework to model the interaction between a learning agent and its environment. In this framework, the interaction is characterized by states, actions, and rewards. The MDP framework is designed to provide a simplified representation of key elements of [artificial intelligence](https://en.wikipedia.org/wiki/Artificial_intelligence "Artificial intelligence") challenges. This modeling framework incorporates the understanding of [cause and effect](https://en.wikipedia.org/wiki/Causality "Causality"), the management of uncertainty and nondeterminism, and the pursuit of explicit goals.[^5]

The name comes from its connection to [Markov chains](https://en.wikipedia.org/wiki/Markov_chain "Markov chain"), a concept developed by the Russian mathematician [Andrey Markov](https://en.wikipedia.org/wiki/Andrey_Markov "Andrey Markov"). The "Markov" in "Markov decision process" refers to the underlying structure of [state transitions](https://en.wikipedia.org/wiki/Transition_system "Transition system") that still follow the [Markov property](https://en.wikipedia.org/wiki/Markov_property "Markov property"). The process is called a "decision process" because it involves making decisions that influence these state transitions, extending the concept of a Markov chain into the realm of decision-making under uncertainty.

## Definition

![](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ad/Markov_Decision_Process.svg/500px-Markov_Decision_Process.svg.png)

Example of a simple MDP with three states (green circles) and two actions (orange circles), with two rewards (orange arrows)

A Markov decision process is a 4- [tuple](https://en.wikipedia.org/wiki/Tuple "Tuple") ${\displaystyle (S,A,P_{a},R_{a})}$, where:

- ${\displaystyle S}$ is a [set](https://en.wikipedia.org/wiki/Set_\(mathematics\) "Set (mathematics)") of states called the *state space*. The state space may be discrete or continuous, like the [set of real numbers](https://en.wikipedia.org/wiki/Set_of_real_numbers "Set of real numbers").
- ${\displaystyle A}$ is a set of actions called the *action space* (alternatively, ${\displaystyle A_{s}}$ is the set of actions available from state ${\displaystyle s}$). As for state, this set may be discrete or continuous.
- ${\displaystyle P_{a}(s,s')}$ is, on an intuitive level, the probability that action ${\displaystyle a}$ in state ${\displaystyle s}$ at time ${\displaystyle t}$ will lead to state ${\displaystyle s'}$ at time ${\displaystyle t+1}$. In general, this probability transition is defined to satisfy ${\displaystyle \Pr(s_{t+1}\in S'\mid s_{t}=s,a_{t}=a)=\int _{S'}P_{a}(s,s')ds',}$ for every ${\displaystyle S'\subseteq S}$ measurable. In case the state space is discrete, the integral is intended with respect to the [counting measure](https://en.wikipedia.org/wiki/Counting_measure "Counting measure"), so that the latter simplifies as ${\displaystyle P_{a}(s,s')=\Pr(s_{t+1}=s'\mid s_{t}=s,a_{t}=a)}$; in case ${\displaystyle S\subseteq \mathbb {R} ^{d}}$, the integral is usually intended with respect to the [Lebesgue measure](https://en.wikipedia.org/wiki/Lebesgue_measure "Lebesgue measure").
- ${\displaystyle R_{a}(s,s')}$ is the immediate reward (or expected immediate reward) received after action ${\displaystyle a}$ is taken to transition from state ${\displaystyle s}$ to state ${\displaystyle s'}$. The reward is in general a [random variable](https://en.wikipedia.org/wiki/Random_variable "Random variable").

A policy function ${\displaystyle \pi }$ is a (potentially probabilistic) mapping from state space (${\displaystyle S}$) to action space (${\displaystyle A}$).

### Optimization objective

The goal in a Markov decision process is to find a good "policy" for the decision maker: a function ${\displaystyle \pi }$ that specifies the action ${\displaystyle \pi (s)}$ that the decision maker will choose when in state ${\displaystyle s}$. Once a Markov decision process is combined with a policy in this way, this fixes the action for each state and the resulting combination behaves like a [Markov chain](https://en.wikipedia.org/wiki/Markov_chain "Markov chain") (since the action chosen in state ${\displaystyle s}$ is completely determined by ${\displaystyle \pi (s)}$).

The objective is to choose a policy ${\displaystyle \pi }$ that will maximize some cumulative function of the random rewards, typically the expected discounted sum over a potentially infinite horizon:

${\displaystyle E\left[\sum _{t=0}^{\infty }{\gamma ^{t}R_{a_{t}}(s_{t},s_{t+1})}\right]}$ (where we choose ${\displaystyle a_{t}=\pi (s_{t})}$, i.e. actions given by the policy). And the expectation is taken over ${\displaystyle s_{t+1}\sim P_{a_{t}}(s_{t},s_{t+1})}$

where ${\displaystyle \ \gamma \ }$ is the discount factor satisfying ${\displaystyle 0\leq \ \gamma \ \leq \ 1}$, which is usually close to ${\displaystyle 1}$ (for example, ${\displaystyle \gamma =1/(1+r)}$ for some discount rate ${\displaystyle r}$). A lower discount factor makes the decision maker more short-sighted, in that it comparatively disregards the effect that following its current policy has at times lying further in the future.

Another possible, but strictly related, objective that is commonly used is the ${\displaystyle H-}$ step return. This time, instead of using a discount factor ${\displaystyle \ \gamma \ }$, the agent is interested only in the first ${\displaystyle H}$ steps of the process, with each reward having the same weight.

${\displaystyle E\left[\sum _{t=0}^{H-1}{R_{a_{t}}(s_{t},s_{t+1})}\right]}$ (where we choose ${\displaystyle a_{t}=\pi (s_{t})}$, i.e. actions given by the policy). And the expectation is taken over ${\displaystyle s_{t+1}\sim P_{a_{t}}(s_{t},s_{t+1})}$

where ${\displaystyle \ H\ }$ is the time horizon. Compared to the previous objective, the latter one is more used in [Learning Theory](https://en.wikipedia.org/w/index.php?title=Learning_Theory&action=edit&redlink=1 "Learning Theory (page does not exist)").

A policy that maximizes the function above is called an *optimal policy* and is usually denoted ${\displaystyle \pi ^{*}}$. A particular MDP may have multiple distinct optimal policies. Because of the [Markov property](https://en.wikipedia.org/wiki/Markov_property "Markov property"), it can be shown that the optimal policy is a function of the current state, as assumed above. When ${\displaystyle R_{a}(s,s')}$ is deterministic, there will always exist an optimal policy ${\displaystyle \pi ^{*}}$ which is deterministic as well.

\[Proof\]

Assume that ${\displaystyle R}$ is deterministic, meaning for constants ${\displaystyle a,s,s'}$ the value ${\displaystyle R_{a}(s,s')}$ is also constant. For ${\displaystyle \gamma <1}$ [it is known](#Value_iteration) that there exists a unique fixed point ${\displaystyle V^{*}}$ which satisfies the value iteration (Bellman equation) recursion

$$
{\displaystyle V^{*}(s)=\max _{a}E\left[R_{a}(s,s')+\gamma V^{*}(s')\right]}
$$

From inspection, notice that this fixed point is the value function associated to the following policy.

$$
{\displaystyle \pi ^{*}(s):=\arg \max _{a}E\left[R_{a}(s,s')+\gamma V^{*}(s')\right]}
$$

By unrolling the Bellman recursion, one can show that ${\displaystyle V^{*}}$ is indeed optimal (simultaneously for all states) over the set of deterministic policies.

$$
{\displaystyle {\begin{aligned}V^{*}(s_{0})&=\max _{a_{0}}E\left[R_{a_{0}}(s_{0},s_{1})+\gamma V^{*}(s_{1})\right]\\&=\max _{a_{0}}E\left[R_{a_{0}}(s_{0},s_{1})+\gamma \max _{a_{1}}E\left[R_{a_{1}}(s_{1},s_{2})+\gamma V^{*}(s_{2})\right]\right]\\&=\max _{a_{0},a_{1}}E\left[R_{a_{0}}(s_{0},s_{1})+\gamma \left(R_{a_{1}}(s_{1},s_{2})+\gamma V^{*}(s_{2})\right)\right]\\&=\sup _{\{a_{t}\}_{t=0}^{\infty }}E\left[\sum _{t=0}^{\infty }\gamma ^{t}R_{a_{t}}(s_{t},s_{t+1})\right]\end{aligned}}}
$$

Consider the case where ${\displaystyle \pi }$ is probabilistic, meaning the action taken ${\displaystyle a:=\pi (s)}$ is a random variable. One can show any such non-deterministic policy is dominated by deterministic ${\displaystyle \pi ^{*}}$ as follows.

$$
{\displaystyle {\begin{aligned}V^{*}(s_{0})&=\max _{a_{0}}E\left[R_{a_{0}}(s_{0},s_{1})+\gamma V^{*}(s_{1})\right]\\&\geq E\left[R_{\pi (s_{0})}(s_{0},s_{1})+\gamma V^{*}(s_{1})\right]\\&=E\left[R_{\pi (s_{0})}(s_{0},s_{1})+\gamma \max _{a_{1}}E\left[R_{a_{1}}(s_{1},s_{2})+\gamma V^{*}(s_{2})\right]\right]\\&\geq E\left[R_{\pi (s_{0})}(s_{0},s_{1})+\gamma \left(R_{\pi (s_{1})}(s_{1},s_{2})+\gamma V^{*}(s_{2})\right)\right]\\&\geq E\left[\sum _{t=0}^{\infty }\gamma ^{t}R_{\pi (s_{t})}(s_{t},s_{t+1})\right]\end{aligned}}}
$$

### Simulator models

In many cases, it is difficult to represent the transition probability distributions, ${\displaystyle P_{a}(s,s')}$, explicitly. In such cases, a simulator can be used to model the MDP implicitly by providing samples from the transition distributions. One common form of implicit MDP model is an episodic environment simulator that can be started from an initial state and yields a subsequent state and reward every time it receives an action input. In this manner, trajectories of states, actions, and rewards, often called *episodes* may be produced.

Another form of simulator is a *generative model*, a single step simulator that can generate samples of the next state and reward given any state and action.[^6] (Note that this is a different meaning from the term [generative model](https://en.wikipedia.org/wiki/Generative_model "Generative model") in the context of [statistical classification](https://en.wikipedia.org/wiki/Statistical_classification "Statistical classification").) In [algorithms](https://en.wikipedia.org/wiki/Algorithms "Algorithms") that are expressed using [pseudocode](https://en.wikipedia.org/wiki/Pseudocode "Pseudocode"), ${\displaystyle G}$ is often used to represent a generative model. For example, the expression ${\displaystyle s',r\gets G(s,a)}$ might denote the action of sampling from the generative model where ${\displaystyle s}$ and ${\displaystyle a}$ are the current state and action, and ${\displaystyle s'}$ and ${\displaystyle r}$ are the new state and reward. Compared to an episodic simulator, a generative model has the advantage that it can yield data from any state, not only those encountered in a trajectory.

These model classes form a hierarchy of information content: an explicit model trivially yields a generative model through sampling from the distributions, and repeated application of a generative model yields an episodic simulator. In the opposite direction, it is only possible to learn approximate models through [regression](https://en.wikipedia.org/wiki/Regression_analysis "Regression analysis"). The type of model available for a particular MDP plays a significant role in determining which solution algorithms are appropriate. For example, the [dynamic programming](https://en.wikipedia.org/wiki/Dynamic_programming "Dynamic programming") algorithms described in the next section require an explicit model, and [Monte Carlo tree search](https://en.wikipedia.org/wiki/Monte_Carlo_tree_search "Monte Carlo tree search") requires a generative model (or an episodic simulator that can be copied at any state), whereas most [reinforcement learning](#Reinforcement_learning) algorithms require only an episodic simulator.

## Example

![](https://upload.wikimedia.org/wikipedia/commons/thumb/4/4f/Cartpole.gif/250px-Cartpole.gif)

Pole Balancing example (rendering of the environment from the Open AI gym benchmark )

An example of MDP is the Pole-Balancing model, which comes from classic control theory.

In this example, we have

- ${\displaystyle S}$ is the set of ordered tuples ${\displaystyle (\theta ,{\dot {\theta }},x,{\dot {x}})}$ given by pole angle, angular velocity, position of the cart and its speed.
- ${\displaystyle A}$ is ${\displaystyle \{-1,1\}}$, corresponding to applying a force on the left (right) on the cart.
- ${\displaystyle P_{a}(s,s')}$ is the transition of the system, which in this case is going to be deterministic and driven by the laws of mechanics.
- ${\displaystyle R_{a}(s,s')}$ is ${\displaystyle 1}$ if the pole is up after the transition, zero otherwise. Therefore, this function only depend on ${\displaystyle s'}$ in this specific case.

## Algorithms

Solutions for MDPs with finite state and action spaces may be found through a variety of methods such as [dynamic programming](https://en.wikipedia.org/wiki/Dynamic_programming "Dynamic programming"). The algorithms in this section apply to MDPs with finite state and action spaces and explicitly given transition probabilities and reward functions, but the basic concepts may be extended to handle other problem classes, for example using [function approximation](https://en.wikipedia.org/wiki/Function_approximation "Function approximation"). Also, some processes with countably infinite state and action spaces can be *exactly* reduced to ones with finite state and action spaces.[^7]

The standard family of algorithms to calculate optimal policies for finite state and action MDPs requires storage for two arrays indexed by state: *value* ${\displaystyle V}$, which contains real values, and *policy* ${\displaystyle \pi }$, which contains actions. At the end of the algorithm, ${\displaystyle \pi }$ will contain the solution and ${\displaystyle V(s)}$ will contain the discounted sum of the rewards to be earned (on average) by following that solution from state ${\displaystyle s}$.

The algorithm has two steps, (1) a value update and (2) a policy update, which are repeated in some order for all the states until no further changes take place. Both recursively update a new estimation of the optimal policy and state value using an older estimation of those values.

${\displaystyle V(s):=\sum _{s'}P_{\pi (s)}(s,s')\left(R_{\pi (s)}(s,s')+\gamma V(s')\right)}$

${\displaystyle \pi (s):=\operatorname {argmax} _{a}\left\{\sum _{s'}P_{a}(s,s')\left(R_{a}(s,s')+\gamma V(s')\right)\right\}}$

Their order depends on the variant of the algorithm; one can also do them for all states at once or state by state, and more often to some states than others. As long as no state is permanently excluded from either of the steps, the algorithm will eventually arrive at the correct solution.[^8]

### Notable variants

#### Value iteration

In value iteration ([Bellman 1957](#CITEREFBellman1957)), which is also called [backward induction](https://en.wikipedia.org/wiki/Backward_induction "Backward induction"), the ${\displaystyle \pi }$ function is not used; instead, the value of ${\displaystyle \pi (s)}$ is calculated within ${\displaystyle V(s)}$ whenever it is needed. Substituting the calculation of ${\displaystyle \pi (s)}$ into the calculation of ${\displaystyle V(s)}$ gives the combined step;

${\displaystyle V_{i+1}(s):=\max _{a}\left\{\sum _{s'}P_{a}(s,s')\left(R_{a}(s,s')+\gamma V_{i}(s')\right)\right\},}$

where ${\displaystyle i}$ is the iteration number. Value iteration starts at ${\displaystyle i=0}$ and ${\displaystyle V_{0}}$ as a guess of the [value function](https://en.wikipedia.org/wiki/Value_function "Value function"). It then iterates, repeatedly computing ${\displaystyle V_{i+1}}$ for all states ${\displaystyle s}$, until ${\displaystyle V}$ converges with the left-hand side equal to the right-hand side (which is the " [Bellman equation](https://en.wikipedia.org/wiki/Bellman_equation "Bellman equation") " for this problem). [Lloyd Shapley](https://en.wikipedia.org/wiki/Lloyd_Shapley "Lloyd Shapley") 's 1953 paper on [stochastic games](https://en.wikipedia.org/wiki/Stochastic_games "Stochastic games") included as a special case the value iteration method for MDPs,[^9] but this was recognized only later on.[^10]

Value iteration is guaranteed to converge for ${\displaystyle \gamma <1}$ by the [Banach fixed-point theorem](https://en.wikipedia.org/wiki/Banach_fixed-point_theorem "Banach fixed-point theorem").

\[Proof\]

The Banach fixed-point theorem states that a given contraction mapping has a unique fixed point; further, one can asymptotically approach this fixed points by iterated application of the contraction mapping. It then suffices to show that value iteration is a contraction mapping, which is shown below for ${\displaystyle \gamma <1}$.

Denote ${\displaystyle X_{a}^{V}(s):=\sum _{s'}P_{a}(s,s')\left(R_{a}(s,s')+\gamma V_{i}(s')\right)}$ and ${\displaystyle ({\mathcal {B}}V)(s):=\max _{a}X_{a}^{V}(s)}$ for convenience.

$$
{\displaystyle {\begin{aligned}\|{\mathcal {B}}V-{\mathcal {B}}W\|_{\infty }&=\max _{s}\left|({\mathcal {B}}V)(s)-({\mathcal {B}}W)(s)\right|\\&=\max _{s}\left|\max _{a}X_{a}^{V}(s)-\max _{a}X_{a}^{W}(s)\right|\\&\leq \max _{s}\max _{a}\left|X_{a}^{V}(s)-X_{a}^{W}(s)\right|\\&=\max _{s}\max _{a}\gamma \left|\sum _{s'}P_{a}(s,s')\left(V_{i}(s')-W_{i}(s')\right)\right|\\&\leq \max _{s}\max _{a}\gamma \max _{s'}\left|V_{i}(s')-W_{i}(s')\right|\\&=\gamma \max _{s'}\left|V_{i}(s')-W_{i}(s')\right|\\&=\gamma \|V_{i}-W_{i}\|_{\infty }\end{aligned}}}
$$

#### Policy iteration

In policy iteration [^11], one first performs *Value Determination* by solving for ${\displaystyle V}$ from the linear system described in step one, then performs *Policy Improvement* by computing ${\displaystyle \pi }$ as in step two, then repeats both steps until the policy converges. (Policy iteration was invented by Howard to optimize [Sears](https://en.wikipedia.org/wiki/Sears "Sears") catalogue mailing, which he had been optimizing using value iteration.[^12])

Since policy iteration effectively interleaves a linear [inverse problem](https://en.wikipedia.org/wiki/Inverse_problem "Inverse problem") with a nonlinear operation, it may interpreted as a type of [relaxation](https://en.wikipedia.org/wiki/Relaxation_\(iterative_method\) "Relaxation (iterative method)") method.

This variant has the advantage that there is a definite stopping condition. Since there is a unique solution ${\displaystyle V}$ for each policy ${\displaystyle \pi }$, the algorithm is completed once the *Policy Improvement* produces the same policy twice consecutively.

While there are situations where policy iteration may be faster than value iteration (e.g. when the action space is significantly larger than the state space), policy iteration is usually slower than value iteration for a large number of possible states.

#### Modified policy iteration

In modified policy iteration ([van Nunen 1976](#CITEREFvan_Nunen1976); [Puterman & Shin 1978](#CITEREFPutermanShin1978)), step one is repeated several times, and then step two is performed once.[^13] [^14] Then step one is again repeated several times and so on.

#### Prioritized sweeping

In this variant, the steps are preferentially applied to states which are in some way important – whether based on the algorithm (there were large changes in ${\displaystyle V}$ or ${\displaystyle \pi }$ around those states recently) or based on use (those states are near the starting state, or otherwise of interest to the person or program using the algorithm).

### Computational complexity

Algorithms for finding optimal policies with [time complexity](https://en.wikipedia.org/wiki/Time_complexity "Time complexity") polynomial in the size of the problem representation exist for finite MDPs. Thus, [decision problems](https://en.wikipedia.org/wiki/Decision_problem "Decision problem") based on MDPs are in computational [complexity class](https://en.wikipedia.org/wiki/Complexity_class "Complexity class") [P](https://en.wikipedia.org/wiki/P_\(complexity\) "P (complexity)").[^15] However, due to the [curse of dimensionality](https://en.wikipedia.org/wiki/Curse_of_dimensionality "Curse of dimensionality"), the size of the problem representation is often exponential in the number of state and action variables, limiting exact solution techniques to problems that have a compact representation. In practice, online planning techniques such as [Monte Carlo tree search](https://en.wikipedia.org/wiki/Monte_Carlo_tree_search "Monte Carlo tree search") can find useful solutions in larger problems, and, in theory, it is possible to construct online planning algorithms that can find an arbitrarily near-optimal policy with no computational complexity dependence on the size of the state space.[^16]

## Extensions and generalizations

A Markov decision process is a [stochastic game](https://en.wikipedia.org/wiki/Stochastic_game "Stochastic game") with only one player.

### Partial observability

The solution above assumes that the state ${\displaystyle s}$ is known when action is to be taken; otherwise ${\displaystyle \pi (s)}$ cannot be calculated. When this assumption is not true, the problem is called a partially observable Markov decision process or POMDP.

### Constrained Markov decision processes

Constrained Markov decision processes (CMDPS) are extensions to Markov decision process (MDPs). There are three fundamental differences between MDPs and CMDPs.[^17]

- There are multiple costs incurred after applying an action instead of one.
- CMDPs are solved with [linear programs](https://en.wikipedia.org/wiki/Linear_programming "Linear programming") only, and [dynamic programming](https://en.wikipedia.org/wiki/Dynamic_programming "Dynamic programming") does not work.
- The final policy depends on the starting state.

The method of [Lagrange multipliers](https://en.wikipedia.org/wiki/Lagrange_multiplier "Lagrange multiplier") applies to CMDPs. Many Lagrangian-based algorithms have been developed.

- Natural policy gradient primal-dual method.[^18]

There are a number of applications for CMDPs. It has recently been used in [motion planning](https://en.wikipedia.org/wiki/Motion_planning "Motion planning") scenarios in robotics.[^19]

### Continuous-time Markov decision process

In discrete-time Markov Decision Processes, decisions are made at discrete time intervals. However, for **continuous-time Markov decision processes**, decisions can be made at any time the decision maker chooses. In comparison to discrete-time Markov decision processes, continuous-time Markov decision processes can better model the decision-making process for a system that has [continuous dynamics](https://en.wikipedia.org/wiki/Continuous_time "Continuous time"), i.e., the system dynamics are defined by [ordinary differential equations](https://en.wikipedia.org/wiki/Ordinary_differential_equation "Ordinary differential equation") (ODEs). This modelling framework can be applied to areas such as [queueing systems](https://en.wikipedia.org/wiki/Queueing_system "Queueing system"), epidemic processes, and [population processes](https://en.wikipedia.org/wiki/Population_process "Population process").

Like the discrete-time Markov decision processes, in continuous-time Markov decision processes the agent aims to find the optimal *policy* that would maximize the expected cumulative reward. The key difference with the standard case is that, due to the continuous nature of the time variable, summation is replaced by an integral:

${\displaystyle \max \operatorname {E} _{\pi }\left[\left.\int _{0}^{\infty }\gamma ^{t}r(s(t),\pi (s(t)))\,dt\;\right|s_{0}\right]}$

where ${\displaystyle 0\leq \gamma <1.}$

#### Discrete space: Linear programming formulation

If the state space and action space are finite, we could use linear programming to find the optimal policy, which was one of the earliest approaches applied. Here we only consider the ergodic model, which means our continuous-time MDP becomes an [ergodic](https://en.wikipedia.org/wiki/Ergodicity "Ergodicity") continuous-time Markov chain under a stationary [policy](https://en.wikipedia.org/wiki/Policy "Policy"). Under this assumption, although the decision maker can make a decision at any time in the current state, there is no benefit in taking multiple actions. It is better to take an action only at the time when system is transitioning from the current state to another state. Under some conditions,[^20] if our optimal value function ${\displaystyle V^{*}}$ is independent of state ${\displaystyle i}$, we will have the following inequality:

${\displaystyle g\geq R(i,a)+\sum _{j\in S}q(j\mid i,a)h(j)\quad \forall i\in S{\text{ and }}a\in A(i)}$

If there exists a function ${\displaystyle h}$, then ${\displaystyle {\bar {V}}^{*}}$ will be the smallest ${\displaystyle g}$ satisfying the above equation. In order to find ${\displaystyle {\bar {V}}^{*}}$, we could use the following linear programming model:

- Primal linear program(P-LP)

${\displaystyle {\begin{aligned}{\text{Minimize}}\quad &g\\{\text{s.t}}\quad &g-\sum _{j\in S}q(j\mid i,a)h(j)\geq R(i,a)\,\,\forall i\in S,\,a\in A(i)\end{aligned}}}$

- Dual linear program(D-LP)

${\displaystyle {\begin{aligned}{\text{Maximize}}&\sum _{i\in S}\sum _{a\in A(i)}R(i,a)y(i,a)\\{\text{s.t.}}&\sum _{i\in S}\sum _{a\in A(i)}q(j\mid i,a)y(i,a)=0\quad \forall j\in S,\\&\sum _{i\in S}\sum _{a\in A(i)}y(i,a)=1,\\&y(i,a)\geq 0\qquad \forall a\in A(i){\text{ and }}\forall i\in S\end{aligned}}}$

${\displaystyle y(i,a)}$ is a feasible solution to the D-LP if ${\displaystyle y(i,a)}$ is nonnative and satisfied the constraints in the D-LP problem. A feasible solution ${\displaystyle y^{*}(i,a)}$ to the D-LP is said to be an optimal solution if

${\displaystyle {\begin{aligned}\sum _{i\in S}\sum _{a\in A(i)}R(i,a)y^{*}(i,a)\geq \sum _{i\in S}\sum _{a\in A(i)}R(i,a)y(i,a)\end{aligned}}}$

for all feasible solution ${\displaystyle y(i,a)}$ to the D-LP. Once we have found the optimal solution ${\displaystyle y^{*}(i,a)}$, we can use it to establish the optimal policies.

#### Continuous space: Hamilton–Jacobi–Bellman equation

In continuous-time MDP, if the state space and action space are continuous, the optimal criterion could be found by solving the [Hamilton–Jacobi–Bellman (HJB) partial differential equation](https://en.wikipedia.org/wiki/Hamilton%E2%80%93Jacobi%E2%80%93Bellman_equation "Hamilton–Jacobi–Bellman equation"). In order to discuss the HJB equation, we need to reformulate our problem

${\displaystyle {\begin{aligned}V(s(0),0)={}&\max _{a(t)=\pi (s(t))}\int _{0}^{T}r(s(t),a(t))\,dt+D[s(T)]\\{\text{s.t.}}\quad &{\frac {ds(t)}{dt}}=f[t,s(t),a(t)]\end{aligned}}}$

${\displaystyle D(\cdot )}$ is the terminal reward function, ${\displaystyle s(t)}$ is the system state vector, ${\displaystyle a(t)}$ is the system control vector we try to find. ${\displaystyle f(\cdot )}$ shows how the state vector changes over time. The Hamilton–Jacobi–Bellman equation is as follows:

${\displaystyle 0=\max _{a}(r(t,s,a)+{\frac {\partial V(t,s)}{\partial s}}f(t,s,a))}$

We could solve the equation to find the optimal [value function](https://en.wikipedia.org/wiki/Value_function "Value function") ${\displaystyle V^{*}}$, which in turns yield the optimal control at any time ${\displaystyle t}$, ${\displaystyle a(t)}$ through ${\displaystyle a(t)={\underset {a}{\text{argmax}}}(r(t,s,a)+{\frac {\partial V^{*}(t,s)}{\partial s}}f(t,s,a)).}$

## Reinforcement learning

[Reinforcement learning](https://en.wikipedia.org/wiki/Reinforcement_learning "Reinforcement learning") is an interdisciplinary area of [machine learning](https://en.wikipedia.org/wiki/Machine_learning "Machine learning") and [optimal control](https://en.wikipedia.org/wiki/Optimal_control "Optimal control") that has, as main objective, finding an approximately optimal policy for MDPs where transition probabilities and rewards are unknown.[^21]

Reinforcement learning can solve Markov-Decision processes without explicit specification of the transition probabilities which are instead needed to perform policy iteration. In this setting, transition probabilities and rewards must be learned from experience, i.e. by letting an agent interact with the MDP for a given number of steps. Both on a theoretical and on a practical level, effort is put in maximizing the sample efficiency, i.e. minimimizing the number of samples needed to learn a policy whose performance is ${\displaystyle \varepsilon -}$ close to the optimal one (due to the stochastic nature of the process, learning the optimal policy with a finite number of samples is, in general, impossible).

### Reinforcement Learning for discrete MDPs

For the purpose of this section, it is useful to define a further function, which corresponds to taking the action ${\displaystyle a}$ and then continuing optimally (or according to whatever policy one currently has):

${\displaystyle \ Q(s,a)=\sum _{s'}P_{a}(s,s')(R_{a}(s,s')+\gamma V(s')).\ }$

While this function is also unknown, experience during learning is based on ${\displaystyle (s,a)}$ pairs (together with the outcome ${\displaystyle s'}$; that is, "I was in state ${\displaystyle s}$ and I tried doing ${\displaystyle a}$ and ${\displaystyle s'}$ happened"). Thus, one has an array ${\displaystyle Q}$ and uses experience to update it directly. This is known as [Q-learning](https://en.wikipedia.org/wiki/Q-learning "Q-learning").

## Other scopes

### Learning automata

Another application of MDP process in [machine learning](https://en.wikipedia.org/wiki/Machine_learning "Machine learning") theory is called learning automata. This is also one type of reinforcement learning if the environment is stochastic. The first detail **learning automata** paper is surveyed by [Narendra](https://en.wikipedia.org/wiki/Kumpati_S._Narendra "Kumpati S. Narendra") and Thathachar (1974), which were originally described explicitly as [finite-state automata](https://en.wikipedia.org/wiki/Finite-state_automata "Finite-state automata").[^22] Similar to reinforcement learning, a learning automata algorithm also has the advantage of solving the problem when probability or rewards are unknown. The difference between learning automata and Q-learning is that the former technique omits the memory of Q-values, but updates the action probability directly to find the learning result. Learning automata is a learning scheme with a rigorous proof of convergence.[^23]

In learning automata theory, **a stochastic automaton** consists of:

- a set *x* of possible inputs,
- a set Φ = { Φ <sub>1</sub>,..., Φ <sub><i>s</i></sub> } of possible internal states,
- a set α = { α <sub>1</sub>,..., α <sub><i>r</i></sub> } of possible outputs, or actions, with *r* ≤ *s*,
- an initial state probability vector *p* (0) = ≪ *p* <sub>1</sub> (0),..., *p <sub>s</sub>* (0) ≫,
- a [computable function](https://en.wikipedia.org/wiki/Computable_function "Computable function") *A* which after each time step *t* generates *p* (*t* + 1) from *p* (*t*), the current input, and the current state, and
- a function *G*: Φ → α which generates the output at each time step.

The states of such an automaton correspond to the states of a "discrete-state discrete-parameter [Markov process](https://en.wikipedia.org/wiki/Markov_process "Markov process") ".[^24] At each time step *t* = 0,1,2,3,..., the automaton reads an input from its environment, updates P(*t*) to P(*t* + 1) by *A*, randomly chooses a successor state according to the probabilities P(*t* + 1) and outputs the corresponding action. The automaton's environment, in turn, reads the action and sends the next input to the automaton.[^23]

### Category theoretic interpretation

Other than the rewards, a Markov decision process ${\displaystyle (S,A,P)}$ can be understood in terms of [Category theory](https://en.wikipedia.org/wiki/Category_theory "Category theory"). Namely, let ${\displaystyle {\mathcal {A}}}$ denote the [free monoid](https://en.wikipedia.org/wiki/Free_monoid "Free monoid") with generating set *A*. Let **Dist** denote the [Kleisli category](https://en.wikipedia.org/wiki/Kleisli_category "Kleisli category") of the [Giry monad](http://ncatlab.org/nlab/show/Giry+monad). Then a functor ${\displaystyle {\mathcal {A}}\to \mathbf {Dist} }$ encodes both the set *S* of states and the probability function *P*.

In this way, Markov decision processes could be generalized from monoids (categories with one object) to arbitrary categories. One can call the result ${\displaystyle ({\mathcal {C}},F:{\mathcal {C}}\to \mathbf {Dist} )}$ a *context-dependent Markov decision process*, because moving from one object to another in ${\displaystyle {\mathcal {C}}}$ changes the set of available actions and the set of possible states.

## Alternative notations

The terminology and notation for MDPs are not entirely settled. There are two main streams — one focuses on maximization problems from contexts like economics, using the terms action, reward, value, and calling the discount factor β or γ, while the other focuses on minimization problems from engineering and navigation, using the terms control, cost, cost-to-go, and calling the discount factor α. In addition, the notation for the transition probability varies.

| in this article | alternative | comment |
| --- | --- | --- |
| action a | control u |  |
| reward R | cost g | g is the negative of R |
| value V | cost-to-go J | J is the negative of V |
| policy π | policy μ |  |
| discounting factor γ | discounting factor α |  |
| transition probability ${\displaystyle P_{a}(s,s')}$ | transition probability ${\displaystyle p_{ss'}(a)}$ |  |

In addition, transition probability is sometimes written ${\displaystyle \Pr(s,a,s')}$, ${\displaystyle \Pr(s'\mid s,a)}$ or, rarely, ${\displaystyle p_{s's}(a).}$

[^1]: Puterman, Martin L. (1994). *Markov decision processes: discrete stochastic dynamic programming*. Wiley series in probability and mathematical statistics. Applied probability and statistics section. New York: Wiley. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-0-471-61977-2](https://en.wikipedia.org/wiki/Special:BookSources/978-0-471-61977-2 "Special:BookSources/978-0-471-61977-2").

[^2]: Yin, Bo (2021). *Airtime Management for Low-Latency Densely Deployed Wireless Networks* (PhD thesis). Japan: Kyoto University.

[^3]: Schneider, S.; Wagner, D. H. (1957-02-26). ["Error detection in redundant systems"](https://dl.acm.org/doi/10.1145/1455567.1455587). *Papers presented at the February 26-28, 1957, western joint computer conference: Techniques for reliability on - IRE-AIEE-ACM '57 (Western)*. New York, NY, USA: Association for Computing Machinery. pp. 115–121. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1145/1455567.1455587](https://doi.org/10.1145%2F1455567.1455587). [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-1-4503-7861-1](https://en.wikipedia.org/wiki/Special:BookSources/978-1-4503-7861-1 "Special:BookSources/978-1-4503-7861-1").

[^4]: Bellman, Richard (1958-09-01). ["Dynamic programming and stochastic control processes"](https://linkinghub.elsevier.com/retrieve/pii/S0019995858800030). *Information and Control*. **1** (3): 228–239. [Bibcode](https://en.wikipedia.org/wiki/Bibcode_\(identifier\) "Bibcode (identifier)"):[1958InfCo...1..228B](https://ui.adsabs.harvard.edu/abs/1958InfCo...1..228B). [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1016/S0019-9958(58)80003-0](https://doi.org/10.1016%2FS0019-9958%2858%2980003-0). [ISSN](https://en.wikipedia.org/wiki/ISSN_\(identifier\) "ISSN (identifier)") [0019-9958](https://search.worldcat.org/issn/0019-9958).

[^5]: Sutton, Richard S.; Barto, Andrew G. (2018). *Reinforcement learning: an introduction*. Adaptive computation and machine learning series (2nd ed.). Cambridge, Massachusetts: The MIT Press. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-0-262-03924-6](https://en.wikipedia.org/wiki/Special:BookSources/978-0-262-03924-6 "Special:BookSources/978-0-262-03924-6").

[^6]: Kearns, Michael; Mansour, Yishay; Ng, Andrew (2002). ["A Sparse Sampling Algorithm for Near-Optimal Planning in Large Markov Decision Processes"](https://doi.org/10.1023%2FA%3A1017932429737). *Machine Learning*. **49** (193–208): 193–208. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1023/A:1017932429737](https://doi.org/10.1023%2FA%3A1017932429737).

[^7]: Wrobel, A. (1984). "On Markovian decision models with a finite skeleton". *Zeitschrift für Operations Research*. **28** (1): 17–27. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1007/bf01919083](https://doi.org/10.1007%2Fbf01919083). [S2CID](https://en.wikipedia.org/wiki/S2CID_\(identifier\) "S2CID (identifier)") [2545336](https://api.semanticscholar.org/CorpusID:2545336).

[^8]: *Reinforcement Learning: Theory and Python Implementation*. Beijing: China Machine Press. 2019. p. 44. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [9787111631774](https://en.wikipedia.org/wiki/Special:BookSources/9787111631774 "Special:BookSources/9787111631774").

[^9]: [Shapley, Lloyd](https://en.wikipedia.org/wiki/Lloyd_Shapley "Lloyd Shapley") (1953). ["Stochastic Games"](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1063912). *Proceedings of the National Academy of Sciences of the United States of America*. **39** (10): 1095–1100. [Bibcode](https://en.wikipedia.org/wiki/Bibcode_\(identifier\) "Bibcode (identifier)"):[1953PNAS...39.1095S](https://ui.adsabs.harvard.edu/abs/1953PNAS...39.1095S). [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1073/pnas.39.10.1095](https://doi.org/10.1073%2Fpnas.39.10.1095). [PMC](https://en.wikipedia.org/wiki/PMC_\(identifier\) "PMC (identifier)") [1063912](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1063912). [PMID](https://en.wikipedia.org/wiki/PMID_\(identifier\) "PMID (identifier)") [16589380](https://pubmed.ncbi.nlm.nih.gov/16589380).

[^10]: Kallenberg, Lodewijk (2002). "Finite state and action MDPs". In [Feinberg, Eugene A.](https://en.wikipedia.org/wiki/Eugene_A._Feinberg "Eugene A. Feinberg"); Shwartz, Adam (eds.). *Handbook of Markov decision processes: methods and applications*. Springer. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-0-7923-7459-6](https://en.wikipedia.org/wiki/Special:BookSources/978-0-7923-7459-6 "Special:BookSources/978-0-7923-7459-6").

[^11]: Howard, Ronald A. (1960). *Dynamic Programming and Markov Processes*. The M.I.T. Press.

[^12]: Howard 2002, ["Comments on the Origin and Application of Markov Decision Processes"](https://pubsonline.informs.org/doi/10.1287/opre.50.1.100.17788)

[^13]: Puterman, M. L.; Shin, M. C. (1978). "Modified Policy Iteration Algorithms for Discounted Markov Decision Problems". *Management Science*. **24** (11): 1127–1137. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1287/mnsc.24.11.1127](https://doi.org/10.1287%2Fmnsc.24.11.1127).

[^14]: van Nunen, J.A. E. E (1976). "A set of successive approximation methods for discounted Markovian decision problems". *Zeitschrift für Operations Research*. **20** (5): 203–208. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1007/bf01920264](https://doi.org/10.1007%2Fbf01920264). [S2CID](https://en.wikipedia.org/wiki/S2CID_\(identifier\) "S2CID (identifier)") [5167748](https://api.semanticscholar.org/CorpusID:5167748).

[^15]: [Papadimitriou, Christos](https://en.wikipedia.org/wiki/Christos_Papadimitriou "Christos Papadimitriou"); [Tsitsiklis, John](https://en.wikipedia.org/wiki/John_Tsitsiklis "John Tsitsiklis") (1987). ["The Complexity of Markov Decision Processes"](https://pubsonline.informs.org/doi/abs/10.1287/moor.12.3.441). *[Mathematics of Operations Research](https://en.wikipedia.org/wiki/Mathematics_of_Operations_Research "Mathematics of Operations Research")*. **12** (3): 441–450. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1287/moor.12.3.441](https://doi.org/10.1287%2Fmoor.12.3.441). [hdl](https://en.wikipedia.org/wiki/Hdl_\(identifier\) "Hdl (identifier)"):[1721.1/2893](https://hdl.handle.net/1721.1%2F2893). Retrieved November 2, 2023.

[^16]: Kearns, Michael; Mansour, Yishay; Ng, Andrew (November 2002). ["A Sparse Sampling Algorithm for Near-Optimal Planning in Large Markov Decision Processes"](https://doi.org/10.1023%2FA%3A1017932429737). *Machine Learning*. **49** (2/3): 193–208. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1023/A:1017932429737](https://doi.org/10.1023%2FA%3A1017932429737).

[^17]: Altman, Eitan (1999). *Constrained Markov decision processes*. Vol. 7. CRC Press.

[^18]: Ding, Dongsheng; Zhang, Kaiqing; Jovanovic, Mihailo; Basar, Tamer (2020). *Natural policy gradient primal-dual method for constrained Markov decision processes*. Advances in Neural Information Processing Systems.

[^19]: Feyzabadi, S.; Carpin, S. (18–22 Aug 2014). ["Risk-aware path planning using hierarchical constrained Markov Decision Processes"](https://www.researchgate.net/publication/270105954). *Automation Science and Engineering (CASE)*. IEEE International Conference. pp. 297, 303.

[^20]: [*Continuous-Time Markov Decision Processes*](https://link.springer.com/book/10.1007/978-3-642-02547-1). Stochastic Modelling and Applied Probability. Vol. 62. 2009. [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1007/978-3-642-02547-1](https://doi.org/10.1007%2F978-3-642-02547-1). [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [978-3-642-02546-4](https://en.wikipedia.org/wiki/Special:BookSources/978-3-642-02546-4 "Special:BookSources/978-3-642-02546-4").

[^21]: Shoham, Y.; Powers, R.; Grenager, T. (2003). ["Multi-agent reinforcement learning: a critical survey"](http://jmvidal.cse.sc.edu/library/shoham03a.pdf) (PDF). *Technical Report, Stanford University*: 1–13. Retrieved 2018-12-12.

[^22]: [Narendra, K. S.](https://en.wikipedia.org/wiki/Kumpati_S._Narendra "Kumpati S. Narendra"); Thathachar, M. A. L. (1974). "Learning Automata – A Survey". *IEEE Transactions on Systems, Man, and Cybernetics*. SMC-4 (4): 323–334. [Bibcode](https://en.wikipedia.org/wiki/Bibcode_\(identifier\) "Bibcode (identifier)"):[1974ITSMC...4..323N](https://ui.adsabs.harvard.edu/abs/1974ITSMC...4..323N). [CiteSeerX](https://en.wikipedia.org/wiki/CiteSeerX_\(identifier\) "CiteSeerX (identifier)") [10.1.1.295.2280](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.295.2280). [doi](https://en.wikipedia.org/wiki/Doi_\(identifier\) "Doi (identifier)"):[10.1109/TSMC.1974.5408453](https://doi.org/10.1109%2FTSMC.1974.5408453). [ISSN](https://en.wikipedia.org/wiki/ISSN_\(identifier\) "ISSN (identifier)") [0018-9472](https://search.worldcat.org/issn/0018-9472).

[^23]: [Narendra, Kumpati S.](https://en.wikipedia.org/wiki/Kumpati_S._Narendra "Kumpati S. Narendra"); Thathachar, Mandayam A. L. (1989). [*Learning automata: An introduction*](https://archive.org/details/learningautomata00nare). Prentice Hall. [ISBN](https://en.wikipedia.org/wiki/ISBN_\(identifier\) "ISBN (identifier)") [9780134855585](https://en.wikipedia.org/wiki/Special:BookSources/9780134855585 "Special:BookSources/9780134855585").

[^24]: [Narendra & Thathachar 1974](#CITEREFNarendraThathachar1974), p.325 left.