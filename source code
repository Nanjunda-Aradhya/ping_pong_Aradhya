import pygame
import sys

# Initialize Pygame
pygame.init()

# Set up display
width, height = 800, 600
screen = pygame.display.set_mode((width, height))
pygame.display.set_caption("Ping Pong Game")

# Colors
black = (0, 0, 0)
white = (255, 255, 255)

# Paddle settings
paddle_width, paddle_height = 10, 100
player_speed = 7
computer_speed = 5

# Ball settings
ball_size = 15
ball_speed_x, ball_speed_y = 5, 5

# Initialize paddles and ball
player_rect = pygame.Rect(50, (height // 2) - (paddle_height // 2), paddle_width, paddle_height)
computer_rect = pygame.Rect(width - 60, (height // 2) - (paddle_height // 2), paddle_width, paddle_height)
ball_rect = pygame.Rect((width // 2) - (ball_size // 2), (height // 2) - (ball_size // 2), ball_size, ball_size)

# Game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    keys = pygame.key.get_pressed()
    if keys[pygame.K_w] and player_rect.top > 0:
        player_rect.y -= player_speed
    if keys[pygame.K_s] and player_rect.bottom < height:
        player_rect.y += player_speed

    # Move computer paddle
    if ball_rect.centery < computer_rect.centery and computer_rect.top > 0:
        computer_rect.y -= computer_speed
    if ball_rect.centery > computer_rect.centery and computer_rect.bottom < height:
        computer_rect.y += computer_speed

    # Move the ball
    ball_rect.x += ball_speed_x
    ball_rect.y += ball_speed_y

    # Ball collision with top and bottom
    if ball_rect.top <= 0 or ball_rect.bottom >= height:
        ball_speed_y = -ball_speed_y

    # Ball collision with paddles
    if ball_rect.colliderect(player_rect) or ball_rect.colliderect(computer_rect):
        ball_speed_x = -ball_speed_x

    # Ball out of bounds
    if ball_rect.left <= 0 or ball_rect.right >= width:
        ball_rect.x = (width // 2) - (ball_size // 2)
        ball_rect.y = (height // 2) - (ball_size // 2)
        ball_speed_x = -ball_speed_x

    # Drawing
    screen.fill(black)
    pygame.draw.rect(screen, white, player_rect)
    pygame.draw.rect(screen, white, computer_rect)
    pygame.draw.ellipse(screen, white, ball_rect)
    pygame.draw.aaline(screen, white, (width // 2, 0), (width // 2, height))

    pygame.display.flip()
    pygame.time.Clock().tick(60)
