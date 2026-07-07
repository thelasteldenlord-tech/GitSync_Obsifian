``` python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats
from matplotlib.animation import FuncAnimation

def evolving_distribution(n_points=1000, n_timesteps=50):
    """
    Simulate and visualize how a mixture of distributions evolves over time.
    The distribution starts as a single normal and gradually splits into a bimodal mixture.
    """
    # Set up the figure
    fig, ax = plt.subplots(figsize=(12, 6))
    ax.set_xlim(-6, 6)
    ax.set_ylim(0, 0.5)
    ax.set_title('Evolution of Probability Distribution Over Time')
    ax.set_xlabel('Value')
    ax.set_ylabel('Density')
    
    # Initial distribution parameters
    mu1, sigma1 = 0, 1
    mu2, sigma2 = -2, 0.5
    mu3, sigma3 = 2, 0.5
    
    # Create initial line
    line, = ax.plot([], [], 'b-', lw=2, label='Distribution')
    ax.grid(True, alpha=0.3)
    ax.legend()
    
    # Set up x-values for plotting
    x = np.linspace(-6, 6, n_points)
    
    def init():
        line.set_data([], [])
        return line,
    
    def animate(frame):
        # Calculate progress (0 to 1)
        progress = frame / n_timesteps
        
        # Start with a single normal distribution
        y1 = stats.norm.pdf(x, mu1, sigma1)
        
        # Gradually introduce the bimodal components
        if progress > 0.2:
            # Smoothly transition from unimodal to bimodal
            weight1 = max(0, 1 - (progress - 0.2) / 0.6)
            weight2 = min(1, (progress - 0.2) / 0.6) / 2
            
            # Calculate the mixture components
            y2 = stats.norm.pdf(x, mu2, sigma2)
            y3 = stats.norm.pdf(x, mu3, sigma3)
            
            # Combine the distributions
            y = y1 * weight1 + y2 * weight2 + y3 * weight2
        else:
            y = y1
        
        # Add some random noise that decreases over time
        noise = np.random.normal(0, 0.02 * (1 - progress), len(x))
        y = np.maximum(0, y + noise)
        
        line.set_data(x, y)
        return line,
    
    # Create the animation
    anim = FuncAnimation(fig, animate, init_func=init,
                        frames=n_timesteps, interval=100, 
                        blit=True)
    
    plt.show()
    return anim

# Function to generate static snapshots at specific times
def distribution_snapshots(n_points=1000, times=[0, 0.25, 0.5, 0.75, 1.0]):
    """
    Generate static snapshots of the distribution at specific points in time
    """
    fig, axes = plt.subplots(1, len(times), figsize=(20, 4))
    x = np.linspace(-6, 6, n_points)
    
    for i, t in enumerate(times):
        mu1, sigma1 = 0, 1
        mu2, sigma2 = -2, 0.5
        mu3, sigma3 = 2, 0.5
        
        # Calculate distribution based on time
        y1 = stats.norm.pdf(x, mu1, sigma1)
        
        if t > 0.2:
            weight1 = max(0, 1 - (t - 0.2) / 0.6)
            weight2 = min(1, (t - 0.2) / 0.6) / 2
            
            y2 = stats.norm.pdf(x, mu2, sigma2)
            y3 = stats.norm.pdf(x, mu3, sigma3)
            
            y = y1 * weight1 + y2 * weight2 + y3 * weight2
        else:
            y = y1
        
        axes[i].plot(x, y, 'b-', lw=2)
        axes[i].set_xlim(-6, 6)
        axes[i].set_ylim(0, 0.5)
        axes[i].set_title(f't = {t:.2f}')
        axes[i].grid(True, alpha=0.3)
        
        if i == 0:
            axes[i].set_ylabel('Density')
        axes[i].set_xlabel('Value')
    
    plt.tight_layout()
    plt.show()