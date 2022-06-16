# main
Space Invaders
import pygame
import random
import math
from pygame import mixer
    # Helps us handle the music functionalities inside the game
    # Repeating, loading music
# Random package: Allows for us to randomize values, different
# Intialize the pygame(Have access to its cool methods, its functionalities)
pygame.init()

# Create the game screen
screen = pygame.display.set_mode((800, 600))

# Title and Icon:
pygame.display.set_caption("Space Invaders")
icon = pygame.image.load('001-ufo.png')
pygame.display.set_icon(icon)

# Background Image:
background = pygame.image.load("Temp-800x600.jpg")

#Background Sound

mixer.music.load('simpsons.mid')
mixer.music.play(-1)

# Load the music you want to play
    #mixer.music.load()
# The music should be played continously!
    #mixer.music.play(-1)
# If you have music that lasts for a short time, implement
    #variable = mixer.Sound('name of the file')
    #variable.play(): Play the sound once and that's it until
    #its next iteration

# How to add images(Player): Load your image, implement coordinates
playerImg = pygame.image.load("001-spaceship.png")
PlayerX = 368
PlayerY = 480
playerX_change = 0
#Enemy:

# How to add multiple enemies?
EnemyImg = []
EnemyX = []
EnemyY = []
EnemyX_change = []
EnemyY_change = []

# We can do in a list, and create a variable that
# specifies the number of enemies we want in the list
# Using these variables, we can add the image, the coordinates,
# the changes in their coordinates, etc.
number_of_enemies = 10

# For loop: Allow us to add our enemies onto the screen
#For every iteration of this loop, we are appending the
#image, coordinates, the changes in position of the enemies
    # Process:
        # Load the image, implement it on its list
        # Implement the x and y coordinates(chosen at random)
        # Implement the speed and the y coordinate change of the enemies


for i in range(number_of_enemies):

    EnemyImg.append(pygame.image.load("001-space-ship.png"))

    EnemyX.append(random.randint(0, 735))
# I want my enemy to appear no less than a length of 0 pixels,
# but no more than a length of 800 pixels

    EnemyY.append(random.randint(50, 150))
# I want my enemy to appear no lower 50 pixels, but no higher
# than 150 pixels

    EnemyX_change.append(1.2)
    EnemyY_change.append(40)

# Enemy: Loading our enemy, implementing its coordinates
# When we hit our enemy, we want it to appear at random
# places, its position should not be constant


# Bullet:
# Ready - You can't see the bullet on the screen
# Fire - The bullet is currently moving
# Load the image, implement the coordinates, and its changes

BulletImg = pygame.image.load("001-bullet.png")
BulletX = 0
BulletY = 480
BulletX_change = 0
BulletY_change = 4
bullet_state = "ready"
# BulletX will be changed based on the x coordinate of
# the spaceship

# Created a function that controls the player's position,
# Takes in two parameters of information: an x and y coordinate
# screen.blit(): Draw the image onto the screen, at a position (x,y)

# Score:

score_value = 0
font = pygame.font.Font('appleberry.ttf', 32)
textX = 10
textY = 10

    # Font: The type or style of the text that's displayed
    # Process:
        # Create a variable that will keep track of our score
        # Implement the font we want and the size of the text
        # Implement the coordinates
def show_score(x,y):
    score = font.render("Score : " + str(score_value), True, (255, 255, 255))
    screen.blit(score, (x, y))

    # Create a function that shows the score
    # Process:
        # Before implementing the image, we need to render
        # the text onto the screen(font and size implemented)
        #font.render():
            # The text you want implemented
            # True(it can be displayed onto the screen
            # The color, with the RGB scale
            # (0-255)(red), 0-255(green), 0-255(blue))
        # We need to draw it onto the screen

# Game Over Function:

over_font = pygame.font.Font('appleberry.ttf', 64)

def game_over():
    over_text = over_font.render("GAME OVER!", True, (255, 255, 255))
    screen.blit(over_text, (250, 250))

    # Called when a particular enemy reaches the y coordinate bound

    # After the enemies are collected and implemented outside the
    # game screen, we want to call the function that displays this line
    # of text

    # We can no longer play the game!

