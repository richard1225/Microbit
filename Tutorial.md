# Hello World
```
    from microbit import *
    display.scroll("Hello, World!")
```
`microbit` 是一个模块(modules)，`display` 是 `microbit` 模块里面的一个类(Class)，这个类里面有我们要的滚屏功能 `scroll`
> modules存在的原因：在操作一台树莓派时，其实这中间有很多繁琐的步骤要去做，但是前人替我们写好了这些操作步骤的代码，并包装成一个模块，我们只需要引用他们做好的模块， 就能轻松地操作树莓派。

> 类： 当我们有很多种功能的时候，为了更方便我们分类这些功能，我们会把他们分成很多类，用不同的类装着分好类的功能, richard.coding()

# Image

## DIY Images
```
from microbit import *

boat = Image("05050:"
             "05050:"
             "05050:"
             "99999:"
             "09990")

display.show(boat)
```
用数字0到9表示每个led灯的强度，0表示off， 9表示最亮
## 系统自带的图案
```
Image.HEART
Image.HEART_SMALL
Image.HAPPY
Image.SMILE
Image.SAD
Image.CONFUSED
Image.ANGRY
Image.ASLEEP
Image.SURPRISED
Image.SILLY
Image.FABULOUS
Image.MEH
Image.YES
Image.NO
...
```

## 动画
```
from microbit import *

boat1 = Image("05050:"
              "05050:"
              "05050:"
              "99999:"
              "09990")

boat2 = Image("00000:"
              "05050:"
              "05050:"
              "05050:"
              "99999")

boat3 = Image("00000:"
              "00000:"
              "05050:"
              "05050:"
              "05050")

boat4 = Image("00000:"
              "00000:"
              "00000:"
              "05050:"
              "05050")

boat5 = Image("00000:"
              "00000:"
              "00000:"
              "00000:"
              "05050")

boat6 = Image("00000:"
              "00000:"
              "00000:"
              "00000:"
              "00000")

all_boats = [boat1, boat2, boat3, boat4, boat5, boat6]
display.show(all_boats, delay=200)
```

# Buttons
```
from microbit import *

sleep(10000)
display.scroll(str(button_a.get_presses()))
```

# While
```
from microbit import *

while running_time() < 10000:
    display.show(Image.ASLEEP)

display.show(Image.SURPRISED)
```

# 处理按键事件
```
from microbit import *

while True:
    if button_a.is_pressed():
        display.show(Image.HAPPY)
    elif button_b.is_pressed():
        break
    else:
        display.show(Image.SAD)

display.clear()
```
## 逻辑操作符
`and` `or` `not`

# Pin针脚
```
from microbit import *

while True:
    if pin0.is_touched():
        display.show(Image.HAPPY)
    else:
        display.show(Image.SAD)
```
> With one hand, hold your device by the GND pin. Then, with your other hand, touch (or tickle) the 0 (zero) pin. You should see the display change from grumpy to happy!

## 蜂鸣器
The wire from pin 0 should be attached to the positive connector on the buzzer and the wire from GND to the negative connector.
>引脚0的导线应连接到蜂鸣器上的正极连接器，针脚GND导线连接到蜂鸣器上的负极连接器。
```
# 让蜂鸣器响一下
from microbit import *

pin0.write_digital(1)
```

```
# 让蜂鸣器每500毫秒响一下
from microbit import *

while True:
    pin0.write_digital(1) # on
    sleep(20)
    pin0.write_digital(0) # off
    sleep(480)
```
# Music
Use crocodile clips to attach pin 0 and GND to the positive and negative inputs on the speaker - it doesn’t matter which way round they are connected to the speaker.
>使用鳄鱼夹将引脚0和GND连接到扬声器的正负输入端 - 它们连接到扬声器的方向无关紧要。
```
import music

music.play(music.NYAN)
```
```
music.DADADADUM
music.ENTERTAINER
music.PRELUDE
music.ODE
music.NYAN
music.RINGTONE
music.FUNK
... 
```

## DIY Music
```
import music

tune = ["C4:4", "D4:4", "E4:4", "C4:4", "C4:4", "D4:4", "E4:4", "C4:4",
        "E4:4", "F4:4", "G4:8", "E4:4", "F4:4", "G4:8"]
music.play(tune)
```
> たとえば 、"A1:4" は音階名が A 、オクターブが 1 、持続時間が 4 である音符を指します。

> ["TO:D"], T: tune, O: octave, D: duration
### 简略版DIY Music
下一个音可以沿用上一个音的octave和持续时间，如["C4:4", "D4:4"] 可以简写为["C4:4", "D"]

以上tune数组可以改写为
```
import music

tune = ["C4:4", "D", "E", "C", "C", "D", "E", "C", "E", "F", "G:8",
        "E:4", "F", "G:8"]
music.play(tune)
```

## 制作声音特效
Eg.警笛声
```
import music

while True:
    for freq in range(880, 1760, 16):
        music.pitch(freq, 6)    # pitch(频率，时长(ms))
    for freq in range(1760, 880, -16):
        music.pitch(freq, 6)
```

# 加速度传感器
```
from microbit import *
import music

while True:
    music.pitch(accelerometer.get_y(), 10)
```

## magic-box
```
from microbit import *
import random

answers = [
    "It is certain",
    "It is decidedly so",
    "Without a doubt",
    "Yes, definitely",
    "You may rely on it",
    "As I see it, yes",
    "Most likely",
    "Outlook good",
    "Yes",
    "Signs point to yes",
    "Reply hazy try again",
    "Ask again later",
    "Better not tell you now",
    "Cannot predict now",
    "Concentrate and ask again",
    "Don't count on it"
    "My reply is no",
    "My sources say no",
    "Outlook not so good",
    "Very doubtful",
]

while True:
    display.show("8")
    if accelerometer.was_gesture("shake"):
        display.clear()
        sleep(1000)
        display.scroll(random.choice(answers))
```

## 指南针
```
from microbit import *

compass.calibrate() # 校正指南针
# 要校准指南针，请像校正iPhone指南针一样倾斜Microbit，直到在显示器的外边缘上绘制一圈像素。

while True:
    needle = ((15 - compass.heading()) // 30) % 12
    display.show(Image.ALL_CLOCKS[needle])
```

# game 思路：
1. 看谁按的快（Button + 蜂鸣器）
2. 摇骰子（random随机数）
3. 对讲机（2.4Ghz无线模块 ）
4. 温度计

# 文件系统
## size: 30k
## tool: pip3 install microfs
> docs: https://microfs.readthedocs.io/en/latest/
## main.py
除了使用Flash `hex`文件的方式让microbit执行脚本。 还可以直接放入main.py, 开机就会执行main.py。此方法还支持模板module
```
from microbit import display
from hello import say_hello

display.scroll(say_hello())
```