# simulated-annealing-quickstart

模拟退火算法是一种用于寻找给定函数的全局最优解的随机化算法。它的灵感来源于材料科学中的退火过程，即将物体加热后再缓慢冷却以减少体系的缺陷，达到更稳定的状态。在优化领域，模拟退火通过模拟这一过程来尝试逃离局部最小值，从而寻求全局最小值。

该算法的基本步骤如下：
1. 初始化：选择一个初始点和初始温度。
2. 迭代过程：
   - 在当前解的邻域内随机选取一个新解。
   - 计算新解与当前解的目标函数值差。
   - 如果新解更优，则接受新解；如果新解较差，以一定概率接受新解，这个概率与温度和解的差异有关。
   - 逐渐降低温度。
3. 重复迭代直到满足终止条件（如温度低于某阈值）。

模拟退火算法可以在Colab中实现，因为Colab支持Python编程，并且可以运行各种数学和统计算法。下面是一个使用Python实现的模拟退火算法的简单示例，这个例子尝试找到函数 \(f(x) = x^2\) 的最小值：

```python
import math
import random

def objective_function(x):
    return x ** 2

def simulated_annealing():
    current_temp = 90  # 初始温度
    min_temp = 1       # 最低温度
    alpha = 0.9        # 温度衰减系数
    current_x = random.uniform(-10, 10)  # 初始解
    current_solution = objective_function(current_x)

    while current_temp > min_temp:
        next_x = current_x + random.uniform(-10, 10)  # 生成新的解
        next_solution = objective_function(next_x)
        
        # 接受条件
        if next_solution < current_solution:
            current_x = next_x
            current_solution = next_solution
        else:
            if random.uniform(0, 1) < math.exp((current_solution - next_solution) / current_temp):
                current_x = next_x
                current_solution = next_solution

        current_temp *= alpha  # 降温
        
    return current_x, current_solution

best_x, best_solution = simulated_annealing()
print(f"Best solution x: {best_x}, f(x): {best_solution}")
```

这段代码初始化了温度和解，然后通过随机选择新的解并根据一定概率接受较差的解来逐渐逼近全局最优解。最终结果会显示在哪个位置找到了函数的最小值。
