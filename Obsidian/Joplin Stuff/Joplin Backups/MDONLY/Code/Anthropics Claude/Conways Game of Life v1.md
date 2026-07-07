```python

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation

class DLA:
    def __init__(self, size=101, n_particles=1000):
        self.size = size
        self.n_particles = n_particles
        self.grid = np.zeros((size, size))
        self.grid[size//2, size//2] = 1  # Seed particle
        self.particles = []

    def add_particle(self):
        angle = np.random.uniform(0, 2*np.pi)
        radius = self.size//2 - 2
        x = int(self.size//2 + radius * np.cos(angle))
        y = int(self.size//2 + radius * np.sin(angle))
        self.particles.append([x, y])

    def move_particle(self, p):
        dx, dy = np.random.choice([-1, 0, 1], size=2)
        new_x, new_y = p[0] + dx, p[1] + dy
        if 0 <= new_x < self.size and 0 <= new_y < self.size:
            p[0], p[1] = new_x, new_y

    def check_neighbor(self, p):
        for dx in [-1, 0, 1]:
            for dy in [-1, 0, 1]:
                if dx == 0 and dy == 0:
                    continue
                nx, ny = p[0] + dx, p[1] + dy
                if 0 <= nx < self.size and 0 <= ny < self.size:
                    if self.grid[nx, ny] == 1:
                        return True
        return False

    def update(self):
        for p in self.particles[:]:
            if self.check_neighbor(p):
                self.grid[p[0], p[1]] = 1
                self.particles.remove(p)
                self.add_particle()
            else:
                self.move_particle(p)
        while len(self.particles) < self.n_particles:
            self.add_particle()

    def animate(self, num_frames=200):
        fig, ax = plt.subplots()
        im = ax.imshow(self.grid, cmap='binary')
        plt.title("Diffusion-Limited Aggregation")

        def update(frame):
            self.update()
            im.set_array(self.grid)
            return [im]

        anim = FuncAnimation(fig, update, frames=num_frames, interval=50, blit=True)
        plt.show()

if __name__ == "__main__":
    dla = DLA(size=101, n_particles=1000)
    dla.animate(num_frames=500)