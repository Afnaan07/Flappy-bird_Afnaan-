# Flappy-bird_Afnaan-
import pygame
from pygame.locals import *
pygame.init()

klocka = pygame.time.Clock()
fps = 60

screen_width = 800
screen_height = 550

screen = pygame.display.set_mode((screen_height, screen_height))
pygame.display.set_caption("Flappy bird, Afnaan")

# variablar
ground_scroll = 0
ground_speed = 4

# backgrunds bilder

bg = pygame.image.load('bg.png')
floor_img = pygame.image.load('floor.png')

class Bird(pygame.sprite.Sprite):
    def __init__(self, x, y):
        pygame.sprite.Sprite.__init__(self)
        self.images = []
        self.index = 0
        self.counter = 0
        for num in range(1, 4):
            img = pygame.image.load(f'bird {num}.png')
            self.images.append(img)
        self.image = self.images[self.index]
        self.rect = self.image.get_rect()
        self.rect.center = [x, y]


bird_group = pygame.sprite.Group()
flappy = Bird(50, int(screen_height / 2))

bird_group.add(flappy)

run = True
while run:

    klocka.tick(fps)
    screen.blit(bg, (0,0))

    bird_group.draw(screen)

    screen.blit(floor_img, (ground_scroll ,500))
    ground_scroll -= ground_speed
    if abs(ground_scroll) > 35:
        ground_scroll = 0

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False
    pygame.display.update()
pygame.quit()