# Player Function:
def player(x, y):
    screen.blit(playerImg, (x, y))
    # Two arguments(Image, tuple(coordinates)), drawing the image

# Enemy Function:

def enemy(x, y, i):
    screen.blit(EnemyImg[i], (x, y))


# We are creating a function that draws the enemy on our screen,
# at a certain position(x,y)

def fire_bullet(x, y):
    global bullet_state
    bullet_state = "fire"
    screen.blit(BulletImg, (x + 16, y + 10))


# Called when we press the spacebar
# Access the bullet_state variable, we want to change
# its value, then we want to draw the image
# The bullet appears at the center of the spaceship

def isCollision(EnemyX, EnemyY, BulletX, BulletY):
    distance = math.sqrt((math.pow(EnemyX - BulletX, 2)) + (math.pow(EnemyY - BulletY, 2)))
    if distance < 30:
        return True
    else:
        return False


# Creating a function that takes in four parameters of information

# (The x and y coordinates of our bullet and our enemy)
# Given these coordinates, we want to calculate the distance between
# the bullet and the enemy

# Afterwards, given our distance, if the distance is less
# than a certain number of pixels, we indicate that a
# collision has occured


# Game Loop: To keep the game running(exit the program if necessary)
# Any element that needs to be consistent: Inside the loop
# Ex:
# Exiting the Program
# Background Colors, the characters, their movements,
# the change in those movements(pressing the arrow keys), etc.
# Background images, characters' attributes, etc.
# Infinite while loop: THose elements are going to be consistent
# throughout the game
running = True
while running:
    screen.fill((0, 0, 0))
    # Background Image: From the top left corner
    screen.blit(background, (0, 0))
    # Implement the background color before your images!
    # For loop: Accounts for all the events inside of a game
    # Ex:
    # Background color, images
    # Characters, their movements
    # Attributes, character shooting, hitting an alien
    # Keeping Score for every alien hit
    # Keys pressed, any instance you hit a key,
    # changing the position of the character
    # Lives, Game Overs, Collisions, etc.

    for event in pygame.event.get():
        # For each event inside of all the events inside a game!

        if event.type == pygame.QUIT:
            running = False
        # If my event involves breaking out of the program,
        # If I want to exit out of the program, then I want
        # to stop my while loop from running

        # Accounts for the Movement Mechanics of our player:
        if event.type == pygame.KEYDOWN:
            # if keystroke is pressed, check to see whether it is left or right,
            # then move the character in accordance

            if event.key == pygame.K_LEFT:
                playerX_change -= 1.3
            # If I press the left arrow key, then move the character,
            # one pixel for every click, move to the right

            if event.key == pygame.K_RIGHT:
                playerX_change += 1.3

            # If I press the right arrow key, then move the character,
            # one pixel for every click, move to the right

            # We also need to account for any instance I let go of
            # a certain arrow key.
            # If we don't, the character will continously move in the
            # direction in which it's influenced by the key we hit

            if event.key == pygame.K_SPACE:
                if bullet_state == "ready":
                    bullet_sound = mixer.Sound('../pythonProjects/venv/laser.wav')
                    bullet_sound.play()
                    # Get the current x coordinate of
                    # the spaceship
                    BulletX = PlayerX
                    fire_bullet(BulletX, BulletY)

        # If the space key is pressed, then we want to
        # call the function(the bullet state has changed)
        # The bullet is implemented onto the screen
        # Not persistent

        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                playerX_change = 0
        # If the key we let go is either a left or a right arrow key,
        # then the character stops moving
    # 5 = 5 + -0.1 -> 5 = 5 - 0.1
    # 5 = 5 + 0.1 -> 5 = 5 + 0.1
    PlayerX = PlayerX + playerX_change
    # New value = #370 + x; x = how many iterations

    # Boundaries of the Game: Player
    # inside of the game screen(influenced by the dimensionalities
    # of the game window
    # Keep in mind: Our image(64 x 64 pixel)
    if PlayerX <= 0:
        PlayerX = 0
    # When we continously press the left arrow key, if it
    # reaches 0, then we want to set it equal to 0

    elif PlayerX >= 736:
        PlayerX = 736
    # 736: The size of the image itself, when Player1
    # (our x-coordinate is equivalent or over 736, we
    # want to stay at 736)

    #For multiple enemies: Perform same functionalities
        # For loop: Apply the functionalities for every enemy
        # Changing direction
        # Respawn to new location, collisions
        # Call our functions(implement on screen)


    for i in range(number_of_enemies):

        EnemyX[i] = EnemyX[i] + EnemyX_change[i]

        # The game is over when one of the enemies,
        # comes in contact with our spaceship or if it
        # reaches a y-coordinate bound

        # If one of the enemies reaches that bound, then
        # for each enemy, we no longer want them on the screen

        # Afterwards, the game over text will be displayed and the
        # enemies will no longer be implemented and their functionalities
        # will be lost


    # Enemy Movement
    # When the enemy hits a certain boundary, we want to keep it
    # at a certain speed when moving from left to right
    # We also want to enemy to move downwards once the enemy hits
    # boundary

        if EnemyX[i] <= 0:
            EnemyX_change[i] = 1.2
            EnemyY[i] = EnemyY[i] + EnemyY_change[i]

        elif EnemyX[i] >= 736:
            EnemyX_change[i] = -1.2
            EnemyY[i] = EnemyY[i] + EnemyY_change[i]

        enemy(EnemyX[i], EnemyY[i], i)
    # Collision: Implemented inside of our while loop

    # When the enemy and the bullet appears simultaneously,
    # the function will be executed continously and returns
    # true if the distance requirement is satisified

    # Only runs when the bullet is activated


