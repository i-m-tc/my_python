# my_python
Python code applications
import tkinter as tk
from tkinter import messagebox
import random

# Initialize the random number and chances
correct_guess = random.randint(1, 10)
chance = 3

def check_guess():
    global chance, correct_guess
    try:
        cust_guess = int(entry_guess.get())
        entry_guess.delete(0, tk.END)
        chance -= 1

        if cust_guess == correct_guess:
            messagebox.showinfo("Result", "Your guess is correct, Congratulations!")
            reset_game()
        else:
            if chance > 0:
                lbl_status.config(text=f"Wrong guess! Try again.")
                lbl_chances.config(text=f"Chances left: {chance}")
            else:
                messagebox.showinfo("Game Over", f"Game Over! Correct answer was: {correct_guess}")
                reset_game()
    except ValueError:
        messagebox.showerror("Error", "Please enter a valid number!")

def reset_game():
    global correct_guess, chance
    correct_guess = random.randint(1, 10)
    chance = 3
    lbl_status.config(text="Guess a number between 1 and 10")
    lbl_chances.config(text=f"Chances left: {chance}")
    entry_guess.delete(0, tk.END)

# ---------------- GUI Design ----------------
root = tk.Tk()
root.title("Number Guessing Game")
root.geometry("400x300")
root.resizable(False, False)

tk.Label(root, text="🎮 Number Guessing Game 🎯", font=('Arial', 14, 'bold')).pack(pady=15)

lbl_status = tk.Label(root, text="Guess a number between 1 and 10", font=('Arial', 12))
lbl_status.pack(pady=5)

lbl_chances = tk.Label(root, text=f"Chances left: {chance}", font=('Arial', 12, 'bold'), fg='red')
lbl_chances.pack(pady=5)

entry_guess = tk.Entry(root, width=10, font=('Arial', 12))
entry_guess.pack(pady=5)

btn_guess = tk.Button(root, text="Submit Guess", command=check_guess, bg="lightgreen", width=15, font=('Arial', 10, 'bold'))
btn_guess.pack(pady=10)

btn_reset = tk.Button(root, text="Reset Game", command=reset_game, bg="lightblue", width=15, font=('Arial', 10, 'bold'))
btn_reset.pack(pady=5)

btn_exit = tk.Button(root, text="Exit", command=root.destroy, bg="salmon", width=15, font=('Arial', 10, 'bold'))
btn_exit.pack(pady=5)

root.mainloop()
