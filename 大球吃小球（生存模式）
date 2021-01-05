from  math import sqrt
from  random import randint

import pygame
import sys

class Color():
    #颜色
    RED = (255, 0, 0)
    GREEN = (0, 255, 0)
    BLUE = (0, 0, 255)
    BLACK = (0, 0, 0)
    WHITE = (255, 255, 255)
    GRAY = (242, 242, 242)

    #随机获得颜色
    def random_color():
        r=randint(0,255)
        g=randint(0,255)
        b=randint(0,255)
        return (r,g,b)

class Ball(object):
    def __init__(self,x,y,radius,sx,sy,color=Color.RED):
        #初始化小球的状态
        self.x=x
        self.y=y
        self.radius=radius
        self.sx=sx
        self.sy=sy
        self.color=color
        self.color=color
        self.alive=True

    def move(self,screen):
        self.x+=self.sx
        self.y+=self.sy
        if self.x-self.radius<=0 or self.x+self.radius>=screen.get_width():
            self.sx=-self.sx
        if self.y-self.radius<=0 or self.y+self.radius>=screen.get_height():
            self.sy=-self.sy

    def movekey(self, xx,yy):
        self.x=xx
        self.y=yy

    def eat(self,other):
        #吃球
        if self.alive and other.alive and self !=other:
            dx, dy = self.x - other.x, self.y - other.y
            distance = sqrt(dx ** 2 + dy ** 2)
            if distance < self.radius + other.radius and self.radius > other.radius:
                other.alive = False
                #self.radius = self.radius + int(other.radius * 0.14)
                self.radius+=0.3
                return True

    # 两个小球接触时，发生弹性碰撞
    def impact(self, other):
        # 计算现在的距离
        dx = self.x - other.x
        dy = self.y - other.y
        ds = sqrt(dx ** 2 + dy ** 2)
        # 计算未来的距离
        dxx = dx + self.sx - other.sx
        dyy = dy + self.sy - other.sy
        dss = sqrt(dxx ** 2 + dyy ** 2)
        if self.radius + other.radius >= ds and self != other and dss <= ds:
            ssx, ssy, osx, osy = self.sx, self.sy, other.sx, other.sy
            self.sx = ((self.radius - other.radius) * ssx + 2 * other.radius * osx) / (self.radius + other.radius)
            self.sy = ((self.radius - other.radius) * ssy + 2 * other.radius * osy) / (self.radius + other.radius)
            other.sx = ((other.radius - self.radius) * other.sx + 2 * self.radius * ssx) / (self.radius + other.radius)
            other.sy = ((other.radius - self.radius) * other.sy + 2 * self.radius * ssy) / (self.radius + other.radius)
            # 防止self和other反转带来的重复运算
            other.alive = False

    def draw(self, screen):
        """在窗口上绘制球"""
        pygame.draw.circle(screen, self.color,(self.x, self.y), self.radius, 0)

def createMap(screen):
    #创建背景颜色
    screen.fill((82, 133, 133))

    #显示得分
    #设置字体和字号
    fontObj=pygame.font.Font('freesansbold.ttf',16)
    #设置得分文字具体内容
    textSurfaceObj=fontObj.render('Score: '+str(score),True,Color.RED,Color.GRAY)
    #文字所属框的内容型为长方形
    textRectObj=textSurfaceObj.get_rect()
    #设置文字中心的坐标
    textRectObj.center=(screen.get_width()-40,20)
    #显示在屏幕上
    screen.blit(textSurfaceObj,textRectObj)

def Result(screen,sound):
    # 设置字体和字号
    fontObj = pygame.font.Font('freesansbold.ttf', 60)
    # 设置得分文字具体内容
    textSurfaceObj = fontObj.render('Congratulations!', True, Color.RED, Color.GRAY)
    # 文字所属框的内容型为长方形
    textRectObj = textSurfaceObj.get_rect()
    # 设置文字中心的坐标
    textRectObj.center = (screen.get_width()/2, screen.get_height()/2)
    # 显示在屏幕上
    screen.blit(textSurfaceObj, textRectObj)
    text='Contact author to receive award'
    news(screen, 20, Color.RED, Color.GRAY, screen.get_width() / 2, screen.get_height() / 2+60, text)
    text1 = 'Email:962701025@qq.com'
    news(screen, 20, Color.RED, Color.GRAY, screen.get_width() / 2, screen.get_height() / 2 + 80, text1)
    # 胜利的音效
    sound_victory = pygame.mixer.Sound("music/victory.wav")
    if sound == 0:
        sound_victory.play()