# Winning Formula!
# Remove the enemies one by one for every collision
# Goal: For every collision, remove the enemy from the screen!
# Account: If there are enemies on the screen


# Calling Game

        collision = isCollision(EnemyX[i], EnemyY[i], BulletX, BulletY)
        if collision:
            collision_sound = mixer.Sound('Doh 4.mp3')
            collision_sound.play()
            BulletY = 480
            bullet_state = "ready"
            score_value += 1
            EnemyX[i] = random.randint(0, 735)
            EnemyY[i] = random.randint(50, 150)

# Collision: Implemented inside of our while loop
# When the enemy and the bullet appears simultaneously,
# the function will be executed continously and returns
# true if the distance requirement is satisified


    #Game Over:
        if EnemyY[i] > 350:
            for j in range(number_of_enemies):
                EnemyY[j] = 2000
            game_over()
            break

        # Only runs when the bullet is activated


    # Called the Function: My Image, then my (x,y) coordinate
    # representing the player's position

    # We want to make sure when the bullet reaches the 0
    # coordinate, we reset the value of the bullet to
    # its original value, then change the bullet_state
    # to ready

    # Bullet Movement:
    if bullet_state == "fire":
        fire_bullet(BulletX, BulletY)
        BulletY = BulletY - BulletY_change

    if BulletY <= 0:
        BulletY = 480
        bullet_state = "ready"

    # We want to check the state of our bullet
    # If the bullet is at fire state, we want to call
    # the function, and send our bullet up
    # The bullet is fired at a certain position inside of our screen,
    # then we want to shoot it up
    # We don't want the bullet to move with the spaceship



    # When the collision occurs, it does the following:
        # Resets the Bullet Y coordinate
        # Changes our bullet_state to ready(not on screen)
        # For every collision, increment the score by 1
        # When the collision occurs, we want to respawn
        # the enemy to random x and y coordinates

    player(PlayerX, PlayerY)
    show_score(textX, textY)
    pygame.display.update()

# .display.update(): Takes certain elements of a game,
# on the screen, and implements them
# Screen, Appearance, Player and object actions, score,
# bullets moving
