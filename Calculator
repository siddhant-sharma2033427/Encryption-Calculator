import tkinter as tk
from tkinter import ttk
from os import path
import os
#importing pySedCrypt API
import pyAesCrypt
from tkinter import messagebox
from tkinter import filedialog


#Function for creating check buttion for for all the file inside cache folder
# creating function not class to get rid of "no object nake tk" error
def creating_labels(frame):
    #global variable for independent use
        global radiolist
        #checking if current directory is cache or not
        #if not then chenge it to cache
        if "cache" not in os.getcwd().split(r"\ ".replace(" ", "")):
            #function for changing current witing directory
            os.chdir(os.getcwd() + r"\cache")
        dirlist  = os.listdir()
        
        radiolist = {}
        #creating check buttion for all files inside cache folder
        for i in dirlist:
            radiolist[i] = tk.IntVar()
            check_button = ttk.Checkbutton(frame,text = i,variable = radiolist[i])
            check_button.grid(sticky="w")
#class for recreating label if any update made in cache folder
class refresh:
    def refresh_label(self,label):
        for child in label.winfo_children():
            child.destroy()
        #calling creating_labels function for creating check button because sone changes are made
        
        creating_labels(label)
#Creating class for delete elements from cache foler
class delete:
    def delete_file(self,label):
        global radiolist
        #list comprehension for creating list containg names of the file which user selected
        #from toplevel window 
        
        del_list = [item for item,val in radiolist.items() if val.get() == 1]
        
        
        #Question box for conformation
        choice = messagebox.askquestion("Delete File","Are you sure want to delete this file?")
        #getting name of all file which user selected to delete
        #all names are stored in del_list list
        for item in del_list:
            #if user selected yes then delete else dont do any thing
            if choice == "yes":
                
                os.remove(item)
        del_list = []
        #calling refresh function because some changes are made in cashe folder
        re = refresh()
        re.refresh_label(label)
class encrypted_files:
    def encrypt_file(self,label):
        #asing user to select single or multiple file encryption
        paths =  filedialog.askopenfilenames()
        for item in paths:
            #cresting buffer 
            bufferSize = 64 * 1024
            #storing user password to a variable
            password = st
            # encrypting using pyAesCrypt API
            pyAesCrypt.encryptFile(item,path.basename(item) + ".aes", password, bufferSize)
            #removing file from its original path
            os.remove(item)
        re = refresh()
        re.refresh_label(label)
#creating class for decrypting data
class decrypt_folder:
    def decrypt(self,label):
        global radiolist
        #list comprehension for storing all file name which user selected from toplevel window
        dec_list = [item for item,val in radiolist.items() if val.get() == 1]
        #asking user to select file to save decrpted file
        save_as = filedialog.askdirectory()
        
        for file in dec_list:
            bufferSize = 64 * 1024
            password = st
            # decrypting file using pyAesCrypt API
            pyAesCrypt.decryptFile(file, save_as + r"/" + file.replace(".aes",""), password, bufferSize)
            #removing file from cache folder
            os.remove(file)
        re = refresh()
        re.refresh_label(label)
class encrypt_folder:
    def open_folder(self):
        #getting current writing directory for checking wether Module and chache filder exist
        path =  os.getcwd().split(r"\ ".replace(" ",""))
        #if Module exist do noting else create folder
        if "Modules" in path:
            try:
                os.chdir("..")
                os.mkdir(os.getcwd() + r"\cache")
                os.chdir(os.getcwd() + r"\cache")
            except:
                pass
        else:
            #if cache folder exist do nothing else create folder
            try:
                os.mkdir(os.getcwd() + r"\cache")
                os.chdir(os.getcwd() + r"\cache")
            except:
                pass
        #creating toplevel window for creating buttion and labels and printing all encrypted data
        top_level = tk.Toplevel()
        top_level.geometry("700x500+500+200")
        top_level.title("Encyption Files")
        #creating objects for various classes
        p2 = encrypted_files()
        dec = decrypt_folder()
        dele = delete()
        #label frame for tool bar (upload,decrypt and delete buttion)
        tool_bar = ttk.LabelFrame(top_level)
        tool_bar.pack(side = "top",fill = "both")
        #label frame for check box 
        main_body = ttk.LabelFrame(top_level)
        main_body.pack(side = "top",fill = "both")
        #crating upload button
        upload_button = ttk.Button(tool_bar,text = "Upload file",command = lambda :p2.encrypt_file(main_body))
        upload_button.grid(row = 0,column = 0)
        #creating decrypt button
        decrypt_button = ttk.Button(tool_bar,text = "Decrypt",command = lambda : dec.decrypt(main_body))
        decrypt_button.grid(row = 0,column = 1)
        #creating delete buttion
        delete_button = ttk.Button(tool_bar,text = "Delete",command = lambda :dele.delete_file(main_body))
        delete_button.grid(row = 0,column = 2)
        #calling creating_labels for adding labels to toplevel window when toplevel window first created
        creating_labels(main_body)
        top_level.mainloop()
