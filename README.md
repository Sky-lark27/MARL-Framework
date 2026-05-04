# Heterogeneous Multi-Agent Disaster Response Environment

This project explores the challenges of heterogeneous multi-agent reinforcement learning within a simulated disaster response scenario. It features different agent types (responders and vehicles) with varying capabilities and aims to rescue civilians from a grid-based environment, bringing them to a shelter.

## Project Overview

This repository contains code for simulating a disaster response scenario using a heterogeneous multi-agent system. The core idea is to train different types of agents (responders and vehicles) to cooperatively rescue civilians and transport them to a designated shelter. The environment is designed to be dynamic, introducing challenges like randomly spawning obstacles.

## Key Features

- **Heterogeneous Agents:** The simulation includes two distinct agent types:
    - **Responders:** Capable of picking up one civilian at a time.
    - **Vehicles:** Capable of carrying multiple civilians (e.g., 2 in the current setup).
- **Dynamic Environment:** The `HeteroDisasterEnv_V2` class introduces dynamic hazards (new obstacles) that can appear at random during the simulation, making the environment more challenging and realistic.
- **Independent Q-Learning (IQL):** Each agent type learns its optimal policy independently using Q-learning, demonstrating a common approach to multi-agent reinforcement learning.
- **Qualitative Metrics:** The project tracks and reports metrics such as total episode rewards, number of rescued civilians, and episode lengths to evaluate policy performance.
- **Visualization:** Tools are provided to render and save frames of the simulation, allowing for visual inspection of agent behavior and environment evolution.
- **Ablation Study:** An ablation is included to compare performance with and without specific agent types (e.g., without vehicles) to understand their impact on the overall system.

## Project Structure

### 1. `HeteroDisasterEnv` (Static Hazards - Baseline)

The foundational environment for the disaster response simulation. It defines:
- A fixed-size grid.
- Placement of responders, vehicles, civilians, a shelter, and static obstacles.
- Observation space for agents (position, nearest civilian distance, distance to shelter, carrying status).
- Action space (move up, down, left, right, or stay).
- Reward structure for picking up civilians, dropping them at the shelter, and penalties for movement/collisions.

### 2. `run_random_policy`

A utility function to evaluate the baseline performance of the environment when agents follow a purely random action selection policy. It logs various performance metrics over multiple episodes.

### 3. `QLearningAgent`

An implementation of a Q-learning agent with:
- A Q-table (using `defaultdict`) to store state-action values.
- A simplified state representation incorporating agent position and carrying status.
- An epsilon-greedy strategy for balancing exploration and exploitation.
- A standard Q-learning update rule to learn from experience.

### 4. `train_iql` (Heterogeneous IQL Training Loop)

The main training loop that orchestrates the learning process for the IQL agents. It instantiates separate `QLearningAgent` instances for responders and vehicles and updates their policies based on their individual observations and rewards within the shared environment.

### 5. `HeteroDisasterEnv_V2` (Dynamic Hazards - Update)

An enhanced version of the `HeteroDisasterEnv` that inherits its functionality and introduces:
- `hazard_prob`: A probability parameter to control the frequency of new, randomly placed obstacles appearing in the environment during simulation steps.

### 6. Rollout and Visualization Utilities

- **`render_and_save`:** A helper function to generate and save visual frames of the environment state at different timesteps. These frames can be compiled into GIFs or videos to visualize the rollout.
- **`rollout_trained_policy`:** A function that runs a simulation using the policies learned by the `train_iql` function. It operates deterministically (no exploration) and saves frames to illustrate the agents' learned behavior in action.

## Getting Started

To run this project, you will need a Python environment with the following libraries:

- `numpy`
- `matplotlib`

The code is designed to be run in a Jupyter Notebook or Google Colab environment, where cells can be executed sequentially.

## Usage

1.  **Initialize the Environment:**
    ```python
    env = HeteroDisasterEnv(grid_size=10, n_responders=1, n_vehicles=1, n_civilians=5, max_steps=200)
    ```
2.  **Run Random Policy (Baseline):**
    ```python
    metrics = run_random_policy(env, episodes=50)
    for k, v in metrics.items():
        print(k, ":", np.mean(v), "±", np.std(v))
    ```
3.  **Train IQL Agents:**
    ```python
    history, responder_agent, vehicle_agent = train_iql(env, episodes=300)
    # plot_results(history) # Assuming a plot_results function is defined elsewhere
    ```
4.  **Run with Dynamic Hazards (V2 Environment):**
    ```python
    env_v2 = HeteroDisasterEnv_V2(hazard_prob=0.05)
    history_v2, responder_agent_v2, vehicle_agent_v2 = train_iql(env_v2, episodes=300)
    # plot_results(history_v2)
    ```
5.  **Perform Rollout and Visualize:**
    ```python
    env_rollout = HeteroDisasterEnv_V2(hazard_prob=0.05) # Or use HeteroDisasterEnv()
    rollout_trained_policy(env_rollout, responder_agent_v2, vehicle_agent_v2)
    ```
    *Note: The `render_and_save` function will create a directory `rollout_frames` and save `.png` files for each rendered step. These can then be stitched together into a GIF or video using external tools.*

## Future Work

- Implement more sophisticated multi-agent reinforcement learning algorithms (e.g., MADDPG, COMA).
- Introduce communication between agents.
- Add more complex hazard types or environmental dynamics.
- Explore different reward structures and observation spaces.
- Conduct extensive hyperparameter tuning for Q-learning agents.
