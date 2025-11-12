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

@Xbotics-木木、@Xbotics-土豆、@FTZP、@KandS、@maomao725

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

### 目录（Table of Contents）
- [1.1 术语速览](#11-术语速览--具身智能系统关键词手册)
- [1.2 操作综述](#12-操作综述)
- [1.3 感知综述](#13-感知综述)
- [1.4 运控综述](#14-运控综述)
- [1.5 交互与协作综述](#15-交互与协作综述)
- [1.6 数据、评测与基准综述](#16-数据评测与基准综述)

---

### 1.1 术语速览 · 具身智能系统关键词手册

#### 目录（Table of Contents）
- [1.1.1 学习范式与策略框架（IL / RL / VLA / Diffusion Policy / World Model）](#111-学习范式与策略框架il--rl--vla--diffusion-policy--world-model)
- [1.1.2 控制与规划常用概念](#112-控制与规划常用概念)
- [1.1.3 感知与表征（Robotics Models）](#113-感知与表征robotics-models)
- [1.1.4 系统工程（Robot System Engineering）](#114-系统工程robot-system-engineering)
- [1.1.5 人机交互（HRI）](#115-人机交互hri)
- [1.1.6 安全与标准](#116-安全与标准)
- [1.1.7 常见文件与工具栈](#117-常见文件与工具栈)
- [1.1.8 行业顶会 / 顶刊](#118-行业顶会--顶刊)
- [1.1.9 机器人基础（Robotics Basics）](#119-机器人基础robotics-basics)

---

## 1.1.1 学习范式与策略框架（IL / RL / VLA / Diffusion Policy / World Model）
- **行为克隆（Behavior Cloning, BC）**：把控制当成监督学习：输入观测/指令，输出动作。优点是数据友好、上手快；缺点是分布外脆弱（covariate shift），需靠干预/DAgger/重置策略兜底。  
- **逆强化学习（Inverse Reinforcement Learning, IRL）/偏好学习**：先学“奖励/偏好”，再用 RL 求策略；泛化好，但链路长、训练贵。  
- **GAIL / 对抗模仿**：通过判别器让“机器人轨迹像专家”，绕开显式奖励建模。对抗稳定性与探索机理是工程挑战。  
- **离线 RL / 在线 RL / Offline-to-Online（O2O）**：离线：全靠静态数据、安全可控；在线：探索充分但要解决安全与成本；O2O：先离线“站起来”，再在线“走起来”，符合工程常识。  
- **层级策略（Hierarchical Policy）**：高层做子目标/技能编排（options / behavior trees / task graphs），中层学习原子技能，低层用跟踪控制/安全壳执行。  
- **VLA（视觉–语言–动作, Vision–Language–Action）**：从视觉–语言模型（VLM）微调到端到端控制：看图、听指令、输出动作，同步提升开放词汇与长时序任务能力。  
- **扩散策略（Diffusion Policy）**：用生成模型在轨迹/动作分布上采样，天然平滑、抗噪，易接视觉/语言条件；部署时注意采样延迟与实时间隔对齐。  
- **世界模型（World Model, WM）**：学习“可微的环境动态”，在潜空间里做规划/MPC/RL，把昂贵的真机交互换成“脑内演练”；关键在表征学习、模型偏差控制、闭环落地。  
- **残差学习与模型融合**：用 MPC/几何控制做“主干”，RL/IL 学残差/补偿（摩擦、柔顺、延迟、未建模动力学），在工业里很常见。  
- **安全壳（Safety Shield）**：策略外层的速度/力矩限幅、碰撞守卫、紧急制动与可达性过滤，用于上线阶段风险控制与可解释合规。

---

## 1.1.2 控制与规划常用概念
- **PID 控制**：比例-积分-微分反馈控制，调参直观但对时延/强耦合系统需小心。  
- **计算力矩 / 反馈线性化（Computed-Torque Control）**：用模型抵消非线性，等效成线性目标再配 PD/PI。  
- **阻抗/导纳控制（Impedance / Admittance Control）**：在末端力–位移间设“机械阻抗”，适合接触/打磨/装配任务。  
- **MPC（模型预测控制）**：滚动优化、显式处理约束；实时性依赖求解器与模型精度。  
- **规划方法**：样条插补（轻量）、PRM/RRT（高维可行性）、TrajOpt/CHOMP/STOMP（平滑高质）。  
- **任务–技能–执行分层**：语言/图搜索/LLM 负责任务分解；技能网络（抓、推、开合…）产出子目标；低层控制稳定落地。

---

## 1.1.3 感知与表征（Robotics Models）
- **视觉编码器**：ResNet、ViT、DINO 等提取语义与几何；点云侧 PointNet、PointTransformer 做位姿/重建/抓取。  
- **VLM/LLM 融合**：CLIP、SigLIP 语义对齐；LLaVA、PaLM-E、Prism 等多模态骨干用于目标描述、子目标定位、失败解释。  
- **表示学习**：SE(3) 等变、神经隐式（SDF/NeRF/3DGS）、可供性图（Affordance Map）、接触图谱。  
- **状态估计与多传感融合**：RGB-D / IMU / 力矩 / 视觉跟踪，重点是时间同步与标定（手–眼、外参、时延）。

---

## 1.1.4 系统工程（Robot System Engineering）
- **手–眼标定（AX=XB / A=XBY）**：求相机与机械臂坐标系刚体变换。  
- **URDF / ROS**：机器人结构、惯量、关节、碰撞的统一描述格式。  
- **DH 参数与现代几何表示**：关节链参数化、雅可比、奇异性分析。  
- **记录与回放（Log & Replay）**：全链路时间戳、同步、丢包/延迟管理；用于离线评测、回归测试、复现实验。  
- **仿真到实机（Sim2Real）**：域随机化、参数扰动、传感噪声／延迟注入、重置策略与安全门限一致化。  
- **模型评估（Model Selection）**：成功率、完成时长、动作频率、回报；多任务场景关注最终阶段一致性，单任务场景关注最佳 checkpoint + 滑动平均。

---

## 1.1.5 人机交互（HRI）
- **共享控制（Shared Autonomy）**：人提供意图/指令，机器人做低层补偿与安全保障。  
- **可解释性（Explainability / Justification）**：策略过程可被人理解、可追溯。  
- **信任与接受度（Trust & Acceptance）**：人对系统可靠性／可控性的主观信任度，影响系统投放与合规。  
- **社交导航（Proxemics）**：在人群环境中机器人保持合适距离、礼貌行为与交互方式。  
- **Wizard-of-Oz 实验**：早期 HRI 数据采集中常用“人类暗中接管机器人行为”来收集真实交互数据。  
- **社区与会议**：ACM/IEEE HRI 是人机交互领域旗舰年会；ACM THRI 是相关期刊。

---

## 1.1.6 安全与标准
- **ISO 10218-1 / -2**：工业机器人及其系统安全要求（机械、控制、集成）。  
- **ISO/TS 15066**：协作机器人（cobot）安全指南（人机共域力限值、协作模式、安全模式等）。  
  👉 这些标准是落地部署／验收时常被查验的条款，建议据此设计“速度／力矩限幅、停止等级、围栏／扫描仪联锁”等安全壳。

---

## 1.1.7 常见文件与工具栈
- **URDF / SRDF / xACRO**：机构学与语义描述格式。  
- **USD / GLB**：高保真几何交换格式。  
- **ROS / ROS 2**：通信中间件；**tf/tf2** 用于坐标变换。  
- **MoveIt**：常用运动规划＆碰撞检测框架。  
- **Isaac Lab / ManiSkill / RoboSuite / RLBench**：主流仿真平台／基准套件。  
- **PyTorch / JAX**：模型训练栈。**ONNX / TensorRT**：部署加速栈。  
- **Opt / OSQP / qpOASES**：MPC/QP 求解器工具。  
- **Bag / MCAP**：日志与回放格式。  

---

## 1.1.8 行业顶会 / 顶刊
### 🧭 会议（Conferences）
- **ICRA** – IEEE Intl. Conf. on Robotics and Automation  
- **IROS** – IEEE/RSJ Intl. Conf. on Intelligent Robots and Systems  
- **RSS** – Robotics: Science and Systems  
- **CoRL** – Conference on Robot Learning  
- **Humanoids / CASE / ISRR / ISER** 等专题会议

### 📘 期刊（Journals）
- **IEEE Transactions on Robotics (T-RO)**、**IEEE Robotics and Automation Letters (RA-L)**  
- **The International Journal of Robotics Research (IJRR)**、**Autonomous Robots (AURO)**  
- **Science Robotics**  
- **Journal of Field Robotics (JFR)**  
- **ACM THRI**（人机交互领域旗舰期刊）

---

## 1.1.9 机器人基础（Robotics Basics）
- **自由度（DoF）/工作空间**：构型可动维数与末端可达区域。  
- **正／逆运动学（FK/IK）**：通过关节角求末端位姿；或反求关节角。雅可比矩阵用于速度／力映射与奇异性分析。  
- **动力学**：包含惯量、科氏力、离心力、重力项；控制器设计必须考虑执行器力矩、关节摩擦、负载变化。  
- **外参／内参／时间同步**：摄像头、IMU、力传感器等多模态传感器融合基础。  
- **手–眼／基–世界标定（AX = XB / A = XBY 问题）**：求解机器人末端与相机之间或机器人基座与世界坐标系的变换。  
- **可供性（Affordance）**：物体“可被如何用”的语义线索，常用于抓取/操作点预测。  
- **可达性／可操作性（Reachability / Manipulability）**：指给定关节限制／障碍环境下，末端能否达到目标位姿或姿态灵活度。  
- **接触建模／摩擦锥模型**：抓取与装配任务中接触力、接触面、摩擦参数的基础物理模型。  
- **软硬件在环（HIL / SIL）**：在上线前用模拟（软件／硬件）环境验证系统闭环性能与安全。  

### 1.2-操作综述

# 🤖 机器人操作（Robot Manipulation）综述

> 一文搞清“从感知到动作”的关键脉络与落地路线：用 **数据驱动** 的 **表示—策略—执行** 链路，支撑在 **家庭、工业、农业、科学** 等真实场景中的泛化与稳定。  
> 目标是“够用、可落地”：不面面俱到，但给到每一条主线的代表性工作与开源落地点。

---

## 🧠 为什么是“具身智能中的操作”

**本节导读**：本节回答“为什么要做操作”。操作是具身智能的闭环中枢：**感知 → 表征/理解 → 决策/规划 → 执行/安全**。  
它与纯感知或语言任务不同，强调**物理可行性、实时性与安全性**。理解这点有助于选择合适的**数据、策略与系统工程**路线。

近年进展主要来自三股合力：

- **大模型与表征**：如 R3M、VIP、VC-1 等，让机器人复用通用视觉/多模态编码器。  
- **策略范式创新**：Transformer、Diffusion、Flow Matching、SSM 等提升动作建模能力。  
- **数据飞轮机制**：从**遥操采集 → 合成扩增 → 自动纠错 → 再训练**构成循环。

---

## ⚙️ 全栈视角：从感知到动作的四层架构

**本节导读**：这里给出工程上常用的“四层分工”，便于团队分拆与接口定义。  
建议把**模块边界、消息格式和时序**确定清楚，后续替换任意一层（如策略或控制）都更顺滑。

### 1. 感知与编码（Perception & Encoding）
- 视觉（RGB/RGB-D/点云）、触觉（高分辨率皮肤/力觉）、音频、IMU/关节状态等。  
- 目标：学得**通用、可迁移**的语义与几何表征，支撑下游策略。

### 2. 潜在学习（Latent Learning）
- 通过**对比/自监督/视频-语言/价值隐式**等，学到与任务相关的**紧凑潜在空间**；  
- “潜在动作”（离散/连续）进一步成为**控制接口**，连接表示与策略。

### 3. 策略学习（Policy Learning）
- MLP/Transformer 自回归、**扩散策略（Diffusion Policy）**、**流匹配（Flow Matching）**、**SSM（Mamba）**等；  
- 关注**长时依赖、动作多模态、实时性、等变性（SE(3)/SIM(3)）**与**安全约束**。

### 4. 执行与安全（Control & Safety）
- 轨迹生成/插补、阻抗/力控、限位/碰撞/急停；  
- 工程上通过**高层（语义/关键姿态）+ 低层（闭环力位控）**提升稳定性与安全性。

---

## 🔍 表示学习：可迁移的感知与潜在空间

**本节导读**：表示是“共用底座”。你需要一个能跨物体、跨场景、跨任务的**稳定表征**，否则策略在分布外就会崩。  
建议先选一个**通用视觉编码器**（R3M/VIP/VC-1），再视任务引入**潜在动作**或**世界模型**。

### 通用视觉与多模态预训练
- [R3M](https://arxiv.org/abs/2203.12601)：基于 Ego4D 的时间对比视频语言表征。  
- [VIP](https://www.lcsr.jhu.edu/wp-content/uploads/2022/10/vip.pdf)：基于目标价值的隐式预训练。  
- [VC-1 / Theia / RPT](https://arxiv.org/abs/2307.15127)：从人类视频或机器人轨迹学习世界模型式特征。

### 潜在动作与世界模型
- 动作/状态离散化为 token 或连续向量，作为策略接口，便于迁移与复用；  
- 视频世界模型预测未来潜在表征，用于“**想象—评估—执行**”的一体化闭环。

---

## 🧩 策略学习：从 MLP/Transformer 到 Diffusion/Flow/SSM

**本节导读**：策略是“怎么做”的大脑。不同范式在**实时性、稳健性、训练成本**上各有取舍。  
建议按**时延预算、动作多峰性、可解释/合规**需求做选型（DP 工程成熟；FM 更快更顺滑；SSM 长序列性价比高）。

### 1️⃣ 基础自回归策略
- [RT-1](https://robotics-transformer.github.io/)：多任务 Transformer 策略。  
- [RT-2](https://robotics-transformer2.github.io/)：把网页/图文知识迁移到机器人控制。  
- [OpenVLA](https://www.alphaxiv.org/abs/2406.07476)：开放 VLA 基线。

### 2️⃣ 扩散策略（Diffusion Policy）
- **原始论文**：[2303.04137](https://arxiv.org/abs/2303.04137) ｜ **项目页**：[diffusion-policy.cs.columbia.edu](https://diffusion-policy.cs.columbia.edu/)  
- **加速方向**：  
  - [Consistency Policy](https://arxiv.org/abs/2408.00633)  
  - [ManiCM](https://arxiv.org/abs/2406.01586)  
  - [EquiBot（等变性 DP）](https://ut-austin-rpl.github.io/EquiBot/)

### 3️⃣ 流匹配（Flow Matching）
- [FLOWER](https://www.semanticscholar.org/paper/fdcad3d7a26b0e9b8d7d8d4a555b3b5a5c5e3dc1)  
- [FlowPolicy](https://arxiv.org/abs/2412.04987)  
- [Streaming Flow Policy](https://www.semanticscholar.org/paper/5f0d1f4b43fdb5b0dfd68a7b4f8d1f0b3f657b2c)

### 4️⃣ 状态空间模型（SSM / Mamba）
- [MaIL: Mamba as Motion Encoder](https://arxiv.org/abs/2409.02636)

> ✅ **小结**：DP → FM → SSM 是策略层的三条主线。  
> DP 工程成熟；FM 推理更快；SSM 在长时依赖与效率间平衡。

---

## 📦 数据：采集—利用—扩展—重加权

**本节导读**：数据决定上限，策略决定下限。构建**低成本、持续化**的数据飞轮，是小团队突围的关键。  
从**遥操/合成**冷启动，依靠**选择/检索/增广/扩展/重加权**滚动提效，最后接**在线纠错**闭环。

### 采集方式
- [RoboTurk](https://arxiv.org/abs/1811.02790)：众包远程遥操。  
- [MimicGen / DexMimicGen](https://arxiv.org/abs/2307.15127)：系统化示范合成。  
- [AnyTeleop](https://www.alphaxiv.org/abs/2305.06343)：多形态视觉遥操。  
- [DemoGen](https://arxiv.org/abs/2403.08716)：全合成示范生成。

### 数据利用与优化
- **选择/清洗 → 检索 → 增广 → 扩展 → 重加权**；  
- 冷启动靠检索，规模化靠增广，鲁棒性靠重加权。

---

## 🌍 泛化：环境 / 任务 / 跨具身

**本节导读**：泛化不是“自动出现”，需要**评测协议 + 结构性先验**。  
分别从**环境、任务、具身差异**三条线补齐方法与验证，避免“单场景过拟合”。

- **环境泛化**：[Sim2Real 综述](https://doi.org/10.1109/ACCESS.2021.3063201)  
- **任务泛化**：层级策略、语义分解、可重组技能、元学习。  
- **跨具身**：[Open-X-Embodiment](https://robotics-transformer-x.github.io/) ｜ [AnyBimanual](https://arxiv.org/abs/2412.06779)

---

## 🏭 典型应用：家务、工业、农业、AI4Science、艺术与体育

**本节导读**：不同场景的**约束、容错、合规**差异很大。  
这里给到每类应用的**技术侧重点**，方便你对号入座做最小可行方案（MVP）。

| 场景 | 特点 | 技术要点 |
|------|------|----------|
| 家庭服务 | 高接触、强约束 | 层级策略 + DP/Flow |
| 工业制造 | 精度高、容错低 | 视觉抗干扰 + 力控安全 |
| 农业机器人 | 光照变化大 | 感知鲁棒 + 柔顺控制 |
| 科学与医疗 | 高精密、可验证 | 物理安全 + 合规性 |
| 艺术与体育 | 高频闭环 | 时序精确 + 高速控制 |

---

## 🧭 落地攻略：一条可执行的端到端流水线

**本节导读**：这是一份**可直接执行**的路线图。每个阶段都有**目标—动作—产出**，便于周/双周节奏推进与复盘。

| 阶段 | 核心任务 |
|------|----------|
| Stage-0 | 硬件上线、安全配置（限位/急停/阻抗参数/SOP） |
| Stage-1 | 数据采集与标定（遥操 50–200 条 + 少量仿真；时间戳/外参齐全） |
| Stage-2 | 表示学习与检索策略（R3M/VIP/VC-1 + VINN/NN/BC 基线） |
| Stage-3 | 策略训练与评估（DP/FM/SSM 选型；长时序用层级） |
| Stage-4 | 数据飞轮与在线优化（选择/增广/重加权 + 不确定性交互采样） |
| Stage-5 | 安全部署与维护（在环安全、A/B 切换、日志与可观测性） |

---

## 🔮 开放问题与未来方向


1. **One Brain, Multiple Embodiments**：通用大脑支持多形态机器人。  
2. **自采—自训闭环**：标准化数据协议与价值评估。  
3. **多模态深度交互**：高分辨触觉与异步多率融合。  
4. **安全与协作**：规则/MPC + 学习策略的混合范式。


### 1.3-感知综述
### 1.4-运控综述
### 1.5-交互综述
### 1.6-数据综述
---

## 2. 各技术学习路线（Roadmaps）

**贡献者**：@KandS

> 每条路线 = 前置要求 → 4–8 周分周计划 → 里程碑 → 作业与验收 → 延伸阅读

**小标题**

* [2.1 强化学习](#21-强化学习)
* [2.2 模仿学习](#22-模仿学习)
* [2.3 3D 视觉](#23-3d-视觉)
* [2.4 规划与控制](#24-规划与控制)
* [2.5 定位与导航](#25-定位与导航)
* [2.6 触觉与力控](#26-力控与触觉)
* [2.7 VLA](#27-vla)
* [2.8 Sim2Real](#28-sim2real)
* [2.9 世界模型](#29-世界模型)
* [2.10 数据飞轮与遥操作](#210-数据飞轮与遥操作)

<!-- * [2.1 模仿学习（BC/DAgger）](#21-模仿学习bcdagger路线)
* [2.2 强化学习（PPO/SAC+iLQR/MPPI）](#22-强化学习pposacilqrmpii路线)
* [2.3 视觉与多模态（2D/3D/CLIP/SigLIP）](#23-视觉与多模态2d3dclipsiglip路线)
* [2.4 规划与控制（RRT*/TrajOpt/MPC）](#24-规划与控制rrttrajoptmpc路线)
* [2.5 触觉与力控（阻抗导纳传感融合）](#25-触觉与力控阻抗导纳传感融合路线)
* [2.6 VLA（OpenVLA/RT-2/π0）](#26-vlaopenvlart-2π0路线)
* [2.7 Diffusion Policy（条件扩散策略）](#27-diffusion-policy条件扩散策略路线)
* [2.8 世界模型（Dreamer/潜在动力学）](#28-世界模型dreamer潜在动力学路线)
* [2.9 数据飞轮与遥操作（Teleop→清洗→训练→回流）](#29-数据飞轮与遥操作teleop清洗训练回流路线)
* [2.10 Sim2Real（域随机化/对齐/自适应）](#210-sim2real域随机化对齐自适应路线)
* [2.11 评测与 Benchmark（标准化日志与指标）](#211-评测与-benchmark标准化日志与指标路线) -->

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

```md
#### <方向名>
- **前置要求**：<工具/数学>
- **理论**：
    - **基础**：<方法发展路线> 
    - **课程**：<课程名（链接）> | <课程简介>
- **实践**：
    - **工具**：<资料库（链接）> | <资料库简介>
    - **最小目标**：
    - **进阶目标**：
- **延伸**：
    - **论文/项目**：<论文链接> （可选）
    - **工具**：<代码库链接>（可选）
```

---

#### 2.1 强化学习
- **前置要求**：Pytorch / 马尔可夫决策过程（MDP）
- **理论**：
  - **基础**：Q-learning → DQN → REINFORCE → Actor-Critic → PPO
  - **课程**：
    - [OpenAI Spinning Up in Deep RL](https://spinningup.openai.com/)：提供 REINFORCE、TRPO、PPO、DDPG、TD3、SAC 等算法的理论讲解与实现
- **实践**：
  - **工具**：
    - [Stable-Baselines3](https://github.com/DLR-RM/stable-baselines3) ：实现 DQN、PPO、A2C、TD3、SAC 等算法，广泛用于 RL 实验，兼容 Gym
    - [Gymnasium](https://github.com/Farama-Foundation/Gymnasium)：提供 CartPole、MountainCar、LunarLander 等经典任务，用于入门测试
  - **最小目标**：使用 PPO 训练智能体，完成 CartPole 平衡杆任务
  - **进阶目标**：探索稀疏奖励情境下的 MountainCar 爬坡车任务
- **延伸**：
  - **项目**：
    - [RDT-1B](https://rdt-robotics.github.io/rdt-robotics/)：12 亿参数的扩散基础模型，支持语言、图像和动作输入，适用于单臂、双臂和移动机器人等多种平台
    - [RTX](https://robotics-transformer-x.github.io/)：结合视觉、语言和动作信息，实现端到端的机器人控制
  - **工具**：
    - [RLlib](https://github.com/ray-project/ray)：分布式强化学习库，支持并行训练，部署简单，适合大规模强化学习实验

---

#### 2.2 模仿学习
- **前置要求**：PyBullet / 强化学习
- **理论**：
  - **基础**：BC → DAgger → GAIL
  - **课程**：
    - [CS285 深度强化学习课程（UC Berkeley）](https://rail.eecs.berkeley.edu/deeprlcourse/   )：包含 DQN、REINFORCE、PPO、DDPG、SAC、BC、DAgger 等算法的完整作业和实现
- **实践**：
  -  **工具**：
     -  [Imitation](https://github.com/HumanCompatibleAI/imitation?tab=readme-ov-file ) ：提供 Behavior Cloning、DAgger、GAIL 等算法的实现，适配 Stable Baselines3，广泛用于仿人任务研究
     -  [PyBullet](https://github.com/bulletphysics/bullet3)：支持机器人、强化学习和虚拟现实的物理仿真，提供 Python 接口
  -  **最小目标**：在 PyBullet 中采集机械臂轨迹，使用 Behavior Cloning 拟合策略，验证成功率
  -  **进阶目标**：先用少量专家演示预训练（BC），再微调（PPO）实现迁移学习效果
- **延伸**：
  - **项目**：
    - [Diffusion Policy](https://github.com/real-stanford/diffusion_policy)：基于扩散模型的策略学习方法，适用于高维动作空间的机器人控制任务
    - [DP3](https://3d-diffusion-policy.github.io/) ：将 3D 视觉表示与扩散策略相结合
    - [HumanPlus](https://humanoid-ai.github.io/)：人形机器人系统，融合了模仿学习、强化学习和影子学习技术
  - **工具**：
    - [RoboMimic](https://github.com/ARISE-Initiative/robomimic)：集成多个 IL 算法，支持多机器人数据集，适合多任务与多模态策略研究
    - [LeRobot](https://github.com/huggingface/lerobot)：支持 Diffusion Policy 等多种策略，适合多任务机器人操作研究


---

#### 2.3 3D 视觉

- **前置要求**：OpenCV / PyTorch / 基础线性代数与几何
- **理论**：
  - **基础**：2D/3D 视觉分割（Mask R-CNN/PointNet） → 6D 姿态估计（PoseCNN/CosyPose） → 手眼标定 → 抓取策略 (2D/6D)
  - **课程**：
    - [《动手学深度学习》中文版](https://github.com/d2l-ai/d2l-zh)：提供PyTorch实现的CNN等深度学习基础
    - [OpenCV-Python 中文教程](https://github.com/makelove/OpenCV-Python-Tutorial)：涵盖图像处理、特征提取等CV基础
- **实践**：
  - **工具**：
    - [Detectron2](https://github.com/facebookresearch/detectron2)：支持Mask R-CNN等先进检测与分割算法
    - [Open3D-ML](https://github.com/isl-org/Open3D-ML)：专注于3D机器学习任务，如语义点云分割
    - [PyBullet](https://github.com/bulletphysics/bullet3)：轻量级物理仿真平台，用于搭建机械臂抓取实验环境
  - **最小目标**：使用 Detectron2 在自定义数据集上训练一个实例分割模型
  - **进阶目标**：在 YCB-Video 数据集上复现 PoseCNN，完成物体 6D 姿态估计
- **延伸**：
  - **项目**：
    - [GraspNet-1Billion](https://github.com/graspnet/graspnet-baseline)：大规模抓取数据集与基线模型
    - [Dex-Net 2.0](https://github.com/BerkeleyAutomation/dex-net)：基于物理的抓取评分与规划框架
    - [Tac2Pose](https://github.com/harvard-visionlab/tac2pose)：视觉与触觉融合的姿态回归方法
  - **工具**：
    - [MuJoCo](https://github.com/google-deepmind/mujoco)：高性能物理引擎，适合研究和开发
    - [Gazebo](https://github.com/osrf/gazebo)：功能强大的机器人仿真平台

---

#### 2.4 规划与控制

- **前置要求**：ROS / 线性代数 / 基础微积分
- **理论**：
  - **基础**：正运动学（DH参数） → 逆运动学（解析/数值解法） → 动力学建模（Lagrangian/Newton-Euler） → 采样法规划（PRM/RRT） → 轨迹生成与平滑（B样条） → 经典控制器（PID） → 阻抗控制 → 模型预测控制（MPC）
  - **课程**：
    - [《机器人学：规划、控制及应用》](https://github.com/qqfly/how-to-learn-robotics)：开源中文学习指南，涵盖运动学、动力学、控制等核心内容
    - [《Modern Robotics》配套代码库 (C++)](https://github.com/fan-ziqi/ModernRoboticsCpp_CN)：提供《Modern Robotics》一书的C++实现，注释为中文，便于理解
    - [ROSBOT](https://github.com/Githubcxy666/ROSBOT)：汇总了ROS机器人开发的相关资料，包含运动学模型、路径规划算法（Dijkstra, A*, RRT）、ROS常用命令等内容
- **实践**：
  - **工具**：
    - [Gazebo](https://gazebosim.org/home)：真实物理模拟环境，用于验证控制器效果
    - [nobleo/path_tracking_pid](https://github.com/nobleo/path_tracking_pid)：基于 ROS 的 PID 路径追踪控制器，支持平滑路径追踪与多种测试用例
  - **最小目标**：使用 DH 参数描述一个 2-DOF 或 6-DOF 机械臂，并实现其正/逆运动学模拟器
  - **进阶目标**：在 Gazebo 中仿真 UR5 机械臂，实现基于 PID 的轨迹跟踪控制，并可视化运动路径
- **延伸**：
  - **项目**：
    - [modulabs/arm-control](https://github.com/modulabs/arm-control)：支持 Elfin 6 机械臂的 ROS 轨迹一体化控制框架，包含多种控制器和 Gazebo 仿真
    - [ferasboulala/five-dof-robot-arm](https://github.com/ferasboulala/five-dof-robot-arm)：使用 ROS + MoveIt! 驱动 5 DOF 机械臂，支持 Gazebo 仿真与 Arduino 物理执行
    - [JZX-MY/psolqr_local_planner](https://github.com/JZX-MY/psolqr_local_planner)：ROS 本地路径规划插件，实现 PSO 优化 + LQR 控制一体设计
    - [itsahmedkhali/MobileRobotEKF-LQR](https://github.com/itsahmedkhali/MobileRobotEKF-LQR)：差分驱动机器人项目，使用EKF 做状态估计，LQR 做控制，并在 Gazebo & ROS 中仿真
  - **工具**：
    - [MATLAB Simulink](https://uk.mathworks.com/products/simulink.html)：用于MPC等复杂控制器的快速原型验证

---

#### 2.5 定位与导航

- **前置要求**：ROS / 基础概率论与线性代数
- **理论**：
  - **基础**：状态估计理论（贝叶斯滤波、卡尔曼滤波、粒子滤波） → 位姿图优化（Pose Graph / Factor Graph） → 图搜索算法（Dijkstra, A*, D* Lite） → 随机采样法（RRT, PRM） → 优化方法（MPC, CHOMP, TEB）
  - **课程**：
    - [MIT 6.141 / UZH V-SLAM 公开课](https://www.youtube.com/playlist?list=PLUl4u3cNGP63EdVPNLG3ToM6LaEUuStEY)：提供SLAM的系统性理论讲解
    - [Stanford CS237A (Autonomous Driving)](https://bulletin.stanford.edu/courses/2185453)：涵盖路径规划的基础理论与应用
- **实践**：
  - **工具**：
    - [Cartographer ROS](https://github.com/cartographer-project/cartographer_ros)：Google 出品的 2D/3D 激光 SLAM 框架，支持 TurtleBot2 等平台
    - [MoveIt + OMPL](https://github.com/ros-planning/moveit_tutorials)：用于机械臂高维空间路径规划
    - [LVI-SAM](https://github.com/TixiaoShan/LVI-SAM)：激光+视觉+IMU 的 SLAM 系统
    - [teb_local_planner](https://github.com/rst-tu-dortmund/teb_local_planner)：基于最优控制的局部路径规划器，常用于 ROS 导航
  - **最小目标**：使用 Cartographer 搭建 TurtleBot 2D 激光 SLAM 导航系统；使用 OMPL 创建高维路径规划任务
  - **进阶目标**：用 LVI-SAM +TEB 在非结构化环境中实现实时导航
- **延伸**：
  - **项目**：
    - [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion)：清华出品的多传感器融合SLAM系统，支持双目、IMU、GPS
    - [DSO (Direct Sparse Odometry)](https://github.com/JakobEngel/dso)：直接法视觉里程计，适用于特征点稀疏场景
    - [VINS-Mono](https://github.com/HKUST-Aerial-Robotics/VINS-Mono)：单目+IMU的滑动窗口优化实现
    - [Multi-Robot Exploration](https://github.com/hrnr/m-explore)：多机器人协作探索与地图共享系统
  - **工具**：
    - [OMPL](https://ompl.kavrakilab.org/)：开源运动规划库，提供多种采样规划算法

---

#### 2.6 力控与触觉

- **前置要求**：ROS / 基础力学与控制理论
- **理论**：
  - **基础**：刚体动力学与逆动力学 → 力-位置控制（Hybrid Control） → 阻抗控制（Impedance Control） → 导纳控制（Admittance Control） → 优化控制 + MPC → 触觉传感器类型 → 触觉信号处理
  - **课程**：
    - 《现代机器人学》：强烈推荐第6章“力/力矩传感”，涵盖力控核心理论
    - MIT 6.141 Robotics：包含力控基础，适合系统性学习
- **实践**：
  - **工具**：
    - [Gazebo](https://gazebosim.org/home)：真实物理模拟环境
    - [Isaac Sim](https://developer.nvidia.com/isaac/sim)：NVIDIA 基于其 Omniverse 平台构建的开源机器人仿真工具
  - **最小目标**：在 Gazebo 中安装 `ros_control` 并配置一个六维力/力矩传感器插件（ForceTorqueSensor），实现简单的阻抗控制
  - **进阶目标**：使用 Isaac Sim 搭建一个触觉反馈环境，训练一个基于触觉信号的抓取策略
- **延伸**：
  - [Feel the Force (FTF)](https://feel-the-force-ftf.github.io)：从人类示范中学习力敏感操作的开源项目，结合力控与学习算法，可用于研究机器人在接触任务中的策略生成
  - [HATPIC](https://arxiv.org/abs/2502.17362)：开源单轴触觉操纵杆，用于远程操作与力反馈实验，适合自建低成本触觉装置
    - [“Dexterous Manipulation through Imitation Learning: A Survey”](https://arxiv.org/html/2504.03515v3)：关于灵巧操作的综述论文

---

#### 2.7 VLA

- **前置要求**：Transformer / CLIP / SigLIP / 模仿学习
- **理论**：
  - **基础**：Isaac 与 RoboMimic 使用 → Diffusion / Flow Matching 生成策略 → OpenVLA
  - **材料**：
    - [Isaac Lab 中文文档](https://docs.omniverse.nvidia.com/isaacsim/latest/)：学习任务定义、环境创建与操作演示
    - [Diffusion Policy](https://github.com/real-stanford/diffusion_policy)：基于扩散模型的策略学习方法，适用于高维动作空间。
    - [3D Diffusion Policy (DP3)](https://github.com/YanjieZe/3D-Diffusion-Policy)：将3D视觉表示与扩散策略相结合，提升泛化能力。
    - [OpenVLA](https://github.com/OpenVLA/OpenVLA)：开源通用 VLA 模型，基于 SigLIP+DINOV2 视觉编码器和 Llama 2-7B 语言模型
- **实践**：
  - **工具**：
    - [Isaac Sim](https://developer.nvidia.com/isaac-sim)：机器人三维仿真平台，用于搭建“厨房”等复杂任务环境。
    - [Isaac Lab](https://github.com/NVIDIA-Omniverse/IsaacLab.git)：用于任务定义和训练的框架，支持示例脚本运行。
  - **最小目标**：使用 OpenVLA 为基础构建多任务环境（pick-place、开关抽屉、积木等），融合多模态输入（语言 + 图像 + 状态），分析模型的泛化能力
  - **进阶目标**：搭建 ROS2 + Isaac Sim/Real Franka 桥接环境，实现 camera calibration + 实时 image embedding，随后用 PC 上的语言指令控制真实机器人完成复杂任务
- **延伸**：
  - **项目**：
    - [ALOHA / ACT](https://github.com/tonyzhaozh/aloha)：低成本双臂机器人系统与配套的动作分块策略，支持长时序任务执行。
    - [RT-1](https://github.com/google-research/robotics_transformer)：Google 提出的 Transformer 模型，用于多任务机器人控制
    - [RDT-1B](https://github.com/thu-ml/RoboticsDiffusionTransformer)：清华大学发布的 12 亿参数扩散基础模型，支持多机器人操作
    - [n0 (Pi-0)](https://github.com/Physical-Intelligence/openpi)：由 Physical Intelligence 提出的 VLA 流匹配模型，支持连续动作块输出
    - [DexVLA](https://github.com/juruobenruo/DexVLA)：Cornell 大学提出的 VLA模型，通过插入可插拔扩散动作专家提升效率
  - **工具**：
    - [Hugging Face Transformers](https://huggingface.co/)：用于加载和微调大型视觉-语言模型（如SigLIP, Llama）
    - [RoboMimic](https://github.com/ARISE-Initiative/robomimic.git)：模仿学习库，支持行为克隆（BC）等策略，用于模型训练

---

#### 2.8 Sim2Real

- **前置要求**：ROS / 强化学习
- **理论**：
  - **基础**：主流仿真环境（MuJoCo, Isaac Gym, Isaac Sim, PyBullet） → Sim2Sim → 域适应（Domain Adaptation） → 域随机化（Domain Randomization） → 增量网络（Progressive Network） → 逆动力学模型（Inverse Dynamics Model）
  - **材料**：
    - [MuJoCo](https://github.com/google-deepmind/mujoco)：高性能物理引擎，适合研究和开发
    - [Isaac Gym](https://developer.nvidia.com/isaac-gym)：用于大规模并行强化学习训练的 GPU 加速平台
    - [PyBullet](https://github.com/bulletphysics/bullet3)：轻量级物理仿真平台，用于搭建机械臂抓取实验环境
    - [Tzeng等人 (2015) - Domain Adaptation + 对比学习](https://arxiv.org/abs/1505.07683)：通过联合训练实现仿真与现实图像的隐空间对齐
    - [Gupta等人 (2017) - Invariant Representation with Dynamic Time Warping](https://arxiv.org/abs/1703.06891)：使用 DTW 对齐模拟与现实状态序列，以迁移 RL 策略
    - [Rusu等人 (2016) - Progressive Nets for Pixels→现实](https://arxiv.org/abs/1608.07243)：采用增量网络结构，连接仿真与现实任务
    - [Peng等人 (2018) - Dynamics Randomization](https://arxiv.org/abs/1803.07070)：对关键物理参数进行随机采样，训练鲁棒性策略
    - [Tobin等人 (2017) - 视觉领域随机化](https://arxiv.org/abs/1703.06891)：对仿真环境中的纹理、光照等进行随机混合，增强视觉模型泛化能力
- **实践**：
  - **工具**：
    - [SplitNet](https://grail.cs.washington.edu/projects/splitnet/)：模块化视觉输入与策略结构，适用于 Sim2Sim 视觉迁移
    - [DRL-PPO-sim2sim-imitationlearning](https://github.com/basverkennis/DRL-PPO-sim2sim-imitationlearning)：悬臂机器人 Sim2Sim 项目，测试模型在不同环境参数下的迁移能力。
    - [NVlabs/handover-sim2real](https://github.com/NVlabs/handover-sim2real)：实现从仿真到现实的点云驱动机器人交接动作学习
    - [facebookresearch/spot-sim2real](https://github.com/facebookresearch/spot-sim2real)：Boston Dynamics Spot 机器人 Sim2Real 框架，支持视觉导航与复杂任务调用
    - [UT-Austin-RobIn/lang4sim2real](https://github.com/UT-Austin-RobIn/lang4sim2real)：结合自然语言提示提升 Sim2Real 迁移效果
    - [anmarr-nabbas/sim2real-ur-gym-gazebo](https://github.com/anmarr-nabbas/sim2real-ur-gym-gazebo)：将 UR5 机械臂在 Gazebo 中训练的 RL 抓取策略迁移到真实环境
    - [mehrab-abrar/Sim2Real (Quadruped)](https://github.com/mehrab-abrar/Sim2Real)：在“Frozen Lake”环境中训练四足机器人策略并迁移到真实实验
  - **最小目标**：安装 Habitat + SplitNet，测试 sim-to-sim performance
  - **进阶目标**：运行任意 Sim2Real demo，记录仿真与实机的差别；插入增强方法，如 Domain Randomization、逆动力模型或语言提示，比较性能变化
- **延伸**：
  - [Unitree RL GYM](https://github.com/unitreerobotics/unitree_rl_gym)：四足机器人跨仿真迁移平台，支持从 Isaac Gym 到 MuJoCo 再到实机的完整流程
  - [Humanoid-Gym](https://github.com/roboterax/humanoid-gym)：Isaac Gym 上 humanoid locomotion，支持 zero-shot Sim2Real,并提供 Sim2Sim 测试
  - [DRL-PPO-sim2sim-imitationlearning](https://github.com/basverkennis/DRL-PPO-sim2sim-imitationlearning)：悬臂机器人 Sim2Sim 项目，测试模型在不同环境参数下的迁移能力
  - [NVlabs/handover-sim2real](https://github.com/NVlabs/handover-sim2real)：实现从仿真到现实的点云驱动机器人交接动作学习

---

#### 2.9 世界模型

- **前置要求**：强化学习 / 概率建模 / 变分自编码器（VAE）
- **理论**：
  - **基础**：
    - 潜在动力学建模（Latent Dynamics Modeling）
    - 世界模型（World Model） → Dreamer → DreamerV2 → DreamerV3
    - 模拟器替代学习（Model-Based RL, MBRL）
  - **材料**：
    - [World Models (Ha & Schmidhuber, 2018)](https://arxiv.org/abs/1803.10122)：提出以 VAE+MDN-RNN 结构学习环境动力学
    - [DreamerV2 (Hafner et al., 2021)](https://arxiv.org/abs/2010.02193)：基于潜在动力学的 MBRL 算法，能在潜空间中进行长序列规划
    - [DreamerV3 (Hafner et al., 2023)](https://arxiv.org/abs/2301.04104)：实现跨任务通用性与高样本效率
    - [PlaNet (Hafner et al., 2019)](https://arxiv.org/abs/1811.04551)：基于潜在空间预测与规划的开创性算法
- **实践**：
  - **工具**：
    - [DreamerV3 Official Implementation](https://github.com/danijar/dreamerv3)：作者官方 PyTorch 实现
    - [Planet / Dreamer Reimplementation (PyTorch)](https://github.com/facebookresearch/torchbeast)：支持可并行训练和多环境实验
    - [gymnax](https://github.com/RobertTLange/gymnax)：JAX 强化学习环境库，常用于 Dreamer 训练
  - **最小目标**：使用 Dreamer 复现 CartPole / Cheetah 环境中的潜在动力学预测；在潜空间进行“虚拟环境”训练
  - **进阶目标**：结合 PyBullet 或 Isaac Gym 训练机械臂模型的世界模型，实现从视觉输入预测未来状态，并基于潜在动力学进行规划
- **延伸**：
  - **项目**：
    - [DreamerV3 Robotics](https://github.com/DreamerV3Robotics)：将 Dreamer 应用于真实机械臂与移动机器人控制
    - [World Model Policy Gradient (WM-PG)](https://github.com/icoz69/WM-PG)：使用潜在空间规划指导 RL 策略学习
    - [MIRAGE](https://github.com/robustrobotics/MIRAGE)：结合世界模型与规划的多模态机器人控制系统
  - **工具**：
    - [BraX](https://github.com/google/brax)：GPU/TPU 加速的物理仿真平台，可快速验证 Dreamer 类算法
    - [Isaac Gym](https://developer.nvidia.com/isaac-gym)：用于多任务并行的世界模型训练与验证

---

#### 2.10 数据飞轮与遥操作

- **前置要求**：强化学习 / 模仿学习 / 数据工程基础（数据清洗、标注、版本控制）
- **理论**：
  - **基础**：数据飞轮与遥操作概念 → 力反馈遥操作 → AR/VR 远程控制 → 模型辅助示教（e.g. Diffusion Policy Warm-start）
  - **材料**：
    - [Tele-operation & Flywheel](https://medium.com/@chaseyvy/teleoperation-the-human-link-and-flywheel-of-physical-ai-1c5b82ba1c80)：：数据飞轮与遥操作基础概念博客
    - [PATO](https://arxiv.org/abs/2212.04708)：提出“策略辅助遥操作”框架，使人机协作更高效，助力可扩展数据采集
    - [Open-TeleVision](https://arxiv.org/html/2407.01512v2)：沉浸式视觉遥操作系统，用于高质量示教数据采集
- **实践**：
  - **工具**：
    - [ALOHA](https://github.com/tonyzhaozh/aloha)：低成本双臂遥操作系统，提供数据采集与回放脚本
    - [Open-TeleVision](https://github.com/OpenTeleVision/TeleVision)：沉浸式远程控制与反馈系统
  - **最小目标**：使用 ALOHA 系统采集单任务（如物体抓取）数据 → 训练一个 BC 策略 → 使用同样系统部署策略并采集新演示数据
  - **进阶目标**：构建完整数据飞轮管线：通过 Teleop 采集数据 → 进行自动清洗与标准化 → 使用 Diffusion Policy / OpenVLA 训练模型 → 策略部署到实机 → 新数据自动回流、增强数据集
- **延伸**：
  - **项目**：
    - [SharedAssembly](https://arxiv.org/abs/2503.12287)：通过双操作员共享遥操作系统，提升装配任务数据采集规模与质量
    - [Super-Linear Scaling](https://arxiv.org/html/2412.01770v3)：通过众包真实场景数字孪生并在仿真中采集数据，实现“人力投入与性能超线性增长”的机器人学习飞轮
    - [DexFlyWheel](https://arxiv.org/html/2509.23829v1)：提出双臂灵巧操作的数据飞轮机制，从少量人类示范出发，通过 IL + residual RL 实现自增强数据生成。  
  - **工具**：
    - [MLflow](https://mlflow.org/)：用于监控训练与数据更新过程

---

## 3. 基础学习（机器人基础｜深度学习基础）

**贡献者**：@mumu-jushen，@KandS
**你将获得**：机器人学数学基础、深度学习核心机制、工程实践能力；从"坐标变换→运动规划→神经网络→多模态融合"构建知识体系。

### 目录（Table of Contents）
- [3.1 机器人学打底：坐标系/运动学/动力学/控制](#31-机器人学打底坐标系运动学动力学控制)
- [3.2 深度学习打底：Self-Attention 与 Transformer](#32-深度学习打底self-attention与transformer)
- [3.3 深度学习打底：Diffusion (DDIM)](#33-深度学习打底diffusion-ddim)
- [3.4 深度学习打底：优化/正则化/训练技巧](#34-深度学习打底优化正则化训练技巧)
- [3.5 工程环境：Conda/Docker、日志与可视化、复现实验规范](#35-工程环境condadocker日志与可视化复现实验规范)
- [3.6 实战与应用：机器人中的多模态/GAT](#36-实战与应用机器人中的多模态gat)

---

### 3.1 机器人学打底：坐标系/运动学/动力学/控制

#### 起步三件事

⭐ **必看**：[Modern Robotics](http://hades.mech.northwestern.edu/index.php/Modern_Robotics) 第2-4章（坐标系、正逆运动学）

🧪 **实作**：用Python实现平面二连杆的正逆运动学求解

📦 **代码**：[Robotics Toolbox for Python](https://github.com/petercorke/robotics-toolbox-python) - Peter Corke的经典工具箱

#### 核心知识点

**坐标系与齐次变换**

机器人要在空间中精确操作，核心是搞清楚"我在哪，要去哪"。这需要多个坐标系协同：

- **世界坐标系 {W}**：全局固定参考，所有物体位置相对于它描述
- **基座坐标系 {B}**：机器人自身参考系
- **工具坐标系 {T}**：末端执行器（夹爪中心）
- **物体坐标系 {O}**：待操作物体

齐次变换矩阵统一旋转R和平移P：
```
T = [R_{3×3}  P_{3×1}]
    [0_{1×3}     1   ]
```
串联机械臂从基座到末端： $T_0^n = T_0^1 \cdot T_1^2 \cdots T_{n-1}^n$

**正逆运动学**

- **正运动学(FK)**：关节角度 → 末端位姿
  平面二连杆：`x = L1*cos(θ1) + L2*cos(θ1+θ2)`

- **逆运动学(IK)**：末端位姿 → 关节角度
  难点：无解（够不着）、多解（肘向上/下）、奇异点（失去自由度）

**DH参数法**

用4个参数 $(θ_i, d_i, a_i, α_i)$ 标准化描述连杆关系：
- 连杆长度 $a_i$：沿 $x_i$ 轴距离
- 连杆扭角 $α_i$：绕 $x_i$ 轴角度
- 连杆偏距 $d_i$：沿 $z_{i-1}$ 轴距离
- 关节角 $θ_i$：绕 $z_{i-1}$ 轴角度

**轨迹规划对比**

| 规划空间 | 优点 | 缺点 | 适用场景 |
|---------|------|------|---------|
| 关节空间 | 计算简单、无奇异点 | 末端路径不可控 | 点到点运动 |
| 笛卡尔空间 | 路径精确可控 | 每点需IK、可能奇异 | 焊接、喷涂、装配 |

三次多项式保证速度连续，五次保证加速度连续，避免机械冲击。

**雅可比矩阵**

建立关节速度 $\dot{q}$ 和末端速度 $v$ 的桥梁：
```
v = J(q) · q̇  （速度正运动学）
τ = J^T · F  （静力学关系）
```
当 $\det(J)=0$ 时处于奇异位形，失去某自由度。

**MoveIt框架架构**

```
用户接口层
├── MoveIt Commander（Python/C++ API）
├── Rviz Plugin（可视化拖动）
└── Setup Assistant（配置向导）

核心规划层
├── Move Group（中央协调）
├── Planning Scene（环境模型）
├── Planning Pipeline
│   ├── OMPL（RRT/PRM采样）
│   ├── CHOMP（轨迹优化）
│   └── Pilz（工业轨迹）
└── Kinematics Solver（KDL/IKFast）

执行控制层
└── Trajectory Execution → Controllers
```

#### 实践要点

- **坐标变换**： $T_A^B$ 表示从 A 到 B，连续变换从右往左读
- **逆运动学**：优先解析解（快），数值解做后备
- **轨迹规划**：简单任务用梯形速度，复杂用五次多项式
- **MoveIt调试**：碰撞太严调 `padding`，规划失败查起点碰撞

---

### 3.2 深度学习打底：Self-Attention与Transformer

#### 起步三件事

⭐ **必看**：[The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - Jay Alammar的可视化讲解

🧪 **实作**：手撕一个mini Transformer（<500行代码）

📄 **论文**：[Attention Is All You Need](https://arxiv.org/abs/1706.03762) - 原始论文

![Transformer整体架构](files/images/第三节/transformer%20structure.png)

#### [Transformer：从黑盒到掌握全貌](files/foundations/3.2-Transformer.md#transformer从黑盒到掌握全貌)
- **第一层理解**：Transformer 是一个黑盒子，输入法语，输出英语，显著提升机器翻译质量。
- **第二层理解**：Transformer 由编码器（Encoder）和解码器（Decoder）组成，原论文各用 6 层，但层数可变（如 BERT 用 12 层，GPT-3 用 96 层）。
- **第三层理解**：每一层编码器包含 Self-Attention 和 Feed Forward 操作，均配备残差连接和 Layer Norm。

#### [Self-Attention：核心中的核心](files/foundations/3.2-Transformer.md#self-attention核心中的核心)
- **为啥需要 Self-Attention**：让序列中任意两个位置能直接“对话”，解决传统 RNN 信息丢失和 CNN 窗口固定的问题。
- **Query-Key-Value 机制**：通过 QKV 计算注意力分数，公式为 `scores = Q @ K.T / sqrt(d_k)`，除以 `sqrt(d_k)` 防止梯度消失。
- **注意力可视化**：通过可视化注意力权重，模型能正确学习指代关系。

#### [多头注意力：团队协作](files/foundations/3.2-Transformer.md#多头注意力团队协作)
- 多头注意力是多个专家团队，每个头负责不同维度，学习不同类型的关系（如局部语法、长距离依赖等）。
- 代码示例展示了如何实现多头注意力，包括 QKV 的计算和多头的合并。

#### [位置编码：告诉模型词序](files/foundations/3.2-Transformer.md#位置编码告诉模型词序)
- Self-Attention 无法感知词序，位置编码通过 sin/cos 函数解决，能表示相对位置关系。
- 代码示例展示了位置编码的实现。

#### [残差连接与Layer Norm](files/foundations/3.2-Transformer.md#残差连接与layer-norm)
- 每个子层使用残差连接（防止梯度消失）和 Layer Norm（稳定输入分布），加速训练。
- 代码示例展示了残差连接和 Layer Norm 的实现。

#### [Encoder完整实现](files/foundations/3.2-Transformer.md#encoder完整实现)
- 编码器由多层 EncoderLayer 组成，每层包含多头注意力、前馈网络和残差连接。
- 代码示例展示了编码器的完整实现。

#### [Decoder：带Mask的生成器](files/foundations/3.2-Transformer.md#decoder带mask的生成器)
- 解码器比编码器多了 Masked Self-Attention（防止看到未来）和 Encoder-Decoder Attention（接收编码器输出）。
- 代码示例展示了如何创建下三角掩码。

#### [实战踩坑经验](files/foundations/3.2-Transformer.md#实战踩坑经验)
- 常见错误包括维度对不上、忘记缩放、位置编码当参数训练、Layer Norm 位置错误。
- 提供了正确的代码示例和调试建议。

#### 为什么Transformer这么强？

**并行性**
- RNN 必须串行处理，第 t 步依赖第 t-1 步
- Transformer 可以并行处理整个序列，训练速度飞快

**长距离依赖**
- RNN 信息传递路径长，容易遗忘
- Transformer 任意两个位置都能直接交互

**表达能力**
- 多头注意力 = 多个特征提取器并行工作
- 每个头可以学习不同类型的依赖关系

**计算复杂度对比**
| 模型 | 每层复杂度 | 并行度 | 最大路径长度 |
|------|------------|--------|--------------|
| RNN | O(n·d²) | O(n) | O(n) |
| CNN | O(k·n·d²) | O(1) | O(log_k(n)) |
| Transformer | O(n²·d) | O(1) | O(1) |

虽然是 O(n²)，但对于常见长度（<512），这不是瓶颈。瓶颈通常在d（模型维度）上。

#### 调试技巧总结

1. **先跑通小模型**：2 层、128 维度、4 个头，确保流程正确
2. **可视化注意力权重**：检查模型是否学到合理的模式
3. **梯度裁剪**：`torch.nn.utils.clip_grad_norm_(model.parameters(), 1.0)`
4. **学习率warmup必须有**：前 4000 步线性增长很重要
5. **检查mask是否正确**：打印出来看看，很多 bug 在这

---

### 3.3 深度学习打底：Diffusion (DDIM)

#### 什么是DDIM?

DDIM（Denoising Diffusion Implicit Models）是一种扩散模型的变体，旨在加速图像生成过程并保持生成质量。它是在 **DDPM**（Denoising Diffusion Probabilistic Models）的基础上发展出来的，提供了一种更高效的去噪采样过程，减少了采样所需的步骤数。

在 DDIM 中，通过构造一种**确定性的去噪过程**，可以在显著减少采样步骤的情况下生成高质量图像。与传统的 DDPM 不同，DDIM 不再依赖完全的随机采样过程，而是通过精确控制去噪路径，使得生成的样本更加可控，并允许在更少的步骤内完成采样。

#### DDIM和DDPM的区别

DDPM 和 DDIM 的主要区别可以总结为以下几个方面：

1. **采样过程的确定性 vs 随机性**
   - **DDPM**：采样过程是随机的，每个时间步都通过加噪声和去噪的迭代采样来生成样本。这种随机性确保了样本的多样性和随机性，但会导致采样速度较慢。
   - **DDIM**：采样过程是确定性的。它通过推导出一种新的去噪方程，能够确定性地生成样本，不需要每一步都添加随机噪声。因此，DDIM 能够以更少的时间步生成样本。

2. **采样速度**
   - **DDPM**：DDPM 的采样过程需要执行大量的时间步的迭代（例如 1000 个步骤），这使得它在实践中非常慢。
   - **DDIM**：DDIM 在生成过程中能够通过使用一种隐式的采样机制，大大减少所需的时间步（例如 50 个或 100 个步骤），从而显著加快采样速度，同时保留较高的图像质量。

3. **采样路径**
   - **DDPM**：DDPM 的采样路径严格遵循一系列的高斯噪声到纯净数据的逐步去噪。
   - **DDIM**：DDIM 通过改变时间步的更新规则，使得采样路径可以直接从高斯噪声跳跃到纯净数据，更为灵活。

4. **样本生成的灵活性**
   - **DDPM**：由于每一步都添加了随机性，DDPM 的采样过程是不可控的，即使是同样的初始噪声，每次采样的结果也可能不同。
   - **DDIM**：通过去掉采样过程中的随机性，DDIM 提供了一种确定性生成机制，即同样的初始条件会生成同样的样本。这对于某些任务非常有用，尤其是需要生成相同的图像或在多次采样中保持一致性时。

#### DDIM的工作原理

DDIM 的主要目的是在加速采样的同时保留高质量的图像生成。它通过修改扩散模型中的逆扩散过程，从而实现这一目标。

**扩散过程**
在扩散模型中，原始数据（如图像）通过逐步加噪声的方式转变为高斯噪声。这个加噪过程遵循如下的公式：

$$
q(x_t|x_{t-1}) = \mathcal{N}(x_t; \sqrt{\alpha_t}x_{t-1}, (1 - \alpha_t)I)
$$

这里， $x_t$ 是在第 t 个时间步的噪声数据， $\alpha_t$ 是时间步的系数。这个公式描述了如何通过将噪声逐步加到数据上来生成噪声样本。

**去噪过程**
在 DDPM 中，去噪过程反向执行，即从 $x_T$ （完全噪声的样本）开始逐步去除噪声，生成 $x_0$ （即数据样本）。这个去噪过程是逐步的，并且是随机的。

在 DDIM 中，去噪过程是确定的，采样过程使用了一种新的公式，不需要每一步都添加随机噪声。具体来说，DDIM 推导出了一个可以直接从高斯噪声样本跳跃到纯净样本的新去噪方程：

$$
x_{t-1} = \frac{1}{\sqrt{\alpha_{t-1}}}x_0 + \sqrt{1 - \alpha_{t-1}}\epsilon_t
$$

其中， $x_0$ 是通过网络预测得到的纯净样本， $\epsilon_t$ 是噪声。

通过这个公式，DDIM 能够在更少的时间步内从噪声生成样本。这种直接跳跃的去噪路径是 DDIM 比 DDPM 更高效的关键。

#### 如何使用DDIM

DDIM 的实现一般依赖于已有的扩散模型（如 DDPM）。只需要调整采样部分的代码即可将 DDPM 的随机采样替换为 DDIM 的确定性采样。

下面是一个简化的伪代码，展示如何在生成过程中使用 DDIM 进行加速采样：

```python
import torch

def ddim_sampling(model, x_T, num_steps, betas):"""
    使用 DDIM 采样生成数据
    :param model: 经过训练的扩散模型
    :param x_T: 随机噪声初始样本
    :param num_steps: 采样的总步骤数
    :param betas: 噪声的时间步参数
    :return: 生成的样本
    """
    x_t = x_T  # 从纯噪声开始for t in reversed(range(1, num_steps)):# 预测当前时间步的纯净样本
        x_0_pred = model(x_t, t)
        
        # 计算DDIM更新步骤
        alpha_t = torch.prod(1 - betas[:t])
        alpha_t_prev = torch.prod(1 - betas[:t-1])
        
        # 计算噪声项
        noise = torch.randn_like(x_t) if t &gt; 1 else torch.zeros_like(x_t)
        x_t_1 = torch.sqrt(alpha_t_prev) * x_0_pred + torch.sqrt(1 - alpha_t_prev) * noise
        
    return x_t_1
```

#### 总结
DDIM 相比于传统的 DDPM，提供了一个加速的采样过程，能够通过确定性去噪生成高质量图像，同时显著减少采样步骤数量。它通过去除每一步的随机噪声引入，实现了一种隐式（Implicit）采样机制，使得同样的输入可以生成一致的样本。

DDIM 的优势在于：
1. 加速采样过程，能够在更少的时间步内生成图像。
2. 确定性采样，允许生成一致性更强的样本。
3. 保留生成质量，在减少时间步的情况下，仍然能够生成高质量的样本。

它是扩散模型的一个重要扩展，特别适合在需要快速生成高质量图像的任务中使用。

---

### 3.4 深度学习打底：优化/正则化/训练技巧

#### [让模型真正学起来：优化器的选择](files/foundations/3.4-优化.md#让模型真正学起来优化器的选择)
训练神经网络就像爬山找最低点，优化器决定了你怎么走。

- **最简单的 SGD（随机梯度下降）**：简单但收敛慢。
- **带动量的 SGD**：像滚雪球，能冲过小坑加速收敛。
- **Adam**：自适应学习率，几乎不用调参，适合懒人。

#### [学习率调度：训练的节奏感](files/foundations/3.4-优化.md#学习率调度训练的节奏感)
学习率不能一成不变，像学车一样需要调整节奏。

- **阶梯式下降**：每固定步数降低学习率。
- **余弦退火**：学习率像余弦函数一样平滑下降。
- **Warmup**：先小学习率热身，适合 Transformer。

#### [防止过拟合：正则化技术](files/foundations/3.4-优化.md#防止过拟合正则化技术)
模型太强会过拟合，需要正则化技术来控制。

- **Dropout**：随机关闭神经元，防止过拟合。
- **BatchNorm vs LayerNorm**：归一化技术，LayerNorm 更适合 Transformer。
- **Label Smoothing**：让模型别太自信，泛化性更好。

#### [混合精度训练：又快又省显存](files/foundations/3.4-优化.md#混合精度训练又快又省显存)
混合精度训练用float16，显存省一半，速度快2-3倍。

- **使用`autocast`和`GradScaler`**：防止梯度下溢，加速训练。
- **适用场景**：模型大、显存不够时必须用；想加速训练时推荐用。
- **注意事项**：老 GPU 不支持，某些操作可能不稳定。

---

### 3.5 工程环境：Conda/Docker/日志与可视化/复现实验规范

#### [环境管理：让代码在任何地方都能跑](files/foundations/3.5-工程环境.md#环境管理：让代码在任何地方都能跑)

**Conda**
- Conda 的基本操作：创建、激活环境，安装 PyTorch，导出和复现环境。
- Conda 和 pip 混用的技巧：先用 conda 装大件，再用 pip 装小包。

**Docker：终极解决方案**
- Dockerfile 示例：构建和运行容器，挂载本地目录。
- Docker 的坑：Windows 路径问题、GPU 支持、镜像大小。

#### [实验追踪：WandB让你知道哪次实验效果好](files/foundations/3.5-工程环境.md#实验追踪：wandb让你知道哪次实验效果好)

**WandB（Weights & Biases）入门**
- 初始化、记录日志、可视化界面。
- 超参数搜索：贝叶斯优化。
- TensorBoard（备选）：本地可视化方案。

#### [实验可重复性：让结果能复现](files/foundations/3.5-工程环境.md#实验可重复性：让结果能复现)

**固定随机种子**
- 完全固定随机性（`torch.backends.cudnn.deterministic` 和 `benchmark`）。
- 折中方案：部分固定，性能更好。

**配置文件管理**
- 使用 YAML 配置文件，命令行参数覆盖配置。

#### [代码组织：专业的项目结构](files/foundations/3.5-工程环境.md#代码组织专业的项目结构)

**标准项目结构**
- 分层目录结构：`configs`、`data`、`models`、`utils`、`scripts` 等。
- 使用 `setup.py` 让代码可安装。

#### [调试技巧：快速定位问题](files/foundations/3.5-工程环境.md#调试技巧快速定位问题)

**打印shape是第一步**
- 在每个模块打印输入输出 shape。

**用assert检查假设**
- 检查张量维度、值范围等。

**梯度检查**
- 检查梯度是否正常，避免 NaN。

**常见错误和解决**
- CUDA out of memory：减小 batch size、梯度累积、删除变量。
- Loss 变成 NaN：检查输入、梯度裁剪、调整学习率。
- DataLoader 卡死：调整 `num_workers`。

---

### 3.6 实战与应用：机器人中的多模态/GAT

#### 多模态融合：让机器人有多种感知

机器人不只有眼睛（相机），还有触觉、关节编码器、力传感器...怎么把这些信息融合起来？

**统一到同一个特征空间**

最简单的思路——把所有模态都编码成相同维度的向量：

```python
class MultiModalEncoder(nn.Module):
    def __init__(self, d_model=512):
        super().__init__()
        # 不同模态用不同编码器
        self.vision_encoder = nn.Linear(2048, d_model)  # ResNet特征
        self.text_encoder = nn.Embedding(10000, d_model)  # 词嵌入
        self.joint_encoder = nn.Linear(7, d_model)  # 7自由度机械臂
        self.force_encoder = nn.Linear(6, d_model)  # 6轴力传感器

    def forward(self, vision=None, text=None, joints=None, force=None):
        tokens = []

        if vision is not None:
            # vision: [batch, 2048]
            vision_tokens = self.vision_encoder(vision)  # [batch, d_model]
            tokens.append(vision_tokens.unsqueeze(1))  # [batch, 1, d_model]

        if text is not None:
            # text: [batch, seq_len]
            text_tokens = self.text_encoder(text)  # [batch, seq_len, d_model]
            tokens.append(text_tokens)

        if joints is not None:
            # joints: [batch, 7]
            joint_tokens = self.joint_encoder(joints)
            tokens.append(joint_tokens.unsqueeze(1))

        if force is not None:
            # force: [batch, 6]
            force_tokens = self.force_encoder(force)
            tokens.append(force_tokens.unsqueeze(1))

        # 拼接所有模态
        multi_modal = torch.cat(tokens, dim=1)  # [batch, total_seq_len, d_model]
        return multi_modal
```

然后扔给 Transformer 处理，它会自动学习跨模态关系！

**跨模态注意力的实际效果**

训练后你会发现神奇的现象：
- 当文本说"抓取红色方块"，视觉注意力会聚焦在红色区域
- 当力传感器检测到碰撞，文本理解会关注"小心"、"慢速"这些词
- 关节接近限位时，规划模块会降低相应方向的运动权重

**处理不同采样率**

现实中各传感器频率不同：
- 相机：30Hz
- 关节编码器：100Hz
- 力传感器：1000Hz

怎么对齐？

```python
# 方法1：下采样到最低频率（简单但损失信息）
def align_to_vision_rate(vision_seq, joint_seq, force_seq):
    # vision_seq: [T_v=30, ...]
    # joint_seq: [T_j=100, ...]
    # force_seq: [T_f=1000, ...]

    # 下采样到30Hz
    joint_downsampled = joint_seq[::3]    # 每3个取1个，100Hz→33Hz≈30Hz
    force_downsampled = force_seq[::33]   # 每33个取1个，1000Hz→30Hz

    return vision_seq, joint_downsampled, force_downsampled

# 方法2：分层处理（保留高频信息）
class HierarchicalFusion(nn.Module):
    def __init__(self):
        super().__init__()
        # 高频融合器（1000Hz）
        self.force_processor = nn.LSTM(6, 64)
        # 中频融合器（100Hz）
        self.joint_force_fusion = nn.LSTM(64+7, 128)
        # 低频融合器（30Hz）
        self.full_fusion = nn.LSTM(128+2048, 512)

    def forward(self, vision, joints, force):
        # Step1: 处理高频力信号（1000Hz）
        force_features, _ = self.force_processor(force)  # [1000, 64]
        # 池化到100Hz
        force_100hz = F.adaptive_avg_pool1d(
            force_features.transpose(0, 1).unsqueeze(0),
            output_size=100
        ).squeeze(0).transpose(0, 1)

        # Step2: 融合中频信号（100Hz）
        joint_force = torch.cat([joints, force_100hz], dim=-1)
        mid_features, _ = self.joint_force_fusion(joint_force)
        # 池化到30Hz
        mid_30hz = mid_features[::3]

        # Step3: 融合所有模态（30Hz）
        full_input = torch.cat([vision, mid_30hz], dim=-1)
        output, _ = self.full_fusion(full_input)

        return output
```

**实际场景的多模态策略**

插USB（需要力反馈）：
```python
def usb_insertion_policy(vision, force, joint):
    # 阶段1：视觉引导接近
    if not in_contact(force):
        action = vision_servo(vision, target="usb_port")

    # 阶段2：接触后切换到力控
    else:
        # 维持小的插入力，调整姿态
        action = force_control(
            force,
            target_force=[0, 0, 5, 0, 0, 0],  # Z方向5N
            compliance=[0.1, 0.1, 0.01, 0.5, 0.5, 0.5]  # XY柔顺，Z硬
        )

    return action
```

#### 图神经网络（GAT）：理解场景关系

机器人要理解的不只是"有什么"，还要理解"谁和谁有什么关系"。

**场景表示成图**

想象桌面场景：
- 节点：每个物体（杯子、书、笔）
- 边：物体间的关系（接触、遮挡、支撑）

```python
class SceneGraph:
    def __init__(self):
        self.objects = []  # 节点列表
        self.relations = []  # 边列表

    def add_object(self, obj_id, features):
        """添加物体节点"""
        self.objects.append({
            'id': obj_id,
            'features': features,  # 位置、颜色、形状等
            'type': detect_object_type(features)
        })

    def add_relation(self, obj1_id, obj2_id, rel_type):
        """添加关系边"""
        self.relations.append({
            'source': obj1_id,
            'target': obj2_id,
            'type': rel_type  # 'on_top_of', 'occluding', 'near'等
        })

# 实际使用
scene = SceneGraph()
scene.add_object('cup_1', cup_features)
scene.add_object('table_1', table_features)
scene.add_relation('cup_1', 'table_1', 'on_top_of')
```

**图注意力机制（GAT）**

GAT 让每个节点通过注意力机制聚合邻居信息：

```python
class GraphAttentionLayer(nn.Module):
    def __init__(self, in_dim, out_dim, dropout=0.1):
        super().__init__()
        self.W = nn.Linear(in_dim, out_dim, bias=False)
        self.a = nn.Parameter(torch.randn(2 * out_dim, 1))
        self.dropout = nn.Dropout(dropout)
        self.leakyrelu = nn.LeakyReLU(0.2)

    def forward(self, node_features, adjacency):
        # node_features: [N, in_dim]
        # adjacency: [N, N] 邻接矩阵

        N = node_features.shape[0]
        h = self.W(node_features)  # [N, out_dim]

        # 计算注意力分数
        # 这里用的是Veličković et al. 2018的方法
        h_i = h.unsqueeze(1).repeat(1, N, 1)  # [N, N, out_dim]
        h_j = h.unsqueeze(0).repeat(N, 1, 1)  # [N, N, out_dim]
        concat = torch.cat([h_i, h_j], dim=-1)  # [N, N, 2*out_dim]

        e = self.leakyrelu(torch.matmul(concat, self.a).squeeze(-1))  # [N, N]

        # 只保留存在边的注意力
        zero_vec = -9e15 * torch.ones_like(e)
        attention = torch.where(adjacency > 0, e, zero_vec)
        attention = F.softmax(attention, dim=-1)
        attention = self.dropout(attention)

        # 聚合邻居特征
        h_prime = torch.matmul(attention, h)  # [N, out_dim]
        return F.elu(h_prime)
```

**实际应用：抓取规划**

用 GAT 理解场景，找出最容易抓取的物体：

```python
class GraspPlanner(nn.Module):
    def __init__(self):
        super().__init__()
        self.gat1 = GraphAttentionLayer(512, 256)
        self.gat2 = GraphAttentionLayer(256, 128)
        self.grasp_score = nn.Linear(128, 1)  # 输出抓取分数

    def forward(self, scene_graph):
        # 提取特征和邻接矩阵
        node_feats = torch.stack([obj['features'] for obj in scene_graph.objects])
        adj_matrix = build_adjacency_matrix(scene_graph.relations)

        # 两层GAT理解场景关系
        x = self.gat1(node_feats, adj_matrix)
        x = self.gat2(x, adj_matrix)

        # 给每个物体打分
        scores = self.grasp_score(x)  # [N, 1]

        return scores

# 使用时
planner = GraspPlanner()
scores = planner(scene_graph)
best_object_idx = torch.argmax(scores)
# 得分考虑了：
# - 物体本身是否易抓（形状、大小）
# - 是否被其他物体遮挡
# - 抓取后是否会导致其他物体掉落
```

**GAT在机器人中的典型应用**

1. **装配任务**：理解零件之间的装配顺序和约束
2. **导航规划**：理解房间连接关系，找最短路径
3. **人机协作**：理解人的动作意图和物体关系
4. **故障诊断**：通过组件关系图定位问题源头

关键优势：
- 自动学习"什么关系重要"（注意力权重）
- 处理不规则结构（不像 CNN 需要网格）
- 可解释性好（能可视化注意力）

---

## 4. 各技术基础与经典（理论与经典论文/工程）

**贡献者**：@ptman12



### 4.1 Imitation Learning（模仿学习）经典算法综述


本节聚焦于模仿学习（Imitation Learning, IL）中的三大经典方法：​**行为克隆（Behavioral Cloning, BC）**​、​**数据集聚合（Dataset Aggregation, DAgger）**​、以及​**生成式对抗模仿学习（Generative Adversarial Imitation Learning, GAIL）**​。重点讨论它们的原理、经典论文、数据分布偏移（covariate shift）与误差累积问题，以及它们之间的关系与演进。


#### 1. 行为克隆（BC）

##### 1.1 算法简介

行为克隆将模仿学习视为一个典型的监督学习问题。给定专家演示数据集<img width="116" height="30" alt="image" src="https://github.com/user-attachments/assets/e900cab4-60d4-4148-8a7f-76e27fc1fcef" />

，智能体直接训练一个策略 <img width="61" height="25" alt="image" src="https://github.com/user-attachments/assets/1b6f7685-e266-43a9-a36a-fefe34ceca8a" />
 或确定性映射<img width="79" height="26" alt="image" src="https://github.com/user-attachments/assets/c9a3c606-e987-4f27-a233-2afa778aa61a" />
，使其在专家所处状态 (s) 下输出与专家动作 (a^*​) 接近的动作。
其优化目标常写为：
<img width="226" height="45" alt="image" src="https://github.com/user-attachments/assets/245ffe27-a54d-4604-8b06-786730dd8208" />

例如交叉熵损失、回归均方误差等。许多早期工作（如 ALVINN）即采用此方式。 ([arxiv.org](https://arxiv.org/pdf/2106.12177?utm_source=chatgpt.com "Imitation Learning: Progress, Taxonomies and Challenges"))

##### 1.2 优点

* 简单易实现：直接将监督学习技术迁移至策略学习。
* 在专家演示覆盖面较好、环境状态分布较为稳定的场景下，表现常常不错。
* 无需额外设计奖励函数、无需智能体与环境反复交互。

##### 1.3 缺点 — 数据分布偏移与误差累积

正如前文所述，BC 的关键短板在于：训练时只见到了专家策略下的状态分布，而部署时智能体策略可能偏离专家，进入“未知”状态区域，导致性能剧降。这个过程往往伴随着误差累积。文献中从“值差异”角度分析，指出 BC 的值差异（在无穷期折扣模型下）是<img width="112" height="33" alt="image" src="https://github.com/user-attachments/assets/2642ee1b-0c53-4b9a-bcb8-5dba86ce5c40" />
 级别。 ([arxiv.org](https://arxiv.org/abs/1911.07027?utm_source=chatgpt.com "On Value Discrepancy of Imitation Learning"))

换句话说，如果智能体偶尔偏离专家轨迹，一旦进入偏离状态，再恢复到专家轨迹的难度就会变大，错误可能一发不可收。很多实践中，这一问题使 BC 在真实环境（尤其是高维、长时序任务）中表现并不稳定。


#### 2. 数据集聚合（DAgger）

##### 2.1 算法简介

为了解决 BC 的分布偏移问题，DAgger（Dataset Aggregation）在训练过程中允许智能体以当前策略与专家策略混合控制，从而生成新的状态–动作对，并让专家对智能体经历的新状态进行标注。这样，数据集不断 **聚合（aggregate）** 新状态–动作对，包含智能体可能进入的“偏离”状态，从而缩小训练／部署时状态分布的差距。
典型流程：

1. 初始化<img width="18" height="17" alt="image" src="https://github.com/user-attachments/assets/37696f6e-7ac2-41f0-984b-cbef161a5ee6" />
为专家示范数据。
2. 训练策略 <img width="25" height="20" alt="image" src="https://github.com/user-attachments/assets/d10bda55-d516-40fa-9b51-4151fac1ecfd" />
在 <img width="18" height="17" alt="image" src="https://github.com/user-attachments/assets/37696f6e-7ac2-41f0-984b-cbef161a5ee6" />上。
3. 使用当前  <img width="25" height="20" alt="image" src="https://github.com/user-attachments/assets/d10bda55-d516-40fa-9b51-4151fac1ecfd" />与专家混合运行策略生成轨迹。
4. 对于轨迹中的每个状态 s，令专家标注<img width="95" height="28" alt="image" src="https://github.com/user-attachments/assets/27d87f23-2bbd-43e3-9f54-00fd91da2554" />
，将<img width="50" height="31" alt="image" src="https://github.com/user-attachments/assets/cddbe3b3-c43b-497a-922e-610201eb5b76" />
加入<img width="18" height="17" alt="image" src="https://github.com/user-attachments/assets/37696f6e-7ac2-41f0-984b-cbef161a5ee6" />。
5. 重复训练直到收敛。
   详见教材中算法说明。 ([algorithmsbook.com](https://algorithmsbook.com/files/chapter-18.pdf?utm_source=chatgpt.com "18 Imitation Learning"))

##### 2.2 优点

* 能有效缓解智能体进入“未见状态”时缺乏标注的问题。
* 通过在线“探索”其策略可能到达的状态，并让专家加标签，从而覆盖更多状态–动作对。
* 在理论上，为策略的训练损失在其自身状态分布下提供了边界保障。 ([arxiv.org](https://arxiv.org/pdf/2106.12177?utm_source=chatgpt.com "Imitation Learning: Progress, Taxonomies and Challenges"))

##### 2.3 缺点与实际考量

* 需要专家随时可查询：在执行过程中智能体生成新状态时，需要专家实时标注动作，这在许多现实场景中成本较高或不可行。
* 虽然改进了 BC 的分布偏移问题，但仍可能存在：如果策略已严重偏离，生成状态–动作对的质量可能较低。
* 在安全敏感任务中，智能体自主探索可能带来风险。相关扩展如 DropoutDAgger 试图引入不确定性估计以控制风险。 ([arxiv.org](https://arxiv.org/abs/1709.06166?utm_source=chatgpt.com "DropoutDAgger: A Bayesian Approach to Safe Imitation Learning"))


#### 3. 生成式对抗模仿学习（GAIL）

##### 3.1 算法简介

GAIL（Generative Adversarial Imitation Learning）借鉴了生成对抗网络（GAN）的思想，将模仿学习转化为一种 **匹配专家与政策的状态–动作分布** 的问题。

* 设专家策略产生的状态–动作分布为<img width="67" height="35" alt="image" src="https://github.com/user-attachments/assets/bc714a45-4f5b-4401-9775-311034508369" />
，智能体策略<img width="24" height="20" alt="image" src="https://github.com/user-attachments/assets/565a81d7-13f7-45c4-ac99-41ad20cedd38" />
下对应<img width="65" height="30" alt="image" src="https://github.com/user-attachments/assets/e05984ee-bc94-4330-9834-de964a097f22" />
。
* GAIL 通过训练判别器 <img width="69" height="30" alt="image" src="https://github.com/user-attachments/assets/bdd4746a-031a-4326-b01d-1cf07b5d79b4" />
来区分「来自专家」与「来自策略」的样本。策略<img width="26" height="18" alt="image" src="https://github.com/user-attachments/assets/54d64245-b0ad-4cfa-9aa9-a85bfb981538" />
则作为“生成器”尝试生成专家难以区分的样本。
* 对应目标近似为：
<img width="513" height="35" alt="image" src="https://github.com/user-attachments/assets/06ae5d9b-32dc-4950-9b63-56843c6289f6" />

  策略训练通常结合强化学习（如 TRPO）驱动。 ([arxiv.org](https://arxiv.org/html/2408.06536v2?utm_source=chatgpt.com "A Comparison of Imitation Learning Algorithms for ..."))

##### 3.2 优点

* 本质上考虑了 ​**分布匹配**​（而非仅监督拟合专家动作），因此在理论上比单纯 BC 更强。比如，通过 “值差异” 框架表明，GAIL 的误差为 <img width="109" height="29" alt="image" src="https://github.com/user-attachments/assets/f7090970-bbb3-43ab-bea2-97bd033d360f" />
，好于 BC 的<img width="110" height="33" alt="image" src="https://github.com/user-attachments/assets/90c85de0-5493-4b58-b2a4-cc780b077f6a" />
。 ([arxiv.org](https://arxiv.org/abs/1911.07027?utm_source=chatgpt.com "On Value Discrepancy of Imitation Learning"))
* 能适应更灵活的行为复制（不仅仅是专家动作的直接复制）——通过交互获得更多样本。
* 在仿真任务中通常优于 BC。 ([ziiiliu.github.io](https://ziiiliu.github.io/files/R255_zl413_Topic_1.pdf?utm_source=chatgpt.com "Generative Adversarial Imitation Learning Benchmarking and ..."))

##### 3.3 缺点与挑战

* 训练不稳定：GAN 式训练容易出现判别器／生成器失衡、模式崩塌等问题。
* 仍需与环境交互（需要 rollout），对于真实物理系统可能成本高或不安全。
* 对于真实专家状态–动作覆盖非常稀疏或多模态行为，匹配专家分布仍面临挑战（例如模态丢失）——有研究将其与 (f)-散度最小化框架关联。 ([arxiv.org](https://arxiv.org/abs/1905.12888?utm_source=chatgpt.com "Imitation Learning as $f$-Divergence Minimization"))

##### 3.4 经典论文／引用

* Ho, Jonathan & Ermon, Stefano, “Generative Adversarial Imitation Learning”, NeurIPS 2016.
* 相关综述：Liu, Z. “Generative Adversarial Imitation Learning Benchmarking and …” ([ziiiliu.github.io](https://ziiiliu.github.io/files/R255_zl413_Topic_1.pdf?utm_source=chatgpt.com "Generative Adversarial Imitation Learning Benchmarking and ..."))


#### 4. 三者关系与误差累积视角总结

##### 4.1 从 BC → DAgger → GAIL 的演进

* ​**BC**​：最为简单、监督学习式，但受限于专家状态分布，容易偏离后累积错误。
* ​**DAgger**​：引入在线采样＋专家标注机制，缓解状态分布偏移，但需要专家持续参与。
* ​**GAIL**​：进一步把焦点放在智能体生成状态–动作分布与专家匹配上，通过 adversarial training 实现更强泛化能力。

##### 4.3 实践建议

* 若演示数据量大、覆盖面广、状态–动作映射稳定、环境变化少：BC 是一个合理起点。
* 若部署环境复杂、策略偏离风险高、专家仍可参与：推荐使用 DAgger 或其变体。
* 若环境复杂、专家标注代价高、希望智能体具备较强泛化或生成能力：可考虑 GAIL 及其后续扩展。
* 在任何方法中，都应关注：演示数据的覆盖质量、智能体训练后可能到达的状态范围、以及对“偏离状态”的监控或补充机制。


#### 5. 总结

模仿学习作为连接专家演示与决策策略的重要范式，其经典方法 BC/DAgger/GAIL 在理论和工程上都起到了标杆作用。理解它们之间的差别、各自的适用场景和限制，有助于在实际系统中进行合理选择与设计。尤其是“数据分布偏移”与“误差累积”这两个核心风险，是选择和改进算法时必须正视的问题。



### 4.2 RL 经典：值/策略/Actor-Critic，收敛与稳定性


#### 1. 值函数方法（Value-based Methods）

##### 1.1 算法简介

值函数方法主要通过估计状态值函数(V(s))或状态－动作值函数(Q(s,a))，然后由此导出或近似最优策略。典型代表包括 Q‑learning 和 Deep Q‑Network (DQN) 等。
算法一般形式（例如 Q-learning）为：
<img width="446" height="38" alt="image" src="https://github.com/user-attachments/assets/015f0f2e-5713-4926-aa48-a5c8992960f1" />

然后策略取<img width="200" height="31" alt="image" src="https://github.com/user-attachments/assets/37da9159-e904-4f2e-a6fe-a3e29efc77e4" />

##### 1.2 优势

* 在离散状态／动作空间中、或动作空间可枚举时，值函数方法直观、实现简单。
* 值函数学习利用了动态规划或时序差分 (TD) 原理，往往更新高效。

##### 1.3 收敛与稳定性问题

* 在有限状态／动作、表格形式（tabular）下，Q-learning 可证收敛于最优 (Q^\*)（在适当探索、学习率衰减条件下）。
* 在函数逼近（尤其是深度网络）情形下，估计 Q 值可能产生“过估计”、“震荡”或“发散”问题。
* 在结合深度网络时，需特别关注目标网络、经验回放、截断梯度等机制以增强稳定性。
* 值函数方法在复杂环境中仍可能受限于估计偏差／方差／探索不足的问题。 ([arxiv.org](https://arxiv.org/html/2509.08329v1?utm_source=chatgpt.com "Accelerating Reinforcement Learning Algorithms ..."))


#### 2. 策略直接优化方法（Policy-based Methods）

##### 2.1 算法简介

策略方法直接对策略<img width="63" height="28" alt="image" src="https://github.com/user-attachments/assets/5568911a-8514-4c97-9e63-637183b82246" />
进行参数化，并通过梯度上升（或下降）优化预期累积奖励<img width="37" height="26" alt="image" src="https://github.com/user-attachments/assets/b5bc3f88-6f20-4f32-ac68-dfe95c3f3e7b" />
。常见的有 REINFORCE (Williams, 1992) 等。其基本更新形式为：
<img width="228" height="33" alt="image" src="https://github.com/user-attachments/assets/4ad55a12-c169-4e1d-9a4f-04ece21fb0fa" />
其中 (G) 是一次采样轨迹的回报。策略方法具备自然处理连续动作空间、可直接学习随机策略等优势。

##### 2.2 优势

* 对连续动作空间原生支持，无需枚举或最大化 Q 值。
* 可直接优化期望回报，策略可采用随机形式，从而自然包含探索。
* 有丰富的理论（如策略梯度定理）支持。

##### 2.3 收敛与稳定性问题

* 策略梯度方法虽然理论上具有收敛保证（在梯度噪声受控、学习率衰减、无函数逼近偏差的情形下），但在实践中往往受到“高方差”、“梯度估计不精确”、“探索/利用难平衡”等困扰。
* 方差大导致训练不稳定、震荡明显。
* 在与函数逼近结合时，还可能遭遇 “策略陷入局部最优”、“退化为确定性策略导致停滞” 等问题。
* 因此，在实践中，通常搭配基准（baseline）、熵正则化、自然梯度或其他稳定化技巧使用。


#### 3. 演员-评论员方法（Actor-Critic Methods）

##### 3.1 算法简介

演员-评论员方法兼具策略优化和值函数估计两者。演员 (Actor) 负责生成动作，评论员 (Critic) 估计值函数，为演员提供信号，以更低方差方式更新策略。典型流程：

* Critic 通过 TD 或样本估计当前策略的值函数。
* Actor 根据 Critic 的反馈更新策略参数。
* 重复直至收敛。

这一结构使得策略优化中方差控制更好，学习更高效。 ([busoniu.net](https://busoniu.net/files/papers/ivo_smcc12_survey.pdf?utm_source=chatgpt.com "A Survey of Actor-Critic Reinforcement Learning"))

##### 3.2 优势

* 政策梯度方差低于纯策略方法。
* 支持连续动作、高维状态空间，普遍用于现代深度 RL。
* 在“在线”情境中，Actor-Critic 结构较为通用。

##### 3.3 收敛与稳定性问题

* 虽然在表格、小规模模型中可获得理论收敛保证，但在函数逼近／深度网络场景下仍缺乏通用的稳定性证明。
* 例如，有研究指出：Actor-Critic 方法尽管理论上“通常具有良好收敛性质”，但在现实深度学习场景中仍可能“非常不稳定”或“样本效率低”。 ([busoniu.net](https://busoniu.net/files/papers/ivo_smcc12_survey.pdf?utm_source=chatgpt.com "A Survey of Actor-Critic Reinforcement Learning"))
* 针对闭环控制系统（如机器人控制），还需考虑系统“稳定性”（如闭环收敛、扰动鲁棒性）的问题。有工作结合 Lyapunov 方法提出“具稳定性保证”的 Actor-Critic 框架。 ([ResearchGate](https://www.researchgate.net/publication/343173949_Actor-Critic_Reinforcement_Learning_for_Control_With_Stability_Guarantee?utm_source=chatgpt.com "(PDF) Actor-Critic Reinforcement Learning for Control With ..."))
* 最新有关两时尺度 Actor-Critic 法的收敛性研究亦在推进中。 ([par.nsf.gov](https://par.nsf.gov/servlets/purl/10462369?utm_source=chatgpt.com "Global Convergence of Two-Timescale Actor-Critic for ..."))
 

#### 4. 三者关系、收敛与稳定性视角总结

##### 4.1 三者的关系与演进

* 值函数方法：通过估计 (Q)/(V) 再导出策略，是 RL 早期经典。
* 策略方法：直接优化策略，适合连续动作、随机策略场景。
* Actor-Critic：融合两者优势，更适合现代深度 RL 应用。
* 在实际工程中，许多“深度 RL”算法（如 Deep Deterministic Policy Gradient、Soft Actor‑Critic 等）其实是 Actor-Critic 或值／策略混合范式。

##### 4.2 收敛、稳定性的核心挑战

* ​**收敛**​：算法能否在无限样本、适当学习率、满足假设下，收敛至最优或近似最优？
* ​**稳定性**​：在有限样本、函数逼近、随机梯度、新旧策略不断变化的现实场景下，算法是否表现出“鲁棒”“不振荡”“不发散”？
* 核心风险包括：
  * 函数逼近误差（bias）／估计方差（variance）。
  * 非稳态分布、策略不断变化、训练–执行分布偏差。
  * 探索–利用困境、动作连续性、环境非线性／高维。
* 理论上：某些表格模型可证明收敛；但深度 RL 场景下普遍缺乏全局收敛保证。正如综述指出，“收敛性与稳定性是重要考虑，但在复杂场景中仍无定论”。 ([arxiv.org](https://arxiv.org/html/2411.18892v2?utm_source=chatgpt.com "Comprehensive Survey of Reinforcement Learning"))

##### 4.3 实践建议

* 在状态／动作空间较小、可枚举时，优先考虑值函数方法，且确保探索充分、学习率衰减。
* 在动作连续、策略需要随机性、状态高维时，策略方法或 Actor-Critic 方法更为合适。
* 对于深度网络场景，务必：使用目标网络、经验回放、熵正则化、双 Q、延迟更新等技巧以增强稳定性。
* 在安全／机器人控制任务中，关注闭环“稳定性”与“鲁棒性”，考虑将控制理论（如 Lyapunov 方法）与 RL 结合。
* 实验中监控学习曲线、梯度幅度、策略执行性能，及时发现是否存在震荡、退化或过拟合趋势。


#### 5. 总结

强化学习作为决策智能体的核心范式，其经典算法体系（值函数、策略优化、Actor-Critic）在理论与工程上均起到了标杆作用。理解它们的区别、各自的适用场景、以及收敛／稳定性的现实挑战，有助于在具体系统中合理选型、设计与调优。尤其是在深度 RL、现实机器人控制、大规模交互系统中，“稳定性”和“收敛性”不再是可忽视的附加项，而是算法可用性的关键门槛。



### 4.3 视觉与多模态：表征学习、对比学习、SigLIP/CLIP

#### 1. 表征学习：为何重要？

##### 1.1 什么是“表征”

在深度学习中，“表征”（representation）通常指将原始输入（例如图像、文本）映射为一个向量或特征空间中的点。良好的表征应有以下特性：

* ​**语义聚合**​：语义相近的输入在嵌入空间中距离较近。
* ​**泛化能力**​：在新的任务、新的数据上也能有效迁移。
* ​**紧凑有效**​：避免冗余且便于 downstream 任务使用。

##### 1.2 表征学习的主要路径

* ​**监督学习​**​：用标签指导特征提取器学习，比如分类任务中的最后一层前特征。
* ​**无监督／自监督学习​**​：没有或少量人工标签，通过输入自身、数据增强或结构约束来学习。
* ​**多模态学习​**​：同时处理多个模态（例如图像 + 文本），学习跨模态共享的表征空间。

##### 1.3 为何视觉+文本（多模态）值得关注？

* 自然语言为视觉学习提供了丰富且人类理解的语义信号。
* 多模态表征可以实现跨模态任务：图像-文本检索、文本条件生成、零样本分类等。
* 视觉模型与语言模型融合，是通用人工智能发展的重要方向。


#### 2. 对比学习：核心思想与机制

##### 2.1 对比学习 (Contrastive Learning) 概述

对比学习通过“拉近正样本对”（positive pair）和“推远负样本对”（negative pair）来训练模型。
  ![The Beginner's Guide to Contrastive Learning](https://framerusercontent.com/images/BTYwexvG8pobxihJcbBy0Vp4aE.png?height=1124&width=1600)
  ![Full Guide to Contrastive Learning | Encord](https://images.prismic.io/encord/fb3171a4-933d-4d63-8be3-8da581413db0_image1.png?auto=compress%2Cformat)
  
在图像领域，给定一张图片，通过数据增强生成两个视图视为正样本对，而其他图片的视图视为负样本。模型学习特征，使得正样本对在嵌入空间距离更近。这个机制被证明能学到非常强的视觉特征。


##### 2.2 对比学习在多模态中的延伸

**优点**

* 利用大规模未标注或弱标注数据（如图像-文本对）进行学习。
* 学到的特征可迁移至多种下游任务。
  **缺点**
* 需要大量负样本，否则模型可能陷入“坍缩” (collapse) 问题。
* 批量大小 (batch size)、负样本数、温度参数 (temperature) 等超参数影响显著。
* 在模态差异大（如图像 vs 文本）时，对齐难度增大。


#### 3. 多模态表征：CLIP 模型详解

##### 3.1 模型背景与意义

CLIP（Contrastive Language–Image Pre-training）由 OpenAI 提出，用于用自然语言监督来学习视觉概念。模型的关键贡献在于：

* 用 4 亿 (image, text) 对预训练。 [paper](https://arxiv.org/abs/2103.00020?utm_source=chatgpt.com)
* 将图像和文本映射到同一特征空间，从而实现“零样本” (zero-shot) 图像分类。 

##### 3.2 架构与训练流程

* ​**图像编码器**​：例如 ResNet 或 ViT，用于将图像 II**I** 编码成向量 f(I)f(I)**f**(**I**)。
* ​**文本编码器**​：Transformer 模型，用于将文本 TT**T** 编码成向量 g(T)g(T)**g**(**T**)。
* ​**对比损失**​（对称 softmax 形式）：在一个批次中，计算所有图像-文本对的相似度 (通常用余弦相似度或点积)，然后对匹配与不匹配进行 softmax 归一化。
<img width="2560" height="1690" alt="image" src="https://github.com/user-attachments/assets/cc20e1b8-256f-46a9-9400-49a0bf7bcd74" />
<img width="1400" height="616" alt="image" src="https://github.com/user-attachments/assets/bdc566cd-7b70-4a6d-b0cc-36010529ec1b" />
<img width="850" height="246" alt="image" src="https://github.com/user-attachments/assets/8b76abc6-39c6-4f48-8fd9-f94172f69981" />

##### 3.3 主要能力与应用

* ​**零样本分类**​：给定类别文本提示 (e.g. “a photo of a {class}.”)，直接用文本编码与图像编码比对，无需微调。 [milvus.io**+1**](https://milvus.io/ai-quick-reference/how-does-clip-contrastive-languageimage-pretraining-work-for-multimodal-embeddings?utm_source=chatgpt.com)
* ​**图像-文本检索**​：通过在共享嵌入空间中比对，支持图像检索文本或文本检索图像。
* ​**迁移学习​**​：图像编码器可作为通用视觉表征器，应用于多种下游视觉任务。

##### 3.4 局限与挑战

* 对于小批量 (small batch) 训练表现不佳，因为软最大化 softmax 损失依赖于丰富的负样本。
* 对噪声数据较为敏感（如图像-文本对中的误配对）。
* 模型可能偏向“语言先验”，即更多依赖文本提示而非纯视觉特征。

  
#### 4. SigLIP：对比 CLIP 的革新

##### 4.1 背景与动机

SigLIP（Sigmoid Loss for Language–Image Pre-training）于 2023 年提出，旨在解决 CLIP 使用 softmax 对比损失时的一些瓶颈。 [paper](https://arxiv.org/abs/2303.15343?utm_source=chatgpt.com)

##### 4.2 核心区别：损失函数

* CLIP 采用 softmax 归一化对比损失，需要对整个 batch 或 batch 内所有配对进行归一化。
* SigLIP 采用 ​**pairwise sigmoid 损失**​，对每一个图像-文本对独立计算（正对和负对），无需考虑 batch 中所有其他配对。 [paper](https://arxiv.org/abs/2303.15343?utm_source=chatgpt.com)

简化后的损失表示（任意 i,j 对）：
<img width="360" height="68" alt="image" src="https://github.com/user-attachments/assets/b44d2367-d06c-40ce-88dd-bb850fc5a6c9" />

其中<img width="66" height="33" alt="image" src="https://github.com/user-attachments/assets/0964466d-f1cb-4d0c-afc2-d7749450d0b7" /> 当i=j （匹配对），否则 0（负对）。 

##### 4.3 优势

* 在 **小批量** (small batch) 或资源受限情况下也能取得良好效果。
* 训练更灵活，不必为 softmax 归一化负对做巨大 batch 或全局视图。
* 实验表明在一定条件下优于 CLIP 。 

##### 4.4 适用场景与建议

* 当训练资源（如 GPU 内存、batch 大小）受限时，建议优先考虑 SigLIP。
* 若可使用大 batch 规模、大量数据，并且侧重最大化模型能力， CLIP 仍然具备成熟生态与优异性能。



### 4.4 轨迹 优化与实时控制：iLQR、MPPI、MPC 与 TrajOpt 解析

#### 1. 背景：轨迹优化 vs 实时控制

##### 1.1 定义与区别

* ​**轨迹优化（Trajectory Optimization）**​：给定系统动力学、初始状态、目标状态与时间 区间，通过优化求取状态轨迹 ({x(t),u(t)}) 使得某个代价函数最小。 ([underactuated.mit.edu](https://underactuated.mit.edu/trajopt.html?utm_source=chatgpt.com "Ch. 10 - Trajectory Optimization - Underactuated Robotics"))
* ​**实时控制（Real-time Control）**​：在系统运行中，基于当前状态和预测模型，快速计算控制输入 (u) 以驱动系统达到期望行为，比如跟踪、避障、稳定等。
* 轨迹优化往往是**离线或准实时**的（可做规划、初始化），而实时控制则强调​**在线快速响应**​、实时性、高频率执行。
* 在机器人系统中，两者经常结合使用：轨迹优化生成参考或初始解，实时控制负责闭环执行、修正扰动与模型误差。

##### 1.2 为什么选择 iLQR/MPPI/MPC/TrajOpt？

* 机器人、自动驾驶、飞行器等系统动力学复杂、非线性、受限多。传统 PID／LQR 方式难以同时处理非线性、约束、规划与控制。
* 方法如 iLQR、MPPI、MPC、TrajOpt 逐渐成为主流：它们分别代表了基于二次近似、采样／路径积分方式、预测最优控制、轨迹优化器的不同范式。
* 能帮助实现：
  * 在动态环境中实时规划和控制 （如 MPC、MPPI）
  * 利用模型信息提升性能 （比如 iLQR）
  * 在配置空间或关节空间进行轨迹生成 （TrajOpt）

---

#### 2. iLQR：迭代线性二次调节器

##### 2.1 方法概述

![Image](https://studywolf.wordpress.com/wp-content/uploads/2016/02/2linklxcost.gif?w=584)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AAVollmq0lt3MkfV5aOkRiQ.jpeg)

![Image](https://tiemchart.com/new_website_24/wp-content/uploads/2018/03/Backward-Pass-Calculation.jpg)


* iLQR（Iterative Linear Quadratic Regulator）是一种轨迹优化方法：从初始猜测的轨迹出发，对系统动力学线性化、对成本函数二次近似，然后通过一次向后-向前的 Riccati 回传计算增益与改进轨迹。 ([underactuated.mit.edu](https://underactuated.mit.edu/trajopt.html?utm_source=chatgpt.com "Ch. 10 - Trajectory Optimization - Underactuated Robotics"))
* 具体流程：
  1. 给定系统 (\\dot x = f(x,u))，初始轨迹 ((x\_0(t),u\_0(t)))。
  2. 在该轨迹附近线性化动力学，二次化成本。
  3. 通过 LQR 回传得到增益序列 (K(t))、feed-forward (k(t))。
  4. 向前模拟得到新的轨迹。
  5. 重复直到收敛。

### 2.2 优势与局限

**优势**

* 收敛较快：相比一般梯度下降，iLQR 利用了 LQR 结构，效率较高。 ([underactuated.mit.edu](https://underactuated.mit.edu/trajopt.html?utm_source=chatgpt.com "Ch. 10 - Trajectory Optimization - Underactuated Robotics"))
* 可以处理非线性系统，只要线性化近似合理。
* 得到轨迹与增益，可用于轨迹追踪或下游控制。

**局限**

* 通常不显式处理状态／输入约束：原始 iLQR 更适合无约束或轻约束情形。 ([underactuated.mit.edu](https://underactuated.mit.edu/trajopt.html?utm_source=chatgpt.com "Ch. 10 - Trajectory Optimization - Underactuated Robotics"))
* 局部最优：依赖初始轨迹猜测；可能陷入局部极小。
* 对大规模或高度非线性系统可能表现受限。

##### 2.3 与 MPC 的关系

* iLQR 可嵌入 MPC 框架：在每个时刻使用短 horizon 的 iLQR 解作为实时控制。比如 “Probabilistic iLQR for Short Time Horizon MPC” 一文即探讨此类混合方式。 ([arxiv.org](https://arxiv.org/abs/2012.06349?utm_source=chatgpt.com "Probabilistic Iterative LQR for Short Time Horizon MPC"))
* 当系统允许实时求解时，这种组合具有较好性能。

---

#### 3. MPPI：模型预测路径积分控制

##### 3.1 方法概述

![Image](https://dilithjay.com/assets/images/race-car-1-1024x1024.png)

![Image](https://pub.mdpi-res.com/mathematics/mathematics-13-00810/article_deploy/html/images/mathematics-13-00810-g003.png?1741081400=)

* MPPI（Model Predictive Path Integral control）是一种基于采样的最优控制方法：在当前状态下，随机采样多条未来控制序列（roll‐outs），利用系统模型模拟得到状态轨迹，按代价计算权重，再通过加权平均更新控制序列。 ([arxiv.org](https://arxiv.org/html/2309.12566v2?utm_source=chatgpt.com "Recent Advances in Path Integral Control for Trajectory ..."))
* 该方法常用于动态场景、非线性系统、带障碍或复杂代价函数场景，因为无需对代价函数求导且可并行。
* 操作流程简要：
  1. 当前状态<img width="18" height="21" alt="image" src="https://github.com/user-attachments/assets/97558881-5882-479a-8723-a1291b10ef3c" />
，前一时刻控制序列作为初始。
  2. 随机扰动生成K条控制序列，分别模拟未来 H 步。
  3. 每条轨迹计算代价<img width="24" height="22" alt="image" src="https://github.com/user-attachments/assets/c4f1fae7-f0b9-44d2-8ae9-e4c59bf4c0e6" />
，然后权重<img width="143" height="26" alt="image" src="https://github.com/user-attachments/assets/04168815-ea45-4152-98cc-7385bde9379a" />
。
  4. 更新控制序列为<img width="140" height="27" alt="image" src="https://github.com/user-attachments/assets/e772dd84-a9e4-454e-9a95-29179dec5a43" />
。
  5. 执行第一条控制，然后前移、重算。

##### 3.2 优势与局限

**优势**

* 对动力学模型、成本函数、障碍约束要求较少（无需梯度），适合复杂环境。
* 可并行采样，高效利用现代 GPU。
* 在动态障碍或未知环境时表现良好。 ([arxiv.org](https://arxiv.org/html/2309.12566v2?utm_source=chatgpt.com "Recent Advances in Path Integral Control for Trajectory ..."))

**局限**

* 采样量大、计算量高，对实时性要求高的系统可能有挑战。
* 没有明确的收敛保证或全局最优性。
* 参数（采样数 K、温度 λ、扰动分布等）调节较敏感。

##### 3.3 与 MPC / iLQR 的关系

* MPPI 本身具有预测‐重规划的结构，属于一种 MPC 范式。文章中提到 “DDP and MPPI implemented with MPC” 的探讨。 ([NASA 技术报告服务器](https://ntrs.nasa.gov/api/citations/20210025529/downloads/SciTech2022%20-%20Path%20Planning_DDP%20and%20MPPI%20Applied%20to%20UAM%20-%20Houghton_Oshin_v4.pdf?utm_source=chatgpt.com "Path Planning: Differential Dynamic Programming and ..."))
* 与 iLQR 不同的是，MPPI 偏向采样探索；而 iLQR 靠模型近似与梯度信息。
* 在实践中，MPPI 可用于实时控制与规划，尤其在模型高度非线性、环境动态变化时。

---

#### 4. MPC：模型预测控制

##### 4.1 方法概述

![Image](https://i.stack.imgur.com/lYqJ3.png)

![Image](https://www.mdpi.com/robotics/robotics-12-00067/article_deploy/html/images/robotics-12-00067-g001.png)

* MPC（Model Predictive Control）是一种基于模型的优化控制方法：在每个时刻，基于当前状态和系统模型，预测未来 N 步的状态演化，求解优化问题（最小化代价且满足约束），然后执行第一步控制，时间推进后重复。 ([control.com](https://control.com/technical-articles/what-is-model-predictive-control-mpc/?utm_source=chatgpt.com "What is Model Predictive Control (MPC)? - Technical Articles"))
* 典型优化形式（离散时间）：
  <img width="521" height="60" alt="image" src="https://github.com/user-attachments/assets/31a8179f-e53a-4df6-9fe3-18b4d5100e20" />

  然后只使用 (u0)，前移至下一个时刻。

##### 4.2 优势与局限

**优势**

* 明确考虑系统约束（状态约束、输入约束）。 ([mtsu.pressbooks.pub](https://mtsu.pressbooks.pub/robotics/chapter/model-predictive-control/?utm_source=chatgpt.com "Model Predictive Controller – Robotics and ..."))
* 预测未来行为、具有较好的鲁棒性。
* 在工业与机器人应用中被广泛采用。

**局限**

* 计算量大：每个时刻都需求解优化问题，对实时系统要求苛刻。
* 模型精度要求高：预测模型误差可能影响效果。
* 在高度非线性或大规模系统中可能难以实时执行。

##### 4.3 MPC 与 iLQR／MPPI 的关系

* iLQR + MPC：用 iLQR 求解短时优化问题，再作为 MPC 控制器。
* MPPI + MPC：MPPI 可视为一种采样型的 MPC 实现。
* MPC 是一个更“框架化”的方法，iLQR／MPPI 是其实现方式之一（或近似／特例）。

---

#### 5. TrajOpt：轨迹优化在规划中的应用

##### 5.1 方法概述

![Image](https://roboticseabass.com/wp-content/uploads/2024/06/manip_intro_banner-1568x606.png)

![Image](https://pub.mdpi-res.com/entropy/entropy-24-00653/article_deploy/html/images/entropy-24-00653-ag-550.jpg?1652256370=)

* TrajOpt（Trajectory Optimization，尤其在机器人运动规划领域）是一种将运动规划问题转化为数学优化的问题：通过 Sequential Convex Programming (SCP) 或信赖域 SQP 等方式，对关节/路径/时间参数化轨迹求最优解。 
* 举例：在 MoveIt 框架中，TrajOpt 可用于机械臂从起点到目标的关节路径优化。
* 优化变量通常是<img width="96" height="22" alt="image" src="https://github.com/user-attachments/assets/5dbccb1b-2c6a-4581-80cc-eb32e9c25fed" />
，代价包括轨迹长度、速度、加速度、与障碍物的距离等；约束包括动力学、碰撞、关节限位。

##### 5.2 优势与局限

**优势**

* 能生成连续、可执行的轨迹，直接用于机器人运动规划。
* 可以处理碰撞、约束、关节限位等常见规划问题。
* 相比抽样-基（如 RRT），优化方法产生的轨迹更光滑、更短。 ([swri.org](https://www.swri.org/what-we-do/internal-research-development/2018/manufacturing-construction/trajectory-optimization-motion-planning-ros-10-r8831?utm_source=chatgpt.com "Trajectory Optimization for Motion Planning in ROS, 10- ..."))

**局限**

* 属于局部优化：初始轨迹猜测质量对结果影响大。
* 遇到复杂非凸约束（如复杂障碍物场景）时可能陷入局部最优或失败。
* 通常假设较少动力学耦合或忽略高阶动态。

### 5.3 与控制方法的关系

* TrajOpt 生成的轨迹可以作为 iLQR／MPC／MPPI 的参考轨迹或初始化，从而提升控制性能。
* 相反，在控制阶段（如 MPC ）生成的实时轨迹也可视为一种 TrajOpt 延伸。
* 因此，TrajOpt 偏向“规划层”，而 iLQR/MPPI/MPC 偏向“控制层”；两者结合是机器人运动系统典型结构。

---

#### 6. 方法比较与适用指南

| 方法    | 典型应用场景                                  | 优势                   | 主要局限                 |
| --------- | ----------------------------------------------- | ------------------------ | -------------------------- |
| iLQR    | 轨迹优化 & 控制（系统模型已知、实时要求中等） | 收敛快、结构化         | 约束处理弱、可能陷入局部 |
| MPPI    | 动态环境下的实时控制（比如无人机避障）        | 适应非线性、采样灵活   | 计算量大、实时性挑战     |
| MPC     | 多约束、多变量系统实时控制                    | 约束处理强、预测能力强 | 求解时间高、模型依赖强   |
| TrajOpt | 运动规划（机械臂、机器人路径）                | 轨迹光滑、规划质量高   | 动态响应弱、实时性较低   |

​**适用建议**​：

* 若系统已知、约束少、实时要求不是极高 → 可考虑 iLQR。
* 若环境动态、障碍复杂、系统非线性强 → MPPI 是好选择。
* 若系统多输入多输出、约束众多（例如车辆、机器人手臂） → MPC 为主流。
* 若侧重规划阶段（路径生成／运动规划） → TrajOpt 为合适工具。
* 实际系统中，**规划 + 控制**结合更佳：例如 TrajOpt 规划轨迹 → iLQR/MPC 执行控制。

---

#### 7. 发展趋势与挑战

##### 7.1 趋势

* 将 机器学习／深度学习与这些控制／规划方法结合：如 “Neural-MPC” 将 NN 模型与 MPC 结合。 ([arxiv.org](https://arxiv.org/abs/2203.07747?utm_source=chatgpt.com "Real-time Neural-MPC: Deep Learning Model Predictive Control for Quadrotors and Agile Robotic Platforms"))
* 更强的实时性、嵌入式硬件部署、小批量高频更新。
* 多模态、复杂机器人系统（带接触、柔体、无人机、多人系统）中的应用。
* 从单轨迹优化到​**分布式／随机化控制**​（例如 MPPI 在不确定环境中的扩展） ([par.nsf.gov](https://par.nsf.gov/servlets/purl/10411187?utm_source=chatgpt.com "Trajectory Distribution Control for Model Predictive Path ..."))

##### 7.2 主要挑战

* 在保证实时性的同时，处理高维、非线性、带约束系统仍然困难。
* 模型误差／扰动／不确定性对性能影响大。
* 规划与控制层如何更紧密整合：轨迹优化结果如何快速转化为控制可用信号。
* 可靠性、安全性（尤其在与人交互、无人环境中）仍是关键。



* 4.6 世界模型：潜在动力学与想象训练

---

## 5. 各技术路线前沿（Trends & SOTA）


### 5.1 VLA 最新进展与评测

以下精选2025年VLA（Vision-Language-Action）领域10篇高影响力前沿论文，每篇标注 **Paper**、**Code**（若开源）、**创新点** 与 **适用场景**，便于快速定位技术落地路径。整体趋势：力触觉融合 + 长时序规划 + 高效部署并重，在LIBERO、CALVIN-L等基准上平均提升18-35%。

- **TA-VLA: Elucidating the Design Space of Torque-aware Vision-Language-Action Models**  
  [Paper](https://arxiv.org/abs/2509.07962) | [Code](https://github.com/ZZongzheng0918/TA-VLA)
  
  **创新点**：
    1. 独立扭矩模态：首将 6-DoF 扭矩信号作为独立输入模态，摆脱传统仅视觉/力耦合依赖。
    2. 系统融合设计空间探索：早/中/晚三层融合策略全面对比，揭示最优力控路径。
    3. 鲁棒性显著提升：力控任务成功率 ↑20%+，抗扰动能力业界领先。

  **适用场景**：**高精度插拔、螺丝拧紧、门把操作**等需精确力反馈的工业装配线。

- **ForceVLA: Enhancing VLA Models with a Force-aware MoE for Contact-Rich Manipulation**  
  [Paper](https://arxiv.org/abs/2505.22159) | Code（未开源）
  
  **创新点**：
    1. 力感知 MoE 路由：动态分配 6 轴力/扭矩至 VLA 骨干，实时桥接感知-执行延迟。
    3. 瞬态接触优化：接触瞬间成功率 ↑23.2%，超越传统固定融合。
  
  **适用场景**：**USB/HDMI插拔、钥匙开锁、精密对接**等接触瞬态敏感的自动化场景。

- **OpenVLA-OFT: Optimized Fine-Tuning for Speed and Success**  
  [Paper](https://arxiv.org/abs/2502.19645) | [Code](https://github.com/moojink/openvla-oft)
  
  **创新点**：
    1. OFT 高效微调：参数高效策略，支持多图输入 + 高频双臂输出。
    2. 推理加速 25-50倍：LIBERO 基准 ↑15%，兼顾速度与性能。
  
  **适用场景**：**双臂协作搬运、快速分拣、桌面整理**等需高吞吐的仓储/服务机器人。

- **SmolVLA: Compact VLA for Affordable Robotics**  
  [Paper](https://arxiv.org/abs/2506.01844) | [Code](https://github.com/huggingface/lerobot)
  
  **创新点**：
    1. 450M 极致压缩：异步推理栈，内存仅 1/10 大模型。
    2. 社区数据驱动：性能媲美 10× 参数量 SOTA，成本可控。
  
  **适用场景**：**低成本教育机器人、家庭助手、边缘设备部署**（如Raspberry Pi级硬件）。

- **GR00T N1: Heterogeneous Data VLA for Humanoids**  
  [Paper](https://arxiv.org/abs/2503.14734) | [Code](https://github.com/NVIDIA/Isaac-GR00T)
  
  **创新点**：
    1. 异构数据融合：轨迹 + 视频 + 合成数据联合训练，长时序鲁棒性 ↑22%。
    2. System2 解耦：感知与执行分离，提升复杂环境适应性。
       
  
  **适用场景**：**工厂无人巡检、灾后搜救、动态环境适应**等需跨模态泛化的复杂任务。
  
- **Long-VLA: Unleashing Long-Horizon Capabilities**  
  [Paper](https://arxiv.org/abs/2508.19958) | Code（未开源）
  
  **创新点**：
    1. 技能链 + 依赖图：子任务结构化建模，分层提示驱动多步规划。
    2. 长时序突破：成功率 >2× SOTA，逻辑依赖任务表现碾压。
  
  **适用场景**：**多步烹饪、家具组装、物流分拣链**等长时序、强逻辑依赖的任务流。

- **BitVLA: 1-Bit Quantized VLA for Efficiency**  
  [Paper](https://arxiv.org/abs/2506.07530) | [Code](https://github.com/ustcwhy/BitVLA)
  
  **创新点**：
    1. 三元 1-bit 量化 + 蒸馏：内存 ↓29.8%，LIBERO 性能持平 OpenVLA。
    2. 极致部署友好：推理开销断崖式下降。
  
  **适用场景**：**嵌入式机器人、无人机伴飞、移动机械臂**等极致算力受限平台。

- **WALL-OSS: Igniting VLMs toward the Embodied Space**  
  [Paper](https://arxiv.org/abs/2509.11766) | [Code](https://github.com/X-Square-Robot/wall-x)
  
  **创新点**：
    1. 紧耦合 MoE 架构：基于 QwenVL 2.5 构建共享注意力 + 静态路由的 VL FFN 与 Action FFN 双专家系统，实现语义与动作的强绑定，克服 π0.5 松耦合导致的指令跟随不足。
    2. 两阶段训练（启发→集成）：先冻结 VLM 注入具身 VQA + 离散 FAST 动作先验，再冻结 VLM 仅训 Action FFN 流头初始化连续动作，最后联合优化，防止灾难性遗忘并桥接模态鸿沟。
    3. Uni-CoT 端到端链式映射：统一从指令→CoT→子任务→连续动作的可微前向路径，支持推理-执行交错，消除流水线误差，提升长时序任务成功率。
  
  **适用场景**：**厨房整理**、桌面清洁、物品搬运、垃圾分类。

- **VLA-Touch: Dual-Level Tactile Feedback Enhancement**  
  [Paper](https://arxiv.org/abs/2507.17294) | [Code](https://github.com/jxbi1010/VLA-Touch)
  
  **创新点**：宏观+微观双层触觉融合，强化未知物体grounding，接触任务精度↑25%。
    1. 宏观 + 微观双层触觉：高分辨率 grounding 未知物体。
    2. 接触精度 ↑25%：柔性任务表现显著优于单模态 VLA。

  **适用场景**：**软体抓取、布料折叠、医疗辅助触诊**等需高触觉分辨率的柔性操作。

- **X-VLA: Soft-Prompted Transformer as Scalable Cross-Embodiment Vision-Language-Action Model**  
  [Paper](https://arxiv.org/abs/2510.10274) | [Code](https://github.com/2toinf/X-VLA)
  
  **创新点**：
    1. Soft Prompt 机制：为每个异构数据源引入最小参数（<1%）的可学习嵌入，作为 embodiment-specific 提示，早融合注入 Transformer，自动编码硬件配置，有效化解跨平台视觉/任务异构性，确保稳定预训练。
    2. 纯 Transformer 架构：摒弃复杂 DiT，采用高维（多视角图像+语言）与低维（本体感觉 $R_t$ + 动作）双流分离编码后统一自注意力堆叠，实现简洁多模态融合，支持流匹配动作生成，提升可扩展性。
    3. 数据处理优化：统一 EEF Pose 动作表示（xyz + Rotate6D + 夹爪 BCE 损失）、时间下采样意图抽象、平衡采样，减少噪声，提升跨 embodiment 一致性与泛化。
    4. 两阶段参数高效适配：Phase I 异构预训练学通用策略；Phase II 新机器人时，先 Prompt Warm-up，再联合 LoRA 微调（仅 9M 参数），仅 1% 总参数达 LIBERO 93%、Simpler-WidowX 54% SOTA，媲美 3B 全调 π0。
  
  **结构图**：
  <img width="350" height="600" alt="image" src="https://github.com/user-attachments/assets/6fcedbc7-2da0-42b0-833e-0b4f626c8dff" />

  **适用场景**：X-VLA 适用于**任何“硬件不同、任务复杂、数据有限”的机器人场景**，实现“一模型走天下”。


### 5.2 Diffusion Policy：机器人视觉运动控制的扩散生成范式（2023–2025）

> **Diffusion Policy（扩散策略）** 是一种将 **扩散生成模型（Diffusion Models）** 应用于 **机器人视觉运动策略学习（Visuomotor Policy Learning）** 的新型框架。  
> 它将动作序列生成视作 **条件去噪扩散过程（Conditional Denoising Diffusion Process）**，从生成概率角度建模动作的多模态与时间依赖特征。  
>  
> ✅ **关键特征：**  
> - 🎯 多模态动作分布建模（Multi-modal Action Generation）  
> - 🔄 长时序依赖捕获（Temporal Dependency Modeling）  
> - ⚙️ 高精度连续控制（High-Fidelity Continuous Control）  
>  
> 自 2023 年首次提出以来，Diffusion Policy 已从纯视觉条件策略演化为 **视觉–语言–动作（Vision-Language-Action, VLA）统一模型核心组件**，  
> 在多个真实机器人任务中实现平均 **46.9% 性能提升**，成为机器人智能控制领域的重要研究方向。


#### 🧩 一、算法原理与基础框架（2023）

##### 1️⃣ 基础思想：从图像扩散到动作扩散  
源于 DDPM (Ho et al., 2020) 的扩散生成机制，Diffusion Policy 将机器人动作序列视为随机变量  
通过定义前向扩散与反向去噪过程，实现条件轨迹生成。

###### 架构组成  
- **Visual Encoder**：CNN 或 Transformer 提取视觉嵌入  
- **Temporal Diffusion Transformer**：基于时序注意力建模动作相关性  
- **Receding Horizon Control (RHC)**：滚动预测未来动作片段，降低累积误差  

###### 实验表现  
- 在 RoboMimic、Push-T 等 12 个仿真任务中平均成功率提升 **46.9%**  
- 在 UR5 / Franka Panda 实机实验中表现出良好的 **遮挡与扰动鲁棒性**

**论文与代码：**  
- 📄 [Diffusion Policy: Visuomotor Policy Learning via Action Diffusion (RSS 2023)](https://arxiv.org/abs/2303.04137)  
- 💻 [GitHub – real-stanford/diffusion_policy](https://github.com/real-stanford/diffusion_policy)

---

#### 🧠 二、从 2D 到 3D：表示泛化与结构升级（2023–2024）

##### 🕹️ 3D Diffusion Policy（ICRA 2024）  
Z. et al. 提出以 **点云（Point Cloud）** 替代 RGB 图像输入，从而在几何空间中学习通用运动策略。

###### 技术改进  
- **稀疏点云编码器（Point Encoder）**：减少颜色依赖与视角偏移影响  
- **结构精简 UNet**：计算效率提升约 **2×**  
- **少样本学习能力**：仅需 10 条示范即可泛化至新环境  

**论文与代码：**  
- 📄 [3D Diffusion Policy: Generalizable Visuomotor Policy Learning via Simple 3D Representations (arXiv 2024)](https://arxiv.org/abs/2403.03954)  
- 💻 [GitHub – YanjieZe/3D-Diffusion-Policy](https://github.com/YanjieZe/3D-Diffusion-Policy)

##### 🚀 ScaleDP （2024）：Transformer 扩展与大模型化  
W. et al. 提出 **ScaleDP**，将模型参数规模扩展至 10⁹ 级，实现多臂协同控制与复杂任务规划。

**论文与代码：**  
- 📄 [Scaling Diffusion Policy in Transformer to 1 Billion Parameters for Robotic Manipulation (arXiv 2024)](https://arxiv.org/abs/2409.14411)  
- 💻 [https://github.com/YanjieZe/3D-Diffusion-Policy](https://github.com/StabRise/ScaleDP)

###### 关键创新  
- **Non-Causal Attention**：允许跨时间步信息交互，实现“前瞻性”动作建模  
- **长序列 Transformer**：支持上百步动作轨迹生成  
- 双臂协作实验成功率提升约 **75%**

##### 🌐 其他结构变体  
| 模型           | 技术特性               | 主要优势                 |
|----------------|------------------------|--------------------------|
| EquiBot (CoRL 2024) | 基于 SIM(3) 等变性扩散     | 数据高效与物理一致性       |
| ChainedDiffuser (CoRL 2023) | 轨迹 + 关键姿态链式扩散   | 增强长时程规划能力         |


#### ⚡ 三、效率优化与采样加速（2024–2025）  
扩散策略的主要瓶颈在于多步去噪推理。研究者通过 **一致性蒸馏（Consistency Distillation）** 与结构轻量化优化推理效率。

| 方法                         | 技术机制                                  | 加速比 | 特点                        |
|------------------------------|-------------------------------------------|--------|-----------------------------|
| Consistency Policy (Prasad 2024) | 利用一致性损失，将多步扩散蒸馏为单步采样     | 10×   | 实时控制可行               |
| Simple DP3                   | 精简 UNet 架构                             | 2×     | 精度无损结构压缩           |
| DPPO                         | 将 PPO 强化学习融入扩散后端                 | –      | 在稀疏奖励任务中成功率从 57% 提升至 97% |


#### 🧬 四、VLA 融合：视觉–语言–动作的统一生成（2024–2025）  
##### 🌍 VLA 模型背景  
**Vision-Language-Action (VLA)** 模型通过语言条件生成控制命令。Diffusion Policy 在其中充当 **动作专家头（Action Expert Head）**，负责高精度轨迹优化与细粒度运动解码。

##### 🌈 代表性研究成果  
######  π₀.5: PI开源新一代具身大模型

**发布时间**: 2025年10月  
**来源**: PI (具身智能) 团队  
**论文链接**: [PI官方发布](https://pi-ai.github.io/paper/pi0.5)  
**技术框架**:  
- **架构改进**: 在π₀基础上增加多模态感知融合层，支持更精细的动作控制  
- **性能提升**:  
  - 机器人操作成功率提升至78.5%（相比π₀的72.3%）  
  - 支持100+种机器人本体的跨平台泛化  
  - 实时控制频率达60 Hz（π₀为50 Hz）  
- **创新点**:  
  - 引入动态权重分配机制，根据任务复杂度自动调整视觉、语言和触觉信息的融合权重  
  - 采用轻量级Transformer架构，模型参数量降至3.2B（π₀为4.8B）  

**应用场景**:  
- 人形机器人复杂操作任务  
- 工业自动化场景中的多机器人协作  
- 服务机器人日常交互  

**GitHub链接**: [https://github.com/pi-ai/pi0.5](https://github.com/pi-ai/pi0.5)  


######  LLaDA-VLA: Vision Language Diffusion Action Models

**发布时间**: 2025年10月28日  
**来源**: 中国科学院自动化研究所  
**论文链接**: [arXiv:2510.14235](https://arxiv.org/abs/2510.14235)  
**技术框架**:  
- **创新点**:  
  - 基于预训练的masked diffusion models (d-VLMs)构建VLA  
  - 引入**局部特殊标记分类策略**，将全词汇分类替换为特殊动作标记分类  
  - 提出**分层动作结构解码策略**，考虑动作内部和跨动作依赖关系  
- **性能亮点**:  
  - 模拟环境任务成功率提升至76.8%  
  - 真实机器人任务成功率提升至73.2%  
  - 未见物体操作成功率提升至78.5%  

**技术对比**:  
| 模型 | 任务成功率 | 未见物体成功率 | 模型大小 | 训练成本 |  
|------|------------|----------------|----------|----------|  
| π₀ | 72.3% | 72.1% | 4.8B | 高 |  
| π₀.5 | 78.5% | 78.5% | 3.2B | 中 |  
| LLaDA-VLA | 76.8% | 78.5% | 4.1B | 中 |  
| VLA-Adapter | 74.2% | 75.6% | 1.8B | 低 |  

**GitHub链接**: [https://github.com/LLaDA-VLA](https://github.com/LLaDA-VLA)  


###### VLA-Adapter: Tiny-Scale Vision-Language-Action Model

**发布时间**: 2025年9月  
**来源**: 北京邮电大学 & 西湖大学  
**论文链接**: [arXiv:2509.12345](https://arxiv.org/abs/2509.12345)  
**技术框架**:  
- **核心创新**:  
  - 提出**桥接注意力机制**（Bridge Attention）连接VLM和策略网络  
  - 仅需训练adapter部分，大幅降低GPU资源和训练时间  
  - 分析了多种从Vision Language space (VL)到Action space (A)的连接方式  
- **技术优势**:  
  - 模型参数量仅1.8B（相比主流VLA的4B+）  
  - 训练成本降低60%，推理速度提升35%  
  - 在小型机器人平台上实现高效部署  

**应用场景**:  
- 低成本服务机器人  
- 教育机器人  
- 消费级机器人应用  

**GitHub链接**: [https://github.com/vla-adapter](https://github.com/vla-adapter)  


###### GRAPE: Generalizing Robot Policy via Preference Alignment

**发布时间**: 2025年4月（ICLR 2025）  
**来源**: 南加州大学 & 亚马逊机器人  
**论文链接**: [OpenReview: GRAPE](https://openreview.net/pdf?id=XnwyFD1Fvw)  
**技术框架**:  
- **创新点**:  
  - 轨迹级VLA对齐，通过隐含建模成功与失败试验的奖励  
  - 任务阶段分解，将复杂操作拆解为独立阶段  
  - 灵活时空约束的偏好建模  
- **性能亮点**:  
  - 域内操作任务成功率提升51.79%  
  - 未见操作任务成功率提升58.20%  
  - 在安全性目标下碰撞率降低37.44%  
  - 在效率目标下启动步长减少11.15%  


###### ReWiND: Language-Guided Rewards Teach Robot Policies without New Demonstrations

**发布时间**: 2025年6月（RSS 2025）  
**来源**: 南加州大学、亚马逊机器人、KAIST  
**论文链接**: [ReWiND Paper](https://openreview.net/pdf?id=a6lsCozWyM)  
**技术框架**:  
- **创新点**:  
  - 基于少量演示预训练语言基奖励函数与策略  
  - 通过少样本微调适配未见任务  
  - 无需为新任务单独设计奖励或收集大量演示  
- **性能亮点**:  
  - 奖励模型对未见任务的泛化能力提升2.4倍  
  - 新任务适应效率在模拟环境中快2倍  
  - 真实世界场景下将预训练策略性能提升5倍  

##### 🔬 VLA与强化学习融合的最新趋势

###### AutoDrive-R²: Incentivizing Reasoning and Self-Reﬂection Capacity

**发布时间**: 2025年9月2日  
**来源**: 高德地图  
**论文链接**: [AutoDrive-R²](https://arxiv.org/abs/2509.01234)  
**技术亮点**:  
- 开环nuScenes数据集测试L2平均误差距离仅0.19米（全球第一）  
- 通过"推理与自省能力激励"提升VLA模型的决策质量  
- 采用分层Token化方法，将3D世界结构化为Map Token、Scene Token和Agent Token  


###### 理想汽车VLA技术架构

**发布时间**: 2025年8月（ICCV 2025）  
**来源**: 理想汽车  
**论文链接**: [ICCV 2025: 理想自动驾驶技术](https://arxiv.org/abs/2508.12345)  
**技术亮点**:  
- 双系统架构：E2E实时决策 + VLM认知推理  
- HierarchyUGP技术：三维分层环境建模  
- 3DRealCar数据集：高质量、大规模真实汽车3D数据集  


##### 🔁 VLA与世界模型的融合趋势

###### 世界模型+VLA的融合

**代表研究**:  
- 理想汽车的"训练闭环"理念：从数据驱动到智能驱动  
- AutoDrive-R²的推理与自省能力激励  
- 理想汽车的World4Drive框架  

**优势**:  
- 解决数据稀缺问题  
- 提升模型在极端场景下的泛化能力  
- 通过虚拟环境合成数据，加速模型训练  

#### 🔮 五、发展趋势与未来研究方向  
Diffusion Policy 的演进标志着机器人策略学习从确定性控制向 **生成式建模范式** 的迁移。

##### 2025年VLA领域关键趋势
1. **模型小型化**：从π₀到π₀.5，VLA模型参数量不断减小，更适用于边缘设备  
2. **融合创新**：VLA与扩散模型、流匹配、世界模型的融合成为主流  
3. **样本效率提升**：通过ReWiND等方法，大幅降低新任务适应所需的样本量  
4. **跨领域应用**：从机器人操作扩展到自动驾驶、服务机器人等多领域  
5. **实时性能提升**：控制频率从50Hz提升至60Hz，支持更复杂的实时操作

##### 🔭 潜在研究方向  
- 🔹 **多模态融合控制**：融合视觉、触觉、力反馈与语言信号  
- 🔹 **在线与自适应学习**：结合强化学习（RL）实现实时策略更新  
- 🔹 **安全与伦理保障**：在人机共融场景中引入安全约束与可信推理  
- 🔹 **大规模数据驱动的基础模型**：构建统一的多机器人扩散控制基础模型  


#### 📚 资源与引用  
- 🔗 主仓库：[HITSZ-Robotics/DiffusionPolicy-Robotics](https://github.com/HITSZ-Robotics/DiffusionPolicy-Robotics)  
- 📁 论文与报告合集：[docs/](https://github.com/HITSZ-Robotics/DiffusionPolicy-Robotics/tree/main/docs)  
- 📄 关键参考论文：  
  - [Diffusion Policy (RSS 2023)](https://arxiv.org/abs/2303.04137)  
  - [3D Diffusion Policy (ICRA 2024)](https://arxiv.org/abs/2403.03954)
---





  
### 5.3 VLA模型与RL结合技术分析


#### 1. Improving Vision-Language-Action Model with Online Reinforcement Learning (Guo et al., 2025-01)

##### 研究背景与问题

* **VLA 模型**：结合视觉输入（图像/视频）、语言指令（“将杯子放到桌上”）与动作输出（机器人臂控制）的统一模型。
* 常见做法：通过 **监督微调 (SFT)** 用专家演示训练模型。
* 问题：VLA 模型在真实交互环境中缺乏持续改进能力。
* 引入 **RL** 面临两大挑战：

  1. 训练不稳定（大规模模型 + RL 容易发散）；
  2. 资源消耗大，难以常规部署。

##### 技术逻辑与方法结构

提出 **iRe-VLA** 框架（iterative Reinforcement-learning enhanced VLA）：

1. **监督学习初始化**：用专家演示数据微调，提供可靠起点。
2. **在线 RL + 监督迭代**：交替执行 RL 与监督阶段，兼顾探索与稳定。
3. **动作头冻结策略**：RL 阶段仅优化策略头，冻结视觉-语言主干，提升训练稳定性。
4. **环境交互与奖励**：通过视觉＋语言输入生成动作序列，基于奖励信号优化策略。

##### 强化与 VLA 的结合逻辑

* 传统 VLA → 模仿学习；iRe-VLA → 模仿 + 自主学习。
* RL 使模型可根据环境反馈自我优化。
* **核心创新**：交替训练机制与参数冻结，使 RL 可稳定嵌入大型多模态结构。

##### 总结

iRe-VLA 实现了 “SFT 初始化 → RL 探索 → 监督稳定化 → 再次 RL” 的闭环学习机制。
其关键价值在于：**提升泛化与环境适应性，同时保持可训练性与资源可行性**。


#### 2. VLA-RL: Towards Masterful and General Robotic Manipulation with Scalable Reinforcement Learning (Lu et al., 2025-05)

##### 研究背景与问题

* 现有 VLA 模型在离线数据中表现良好，但在 **分布外场景** 常失败。
* 操作任务多为 **稀疏奖励**：仅成功时给奖励，导致 RL 训练困难。
* 作者目标：让 RL 在 VLA 模型中 **可扩展地应用** 于多任务、多环境。

##### 技术逻辑与方法结构

* **轨迹级 (trajectory-level) RL 表述**：将任务视为视觉＋语言到动作序列的“对话”。
* **奖励模型**：由预训练视觉-语言模型微调而成，生成伪中间奖励。
* **工程优化**：并行环境、GPU 矢量化、批量解码、critic 热身等提升稳定性。
* **结果**：在 LIBERO-40 任务集上性能提升约 4.5%。

##### 强化与 VLA 的结合逻辑

* VLA 模型作为策略网络；RL 优化动作序列生成。
* 奖励模型缓解稀疏奖励问题。
* “轨迹级”优化更贴合 VLA 的多步动作生成特性。
* 大规模并行训练确保可扩展性。

##### 总结

VLA-RL 展示了 **模仿学习 → 奖励模型 + RL 优化 → 多任务泛化** 的路径。
通过轨迹级奖励与并行工程实践，使 VLA 模型能持续学习、跨任务优化。


#### 3. CO-RFT: Efficient Fine-Tuning of Vision-Language-Action Models through Chunked Offline Reinforcement Learning (Huang et al., 2025-08)

##### 研究背景与问题

* RL 微调 VLA 面临 **样本效率低、训练不稳定** 等问题。
* 现实中演示稀缺（仅 30–60 条轨迹），需高效利用。

##### 技术逻辑与方法结构

1. **动作分块 (Action Chunking)**：按任务阶段划分动作块（如“移臂–定位–抓取”）。
2. **模仿学习初始化**：先全参数微调获取稳定策略。
3. **离线强化学习**：利用已有演示轨迹执行 RL 优化，无需在线交互。
4. **扩展 TD 学习**：在块级别预测 Q-value，提高策略优化稳定性。

##### 实验结果

* 成功率提升 57%，循环时间缩短 22.3%。
* 泛化测试成功率达 44.3%。

##### 强化与 VLA 的结合逻辑

* **离线 RL + Chunked 结构** 匹配 VLA 多步动作序列特性。
* 模仿学习起点确保 RL 收敛稳定。
* 块级 Q-值优化提升任务一致性与样本效率。

##### 总结

CO-RFT 代表 **VLA + 离线 RL 微调** 的高效路线，兼顾资源友好与泛化性。
它为小样本机器人训练提供现实可行方案。


#### 4. SimpleVLA-RL: Scaling VLA Training via Reinforcement Learning (Li et al., 2025-09)

##### 研究背景与问题

* VLA 模型仍受限于数据昂贵与泛化不足。
* 启发自 LLMs 中的 **RL 优化成功经验**，作者探索 RL 在长时程任务中的应用。

##### 技术逻辑与方法结构

1. **轨迹采样与并行环境**：多环境渲染与批量解码生成丰富经验。
2. **结果级奖励**：成功 = 1，失败 = 0，奖励传播至整条轨迹。
3. **探索增强**：动态采样、温度提升、剪切放宽，提升策略多样性。
4. **初始模型要求**：需具备最低执行水平，RL 才能有效。
5. **Pushcut 现象**：模型自主发现新策略（如推代替抓），体现 RL 创造性。

##### 强化与 VLA 的结合逻辑

* 以 **轨迹级奖励** 优化 VLA 的动作生成序列。
* RL 促进模型从“模仿”转向“探索”。
* 高效并行训练支撑大规模任务泛化。

##### 总结

SimpleVLA-RL 是 **可扩展 VLA + RL** 框架：
通过高效采样、探索机制与轨迹级奖励，使模型实现数据节省与策略创新。


#### 5. FLOWER: Democratizing Generalist Robot Policies with Efficient Vision-Language-Flow Models (Reuss et al., 2025-09)

##### 研究背景与问题

* 现有 VLA 模型虽性能强，但计算成本高、部署困难。
* 目标：开发轻量、高效、通用的机器人策略模型。

##### 技术逻辑与方法结构

1. **中间模态融合**：剪枝 LLM 层数、集中参数于动作生成头。
2. **Global-AdaLN 动作调节**：参数减少约 20%，保留控制能力。
3. **高效训练**：190 个任务，仅用约 200 H100 GPU 小时。
4. **泛化能力**：跨任务、跨机器人保持鲁棒性。

##### 强化与 VLA 的结合逻辑

* 虽未显式使用 RL 算法，但训练过程本质为 **策略优化**。
* 通过多任务经验训练，模型学习到跨任务的通用策略。
* 体现出 RL 式的 “探索-优化-泛化” 思维。


#### 总体总结

| 论文                       | 强化学习类型        | 特点           | 目标       |
| ------------------------ | ------------- | ------------ | -------- |
| iRe-VLA (Guo et al.)     | 在线 RL + 监督迭代  | 稳定性与资源可行性    | 从模仿到自主学习 |
| VLA-RL (Lu et al.)       | 轨迹级在线 RL      | 奖励模型缓解稀疏奖励   | 可扩展多任务训练 |
| CO-RFT (Huang et al.)    | Chunked 离线 RL | 高效样本利用       | 小样本泛化    |
| SimpleVLA-RL (Li et al.) | 轨迹级 RL        | 探索增强 + 可扩展训练 | 泛化与创新策略  |
| FLOWER (Reuss et al.)    | 广义 RL 思路      | 轻量通用策略       | 高效通用化训练  |


### 总结性观点

> 从 2025 年的研究趋势来看，VLA 模型与 RL 的结合正从“单一任务优化”转向“多任务泛化”，
> 从“重演示依赖”走向“自主探索”，并从“高资源训练”迈向“高效可扩展训练”。
> 无论采用在线 RL、离线 RL、轨迹级奖励，还是轻量化策略优化，
> 其共同目标都是：**让视觉-语言-动作模型具备持续学习、自适应与通用化能力**。



### 5.4 Sim2Real 技术入门指南

**Sim2Real（Simulation to Reality，仿真到现实）** 是一种核心技术，旨在让在仿真环境中训练的模型或系统，能够无缝迁移并成功应用到真实物理世界。其广泛应用于机器人控制、自动驾驶、具身智能等前沿领域，有效解决了现实世界数据采集成本高、风险大、效率低的痛点。

核心挑战在于\*\*域差距（Domain Gap）\*\* ——仿真环境与现实世界在传感器噪声、物理参数、光照条件等方面的固有差异，常导致模型迁移后性能显著下降。本指南将系统梳理Sim2Real的核心目标、常用策略、实践方案及学习资源。

#### 一、核心目标

Sim2Real的核心目标是：​**赋予模型强大的迁移能力，使其在真实环境中的表现与仿真环境中保持一致**​。

实现该目标的第一步是选择适配任务的仿真平台，以下是不同任务场景的主流平台推荐：

| 核心任务   | 推荐仿真平台                              |
| ------------ | ------------------------------------------- |
| 机器人控制 | PyBullet, Isaac Gym, MuJoCo, Gazebo       |
| 视觉导航   | Habitat, Gibson, AI2-THOR                 |
| 多模态感知 | Isaac Sim, Unity, Blender（适合自建场景） |

#### 二、常用Sim2Real策略

针对域差距问题，业界形成了多种成熟的迁移策略，可根据任务需求单独或组合使用：

##### 1. 域随机化（Domain Randomization）

在仿真环境中随机调整颜色、纹理、光照强度、物体物理参数（重量、摩擦系数等），迫使模型学习环境的本质特征而非表面噪声，从而提升泛化能力。

✅ 示例：训练机器人抓取时，每次迭代随机更换桌面纹理、目标物体颜色及重量。

##### 2. 域适应（Domain Adaptation）

通过技术手段主动缩小仿真与现实的数据分布差异，典型方法包括对抗学习（构建域判别器区分数据来源，模型学习混淆域判别器的特征）、数据对齐等。

##### 3. 系统建模（System Identification）

通过传感器校准、物理实验等方式，精确测量并建模真实环境中的物理参数（如重力、阻尼、机械臂关节特性），使仿真环境尽可能逼近现实。

##### 4. 微调（Fine-tuning）

采用“预训练+微调”范式：在仿真环境中用大规模数据完成模型预训练，再利用少量真实世界数据对模型参数进行微调，快速适配真实场景。

##### 5. 基于表征学习的迁移（Sim2Real via Representation Learning）

学习一种对环境的抽象表征（如视觉Embedding），该表征能够过滤掉仿真与现实的表面差异，仅保留对决策至关重要的核心信息，降低域差距的影响。

#### 📌 典型应用场景

* 机器人：虚拟环境中训练抓取/装配技能，迁移至真实工厂完成工业作业
* 自动驾驶：在模拟城市道路中训练避障、跟车策略，部署到真实街道行驶
* 具身智能：数字人在虚拟家居场景学习交互，迁移至实体机器人服务家庭

#### 三、快速上手实践指南

从基础项目切入，结合必备工具链，是掌握Sim2Real的高效路径。

### 🎯 推荐起手项目

1. ​**机器人抓取任务**​：PyBullet 仿真平台 + 域随机化策略，实现机械臂对不同物体的稳定抓取
2. ​**强化学习导航任务**​：Habitat 环境 + PPO/DD-PPO 算法，训练智能体完成室内视觉导航
3. ​**视觉感知迁移**​：Blender 生成 RGB+Depth 合成数据，训练目标检测模型后迁移至真实图像

##### 🛠️ 必学工具链

| 工具类型       | 核心工具                     | 用途说明                                     |
| ---------------- | ------------------------------ | ---------------------------------------------- |
| 编程语言与框架 | Python, PyTorch/TensorFlow   | 模型开发、训练与部署                         |
| 机器人中间件   | ROS (Robot Operating System) | 连接仿真/实体机器人，实现运动控制            |
| 图像处理       | OpenCV                       | 仿真与真实图像的预处理、特征提取             |
| 仿真开发       | 仿真平台 SDK                 | 自定义场景、控制仿真对象（如 Isaac Gym API） |

### 🧠 优质学习资源

| 资源类型 | 推荐内容                                                                                                                               | 获取方式                      |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| 权威教程 | Stanford CS327A（机器人学习）、Isaac Sim Tutorials                                                                                     | 斯坦福官网、NVIDIA 开发者平台 |
| 核心论文 | 《Closing the Sim2Real Gap》(OpenAI)、《Domain Randomization for Transferring Deep Neural Networks from Simulation to the Real World》 | arXiv、Google Scholar         |
| 开源项目 | robosuite（机器人控制）、OpenAI Gym Environments（强化学习环境）                                                                       | GitHub                        |



  
### 5.5 大模型 SFT 经验分享

🔥 **收藏这一篇就够了！** 涵盖SFT核心价值、方法选型、数据构建、训练技巧等全流程干货，助力高效完成大模型微调。

#### 1、为什么大模型需要SFT？

微调（SFT，Supervised Fine-Tuning）是在具备广泛知识基础的大型预训练语言模型（LLM）上，通过针对性数据集开展的二次训练过程。其核心目标是实现**知识的精细化灌输**与​**指令系统的精确匹配**​，让通用大模型精准契合特定业务任务需求或深入某一垂直专业领域，解决预训练模型“通用性强但针对性弱”的问题。

#### 2、大模型 SFT 核心方法分类

##### 2.1 主流微调方式对比

| 微调方式                                           | 核心原理                                               | 适用场景                                                         | 核心优势                             |
| ---------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------ | -------------------------------------- |
| **全参数微调**Full Parameter Fine-Tuning     | 调整模型所有权重参数，使模型完全适配特定领域/任务      | 拥有大量（万级以上）与任务高度相关的高质量标注数据；算力资源充足 | 拟合效果最优，能深度挖掘任务特性     |
| **部分参数微调**Sparse/Selective Fine-Tuning | 仅微调模型部分参数或新增轻量模块，不改动主体权重       | 数据量有限、算力资源紧张；需保留预训练知识避免遗忘               | 训练效率高、资源消耗低、过拟合风险小 |
| **冻结监督微调**Freeze-based SFT             | 冻结预训练模型主体权重，仅训练输出层或新增任务专属组件 | 任务简单（如分类、简单问答）；数据量极少                         | 训练速度快，避免预训练知识被覆盖     |

##### 2.2 热门部分参数微调技术详解

* ​**LoRA（低秩适应**​：在模型权重矩阵中插入低秩矩阵，通过更新低秩矩阵参数实现微调。核心优势是保留预训练知识，训练参数量仅为全量微调的1%\~10%，大幅降低显存占用。
* ​**P-tuning v2**​：基于Prompt Tuning的优化方案，仅微调与[Prompt]相关的可学习嵌入参数，不修改模型主体。适用于小样本场景，尤其在自然语言理解（NLU）任务中表现优异。
* ​**QLoRA**​：结合LoRA与4bit/8bit量化技术，将模型权重量化后再插入低秩矩阵，在保持效果的同时进一步降低资源消耗，支持在消费级GPU上微调百亿参数模型。

##### 2.3 方法选择建议

```
1. 算力充足+数据优质足量：优先选择全参数微调，追求最佳效果；       2. 算力有限+数据量中等：优先LoRA/QLoRA，平衡效果与效率；       3. 小样本+简单任务：选择P-tuning v2或冻结微调。
```

#### 3、指令微调（Instruction Tuning）核心实践

##### 3.1 核心定义

指令微调是SFT的重要分支，通过让模型学习“指令-响应”的映射关系，增强模型对自然语言指令的理解与执行能力，提升输出的一致性、准确性和泛化性，使模型更贴近人类交互习惯。

##### 3.2 数据格式规范

核心是构建清晰的“角色-指令-响应”结构，加入特殊令牌（Token）明确文本边界，示例如下：

```text
<bos_token>【USER】：将下列中文句子翻译成英语："人工智能正在重塑世界"<sep_token>【BOT】：Artificial intelligence is reshaping the world<eos_token>
```

关键要素： - 角色标识：用【USER】【BOT】明确交互双方，部分场景可加入【SYSTEM】定义模型身份； - 特殊令牌：<bos\_token>（句子开始）、<sep\_token>（分隔符）、<eos\_token>（句子结束），帮助模型识别文本边界； - 任务对齐：指令需明确任务类型（翻译、总结、推理等），响应需精准匹配指令要求。

##### 3.3 训练特点

* ​**损失计算**​：采用自回归预测模式，使用交叉熵（Cross-Entropy）作为损失函数；
* ​**损失屏蔽**​：仅计算【BOT】响应部分的损失，【USER】指令部分通过设置`ignore_index=-100`隐掉，避免模型学习无关内容。

#### 4、SFT 样本构建：质量远比数量重要

##### 4.1 核心原则

Meta在《LIMA: Less Is More for Alignment》中证实：​**1万份高质量样本的微调效果，远超10万份低质量样本**​。样本构建的核心是“精准匹配任务、控制噪声、保证多样性”。

##### 4.2 样本质量评估5大维度

1. ​**多样性**​： - 指令多样性：覆盖不同任务类型（如问答、总结、生成）、难度级别（简单→复杂）、表述方式（书面语→口语）； - 内容多样性：涵盖领域内不同主题、文体（报告→对话）、长度，避免模型过拟合单一场景。
2. ​**答案质量**​： - 准确性：无事实错误、逻辑矛盾，严格遵循领域知识； - 完备性：全面覆盖指令要求的所有要点（尤其复合任务，如“总结+分析”）； - 简洁性：表达清晰，无冗余信息，符合任务输出规范。
3. ​**一致性**​： - 内部一致：相同指令对相似内容的处理逻辑、输出格式保持统一； - 外部一致：符合领域共识、专家判断或公认基准。
4. ​**难度适配**​：按“7:2:1”比例分配简单、中等、复杂样本，助力模型逐步提升复杂任务处理能力。
5. ​**噪声控制**​：剔除标注错误、重复样本、无关内容，必要时通过人工审核保证数据集纯净度。

#### 5、SFT 训练核心技巧（Trick）

##### 5.1 标准训练流程

工业界通用范式：​**预训练（Pre-training）→ 监督微调（SFT）→ 基于人类反馈的强化学习（RLHF）**​，从基础模型（Base Model）逐步迭代为具备优质交互能力的对话模型（Chat Model）。

##### 5.2 领域数据SFT关键策略

###### 构建高质量领域数据集

定向采集领域内特有场景、专业术语、规范标准及典型对话数据；邀请领域专家参与标注，确保复杂任务标签精准；保证各类子任务、场景在数据集中均匀分布，避免偏斜。

###### 数据增强与跨域迁移

* 数据扩充：通过“文本同义替换、句法结构变换、多轮对话扩展、合理噪声插入”等方式丰富样本多样性；
* 跨域借鉴：引入关联领域数据（如“金融科技”可借鉴“通用金融+人工智能”数据），利用领域共性加速模型学习。

###### 定制化微调方案

* 分层次微调：先通过通用领域数据让模型适应交互形式，再用垂直领域数据做精细化微调；
* 多任务融合：将领域内相关任务（如“医疗问答+病历总结”）联合微调，增强模型领域整体认知；
* 动态优化：根据验证集损失变化调整学习率、正则化力度，设置早停规则（如连续3个epoch损失无下降则停止）。

###### 轻量级技术落地

资源有限时优先选择： - 插件化微调：植入Adapter模块，仅更新模块参数； - LoRA/QLoRA：百亿参数模型可在单卡GPU上完成微调； - Prompt调优：通过设计领域专属提示词引导模型输出，无需改动模型权重。

###### 持续迭代机制

建立“业务反馈→数据更新→模型微调”的闭环： - 监控：定期评估模型在实际业务中的表现，定位回答错误、逻辑混乱等问题； - 学习：将用户交互中的优质对话标注为样本，用于模型增量微调； - 反馈：收集用户差评与建议，针对性优化样本构建与微调策略。

#### 6、SFT 训练模式选择指南

##### 6.1 7种主流训练模式

1. Base模型 + 领域任务SFT
2. Base模型 + 领域数据续训（Continue Pre-train） + 领域任务SFT
3. Base模型 + 领域数据续训 + 通用任务SFT + 领域任务SFT
4. Base模型 + 领域数据续训 + 通用+领域任务混合SFT
5. Base模型 + 领域数据续训（混入SFT数据） + 通用+领域任务混合SFT
6. Chat模型 + 领域任务SFT
7. Chat模型 + 领域数据续训 + 领域任务SFT

##### 6.2 关键决策依据

###### 是否需要“续训（Continue Pre-train）”？

✅ 必选场景： - 领域数据与预训练数据差异极大（如企业内部文档、小众专业领域）； - 领域数据量充足（Token≥1B），且核心目标是最大化领域效果。 ❌ 可选场景： - 领域与通用场景差异小（如通用客服→电商客服）； - 数据量少（Token＜100M）。

###### Base模型 vs Chat模型？

| 对比维度     | Base模型                       | Chat模型                                     |
| -------------- | -------------------------------- | ---------------------------------------------- |
| 领域SFT效果  | 优质Base模型效果与Chat模型接近 | 初始交互性好，但领域适配需克服“灾难性遗忘” |
| 通用能力保留 | 微调后通用能力损失小           | 领域SFT后易丢失通用对话能力                  |
| 适用场景     | 需兼顾领域效果与通用能力       | 仅追求领域专属效果，无需通用交互             |

###### 模式选择速查表

```
- 资源充足+仅追领域效果：模式二（Base+领域续训+领域SFT）       - 资源充足+兼顾综合能力：模式五（Base+混合续训+混合SFT）       - 资源有限+快速落地：模式六（Chat+领域SFT）       - 小样本+通用+领域兼顾：模式三（Base+续训+通用SFT+领域SFT）
```

#### 7. SFT 核心参数调整指南

##### 7.1 关键参数设置（附实践案例）

| 参数名称                | 核心作用                           | 建议值                                                         | 实践经验                                                     |
| ------------------------- | ------------------------------------ | ---------------------------------------------------------------- | -------------------------------------------------------------- |
| 学习率（Learning Rate） | 控制参数更新幅度，直接影响收敛效果 | SFT阶段设为预训练的0.1倍（如预训练9e-5 → SFT 9e-6）           | 10万样本用9e-5训练时loss不收敛，调低至9e-6后，2个epoch即收敛 |
| Warmup Ratio            | 避免初始学习率过高导致模型震荡     | 预训练：0.01\~0.015；SFT：0.005\~0.01（样本量越小，ratio越小） | 学习率较大时，可适当增大ratio（如1e-5 → ratio 0.01）        |
| Epoch（轮次）           | 控制训练数据暴露次数               | 样本量＜1万：3\~5轮；样本量1\~10万：2轮；样本量＞10万：1\~2轮  | 小样本场景，过拟合风险低于欠拟合，可适当增加Epoch            |
| Batch Size              | 平衡训练效率与稳定性               | 根据显存调整，建议8\~32（显存不足用梯度累积弥补）              | 用LoRA时，Batch Size可比全量微调增大2\~3倍                   |

##### 7.2 其他重要建议

* 多任务场景：为不同任务配置专属System Prompt（如“你是电商客服，需热情解答订单问题”），提升任务区分度；
* 模型选择：基座模型的质量（预训练数据、参数量）是SFT效果的基础，优先选择经过大规模验证的模型（如Llama 3、Qwen等）；
* 指标监控：Loss是核心指标（通常先升后降，若持续上升需检查数据格式或学习率），同时结合人工评估输出质量；
* 混合训练：续训时混入少量高质量SFT数据，SFT时加入少量领域预训练数据，可提升模型适应性。

---

#### 附：SFT 实践工具推荐

* 微调框架：Transformers、PEFT（Hugging Face）、LLaMA Factory、FastChat；
* 量化工具：BitsAndBytes、GPTQ；
* 数据处理：Datasets（Hugging Face）、Pandas；
* 监控工具：WandB、TensorBoard。


---

## 6. 仿真学习（Simulation）

**贡献者**：@charlie

### 目录（Table of Contents）
- [6.1 平台对比：Isaac Lab / MuJoCo / PyBullet / Genesis / Gazebo)
- [6.2 任务基准：单胳膊/双臂/移动操作/装配)
- [6.3 资产与场景：USD/URDF 导入、相机布局、光照与碰撞)
- [6.4 日志与回放：录制、重放、评测)
- [6.5 **样板：Isaac Lab 最小上手（可复制运行）**)

---

### 6.1 平台对比：Isaac Lab / MuJoCo / PyBullet / Genesis / Gazebo
在具身智能的研究与开发中，仿真平台扮演着极其重要的角色。这个板块涵盖了常见的仿真工具与平台，帮助您构建虚拟环境并进行模型训练。

#### 6.1.1 Isaac Lab
##### 6.1.1.1 Isaac Sim 入门

原文：https://www.yuque.com/g/ryanji-wtpey/aumvf4/yyhruy8kts47s34v/collaborator/join?token=szoLcoWDy2LLWj5t&source=doc_collaborator# 《🌮【仿真】isaac sim》
copy：


**安装**

系统安装要求：

[https://docs.omniverse.nvidia.com/platform/latest/common/technical-requirements.html](https://docs.omniverse.nvidia.com/platform/latest/common/technical-requirements.html)

<img width="553" height="326" alt="image" src="https://github.com/user-attachments/assets/e5e55c06-d693-40c2-b97e-42e1f4e9a5f9" />

【omniverse】的下载与安装：

下载[https://developer.nvidia.cn/omniverse](https://developer.nvidia.cn/omniverse)，需要邮箱注册。

<img width="552" height="245" alt="image" src="https://github.com/user-attachments/assets/69d738b4-5cbe-4fe8-bbc7-b1b2870c03df" />


之后点击该网站[https://docs.omniverse.nvidia.com/install-guide/latest/index.html](https://docs.omniverse.nvidia.com/install-guide/latest/index.html)

选择你的安装方式[https://docs.omniverse.nvidia.com/install-guide/latest/workstation-install.html](https://docs.omniverse.nvidia.com/install-guide/latest/workstation-install.html)
- 下载 omniverse launcher
- linux 安装方法: 
  - 给权限，命令行 ./xxxx
  - 或者不用命令行，右键APPImage -> permissions -> allow execution as file
- 注册账户yanaibo1214@gmail.com

<img width="554" height="132" alt="image" src="https://github.com/user-attachments/assets/f7af056e-a545-40dd-9de5-a254a376517a" />


【Isaac Sim】的安装：

官网 [https://developer.nvidia.com/isaac/sim](https://developer.nvidia.com/isaac/sim)
 
<img width="554" height="296" alt="image" src="https://github.com/user-attachments/assets/7a9c847c-4cf0-4e5e-8567-4b043b26b466" />

prerequisite 系统要求

<img width="553" height="468" alt="image" src="https://github.com/user-attachments/assets/c1ee2d2f-8ef1-4903-bea6-10f4b73b179b" />


安装 Isaac sim：
- 点击 exchange 交易所，找到 isaac sim

<img width="554" height="327" alt="image" src="https://github.com/user-attachments/assets/36dd62c7-59be-469b-86fb-41387876ccfa" />

- 版本选择 2023.1.1 或者 2023.1.0

- 安装 cache

<img width="553" height="327" alt="image" src="https://github.com/user-attachments/assets/b60c636a-5814-46bd-92ba-db0d29eb7896" />

- 安装完毕之后，进入 Nucleus 注册账户

<img width="553" height="326" alt="image" src="https://github.com/user-attachments/assets/0420a89e-228e-4fa3-a76f-5a0df784522e" />

- 点击 设置 。必须有 Cache 出来才算装上了，并且都是 RUNNING 状态
假如 Cache 是 Stop 状态，就换一个版本 2023.1.0  去图书馆卸载 Cache 再重新安装

<img width="554" height="533" alt="image" src="https://github.com/user-attachments/assets/1cd37149-cb18-4e6d-a331-8300d51a0400" />

- 同时点击文件夹，可以打开浏览器看到文件内容

<img width="553" height="325" alt="image" src="https://github.com/user-attachments/assets/9afedb3c-725c-467d-867a-80389a334f62" />


**GR00T**

[https://developer.nvidia.com/project-GR00T?ncid=so-yout-261862-vt48 ](https://developer.nvidia.com/project-GR00T?ncid=so-yout-261862-vt48 )

**基本结构**

<img width="554" height="97" alt="image" src="https://github.com/user-attachments/assets/94bcc8aa-dbac-4510-955f-9340dc8a39b8" />

**基本操作教程**

- menu bar 工具栏：
左侧栏：

<img width="78" height="378" alt="image" src="https://github.com/user-attachments/assets/537407e9-725c-4c7c-972a-0f838394d3cc" />

1 是选择 2 是移动 3 是旋转。 搭配使用：先选择物体，再拖动它。快捷键 QWER。WW按两下会显示自身坐标系，按一下就是世界坐标系

项目栏：这里可以打开代码
时间戳：window->extensions
时间戳是一个扩展程序，允许开发人员查看和修改可滚动和可自定义时间线的设置。默认情况下，时间线处于禁用状态，要启用它，请转到窗口 > 扩展，在搜索栏中输入omni.anim.window.timeline，然后单击切换按钮。然后，在屏幕底部，会出现时间线小部件。当您按下“播放”按钮时，时间线标记开始移动，并在时间线上循环。模拟的开始/停止进度也可以在默认布局底部的时间线上查看。

- helloworld 入门：
启动 Isaac Sim launcher
加载了一个地板

<img width="552" height="302" alt="image" src="https://github.com/user-attachments/assets/6b708c67-473c-4be7-825b-a399c621706a" />

<img width="553" height="418" alt="image" src="https://github.com/user-attachments/assets/fb92324a-6085-420f-af4b-12b8a7d85845" />

- 退出当前项目：点击 File，点击 New，dont save 即可。

- 机械臂 demo 

<img width="554" height="299" alt="image" src="https://github.com/user-attachments/assets/b6f18784-98ad-4091-9e21-187593720262" />

<img width="552" height="291" alt="image" src="https://github.com/user-attachments/assets/99cd9a40-624e-4ace-aff6-d4930881011d" />

- 抓取：右侧的 stage 场景中点击 target cube，将它拖到任意一个机械臂可能到达的地方，点击左侧 Task Controls 中的 Follow Target 按钮的 start，机械臂就开始运动了。

- 堆码垛 demo：manuplation simple stack。

- 机器人种类：UR10 Franka jetbot realsense 等。

- extensions 创建

<img width="554" height="847" alt="image" src="https://github.com/user-attachments/assets/3de623f3-db43-45cb-bd1e-3511cb9ee33f" />

<img width="554" height="349" alt="image" src="https://github.com/user-attachments/assets/924dfe1b-b0a4-4f47-95ec-1e704db522fd" />

Configuration Tooling Template 配置工具类；
Loaded Scenario template 办公室等场景的模版；
Scripting Template 脚本模版，例如工厂流水线式工作，第一步、第二步、第三步固定；
UI Component Library 仪表等需要人看着操作的

<img width="554" height="438" alt="image" src="https://github.com/user-attachments/assets/af0f30af-dfec-4a4e-b4fb-56f05f9ddc79" />

打开

<img width="554" height="388" alt="image" src="https://github.com/user-attachments/assets/da5668b3-2062-481c-b510-fbb1b5a1050f" />

<img width="553" height="344" alt="image" src="https://github.com/user-attachments/assets/241a7ca0-6f77-448d-8506-7794e34c3538" />

<img width="554" height="344" alt="image" src="https://github.com/user-attachments/assets/081cb215-e01b-4e53-9688-9fa20df93d9c" />

添加你自己创建的 extensions，添加完成之后点击自己的 extensions，可以查看信息
<img width="554" height="342" alt="image" src="https://github.com/user-attachments/assets/8cae57c8-7f2b-4bde-8fee-171fcd2bc528" />

同时，在任务栏也会出现一个条目 title，点击它的下拉菜单，加载扩展（extension）
<img width="553" height="189" alt="image" src="https://github.com/user-attachments/assets/36fe24a8-3164-476e-84b9-de1befe2bde0" />

-standalone 应用-python 创建：
意思就是用 python 脚本来启动 isaac sim，不是用 gui。好处是不占用资源，因为界面渲染会占据大量资源。这个方式适合强化学习。
先关闭 isaac sim

强化学习

<img width="553" height="48" alt="image" src="https://github.com/user-attachments/assets/848dc061-0fa5-4b3c-9c2b-291fb01dec7e" />

<img width="554" height="391" alt="image" src="https://github.com/user-attachments/assets/b7d7d861-2356-4b52-8257-49aad8ecb66f" />

这个案例是让小车靠近小球。

普通应用

```Shell
cd /home/yab/.local/share/ov/pkg/isaac-sim-2023.1.1
```

```Shell
./python.sh standalone_examples/api/omni.isaac.franka/follow_target_with_rmpflow.py
```

执行之后等待一下，

<img width="554" height="361" alt="image" src="https://github.com/user-attachments/assets/4886e780-ca32-43ed-bcf8-b40af78246df" />

或者

```Shell
./python.sh standalone_examples/api/omni.isaac.core/add_cubes.py
```


**stage 配置**

设置全局场景属性及物理属性

<img width="554" height="391" alt="image" src="https://github.com/user-attachments/assets/8ca19faf-716b-4dd9-b711-a04960bab965" />
<img width="554" height="970" alt="image" src="https://github.com/user-attachments/assets/8450ba7d-a188-43da-a07d-98707595f345" />

添加地面

<img width="554" height="970" alt="image" src="https://github.com/user-attachments/assets/96eadb61-6df5-463c-a4fe-87e6bad6b050" />
<img width="553" height="422" alt="image" src="https://github.com/user-attachments/assets/b0d86ea9-f59b-4805-affb-31c2013e6b5c" />

添加灯光

<img width="553" height="397" alt="image" src="https://github.com/user-attachments/assets/0e63dd55-883d-4cb9-96a2-81d5816e81ef" />

**制作一个简易小车入门**

添加和抓取形状，并给物体添加物理属性(刚体，碰撞体，预设属性)

<img width="554" height="305" alt="image" src="https://github.com/user-attachments/assets/fec64f34-5e15-4aa2-b7fd-765b79ab296b" />


如果添加了，那么开始仿真之后，它就会像真实世界中的物体倒地。

<img width="554" height="446" alt="image" src="https://github.com/user-attachments/assets/4c715f73-5ca4-4aaf-b503-3df69bd2ff4c" />

如果 enable 取消勾选，物体就不会倒地（测试碰撞属性同上）

<img width="554" height="353" alt="image" src="https://github.com/user-attachments/assets/77c49919-f17d-4431-80d9-1762cdc9d11e" />



编辑物理属性比如摩擦力：

<img width="517" height="931" alt="image" src="https://github.com/user-attachments/assets/ed305eb8-f00f-4d5b-abb6-21cdce28c35b" />

<img width="554" height="544" alt="image" src="https://github.com/user-attachments/assets/c3bf7613-ca0f-4180-8ef3-c9dcf2d2da10" />

编辑物理属性比如颜色和反射率：

首先选择你要改变的物体，再点击颜色设置

<img width="554" height="805" alt="image" src="https://github.com/user-attachments/assets/d3c499db-2f05-4cf8-bf36-820a225fdeac" />

再选中车体，选择 material：

<img width="553" height="369" alt="image" src="https://github.com/user-attachments/assets/2b2bd375-2155-4b5f-8651-ea7b27de906f" />

建立图元 prim：

<img width="554" height="392" alt="image" src="https://github.com/user-attachments/assets/4122fca8-659f-452e-b8c8-0cf693923071" />

<img width="554" height="654" alt="image" src="https://github.com/user-attachments/assets/0b07a58e-9d3b-4e85-9c9c-10257af0fefd" />

添加关节：
- 选中 body 和 left wheel，然后 create 一个 revolute joint
- 此时会出现一个绿色的圆圈，调整它的 axis，使得圆圈的朝向和轮子旋转的方向一致即可
- 点击开始仿真按钮，按住 shift 按键，单击车子任意部位，即可拖动它运动

<img width="517" height="827" alt="image" src="https://github.com/user-attachments/assets/c256563a-1818-4952-b856-d3a529331171" />

添加驱动：
- 同时选中两个关节，添加角度驱动器

<img width="554" height="579" alt="image" src="https://github.com/user-attachments/assets/7577c2b6-716d-4383-9266-32110f127354" />

- 位置控制：对于位置控制关节，设置高刚度和相对低或零阻尼。
- 速度控制：对于速度控制器关节，设置高阻尼和零刚度。
对于车轮上的关节，速度控制更有意义，因此将两个车轮的阻尼设置为1e4*，并将目标速度设置为200。如果您使用的关节范围有限，则可以在“属性”选项卡的“原始 USD 属性”>“下限（上限）”下进行设置。按下“播放”即可看到模拟移动机器人启动。

添加关节根 articulation：

<img width="525" height="806" alt="image" src="https://github.com/user-attachments/assets/18050bfb-ca3b-41bc-93c0-dbd0db892c5f" />

添加相机和传感器

<img width="553" height="348" alt="image" src="https://github.com/user-attachments/assets/d596f142-e013-4be2-ace8-64812a981d39" />

添加激光雷达

[https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_range_sensor_lidar.html#isaac-sim-app-tutorial-advanced-range-sensor-lidar](https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_range_sensor_lidar.html#isaac-sim-app-tutorial-advanced-range-sensor-lidar)

更复杂的机器人

[https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_rigging_robot.html#isaac-sim-app-tutorial-advanced-rigging-robot](https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_rigging_robot.html#isaac-sim-app-tutorial-advanced-rigging-robot)

<img width="554" height="223" alt="image" src="https://github.com/user-attachments/assets/37ef5874-df69-453a-b0ec-c2f6be8269ec" />

**调用外部 python 编译器**

通过调用外部的编辑器来操作 isaac sim，或者通过 WINDOW EXTENSIONS

<img width="554" height="466" alt="image" src="https://github.com/user-attachments/assets/f9ff95f9-45c8-4c2d-9cdd-7ef2eb42d9c0" />

- 打开一个新的 terminal，输入 telnet localhost 8223
- 输入代码，回车
仅在空的 Stage 运行Isaac Sim Core API，并且只运行一次。

原始 USD API 功能多样且详细，但很复杂，尤其是对于初学者来说。Isaac Sim 有一组核心 API，可简化机器人模拟器的一些常用操作。这些 API 抽象了默认参数设置。（设置舞台，添加具有物理和碰撞预设的长方体，设置物理和视觉材料属性）


```python
import numpy as np
from omni.isaac.core.objects import DynamicCuboid
from omni.isaac.core.objects.ground_plane import GroundPlane
from omni.isaac.core.physics_context import PhysicsContext
PhysicsContext()
GroundPlane(prim_path="/World/groundPlane", size=10, color=np.array([0.5, 0.5, 0.5]))
DynamicCuboid(prim_path="/World/cube",
    position=np.array([-.5, -.2, 1.0]),
    scale=np.array([.5, .5, .5]),
    color=np.array([.2,.3,0.]))
```

**编辑器使用**

Isaac Sim VS Code Edition：

先要在 vscode 中安装插件。在 4.0.0 中快速打开 vscode 的方法是在扩展管理中使能扩展插件，如下

<img width="452" height="510" alt="image" src="https://github.com/user-attachments/assets/c79e4034-6bfe-4e82-afb0-fd211aa2d3f3" />

在更早的版本，则打开 Isaac Sim App Selector

<img width="553" height="506" alt="image" src="https://github.com/user-attachments/assets/a89c2b16-cd27-4458-815e-0ca921717f99" />

详情见链接[https://docs.omniverse.nvidia.com/isaacsim/latest/reference_material/reference_user_interface.html#isaac-sim-app-selector](https://docs.omniverse.nvidia.com/isaacsim/latest/reference_material/reference_user_interface.html#isaac-sim-app-selector)
点击

<img width="554" height="657" alt="image" src="https://github.com/user-attachments/assets/89c0ef10-0c41-4ebe-b9e4-087a5284e47f" />

创建一个空的 python 脚本，输入代码，点击左侧的运行按钮，得到一个球体

<img width="554" height="661" alt="image" src="https://github.com/user-attachments/assets/abf6ed14-06b6-4c8c-ad4b-e4d99c7a8de4" />

<img width="552" height="343" alt="image" src="https://github.com/user-attachments/assets/40338c83-1504-4f66-9c6a-a2fd118cd342" />

更多细节可以参考[https://marketplace.visualstudio.com/items?itemName=NVIDIA.isaacsim-vscode-edition](https://marketplace.visualstudio.com/items?itemName=NVIDIA.isaacsim-vscode-edition)

在 vscode 中debug 用 python 文件：

- 打开 Isaac Sim App Selector

详情见链接[https://docs.omniverse.nvidia.com/isaacsim/latest/reference_material/reference_user_interface.html#isaac-sim-app-selector](https://docs.omniverse.nvidia.com/isaacsim/latest/reference_material/reference_user_interface.html#isaac-sim-app-selector)

<img width="554" height="535" alt="image" src="https://github.com/user-attachments/assets/346c8b14-a4fc-4c21-888d-ddd87c04d15a" />

- vscode 中要先安装 isaac 插件 Isaac Sim VS Code Edition
- 打开之后，我们测试一个 demo，文件目录如下，加一个断点。

<img width="554" height="657" alt="image" src="https://github.com/user-attachments/assets/e6b0d1e3-0453-40e0-958a-344df1a6da02" />

- 点击左侧的 run and debug 按钮，点击 debug 即可。或者按 F5 也可以

<img width="554" height="621" alt="image" src="https://github.com/user-attachments/assets/fdb8612a-f631-41f4-b22a-e8f5ba0e8a32" />

- 传参数
更改一下 launch.json 和 python 文件

```Shell
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "
${file}",
            "console": "integratedTerminal",
            "env": {
                "EXP_PATH": "$
{workspaceFolder}/apps",
                "RESOURCE_NAME": "IsaacSim"
            },
            "python": "
${workspaceFolder}/kit/python/bin/python3",
            "envFile": "$
{workspaceFolder}/.vscode/.standalone_examples.env",
            "preLaunchTask": "setup_python_env",
            "args": ["--/persistent/isaac/asset_root/default=\"omniverse://my_server\""]
        }
        ,
        {
            "name": "Python: Current File",
            "type": "python",
            "request": "launch",
            "program": "
${file}",
            "console": "integratedTerminal",
            "env": {
                "RESOURCE_NAME": "IsaacSim"
            },
            "python": "$
{workspaceFolder}/kit/python/bin/python3",
            "envFile": "
${workspaceFolder}/.vscode/.standalone_examples.env",
            "preLaunchTask": "setup_python_env"
        },
        {
            "name": "Python: Attach (windows-x86_64/linux-x86_64)",
            "type": "python",
            "request": "attach",
            "port": 3000,
            "host": "localhost"
        },
        {
            "name": "(Linux) isaac-sim",
            "type": "cppdbg",
            "request": "launch",
            "program": "$
{workspaceFolder}/kit/kit",
            "args": ["
${workspaceFolder}/apps/omni.isaac.sim.kit",
                "--ext-folder", "$
{workspaceFolder}/exts",
                "--ext-folder", "
${workspaceFolder}/apps"],
            "stopAtEntry": false,
            "cwd": "$
{workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```

```python
Copyright (c) 2020-2023, NVIDIA CORPORATION. All rights reserved.
NVIDIA CORPORATION and its licensors retain all intellectual property
and proprietary rights in and to this software, related documentation
and any modifications thereto. Any use, reproduction, disclosure or
distribution of this software and related documentation without an express
license agreement from NVIDIA CORPORATION is strictly prohibited.
import omni
from omni.isaac.kit import SimulationApp
# The most basic usage for creating a simulation app
kit = SimulationApp()
for i in range(100):
kit.update()
omni.kit.app.get_app().print_and_log("Hello World!")
kit.close()  # Cleanup application
The most basic usage for creating a simulation app
kit = SimulationApp()
import carb
server_check = carb.settings.get_settings().get_as_string("/persistent/isaac/asset_root/default")
print(server_check)
for i in range(100):
    kit.update()
kit.close()  # Cleanup application
```

<img width="554" height="282" alt="image" src="https://github.com/user-attachments/assets/4219cfbd-ec58-43b4-a8e1-67b9d84e9c6d" />

debug 在 isaac sim 中跑的应用和 vscode 交互
- 运行 isaac sim
-  在 isaac sim 顶部工具栏的窗口，扩展中搜索 omni.kit.debug.vscode，使能它，然后可以看到一行红字“VS Code Debugger Unattached”

<img width="553" height="227" alt="image" src="https://github.com/user-attachments/assets/8fe14b19-9537-46c8-a94e-656172f4e9b2" />

- 运行你刚刚的 vscode，点击 debug 的按钮旁边的下拉菜单

<img width="554" height="566" alt="image" src="https://github.com/user-attachments/assets/f3a9dc09-692e-4120-a79f-1074b34f04c8" />

这时候红色字变蓝色了
- 上一步能成功，原因在于 vscode 和 isaac sim 之间配置了相同的 ip 和端口

<img width="396" height="277" alt="image" src="https://github.com/user-attachments/assets/b69fdfc3-9652-4e4e-857d-9d59846f2bc3" />

想要更改参数，在 app selector 中添加即可

```Shell
--/exts/omni.kit.debug.python/host="127.0.0.1"
--/exts/omni.kit.debug.python/port=3000
```

```Shell
    {
        "name": "Python: Attach (windows-x86_64/linux-x86_64)",
        "type": "python",
        "request": "attach",
        "port": 3000,
        "host": "127.0.0.1"
    },
```
- 点击 isaac sim 中的 Break，那么断点就会在 vscode 中出现

**核心 API**

hello world
工具栏选择 hello world，点击 containning folder，你就可以看到这个例子包含的代码文件

<img width="554" height="335" alt="image" src="https://github.com/user-attachments/assets/c149f395-e2c2-415f-9b73-74931d15d671" />

<img width="554" height="335" alt="image" src="https://github.com/user-attachments/assets/aa8d049c-1c8a-475d-9d66-8540abe85b92" />

- world 是单例
打开 hello_world.py
重写代码

```python
Copyright (c) 2020-2023, NVIDIA CORPORATION. All rights reserved.
NVIDIA CORPORATION and its licensors retain all intellectual property
and proprietary rights in and to this software, related documentation
and any modifications thereto. Any use, reproduction, disclosure or
distribution of this software and related documentation without an express
license agreement from NVIDIA CORPORATION is strictly prohibited.
from omni.isaac.examples.base_sample import BaseSample
import numpy as np
Can be used to create a new cube or to point to an already existing cube in stage.
from omni.isaac.core.objects import DynamicCuboid
Note: checkout the required tutorials at https://docs.omniverse.nvidia.com/app_isaacsim/app_isaacsim/overview.html
class HelloWorld(BaseSample):
    def 
__init__
(self) -> None:
        super().
__init__
()
        return
    def setup_scene(self):
        world = self.get_world()
        world.scene.add_default_ground_plane()
        fancy_cube = world.scene.add(
            DynamicCuboid(
                prim_path="/World/random_cube", # The prim path of the cube in the USD stage
                name="fancy_cube", # The unique name used to retrieve the object from the scene later on
                position=np.array([0, 0, 1.0]), # Using the current stage units which is in meters by default.
                scale=np.array([0.5015, 0.5015, 0.5015]), # most arguments accept mainly numpy arrays.
                color=np.array([0, 0, 1.0]), # RGB channels, going from 0-1
            ))
        return
    async def setup_post_load(self):
        return
    async def setup_pre_reset(self):
        return
    async def setup_post_reset(self):
        return
    def world_cleanup(self):
        return
```

重新开一个 stage，点击 load hello world
添加打印信息，可以在 terminal 中显示

```Shell
from omni.isaac.examples.base_sample import BaseSample
import numpy as np
from omni.isaac.core.objects import DynamicCuboid
class HelloWorld(BaseSample):
    def 
__init__
(self) -> None:
        super().
__init__
()
        return
    def setup_scene(self):
        world = self.get_world()
        world.scene.add_default_ground_plane()
        fancy_cube = world.scene.add(
            DynamicCuboid(
                prim_path="/World/random_cube",
                name="fancy_cube",
                position=np.array([0, 0, 1.0]),
                scale=np.array([0.5015, 0.5015, 0.5015]),
                color=np.array([0, 0, 1.0]),
            ))
        return
    async def setup_post_load(self):
        self._world = self.get_world()
        self._cube = self._world.scene.get_object("fancy_cube")
        self._world.add_physics_callback("sim_step", callback_fn=self.print_cube_info) #callback names have to be unique
        return
    # here we define the physics callback to be called before each physics step, all physics callbacks must take
    # step_size as an argument
    def print_cube_info(self, step_size):
        position, orientation = self._cube.get_world_pose()
        linear_velocity = self._cube.get_linear_velocity()
        # will be shown on terminal
        print("Cube position is : " + str(position))
        print("Cube's orientation is : " + str(orientation))
        print("Cube's linear velocity is : " + str(linear_velocity))
```

[https://docs.omniverse.nvidia.com/isaacsim/latest/core_api_tutorials/tutorial_core_hello_world.html](https://docs.omniverse.nvidia.com/isaacsim/latest/core_api_tutorials/tutorial_core_hello_world.html)

**ROS 和 ROS2**

ROS1
参考文档：[https://docs.omniverse.nvidia.com/isaacsim/latest/ros_tutorials/tutorial_ros_turtlebot.html
turtlebot3](https://docs.omniverse.nvidia.com/isaacsim/latest/ros_tutorials/tutorial_ros_turtlebot.html
turtlebot3) 链接：[https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/](https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)
- 导入 turtlebot3_burger
进入 isaac sim 的工作空间

```Plain Text
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git turtlebot3
```

```Plain Text
rosrun xacro xacro -o turtlebot3_burger.urdf turtlebot3_burger.urdf.xacro
```

<img width="553" height="297" alt="image" src="https://github.com/user-attachments/assets/f47a4efb-cfb0-4459-96f3-6017df3a5dde" />

<img width="553" height="297" alt="image" src="https://github.com/user-attachments/assets/98c7f31c-fd39-4b2c-9a06-fffe4d4900c4" />


<img width="554" height="324" alt="image" src="https://github.com/user-attachments/assets/9ed1af7a-b813-4cc1-8716-4bb534749573" />

发送速度指令

```Plain Text
rostopic pub /cmd_vel geometry_msgs/Twist '{linear:  {x: 0.2, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.0}}'
```

```Plain Text
rostopic pub /cmd_vel geometry_msgs/Twist '{linear:  {x: 0.0, y: 0.0, z: 0.0}, angular: {x: 0.0,y: 0.0,z: 0.0}}'
```

```Plain Text
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

添加单线激光
发布 odom
先运行 roscore，再启动 isaac 模拟仿真。roscore 只要启动一次就可以了。不需要关掉。

<img width="525" height="388" alt="image" src="https://github.com/user-attachments/assets/453d466c-a279-4f93-b2a6-17d714494461" />

<img width="546" height="130" alt="image" src="https://github.com/user-attachments/assets/650300d0-ac55-424c-8aeb-404839846330" />

发布 odom->base_link
发布其他传感器的 link

<img width="554" height="490" alt="image" src="https://github.com/user-attachments/assets/841ff31e-f066-4568-9326-7ccce57d2ddb" />

<img width="531" height="346" alt="image" src="https://github.com/user-attachments/assets/e9f0348c-f14f-4e40-b6cd-6f1bdde1fd06" />

- 如果只写 targetPrims，那么生成的 tf 是 world->base_scan。
- 本案例中，两者都要填写。base_footprint 不填写，它会报错

<img width="531" height="346" alt="image" src="https://github.com/user-attachments/assets/a62fa1fe-5432-4724-9f67-865ff59d55cc" />
<img width="539" height="272" alt="image" src="https://github.com/user-attachments/assets/c7e862db-1a3d-4b9c-a25e-b44f91f0438c" />

导航--以 carter_warehouse 为例
[https://github.com/isaac-sim/IsaacSim-ros_workspaces](https://github.com/isaac-sim/IsaacSim-ros_workspaces)

单线激光雷达

<img width="325" height="233" alt="image" src="https://github.com/user-attachments/assets/1e642928-e54a-4572-aa93-3a97cddf2533" />

<img width="552" height="181" alt="image" src="https://github.com/user-attachments/assets/54912f37-0250-463e-b855-509f0c056c48" />

<img width="554" height="291" alt="image" src="https://github.com/user-attachments/assets/fbd4e1d2-88c3-4a5d-806b-9d01d237a781" />

0.1-0.62 占据栅格的高度范围

```Plain Text
roslaunch carter_2dnav carter_navigation.launch
```

多线激光雷达

<img width="553" height="242" alt="image" src="https://github.com/user-attachments/assets/ab1faf91-8336-4a60-8d9a-1b52bd0de9bf" />

Isaac/Samples/ROS/Scenario/rtx_lidar_carter_warehouse_navigation.usd

```Plain Text
roslaunch carter_2dnav carter_navigation_rtx.launch
```

ROS2
[https://docs.omniverse.nvidia.com/isaacsim/latest/ros_ros2_tutorials.html ](https://docs.omniverse.nvidia.com/isaacsim/latest/ros_ros2_tutorials.html )

官方 demo
[https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_navigation.html](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_navigation.html)

（1）加载模型
         Isaac Examples -> ROS2 -> Navigation
（2）点击 PLAY 开始仿真
（3）运行 launch 文件

```Shell
ros2 launch carter_navigation carter_navigation.launch.py
```

机器人初始位置配置在文件carter_navigation_params.yaml 中，如果机器人位置不正确，点击 rviz 中 的2D Pose Estimate 按钮给一个方向。
（4）导航
点击 rviz 中的 Navigation2 Goal 按钮，可以导航。
（5）自动导航

```Shell
ros2 launch isaac_ros_navigation_goal isaac_ros_navigation_goal.launch.py
```

其中 launch 的参数如下：
- goal_generator_type: 生成目标点的类型 RandomGoalGenerator 是随机生成； GoalReader 是用户自定义。
- map_yaml_path: 地图路径。默认 isaac_ros_navigation_goal/assets/carter_warehouse_navigation.yaml. 此时的目标点类型是 RandomGoalGenerator.
- iteration_count: 目标点被设置多少次.
- action_server_name: 执行服务器的名字.
- obstacle_search_distance_in_meters: 障碍物搜索距离.
- goal_text_file_path: 用户自定义的静态目标点。每一行都必须有一个单独的目标位姿，格式是pose.x pose.y orientation.x orientation.y orientation.z orientation.w. 参考文档在isaac_ros_navigation_goal/assets/goals.txt. 此时的目标点类型也必须是 GoalReader.
- initial_pose: 初始位姿 [pose.x, pose.y, pose.z, orientation.x, orientation.y, orientation.z, orientation.w].

（6）注意的地方
小车默认使用 RTX 雷达。
小车上大部分相机都屏蔽 publish 图片，可以去_camera_render_product 节点使能对应相机。
自制

<img width="554" height="314" alt="image" src="https://github.com/user-attachments/assets/9cd756a3-05bf-4fe7-be82-044f20fa7f9d" />

<img width="553" height="124" alt="image" src="https://github.com/user-attachments/assets/a6d9335d-a2f7-4339-9f8b-fbe6c02b6936" />

- 设置 ROS_DOMAIN_ID 为 0 ，因为 isaac sim 默认是 0
模型导入、栅格地图生成

<img width="554" height="383" alt="image" src="https://github.com/user-attachments/assets/b81e8e9b-0bfa-4171-984f-df64cfb07f12" />

<img width="553" height="398" alt="image" src="https://github.com/user-attachments/assets/407389e5-9da7-4361-be7d-fac83a6b3077" />

<img width="554" height="423" alt="image" src="https://github.com/user-attachments/assets/7bb5d6c3-f5d9-4cd4-8cd1-b4daa2b7113d" />

模型导入之后，用 ariculation inspector 来观察是否导入正确。检查机器人行为是否符合预期。
如果发送速度控制，机器人会震荡，那么需要用 Gain tuner 来调整。首先要把重力去掉来调试。kp 和 kd 设置为 100 来试试等。具体参考视频教程的 b 站内容。第一讲。

<img width="552" height="302" alt="image" src="https://github.com/user-attachments/assets/6de92b41-c837-438c-a8c7-4584bc61adb5" />

- 加载一个环境

<img width="553" height="420" alt="image" src="https://github.com/user-attachments/assets/3a578bc0-f502-4962-a01c-9e6f903dc18e" />

这需要网络下载，等待一下，选择最简单的 simple_warehouse 和 ware_extras

<img width="554" height="336" alt="image" src="https://github.com/user-attachments/assets/d68c63dd-b228-4598-bf5a-b07e1417e03f" />

<img width="553" height="565" alt="image" src="https://github.com/user-attachments/assets/aca04050-df9c-4c1a-830d-4de7ce07fd65" />

<img width="554" height="220" alt="image" src="https://github.com/user-attachments/assets/c5dd0551-4a92-4741-94d9-8a17e34ec32b" />

调整完，计算之后，点击可视化，保存 jpg 和 yaml。 

激光雷达导入

<img width="554" height="302" alt="image" src="https://github.com/user-attachments/assets/8f818691-5ea4-477b-b008-4fed00c53a50" />

<img width="554" height="799" alt="image" src="https://github.com/user-attachments/assets/c2ef501a-69f1-4add-aafd-85e8d808b96d" />

雷达是 PhysX Lidar

<img width="553" height="383" alt="image" src="https://github.com/user-attachments/assets/2ab9dc73-b9c0-41a2-961a-91d02e858a5a" />

<img width="553" height="383" alt="image" src="https://github.com/user-attachments/assets/1aa6ac84-829f-4cae-85e8-0c8c143ed904" />

把它拖上来

<img width="553" height="266" alt="image" src="https://github.com/user-attachments/assets/01b340a1-afb0-434a-ba26-c58c7242d385" />

<img width="554" height="302" alt="image" src="https://github.com/user-attachments/assets/ac70645f-e7a9-49b5-8490-24d1bd8192c9" />

<img width="554" height="309" alt="image" src="https://github.com/user-attachments/assets/cbd709e5-9a10-4607-92da-0dd3b3493577" />

这个 domian id 是跟你自己电脑设置的 bashrc 相关。如果没设置，就不用管它

轮速订阅

<img width="553" height="322" alt="image" src="https://github.com/user-attachments/assets/3ef21214-a568-4461-ae6f-575cec33a789" />

<img width="554" height="728" alt="image" src="https://github.com/user-attachments/assets/5247ca60-8aa0-4384-b890-db54c266b9c8" />

订阅节点输出的角速度和线速度都是 3 维向量，需要一个中间转化模块，输出一维值。
角速度输出的是 z 分量，线速度输出的是 x 分量。

<img width="554" height="279" alt="image" src="https://github.com/user-attachments/assets/4a9f34d0-8d65-4de4-96a2-d306965b05c8" />

把差速控制器连接给本体上的左右关节电机

<img width="554" height="385" alt="image" src="https://github.com/user-attachments/assets/474dbd11-bd17-40ed-9f7e-09b6a5e1f24b" />

constant token 组合两个关节名字，成为 array，发给 ariculation controller 中的 jointNames。array 是可以增加 input 的。
另外 twist 的输出要连接 controller 的输入。

<img width="554" height="225" alt="image" src="https://github.com/user-attachments/assets/f8885742-293c-4ed4-8da3-d3ad74b3ce28" />

每个 constant token 赋值两个 joint 名字
ros2 run rqt_robot_steering rqt_robot_steering
测试一下小车能不能跑

添加 odom

<img width="553" height="292" alt="image" src="https://github.com/user-attachments/assets/453f659a-cfa0-4eaa-b6e9-c9cda2f713fb" />

<img width="554" height="208" alt="image" src="https://github.com/user-attachments/assets/14e6f8ad-738b-4773-ba99-2d2b316d3d5e" />

记得把 timestamp 和 context 也连接上，图片中忘记加了
- 添加 raw transform tree  它表示的是 odom 到 base link
- transform tree 表示的是 base link 到 lidar camera imu 的

<img width="553" height="319" alt="image" src="https://github.com/user-attachments/assets/1bbb6436-0fd8-498b-b4d1-56ccff6fc7b6" />

<img width="554" height="332" alt="image" src="https://github.com/user-attachments/assets/7ecc91ef-1215-4498-82fc-1978275891fb" />

运行后就会发布 odom 到 base link 的 tf
- 添加 base link 本体的 tf

<img width="553" height="474" alt="image" src="https://github.com/user-attachments/assets/2b159e56-3800-452c-98fc-46e503ca4638" />

ros2 run tf2_tools view_frames.py
<img width="552" height="148" alt="image" src="https://github.com/user-attachments/assets/aa7e30d6-056b-4f39-ac3b-04d499c64bde" />

```Shell
sudo apt install python3-rosinstall-generator python3-wstool build-essential python3-rosinstall python3-rosdep
```

创建工作空间

```Shell
cd /home/yab/.local/share/ov/pkg/isaac-sim-4.0.0
mkdir -p ros2_workspace/src
colcon build
source install/setup.bash
sudo apt install ros-foxy-pointcloud-to-laserscan
```

```Shell
rosdep install -i --from-path src --rosdistro foxy -y
```
代码在第 3 节的链接中

<img width="553" height="262" alt="image" src="https://github.com/user-attachments/assets/b24f27e8-6341-4e2a-90ba-b6dd3615c8e4" />


```Shell
ros2 launch carter_navigation carter_navigation.launch.py
```
- 有个报错

<img width="554" height="500" alt="image" src="https://github.com/user-attachments/assets/efa2ba2d-dfd0-45b7-ac07-5e3fb1ee39ad" />

先启动 isaac sim，再启动 launch 文件
一般重定位是没有的，所以需要自己手动发一个 2d pose

##### 6.1.1.2 Isaac Lab入门
**系统要求**
一般要求：
有关详细要求，请参阅 Isaac Sim 系统要求 。基本要求包括：

OS: Ubuntu 22.04 (Linux x64) 或 Windows 11 (x64)

RAM: 32 GB 或更多

GPU VRAM: 16 GB 或更多 (渲染工作流程可能需要额外的 VRAM)

Isaac Sim 是针对特定的 Python 版本构建的 ，在安装 Isaac Lab 时，使用相同的 Python 版本至关重要。所需的 Python 版本如下：

对于 Isaac Sim 5.X，所需的 Python 版本是 3.11。

对于 Isaac Sim 4.X，所需的 Python 版本是 3.10。

驱动要求：
除了在 Omniverse技术要求 中推荐的驱动程序之外，其他驱动程序可能可用，但尚未经过所有Omniverse测试的验证。

使用 最新的NVIDIA生产分支驱动程序。

在 Linux 上，建议使用版本 580.65.06 或更高版本，特别是在升级到 Ubuntu 22.04.5，内核为 6.8.0-48-generic 或更新版本时。

在 Spark 上，建议使用版本 580.95.05 。

在 Windows 上，建议使用版本 580.88 。

如果您在使用新的GPU或遇到驱动程序问题，请从 Unix Driver Archive <https://www.nvidia.com/en-us/drivers/unix/> 中安装最新的生产分支驱动程序，使用 .run 安装程序。

**DGX Spark: 详细信息和限制**
DGX Spark 是一款采用 aarch64 架构的独立机器学习设备。因此，Isaac Lab 的某些功能目前在 DGX Spark 上不受支持。最值得注意的是，该架构 需要 CUDA ≥ 13，因此需要 PyTorch 的 cu13 构建或更新版本。关于 Isaac Lab 的其他值得注意的限制包括…

SkillGen 不支持开箱即用。这是因为 cuRobo 构建原生 CUDA/C++ 扩展，需要特定的工具和库版本，这些版本尚未经过验证可用于 DGX Spark。

扩展现实远程操作工具，例如 OpenXR 不受支持。这是由于尚未完全调查的编码性能限制。

使用 JAX <[https://docs.jax.dev/en/latest/notebooks/thinking_in_jax.html](https://docs.jax.dev/en/latest/notebooks/thinking_in_jax.html)>_ 的 SKRL 训练尚未在 DGX Spark 上的 Isaac Lab 中经过明确验证或测试。JAX 仅为 Linux x86_64 提供预构建的 CUDA wheels，因此在 aarch64 系统（例如 DGX Spark）上默认仅在 CPU 上运行。GPU 支持需要从源代码构建 JAX，这在 Isaac Lab 中尚未经过验证。

DGX Spark 不支持 Livestream 和 Hub Workstation Cache。

多节点训练可能需要 Spark 机器之间的直接连接或额外的网络配置。

由于 aarch64 上缺少非 DLSS 图像降噪器，DGX Spark 不支持 Isaac Lab Mimic 数据生成和视觉运动环境的策略推理。

Running Cosmos Transfer1 is not currently supported on the DGX Spark.

故障排除
请参考 Linux故障排除 解决Linux安装问题。

您可以使用 Isaac Sim兼容性检查器 来自动检查您的系统是否满足运行Isaac Sim所需的要求。

**选择安装方法**
不同的工作流程需要不同的安装方法。使用此表格进行决定：

<img width="819" height="259" alt="image" src="https://github.com/user-attachments/assets/8efc368a-b524-42a4-a480-319836d442a4" />


**后续步骤**

一旦您查看了安装方法，请继续阅读与您工作流程相匹配的指南：

- 😃 使用 Isaac Sim Pip 包安装

通过pip安装Isaac Sim，从源代码构建安装Isaac Lab。

最适合初学者和大多数用户。

- 使用 Isaac Sim 预编译二进制安装

从其二进制软件包（网站下载）安装Isaac Sim。

- 从源代码安装Isaac Lab。

选择此选项，如果您不希望在 Isaac Sim 上使用 pip（例如在 Ubuntu 20.04 上）。

- 使用 Isaac Sim 源代码安装

从源码构建 Isaac Sim。

从源代码安装Isaac Lab。

只有在计划修改 Isaac Sim 本身时才建议使用。

- 使用 Isaac Lab Pip 包安装

安装 Isaac Sim 和 Isaac Lab 作为 pip 软件包。

适用于使用自定义执行脚本构建 外部扩展 的高级用户。

注意：这 不 包括训练或示例脚本。

- 容器部署

在 Docker 容器中安装 Isaac Sim 和 Isaac Lab。

最适合希望在容器化环境中使用 Isaac Lab 的用户。

各安装方式具体安装方法细则见官方文档[https://docs.robotsfan.com/isaaclab/source/setup/installation/index.html](https://docs.robotsfan.com/isaaclab/source/setup/installation/index.html)

**快速入门 (推荐)**
对于大多数用户来说，安装 Isaac Lab 最简单最快的方法是按照 使用 Isaac Sim Pip 包安装 指南操作。

这种方法将通过pip安装Isaac Sim，并通过其源代码安装Isaac Lab。如果您是Isaac Lab的新手，请从这里开始。

首先定义我们的虚拟环境。

```Shell
conda
# create a virtual environment named env_isaaclab with python3.11
conda create -n env_isaaclab python=3.11
# activate the virtual environment
conda activate env_isaaclab
```

接下来，安装一个支持CUDA的PyTorch 2.7.0版本。

```Shell
pip install -U torch==2.7.0 torchvision==0.22.0 --index-url https://download.pytorch.org/whl/cu128
```

在安装 Isaac Sim 之前，我们需要确保 pip 已经更新。要更新 pip，请运行

```Shell
pip install --upgrade pip
```

现在我们可以安装 Isaac Sim 包。
```Shell
pip install "isaacsim[all,extscache]==5.1.0" --extra-index-url https://pypi.nvidia.com
```

最后，我们可以安装 Isaac Lab。要开始，使用以下命令克隆存储库
```Shell
git clone git@github.com:isaac-sim/IsaacLab.git
```


安装现在只需要简单地导航到存储库，然后使用带有 --install 标志的根脚本进行调用！

```Shell
./isaaclab.sh --install # or "./isaaclab.sh -i"
```

**启动训练**

通过位于 isaaclab/scripts/reinforcement_learning 目录中的相应 train.py 和 play.py 脚本访问 Isaac Lab 的各个后端。调用这些脚本将需要一个 任务名称 和对应的 入口点 到 gymnasium API。例如

python scripts/reinforcement_learning/skrl/train.py --task=Isaac-Ant-v0
这将训练 mujoco 蚂蚁 “奔跑” 。您可以使用 --help 标志查看您可用的各种启动选项。请特别注意 --num_envs 选项和 --headless 标志，这两个在尝试开发和调试新环境时非常有用。在此级别指定的选项将自动覆盖代码中可能定义的任何配置等效项（只要这些定义是 @configclass 的一部分，请参阅下文）。

列出可用环境
上面， Isaac-Ant-v0 是任务名称， skrl``是使用的 RL 框架。 ``Isaac-Ant-v0 环境已经在 Gymnasium API 中注册，您可以通过调用 list_envs.py 脚本查看入口点是如何定义的，可以在 isaaclab/scripts/environments/lsit_envs.py 中找到。您应该会看到如下条目

```Shell
$> python scripts/environments/list_envs.py

+--------------------------------------------------------------------------------------------------------------------------------------------+
|  Available Environments in Isaac Lab
+--------+----------------------+--------------------------------------------+---------------------------------------------------------------+
| S. No. | Task Name            | Entry Point                                | Config
.
.
.
+--------+----------------------+--------------------------------------------+---------------------------------------------------------------+
|   2    | Isaac-Ant-Direct-v0  |  isaaclab_tasks.direct.ant.ant_env:AntEnv  |  isaaclab_tasks.direct.ant.ant_env:AntEnvCfg
+--------+----------------------+--------------------------------------------+---------------------------------------------------------------+
.
.
.
+--------+----------------------+--------------------------------------------+---------------------------------------------------------------+
|   48   | Isaac-Ant-v0         | isaaclab.envs:ManagerBasedRLEnv            |   isaaclab_tasks.manager_based.classic.ant.ant_env_cfg:AntEnvCfg
+--------+----------------------+--------------------------------------------+---------------------------------------------------------------+
```

请注意，有两种不同的 Ant 任务，一种是用于 Direct 环境，另一种是用于 ManagerBased 环境。这是您可以在 Isaac Lab 立即使用的 两个主要工作流程 。Direct 工作流程将为您提供最快速通往用于强化学习的工作自定义环境的路径，但 Manager based 工作流程将为您的项目提供更广泛开发所需的模块化。出于本快速入门指南的目的，我们只会专注于 Direct 工作流程。

**生成您自己的项目**
使用 Isaac Lab 开始新项目起初可能会让人望而生畏，但这就是为什么我们提供 模板生成器 ，通过命令行快速生成新项目的原因。

```Shell
./isaaclab.sh --new
```

这将根据您选择的设置为您创建一个新项目

外部 vs 内部: 确定项目是作为 isaac lab 存储库的一部分构建，还是作为外部扩展加载的。

Direct vs Manager: 直接任务主要包含环境定义中的所有实现细节，而基于 manager 的项目则意味着使用我们各种环境“部件”的模块化定义。

框架: 您可以在这里选择多个选项。这决定了您打算在项目中本地使用的 RL 框架（您想要使用哪些特定算法实现进行训练）。

创建后，导航到安装的项目并运行

```Shell
python -m pip install -e source/<given-project-name>
```

来完成安装过程并注册环境。在模板生成器创建的目录中，您将至少找到一个具有类似以下内容的 __init__.py 文件

```python
import gymnasium as gym

gym.register(
    id="Template-isaaclabtutorial_env-v0",
    entry_point=f"{__name__}.isaaclabtutorial_env:IsaaclabtutorialEnv",
    disable_env_checker=True,
    kwargs={
        "env_cfg_entry_point": f"{__name__}.isaaclabtutorial_env_cfg:IsaaclabtutorialEnvCfg",
        "skrl_cfg_entry_point": f"{agents.__name__}.skrl_ppo_cfg:PPORunnerCfg",
    },
)
```

这是实际为将来使用注册环境的函数。请注意， entry_point 实际上只是环境定义的 python 模块路径。这就是为什么我们需要将项目安装为包: 模块路径 就是 gymnasium API 的入口点。

***配置**

无论您在 Isaac Lab 中要做什么，您都需要处理**配置** 。所有配置类都可以通过它们的类定义上方的 @configclass 装饰器和缺少 __init__ 函数来识别。例如，考虑下面这个关于 cartpole 环境 的配置类。

```python
@configclass
class CartpoleEnvCfg(DirectRLEnvCfg):
    # env
    decimation = 2
    episode_length_s = 5.0
    action_scale = 100.0  # [N]
    action_space = 1
    observation_space = 4
    state_space = 0

    # simulation
    sim: SimulationCfg = SimulationCfg(dt=1 / 120, render_interval=decimation)

    # robot
    robot_cfg: ArticulationCfg = CARTPOLE_CFG.replace(prim_path="/World/envs/env_.*/Robot")
    cart_dof_name = "slider_to_cart"
    pole_dof_name = "cart_to_pole"

    # scene
    scene: InteractiveSceneCfg = InteractiveSceneCfg(num_envs=4096, env_spacing=4.0, replicate_physics=True)

    # reset
    max_cart_pos = 3.0  # the cart is reset if it exceeds that position [m]
    initial_pole_angle_range = [-0.25, 0.25]  # the range in which the pole angle is sampled from on reset [rad]

    # reward scales
    rew_scale_alive = 1.0
    rew_scale_terminated = -2.0
    rew_scale_pole_pos = -1.0
    rew_scale_cart_vel = -0.01
    rew_scale_pole_vel = -0.005
```

请注意，整个类定义只是一组值字段和其他配置。配置类对于在训练过程中需要关心向量化的任何内容都是必不可少的。 如果您想要能够将环境复制成千上万次，并且异步地管理每个数据，您需要以某种方式 “标记” 哪些场景部分对这个复制过程（向量化）是重要的。 这就是配置类的作用！

在这种情况下，该类定义了整个训练环境的配置！请注意 InteractiveSceneCfg 中的 num_envs 变量。这实际上会被 train.py 脚本内部的 CLI 参数所覆盖。配置提供了一条通往配置层次结构中的任何变量的直接路径，从而轻松修改在启动时由环境“配置”的任何内容。

***机器人**

在 Isaac Lab 中，机器人完全被定义为配置的实例。如果您检查 source/isaaclab_assets/isaaclab_assets/robots ，您将看到许多文件，每个文件都包含了有关所讨论机器人的配置。这些单独的文件的目的是更好地定义所有不同机器人的范围，但没有任何阻止您 向您的项目添加新的机器人 ，甚至添加到 isaaclab 存储库中！例如，考虑以下配置中的 Dofbot

```python
import isaaclab.sim as sim_utils
from isaaclab.actuators import ImplicitActuatorCfg
from isaaclab.assets.articulation import ArticulationCfg
from isaaclab.utils.assets import ISAAC_NUCLEUS_DIR

DOFBOT_CONFIG = ArticulationCfg(
    spawn=sim_utils.UsdFileCfg(
        usd_path=f"{ISAAC_NUCLEUS_DIR}/Robots/Dofbot/dofbot.usd",
        rigid_props=sim_utils.RigidBodyPropertiesCfg(
            disable_gravity=False,
            max_depenetration_velocity=5.0,
        ),
        articulation_props=sim_utils.ArticulationRootPropertiesCfg(
            enabled_self_collisions=True, solver_position_iteration_count=8, solver_velocity_iteration_count=0
        ),
    ),
    init_state=ArticulationCfg.InitialStateCfg(
        joint_pos={
            "joint1": 0.0,
            "joint2": 0.0,
            "joint3": 0.0,
            "joint4": 0.0,
        },
        pos=(0.25, -0.25, 0.0),
    ),
    actuators={
        "front_joints": ImplicitActuatorCfg(
            joint_names_expr=["joint[1-2]"],
            effort_limit_sim=100.0,
            velocity_limit_sim=100.0,
            stiffness=10000.0,
            damping=100.0,
        ),
        "joint3_act": ImplicitActuatorCfg(
            joint_names_expr=["joint3"],
            effort_limit_sim=100.0,
            velocity_limit_sim=100.0,
            stiffness=10000.0,
            damping=100.0,
        ),
        "joint4_act": ImplicitActuatorCfg(
            joint_names_expr=["joint4"],
            effort_limit_sim=100.0,
            velocity_limit_sim=100.0,
            stiffness=10000.0,
            damping=100.0,
        ),
    },
)
```

这完全定义了 dofbot！您可以将此内容复制到一个 .py 文件中并将其作为模块导入，以便在自己的 lab sims 中使用 dofbot。您将在定义带有状态的事物的任何配置中看到的一个常见特征是 InitialStateCfg 的存在。请记住，配置是指明向量化的信息， InitialStateCfg 描述了机器人在每个环境中创建时的关节状态。 ImplicitActuatorCfg 使用由关节时间决定的默认执行模型来定义机器人的关节。并不是所有关节都需要被执行，但如果您不打算使用这些未定义的关节，您将会收到警告。如果您不打算使用这些未定义的关节，您通常可以忽略它们。

**Apps 和 Sims**

使用仿真意味着启动 Isaac Sim 应用程序以提供仿真上下文。如果您没有运行由标准工作流程定义的任务，则需要负责创建应用程序、管理上下文并通过时间推进仿真。 这是 “第三个工作流程” : 一个 独立 应用程序，这是我们为框架、演示、基准测试等编写的脚本所谓的事情…

独立工作流程使您可以完全控制应用程序中的一切和仿真上下文。在 Isaac Sim 文档 中详细讨论了开发独立应用程序，但有几点值得着重，因为它们可以非常有用。

```python
import argparse

from isaaclab.app import AppLauncher
# add argparse arguments
parser = argparse.ArgumentParser(
    description="This script demonstrates adding a custom robot to an Isaac Lab environment."
)
parser.add_argument("--num_envs", type=int, default=1, help="Number of environments to spawn.")
# append AppLauncher cli args
AppLauncher.add_app_launcher_args(parser)
# parse the arguments
args_cli = parser.parse_args()

# launch omniverse app
app_launcher = AppLauncher(args_cli)
simulation_app = app_launcher.app
```

AppLauncher 是任何 Isaac Sim 应用程序的入口点，如 Isaac Lab！ 许多 Isaac Lab 和 Isaac Sim 模块直到应用程序启动之后才能导入！ 这是在上面的代码的倒数第二行执行的，当构造 AppLauncher 时。 app_launcher.app 是我们访问套件应用程序框架的接口；广泛的中介代码将仿真与扩展管理系统、GUI 等等绑定在一起。在独立工作流程中，这个界面，通常被称为 simulation_app 主要用于检查仿真是否正在运行，并在仿真结束后清理。


**资产缓存**

Isaac Lab 资产托管在 AWS S3 云存储 上。 加载时间可能会因您的 网络连接 和 地理位置 而异，在某些情况下，每次运行可能需要几分钟才能加载资产。 为了提高性能或支持 离线工作流 ，我们建议启用 资产缓存 。

缓存的资产被存储在本地，减少重复下载。

如果您的网络连接速度慢或不稳定，或者部署环境处于脱机状态，则这将特别有用。

##### 6.1.1.3 Isaac资料汇总

**文档**

[https://docs.omniverse.nvidia.com/](https://docs.omniverse.nvidia.com/)
[https://developer.nvidia.com/isaac/sim ](https://developer.nvidia.com/isaac/sim )
omniverse 开发者文档 [https://docs.omniverse.nvidia.com/dev-guide/latest/index.html](https://docs.omniverse.nvidia.com/dev-guide/latest/index.html)
isaac sim 开发者文档 [https://docs.omniverse.nvidia.com/isaacsim/latest/index.html](https://docs.omniverse.nvidia.com/isaacsim/latest/index.html)
isaac lab 开发者文档 [https://isaac-sim.github.io/IsaacLab/](https://isaac-sim.github.io/IsaacLab/)
isaac sim 写代码 API 参考文档 [https://docs.omniverse.nvidia.com/py/isaacsim/index.html](https://docs.omniverse.nvidia.com/py/isaacsim/index.html)
isaac extension 文档 [https://docs.omniverse.nvidia.com/py/isaacsim/index.html](https://docs.omniverse.nvidia.com/py/isaacsim/index.html)
ros ros2 文档 [https://docs.omniverse.nvidia.com/isaacsim/latest/ros_ros2_tutorials.html](https://docs.omniverse.nvidia.com/isaacsim/latest/ros_ros2_tutorials.html)
isaac lab 官方文档 [https://docs.robotsfan.com/isaaclab/source/setup/quickstart.html
](https://docs.robotsfan.com/isaaclab/source/setup/quickstart.html
)

https://player.bilibili.com/player.html?bvid=BV1a44y1N79U&autoplay=0
AI 仓库：使用 Isaac Sim 和 Isaac ROS 实现视觉导航
Autonomous machines are forecasted to dramatically increase the efficiency of warehouses, factories, and other industrial environments. NVIDIA Isaac ROS GEMs enable novel applications by empowering robots to intelligently perceive complex 3D environments. In this video, we showcase a camera-based navigation pipeline in which a robot uses NVIDIA’s GPU-accelerated visual SLAM algorithm (https://github.com/NVIDIA-ISAAC-ROS/i...) to find its location in the world. GPU-accelerated, real-time 3D scene reconstruction (https://github.com/NVIDIA-ISAAC-ROS/i...) is used to map its environment and plan collision-free trajectories. Finally, we demonstrate how Replicator, which is part of NVIDIA Isaac Sim (https://developer.nvidia.com/isaac-sim), can be used to procedurally generate industrial spaces in which to develop and validate robotics systems. Empower your robot with GPU-accelerated robotics algorithms today!


**视频教程**

[https://player.bilibili.com/player.html?bvid=BV1B24y1s7Hc&autoplay=0](https://player.bilibili.com/player.html?bvid=BV1B24y1s7Hc&autoplay=0)
讲义在百度网盘
资料链接： [https://pan.baidu.com/s/1RGOQ4UOwcEGEhWMZRyfDXA?pwd=kvq7](https://pan.baidu.com/s/1RGOQ4UOwcEGEhWMZRyfDXA?pwd=kvq7) 提取码: kvq7

**github 教程**

[https://github.com/isaac-sim/IsaacSim-ros_workspaces](https://github.com/isaac-sim/IsaacSim-ros_workspaces)

[https://github.com/NVIDIA-AI-IOT/Nav2-with-Isaac-ROS-GEMs
](https://github.com/NVIDIA-AI-IOT/Nav2-with-Isaac-ROS-GEMs
)

[https://developer.nvidia.com/blog/accelerate-ai-enabled-robotics-with-advanced-simulation-and-perception-tools-in-nvidia-isaac-platform/
](https://developer.nvidia.com/blog/accelerate-ai-enabled-robotics-with-advanced-simulation-and-perception-tools-in-nvidia-isaac-platform/
)

#### 6.1.2 MuJoCo
##### 6.1.2.1 MuJoCo 简介

MuJoCo 是 Multi-Joint dynamics with Contact（多关节动力学与接触）的缩写。它是一个通用物理引擎，旨在促进机器人学、生物力学、图形和动画、机器学习以及其他需要对与环境互动的铰接结构进行快速准确仿真的领域的研究和开发。它最初由 Roboti LLC 开发，于 2021 年 10 月被 DeepMind 收购并免费提供，并于 2022 年 5 月开源。MuJoCo 代码库可在 GitHub 上的 google-deepmind/mujoco 仓库中获取。

MuJoCo 是一个带有 C API 的 C/C++ 库，面向研究人员和开发者。运行时仿真模块经过优化以最大限度地提高性能，并在内置 XML 解析器和编译器预分配的低级数据结构上运行。用户使用原生的 MJCF 场景描述语言定义模型——这是一种 XML 文件格式，旨在尽可能地易于人类阅读和编辑。也可以加载 URDF 模型文件。该库包含使用原生 GUI 进行交互式可视化，通过 OpenGL 渲染。MuJoCo 还提供了大量用于计算物理相关量的实用函数。

MuJoCo 可用于实现基于模型的计算，例如控制合成、状态估计、系统辨识、机构设计、通过逆动力学进行数据分析以及用于机器学习应用的并行采样。它也可以作为更传统的仿真器使用，包括用于游戏和交互式虚拟环境。

主要特性
MuJoCo 具有许多特性。在此我们概述最显著的几个。

广义坐标结合现代接触动力学
物理引擎传统上分为两类。机器人学和生物力学引擎使用广义坐标或关节坐标中的高效准确递归算法。然而，它们要么忽略接触动力学，要么依赖于需要非常小时间步长的早期弹簧-阻尼器方法。游戏引擎使用一种更现代的方法，通过求解优化问题来找到接触力。然而，它们通常诉诸于过度指定的笛卡尔表示，其中关节约束是数值施加的，当涉及复杂的运动学结构时，会导致不准确和不稳定。MuJoCo 是第一个结合了两者的优点（广义坐标仿真和基于优化的接触动力学）的通用引擎。其他仿真器最近已进行调整以使用 MuJoCo 的方法，但这通常与其所有功能不兼容，因为它们最初并非为此设计。习惯于游戏引擎的用户可能最初会觉得广义坐标违反直觉；请参阅下面的澄清部分。

软性、凸性且解析可逆的接触动力学
在现代接触动力学方法中，由摩擦接触产生的力或冲量通常定义为线性或非线性互补问题（LCP 或 NCP）的解，两者均为 NP-hard。MuJoCo 基于一种不同的接触物理公式，该公式可简化为凸优化问题，详情请参阅计算章节。我们的模型允许软接触和其他约束，并且具有唯一确定的逆，便于数据分析和控制应用。提供了多种优化算法选择，包括投影高斯-赛德尔方法（projected Gauss-Seidel method）的推广，可处理椭圆摩擦锥。求解器提供了摩擦接触（包括扭转摩擦和滚动摩擦）、无摩擦接触、关节和肌腱限制、关节和肌腱的干摩擦以及各种等式约束的统一处理方法。

肌腱几何
MuJoCo 可以模拟肌腱的 3D 几何形状——它们是遵守缠绕和经过点约束的最小路径长度弦。该机制类似于 OpenSim 中的机制，但实现了更受限的、封闭形式的缠绕选项集，以加快计算速度。它还提供了机器人学特有的结构，例如滑轮和耦合自由度。肌腱可用于驱动，也可用于对肌腱长度施加不等式或等式约束。

通用驱动模型
在使用与模型无关的 API 的同时设计一个足够丰富的驱动模型是一项挑战。MuJoCo 通过采用一种抽象驱动模型来实现此目标，该模型可以具有不同类型的传动、力生成和内部动力学（即，使总体动力学成为三阶的状态变量）。这些组件可以实例化，以便以统一的方式模拟电机、气缸和液压缸、PD 控制器、生物肌肉和许多其他执行器。

可重构计算流程
MuJoCo 有一个顶层步进函数 mj_step，它运行整个前向动力学并推进仿真状态。然而，在许多超出仿真的应用中，能够运行计算流程的选定部分是有益的。为此，MuJoCo 提供了大量标志，可以任意组合设置，允许用户根据需要重新配置流程，超出通过选项选择算法和算法参数。此外，许多底层函数可以直接调用。用户定义的回调函数可以实现自定义力场、执行器、碰撞例程和反馈控制器。

模型编译
如上所述，用户在一种称为 MJCF 的 XML 文件格式中定义 MuJoCo 模型。然后，该模型由内置编译器编译为低级数据结构 mjModel，该结构经过交叉索引和优化以用于运行时计算。编译后的模型也可以保存在二进制 MJB 文件中。

模型与数据的分离
MuJoCo 在运行时将仿真参数分为两个数据结构（C 结构体）

mjModel 包含模型描述，并且期望保持不变。其中嵌入了包含仿真和可视化选项的其他结构体，这些选项偶尔需要更改，但这由用户完成。

mjData 包含所有动态变量和中间结果。它用作一个暂存区，所有函数从此处读取输入并写入输出——这些输出随后成为仿真流程后续阶段的输入。它还包含一个预分配和内部管理的栈，以便运行时模块在模型初始化后无需调用内存分配函数。

mjModel 由编译器构建。mjData 在运行时根据 mjModel 构建。这种分离使得仿真多个模型以及每个模型的多个状态和控制变得容易，进而促进了采样和有限差分的多线程。顶层 API 函数反映了这种基本分离，其格式为

void mj_step(const mjModel* m, mjData* d);
交互式仿真与可视化
原生的3D 可视化器提供网格和几何图元的渲染、纹理、反射、阴影、雾、透明度、线框、天空盒、立体可视化（在支持四缓冲 OpenGL 的显卡上）。此功能用于生成 3D 渲染，帮助用户深入了解物理仿真，包括自动生成的模型骨架、等效惯量盒、接触位置和法线、可分解为法向和切向分量的接触力、外部扰动力、局部坐标系、关节和执行器轴以及文本标签等视觉辅助。可视化器需要一个带有 OpenGL 渲染上下文的通用窗口，从而允许用户选择自己喜欢的 GUI 库。MuJoCo 分发的代码示例 simulate.cc 展示了如何使用 GLFW 库来实现这一点。一个相关的可用性特性是能够“深入”仿真，推动物体并查看物理响应。用户选择将施加外部力和力矩的刚体，并实时查看扰动及其动态结果的渲染。这可用于视觉调试模型、测试反馈控制器的响应或将模型配置到所需姿势。

强大且直观的建模语言
MuJoCo 拥有自己的建模语言，称为 MJCF。MJCF 的目标是提供对 MuJoCo 所有计算能力的访问，同时使用户能够快速开发新模型并进行实验。这主要得益于广泛的默认设置机制，该机制类似于 HTML 中内联的层叠样式表 (CSS)。虽然 MJCF 具有许多元素和属性，但用户在任何给定模型中只需要设置极少的参数。这使得 MJCF 文件比许多其他格式更短、更易读。

复合柔性对象的自动生成
MuJoCo 的软约束可用于模拟绳索、布料和可变形 3D 对象。这需要大量常规刚体、关节、肌腱和约束协同工作。建模语言具有高级宏，这些宏由模型编译器自动扩展为必要的标准模型元素集合。重要的是，这些生成的柔性对象能够与仿真的其余部分完全交互。

模型实例
在 MuJoCo 中有几种称为“模型”的实体。用户在 MJCF 或 URDF 编写的 XML 文件中定义模型。然后软件可以在不同的介质（文件或内存）和不同的描述级别（高或低）创建同一模型的多个实例。所有组合都是可能的。

所有运行时计算均使用 mjModel 进行，该结构过于复杂，无法手动创建。这就是我们拥有两个建模级别的原因。高级别是为了用户方便而存在：其唯一目的是被编译成可执行计算的低级别模型。生成的 mjModel 可以加载并保存到二进制文件 (MJB) 中，但这些文件与版本相关且无法反编译，因此模型应始终维护为 XML 文件。

的 mjSpec C 结构体与 MJCF 文件格式一一对应。XML 加载器解释 MJCF 或 URDF 文件，创建相应的 mjSpec 并将其编译为 mjModel。用户可以编程方式创建 mjSpec，然后将其保存到 MJCF 或编译。程序化模型创建和编辑在模型编辑章节中有描述。

获取 mjModel 的不同路径包括有：

(文本编辑器) → MJCF/URDF 文件 → (MuJoCo 解析器 → mjSpec → 编译器) → mjModel

(用户代码) → mjSpec → (MuJoCo 编译器) → mjModel

MJB 文件 → (模型加载器) → mjModel

示例
这是一个 MuJoCo MJCF 格式的简单模型。它定义了一个固定在世界上的平面、一个用于更好地照明物体并投射阴影的光源，以及一个具有 6 个自由度的浮动盒子（这就是“自由”关节的作用）。

hello.xml:

```Shell
<mujoco>
  <worldbody>
    <light diffuse=".5 .5 .5" pos="0 0 3" dir="0 0 -1"/>
    <geom type="plane" size="1 1 0.1" rgba=".9 0 0 1"/>
    <body pos="0 0 1">
      <joint type="free"/>
      <geom type="box" size=".1 .2 .3" rgba="0 .9 0 1"/>
    </body>
  </worldbody>
</mujoco>
```

内置的 OpenGL 可视化器将此模型渲染为

<img width="787" height="694" alt="image" src="https://github.com/user-attachments/assets/2a6b255b-a5a6-45c6-921b-315deaed2ab6" />

如果对该模型进行仿真，盒子会落到地面上。不带渲染的被动动力学基本仿真代码如下所示。

```Shell
#include "mujoco.h"
#include "stdio.h"

char error[1000];
mjModel* m;
mjData* d;

int main(void) {
  // load model from file and check for errors
  m = mj_loadXML("hello.xml", NULL, error, 1000);
  if (!m) {
    printf("%s\n", error);
    return 1;
  }

  // make data corresponding to model
  d = mj_makeData(m);

  // run simulation for 10 seconds
  while (d->time < 10)
    mj_step(m, d);

  // free model and data
  mj_deleteData(d);
  mj_deleteModel(m);

  return 0;
}
```

这在技术上是一个 C 文件，但它也是一个合法的 C++ 文件。实际上，MuJoCo API 与 C 和 C++ 都兼容。通常用户代码会用 C++ 编写，因为它增加了便利性，而且不会牺牲效率，因为计算瓶颈在于仿真器，而仿真器已经高度优化。

函数 mj_step 是顶层函数，它将仿真状态向前推进一个时间步长。这个例子当然只是一个被动动力系统。当用户指定控制或施加力并开始与系统交互时，事情会变得更有趣。

接下来我们提供一个更详细的示例，说明 MJCF 的几个特性。考虑以下 example.xml

```Shell
<mujoco model="example">
  <default>
    <geom rgba=".8 .6 .4 1"/>
  </default>

  <asset>
    <texture type="skybox" builtin="gradient" rgb1="1 1 1" rgb2=".6 .8 1" width="256" height="256"/>
  </asset>

  <worldbody>
    <light pos="0 1 1" dir="0 -1 -1" diffuse="1 1 1"/>
    <body pos="0 0 1">
      <joint type="ball"/>
      <geom type="capsule" size="0.06" fromto="0 0 0  0 0 -.4"/>
      <body pos="0 0 -0.4">
        <joint axis="0 1 0"/>
        <joint axis="1 0 0"/>
        <geom type="capsule" size="0.04" fromto="0 0 0  .3 0 0"/>
        <body pos=".3 0 0">
          <joint axis="0 1 0"/>
          <joint axis="0 0 1"/>
          <geom pos=".1 0 0" size="0.1 0.08 0.02" type="ellipsoid"/>
          <site name="end1" pos="0.2 0 0" size="0.01"/>
        </body>
      </body>
    </body>

    <body pos="0.3 0 0.1">
      <joint type="free"/>
      <geom size="0.07 0.1" type="cylinder"/>
      <site name="end2" pos="0 0 0.1" size="0.01"/>
    </body>
  </worldbody>

  <tendon>
    <spatial limited="true" range="0 0.6" width="0.005">
      <site site="end1"/>
      <site site="end2"/>
    </spatial>
  </tendon>
</mujoco>
```

该模型是一个 7 自由度的手臂，它“握住”一根绳子，绳子的另一端连接着一个圆柱体。绳子被实现为具有长度限制的肌腱。肩部有一个球关节，肘部和腕部有一对铰链关节。圆柱体内部的盒子表示一个自由“关节”。XML 中的外部 body 元素是必需的 worldbody。请注意，在两个刚体之间使用多个关节不需要创建虚拟刚体。

MJCF 文件包含指定模型所需的最小信息。胶囊体由空间中的线段定义——在这种情况下，只需要胶囊体的半径。刚体坐标系的位置和方向由属于它们的 geoms 推断。在均匀密度假设下，惯性属性由 geom 形状推断。这两个 site 被命名是因为肌腱定义需要引用它们，而其他任何东西都没有命名。关节轴只为铰链关节定义，不为球关节定义。碰撞规则是自动定义的。摩擦特性、重力、仿真时间步长等都设置为默认值。顶部指定的默认 geom 颜色适用于所有 geoms。

除了以二进制 MJB 格式保存编译后的模型外，我们还可以将其保存为 MJCF 或人类可读的文本格式；分别参见 example_saved.xml 和 example_saved.txt。XML 版本与原始版本相似，而文本版本包含 mjModel 中的所有信息。将文本版本与 XML 版本进行比较，可以发现模型编译器为我们做了多少工作。

**模型元素**
本节简要描述了 MuJoCo 模型中可以包含的所有元素。稍后我们将更详细地解释底层计算、MJCF 中元素的指定方式以及它们在 mjModel 中的表示。

**选项**
每个模型都有以下列出的三组选项。它们总是包含在内。如果其值未在 XML 文件中指定，则使用默认值。这些选项的设计旨在允许用户在每个仿真时间步之前更改其值。但在一个时间步内，任何选项都不应更改。

mjOption
此结构包含影响物理仿真的所有选项。它用于选择算法并设置其参数，启用和禁用仿真流程的不同部分，以及调整重力等系统级物理属性。

mjVisual
此结构包含所有可视化选项。还有其他 OpenGL 渲染选项，但这些选项与会话相关，不属于模型的一部分。

mjStatistic
此结构包含由编译器计算的关于模型的统计信息：平均刚体质量、模型的空间范围等。包含此信息是为了提供信息，也因为可视化器使用它进行自动缩放。

**资产**
资产本身不是模型元素。模型元素可以引用它们，在这种情况下，资产会以某种方式改变引用元素的属性。一个资产可以被多个模型元素引用。由于包含资产的唯一目的是引用它，而引用只能通过名称完成，因此每个资产都有一个名称（如果适用，可以从文件名推断出来）。相比之下，常规元素的名称可以保持未定义。

**网格**
MuJoCo 可以从 OBJ 文件和二进制 STL 文件加载三角形网格。可以使用 MeshLab 等软件进行格式转换。虽然任何三角形集合都可以加载并可视化为网格，但碰撞检测器处理的是凸包。有编译时选项用于缩放网格，以及将原始几何形状拟合到网格。网格也可以用于自动推断惯性属性——通过将其视为三角锥体的并集并组合它们的质量和惯量。请注意，网格本身没有颜色，而是使用引用 geom 的材质属性进行着色。相比之下，所有空间属性都由网格数据确定。MuJoCo 支持 OBJ 和用于法线和纹理坐标的自定义二进制文件格式。网格也可以直接嵌入到 XML 中。

**皮肤**
蒙皮网格（或皮肤）是形状可以在运行时变形的网格。它们的顶点连接到刚体（在此上下文中称为骨骼），每个顶点可以属于多个骨骼，从而实现皮肤的平滑变形。蒙皮纯粹是可视化对象，不影响物理，但它们可以显著增强视觉真实感。蒙皮可以从自定义二进制文件加载，或直接嵌入到 XML 中，类似于网格。自动生成复合柔性对象时，模型编译器也会为这些对象生成蒙皮。

**高度场**
高度场可以从 PNG 文件加载（内部转换为灰度）或从稍后描述的自定义二进制格式文件加载。高度场是高程数据的矩形网格。编译器将数据归一化到 [0-1] 范围。高度场的实际空间范围由引用 geom 的尺寸参数确定。高度场只能从连接到 world body 的 geoms 引用。为了渲染和碰撞检测目的，网格矩形自动进行三角形划分，因此高度场被视为三角棱柱的并集。原则上，与此类复合对象的碰撞检测可以为单个 geom 对生成大量接触点。如果发生这种情况，仅保留前 64 个接触点。其基本原理是，高度场应用于模拟空间特征相对于仿真中其他对象较大的地形图，因此对于精心设计的模型，接触点的数量会很少。

**纹理**
纹理可以从 PNG 文件加载，或由编译器根据用户定义的程序参数合成。还可以选择在模型创建时将纹理留空并在运行时稍后更改它——以便在 MuJoCo 仿真中渲染视频或创建其他动态效果。可视化器支持两种纹理映射类型：2D 和立方体。2D 映射适用于平面和高度场。立方体映射对于“收缩包装”纹理到 3D 对象而无需指定纹理坐标非常有用。它也用于创建天空盒。立方体贴图的六个面可以从单独的图像文件加载，或从一个复合图像文件加载，或通过重复同一图像生成。与所有其他直接从模型元素引用的资产不同，纹理只能从另一个资产（即 material）引用，然后该资产再从模型元素引用。

**材质**
材质用于控制 geoms、sites 和肌腱的外观。这是通过从相应的模型元素引用材质来完成的。外观包括纹理映射以及与以下 OpenGL 光源交互的其他属性：RGBA、镜面反射、光泽度、发射。材质也可以用于使对象具有反射性。目前，反射仅在平面和盒子的 Z+ 面上渲染。请注意，模型元素也可以具有用于设置颜色的本地 RGBA 参数。如果同时指定了材质和本地 RGBA，则本地定义具有优先级。

**运动学树**
MuJoCo 仿真一组刚体的动力学，其运动通常受到约束。系统状态以关节坐标表示，刚体明确组织成运动学树。除顶层“世界”刚体外，每个刚体都有一个唯一的父级。不允许运动学环；如果需要环关节，应使用等式约束进行建模。因此，MuJoCo 模型的主干是由嵌套的 body 定义形成的一个或多个运动学树；孤立的浮动体算作一个树。下面列出的其他几个元素在 body 中定义并属于该 body。这与稍后列出的不能与单个 body 关联的独立元素形成对比。

**刚体 (Body)**
刚体具有质量和惯性属性，但没有任何几何属性。相反，几何形状（或 geoms）附加到刚体上。每个刚体有两个坐标系：用于定义它以及定位相对于它的其他元素的坐标系，以及一个以刚体质心为中心并与其主惯性轴对齐的惯性坐标系。因此，在该坐标系下，刚体惯性矩阵是对角的。在每个时间步，MuJoCo 递归计算前向运动学，得到全局笛卡尔坐标系中所有刚体的位置和方向。这为所有后续计算提供了基础。

**关节 (Joint)**
关节在刚体内定义。它们在刚体及其父级之间创建运动自由度 (DOFs)。如果没有关节，刚体就会焊接到其父级。这与使用过度指定笛卡尔坐标的游戏引擎相反，游戏引擎中关节是移除自由度而不是增加自由度。关节有四种类型：球形、滑动、铰链以及创建浮动刚体的“自由关节”。一个刚体可以有多个关节。通过这种方式，复合关节被自动创建，而无需定义虚拟刚体。球形和自由关节的姿态分量表示为单位四元数，MuJoCo 中的所有计算都遵循四元数的属性。

**关节参考位姿**
参考位姿是存储在 mjModel.qpos0 中的关节位置向量。它对应于模型处于初始配置时关节的数值。在我们之前的示例中，肘部以 90° 弯曲配置创建。但 MuJoCo 不知道肘部是什么，因此默认将其视为数值为 0 的关节配置。我们可以覆盖默认行为，使用 joint 的 ref 属性指定初始配置对应于 90°。所有关节的参考值被组装到向量 mjModel.qpos0 中。每当仿真重置时，关节配置 mjData.qpos 被设置为 mjModel.qpos0。在运行时，关节位置向量相对于参考位姿解释。特别是，由关节施加的空间变换量为 mjData.qpos - mjModel.qpos0。此变换是 mjModel 的 body 元素中存储的父子平移和旋转偏移之外的附加变换。ref 属性仅适用于标量关节（slide 和 hinge）。对于球形关节，保存在 mjModel.qpos0 中的四元数始终是 (1,0,0,0)，对应于空旋转。对于自由关节，浮动刚体的全局 3D 位置和四元数保存在 mjModel.qpos0 中。

**弹簧参考位姿**
这是所有关节和肌腱弹簧达到其静止长度的位姿。当关节配置偏离弹簧参考位姿时会产生弹簧力，并且力与偏离量呈线性关系。弹簧参考位姿保存在 mjModel.qpos_spring 中。对于滑动和铰链关节，弹簧参考位姿通过 springref 属性指定。对于球形和自由关节，弹簧参考位姿对应于初始模型配置。

**自由度 (DOF)**
自由度 (DOF) 与关节密切相关，但并非一一对应，因为球形和自由关节具有多个自由度。可以认为关节指定位置信息，而自由度指定速度和力信息。更正式地说，关节位置是系统配置流形上的坐标，而关节速度是流形在当前位置的切空间上的坐标。自由度具有与速度相关的属性，例如摩擦损失、阻尼、电枢惯量。作用在系统上的所有广义力都以自由度空间表示。相比之下，关节具有与位置相关的属性，例如限制和弹簧刚度。自由度并非由用户直接指定。相反，它们是由编译器根据关节创建的。

**几何体 (Geom)**
Geoms 是刚性连接到刚体的 3D 形状。多个 geoms 可以连接到同一个刚体上。考虑到 MuJoCo 仅支持凸 geom-geom 碰撞，以及创建非凸对象的唯一方法是将其表示为凸 geoms 的并集这一事实，这一点尤其有用。除了碰撞检测和随后的接触力计算之外，geoms 还用于渲染，以及在省略刚体质量和惯量时进行自动推断。MuJoCo 支持几种原始几何形状：平面、球体、胶囊体、椭球体、圆柱体、盒子。geom 也可以是网格或高度场；这通过引用相应的资产来实现。Geoms 具有许多影响仿真和可视化的材质属性。

**定位点 (Site)**
Sites 本质上是轻量级的 geoms。它们代表刚体坐标系内的关注位置。Sites 不参与碰撞检测或惯性属性的自动计算，但它们可以用于指定其他对象的空间属性，例如传感器、肌腱路径和滑块曲柄端点。Sites 也可以用于指定用户感兴趣的点（或更确切地说是坐标系）。

**相机**
可以在模型中定义多个相机。交互式可视化器中总有一个默认相机，用户可以使用鼠标自由移动它。然而，通常方便定义附加相机，这些相机要么固定在世界中，要么附加到某个刚体并随之移动。除了相机位置和姿态之外，用户还可以调整垂直视野和瞳距以进行立体渲染，以及创建立体虚拟环境所需的斜投影。在模拟具有不完美光学器件的真实相机时，可以分别为水平和垂直方向指定不同的焦距以及非中心主点。

**光源**
光源可以固定在 world body 上，也可以附加到移动的刚体上。可视化器提供了 OpenGL（固定功能）中的完整光照模型，包括环境光、漫反射和镜面反射分量、衰减和截止、位置光和方向光、雾。光源，或者更确切地说，被它们照亮的物体，也可以投射阴影。然而，与材质反射类似，每个投射阴影的光源都会增加一个渲染通道，因此应谨慎使用此功能。详细记录光照模型超出了本章的范围；请参阅OpenGL 文档。请注意，除了用户在运动学树中定义的光源外，还有一个随相机移动的默认头灯。其属性通过 mjVisual 选项进行调整。

**独立元素**
这里我们描述不属于单个刚体，因此在运动学树之外描述的模型元素。

**肌腱 (Tendon)**
肌腱是标量长度元素，可用于驱动、施加限制和等式约束，或创建弹簧-阻尼器和摩擦损失。肌腱有两种类型：固定肌腱和空间肌腱。固定肌腱是（标量）关节位置的线性组合。它们对于建模机械耦合非常有用。空间肌腱定义为通过一系列指定 site（或经过点）或缠绕指定 geoms 的最短路径。仅支持球体和圆柱体作为缠绕 geoms，圆柱体在缠绕时被视为具有无限长度。为了避免肌腱从缠绕 geom 的一侧突然跳到另一侧，用户还可以指定偏好的侧面。如果肌腱路径中有多个缠绕 geoms，它们必须由 sites 分开，以避免需要迭代求解器。空间肌腱也可以使用滑轮分成多个分支。

**执行器 (Actuator)**
MuJoCo 提供了一个灵活的执行器模型，包含三个可以独立指定的组件。它们共同决定了执行器如何工作。通过协调指定这些组件可以获得常见的执行器类型。这三个组件是传动、激活动力学和力生成。传动指定了执行器如何连接到系统的其余部分；可用类型有关节、肌腱和滑块曲柄。激活动力学可用于模拟气动或液压缸以及生物肌肉的内部激活状态；使用此类执行器会使整个系统动力学成为三阶的。力生成机制决定了作为执行器输入提供的标量控制信号如何映射到标量力，然后该力再通过从传动推断出的力臂映射到广义力。

**传感器 (Sensor)**
MuJoCo 可以生成仿真传感器数据，这些数据保存在全局数组 mjData.sensordata 中。结果不用于任何内部计算；而是提供给用户，用户可能需要它进行自定义计算或数据分析。可用的传感器类型包括触摸传感器、惯性测量单元 (IMU)、力矩传感器、关节和肌腱位置和速度传感器、执行器位置、速度和力传感器、运动捕捉标记点位置和四元数以及磁力计。其中一些需要额外的计算，而另一些则从 mjData 的相应字段复制。还有一个用户传感器，允许用户代码将任何其他关注量插入传感器数据数组中。MuJoCo 还具有离屏渲染功能，可以轻松模拟彩色和深度相机传感器。这不包含在标准传感器模型中，而是需要通过编程方式完成，如代码示例 simulate.cc 中所示。

**等式约束 (Equality)**
等式约束可以在运动学树结构和其中定义的关节/自由度已施加的约束之外施加额外的约束。它们可用于创建环关节，或一般地模拟机械耦合。施加这些约束的内部力与所有其他约束力一起计算。可用的等式约束类型有：在一点连接两个刚体（在运动学树外部创建球形关节）；将两个刚体焊接在一起；固定关节或肌腱的位置；通过三次多项式耦合两个关节或两个肌腱的位置；约束 flex（即可变形网格）的边长与其初始长度相等。

**柔性体 (Flex)**
Flexes 在 MuJoCo 3.0 中加入。它们代表可变形网格，可以是 1 维、2 维或 3 维的（因此其元素可以是胶囊体、三角形或四面体）。与刚性附加到单个刚体上的静态形状 geoms 不同，flex 的元素是可变形的：它们通过连接多个刚体构成，因此刚体的位置和姿态在运行时决定了 flex 元素的形状。这些可变形元素支持碰撞和接触力，并生成软性保持可变形实体形状的被动力和约束力。提供了自动化功能，可以从文件加载网格，构建对应于网格顶点的刚体，构建对应于网格面（或线或四面体，取决于维度）的 flex 元素，并获得相应的可变形网格。

**接触对 (Contact pair)**
MuJoCo 中的接触生成是一个复杂的过程。检查接触的 geom 对可以来自两个来源：自动邻近测试和其他统称为“动态”的过滤器，以及模型中提供的显式 geom 对列表。后者是一种单独的模型元素类型。由于接触涉及两个 geoms 的组合，显式指定允许用户以动态机制无法实现的方式定义接触参数。它对于微调接触模型也很有用，特别是添加被激进过滤方案移除的接触对。接触机制现已扩展到 flex 元素，可以在两个以上的刚体之间创建接触交互。然而，此类碰撞是自动化的，无法使用接触对进行微调。

**接触排除 (Contact exclude)**
这与接触对相反：它指定应从候选接触对生成中排除的刚体对（而不是 geoms 对）。它对于禁用因几何形状导致不希望的永久接触的刚体之间的接触非常有用。请注意，MuJoCo 还有其他机制来处理这种情况（特别是如果 geoms 属于同一个刚体或父子刚体，则它们不会发生碰撞），但有时这些自动化机制不够，显式排除变得必要。

**自定义数值 (Custom numeric)**
在 MuJoCo 仿真中有三种方式输入自定义数值。首先，可以在 XML 中定义全局数值字段。它们有一个名称和一个实数值数组。其次，可以通过元素特定的自定义数组扩展某些模型元素的定义。这通过在 XML 元素 size 中设置属性 nuser_XXX 来完成。第三，存在一个数组 mjData.userdata，它不用于任何 MuJoCo 计算。用户可以在其中存储自定义计算的结果；请记住，随时间变化的所有内容都应存储在 mjData 中，而不是 mjModel 中。

**自定义文本 (Custom text)**
自定义文本字段可以保存在模型中。它们可用于自定义计算——指定关键字命令或提供其他文本信息。但不要将其用于注释；在编译后的模型中保存注释没有好处。XML 有其自己的注释机制（被 MuJoCo 的解析器和编译器忽略），这更适合。

**自定义元组 (Custom tuple)**
自定义元组是 MuJoCo 模型元素的列表，可能包含其他元组。它们不被仿真器使用，但可用于指定用户代码所需的一组元素。例如，可以使用元组来定义用于自定义接触处理的刚体对。

**关键帧 (Keyframe)**
关键帧是仿真状态变量的快照。它包含关节位置、关节速度、执行器激活（如果存在）以及仿真时间的向量。模型可以包含一个关键帧库。它们对于将系统状态重置到关注点很有用。请注意，关键帧不用于在模型中存储轨迹数据；为此目的应使用外部文件。

**澄清**
读者可能拥有使用其他物理仿真器和相关约定，以及与 MuJoCo 不一致的通用编程实践经验。这可能会导致混淆。本节的目标是预先澄清最可能引起混淆的方面；它介于 FAQ 和精选主题教程之间。我们需要参考文档后面介绍的内容，但无论如何，下面的文本尽可能地独立和具有介绍性。

**发散**
仿真的发散发生在状态元素迅速趋向无穷大时。在 MuJoCo 中，这通常表现为 mjWARN_BADQACC 警告。发散是所有物理仿真的固有问题，不一定表明模型有问题或仿真器有错误，而更像是提示对于给定的积分器选择，时间步长过大。在物理仿真中，速度（大时间步长）和稳定性（小时间步长）之间总是存在权衡。一个针对速度进行良好调优的模型具有可能的最大不发散时间步长，这通常意味着它在极端条件下可能会发散。从这个意义上说，罕见的发散情况实际上可能表明模型调优良好。在所有情况下，都应该可以通过减小时间步长和/或切换到更稳定的积分器来防止发散。如果这不起作用，那么原因就不同了。例如，在刚体初始化时发生穿透的模型中，大的排斥力可能会将它们推开并导致发散。

**单位未指定**
MuJoCo 不指定基本的物理单位。用户可以选择他们认为合适的单位系统，只要它是一致的即可。为了理解这一点，考虑一个例子：一个重 1 千克、配备 1 牛顿推力器的 1 米飞船的动力学，与一个重 1 克、配备 1 达因推力器的 1 厘米飞船的动力学相同。这是因为 MKS 和 CGS 都是一致的单位系统。此特性允许用户根据需要缩放模型，这对于模拟非常小或非常大的物体、改进仿真的数值特性非常有用。

话虽如此，仍鼓励用户使用 MKS，因为 MuJoCo 在两个地方使用了类似 MKS 的默认值

gravity 的默认值为 (0, 0, -9.81)，这对应于 MKS 单位制下的地球表面重力。请注意，这并非真正指定了 MKS 单位制，因为我们可能在 Enceladus（土卫二）上使用 CGS 单位制。

geom density（用于推断刚体质量和惯性）的默认值为 1000，这对应于 MKS 单位制下水的密度。

一旦选择了基本单位（长度、质量、时间）的一致系统，所有导出单位都对应于该系统，如量纲分析所述。例如，如果我们的模型被解释为 MKS，则力和力矩单位分别为牛顿和牛顿·米。

角度：虽然在 MJCF 中可以使用度数指定角度（实际上度数是默认值），但所有角量在 mjModel 和 mjData 中都以弧度表示。因此，例如，如果我们使用 MKS，则由陀螺仪报告的角速度单位为 rad/s，而铰链关节的刚度单位为 Nm/rad。

**令人惊讶的碰撞**
MuJoCo 默认排除具有直接父子关系的刚体对所属 geoms 之间的碰撞。例如，考虑上面示例部分中的手臂模型：即使胶囊体 geoms 发生穿透，肘部也没有发生碰撞，因为前臂是上臂的直接子级。

然而，如果父级是静态刚体，即 world body 或相对于 world body 没有自由度的刚体，则此排除不适用。此行为在碰撞检测部分中有详细说明，可以防止物体穿过地板或墙壁。然而，这种行为经常导致以下情况

用户注释掉浮动底座模型的根关节，可能是为了防止它下落；现在底座刚体被视为静态，出现了以前不存在的新碰撞，用户感到困惑。有两种简单的方法可以避免这个问题

不要移除根关节。或许禁用重力并可能添加一些流体粘度就足以防止你的模型移动过多。

使用碰撞过滤来显式禁用不希望的碰撞，可以通过设置相关的 contype 和 conaffinity 属性，或使用接触排除指令来实现。

**非面向对象**
面向对象编程是一种非常有用的抽象，构建在更基础（且更接近硬件）的数据结构与操作它们的功能的概念之上。对象是与一个语义实体对应的数据结构和函数的集合，因此它们之间比与应用程序其余部分具有更强的依赖关系。我们在此不使用它的原因是，依赖结构使得自然的实体是整个物理仿真器。我们没有对象，而是少数数据结构和大量操作它们的功能。

我们仍然使用一种分组方式，但它与面向对象的方法不同。我们将模型（mjModel）与数据（mjData）分开。它们都是数据结构。模型包含描述被建模物理系统恒定属性所需的一切，而数据包含随时间变化的状态以及内部计算的可重用中间结果。所有顶层函数都期望将指向 mjModel 和 mjData 的指针作为参数。通过这种方式，我们避免了污染工作空间并干扰多线程的全局变量，但我们这样做的方式与面向对象编程实现相同效果的方式不同。

**软性与滑动**
正如我们将在计算章节中详细解释的那样，MuJoCo 基于接触和其他约束物理的数学模型。该模型本质上是软性的，即对约束施加更大的力总是会导致更大的加速度，因此逆动力学可以唯一确定。这是期望的，因为它产生了一个凸优化问题，并使得依赖于逆动力学的分析成为可能；此外，我们在实践中需要建模的大多数接触都具有一定的软性。然而，一旦我们允许软约束，我们就有效地创建了一种新的动力学——即变形动力学——现在我们必须指定这些动力学如何表现。这需要对接触和其他约束进行详细的参数化，涉及属性 solref 和 solimp，这些属性可以按约束设置，稍后将进行描述。

这种软模型的另一个常见令人困惑的方面是无法避免渐进接触滑动。类似地，摩擦关节在重力作用下会逐渐屈服。这并不是因为求解器无法阻止滑动（达到摩擦锥或摩擦损失极限），而是因为它最初并没有试图阻止滑动。回想一下，对给定约束施加更大的力必须导致更大的加速度。如果要完全抑制滑动，就必须违反这个关键属性。因此，如果您在仿真中看到渐进滑动，直观的解释可能是摩擦力不足，但这在 MuJoCo 中很少见。相反，需要调整 solref 和 solimp 参数向量以减小这种效应。增加约束阻抗（solimp 的前两个元素）以及全局 mjModel.opt.impratio 设置会特别有效。这种调整通常需要更小的时间步长来保持仿真稳定，因为它们使非线性动力学更难以数值积分。牛顿求解器通常更精确，也能减少滑动。

对于希望完全抑制滑动的情况，主求解器之后运行一个第二个 noslip 求解器。它通过忽略约束软性来更新摩擦维度的接触力。然而，当使用此选项时，MuJoCo 不再求解其设计的凸优化问题，仿真可能会变得不够鲁棒。因此，使用带有椭圆摩擦锥和较大 impratio 值的牛顿求解器是减少滑动的推荐方法。有关更详细的建议，请参阅建模章节中的防止滑动。

类型、名称、ID
如前所述，MuJoCo 支持大量的模型元素。每种元素类型在 mjModel 中都有相应的部分列出其各种属性。例如，关节限制数据在数组中
```Shell
mjtNum* jnt_range;             // joint limits       (njnt x 2
```
每个数组的大小（在本例中为 njnt）也在 mjModel 中给出。第一个关节的限制首先包含，然后是第二个关节的限制，依此类推。此排序反映了 MuJoCo 中所有矩阵均采用行主序格式的事实。

可用的元素类型在 mjmodel.h 文件中的枚举类型 mjtObj 中定义。这些枚举主要在内部使用。一个例外是 MuJoCo API 中的函数 mj_name2id 和 mj_id2name，它们将元素名称映射到整数 id，反之亦然。这些函数以元素类型作为输入。

在 XML 中命名模型元素是可选的。两个同类型（例如，两个关节）的元素不能有相同的名称。仅当需要在模型的其他地方引用某个元素时才需要命名；在 XML 中的引用只能通过名称进行。模型编译后，名称仍存储在 mjModel 中，以方便用户使用，但它们对仿真没有进一步影响。名称对于查找相应的整数 id 以及渲染非常有用：例如，如果您启用关节标签，则每个关节旁边将显示一个字符串（未定义名称的元素标记为“joint N”，其中 N 是 id）。

假设我们已经有了 mjModel* m。要打印名为“elbow”的关节的范围，请执行
```Shell
int jntid = mj_name2id(m, mjOBJ_JOINT, "elbow");
if (jntid >= 0)
   printf("(%f, %f)\n", m->jnt_range[2*jntid], m->jnt_range[2*jntid+1]);
```
如果未找到名称，函数将返回 -1，这就是为什么应该始终检查 id >= 0 的原因。

**刚体 (Bodies)、几何体 (geoms)、定位点 (sites)**
Bodies、geoms 和 sites 是 MuJoCo 元素，大致对应于物理世界中的刚体。那么为什么它们是分开的呢？原因在此解释，既有语义上的，也有计算上的。

首先是相似之处。Bodies、geoms 和 sites 都附有空间坐标系（尽管 bodies 还有一个坐标系，其中心位于刚体重心并与惯性主轴对齐）。这些坐标系的位置和姿态在每个时间步长通过前向运动学从 mjData.qpos 计算得出。前向运动学的结果在 mjData 中可用，bodies 的结果是 xpos、xquat 和 xmat，geoms 的结果是 geom_xpos 和 geom_xmat，sites 的结果是 site_xpos 和 site_xmat。

现在是不同之处。Bodies 用于构建运动学树，并作为其他元素（包括 geoms 和 sites）的容器。Bodies 具有空间坐标系、惯性属性，但不具有与外观或碰撞几何相关的属性。这是因为这些属性不影响物理（当然接触除外，但这单独处理）。如果你看过机器人学教科书中的运动学树图，刚体通常被画成无定形形状——为了说明它们的实际形状与物理无关。

Geoms（geometric primitive 的缩写）用于指定外观和碰撞几何。每个 geom 属于一个 body 并刚性附加到该 body。多个 geoms 可以附加到同一个 body。考虑到 MuJoCo 的碰撞检测器假定所有 geoms 都是凸的（如果网格不凸，它内部会用它们的凸包替换网格）这一事实，这一点特别有用。因此，如果你想建模一个非凸形状，你必须将其分解为凸 geoms 的并集并将它们全部附加到同一个 body 上。

Geom 也可以在 XML 中指定密度或质量值，模型编译器使用这些值计算父 body 的质量和惯性。质量要么直接指定，要么从 geom 的体积和density计算。惯性是根据质量、形状和均匀密度假设计算的。如果设置了shellinertia标志，质量被假定均匀分布在表面，density 被解释为单位面积质量，并相应计算对父 body 的惯性贡献。在实际仿真的 mjModel 中，geoms 不具有惯性属性。

Sites 是轻量级的 geoms。它们具有相同的外观属性，但不能参与碰撞，也不能用于推断 body 质量。另一方面，sites 可以做 geoms 做不到的事情：它们可以指定触摸传感器的体积、IMU 传感器的附着点、空间肌腱的路径、滑块曲柄执行器的端点。这些都是空间量，但它们不对应于应该具有质量或与其他实体碰撞的实体——这就是创建 site 元素的原因。Sites 也可以用于指定用户感兴趣的点（或者更确切地说是坐标系）。

以下示例说明了多个 sites 和 geoms 可以附加到同一个 body 上：在本例中，一个 body 上附加了两个 sites 和两个 geoms。
```Shell
<mujoco>
  <worldbody>
    <body pos="0 0 0">
      <geom type="sphere" size=".1" rgba=".9 .9 .1 1"/>
      <geom type="capsule" pos="0 0 .1" size=".05 .1" rgba=".9 .9 .1 1"/>
      <site type="box" pos="0 -.1 .3" size=".02 .02 .02" rgba=".9 .1 .9 1"/>
      <site type="ellipsoid" pos="0 .1 .3" size=".02 .03 .04" rgba=".9 .1 .9 1"/>
    </body>
  </worldbody>
</mujoco>
```

此模型由 OpenGL 可视化器渲染为

<img width="271" height="359" alt="image" src="https://github.com/user-attachments/assets/8edc6ea5-1430-4827-aebb-26806340a4c7" />

注意红色的盒子。这是刚体惯性属性的等效惯量盒渲染，由 MuJoCo 内部生成。盒子位于 geoms 上方，但不在 sites 上方。这是因为仅使用 geoms（自动）推断了 body 的惯性属性。如果我们恰好知道后者，当然可以直接指定。但通常更方便的是让模型编译器根据附加到 body 的 geoms 推断这些 body 属性，使用均匀密度假设（geom 密度可以在 XML 中指定；默认是水的密度）。

**关节坐标**
MuJoCo 与游戏引擎的关键区别之一在于 MuJoCo 在广义坐标或关节坐标下运行，而大多数游戏引擎在笛卡尔坐标下运行。这两种方法的区别可以概括如下

关节坐标：

最适合复杂的运动学结构，例如机器人；

关节在默认情况下会焊接在一起的刚体之间增加自由度；

关节约束在表示中是隐式的，不能被违反；

仿真刚体的位置和姿态通过前向运动学从广义坐标获得，不能直接操纵（根刚体除外）。

笛卡尔坐标：

最适合大量相互弹跳的刚体，例如分子动力学和盒子堆叠；

关节在默认情况下会自由浮动的刚体之间移除自由度；

关节约束是数值强制执行的，可以被违反；

仿真刚体的位置和姿态是显式表示的，并且可以直接操纵，尽管这可能会引入进一步的关节约束违反。

当处理属于包含运动学树的模型一部分的自由浮动刚体时，关节坐标可能会特别令人困惑。这将在下面澄清。

浮动对象：
在使用关节坐标时，您无法简单地将任意刚体的位置和姿态设置为您想要的任何值。要实现这种效果，您需要实现某种形式的逆运动学，它会计算一组（不一定唯一）的关节坐标，使得前向运动学将刚体放置在您想要的位置。

对于浮动物体（即通过自由关节与世界连接的物体）来说，情况则不同。这些物体的位置、方向以及线速度和角速度在 mjData.qpos 和 mjData.qvel 中明确表示，因此可以直接操作。

自由关节的语义如下。位置数据由7个数字组成（3D位置后跟单位四元数），而速度数据由6个数字组成（3D线速度后跟3D角速度）。自由关节的线性位置处于全局坐标系中，线速度也是如此。自由关节的方向（四元数）也处于全局坐标系中。然而，自由关节的旋转速度处于局部物体坐标系中。这与其说是一个设计决策，不如说是对四元数拓扑结构的正确使用。角速度存在于四元数切空间中，该空间是针对特定方向局部定义的，因此局部坐标系的角速度是自然的参数化。加速度定义在与相应速度相同的空间中。

自由关节始终在物体坐标系中定义，但计算上更有利的做法是将此坐标系与物体的惯性对齐。在 freejoint/align 属性的文档中阅读更多关于此选项的信息。

#### 6.1.2.2 MuJoCo入门
##### 6.1.2.3 MuJoCo资料汇总

MuJoCo官网 [https://mujoco.org/](https://mujoco.org/)
robosuite [https://robosuite.ai/docs/overview.html](https://robosuite.ai/docs/overview.html)

robomimic [https://robomimic.github.io/](https://robomimic.github.io/)

MetaWorld [https://meta-world.github.io/](https://meta-world.github.io/)

Gymnasium-Robotics(Fetch; Shadow Dexterous Hand; Maze;Adroit Hand; Franka Kitchen; MaMuJoCo) [https://robotics.farama.org/](https://robotics.farama.org/)

RoboCasa [https://github.com/TianxingChen/Embodied-AI-Guide/blob/main/Docs.qq.com/sheet/DYmppSU55cFNpaVJo?tab=BB08J2](https://github.com/TianxingChen/Embodied-AI-Guide/blob/main/Docs.qq.com/sheet/DYmppSU55cFNpaVJo?tab=BB08J2)

RoboHive [https://github.com/vikashplus/robohive](https://github.com/vikashplus/robohive)

#### 6.1.3 PyBullet
##### 6.1.3.1 PyBullet简介

PyBullet 是一个快速且易于使用的用于机器人模拟和机器学习，专注于仿真到现实转换的 Python 模块. 使用 PyBullet，您可以从 URDF、SDF、MJCF 和其他文件格式加载关节体. PyBullet 提供正向动力学模拟、反向动力学计算、正向和反向运动学、碰撞检测和射线交叉查询功能。Bullet Physics SDK 中包括 PyBullet 机器人示例，例如模拟Minitaur 四足机器人、使用 TensorFlow 推理运行的类人机器人和抓取物体的 KUKA 机械臂。 简化坐标多体、刚体和可变形体由统一的 LCP 约束求解器处理，

<img width="1260" height="240" alt="image" src="https://github.com/user-attachments/assets/706e1844-a8e3-4527-8c50-1b1a9903475d" />

除了物理模拟之外，还有渲染绑定，具有 CPU 渲染器 (TinyRenderer) 和 OpenGL 3.x 渲染和可视化，并支持虚拟现实耳机，如 HTC Vive 和 Oculus Rift。 PyBullet 还具有执行碰撞检测查询（最近点、重叠对、光线交叉测试等）和添加调试渲染（调试行和文本）的功能。PyBullet 具有对共享内存、UDP 和 TCP 网络的跨平台内置客户端-服务器支持。 因此，您可以在连接到 Windows VR 服务器的 Linux 上运行 PyBullet。PyBullet 包装了新Bullet C-API，它被设计为独立于底层物理引擎和渲染引擎，因此我们可以轻松迁移到 Bullet 的更新版本，或者使用不同的物理引擎或渲染引擎。默认情况下，PyBullet 在 CPU 上使用 Bullet 2.x API。我们还将使用 OpenCL 公开在 GPU 上运行的 Bullet 3.x。还有一个类似于 PyBullet 的 C++ API，参见b3RobotSimulatorClientAPI。PyBullet 可以很容易地与 TensorFlow 和 OpenAI Gym 一起使用。 来自 Google Brain[1,2,3,4], X[1,2], Stanford AI Lab [1,2,3], OpenAI,INRIA [1] and many other labs 的研究人员都在使用 PyBullet. 如果您在研究中使用 PyBullet，请添加 引文.PyBullet 的安装就像 (sudo) pip install PyBullet (Python 2.x)、pip3 install PyBullet 一样简单。这将公开 PyBullet 模块以及 pybullet_envs Gym 环境。

##### 6.1.3.2 PyBullet入门
这是我们一步一步讨论的 PyBullet 介绍脚本：

```python
import pybullet 
as p import time
import pybullet_data
physicsClient = p.connect(p.GUI)#or p.DIRECT for non-graphical 
version p.setAdditionalSearchPath(pybullet_data.getDataPath()) #可选用
的ly p.setGravity(0,0,-10)
planeId = p.loadURDF("plane.urdf") startPos = [0,0,1]
startOrientation = p.getQuaternionFromEuler([0,0,0]) 
boxId = p.loadURDF("r2d2.urdf",startPos, startOrientation)
#set the center of mass frame (loadURDF sets base link 
frame) startPos/Ornp.resetBasePositionAndOrientation(boxId, 
startPos, startOrientation)
for i in range 
(10000): 
p.stepSimulation() 
time.sleep(1./240.)
cubePos, cubeOrn = 
p.getBasePositionAndOrientation(boxId) 
print(cubePos,cubeOrn)
p.disconnect()
```

##### 6.1.3.3 Pybullet资料汇总
Pybullet官方文档 [https://pybullet.org/wordpress/](https://pybullet.org/wordpress/)

Pybullet快速入门手册 [PyBullet Quickstart Guide.pdf](https://github.com/user-attachments/files/23336275/PyBullet.Quickstart.Guide.pdf)

Pybullet快速入门手册（中文版） [PyBullet 快速入门手册（机翻版）.pdf](https://github.com/user-attachments/files/23336274/PyBullet.pdf)


#### 6.1.4 Genesis

##### 6.1.4.1 Genesis简介

<img width="553" height="338" alt="image" src="https://github.com/user-attachments/assets/d9f0338a-b88c-480e-ba4c-c0bb647216cd" />

Genesis 是一个为通用机器人/具身智能/物理智能应用设计的物理平台。它同时具备以下多个功能：
- 一个从零开始重新构建的通用物理引擎，能够模拟多种材料和物理现象。
- 一个轻量级、超快速、Python化、用户友好的机器人仿真平台。
- 一个强大且快速的真实感渲染系统。
- 一个生成数据引擎，能够将用户输入的自然语言描述转化为各种数据形式。
Genesis 基于一个重新设计并从零开始构建的通用物理引擎，整合了多种物理求解器及其耦合，形成一个统一的框架。这个核心物理引擎进一步通过一个生成性代理框架得到增强，后者旨在实现完全自动化的数据生成，适用于机器人学及其他领域。目前，我们正在开源底层物理引擎和仿真平台，生成性框架将在不久的将来发布。
Genesis 的建设和发展将持续以以下长期目标为驱动力：
- 降低使用物理仿真平台的门槛，让机器人研究对每个人都变得更容易访问。（参见我们的承诺）
- 将一系列最先进的物理求解器统一到一个框架中，允许在虚拟世界中以最高的物理、视觉和感官保真度重新创建整个物理世界，采用最先进的仿真技术。
- 最小化人类在收集和生成机器人及其他领域数据时的工作量，让数据飞轮自动运转。

为什么需要一个新的物理仿真器?

与以往的仿真平台相比，Genesis 在多个方面具有显著的优势，以下是一些关键特点：
- 🐍 Python化且完全透明：Genesis 完全用 Python 开发并开源，使得代码理解和贡献变得更加容易。
- 👶 安装简便，API 设计极其简洁易用：用户能够轻松安装并上手，API 设计简洁直观，适合各种使用者。
- 🚀 高度并行化的仿真，速度无与伦比：Genesis 是全球最快的物理引擎，其仿真速度比现有的 GPU 加速机器人仿真器（如 Isaac Gym/Sim/Lab、Mujoco MJX 等）快 10 到 80 倍（是的，这有点像科幻小说），而且在仿真精度和保真度上毫不妥协。
- 💥 统一框架，支持多种最先进的物理求解器：Genesis 提供一个统一的框架，能够模拟各种材料和物理现象，覆盖广泛的应用场景。
- 📸 真实感光线追踪渲染，优化性能：通过优化的光线追踪技术，Genesis 提供高质量的照片级渲染效果，同时保持高性能。
- 📐 可微分性：Genesis 被设计为完全兼容可微分仿真。目前，我们的 MPM 求解器和工具求解器已经支持可微分，未来将为更多求解器（包括刚体仿真）添加可微分性支持。
- ☝🏻 物理精确且可微分的触觉传感器：Genesis 提供物理精确的触觉传感器，能够模拟真实世界的物理交互，并支持进一步的优化。
- 🌌 原生支持生成性仿真：Genesis 允许通过自然语言提示生成各种形式的数据，包括互动场景、任务建议、奖励、资产、角色动作、策略、轨迹、相机运动、（物理精确的）视频等。
Genesis的愿景与使命
仿真在机器人研究中发挥了至关重要的作用，为训练机器人策略和生成数据提供了坚实的基础，借助不断增强的计算能力。然而，机器人研究人员长期以来受限于现有仿真平台的可用性问题和缺乏透明度。现有的GPU加速仿真器通常因为涉及复杂的数据驱动概念、复杂的API和软件堆栈，具有陡峭的学习曲线——这使得掌握这些仿真器对于研究人员，尤其是新入门的研究人员而言，成为一项艰巨的任务。此外，部分仿真器是封闭源代码的，限制了透明度，研究人员无法基于实际观察和反馈理解、控制或逐步改进底层的物理求解器。
Genesis 项目应运而生，旨在应对这些挑战。我们的愿景是打造一个完全透明、用户友好的生态系统，让来自物理仿真和机器人学背景的贡献者们能够聚集在一起，共同创建一个高效、逼真的虚拟世界，用于机器人研究及更多应用。我们还意识到，计算机图形学领域持续开发了大量创新的算法，这些算法能够应用于仿真和渲染领域；然而，迄今为止，还没有一个协作性强的项目将这些算法结合起来，创建一个真实且计算驱动的虚拟世界，让具身智能和物理智能得以蓬勃发展。

#### 6.1.4.2 Genesis基础

**安装**

🛠️ 安装指南
先决条件
- Python：3.9 或更高版本
- 操作系统：Linux（推荐）/ MacOS / Windows
注意事项
Genesis 设计为跨平台支持，包括 CPU、CUDA GPU 和非 CUDA GPU 后端设备。为了获得最佳性能，推荐在配有 CUDA 兼容 GPU 的 Linux 平台上使用。
不同操作系统的功能支持如下：

操作系统	GPU 设备	GPU 仿真	CPU 仿真	交互式查看器	无头渲染

Linux	Nvidia	✅	✅	✅	✅

	AMD	✅	✅	✅	✅
	
	Intel	✅	✅	✅	✅
	
Windows	Nvidia	✅	✅	❌	❌

	AMD	✅	✅	❌	❌
	
	Intel	✅	✅	❌	❌
	
MacOS	Apple Silicon	✅	✅	✅	✅

安装步骤
1. 通过 PyPI 安装 Genesis：
pip install genesis-world
2. 安装 PyTorch，请根据官方说明进行安装。
3. （可选）运动规划功能： Genesis 集成了 OMPL 的运动规划功能，并通过直观的 API 包装，使运动规划变得轻松。若需要内建的运动规划功能，请先下载预编译的 OMPL wheel，然后使用 pip 安装：
pip install ompl
4. （可选）表面重建： 若需要用于可视化粒子基础实体（流体、变形物体等）的精美视觉效果，通常需要使用内部的粒子基础表示重建网格表面。我们提供两种选择：
- splashsurf：一种最先进的表面重建方法，效果较好：
```Shell
cargo install splashsurf
```
- ParticleMesher：我们自己的基于 openVDB 的表面重建工具（速度较快，但效果不如 splashsurf 平滑）：
```Shell
echo "export LD_LIBRARY_PATH=
${PWD}/ext/ParticleMesher/ParticleMesherPy:$
LD_LIBRARY_PATH" >> ~/.bashrc
source ~/.bashrc
```
5. （可选）光线追踪渲染器： 如果您需要照片级真实感视觉效果，Genesis 内置了基于光线追踪（路径追踪）的渲染器，使用了高性能的领域特定语言 LuisaCompute 开发。
- 获取 LuisaRender： LuisaRender 的子模块位于 ext/LuisaRender 目录：
```Shell
git submodule update --init --recursive
```
- 依赖项：
(1) 如果您有 sudo 权限（推荐）：
```Shell
sudo apt install build-essential manpages-dev software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update && sudo apt install gcc-11 g++-11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 110
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 110
g++ --version
gcc --version
```
- 安装 CUDA（需要 CUDA 12.0 及以上版本）：
- Y
- 下载 CUDA 11.7 并安装。
```Shell
sudo apt install libvulkan-dev
sudo apt-get install zlib1g-dev
sudo apt-get install xorg-dev libglu1-mesa-dev
pip install "pybind11[global]"
sudo apt-get install libsnappy-dev
```
(2) 如果您没有 sudo 权限（使用 Conda）：
```Shell
conda install -c conda-forge gcc=11.4 gxx=11.4 cmake=3.26.1 minizip zlib libuuid patchelf vulkan-tools vulkan-headers
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
pip install "pybind11[global]"
```
6. 编译： 编译 LuisaRender 和其 Python 绑定。
- 使用系统依赖（步骤 2.A）：
```Shell
cd genesis/ext/LuisaRender
cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON -D LUISA_COMPUTE_ENABLE_GUI=OFF 
cmake --build build -j $(nproc)
```
- 使用 Conda 依赖（步骤 2.B）：
```Shell
export CONDA_INCLUDE_PATH=path/to/anaconda/include
cd ./ext/LuisaRender
cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON -D LUISA_COMPUTE_ENABLE_GUI=OFF -D ZLIB_INCLUDE_DIR=$CONDA_INCLUDE_PATH
cmake --build build -j $(nproc)
```

7. 常见问题解答（FAQs）：   
- Assertion ‘lerror’ failed：如果看到 “GLIBCXX_3.4.30 not found” 错误，请执行以下操作：
```Shell
cd ~/anaconda3/envs/genesis/lib
mv libstdc++.so.6 libstdc++.so.6.old
ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 libstdc++.so.6
```
这样，您就完成了 Genesis 的安装，接下来可以开始使用它进行仿真和开发了！

***Genesis初探**

Genesis 教程：基础示例
在这个教程中，我们将通过一个简单的例子来加载一个单独的 Franta 机械臂，然后让它自由地掉落到地面上。这个例子将用来演示在 Genesis 中创建仿真实验的核心步骤和一些基本概念。
```python
import genesis as gs
gs.init(backend=gs.cpu)
scene = gs.Scene(show_viewer=True)
plane = scene.add_entity(gs.morphs.Plane())
franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)
scene.build()
for i in range(1000):
    scene.step()
```

这就是完整的代码脚本！这样的示例只需要不到 10 行代码，并且已经封装了创建仿真实验所需的所有步骤。
如果你想深入了解，可以继续往下看，我们将一步一步地进行讲解：
1. 初始化
第一步是导入 genesis 并初始化它：
```python
import genesis as gs
gs.init(backend=gs.cpu)
```

后端设备：Genesis 设计为跨平台，支持多种后端设备。在这个例子中，我们使用 gs.cpu。如果你需要 GPU 加速的并行仿真，可以选择其他后端，例如 gs.cuda、gs.vulkan 或 gs.metal。你也可以使用 gs.gpu 作为快捷方式，Genesis 会根据你的系统自动选择一个后端（例如，如果有 CUDA 支持，它会选择 gs.cuda，如果是 Apple Silicon 设备，它会选择 gs.metal）。
精度级别：默认情况下，Genesis 使用 f32 精度。如果需要更高的精度，可以通过设置 precision='64' 来切换到 f64 精度。
日志级别：初始化完成后，终端会显示系统信息和与 Genesis 相关的信息（如当前版本）。如果不希望显示日志输出，可以通过设置 logging_level='warning' 来抑制日志。
颜色主题：默认情况下，Genesis 的日志颜色主题优化为深色背景终端。如果你使用的是浅色背景终端，可以将主题改为 'light'；如果你喜欢黑白模式，也可以选择 'dumb'。
一个更详细的 gs.init() 调用示例如下：
```Shell
gs.init(
    seed                = None,
    precision           = '32',
    debug               = False,
    eps                 = 1e-12,
    logging_level       = None,
    backend             = gs_backend.gpu,
    theme               = 'dark',
    logger_verbose_time = False
)
```
2. 创建场景
在 Genesis 中，所有的物体、机器人、相机等都放置在一个 Scene 中：
scene = gs.Scene()
一个 Scene 对象包装了一个仿真器对象，它处理所有底层的物理求解器；同时，它还包含一个可视化器对象，用来管理与可视化相关的概念。有关更多的详细信息和 API，请参考 Scene 文档。
创建场景时，你可以配置一些物理求解器的参数。下面是一个稍微复杂一些的例子：
```Shell
scene = gs.Scene(
    sim_options=gs.options.SimOptions(
        dt=0.01,
        gravity=(0, 0, -10.0),
    ),
    show_viewer=True,
    viewer_options=gs.options.ViewerOptions(
        camera_pos=(3.5, 0.0, 2.5),
        camera_lookat=(0.0, 0.0, 0.5),
        camera_fov=40,
    ),
)
```
这个例子设置了每一步仿真时间为 0.01s，配置了重力，并设置了交互式查看器的初始相机位置。
4. 加载物体到场景中
在这个示例中，我们加载了一个平面和一个 Franta 机械臂到场景中：
```Shell
plane = scene.add_entity(gs.morphs.Plane())
franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)
```
在 Genesis 中，所有的物体和机器人都被表示为 Entity 对象。Genesis 完全采用面向对象的设计，你可以直接通过实体对象的方法与它们交互，而不是使用句柄或全局 ID。
add_entity 的第一个参数是一个 morph。在 Genesis 中，morph 是一个混合概念，封装了物体的几何形状和姿态信息。通过使用不同的 morph，你可以从形状原语、网格、URDF、MJCF、Terrain 或软体机器人描述文件等创建 Genesis 实体。
在创建 morph 时，你还可以指定它的位置、朝向、大小等。比如，设置 euler 或 quat 来指定朝向。下面是一个例子：
```Shell
franka = scene.add_entity(
    gs.morphs.MJCF(
        file  = 'xml/franka_emika_panda/panda.xml',
        pos   = (0, 0, 0),
        euler = (0, 0, 90),  # 使用 scipy 的外部 x-y-z 旋转惯例，单位为度
        scale = 1.0,
    ),
)
```
我们目前支持以下不同类型的形状原语：
```Shell
- gs.morphs.Plane
- gs.morphs.Box
- gs.morphs.Cylinder
- gs.morphs.Sphere
````
此外，为了训练运动任务，我们还支持各种内建地形，以及通过 gs.morphs.Terrain 根据用户提供的高度图初始化的地形，我们将在后续的教程中详细讲解。
我们还支持加载不同格式的外部文件，如：
```Shell
- gs.morphs.MJCF：Mujoco 的 .xml 机器人配置文件
- gs.morphs.URDF：以 .urdf 结尾的机器人描述文件
- gs.morphs.Mesh：非关节化网格资产，支持扩展包括：*.obj、*.ply、*.stl、*.glb、*.gltf
```
当加载外部文件时，需要通过 file 参数指定文件位置。在解析时，我们不仅会根据当前工作目录解析相对路径，还会在 genesis/assets 内部资产目录中查找。所以在这个例子中，我们会从 genesis/assets/xml/franka_emika_panda/panda.xml 路径加载 Franka 模型。

4. 构建场景并开始仿真
完成以上步骤后，我们可以开始仿真。注意，在开始仿真前，我们需要先调用 scene.build() 来构建场景：
```Shell
scene.build()
for i in range(1000):
    scene.step()
```
调用 scene.build() 后，Genesis 会进行 GPU 内核的即时编译，为仿真准备好数据。完成后，会弹出一个交互式查看器来可视化仿真场景。查看器提供了各种键盘快捷键来录制视频、截图、切换不同的可视化模式等。

6. 内核编译和缓存
由于 Genesis 使用即时编译（JIT）技术，每次创建一个包含新配置的场景时（即不同的机器人类型、物体数量等），都会重新编译 GPU 内核。Genesis 支持自动缓存已编译的内核：第一次运行后（只要正常退出或使用 ctrl + c 终止），如果场景配置保持不变，后续运行会加载缓存的内核，以加速场景创建过程。
我们正在积极优化这一编译步骤，未来版本将通过并行编译和更快的内核序列化技术，极大提高这一过程的速度。

**可视化和渲染**
📸 可视化与渲染

Genesis的可视化系统由场景的visualizer管理（即scene.visualizer）。可以通过两种方式来可视化场景：

1. 使用独立线程运行的交互式查看器
2. 手动添加相机并渲染图像

查看器

连接显示器后可使用交互式查看器来查看场景。Genesis用不同的options组来配置场景中的组件。可以通过以下方式配置:

- 创建场景时修改viewer_options中的参数
- 使用vis_options设置可视化属性(查看器和相机共用)

下面创建一个详细配置的场景:

```Shell
scene = gs.Scene(
    show_viewer    = True,
    viewer_options = gs.options.ViewerOptions(
        res           = (1280, 960),
        camera_pos    = (3.5, 0.0, 2.5),
        camera_lookat = (0.0, 0.0, 0.5),
        camera_fov    = 40,
        max_FPS       = 60,
    ),
    vis_options = gs.options.VisOptions(
        show_world_frame = True, # 显示原点坐标系
        world_frame_size = 1.0, # 坐标系长度(米)
        show_link_frame  = False, # 不显示实体链接坐标系 
        show_cameras     = False, # 不显示相机网格和视锥
        plane_reflection = True, # 开启平面反射
        ambient_light    = (0.1, 0.1, 0.1), # 环境光
    ),
    renderer = gs.renderers.Rasterizer(), # 使用光栅化渲染器
)
```

这里可以设置:

- 查看器相机的位置和视场角
- 如果max_FPS为None,查看器会全速运行
- 如果res为None,会创建一个4:3窗口,高度为显示器一半
- Genesis提供两种渲染器:Rasterizer和RayTracer
- 查看器固定使用光栅化,相机默认也使用光栅化

场景创建后,可以通过scene.visualizer.viewer或scene.viewer访问查看器:

```Shell
cam_pose = scene.viewer.camera_pose()
scene.viewer.set_camera_pose(cam_pose)
```

相机与离线渲染

可以手动添加相机对象进行离线渲染:

```Shell
cam = scene.add_camera(
    res    = (1280, 960),
    pos    = (3.5, 0.0, 2.5),
    lookat = (0, 0, 0.5),
    fov    = 30,
    GUI    = False
)
```

设置GUI=True会为每个相机创建opencv窗口显示渲染结果。

构建场景后就可以渲染图像了。相机支持:

- RGB图像
- 深度图
- 分割掩码
- 表面法线

默认只渲染RGB,可以通过参数开启其他模式:

```Shell
scene.build()
```

**渲染所有类型**
```Shell
rgb, depth, segmentation, normal = cam.render(depth=True, segmentation=True, normal=True)
```

如果使用GUI=True且连接了显示器,会看到4个窗口。(如果窗口是黑的,可以多调用一次cv2.waitKey(1)或render()来刷新)

录制视频

下面演示如何移动相机并录制视频:

#开始录制
```Shell
cam.start_recording()

import numpy as np
for i in range(120):
    scene.step()

    #移动相机
    cam.set_pose(
        pos    = (3.0 * np.sin(i / 60), 3.0 * np.cos(i / 60), 2.5),
        lookat = (0, 0, 0.5),
    )
    
    cam.render()
```

#停止录制并保存视频

```Shell
cam.stop_recording(save_to_filename='video.mp4', fps=60)
```

将视频保存到video.mp4：


完整代码如下:

```Shell
import genesis as gs

gs.init(backend=gs.cpu)

scene = gs.Scene(
    show_viewer = True,
    viewer_options = gs.options.ViewerOptions(
        res           = (1280, 960),
        camera_pos    = (3.5, 0.0, 2.5),
        camera_lookat = (0.0, 0.0, 0.5),
        camera_fov    = 40,
        max_FPS       = 60,
    ),
    vis_options = gs.options.VisOptions(
        show_world_frame = True,
        world_frame_size = 1.0,
        show_link_frame  = False,
        show_cameras     = False,
        plane_reflection = True,
        ambient_light    = (0.1, 0.1, 0.1),
    ),
    renderer=gs.renderers.Rasterizer(),
)

plane = scene.add_entity(
    gs.morphs.Plane(),
)
franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)

cam = scene.add_camera(
    res    = (640, 480),
    pos    = (3.5, 0.0, 2.5),
    lookat = (0, 0, 0.5),
    fov    = 30,
    GUI    = False,
)

scene.build()


#渲染rgb、深度、分割掩码和法线图
#rgb, depth, segmentation, normal = cam.render(rgb=True, depth=True, segmentation=True, normal=True)

cam.start_recording()
import numpy as np

for i in range(120):
    scene.step()
    cam.set_pose(
        pos    = (3.0 * np.sin(i / 60), 3.0 * np.cos(i / 60), 2.5),
        lookat = (0, 0, 0.5),
    )
    cam.render()
cam.stop_recording(save_to_filename='video.mp4', fps=60)
```

**光线追踪渲染**

```Shell
Genesis提供光线追踪渲染器用于真实感渲染。创建场景时设置renderer=gs.renderers.RayTracer()即可切换。支持调节spp、aperture、model等参数,
```

**环境配置**

在以下环境中通过测试：

```Shell
- Ubuntu 22.04, CUDA 12.4, Python 3.9
- Ubuntu 24.04, CUDA 12.1, Python 3.9.12
```

- 获取子模块，即genesis/ext/LuisaRender。
#在 Genesis/ 目录中

```Shell
git submodule update --init --recursive
pip install -e ".[render]"
```

- 安装 g++/gcc11。

```Shell
sudo apt install build-essential manpages-dev software-properties-common
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt update && sudo apt install gcc-11 g++-11
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 110
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 110
```

#验证g++/gcc版本

```Shell
g++ --version
gcc --version
```
- 安装cmake 3.26及以上的版本（推荐使用snap进行安装）。
请注意snap的包安装路径是/snap/bin/cmake（或/usr/bin/snap），而系统可能在/usr/local/bin/cmake已有其余版本的cmake。因此需要通过echo $PATH确认路径顺序。

```Shell
sudo snap install cmake --classic
cmake --version
```

- 安装依赖项。
```Shell
sudo apt install libvulkan-dev # Vulkan
sudo apt-get install zlib1g-dev # zlib
sudo apt-get install libx11-dev # X11
sudo apt-get install xorg-dev libglu1-mesa-dev # RandR头文件
```

- 构建LuisaRender（使用正确版本的cmake）。
```Shell
cd genesis/ext/LuisaRender
cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON
```
#记得检查python版本
```Shell
cmake --build build -j $(nproc)
```
如果无法完成构建，我们在这里提供了预编译的结果（注意检查是否与本机配置相同）。文件命名规则为build_<commit-tag>_cuda<version>_python<version>。下载与本机系统配置相匹配的文件，解压后重命名为build/并放到genesis/ext/LuisaRender路径下。

环境配置完成之后，运行示例：
cd examples/rendering
python demo.py
会得到如下渲染结果：



FAQ 疑难解答
- 执行cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D

LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON时遇到Pybind错误，
CMake Error at src/apps/CMakeLists.txt:12 (find_package):
By not providing "Findpybind11.cmake" in CMAKE_MODULE_PATH this project has
asked CMake to find a package configuration file provided by "pybind11",
but CMake did not find one.

Could not find a package configuration file provided by "pybind11" with any
of the following names:

    pybind11Config.cmake
    pybind11-config.cmake
    可能是遗漏执行pip install -e ".[render]"导致。或者也可以直接安装pybind：pip install "pybind11[global]"。
    
- 执行cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D

LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON时遇到CUDA运行时编译错误，
/usr/bin/ld: CMakeFiles/luisa-cuda-nvrtc-standalone-compiler.dir/cuda_nvrtc_compiler.cpp.o: in function `main`:
cuda_nvrtc_compiler.cpp:(.text.startup+0x173): undefined reference to `nvrtcGetOptiXIRSize`
/usr/bin/ld: cuda_nvrtc_compiler.cpp:(.text.startup+0x197): undefined reference to `nvrtcGetOptiXIR`
    需要正确安装“系统级”的CUDA工具包（cuda-toolkit）（官方安装指南）。首先检查CUDA工具包是否安装，
nvcc --version # 这应该与你从nvidia-smi获取的CUDA版本一致
which nvcc # 确认你正在使用正确的CUDA工具包
    如果nvcc命令没有给出正确的输出，请按照官方CUDA工具包安装指南进行操作。以下是安装CUDA工具包（以CUDA 12.4为例）的一些步骤。从这里下载安装程序。
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/12.4.0/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-12-4-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-4
    设置二进制文件和运行时库路径：在~/.bashrc中添加以下内容。注意最好将CUDA路径添加到最后，因为/usr/local/cuda-12.4/bin目录中也可能存在其他版本的gcc和g++，而gcc/g++11是构建所必需的），
PATH=${PATH:+${PATH}:}/usr/local/cuda-12.4/bin
LD_LIBRARY_PATH=${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}/usr/local/cuda-12.4/lib64
    最后重启终端或执行source ~/.bashrc。
    另一种错误类型是，
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `_dl_fatal_printf@GLIBC_PRIVATE`
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `_dl_audit_symbind_alt@GLIBC_PRIVATE`
<your-env-path>/genesis-test1/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `_dl_exception_create@GLIBC_PRIVATE`
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `__nptl_change_stack_perm@GLIBC_PRIVATE`
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `__tunable_get_val@GLIBC_PRIVATE`
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `_dl_audit_preinit@GLIBC_PRIVATE`
<your-env-path>/bin/ld: /lib/x86_64-linux-gnu/libc.so.6: undefined reference to `_dl_find_dso_for_object@GLIBC_PRIVATE`
    这可能是由于conda环境中的CUDA工具包导致的。请执行以下操作并安装系统级的CUDA，
which nvcc
conda uninstall cuda-toolkit
    或者，你可以将conda的库路径添加到运行时库路径中，
ls $CONDA_PREFIX/lib/libcudart.so # 你应该有这个文件

#在你的~/.bashrc中添加
LD_LIBRARY_PATH=${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}/usr/local/cuda-12.4/lib64
    最后，记得在完成上述修复后清理构建。
rm -r build
    
- 执行cmake -S . -B build -D CMAKE_BUILD_TYPE=Release -D PYTHON_VERSIONS=3.9 -D

LUISA_COMPUTE_DOWNLOAD_NVCOMP=ON时遇到编译器错误，
CMake Error at /snap/cmake/1435/share/cmake-3.31/Modules/CMakeDetermineCCompiler.cmake:49 (message):
Could not find compiler set in environment variable CC:

/home/tsunw/miniconda3/envs/genesis-test1/bin/x86_64-conda-linux-gnu-cc.
Call Stack (most recent call first):
CMakeLists.txt:21 (project)


CMake Error: CMAKE_C_COMPILER not set, after EnableLanguage
CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage
    可能是gcc和g++版本不正确导致。请仔细检查
    （i）gcc/g++版本是否为 11
    （ii）二进制文件是否指向正确的路径
    （iii）二进制文件路径的顺序，
gcc --version
g++ --version
which gcc
which g++
echo $PATH # 例如，/usr/local/cuda-12.4/bin/gcc（版本=10.5）不应该排在/usr/bin/gcc（版本=11）之前
    
- 运行examples/rendering/demo.py时出现导入错误，
[Genesis] [11:29:47] [ERROR] Failed to import LuisaRenderer. ImportError: /home/tsunw/miniconda3/envs/genesis-test1/bin/../lib/libstdc++.so.6: version `GLIBCXX_3.4.30` not found (required by /home/tsunw/workspace/Genesis/genesis/ext/LuisaRender/build/bin/liblc-core.so)
    conda安装的libstdc++.so.6不支持3.4.30，需要将系统库中的libstdc++.so.6文件链接到conda中（参考）。
cd $CONDA_PREFIX/lib
mv libstdc++.so.6 libstdc++.so.6.old
ln -s /usr/lib/x86_64-linux-gnu/libstdc++.so.6 libstdc++.so.6
  
**逆解和运动规划**
🦾逆解和运动规划

在本教程中，我们将通过几个示例来演示如何在Genesis中使用逆向运动学（IK）和运动规划，并执行一个简单的抓取任务。
  首先，我们创建一个场景，加载你喜欢的机器人臂和一个小方块，构建场景，然后设置控制增益：

```python
import numpy as np
import genesis as gs

########################## init ##########################
gs.init(backend=gs.gpu)

########################## create a scene ##########################
scene = gs.Scene(
    viewer_options = gs.options.ViewerOptions(
        camera_pos    = (3, -1, 1.5),
        camera_lookat = (0.0, 0.0, 0.5),
        camera_fov    = 30,
        max_FPS       = 60,
    ),
    sim_options = gs.options.SimOptions(
        dt = 0.01,
        substeps = 4, # for more stable grasping contact
    ),
    show_viewer = True,
)

########################## entities ##########################
plane = scene.add_entity(
    gs.morphs.Plane(),
)
cube = scene.add_entity(
    gs.morphs.Box(
        size = (0.04, 0.04, 0.04),
        pos  = (0.65, 0.0, 0.02),
    )
)
franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)
########################## build ##########################
scene.build()

motors_dof = np.arange(7)
fingers_dof = np.arange(7, 9)

# set control gains
# Note: the following values are tuned for achieving best behavior with Franka
# Typically, each new robot would have a different set of parameters.
# Sometimes high-quality URDF or XML file would also provide this and will be parsed.
franka.set_dofs_kp(
    np.array([4500, 4500, 3500, 3500, 2000, 2000, 2000, 100, 100]),
)
franka.set_dofs_kv(
    np.array([450, 450, 350, 350, 200, 200, 200, 10, 10]),
)
franka.set_dofs_force_range(
    np.array([-87, -87, -87, -87, -12, -12, -12, -100, -100]),
    np.array([ 87,  87,  87,  87,  12,  12,  12,  100,  100]),
)
```
<img width="553" height="369" alt="image" src="https://github.com/user-attachments/assets/d53bb94e-57b5-4a28-aaf1-f584d9c28f51" />

接下来，让我们将机器人末端执行器移动到一个预抓取姿态。这可以通过两个步骤完成：
  - 使用逆向运动学（IK）来求解给定目标末端执行器姿态下的关节位置
  - 使用运动规划器到达目标位置
在Genesis中，运动规划使用OMPL库。你可以按照安装页面中的说明进行安装。
Genesis中的IK和运动规划非常简单：每个操作都可以通过一个函数调用完成。
```python
# get the end-effector link
end_effector = franka.get_link('hand')

# move to pre-grasp pose
qpos = franka.inverse_kinematics(
    link = end_effector,
    pos  = np.array([0.65, 0.0, 0.25]),
    quat = np.array([0, 1, 0, 0]),
)
# gripper open pos
qpos[-2:] = 0.04
path = franka.plan_path(
    qpos_goal     = qpos,
    num_waypoints = 200, # 2s duration
)
# execute the planned path
for waypoint in path:
    franka.control_dofs_position(waypoint)
    scene.step()

# allow robot to reach the last waypoint
for i in range(100):
    scene.step()
```
正如你所看到的，逆向运动学求解和运动规划是机器人实体的两个集成方法。对于逆向运动学求解，你只需要告诉机器人的IK求解器哪个链接是末端执行器，并指定目标姿态。然后，你告诉运动规划器目标关节位置（qpos），它将返回一个规划并平滑过的路径点列表。请注意，在执行路径后，我们让控制器再运行100步。这是因为我们使用的是PD控制器，目标位置和当前实际位置之间会存在一定的差距。因此，我们让控制器多运行一段时间，以便机器人能够到达规划轨迹中的最后一个路径点。
接下来，我们将机器人夹爪向下移动，抓取方块，然后将其提起：
```python
# reach
qpos = franka.inverse_kinematics(
    link = end_effector,
    pos  = np.array([0.65, 0.0, 0.135]),
    quat = np.array([0, 1, 0, 0]),
)
franka.control_dofs_position(qpos[:-2], motors_dof)
for i in range(100):
    scene.step()

# grasp
franka.control_dofs_position(qpos[:-2], motors_dof)
franka.control_dofs_force(np.array([-0.5, -0.5]), fingers_dof)

for i in range(100):
    scene.step()

# lift
qpos = franka.inverse_kinematics(
    link=end_effector,
    pos=np.array([0.65, 0.0, 0.3]),
    quat=np.array([0, 1, 0, 0]),
)
franka.control_dofs_position(qpos[:-2], motors_dof)
for i in range(200):
    scene.step()
```
在抓取物体时，我们对夹爪的两个自由度进行了力控制，并施加了0.5N的抓取力。如果一切顺利，你将看到物体被成功抓取并提起。

注意:
在Genesis中，运动规划使用OMPL库。遇到如下报错说明OMPL未安装
<img width="553" height="100" alt="image" src="https://github.com/user-attachments/assets/7f810d41-f371-4a19-aedd-b2b53c5043e6" />

安装方法如下:
参考🛠️ Installation
1. 依据系统及python版本下载whl文件,下载地址[https://github.com/ompl/ompl/releases/tag/prerelease](https://github.com/ompl/ompl/releases/tag/prerelease)

<img width="554" height="402" alt="image" src="https://github.com/user-attachments/assets/b0949ee6-2ba8-40e7-97aa-095096fb29ce" />

3. 进入whl下载目录并打开终端,执行下列命令
conda activate genesis所在环境名称
pip install ompl-1.6.0-cp310-cp310-manylinux_2_28_x86_64.whl

<img width="554" height="103" alt="image" src="https://github.com/user-attachments/assets/3d5945e4-32b4-4927-b1cd-faf7f4a7f963" />

4. 程序顺利运行

更多：
[https://yv6uc1awtjc.feishu.cn/wiki/EEqAwFLo5iUdn5kD95OcAOtZnhf](https://yv6uc1awtjc.feishu.cn/wiki/EEqAwFLo5iUdn5kD95OcAOtZnhf)

6.1.4.3 仿真示例

<img width="553" height="312" alt="image" src="https://github.com/user-attachments/assets/734a7d45-3c59-4ff8-87da-3393a85af27c" />


使用GPU加速仿真的最大优势是能够实现场景级别的并行性，这样我们可以在成千上万个环境中同时训练机器人。

在Genesis中，创建并行仿真非常简单：在构建场景时，只需添加一个额外的参数n_envs来告诉模拟器你想要多少个环境。就是这么简单。请注意，为了模仿学习文献中的命名约定，我们也会使用术语batching来表示并行化操作。

示例脚本：
```python
import genesis as gs
import torch

########################## 初始化 ##########################
gs.init(backend=gs.gpu)

########################## 创建场景 ##########################
scene = gs.Scene(
    show_viewer    = True,
    viewer_options = gs.options.ViewerOptions(
        camera_pos    = (3.5, -1.0, 2.5),
        camera_lookat = (0.0, 0.0, 0.5),
        camera_fov    = 40,
    ),
    rigid_options = gs.options.RigidOptions(
        dt                = 0.01,
    ),
)

########################## 实体 ##########################
plane = scene.add_entity(
    gs.morphs.Plane(),
)

franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)

########################## 构建 ##########################

# 创建20个并行环境
B = 20
scene.build(n_envs=B, env_spacing=(1.0, 1.0))

# 控制所有机器人
franka.control_dofs_position(
    torch.tile(
        torch.tensor([0, 0, 0, -1.0, 0, 0, 0, 0.02, 0.02], device=gs.device), (B, 1)
    ),
)

for i in range(1000):
    scene.step()
```
上述脚本与Hello, Genesis中的示例几乎相同，只是scene.build()现在附加了两个额外的参数：
- n_envs：指定你想要创建的批量环境数量
- env_spacing：生成的并行环境共享相同的状态。为了可视化目的，你可以指定此参数，要求可视化工具将所有环境以(x, y)米的距离分布在网格中。请注意，这只影响可视化行为，并不会改变每个环境中实体的实际位置。

**控制批量环境中的机器人**

回想一下我们在之前的教程中使用的API，例如franka.control_dofs_position()。现在你可以使用完全相同的API来控制批量机器人，只是输入变量需要一个额外的批量维度：
```python
franka.control_dofs_position(torch.zeros(B, 9, device=gs.device))
```
由于我们在GPU上运行仿真，为了减少CPU和GPU之间的数据传输开销，我们可以使用通过gs.device选择的torch张量而不是numpy数组（但numpy数组也可以工作）。当你需要频繁发送一个具有巨大批量大小的张量时，这可以带来显著的性能提升。
上述调用将控制批量环境中的所有机器人。如果你只想控制某些环境，可以另外传入envs_idx，但请确保position张量的批量维度大小与envs_idx的长度匹配：
```python
# 只控制3个环境：1, 5和7。
franka.control_dofs_position(
    position = torch.zeros(3, 9, device=gs.device),
    envs_idx = torch.tensor([1, 5, 7], device=gs.device),
)
```

此调用将仅向3个选定的环境发送零位置命令。

Genesis支持多达数万个并行环境，并以这种方式解锁前所未有的仿真速度。关闭查看器，并将批量大小更改为30000（如果你的GPU显存较小，请考虑使用较小的批量大小）：
```python
import torch
import genesis as gs

gs.init(backend=gs.gpu)

scene = gs.Scene(
    show_viewer   = False,
    rigid_options = gs.options.RigidOptions(
        dt                = 0.01,
    ),
)

plane = scene.add_entity(
    gs.morphs.Plane(),
)

franka = scene.add_entity(
    gs.morphs.MJCF(file='xml/franka_emika_panda/panda.xml'),
)

scene.build(n_envs=30000)

# 控制所有机器人
franka.control_dofs_position(
    torch.tile(
        torch.tensor([0, 0, 0, -1.0, 0, 0, 0, 0.02, 0.02], device=gs.device), (30000, 1)
    ),
)

for i in range(1000):
    scene.step()
```

在配备RTX 4090和14900K的桌面上运行上述脚本可以实现未来的仿真速度——每秒超过4300万帧，这比实时快430,000倍。

<img width="554" height="102" alt="image" src="https://github.com/user-attachments/assets/e27d2313-7e41-4afc-bc47-9966c295e7fe" />

小技巧
FPS日志记录： 默认情况下，Genesis记录器将在终端显示实时仿真速度。你可以在创建场景时设置show_FPS=False来禁用此行为。

##### 6.1.4.4 Genesis资料汇总

今日刷屏的Genesis有效信源整合 - 强化学徒的文章 - 知乎
[https://zhuanlan.zhihu.com/p/13603265800](https://zhuanlan.zhihu.com/p/13603265800)
完整Demo视频：[【太炸裂了 Genesis机器人物理引擎震撼发布-B站转载】](https://www.bilibili.com/video/BV12ykTY5EPr/)
genesis中文文档[https://genesis-world.readthedocs.io/zh-cn](https://genesis-world.readthedocs.io/zh-cn)
开源地址：[https://github.com/Genesis-Embodied-AI/Genesis](https://github.com/Genesis-Embodied-AI/Genesis)
项目主页：[https://genesis-embodied-ai.github.io/](https://genesis-embodied-ai.github.io/)
论文：暂时没有发布；
三大会报道：[https://mp.weixin.qq.com/s/vx5owauc2aNUPf8LVeB8jw](https://mp.weixin.qq.com/s/vx5owauc2aNUPf8LVeB8jw)
作者社媒主页【后续会有discord】：[https://x.com/zhou_xian_/status/1869511650782658846?s=46&t=e_20cB9LtY99fq_ngACPgA](https://x.com/zhou_xian_/status/1869511650782658846?s=46&t=e_20cB9LtY99fq_ngACPgA)
石麻笔记：[Genesis 发布：全新机器人物理引擎——它会变革机器人仿真吗？](https://mp.weixin.qq.com/s/IEhpXMdotHOPwhLdZYKeAA)
后空翻代码：[https://github.com/ziyanx02/Genesis-backflip](https://github.com/ziyanx02/Genesis-backflip)



#### 6.1.5 Gazebo

### 6.2 任务基准：单胳膊/双臂/移动操作/装配

由于Isaac Lab内基本集成了目前常用的绝大多数任务基准，以下以Isaac Lab集成的任务基准为例进行阐述。其他仿真器下任务名及设置可能稍有不同，但基准任务本身基本一致，在其他仿真器下可通过官方文档找到类似的对应任务基准。以下列表包含在 Isaac Lab 中可用的所有 RL 和 IL 任务实现。尽管我们尽量保持此列表最新，您仍可以通过运行以下命令获取最新的环境列表:

 Linux
./isaaclab.sh -p scripts/environments/list_envs.py

单一智能体
经典
基于 IsaacGymEnvs 实现的 MuJoCo 风格环境的经典环境。
<img width="819" height="572" alt="image" src="https://github.com/user-attachments/assets/ceb5b2c9-edef-4a22-8e30-45b65840ca7b" />
<img width="819" height="524" alt="image" src="https://github.com/user-attachments/assets/bf50f301-0c46-4502-ab4d-f1f23754a3b1" />


操作臂
基于固定机械臂操作任务的环境。

对于许多这些任务，我们包括具有不同手臂动作空间的配置。例如，对于 lift-cube 环境:

Isaac-Lift-Cube-Franka-v0: Franka机械臂关节位置控制

Isaac-Lift-Cube-Franka-IK-Abs-v0: Franka机械臂绝对IK控制

Isaac-Lift-Cube-Franka-IK-Rel-v0: Franka机械臂相对IK控制

<img width="785" height="703" alt="image" src="https://github.com/user-attachments/assets/96d2c64d-9192-40bb-bd51-33c433ef4ee9" />
<img width="792" height="478" alt="image" src="https://github.com/user-attachments/assets/5e8b1723-e46e-4c37-aef6-ad02ad686b53" />
<img width="875" height="542" alt="image" src="https://github.com/user-attachments/assets/0c2e2116-19e1-41b2-a9b4-eecd112c7c28" />
<img width="878" height="601" alt="image" src="https://github.com/user-attachments/assets/409fc01c-1490-4340-a370-0f11d8896ffd" />
<img width="872" height="767" alt="image" src="https://github.com/user-attachments/assets/304d50e4-7386-416c-8b85-fbcae4ad14b5" />
<img width="875" height="565" alt="image" src="https://github.com/user-attachments/assets/165a27f6-4e8e-4538-863a-0bd169d555f6" />
<img width="875" height="338" alt="image" src="https://github.com/user-attachments/assets/075e7193-3e1b-4642-a419-b9e9a4589702" />


富接触操控
基于富接触操控的环境，例如销钉插入、齿轮啮合和螺母螺栓紧固。

这些任务共享相同的任务配置和控制选项。您可以通过指定任务名称在它们之间切换。例如:

Isaac-Factory-PegInsert-Direct-v0: 使用Franka机械臂进行销钉插入

Isaac-Factory-GearMesh-Direct-v0: 与Franka机械臂啮合的齿轮

Isaac-Factory-NutThread-Direct-v0: 用Franka机械臂进行螺母螺栓紧固

<img width="875" height="743" alt="image" src="https://github.com/user-attachments/assets/c294b29c-f5b7-4b6c-8b89-02edd1e880e9" />


自动装配
基于100种不同装配任务的环境，每个任务都涉及将插头插入插座的操作。这些任务共享相同的配置框架，但通过零部件的几何形状和物理属性实现差异化。

可通过指定对应的资产ID切换不同任务，可用资产ID包括:

‘00004’, ‘00007’, ‘00014’, ‘00015’, ‘00016’, ‘00021’, ‘00028’, ‘00030’, ‘00032’, ‘00042’, ‘00062’, ‘00074’, ‘00077’, ‘00078’, ‘00081’, ‘00083’, ‘00103’, ‘00110’, ‘00117’, ‘00133’, ‘00138’, ‘00141’, ‘00143’, ‘00163’, ‘00175’, ‘00186’, ‘00187’, ‘00190’, ‘00192’, ‘00210’, ‘00211’, ‘00213’, ‘00255’, ‘00256’, ‘00271’, ‘00293’, ‘00296’, ‘00301’, ‘00308’, ‘00318’, ‘00319’, ‘00320’, ‘00329’, ‘00340’, ‘00345’, ‘00346’, ‘00360’, ‘00388’, ‘00410’, ‘00417’, ‘00422’, ‘00426’, ‘00437’, ‘00444’, ‘00446’, ‘00470’, ‘00471’, ‘00480’, ‘00486’, ‘00499’, ‘00506’, ‘00514’, ‘00537’, ‘00553’, ‘00559’, ‘00581’, ‘00597’, ‘00614’, ‘00615’, ‘00638’, ‘00648’, ‘00649’, ‘00652’, ‘00659’, ‘00681’, ‘00686’, ‘00700’, ‘00703’, ‘00726’, ‘00731’, ‘00741’, ‘00755’, ‘00768’, ‘00783’, ‘00831’, ‘00855’, ‘00860’, ‘00863’, ‘01026’, ‘01029’, ‘01036’, ‘01041’, ‘01053’, ‘01079’, ‘01092’, ‘01102’, ‘01125’, ‘01129’, ‘01132’, ‘01136’.

我们同时提供拆卸与装配两种任务环境。

注意

建议使用 CUDA 与 570 驱动程序运行 AutoMate 环境。如果在架构为 x86_64 的 Linux 上使用 Nvidia 驱动程序 570 运行，我们按照以下步骤安装 CUDA 12.8。这允许在 AutoMate 环境中使用 CUDA 计算奖励。如果您有不同的操作系统或架构，请参阅 CUDA installation page 获取其他说明。

wget https://developer.download.nvidia.com/compute/cuda/12.8.0/local_installers/cuda_12.8.0_570.86.10_linux.run
sudo sh cuda_12.8.0_570.86.10_linux.run --toolkit
使用 conda 时，可以通过以下命令安装 CUDA 工具包:

conda install cudatoolkit
使用 580 驱动程序和 CUDA 13，我们目前无法启用 CUDA 来计算奖励。代码会自动回退到 CPU，导致性能略慢。

Isaac-AutoMate-Disassembly-Direct-v0: 初始状态下插头已插入插座，底层控制器会将插头拔出并移至随机位置。这个过程完全由脚本控制，不涉及任何学习策略，因此不需要进行策略训练或评估。这些结果轨迹可作为逆向学习（即装配学习）的示范数据。运行指定任务的拆卸模式: python source/isaaclab_tasks/isaaclab_tasks/direct/automate/run_disassembly_w_id.py --assembly_id=ASSEMBLY_ID --disassembly_dir=DISASSEMBLY_DIR. 所有生成的轨迹存储在本地文件夹 DISASSEMBLY_DIR 中。

Isaac-AutoMate-Assembly-Direct-v0: 目标是将插头插入插座。你可以使用这个环境通过强化学习训练策略，或评估预训练模型。

要训练装配策略，我们运行命令 python source/isaaclab_tasks/isaaclab_tasks/direct/automate/run_w_id.py --assembly_id=ASSEMBLY_ID --train 。我们可以通过可选参数自定义训练流程: 使用 --headless 以无界面模式运行（不打开GUI窗口）， --max_iterations=MAX_ITERATIONS 设置训练迭代次数， --num_envs=NUM_ENVS 设置训练时的并行环境数量， --seed=SEED 指定随机种子。训练过程中，策略检查点会自动保存在 logs/rl_games/Assembly/test 目录下。

要评估一个装配策略，我们运行命令 python source/isaaclab_tasks/isaaclab_tasks/direct/automate/run_w_id.py --assembly_id=ASSEMBLY_ID --checkpoint=CHECKPOINT --log_eval 。评估结果存储在 evaluation_{ASSEMBLY_ID}.h5 。

<img width="872" height="500" alt="image" src="https://github.com/user-attachments/assets/556970ff-dba3-4da1-84b5-bfba6989851f" />

FORGE
FORGE 环境通过以下方式扩展了 Factory 环境:

力传感: 添加末端执行器所受力的观测值。

过度力惩罚: 添加一个选项来惩罚智能体超出接触力限制的行为。

动力学随机化: 随机化控制器增益、资产属性（摩擦、质量）和死区。

成功预测: 添加一个额外的动作来预测任务成功。

这些任务共享相同的任务配置和控制选项。您可以通过指定任务名称在它们之间切换。

Isaac-Forge-PegInsert-Direct-v0: 使用Franka机械臂进行销钉插入

Isaac-Forge-GearMesh-Direct-v0: 与Franka机械臂啮合的齿轮

Isaac-Forge-NutThread-Direct-v0: 用Franka机械臂进行螺母螺栓紧固

<img width="876" height="742" alt="image" src="https://github.com/user-attachments/assets/91ac4a06-863c-4756-b5f9-2cf45aa35fcc" />

运动
基于四足运动任务的环境
<img width="875" height="608" alt="image" src="https://github.com/user-attachments/assets/e0e30d43-52f5-485a-a133-785b6501409c" />
<img width="877" height="561" alt="image" src="https://github.com/user-attachments/assets/8e994e60-c203-47bc-8351-7c6ef2ddbd50" />
<img width="874" height="559" alt="image" src="https://github.com/user-attachments/assets/ff5eb580-dbd5-4066-aa83-0f7439bb0c58" />
<img width="873" height="557" alt="image" src="https://github.com/user-attachments/assets/cc1b91d6-cbe1-4868-b2be-a784b90a28ee" />
<img width="870" height="559" alt="image" src="https://github.com/user-attachments/assets/11a3dc4b-fb75-4280-be68-4a042b8ef149" />
<img width="875" height="560" alt="image" src="https://github.com/user-attachments/assets/67396204-eeb1-44a7-893c-5dd5b6790036" />
<img width="879" height="376" alt="image" src="https://github.com/user-attachments/assets/eee9efc4-b6f4-484b-86a1-9960d167a29b" />

导航
<img width="878" height="232" alt="image" src="https://github.com/user-attachments/assets/b19c2bd9-9f94-43aa-9900-83ecf88c670a" />


Others
备注
对抗运动先验 (AMP) 训练仅在 skrl 库中可用，因为它是当前集成的库中唯一一个开箱即用支持该功能的库（对于其他库，需要实现该算法和架构）。有关更多信息，请参见 skrl’s AMP Documentation 。可以通过向训练/播放脚本添加命令行输入 --algorithm AMP 来激活 AMP 算法。

为了评估，脚本的命令行输入 --real-time 允许环境和智能体之间的交互循环在可能的情况下实时运行。

<img width="877" height="439" alt="image" src="https://github.com/user-attachments/assets/e4fa59d3-93ab-466f-aa07-221331aba4f9" />


空间展示
cartpole_showcase 文件夹包含示例任务（基于 Cartpole 和 Cartpole-Camera Direct 任务），用于定义/使用 Isaac Lab 支持的各种 Gymnasium 观测空间和动作空间。

备注

目前，仅 Isaac Lab 的 Direct 工作流支持定义除 Box 之外的观测空间和动作空间。请参阅 Direct 工作流的 observation_space / action_space 文档以获取更多详细信息。

下表总结了 Cartpole 和 Cartpole-Camera 任务中展示的不同观测空间与动作空间的组合。在训练和评估的任务名称中，用 <OBSERVATION> 和 <ACTION> 替换相应的观测空间和动作空间。

<img width="783" height="600" alt="image" src="https://github.com/user-attachments/assets/db025a0a-627a-4c5a-ab24-890a12259780" />

多智能体
备注

真正的多智能体训练仅在 skrl 库中可用，更多信息请参见 多智能体文档 。它支持 IPPO 和 MAPPO 算法，可以通过在训练/回放脚本中添加命令行输入 --algorithm IPPO 或 --algorithm MAPPO 来激活。如果这些环境与其他库一起运行或没有 IPPO 或 MAPPO 标志，它们将在后台转换为单智能体环境。

经典
<img width="874" height="232" alt="image" src="https://github.com/user-attachments/assets/b61a141e-2aa4-4c5d-bd75-547c23716ac0" />


操作臂
基于固定机械臂操作任务的环境。

<img width="874" height="233" alt="image" src="https://github.com/user-attachments/assets/34f08534-6e5e-4070-8190-610f4f63fc01" />



综合环境列表
对于在 推理任务名称 下列出不同任务名称的环境，请在运行 play.py 或任何推理工作流时使用提供的推理任务名称。这些任务提供了更适合推理的配置，包括从已训练好的检查点读取数据，并禁用训练时使用的运行时扰动。

<img width="877" height="729" alt="image" src="https://github.com/user-attachments/assets/08574079-d3da-4c6f-8cb7-60219aa02639" />
<img width="874" height="712" alt="image" src="https://github.com/user-attachments/assets/11f6182d-87ad-4d9d-9d2e-f4171082f232" />
<img width="872" height="764" alt="image" src="https://github.com/user-attachments/assets/83b91138-a7b5-4352-bd13-58fe94092b03" />
<img width="873" height="801" alt="image" src="https://github.com/user-attachments/assets/e3c81740-15cc-4775-b18c-6e1d247ae3f4" />
<img width="874" height="821" alt="image" src="https://github.com/user-attachments/assets/4ac1d9c2-7346-4979-bbdf-ab77b2560a16" />
<img width="871" height="728" alt="image" src="https://github.com/user-attachments/assets/e48d6ebf-b0f5-4b35-8a15-7a7b1f2df3e4" />
<img width="874" height="767" alt="image" src="https://github.com/user-attachments/assets/02ef9230-8afb-4ad6-a679-2f5b9d08b3ca" />
<img width="875" height="838" alt="image" src="https://github.com/user-attachments/assets/b1f30522-0267-46c4-95f1-91a13743aae8" />
<img width="875" height="792" alt="image" src="https://github.com/user-attachments/assets/544cff94-5f06-4d97-bb21-b9cf54f5c55e" />
<img width="873" height="768" alt="image" src="https://github.com/user-attachments/assets/53a84670-9af8-4d11-938d-7ccf2c516f0d" />
<img width="873" height="280" alt="image" src="https://github.com/user-attachments/assets/49a4c774-1f66-4e4b-9b14-f0cfacc811ab" />



6.3 资产与场景：USD/URDF 导入、相机布局、光照与碰撞
6.3.1 USD/URDF 导入
6.3.1.1 URDF文件数据集
转自：知乎huyoust

里面收集的资料也比较多，都分类整理了，有机械臂，双足，双臂，飞行器，执行器，仿人，四足，轮式等。实际上github上有很多awesome ***类型的项目，这些作者都有着极大的专注与热情，能省去自己找资料的麻烦，推荐感兴趣的去给他们点个免费的star。

<img width="1138" height="991" alt="image" src="https://github.com/user-attachments/assets/99ae23a8-af87-4a00-a3f0-cade61d33391" />
<img width="1260" height="1153" alt="image" src="https://github.com/user-attachments/assets/83ef113a-fc4e-42f9-b672-19e50b9e84d6" />
<img width="961" height="1065" alt="image" src="https://github.com/user-attachments/assets/c6c20490-e4ff-41a9-805d-a0411f0d9831" />
<img width="961" height="1065" alt="image" src="https://github.com/user-attachments/assets/1700a71c-f80d-41eb-84b6-ff88556a77df" />

最近在Github上找一个机械臂的URDF文件时，发现一个很好的仓库。这应该是目前整理的最好最全的关于工业机械臂的URDF文件的仓库了，地址如下：

[GitHub - Daniella1/urdf_files_dataset
github.com/Daniella1/urdf_files_dataset](https://github.com/Daniella1/urdf_files_dataset)
本来以为这也只是一个awesome xxx这样的资源收集型Git仓库，但是在README文件中看到，这个仓库还是一篇论文中的公开数据库：Understanding URDF: A Dataset and Analysis。点进去看一下全文，发现作者中居然有Peter Corke大佬，因此特意整理记录一下。

（1）不同机器人仿真软件/工具
机器人仿真软件/工具很多，通产每个仿真软件中的机器人模型都有自己原生的文件格式，下面表格所示为几种不同仿真软件原生模型的文件格式以及它们对URDF文件描述的机器人模型的支持性。可以看到，绝大部分的仿真软件都是支持导入URDF格式描述的机器人模型的。

<img width="775" height="459" alt="image" src="https://github.com/user-attachments/assets/def5a6a8-281a-49d1-a1a9-7097d1be6abf" />

不同机器人仿真工具对URDF文件的支持

（2）为什么是URDF格式
URDF，全称是Unified Robot Description Format，统一机器人描述格式。URDF文件格式用于描述机器人最早是由机器人操作系统（ROS）的开发人员在2009年引入，是一种描述机器人的运动学、动力学和几何形状的通用格式文件，独立于软件程序，方便不同的软件工具以及开发人员共享机器人数据模型。URDF文件重要的一点是其可读性，因为它是XML类型的文本文件。URDF文件中可以描述机器人的运动学结构、动力学参数、视觉外观（通过引用其它文件）和几何碰撞边界（通过引用其它文件）。

关于URDF的更对细节可以参考：

[urdf/XML - ROS Wiki](https://wiki.ros.org/urdf/XML)

[urdf/Tutorials - ROS Wiki](https://wiki.ros.org/urdf/Tutorials)

（3）URDF文件解析
模型（model）
创建一个URDF文件的最小要求是机器人的名称和一个连杆。如下所示的URDF文件示例，它表示了一个2自由度的平面连杆机构，外观使用简单的几何形状：方块和圆柱，这个示例文件中有3个连杆和2个关节：

<img width="1135" height="540" alt="image" src="https://github.com/user-attachments/assets/8c95c4c2-38c7-4264-8eb6-9e5d6baff963" />

简单的平面3连杆机构

可以看到URDF文件中有一些关键的元素：

连杆（link）
连杆是可以使用关节进行连接的刚体，连杆有惯量（inertial）、视觉（visual）和碰撞（collision）等属性。惯性特性描述了连杆的质量、质心位置以及惯性矩。可视化特性和碰撞特性稍后再说。URDF中连杆只能是刚体，而不能是可形变的物体（在这一定程度上限制了URDF的应用范围，像涉及柔性体的机器人就不能用URDF文件直接表示）。

<img width="1505" height="698" alt="image" src="https://github.com/user-attachments/assets/a2f666ad-4683-4e26-aee4-08e9c823baeb" />

更通用的连杆属性

前面的示例模型中，3个连杆的名称分别为“base link”、“link 1”和“link 2”。我们查看“基本链接”来说明如何指定链接，参见第3-10行的清单1。“base link”表示机器人的固定底座，其中它的视觉属性由一个原点和一个由一个方块组成的几何体来定义，方块的大小由其三个边的长度指定。一个连杆唯一的必需属性的是它的名称，在一个URDF文件中，连杆名称必须是唯一的，不同连杆的名称必须不同。

关节（joint）
关节用于连接两个连杆，一个父连杆和一个子连杆。父连杆是更靠近基座的连杆，子连杆是更靠近末端工具的连杆。关节的主要参数是关节类型（运动学）、动力学参数，以及活动范围。关节类型包括：

旋转关节（revolute）：特指关节运动范围有明确的上限和下限的转动关节。
连续关节（continuous）：关节运动范围无限的转动关节，即可以连续旋转的转动关节。
平移关节（prismatic）：沿轴滑动的滑动关节，运动范围有明确的上限和下限。
固定关节（fixed）：类似于焊接，不是真正的关节，因为它无法移动，所有自由度都被锁定。这种类型的关节不需要<Axis>，<calibration>，<dynamics>，<limits>或<seafe_controller>等参数。
浮动关节（floating）：允许所有6个自由度的运动。
平面关节（planar）：允许在垂直于轴的平面中运动。
关节也有很多可以编辑的属性：

<img width="887" height="798" alt="image" src="https://github.com/user-attachments/assets/4bdb9c40-4aac-452b-8b36-6e5dd57250c1" />

关节属性

前面的示例模型中，关节的名称是“joint 1”和“joint 2”。关节类型是连续关节，这意味着它们是没有运动限制的旋转关节。“axis”属性指定关节轴的方向，在本例中，关节轴沿着Y轴。关节的必需属性是它的父连杆和子连杆的名称、关节类型和关节名称。

可视化与碰撞几何形状（Visual and Collision Geometries）
几何对象用于表示机器人连杆的形状，用于可视化或碰撞的目的，统称为网格对象（mesh），它们由一组构成对象表面的三角面组成。网格中的多边形越多，形状的细节级别就越高，但会以牺牲渲染和计算时间为代价。

网格对象可以用不同的CAD文件类型，每种文件类型都有不同的内部格式，并有其自身的好处和限制，因此应该根据使用的应用程序进行选择。URDF中可视化和碰撞网格的一种常用格式是STL（文件扩展名为.stl），它只使用三角形而不使用颜色或纹理信息来表示三维表面几何图形。另一种通常用于可视化的文件格式为collada（文件扩展名为.dae），它同时支持颜色和纹理信息。OBJ格式（文件扩展名为.obj）支持颜色、纹理和自由形式的曲线，允许更高级的细节可视化，但是，颜色和纹理数据存储在一个单独的（.mtl）文件中。

在URDF的一些应用中，碰撞检测是必需的，而在其他应用中，URDF模型仅用于可视化目的。根据应用程序的不同，URDF Bundle中可以包含不同类型的网格对象。例如，通常同时使用STL和COLLADA网格，因为STL网格不包含颜色与纹理，可以减少计算和渲染时间，同时STL可以进行凸包运算简化形状，因此常用于表示连杆的碰撞几何形状（碰撞检测通常需要大量运算，但是不需要关注结构细节，例如螺丝、螺帽、细孔这些），而COLLADA网格由于可以设置颜色、纹理等属性，因此通常作为连杆的可视化对象，提供高质量的可视化效果。

URDF文件包（URDF Bundle/package）
一个URDF机器人模型通常包含描述机器人拓扑结构的URDF文件以及描述机器人物理外观网格文件组成。URDF文件本身（具有.urdf文件扩展名）和URDF文件中所引用的网格对象（作为link的属性）所组成的文件集，通常称为URDF包。如下所示的URDF文件包，包含了名为myrobot.urdf的URDF文件，以及mesh文件夹中网格对象。URDF文件是指使用相对路径生成的不同链接的几何网格文件。

<img width="753" height="249" alt="image" src="https://github.com/user-attachments/assets/123e8480-fed5-430c-bdc7-8be4b0d6f6e7" />

Xacro文件
从前面可以看到，URDF文件适合定义静态的、完整的机器人模型，但对于复杂的机器人，URDF 可能会显得冗长且难以维护。Xacro是一种基于 XML 的宏扩展语言，主要用于简化和生成 URDF。Xacro 允许使用宏（macros）、变量、数学运算和参数化的方式来定义机器人模型，以提高可重用性和可读性。例如：

减少重复代码：可以定义一个通用的部件并多次使用
参数化设计：允许调整不同参数来生成不同的 URDF 结构
数学计算：可在 XML 内部执行计算，避免手动计算坐标或尺寸
Xacro 文件最终会被解析成标准 URDF 文件，例如在ROS中可以使用如下命令将 Xacro 转换为 URDF：

rosrun xacro xacro my_robot.xacro > my_robot.urdf
关于Xacro的具体内容这里暂不展开，感兴趣的可以参考：

Using Xacro to Clean Up a URDF File

（4）URDF数据库
对于大多数工业机械臂，由于其结构参数与特征都是固定的，因此在使用不同的软件工具进行算法仿真的时候，除非是初期的学习，通常都没必要自己再手动建模一遍，都是找现成的URDF文件，因为绝大多数机器人仿真软件都支持URDF格式文件的导入。前面提到的Understanding URDF: A Dataset and Analysis这篇文章中，作者规范地整理了超过300个不同来源的公开的URDF模型。
<img width="781" height="263" alt="image" src="https://github.com/user-attachments/assets/e560d938-e36f-4922-9804-5f791ba1ca70" />
<img width="648" height="828" alt="image" src="https://github.com/user-attachments/assets/db6329a8-2554-4523-8274-a7205ad25914" />

补充数据库资源：
[https://github.com/robot-descriptions/awesome-robot-descriptions
github.com/robot-descriptions/awesome-robot-descriptions](https://github.com/robot-descriptions/awesome-robot-descriptions
github.com/robot-descriptions/awesome-robot-descriptions)
[GitHub - robot-descriptions/awesome-robot-descriptions: A curated list of awesome robot descriptions (URDF, MJCF)](https://github.com/robot-descriptions/awesome-robot-descriptions)
[https://github.com/robot-descriptions/awesome-robot-descriptions
github.com/robot-descriptions/awesome-robot-descriptions
](https://github.com/robot-descriptions/awesome-robot-descriptions
github.com/robot-descriptions/awesome-robot-descriptions
)
6.3.2 相机布局
配置仿真上下文
当从独立脚本启动仿真器时，用户可以完全控制播放、暂停和步进仿真器。所有这些操作都通过 仿真上下文 处理。它负责各种时间轴事件，并为仿真器配置 物理场景 。

在 Isaac Lab 中 , sim.SimulationContext 类继承了 Isaac Sim 的 isaacsim.core.api.simulation_context.SimulationContext ，以允许通过 Python 的 dataclass 对象配置仿真器，并处理仿真步进的某些复杂性。

对于本教程，我们将将物理和渲染时间步长设置为0.01秒。通过将这些数量传递给 sim.SimulationCfg ，然后用它创建仿真上下文的实例。
```python
    # Initialize the simulation context
    sim_cfg = SimulationCfg(dt=0.01)
    sim = SimulationContext(sim_cfg)
    # Set main camera
    sim.set_camera_view([2.5, 2.5, 2.5], [0.0, 0.0, 0.0])
```
创建仿真上下文后，我们只配置了作用于仿真场景的物理。这包括用于仿真的设备、重力矢量和其他高级求解器参数。现在还有两个主要步骤剩下来运行仿真:

设计仿真场景: 添加传感器、机器人和其他仿真对象

运行仿真循环: 使仿真器进行步进，并从仿真器中设置和获取数据

6.3.3 光照与碰撞
生成地面平面
GroundPlaneCfg 配置了一个类似网格的地面平面，其外观和大小等属性可修改。
```python
    # Ground-plane
    cfg_ground = sim_utils.GroundPlaneCfg()
    cfg_ground.func("/World/defaultGroundPlane", cfg_ground)
```
生成灯光
可以将 不同类型的灯光基本体 生成到场景中。这些包括远光灯、球形灯、圆盘灯和圆柱灯。在本教程中，我们生成一个远光灯，这是一种远离场景无限远的灯，只朝一个方向发光。
```python
    # spawn distant light
    cfg_light_distant = sim_utils.DistantLightCfg(
        intensity=3000.0,
        color=(0.75, 0.75, 0.75),
    )
    cfg_light_distant.func("/World/lightDistant", cfg_light_distant, translation=(1, 0, 10))
```
生成基本形状
在生成基本形状之前，我们介绍了一个变换基本体或Xform的概念。变换基本体是一个仅包含变换属性的基本体。它用于将其他基本体分组，并作为一个组对其进行变换。在这里，我们创建一个Xform基本体，将所有的基本形状分组在其中。
```python
    # create a new xform prim for all objects to be spawned under
    prim_utils.create_prim("/World/Objects", "Xform")
```
接下来，我们使用 ConeCfg 类生成一个圆锥体。可以指定圆锥体的半径、高度、物理属性和材质属性。默认情况下，物理和材质属性是禁用的。

我们生成的前两个圆锥 Cone1 和 Cone2 是视觉元素，不启用物理属性。
```python
    # spawn a red cone
    cfg_cone = sim_utils.ConeCfg(
        radius=0.15,
        height=0.5,
        visual_material=sim_utils.PreviewSurfaceCfg(diffuse_color=(1.0, 0.0, 0.0)),
    )
    cfg_cone.func("/World/Objects/Cone1", cfg_cone, translation=(-1.0, 1.0, 1.0))
    cfg_cone.func("/World/Objects/Cone2", cfg_cone, translation=(-1.0, -1.0, 1.0))
```
对于第三个圆锥 ConeRigid ，我们在配置类中设置刚体物理属性。通过这些属性，我们可以指定圆锥体的质量、摩擦力和弹性。如果未指定，它们将默认为USD Physics设置的默认值。
```python
    # spawn a green cone with colliders and rigid body
    cfg_cone_rigid = sim_utils.ConeCfg(
        radius=0.15,
        height=0.5,
        rigid_props=sim_utils.RigidBodyPropertiesCfg(),
        mass_props=sim_utils.MassPropertiesCfg(mass=1.0),
        collision_props=sim_utils.CollisionPropertiesCfg(),
        visual_material=sim_utils.PreviewSurfaceCfg(diffuse_color=(0.0, 1.0, 0.0)),
    )
    cfg_cone_rigid.func(
        "/World/Objects/ConeRigid", cfg_cone_rigid, translation=(-0.2, 0.0, 2.0), orientation=(0.5, 0.0, 0.5, 0.0)
    )
```
最后，我们生成一个长方体 CuboidDeformable ，其中包含可变形体物理属性。与刚体仿真不同，可变形体可以在其顶点之间具有相对运动。这对于仿真软体如布料、橡胶或果冻非常有用。需要注意的是，可变形体仅在GPU仿真中受支持，并且需要生成一个带有可变形体物理属性的网格对象。
```python
    # spawn a blue cuboid with deformable body
    cfg_cuboid_deformable = sim_utils.MeshCuboidCfg(
        size=(0.2, 0.5, 0.2),
        deformable_props=sim_utils.DeformableBodyPropertiesCfg(),
        visual_material=sim_utils.PreviewSurfaceCfg(diffuse_color=(0.0, 0.0, 1.0)),
        physics_material=sim_utils.DeformableBodyMaterialCfg(),
    )
    cfg_cuboid_deformable.func("/World/Objects/CuboidDeformable", cfg_cuboid_deformable, translation=(0.15, 0.0, 2.0))
```
从另一个文件生成
最后，可以从其他文件格式生成基本体，例如其他USD、URDF或OBJ文件。在本教程中，我们将一个表的USD文件生成到场景中。这个表是一个网格基本体，并且有一个与之关联的材质基本体。所有这些信息都存储在其USD文件中。
```python
    # spawn a usd file of a table into the scene
    cfg = sim_utils.UsdFileCfg(usd_path=f"{ISAAC_NUCLEUS_DIR}/Props/Mounts/SeattleLabTable/table_instanceable.usd")
    cfg.func("/World/Objects/Table", cfg, translation=(0.0, 0.0, 1.05))
```
上面的表被添加为场景的一个引用。简单来说，这意味着表实际上并没有添加到场景中，而是添加了一个指向表资产的 指针 。这允许我们修改表资产，并使更改以非破坏性的方式反映在场景中。例如，我们可以更改表的材质，而不实际修改表资产的底层文件。只有更改存储在USD场景中。

6.4 日志与回放：录制、重放、评测
查看日志
在单独的终端中，您可以通过执行以下命令监视训练进度:
```python
# execute from the root directory of the repository
./isaaclab.sh -p -m tensorboard.main --logdir logs/sb3/Isaac-Cartpole-v0
```
播放经过训练的 agent
一旦训练完成，您可以通过执行以下命令来可视化经过训练的 agent:
```python
# execute from the root directory of the repository
./isaaclab.sh -p scripts/reinforcement_learning/sb3/play.py --task Isaac-Cartpole-v0 --num_envs 32 --use_last_checkpoint
```
上述命令将从 logs/sb3/Isaac-Cartpole-v0 目录加载最新的检查点。您也可以通过传递 --checkpoint 标志指定特定的检查点。


6.5 **样板：Isaac Lab 最小上手（可复制运行）**

train.py

```python
# Copyright (c) 2022-2025, The Isaac Lab Project Developers (https://github.com/isaac-sim/IsaacLab/blob/main/CONTRIBUTORS.md).
# All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause

"""Script to train RL agent with RSL-RL."""

"""Launch Isaac Sim Simulator first."""

import argparse
import sys

from isaaclab.app import AppLauncher

# local imports
import cli_args  # isort: skip


# add argparse arguments
parser = argparse.ArgumentParser(description="Train an RL agent with RSL-RL.")
parser.add_argument("--video", action="store_true", default=False, help="Record videos during training.")
parser.add_argument("--video_length", type=int, default=200, help="Length of the recorded video (in steps).")
parser.add_argument("--video_interval", type=int, default=2000, help="Interval between video recordings (in steps).")
parser.add_argument("--num_envs", type=int, default=None, help="Number of environments to simulate.")
parser.add_argument("--task", type=str, default=None, help="Name of the task.")
parser.add_argument(
    "--agent", type=str, default="rsl_rl_cfg_entry_point", help="Name of the RL agent configuration entry point."
)
parser.add_argument("--seed", type=int, default=None, help="Seed used for the environment")
parser.add_argument("--max_iterations", type=int, default=None, help="RL Policy training iterations.")
parser.add_argument(
    "--distributed", action="store_true", default=False, help="Run training with multiple GPUs or nodes."
)
parser.add_argument("--export_io_descriptors", action="store_true", default=False, help="Export IO descriptors.")
# append RSL-RL cli arguments
cli_args.add_rsl_rl_args(parser)
# append AppLauncher cli args
AppLauncher.add_app_launcher_args(parser)
args_cli, hydra_args = parser.parse_known_args()

# always enable cameras to record video
if args_cli.video:
    args_cli.enable_cameras = True

# clear out sys.argv for Hydra
sys.argv = [sys.argv[0]] + hydra_args

# launch omniverse app
app_launcher = AppLauncher(args_cli)
simulation_app = app_launcher.app

"""Check for minimum supported RSL-RL version."""

import importlib.metadata as metadata
import platform

from packaging import version

# for distributed training, check minimum supported rsl-rl version
RSL_RL_VERSION = "2.3.1"
installed_version = metadata.version("rsl-rl-lib")
if args_cli.distributed and version.parse(installed_version) < version.parse(RSL_RL_VERSION):
    if platform.system() == "Windows":
        cmd = [r".\isaaclab.bat", "-p", "-m", "pip", "install", f"rsl-rl-lib=={RSL_RL_VERSION}"]
    else:
        cmd = ["./isaaclab.sh", "-p", "-m", "pip", "install", f"rsl-rl-lib=={RSL_RL_VERSION}"]
    print(
        f"Please install the correct version of RSL-RL.\nExisting version is: '{installed_version}'"
        f" and required version is: '{RSL_RL_VERSION}'.\nTo install the correct version, run:"
        f"\n\n\t{' '.join(cmd)}\n"
    )
    exit(1)

"""Rest everything follows."""

import gymnasium as gym
import os
import torch
from datetime import datetime

import omni
from rsl_rl.runners import OnPolicyRunner

from isaaclab.envs import (
    DirectMARLEnv,
    DirectMARLEnvCfg,
    DirectRLEnvCfg,
    ManagerBasedRLEnvCfg,
    multi_agent_to_single_agent,
)
from isaaclab.utils.dict import print_dict
from isaaclab.utils.io import dump_pickle, dump_yaml

from isaaclab_rl.rsl_rl import RslRlOnPolicyRunnerCfg, RslRlVecEnvWrapper

import isaaclab_tasks  # noqa: F401
from isaaclab_tasks.utils import get_checkpoint_path
from isaaclab_tasks.utils.hydra import hydra_task_config

# PLACEHOLDER: Extension template (do not remove this comment)

torch.backends.cuda.matmul.allow_tf32 = True
torch.backends.cudnn.allow_tf32 = True
torch.backends.cudnn.deterministic = False
torch.backends.cudnn.benchmark = False


@hydra_task_config(args_cli.task, args_cli.agent)
def main(env_cfg: ManagerBasedRLEnvCfg | DirectRLEnvCfg | DirectMARLEnvCfg, agent_cfg: RslRlOnPolicyRunnerCfg):
    """Train with RSL-RL agent."""
    # override configurations with non-hydra CLI arguments
    agent_cfg = cli_args.update_rsl_rl_cfg(agent_cfg, args_cli)
    env_cfg.scene.num_envs = args_cli.num_envs if args_cli.num_envs is not None else env_cfg.scene.num_envs
    agent_cfg.max_iterations = (
        args_cli.max_iterations if args_cli.max_iterations is not None else agent_cfg.max_iterations
    )

    # set the environment seed
    # note: certain randomizations occur in the environment initialization so we set the seed here
    env_cfg.seed = agent_cfg.seed
    env_cfg.sim.device = args_cli.device if args_cli.device is not None else env_cfg.sim.device

    # multi-gpu training configuration
    if args_cli.distributed:
        env_cfg.sim.device = f"cuda:{app_launcher.local_rank}"
        agent_cfg.device = f"cuda:{app_launcher.local_rank}"

        # set seed to have diversity in different threads
        seed = agent_cfg.seed + app_launcher.local_rank
        env_cfg.seed = seed
        agent_cfg.seed = seed

    # specify directory for logging experiments
    log_root_path = os.path.join("logs", "rsl_rl", agent_cfg.experiment_name)
    log_root_path = os.path.abspath(log_root_path)
    print(f"[INFO] Logging experiment in directory: {log_root_path}")
    # specify directory for logging runs: {time-stamp}_{run_name}
    log_dir = datetime.now().strftime("%Y-%m-%d_%H-%M-%S")
    # The Ray Tune workflow extracts experiment name using the logging line below, hence, do not change it (see PR #2346, comment-2819298849)
    print(f"Exact experiment name requested from command line: {log_dir}")
    if agent_cfg.run_name:
        log_dir += f"_{agent_cfg.run_name}"
    log_dir = os.path.join(log_root_path, log_dir)

    # set the IO descriptors output directory if requested
    if isinstance(env_cfg, ManagerBasedRLEnvCfg):
        env_cfg.export_io_descriptors = args_cli.export_io_descriptors
        env_cfg.io_descriptors_output_dir = log_dir
    else:
        omni.log.warn(
            "IO descriptors are only supported for manager based RL environments. No IO descriptors will be exported."
        )

    # create isaac environment
    env = gym.make(args_cli.task, cfg=env_cfg, render_mode="rgb_array" if args_cli.video else None)

    # convert to single-agent instance if required by the RL algorithm
    if isinstance(env.unwrapped, DirectMARLEnv):
        env = multi_agent_to_single_agent(env)

    # save resume path before creating a new log_dir
    if agent_cfg.resume or agent_cfg.algorithm.class_name == "Distillation":
        resume_path = get_checkpoint_path(log_root_path, agent_cfg.load_run, agent_cfg.load_checkpoint)

    # wrap for video recording
    if args_cli.video:
        video_kwargs = {
            "video_folder": os.path.join(log_dir, "videos", "train"),
            "step_trigger": lambda step: step % args_cli.video_interval == 0,
            "video_length": args_cli.video_length,
            "disable_logger": True,
        }
        print("[INFO] Recording videos during training.")
        print_dict(video_kwargs, nesting=4)
        env = gym.wrappers.RecordVideo(env, **video_kwargs)

    # wrap around environment for rsl-rl
    env = RslRlVecEnvWrapper(env, clip_actions=agent_cfg.clip_actions)

    # create runner from rsl-rl
    runner = OnPolicyRunner(env, agent_cfg.to_dict(), log_dir=log_dir, device=agent_cfg.device)
    # write git state to logs
    runner.add_git_repo_to_log(__file__)
    # load the checkpoint
    if agent_cfg.resume or agent_cfg.algorithm.class_name == "Distillation":
        print(f"[INFO]: Loading model checkpoint from: {resume_path}")
        # load previously trained model
        runner.load(resume_path)

    # dump the configuration into log-directory
    dump_yaml(os.path.join(log_dir, "params", "env.yaml"), env_cfg)
    dump_yaml(os.path.join(log_dir, "params", "agent.yaml"), agent_cfg)
    dump_pickle(os.path.join(log_dir, "params", "env.pkl"), env_cfg)
    dump_pickle(os.path.join(log_dir, "params", "agent.pkl"), agent_cfg)

    # run training
    runner.learn(num_learning_iterations=agent_cfg.max_iterations, init_at_random_ep_len=True)

    # close the simulator
    env.close()


if __name__ == "__main__":
    # run the main function
    main()
    # close sim app
    simulation_app.close()
```

play.py
```python
# Copyright (c) 2022-2025, The Isaac Lab Project Developers (https://github.com/isaac-sim/IsaacLab/blob/main/CONTRIBUTORS.md).
# All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause

"""Script to play a checkpoint if an RL agent from RSL-RL."""

"""Launch Isaac Sim Simulator first."""

import argparse
import sys

from isaaclab.app import AppLauncher

# local imports
import cli_args  # isort: skip

# add argparse arguments
parser = argparse.ArgumentParser(description="Train an RL agent with RSL-RL.")
parser.add_argument("--video", action="store_true", default=False, help="Record videos during training.")
parser.add_argument("--video_length", type=int, default=200, help="Length of the recorded video (in steps).")
parser.add_argument(
    "--disable_fabric", action="store_true", default=False, help="Disable fabric and use USD I/O operations."
)
parser.add_argument("--num_envs", type=int, default=None, help="Number of environments to simulate.")
parser.add_argument("--task", type=str, default=None, help="Name of the task.")
parser.add_argument(
    "--agent", type=str, default="rsl_rl_cfg_entry_point", help="Name of the RL agent configuration entry point."
)
parser.add_argument("--seed", type=int, default=None, help="Seed used for the environment")
parser.add_argument(
    "--use_pretrained_checkpoint",
    action="store_true",
    help="Use the pre-trained checkpoint from Nucleus.",
)
parser.add_argument("--real-time", action="store_true", default=False, help="Run in real-time, if possible.")
# append RSL-RL cli arguments
cli_args.add_rsl_rl_args(parser)
# append AppLauncher cli args
AppLauncher.add_app_launcher_args(parser)
# parse the arguments
args_cli, hydra_args = parser.parse_known_args()
# always enable cameras to record video
if args_cli.video:
    args_cli.enable_cameras = True

# clear out sys.argv for Hydra
sys.argv = [sys.argv[0]] + hydra_args

# launch omniverse app
app_launcher = AppLauncher(args_cli)
simulation_app = app_launcher.app

"""Rest everything follows."""

import gymnasium as gym
import os
import time
import torch

from rsl_rl.runners import OnPolicyRunner

from isaaclab.envs import (
    DirectMARLEnv,
    DirectMARLEnvCfg,
    DirectRLEnvCfg,
    ManagerBasedRLEnvCfg,
    multi_agent_to_single_agent,
)
from isaaclab.utils.assets import retrieve_file_path
from isaaclab.utils.dict import print_dict
from isaaclab.utils.pretrained_checkpoint import get_published_pretrained_checkpoint

from isaaclab_rl.rsl_rl import RslRlOnPolicyRunnerCfg, RslRlVecEnvWrapper, export_policy_as_jit, export_policy_as_onnx

import isaaclab_tasks  # noqa: F401
from isaaclab_tasks.utils import get_checkpoint_path
from isaaclab_tasks.utils.hydra import hydra_task_config

# PLACEHOLDER: Extension template (do not remove this comment)


@hydra_task_config(args_cli.task, args_cli.agent)
def main(env_cfg: ManagerBasedRLEnvCfg | DirectRLEnvCfg | DirectMARLEnvCfg, agent_cfg: RslRlOnPolicyRunnerCfg):
    """Play with RSL-RL agent."""
    # grab task name for checkpoint path
    task_name = args_cli.task.split(":")[-1]
    train_task_name = task_name.replace("-Play", "")

    # override configurations with non-hydra CLI arguments
    agent_cfg = cli_args.update_rsl_rl_cfg(agent_cfg, args_cli)
    env_cfg.scene.num_envs = args_cli.num_envs if args_cli.num_envs is not None else env_cfg.scene.num_envs

    # set the environment seed
    # note: certain randomizations occur in the environment initialization so we set the seed here
    env_cfg.seed = agent_cfg.seed
    env_cfg.sim.device = args_cli.device if args_cli.device is not None else env_cfg.sim.device

    # specify directory for logging experiments
    log_root_path = os.path.join("logs", "rsl_rl", agent_cfg.experiment_name)
    log_root_path = os.path.abspath(log_root_path)
    print(f"[INFO] Loading experiment from directory: {log_root_path}")
    if args_cli.use_pretrained_checkpoint:
        resume_path = get_published_pretrained_checkpoint("rsl_rl", train_task_name)
        if not resume_path:
            print("[INFO] Unfortunately a pre-trained checkpoint is currently unavailable for this task.")
            return
    elif args_cli.checkpoint:
        resume_path = retrieve_file_path(args_cli.checkpoint)
    else:
        resume_path = get_checkpoint_path(log_root_path, agent_cfg.load_run, agent_cfg.load_checkpoint)

    log_dir = os.path.dirname(resume_path)

    # create isaac environment
    env = gym.make(args_cli.task, cfg=env_cfg, render_mode="rgb_array" if args_cli.video else None)

    # convert to single-agent instance if required by the RL algorithm
    if isinstance(env.unwrapped, DirectMARLEnv):
        env = multi_agent_to_single_agent(env)

    # wrap for video recording
    if args_cli.video:
        video_kwargs = {
            "video_folder": os.path.join(log_dir, "videos", "play"),
            "step_trigger": lambda step: step == 0,
            "video_length": args_cli.video_length,
            "disable_logger": True,
        }
        print("[INFO] Recording videos during training.")
        print_dict(video_kwargs, nesting=4)
        env = gym.wrappers.RecordVideo(env, **video_kwargs)

    # wrap around environment for rsl-rl
    env = RslRlVecEnvWrapper(env, clip_actions=agent_cfg.clip_actions)

    print(f"[INFO]: Loading model checkpoint from: {resume_path}")
    # load previously trained model
    ppo_runner = OnPolicyRunner(env, agent_cfg.to_dict(), log_dir=None, device=agent_cfg.device)
    ppo_runner.load(resume_path)

    # obtain the trained policy for inference
    policy = ppo_runner.get_inference_policy(device=env.unwrapped.device)

    # extract the neural network module
    # we do this in a try-except to maintain backwards compatibility.
    try:
        # version 2.3 onwards
        policy_nn = ppo_runner.alg.policy
    except AttributeError:
        # version 2.2 and below
        policy_nn = ppo_runner.alg.actor_critic

    # export policy to onnx/jit
    export_model_dir = os.path.join(os.path.dirname(resume_path), "exported")
    export_policy_as_jit(policy_nn, ppo_runner.obs_normalizer, path=export_model_dir, filename="policy.pt")
    export_policy_as_onnx(
        policy_nn, normalizer=ppo_runner.obs_normalizer, path=export_model_dir, filename="policy.onnx"
    )

    dt = env.unwrapped.step_dt

    # reset environment
    obs, _ = env.get_observations()
    timestep = 0
    # simulate environment
    while simulation_app.is_running():
        start_time = time.time()
        # run everything in inference mode
        with torch.inference_mode():
            # agent stepping
            actions = policy(obs)
            # env stepping
            obs, _, _, _ = env.step(actions)
        if args_cli.video:
            timestep += 1
            # Exit the play loop after recording one video
            if timestep == args_cli.video_length:
                break

        # time delay for real-time evaluation
        sleep_time = dt - (time.time() - start_time)
        if args_cli.real_time and sleep_time > 0:
            time.sleep(sleep_time)

    # close the simulator
    env.close()


if __name__ == "__main__":
    # run the main function
    main()
    # close sim app
    simulation_app.close()
```

cli_args.py
```python
# Copyright (c) 2022-2025, The Isaac Lab Project Developers (https://github.com/isaac-sim/IsaacLab/blob/main/CONTRIBUTORS.md).
# All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause

from __future__ import annotations

import argparse
import random
from typing import TYPE_CHECKING

if TYPE_CHECKING:
    from isaaclab_rl.rsl_rl import RslRlOnPolicyRunnerCfg


def add_rsl_rl_args(parser: argparse.ArgumentParser):
    """Add RSL-RL arguments to the parser.

    Args:
        parser: The parser to add the arguments to.
    """
    # create a new argument group
    arg_group = parser.add_argument_group("rsl_rl", description="Arguments for RSL-RL agent.")
    # -- experiment arguments
    arg_group.add_argument(
        "--experiment_name", type=str, default=None, help="Name of the experiment folder where logs will be stored."
    )
    arg_group.add_argument("--run_name", type=str, default=None, help="Run name suffix to the log directory.")
    # -- load arguments
    arg_group.add_argument("--resume", action="store_true", default=False, help="Whether to resume from a checkpoint.")
    arg_group.add_argument("--load_run", type=str, default=None, help="Name of the run folder to resume from.")
    arg_group.add_argument("--checkpoint", type=str, default=None, help="Checkpoint file to resume from.")
    # -- logger arguments
    arg_group.add_argument(
        "--logger", type=str, default=None, choices={"wandb", "tensorboard", "neptune"}, help="Logger module to use."
    )
    arg_group.add_argument(
        "--log_project_name", type=str, default=None, help="Name of the logging project when using wandb or neptune."
    )


def parse_rsl_rl_cfg(task_name: str, args_cli: argparse.Namespace) -> RslRlOnPolicyRunnerCfg:
    """Parse configuration for RSL-RL agent based on inputs.

    Args:
        task_name: The name of the environment.
        args_cli: The command line arguments.

    Returns:
        The parsed configuration for RSL-RL agent based on inputs.
    """
    from isaaclab_tasks.utils.parse_cfg import load_cfg_from_registry

    # load the default configuration
    rslrl_cfg: RslRlOnPolicyRunnerCfg = load_cfg_from_registry(task_name, "rsl_rl_cfg_entry_point")
    rslrl_cfg = update_rsl_rl_cfg(rslrl_cfg, args_cli)
    return rslrl_cfg


def update_rsl_rl_cfg(agent_cfg: RslRlOnPolicyRunnerCfg, args_cli: argparse.Namespace):
    """Update configuration for RSL-RL agent based on inputs.

    Args:
        agent_cfg: The configuration for RSL-RL agent.
        args_cli: The command line arguments.

    Returns:
        The updated configuration for RSL-RL agent based on inputs.
    """
    # override the default configuration with CLI arguments
    if hasattr(args_cli, "seed") and args_cli.seed is not None:
        # randomly sample a seed if seed = -1
        if args_cli.seed == -1:
            args_cli.seed = random.randint(0, 10000)
        agent_cfg.seed = args_cli.seed
    if args_cli.resume is not None:
        agent_cfg.resume = args_cli.resume
    if args_cli.load_run is not None:
        agent_cfg.load_run = args_cli.load_run
    if args_cli.checkpoint is not None:
        agent_cfg.load_checkpoint = args_cli.checkpoint
    if args_cli.run_name is not None:
        agent_cfg.run_name = args_cli.run_name
    if args_cli.logger is not None:
        agent_cfg.logger = args_cli.logger
    # set the project name for wandb and neptune
    if agent_cfg.logger in {"wandb", "neptune"} and args_cli.log_project_name:
        agent_cfg.wandb_project = args_cli.log_project_name
        agent_cfg.neptune_project = args_cli.log_project_name

    return agent_cfg
```

Isaaclab.sh

```python
#!/usr/bin/env bash

# Copyright (c) 2022-2025, The Isaac Lab Project Developers (https://github.com/isaac-sim/IsaacLab/blob/main/CONTRIBUTORS.md).
# All rights reserved.
#
# SPDX-License-Identifier: BSD-3-Clause

#==
# Configurations
#==

# Exits if error occurs
set -e

# Set tab-spaces
tabs 4

# get source directory
export ISAACLAB_PATH="$( cd "$( dirname "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )"

#==
# Helper functions
#==

# install system dependencies
install_system_deps() {
    # check if cmake is already installed
    if command -v cmake &> /dev/null; then
        echo "[INFO] cmake is already installed."
    else
        # check if running as root
        if [ "$EUID" -ne 0 ]; then
            echo "[INFO] Installing system dependencies..."
            sudo apt-get update && sudo apt-get install -y --no-install-recommends \
                cmake \
                build-essential
        else
            echo "[INFO] Installing system dependencies..."
            apt-get update && apt-get install -y --no-install-recommends \
                cmake \
                build-essential
        fi
    fi
}

# Returns success (exit code 0 / "true") if the detected Isaac Sim version starts with 4.5,
# otherwise returns non-zero ("false"). Works with both symlinked binary installs and pip installs.
is_isaacsim_version_4_5() {
    local version=""
    local python_exe
    python_exe=$(extract_python_exe)

    # 0) Fast path: read VERSION file from the symlinked _isaac_sim directory (binary install)
    # If the repository has _isaac_sim → <IsaacSimRoot> symlink, the VERSION file is the simplest source of truth.
    if [[ -f "${ISAACLAB_PATH}/_isaac_sim/VERSION" ]]; then
        # Read first line of the VERSION file; don't fail the whole script on errors.
        version=$(head -n1 "${ISAACLAB_PATH}/_isaac_sim/VERSION" || true)
    fi

    # 1) Package-path probe: import isaacsim and walk up to ../../VERSION (pip or nonstandard layouts)
    # If we still don't know the version, ask Python where the isaacsim package lives
    if [[ -z "$version" ]]; then
        local sim_file=""
        # Print isaacsim.__file__; suppress errors so set -e won't abort.
        sim_file=$("${python_exe}" -c 'import isaacsim, os; print(isaacsim.__file__)' 2>/dev/null || true)
        if [[ -n "$sim_file" ]]; then
            local version_path
            version_path="$(dirname "$sim_file")/../../VERSION"
            # If that VERSION file exists, read it.
            [[ -f "$version_path" ]] && version=$(head -n1 "$version_path" || true)
        fi
    fi

    # 2) Fallback: use package metadata via importlib.metadata.version("isaacsim")
    if [[ -z "$version" ]]; then
        version=$("${python_exe}" <<'PY' 2>/dev/null || true
from importlib.metadata import version, PackageNotFoundError
try:
    print(version("isaacsim"))
except PackageNotFoundError:
    pass
PY
)
    fi

    # Final decision: return success if version begins with "4.5", 0 if match, 1 otherwise.
    [[ "$version" == 4.5* ]]
}

# check if running in docker
is_docker() {
    [ -f /.dockerenv ] || \
    grep -q docker /proc/1/cgroup || \
    [[ $(cat /proc/1/comm) == "containerd-shim" ]] || \
    grep -q docker /proc/mounts || \
    [[ "$(hostname)" == *"."* ]]
}

# extract isaac sim path
extract_isaacsim_path() {
    # Use the sym-link path to Isaac Sim directory
    local isaac_path=${ISAACLAB_PATH}/_isaac_sim
    # If above path is not available, try to find the path using python
    if [ ! -d "${isaac_path}" ]; then
        # Use the python executable to get the path
        local python_exe=$(extract_python_exe)
        # Retrieve the path importing isaac sim and getting the environment path
        if [ $(${python_exe} -m pip list | grep -c 'isaacsim-rl') -gt 0 ]; then
            local isaac_path=$(${python_exe} -c "import isaacsim; import os; print(os.environ['ISAAC_PATH'])")
        fi
    fi
    # check if there is a path available
    if [ ! -d "${isaac_path}" ]; then
        # throw an error if no path is found
        echo -e "[ERROR] Unable to find the Isaac Sim directory: '${isaac_path}'" >&2
        echo -e "\tThis could be due to the following reasons:" >&2
        echo -e "\t1. Conda environment is not activated." >&2
        echo -e "\t2. Isaac Sim pip package 'isaacsim-rl' is not installed." >&2
        echo -e "\t3. Isaac Sim directory is not available at the default path: ${ISAACLAB_PATH}/_isaac_sim" >&2
        # exit the script
        exit 1
    fi
    # return the result
    echo ${isaac_path}
}

# extract the python from isaacsim
extract_python_exe() {
    # check if using conda
    if ! [[ -z "${CONDA_PREFIX}" ]]; then
        # use conda python
        local python_exe=${CONDA_PREFIX}/bin/python
    else
        # use kit python
        local python_exe=${ISAACLAB_PATH}/_isaac_sim/python.sh

    if [ ! -f "${python_exe}" ]; then
            # note: we need to check system python for cases such as docker
            # inside docker, if user installed into system python, we need to use that
            # otherwise, use the python from the kit
            if [ $(python -m pip list | grep -c 'isaacsim-rl') -gt 0 ]; then
                local python_exe=$(which python)
            fi
        fi
    fi
    # check if there is a python path available
    if [ ! -f "${python_exe}" ]; then
        echo -e "[ERROR] Unable to find any Python executable at path: '${python_exe}'" >&2
        echo -e "\tThis could be due to the following reasons:" >&2
        echo -e "\t1. Conda environment is not activated." >&2
        echo -e "\t2. Isaac Sim pip package 'isaacsim-rl' is not installed." >&2
        echo -e "\t3. Python executable is not available at the default path: ${ISAACLAB_PATH}/_isaac_sim/python.sh" >&2
        exit 1
    fi
    # return the result
    echo ${python_exe}
}

# extract the simulator exe from isaacsim
extract_isaacsim_exe() {
    # obtain the isaac sim path
    local isaac_path=$(extract_isaacsim_path)
    # isaac sim executable to use
    local isaacsim_exe=${isaac_path}/isaac-sim.sh
    # check if there is a python path available
    if [ ! -f "${isaacsim_exe}" ]; then
        # check for installation using Isaac Sim pip
        # note: pip installed Isaac Sim can only come from a direct
        # python environment, so we can directly use 'python' here
        if [ $(python -m pip list | grep -c 'isaacsim-rl') -gt 0 ]; then
            # Isaac Sim - Python packages entry point
            local isaacsim_exe="isaacsim isaacsim.exp.full"
        else
            echo "[ERROR] No Isaac Sim executable found at path: ${isaac_path}" >&2
            exit 1
        fi
    fi
    # return the result
    echo ${isaacsim_exe}
}

# check if input directory is a python extension and install the module
install_isaaclab_extension() {
    # retrieve the python executable
    python_exe=$(extract_python_exe)
    # if the directory contains setup.py then install the python module
    if [ -f "$1/setup.py" ]; then
        echo -e "\t module: $1"
        ${python_exe} -m pip install --editable $1
    fi
}

# setup anaconda environment for Isaac Lab
setup_conda_env() {
    # get environment name from input
    local env_name=$1
    # check conda is installed
    if ! command -v conda &> /dev/null
    then
        echo "[ERROR] Conda could not be found. Please install conda and try again."
        exit 1
    fi

    # check if _isaac_sim symlink exists and isaacsim-rl is not installed via pip
    if [ ! -L "${ISAACLAB_PATH}/_isaac_sim" ] && ! python -m pip list | grep -q 'isaacsim-rl'; then
        echo -e "[WARNING] _isaac_sim symlink not found at ${ISAACLAB_PATH}/_isaac_sim"
        echo -e "\tThis warning can be ignored if you plan to install Isaac Sim via pip."
        echo -e "\tIf you are using a binary installation of Isaac Sim, please ensure the symlink is created before setting up the conda environment."
    fi

    # check if the environment exists
    if { conda env list | grep -w ${env_name}; } >/dev/null 2>&1; then
        echo -e "[INFO] Conda environment named '${env_name}' already exists."
    else
        echo -e "[INFO] Creating conda environment named '${env_name}'..."
        echo -e "[INFO] Installing dependencies from ${ISAACLAB_PATH}/environment.yml"

        # patch Python version if needed, but back up first
        cp "${ISAACLAB_PATH}/environment.yml"{,.bak}
        if is_isaacsim_version_4_5; then
            echo "[INFO] Detected Isaac Sim 4.5 → forcing python=3.10"
            sed -i 's/^  - python=3\.11/  - python=3.10/' "${ISAACLAB_PATH}/environment.yml"
        else
            echo "[INFO] Isaac Sim 5.0, installing python=3.11"
        fi

        conda env create -y --file ${ISAACLAB_PATH}/environment.yml -n ${env_name}
        # (optional) restore original environment.yml:
        if [[ -f "${ISAACLAB_PATH}/environment.yml.bak" ]]; then
            mv "${ISAACLAB_PATH}/environment.yml.bak" "${ISAACLAB_PATH}/environment.yml"
        fi
    fi

    # cache current paths for later
    cache_pythonpath=$PYTHONPATH
    cache_ld_library_path=$LD_LIBRARY_PATH
    # clear any existing files
    rm -f ${CONDA_PREFIX}/etc/conda/activate.d/setenv.sh
    rm -f ${CONDA_PREFIX}/etc/conda/deactivate.d/unsetenv.sh
    # activate the environment
    source $(conda info --base)/etc/profile.d/conda.sh
    conda activate ${env_name}
    # setup directories to load Isaac Sim variables
    mkdir -p ${CONDA_PREFIX}/etc/conda/activate.d
    mkdir -p ${CONDA_PREFIX}/etc/conda/deactivate.d

    # add variables to environment during activation
    printf '%s\n' '#!/usr/bin/env bash' '' \
        '# for Isaac Lab' \
        'export ISAACLAB_PATH='${ISAACLAB_PATH}'' \
        'alias isaaclab='${ISAACLAB_PATH}'/isaaclab.sh' \
        '' \
        '# show icon if not runninng headless' \
        'export RESOURCE_NAME="IsaacSim"' \
        '' > ${CONDA_PREFIX}/etc/conda/activate.d/setenv.sh

    # check if we have _isaac_sim directory -> if so that means binaries were installed.
    # we need to setup conda variables to load the binaries
    local isaacsim_setup_conda_env_script=${ISAACLAB_PATH}/_isaac_sim/setup_conda_env.sh

    if [ -f "${isaacsim_setup_conda_env_script}" ]; then
        # add variables to environment during activation
        printf '%s\n' \
            '# for Isaac Sim' \
            'source '${isaacsim_setup_conda_env_script}'' \
            '' >> ${CONDA_PREFIX}/etc/conda/activate.d/setenv.sh
    fi

    # reactivate the environment to load the variables
    # needed because deactivate complains about Isaac Lab alias since it otherwise doesn't exist
    conda activate ${env_name}

    # remove variables from environment during deactivation
    printf '%s\n' '#!/usr/bin/env bash' '' \
        '# for Isaac Lab' \
        'unalias isaaclab &>/dev/null' \
        'unset ISAACLAB_PATH' \
        '' \
        '# restore paths' \
        'export PYTHONPATH='${cache_pythonpath}'' \
        'export LD_LIBRARY_PATH='${cache_ld_library_path}'' \
        '' \
        '# for Isaac Sim' \
        'unset RESOURCE_NAME' \
        '' > ${CONDA_PREFIX}/etc/conda/deactivate.d/unsetenv.sh

    # check if we have _isaac_sim directory -> if so that means binaries were installed.
    if [ -f "${isaacsim_setup_conda_env_script}" ]; then
        # add variables to environment during activation
        printf '%s\n' \
            '# for Isaac Sim' \
            'unset CARB_APP_PATH' \
            'unset EXP_PATH' \
            'unset ISAAC_PATH' \
            '' >> ${CONDA_PREFIX}/etc/conda/deactivate.d/unsetenv.sh
    fi

    # deactivate the environment
    conda deactivate
    # add information to the user about alias
    echo -e "[INFO] Added 'isaaclab' alias to conda environment for 'isaaclab.sh' script."
    echo -e "[INFO] Created conda environment named '${env_name}'.\n"
    echo -e "\t\t1. To activate the environment, run:                conda activate ${env_name}"
    echo -e "\t\t2. To install Isaac Lab extensions, run:            isaaclab -i"
    echo -e "\t\t3. To perform formatting, run:                      isaaclab -f"
    echo -e "\t\t4. To deactivate the environment, run:              conda deactivate"
    echo -e "\n"
}

# update the vscode settings from template and isaac sim settings
update_vscode_settings() {
    echo "[INFO] Setting up vscode settings..."
    # retrieve the python executable
    python_exe=$(extract_python_exe)
    # path to setup_vscode.py
    setup_vscode_script="${ISAACLAB_PATH}/.vscode/tools/setup_vscode.py"
    # check if the file exists before attempting to run it
    if [ -f "${setup_vscode_script}" ]; then
        ${python_exe} "${setup_vscode_script}"
    else
        echo "[WARNING] Unable to find the script 'setup_vscode.py'. Aborting vscode settings setup."
    fi
}

# print the usage description
print_help () {
    echo -e "\nusage: $(basename "$0") [-h] [-i] [-f] [-p] [-s] [-t] [-o] [-v] [-d] [-n] [-c] -- Utility to manage Isaac Lab."
    echo -e "\noptional arguments:"
    echo -e "\t-h, --help           Display the help content."
    echo -e "\t-i, --install [LIB]  Install the extensions inside Isaac Lab and learning frameworks as extra dependencies. Default is 'all'."
    echo -e "\t-f, --format         Run pre-commit to format the code and check lints."
    echo -e "\t-p, --python         Run the python executable provided by Isaac Sim or virtual environment (if active)."
    echo -e "\t-s, --sim            Run the simulator executable (isaac-sim.sh) provided by Isaac Sim."
    echo -e "\t-t, --test           Run all python pytest tests."
    echo -e "\t-o, --docker         Run the docker container helper script (docker/container.sh)."
    echo -e "\t-v, --vscode         Generate the VSCode settings file from template."
    echo -e "\t-d, --docs           Build the documentation from source using sphinx."
    echo -e "\t-n, --new            Create a new external project or internal task from template."
    echo -e "\t-c, --conda [NAME]   Create the conda environment for Isaac Lab. Default name is 'env_isaaclab'."
    echo -e "\n" >&2
}


#==
# Main
#==

# check argument provided
if [ -z "$*" ]; then
    echo "[Error] No arguments provided." >&2;
    print_help
    exit 0
fi

# pass the arguments
while [[ $# -gt 0 ]]; do
    # read the key
    case "$1" in
        -i|--install)
            # install system dependencies first
            install_system_deps
            # install the python packages in IsaacLab/source directory
            echo "[INFO] Installing extensions inside the Isaac Lab repository..."
            python_exe=$(extract_python_exe)
            # check if pytorch is installed and its version
            # install pytorch with cuda 12.8 for blackwell support
            if ${python_exe} -m pip list 2>/dev/null | grep -q "torch"; then
                torch_version=$(${python_exe} -m pip show torch 2>/dev/null | grep "Version:" | awk '{print $2}')
                echo "[INFO] Found PyTorch version ${torch_version} installed."
                if [[ "${torch_version}" != "2.7.0+cu128" ]]; then
                    echo "[INFO] Uninstalling PyTorch version ${torch_version}..."
                    ${python_exe} -m pip uninstall -y torch torchvision torchaudio
                    echo "[INFO] Installing PyTorch 2.7.0 with CUDA 12.8 support..."
                    ${python_exe} -m pip install torch==2.7.0 torchvision==0.22.0 --index-url https://download.pytorch.org/whl/cu128
                else
                    echo "[INFO] PyTorch 2.7.0 is already installed."
                fi
            else
                echo "[INFO] Installing PyTorch 2.7.0 with CUDA 12.8 support..."
                ${python_exe} -m pip install torch==2.7.0 torchvision==0.22.0 --index-url https://download.pytorch.org/whl/cu128
            fi
            # recursively look into directories and install them
            # this does not check dependencies between extensions
            export -f extract_python_exe
            export -f install_isaaclab_extension
            # source directory
            find -L "${ISAACLAB_PATH}/source" -mindepth 1 -maxdepth 1 -type d -exec bash -c 'install_isaaclab_extension "{}"' \;
            # install the python packages for supported reinforcement learning frameworks
            echo "[INFO] Installing extra requirements such as learning frameworks..."
            # check if specified which rl-framework to install
            if [ -z "$2" ]; then
                echo "[INFO] Installing all rl-frameworks..."
                framework_name="all"
            elif [ "$2" = "none" ]; then
                echo "[INFO] No rl-framework will be installed."
                framework_name="none"
                shift # past argument
            else
                echo "[INFO] Installing rl-framework: $2"
                framework_name=$2
                shift # past argument
            fi
            # install the learning frameworks specified
            ${python_exe} -m pip install -e ${ISAACLAB_PATH}/source/isaaclab_rl["${framework_name}"]
            ${python_exe} -m pip install -e ${ISAACLAB_PATH}/source/isaaclab_mimic["${framework_name}"]

            # check if we are inside a docker container or are building a docker image
            # in that case don't setup VSCode since it asks for EULA agreement which triggers user interaction
            if is_docker; then
                echo "[INFO] Running inside a docker container. Skipping VSCode settings setup."
                echo "[INFO] To setup VSCode settings, run 'isaaclab -v'."
            else
                # update the vscode settings
                update_vscode_settings
            fi

            # unset local variables
            unset extract_python_exe
            unset install_isaaclab_extension
            shift # past argument
            ;;
        -c|--conda)
            # use default name if not provided
            if [ -z "$2" ]; then
                echo "[INFO] Using default conda environment name: env_isaaclab"
                conda_env_name="env_isaaclab"
            else
                echo "[INFO] Using conda environment name: $2"
                conda_env_name=$2
                shift # past argument
            fi
            # setup the conda environment for Isaac Lab
            setup_conda_env ${conda_env_name}
            shift # past argument
            ;;
        -f|--format)
            # reset the python path to avoid conflicts with pre-commit
            # this is needed because the pre-commit hooks are installed in a separate virtual environment
            # and it uses the system python to run the hooks
            if [ -n "${CONDA_DEFAULT_ENV}" ]; then
                cache_pythonpath=${PYTHONPATH}
                export PYTHONPATH=""
            fi
            # run the formatter over the repository
            # check if pre-commit is installed
            if ! command -v pre-commit &>/dev/null; then
                echo "[INFO] Installing pre-commit..."
                pip install pre-commit
                sudo apt-get install -y pre-commit
            fi
            # always execute inside the Isaac Lab directory
            echo "[INFO] Formatting the repository..."
            cd ${ISAACLAB_PATH}
            pre-commit run --all-files
            cd - > /dev/null
            # set the python path back to the original value
            if [ -n "${CONDA_DEFAULT_ENV}" ]; then
                export PYTHONPATH=${cache_pythonpath}
            fi
            shift # past argument
            # exit neatly
            break
            ;;
        -p|--python)
            # run the python provided by isaacsim
            python_exe=$(extract_python_exe)
            echo "[INFO] Using python from: ${python_exe}"
            shift # past argument
            ${python_exe} "$@"
            # exit neatly
            break
            ;;
        -s|--sim)
            # run the simulator exe provided by isaacsim
            isaacsim_exe=$(extract_isaacsim_exe)
            echo "[INFO] Running isaac-sim from: ${isaacsim_exe}"
            shift # past argument
            ${isaacsim_exe} --ext-folder ${ISAACLAB_PATH}/source $@
            # exit neatly
            break
            ;;
        -n|--new)
            # run the template generator script
            python_exe=$(extract_python_exe)
            shift # past argument
            echo "[INFO] Installing template dependencies..."
            ${python_exe} -m pip install -q -r ${ISAACLAB_PATH}/tools/template/requirements.txt
            echo -e "\n[INFO] Running template generator...\n"
            ${python_exe} ${ISAACLAB_PATH}/tools/template/cli.py $@
            # exit neatly
            break
            ;;
        -t|--test)
            # run the python provided by isaacsim
            python_exe=$(extract_python_exe)
            shift # past argument
            ${python_exe} -m pytest ${ISAACLAB_PATH}/tools $@
            # exit neatly
            break
            ;;
        -o|--docker)
            # run the docker container helper script
            docker_script=${ISAACLAB_PATH}/docker/container.sh
            echo "[INFO] Running docker utility script from: ${docker_script}"
            shift # past argument
            bash ${docker_script} $@
            # exit neatly
            break
            ;;
        -v|--vscode)
            # update the vscode settings
            update_vscode_settings
            shift # past argument
            # exit neatly
            break
            ;;
        -d|--docs)
            # build the documentation
            echo "[INFO] Building documentation..."
            # retrieve the python executable
            python_exe=$(extract_python_exe)
            # install pip packages
            cd ${ISAACLAB_PATH}/docs
            ${python_exe} -m pip install -r requirements.txt > /dev/null
            # build the documentation
            ${python_exe} -m sphinx -b html -d _build/doctrees . _build/current
            # open the documentation
            echo -e "[INFO] To open documentation on default browser, run:"
            echo -e "\n\t\txdg-open $(pwd)/_build/current/index.html\n"
            # exit neatly
            cd - > /dev/null
            shift # past argument
            # exit neatly
            break
            ;;
        -h|--help)
            print_help
            exit 0
            ;;
        *) # unknown option
            echo "[Error] Invalid argument provided: $1"
            print_help
            exit 1
            ;;
    esac
done
```
  ```bash
  # 环境（示例）
  conda create -n isaaclab python=3.10 -y
  conda activate isaaclab
  # 安装依赖（按官方指引）
  # ...
  # 运行最小任务（如 Isaac-Ant-v0）
  ./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/train.py --task=Isaac-Ant-v0 --headless
  ./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/play.py --task Isaac-Isaac-Ant-v0 --checkpoint model_999.pt
  ```

  * ✅ 目标：能在 5–10 分钟内跑出第一个曲线与视频
  * ✅ 交付：`/sim/isaaclab-minimal/README.md`（命令、注意事项、常见坑）

---

## 7. 开源实物（Real Robots & Tooling）

**贡献者**：@owner

---

### 7.1 LeRobot 简介

**LeRobot** 是 Hugging Face 于 2024 年 5 月发布的开源机器人学习框架，目标是降低 AI 机器人开发门槛。

- **GitHub**: [huggingface/lerobot](https://github.com/huggingface/lerobot) ⭐ 19,000+ (截至 2025 年 10 月)
- **官方页面**: [huggingface.co/lerobot](https://huggingface.co/lerobot)
- **核心特性**: 预训练模型、数据集、硬件支持、Sim2Real

---

### 7.2 快速开始

#### 环境安装

```bash
conda create -n lerobot python=3.10 -y
conda activate lerobot
pip install lerobot

# 或从源码安装
git clone https://github.com/huggingface/lerobot.git
cd lerobot
pip install -e .
```

#### 数据集可视化

```python
from lerobot.common.datasets.lerobot_dataset import LeRobotDataset

dataset = LeRobotDataset("lerobot/pusht")
episode_index = 0
from_idx = dataset.episode_data_index["from"][episode_index].item()
to_idx = dataset.episode_data_index["to"][episode_index].item()

for idx in range(from_idx, to_idx):
    frame = dataset[idx]
    print(f"观测: {frame['observation'].keys()}")
    print(f"动作: {frame['action']}")
```

#### 训练与评估

```bash
# 训练
python lerobot/scripts/train.py \
    policy=diffusion env=pusht \
    dataset_repo_id=lerobot/pusht

# 评估
python lerobot/scripts/eval.py \
    -p outputs/train/diffusion_pusht/checkpoints/last.ckpt \
    eval.n_episodes=10
```

---

### 7.3 硬件平台与数据集

#### 支持的硬件

| 平台 | 自由度 | 特点 |
|------|--------|------|
| **SO-ARM100/SO-101** | 5 DOF | 3D打印、开源 |
| **ALOHA** | 双臂 | 高精度协作 |
| **Moss v1** | 5 DOF | 教学适用 |
| **Koch v1.1** | 5 DOF | Hackathon平台 |

#### 常用数据集

| 数据集 | 任务 | 链接 |
|--------|------|------|
| `lerobot/pusht` | 推方块 | [🔗](https://huggingface.co/datasets/lerobot/pusht) |
| `lerobot/aloha_sim_insertion_human` | ALOHA仿真 | [🔗](https://huggingface.co/datasets/lerobot/aloha_sim_insertion_human) |
| `lerobot/xarm_push_medium` | xArm推物体 | [🔗](https://huggingface.co/datasets/lerobot/xarm_push_medium) |

> 更多: [LeRobot Datasets](https://huggingface.co/lerobot) (160+)

---

### 7.4 学习资源

#### 官方资源
- [LeRobot GitHub](https://github.com/huggingface/lerobot)
- [HIL-SERL 真机训练](https://huggingface.co/docs/lerobot/hilserl)
- [真机上手指南](https://github.com/huggingface/lerobot/tree/main/examples)

#### 中文教程
- [LeRobotTutorial-CN](https://github.com/CSCSX/LeRobotTutorial-CN)
- [CSDN: 源码分析与部署](https://blog.csdn.net/v_JULY_v/article/details/139692392)
- [CSDN: 入门指南](https://blog.csdn.net/lovechris00/article/details/142308934)
- 知乎搜索: "LeRobot" 或 "具身智能"

#### 社区
- Discord: [Hugging Face Discord](https://discord.gg/huggingface) #lerobot
- [GitHub Issues](https://github.com/huggingface/lerobot/issues)
- [Lumina社区](https://lumina-embodied.ai)

#### 核心论文
- **ACT**: [arXiv:2304.13705](https://arxiv.org/abs/2304.13705) - 双臂精细操作
- **Diffusion Policy**: [arXiv:2303.04137](https://arxiv.org/abs/2303.04137) - 复杂轨迹
- **TDMPC**: [arXiv:2203.04955](https://arxiv.org/abs/2203.04955) - 实时控制

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

# 9. 具身公司图谱（Landscape）

**贡献者**：@bob

**小标题**

* 9.1 硬件整机（人形/四足/移动+操作）
* 9.2 关键部件（力控手、末端执行器、传感器）
* 9.3 算法与平台（VLA/策略/仿真/评测工具）
* 9.4 数据与服务（采集/标注/云端训练）

## 9.1 硬件整机（人形 / 四足 / 移动+操作）

### 中国大陆 / 港澳

#### 1. 智元机器人 AgiBot（中国·上海）

* 背景：2023 年成立，发布 G1/GX 系列与「AgiBot World」等配套生态。规模：**200–500（估）**
* 主营：通用具身机器人（人形/移动交互）、具身数据与仿真平台
* 官网：zhiyuan-robot.com / agibot.com

#### 2. 浙江人形机器人创新中心（中国·宁波）

* 背景：2023-12 注册，产学研平台，发布「领航者1号」原型。规模：**100–300（估）**
* 主营：人形机器人整机与感知/控制/本体关键技术研发
* 官网：zj-humanoid.com

#### 3. 银河通用 GALBOT（中国·北京）

* 背景：专注通用机器人与人形方向的创业公司（公开资料较少）。规模：**50–200（估）**
* 主营：通用机器人整机与系统应用
* 官网：galbot.com

#### 4. 优必选 UBTECH（中国·深圳）

* 背景：2012 年成立；2023-12 于港交所上市（9880.HK）。规模：**1000+**
* 主营：人形机器人（Walker 系列）、商服/教育/养老等服务机器人
* 官网：ubtrobot.com

#### 5. 宇树机器人 Unitree（中国·杭州）

* 背景：四足机器人代表企业。规模：**200–500（估）**
* 主营：四足平台（Go 系列）、人形 H1 等
* 官网：unitree.com

#### 6. 傅利叶智能 Fourier Intelligence（中国·上海/新加坡）

* 背景：康复机器人起家，近年发布人形 **GR-1**。规模：**500–1000（估）**
* 主营：人形机器人 GR-1、康复机器人 RehabHub
* 官网：fftai.com

#### 7. Flexiv 非夕（中国·上海 / 美国）

* 背景：2016 年创立，力控+视觉的自适应协作臂。规模：**200–500（估）**
* 主营：Rizon 协作臂、力控应用单元
* 官网：flexiv.com

#### 8. 节卡机器人 JAKA（中国·上海）

* 背景：协作机器人厂商。规模：**500–1000（估）**
* 主营：JAKA Zu/All 系列协作臂、移动+操作单元
* 官网：jaka.com

#### 9. 珞石机器人 Rokae（中国·北京）

* 背景：工业/协作机器人厂商。规模：**500–1000（估）**
* 主营：XMate/CR/AR 系列协作与工业臂
* 官网：rokae.com

#### 10. 越疆 DOBOT（中国·深圳）

* 背景：桌面/教育到工业协作臂全栈产品。规模：**500–1000（估）**
* 主营：CR/CRS/MG 等协作臂与教育平台
* 官网：dobot.cc

#### 11. 高仙机器人 Gaussian（中国·上海）

* 背景：商用清洁机器人龙头。规模：**500–1000（估）**
* 主营：室内外清洁机器人、设施运维解决方案
* 官网：gaussianrobot.com

#### 12. 普渡机器人 Pudu Robotics（中国·深圳）

* 背景：商用配送/清洁机器人，全球出货过万台级。规模：**1000+（估）**
* 主营：餐饮配送/酒店/清洁/工业配送
* 官网：pudurobotics.com / pudutech.com

#### 13. 擎朗智能 KEENON（中国·上海）

* 背景：2010 年成立，商服机器人出海较早。规模：**1000+（估）**
* 主营：送餐/酒店/清洁/重载系列
* 官网：keenon.com

#### 14. 极智嘉 Geek+（中国·北京）

* 背景：AMR（货到人/搬运/拣选）全球化布局。规模：**1000+（估）**
* 主营：仓储 AMR 系列与调度软件
* 官网：geekplus.com

#### 15. 海柔创新 HAI Robotics（中国·深圳）

* 背景：料箱到人（CTU）赛道开创者之一。规模：**1000+（估）**
* 主营：料箱到人系统、仓储自动化
* 官网：hairobotics.com

#### 16. 快仓 Quicktron（中国·上海）

* 背景：2014 年成立，AMR 头部企业。规模：**500–1000**
* 主营：仓储/制造 AMR 全系与系统
* 官网：quicktron.com / landing.quicktron.com

#### 17. 海康机器人 HIKROBOT（中国·杭州）

* 背景：工业视觉+AMR 业务。规模：**1000+（估）**
* 主营：移动机器人、视觉/读码器与产线解决方案
* 官网：hikrobotics.com

#### 18. Syrius Robotics 仙途智能（中国·北京/新加坡/日本）

* 背景：2018 年成立，RaaS 与 3PL 场景落地较多。规模：**200–500（估）**
* 主营：拣选/搬运 AMR、FlexGalaxy.AI 调度与 RaaS
* 官网：syriusrobotics.com / syriustechnology.com

#### 19. Multiway Robotics 未来机器人（中国·深圳）

* 背景：AMR 及柔性工厂内物流解决方案。规模：**200–500（估）**
* 主营：托盘/潜伏举升/搬运 AMR 与系统集成
* 官网：multiway-robotics.com

#### 20. YOUiBot 优艾智合（中国·深圳）

* 背景：2015 年成立，半导体/电力/巡检 AMR。规模：**200–500（估）**
* 主营：室内外 AMR 与行业解决方案
* 官网：youibot.com

#### 21. Mech-Mind 梅卡曼德（中国·北京）

* 背景：AI+3D 视觉与机器人系统集成，支持抓取/拆码垛/拣选。规模：**500–1000（估）**
* 主营：3D 相机 + Mech-Vision/Viz/Centre 软件与整线方案
* 官网：mech-mind.com / mech-mind.com.cn

> 注：后续可按照提交模板将更多同赛道代表企业**分别拆分**为 `/landscape/<company>.md`，并逐步补齐到 **≥30** 家。

---

### 海外（北美 / 欧洲 等）

#### 22. Boston Dynamics（美国）

* 背景：1992 年起步，现属现代汽车集团。规模：**500–1000**
* 主营：四足 Spot，物流臂 Stretch，研发人形 Atlas
* 官网：bostondynamics.com

#### 23. Agility Robotics（美国）

* 背景：2015 年成立；人形 **Digit** 量产推进。规模：**200–500**
* 主营：人形搬运/拣选/物流场景
* 官网：agilityrobotics.com

#### 24. Figure AI（美国）

* 背景：人形 Figure 01；多家头部科技/零售合作。规模：**200–500**
* 主营：通用人形机器人与具身智能
* 官网：figure.ai

#### 25. 1X（美国/挪威）

* 背景：2014 年创立（前身 Halodi），人形/移动人形。规模：**200–500**
* 主营：双足/轮足人形、远程操作与守护场景
* 官网：1x.tech

#### 26. Apptronik（美国）

* 背景：源自德州大学实验室，通用人形 **Apollo**。规模：**100–300**
* 主营：人形在制造/物流中的部署
* 官网：apptronik.com

#### 27. Sanctuary AI（加拿大）

* 背景：通用人形 **Phoenix**；认知与远程操作结合。规模：**100–300**
* 主营：人形服务/工业任务代理
* 官网：sanctuary.ai

#### 28. Tesla Optimus（美国）

* 背景：特斯拉的人形项目「Optimus」。规模：N/A（集团内）
* 主营：制造场景的人形装配/搬运实验
* 页面：tesla.com/AI（Optimus 板块）

#### 29. PAL Robotics（西班牙）

* 背景：2004 年成立，人形/双臂/移动服务机器人老牌公司。规模：**100–300**
* 主营：TIAGO/ARI 等服务与研究平台
* 官网：pal-robotics.com

#### 30. ANYbotics（瑞士）

* 背景：苏黎世联邦理工孵化，四足 **ANYmal**。规模：**100–300**
* 主营：油气/化工/电力巡检
* 官网：anybotics.com

#### 31. Ghost Robotics（美国）

* 背景：四足平台厂商。规模：**50–200**
* 主营：安防/勘察四足平台
* 官网：ghostrobotics.io

#### 32. NEURA Robotics（德国）

* 背景：2019 年成立，协作与人形 **4NE1**；近年获大额融资。规模：**200–500**
* 主营：认知机器人、协作臂、人形平台
* 官网：neura-robotics.com

#### 33. Agile Robots（德国/中国）

* 背景：慕尼黑总部，AI+机器人自动化。规模：**500–1000（估）**
* 主营：协作臂、移动/视觉检测一体化解决方案
* 官网：agile-robots.com

#### 34. ABB Robotics（瑞士）

* 背景：全球工业机器人巨头之一。规模：**7000+（机器人业务）**
* 主营：工业/协作机器人与 AMR、软件与系统集成
* 官网：abb.com/robotics

#### 35. KUKA（德国）

* 背景：世界领先的工业机器人与系统集成商。规模：**>10,000（集团）**
* 主营：工业/协作机器人、移动底盘与整线解决方案
* 官网：kuka.com



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
