# Simplified Multi-Agent Cybersecurity Environment

This repository contains a **simplified simulation environment** for multi-agent cyber defense challenges. It is inspired by the original TTCP CAGE Challenge environment but has been restructured for flexibility and ease-of-use. In this new codebase, you can easily define new attacker types and configure the network structure by setting the number of user hosts and servers in each subnet. In addition, we have implemented zero trust actions (at the subnet level) within the environment.

## Features

- **Simplified Environment:**  
  A streamlined version of the original CAGE simulation that focuses on key elements, without the overhead of unnecessary packages.
  
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
  Implemented zero trust actions for network defenders. Blue agents now have actions like enabling/disabling subnet-level access control, which mimics real-world zero trust security architectures.

- **Reduced Dependencies:**  
  This environment requires fewer packages than the original setup, making it more lightweight and easier to install.

## Dependencies

To run this simulation environment, ensure you have Python 3.x installed along with the following packages:

- `networkx`
- `numpy`
- `gymnasium`
- `ray[rllib]`
- `matplotlib`

You can install these packages using pip:

```bash
pip install networkx numpy gymnasium ray[rllib] matplotlib

```

## Installation

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```

2. **Install the Dependencies:**  
   Use the command above or add the dependencies to your `requirements.txt` file and run:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

You can integrate the environment into your reinforcement learning pipeline or use it as a standalone simulation. Below is an example snippet on how to create and interact with the environment:

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

## Zero Trust Actions

Blue agents now have the ability to perform subnet-level actions:
- **ENABLE_SUBNET_AC / DISABLE_SUBNET_AC:**  
  These actions simulate a zero trust security model by temporarily isolating or rejoining segments of the network, effectively modifying the network topology on the fly.

## Extending the Environment

- **New Attackers:**  
  You can easily add or modify red agent classes by extending the provided attacker classes.
  
- **Network Flexibility:**  
  Change the number of user hosts and servers per zone by modifying the configuration values during environment initialization.

## Contributing

Contributions and feedback are welcome! If you have ideas or improvements, please open an issue or submit a pull request.

## License

[MIT License](LICENSE)
```

