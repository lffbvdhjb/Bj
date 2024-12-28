# Bj
Spider attack
import pygame
import random

# Pygame ആരംഭിക്കുക
pygame.init()

# സ്ക്രീൻ ഡൈമെൻഷൻ നിർവ്വചിക്കുക
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("വെള്ള ബിന്ദുവും ചുവന്ന ചിലന്തിയും")

# നിറങ്ങൾ നിർവ്വചിക്കുക
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# ബിന്ദുവിന്റെ പ്രാരംഭ സ്ഥാനം
dot_x = SCREEN_WIDTH // 2
dot_y = SCREEN_HEIGHT // 2
dot_radius = 10
dot_speed = 5

# ചിലന്തിയുടെ പ്രാരംഭ സ്ഥാനം
spider_x = random.randint(0, SCREEN_WIDTH)
spider_y = 0
spider_speed = 2

# ക്ലോക്ക് സജ്ജീകരിക്കുക
clock = pygame.time.Clock()

# ഗെയിം ലൂപ്പ്
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # കീപ്രസ് പരിശോധിക്കുക
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP]:
        dot_y -= dot_speed
    if keys[pygame.K_DOWN]:
        dot_y += dot_speed

    # ചിലന്തിയുടെ നീക്കം
    spider_y += spider_speed
    if spider_y > SCREEN_HEIGHT:
        spider_y = 0
        spider_x = random.randint(0, SCREEN_WIDTH)

    # ബിന്ദുവും ചിലന്തിയും തമ്മിലുള്ള തട്ടിപ്പ് പരിശോധിക്കുക
    distance = ((dot_x - spider_x) ** 2 + (dot_y - spider_y) ** 2) ** 0.5
    if distance < dot_radius + 15:  # 15 is the approximate radius of the spider
        print("ചിലന്തി ആക്രമിച്ചു! ഗെയിം ഓവർ.")
        running = False

    # സ്ക്രീൻ അപ്‌ഡേറ്റ് ചെയ്യുക
    screen.fill(BLACK)
    pygame.draw.circle(screen, WHITE, (dot_x, dot_y), dot_radius)
    pygame.draw.circle(screen, RED, (spider_x, spider_y), 15)  # ചിലന്തി
    pygame.display.flip()

    # ഫ്രെയിം നിരക്ക് നിയന്ത്രിക്കുക
    clock.tick(60)
