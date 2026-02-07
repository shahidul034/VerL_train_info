

# 📊 Verl RL (GRPO) Training Monitor Guide

This document serves as a reference for monitoring training progress in **Verl** using the **GRPO** (Group Relative Policy Optimization) algorithm. Use this to decode your WandB charts and predict model stability.

## 1. Core Parameter Summary

| Parameter | Metric Name in Verl | Role in GRPO | Ideal Trend |
| --- | --- | --- | --- |
| **The Scorecard** | `critic/rewards/mean` | Tracks the average reward (accuracy/format) achieved by the group. | **Steady Increase ↗️** |
| **The Penalty** | `actor/kl_loss` | The penalty applied to keep the model from drifting too far from its original state. | **Slight Upward ↗️** |
| **The Speedometer** | `actor/ppo_kl` | Measures the step-by-step distance between the new policy and the old policy. | **Stable / Low ↔️** |

---

## 2. Scenario Diagnostics

Use this section to diagnose what is happening during your training run based on your visual charts.

### **Scenario A: The "Search" Phase (Flat Reward + Rising KL)**

* **Observation:** `critic/rewards/mean` is horizontal, but `actor/kl_loss` is trending up.
* **What it means:** The model is exploring new output patterns (moving away from the base model) but has not yet found a strategy that consistently earns more rewards.
* **Prediction:** If the reward doesn't "break out" soon, the model may be stuck in a local minimum or the learning rate is too low to escape the noise.

### **Scenario B: The "Reward Hack" (Spiking Reward + Spiking KL)**

* **Observation:** Sudden, sharp increases in both Reward and KL Loss.
* **What it means:** The model has found a way to "cheat" the reward function (e.g., repeating keywords) rather than learning the actual task.
* **Prediction:** Training will likely collapse soon as the output becomes gibberish that happens to satisfy the reward logic.

### **Scenario C: The "Dead Loop" (Zero KL)**

* **Observation:** `actor/ppo_kl` and `actor/kl_loss` stay near zero.
* **What it means:** The model is not learning or updating at all.
* **Prediction:** This usually indicates a broken gradient path, a learning rate set to zero, or a reward function that provides identical feedback for every sample.

---

## 3. Behavior Prediction Framework

How to anticipate model changes before they happen:

1. **Glimpses of Success:** Monitor `critic/rewards/max`. If the maximum reward in a group is frequently high while the `mean` is low, the model is "seeing" the right answer. A breakthrough in the mean is likely coming.
2. **Efficiency Check:** Compare the ratio of Reward gain to KL Loss. If you are gaining minimal reward at the cost of massive KL increases, the model is becoming inefficient and losing general knowledge.
3. **Instability Warning:** If `actor/ppo_kl` shows frequent vertical spikes (the "comb" pattern), the updates are too aggressive. Reduce your learning rate immediately to prevent a crash.

---

### 🛠 Suggested Next Steps

* **For Flat Rewards:** Increase your `num_generations` (group size) to provide better relative contrast for the GRPO advantage calculation.
* **For High Drift:** Increase the `kl_loss_coef` in your config to anchor the model more firmly.

