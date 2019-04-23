# 消消乐记分小游戏GUI界面

### 文件结构规划
1. 定义config.py文件存储相关参数：包括界面的宽高，整个方格行列个数，总格数等等。
2. 定义utils.py文件用于存放基础的类和函数：包括整个消除拼图类，游戏类，拼图块移动函数，坐标设置与获取函数，开始游戏主函数，初始化随机生成拼图函数，时间倒计时展示函数，显示得分函数，加分函数，消除函数以及消除后新拼图块生成函数，拼图交换位置函数等等。
3. 定义main.py主函数：主要用于界面初始化开启游戏主程序

### 实现方法
1. config参数设置：
```
WIDTH = 600
HEIGHT = 600
NUMGRID = 8
GRIDSIZE = 64
XMARGIN = (WIDTH - GRIDSIZE * NUMGRID) // 2
YMARGIN = (HEIGHT - GRIDSIZE * NUMGRID) // 2
ROOTDIR = os.getcwd()
FPS = 30
```
2. utils类与函数设置
1） 导入库:time计时，random生成随机数，pygame跨平台Python模块主要用于游戏图形化界面生成以及音频播放，config自己定义的相关变量
```
import time
import random
import pygame
from config import *
```
2） 定义拼图类
```
class gemSprite(pygame.sprite.Sprite):
```
主要有函数：
+ 初始化函数：self=类具体化对象本身，img_path=图片文件所在路径，size=整个界面大小，position=拼图块位置，downlen=消除拼图块后下降格数
```
def __init__(self, img_path, size, position, downlen, **kwargs):
```
+ 移动函数：主要通过鼠标控制拼图块交换方向，有上下左右四个方向
```
def move(self):
```
+ 获取坐标函数:获取当前拼图块坐标，主要通过左（left）和上（top）两个方向定义坐标距离
```
def getPosition(self):
```
+ 设置坐标函数：设置拼图块坐标
```
def setPosition(self, position):
```
3) 定义游戏类：
```
class gemGame():
```
主要函数有：
+ 初始化函数：self=类具体化对象本身,screen=屏幕，sounds=音频，font=字体，gem_imgs=拼图块图片
```
def __init__(self, screen, sounds, font, gem_imgs, **kwargs):
```
+ 开始游戏函数：游戏开始主循环
```
def start(self):
```
+ 随机拼图块生成函数：消除后随机生成新的拼图模块
```
def reset(self):
```
+ 显示游戏倒计时时间函数：
```
def showRemainingTime(self):
```
+ 显示得分函数：
```
def drawScore(self):
```
+ 分数计算函数：
```
def drawAddScore(self, add_score):
```
+ 新拼图块生成函数：
```
def generateNewGems(self, res_match):
```
+ 消除匹配成功的拼图块：行或列三个一样的拼图块出现即消除
```
def removeMatched(self, res_match):
```
+ 界面网格绘制：
```
def drawGrids(self):
```
+ 画矩形框：
```
def drawBlock(self, block, color=(255, 0, 255), size=4):
```
+ 新的拼图块出现下落特效：
```
def dropGems(self, x, y):
```
+ 检查有无拼图块被选中：
```
def checkSelected(self, position):
```
+ 有无行列三个拼图块相同判断：
```
def isMatch(self):
```
+ 交换拼图函数：
```
def swapGem(self, gem1_pos, gem2_pos):
```
