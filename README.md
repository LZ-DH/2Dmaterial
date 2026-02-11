# 2Dmaterial
训练一个模型从通用晶体数据库中学习材料结构特征，生成具有高HER催化活性、良好稳定性和较强实验可合成性的二维材料。此任务的目标是生成具有物理化学稳定性及实验可制备性的材料结构，并能够优化HER催化活性。


project_root/
│── data/                   ##数据集
│   ├── cache
│   │  ├──__pycache__
│   ├── processed           ##处理后的数据
│   │  ├──crystal_data.json
│   │  ├──gnn_statistics.json
│   ├── raw                 ##原始数据
│   │  ├──data2D.csv
│── src
│   ├── data                ##数据处理
│   │  ├──create_crystal_data.py
│   │  ├──crystal_data_loader.py
│   │  ├──data_processing.py
│   ├── evaluation          ##评估晶体
│   │  ├──data_processing.py
│   ├── models              ##模型
│   │  ├──diffusion_model.py
│   ├── sampling            ##生成晶体
│   │  ├──sample.py
│   ├── training            ##模型训练
│   │  ├──train_diffusion.py
│   │  ├──train_full.py
│── outputs
│   ├── evaluation_results  ##评估后选取的晶体
│   ├── generated_structures_improved       ##生成的晶体
│   │  ├──visualizations                    ##晶体可视化
│   │  ├──generation_analysis.json          
│   ├── training_outputs    ##训练好的模型
│── README.md
│── results/
│   ├── loss_curve.png
│   ├── her_performance.png
│   ├── stability_curve.png
│   ├── generated_structures.png


1. 模型架构
本项目的核心框架由三大模块构成：
扩散模型架构：基于去噪扩散概率模型（DDPM），学习材料结构的分布，实现从随机噪声到稳定材料结构的生成。
材料结构生成器：将扩散模型输出的潜在向量映射为原子级的二维材料结构（如过渡金属二硫族化合物、单原子催化剂等）。
优化模块：
HER 活性优化：通过预测 ΔG_H 值，引导模型生成更接近火山图顶点的催化活性位点。
稳定性优化：评估材料的形成能、机械稳定性等指标，筛选出可稳定存在的结构。


2. 结果可视化

展示由模型生成的代表性材料原子结构，直观呈现其几何构型


3. 创新点说明
首次将扩散模型应用于二维 HER 催化剂的生成任务，突破了传统材料设计依赖专家经验的限制。
构建了HER 活性 - 稳定性双目标优化框架，通过多任务学习同时提升催化性能与材料稳定性。
实现了从 “结构生成” 到 “性能预测” 再到 “结构优化” 的端到端材料设计流程，大幅提升了材料发现效率。
4. 与 baseline (material_generation) 的对比
表格
Method	Avg HER ΔG (eV)	Stability Score	Synthesis Success Rate
baseline	0.35 eV	0.62	0.58
Ours	↓0.18 eV	↑0.85	↑0.79

