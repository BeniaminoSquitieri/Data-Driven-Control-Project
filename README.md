# Data-Driven Control Project

## Project Overview

This project explores the implementation and analysis of **data-driven control algorithms** for autonomous mobile robots operating in complex environments. The aim is to design and evaluate control strategies to navigate these robots through spaces with obstacles, leveraging both **Forward Optimal Control (FOC)** and **Inverse Optimal Control (IOC)** techniques. The project applies these methods to the **Robotarium** environment, a platform for both simulation and real-world testing of autonomous robots.

## Key Themes and Concepts

### 1. **Forward Optimal Control (FOC)**
   Forward Optimal Control is employed to guide a robot from a starting position to a target destination while avoiding obstacles. In this project, a simplified version of FOC is used to reduce computational complexity. This involves a **greedy approach** where the instantaneous cost function is used to determine the optimal policy.

   #### Key Points:
   - **Robot Navigation**: The goal is to move the robot to the target while avoiding collisions with obstacles.
   - **Cost Function**: The cost is calculated based on the distance to the target and proximity to obstacles, modeled using **Gaussian distributions**.
   - **Entropy Calculation**: Entropy is used as part of the decision-making process, helping the robot choose its actions based on a probability distribution.

### 2. **Inverse Optimal Control (IOC)**
   In the second phase, **Inverse Optimal Control** is used to infer the cost function that a robot follows, based on a set of example trajectories. The goal is to reconstruct the cost function by analyzing robot behavior (input/output data) and learning from these demonstrations.

   #### Key Points:
   - **Cost Reconstruction**: IOC estimates the cost function as a linear combination of specific features, such as the distance from obstacles and the target.
   - **Convex Optimization**: A **convex optimization** problem is formulated to determine the weights that best approximate the cost function.
   - **Feature-Based Learning**: 16 features are used to capture important environmental factors, such as the robot's distance from the goal and its proximity to obstacles.

## Design Choices and Methodology

### Algorithm Development:
- **Forward Optimal Control**: 
  - The algorithm calculates the optimal policy by minimizing the discrepancy between expected and actual costs, with entropy used as a regularizer.
  - Control decisions are made using **Monte Carlo (MC) sampling** to choose actions at each time step.
  
- **Inverse Optimal Control**:
  - IOC uses the data from FOC trajectories to reconstruct the cost function.
  - **CVXPY** library is used for convex optimization, fitting the cost function based on the observed data.

### Key Functions:
- **State Cost Function**: Calculates the cost for a given state, considering distance from the target, proximity to obstacles, and environment limits.
- **Log Probability Density Function (logpdf)**: Computes the probability of a state based on a multivariate Gaussian distribution, used in the cost and entropy calculations.
- **Control Step**: Core function for both FOC and IOC, executing the policy decisions and updating the robot’s state at each time step.

## Results

### Forward Optimal Control (FOC):
- FOC successfully guides the robot to the target in most cases, with minimal oscillations near obstacles.
- Some edge cases cause the robot to become trapped in **local minima**, especially when obstacles are clustered.
- Results show that **entropy-based regularization** helps to balance exploration and exploitation during navigation.

### Inverse Optimal Control (IOC):
- IOC successfully reconstructs the cost function for most test cases, but **limitations** arise when the robot navigates near the boundaries of the environment.
- The lack of features to model environment boundaries causes the robot to go outside the predefined limits.
- The reconstruction of the cost function improved after adding features that take into account the **limits of the Robotarium environment**.

## Limitations and Future Developments

### Limitations:
- **Local Minima**: In certain configurations, the robot becomes trapped in local minima, particularly when the goal is close to an obstacle.
- **Unstable Trajectories**: In some cases, the reconstructed cost function leads to more oscillatory and noisy trajectories, especially near the target.

### Proposed Improvements:
- **Exponential Repulsion Term**: A repulsion term can be introduced to avoid obstacles more effectively. This term would increase the system’s ability to navigate around clusters of obstacles.
- **Refining the Cost Function**: The cost function could be further refined by modeling obstacles as clusters with Gaussian centers and introducing an **attraction term** near the target.
- **Robot Dimensions**: Future work could account for the robot's physical size, preventing it from navigating through spaces too narrow for its dimensions.

## Tools and Technologies

- **MATLAB/Simulink**: Used for simulation and algorithm development.
- **CVXPY**: A Python library for convex optimization, used to solve the optimization problems in IOC.
- **Robotarium**: Provides both simulation and real-world testing environments for the algorithms developed.


## References

1. **MATLAB Documentation**: [MATLAB & Simulink Documentation](https://www.mathworks.com/help/matlab/)
2. **CVXPY Documentation**: [CVXPY Documentation](https://www.cvxpy.org/)
3. **Robotarium**: [Robotarium Environment](https://www.robotarium.org/)



