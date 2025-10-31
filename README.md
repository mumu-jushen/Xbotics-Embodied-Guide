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

### 目录（Table of Contents）  
- [1.1 术语速览](#1.1-术语速览)  
- [1.2 操作综述](#1.2-操作综述)  
- [1.3 感知综述](#1.3-感知综述)  
- [1.4 运控综述](#1.4-运控综述)  
- [1.5 交互与协作综述](#1.5-交互与协作综述)  
- [1.6 数据、评测与基准综述](#1.6-数据评测与基准综述)  

# 1.1术语速览 · 具身智能系统关键词手册

## 目录（Table of Contents）
- [1.1.1 学习范式与策略框架（IL / RL / VLA / Diffusion Policy / World Model）](#1.1.1-学习范式与策略框架il--rl--vla--diffusion-policy--world-model)
- [1.1.2 控制与规划常用概念](#1.1.2-控制与规划常用概念)
- [1.1.3 感知与表征（Robotics Models）](#1.1.3-感知与表征robotics-models)
- [1.1.4 系统工程（Robot System Engineering）](#1.1.4-系统工程robot-system-engineering)
- [1.1.5 人机交互（HRI）](#1.1.5-人机交互hri)
- [1.1.6 安全与标准](#1.1.6-安全与标准)
- [1.1.7 常见文件与工具栈](#1.1.7-常见文件与工具栈)
- [1.1.8 行业顶会 / 顶刊](#1.1.8-行业顶会--顶刊)
- [1.1.9 机器人基础（Robotics Basics）](#1.1.9-机器人基础robotics-basics)

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


#1.2-操作综述
#1.3-感知综述
#1.4-运控综述
#1.5-交互综述
#1.6-数据综述
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
  
  **创新点**：三元1-bit量化+蒸馏，内存↓29.8%，LIBERO性能持平OpenVLA。
    1. 三元 1-bit 量化 + 蒸馏：内存 ↓29.8%，LIBERO 性能持平 OpenVLA。
    2. 极致部署友好：推理开销断崖式下降。
  
  **适用场景**：**嵌入式机器人、无人机伴飞、移动机械臂**等极致算力受限平台。

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
