<h1 align="center">CondenseVLA</h1>

<p align="center"><strong>Learnable History Condensation for Efficient Multi-Frame VLA</strong></p>

<p align="center"><strong>NeurIPS 2026</strong></p>

<p align="center">
  <a href="https://arxiv.org/abs/2610.25927"><img src="https://img.shields.io/badge/arXiv-2610.25927-red?style=flat&amp;logo=arxiv" alt="Paper on arXiv"></a>
</p>

> **Code coming soon in 3 months.** This repository currently provides the method overview and experimental results.

## Overview

Robot manipulation often requires knowing what happened a few moments ago. In **Pick and Place Twice**, the robot must remember whether it has already moved the object to the other plate; in **Swap Cubes**, it must keep track of which cube to move next.

**CondenseVLA** equips a vision-language-action policy with **Learnable History Condensation (LHC)**. LHC turns cached visual history into a fixed number of learned slots that condition a diffusion action decoder, allowing the policy to use recent observations without passing the entire history to the decoder.

![CondenseVLA overview and representative history-dependent tasks](assets/overview.png)

## Architecture

![CondenseVLA architecture](assets/architecture.png)

1. **Encode and cache.** Encode the current observation with the vision-language backbone and reuse cached features from earlier observations.
2. **Condense history.** Learned slot queries attend to the cached features and produce a compact set of history summaries.
3. **Predict actions.** A diffusion decoder uses the history slots together with the current observation feature to predict the next action chunk.

Fine-tuning freezes the vision encoders and language model while updating the multimodal projector, LHC, and action decoder. Attention-diversity and slot-decorrelation losses encourage complementary summaries. The number of history-conditioning slots stays fixed as the history window grows.

## Main Results

Mean task success rate (%); higher is better. Each row uses the corresponding benchmark setting from the paper.

| Benchmark | CronusVLA | CondenseVLA |
|:--|--:|--:|
| Simpler-WidowX | 58.7 | **69.8** |
| LIBERO | 96.3 | **97.2** |
| RMBench | 14.3 | **21.6** |
| Real-world manipulation | 45.2 | **52.8** |

Simpler-WidowX and local LIBERO results average three evaluation seeds of fixed trained checkpoints. RMBench uses 100 evaluation rollouts per task across nine tasks. Real-world evaluation uses 50 trials per task and method on a Galaxea R1 Lite robot.

### Real-world Tasks

Final task success rate (%) over 50 trials per task and method.

| Task | CronusVLA | CondenseVLA |
|:--|--:|--:|
| Put Apple on Plate | 66.0 | **70.0** |
| Open then Close Drawer | 48.0 | **54.0** |
| Pick and Place Twice | 40.0 | **50.0** |
| Swap Cubes | 50.0 | **62.0** |
| Put Objects in Drawer | 22.0 | **28.0** |
| **Average** | **45.2** | **52.8** |

Pick and Place Twice transfers the apple to the other plate and then returns it. Put Objects in Drawer requires placing both objects inside and closing the drawer.

## Code Release

**Coming soon in 3 months.**

The release will include the implementation and instructions for training and evaluation. Updates will be posted in this repository.

## Citation

If you find this work useful, please cite:

```bibtex
@article{hong2026condensevla,
  title   = {{CondenseVLA}: Learnable History Condensation for Efficient Multi-Frame {VLA}},
  author  = {Feiyang Hong and Yujie Wei and Bo Zhao and Xiu Su and Hongxun Yao and Shuo Yang},
  year    = {2026},
  journal = {arXiv preprint arXiv: 2610.25927}
}
```

## Contact

For questions, please contact [Feiyang Hong](mailto:feiyanghong7040@qq.com) or [Shuo Yang](mailto:shuoyang@hit.edu.cn).
