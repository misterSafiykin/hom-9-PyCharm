
import tkinter as tk
import random

score = 0
time_left = 30
game_started = False

root = tk.Tk()
root.title("Лови зірки")
root.geometry("500x450")
root.resizable(False, False)
root.configure(bg="#202040")

title = tk.Label(
    root,
    text="⭐ ЛОВИ ЗІРКИ ⭐",
    font=("Arial", 24, "bold"),
    bg="#202040",
    fg="yellow"
)
title.pack(pady=20)

score_label = tk.Label(
    root,
    text="Очки: 0",
    font=("Arial", 18),
    bg="#202040",
    fg="white"
)
score_label.pack(pady=5)

time_label = tk.Label(
    root,
    text="Час: 30",
    font=("Arial", 16),
    bg="#202040",
    fg="white"
)
time_label.pack(pady=5)

message = tk.Label(
    root,
    text="Натисни СТАРТ, щоб почати!",
    font=("Arial", 12),
    bg="#202040",
    fg="lightblue"
)
message.pack(pady=15)


def start_game():
    global score, time_left, game_started

    if game_started:
        return

    score = 0
    time_left = 30
    game_started = True

    score_label.config(text="Очки: 0")
    time_label.config(text="Час: 30")
    message.config(text="Лови зірки!")
    start_button.config(state="disabled")
    catch_button.config(state="normal")

    countdown()


def catch_star():
    global score

    if game_started:
        points = random.randint(1, 5)
        score += points

        score_label.config(text=f"Очки: {score}")
        message.config(text=f"+{points} очок! ⭐")


def countdown():
    global time_left, game_started

    if time_left > 0 and game_started:
        time_left -= 1
        time_label.config(text=f"Час: {time_left}")
        root.after(1000, countdown)
    else:
        game_started = False
        catch_button.config(state="disabled")
        start_button.config(state="normal")
        message.config(text=f"Гру завершено! Результат: {score}")


start_button = tk.Button(
    root,
    text="СТАРТ",
    font=("Arial", 14, "bold"),
    bg="#4CAF50",
    fg="white",
    width=15,
    command=start_game
)
start_button.pack(pady=10)

catch_button = tk.Button(
    root,
    text="⭐ ЛОВИТИ ЗІРКУ ⭐",
    font=("Arial", 16, "bold"),
    bg="#FFD700",
    fg="#202040",
    width=20,
    height=2,
    state="disabled",
    command=catch_star
)
catch_button.pack(pady=15)

root.mainloop()
