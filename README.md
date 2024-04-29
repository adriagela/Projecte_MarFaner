# PROJECTE MAR FANER
## Es millor projecte de s'història.
### Poole Party🏆🔥
![JordanPoole](https://cdn.nba.com/headshots/nba/latest/1040x760/1629673.png)
### Base de dades:
### Codi momentani del projecte foc foc foc:
import pygame
import random

pygame.init()

#Variables necessaries
size = width, height = 800, 600
pantalla = pygame.display.set_mode(size)
clock = pygame.time.Clock()
fps = 60

fondo = pygame.image.load("projecte/imatges/fondo.png").convert()
fondo = pygame.transform.scale(fondo, size)

basketball = pygame.image.load("projecte/imatges/Basketball.png").convert_alpha()
basketball = pygame.transform.scale(basketball, (60, 60))

#aro = pygame.image.load("projecte/imatges/aro.png").convert_alpha()
#aro = pygame.transform.scale(aro, (500, 500))

# Colors
negre = (0, 0, 0)

def main():
    game_on = True
    ballX = 120
    ballY = height - 170
    ball_dy = 0
    gravetat = 0.6 
    puntuacio = 0
    ball_dx = 0
    game_over = False

    while game_on:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_on = False

            elif event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE and not game_over:
                    ball_dy = -10  # Impuls per amunt al pitjar espai
                    ball_dx = 5  # Impuls lateral al pitjar espai

        pantalla.blit(fondo, (0, 0))

        
        pantalla.blit(basketball, (ballX, ballY))
        #Moviment lateral 
        ballY += ball_dy
        ball_dy += gravetat
        ballX += ball_dx

        

        # Rebot inferior
        if ballY >= height - basketball.get_height():
            ballY = height - basketball.get_height()
            ball_dy *= -0.5  # Amortiguació
            ball_dx *= 0.8  # -velocitat horitzontal alñ rebotar

        # Rebots laterals
        if ballX <= 0 or ballX >= width - basketball.get_width():
            ball_dx *= -1
        

        # Mostrar puntuació
        font = pygame.font.Font(None, 36)
        pantalla_text = font.render(f"Puntuación: {puntuacio}", True, negre)
        pantalla.blit(pantalla_text, (10, 10))

        pygame.display.update()
        clock.tick(fps)

if __name__ == "__main__":
    main()
