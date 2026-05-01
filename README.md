Heterogeneous Multi-Agent Reinforcement Learning for Adaptive Disaster Evacuation

This repository contains the implementation and simulation framework for the research project:

“Heterogeneous Multi-Agent Reinforcement Learning for Adaptive Disaster Evacuation”

The project explores how multi-agent reinforcement learning (MARL) can be used to model intelligent evacuation strategies in dynamic disaster environments.

Overview

Disaster evacuation is a complex decision-making problem characterized by:

Dynamic hazards
Limited environmental observability
Multiple agents with different roles

Traditional evacuation models rely on static routes or centralized control, which often fail in rapidly changing disaster situations.

This project proposes a simulation-based MARL framework where heterogeneous agents learn decentralized evacuation policies through reinforcement learning.

The system models evacuation scenarios using a grid-based environment where agents interact with civilians, obstacles, shelters, and hazards.

Key Features
Multi-Agent Reinforcement Learning environment
Heterogeneous agents with role-specific behavior
Grid-based disaster simulation environment
Independent Q-Learning implementation
Dynamic hazard generation
Training visualization (reward curves, episode metrics)
Ablation study comparing heterogeneous vs homogeneous agents
Policy rollout visualization
Environment Simulation

The disaster environment is modeled as a grid-based world containing:

Civilians requiring evacuation
Responder agents
Support agents
Safe shelter zones
Obstacles and blocked paths
Dynamic hazard cells

Agents interact with the environment and learn optimal policies to maximize evacuation success.

Reinforcement Learning Framework

Each agent learns independently using Q-Learning.

State

Local observation of nearby grid cells including hazards, civilians, and shelters.

Actions
Move Up
Move Down
Move Left
Move Right
Stay

Reward Structure
Event	Reward
Civilian rescued	+10
Reach shelter	+5
Obstacle collision	-5
Enter hazard cell	-10
Step penalty	-0.1
Experimental Setup
Parameter	Value
Grid Size	20 × 20
Civilians	5
Responder Agents	4
Support Agents	2
Shelters	3
Training Episodes	1000
Learning Rate	0.1
Discount Factor	0.9
Exploration Strategy	ε-greedy

Implementation was done using Python, with NumPy for computation and Matplotlib for visualization.

Results

Training results demonstrate that agents learn efficient evacuation strategies.

Key observations:

Episode reward increases steadily during training
Civilians rescued improves from ~2.5 to ~4.3–4.5 out of 5
Episode length decreases, indicating improved efficiency
Ablation Study

The impact of heterogeneous agents was evaluated by comparing them with homogeneous agents.

Metric	Heterogeneous Agents	Homogeneous Agents
Rescue Success Rate	85%	60%
Civilians Rescued	4.3 / 5	3.0 / 5
Learning Stability	High	Moderate

Results show that heterogeneous agents significantly improve coordination and evacuation success.

Example Simulation Rollout

The simulation demonstrates agent behavior during evacuation episodes.

Typical progression:

Initial random placement of agents and civilians
Agents navigate around hazards and obstacles
Agents guide civilians toward shelter locations
Project Structure

Example repository structure:

project/
│
├── environment/
│   └── disaster_environment.py
│
├── agents/
│   └── q_learning_agent.py
│
├── training/
│   └── train_agents.py
│
├── visualization/
│   └── plotting.py
│
├── results/
│   └── learning_curves.png
│
└── README.md
Applications

This framework can be used for:

Disaster response simulation
Evacuation strategy planning
Multi-agent coordination research
Reinforcement learning experimentation

Future extensions may integrate real-world spatial data (GPS/GIS) to model urban evacuation scenarios.

Future Work

Future improvements include:

Deep Reinforcement Learning (DQN, PPO)
Large-scale environment simulations
Integration with real-world GIS and GPS data
Real-time disaster response modeling
Authors

Tanisha Bhatnagar
School of Computing Science and Engineering
Galgotias University, Greater Noida, India

Himanshu Kumar

Niteesh Kumar Mishra

Conference Presentation

This project was presented at:

International Symposium on Artificial Intelligence in Education (ISAIED 2026)
Don Bosco College of Engineering, Goa

License

This project is intended for academic and research purposes.
