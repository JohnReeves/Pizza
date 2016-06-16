
```python
#import libraries
from Tkinter import *
from random import randint

# step 1: create the top level Tk object
window=Tk()
window.title("a window")
 
# step 2: create the canvas
canvas=Canvas(width=600, height=600)
 
# step 3: draw stuff on the canvas
def mushroom(xo,yo,d,angle):
    #from math import cos, sin
    from cmath import exp
    cangle = exp(angle*1j)
    canvas.create_arc(xo,yo,xo+d,yo+d,style="chord",
                      start=angle,extent=180,fill="darkgrey")

    x,y=xo+d/4, yo+d/2
    center=(xo+d/2,yo+d/2)
    points=[(x,y),(x+d/2,y),(x+d/2,y+d/2),(x,y+d/2)]
    poly=canvas.create_polygon(points,fill="blue")
    
    newxy=[]
    #offset = complex(center[0],center[1])
    offset = complex(x+d/4,y+d/2)
    for x1,y1 in points:
        v = cangle * (complex(x1, y1) - offset) + offset
        newxy.append(int(v.real))
        newxy.append(int(v.imag))
    canvas.coords(poly, *newxy)

for x in range(1):
    randX,randY= randint(0,400),randint(0,400)
    randAngle=randint(0,100)
    mushroom(randX,randY,200,randAngle)
 
canvas.pack()
window.mainloop()
```