class writng_passward:
    def writing(self,val,button):
        global st
        #creating Module folder if it is not exist 
        try:
            os.mkdir(os.getcwd() + r"\Modules")
        except:
            pass
        #changing current writing directory to Module
        try:
            os.chdir(os.getcwd() + r"\Modules")
        except:
            pass
        #importing from entry box to val variable
        val = val.get()
        # rules for creating password:
        #1. should be atleast 10 digit
        #2.should not contail and alphabet of other symbol
        #here checking whether length of password is more than equal to 10 
        if len(val) >= 10:
            #Checking wether password contaning only digits or not
            if all([True if i in ["0","1","2","3","4","5","6","7","8","9"] else False for i in val]):
                label = ttk.Label(button,text = "passward created you can close window").grid(row = 4,column = 0)
                st = val
                #writing password to module.txt file after performing xor by 5
                #adding " " so that passward does not mix up in txt file
                with open("module.txt","w") as fp:
                    for i in val:
                        fp.write(str(int(i) ^ 5)+ " ")
                    fp.close()
            else:
                #if any rule for not followed during creation of password then show message box
                messagebox.showerror("Wrong","1.create 10 digit passward\n2. only number are allowed 1")
        else:
            #if any rule for not followed during creation of password then show message box
            messagebox.showerror("Wrong","1.create atleast 10 digit passward\n2. only number are allowed 2")
class passward:
    def enter_passward(self):
        #creating toplevel window for input password
        pass_input = tk.Toplevel()
        pass_input.geometry("450x250+500+200")
        pass_input.title("enter passward")
        pass_input.resizable(0,0)
        
        label_frame = ttk.LabelFrame(pass_input)
        label_frame.pack()
        
        #create password label
        pass_label = ttk.Label(label_frame,text = "Create new passward").grid(row = 0,column = 0)
        
        #label printing rules for creating password
        condition = ttk.Label(label_frame,text = "1.Create atleast  10 digit passward\n2.Only numbers are allowed")
        condition.grid(row = 3,column = 0)
        
        #Entry box to input password
        pass_text = ttk.Entry(label_frame,width = 30)
        pass_text.grid(row = 1,column =1)
        
        #creating writing password object
        obj = writng_passward()
        
        #calling writing password function from create buttion to creating and storying password
        enter_button = ttk.Button(label_frame,text = "Create",command = lambda : obj.writing(pass_text,label_frame)).grid(row = 2,column = 1)
        
        pass_input.mainloop()

class first_class:
    def ispresent(self):
        global st
        st = ""
        #checking wether Module folder and module folder exist or not
        #if they are not exist it means software runned first time
        if path.isdir(r"Modules"):
            if path.isfile(r"Modules\module.txt"):
                with open(r"Modules\module.txt","r") as fp:
                    #spliting to nemove " " from passward
                    temp = fp.read().split(" ")
                    for i in temp:
                        try:
                            #perfoming xor gate to decrypt  password
                            st += str(int(i) ^ 5)
                            
                        except:
                            pass
            else:
                #if folder does not exist then create them and create new password
                obj = passward()
                obj.enter_passward()
        else:
            obj = passward()
            obj.enter_passward()
root = tk.Tk()
root.geometry('250x350')
root.title('Calculator')
root.resizable(0,0)
# adding icon to software
#root.wm_iconbitmap("cal.ico")

class function:
    def comm(self,value,entry):
        #adding newly clicked number to entrybox
        entry.insert(tk.END,value)
    def show_result(self,entry):
        data = entry.get()
        # if entered value to entry box is password then store true to bollean else store false
        try:
            boolean =  all([True if data[i] == st[i] else False for i in range(0,len(st)-1)])
        except:
            boolean = False
        #if true stored in boolean then open toplevel window else show methimatical calculation on entry box
        if(boolean == True):
            obj = encrypt_folder()
            obj.open_folder()
        else:
            total = eval(data)
            entry.delete("0",tk.END)
            entry.insert("0",total)
            
class clear:
    def clear_text(self,entry):
        entry.delete("0",tk.END)
