"""
學號:B0029058
姓名:林宏翰
作業編號:HW07
程式名稱:Sample Breakout Game
        Sample Python/Pygame Programs
        Simpson College Computer Science
        http://programarcadegames.com/
        http://simpson.edu/computer-science/
完成時間:0:30
""" 

# --- 匯入library

import math
import pygame as pg

啟動 = pg.init
結束 = pg.quit
動畫 = pg.sprite.Sprite
翻轉 = pg.display.flip
表面 = pg.Surface
取滑鼠位置 = pg.mouse.get_pos
顯示滑鼠 = pg.mouse.set_visible
設定螢幕 = pg.display.set_mode
# 定義顏色
黑 = (0, 0, 0)
白 = (255, 255, 255)
藍 = (0, 0, 255)

# 磚塊寬高
磚塊寬度 = 23
磚塊高度 = 15

class 磚塊(動畫):
    """此類別為每個磚塊會被球打掉
    繼承pygame中的spirte類別 """

    def __init__(自己, 顏色, 橫, 縱):
        """ 建構子. 傳入磚塊的顏色, 
            與橫、縱值. """
        
        # 呼叫父類別的建構子
        動畫.__init__(自己)
        
        # 創造適合大小的磚塊
        自己.image = 表面([磚塊寬度, 磚塊高度])
        
        # 磚塊上色
        自己.image.fill(顏色)
        
        # 使用磚塊影像
        自己.rect = 自己.image.get_rect()
        
        # 擺放磚塊的位置
        自己.rect.x = 橫
        自己.rect.y = 縱


class 球(動畫):
    """ 此類別為球        
        繼承pygame中的spirte類別 """
    
    # 每週期所顯示的畫素
    速度 = 10.0
    
    # 球的浮點數位置
    x = 0.0
    y = 180.0
    
    # 球的方向(角度)
    direction = 200

    width = 10
    height = 10
    
    # 建構子.傳入磚塊顏色與橫縱軸
    def __init__(自己):
        # 呼叫父類別
        動畫.__init__(自己)
        
        # 創造球
        自己.image = 表面([自己.width, 自己.height])
        
        # 球上色
        自己.image.fill(白)
        
        # 創造長方形物件
        自己.rect = 自己.image.get_rect()
        
        # 得到螢幕大小的屬性
        自己.screenheight = pg.display.get_surface().get_height()
        自己.screenwidth = pg.display.get_surface().get_width()
    
    def 彈跳(自己, 差距):
        """ 此函式為球的彈跳 
            在水平的邊上"""
        
        自己.direction = (180 - 自己.direction) % 360
        自己.direction -= 差距
    
    def 更新(自己):
        """ 更新球的位置"""
        # 轉換三角函數到弧度
        direction_radians = math.radians(自己.direction)
        
        # 根據速度和方向改變座標值
        自己.x += 自己.速度 * math.sin(direction_radians)
        自己.y -= 自己.速度 * math.cos(direction_radians)
        
        # 把圖像移到目前的座標值上
        自己.rect.x = 自己.x
        自己.rect.y = 自己.y
        
        # 是否在螢幕上限
        if 自己.y <= 0:
            自己.彈掉(0)
            自己.y = 1
            
        # 是否在螢幕左框
        if 自己.x <= 0:
            自己.direction = (360 - 自己.direction) % 360
            自己.x = 1
            
        # 是否在螢幕右框
        if 自己.x > 自己.screenwidth - 自己.width:
            自己.direction = (360 - 自己.direction) % 360
            自己.x = 自己.screenwidth - 自己.width - 1
        
        # 是否在螢幕下限
        if 自己.y > 600:
            return True
        else:
            return False

