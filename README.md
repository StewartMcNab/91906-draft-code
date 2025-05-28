# 91906-draft-code
#My Math quiz game draft code
#hello world

import random
from tkinter import *

num = [1,2,3,4,5,6,7,8,9]

##!Function##!
#user_entry is the solving entry (solving = entry(app))

def create_error_window(error_message):
    error_window = Toplevel(app)
    error_window.title("Warning")
    error_window.geometry("200x150")
    error_window.resizable(True,True)
    error_window_warning = Label(error_window, text="NO BLANKS!", fg="RED", font=("Terminal", 16))

    error_window_warning.config(text=error_message) 
    error_window_warning.place(relx=0.3, rely=0.1)
    
def input_validator(user_input):

    
    if user_input == "":
        print("user input is blank")
        create_error_window("No Blanks")
# Alphabet, Whitespace, And Symbols
    elif user_input.isdigit() == False:
        if user_input.isalnum() == True:
            print("Alphabet detected")
            create_error_window("No Letters")
        elif " " in user_input:
            print("Whitespace detected")
            create_error_window("No Whitespace")
        else:
            print("Symbols detected")
            create_error_window("No Symbols")

        #boundaries
    elif len(user_input) > 6:
        print("number limit is 6!")
        create_error_window("6 Numbers Max")
    else:
        return True
    return False

        

def submt(user_entry):
    #invalid entries
    
    user_input = user_entry.get()

    validity = input_validator(user_input)
    if validity == True:
        if user_input == str(resultPLUS()):
            correct = Label(app, text="correct!", fg="green", font=("Terminal", 16))
            correct.place(relx=0.3, rely=0.2)
        else:
            wrong = Label(app, text="wrong!", fg="red", font=("Terminal", 16))
            wrong.place(relx=0.3, rely=0.2)
#
def try_again():
    try_again.num1update = random.choice(num)
    try_again.num2update = random.choice(num)
    question = Label(
        app, text=f"{try_again.num1update}+{try_again.num2update}", font=("Courier")
    )
    question.place(relx=0.16, rely=0.14, relwidth=0.7, relheight=0.23)

def resultPLUS():
    try_again

    return try_again.num1update + try_again.num2update


def save_input():
    with open ("answers.txt","a") as file:
        file.write("Answers: "f"{str(resultPLUS())}")
####!

app = Tk()
app.title("MathsGame")
app.geometry("250x300")
app.resizable(True,True)
#ajusting the window size and usability

start = Button(app, text="Start Game", bg = "yellow", fg = "red", command=try_again)
start.place(relx=0.35, rely=0.2)

solving  = Entry(app)
solving.place(relx=0.35, rely=0.4, relwidth=0.34, relheight=0.23)

submit = Button(app, text="Submit", bg = "lightblue", fg = "darkblue", command=lambda: [submt(solving), save_input()])
submit.place(relx=0.35, rely=0.64, relwidth=0.34, relheight=0.23)

try_again = Button(app, text="Try Again", bg = "lightgreen", fg = "darkgreen", command=try_again)
try_again.place(relx=0.39, rely=0.9)
app.mainloop
