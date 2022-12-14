## Bandits

Mostly standard stuff here, a basic intro to the multi-armed bandit problem and basic approaches to solving.

As opposed to other RL problems, the bandits problem involves taking action from a _single_ state (i.e. they call this non-associative).

**Incremental average reward**: Can transform the standard expression for average reward into one that supports incremental updates (this is a theme for DP techniques in general).
I.e. $$Q_{n+1} = 1/n \sum_{i=1}^{n} R_i$$
becomes
$$Q_{n+1} = Q_n + 1/n[R_n - Q_n]$$

**Tracking a non-stationary problem**: for non-stationary problems, it makes sense to give more weight to recent rewards vs. rewards seen long in the past. One solution: use constant step-size. This yields a weighted average, or _exponential recency-weight average_. Convergence is not guaranteed in this case, but this is actually a desirable property for non-stationary problems.

**Optimistic initial values**: use initial estimate bias to encourage exploration, by setting initial values to large number. Works well in the stationary case, but not so well in the non-stationary case. "The beginning of time occurs only once, and we should focus on it too much."

**UCB**: alternative method for handling exploitation vs. exploration. Use optimality + uncertainty about each action as a way to select next action.

$$A_t \doteq [Q_t(a) + c \sqrt{ln{t}/N_t(a)}]$$
