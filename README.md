# mini-project
from tkinter import *
from tkinter import ttk
import tkinter.messagebox
import csv
import tkinter.scrolledtext as tkst
import matplotlib.pyplot as plt

def fetch_names():
    x=variable.get()
    loc='Baby Names 1944-2013//'+x
    loc=loc+'_cy'+y_e.get()+'_top.csv'
    file=open(loc,'r')
    j=0
    a='\nLIST OF TOP '
    a=a+(s_e.get()).upper()+' '+x.upper()+' NAMES IN THE YEAR '+y_e.get()+'\n\n'
    list_fetch.insert(INSERT,a)
    for i in file:
        if j==0:
            j=j+1
            continue
        elif j<=int(s_e.get()):
            j=j+1
            x=i.split(',')
            x1=x[0]
            x2=x[1]
            x1=x1.split('"')[1]
            x2=x2.split('"')[1]
            z=str(j-1)+'   '+x1+'   '+x2+'   '+'\n'
            list_fetch.insert(INSERT,z)
        else:
            break
    file.close()
def extract():
    cl=0
    cl2=0
    
    if y_e.get()=='':
        messagebox.showinfo(message='enter a year')
    elif int(y_e.get())<1944 and (y_e.get()>2013):
        messagebox.showinfo(message='year record not present')
    else:
        cl=1
        
    if s_e.get()=='':
        messagebox.showinfo(message='enter the number of names in show')
    else:
        cl2=1

    if cl==1 and cl2==1:
        fetch_names()
def plot():
    x=variable.get()
    loc='Baby Names 1944-2013//'+x
    y=int(y_e.get())
    j=0
    year=[] 
    amount=[]
    while y<=2013:
        year.append(y)
        loc2=loc+'_cy'+str(y)+'_top.csv'
        file=open(loc2,'r')
        file_read=csv.reader(file)
        count=0
        for i in file_read:
            if i[0]==n_e.get().upper():
                count=1
                ip=i[1]
                amount.append(int(ip))
                break
        y=y+1
    plt.title('POPULARITY GRAPH OF "%s" FROM THE YEAR %d TO 2013' %(n_e.get().upper(),int(y_e.get())))
    plt.xlabel('NO. OF CHILDREN')
    plt.ylabel('YEAR')
    plt.plot(year,amount)
    plt.show()
def graph():
    cl=0
    cl2=0
    
    if y_e.get()=='':
        messagebox.showinfo(message='enter a year')
    elif int(y_e.get())<1944 and (y_e.get()>2013):
        messagebox.showinfo(message='year record not present')
    else:
        cl=1
        
    if n_e.get()=='':
        messagebox.showinfo(message='enter the number of names in show')
    else:
        cl2=1

    if cl==1 and cl2==1:
        plot()

def res():
    list_fetch.delete("1.0",END)
    empty=0

root=Tk()
root.resizable(0,0)
a=''
lst_year=[]
lst_count=[]
lst_count2=[]
g=Label(root, text='Gender', font='bold')
variable = StringVar(root)
variable.set("male")
g_o = OptionMenu(root, variable, "male", "female")
y=Label(root, text='Year', font='bold')
y_e=Entry(root)
list_fetch = tkst.ScrolledText(master=root, wrap=WORD, width=50, height=10, font='bold')
s=Label(root, text='Show', font='bold')
s_e=Entry(root)
sub_1=Button(root, text='Submit', command=extract, font='bold')
rst=Button(root, text='RESET', command=res, font='bold')
n=Label(root, text='Name', font='bold')
n_e=Entry(root)
sub_2=Button(root, text='Graph', command=graph, font='bold')

g.grid(row=0, column=0, pady=10, sticky=E)
g_o.grid(row=0, column=1)
y.grid(row=0, column=2, pady=10, sticky=E)
y_e.grid(row=0, column=3, pady=10, padx=20)
s.grid(row=11, column=0, pady=10, sticky=E)
s_e.grid(row=11, column=1, pady=10, padx=20)
sub_1.grid(row=11, column=2, pady=10, padx=10, sticky=E)
rst.grid(row=11, column=3)
list_fetch.grid(row=1, column=0, columnspan=5, rowspan=10)
n.grid(row=12, column=0, pady=20, sticky=E)
n_e.grid(row=12, column=1)
sub_2.grid(row=12, column=2)
