# 🐍 Snake AI with Deep Q-Learning

An autonomous Snake agent trained with **Deep Q-Learning (DQN)**. The project combines a custom **Pygame** environment with **PyTorch** and visualizes the learning progress live using **Matplotlib**.

The agent starts without knowledge of the game rules. It learns through interaction with the environment: eating food is rewarded, collisions are penalized, and previously observed situations are reused during training.

## Features

- Deep Q-Network implemented with PyTorch
- Epsilon-greedy exploration strategy
- Experience replay with mini-batch training
- Short-term and long-term memory training
- Live score and mean-score visualization
- Automatic model checkpointing
- Custom Pygame Snake environment

## How It Works

For every game step, the agent:

1. reads the current game state,
2. chooses an action using its neural network or exploration,
3. executes the action in the environment,
4. receives a reward,
5. stores the experience in replay memory,
6. trains the network from the current and earlier experiences.

### Actions

The output consists of three relative movement commands:

| Action | Meaning |
|---|---|
| `[1, 0, 0]` | Continue straight |
| `[0, 1, 0]` | Turn right |
| `[0, 0, 1]` | Turn left |

### Rewards

| Event | Reward |
|---|---:|
| Food eaten | `+10` |
| Collision / game over | `-10` |
| Normal move | `0` |

An episode is also stopped when the agent takes more than `100 × snake length` steps without making sufficient progress.

## Game Configuration

| Setting | Value |
|---|---:|
| Window size | `640 × 480` |
| Block size | `20 px` |
| Game speed | `40 FPS` |
| Initial snake length | `3` |

The environment supports movement in four directions: `RIGHT`, `LEFT`, `UP`, and `DOWN`. Food is placed randomly on a free position. Wall and self-collisions end the current episode.

## Project Structure

```text
.
├── agent.py        # Agent loop, state calculation and training logic
├── game.py         # Snake environment, movement, food and collisions
├── model.py        # Neural network and Q-learning trainer
├── helper.py       # Live training plots
├── model/          # Saved model checkpoints
├── README.md       # Project documentation
├── LICENSE         # MIT License
└── .gitignore      # Ignored files and training artifacts
```

## Requirements

- Python 3.10 or newer
- PyTorch
- Pygame
- Matplotlib
- NumPy

## Installation

Clone the repository and enter the project directory:

```bash
git clone https://github.com/carstensaal-ux/REPOSITORY-NAME.git
cd REPOSITORY-NAME
```

Create and activate a virtual environment:

```bash
python -m venv .venv
```

Windows:

```powershell
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install torch pygame matplotlib numpy
```

## Training

Start a new training run with:

```bash
python agent.py
```

The Pygame window shows the current game, while Matplotlib displays the score and the running mean score. Saved model files are written to the `model/` directory.

## Deep Q-Learning

The model approximates the Q-value for each possible action. Training is based on the Bellman equation:

```text
Q_new = reward + gamma × max(Q_next)
```

The trainer minimizes the difference between the predicted Q-values and the calculated target values. Experience replay reduces the correlation between consecutive game states and makes training more stable.

## Roadmap

- [ ] Add a pinned `requirements.txt`
- [ ] Add command-line options for speed and training parameters
- [ ] Add evaluation mode without exploration
- [ ] Add automated tests for collision and movement logic
- [ ] Document training results and example scores

## License

This project is licensed under the [MIT License](LICENSE).

## Author

Created by [carstensaal-ux](https://github.com/carstensaal-ux).

