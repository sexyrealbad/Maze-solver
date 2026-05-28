from PIL import Image, ImageDraw
from collections import deque

# Load maze as a grid
def load_maze(image_path):
    maze = Image.open(image_path).convert('L')  # Grayscale
    width, height = maze.size
    pixels = maze.load()
    grid = [[1 if pixels[x, y] > 128 else 0 for x in range(width)] for y in range(height)]
    return grid, maze

# Solve maze using BFS
def solve_maze(grid):
    start = (0, 0)  # Adjust start point if necessary
    end = (len(grid[0]) - 1, len(grid) - 1)  # Adjust end point if necessary
    queue = deque([start])
    visited = set()
    visited.add(start)
    parent = {start: None}
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
    while queue:
        x, y = queue.popleft()
        if (x, y) == end:
            path = []
            while (x, y):
                path.append((x, y))
                x, y = parent[(x, y)]
            path.reverse()
            return path
        for dx, dy in directions:
            nx, ny = x + dx, y + dy
            if 0 <= nx < len(grid[0]) and 0 <= ny < len(grid) and grid[ny][nx] == 0 and (nx, ny) not in visited:
                queue.append((nx, ny))
                visited.add((nx, ny))
                parent[(nx, ny)] = (x, y)
    return None

# Draw the solution on the maze image
def draw_solution(maze, solution_path, output_path):
    draw = ImageDraw.Draw(maze)
    for x, y in solution_path:
        draw.point((x, y), fill=(255, 0, 0))  # Red for solution path
    maze.save(output_path)

# Main function
if __name__ == "__main__":
    input_path = "input/maze.png"
    output_path = "solved_maze.png"
    grid, maze = load_maze(input_path)
    solution_path = solve_maze(grid)
    if solution_path:
        draw_solution(maze, solution_path, output_path)
        print("Maze solved successfully!")
    else:
        print("No solution found.")
