# Simplified Multi-Agent Cybersecurity Environment

This repository contains a **simplified simulation environment** for multi-agent cyber defense challenges. It is inspired by the original TTCP CAGE Challenge environment but has been restructured for flexibility and ease-of-use. This project is built upon the main [CAGE4 repository](https://github.com/cage-challenge/cage-challenge-4).

In this new codebase, you can easily define new attacker types and configure the network structure by setting the number of user hosts and servers in each subnet. In addition, we have implemented a range of access control actions—including normal access control, decoy actions, and subnet-level access control—to mimic real-world zero trust security architectures.

## Features

- **Simplified Environment:**  
  A streamlined version of the original CAGE simulation focusing on key elements without the overhead of unnecessary packages.
  
- **Flexible Network Structure:**  
  Easily configure the simulation by setting the number of green agents (user hosts) and servers per zone. This new structure adapts based on your configuration settings.

- **Custom Attacker Definitions:**  
  Define new attacker types by extending built-in agents such as:
  - `NoAttackRedAgent`
  - `AllSubnetAttacker`
  - `SpecificSubnetAttacker`
  - `TimeDependentAllSubnetAttacker`  
  These classes provide a baseline for simulating different attack strategies.

- **Zero Trust Actions:**  
  Blue agents now have a comprehensive suite of access control actions:
  - **Normal Access Control and Decoy Actions:**  
    Blue agents can enable or disable access control on individual green agents and deploy decoy services to detect and counter malicious activity.
  - **Subnet-Level Access Control:**  
    Additionally, Blue agents can isolate entire network subnets by enabling or disabling access control at the subnet level, effectively modifying the network topology on the fly.

- **Reduced Dependencies:**  
  This environment requires fewer packages than the original setup, making it more lightweight and easier to install.

## Dependencies

This project requires Python 3.x. The following libraries are used with these specific versions:

- **Gym Libraries:**
  - `gym==0.26.2`
  - `gymnasium==0.28.1`
  
- **RLlib:**
  - `ray[rllib]`
  - `lz4==4.3.3`
  
Additionally, the project utilizes:
- `networkx`
- `numpy`
- `matplotlib`

You can install these dependencies using pip.

## Usage

You can integrate the environment into your reinforcement learning pipeline or use it as a standalone simulation. Below is an example snippet showing how to create and interact with the environment:

```python
import gymnasium as gym
from your_module import CAGE4MultiAgentEnv  # adjust import based on your module structure

# Create the environment; you can pass configuration parameters if desired
env = CAGE4MultiAgentEnv(env_config={
    "num_green_agents_per_zone": 3,
    "num_servers_per_zone": 3,
    "security_risk": 0.05,
    "success_rate": 0.8,
    "step_threshold": 100,
    "debug": True
})

# Reset the environment
obs, info = env.reset()

# Run a single simulation step (example: random blue agent actions)
action_dict = {agent: env.action_space.sample() for agent in env.blue_agents.keys()}
obs, rewards, terminated, truncated, info = env.step(action_dict)

# Optionally, render the current network graph
env.render()

```

## Code Structure

- **Agent Classes:**  
  Contains definitions for different agent types:
  - `GreenAgent`: Simulates benign user behavior with the risk of compromise.
  - `RedAgent` and its subclasses: Implement various attack strategies.
  - `BlueAgent`: Acts as the defender with a defined action space (e.g., monitoring, rebooting, deploying decoys, and zero trust actions).

- **Environment Class:**  
  The `CAGE4MultiAgentEnv` class defines the simulation loop, state updates, reward calculations, network graph building, and interactions (including zero trust actions via subnet level access control).

- **Network & Graph Logic:**  
  Uses NetworkX to create and update a dynamic network graph, representing zones, walls, and connected hosts. The graph is updated during each step as agents take their actions.

## Extending the Environment

- **New Attackers:**  
  You can easily add or modify red agent classes by extending the provided attacker classes.
  
- **Network Flexibility:**  
  Change the number of user hosts and servers per zone by modifying the configuration values during environment initialization.

## Contributing

Contributions and feedback are welcome! If you have ideas or improvements, please open an issue or submit a pull request or email me at: ravari.a@northeastern.edu

## License

[MIT License](LICENSE)
```

