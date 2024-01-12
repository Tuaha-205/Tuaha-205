import pygame
import random

# Initialize Pygame
pygame.init()

# Set screen dimensions
screen_width = 600
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Snake Game")

# Define colors
black = (0, 0, 0)
white = (255, 255, 255)
red = (255, 0, 0)
green = (0, 255, 0)

# Set snake starting position and dimensions
snake_position = [100, 50]
snake_body = [[100, 50], [90, 50], [80, 50]]
snake_size = 10

# Set food position randomly
food_position = [random.randrange(1, screen_width // snake_size) * snake_size,
                 random.randrange(1, screen_height // snake_size) * snake_size]

# Set movement variables
food_eaten = False
game_over = False
change_to = "RIGHT"  # Possible values: "RIGHT", "LEFT", "UP", "DOWN"

# Function to display score
def display_score(score):
    font = pygame.font.Font(None, 36)
    text = font.render("Your Score: " + str(score), True, white)
    screen.blit(text, [0, 0])

# Main game loop

while
 
not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True

        
elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_RIGHT and change_to != "LEFT":
                change_to = "RIGHT"
            elif event.key == pygame.K_LEFT and change_to != "RIGHT":
                change_to = "LEFT"
            elif event.key == pygame.K_UP and change_to != "DOWN":
                change_to = "UP"
            elif event.key == pygame.K_DOWN and change_to != "UP":
                change_to = "DOWN"

    # Update snake position based on change_to
    if change_to == "RIGHT":
        snake_position[0] += snake_size
    elif change_to == "LEFT":
        snake_position[0] -= snake_size
    elif change_to == "UP":
        snake_position[1] -= snake_size
    elif change_to == "DOWN":
        snake_position[1] += snake_size

    # Check for collisions with walls or self
    snake_body.insert(0, list(snake_position))
    if snake_position[0] >= screen_width or snake_position[0] < 0 or snake_position[1] >= screen_height or snake_position[1] < 0:
        game_over = True
    for block in snake_body[1:]:
        if snake_position[0] == block[0] and snake_position[1] == block[1]:
            game_over = True

    # Check for food collision
    if snake_position[0] == food_position[0] and snake_position[1] == food_position[1]:
        food_eaten = True
    else:
        snake_body.pop()

    if food_eaten:
        food_position = [random.randrange(1, screen_width // snake_size) * snake_size,
                         random.randrange(1, screen_height // snake_size) * snake_size]
        food_eaten = False

    # Fill background
    screen.fill(black)

    # Draw snake
    for pos in snake_body:
        pygame.draw.rect(screen,