class Calculator_front:
    def __init__(self,root):
        self.root = root
        ## making label frame for displaying user entered values
        self.label_frame = ttk.LabelFrame(self.root)
        self.label_frame.pack(side = "top",fill = "both")
        ## Making entry box
        self.calculator_var = tk.StringVar(self.label_frame)
        self.entrybox = tk.Entry(self.label_frame,width = 40,justify = "right",textvariable = self.calculator_var)
        self.entrybox.pack(side = "top",fill = "both",ipady = 5)
        ## second label frame for buttons
        self.label_frame2 = ttk.LabelFrame(self.root)
        self.label_frame2.pack(side = "top",fill = "both")
        
        p1 = function()
        cl = clear()
        
        #number, methimatical symbols and other buttons
        self.clear_image = tk.PhotoImage(file = r"icon\clear2.png")
        self.clear_button = ttk.Button(self.label_frame2,image = self.clear_image,command = lambda : cl.clear_text(self.entrybox))
        self.clear_button.grid(row = 0,column = 3)
        
        self.number7_image = tk.PhotoImage(file = r"icon\seven.png")
        self.number7_button = ttk.Button(self.label_frame2,image = self.number7_image,command = lambda : p1.comm("7",self.entrybox))
        self.number7_button.grid(row = 1,column = 0)
        
        self.number8_image = tk.PhotoImage(file = r"icon\eight.png")
        self.number8_button = ttk.Button(self.label_frame2,image = self.number8_image,command = lambda : p1.comm("8",self.entrybox))
        self.number8_button.grid(row = 1,column = 1)
        
        self.number9_image = tk.PhotoImage(file = r"icon\nine.png")
        self.number9_button = ttk.Button(self.label_frame2,image = self.number9_image,command = lambda : p1.comm("9",self.entrybox))
        self.number9_button.grid(row = 1,column = 2)
        
        self.div_image = tk.PhotoImage(file = r"icon\div.png")
        self.div_button = ttk.Button(self.label_frame2,image = self.div_image,command = lambda : p1.comm(r"/",self.entrybox))
        self.div_button.grid(row = 1,column = 3)
        
        self.number4_image = tk.PhotoImage(file = r"icon\four.png")
        self.number4_button = ttk.Button(self.label_frame2,image = self.number4_image,command = lambda : p1.comm("4",self.entrybox))
        self.number4_button.grid(row = 2,column = 0)
        
        self.number5_image = tk.PhotoImage(file = r"icon\five.png")
        self.number5_button = ttk.Button(self.label_frame2,image = self.number5_image,command = lambda : p1.comm("5",self.entrybox))
        self.number5_button.grid(row = 2,column = 1)
        
        self.number6_image = tk.PhotoImage(file = r"icon\six.png")
        self.number6_button = ttk.Button(self.label_frame2,image = self.number6_image,command = lambda : p1.comm("6",self.entrybox))
        self.number6_button.grid(row = 2,column = 2)
        
        self.multi_image = tk.PhotoImage(file = r"icon\multi.png")
        self.multi_button = ttk.Button(self.label_frame2,image = self.multi_image,command = lambda : p1.comm("*",self.entrybox))
        self.multi_button.grid(row = 2,column = 3)
        
        self.number1_image = tk.PhotoImage(file = r"icon\one.png")
        self.number1_button = ttk.Button(self.label_frame2,image = self.number1_image,command = lambda : p1.comm("1",self.entrybox))
        self.number1_button.grid(row = 3,column = 0)
        
        self.number2_image = tk.PhotoImage(file = r"icon\two.png")
        self.number2_button = ttk.Button(self.label_frame2,image = self.number2_image,command = lambda : p1.comm("2",self.entrybox))
        self.number2_button.grid(row = 3,column = 1)
        
        self.number3_image = tk.PhotoImage(file = r"icon\three.png")
        self.number3_button = ttk.Button(self.label_frame2,image = self.number3_image,command = lambda : p1.comm("3",self.entrybox))
        self.number3_button.grid(row = 3,column = 2)
        
        self.minus_image = tk.PhotoImage(file = r"icon\minus.png")
        self.minus_button = ttk.Button(self.label_frame2,image = self.minus_image,command = lambda : p1.comm("-",self.entrybox))
        self.minus_button.grid(row = 3,column = 3)
        
        self.dot_image = tk.PhotoImage(file = r"icon\dot.png")
        self.dot_button = ttk.Button(self.label_frame2,image = self.dot_image,command = lambda : p1.comm(".",self.entrybox))
        self.dot_button.grid(row = 4,column = 0)
        
        self.number0_image = tk.PhotoImage(file = r"icon\zero.png")
        self.number0_button = ttk.Button(self.label_frame2,image = self.number0_image,command = lambda : p1.comm("0",self.entrybox))
        self.number0_button.grid(row = 4,column = 1)
        
        self.plus_image = tk.PhotoImage(file = r"icon\plus.png")
        self.plus_button = ttk.Button(self.label_frame2,image = self.plus_image,command = lambda : p1.comm("+",self.entrybox))
        self.plus_button.grid(row = 4,column = 3)
        
        self.isequal_image = tk.PhotoImage(file = r"icon\isequal.png")
        self.isequal_button = ttk.Button(self.label_frame2,image = self.isequal_image,command = lambda : p1.show_result(self.entrybox))
        self.isequal_button.grid(row = 4,column = 2)
#calling main classes

st = ""
radiolist = {}
button_dict = []
root_obj = Calculator_front(root)
se = first_class()
se.ispresent()
root.mainloop()
