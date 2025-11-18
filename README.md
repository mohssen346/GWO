# Grey Wolf Optimizer (GWO) Implementation

A Python implementation of the Grey Wolf Optimizer algorithm for solving optimization problems.

## 📋 Overview

This repository contains a complete implementation of the Grey Wolf Optimizer (GWO), a nature-inspired metaheuristic optimization algorithm based on the leadership hierarchy and hunting mechanism of grey wolves in nature.

## 🐺 Algorithm Description

The Grey Wolf Optimizer mimics the social hierarchy and hunting behavior of grey wolves:

- **Alpha (α)**: The best solution
- **Beta (β)**: The second-best solution
- **Delta (δ)**: The third-best solution
- **Omega (ω)**: The rest of the candidate solutions

The algorithm iteratively updates the positions of search agents based on the positions of alpha, beta, and delta wolves.

## 🚀 Features

- Clean and simple implementation
- Easy to customize for different optimization problems
- Includes sphere function as a benchmark test case
- Visualizes convergence through iteration logging

## 📦 Requirements

```python
numpy
copy
```

## 💻 Usage

### Basic Example

```python
import numpy as np
from gwo import GWO

# Define your fitness function
def sphere_fitness(X):
    fit_val = 0
    for i in range(len(X)):
        fit_val = fit_val + X[i]*X[i]
    return fit_val

# Set parameters
dim = 3                    # Problem dimension
fitness = sphere_fitness   # Fitness function
max_iter = 1000           # Maximum iterations
num_wolf = 50             # Population size
minx, maxx = -10, 10      # Search space bounds

# Run optimization
best_position = GWO.main(fitness, max_iter, num_wolf, dim, minx, maxx)

print("Best position found:", best_position)
print("Best fitness value:", fitness(best_position))
```

## 📊 Parameters

| Parameter | Description | Type |
|-----------|-------------|------|
| `fitness` | Objective function to minimize | function |
| `max_iter` | Maximum number of iterations | int |
| `num_wolf` | Population size (number of wolves) | int |
| `dim` | Problem dimension | int |
| `minx` | Lower bound of search space | float |
| `maxx` | Upper bound of search space | float |

## 🔧 How It Works

1. **Initialization**: Random population of wolves within search space
2. **Evaluation**: Calculate fitness for each wolf
3. **Hierarchy**: Identify alpha, beta, and delta wolves
4. **Position Update**: Update positions based on top three wolves
5. **Iteration**: Repeat steps 2-4 until convergence or max iterations

### Key Algorithm Components

**Convergence Parameter (a)**:
```python
a = 2 * (1 - Iter/max_iter)  # Linearly decreases from 2 to 0
```

**Position Update**:
```python
A1, A2, A3 = a*(2*np.random.rand()-1)
C1, C2, C3 = 2*np.random.rand()

X1 = alpha_position - A1 * abs(C1 * alpha_position - current_position)
X2 = beta_position - A2 * abs(C2 * beta_position - current_position)
X3 = delta_position - A3 * abs(C3 * delta_position - current_position)

new_position = (X1 + X2 + X3) / 3
```

## 📈 Example Results

For the sphere function with:
- Dimensions: 3
- Search space: [-10, 10]
- Population: 50 wolves
- Iterations: 1000

The algorithm converges to near-optimal solution (≈ 0) within 400 iterations.

## 🎯 Applications

The GWO algorithm can be applied to various optimization problems:

- Function optimization
- Feature selection
- Neural network training
- Engineering design problems
- Scheduling problems
- And more...

## 📝 Customization

To use GWO with your own optimization problem:

1. Define your fitness/objective function:
```python
def your_fitness_function(X):
    # X is a list/array of decision variables
    # Return the fitness value (to be minimized)
    return fitness_value
```

2. Set appropriate parameters for your problem
3. Run the optimizer

## 🔍 Code Structure

```
GWO.ipynb
├── Imports (numpy, copy)
├── sphere_fitness()      # Example fitness function
├── GWO class
│   ├── __init__()       # Initialize wolf position
│   └── main()           # Main optimization loop
└── Example usage
```

## 📚 References

Mirjalili, S., Mirjalili, S. M., & Lewis, A. (2014). Grey wolf optimizer. Advances in engineering software, 69, 46-61.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page.

## 📄 License

This project is open source and available under the MIT License.

## 👤 Author

Your Name - [Your GitHub Profile](https://github.com/yourusername)

## ⭐ Show your support

Give a ⭐️ if this project helped you!

---

**Note**: This is a basic implementation for educational purposes. For production use, consider adding features like:
- Constraint handling
- Multi-objective optimization
- Parallel computation
- Advanced convergence criteria
- Parameter adaptation strategies
