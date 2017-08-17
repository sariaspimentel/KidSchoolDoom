#KidSchoolDoom
#game created as our final project
#python

import os, sys
import pygame
from time import time, sleep
from pygame.locals import *
from helpers import *
import random
if not pygame.font: print('Warning, fonts disabled')
if not pygame.mixer: print('Warning, sound disabled')

class PyManMain:

    def __init__(self, width=640,height=480):
        """Initialize"""
        """Initialize PyGame"""
        pygame.init()
        """Set the window Size"""
        self.width = width
        self.height = height
        """Create the Screen"""
        self.screen = pygame.display.set_mode((self.width
                                               , self.height))

    def MainLoop(self):
        """This is the Main Loop of the Game"""

        """tell pygame to keep sending up keystrokes when they are
        held down"""
        pygame.key.set_repeat(500, 30)
        """Load All of our Sprites"""
        self.LoadSprites();
        """Create the background"""
        self.background = pygame.Surface(self.screen.get_size())
        self.background = self.background.convert()
        self.background.fill((0,0,0))
        self.showIntro()
        start= time()
        school = pygame.image.load("data/images/school.png")
        #############JOE'S COMMENT################
        #This loop runs the snake game          #
        #########################################
        while 1:
            self.screen.blit(school, (0,0))
            # pygame.display.flip()
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    sys.exit()
                elif event.type == KEYDOWN:
                    if ((event.key == K_RIGHT)
                    or (event.key == K_LEFT)
                    or (event.key == K_UP)
                    or (event.key == K_DOWN)):
                        self.snake.move(event.key)

            """Check for collision"""
            lstCols = pygame.sprite.spritecollide(self.snake
                                                 , self.pellet_sprites
                                                 , True)
            """Update the amount of pellets eaten"""
            self.snake.pellets = self.snake.pellets + len(lstCols)

            """Do the Drawing"""
            self.screen.blit(self.background, (0, 0))
            if pygame.font:
                font = pygame.font.Font(None, 36)
                text = font.render("Number of Melons Collected: %s" % self.snake.pellets
                                    , 1, (58, 255, 28))
                textpos = text.get_rect(centerx=self.background.get_width()/2)
                self.screen.blit(text,textpos)
                if self.snake.pellets == 70:
                    conclusion = pygame.image.load('data/images/watertopicture.png')
                    trans = 1
                    break
                    while 1:
                       self.screen.blit(conclusion,(0,0))
                       pygame.display.flip()

            self.pellet_sprites.draw(self.screen)
            self.snake_sprites.draw(self.screen)
            pygame.display.flip()

            if self.snake.pellets < 70 and time()-start>14:
                lost = pygame.image.load('Lost screen 1.png')
                while 1:
                    self.screen.blit(lost,(0,0))
                    pygame.display.flip()
                    self.pellet_sprites.draw(self.screen)
                    self.snake_sprites.draw(self.screen)
                    pygame.display.flip()
        #END OF THE SNAKE GAME loop
        transition = pygame.image.load('data/images/watertopicture.png')
        trans = 1
        while trans == 1:
            self.screen.blit(transition, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    sys.exit()
                elif event.type == KEYDOWN:
                    if (event.key == K_SPACE):
                        trans = 0

        #start of 4pics1 word
        self.fourpicsoneword()
        print("done")
        #End of 4pics1word
        #Start of DDR
        self.jackieStart()
        self.JackieLoop()
        #End of DDR
        print("reached end of game")
        ending= pygame.image.load('data/images/Cconclusion.png')
        trans = 1
        while trans == 1:
            self.screen.blit(ending, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    sys.exit()
                elif event.type == KEYDOWN:
                    if (event.key == K_SPACE):
                        trans = 0
    def jackieStart(self, width=640,height=480):
        """Initialize"""
        """Initialize PyGame"""
        pygame.init()
        """Set the window Size"""
        self.width = width
        self.height = height
        """Create the Screen"""
        self.screen = pygame.display.set_mode((self.width
                                               , self.height))
        self.sdrevvv=pygame.image.load("data/images/sdrbackground-1.png")
        self.top=480
    def JackieLoop(self):
        """This is the Main Loop of the Game"""

        """Load All of our Sprites"""
        self.LoadSprites();
        """tell pygame to keep sending up keystrokes when they are
        held down"""
        pygame.key.set_repeat(500, 30)

        """Create the background"""
        self.background = pygame.Surface(self.screen.get_size())
        self.background = self.background.convert()
        self.background=self.sdrevvv

        while 1==1:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    sys.exit()
                    if event.key==K_ESCAPE:
                        sys.exit()
            self.screen.blit(self.background, (0, 0))
            self.arrows_sprite1.draw(self.screen)
            self.arrows_sprite2.draw(self.screen)
            self.arrows_sprite3.draw(self.screen)
            self.arrows_sprite4.draw(self.screen)
            self.gameStart()
            break
            pygame.display.flip()
    ##############4pics1word###########################
    def fourpicsoneword(self):

        pygame.key.set_repeat(500, 30)

        # """Create the background"""
        self.background = pygame.Surface(self.screen.get_size())
        self.background = self.background.convert()
        self.background.fill((0,0,0))

        img1 = pygame.image.load("data/images/pic 1.png")
        img2 = pygame.image.load("data/images/pic 2.png")
        img3 = pygame.image.load("data/images/pic 3.png")
        img4 = pygame.image.load("data/images/pic 4.png")
        img5 = pygame.image.load("data/images/pic 5.png")

        slide = 0
        while slide == 0:
            self.screen.blit(img1, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_a):
                            slide = 1
                        if (event.key == K_b or event.key == K_c):
                            if pygame.font:
                                font = pygame.font.Font(None, 16)
                                text = font.render("Try Again"
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                            pygame.display.flip()
        self.screen.blit(self.background, (0, 0))
        while slide == 1:
            self.screen.blit(img2, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_b):
                            slide = 2
                        if (event.key == K_a or event.key == K_c):
                            if pygame.font:
                                font = pygame.font.Font(None, 16)
                                text = font.render("Try Again"
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                            pygame.display.flip()
        while slide == 2:
            self.screen.blit(img3, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_c):
                            slide = 3
                        if (event.key == K_b or event.key == K_a):
                            if pygame.font:
                                font = pygame.font.Font(None, 16)
                                text = font.render("Try Again"
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                            pygame.display.flip()
        while slide == 3:
            self.screen.blit(img4, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_a):
                            slide = 4
                        if (event.key == K_b or event.key == K_c):
                            if pygame.font:
                                font = pygame.font.Font(None, 16)
                                text = font.render("Try Again"
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                            pygame.display.flip()
        while slide == 4:
            self.screen.blit(img5, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_b):
                            slide = 5
                            switch = 0
                            artintro = pygame.image.load("data/images/introtodance.png")
                        if (event.key == K_a or event.key == K_c):
                            if pygame.font:
                                font = pygame.font.Font(None, 16)
                                text = font.render("Try Again"
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                            pygame.display.flip()
        while switch == 0:
            self.screen.blit(artintro, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(switch)
                            switch = 2

    ##############4pics1wordtransition###########################
        #transition2 = pygame.image.load('data/images/2ndGameEnd.png')
        #trans = 0
        #while trans == 0:
            # self.screen.blit(transition2, (0,0))
            # pygame.display.flip()
            # for event in pygame.event.get():
            #     if event.type == pygame.QUIT:
            #         sys.exit()
            #     elif event.type == KEYDOWN:
            #         if (event.key == K_SPACE):
            #             trans = 0
    ##############school dance revolution#########################
    def gameStart(self):
        a=50
        missed = 0

        while a>0:
            x = random.randrange(0,100)
            z = random.randrange(0,100)
            a-=1
            clear=False
            delay= (-.0001*(self.arrows.newarrows)**2 + 1)*.01
            if delay<=0:
                delay=0.00001
            if pygame.font:
                font = pygame.font.Font(None, 36)
                text = font.render("Score: %s" % self.arrows.newarrows
                                    , 1, (255, 0, 0))
                textpos = text.get_rect(centerx=self.background.get_width()/2)
                self.screen.blit(text, textpos)
            if missed == 10:
                lost = pygame.image.load('Lost screen 1.png')
                while 1:
                    self.screen.blit(lost,(0,0))
                    pygame.display.flip()
            if self.arrows.newarrows >= 105:
                break

            while clear==False:
                self.arrows_sprite1.draw(self.screen)
                self.arrows_sprite2.draw(self.screen)
                self.arrows_sprite3.draw(self.screen)
                self.arrows_sprite4.draw(self.screen)
                if self.top==-30:
                    clear=True
                if x%4==0:
                    target=self.newarrows_sprite1
                    if z%8==1:
                        target2=self.newarrows_sprite2
                    elif z%8==2:
                        target2=self.newarrows_sprite3
                    elif z%8==3:
                        target2=self.newarrows_sprite4
                elif x%4==1:
                    target=self.newarrows_sprite2
                    if z%8==0:
                        target2=self.newarrows_sprite1
                    elif z%8==2:
                        target2=self.newarrows_sprite3
                    elif z%8==3:
                        target2=self.newarrows_sprite4
                elif x%4==2:
                    target=self.newarrows_sprite3
                    if z%8==0:
                        target2=self.newarrows_sprite1
                    elif z%8==1:
                        target2=self.newarrows_sprite2
                    elif z%8==3:
                        target2=self.newarrows_sprite4
                elif x%4==3:
                    target=self.newarrows_sprite4
                    if z%8==0:
                        target2=self.newarrows_sprite1
                    elif z%8==1:
                        target2=self.newarrows_sprite2
                    elif z%8==2:
                        target2=self.newarrows_sprite3
                self.y = -2
                for sprite in target.sprites():
                    sprite.rect=sprite.rect.move(0,self.y)
                    self.top=sprite.rect.top
                target.draw(self.screen)
                if z%8<4 and z%8 != x%4:
                    for sprite in target2.sprites():
                        sprite.rect=sprite.rect.move(0,self.y)
                        self.top=sprite.rect.top
                    target2.draw(self.screen)
                sleep(delay)
                pygame.display.flip()
                target.clear(self.screen,self.background)
                if z%8<4 and z%8 != x%4:
                    target2.clear(self.screen,self.background)
                self.arrows_sprite1.draw(self.screen)
                self.arrows_sprite2.draw(self.screen)
                self.arrows_sprite3.draw(self.screen)
                self.arrows_sprite4.draw(self.screen)
                lstCols1 = pygame.sprite.groupcollide(self.arrows_sprite1, self.newarrows_sprite1,False,False)
                lstCols2 = pygame.sprite.groupcollide(self.arrows_sprite2,self.newarrows_sprite2,False,False)
                lstCols3 = pygame.sprite.groupcollide(self.arrows_sprite3,self.newarrows_sprite3,False,False)
                lstCols4 = pygame.sprite.groupcollide(self.arrows_sprite4,self.newarrows_sprite4,False,False)
                if self.top==-30:
                    self.screen.blit(text,textpos)
                    self.arrows.newarrows = self.arrows.newarrows - 1
                    missed +=1
                    self.screen.blit(self.background, (0, 0))
                    if pygame.font:
                        font = pygame.font.Font(None, 36)
                        text = font.render("Score: %s" % self.arrows.newarrows
                                            , 1, (255, 0, 0))
                        textpos = text.get_rect(centerx=self.background.get_width()/2)
                        self.screen.blit(text, textpos)
                for event in pygame.event.get():
                    if event.type==KEYDOWN:
                        if (event.key==K_DOWN and lstCols3):
                            self.screen.blit(text,textpos)
                            self.arrows.newarrows = self.arrows.newarrows + 5
                            self.screen.blit(self.background, (0, 0))
                            self.newarrows_sprite3.clear(self.screen,self.background)
                            for sprite in self.newarrows_sprite3.sprites():
                                sprite.rect.top=480
                            clear=True
                            if pygame.font:
                                font = pygame.font.Font(None, 36)
                                text = font.render("Score: %s" % self.arrows.newarrows
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                        if (event.key==K_RIGHT and lstCols4):
                            self.screen.blit(text,textpos)
                            self.arrows.newarrows = self.arrows.newarrows + 5
                            self.screen.blit(self.background, (0, 0))
                            self.newarrows_sprite4.clear(self.screen, self.background)
                            for sprite in self.newarrows_sprite4.sprites():
                                sprite.rect.top=480
                            clear=True
                            if pygame.font:
                                font = pygame.font.Font(None, 36)
                                text = font.render("Score: %s" % self.arrows.newarrows
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                        if (event.key==K_UP and lstCols2):
                            self.screen.blit(text,textpos)
                            self.arrows.newarrows = self.arrows.newarrows + 5
                            self.screen.blit(self.background, (0, 0))
                            self.newarrows_sprite2.clear(self.screen,self.background)
                            for sprite in self.newarrows_sprite2.sprites():
                                sprite.rect.top=480
                            clear=True
                            if pygame.font:
                                font = pygame.font.Font(None, 36)
                                text = font.render("Score: %s" % self.arrows.newarrows
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                        if (event.key==K_LEFT and lstCols1):
                            self.screen.blit(text,textpos)
                            self.arrows.newarrows = self.arrows.newarrows + 5
                            self.screen.blit(self.background, (0, 0))
                            self.newarrows_sprite1.clear(self.screen,self.background)
                            for sprite in self.newarrows_sprite1.sprites():
                                sprite.rect.top=480
                            clear=True
                            if pygame.font:
                                font = pygame.font.Font(None, 36)
                                text = font.render("Score: %s" % self.arrows.newarrows
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                        if (event.key==K_LEFT and not lstCols1) or (event.key==K_UP and not lstCols2) or (event.key==K_RIGHT and not lstCols4) or (event.key==K_DOWN and not lstCols3):
                            self.screen.blit(text,textpos)
                            self.arrows.newarrows = self.arrows.newarrows - 1
                            self.screen.blit(self.background, (0, 0))
                            if pygame.font:
                                font = pygame.font.Font(None, 36)
                                text = font.render("Score: %s" % self.arrows.newarrows
                                                    , 1, (255, 0, 0))
                                textpos = text.get_rect(centerx=self.background.get_width()/2)
                                self.screen.blit(text, textpos)
                        if event.key==K_ESCAPE:
                            sys.exit()
            if self.top<-30:
                for sprite in target.sprites():
                    sprite.rect.top=480
                if z%8<4 and z%8 != x%4:
                    for sprite in target2.sprites():
                        sprite.rect.top=480
    ##############loadingssprites#################################
    def LoadSprites(self):
        """Load the sprites that we need"""
        self.snake = Snake()
        self.snake_sprites = pygame.sprite.RenderPlain((self.snake))

        """figure out how many pellets we can display"""
        nNumHorizontal = int(self.width/64)
        nNumVertical = int(self.height/64)
        """Create the Pellet group"""
        self.pellet_sprites = pygame.sprite.Group()
        """Create all of the pellets and add them to the
        pellet_sprites group"""
        for x in range(nNumHorizontal):
            for y in range(nNumVertical):
                self.pellet_sprites.add(Pellet(pygame.Rect(x*64, y*64, 64, 64)))
        self.arrows = Arrows()
        self.arrows_sprite1 = pygame.sprite.Group()
        self.arrows_sprite1.add(Arrows(pygame.Rect(180,75,64,64),"arrow1.png"))
        self.arrows_sprite2 = pygame.sprite.Group()
        self.arrows_sprite2.add(Arrows(pygame.Rect(260, 75, 64, 64),"arrow2.png"))
        self.arrows_sprite3 = pygame.sprite.Group()
        self.arrows_sprite3.add(Arrows(pygame.Rect(340, 75, 64, 64),"arrow3.png"))
        self.arrows_sprite4 = pygame.sprite.Group()
        self.arrows_sprite4.add(Arrows(pygame.Rect(420, 75, 64, 64),"arrow4.png"))

        self.newArrows = newArrows()
        self.newarrows_sprite1 = pygame.sprite.Group()
        self.newarrows_sprite1.add(newArrows(pygame.Rect(180, 480, 64, 64),"arrow11.png"))
        self.newarrows_sprite2 = pygame.sprite.Group()
        self.newarrows_sprite2.add(newArrows(pygame.Rect(260, 480, 64, 64),"arrow22.png"))
        self.newarrows_sprite3 = pygame.sprite.Group()
        self.newarrows_sprite3.add(newArrows(pygame.Rect(340, 480, 64, 64),"arrow33.png"))
        self.newarrows_sprite4 = pygame.sprite.Group()
        self.newarrows_sprite4.add(newArrows(pygame.Rect(420, 480, 64, 64),"arrow44.png"))

    #############intro##############3
    def showIntro(self):
        # intro
        bg = pygame.image.load("data/images/intro.png")
        intropic1 = pygame.image.load("data/images/intro1.png")
        intropic2 = pygame.image.load("data/images/intro2.png")
        wrongdecisionforhelp = pygame.image.load("data/images/wrongdecisionforhelp.png")
        sweetkid = pygame.image.load("data/images/sweetkid.png")
        badkid = pygame.image.load("data/images/badkid.png")
        wrongdecisionforbadkid = pygame.image.load("data/images/wrongdecisionforbadkid.png")
        # watermelongame
        waterintro = pygame.image.load("data/images/watermelonintro.png")
        waterinstruct = pygame.image.load("data/images/watermeloninstruction.png")
        intro = True
        while intro == True:
            self.screen.blit(bg, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = False
        while intro == False:
            self.screen.blit(intropic1, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 1
        while intro == 1:
            self.screen.blit(intropic2, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 2
        while intro == 2:
            self.screen.blit(sweetkid, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_x):
                            print(intro)
                            intro = 0
                        if (event.key ==K_z):
                            print(intro)
                            intro = 3
        while intro == 0:
            self.screen.blit(wrongdecisionforhelp, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 3
        while intro == 3:
            self.screen.blit(badkid, (0, 0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_x):
                            print(intro)
                            intro = 5
                        if (event.key == K_z):
                            print(intro)
                            intro = 4
        while intro == 4:
            self.screen.blit(wrongdecisionforbadkid, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 5
        while intro == 5:
            self.screen.blit(waterintro, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 6
        while intro == 6:
            self.screen.blit(waterinstruct, (0,0))
            pygame.display.flip()
            for event in pygame.event.get():
                    if event.type == pygame.QUIT:
                        sys.exit()
                    elif event.type == KEYDOWN:
                        if (event.key == K_SPACE):
                            print(intro)
                            intro = 7


class Snake(pygame.sprite.Sprite):
    """This is our snake that will move around the screen"""

    def __init__(self):
        pygame.sprite.Sprite.__init__(self)
        self.image, self.rect = load_image('player_front.png',-1)
        self.pellets = 0
        """Set the number of Pixels to move each time"""
        self.x_dist = 14
        self.y_dist = 14
        self.image2, self.rect2 = load_image('player.side.png',-1)
        self.image3, self.rect3 = load_image('player.side.step.png',-1)
        self.image4, self.rect4 = load_image('player.side.2.png', -1)
        self.image5, self.rect5 = load_image('player.side.step2.png', -1)
        self.image6, self.rect6 = load_image('player.back.step1.png', -1)
        self.image7, self.rect7 = load_image('player.back.step2.png', -1)
        self.image8, self.rect8 = load_image('player.front.step1.png', -1)
        self.image9, self.rect9 = load_image('player.front.step2.png', -1)
    def move(self, key):
        """Move your self in one of the 4 directions according to key"""
        """Key is the pyGame define for either up,down,left, or right key
        we will adjust outselfs in that direction"""
        xMove = 0;
        yMove = 0;

        if (key == K_RIGHT):
            xMove = self.x_dist
            self.image = self.image2

        elif (key == K_LEFT):
            xMove = -self.x_dist
            self.image = self.image4
        elif (key == K_UP):
            yMove = -self.y_dist
            self.image = self.image7
        elif (key == K_DOWN):
            yMove = self.y_dist
            self.image = self.image8
        #self.rect = self.rect.move(xMove,yMove);
        self.rect.move_ip(xMove,yMove);

class Pellet(pygame.sprite.Sprite):

    def __init__(self, rect=None):
        pygame.sprite.Sprite.__init__(self)
        self.image, self.rect = load_image('watermelon.png',-1)
        if rect != None:
            self.rect = rect

class Arrows(pygame.sprite.Sprite):
    """This is our snake that will move around the screen"""

    def __init__(self,rect=None,img=None):
        pygame.sprite.Sprite.__init__(self)
        if img != None:
            self.image,self.rect = load_image(img, -1)
        if rect != None:
            self.rect = rect
        self.newarrows=0
class newArrows(pygame.sprite.Sprite):
    def __init__(self,rect=None,img=None):
        pygame.sprite.Sprite.__init__(self)
        if img != None:
            self.image,self.rect = load_image(img,-1)
        if rect != None:
            self.rect = rect


if __name__ == "__main__":
    MainWindow = PyManMain()
    MainWindow.MainLoop()