def ResultOver(screen,sound):
    # 设置字体和字号
    fontObj = pygame.font.Font('freesansbold.ttf', 60)
    # 设置得分文字具体内容
    textSurfaceObj = fontObj.render('GAME OVER!', True, Color.RED, Color.GRAY)
    # 文字所属框的内容型为长方形
    textRectObj = textSurfaceObj.get_rect()
    # 设置文字中心的坐标
    textRectObj.center = (screen.get_width()/2, screen.get_height()/2)
    # 显示在屏幕上
    screen.blit(textSurfaceObj, textRectObj)
    text1= "Click the mouse to get a new life"
    news(screen, 25, Color.RED, Color.GRAY, screen.get_width() / 2, screen.get_height() / 2 +60, text1)
    # 失败的音效
    sound_gameover = pygame.mixer.Sound("music/gameover.wav")
    if sound==0:
        sound_gameover.play()

def Level(screen,sound1):
    level=score//10+1
    # 设置字体和字号
    fontObj = pygame.font.Font('freesansbold.ttf', 16)
    # 设置得分文字具体内容
    textSurfaceObj = fontObj.render('Level: '+str(level), True, Color.RED, Color.GRAY)
    # 文字所属框的内容型为长方形
    textRectObj = textSurfaceObj.get_rect()
    # 设置文字中心的坐标
    textRectObj.center = (50, 20)
    # 显示在屏幕上
    screen.blit(textSurfaceObj, textRectObj)
    if score%10==0 and score!=0:
        fontObj1 = pygame.font.Font('freesansbold.ttf', 30)
        textSurfaceObj1 = fontObj.render('Pass Level   '+str(level), True, Color.RED, Color.GRAY)
        textRectObj1 = textSurfaceObj1.get_rect()
        textRectObj1.center = (screen.get_width()/2, screen.get_height()/2-50)
        screen.blit(textSurfaceObj1, textRectObj1)

    if score%10==0 and score!=0 and sound1 == 0:
        # 升级的音效
        sound_upgrade = pygame.mixer.Sound("music/upgrade.wav")
        sound_upgrade.play()

def Instructions(screen):
    size=30
    size1=25
    text1="Instructions"
    text2="1.Click the mouse to start the game"
    text3="2.Move the mouse to avoid or eat the ball"
    text4="3.Be careful of being eaten by other big balls"
    news(screen, size, Color.RED, Color.GRAY, screen.get_width()/2-150, screen.get_height()/2-100, text1)
    news(screen, size1, Color.RED, Color.GRAY, screen.get_width() / 2-60, screen.get_height() / 2-60, text2)
    news(screen, size1, Color.RED, Color.GRAY, screen.get_width() / 2-26, screen.get_height() / 2-35, text3)
    news(screen, size1, Color.RED, Color.GRAY, screen.get_width() / 2, screen.get_height() / 2-10, text4)

def news(screen,size,fcolor,bcolor,x,y,text):
    # 显示得分
    # 设置字体和字号
    fontObj = pygame.font.Font('freesansbold.ttf', size)
    # 设置得分文字具体内容
    textSurfaceObj = fontObj.render(text, True, fcolor, bcolor)
    # 文字所属框的内容型为长方形
    textRectObj = textSurfaceObj.get_rect()
    # 设置文字中心的坐标
    textRectObj.center = (x, y)
    # 显示在屏幕上
    screen.blit(textSurfaceObj, textRectObj)


