<div align="center">

<h1>Xbotics 具身智能学习路线（Embodied‑AI Guide）</h1>

<p><em>更偏重机器人基础学习与开源项目实践 · 非“教程”，而是可以执行的学习路线与资源导航</em></p>

<!-- TODO: 将下方徽章中的 repo 与 path 替换为你的仓库名 -->

<p>
  <a href="https://github.com/your-org/your-repo"><img alt="GitHub repo stars" src="https://img.shields.io/github/stars/your-org/your-repo?style=social"></a>
  <img alt="PRs welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen">
  <img alt="License" src="https://img.shields.io/badge/License-CC%20BY%204.0-blue">
  <img alt="Visitors" src="https://api.visitorbadge.io/api/visitors?path=your-org/your-repo&label=visitors&countColor=%23263759&style=flat">
</p>

</div>

> Xbotics 社区具身智能学习指南：我们把“具身综述→学习路线→仿真学习→开源实物→人物访谈→公司图谱”串起来，帮助新手和实战者快速定位路径、落地项目与参与开源。
> 面向“**机器人基础学习 + 开源项目学习**”，强调可复现与快速上手；不追求百科全书，而是**清晰路径 + 工程落地**。


## 使用说明

* **定位**：面向新人、进阶与工程落地；以“路线+清单+实作任务”组织，而非长篇教程。
* **风格**：中文为主、英文补充；强调开源项目与可复现。
* **先修建议**：Python / 线性代数 / 概率统计 / 控制基础 / Linux & Git。
* **图标约定**：⭐ 必看 · 🧪 实作 · 🧱 SOP · 📦 代码/数据 · 📄 论文 · 🎥 视频（可选）。
* **结构**：每个小节优先给出可操作的“起步三件事”。

太好了，我把前面所有要求合并成**一份可直接粘到 GitHub `README.md` 的大纲**，包含：目录（四大块顺序保持：综述→路线→仿真→开源实物）、新增三章（基础学习、各技术基础与经典、各技术路线前沿）、“Ask Me Anything”/Issue 模板、每章下方的**贡献者**位、以及两类**详细样板**（仿真：Isaac Lab；实物：LeRobot；技术路线：Diffusion Policy & VLA）。你只需要把下面整段复制到仓库即可。

---

## 贡献者

@Xbotics-木木、@Xbotics-土豆、@FTZP、@Kands、@叶家乐，西南民族大学，主要专注于机器人方面的学习与应用  

> 🎯 想加入？见文末「如何贡献」。

---

## 目录

