# -Dungeon-Explorer-Reinforcement-Learning-in-a-Grid-based-Adventure

### Journeying Through the Dungeon

In this project, we've dived into the world of reinforcement learning to guide an adventurer through a maze-like dungeon. Picture a grid-based space, a 5x5 map filled with treasures, dragons, keys, and mysterious doors.

#### Setting the Scene

Our protagonist, the player, has a mission: to navigate this adventurous but perilous dungeon. With the ability to move in four directions—Up, Down, Left, and Right—the player's goal is to reach the bottom-right corner of the grid. Along the way, they'll collect treasures, unlock doors, and evade lurking dragons.

#### The Dungeon's Components

**Player State**: This is where your journey begins, marked by your initial position within the grid.

**Enemy Positions**: Dragons occupy specific spots within the grid, a constant threat to be cautious of.

**Rewards and Penalties**: Each action has its consequences. For instance:
- Encountering a dragon comes with a penalty of -10.
- Discovering a treasure rewards +10.
- Successfully unlocking a door yields +5, while attempting without a key incurs a penalty of -5.
- Moving to a new state is rewarded with +1, but staying in the same state results in a small penalty of -2.

#### Visualizing the Adventure

The grid-based environment is visually captivating, showcasing different icons for players, enemies, treasures, keys, doors, and clear pathways. The grid paints a vivid picture of this thrilling dungeon.

![Dungeon](images_desc/GRID.png)

#### Exploring the Unknown

To grasp the dynamics of this environment, we embarked on a 10-step exploration. Each step represents a random action taken by the player, resulting in state changes and associated rewards or penalties. This random journey offers a glimpse into the interactive nature of players within this Dungeon realm.

This journey helps us understand how the player's choices affect their progress, the risks involved in encountering enemies, the thrill of discovering treasures, and the strategy behind unlocking doors. It's a glimpse into the adventurous yet challenging world of navigating a dungeon using reinforcement learning techniques.


=============================================================================================

### Implementation of SARSA Algorithm

SARSA, known as State-Action-Reward-State-Action, is a learning approach focused on the agent's actions within an environment. It's a technique where the agent constantly updates its understanding based on its current state, the action it takes, the reward received, and the subsequent state it transitions into. In our implementation, the 'train_sarsa' method houses the core update function responsible for adjusting Q-values. This method captures the essence of SARSA by considering observed transitions and incorporating the chosen action, received rewards, and state changes. We employ an epsilon-greedy strategy for action selection, allowing the agent to balance between exploring new actions and exploiting learned knowledge. Our training regimen spans 500 episodes, enabling the agent to learn from interactions with the environment, updating Q-values accordingly. Throughout this process, we track episode-wise rewards, visualizing the learning curve through a graph showcasing total rewards. Moreover, monitoring the decay of epsilon across episodes provides insights into the exploration factor's evolution during training.

### Evaluation Insights

In the realm of SARSA, our agent's learning journey unveils intriguing insights. Beginning with humble rewards, the agent evolves its strategy, eventually reaching substantial rewards—peaking at 474 in one episode. The epsilon decay graph illustrates a deliberate shift from exploratory actions to more deterministic, greedy choices. Examining the initial and trained Q-tables provides a glimpse into the learned policy, showcasing the evolving strategies and preferences.

Hyperparameter tuning, a key aspect of refining the SARSA algorithm, involves tweaking factors like the discount factor (γ) and epsilon decay rate. These adjustments aim to enhance the agent's learning curve, fine-tuning its decisions for more optimal outcomes. By experimenting with these parameters, we aim to harness SARSA's potential, further honing the agent's ability to navigate the dungeon environment with efficiency and strategy.

  
  - Initial and trained Q-tables.
     - ![Q-Table](images_desc/Intial-Qtable(SARSA).png)

  - Total reward per episode graph.
     - ![Total-reward](images_desc/total-reward-per-episode-SARSA.png)
    
  - Epsilon decay graph.
    - ![decay-graph](images_desc/epsilon_decay.png)
  
=============================================================================================

### Part III: Implement Double Q-learning

In this phase, we applied the Double Q-Learning algorithm to tackle challenges in our interview environment. Unlike SARSA, which is on-policy, Double Q-Learning is an off-policy algorithm. The key innovation lies in maintaining two Q-tables, Q1 and Q2, for more robust learning. The update function, within the "train_double_Q" method, involves updating Q1 or Q2 based on a random choice. If the random number is less than 0.5, Q1 is updated; otherwise, Q2 is updated. This dual-table approach refines the agent's understanding of total expected rewards for actions in specific states.

