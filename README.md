# notepad
from tkinter import *
import tkinter.messagebox as tmsg
from tkinter.filedialog import askopenfilename,asksaveasfilename
import os
import tkinter
def newb():
    global file
    root.title("My Notebook")
    file=None
    textbar.delete(1.0, END)

def openb():
    global file
    file=askopenfilename(defaultextension=".txt",filetypes=[("All files","*.*"),("Text Document","*.txt")])
    if file=="":
        file=None

    else:
        root.title(os.path.basename(file) + "-My notebook")
        textbar.delete(1.0,END)
        f=open(file,"r")
        textbar.insert(1.0,f.read())
        f.close()

def exitb():
    root.destroy()


def cutb():
    textbar.event_generate(("<<Cut>>"))
    
def copyb():
    textbar.event_generate(("<<Copy>>"))

def pasteb():
    textbar.event_generate(("<<Paste>>"))

def helpb():
    a=tmsg.showinfo("help....","I am gagan.\n How may i help you??")

root=Tk()
root.geometry("600x300")
root.title("notebook")

textbar=Text(root, font="arabic")
file=None
textbar.pack(expand= True, fill= "both")

def saveb():
    global file
    if file == None:
        file=asksaveasfilename(initialfile="untitled.txt",defaultextension=".txt",filetypes=[("All files","*.*"),("Text Document","*.txt")])
        if file==None:
            file=None
        else:
            f=open(file,"w")
            f.write(textbar.get(1.0,END))
            f.close()
            root.title(os.path.basename(file)+"-mynotebook")
    else:
        f=open(file,"w")
        f.write(textbar.get(1.0,END))
        f.close()


#menu
menubar=Menu(root)
#filebar
filebar=Menu(menubar, tearoff=0)
filebar.add_command(label="New",font="arial 10",command=newb)
filebar.add_command(label="open",font="arial 10",command=openb)
filebar.add_command(label="Save",font="arial 10",command=saveb)
filebar.add_separator()
filebar.add_command(label="Exit",font="arial 10",command=exitb)
root.config(menu=menubar)
menubar.add_cascade(label="File",font="arial",menu=filebar)

#editbar
editbar=Menu(menubar,tearoff=0)
editbar.add_command(label="Cut",font="arial 10",command=cutb)
editbar.add_separator()
editbar.add_command(label="Copy",font="arial 10",command=copyb)
editbar.add_separator()
editbar.add_command(label="Paste",font="arial 10",command=pasteb)
root.config(menu=menubar)
menubar.add_cascade(label="Edit",font="arial 10",menu=editbar)

#helpbar
helpbar=Menu(menubar, tearoff=0)
helpbar.add_command(label="About me",font="arial 10",command=helpb)
root.config(menu=menubar)
menubar.add_cascade(label="Help",font="arial 10", menu=helpbar)

#scrollbar
scroll=Scrollbar(textbar)
scroll.pack(side=RIGHT,fill=Y)
scroll.config(command=textbar.yview)
textbar.config(yscrollcommand=scroll.set)

root.mainloop()
