import pygame
pygame.init()

pygame.display.set_caption("easy platformer")  # sets the window title
screen = pygame.display.set_mode((800, 800))  # creates game screen
screen.fill((0,0,0))
clock = pygame.time.Clock() #set up clock
gameover = False #variable to run our game loop
image = pygame.image.load("fish in the ocean.jpg")
Link = pygame.image.load('fish.png') #load your spritesheet
Link.set_colorkey((255, 0, 255)) #this makes bright pink (255, 0, 255) transparent (sort of)

#CONSTANTS
LEFT=0
RIGHT=1
UP = 2
DOWN = 3

A=0
W=2
D=1
S=3

xpos=50
ypos=50


controller = pygame.joystick.Joystick(0)
controller.init()

#player variables
xpos = 500 #xpos of player
ypos = 200 #ypos of player
vx = 0 #x velocity of player
vy = 0 #y velocity of player
keys = [False, False, False, False] #this list holds whether each key has been pressed
isOnGround = False #this variable stops gravity from pulling you down more when on a platform

#player 2
xpos2 = 100 #xpos of player
ypos2 = 100 #ypos of player
vx2 = 0 #x velocity of player
vy2 = 0 #y velocity of player
keys2=[False, False, False, False] #this list holds whether each key has been pressed
isOnGround2 = False #this variable stops gravity from pulling you down more when on a platform

#SOUND
jump = pygame.mixer.Sound('jump.wav')
music = pygame.mixer.music.load('music.wav')
pygame.mixer.music.play(-1)

xpos = 400 #xpos of player
ypos = 500-18 #ypos of player
vx = 0 #x velocity of player
keys = [False, False, False, False] #this list holds whether each key has been pressed

frameWidth = 60
frameHeight = 70
RowNum = 0 #for left animation, this will need to change for other animations
frameNum = 0
ticker = 0
pygame.image.load("sky.jfif")
while not gameover: #GAME LOOP############################################################
    clock.tick(60) #FPS
   #Input Section------------------------------------------------------------
    for event in pygame.event.get(): #quit game if x is pressed in top corner
        if event.type == pygame.QUIT:
            gameover = True
  
        if event.type == pygame.KEYDOWN: #keyboard
            if event.key == pygame.K_LEFT:
                keys[LEFT]=True
            
            elif event.key == pygame.K_UP:
                keys[UP]=True
            
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT]=True
            elif event.key == pygame.K_w:#2 player up
                keys2[W]=True
            elif event.key == pygame.K_a:#2 player left
                keys2[A]=True
            elif event.key == pygame.K_d:#right 2 player
                keys2[D]=True
                
            
            
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[LEFT]=False
            
            elif event.key == pygame.K_UP:
                keys[UP]=False
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT]=False
            elif event.key == pygame.K_w:#2 player
                keys2[W]=False
            elif event.key == pygame.K_a:#2 player
                keys2[A]=False
            elif event.key == pygame.K_d:#2 player
                keys2[D]=False
    
        if event.type == pygame.KEYDOWN: #keyboard input
            if event.key == pygame.K_LEFT:
                keys[0]=True
            elif event.key == pygame.K_RIGHT:
                keys[1]=True
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[0]=False
            elif event.key == pygame.K_RIGHT:
                keys[1]=False
                
    if controller.get_button(0):
        keys [UP] =True
    else:
        keys [UP] =False

    xVel = controller.get_axis(0) #returns a number b/t -1 and 1
    yVel = controller.get_axis(1) #returns a number b/t -1 and 1
#physics section--------------------------------------------------------------------
#LEFT MOVEMENT
    if keys[LEFT]==True:
        vx=-3
#RIGHT movement
    elif keys[RIGHT]==True:
        vx=3
#turn off velocity
    else:
        vx = 0
    
    if keys2[A]==True:
        vx2=-3
#RIGHT movement
    elif keys2[D]==True:
        vx2=3
        
        
#turn off velocity
    else:
        vx2 = 0
    
    #JUMPING
    if keys[UP] == True and isOnGround == True: #only jump when on the ground
        vy = -8
        isOnGround = False
        direction = UP
        pygame.mixer.Sound.play(jump)
    if keys2[W] == True and isOnGround2 == True: #only jump when on the ground
        vy2 = -8
        isOnGround2 = False
        direction = UP
        pygame.mixer.Sound.play(jump)
        
        
    




