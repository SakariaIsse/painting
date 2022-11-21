# paint

>This was my final project for conclude the CS50 Introduction to Computer Sciense course.

>python, CS50


# Demonstration on youtube:

[Painting Video](https://youtu.be/PW7EHAiQ0Qg)

## Description

**painting Application Using Python**

My final project is a app that allow the user to paint what arts that he want to draw easily,
The user can also change your color and choosen any color he just clicking the color, 
you can erase any wrong arts you want to erase easily.
it can save your computer the drawing of your arts you drawed,
and choosen the your background color that you like for painting.
you can increase or decrease the size of your painting pen and chosen what size the you want


### importing all the necessary Libraries.

```python
from tkinter import *
from tkinter.ttk import Scale
from tkinter import colorchooser,filedialog,messagebox
import PIL.ImageGrab as ImageGrab
```

### Defining Class and constructor of the Program.

```python
class Draw():
    def __init__(self,root):
```

### Defining title and Size of the Tkinter Window GUI.

```python
  self.root =root
  self.root.title("Copy Assignment Painter")
  self.root.configure(background="white")
```

### variables for pointer and Eraser.

```python
self.pointer= "black"
self.erase="white"
```
# Widgets for Tkinter Window
    
### Configure the alignment , font size and color of the text.

```python
text=Text(root)
text.tag_configure("tag_name", justify='center', font=('arial',25),background='#292826',foreground='orange')
```

### Insert a Text.

```python
text.insert("1.0", "Drawing Application in Python")
```

### Add the tag for following given text.

```python
text.tag_add("tag_name", "1.0", "end")
text.pack()
```

### Pick a color for drawing from color pannel.

```python
self.pick_color = LabelFrame(self.root,text='Colors',font =('arial',15),bd=5,relief=RIDGE,bg="white")
self.pick_color.place(x=0,y=40,width=90,height=185)

colors = ['blue','red','green', 'orange','violet','black','yellow','purple','pink','gold','brown','indigo']
i=j=0
for color in colors:
    Button(self.pick_color,bg=color,bd=2,relief=RIDGE,width=3,command=lambda col=color:self.select_color(col)).grid(row=i,column=j)
    +=1
    if i==6:
       i=0
       j=1
```

### Erase Button and its properties.  

```python
self.eraser_btn= Button(self.root,text="Eraser",bd=4,bg='white',command=self.eraser,width=9,relief=RIDGE)
self.eraser_btn.place(x=0,y=197)
```
   
### Reset Button to clear the entire screen.

```python
self.clear_screen= Button(self.root,text="Clear Screen",bd=4,bg='white',command= lambda : self.background.delete('all'),width=9,relief=RIDGE)
self.clear_screen.place(x=0,y=227)
```

### Save Button for saving the image in local computer.

```python
self.save_btn= Button(self.root,text="ScreenShot",bd=4,bg='white',command=self.save_drawing,width=9,relief=RIDGE)
self.save_btn.place(x=0,y=257)
```

### Background Button for choosing color of the Canvas.

```python
self.bg_btn= Button(self.root,text="Background",bd=4,bg='white',command=self.canvas_color,width=9,relief=RIDGE)
self.bg_btn.place(x=0,y=287)
```

### Creating a Scale for pointer and eraser size.

```python
self.pointer_frame= LabelFrame(self.root,text='size',bd=5,bg='white',font=('arial',15,'bold'),relief=RIDGE)
self.pointer_frame.place(x=0,y=320,height=200,width=70)
self.pointer_size =Scale(self.pointer_frame,orient=VERTICAL,from_ =48 , to =0, length=168)
self.pointer_size.set(1)
self.pointer_size.grid(row=0,column=1,padx=15)
```

### Defining a background color for the Canvas.

```python
self.background = Canvas(self.root,bg='white',bd=5,relief=GROOVE,height=470,width=680)
self.background.place(x=80,y=40)
```
     
### Bind the background Canvas with mouse click.

```python
self.background.bind("<B1-Motion>",self.paint)
```

# Functions are defined here.

## Paint Function for Drawing the lines on Canvas.

```python
def paint(self,event):       
    x1,y1 = (event.x-2), (event.y-2)  
    x2,y2 = (event.x+2), (event.y+2)  
    self.background.create_oval(x1,y1,x2,y2,fill=self.pointer,outline=self.pointer,width=self.pointer_size.get())
```

### Function for choosing the color of pointer.

```python
def select_color(self,col):
    self.pointer = col
```

### Function for defining the eraser.
```python
def eraser(self):
    self.pointer= self.erase
```

### Function for choosing the background color of the Canvas.  

```python
def canvas_color(self):
    color=colorchooser.askcolor()
    self.background.configure(background=color[1])
    self.erase= color[1]
```

### Function for saving the image file in Local Computer.
```python
 def save_drawing(self):
        try:
            # self.background update()
            file_ss =filedialog.asksaveasfilename(defaultextension='jpg')
            #print(file_ss)
            x=self.root.winfo_rootx() + self.background.winfo_x()
            #print(x, self.background.winfo_x())
            y=self.root.winfo_rooty() + self.background.winfo_y()
            #print(y)

            x1= x + self.background.winfo_width() 
            #print(x1)
            y1= y + self.background.winfo_height()
            #print(y1)
            ImageGrab.grab().crop((x , y, x1, y1)).save(file_ss)
            messagebox.showinfo('Screenshot Successfully Saved as' + str(file_ss))

        except:
            print("Error in saving the screenshot")
            
if __name__ =="__main__":
    root = Tk()
    p= Draw(root)
    root.mainloop()
```

## Running the application
```

$ python paint.py
```
## Prerequisites

[Python](https://www.python.org/)

[Tkinter](https://docs.python.org/3/library/tkinter.html)
