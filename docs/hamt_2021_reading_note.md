# HAMT (2021) Reading Note

## Citation

Chen, S., Guhur, P.-L., Schmid, C., and Laptev, I. (2021). *History Aware Multimodal Transformer for Vision-and-Language Navigation*. NeurIPS 2021.

## Polished Summary

This paper introduces HAMT, or History Aware Multimodal Transformer, to address one of the main weaknesses of earlier VLN systems: limited memory over long navigation trajectories. Previous agents often relied on recurrent models such as LSTMs to compress past observations into a fixed-size hidden state. That design is convenient, but it tends to forget early visual cues and action history when the route becomes long or complex.

HAMT replaces this compressed recurrent memory with an explicit history sequence. Instead of storing the past in a single vector, the model keeps a structured record of panoramic observations and actions over time. This allows the agent to revisit earlier context more directly, which is especially important when instructions involve multiple landmarks, long paths, or delayed decisions.

To make this long history tractable, the paper proposes a hierarchical visual transformer. At the view level, a ViT-style encoder processes local sub-views. At the panoramic level, a transformer models spatial relations among views within the same time step. At the temporal level, another transformer captures changes across time. This hierarchy reduces the computational burden compared with a flat transformer over every view from every step, while preserving both spatial and temporal structure.

The training strategy is also carefully designed. HAMT first uses several proxy pretraining tasks to align language, vision, actions, and spatial reasoning. These include masking-based objectives, trajectory-image matching, action prediction, and spatial relation learning. After pretraining, the model is fine-tuned with imitation learning and reinforcement learning, which improves navigation policy quality on downstream tasks.

Experimentally, HAMT achieves state-of-the-art performance on multiple embodied navigation benchmarks, including R2R, RxR, R4R, and REVERIE. The broader significance of the paper is that it shows better history modeling is not a minor implementation detail, but a central factor in improving VLN performance. For this project, the paper is valuable because it explains why long-horizon memory matters and why later navigation systems increasingly move away from overly compressed recurrent states.

## Why It Matters for This Project

- It explains why long-range history is essential in language-guided navigation.
- It shows a stronger alternative to fixed-size recurrent state compression.
- It connects benchmark VLN research to more realistic long-horizon decision making.
- It helps justify later system designs that preserve richer context rather than only the current observation.