def main():
    #设置存放NPC小球容器
    balls = []
    #设置存放玩家小球的容器
    ballkey=[]
    #屏幕刷新频率设置
    ping=int(20)
    #出球频率设置，屏幕刷新30次出一个小球
    rate=35
    #定义得分参数
    global score
    score=int(0)
    pygame.init()
    # 初始化用于显示的窗口并设置窗口尺寸
    screen = pygame.display.set_mode((800, 600))
    # 设置当前窗口的标题
    pygame.display.set_caption('大球吃小球_成长模式v1.42 by NepoGod')
    #设置背景音乐
    pygame.mixer.music.load("music/bgm.wav")
    pygame.mixer.music.play(-1)
    pygame.mixer.music.set_volume(0.3)
    #设置个变量，只让胜利、失败、升级音播放一遍
    sound,sound1=int(0),int(0)

    running = True
    #开启一个事件循环处理发生的事件
    #设置关卡
    level,time,newlife=0,0,0
    while running:
        # 从消息队列中获取事件并对事件进行处理
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
                sys.exit()
            #处理鼠标事件的代码

            if event.type == pygame.MOUSEBUTTONDOWN and event.button == 1 and level==0:
                # 获得点击鼠标的位置
                x, y = event.pos
                radius = 10
                color = Color.random_color()
                #点击鼠标，产生一个初始小球，玩家使用小球完成游戏
                ball = Ball(x, y, radius, 0, 0, color)
                ballkey.append(ball)
                level=1
                score=0

            if event.type == pygame.MOUSEBUTTONDOWN and event.button == 1 and newlife==1:
                # 获得点击鼠标的位置
                x, y = event.pos
                radius = 10
                color = Color.random_color()
                #点击鼠标，产生一个初始小球，玩家使用小球完成游戏
                ball = Ball(x, y, radius, 0, 0, color)
                ballkey[0]=ball
                ballkey[0].alive=True
                level, time, newlife ,score,sound= 1, 0, 0,0,0


            if ballkey:
                if level>=1 and ballkey[0].alive:
                    x, y = pygame.mouse.get_pos()
                    ballkey[0].movekey(x,y)

        if score>=10 and score<20:
            rate,level=30,2
        elif score>=20 and score<30:
            rate,level = 25,3
        elif score >= 30 and score < 40:
            rate,level = 20,4
        elif score >= 40 and score < 50:
            rate,level = 17,5
        elif score >= 50 and score < 60:
            rate,level = 13,6
        elif score >= 60:
            rate,level = 10,7


        if level>=1 and time%rate==0:
            x, y = randint(100, 700), randint(100, 500)
            sx, sy = randint(-10, 10), randint(-10, 10)
            color = Color.random_color()
            radius = randint(3*level+2, 3*level+12)
            # 在点击鼠标的位置创建一个球(大小、速度和颜色随机)
            ball = Ball(x, y, radius, sx, sy, color)
            # 将球添加到列表容器中
            balls.append(ball)

        if ballkey:
            if ballkey[0].alive:
                for ball in balls:
                    if ballkey[0].eat(ball):
                        score+=1
                        # 吃球的音效
                        sound_eat = pygame.mixer.Sound("music/eat.wav")
                        sound_eat.play()

                    ball.eat(ballkey[0])

        #产生地图界面
        createMap(screen)
        #游戏说明文件
        if level==0:
            Instructions(screen)

        #显示玩家小球
        for ball in ballkey:
            if ball.alive:
                ball.draw(screen)
            else:
                ResultOver(screen, sound)
                sound,level,newlife=1,1,1

        #如果玩家还活着，显示其他还存活的NPC小球，如果玩家死亡，全部NPC清零
        if ballkey:
            if ballkey[0].alive:
                for ball in balls:
                    if ball.alive:
                        ball.draw(screen)
                    else:
                        balls.remove(ball)
            else:
                for ball in balls:
                    balls.remove(ball)


        #获胜条件
        if score>=100:
            Result(screen,sound)
            sound=1

        #通关信息
        Level(screen,sound1)
        #只让升级音乐响一次
        if score%10==0 and score!=0:
            sound1=1
        else:
            sound1=0

        pygame.display.flip()

        # 每隔50毫秒就改变球的位置再刷新窗口
        pygame.time.delay(int(1000/ping))
        time+=1

        for ball in balls:
            ball.move(screen)
            # 检查球有没有吃到其他的球
            for other in balls:
                ball.impact(other)

        for ball in balls:
            ball.alive=True


if __name__ == '__main__':
    main()