**Update Function:**
Both Q1 and Q2 values are updated considering immediate rewards, discounted future rewards from the next state, and the current Q-values. Q1 values are based on Q2 values, and vice versa, balancing the learning process.

**Greedy Action Selection - Epsilon-Greedy Exploration:**
For action selection, the epsilon-greedy strategy is employed. The agent either randomly chooses an action with a certain probability (epsilon) or selects the action with the highest Q-values from both sets, Q1 and Q2.

**Training Loop:**
The "train_double_Q" method iterates over 500 episodes. During each episode, the agent interacts with the environment, updating Q1 or Q2 values based on random choices. Rewards obtained in each episode are tracked to visualize the learning progress.

**Graph Analysis:**
Upon running the scenario for 500 episodes, the rewards graph indicates significant progress. The agent, focusing on greedy actions from the learning policy, initially had minimal rewards. However, over episodes, it effectively exploited incentives, resulting in substantial rewards. The epsilon decay graph reveals a gradual reduction in epsilon, indicating a shift towards choosing mainly greedy actions from the learning policy.

**Evaluation Results:**
- **Initial and Trained Q-Tables:** Displaying the Q1 and Q2 tables before and after training.
  
     - ![Q-Table](images_desc/Double-Q-learning-Q-table.png)

- **Total Reward per Episode Graph:** Visualizing the learning progress through rewards over 1000 episodes.
 
     ![Total-reward](images_desc/total-reward-per-episode-d-Q.png)

- **Epsilon Decay Graph:** Demonstrating the reduction in epsilon over episodes, reflecting the agent's focus on greedy actions.

     ![decay-graph](images_desc/epsilon-decay-D-Q.png)


This implementation showcases the effectiveness of Double Q-Learning in enhancing the agent's decision-making in our interview environment.


## Compare the performance of both algorithms in the same environment

Based on the above rewards vs episodes plot, it appears that the SARSA algorithm consistently outperforms the Double Q-learning algorithm in the same environment.
The x-axis of the plot represents the episode number, and the y-axis represents the reward value. The blue line represents the SARSA algorithm, and the red line represents the Double Q-learning algorithm.
Throughout the episodes, the reward values for both algorithms fluctuate. However, the SARSA algorithm consistently achieves a higher reward value than the Double Q-learning algorithm. This suggests that the SARSA algorithm is more effective in this environment.

The possible understanding is:

**Exploration vs Exploitation Trade-off:** SARSA, being an on-policy algorithm, follows the policy that’s being learned, while Double Q-learning, an off-policy method, learns the value of the optimal policy irrespective of the policy being followed. This difference could lead to SARSA making safer, more conservative updates, which might be beneficial in the dungeons and dragons’ environment.

**Reward Structure Sensitivity:** SARSA considers the next action that the policy will take and therefore can be more sensitive to the reward structure of the state-action pairs in the environment. Particularly in a closed environment such as ours, the reward structure favors the characteristics of the SARSA algorithm, which could explain the improved performance.

 ![Compare-graph](images_desc/SARSAvsDQlearning.png)



## Comparison of SARSA vs 2 step Bootstrapping SARSA:

 ![Compare-graph](images_desc/bootstrap.png)


### N-step Bootstrapping
- **Implementation:** Added n-step Bootstrapping (e.g., 2-step or 3-step SARSA) for comparison.
- 
#### Consistent Performance
In our dungeon quest, a fascinating trend emerges: the 2-step bootstrapping SARSA algorithm consistently outshines its SARSA counterpart. Across episodes, both algorithms experience reward fluctuations, yet the 2-step bootstrapping SARSA consistently secures higher reward values. This pattern strongly indicates its superior effectiveness within this environment.

#### Unveiling the Advantages
What sets the 2-step bootstrapping SARSA apart? It delves into multi-step updates, leveraging a 2-step return mechanism to update Q-values. Unlike SARSA, which considers immediate rewards, the 2-step approach factors in the next two rewards. This expanded perspective offers a more accurate estimation of future rewards, proving beneficial, especially in scenarios where rewards for actions are delayed or spread over time.

#### Balancing Act: Exploration and Exploitation
Both SARSA and 2-step bootstrapping SARSA operate as on-policy algorithms, but the multi-step update presents a nuanced shift in their exploration-exploitation balance. The 2-step bootstrapping SARSA seems adept at navigating this delicate trade-off, potentially achieving a finer equilibrium between exploring new strategies and exploiting known profitable actions within our specific dungeon environment.

This fascinating exploration showcases how a slight alteration in algorithmic approach—leveraging multi-step updates—can wield significant impact, offering a more refined and rewarding journey through the complexities of our dungeon adventure.

