
## 21-11-10
### str转datetime.date
```python
   t = '2021-11-10'
   year, month, day = time.strptime(t, "%Y-%m-%d")[:3]
   t1 = datetime.date(year, month, day)
   print(t1)

##  2021-11-10

```

## 22-04-122
### 模拟鼠标点击
安装： pip install pywin32 或  pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pywin32
安装： pip install PyUserInput 或 pip install -i https://pypi.tuna.tsinghua.edu.cn/simple PyUserInput
from pymouse import PyMouse
x = PyMouse()
txt = x.position()  # 获取当前坐标的位置

x.move(50, 50)      # 鼠标移动到(x,y)位置
x.click(50, 50)     # 鼠标左击(x,y)
x.click(50, 50, 2)  # 鼠标右击(x,y)
