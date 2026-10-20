``` python
import random
import math
from collections import defaultdict
import matplotlib.pyplot as plt

class SimpleDistribution:
    """
    A lightweight implementation of probability distribution calculations
    using only Python's standard library.
    """
    def __init__(self, mean=0, std=1):
        self.mean = mean
        self.std = std
    
    def normal_pdf(self, x):
        """Calculate normal distribution PDF without numpy"""
        exp_term = math.exp(-(x - self.mean)**2 / (2 * self.std**2))
        return (1 / (self.std * math.sqrt(2 * math.pi))) * exp_term
    
    def generate_samples(self, n_samples=1000):
        """Generate samples using Box-Muller transform"""
        samples = []
        for _ in range((n_samples + 1) // 2):
            # Box-Muller transform
            u1 = random.random()
            u2 = random.random()
            z1 = math.sqrt(-2 * math.log(u1)) * math.cos(2 * math.pi * u2)
            z2 = math.sqrt(-2 * math.log(u1)) * math.sin(2 * math.pi * u2)
            samples.extend([z1 * self.std + self.mean, z2 * self.std + self.mean])
        return samples[:n_samples]

def visualize_distribution_evolution(n_steps=5, n_samples=1000):
    """
    Visualize how a distribution evolves over time using simple histogram
    """
    fig, axes = plt.subplots(1, n_steps, figsize=(15, 3))
    
    for i in range(n_steps):
        progress = i / (n_steps - 1)
        
        # Start with one distribution and gradually split into two
        samples = []
        if progress < 0.5:
            # Single distribution
            dist = SimpleDistribution(mean=0, std=1)
            samples = dist.generate_samples(n_samples)
        else:
            # Mixture of two distributions
            weight = min(1.0, (progress - 0.5) * 2)
            dist1 = SimpleDistribution(mean=-2, std=0.5)
            dist2 = SimpleDistribution(mean=2, std=0.5)
            
            # Generate weighted samples
            n1 = int(n_samples * weight)
            n2 = n_samples - n1
            samples = dist1.generate_samples(n1) + dist2.generate_samples(n2)
            random.shuffle(samples)
        
        # Create histogram
        axes[i].hist(samples, bins=30, density=True, alpha=0.7)
        axes[i].set_xlim(-6, 6)
        axes[i].set_ylim(0, 0.5)
        axes[i].set_title(f't = {progress:.2f}')
        
        if i == 0:
            axes[i].set_ylabel('Density')
        axes[i].set_xlabel('Value')
    
    plt.tight_layout()
    plt.show()

def simple_monte_carlo(n_samples=10000):
    """
    Simple Monte Carlo simulation using only standard library
    """
    results = defaultdict(int)
    for _ in range(n_samples):
        # Simulate random walk
        position = 0
        for _ in range(10):
            position += random.choice([-1, 1])
        results[position] += 1
    
    # Convert to probabilities
    total = sum(results.values())
    positions = sorted(results.keys())
    probabilities = [results[pos]/total for pos in positions]
    
    # Plot
    plt.figure(figsize=(10, 5))
    plt.bar(positions, probabilities)
    plt.title('Simple Random Walk Distribution')
    plt.xlabel('Final Position')
    plt.ylabel('Probability')
    plt.grid(True, alpha=0.3)
    plt.show()

# Example usage:
# visualize_distribution_evolution()
# simple_monte_carlo()