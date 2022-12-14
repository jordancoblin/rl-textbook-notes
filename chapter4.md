## Dynamic Programming

Collection of algos that can compute optimal policies given a perfect model of the env. Disadvantages: require perfect model and sometimes computationally expensive.
Useful as a foundation for more sophisticated methods.

Continuous states/action spaces -> quantize/bin into finite spaces.

**Key idea**: use value function to structure policy search -> DP can be used to compute value functions, by splitting into sub-problems (recursive definition). I.e. estimates value of states based on values of successor states -> we call this _bootstrapping_.

DP requires a perfect model of env/MDP, since it uses state transition function $p(s^\prime, r | s, a)$ to compute expected returns.


### 4.1 Policy Evaluation
Prediction problem -> computing the value function.

**Iterative Policy Evaluation**:
Can do this iteratively, by updating $v_{k+1}$ to be the result of the bellman equation over $v_k$:

$$ v_{k+1}(s) = \mathbb{E_\pi} [R_{t+1} + \gamma v_k(S_{t+1}) | S_t = s] $$

$v_k$ can be shown to converge to $v_\pi$ as $k \rightarrow \infty$.

One iteration -> update value of _every state_ once.

### 4.2 Policy Improvement

Question: is it better or worse to change to a new policy? One way to answer is to consider selecting action $a$ in state $s$ and following the existing policy $\pi$ thereafter. Value would be:

$$ 
\begin{align} 
q_{\pi}(s, a) &= \mathbb{E} [R_{t+1} + \gamma v_{\pi}(S_{t+1}) | S_t = s, A_t = a] \\
&= \sum_{s^{\prime},r} p(s^{\prime}, r | s, a) [r + \gamma v_{\pi}(s^\prime) ]
\end{align}
$$

If this new policy, of taking action a, then following $\pi$ has a higher value than just following $\pi$, then this new policy is better.

**Policy Improvement Theorem**:
Let $\pi$ and $\pi^{\prime}$ be any two deterministic policies, such that for all s $\in$ S:

$$ q_\pi(s, \pi^{\prime}(s)) \ge v_\pi(s) $$

then $\pi^{\prime}$ must be better than $\pi$:

$$ v_{\pi^\prime}(s) \ge v_\pi(s) $$

for all s $\in$ S.

Then, we can consider a new greedy policy $\pi^\prime$ that selects best action across all states according to $q_\pi(s,a)$:

$$ \pi^\prime(s) = \arg \max_a q_\pi(s,a) $$

Ideas in this section **extend to stochastic policies**

### 4.3 Policy Iteration

Combine evaluation and improvement: Evaluate $v_\pi$ -> improve to $\pi^\prime$ -> evaluate $v_{\pi^{\prime}}$ -> ...

### 4.4. Value Iteration

Policy iteration can be slow because each iteration requires us to do policy evaluation, which may itself require many iterations. Can truncate policy evaluation to speed things up, while still maintaining convergence guarantees.

**Value Iteration**: truncate policy evaluation after just one sweep (one update of all states).

Can now combine evaluation and improvement into a single update:

$$ v_{k+1}(s) = \max_a \mathbb{E} [ R_{t+1} + \gamma v_k(S_{t+1}) | S_t = s, A_t = a ] $$

Can often achieve faster convergence by taking multiple steps of policy evaluation between each step of policy improvement (instead of just one step, as in value iteration).

**Generalized Policy Iteration**: general idea of interleaving policy evaluation and improvement processes, independend of frequency/details of the processes.

### 4.7 Efficiency of DP

DP methods quite efficient at solving MDP's compared to other methods. Worst case: polynomial in number of states and actions. 