class 玩家(動畫):
    """ 此類別為橫桿 """
    
    def __init__(自己):
        """ 玩家的建構子 """
        # 呼叫父類別的建構子
        動畫.__init__(自己)
        
        自己.width = 75
        自己.height = 15
        自己.image = 表面([自己.width, 自己.height])
        自己.image.fill((白))
        
        # 左上小為球的起點
        自己.rect = 自己.image.get_rect()
        自己.screenheight = pg.display.get_surface().get_height()
        自己.screenwidth = pg.display.get_surface().get_width()

        自己.rect.x = 0
        自己.rect.y = 自己.screenheight-自己.height
    
    def 更新(自己):
        """ 更新玩家位置 """
        # 取得滑鼠位置
        位置 = 取滑鼠位置()
        # Set the left side of the player bar to the mouse position
        自己.rect.x = 位置[0]
        # Make sure we don't push the player paddle 
        # off the right side of the screen
        if 自己.rect.x > 自己.screenwidth - 自己.width:
            自己.rect.x = 自己.screenwidth - 自己.width

# Call this function so the Pygame library can initialize itself
啟動()

# Create an 800x600 sized screen
螢幕 = pg.display.set_mode([800, 600])

# Set the title of the window
pg.display.set_caption('Breakout')

# Enable this to make the mouse disappear when over our window
顯示滑鼠(0)

# This is a font we use to draw text on the screen (size 36)
font = pg.font.Font(None, 36)

# Create a surface we can draw on
background = pg.Surface(螢幕.get_size())

# Create sprite lists
磚塊團體 = pg.sprite.Group()
球團體 = pg.sprite.Group()
allsprites = pg.sprite.Group()

# Create the player paddle object
個體玩家 = 玩家()
allsprites.add(個體玩家)

# Create the ball
個體球 = 球()
allsprites.add(個體球)
球團體.add(個體球)

# The top of the block (y position)
top = 80

# Number of blocks to create
blockcount = 32

# --- Create blocks

# Five rows of blocks
for row in range(5):
    # 32 columns of blocks
    for column in range(0, blockcount):
        # Create a block (color,x,y)
        磚塊個體 = 磚塊(藍, column * (磚塊寬度 + 2) + 1, top)
        磚塊團體.add(磚塊個體)
        allsprites.add(磚塊個體)
    # Move the top of the next row down
    top += 磚塊高度 + 2

# Clock to limit speed
clock = pg.time.Clock()

# 遊戲是否失敗?
GG = False

# Exit the program?
跳出程式 = False

# Main program loop
while 跳出程式 != True:

    # Limit to 30 fps
    clock.tick(30)

    # Clear the screen
    螢幕.fill(黑)
    
    # Process the events in the game
    for event in pg.event.get():
        if event.type == pg.QUIT:
            跳出程式 = True
    
    # Update the ball and player position as long
    # as the game is not over.
    if not GG:
        # Update the player and ball positions
        個體玩家.更新()
        GG = 個體球.更新()
    
    # If we are done, print game over
    if GG:
        文字 = font.render("Game Over", True, 白)
        文字位置 = 文字.get_rect(centerx=background.get_width()/2)
        文字位置.top = 300
        螢幕.blit(文字, 文字位置)
    
    # See if the ball hits the player paddle
    if pg.sprite.spritecollide(個體玩家, 球團體, False):
        # The 'diff' lets you try to bounce the ball left or right 
        # depending where on the paddle you hit it
        差距 = (個體玩家.rect.x + 個體玩家.width/2) - (個體球.rect.x+個體球.width/2)
        
        # Set the ball's y position in case 
        # we hit the ball on the edge of the paddle
        個體球.rect.y = 螢幕.get_height() - 個體玩家.rect.height - 個體球.rect.height - 1
        個體球.彈跳(差距)
    
    # Check for collisions between the ball and the blocks
    壞磚 = pg.sprite.spritecollide(個體球, 磚塊團體, True)
    
    # If we actually hit a block, bounce the ball
    if len(壞磚) > 0:
        個體球.彈跳(0)
        
        # Game ends if all the blocks are gone
        if len(磚塊團體) == 0:
            GG = True
    
    # Draw Everything
    allsprites.draw(螢幕)

    # Flip the screen and show what we've drawn
    翻轉()

結束()


