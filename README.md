Heterogeneous Multi-Agent Disaster Response Environment

This project explores the challenges of heterogeneous multi-agent reinforcement learning within a simulated disaster response scenario. It features different agent types (responders and vehicles) with varying capabilities and aims to rescue civilians from a grid-based environment, bringing them to a shelter.

Project Structure:
1. HeteroDisasterEnv (Static Hazards - Baseline)
This is the initial environment definition. It simulates a disaster scenario with:

Fixed Grid: A defined grid size where agents operate.
Responders & Vehicles: Agents with different carrying capacities (responders carry 1, vehicles carry 2).
Civilians: Entities to be rescued.
Shelter: A target location for rescued civilians.
Static Obstacles: Pre-defined impassable areas.
Observation Space: Agents observe their own position, distance to the nearest civilian (for responders), carrying status (for vehicles), and distance to the shelter.
Actions: Agents can move in four cardinal directions or stay put.
Rewards: Agents are rewarded for picking up civilians, dropping them off at the shelter, and penalized for stepping and colliding with obstacles.

2. run_random_policy
This function evaluates the performance of a purely random policy within the HeteroDisasterEnv. It logs various metrics such as total episode rewards, rescued civilians, episode lengths, and separate rewards for responders and vehicles.

3. QLearningAgent
An implementation of a Q-learning agent. It includes:

Q-table: A defaultdict to store Q-values for state-action pairs.
State Representation: A simplified state based on agent position and whether it's carrying a civilian.
Epsilon-Greedy Policy: For action selection, balancing exploration and exploitation.
Q-value Update Rule: Standard Q-learning update.

4. train_iql (Heterogeneous IQL Training Loop)
This function trains two independent Q-learning agents (one for responders, one for vehicles) using Independent Q-Learning (IQL). It logs training progress including episode rewards, rescued civilians, and episode lengths.

5. HeteroDisasterEnv_V2 (Dynamic Hazards - Update)
An extension of the base environment that introduces dynamic hazards:
Hazard Probability: A chance for new obstacles to spawn dynamically at each step, adding complexity and uncertainty to the environment.

6. Rollout and Visualization
render_and_save: A utility function to capture frames of the environment state for visualization purposes.
rollout_trained_policy: A function to run a deterministic simulation using the trained Q-learning policies, saving frames to visualize the agents' learned behavior.
Ablation Study:
The notebook also includes an ablation study by running HeteroDisasterEnv_V2 with n_vehicles=0 to understand the impact of heterogeneity (specifically, the absence of vehicle agents) on the performance of the system.

Key Concepts Demonstrated:
Multi-Agent Systems: Simulation of multiple interacting agents.
Heterogeneous Agents: Agents with different roles and capabilities.
Reinforcement Learning (Q-Learning): Agents learn optimal policies through trial and error.
Independent Q-Learning (IQL): A common baseline approach for multi-agent reinforcement learning where each agent learns independently.
Dynamic Environments: Introduction of elements that change over time (dynamic hazards).
Qualitative Metrics: Tracking performance metrics relevant to the disaster response scenario.
Policy Rollout & Visualization: Observing and debugging learned policies.
This project serves as a foundation for exploring more advanced multi-agent reinforcement learning techniques in complex, dynamic environments.
