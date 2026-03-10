

# Research Paper Experiment Checklist

## 1️⃣ Train Baseline Models (to justify why RL is needed)

Goal: Show **RL is better than standard training methods**.

### Models to train

* [ ] **Qwen3-4B-Instruct + SFT**

  * Same training dataset
  * Same prompts
  * Train supervised only

* [ ] **Qwen3-4B-Instruct + DPO**

  * Use same dataset
  * Preference optimization instead of RL

### Evaluation

* [ ] Evaluate SFT model
* [ ] Evaluate DPO model
* [ ] Compare with **your RL model**

Metrics to report:

* [ ] Readability accuracy
* [ ] Content preservation
* [ ] Hallucination
* [ ] Overall score

Goal for paper:
➡ show **SFT/DPO cannot solve readability control well**

---

# 2️⃣ Add Test-Time Scaling Baselines

Goal: Show **prompting alone cannot solve the task**

### Baseline 1 — Prompting (ReadCtrl)

* [ ] Implement **ReadCtrl prompting**
* [ ] Use Qwen3-4B-Instruct
* [ ] No training

---

### Baseline 2 — Best-of-N

Procedure:

* [ ] Generate **5 summaries**
* [ ] Ask model to **choose best one**

Example:

```
Generate 5 summaries for readability level X.
Select the best summary that best matches the readability requirement.
```

* [ ] Evaluate selected output

---

### Baseline 3 — Self-Refinement

Procedure:

* [ ] Iterative critique + revise
* [ ] 5 iterations

Example loop:

```
1. Generate summary
2. Critique readability
3. Revise
```

* [ ] Evaluate final output

Goal in paper:
➡ show **test-time scaling < RL training**

---

# 3️⃣ Reward Ablation Study

Goal: Prove **your reward design is correct**

You mentioned **3 rewards**.

### Reward ablation experiments

Train models with:

* [ ] **Reward A only**
* [ ] **Reward B only**
* [ ] **Reward C only**

Then evaluate each.

---

### Remove each reward

* [ ] A + B (remove C)
* [ ] A + C (remove B)
* [ ] B + C (remove A)

---

### Replace classification reward

Experiment:

* [ ] Replace classification reward with **FKGL metric**

Then compare:

* [ ] RL with FKGL reward
* [ ] RL with classification reward

Goal:

Show classification reward is better because:

* [ ] better readability accuracy
* [ ] more stable training
* [ ] fewer hallucinations

---

# 4️⃣ Multilingual Experiments

Goal: Show **method works beyond English**

### Languages

Required:

* [ ] English
* [ ] Bengali

Optional (if dataset allows):

* [ ] Other workshop languages

Examples:

* [ ] Spanish
* [ ] Chinese
* [ ] Hindi
* [ ] others in dataset

---

### Steps

For each language:

* [ ] Prepare dataset
* [ ] Train RL model
* [ ] Evaluate readability control

Goal for paper:

➡ multilingual generalization

---

# 5️⃣ Different Model Sizes

Goal: Show **method works across model scales**

### Train RL models for

* [ ] **Qwen3-0.6B**
* [ ] **Qwen3-1.7B**
* [ ] **Qwen3-4B** (main model)
* [ ] **Qwen3-8B** (optional if resources allow)

---

### Report

* [ ] performance improvement
* [ ] scaling trend

Goal:

➡ RL improves models **even at small scale**

---

# 6️⃣ Human Evaluation

Goal: Validate results from **human perspective**

### Prepare evaluation data

* [ ] Select **30 test examples**

For each example include:

* [ ] 5 models
* [ ] 3 outputs per model

Models to include (example):

* [ ] SFT
* [ ] DPO
* [ ] RL (yours)
* [ ] Best-of-N
* [ ] Self-refine

Important:

* [ ] **Shuffle outputs**

Annotators should **not know which model produced them**

---

### Annotation process

You have **3 annotators**

Each annotator:

* [ ] Annotates **10 examples**

Evaluation criteria:

Score each model (1–5):

* [ ] **Comprehensiveness**
* [ ] **Competence**
* [ ] **Hallucination**

Then:

* [ ] Provide **final ranking**
* [ ] Provide **reasoning**

---

### Expert verification

Wonseok will:

* [ ] Review annotations
* [ ] Remove unreasonable evaluations
* [ ] Select representative examples

---

### Qualitative examples for paper

* [ ] Select **best comparison examples**
* [ ] Highlight model strengths

---

# 7️⃣ Final Paper Preparation

When experiments are done:

### Results tables

* [ ] Baselines comparison
* [ ] Test-time scaling comparison
* [ ] Reward ablation
* [ ] Multilingual results
* [ ] Model size scaling
* [ ] Human evaluation

---

### Figures

* [ ] RL training curve
* [ ] reward ablation visualization
* [ ] model scaling plot

---

### Qualitative section

* [ ] Example outputs
* [ ] Human evaluation examples

---

# Final Deliverables Checklist

Before submission:

* [ ] All baselines completed
* [ ] Test-time scaling evaluated
* [ ] Reward ablation finished
* [ ] Multilingual results included
* [ ] Multiple model sizes tested
* [ ] Human evaluation completed
* [ ] Expert verification done
* [ ] Qualitative examples added
* [ ] Final tables + figures prepared

---

✅ If you want, I can also help you create a **recommended experiment timeline (2-week or 3-week plan)** so you can finish this efficiently. It will help a lot because this is **~20 experiments total**.
