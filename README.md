# 2048-game-Ahza-Bagas-Kenzhi1
Made by Muhammad Muliantafa Ahza, Kinza Bagas Adhistira &amp; Kenzhi Alvaro Gani

import random
import os

# ------ UTILITIES ------
def clear():
    os.system("cls" if os.name == "nt" else "clear")

def print_board(board):
    clear()
    print("\n   2 0 4 8   (W A S D to move)")
    print("----------------------------")
    for row in board:
        print(" ".join([f"{x:4}" if x != 0 else "   ." for x in row]))
    print()

def add_tile(board):
    empty = [(r,c) for r in range(4) for c in range(4) if board[r][c] == 0]
    if empty:
        r, c = random.choice(empty)
        board[r][c] = random.choice([2,2,2,4])

# ------ GAME LOGIC ------
def compress(row):
    row = [x for x in row if x != 0]
    row += [0] * (4 - len(row))
    return row

def merge(row):
    for i in range(3):
        if row[i] == row[i+1] and row[i] != 0:
            row[i] *= 2
            row[i+1] = 0
    return row

def move_left(board):
    new = []
    for row in board:
        r = compress(row)
        r = merge(r)
        r = compress(r)
        new.append(r)
    return new

def move_right(board):
    return [list(reversed(r)) for r in move_left([list(reversed(r)) for r in board])]

def move_up(board):
    rotated = list(map(list, zip(*board)))
    moved = move_left(rotated)
    return list(map(list, zip(*moved)))

def move_down(board):
    rotated = list(map(list, zip(*board)))
    moved = move_right(rotated)
    return list(map(list, zip(*moved)))

# ------ MAIN GAME ------
board = [[0]*4 for _ in range(4)]
add_tile(board)
add_tile(board)

while True:
    print_board(board)
    move = input("Move (W/A/S/D): ").lower()

    if move not in ["w","a","s","d"]:
        continue

    if move == "a":
        new = move_left(board)
    elif move == "d":
        new = move_right(board)
    elif move == "w":
        new = move_up(board)
    elif move == "s":
        new = move_down(board)

    if new != board:
        board = new
        add_tile(board)


python 2048_simple.py

Sorry ko saya cuma buat di web jadi ngga bisa di running jadi saya kasih kode nya aja