#COLLISION
    if xpos+20>100 and xpos<200 and ypos+60 >750 and ypos+60 <770:
        ypos = 750-60
        isOnGround = True
        vy = 0
    elif xpos+20>200 and xpos<300 and ypos+60 >650 and ypos+60 <670:
        ypos = 650-60
        isOnGround = True
        vy = 0
    elif xpos+20>300 and xpos<400 and ypos+60 >550 and ypos+60 <570:
        ypos = 550-60
        isOnGround = True
        vy = 0
    
    elif xpos+20>400 and xpos<500 and ypos+60 >450 and ypos+60 <470:
        ypos = 450-60
        isOnGround = True
        vy = 0
    
    elif xpos+20>500 and xpos<600 and ypos+60 >550 and ypos+60 <570:
        ypos = 550-60
        isOnGround = True
        vy = 0
    
    #yellow collision!
    elif xpos+20>600 and xpos<700 and ypos+60 >650 and ypos+60 <670:
        ypos = 650-60
        isOnGround = True
        vy = 0
    else:
        isOnGround = False
    
    if xpos2+20>100 and xpos2<200 and ypos2+60 >750 and ypos2+60 <770:
        ypos2 = 750-60
        isOnGround2 = True
        vy2 = 0
    elif xpos2+20>200 and xpos2<300 and ypos2+60 >650 and ypos2+60 <670:
        ypos2= 650-60
        isOnGround2 = True
        vy2 = 0
    elif xpos2+20>300 and xpos2<400 and ypos2+60 >550 and ypos2+60 <570:
        ypos2 = 550-60
        isOnGround2 = True
        vy2 = 0
    
    elif xpos2+20>400 and xpos2<500 and ypos2+60 >450 and ypos2+60 <470:
        ypos2 = 450-60
        isOnGround2 = True
        vy2 = 0
    
    elif xpos2+20>500 and xpos2<600 and ypos2+60 >550 and ypos2+60 <570:
        ypos2 = 550-60
        isOnGround2 = True
        vy2 = 0
    
    #yellow collision!
    elif xpos2+20>600 and xpos2<700 and ypos2+60 >650 and ypos2+60 <670:
        ypos2 = 650-60
        isOnGround2 = True
        vy2= 0
    else:
        isOnGround2 = False




#stop falling if on bottom of game screen
    if ypos > 760:
        isOnGround = True
        vy = 0
        ypos = 760
        
    if ypos2 > 760:
        isOnGround2 = True
        vy2 = 0
        ypos2 = 760

#gravity
    if isOnGround == False:
        vy+=.2 #notice this grows over time, aka ACCELERATION
    if isOnGround2== False:
        vy2+=.2


#update player position
    xpos+=vx 
    ypos+=vy
    xpos += int(xVel * 10)
    ypos += int(yVel * 10)
    xpos2+=vx2
    ypos2+=vy2
 #ANIMATION-------------------------------------------------------------------
        
    # Update Animation Information
    # Only animate when in motion
    if vx>0:
        RowNum = 0
        
    if vx < 0: #left animation
        Rownum=1
        # Ticker is a spedometer. We don't want Link animating as fast as the
        # processor can process! Update Animation Frame each time ticker goes over
        ticker+=1
        if ticker%10==0: #only change frames every 10 ticks
          frameNum+=1
           #If we are over the number of frames in our sprite, reset to 0.
           #In this particular case, there are 10 frames (0 through 9)
        if frameNum>2: 
           frameNum = 0
  

# RENDER Section--------------------------------------------------------------------------------
        
    screen.fill((255,255,255)) #wipe screen so it doesn't smear
    screen.blit(image,(0,0))
    #pygame.draw.rect(screen, (100, 200, 100), (xpos, ypos, 20, 40))
    #pygame.draw.rect(screen, (100, 200, 100), (xpos2, ypos2, 20, 40))
   
#first platform
    pygame.draw.rect(screen, (200, 0, 100), (100, 750, 100, 20))

#second platform
    pygame.draw.rect(screen, (100, 0, 200), (200, 650, 100, 20))#purple
#third platform
    pygame.draw.rect(screen, (255, 0, 255), (300, 550, 100, 20))#white

    pygame.draw.rect(screen, (0, 255, 255), (400, 450, 100, 20))#aqua

    pygame.draw.rect(screen, (138,43,226), (500, 550, 100, 20))#magenta

    pygame.draw.rect(screen, (255, 255, 0), (600, 650, 100, 20))#yellow
    pygame.draw.rect(screen, (255, 0, 255), (700, 750, 100, 20))#magenta
    pygame.draw.rect(screen, (255,255,0), (500, 350, 100, 20))
    screen.blit(Link, (xpos, ypos), (frameWidth*frameNum, RowNum*frameHeight, frameWidth, frameHeight))
   
    pygame.display.flip()#this actually puts the pixel on the screen
    
    pygame.quit()
