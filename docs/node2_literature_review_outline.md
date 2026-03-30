# Node 2 Literature Review Outline

## Scope

This reading list contains seven papers for the Node 2 literature review. The first six papers are directly aligned with vision-language navigation (VLN), embodied navigation, or robot-oriented language grounding. The seventh paper is retained as a supplementary related-work reference because it is about agentic LLM planning for vehicle routing rather than VLN itself.

## Recommended Structure

1. Define the VLN task and benchmark setting.
2. Review representative supervised or pre-trained VLN models.
3. Discuss the shift from benchmark VLN to continuous and robot-oriented navigation.
4. Cover recent LLM-based reasoning approaches for embodied navigation.
5. Position logistics-oriented agentic planning as adjacent, but not central, work.

## Core References

### 1. Task Definition and Benchmark

- Anderson, P., Wu, Q., Teney, D., Bruce, J., Johnson, M., Sunderhauf, N., Reid, I., Gould, S., and van den Hengel, A. (2018). *Vision-and-Language Navigation: Interpreting Visually-Grounded Navigation Instructions in Real Environments*. CVPR 2018.
  - Link: <https://openaccess.thecvf.com/content_cvpr_2018/html/Anderson_Vision-and-Language_Navigation_Interpreting_CVPR_2018_paper.html>
  - Why it matters: This is the foundational VLN paper. It defines the task clearly and introduces the Room-to-Room (R2R) benchmark.
  - How to use it in the review: Use this paper to open the literature review and explain what VLN is, why it is difficult, and how instruction grounding is evaluated.

### 2. Transformer-Based VLN Baseline

- Hong, Y., Wu, Q., Qi, Y., Rodriguez-Opazo, C., and Gould, S. (2021). *VLN BERT: A Recurrent Vision-and-Language BERT for Navigation*. CVPR 2021.
  - Link: <https://openaccess.thecvf.com/content/CVPR2021/html/Hong_VLN_BERT_A_Recurrent_Vision-and-Language_BERT_for_Navigation_CVPR_2021_paper.html>
  - Why it matters: This paper shows how BERT-style cross-modal modeling can be adapted to sequential navigation.
  - How to use it in the review: Use it as a representative strong baseline for instruction encoding, history handling, and multimodal decision making.

### 3. Long-Horizon History Modeling

- Chen, S., Guhur, P.-L., Schmid, C., and Laptev, I. (2021). *History Aware Multimodal Transformer for Vision-and-Language Navigation*. NeurIPS 2021.
  - Link: <https://proceedings.neurips.cc/paper/2021/hash/2e5c2cb8d13e8fba78d95211440ba326-Abstract.html>
  - Why it matters: HAMT emphasizes long-horizon memory and multimodal history, which is especially useful when instructions contain multiple landmarks or sequential sub-goals.
  - How to use it in the review: Compare its explicit history modeling with VLN-BERT, especially for longer or more complex trajectories.

### 4. From Discrete VLN to Continuous Navigation

- Hong, Y., Wang, Z., Wu, Q., and Gould, S. (2022). *Bridging the Gap Between Learning in Discrete and Continuous Environments for Vision-and-Language Navigation*. CVPR 2022.
  - Link: <https://openaccess.thecvf.com/content/CVPR2022/html/Hong_Bridging_the_Gap_Between_Learning_in_Discrete_and_Continuous_Environments_CVPR_2022_paper.html>
  - Why it matters: This paper is directly relevant to deployment-oriented simulation because it addresses the gap between graph-based VLN settings and continuous control environments.
  - How to use it in the review: Use it to motivate why a simulation pipeline based on Isaac Sim and Nav2 needs more than a benchmark-only VLN model.

### 5. Robot-Oriented Language Navigation with Foundation Models

- Shah, D., Osiński, B., Ichter, B., and Levine, S. (2022). *LM-Nav: Robotic Navigation with Large Pre-Trained Models of Language, Vision, and Action*. CoRL 2022.
  - Link: <https://openreview.net/forum?id=UW5A3SweAH>
  - Why it matters: LM-Nav is highly relevant for a practical robotics pipeline because it decomposes navigation into language understanding, landmark grounding, and goal-reaching modules.
  - How to use it in the review: Use it to justify a modular bridge design between language input, visual grounding, and the downstream Nav2 navigation stack.

### 6. LLM Reasoning for VLN

- Zhou, G., Hong, Y., and Wu, Q. (2024). *NavGPT: Explicit Reasoning in Vision-and-Language Navigation with Large Language Models*. AAAI 2024.
  - Link: <https://openreview.net/forum?id=KoOb7c4guE>
  - Why it matters: This paper shows how large language models can perform explicit reasoning over navigation history, observed landmarks, and candidate actions.
  - How to use it in the review: Use it to describe the recent shift from specialized VLN architectures toward LLM-based embodied reasoning.

## Supplementary Related Work

### 7. Agentic LLM Planning in Logistics

- Zhang, N., Cao, Z., Zhou, J., Zhang, C., and Ong, Y.-S. (2026). *An Agentic Framework with LLMs for Solving Complex Vehicle Routing Problems*. ICLR 2026.
  - Link: <https://arxiv.org/abs/2510.16701>
  - Why it is included: This paper is not a VLN paper, but it is still useful as adjacent evidence that agentic LLM frameworks can solve complex planning problems in logistics-style settings.
  - How to use it in the review: Do not present it as a VLN backbone paper. Instead, place it in a short related-work paragraph about LLM planning and task decomposition beyond embodied navigation.

## Suggested Writing Position

If the final literature review needs to justify a practical model choice for this project, the strongest narrative is:

- Anderson et al. (2018) defines the task and benchmark.
- VLN-BERT and HAMT represent mature VLN model design.
- Hong et al. (2022) explains why continuous navigation matters for simulation.
- LM-Nav offers a more robotics-friendly modular direction.
- NavGPT represents the newest LLM reasoning trend.
- Zhang et al. (2026) is supplementary evidence from logistics planning, not a direct VLN solution.

## Practical Recommendation

For this repository, the most defensible backbone direction is to treat the system as a modular language-to-goal pipeline inspired more by LM-Nav and the continuous-navigation literature than by a benchmark-only R2R agent. That choice will fit ROS 2, Nav2, and Isaac Sim more naturally than directly reproducing a discrete VLN benchmark model end to end.
