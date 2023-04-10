# Text-to-speech-using-Python
import tkinter as tk
import PyPDF2
import pyttsx3
from tkinter import *
#from tkinter import filedialog
from tkinter.filedialog import askopenfile
from tkinter import ttk
import pyttsx3
import os
from PIL import Image, ImageTk



'''def get_text():
    text=text_area.get(1.0,END)
    print(text)
    return text'''
    #pgno.config(text=text_area.get(1.0,END))
def select_pdf():
    file = askopenfile(parent=root,mode='rb',title="choose a file",filetype=[("Pdf file","*.pdf")])
    if file:
        read_pdf = PyPDF2.PdfFileReader(file)
        def get_text():
            text=text_area.get(1.0,END)
            print(text)
            return text
        a=get_text()
        page = read_pdf.getPage(a)
        page_content=page.extractText()
        print(page_content)
        
#c=select_pdf()




#objectcreation
speak = pyttsx3.init()

'''def play():
    speak.say()
    speak.runAndWait()'''
#b=play(c)

'''speak.getProperty('speak.Languages')
print(Languages)'''

#speedmodulation
def func2():
    speedmod=v2.get()
    if speedmod=="SLOW":
        speak.setProperty('rate',50)
    elif speedmod=="NORMAL":
        speak.setProperty('rate',200)
    elif speedmod=="FAST":
        speak.setProperty('rate',400)
    else :
        speak.setProperty('rate',200)

#volumevariation
def func3():
    volumevar=v3.get()
    if volumevar=="LOW":
        speak.setProperty("volume",0.1)
    elif volumevar=="MEDIUM":
        speak.setProperty("volume",0.5)
    elif volumevar=="HIGH":
        speak.setProperty("volume",1)
    else :
        speak.setProperty("volume",0.5)

#voices
voices = speak.getProperty('voices')
def func1():
    gender=v1.get()
    if gender =="MALE":
        speak.setProperty("voice",voices[0].id)
    elif gender =="FEMALE":
        speak.setProperty("voice",voices[1].id)
    else :
        speak.setProperty("voice",voices[0].id)

#SavingtoMp3
#speak.save_to_file(text, 'test.mp3')

# reading the text
#speak.say(page_content)
#speak.runAndWait()
        
    
root=Tk()
root.title("Text to speech")
root.geometry("1300x700")
root.maxsize(1300,700)
root.minsize(1300,700)
root.configure(bg="#A80000")
#logo
#root.wm_iconbitmap("logo_omkar.jpeg")
#Topframe
Top_frame=Frame(root,bg="white",width=1300,height=100)
Top_frame.place(x=0,y=0)

###
#text_area=Text(root,font="Robote 20",bg="white",relief=GROOVE,wrap=WORD)
#text_area.place(x=10,y=150,width=500,height=250)


#Topframe
'''Top_frame=Frame(root,bg="white",width=900,height=100)
Top_frame.place(x=0,y=0)'''

###
x=StringVar()
x.set("")
y=StringVar()
y.set("")
text_area=Entry(root,textvariable=x,font="Robote 20",bg="white",relief=GROOVE)
text_area.place(x=70,y=350)
error=Entry(root,textvariable=y,font="Robote 20",bg="white",relief=GROOVE)
error.place(x=70,y=450)

#Labeling
Label(root,text="GENDER",font="Lucida 15 bold",bg="#A80000",fg="cyan").place(x=590,y=160)
Label(root,text="SPEED",font="Lucida 15 bold",bg="#A80000",fg="cyan").place(x=800,y=160)
Label(root,text="VOLUME",font="Lucida 15 bold",bg="#A80000",fg="cyan").place(x=990,y=160)
Label(root,text="Enter Page Number",font="Lucida 15 bold",bg="#A80000",fg="cyan").place(x=115,y=300)
#buttons
select=Button(root,text="Select PDF",font="lucida 20 bold",fg="black",bg="yellow",command=select_pdf,width=13,height=2)
select.place(x=100,y=170)
play=Button(root,text="PLAY",width=10,height=2,fg="black",bg="lightgreen",relief=SUNKEN,font="lucida 25 bold")
play.place(x=600,y=400)
play=Button(root,text="SAVE",width=10,height=2,fg="black",bg="lightgreen",relief=SUNKEN,font="lucida 25 bold")
play.place(x=850,y=400)
play=Button(root,text="STOP",width=10,height=2,fg="black",bg="lightgreen",relief=SUNKEN,font="lucida 25 bold")
play.place(x=725,y=540)
#radiobuttonfunctions

#radiobuttons
v1=StringVar()
v1.set(1)
v2=StringVar()
v2.set(1)
v3=StringVar()
v3.set(1)
l1=["MALE","FEMALE"]
l2=["SLOW","NORMAL","FAST"]
l3=["LOW","MEDIUM","HIGH"]
for i in range(2):
    radio=Radiobutton(root,relief=SUNKEN,text=l1[i],variable=v1,value=l1[i],command=func1).place(x=600,y=200+30*i)
for i in range(3):
    radio=Radiobutton(root,relief=SUNKEN,text=l2[i],variable=v2,value=l2[i],command=func2).place(x=800,y=200+30*i)
for i in range(3):
    radio=Radiobutton(root,relief=SUNKEN,text=l3[i],variable=v3,value=l3[i],command=func3).place(x=1000,y=200+30*i)

root.mainloop()
