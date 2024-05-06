import tkinter as tk
import random
from tkinter import messagebox

class GuessTheNumberGame:
    def __init__(self, master):
        self.master = master
        self.master.title("Guess The Number")
        
        # Initialize variables
        self.secret_number = random.randint(1, 100)
        self.attempts_left = 10
        
        # Create widgets
        self.label = tk.Label(master, text="Guess the number (between 1 and 100):")
        self.label.pack()
        
        self.entry = tk.Entry(master)
        self.entry.pack()
        
        self.button = tk.Button(master, text="Guess", command=self.check_guess)
        self.button.pack()
        50
        self.info_label = tk.Label(master, text=f"Attempts left: {self.attempts_left}")
        self.info_label.pack()
    
    def check_guess(self):
        guess = int(self.entry.get())
        self.attempts_left -= 1
        
        if guess < self.secret_number:
            messagebox.showinfo("Guess The Number", "Too low! Try again.")
        elif guess > self.secret_number:
            messagebox.showinfo("Guess The Number", "Too high! Try again.")
        else:
            messagebox.showinfo("Guess The Number", "Congratulations! You guessed the number!")
            self.reset_game()
            return
        
        if self.attempts_left == 0:
            messagebox.showinfo("Guess The Number", f"Out of attempts! The number was {self.secret_number}.")
            self.reset_game()
            return
        
        self.info_label.config(text=f"Attempts left: {self.attempts_left}")
        self.entry.delete(0, tk.END)
    
    def reset_game(self):
        self.secret_number = random.randint(1, 100)
        self.attempts_left = 10
        self.info_label.config(text=f"Attempts left: {self.attempts_left}")
        self.entry.delete(0, tk.END)

def main():
    root = tk.Tk()
    game = GuessTheNumberGame(root)
    root.mainloop()

if __name__ == "__main__":
    main()
