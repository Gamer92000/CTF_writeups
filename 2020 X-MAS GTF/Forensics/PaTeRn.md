# PaTeRn

![](PaTeRn.png)

Even though I was not able to solve this challenge in time I will still provide two possible ways to find the flag here.
Both technically work the same.

![](scramble.png)
*scramble.png*

## 1. The intended way

Apparently the background was purely random pixels (33% black).
However if you deleted every pixel but every 3rd per row and column you were left with this.

```python
from PIL import Image

pixelsize = 10

img = Image.open('scramble.png')

def process():
    nev = Image.new("RGB", (8880, 360), color=0)
    for j in range(8880 * 360):
        if int(j/pixelsize)%3 == 0 and int(int(j/8880)/pixelsize)%3 == 0:
            nev.putpixel((j%8880, int(j/8880)), img.getpixel((j%8880, int(j/8880))))
        else:
            nev.putpixel((j%8880, int(j/8880)), (255, 255, 255))
    nev.save('result.png')
            
process()
```
![](result.png)

If you clean this up you apparently get this:

![](flag.png)
*Milkdrops solution - at least he provided it*

## 2. My solution

My general idea was to shift the "linebreaks". This got me some trippy image sequences but not the solution.
After knowing the solution however I could simply make my script go to the correct solution by still just shifting linebreaks (both horizontally and vertically).
Before I could do so however I had to resize the scramble image to `888 x 36` px as each pixel was actually `10 x 10` pixels.

Afterwars I could simply run my updated script:
```python
from PIL import Image

def process(i):
    nev = Image.new("RGBA", (888 * 3, int(36/3)), color=0)
    for j in range(888 * 36):
        nev.putpixel((j%i, int(j/i)), img.getpixel((j%888, int(j/888))))
    nev.save("tmp.png")
    
def process2():
    nev = Image.new("RGBA", (888, 36), color=0)
    for j in range(888 * 36):
        nev.putpixel((int(j/36), j%36), img.getpixel((int(j/(36/3)), j%(36/3))))
    nev.save('solution.png')

img = Image.open('scramble.png')
process(888 * 3)
img = Image.open('tmp.png')
process2()
```

This gave me the following image:
![](solution.png)

### Flag: `X-MAS{Y0U_KNOW_HOW_7O_5OLV3_4_PUZZLE}`