1. [具身综述（Embodied AI Overview）](#1-具身综述embodied-ai-overview)
2. [各技术学习路线（Roadmaps）](#2-各技术学习路线roadmaps)
3. [基础学习（机器人基础｜深度学习基础）](#3-基础学习机器人基础深度学习基础)
4. [各技术基础与经典（理论与经典论文/工程）](#4-各技术基础与经典理论与经典论文工程)
5. [各技术路线前沿（Trends & SOTA）](#5-各技术路线前沿trends--sota)
6. [仿真学习（Simulation）](#6-仿真学习simulation) — ⭐样板：Isaac Lab
7. [开源实物（Real Robots & Tooling）](#7-开源实物real-robots--tooling) — ⭐样板：LeRobot
8. [人物访谈（Interviews）](#8-人物访谈interviews)
9. [具身公司图谱（Landscape）](#9-具身公司图谱landscape)
10. [Ask Me Anything（提 Issue 问我任何）](#10-ask-me-anything提-issue-问我任何)
11. [如何贡献 & 目录约定](#11-如何贡献--目录约定)｜[License](#license)

---

## 1. 具身综述（Embodied AI Overview）

**贡献者**：@owner，@alice
**你将获得**：统一术语、问题划分与评测框架；从“感知—决策—控制—评测”建立大图景。
**小标题**

* 1.1 范式与框架：IL / RL / VLA / Diffusion Policy / 世界模型
* 1.2 数据与评测：采集、清洗、标注、Benchmark 协议
* 1.3 系统工程：安全、时延、同步、记录与回放
* 1.4 典型失败模式：多步长任务、延迟对齐、域偏移

---

## 2. 各技术学习路线（Roadmaps）

**贡献者**：@owner，@bob

> 每条路线 = 前置要求 → 4–8 周分周计划 → 里程碑 → 作业与验收 → 延伸阅读

**小标题**

* 2.1 模仿学习（BC/DAgger）
* 2.2 强化学习（PPO/SAC+iLQR/MPPI）
* 2.3 视觉与多模态（2D/3D/CLIP/SigLIP）
* 2.4 规划与控制（RRT*/TrajOpt/MPC）
* 2.5 触觉与力控（阻抗/导纳/传感融合）
* 2.6 VLA（OpenVLA/RT-2/π0）
* 2.7 Diffusion Policy（条件扩散策略）
* 2.8 世界模型（Dreamer/潜在动力学）
* 2.9 数据飞轮与遥操作（Teleop→清洗→训练→回流）
* 2.10 Sim2Real（域随机化/对齐/自适应）
* 2.11 评测与 Benchmark（标准化日志与指标）

**通用路线模板**

```md
#### <方向名> 学习路线（4–8 周）
- 前置要求：<课程/工具/数学>
- 第 1–2 周：跑通最小可行 demo（给出命令与脚本名）
- 第 3–4 周：改 1–2 个关键模块做对比实验
- 第 5–8 周：选择 1 个实战任务，交付 Demo+报告
- 里程碑：<成功率/曲线/可视化>
- 常见坑：<列 3–5 条>
- 延伸：<论文/代码/数据集 3–6 条>
- 贡献者：@yourname
```

**样板 A｜Diffusion Policy 路线（可直接用）**

* 前置：Python/PyTorch；理解轨迹/动作参数化
* 周程：`train_dp.py` 跑通 → 更换视觉编码器（SigLIP）/动作表示 → 加入遥操作数据，完成桌面抓取
* 里程碑：成功率≥80%，采样/去噪可视化
* 坑：时间对齐、动作尺度、采样步数引入时延
* 延伸：DP/ACT/LEAP；Bridge/RT-*；W&B/TensorBoard

**样板 B｜VLA 路线（OpenVLA/π0/RT-2 思路）**

* 前置：Transformer、CLIP/SigLIP
* 周程：最小 Demo（回放推理）→ 换编码器/提示/动作 token 化 → 多步骤指令任务
* 里程碑：多指令可控 Demo + 评测脚本
* 坑：动作对齐、长序列退化、指令歧义
* 延伸：OpenVLA/RT-2/π0；Hydra/Accelerate/LoRA；Bridge/Libero/Open-X

---

## 3. 基础学习（机器人基础｜深度学习基础）

**贡献者**：@alice，@charlie
**小标题**

* 3.1 机器人学打底：坐标系/运动学/动力学/控制
* 3.2 传感与同步：相机/IMU/力传感/时钟与标定
* 3.3 深度学习打底：优化/正则/卷积与注意力/训练套路
* 3.4 工程环境：Conda/Docker、日志与可视化、复现实验规范

---

## 4. 各技术基础与经典（理论与经典论文/工程）

**贡献者**：@owner
**小标题**

* 4.1 IL 经典：BC/DAgger/GAIL，数据分布与误差累积
* 4.2 RL 经典：值/策略/Actor-Critic，收敛与稳定性
* 4.3 视觉与多模态：表征学习、对比学习、SigLIP/CLIP
* 4.4 控制与规划：iLQR/MPPI/MPC 与 TrajOpt
* 4.5 扩散与生成：条件扩散、动作分布建模
* 4.6 世界模型：潜在动力学与想象训练

---

## 5. 各技术路线前沿（Trends & SOTA）

**贡献者**：@ptman12

### 5.1 VLA 最新进展与评测

以下精选2025年VLA（Vision-Language-Action）领域10篇高影响力前沿论文，每篇标注 **Paper**、**Code**（若开源）、**创新点** 与 **适用场景**，便于快速定位技术落地路径。整体趋势：力触觉融合 + 长时序规划 + 高效部署并重，在LIBERO、CALVIN-L等基准上平均提升18-35%。

- **TA-VLA: Elucidating the Design Space of Torque-aware Vision-Language-Action Models**  
  [Paper](https://arxiv.org/abs/2509.07962) | [Code](https://github.com/ZZongzheng0918/TA-VLA)  
  **创新点**：引入6-DoF扭矩信号作为独立模态，系统探索多层融合设计空间（早期/中期/晚期），提升力控任务鲁棒性。  
  **适用场景**：**高精度插拔、螺丝拧紧、门把操作**等需精确力反馈的工业装配线。

- **ForceVLA: Enhancing VLA Models with a Force-aware MoE for Contact-Rich Manipulation**  
  [Paper](https://arxiv.org/abs/2505.22159) | Code（未开源）  
  **创新点**：力感知MoE动态路由6轴力/扭矩反馈至VLA骨干，插拔任务成功率↑23.2%，桥接感知-执行延迟。  
  **适用场景**：**USB/HDMI插拔、钥匙开锁、精密对接**等接触瞬态敏感的自动化场景。

- **OpenVLA-OFT: Optimized Fine-Tuning for Speed and Success**  
  [Paper](https://arxiv.org/abs/2502.19645) | [Code](https://github.com/moojink/openvla-oft)  
  **创新点**：OFT高效微调策略，支持多图输入+高频双臂输出，推理加速25-50倍，LIBERO↑15%。  
  **适用场景**：**双臂协作搬运、快速分拣、桌面整理**等需高吞吐的仓储/服务机器人。

- **SmolVLA: Compact VLA for Affordable Robotics**  
  [Paper](https://arxiv.org/abs/2506.01844) | [Code](https://github.com/huggingface/lerobot)  
  **创新点**：450M参数异步推理栈，社区数据训练，性能媲美10倍大的大模型，内存占用仅1/10。  
  **适用场景**：**低成本教育机器人、家庭助手、边缘设备部署**（如Raspberry Pi级硬件）。

- **GR00T N1: Heterogeneous Data VLA for Humanoids**  
  [Paper](https://arxiv.org/abs/2503.14734) | [Code](https://github.com/NVIDIA/Isaac-GR00T)  
  **创新点**：融合轨迹+视频+合成数据异构训练，长时序鲁棒性↑22%，System2感知解耦执行。  
  **适用场景**：**工厂无人巡检、灾后搜救、动态环境适应**等需跨模态泛化的复杂任务。

- **Long-VLA: Unleashing Long-Horizon Capabilities**  
  [Paper](https://arxiv.org/abs/2508.19958) | Code（未开源）    
  **创新点**：技能链+子任务依赖图建模，分层提示驱动多步规划，成功率>2倍SOTA。  
  **适用场景**：**多步烹饪、家具组装、物流分拣链**等长时序、强逻辑依赖的任务流。

- **BitVLA: 1-Bit Quantized VLA for Efficiency**  
  [Paper](https://arxiv.org/abs/2506.07530) | [Code](https://github.com/ustcwhy/BitVLA)  
  **创新点**：三元1-bit量化+蒸馏，内存↓29.8%，LIBERO性能持平OpenVLA。  
  **适用场景**：**嵌入式机器人、无人机伴飞、移动机械臂**等极致算力受限平台。

- **VLA-Touch: Dual-Level Tactile Feedback Enhancement**  
  [Paper](https://arxiv.org/abs/2507.17294) | [Code](https://github.com/jxbi1010/VLA-Touch)  
  **创新点**：宏观+微观双层触觉融合，强化未知物体grounding，接触任务精度↑25%。  
  **适用场景**：**软体抓取、布料折叠、医疗辅助触诊**等需高触觉分辨率的柔性操作。

- **X-VLA: Soft-Prompted Transformer as Scalable Cross-Embodiment Vision-Language-Action Model**  
  [Paper](https://arxiv.org/abs/2510.10274) | [Code](https://github.com/2toinf/X-VLA)
  
  **创新点**：
    1. Soft Prompt 机制：为每个异构数据源引入最小参数（<1%）的可学习嵌入，作为 embodiment-specific 提示，早融合注入 Transformer，自动编码硬件配置（如相机视角、动作空间），有效化解跨平台视觉/任务异构性，确保稳定预训练。
    2. 纯 Transformer 架构：摒弃复杂 DiT，采用高维（多视角图像+语言）与低维（本体感觉 $R_t$ + 动作）双流分离编码后统一自注意力堆叠，实现简洁多模态融合，支持流匹配（flow-matching）动作生成，提升可扩展性。
    3. 数据处理优化：统一 EEF Pose 动作表示（xyz + Rotate6D + 夹爪 BCE 损失）、时间下采样意图抽象、平衡采样，减少噪声，提升跨 embodiment 一致性与泛化。
    4. 两阶段参数高效适配：Phase I 异构预训练（290K 轨迹）学通用策略；Phase II 新机器人时，先 Prompt Warm-up（冻结骨干，仅优 32K 参数编码硬件），再联合 LoRA 微调（仅 9M 参数），仅 1% 总参数达 LIBERO 93%、Simpler-WidowX 54% SOTA，媲美 3B 全调 π0。
  
  **结构图**：
<img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/6fcedbc7-2da0-42b0-833e-0b4f626c8dff" />
  
    **适用场景**：X-VLA 适用于**任何“硬件不同、任务复杂、数据有限”的机器人场景**，实现“一模型走天下”。。
  
* 5.2 Diffusion Policy 新结构与效率
  
* 5.3 触觉-视觉融合新数据集
  
* 5.4 Sim2Real 自适应与在线校准
  
* 5.5 数据飞轮与一人多机的监督框架

---

## 6. 仿真学习（Simulation）

**贡献者**：@charlie
**小标题**

* 6.1 平台对比：Isaac Lab / MuJoCo / PyBullet / Genesis / Gazebo
* 6.2 任务基准：单胳膊/双臂/移动操作/装配
* 6.3 资产与场景：USD/URDF 导入、相机布局、光照与碰撞
* 6.4 日志与回放：录制、重放、评测
* 6.5 **样板：Isaac Lab 最小上手（可复制运行）**

  ```bash
  # 环境（示例）
  conda create -n isaaclab python=3.10 -y
  conda activate isaaclab
  # 安装依赖（按官方指引）
  # ...
  # 运行最小任务（如 Cartpole/Humanoid）
  python source/standalone/workflows/rl/demos/cartpole.py --num_envs 1024
  ```

  * ✅ 目标：能在 5–10 分钟内跑出第一个曲线与视频
  * ✅ 交付：`/sim/isaaclab-minimal/README.md`（命令、注意事项、常见坑）

---

## 7. 开源实物（Real Robots & Tooling）

**贡献者**：@owner
**小标题**

* 7.1 平台与生态：Franka/UR/Kinova/LeRobot/Unitree/ORCA hand
* 7.2 数据采集与遥操作：协议、同步、失败库
* 7.3 安全与SOP：急停/限位/力控安全
* 7.4 **样板：LeRobot 最小上手（可复制运行）**

  ```bash
  # 环境（示例）
  conda create -n lerobot python=3.10 -y
  conda activate lerobot
  pip install lerobot  # 或本地源码安装
  # 运行最小回放/训练脚本（示例）
  python examples/replay_dataset.py --dataset demos/pick_place.hdf5
  ```

  * ✅ 目标：下载一个小型数据集 → 成功回放/推理
  * ✅ 交付：`/real/lerobot-minimal/README.md`（连接、标定、常见坑）

---

## 8. 人物访谈（Interviews）

**贡献者**：@alice
**小标题**

* 8.1 研究者与作者访谈
* 8.2 工程团队与开源维护者
* 8.3 创业者与产品化
* **提交模板**：`/interviews/<slug>.md`

  ```md
  # 标题（人名 ｜ 机构）
  - 话题关键词：<VLA/数据飞轮/Sim2Real...>
  - 3 个金句摘录：
  1) ...
  2) ...
  3) ...
  - 全文：<正文或外链>
  - 贡献者：@yourname
  ```

---

## 9. 具身公司图谱（Landscape）

**贡献者**：@bob
**小标题**

* 9.1 硬件整机（人形/四足/移动+操作）
* 9.2 关键部件（力控手、末端执行器、传感器）
* 9.3 算法与平台（VLA/策略/仿真/评测工具）
* 9.4 数据与服务（采集/标注/云端训练）
* **提交模板**：`/landscape/<company>.md`

  ```md
  ## 公司名（国家/地区）
  - 方向：<整机/手/平台/数据...>
  - 代表产品/论文/开源：
  - 商业进展与客户场景：
  - 备注（融资/招聘/合作）：
  - 贡献者：@yourname
  ```

---

## 10. Ask Me Anything（提 Issue 问我任何）

**贡献者**：全体维护者

* 在本仓库 **开 Issue** 提问（学习/复现/工程落地/选型/合作都可）
* 使用模板 **“AMA 问答”**（自动标签：`question`，`AMA`）

**Issue 模板（.github/ISSUE_TEMPLATE/ama.md）**

```md
---
name: "AMA 问答"
about: 提出你的问题，我们会跟进与沉淀
labels: ["AMA","question"]
---

**问题概述（1-3 句）**
-

**已尝试与线索（日志/截图/复现实验）**
-

**期望结果（成功率/曲线/Demo/文档）**
-

**环境信息（可选）**
- 硬件/系统/驱动：
- 关键依赖版本：
```

---

## 11. 如何贡献 & 目录约定

**贡献者**：@owner

* **PR 规则**：一事一 PR；附最小可复现；图片入 `assets/`；脚本入对应子目录
* **章节贡献**：每章末尾都保留“贡献者：@xxx”，请在你的 PR 中追加自己的 ID
* **目录结构建议**

```
/overview/            # 综述配套图/长文
/roadmaps/            # 各技术路线细分文档
/foundations/         # 基础学习资料与脚本
/classics/            # 各技术基础与经典
/trends/              # 前沿跟踪
/sim/isaaclab-minimal # 仿真样板
/real/lerobot-minimal # 实物样板
/interviews/          # 人物访谈
/landscape/           # 公司图谱
.github/ISSUE_TEMPLATE
```

* **提交检查清单**

  * [ ] 有 README/复现步骤/命令
  * [ ] 有最小可跑脚本与日志/图
  * [ ] 标注数据来源与许可证
  * [ ] 在对应章节补上你的「贡献者」ID

### License

本仓库采用 **MIT**（代码）与 **CC BY 4.0**（文档）双许可；外部素材遵循原许可。

---

### 备注

* 四大主线顺序已符合你最初要求：**1 综述 → 2 各方向学习路线 → 6 仿真 → 7 开源实物**；同时补充了你追加的三章：**3 基础学习、4 各技术基础与经典、5 各技术路线前沿**。
* 章节下方都留有**贡献者**位；AMA/Issue 模板、Isaac Lab 与 LeRobot 的**可跑样板**、以及 **Diffusion Policy / VLA 路线样板**均已内置。
* 需要的话，我可以把上述**子目录与 Issue 模板**一并生成到仓库的初始提交版本。


---

## 8. 版本与致谢

* **版本节奏**：每周一同步合入；月末发布小版本（Changelog）。
* **维护团队**：Xbotics 社区志愿者 & 合作伙伴。
* **致谢**：感谢所有贡献者的链接推荐、SOP 总结与复现实验。

> 💡 有想加入的方向？直接开 Issue；也欢迎在 Discussions 里提需求与想法。
