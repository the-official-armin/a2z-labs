# Updated Post-Lab Observations & Reflection

## Experiment 1: Exploration Probability vs. Goal Q-value

### Initial Hypothesis

I initially expected that lowering the exploration probability (ε) would consistently produce higher Q-values because the agent would spend more time exploiting its learned policy rather than exploring random actions.

### Observation

The measured Q-values varied considerably between repeated runs of the experiment. Re-running the same experiment produced noticeably different Q-values, even though the environment and hyperparameters were unchanged.

### Conclusion

This demonstrated that Q-learning is a stochastic algorithm. A single training run is not sufficient to draw conclusions because randomness in exploration and episode initialization can significantly affect the learned Q-values.

---

## Experiment 2: Repeated Training

### Objective

Determine whether the variation observed in the first experiment was due to randomness.

### Observation

Repeating training multiple times for each exploration probability showed that the learned Q-values exhibited measurable variance. This reinforced the importance of evaluating reinforcement learning algorithms over multiple independent training runs instead of relying on a single result.

### Conclusion

Statistical summaries such as the mean and variance provide a more reliable picture of an algorithm's behavior than individual runs.

---

## Experiment 3: Evaluating the Learned Policy

### Motivation

After further analysis, I realized that measuring the Q-value of the goal state was not an appropriate evaluation metric.

The Q-table estimates the expected future reward of taking an action **from** a particular state. Since the goal state immediately terminates the episode, the values stored for actions from the goal state do not directly indicate how well the agent learned to solve the task.

Instead, I evaluated the learned policy itself.

### Method

For each exploration probability:

* Train a new Q-learning agent.
* Disable exploration during evaluation (greedy policy).
* Start from the same initial state.
* Record whether the agent successfully reached the goal.
* Repeat training and evaluation multiple times.

### Results

Every exploration probability achieved a **100% success rate**.

### Interpretation

This result suggests that, for this simple 5×5 deterministic Grid World, the exploration probability had little impact on the final learned policy.

Although different exploration probabilities produced different Q-values during training, they ultimately learned policies that successfully reached the goal every time.

The earlier differences in Q-values therefore reflected differences in the internal value estimates rather than differences in task performance.

---

# Overall Conclusions

* Reinforcement learning is inherently stochastic, so repeated experiments are necessary for reliable evaluation.
* Internal quantities such as Q-values can vary substantially between runs without changing the agent's final behavior.
* Choosing an appropriate evaluation metric is critical. Measuring the learned policy (success rate) is more informative than measuring individual Q-values.
* For a small deterministic environment with only 25 states and sufficient training episodes, Q-learning consistently learned a successful policy regardless of the exploration probability.
* Hyperparameter sensitivity often depends on the difficulty of the environment. In this simple Grid World, the problem was easy enough that nearly every exploration probability produced an optimal policy after sufficient training.

## Personal Reflection

The most valuable lesson from this investigation was not discovering an "optimal" exploration probability, but learning how to evaluate reinforcement learning experiments properly.

Initially, I focused on individual Q-values and attempted to infer algorithm performance from them. Through repeated experimentation and analysis, I realized that the learned policy itself is the most meaningful quantity to evaluate. This experience reinforced the importance of designing experiments around metrics that directly measure the behavior of the agent rather than relying solely on internal model values.
