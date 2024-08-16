# -GUI_Based_Snake_Gun-Gmae
import tkinter as tk
import random

# Function to get computer's choice
def comp_choice():
    options = ["S", "G", "W"]
    return random.choice(options)

# Function to determine the winner
def game_winner(user, comp):
    if user == comp:
        return "It's a draw!"
    elif (user == 'S' and comp == 'W') or \
         (user == 'W' and comp == 'G') or \
         (user == 'G' and comp == 'S'):
        return "You win!"
    else:
        return "You lose!"

# Function to handle the game play
def play(user_choice):
    comp = comp_choice()
    result = game_winner(user_choice, comp)
    
    # Update images based on computer's choice
    if comp == 'S':
        comp_img_label.config(image=snake_img)
    elif comp == 'W':
        comp_img_label.config(image=water_img)
    else:
        comp_img_label.config(image=gun_img)
    
    result_label.config(text=f"Computer chose: {comp}\n{result}")

# Setting up the GUI
root = tk.Tk()
root.title("Snake-Water-Gun Game")

# Load images
snake_img = tk.PhotoImage(file=" ")
water_img = tk.PhotoImage(file=" ")
gun_img = tk.PhotoImage(file=r" ")


# Creating labels and buttons
instruction_label = tk.Label(root, text="Choose S for Snake, W for Water, G for Gun", font=("Arial", 14))
instruction_label.pack(pady=20)

comp_img_label = tk.Label(root)
comp_img_label.pack(pady=10)

result_label = tk.Label(root, text="", font=("Arial", 16))
result_label.pack(pady=20)

btn_frame = tk.Frame(root)
btn_frame.pack(pady=10)

s_btn = tk.Button(btn_frame, text="Snake", image=snake_img, compound=tk.LEFT, command=lambda: play('S'))
s_btn.grid(row=0, column=0, padx=10)

w_btn = tk.Button(btn_frame, text="Water", image=water_img, compound=tk.LEFT, command=lambda: play('W'))
w_btn.grid(row=0, column=1, padx=10)

g_btn = tk.Button(btn_frame, text="Gun", image=gun_img, compound=tk.LEFT, command=lambda: play('G'))
g_btn.grid(row=0, column=2, padx=10)

# Play Again and Quit Buttons
play_again_btn = tk.Button(root, text="Play Again", command=lambda: [result_label.config(text=""), comp_img_label.config(image='')])
play_again_btn.pack(side=tk.LEFT, padx=20, pady=20)

quit_btn = tk.Button(root, text="Quit", command=root.quit)
quit_btn.pack(side=tk.RIGHT, padx=20, pady=20)

root.mainloop()
